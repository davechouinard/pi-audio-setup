# pi-audio-setup

Simple audio server setup to play local high quality audio files.

This project was created to free up my laptop from always being connected to the stereo to play music.

Since the digital-to-analog converter on the raspberry pi is likely low quality we'll use a dedicated 
USB DAC to do that conversion. If you wanted to spend more and don't mind the extra cable,
a DAC with a dedicated power supply would likely be even better.

```
Plug the usb hub into a power outlet to power it.
Plug a mini usb cable from the pi power connector to the usb hub to power the pi.
Plug the computer usb cable from the usb hub into an open usb port on the pi 
so the pi can communicate with devices plugged into the usb hub.
Plug the usb cable on the dac into the usb hub.
Plug a usb music drive into the usb hub.
Plug the rca outputs on the dac into rca inputs on the amp.

+-----------+    +-----------+
|           |    |           |   +-------------+
|           +---->           <---+  usb drive  |
|   pi      |    |           |   +-------------+
|           <----+           |
|           |    |  powered  |
+-----------+    |  usb hub  |
+-----------+    |           |
|           |    |           |
|           |    |           |
|   dac     +---->           |
|           |    |           |
|           |    |           |
+-----+-----+    +-----------+
      |
      |
+-----v-----+    +-----------+
|           +---->  speaker  |
|           |    +-----------+
|    amp    |
|           |    +-----------+
|           +---->  speaker  |
+-----------+    +-----------+
```

## Setup
Assumes NOOBS or other Debian based OS is running on the pi and a static IP has been assigned.
```
alsamixer
# F6->Select USB DAC->(Make sure not muted, press 'm')->ESC

sudo apt-get update 
sudo apt-get install vlc
vlc &
```

Set a password for the web interface:
`Tools->Preferences (select "All" radio button)->Interface->Main interfaces->Lua` Set a password and 'Save'.

Set audio output to the correct output device:

`Tools->Preferences->Audio`: select "All" radio button

`Output modules->Audio output module:` ALSA audio output

`Output modules->ALSA->Audio output device:` Select the USB Audio Default Audio Device and 'Save'.

Plug in a usb drive with audio files to the pi and setup a playlist etc. in vlc.

Exit vlc

```
# add the following line to /etc/rc.local
su -c "vlc -I http &>/tmp/vlc.log" pi &
```

Reboot the pi or run the command above.

## Connect
Use a browser to connect to the pi and start playing music.

When prompted leave the user name blank and type in the password you set earlier.

`http://<pi-address>:8080/`
