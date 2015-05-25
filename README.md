# yncactl
Script to control a Yamaha AVR from the command line

I created this python script to control my Yamaha RX-V475 from my computer.
Initially it was just a way to change the volume, but what I really wanted, was a way to remote control it to play music from my NAS.

### Install

Make sure to copy the configuration file to ~/.config/ynca.conf. Without this, it will not know how to contact the AVR nor which features are available.

### Usage

     ynca [options] command [cmd args]

**Options:**
```
     -h  --help          print this message
     -d  --debug         print debug strings
     -v  --verbose       print more detailed output
     -a  --address       hostname of the AVR
     -p  --port          TCP port. Def. 50000
     -n  --no-cache      disables the list cache
```

**Commands:**

commands without any arguments will typically return the current state
```
     power [ on | off | toggle ]
                         power AVR on or off
     vol[ume] [ up | down | <value> | mute ]
                         read or modify volume
     scene <scene #>     select scene
     input [<input>]     return active or select input
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
     raw <command>       send raw YNCA command
     ir-code <code>      send ir-code of remote button
     list <subunit> [#]  lists all items for the subunit specified
                         adding a number selects item number # instead of listing
```

The list function is meant to be used with scripting. It is quite slow as all operations will be duplicated on the AVR as it navigates the lists. Specify the subunit of the AVR you want to create the list from. Subunits include 'server' and 'netradio' and will allow you to browse these lists to remotely control the AVR.

Example of list usage:

```
     $ yncactl list netradio
     NET RADIO
     0 Back
     1 Bookmarks
     2 Locations
     3 Genres
     4 New Stations
     5 Popular Stations
     6 Podcasts
     7 Help
     $ yncactl list netradio 3
     $ yncactl list netradio
     0 Back
     [lists all genres]
     ...
```
   
### ynchoose  
The script _ynchoose_ integrates these list calls into dmenu so you can navigate them easily.

### config     
Since all Yamaha AVRs don't have the same functions, you need to edit your configuration file to reflect that. I have only tested this on a RX-V475, but it should be quite easy to make it work with most other Yamaha AVRs of the same series.

### caching
Since the AVR is slow at navigating and returning lists, yncactl caches various lists to speed things up. When a cache exists, it doesn't need to navigate through a whole list just to determine what the items are. If you do not want to use the cache, use the -n or --no-cache option when calling yncactl. The cache will be created in ~/.cache/yncactl. 
Each file in there represents a list. The hit mechanism is rudimentary and should work for most standard cases, but it is definitely not complete. If you are having problems with the cache, just delete the contents of the folder.
It considers a cache file a hit if the name corresponds to the depth of the list followed by the list name and if the contents have the same number of items.
