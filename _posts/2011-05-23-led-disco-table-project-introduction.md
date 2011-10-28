--- 
layout: post
title: LED Disco Table Project - Introduction
published: true
meta: 
  dsq_thread_id: "404303995"
  _edit_last: "1"
tags: 
- arduino
- disco table
- Electronics
- leds
- Projects
- rainbowduino
type: post
status: publish
---
I’ve always got a side project on the go, I enjoy doing something a bit
different from my usual day job and working with electronics (especially
LEDs) can be pretty interesting. Back in 2004, Daft Punk designed a
coffee table for Habitat which featured a 5x5 grid of red LEDs mounted
under smoked glass which would light up and animate in time with an
external music source. I always wanted one of these but could never
afford it. Fast forward to 2009 and a few people started building 8x8
LED matrix coffee tables. These featured 64 RGB LEDs arranged in a 8 by
8 pattern which would animate and generally look awesome. Soon after
that people started adding touch sensing capabilities to tables to
enable some cool interactive effects. I want to draw from all these
projects and build my own ultimate LED coffee table. 

Here’s a little
spec I put together:

1.  8x8 RGB LED matrix to display simple animations, effects (e.g plasma
    demo).
2.  Synced to external music source.
3.  Multitouch capable.
4.  Gesture-based interface.
5.  Completely standalone operation - Table doesn’t need to be plugged
    into a PC. The only wire connected will be the power supply.
6.  Remote control via iPhone over WiFi.\*

*\* This last feature depends on how much time I have free to program
it.*

## Getting started

![image][]

The base of the table will be formed out of an Ikea
Magiker coffee table.These haven’t been on sale for the past few years
but my old flatmate generously donated his for the project. They are
almost the perfect size (75cm x 75xm x 45cm) but I’m still going to be
making some modifications. The two open ends will be boarded up to stop
light leakage and then the sides clad in clear 6mm Perspex. The Perspex
will have a white vinyl backing on the inside giving it a similar effect
to the first generation iPod Nano and Nintendo DS Lite. Inside the table
I’m constructing a 8x8 grid out of 1mm PVC foamboard to divide up each
LED and form what I’m calling a “cell”. I’ll probably replace the
original glass top which has a frosted border with some low iron clear
stuff which doesn’t have that usual green tint you get with glass. Where
the glass sits on the wood I’m going to add a white rubber strip to form
a (fairly) watertight seal, just in case a drink gets knocked over on
top, I don’t want it seeping down into the electronics. The final
element is the diffusion film to even out the LEDs, I’ve found some
white frosted self adhesive film which works a treat.

## Driving the LEDs

In a RGB LED matrix, each LED is actually three combined in a single
package, this means that in a 8x8 matrix there’s 192 LEDs to drive.
Rather than trying to power all LEDs at once with some crazy power
hungry LED driver, I’ll instead be using a multiplexing approach. This
technique involves only lighting one column at a time, by switching very
quickly between the columns your brain perceives that they are
constantly on due to persistence of vision. I’ll be using a Rainbowduino
to drive the LED array, being controlled by the main Arduino over I2C.
Each cell will have three 10mm diffused RGB LEDs. The cheap Chinese LEDs
which I’ve purchased, although bright, aren’t particularly high quality
and the colour varies slightly between each one. By using three in a
cell running at a slightly lower power I’m hoping to even out this
problem (even though it means a load more soldering). It also evens out
the light spread so there’s no bright spots on the diffusion film.

## Touch sensitivity

A capacitive or resistive panel on this scale would be too expensive for
my budget so I’ve decided to go for a low tech optical solution
involving infrared light. Each cell will have a IR LED and a matching IR
photodiode. The LED will fire infrared light up out of the cell, if
something is placed above it (a hand / cup / face), the IR light is
bounced back and detected by the photodiode. At least that’s how it
should work in theory. I’m expecting lot of problems with crosstalk
(where adjacent cells are detecting their neighbours reflected light),
reduced IR emission (due to the light diffusion film on the bottom of
the glass) and interference from ambient lighting. 

Each photodiode would
will need to be connected to an analog pin on the Arduino to take a
reading. Since the the Arduino doesn’t have 64 analog inputs I’ll be
using an eight channel demultiplexer and an eight channel multiplexer to
achieve this. The multiplexer supply power to one column at a time via a
transistor. The demultiplexer will be connected to the photodiodes on
each row. Working much like the LEDs, only one column is on at a time.
This allows the demux to read each row individually, the next column is
lit up and another reading taken. This happens over and over, scanning
the entire table around 20 times a second.

## Syncing to music

They key to syncing lights to music is beat detection. A kick drum
(which in most dance music sounds on the beat) is in the 60–120hz
frequency area, by using a filter it’s possible to pull out just that
frequency from an audio source and then do something when it happens. I
spent a bit of time looking into active and passive low pass filters and
beat detection and it turns out it’s a lot harder than first appears.
Luckily I came across the MSGEQ7 chip; it takes a line level input and
reports back the amplitude of seven different frequency bands. It has a
built in demultiplexer so it only takes up 3 pins on the Arduino. One of
the bands is 63hz which means I can do the beat detection very easily.
Another positive about this approach is that I can include a graphic
equaliser animation mode without needing to plug the table into a PC
running a Processing sketch. I’ve bought a little pre-built board with
an electret mic, built in pre-amp and gain control to feed into the
MSGEQ7. 

This post summarises where I’m at with the initial design of the
Disco Table. I’ve started ordering parts in for the construction
process. My next post will outline my progress on modifying the Ikea
table and some prototype circuits I’ve built on a breadboard.

  [image]: http://jamesmoss.co.uk/wp-content/uploads/2011/05/45352442-300x224.jpg "Magiker Coffee Table"