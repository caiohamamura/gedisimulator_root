cmake_minimum_required(VERSION 3.24)
project(gedisimulator_root C)

include(FetchContent)

FetchContent_Declare(
  cmpfit
  URL https://pages.physics.wisc.edu/~craigm/idl/down/cmpfit-1.5.zip
  URL_HASH SHA256=0DB86E2FD7D40FCEA9BF638ACE7951F7BCCA955F31CB9AE4D32190CF616DC338
  DOWNLOAD_EXTRACT_TIMESTAMP FALSE
  DOWNLOAD_NO_PROGRESS FALSE
)

FetchContent_MakeAvailable(cmpfit)

set(CMPFIT_ROOT ${cmpfit_SOURCE_DIR} CACHE STRING "Path for MPFIT: https://pages.physics.wisc.edu/~craigm/idl/cmpfit.html")

# Use modern target-based approach instead of include_directories
add_subdirectory(gedisimulator)
