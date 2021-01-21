cmake_minimum_required(VERSION 3.0.2)
project(torch_catkin_test)

find_package(catkin REQUIRED COMPONENTS
  torch_catkin
)

# TODO: Add a C++ test... but the above already resolves all paths and checks what includes can be found as well.
