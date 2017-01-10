## Prepare the build system (MSYS2)

Download the MSYS2 64bit installer from here: https://msys2.github.io/ (for 32bit systems like XP, use i686 installer).

Follow the instructions of that page otherwise install it using all the defaults (c:\msys64 or c:\msys32 for 32bit system), then open the MSYS2 shell and type:<br>
`update-core`<br>
Close the MSYS2 shell and open it again.<br>
Now install the packages required to build QLC+, by typing:<br>
`pacman -Su`<br>
`pacman -S make automake autoconf libtool mingw32/mingw-w64-i686-gcc mingw32/mingw-w64-i686-pkg-config mingw32/mingw-w64-i686-tools git`<br>
`pacman -S mingw32/mingw-w64-i686-qt5 mingw32/mingw-w64-i686-libmad mingw32/mingw-w64-i686-libsndfile mingw32/mingw-w64-i686-flac mingw32/mingw-w64-i686-fftw`<br>

**Now close the MSYS2 Shell. From now on we'll use the 'MinGW-w64 Win32 Shell'. So open it.**<br>

## Acquire the QLC+ sources

These instructions suppose you have a folder called "Qt" in C:. If it doesn't exist, create it and 'cd' into it.<br>

If you wish to get the latest released QLC+ version download the source tarball from here:<br>
[http://www.qlcplus.org/downloads.html](http://www.qlcplus.org/downloads.html)

If you wish to get the very latest bleeding edge (but only if your intention is to do development or are just curious), download the [GitHub client](https://windows.github.com/) or use the command line:
`git clone https://github.com/mcallegari/qlcplus.git`

This will create a directory called qlcplus which will contain the latest sources from GIT repository. After you have made the initial clone and later wish to keep living on the bleeding egde, you can just update the sources (instead of making a new clone every time):

`cd qlcplus`<br>
`git pull`<br>

Once done you should have a folder called 'qlcplus' in C:\Qt.

### Debug or release mode

If you are a developer and want to contribute to QLC+, the default settings will build a debug version of the program. Please note that a debug version is bigger than a release one and might have worse performances.
If what you need is a production build, then you need to edit the `variables.pri` file and change the following lines, adding a `+=` of the build you need and `-=` of the one you don't need:

`CONFIG         += release # Enable this when making a release`<br>
`CONFIG         -= debug   # Disable this when making a release`

## DMX USB Support

To compile the DMX USB plugin, you need to:

Download the latest SDK from [FTDI Driver page](http://www.ftdichip.com/Drivers/D2XX.htm).<br>
Install the package contents for example to C:\Qt\D2XXSDK<br>
Edit <QLC>/plugins/dmxusb/src/src.pro to point to the directory you picked:

`FTD2XXDIR = C:/Qt/D2XXSDK`<br>

Since the SDK provided by ftdichip.com is not compatible with the MSYS2 system, it is necessary to manually create a compatible libftd2xx.a file that will be used at build time:<br>
`cd /c/Qt/D2XXSDK/i386`<br>
`gendef.exe - ftd2xx.dll > ftd2xx.def`<br>
`dlltool -k --input-def ftd2xx.def --dllname ftd2xx.dll --output-lib libftd2xx.a`<br>

If you don't need the DMX USB plugin and would like to disable building it completely, edit <QLC>/plugins/plugins.pro and put a hash (#) on the line that says SUBDIRS += dmxusb:

`#SUBDIRS += dmxusb`<br>

## Velleman SDK

To compile the Velleman Output plugin, you need to:

Download the [modified Velleman DLL](http://www.qlcplus.org/misc/K8062DLL_mod1.zip)<br>
Extract the package contents for example to C:\Qt\K8062D<br>
Edit <QLC>/plugins/velleman/src/src.pro to point to the directory you picked:

`K8062DDIR = C:/Qt/K8062D`<br>

To use the DLL during build time, it is necessary to manually create a compatible K8062D.a:<br>
`cd /c/Qt/K8062D`<br>
`gendef.exe - K8062D.dll > K8062D.def`<br>
`dlltool -k --input-def K8062D.def --dllname K8062D.dll --output-lib K8062D.a`<br>

If you don't need the Velleman Output plugin and would like to disable building it completely, edit <QLC>/plugins/plugins.pro and put a hash (#) on the line that says SUBDIRS += velleman:

`#SUBDIRS += velleman`<br>

## Build QLC+

Now compile QLC+ by typing:<br>
`cd /c/Qt/qlcplus`<br>
`qmake`<br>
`make`<br>
`make install`<br>

It will install QLC+ and all the required DLLs in C:\qlcplus.