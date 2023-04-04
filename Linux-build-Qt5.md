### QLC+ Installation from sources on Linux (Debian, Ubuntu, Fedora, RedHat)
### Pre-requisities

You need a number of packages installed before you can compile QLC+ from sources. Everything here happens in the terminal window, so launch one now. Usually it's an entry under Accessories in your desktop main menu.

### Ubuntu/Debian/Mint

Issue these commands to install the required packages for an Ubuntu system:

`sudo apt-get update`<br>
`sudo apt-get install g++ make git build-essential qtchooser qt5-qmake qtbase5-dev qtbase5-dev-tools qtscript5-dev qtmultimedia5-dev libqt5multimedia5-plugins qttools5-dev-tools fakeroot debhelper devscripts pkg-config libxml2-utils libglib2.0-dev libpulse-dev`<br>
`sudo apt-get install libasound2-dev libusb-1.0-0-dev libftdi1-dev libudev-dev libmad0-dev libsndfile1-dev libfftw3-dev`<br>

### Optional helpers

If you intend on doing a lot of development, cleaning often and recompiling everything, you might want to install ccache, which speeds up consequent compilations (after the first caching run) IMMENSELY.<br>
`sudo apt-get install ccache`<br>
`sudo ln -s /usr/bin/ccache /usr/local/bin/gcc`<br>
`sudo ln -s /usr/bin/ccache /usr/local/bin/g++`<br>
`sudo ln -s /usr/bin/ccache /usr/local/bin/cc`<br>
`sudo ln -s /usr/bin/ccache /usr/local/bin/c++`<br>

### Fedora/RedHat

Issue these commands to install the required packages for a Fedora/RedHat system:

`su -`<br>
`yum update`<br>
`yum install gcc-c++ qtbase5-common-devel qtmultimedia5-devel libftdi-devel libusb-devel alsa-lib-devel rpm-build git libudev-devel libsndfile-devel libmad-devel`<br>
`yum install systemd-devel fftw-devel qt5-qtscript-devel qt5-qtmultimedia-devel qt5-qtbase-devel # Fedora 21`

Notice that there's a space between su and - and that you need to give the root user password for su. When you're done with these commands, become a normal user again with:

`exit`

### QLC+ sources

If you wish to get the latest released QLC+ version:<br>
[http://www.qlcplus.org/downloads.html](http://www.qlcplus.org/downloads.html)

If you wish to get the very latest bleeding edge (but only if your intention is to do development or are just curious):
`git clone git://github.com/mcallegari/qlcplus.git`

This will create a directory called qlcplus which will contain the latest sources from GIT repository. After you have made the initial clone and later wish to keep living on the bleeding egde, you can just update the sources (instead of making a new checkout each time):

`cd qlcplus`<br>
`git pull`<br>

### Debug or release mode

If you are a developer and want to contribute to QLC+, the default settings will build a debug version of the program. Please note that a debug version is bigger than a release one and might have worse performances.
If what you need is a production build, then you need to edit the `variables.pri` file and change the following lines, adding a `+=` of the build you need and `-=` of the one you don't need:

`CONFIG         += release # Enable this when making a release`<br>
`CONFIG         -= debug   # Disable this when making a release`

### Plugins build note

QLC+ needs several external dependencies to be compiled with all the plugins support.<br>
If you want to exclude some of them from the build process then just comment them out by placing the character `#` at the beginning of the plugin line in the file `plugins/plugins.pro`
For example:

`#unix:SUBDIRS += ola`

### Build OLA (Open Lighting Architecture)

This step is optional depending if you need OLA or not. See previous paragraph in case you want to disable the OLA plugin.

To build the sources, acquire the latest tarball from [github](https://github.com/OpenLightingProject/ola/releases/latest)

Extract the package and enter into the OLA folder.<br>
Follow the [Linux build instructions](http://www.openlighting.org/ola/linuxinstall). <br>
Then, when build time comes, type:

`./configure --prefix=/usr`<br>
`make`<br>
`sudo make install`<br>

### Compile

Now you have two choices: either go ahead with the compilation and manual installation or, spend a little more time with packages in order to create separate QLC+ packages that you can easily upgrade (and uninstall) later. If you wish to do everything manually, continue reading. If you wish to create packages for Ubuntu/Debian, skip to the Package Creation section on this page.

**Note:** On some distributions, Qt5 is not the default Qt package, so you need to locate the 'qmake' executable in your computer.
For example in Ubuntu 14.04 you can find it in `/usr/lib/x86_64-linux-gnu/qt5/bin`<br>
You can quickly check if the version is correct by typing:
`qmake -v`<br>

In general, you can invoke qmake with its absolute path. For example:
`/home/user/Qt5.14.2/5.14.2/gcc_64/bin/qmake`<br>

In this way you can build QLC+ with any Qt version, located where you prefer in your hard disk.
If you wish to build QLC+ with the latest Qt version, you can get it via online installers available here: https://download.qt.io/official_releases/online_installers/

**Note:** Out-of-tree builds are not tested and most probably do not work.

Issue the following commands to start building QLC+:

`cd qlcplus`<br>
`qmake` (see note above)<br>
`make`<br>

To speed up the build process, if your computer has a multicore CPU you can use the -j option followed by the number of cores of your CPU, like this:

`make -j4`<br>

You should see your terminal filling with compiler messages for quite a while.
Everything should go smoothly until the end. If it doesn't happen and you see misterious building errors try either to clone the repository again or completely clean your source tree and start over again:

`make distclean`<br>
`qmake`<br>
`make`<br>

### Install

OK. When the compiler is done, issue this command to install QLC+ to your system:

`sudo make install`

or, for non-sudo systems like Debian, Fedora etc:

`su -c "make install"`

Now you're done. Type

`qlcplus`

to start using QLC+. If you wish to edit/create fixture definitions, type:

`qlcplus-fixtureeditor`

(At least) on Debian-based systems, the installation script creates desktop menu entries that are usually available in your desktop main menu, under the Other category.

### Debian/Ubuntu Package Creation

Go to the main QLC+ directory and issue the following command:

`./create-deb.sh`

The package is now being built. If the process fails at an early stage, you are probalby missing some dependency package. See above what packages you need to install. When the package script is done, the newly-created packages appear to the folder, where you have the qlc folder, i.e. you need to go up once:

`cd ..`

To install the packages, just type:

`su -c "dpkg -i <package name>.deb"`

### Fedora/RedHat package creation

Go to the newly-created qlc sub-directory and issue the following command:

`./create-rpm.sh`

The script will create an RPM build directory structure under your home directory (~/rpmbuild) and build the packages there. When the packager is done, go and see the newly-created packages:

`cd ~/rpmbuild/RPMS`
`ls`

To install the packages, just type:

`su -c "rpm -Uvh <package name>.rpm"`

To install all packages, you can type:

`su -c "rpm -Uvh qlcplus*.rpm"`

You can find more information from the InstallationRedhat? pages (after they have been written, that is).