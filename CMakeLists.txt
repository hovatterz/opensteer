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

include_directories("${CMAKE_SOURCE_DIR}/include")
add_library(opensteer ${OPENSTEER_SRCS})

install(
    TARGETS opensteer
    RUNTIME DESTINATION bin COMPONENT bin
    LIBRARY DESTINATION lib COMPONENT bin
    ARCHIVE DESTINATION lib COMPONENT dev
    )
install(DIRECTORY include DESTINATION .)

add_subdirectory(example)
