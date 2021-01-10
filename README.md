# Raspberry Pi 4/400 - RetroArch Guide

This Guide written in Jan 2021, and is meant to be used on a fresh install of the 32bit Raspberry Pi OS Desktop, on a Raspberry Pi 4.

I love RetroArch more than any other Raspberry Pi retro gaming solution, so I thought it would be nice to have a very focused guide about installing RetroArch on a Raspberry Pi 4/400 and some detailed info to help someone to understand how it all works.  Another reason I did this is because I had a very specific set of things I wanted my Retro Gaming Raspberry Pi to do, that didn't seem very possible on other retro gaming solutions.

I wanted to:
* Keep games separate from the OS on a different USB thumbdrive.  
* On boot, auto backup RetroArch config files to the extra USB thumbdrive, and run some other scripts in the future, I haven't even thought of yet.
* 1 retro gaming GUI like RetroArch. Most others combine RetroArch and Emulationstation, which seems like overkill to me.
* Edit config files and adding games without having to connect through the wifi.
* Configure other things like Bluetooth or wifi through the Raspberry Pi OS.
* Be able to close Retroarch and use the Raspberry Pi as a normal computer.

Here are the basics of what we'll be doing in this guide:

* Install RetroArch
* Configure RetroArch
* Install a script to autostart Retroarch, shutdown the Rraspbery Pi, and backup RetroArch config files to the thumbdrive.

## Boot up Raspberry Pi OS and lets get started

First lets make sure the Raspberry Pi OS logs on automatically.

Desktop Menu > Preferences > Raspberry Pi Configuration > System > Auto Login > [yes]

Connect to the internet the usual way and then open a Terminal and update.
The '-y' automatically chooses 'yes' during package installation. We'll use it in this project to make things quicker, but be careful with this flag when installing things.  Also as a reminder, when doing a copy or paste on a Terminal, use Shift + Ctrl + c, and Shift + Ctrl + v to copy and paste.
```
sudo apt update
sudo apt full-upgrade -y
```

After you are connected to the internet and have a web browser, I would recommend doing a git clone to this guide or bookmarking this page in your browser, so you'll have easy access to these instructions.

Use a Terminal to install snapd and retroarch:
```
sudo apt install snapd -y
```
We have to reboot after installing snapd, but first lets do a change to the system that will help fix display issues while gaming.

```
sudo raspi-config
```
Advanced Options > Compositor > [no]

Display Options > Composite Video > [no]

This is optional, use this if your screen does something annoying when the screen loses signal.

Display Options > Screen Blanking > [no]

After you select 'Finish', it will ask you to reboot.

Now lets install RetroArch
```
sudo snap install retroarch
```
Install your favorite command line editor or if you like nano, then replace 'vim' with 'nano' throughout this guide.
```
sudo apt install vim -y
```
Enable exfat.  This is optional.  I like using an exfat external thumbdrive to store the Games.  I chose Exfat because it works on all OS's.
```
sudo apt install exfat-fuse -y
```
## Optional Argon One case shutdown script

I bought the Argon One case because it relocates all the inputs to the back of the device.  Heres the script that adjusts the fan and power button.

https://github.com/okunze/Argon40-ArgonOne-Script

Skip this if you don't have an Argon One Raspberry Pi 4 case.
```
curl https://download.argon40.com/argon1.sh | bash
```
## Configure Retroarch Downloader
Lets get the default config files for RetroArch created by running RetroArch, and then close it for now.  Since this is the first time running RetroArch, this may be a bit slow.  You'll also see some errors, but that's ok.
```
retroarch
```
Now close RetroArch by closing out the window.  If your in full screen mode, press F, and then close out the window.

The default set of downloadable cores are ok, but the Playstation core isn't the best, since it only offers lower resolutins. To fix this we need to open a terminal and edit this file and change the URL:

The '427' may be a different number for you.  Also, use your favorite editor instead of vim.
```
vim snap/retroarch/427/.config/retroarch/retroarch.cfg
```
Find the line that starts with:
```
core_updater_buildbot_cores_url=
```
and change that line to:
```
core_updater_buildbot_cores_url="https://buildbot.libretro.com/nightly/linux/armv7-neon-hf/latest/"
```
Also, there are other URL's you can use, if you'd like to experiment with an older set of cores. Go to that URL in a web browser and browse around!

## Configure Retroarch. 

```
retroarch
```

Change to XMB in retroarch

Settings > Drivers > Menu > [xmb]

Make sure your settings get saved when exiting RetroArch.

Settings > Configuration > Save Configuration on Quit > [on]

Restart Retroarch

Main Menu > Restart RetroArch

Now you should be using XMB.  Lets do some more things in Retroarch.

Set retroarch to fullscreen

Settings > Video > Fullscreen Mode > Start in Fullscreen Mode > [on]

If you'd like to toggle fullscreen, press 'f' on the keyboard.

Hopefully your controller is mostly working, so you should be able to use that now, or you can use the keyboard's up, down, left, right and enter keys to get around in XMB.  

If your controller isn't working go to:

Settings(Second icon from the left) > input > Port 1 controls > Set All Controls

You may have to do this a couple times if you mess up, so don't forget you do have the keyboard if you lose control with your controller.

If you have a spare button on your controller you may want to asign a button that will pop up the XMB during gameplay:

