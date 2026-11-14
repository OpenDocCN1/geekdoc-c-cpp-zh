+   - Statically: The archive is entirely contained in the executable. This linkage is applied to .a libraries on Unix systems and .lib libraries on Windows.
+   - Dynamically: The linker only checks the presence of all symbols and keeps some sort of reference to the archive. This is used for .so (Unix) and .dll (Windows) libraries.

The impact is obvious: Executables that are linked against dynamic libraries are much smaller but depend on the presence of the libraries on the machine where the binary is executed. When a dynamic library is not found on Unix/Linux, we can add its directory to the search path in the environment LD_LIBRARY_PATH. On Windows, it requires a little more work. Conversely, the larger, statically linked executables contain the complete code and run independently of present libraries.

# 7.2.1.5 The Complete Build

Figure 7-4 illustrates how the application for a flux simulator might be generated. First we preprocess the main application in fluxer.cpp which includes standard libraries like <iostream> and domain-specific libraries for meshing and solving. The expanded source is then compiled to the object file fluxer.o. Finally, the application's object file is linked with standard libraries like libstdc++.so and the domain libraries whose headers we included before. Those libraries can be linked statically like libsolver.a or dynamically like libmesher.so. Frequently used libraries like those from the system are often available in both forms.

# 7.2.2 Build Tools

When we build our applications and libraries from program sources and already-compiled libraries, we can either type in lots of commands over and over or use suitable tools. In this section, we present two of them: make and CMake. As a case study we consider a scenario like in Figure 7-4: a fluxer application that is linked with a mesher and a solver library which in turn are built from the appropriate source and header files.

# 7.2.2.1 make

```
-> makefile_example/makefile
```