We do not know what you have heard about make, but it is not as bad as its reputation.6 Actually it works pretty well for small projects. The basic idea is that we express dependencies between targets and their sources, and when a target is older than its sources or missing, that target is generated with the given commands. These dependencies are written to a makefile and automatically resolved by make. In our example, we have to compile fluxer.cpp to the corresponding object file fluxer.o:

```
fluxer.o: fluxer.cpp mesher.hpp solver.hpp
    g++ fluxer.cpp -c -o fluxer.o
```

6. Rumor has it that its author showed it to his colleagues before leaving on vacation. When he came back, already regretting the design, it was being used all over the company and it was too late to retract it.

The line(s) with the command(s) must start with a tab character. As the rules for all object files are similar enough, we can write a generic rule for all C++ sources:

![](bbox=[0.14, 0.44, 0.36, 0.45])

```
.cpp.o:
    ${CXX} ${CXXFLAGS} $^ -c -o $@
```

The command contains automatic variables: $@ for the rule's target and $^ for its sources. The variable ${CXX} is preset to the default C++ compiler and ${CXXFLAGS} to its default flags. We can change these variables:

![](bbox=[0.14, 0.58, 0.36, 0.59])

```
CXX=    g++-10
CXXFLAGS= -O3 -DNDEBUG    # Release
# CXXFLAGS= -O0 -g    # Debug
```

Here we have changed the compiler and applied aggressive optimization (for release mode). As a comment, we also demonstrated the debug mode with no optimization and symbol tables within object files needed by debugging tools. Next we have to build our libraries:

![](bbox=[0.14, 0.76, 0.36, 0.77])

```
libmesher.a: mesher.o # more mesher sources
    ar cr $@ $^
libsolver.a: solver.o # more solver sources
    ar cr $@ $^
```