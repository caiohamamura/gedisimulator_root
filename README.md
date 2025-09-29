[![CMake Cross-Platform Build](https://github.com/caiohamamura/gedisimulator_root/actions/workflows/build.yaml/badge.svg)](https://github.com/caiohamamura/gedisimulator_root/actions/workflows/build.yaml)

# CMake support for building Hancock tooling for GEDI and LVIS

This project allows to build Steven Hancock tools without having to checkout the code and tools yourself.

This project is fully tested with continuous integrated tools as seen from the badge [![CMake Cross-Platform Build](https://github.com/caiohamamura/gedisimulator_root/actions/workflows/build.yaml/badge.svg)](https://github.com/caiohamamura/gedisimulator_root/actions/workflows/build.yaml).

## Requirements

 - cmake > 3.20
 - gdal-dev(el)
 - libhdf5-dev / hdf5-devel
 - gsl-dev(el)

## Building:

```bash
cmake -B build
cmake --build build
```

## Installing

```bash
sudo cmake --install build
```

And it should be ready to use, unless the default cmake install prefix is not added to PATH. But you can also select where you want to install it, for example without the need for root permission:
```
cmake --install build --prefix ~/.local/
```

This version will pack majority of the functionalities into a shared library (since they are) into a libgedisimulator.so or libgedisimulator.dll so you need to make sure the ~/.local/lib is also in any file within /etc/ld.so.conf.d/ and you ran sudo ldconfig if you had to add the new path where to seach for the shared libraries.
By separating into a dedicated SHARED library now most functionalities such as those from libclidar, tools and gediIO.c, etc are all packed within the same SHARED library, so just a few code is new for each binary file mapLidar, collocateWaves, gediRat, gediMetric, only include the code from its specific source, making them slim instead of including everything within each tool in a self-contained binary.
