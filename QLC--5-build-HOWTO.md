# QLC+ 5 build instructions

Building QLC+ 5 is very similar to building QLC+ 4.
However, the minimum Qt version required is 5.9.4. 
It is recommended to use the official version available here: https://www.qt.io/download-open-source/

The environment preparation is the same explained for [Linux](https://github.com/mcallegari/qlcplus/wiki/Linux-build-Qt5), [macOS](https://github.com/mcallegari/qlcplus/wiki/OSX-build-Qt5) and [Windows](https://github.com/mcallegari/qlcplus/wiki/Windows-Build-Qt5).

When it comes the time to invoke `qmake`, add the `CONFIG+=qmlui` option.
Examples:

Windows: 

`qmake CONFIG+=qmlui`<br>
`make`<br>
`make install` (binaries will go to C:\qlcplus)

macOS:

`export QTDIR=/Users/myuser/Qt5.9.4/5.9.4/clang_64`<br>
`/Users/myuser/projects/Qt5.9.4/5.9.4/clang_64/bin/qmake CONFIG+=qmlui`<br>
`make`<br>
`make install` (binaries will be bundled into /Users/myuser/QLC+.app)<br>
or
`export QTDIR=/Users/myuser/Qt5.9.4/5.9.4/clang_64`<br>
`./create-dmg.sh CONFIG+=qmlui`<br>

Linux:

`/home/myuser/projects/Qt5.9.4/5.9.4/gcc_64/bin/qmake CONFIG+=qmlui`<br>
`make`<br>
`make install` (binaries will be installed in your system. **Warning**: this will overwrite QLC+ 4)<br>
or
`export QTDIR=/home/myuser/projects/Qt5.9.4/5.9.4/gcc_64`<br>
`./create-appimage.sh` (a file called `Q_Light_Controller_Plus-x86_64.AppImage` will be created in /home/myuser)
