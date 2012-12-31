# QLC Installation from sources on Linux (Debian, Ubuntu, Fedora, RedHat)
## Pre-requisities

You need a bunch packages installed before you can compile QLC from sources. Everything here happens in the terminal window, so launch one now. Usually it's an entry under Accessories in your desktop main menu.

## Ubuntu/Debian

Issue these commands to install the required packages for an Ubuntu system:

`sudo apt-get update`

`sudo apt-get install g++ make git libqt4-dev qt4-dev-tools libasound2-dev libusb-dev debhelper`

`sudo apt-get install devscripts fakeroot libftdi-dev pkg-config libudev-dev libmad-dev libsndfile-dev liblo-dev`

## Optional helpers

If you intend on doing a lot of development, cleaning often and recompiling everything, you might want to install ccache, which speeds up consequent compilations (after the first caching run) IMMENSELY.
`sudo apt-get install ccache`
`sudo ln -s /usr/bin/ccache /usr/local/bin/gcc`

`sudo ln -s /usr/bin/ccache /usr/local/bin/g++`

`sudo ln -s /usr/bin/ccache /usr/local/bin/cc`

`sudo ln -s /usr/bin/ccache /usr/local/bin/c++`

## Fedora/RedHat

Issue these commands to install the required packages for a Fedora/RedHat system:

`su -`

`yum update`

`yum install gcc-c++ qt4-devel libftdi-devel libusb-devel alsa-lib-devel rpm-build subversion libudev-devel`

Notice that there's a space between su and - and that you need to give the root user password for su. When you're done with these commands, become a normal user again with:

`exit`

## OLA (Open Lighting Architecture)

Acquire the sources

If you're still logged in as root, it's time to stop living dangerously and become a regular user and issue one of the following commands:

If you wish to get the latest released QLC version:
  svn checkout https://qlc.svn.sourceforge.net/svnroot/qlc/tags/qlc-3.2.1 qlc
If you wish to get the very latest bleeding edge (but only if your intention is to do development or are just curious):
  svn checkout https://qlc.svn.sourceforge.net/svnroot/qlc/trunk qlc
This will create a directory called qlc which will contain the latest sources from SVN repository. After you have made the initial check-out and later wish to keep living on the bleeding egde, you can just update the sources (instead of making a new checkout each time):

  cd qlc
  svn update
Compile

Now you have two choices: either go ahead with the compilation and manual installation or, spend a little more time with packages in order to create separate qlc packages that you can easily upgrade (and uninstall) later. If you wish to do everything manually, continue reading. If you wish to create packages for Ubuntu/Debian, skip to the Package Creation section on this page.

Issue the following commands to start building QLC:

  cd qlc
  qmake-qt4
  make
You should see your terminal filling with compiler messages for quite a while. Naturally there shouldn't be any errors, but if you encounter any, please mail me, it's probably just some small detail I've forgotten to include in these instructions.

Install

OK. When the compiler is done, issue this command to install QLC to your system:

  sudo make install
or, for non-sudo systems like Debian, Fedora etc:

  su -c "make install"
Now you're done. Type

  qlc
to start using QLC. If you wish to edit/create fixture definitions, type:

  qlc-fixtureeditor
(At least) on Debian-based systems, the installation script creates desktop menu entries that are usually available in your desktop main menu, under the Other category.

Debian/Ubuntu Package Creation

Go to the newly-created qlc sub-directory and issue the following command:

  ./create-deb.sh
The package is now being built. If the process fails at an early stage, you are probalby missing some dependency package. See above what packages you need to install. When the package script is done, the newly-created packages appear to the folder, where you have the qlc folder, i.e. you need to go up once:

  cd ..
To install the packages, just say:

  su -c "dpkg -i <package name>.deb"
If you're installing QLC 3.2.0-3 on a 32bit Ubuntu environment, you might say for example:

  sudo dpkg -i qlc_3.2.0-3_i386.deb
You can find more information under the topic Debian/Ubuntu installation.

Fedora/RedHat package creation

Go to the newly-created qlc sub-directory and issue the following command:

  ./create-rpm.sh
The script will create an RPM build directory structure under your home directory (~/rpmbuild) and build the packages there. When the packager is done, go and see the newly-created packages:

  cd ~/rpmbuild/RPMS
  ls
To install the packages, just say:

  su -c "rpm -Uvh <package name>.rpm"
To install all packages, you can say:

  su -c "rpm -Uvh qlc*.rpm"
You can find more information from the InstallationRedhat? pages (after they have been written, that is).