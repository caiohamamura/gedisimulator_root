[![CMake Cross-Platform Build](https://github.com/caiohamamura/gedisimulator_root/actions/workflows/build.yaml/badge.svg)](https://github.com/caiohamamura/gedisimulator_root/actions/workflows/build.yaml)

# CMake support for building Hancock tooling for GEDI and LVIS

This project allows to build Steven Hancock tools without having to checkout the code and tools yourself. 

This version will pack majority of the functionalities into a shared library (since they are) into a `libgedisimulator.so` or `libgedisimulator.dll`. By separating into a dedicated SHARED library now most functionalities such as those from libclidar, tools and gediIO.c, etc. are all packed within the same SHARED library, so just a few functions are needed for each binary file `mapLidar`, `collocateWaves`, `gediRat`, `gediMetric`, only include the code from its specific source, making them slim instead of including everything within each tool in a self-contained binary.

This is fully tested with continuous integration tools across windows, ubuntu and macos as seen from the badge [![CMake Cross-Platform Build](https://github.com/caiohamamura/gedisimulator_root/actions/workflows/build.yaml/badge.svg)](https://github.com/caiohamamura/gedisimulator_root/actions/workflows/build.yaml).

## Requirements

 - cmake > 3.20
 - gdal-dev(el)
 - libhdf5-dev / hdf5-devel
 - gsl-dev(el)
 - git

## Linux

### Building:

```bash
git clone https://github.com/caiohamamura/gedisimulator_root --depth=1 --recurse-submodules --shallow-submodules
cd gedisimulator_root
cmake -B build
cmake --build build
```

### Installing

```bash
sudo cmake --install build
```

And it should be ready to use, unless the default cmake install prefix is not added to PATH. But you can also select where you want to install it, for example without the need for root permission:
```
cmake --install build --prefix ~/.local/
```

In linux you need to make sure the `~/.local/lib` is also in any file within `/etc/ld.so.conf.d/` and you ran `sudo ldconfig` if you had to add the new path where to seach for the shared libraries.

## Windows:

For windows you could either use rtools bash, msys2, or even better `Visual Studio Build Tools 2022` with vcpkg. 

In Windows 11 you could run:

```powershell
winget install Microsoft.VisualStudio.2022.BuildTools --force --override "--wait --passive --add Microsoft.VisualStudio.Component.VC.Tools.x86.x64 --add Microsoft.VisualStudio.Component.Windows11SDK.22621"
winget install Kitware.CMake Git.Git
```

Now open Developer Powershell for VS 2022 or Developer Command Prompt for VS 2022 and `cd` to whatever folder you want to download and build everything. Then run:

```
git clone https://github.com/microsoft/vcpkg --depth=1
git clone https://github.com/caiohamamura/gedisimulator_root --depth=1 --recurse-submodules --shallow-submodules
cd gedisimulator_root
cmake -B build -DCMAKE_TOOLCHAIN_FILE="../vcpkg/scripts/buildsystems/vcpkg.cmake"
cmake --build build
cmake --install build --prefix .
```

Downloading all dependencies may take a while, be patient. Everything will be installed within `bin` folder.


