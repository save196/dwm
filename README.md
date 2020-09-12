dwm - dynamic window manager
============================
dwm is an extremely fast, small, and dynamic window manager for X.

This is my personal version of dwm. For further information visit
the official website: https://dwm.suckless.org

Requirements
------------
In order to build dwm you need the Xlib header files.

This build add to config.def.h some shortcuts to run some additional programs.
To have a fully functional configuration, you need to install the following dependencies:

    - playerctl (to control music using media keys) lines: 119, 120, 121
        Debian/Ubuntu based distros installation: sudo apt install playerctl
        Arch based distros installation: sudo pacman -S playerctl
    - ALSA Utilities (to mute and unmute microphone) line: 122
        Debian/Ubuntu based distros installation: sudo apt install alsa-utils
        Arch based distros installation: sudo pacman -S alsa-utils
    - ncspot (FOSS cli Spotify client) line: 77
        Debian/Ubuntu based distros installation: https://github.com/hrkfdn/ncspot
        Arch based distros installation (AUR package): yay -S ncspot
    - ranger (cli file manager) line: 76
        Debian/Ubuntu based distros installation: sudo apt install ranger
        Arch based distros installation: sudo pacman -S ranger
    - Vim (cli text editor) line: 65
        Debian/Ubuntu based distros installation: sudo apt install vim
        Arch based distros installation: sudo pacman -S vim
    - VimWiki Vim Plugin (to create your personal wiki using vim) line: 65
        Installation described in the project page: https://github.com/vimwiki/vimwiki
    - dmenu (suckless fast and lightweight dynamic menu for X)
       	Debian/Ubuntu based distros installation: sudo apt install suckless-tools
       	Arch based distros installation: sudo pacman -S dmenu

Of course you can replace these dependencies with your favorite alternatives to these programs. To ease this
process I specified at what line of config.def.h you can find these dependencies
mentioned.

The default terminal is suckless st, but you can change it with your favourite terminal.
Occurrences of st to replace can be found in config.def.h at lines: 63, 65, 76.

To set your favorite web browser you can either set a system env var '$BROWSER' in your
.profile file (ex. by adding 'export BROWSER="firefox"' to it) or replace '$BROWSER' in config.def.h at line
75 with your favorite one.

For some tasks (change volume/change backlight/take a screenshot) custom scripts are used.
To perform these actions you need to create your own scripts. You can find these custom
scripts defined at line 116, 117, 118, 123, 124, 125, 126 of config.def.h file.
TODO: publish those custom scripts.


Installation
------------
Edit config.mk to match your local setup (dwm is installed into
the /usr/local namespace by default).

Afterwards enter the following command to build and install dwm (if
necessary as root):

    make clean install

For Debian/Ubuntu based distro users that come from a Desktop Environment,
a fast way to install dwm, is to first install it from the official repositories
by running:

    sudo apt install dwm

This will add a dwm entry to your display manager, so the next time you will
login to your system you will have the ability to select dwm as your window
manager. After having installed dwm using your package manager, you can run
with root privileges:

    make clean install

to install and use this custom dwm build instead of the one installed by your
package manager.


Running dwm
-----------
For Debian/Ubuntu based distros, you can skip this part and read the last
part of the installation section.

Add the following line to your .xinitrc to start dwm using startx:

    exec dwm

In order to connect dwm to a specific display, make sure that
the DISPLAY environment variable is set correctly, e.g.:

    DISPLAY=foo.bar:1 exec dwm

(This will start dwm on display :1 of the host foo.bar.)

In order to display status info in the bar, you can do something
like this in your .xinitrc:

    while xsetroot -name "`date` `uptime | sed 's/.*,//'`"
    do
    	sleep 1
    done &
    exec dwm


Configuration
-------------
The configuration of dwm is done by editing config.def.h
and (re)compiling the source code.

Before recompiling, run:

    make clean

Otherwise the new configuration will not be applied.


Shortcuts
---------
Super is defined as the Win key.


Super+p			-> launch dmenu

Super+Enter		-> launch terminal (default: st)

Super+`			-> launch scratchpad (uses Vim and its VimWiki plugin)

Super+w			-> launch browser

Super+e			-> launch file manager (default: ranger)

Super+s			-> launch Spotify client (default: ncspot)

Super+Shift+Backspace	-> asks if you want to poweroff your pc

Super+b			-> toggle statusbar

Super+[j, k]		-> rotate windows focus

Super+[i, d]		-> increase/decrease the number of master windows

Super+[h, l]		-> increase/decrease master windows size

Super+Shift+Enter	-> set selected window as master

Super+Tab		-> switch to the last used tag

Super+Shift+q		-> kill dwm

Super+[t, f, m, u, o]	-> change windows layout to tiled/float/monocle/bottomstack1/bottomstack2

Super+Space		-> switch layout with the last one used

Super+Shift+Space	-> toggle floating layout for the selected window

Super+Shift+f		-> toggle full screen

Super+[., ,]		-> switch monitor

Super+Shift+[., ,]	-> move selected window to the next or previous monitor

Super+[1..9]		-> change tag

Super+Shift+q		-> kill selected window

Super+PrintScreen	-> screenshot on a specific area

Working media keys: VolUp/Down, VolMute, MicMute, NextTrack, PrevTrack, Play/Pause, BrightnessUp/Down, PrintScreen.

NOTES: if something does not work, please refer to the Requirements section.


Patches
-------
attachbelow - https://dwm.suckless.org/patches/attachbelow/dwm-attachbelow-6.2.diff

actualfullscreen - https://dwm.suckless.org/patches/actualfullscreen/dwm-actualfullscreen-20191112-cb3f58a.diff

statusallmons - https://dwm.suckless.org/patches/statusallmons/dwm-statusallmons-6.2.diff

pertag - https://dwm.suckless.org/patches/pertag/dwm-pertag-6.2.diff

scratchpad - https://dwm.suckless.org/patches/scratchpad/dwm-scratchpad-6.2.diff

alpha (fixborders) - https://dwm.suckless.org/patches/alpha/dwm-fixborders-6.2.diff

bottomstack - https://dwm.suckless.org/patches/bottomstack/dwm-bottomstack-6.1.diff

ru_gaps tile - https://dwm.suckless.org/patches/ru_gaps/dwm-ru_gaps-6.2.diff

ru_gaps bottomstack - https://dwm.suckless.org/patches/ru_gaps/dwm-ru_bottomstack-6.2.diff

canfocusrule - custom patch based on https://dwm.suckless.org/patches/canfocusrule/dwm-canfocusrule-20200702-f709b19.diff (original has a bug that prevent windows spawned by another window to be focused. Example: Basic HTTP Login window spawned by Firefox)


Additional Information
----------------------

This build includes also a patch written by me based on the canfocusrule patch that allow the
official Microsoft Teams client to properly display notifications. Indeed, teams uses its own
notification system that vanilla dwm do not handle properly.
This patch do not want to encourage the use of Microsoft Teams since it is proprietary
software. But in many working environments it is the main teams communication software,
so in the case you must use Microsoft Teams, this patch can be handy.
