# QLC+ 5 build instructions

Building QLC+ 5 is very similar to building QLC+ 4.<br>
However, the minimum Qt version required is 6.8.0. <br>
It is recommended to use the official Qt versions via [online installer](https://download.qt.io/official_releases/online_installers)<br>

Notes about Qt:

* Qt 6.8.2 and higher won't play audio files on Windows because of [QTBUG-136057](https://bugreports.qt.io/browse/QTBUG-136057)

The environment preparation is the same explained for [Linux](https://github.com/mcallegari/qlcplus/wiki/Linux-build-(Qt5-&-cmake)), [Windows](https://github.com/mcallegari/qlcplus/wiki/Windows-Build-(Qt5-&-cmake)) and [macOS](https://github.com/mcallegari/qlcplus/wiki/macOS-build-Qt5).

On Linux, add the following development packages:<br>
`sudo apt install qt3d5-dev qt3d-defaultgeometryloader-plugin qt3d-assimpsceneimport-plugin qml-module-qt3d qml-module-qtquick-scene3d qml-module-qtmultimedia`<br>


When it comes the time to invoke `cmake`, add the `-Dqmlui=ON` option.
Examples:

## Windows: 

`cmake -Dqmlui=ON ..`<br>
`ninja`<br>
`ninja install` (binaries will go to `C:\qlcplus`)

## macOS:

`export QTDIR=/Users/myuser/Qt/6.8.1/clang_64`<br>
`$QTDIR/bin/qmake CONFIG+=qmlui`<br>
`make`<br>
`make install` (binaries will be bundled into `/Users/myuser/QLC+.app`)

**or**

`export QTDIR=/Users/myuser/Qt/6.8.1/clang_64`<br>
`./create-dmg.sh CONFIG+=qmlui`<br>

## Linux:

`cmake -DCMAKE_PREFIX_PATH="/home/myuser/Qt/6.8.1/gcc_64/lib/cmake" -Dqmlui=ON ..`<br>
`make`<br>
`make install` (binaries will be installed in your system. **Warning**: this will overwrite QLC+ 4)

**or**

`export QTDIR=/home/myuser/Qt/6.8.1/gcc_64`<br>
`./create-appimage-cmake.sh` (a file called `Q_Light_Controller_Plus-x86_64.AppImage` will be created in `/home/myuser`)

P.S. Obviously replace `myuser` with the name of your *nix user !