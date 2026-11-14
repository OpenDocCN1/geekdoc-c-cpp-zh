between targets and their sources, and when a target is older than its sources or missing, that target is generated with the given commands. These dependencies are written to a makefile and automatically resolved by make. In our example, we have to compile fluxer.cpp to the corresponding object file fluxer.o:

```
fluxer.o: fluxer.cpp mesher.hpp solver.hpp
    g++ fluxer.cpp -c -o fluxer.o
```

The line(s) with the command(s) must start with a tabulator. As the rules for all object files are similar enough, we write a generic rule instead for all that originate from C++ sources:

```
.cpp.o:
    ${CXX} ${CXXFLAGS} $^ -c -o $@
```

The variable ${CXX} is preset to the default C++ compiler and ${CXXFLAGS} to its default flags. We can change these variables:

```
CXX = g++ -S
CXXFLAGS = -O3 -DNDEBUG    # Release
# CXXFLAGS = -O0 -g         # Debug
```

Here we changed the compiler or applied aggressive optimization (for release mode). As a comment, we also demonstrated the debug mode with no optimization and symbol tables within object files needed by debugging tools. We used automatic variables: $@ for the rule's target and $^ for its sources. Next we have to build our mesher and solver libraries:

```
libmesher.a: mesher.o # more mesher sources
    ar cr $@ $^

libsolver.a: solver.o # more solver sources
    ar cr $@ $^
```

For simplicity we build both with static linkage (deviating from Figure 7-4). Finally, we link the application and the libraries together:

```
fluxer: fluxer.o libmesher.a libsolver.a
    ${CXX} ${CXXFLAGS} $^ -o $@
```

If we used the default linker instead of the C++ compiler here, we would need to add C++ standard libraries and possibly some flags specific to C++ linkage. Now we can build our project with one single command:

```
make fluxer
```

This triggers the following commands:

```
g++ fluxer.cpp -c -o fluxer.o
g++ mesher.cpp -c -o mesher.o
ar cr libmesher.a mesher.o
g++ solver.cpp -c -o solver.o
ar cr libsolver.a solver.o
g++ fluxer.o libmesher.a libsolver.a -o fluxer
```