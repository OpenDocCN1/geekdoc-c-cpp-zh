# **Listing A.5** An example *CMake* script for generating simple application projects for different OSS (in *EmptyPro*, CMakeLists.txt).

```
```cmake
cmake_minimum_required( VERSION 3.6.2 )

# For a new project it is sufficient to change only its name in the following line
set( PROJECT_NAME EmptyPro )

project( ${PROJECT_NAME} )

set( CMAKE_BUILD_TYPE Debug )
#set( CMAKE_BUILD_TYPE Release )

if( WIN32 )
    set( CMAKE_CXX_FLAGS "/DWIN32 /D_WINDOWS /W3 /GR /EHsc /std:c++17 /D_UNICODE /DUNICODE" )
    set( CMAKE_CXX_FLAGS_DEBUG "/Md /Zi /Ob0 /Od /RTC1 /std:c++17 /D_UNICODE /DUNICODE" )
    message( "Win settings chosen..." )
elseif( ${CMAKE_SYSTEM_NAME} STREQUAL "Darwin" )
    set( CMAKE_CXX_FLAGS "-std=c++17 -Wall" )
    set( CMAKE_CXX_FLAGS_DEBUG "-g -std=c++17 -Wall" )
    message( "Mac settings chosen..." )
elseif( UNIX )
    set( CMAKE_CXX_FLAGS "-std=c++17 -Wall" )
    set( CMAKE_CXX_FLAGS_DEBUG "-g -std=c++17 -Wall" )
    message( "Linux settings chosen..." )
endif()

# Inform CMake where the header files are
include_directories( include )

# Automatically add all *.cpp and *.h files to the project
file( GLOB SOURCES "./src/*.cpp" "./include/*.h" )
add_executable( ${PROJECT_NAME} ${SOURCES} )

# Set the default project
set_property( DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT ${PROJECT_NAME} )

message( "CMAKE BUILD TYPE is ${CMAKE_BUILD_TYPE}" )
```
```

Line [1] is a clause for a minimal version of *CMake*. The project name is defined on line [4]. For simple projects, and assuming the same directory structure, this is the only one line you will need to modify by entering the name of your project. We will do this in a moment for the *EasyMatrix* project. Lines [8–9] choose a *Debug* or *Release* project version. Notice that in CMake, # is used to enter a comment: this can be used to temporarily comment out a line that may be useful later. Lines [11–23] contain command-line options for various compiler calls. This is the most technical part of our script, which requires knowledge of a particular compiler setup. But once set, these can be used with no further interference. A deeper explanation can be found in the *CMake* documentation.

Line [27] instructs the *CMake* project generator to look for header files in the *include* directory. Similarly, lines [31–32] make *CMake* pull in all source files, i.e. files with the *cpp* extension, from