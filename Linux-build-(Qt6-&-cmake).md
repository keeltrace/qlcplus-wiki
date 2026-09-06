### QLC+ Installation from sources on Linux (Debian, Ubuntu, Fedora, RedHat)
### Pre-requisities

You need a number of packages installed before you can compile QLC+ from sources. Everything here happens in the terminal window, so launch one now. Usually it's an entry under Accessories in your desktop main menu.

### Ubuntu/Debian/Mint

If you plan to use the system/distribution-provided Qt packages, Ubuntu 22.04 Jammy Jellyfish or Debian 12 Bookworm are the minimum requirement since they first introduced Qt6.

Issue these commands to install the required packages for an Ubuntu system:

```shell
sudo add-apt-repository universe
sudo apt update
sudo apt install git build-essential g++ make cmake
sudo apt install debhelper devscripts fakeroot pkg-config

sudo apt install libglx-dev libgl1-mesa-dev

sudo apt install qt6-base-dev qt6-declarative-dev qt6-multimedia-dev qt6-tools-dev qt6-tools-dev-tools qt6-l10n-tools

sudo apt install libqt6serialport6-dev libqt6svg6-dev libqt6websockets6-dev  # (only < Ubuntu 23.04 Lunar)
sudo apt install qt6-serialport-dev qt6-svg-dev qt6-websockets-dev  # (only >= Ubuntu 23.04 Lunar, Debian)

sudo apt install libasound2-dev libftdi-dev libftdi1-dev libfftw3-dev libsndfile1-dev libudev-dev libusb-dev libusb-1.0-0-dev libxkbcommon-dev

sudo apt install libmad0-dev  # (only < Ubuntu 23.04 Lunar, < Debian 12 Bookworm)

sudo apt install libxml2-utils python-is-python3 python3-lxml  # to run "make check"

sudo apt install gstreamer1.0-libav  # h264 video playback

# might be needed to make "lupdate" run on dual Qt5/Qt6 systems
# sudo rm -f /usr/bin/lrelease
# sudo ln -s /usr/lib/qt6/bin/lrelease /usr/bin/lrelease
```

### Fedora/RedHat (TODO)

Issue these commands to install the required packages for a Fedora/RedHat system:

```shell
su -
yum update
yum install gcc-c++ qtbase5-common-devel qtmultimedia5-devel libftdi-devel libusb-devel alsa-lib-devel rpm-build git libudev-devel libsndfile-devel libmad-devel
yum install systemd-devel fftw-devel qt5-qtscript-devel qt5-qtmultimedia-devel qt5-qtbase-devel # Fedora 21
```

Notice that there's a space between su and - and that you need to give the root user password for su. When you're done with these commands, become a normal user again with:

```shell
exit
```

### QLC+ sources

