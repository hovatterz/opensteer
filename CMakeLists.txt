set(EXECUTABLE_OUTPUT_PATH "${CMAKE_SOURCE_DIR}/bin")
set(LIBRARY_OUTPUT_PATH "${CMAKE_SOURCE_DIR}/lib")
set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake/modules")

cmake_minimum_required(VERSION 2.8)
project(opensteer)

SET(OPENSTEER_COMPILE_EXAMPLE 		ON CACHE BOOL "Build Example Application")


SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -fpermissive")


find_package(OpenGL REQUIRED)
find_package(GLUT REQUIRED)


if(APPLE)
    SET(CMAKE_CXX_LINK_FLAGS "${CMAKE_CXX_LINK_FLAGS} -framework OpenGL -framework GLUT")
endif(APPLE)

FILE(GLOB OPENSTEER_SRCS "src/*.cpp" "src/*.c")

include_directories("${CMAKE_SOURCE_DIR}/include" ${OPENGL_INCLUDE_DIRS})

add_library(opensteer ${OPENSTEER_SRCS} ${OPENGL_LIBRARIES})

install(
    TARGETS opensteer
    RUNTIME DESTINATION bin COMPONENT bin
    LIBRARY DESTINATION lib COMPONENT bin
    ARCHIVE DESTINATION lib COMPONENT dev
    )
install(DIRECTORY include DESTINATION .)

if(OPENSTEER_COMPILE_EXAMPLE)
    add_subdirectory(example)
endif(OPENSTEER_COMPILE_EXAMPLE)