Settings > Input > Hotkeys > Menu (Toggle) > [press the button]

If you don't have a spare button for Menu Toggle, then do this to set a combo button press for the Menu Toggle:

Settings > input > Hotkeys > Menu Toggle Gamepad Combo > [start + select]

This is optional and you can come back to this later, but if you would like to swap the OK and Cancel buttons:

Settings(Second icon from the left) > input > menu controls > Menu Swap OK and Cancel Buttons [on]

Main Menu(First Icon from the left) Online Updater -> Update Assets

## Download Some Cores

Main Menu > Online Updater -> Core Downloader > [choose cores here to download]

Cores I am currently using.  I'll swap these out later if I find better alternatives.
```
ATARI - 2600 (STELLA 2014)
Nintendo - Game Boy / Color (Gambatte)
Nintendo - Game Boy Advance (gbSP)
Nintendo - NES / Famicom (FCEUmm)
Nintendo - SNES / SFC (Snes9x - Current)
Sega - MS/MD/CD/32x (Genesis Plus GX)
Sony - PlayStation (PCSX ReARMed)
```
## Add some games

Import Content(Big Plus Icon) > Scan Directory > [choose rom directory]

If your having trouble finding them, make sure you have your USB drive plugged in, and restart the Pi 4.  Then
select the 'Parent Directory' button until you see a directory called /media.  Select /media, then /pi, then your thumbdrive, and then your games you want to import.  I would recommend importing 1 gaming console at a time.

After adding all your games, press the back button on your controller many times to get back to the top level of the Retroarch menu.

You're getting ready to play some games.  Just in case something goes wrong or crashes, lets make sure all of the settings we just applied got saved.

Main Menu > Configuration File > Save Current Configuration

## Play some games!

In the top level menu of Retroarch, go right until you see some console icons.  Pick a game, click OK a couple more times to select the core, and play the game.

## Audio Issues
If your headphone jack to low

In terminal type 
```
alsamixer
```
Select the headphone jack by pressing F6 on the keyboard, increase the level just below red levels by pressing up. Press escape to exit.

Also, for audio, on the Raspberry Pi OS panel, there is a speaker icon you can click or right click on to adjust some volume related things.

# Auto Start and Shutdown RetroArch
I wrote some scripts that will help with autostarting and shutting down RetroArch.  I just quickly want to point out that there is probably a better
way of doing this like using SystemD, but that never worked out for me, so I either don't know enough about it yet, or maybe it's behind on the Raspberry Pi OS. So lets do this with my scripts until I find a better way.  
```
cd ~
```
This is my autostart script that will perform some config backups.
```
git clone https://github.com/LowTechCoder/pi_auto_start_scripts.git
```
This is my script that watches for the USB drive to mount, and then it runs the above autostart script.
```
git clone https://github.com/LowTechCoder/watch_for_dirs_to_exist.git

cd pi_auto_start_scripts/
mkdir /home/pi/.config/autostart/
```
This script will start when the desktop is going
```
cp desktop.txt /home/pi/.config/autostart/.desktop
```
My script that contains backup commands for RetroArch configs
```
cp autostart.bash ../
cd ~
```
Edit the file and see if it needs any changes to match your pi
```
vim autostart.bash
```
Change this line to match your thumbdrive directory you want your backup files to go in:

cd /media/pi/USBDRIVE/rasp_pi_retroarch_conf_backups/

```
cd ~/watch_for_dirs_to_exist/
vim paths.conf
```
Delete the paths in this file, and add a path to match your path on your thumbdrive. This will help the script detect if this USB drive is mounted and ready to go before it runs the backups.
```
/media/pi/USBDRIVE/
```
The autoscript we installed also made it possible to shutdown the Raspberry Pi from RetroArch XMB, but don't do this now!  Just letting you know for future reference.

Main Menu > Quit RetroArch

While playing a game if you notice a little lag from the time you press a button and when the character on the game moves, then you may want to turn on Run Ahead Mode.

Settings > Latency > Run-Ahead to Reduce Latency > [on]

From my experience, setting this to 1 or 2 is ok for most games.  If you set it too high, you'll notice games acting a bit strange. If you want to be super picky about this, you probably need to have a different setting for each game.  Personally, thats too much work for me, so I just set it globally on 2.  And if I find a game that seems a bit jumpy from this, i will lower the setting for that game.

Settings > Latency > Number of Frames to Run-Ahead > [1 or 2]

Settings > Latency > Use Second Instance for Run-Ahead > [off]

We could just exit RetroArch to save settings, but lets make sure the global file gets saved after making these changes.  

Main Menu > Configuration File > Save Current Configuration

After turning Run-Ahead on globally, you'll need to turn it off for any console that can't handle it.  We'll use the Playstation as an example, and out of all the cores I use, this is the only one I need to turn off. This is also a good lesson on how to set settings for a single core, that will override the global settings you may set.

Start up a Playstion game and then: 

Sony - Playstation > Latency > Run-Ahead to Reduce Latency > [off]

Now press the Back button until you see 'Overrides' in the menu, close to the bottom of the list.  Select 'Overrides' and select 'Save Core Overrides' to save those Run-Ahead settings only for the Playstation core.

Have fun!  If you notice any issues with a core, it could be that you need to find BIOS files for that core. I'll let you google that for your self, since they aren't really needed in this guide and cores I've selected.
