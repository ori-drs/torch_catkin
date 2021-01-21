# torch_catkin

This repository provides a catkin wrapper to automatically download and extract Torch in a catkin workspace. Note, since we are directly installing headers and cmake configurations into the root of the workspace, this does not follow proper package isolation. It's fine in devel workspaces and works well out of the box.

## Usage
- Clone and build this repository as part of your workspace
- Include `torch_catkin` from catkin - this internally calls `find_package(Torch REQUIRED)` so the variables are pre-populated


```cmake
find_package(catkin REQUIRED COMPONENTS torch_catkin)

...

add_executable(torch_test src/torch_test.cpp)
target_link_libraries(torch_test ${TORCH_LIBRARIES})
```
