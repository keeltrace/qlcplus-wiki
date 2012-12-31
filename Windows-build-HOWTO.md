Get latest Qt prebuilt for MinGW32 here:<br>
[http://releases.qt-project.org/qt4/source/](http://releases.qt-project.org/qt4/source/)<br>
and install them in C:\Qt

Download MinGW installer here:<br>
[http://sourceforge.net/projects/mingw/files/Installer/mingw-get-inst/](http://sourceforge.net/projects/mingw/files/Installer/mingw-get-inst/)<br>
and install both MinGW and MSYS.

Download pkg-config prebuilt binaries and install them in the MinGW tree<br>
[http://ftp.gnome.org/pub/gnome/binaries/win32/dependencies/](http://ftp.gnome.org/pub/gnome/binaries/win32/dependencies/)<br>

I used this: http://ftp.gnome.org/pub/gnome/binaries/win32/dependencies/pkg-config_0.26-1_win32.zip

Download glib devel libraries needed by pkg-config: http://ftp.gnome.org/pub/gnome/binaries/win32/glib/
I used this: http://ftp.gnome.org/pub/gnome/binaries/win32/glib/2.24/glib_2.24.0-2_win32.zip

Download from this URL: http://lrn.no-ip.info/other/mingw/mingw32/
the -ming32-dev version of the following packages and extract them in the MinGW tree:
libmad<br>
libsndfile<br>
flac<br>
libogg<br>
libvorbis<br>


Download the latest SVN snapshot of liblo from here: http://sourceforge.net/projects/liblo/

Compile libLO by doing:

`./autogen.sh`<br>
`./configure --enable-static --disable-shared --prefix=/mingw`<br>
`make`<br>
`make install`<br>

Now compile QLC+:
`qmake`<br>
`make`<br>
`make install`<br>
