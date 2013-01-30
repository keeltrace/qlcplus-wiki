## Prepare QT and MinGW32 build system

Get latest Qt prebuilt for MinGW32 here:<br>
[http://releases.qt-project.org/qt4/source/](http://releases.qt-project.org/qt4/source/)<br>
and install them in C:\Qt

Download MinGW installer here:<br>
[http://sourceforge.net/projects/mingw/files/Installer/mingw-get-inst/](http://sourceforge.net/projects/mingw/files/Installer/mingw-get-inst/)<br>
and install both MinGW and MSYS in the default path proposed by the installer.

## Prerequisites

Download **pkg-config** prebuilt binaries and install them in the MinGW tree<br>
[http://ftp.gnome.org/pub/gnome/binaries/win32/dependencies/](http://ftp.gnome.org/pub/gnome/binaries/win32/dependencies/)<br>

I used this: http://ftp.gnome.org/pub/gnome/binaries/win32/dependencies/pkg-config_0.26-1_win32.zip

Download **glib devel** libraries needed by pkg-config: http://ftp.gnome.org/pub/gnome/binaries/win32/glib/<br>
I used this: http://ftp.gnome.org/pub/gnome/binaries/win32/glib/2.24/glib_2.24.0-2_win32.zip

## Audio support (optional)

Download from this URL: http://lrn.no-ip.info/other/mingw/mingw32/<br>
the **-ming32-dev** version of the following packages and extract them in the MinGW tree:<br>
* libmad
* libsndfile
* flac
* libogg
* libvorbis

## Enttec/FTDI SDK

To compile the Enttec DMXUSB Output plugin on Windows, you need to:

Download the latest SDK from [FTDI Driver page](http://www.ftdichip.com/Drivers/D2XX.htm).<br>
Install the package contents for example to C:\CDM20802<br>
Edit <QLC>/plugins/enttecdmxusb/src/src.pro to point to that directory:

`FTD2XXDIR = C:\CDM20802`<br>

If you don't need the Enttec DMXUSB plugin and would like to disable building it completely, edit <QLC>/plugins/plugins.pro and put a hash (#) on the line that says SUBDIRS += enttecdmxusb:

`#SUBDIRS += enttecdmxusb`<br>

## Velleman SDK

To compile the Velleman Output plugin on Windows, you need to:

Download the [modified Velleman SDK](https://sourceforge.net/apps/trac/qlc/wiki/VellemanK8062D)<br>
Unpack the zip to C:\K8062D<br>
Not applicable yet: If you don't need the Velleman Output plugin and would like to disable building it completely, edit <QLC>/plugins/plugins.pro and put a hash (#) on the line that says SUBDIRS += velleman:

`#SUBDIRS += velleman`<br>

## OSC support library (liblo)

**Note**: if you don't need the OSC support just comment `SUBDIRS += osc` in plugins/plugins.pro and skip this section.<br>

Download the latest SVN snapshot of liblo from here: http://sourceforge.net/projects/liblo/<br>
Compile libLO by doing:

`./autogen.sh`<br>
`./configure --enable-static --disable-shared --prefix=/mingw`<br>
`make`<br>
`make install`<br>

Now you need to manually patch libLO pkg-config file to avoid build issues. Edit the file liblo.pc that you can find in your MinGW installation path /lib/pkgconfig folder. (usually C:\MinGW\lib\pkgconfig)<br>
Change the line starting with "Libs:" into:<br>
`Libs: -L${libdir} -llo -lpthread -lws2_32 -liphlpapi`

## Build QLC+

Now compile QLC+ (I use Windows PowerShell to do so):<br>
`qmake`<br>
`make`<br>
`make install`<br>

## Post installation
Now to launch QLC+ the dependency libraries are needed as DLLs files. 
Download from this URL: http://lrn.no-ip.info/other/mingw/mingw32/<br>
the -mingw32-dll version of the following packages and copy them in the main QLC+ folder:
* libFLAC-8.dll (optional - see Audio support)
* libmad-0.dll (optional - see Audio support)
* libogg-0.dll (optional - see Audio support)
* libsndfile-1.dll (optional - see Audio support)
* libstdc++-6.dll (optional for OSC support)
* libvorbis-0.dll (optional - see Audio support)
* libvorbisenc-2.dll (optional - see Audio support)
* pthreadGC2.dll (optional for OSC support)

Most likely the plugins folder will contain ".a" binaries. Rename them to ".dll" to let QLC+ load them.