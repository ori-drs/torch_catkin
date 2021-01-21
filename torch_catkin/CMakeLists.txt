cmake_minimum_required(VERSION 3.4)
project(torch_catkin)

find_package(catkin REQUIRED)
include(ExternalProject)

# Important note:
# We are installing the cmake files for torch into the root of "share".
# This is _not_ how isolated workspaces should operate. But it works fine for us here.
ExternalProject_Add(torch_src
  URL "https://download.pytorch.org/libtorch/nightly/cpu/libtorch-cxx11-abi-shared-with-deps-1.4.0%2Bcpu.zip"
  PREFIX ${PROJECT_BINARY_DIR}/libtorch
  UPDATE_COMMAND ""
  CONFIGURE_COMMAND ""
  BUILD_COMMAND ""
  # INSTALL_COMMAND ${CMAKE_COMMAND} -E copy_directory ${PROJECT_BINARY_DIR}/libtorch/src/torch_src/include/ ${CATKIN_DEVEL_PREFIX}/include/${PROJECT_NAME} &&
  #                 ${CMAKE_COMMAND} -E copy_directory ${PROJECT_BINARY_DIR}/libtorch/src/torch_src/lib/ ${CATKIN_DEVEL_PREFIX}/lib &&
  #                 ${CMAKE_COMMAND} -E copy_directory ${PROJECT_BINARY_DIR}/libtorch/src/torch_src/share/cmake/ ${CATKIN_DEVEL_PREFIX}/share/cmake
  #                 #${CMAKE_COMMAND} -E copy_directory ${PROJECT_BINARY_DIR}/libtorch/src/torch_src/share/cmake/ ${CATKIN_DEVEL_PREFIX}/share/${PROJECT_NAME}/cmake
  # Nasty hack (everything in root of workspace) to avoid breaking interfaces:
  INSTALL_COMMAND ${CMAKE_COMMAND} -E copy_directory ${PROJECT_BINARY_DIR}/libtorch/src/torch_src/include/ ${CATKIN_DEVEL_PREFIX}/include &&
                  ${CMAKE_COMMAND} -E copy_directory ${PROJECT_BINARY_DIR}/libtorch/src/torch_src/lib/ ${CATKIN_DEVEL_PREFIX}/lib &&
                  ${CMAKE_COMMAND} -E copy_directory ${PROJECT_BINARY_DIR}/libtorch/src/torch_src/share/cmake/ ${CATKIN_DEVEL_PREFIX}/share/cmake
)

catkin_package(
  CFG_EXTRAS torch_catkin.cmake
)

# TODO: Install!
# install(
#   DIRECTORY ${CATKIN_DEVEL_PREFIX}/include/${PROJECT_NAME}/
#   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
# )
