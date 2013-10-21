## Prepare QT and MinGW32 build system

Download MinGW installer here:<br>
[https://sourceforge.net/projects/mingw/files/Installer/](https://sourceforge.net/projects/mingw/files/Installer/)<br>
and install both MinGW and MSYS in the default path proposed by the installer.<br>
When asked, remember to install the c++ compiler.

Get latest Qt prebuilt for MinGW32 here:<br>
[http://download.qt-project.org/official_releases/qt/](http://download.qt-project.org/official_releases/qt/)<br>
and install them in C:\Qt

Make sure your environment variables are set as follows:<br>
QMAKESPEC = win32-g++<br>
QTDIR = C:\Qt\4.8.5<br>
PATH = ....;C:\Qt\4.8.5\bin;C:\Qt\4.8.5;C:\MinGW\bin<br>

## Prerequisites

Download **pkg-config** prebuilt binaries and install them in the MinGW tree<br>
[http://ftp.gnome.org/pub/gnome/binaries/win32/dependencies/](http://ftp.gnome.org/pub/gnome/binaries/win32/dependencies/)<br>

I used this: http://ftp.gnome.org/pub/gnome/binaries/win32/dependencies/pkg-config_0.26-1_win32.zip

Download **glib devel** libraries needed by pkg-config: http://ftp.gnome.org/pub/gnome/binaries/win32/glib/<br>
I used this: http://ftp.gnome.org/pub/gnome/binaries/win32/glib/2.24/glib_2.24.0-2_win32.zip

## Audio input support

Download from this URL: http://lrn.no-ip.info/other/mingw/mingw32/<br>
the **-ming32-dev** version of the **fftw3** package and extract it in the MinGW tree.

## Audio output support (optional)

Download from this URL: http://lrn.no-ip.info/other/mingw/mingw32/<br>
the **-ming32-dev** version of the following packages and extract them in the MinGW tree:<br>
* libmad
* libsndfile
* flac
* libogg
* libvorbis

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
For FFTW3 the correct DLL must be downloaded from here: http://download.qt-project.org/official_releases/qt/

If the plugins folder will contain ".a" binaries, rename them to ".dll" to let QLC+ load them.