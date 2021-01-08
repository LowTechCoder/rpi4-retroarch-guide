# rpi4-retroarch-guide

This Guide written in Jan 2021, and is meant to be used on a fresh install of the 32bit Raspberry Pi OS Desktop, on a Raspberry Pi 4.  

During Raspberry Pi OS Installation,
Choose Auto login, choose a password, and do anything else it asks for.

Connect to the internet the usual way and then open a Terminal and update.
The '-y' automatically chooses 'yes' during package installation. We'll use it in this project to make things quicker, but be careful with this flag when installing things.
```
sudo apt update
sudo apt full-upgrade -y
```

After you are connected to the internet and have a web browser, I would recommend doing a git clone to this guide or bookmarking this page in your browser, so you'll have easy access to these instructions.

Use a Terminal to install snapd and retroarch:
```
sudo apt install snapd -y
sudo snap install retroarch
```
Install your favorite command line editor.  If your new, replace vim with nano.
```
sudo apt install vim -y
```
Enable exfat.  This is optional.  I like using an exfat external thumbdrive to store the Games.  I chose Exfat because it works on all OS's.
```
sudo apt install exfat-fuse -y
```
Optional Argon One case shutdown script:

https://github.com/okunze/Argon40-ArgonOne-Script

Skip this if you don't have an Argon One Raspberry Pi 4 case.
```
curl https://download.argon40.com/argon1.sh | bash
```
Fixes emulation display issues
Desktop Menu > Preferences > Raspberry Pi Configuration > Display > Composite Video [Disable]
This is optional, use this if your screen does something annoying when the screen loses signal.
Desktop Menu > Preferences > Raspberry Pi Configuration > Display > Screen Blanking [Disable]
   
   

fixme! not sure yet if I need this, default may be fine.
Menu > Preferences > Raspberry Pi Configuration > Performance > GPU Memory > [128]

Click OK, when done, and you will now be asked to reboot or you can type this into terminal to reboot:
sudo reboot

Configure Retroarch

The default set of downloadable cores are ok, but the Playstation core isn't the best, since it only offers lower resolutins.  
To fix this we need to open a terminal and edit this file and change the URL:
The '427' may be a different number for you.  Also, use your favorite editor instead of vim.
vim snap/retroarch/427/.config/retroarch/retroarch.cfg
Find the line that starts with:
core_updater_buildbot_cores_url=
and change that line to:
core_updater_buildbot_cores_url="https://buildbot.libretro.com/nightly/linux/armv7-neon-hf/latest/"

Also, there are other URL's you can use, if you'd like to experiment with an older set of cores. Go to that URL in a web browser and browse around!

Configure Retroarch. This first run will be slow.
retroarch

Change to XMB in retroarch
Settings > Drivers > Menu > [xmb]
Restart Retroarch

Now you should be using XMB.  Lets do some more things in Retroarch.

If you'd like to go full screen, press 'f' on the keyboard.

Hopefully your controller is mostly working, so you should be able to use that now, or you can use the keyboard's up
down left right and enter keys to get around in XMB.  

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

Main Menu > Online Updater -> Core Downloader > [choose cores here to download]

Cores I am currently using.  I'll swap these out later if I find better alternatives.
ATARI - 2600 (STELLA 2014)
Nintendo - Game Boy / Color (Gambatte)
Nintendo - Game Boy Advance (gbSP)
Nintendo - NES / Famicom (FCEUmm)
Nintendo - SNES / SFC (Snes9x - Current)
ScummVM
Sega - MS/MD/CD/32x (PicoDrive)
Sony - PlayStation (PCSX ReARMed)

Add some games

Import Content(Big Plus Icon) > Scan Directory > [choose rom directory]
If your having trouble finding them, make sure you have your USB drive plugged in, and restart the Pi 4.  Then
select the 'Parent Directory' button until you see a directory called /media.  Select /media, then /pi, then your thumbdrive, and then your games you want to import.  I would recommend importing 1 gaming console at a time.

After adding all your games, press the back button on your controller many times to get back to the top level of the Retroarch menu.

Play some games!
In the top level menu of Retroarch, go right until you see some console icons.  Pick a game, click OK a couple more times to select the core, and play the game.

Audio headphone jack to low
In terminal type "alsamixer"
Select the headphone jack, increase the level just below red levels.
Press escape to exit.

Also, for audio, on the Raspberry Pi OS panel, there is a speaker icon you can click or right click on to adjust some volume related things.

