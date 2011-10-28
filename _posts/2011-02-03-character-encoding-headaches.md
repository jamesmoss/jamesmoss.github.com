--- 
layout: post
title: Character encoding headaches
published: true
meta: 
  dsq_thread_id: "415578394"
  _edit_last: "1"
  _wp_old_slug: ""
tags: 
- encoding
- mysql
- php
- Snippets
- utf8
type: post
status: publish
---
I recently worked on a project with a strange character encoding issue.
The application in question was an old CMS system which had originally
been developed using a Latin–1 character set both for storing it’s data
and in regards to the pages being served by Apache. More recently it had
been updated to use UTF8 to eliminate lots of encoding problems which
were arising, especially as more non English speaking users started to
utilise the system. 

There was however an odd issue occurring; the
database and it’s tables had been setup correctly to store everything as
UTF8; PHP and Apache had been configured to correctly serve UTF8 content
and the application itself had been updated to use PHP’s set of [mb\_
string functions][]. However when I viewed the database using
[Navicat][] it still looked like the data was being stored as Latin–1.

After a bit of digging I discovered that when the connection to the
database was being made, [mysql\_set\_charset()][] wasnt being called
which meant PHP was defaulting to Latin–1. I fixed this but in doing so,
Latin–1 characters were being displayed as UTF8, and everything ended up
looking like a mess. I set about writing a script to fix the data in
MySQL and came across this great snippet on [stackoverflow][]:

    UPDATE table SET col = CONVERT(CONVERT(CONVERT(col USING latin1) USING binary) using utf8);

I wrote a quick PHP script which iterated over the database ran this
query on any text, varchar or char columns and the problem was solved.
There are other ways to achieve the same effect which involve dumping
the database without any encoding information and then re-importing it,
specifying UTF8 but I prefer this approach. As a word of warning,
remember to backup any databases before running this. Also be aware if
you have a lot of data it could take some time.

  [mb\_ string functions]: http://php.net/manual/en/book.mbstring.php
  [Navicat]: http://navicat.com/
  [mysql\_set\_charset()]: http://php.net/manual/en/function.mysql-set-charset.php
  [stackoverflow]: http://stackoverflow.com/questions/3175929/inserting-latin1-encoded-text-into-utf8-tables-forgot-to-use-mysql-set-charset