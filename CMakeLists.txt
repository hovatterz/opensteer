set(EXECUTABLE_OUTPUT_PATH "${CMAKE_SOURCE_DIR}/bin")
set(LIBRARY_OUTPUT_PATH "${CMAKE_SOURCE_DIR}/lib")
set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake/modules")

cmake_minimum_required(VERSION 2.8)
project(opensteer)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")

find_package(GLUT)
find_package(OpenGL)
if(APPLE)
    SET(CMAKE_CXX_LINK_FLAGS "${CMAKE_CXX_LINK_FLAGS} -framework OpenGL -framework GLUT")
endif(APPLE)

FILE(GLOB OPENSTEER_SRCS "src/*.cpp" "src/*.c")
FILE(GLOB OPENSTEER_PLUGIN_SRCS "plugins/*.cpp")

include_directories("${CMAKE_SOURCE_DIR}/include")
add_library(opensteer ${OPENSTEER_SRCS})

add_executable(example ${OPENSTEER_PLUGIN_SRCS} "example/main.cpp")
target_link_libraries(example opensteer ${OPENGL_LIBRARIES})
