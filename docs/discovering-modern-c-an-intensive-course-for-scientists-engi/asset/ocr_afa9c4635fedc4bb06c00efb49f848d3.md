If we change mesher.cpp, the next build process only generates targets depending on it:

```
g++ mesher.cpp -c -o mesher.o
ar cr libmesher.a mesher.o
g++ fluxer.o libmesher.a libsolver.a -o fluxer
```

By convention, the first target not starting with a dot is considered the default target:

```
all: fluxer
```

so we can just write make.

# 7.2.2.2 CMake

```
=> buildtools/CMakeLists.txt
```

CMake is a tool of higher abstraction than make as we will demonstrate in this section. Our build project is specified here in a file named CMakeLists.txt. It typically starts with declaring which tool version is needed and naming a project:

```
cmake_minimum_required (VERSION 2.6)
project (Fluxer)
```

Generating a new library is easily done by just declaring its sources:

```
add_library(solver solver.cpp)
```

Which commands are used and how they are parameterized is decided by CMake unless we insist on more detailed specification. A library with dynamic linkage can be generated as easily:

```
add_library(mesher SHARED mesher.cpp)
```

Our final goal is the creation of the fluxer application that is linked against these two libraries:

```
add_executable(fluxer fluxer.cpp)
target_link_libraries(fluxer solver mesher)
```

It is good practice to build CMake projects in separate directories so that we can toss all generated files at once. One typically creates a sub-directory named build and runs all commands there:

```
cd build
cmake ..
```

Now CMake searches for compilers and other tools, including their flags:

```
-- The C compiler identification is GNU 4.9.2
-- The CXX compiler identification is GNU 4.9.2
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++
```