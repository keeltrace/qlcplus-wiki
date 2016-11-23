# QLC+ Installation from sources on Mac OSX using Qt5

## Development environment

You need to download and install two components before you can compile QLC+ from sources on a Mac OSX:

**Apple XCode** development tools (just the Mac version will do, no need for iPhone stuff). Some recent versions might need to install Command Line Tools after base packet is installed (XCode->Preferences->Downloads)<br>
**The Qt5 Framework**<br>
Download the latest Qt5 version from here: http://download.qt.io/official_releases/qt/<br>
It is suggested to use an offline installer instead of the online one.
Install the framework where you want. In this guide we'll be using this path: /Users/myuser/Qt5.5.1<br>

## Dependencies/Ports

QLC+ and some plugins require additional external packages including: libusb, libftdi, protobuf, cppunit, libcrypt, libmicrohttpd, uuid, OLA, libmad, libsndfile and fftw3

These dependencies are easily available through macports.

Download macports package from [macports.org](https://www.macports.org/install.php) and install it.<br>
Then, open the OSX Terminal application and type:<br>
`sudo port selfupdate`<br>
`sudo port install libftdi0 pkgconfig libmad libsndfile fftw-3 ola`<br>

**OLA build**: in case OLA fails to install via macports, you might want to compile it from sources. To do so, follow the [instructions here](http://opendmx.net/index.php/OLA_Mac_Install_From_Tarball) and at the end type:<br>
`./configure --prefix=/opt/local`<br>
`make`<br>
`sudo make install`

## Getting the sources from GIT

Open the terminal window (under Applications/Utilities in Finder) and write one of the following commands:

If you wish to get the latest released QLC+ version:<br>
[http://www.qlcplus.org/downloads.html](http://www.qlcplus.org/downloads.html)<br>

If you wish to get the very latest bleeding edge (but only if your intention is to do development or are just curious):<br>
`git clone git://github.com/mcallegari/qlcplus.git`<br>

You might be asked to accept an SSL site certificate. After you have accepted it, the sources will be downloaded to a directory called qlc under your home directory (where the terminal usually starts at). It can take a while, depending on your internet connection speed.

### Plugins build note

QLC+ needs several external dependencies to be compiled with all the plugins support.<br>
If you want to exclude some of them from the build process then just comment them out by placing the character `#` at the beginning of the plugin line in the file `plugins/plugins.pro`
For example:

`#unix:SUBDIRS += ola`

## Compiling

After the sources have been cloned out from the GIT repository, issue these commands to start building QLC+:

`export QTDIR=/Users/myuser/Qt5.5.1/5.5/clang_64`<br>
`cd qlcplus`<br>
`/Users/myuser/Qt5.5.1/5.5/clang_64/bin/qmake`<br>
`make`<br>

You should see the terminal window fill up with compiler calls. Go grab a cup of your preferred beverage, as this can take anything from about a minute to several minutes, depending on your system performance. If you see any errors, please report it in the QLC+ forum (development forum).

Finally, make says something like "Nothing to be done for 'first'. That's it, you're done!

## Installation

When QLC+ has been successfully compiled, you can install it into your home directory as QLC+.app by issuing the following command to the terminal:<br>
`make install`<br>

Don't worry; everything is installed inside this one application bundle in your home directory. Go to Finder and navigate to your home directory. You should see the QLC+ logo there and if you dare click it, QLC+ launcher should open. You can move the application bundle manually under Applications if you wish. Have fun! :)

## Package creation

If you wish to create a distributable .dmg package, that doesn't require the presence of Qt SDK, XCode or macports, type the following commands after installation to your terminal window:<br>
`./create-dmg.sh`<br>

This creates an Apple .dmg package in the dmg folder of the QLC+ sources tree.
This script works also on non-built sources, so you just need to follow the steps above up to "cd qlcplus", right after "export QTDIR..."