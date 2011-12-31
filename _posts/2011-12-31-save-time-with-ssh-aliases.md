---
title: Save time with SSH aliases
layout: post
---

If you're a developer you probably find yourself connecting to servers over ssh several times each day. Remembering the server address, port, user and password can be hard sometimes. You might find yourself needing to use the following to get into a server:

    $ ssh -p 3241 james@somehost-532242.long.example.org

Then you have to remember (or maybe even lookup) the password.  It's pretty tedious and time consuming. You could create a bash alias for each server but it's not ideal; there's a better way.

## ~/.ssh/config

Within this file you can define the hostname, user and port of a server and associate it to a short name like `mainserver`.

The syntax us fairly straightforward, here's an alias based on the previous example.

    host mainserver
      hostname somehost-532242.long.example.org
      user james
      port 3241

Now if you want to connect, you just need to type:

    $ ssh mainserver

Much easier to remember. As an added bonus, `scp` also observes the alias so transferring files is now pretty simple.

    # transfers access.log from the server to the current directory
    $ scp mainserver:/var/log/access.log .

## ssh-host-aliases

I've put together a ruby script which makes it easy to add, delete and list the aliases in `~/.ssh/config`.

Installation is simple:

    $ git clone git://github.com/jamesmoss/ssh-host-aliases.git
    $ cd ssh-host-aliases
    $ chmod +x .

To add a host run `./new-ssh-alias.rb` and follow the prompts. The script also takes care of transferring your public key to the server so you won't have to re-enter your password every time you connect.

If you want to remove an alias use `./delete-ssh-alias.rb` and follow the prompts. `./list-ssh-aliases.rb` will print a list of every alias you've got setup.

The code is up on [github](https://github.com/jamesmoss/ssh-host-aliases) if you want to fork or send a pull request. This is my first proper ruby project, so go easy on me.