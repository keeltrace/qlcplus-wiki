# QLC+ Installation from sources on Mac OSX

## Development environment

You need to download and install two components before you can compile QLC+ from sources on a Mac OSX:

**Apple XCode** development tools (just the Mac version will do, no need for iPhone stuff)<br>
**Nokia Qt Framework**<br>
NOTE: Qt 4.6.3 has some issues with its QFontDialog in OS X so you shouldn't use it any longer. Qt 4.8.x is nowadays the preferred Qt version.

Note that Nokia Qt no longer supports Leopard (10.5.x) and older Mac OS X versions.

## Dependencies/Ports

QLC+ and some plugins require additional external packages including: libusb, libftdi, protobuf, cppunit, libcrypt?, libmicrohttpd, uuid?, and OLA

These dependencies are easily available thru macports.

Download macports dmg package from macports.org and install it.
Then, launch the terminal and type:
`sudo port selfupdate`<br>
`sudo port install libftdi pkgconfig ola mad libdnfile liblo`<br>

## Optional Ports & Helpers

If you intend on doing a lot of development, cleaning often and recompiling everything, you might want to install ccache, which speeds up consequent compilations (after the first caching run) IMMENSELY.
sudo port install ccache`<br>
`sudo ln -s /opt/local/bin/ccache /opt/local/bin/gcc`<br>
`sudo ln -s /opt/local/bin/ccache /opt/local/bin/g++`<br>
`sudo ln -s /opt/local/bin/ccache /opt/local/bin/cc`<br>
`sudo ln -s /opt/local/bin/ccache /opt/local/bin/c++`<br>

Also, colordiff is a nice tool for seeing your changes (svn diff) in color :
`sudo port install colordiff less`

Edit ~/.subversion/config and change the line with "# diff-cmd = <something" to "diff-cmd = colordiff". Also, to get it working with less (as in "svn diff | less"), put this into your ~/.profile:
  export LESS="-erX"
You might want to make an alias for qmake so that you only need to write "qmake" instead of "qmake -spec macx-g++"
Edit ~/.profile and put this somewhere:
    alias qmake="qmake -spec macx-g++"
To clean up the output of "svn status", you might want to put this into your ~/.subversion/config file (very Qt/QLC specific, note that it affects all of your svn projects):
  global-ignores = *.o *.lo *.la *.al .libs *.so *.so.[0-9]* *.a *.pyc *.pyo *.rej *~ #*# .#* .*.swp .DS_Store moc_* ui_* qrc_* *.qm *_test Makefile
  or a little more relaxed:
  global-ignores = *.o *.lo *.la *.al .libs *.so *.so.[0-9]* *.a *.pyc *.pyo *.rej *~ #*# .#* .*.swp .DS_Store moc_* ui_* qrc_* *.qm
Getting the sources from Subversion

Open the terminal window (under Applications/Utilities in Finder) and write one of the following commands:

If you wish to get the latest released QLC version:
  svn checkout https://qlc.svn.sourceforge.net/svnroot/qlc/tags/qlc-3.2.2 qlc
If you wish to get the very latest bleeding edge (but only if your intention is to do development or are just curious):
  svn checkout https://qlc.svn.sourceforge.net/svnroot/qlc/trunk qlc
You might be asked to accept an SSL site certificate. After you have accepted it, the sources will be downloaded to a directory called qlc under your home directory (where the terminal usually starts at). It can take a while, depending on your internet connection speed.

Compiling

After the sources have been checked out from the subversion repository, issue these commands to start building QLC:

  cd qlc
  qmake -spec macx-g++
  make
You should see the terminal window fill up with compiler calls. Go grab a cup of your preferred beverage, as this can take anything from about a minute to several minutes, depending on your system performance. If you see any errors, please Mail me since it's probably just a small thing I forgot to write in this document.

Finally, make says someting like "Nothing to be done for 'first'. That's it, you're done!

Installation

When QLC has been successfully compiled, you can install it into your home directory as QLC.app by issuing the following command to the terminal:

  make install
Don't worry; everything is installed inside this one application bundle in your home directory. Go to Finder and navigate to your home directory. You should see the QLC logo there and if you dare click it, QLC launcher should open. You can move the application bundle manually under Applications if you wish. Have fun! :)

Package creation

If you wish to create a distributable .dmg package, that doesn't require the presence of Qt SDK, XCode or macports, type the following commands after installation to your terminal window:

  cd create-dmg
  ./create-qlc-dmg
This creates an Apple .dmg package to the same directory you're currently in. If you haven't compiled and installed QLC prior to this step, the created package will not work, as it assumes that QLC has been installed to ~/QLC.app/.