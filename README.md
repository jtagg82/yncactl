# yncactl
Script to control a Yamaha AVR from the command line

I created this python script to control my Yamaha RX-V475 from my computer.
Initially it was just a way to change the volume, but what I really wanted, was a way to remote control it to play music from my NAS.

Usage:

yncactl vol           up, down, mute, xx
yncactl power         on, off, toggle
yncactl input         input-name
yncactl program       audio-program-name
yncactl list-inputs   lists all inputs
yncactl list-programs lists all audio programs
yncactl list          server, netradio

The bash script is for integrating the list function with dmenu and allows navigation of the AVR lists for the NAS server.
