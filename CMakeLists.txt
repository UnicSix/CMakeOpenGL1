cmake_minimum_required(VERSION 3.20 FATAL_ERROR)

set( CMAKE_EXPORT_COMPILE_COMMANDS ON )
set( CMAKE_CXX_FLAGS "-g" )
project( CMakeOpenGL1 )

set( CMakeOpenGL1_SRC src/*.cpp )

file( GLOB_RECURSE CMakeOpenGL1_SRC "src/*.cpp" )
file( GLOB_RECURSE IMGUI_SRC "/src/vender/imgui/i*.cpp" )
#file( GLOB_RECURSE CMakeOpenGL1_TEST "src/test/*.cpp" )

add_executable( cmake-opengl
	src/vender/stb_image/stb_image.cpp
	${IMGUI_SRC}
	${CMakeOpenGL1_SRC}
)

include_directories( "src/" )
include_directories( "src/vender" )
include_directories( "Dependencies/glm" )
include_directories( "src/vender/imgui" )

set_property(TARGET cmake-opengl PROPERTY CXX_STANDARD 17)
target_compile_options( cmake-opengl PRIVATE -Wall )

add_definitions(-DGLEW_STATIC)
add_subdirectory(Dependencies/glfw EXCLUDE_FROM_ALL)
add_subdirectory(Dependencies/glew EXCLUDE_FROM_ALL)
add_subdirectory(Dependencies/glm EXCLUDE_FROM_ALL)

target_link_libraries(cmake-opengl
  PRIVATE glfw
  PRIVATE libglew_static
  PRIVATE glm
)

configure_file(
	${CMAKE_CURRENT_SOURCE_DIR}/src/asset.hpp.in
	${CMAKE_CURRENT_BINARY_DIR}/src/asset.hpp
)

target_include_directories(cmake-opengl
  PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/src
  PRIVATE ${CMAKE_CURRENT_BINARY_DIR}/src
)
