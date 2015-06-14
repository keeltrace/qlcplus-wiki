## Prepare the build system (MSYS2)

Download the MSYS2 64bit installer from here: https://msys2.github.io/

Follow the instructions of that page otherwise:
Install it using all the defaults (C:\msys64), then open the MSYS2 shell and type:<br>
`pacman --needed -Sy bash pacman pacman-mirrors msys2-runtime
pacman -Su`

Close the MSYS2 shell and open it again.<br>
Now install the packages required to build QLC+, by typing:<br>
`pacman -S make automake autoconf libtool mingw32/mingw-w64-i686-gcc mingw32/mingw-w64-i686-pkg-config
pacman -S mingw32/mingw-w64-i686-qt5 mingw32/mingw-w64-i686-libmad mingw32/mingw-w64-i686-libsndfile mingw32/mingw-w64-i686-flac mingw32/mingw-w64-i686-fftw
`
