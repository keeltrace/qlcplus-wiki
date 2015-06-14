## Prepare the build system (MSYS2)

Download the MSYS2 64bit installer from here: https://msys2.github.io/

Follow the instructions of that page otherwise install it using all the defaults (c:\msys64), then open the MSYS2 shell and type:<br>
`pacman --needed -Sy bash pacman pacman-mirrors msys2-runtime`<br>
`pacman -Su`<br>

Close the MSYS2 shell and open it again.<br>
Now install the packages required to build QLC+, by typing:<br>
`pacman -S make automake autoconf libtool mingw32/mingw-w64-i686-gcc mingw32/mingw-w64-i686-pkg-config mingw-w64-i686-tools`<br>
`pacman -S mingw32/mingw-w64-i686-qt5 mingw32/mingw-w64-i686-libmad mingw32/mingw-w64-i686-libsndfile mingw32/mingw-w64-i686-flac mingw32/mingw-w64-i686-fftw`<br>

## FTDI DMX USB Support

To compile the DMX USB plugin on Windows, you need to:

Download the latest SDK from [FTDI Driver page](http://www.ftdichip.com/Drivers/D2XX.htm).<br>
Install the package contents for example to C:\Qt\CDM20828<br>
Edit <QLC>/plugins/dmxusb/src/src.pro to point to that directory:

`FTD2XXDIR = C:\Qt\CDM20828`<br>

If you don't need the DMX USB plugin and would like to disable building it completely, edit <QLC>/plugins/plugins.pro and put a hash (#) on the line that says SUBDIRS += dmxusb:

`#SUBDIRS += dmxusb`<br>

## Velleman SDK

To compile the Velleman Output plugin on Windows, you need to:

Download the [modified Velleman SDK](https://sourceforge.net/apps/trac/qlc/wiki/VellemanK8062D)<br>
Unpack the zip to C:\Qt\K8062D<br>
Not applicable yet: If you don't need the Velleman Output plugin and would like to disable building it completely, edit <QLC>/plugins/plugins.pro and put a hash (#) on the line that says SUBDIRS += velleman:

`#SUBDIRS += velleman`<br>
