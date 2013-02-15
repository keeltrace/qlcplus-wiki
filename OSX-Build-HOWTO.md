# QLC+ Installation from sources on Mac OSX

## Development environment

You need to download and install two components before you can compile QLC+ from sources on a Mac OSX:

**Apple XCode** development tools (just the Mac version will do, no need for iPhone stuff). Some recent versions might need to install Command Line Tools after base packet is installed (XCode->Preferences->Downloads)<br>
**Digia Qt Framework**<br>
NOTE: Qt 4.6.3 has some issues with its QFontDialog in OS X so you shouldn't use it any longer. Qt 4.8.x is nowadays the preferred Qt version.

Note that Qt no longer supports Leopard (10.5.x) and older Mac OS X versions.

## Dependencies/Ports

QLC+ and some plugins require additional external packages including: libusb, libftdi, protobuf, cppunit, libcrypt, libmicrohttpd, uuid, OLA, libmad, libsndfile and liblo

These dependencies are easily available thru macports.

Download macports dmg package from macports.org and install it.<br>
Then, launch the terminal and type:<br>
`sudo port selfupdate`<br>
`sudo port install libftdi pkgconfig git ola mad libdnfile liblo`<br>

## Optional Ports & Helpers

If you intend on doing a lot of development, cleaning often and recompiling everything, you might want to install ccache, which speeds up consequent compilations (after the first caching run) IMMENSELY.<br>
`sudo port install ccache`<br>
`sudo ln -s /opt/local/bin/ccache /opt/local/bin/gcc`<br>
`sudo ln -s /opt/local/bin/ccache /opt/local/bin/g++`<br>
`sudo ln -s /opt/local/bin/ccache /opt/local/bin/cc`<br>
`sudo ln -s /opt/local/bin/ccache /opt/local/bin/c++`<br>

Also, colordiff is a nice tool for seeing your changes (svn diff) in color:<br>
`sudo port install colordiff less`

You might want to make an alias for qmake so that you only need to write "qmake" instead of "qmake -spec macx-g++"
Edit ~/.profile and put this somewhere:<br>
`alias qmake="qmake -spec macx-g++"`<br>

## Getting the sources from GIT

Open the terminal window (under Applications/Utilities in Finder) and write one of the following commands:

If you wish to get the latest released QLC version:<br>
http://sourceforge.net/projects/qlcplus/files/Sources/<br>

If you wish to get the very latest bleeding edge (but only if your intention is to do development or are just curious):<br>
`git clone git://github.com/mcallegari/qlcplus.git`<br>

You might be asked to accept an SSL site certificate. After you have accepted it, the sources will be downloaded to a directory called qlc under your home directory (where the terminal usually starts at). It can take a while, depending on your internet connection speed.

## Compiling

After the sources have been checked out from the subversion repository, issue these commands to start building QLC:

`cd qlcplus`<br>
`qmake -spec macx-g++`<br>
`make`<br>

You should see the terminal window fill up with compiler calls. Go grab a cup of your preferred beverage, as this can take anything from about a minute to several minutes, depending on your system performance. If you see any errors, please Mail me since it's probably just a small thing I forgot to write in this document.

Finally, make says someting like "Nothing to be done for 'first'. That's it, you're done!

## Installation

When QLC+ has been successfully compiled, you can install it into your home directory as QLC.app by issuing the following command to the terminal:<br>
`make install`<br>

Don't worry; everything is installed inside this one application bundle in your home directory. Go to Finder and navigate to your home directory. You should see the QLC+ logo there and if you dare click it, QLC+ launcher should open. You can move the application bundle manually under Applications if you wish. Have fun! :)

## Package creation

If you wish to create a distributable .dmg package, that doesn't require the presence of Qt SDK, XCode or macports, type the following commands after installation to your terminal window:<br>
`./create-dmg.sh`<br>

This creates an Apple .dmg package to the same directory you're currently in. If you haven't compiled and installed QLC+ prior to this step, the created package will not work, as it assumes that QLC+ has been installed to ~/QLC+.app/.