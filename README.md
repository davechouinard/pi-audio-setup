# pi-audio-setup

Simple audio server setup to play local high quality audio files.

This project was created to free up my laptop from always being connected to the stereo to play music.

Since the digital-to-analog converter on the raspberry pi is likely low quality we'll use a dedicated 
USB DAC to do that conversion. If you wanted to spend more and don't mind the extra cable,
a DAC with a dedicated power supply would likely be even better.

```
+--------------------+               +--------------------+               +---------------------+
|                    |               |                    |               |                     |
|                    |               |                    |               |                     |
|   raspberry pi     |  usb cable    |      usb dac       |  rca cables   |    amp/speakers     |
|                    +---------------+                    +---------------+                     |
|                    |               |                    |               |                     |
|                    |               |                    |               |                     |
+--------------------+               +--------------------+               +---------------------+
```

## Setup
Assumes NOOBS or other Debian based OS is running on the pi and a static IP has been assigned.
```
sudo apt-get update 
sudo apt-get install vlc
vlc &
```

In the vlc interface go to: 
`Tools->Preferences (select "All" radio button)->Interface->Main interfaces->Lua` Set a password and 'Save'.

Plug in a usb drive with audio files to the pi and setup a playlist etc. in vlc.

Set default audio to the correct output device:
`Tools->Preferences->Audio (select "All" radio button)->Output Modules->ALSA->Audio output device` Select the USB DAC default audio device.

Exit vlc

```
# add the following line to /etc/rc.local
su -c "vlc -I http &>/tmp/vlc.log" pi &
```

Reboot the pi or run the command above.

## Connect
Use a browser on a computer or phone to connect to the pi and start playing music.

When prompted leave the user name blank and type in the password you set earlier.

`http://<pi-address>:8080/`
