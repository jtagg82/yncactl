# yncactl
Script to control a Yamaha AVR from the command line

I created this python script to control my Yamaha RX-V475 from my computer.
Initially it was just a way to change the volume, but what I really wanted, was a way to remote control it to play music from my NAS.

Usage:

ynca [options] command [cmd args]
Options:
     -h  --help          print this message
     -d  --debug         print debug strings
     -v  --verbose       print more detailed output
     -a  --address       hostname of the AVR
     -p  --port          TCP port. Def. 50000
Commands:
commands without any arguments will typically return the current state
     power [ on | off | toggle ]
                         power AVR on or off
     vol[ume] [ up | down | <value> | mute ]
                         read or modify volume
     scene [<scene #>]
                         select scene
     input [<input>]
                         return or select current input
     sound-program [<program>]
                         return or select sound program
     list <subunit>      name of the subunit to list
     list-inputs         lists all possible inputs
     list-programs       lists all possible programs
     device-info         print AVR model name and version
     next                skip to next song
     prev                skip to previous song
     pause               pause playback
     play                start playback
     stop                stop playback
     songinfo            print information on currently playing song
     raw                 send raw YNCA command
     ir-code             send ir-code of remote button
     list <subunit> [#]  lists all items for the subunit specified
                         adding a number selects item number # instead of listin

The bash script is for integrating the list function with dmenu and allows navigation of the AVR lists for the NAS server.
