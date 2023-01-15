# Vibeboard

## Overview

Vibeboard is a JavaScript-based, customizable soundboard application which
interfaces with [Buttplug.io](https://buttplug.io) to activate Bluetooth-
enabled vibrators in conjunction with sounds. Intended to be use in conjunction
with headphones, it could be used as a conditioning tool or in remote-control
fantasies.

## Installation
Regardless of whether you intend to use Vibeboard on a computer or a mobile
device, download and install [Intiface Central](https://intiface.com/central)
on the device on which you intend to access Vibeboard.

### For Desktop
Download Vibeboard from GitHub and open `vibeboard.html` in a Chrome-based
browser such as [Google Chrome](https://google.com/chrome) or [Microsoft Edge] (https://microsoft.com/edge/download).

### For Mobile
To use Vibeboard on a mobile device, you will need both a mobile device and a 
Windows, Linux or Mac computer on the same WiFi network. Vibeboard could 
conceivably be deployed on an Internet-accessible server, but the necessary 
security configuration to do so is beyond the scope of this README at this 
time. To access Vibeboard on a mobile device, first download Vibeboard to 
your computer. You will then need a web server which can serve vibeboard.html 
up for your mobile device's browser. The easiest way to do this is to use 
[Python's](https://python.org) http.server module. Linux and Mac computers 
should have Python installed.  On a Windows device, you can either 
[download](https://www.python.org/downloads/) it from Python.org, or via 
the Microsoft App store. Once Python is installed, open
your preferred command shell, `cd` into the Vibeboard directory, and start the
server by executing `python3 -m http.server`. Find your computer's IP address
(`ipconfig` on Windows, `ip addr` on Linux or `ipconfig ifaddr en1` on Mac).
On your mobile device, open Chrome, and go to 
`http://<your IP address>:8000/vibeboard.html`. You should now see Vibeboard.

## Usage
Start Intiface Central on the device on which you will be using vibeboard.
Be sure to press the `play` button at the top of the window to actually start
the Buttplug server. Note the server address, likely `null:12345`.
Power on whatever toy or toys you'd like to use with Vibeboard.
Access `vibeboard.html` as described in the Installation section above.
In Vibeboard, set the Intiface address to the address shown in Intiface 
Central. If the address is `null:12345`, use `ws://127.0.0.1:12345`, which is
the default IP.

Press `Connect` and `Scan`. After a moment, Vibeboard will populate with the 
devices identified by Intiface. Press the `Stop Scan` button once all devices
have been identified. Note: Vibeboard currently will not pick up devices that
are already associated with Intiface Central when Vibeboard connects. If you 
need to disconnect Vibeboard from Intiface, you will need to reload the
Vibeboard page, then stop and start the Buttplug server by pressing the big 
blue button at the top of the Intiface window. You do not need to power-cycle 
your toys, they will not reassociate with Intiface until you start a scan from 
Vibeboard. Handling this more gracefully is on my to-do list.

The remainder of the controls are fairly self explanatory. You can select a
background sound, set its volume, set it to play once or loop; you can set
the vibration intensity for a vibrator, stop and start it. The main 
functionality is in the clips section, where you can for each configured clip,
set the clip's volumne, select which vibrator you want to activate when that 
clip is played, and set the intensity for the vibrator. The vibrator will 
activate for one second when the clip finishes playing.

## Configuration
Vibeboard ships with three innocuous sound clips, but is intended to be used
with clips you choose or create yourself. To make Vibeboard use your clips,
place your clips into the `vibeboard/sounds/clips/` directory, then find the
following chunk of code in vibeboard.html
```
	var clipSounds = [["./sounds/clips/chirp.mp3","Chirp", "clip:0"],
	["./sounds/clips/drum.mp3", "Drum", "clip:1"],
	["./sounds/clips/hawk.mp3", "Hawk", "clip:2"]];
```

Using the existing code as a template replace the existing sounds. Each entry
in the sounds array consists of a three parts: the path to the file, the label
for the clip which will be displayed in Vibeboard, an then a tag, consisting of
"clip:N", where N is the number of the clip in the list of clips. Vibeboard
will read the array when it executes, and automatically populate the page with
the clips and their controls.

Similarly, you can replace the background sounds, by placing the sounds into
the `vibeboard/sounds/background/` directory, and editing the following bit of
code:
```
var backgroundSounds = [["./sounds/background/white-noise.mp3", "White Noise"],
	["./sounds/background/pink-noise.mp3", "Pink Noise"],
	["./sounds/background/binaural-204Hz.mp3", "Binaural 204Hz"],
	["./sounds/background/binaural-154Hz.mp3", "Binaural 154Hz"]];
```
The background sound entries consist of only two parts, the file path, and the 
display name. Background sounds should either be long, or loopable.


## To-Do
+ Write a configuration tool capable of importing sounds and filling out the `backgroundSounds` and `clipSounds` arrays
+ Add the ability to create vibration patterns which can be executed on demand
+ Add a floating intensity control usable for more interactive direct use of the vibrators
+ Add the ability to define for how long a vibrator activates after a given clip is played
+ Improve the UI