If you wish to get the latest released QLC+ version:<br>
[https://github.com/mcallegari/qlcplus/releases/latest/](https://github.com/mcallegari/qlcplus/releases/latest/)

If you wish to get the very latest bleeding edge (but only if your intention is to do development or are just curious):

```shell
git clone https://github.com/mcallegari/qlcplus.git
```

This will create a directory called `qlcplus` which will contain the latest sources from GIT repository. After you have made the initial clone and later wish to keep living on the bleeding egde, you can just update the sources (instead of making a new checkout each time):

```shell
cd qlcplus
git pull
```

### Debug or release mode

If you are a developer and want to contribute to QLC+, the default settings will build a debug version of the program. Please note that a debug version is bigger than a release one and might have worse performances.
If what you need is a production build, then you need to edit the main `CMakeLists.txt` file and change the line starting with<br>

```cmake
set(CMAKE_BUILD_TYPE "Release" ... )
```

Switch between `Debug` and `Release` depending on your needs.

### Plugins build note

QLC+ needs several external dependencies to be compiled with all the plugins support.<br>
If you want to exclude some of them from the build process then just comment them out by placing the character `#` at the beginning of the plugin line in the file `plugins/CMakeLists.txt`
For example:

```cmake
# add_subdirectory(ola)
```

### Build OLA (Open Lighting Architecture) (TODO)

This step is optional depending if you need OLA or not. See previous paragraph in case you want to disable the OLA plugin.

To build the sources, acquire the latest tarball from [GitHub](https://github.com/OpenLightingProject/ola/releases/latest)

Extract the package and enter into the OLA folder.<br>
Follow the [Linux build instructions](https://www.openlighting.org/ola/linuxinstall/). <br>
Then, when build time comes, type:

```shell
./configure --prefix=/usr
make
sudo make install
```

### Playback of MPEG audio files (e.g. MP3)

QLC+ uses `libsndfile` to decode and play audio files. However, `libsndfile` only supports MPEG files from version 1.1.0+.
Older, but still supported OS versions (e.g. < Ubuntu 23.04 Lunar, < Debian 12 Bookworm) only offer `libsndfile` in a version below this version.

Therefore, if playback of MPEG audio files is required, `libmad` is needed (hence the above installation).
To use it with QLC+, you need to enable the `mad` plugin of the QLC+ engine before compiling by applying this patch (partially reverting [0359dd921](https://github.com/mcallegari/qlcplus/commit/0359dd921c5717eb49cafc58fd707814ef691b13)):

<details>
  <summary>Patch</summary>

```diff
diff --git a/debian/control b/debian/control
index a4a65ad92..c5e87c959 100644
--- a/debian/control
+++ b/debian/control
@@ -8,6 +8,7 @@ Build-Depends:
  libasound2-dev (>= 1.0.16),
  libfftw3-dev,
  libftdi1-dev (>= 0.17),
+ libmad0-dev,
  libsndfile1-dev,
  qtbase5-dev, qtscript5-dev,
  qtmultimedia5-dev, libqt5serialport5-dev,
@@ -29,6 +30,7 @@ Depends:
  ${shlibs:Depends},
  ${misc:Depends},
 Recommends:
+ libmad0,
  libsndfile1,
  libqt5multimedia5-plugins,
 Description: Q Light Controller Plus - The open DMX lighting desk
diff --git a/debian/rules b/debian/rules
index 72faf000a..6de9e0987 100755
--- a/debian/rules
+++ b/debian/rules
@@ -14,7 +14,7 @@ override_dh_auto_configure:
 	#dh_auto_configure -- -Dqmlui=on
 
 override_dh_shlibdeps:
-	dh_shlibdeps -Xlibsndfileplugin.so -Xlibolaio.so
+	dh_shlibdeps -Xlibmadplugin.so -Xlibsndfileplugin.so -Xlibolaio.so
 
 override_dh_install:
 	dh_install
diff --git a/engine/audio/plugins/CMakeLists.txt b/engine/audio/plugins/CMakeLists.txt
index b9bb778e2..e9a54a0e5 100644
--- a/engine/audio/plugins/CMakeLists.txt
+++ b/engine/audio/plugins/CMakeLists.txt
@@ -1,10 +1,10 @@
 project(plugins)
 
 if((((NOT ANDROID AND NOT IOS))))
-#    pkg_check_modules(MAD IMPORTED_TARGET mad)
-#    if(${MAD_FOUND})
-#        add_subdirectory(mad)
-#    endif()
+    pkg_check_modules(MAD IMPORTED_TARGET mad)
+    if(${MAD_FOUND})
+        add_subdirectory(mad)
+    endif()
 
     pkg_check_modules(SNDFILE IMPORTED_TARGET sndfile)
     if(${SNDFILE_FOUND})
diff --git a/engine/audio/plugins/sndfile/audiodecoder_sndfile.cpp b/engine/audio/plugins/sndfile/audiodecoder_sndfile.cpp
index 36ccbfa8d..9205c8828 100644
--- a/engine/audio/plugins/sndfile/audiodecoder_sndfile.cpp
+++ b/engine/audio/plugins/sndfile/audiodecoder_sndfile.cpp
@@ -149,8 +149,6 @@ QStringList AudioDecoderSndFile::supportedFormats()
             caps << "*.oga" << "*.ogg";
         else if (ext == "wav" && !caps.contains("*.wav"))
             caps << "*.wav";
-        else if (ext == "mp3" && !caps.contains("*.mp3"))
-            caps << "*.mp3";
     }
 
     return caps;
diff --git a/platforms/linux/qlcplus.spec b/platforms/linux/qlcplus.spec
index fab4ac10f..c76f5b36e 100644
--- a/platforms/linux/qlcplus.spec
+++ b/platforms/linux/qlcplus.spec
@@ -18,7 +18,7 @@ BuildRequires:  pkgconfig(fftw3)
 BuildRequires:  pkgconfig(libftdi1)
 BuildRequires:  pkgconfig(libola)
 BuildRequires:  pkgconfig(libudev)
-#BuildRequires:  pkgconfig(mad)
+BuildRequires:  pkgconfig(mad)
 BuildRequires:  pkgconfig(sndfile)
 %if %{defined fedora}
 BuildRequires:  pkgconfig(libusb-1.0)
@@ -121,7 +121,7 @@ desktop-file-validate %{buildroot}/%{_datadir}/applications/*.desktop
 %else
 %{_datadir}/qlcplus/web
 %endif
-#%_libdir/qt5/plugins/qlcplus/audio/libmadplugin.so
+%_libdir/qt5/plugins/qlcplus/audio/libmadplugin.so
 %_libdir/qt5/plugins/qlcplus/audio/libsndfileplugin.so
 %_libdir/qt5/plugins/qlcplus/libartnet.so
 %_libdir/qt5/plugins/qlcplus/libdmx4linux.so
diff --git a/platforms/macos/CMakeLists.txt b/platforms/macos/CMakeLists.txt
index 6e7286f33..8cc43d60c 100644
--- a/platforms/macos/CMakeLists.txt
+++ b/platforms/macos/CMakeLists.txt
@@ -133,7 +133,7 @@ install(FILES ${FFTW3_LIBDIR}/${FFTW_LIBNAME} DESTINATION ${INSTALLROOT}/${LIBSD
 install(FILES ${LIBFTDI1_libftdi1_LIBDIR}/libftdi1.2.dylib DESTINATION ${INSTALLROOT}/${LIBSDIR})
 install(FILES ${LIBFTDI1_libftdi1_LIBDIR}/libftdi1.2.5.0.dylib DESTINATION ${INSTALLROOT}/${LIBSDIR})
 install(FILES ${LIBUSB1_LIBDIR}/libusb-1.0.0.dylib DESTINATION ${INSTALLROOT}/${LIBSDIR})
-#install(FILES ${MAD_LIBDIR}/libmad.0.dylib DESTINATION ${INSTALLROOT}/${LIBSDIR})
+install(FILES ${MAD_LIBDIR}/libmad.0.dylib DESTINATION ${INSTALLROOT}/${LIBSDIR})
 install(FILES ${SNDFILE_LIBDIR}/libsndfile.1.dylib DESTINATION ${INSTALLROOT}/${LIBSDIR})
 install(FILES ${SNDFILE_LIBDIR}/libsndfile.1.0.37.dylib DESTINATION ${INSTALLROOT}/${LIBSDIR})
 
diff --git a/platforms/windows/CMakeLists.txt b/platforms/windows/CMakeLists.txt
index 41689084d..454beaaf7 100644
--- a/platforms/windows/CMakeLists.txt
+++ b/platforms/windows/CMakeLists.txt
@@ -23,6 +23,7 @@ install(FILES ${msys_files} DESTINATION ${msys_path})
 
 # audio libraries
 set(mmedia_path "${INSTALLROOT}/${LIBSDIR}")
+copy_system_library(mmedia_files "libmad-0.dll")
 copy_system_library(mmedia_files "libogg-0.dll")
 copy_system_library(mmedia_files "libopus-0.dll")
 copy_system_library(mmedia_files "libmp3lame-0.dll")
```
</details>

### Support for GPIO access

QLC+ supports direct access to the device's GPIO pins, if available (e.g. on a Raspberry Pi), via `libgpiod`.

On an Ubuntu/Debian system, this dependency can be easily installed with the following command:

```shell
sudo apt install libgpiod-dev
```

**Important:** Breaking changes have been made to the `libgpiod` API in recent years. QLC+ (or more precisely, its `gpio` plugin) previously only supported the old API (`libgpiod` v.1.6.x and below; found on <= Ubuntu 24.10 Oracular Oriole, <= Debian 11 Bullseye, Debian 12 Bookworm without backports), but nowadays (since [22913325d](https://github.com/mcallegari/qlcplus/commit/22913325df0e65b390fb317b8d5eb7d5debfaea7)) it only supports the new one (`libgpiod` v.2.x and above; found on >= Ubuntu 25.04 Plucky Puffin, >= Debian 13 Trixie, Debian 12 Bookworm with backports). You can try to revert the above commit at your own risk, if support for `libgpiod` v.1.6.x or below is required.

### Compile

Now you have two choices: either go ahead with the compilation and manual installation or, spend a little more time with packages in order to create separate QLC+ packages that you can easily upgrade (and uninstall) later. If you wish to do everything manually, continue reading. If you wish to create packages for Ubuntu/Debian, skip to the Package Creation section on this page.

If you wish to build QLC+ with the latest Qt version, you can get it via online installers available here: https://download.qt.io/official_releases/online_installers/

**Note:** Out-of-tree builds are not tested and most probably do not work.

Issue the following commands to start building QLC+:

```shell
cd qlcplus
mkdir build && cd build
```

To build with an official Qt package issue the following:

```shell
cmake -DCMAKE_PREFIX_PATH="/home/<user>/Qt/6.9.3/gcc_64/lib/cmake" ..
```

To build with the system Qt package run the following:

```shell
cmake -DCMAKE_PREFIX_PATH="/usr/lib/x86_64-linux-gnu/cmake/Qt6" ..
```

Then finally type

```shell
make
```

To speed up the build process, if your computer has a multicore CPU, you can use the `-j` option followed by the number of cores of your CPU, like this:

```shell
make -j4
```

You should see your terminal filling with compiler messages and a completion percentage for quite a while.
Everything should go smoothly until the end. If it doesn't happen and you see misterious building errors, try either to clone the repository again or completely clean your source tree and start over again by deleting the `build` folder and creating it again.

### Install

OK. When the compiler is done, issue this command to install QLC+ to your system:

```shell
sudo make install
```

or, for non-sudo systems like Debian, Fedora etc:

```shell
su -c "make install"
```

Now you're done. Type

```shell
qlcplus
```

to start using QLC+. If you wish to edit/create fixture definitions, type:

```shell
qlcplus-fixtureeditor
```

(At least) on Debian-based systems, the installation script creates desktop menu entries that are usually available in your desktop main menu, under the Other category.

### Debian/Ubuntu Package Creation (TODO)

From the build folder, issue the following command:

```shell
cpack -G DEB
```

The package is now being built. If the process fails at an early stage, you are probably missing some dependency package. See above what packages you need to install. When the package script is done, the newly-created packages appear to the folder, where you have the qlcplus folder, i.e. you need to go up once:

```shell
cd ..
```

To install the packages, just type:

```shell
su -c "dpkg -i <package name>.deb"
```

### Fedora/RPM package creation (TODO)

The old wiki instructions referenced `create-rpm.sh`, but that script is no longer present in the current QLC+ tree and should not be used as a Qt 6 packaging recipe. The current top-level CMake configuration enables the DEB CPack generator only.

QLC+ still contains `platforms/linux/qlcplus.spec`, but that spec currently describes the older Qt 5/qmake layout. In particular, current CMake installs libraries using GNUInstallDirs and builds the plugin path from the detected Qt major version, so copying the old hard-coded `qt5` RPM file list would produce an incorrect package.

Until the RPM spec is ported and tested against the Qt 6/CMake build, build and install QLC+ from source using the instructions above. A future RPM packaging update should, at minimum:

- port `platforms/linux/qlcplus.spec` from qmake/Qt 5 to CMake/Qt 6;
- use Fedora RPM macros/GNUInstallDirs for architecture-dependent library paths;
- package plugins from the Qt-major-aware QLC+ plugin directory rather than a hard-coded `qt5` path;
- verify the resulting RPM contents on a current Fedora release before documenting installation commands here.
