cmake_minimum_required(VERSION 2.8.3)
project(plugin)

find_package(PythonLibs REQUIRED)
include_directories(${PYTHON_INCLUDE_DIRS})

find_package(catkin REQUIRED COMPONENTS
    pybind11_catkin)

catkin_python_setup()

catkin_package(
    LIBRARIES
    CATKIN_DEPENDS pybind11_catkin
)


add_library(base_plugin SHARED src/base_plugin.cpp)

pybind_add_module(py_base_plugin MODULE src/py_base_plugin.cpp)

pybind_add_module(plugin_wrapper SHARED src/plugin_wrapper.cpp )
add_executable(plugin_runner src/plugin_runner.cpp)
target_link_libraries(plugin_runner ${PYTHON_LIBRARIES} plugin_wrapper base_plugin)
