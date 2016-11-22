cmake_minimum_required(VERSION 2.8.12 FATAL_ERROR)

project(webcam-lcm-driver)

add_definitions(-Wall -std=c++11)

# transmit webcam to lcm
add_executable(oh-webcam-driver WebcamToLCM.cpp)
pods_use_pkg_config_packages(oh-webcam-driver opencv lcm lcmtypes_bot2-core)
target_link_libraries(oh-webcam-driver)
pods_install_executables(oh-webcam-driver)
