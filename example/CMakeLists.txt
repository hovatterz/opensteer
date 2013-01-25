add_definitions(-DOPENSTEERDEMO=true)
include_directories("${CMAKE_SOURCE_DIR}/example")

FILE(GLOB OPENSTEER_EXAMPLE_SRCS "./*.cpp")
FILE(GLOB OPENSTEER_PLUGIN_SRCS "../plugins/*.cpp")

add_executable(example ${OPENSTEER_PLUGIN_SRCS} ${OPENSTEER_EXAMPLE_SRCS})
target_link_libraries(example opensteer ${OPENGL_LIBRARIES})
