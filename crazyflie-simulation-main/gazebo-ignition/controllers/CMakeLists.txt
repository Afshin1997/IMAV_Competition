cmake_minimum_required(VERSION 3.10.2 FATAL_ERROR)

find_package(ignition-cmake2 REQUIRED)

project(CrazyflieController)

find_package(ignition-plugin1 REQUIRED COMPONENTS register)
set(IGN_PLUGIN_VER ${ignition-plugin1_VERSION_MAJOR})

find_package(ignition-gazebo6 REQUIRED)
add_library(CrazyflieController SHARED CrazyflieController.cc)
target_link_libraries(CrazyflieController
  PRIVATE ignition-plugin${IGN_PLUGIN_VER}::ignition-plugin${IGN_PLUGIN_VER}
  PRIVATE ignition-gazebo6::ignition-gazebo6  )
