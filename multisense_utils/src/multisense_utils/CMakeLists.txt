################################################################
cmake_minimum_required(VERSION 2.8 FATAL_ERROR)
project(multisense_utils)

find_package(PkgConfig REQUIRED)

pkg_check_modules(PCL_IO pcl_io-1.7)
if(PCL_IO_FOUND)
  set(PCL_LIBRARIES  pcl_io-1.7)
  set(PCL_IO_PKG_CONFIG "pcl_io-1.7")
endif()

pkg_check_modules(PCL_IO_1_8 pcl_io-1.8)
if(PCL_IO_1_8_FOUND)
  set(PCL_LIBRARIES  pcl_io-1.8)
  set(PCL_IO_PKG_CONFIG "pcl_io-1.8")
endif()

################################################################
message(STATUS "PCL_IO_PKG_CONFIG={${PCL_IO_PKG_CONFIG}}")


add_library(multisense_utils SHARED multisense_utils.cpp)

pods_use_pkg_config_packages(multisense_utils ${PCL_LIBRARIES} lcm image-utils multisense_image_utils
   opencv lcmtypes_bot2-core)

# set the library API version.  Increment this every time the public API changes.
set_target_properties(multisense_utils PROPERTIES SOVERSION 1)
pods_install_libraries(multisense_utils)
pods_install_headers(multisense_utils.hpp conversions_lcm.hpp DESTINATION multisense_utils)

target_link_libraries(multisense_utils
    z)
pods_install_pkg_config_file(multisense_utils
    LIBS -lmultisense_utils -lz
    REQUIRES image-utils ${PCL_LIBRARIES} opencv multisense_image_utils
    VERSION 0.0.1)

