# QLC+ 5 build instructions

Building QLC+ 5 is very similar to building QLC+ 4.<br>
However, the minimum Qt version required is 5.14.2. <br>
It is recommended to use the official Qt versions available here: https://www.qt.io/download-open-source/<br>

Notes about Qt:
* Qt 6.x build is not yet supported!
* Qt 5.15.x on Linux misses a Qt3D plugin, so meshes will not be loaded. Use Qt 5.14.2 instead.

The environment preparation is the same explained for [Linux](https://github.com/mcallegari/qlcplus/wiki/Linux-build-Qt5), [macOS](https://github.com/mcallegari/qlcplus/wiki/OSX-build-Qt5) and [Windows](https://github.com/mcallegari/qlcplus/wiki/Windows-Build-Qt5).

When it comes the time to invoke `qmake`, add the `CONFIG+=qmlui` option.
Examples:

## Windows: 

`qmake CONFIG+=qmlui`<br>
`make`<br>
`make install` (binaries will go to `C:\qlcplus`)

## macOS:

`export QTDIR=/Users/myuser/Qt5.10.1/5.10.1/clang_64`<br>
`$QTDIR/bin/qmake CONFIG+=qmlui`<br>
`make`<br>
`make install` (binaries will be bundled into `/Users/myuser/QLC+.app`)

**or**

`export QTDIR=/Users/myuser/Qt5.14.2/5.14.2/clang_64`<br>
`./create-dmg.sh CONFIG+=qmlui`<br>

## Linux:

`/home/myuser/Qt5.14.2/5.14.2/gcc_64/bin/qmake CONFIG+=qmlui`<br>
`make`<br>
`make install` (binaries will be installed in your system. **Warning**: this will overwrite QLC+ 4)

**or**

`export QTDIR=/home/myuser/Qt5.14.2/5.14.2/gcc_64`<br>
`./create-appimage.sh` (a file called `Q_Light_Controller_Plus-x86_64.AppImage` will be created in `/home/myuser`)

P.S. Obviously replace `myuser` with the name of your *nix user !