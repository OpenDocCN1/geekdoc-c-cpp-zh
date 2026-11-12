to be compiled. We’ve defined __DEBUG__ and FUSE_EXPORT in this scenario. The __DEBUG__ macro instructs the compiler to generate data for the debugging. FUSE_EXPORT will be used to instruct the compiler about which modules of the engine to export into the library (more about later). We also want to make sure CMake knows where the external libraries that the engine will be using are on Windows. which is why we are using the if(WIN32) statements to check if the current platform used is Windows. You will get later why we don’t have to do that for Linux.

A precompiled header (PCH) is a header file (C/C++) that has been compiled into an intermediate form that the compiler can parse more quickly. Precompiled headers can significantly reduce compilation time, especially for large header files, header files that include many other header files, or header files that are included in many translation units. CMake gives us the ability to add precompile headers to our project via the function: target_precompile_headers().

There is a file called “pch.h” in the folder “engine” which is the precompiled header for the engine library. It will be used to include all important C++ standard libraries as well as other custom code that will be accessible globally. This will significantly reduce the time needed to compile the engine library.

Note : The only requirement for using precompile headers is that we must include the pch.h header file in all .cpp-files of the engine.

We call the function “target_include_directories” to attach all include directories, so that the compiler will know which header files to include during the compilation process.

The last CMakeLists.txt file we will talk about is the one found in “game”.

+   ↘ Project/game/CMakeLists.txt