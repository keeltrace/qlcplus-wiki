Get latest Qt prebuilt for MinGW32 here: [http://releases.qt-project.org/qt4/source/](http://releases.qt-project.org/qt4/source/)<br>
and install them in C:\Qt

Download MinGW installer here: [http://sourceforge.net/projects/mingw/files/Installer/mingw-get-inst/](http://sourceforge.net/projects/mingw/files/Installer/mingw-get-inst/)<br>
and install both MinGW and MSYS.

Download pkg-config prebuilt binaries and install them in the MinGW tree:
http://ftp.gnome.org/pub/gnome/binaries/win32/dependencies/

I used this: http://ftp.gnome.org/pub/gnome/binaries/win32/dependencies/pkg-config_0.26-1_win32.zip

Download glib devel libraries needed by pkg-config: http://ftp.gnome.org/pub/gnome/binaries/win32/glib/
I used this: http://ftp.gnome.org/pub/gnome/binaries/win32/glib/2.24/glib_2.24.0-2_win32.zip

Download the -ming32-dev version of the following packages and extract them in the MinGW tree:
libmad
libsndfile
flac
libogg
libvorbis

from this URL: http://lrn.no-ip.info/other/mingw/mingw32/

Download the latest SVN snapshot of liblo from here: http://sourceforge.net/projects/liblo/

Compile libLO by doing:

./autogen.sh
./configure --enable-static --disable-shared --prefix=/mingw
make
make install

Now compile QLC+:
qmake
make
make install