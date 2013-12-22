PROJECT(poco)

cmake_minimum_required( VERSION 2.8.11 )

# FIXME: This is a ugly workaround because cmake handles rpath invalidly.
# See http://public.kitware.com/Bug/view.php?id=13934
set(CMAKE_SKIP_RPATH 1)

# Append our module directory to CMake
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

add_definitions(-s DISABLE_EXCEPTION_CATCHING=0)

set(CMAKE_EXE_LINKER_FLAGS    "${CMAKE_EXE_LINKER_FLAGS} -s DISABLE_EXCEPTION_CATCHING=0")
set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} -s DISABLE_EXCEPTION_CATCHING=0")
set(CMAKE_MODULE_LINKER_FLAGS "${CMAKE_MODULE_LINKER_FLAGS} -s DISABLE_EXCEPTION_CATCHING=0")

option(POCO_STATIC
  "Set to OFF|ON (default is OFF) to control build of POCO as STATIC library" OFF)

# Uncomment from next two lines to force statitc or dynamic library, default is autodetection
if(POCO_STATIC)
    add_definitions( -DPOCO_STATIC -DPOCO_NO_AUTOMATIC_LIBS)    
    set( LIB_MODE STATIC )
    message(STATUS "Building static libraries")
else(POCO_STATIC)
    set( LIB_MODE SHARED )
    message(STATUS "Building dynamic libraries")
endif(POCO_STATIC)

# Set local include path
include_directories(
	Foundation/include
	XML/include
	Util/include
)

add_subdirectory(Foundation)
add_subdirectory(XML)
add_subdirectory(Util)
#add_subdirectory(Zip)

message(STATUS "CMake ${CMAKE_VERSION} successfully configured ${PROJECT_NAME} using ${CMAKE_GENERATOR} generator")
message(STATUS "Installation target path: ${CMAKE_INSTALL_PREFIX}")

message(STATUS "C_FLAGS:  =${CMAKE_C_FLAGS}")
message(STATUS "CXX_FLAGS:=${CMAKE_CXX_FLAGS}")


