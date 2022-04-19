# inspectrum-windows-x86_64-build

## Requirements for inspectrum:
* cmake >= 3.1 (explicitly installed this and ninja)
* fftw 3.x	(explicitly installed)
* liquid-dsp >= v1.3.0 (found pre-compiled libraries)
* pkg-config (did not explicitly install this)
* qt5 (explicitly installed the static library)


## get MSYS2 here https://www.msys2.org/
following instructions - I used the defaul options

## From MSYS2 "Base" application configure the needed packages

```
pacman -Syu
pacman -Su
pacman -S mingw-w64-x86_64-toolchain git mingw-w64-x86_64-qt5-static mingw-w64-x86_64-fftw
pacman -S mingw-w64-x86_64-cmake mingw-w64-x86_64-ninja
git clone https://github.com/miek/inspectrum.git
git clone https://github.com/cjcliffe/CubicSDR.git
```

Get liquid-dsp precomplied library below and copy the header and library files into the following locations

```
git clone https://github.com/cjcliffe/CubicSDR.git
cp C:\msys64\home\craig\CubicSDR\external\liquid-dsp\include\liquid\liquid.h C:\msys64\mingw64\include
cp C:\msys64\home\craig\CubicSDR\external\liquid-dsp\gcc\64\libliquid.a C:\msys64\mingw64\lib
```


## From MinGW x64 application (the blue one) build the program:

```
cd inspectrum/
cd build/
cmake -G Ninja ..
find / -iname Qt5WidgetsConfig.cmake
export Qt5Widgets_DIR=/mingw64/qt5-static/lib/cmake/Qt5Widgets
cmake -G Ninja ..
find / -iname Qt5ConcurrentConfig.cmake
export Qt5Concurrent_DIR=/mingw64/qt5-static/lib/cmake/Qt5Concurrent
cmake -G Ninja ..
cmake --build .
cd src
cp /mingw64/bin/zlib1.dll .
cp /mingw64/bin/libzstd.dll .
cp /mingw64/bin/libwinpthread-1.dll .
cp /mingw64/bin/libstdc++-6.dll .
./inspectrum
```

Trying to run inspectrum with gave some errors as some dlls are not found. TODO: static link these so that they don't have to "travel" with program

```
cp /mingw64/bin/zlib1.dll .
cp /mingw64/bin/libzstd.dll .
cp /mingw64/bin/libwinpthread-1.dll .
cp /mingw64/bin/libstdc++-6.dll .
cp /mingw64/bin/libgcc_s_seh-1.dll .
```
