
## 2.3. Building programs using GNU Make

Makefiles bring order into the translation of sources to object files and the building of executables from the object files. They reflect the hierarchy of the source tree. Makefiles can get complicated when executables must be built on multiple platforms. If the source tree of figure 2.2 must be built for Linux machines using GNU, Intel, or P compilers, or if they must be built for both Linux and Windows, the Makefiles get much more complicated. In such situations, it is common to configure scripts that generate the Makefiles. Configure scripts are typically written as shell scripts, although Python is equally effective and far more pleasant to use.

### 2.3.7 Beyond recursive make

Modularity and simplicity are two virtues of recursive make. However, there are severe problems with it.¹<sup>11</sup>. It can be slow for large projects because a new shell process is created every time make is called recursively. It does not get well with parallel make using the -j option. It leads to needless compilation because all object files and libraries that may be externally built during recursive make and not those that are actually needed. It must be said that these deficiencies are not fatal. Recursive make is still used.

There appears to be a fundamental tension between the two-pass structure of the make utility and recursive invocation of make. The first pass is supposed to build a dependency graph, for example, of object files on sources and executables on object files. The second pass is supposed to invoke recursive to update targets that are out of date with their prerequisites. The recursive invocation of make happens during the second pass. The dependency graph of object files and sources in the external module is built only when its Makefile is invoked recursively. The result is to splinter the dependency graph, leading to multiple first and second passes.

It is possible to avoid recursive make entirely by building a single dependency graph for all the sources, object files, executables in the project.¹<sup>12</sup>. One way to do...

> ¹¹ See Miller (Recursive make considered harmful, 1997, http://aegis.sourceforge.net/auug97.pdf).

> ¹² One to avoid recursive make was suggested by Peter Miller (Recursive Make considered harmful, 1997, http://aegis.sourceforge.net/auug97.pdf) and developed further by Emile Bergen (http://evbergen.home.xs4all.nl/nonrecursive-make.html). This method relies on stack manipulation using make variables. Another method developed by Zhongning Qu is briefly described in the text. The heart of Qu's idea is to use pattern rules for each subdirectory or submodule.

## Chapter 2. C/C++: Libraries and Makefiles

this is to include a rules.mk file in each subdirectory or submodule. The rules.mk file contains pattern rules specific to the subdirectory as well as dependencies of object files on sources in the subdirectory.

In each rules.mk, it is assumed that a variable R, which expands to the full absolute path of the root of the project, is defined. A rules.mk file in linking/linalg may look as follows:

```
1 saved := $(D)
2 D := $(R)/linking/linalg R defined externally
3 $(D)CFLAGS := $(CFLAGS) -mkl
4
5 $(D)/%.o: $(D)/%.cpp
6 $(CPP) ($@D) CFLAGS) -o $@ -c $<
7
8 $(D)/lusolve.o: $(D)/lusolve.cpp
9 $(D)/test_lusolve.o: $(D)/test_lusolve.cpp D := $(saved)
```

This rules.mk file defines the variable D (line 2) to be the absolute path to the directory that contains itself as well as the source files that it manages. The variable R is assumed to point to the root of the source tree.

On line 3, we define the variable $(D)CFLAGS. Here $(D) evaluates to the absolute path of the directory, and the variable name is in that absolute path appended to it. This variable holds compilation flags specific to it. In this example, the only change is to append the -mkl flag.

On lines 5 and 6, the pattern rule for generating a .o object from a .cpp source is made specific to the directory. GNU make, @D is a variable that evaluates to the current directory. Therefore, the syntax

```
$($@D) CFLAGS)
```

which occurs on line 6, evaluates the variable defined on line 3. GNU make always chooses the most specific pattern rule. On lines 5 and 6, the pattern rule is made specific to the object files to be generated in the current module.

The use of $(D) to evaluate the make variable D on lines 8 and 9 implies that the object and source files are given in full absolute paths. Giving object and source file names in full absolute paths is essential to the technique described.

## 2.3. Building programs using GNU Make

A rules.mk file for the module utils/ written along the same lines looks like:

```
saved := $(D)
D := $(R)/utils
$(D)CFLAGS := $(CFLAGS) -fPIC
```

```
$(D)/%.o: $(D)/%.cpp
$(CPP) $(<) $(CFLAGS) -o $$ -c $$
```

```
$(D)/utils.o: $(D)/utils.cpp
$(D)/Table.o: $(D)/Table.cpp
```

```
D := $(saved)
```

A Makefile in linking/linalg builds the executable to test the LU solver looks as follows.

```
1 include ../.root.mk #define R, CPP, CFLAGS
2 D := $(R)/linking/linalg
3 LIBS := = -mkl
4
5 $(D)/%.o: $(D)/%.cpp
6 $(CPP) $(<) $(CFLAGS) -o $$ -c $$
7
8 $(D)/lusolve.o: $(D)/lusolve.cpp
9 $(D)/test_lusolve.o: $(D)/test_lusolve.cpp D := $(saved)
```

This rules.mk file defines the variable D (line 2) to be the absolute path to the directory that contains itself as well as the source files that it manages. The variable R is assumed to point to the root of the source tree. 

On line 3, we define the variable $(D)CFLAGS. Here $(D) evaluates to the absolute path of the directory, and the variable name is in that absolute path appended to it. This variable holds compilation flags specific to it. In this example, the only change is to append the -mkl flag.

On lines 5 and 6, the pattern rule for generating a .o object from a .cpp source is made specific to the directory. GNU make, @D is a variable that evaluates to the current directory. Therefore, the syntax

```
$($@D) CFLAGS)
```

which occurs on line 6, evaluates the variable defined on line 3. GNU make always chooses the most specific pattern rule. On lines 5 and 6, the pattern rule is made specific to the object files to be generated in the current module.

The use of $(D) to evaluate the make variable D on lines 8 and 9 implies that the object and source files are given in full absolute paths. Giving object and source file names in full absolute paths is essential to the technique described.

A Makefile in linking/linalg builds the executable to test the LU solver looks as follows.

```
1 include ../.root.mk #define R, CPP, CFLAGS
2 D := $(R)/linking/linalg
3 LIBS := = -mkl
4
5 $(D)/%.o: $(D)/%.cpp
6 $(CPP) $(<) $(CFLAGS) -o $$ -c $$
7
8 $(D)/lusolve.o: $(D)/lusolve.cpp
9 $(D)/test_lusolve.o: $(D)/test_lusolve.cpp D := $(saved)
```

This rules.mk file defines the variable D (line 2) to be the absolute path to the directory that contains itself as well as the source files that it manages. The variable R is assumed to point to the root of the source tree. 

On line 3, we define the variable $(D)CFLAGS. Here $(D) evaluates to the absolute path of the directory, and the variable name is in that absolute path appended to it. This variable holds compilation flags specific to it. In this example, the only change is to append the -mkl flag.

On lines 5 and 6, the pattern rule for generating a .o object from a .cpp source is made specific to the directory. GNU make, @D is a variable that evaluates to the current directory. Therefore, the syntax

```
$($@D) CFLAGS)
```

which occurs on line 6, evaluates the variable defined on line 3. GNU make always chooses the most specific pattern rule. On lines 5 and 6, the pattern rule is made specific to the object files to be generated in the current module.

The use of $(D) to evaluate the make variable D on lines 8 and 9 implies that the object and source files are given in full absolute paths. Giving object and source file names in full absolute paths is essential to the technique described.

A Makefile in linking/linalg builds the executable to test the LU solver looks as follows.

```
1 include ../.root.mk #define R, CPP, CFLAGS
2 D := $(R)/linking/linalg
3 LIBS := = -mkl
4
5 $(D)/%.o: $(D)/%.cpp
6 $(CPP) $(<) $(CFLAGS) -o $$ -c $$
7
8 $(D)/lusolve.o: $(D)/lusolve.cpp
9 $(D)/test_lusolve.o: $(D)/test_lusolve.cpp D := $(saved)
```

This rules.mk file defines the variable D (line 2) to be the absolute path to the directory that contains itself as well as the source files that it manages. The variable R is assumed to point to the root of the source tree. 

On line 3, we define the variable $(D)CFLAGS. Here $(D) evaluates to the absolute path of the directory, and the variable name is in that absolute path appended to it. This variable holds compilation flags specific to it. In this example, the only change is to append the -mkl flag.

On lines 5 and 6, the pattern rule for generating a .o object from a .cpp source is made specific to the directory. GNU make, @D is a variable that evaluates to the current directory. Therefore, the syntax

```
$($@D) CFLAGS)
```

which occurs on line 6, evaluates the variable defined on line 3. GNU make always chooses the most specific pattern rule. On lines 5 and 6, the pattern rule is made specific to the object files to be generated in the current module.

The use of $(D) to evaluate the make variable D on lines 8 and 9 implies that the object and source files are given in full absolute paths. Giving object and source file names in full absolute paths is essential to the technique described.

A Makefile in linking/linalg builds the executable to test the LU solver looks as follows.

```
1 include ../.root.mk #define R, CPP, CFLAGS
2 D := $(R)/linking/linalg
3 LIBS := = -mkl
4
5 $(D)/%.o: $(D)/%.cpp
6 $(CPP) $(<) $(CFLAGS) -o $$ -c $$
7
8 $(D)/lusolve.o: $(D)/lusolve.cpp
9 $(D)/test_lusolve.o: $(D)/test_lusolve.cpp D := $(saved)
```

This rules.mk file defines the variable D (line 2) to be the absolute path to the directory that contains itself as well as the source files that it manages. The variable R is assumed to point to the root of the source tree. 

On line 3, we define the variable $(D)CFLAGS. Here $(D) evaluates to the absolute path of the directory, and the variable name is in that absolute path appended to it. This variable holds compilation flags specific to it. In this example, the only change is to append the -mkl flag.

On lines 5 and 6, the pattern rule for generating a .o object from a .cpp source is made specific to the directory. GNU make, @D is a variable that evaluates to the current directory. Therefore, the syntax

```
$($@D) CFLAGS)
```

which occurs on line 6, evaluates the variable defined on line 3. GNU make always chooses the most specific pattern rule. On lines 5 and 6, the pattern rule is made specific to the object files to be generated in the current module.

The use of $(D) to evaluate the make variable D on lines 8 and 9 implies that the object and source files are given in full absolute paths. Giving object and source file names in full absolute paths is essential to the technique described.

## 2.3. Building programs using GNU Make

```
saved := $(D)
D := $(R)/utils
$(D)CFLAGS := $(CFLAGS) -fPIC
```

```
$(D)/%.o: $(D)/%.cpp
$(CPP) $(<) $(CFLAGS) -o $$ -c $$
```

```
$(D)/utils.o: $(D)/utils.cpp
$(D)/Table.o: $(D)/Table.cpp
```

```
D := $(saved)
```

A Makefile in linking/linalg builds the executable to test the LU solver looks as follows.

```
1 include ../.root.mk #define R, CPP, CFLAGS
2 D := $(R)/linking/linalg
3 LIBS := = -mkl
4
5 $(D)/%.o: $(D)/%.cpp
6 $(CPP) $(<) $(CFLAGS) -o $$ -c $$
7
8 $(D)/lusolve.o: $(D)/lusolve.cpp
9 $(D)/test_lusolve.o: $(D)/test_lusolve.cpp D := $(saved)
```

This rules.mk file defines the variable D (line 2) to be the absolute path to the directory that contains itself as well as the source files that it manages. The variable R is assumed to point to the root of the source tree. 

On line 3, we define the variable $(D)CFLAGS. Here $(D) evaluates to the absolute path of the directory, and the variable name is in that absolute path appended to it. This variable holds compilation flags specific to it. In this example, the only change is to append the -mkl flag.

On lines 5 and 6, the pattern rule for generating a .o object from a .cpp source is made specific to the directory. GNU make, @D is a variable that evaluates to the current directory. Therefore, the syntax

```
$($@D) CFLAGS)
```

which occurs on line 6, evaluates the variable defined on line 3. GNU make always chooses the most specific pattern rule. On lines 5 and 6, the pattern rule is made specific to the object files to be generated in the current module.

The use of $(D) to evaluate the make variable D on lines 8 and 9 implies that the object and source files are given in full absolute paths. Giving object and source file names in full absolute paths is essential to the technique described.

This rules.mk file defines the variable D (line 2) to be the absolute path to the directory that contains itself as well as the source files that it manages. The variable R is assumed to point to the root of the source tree. 

On line 3, we define the variable $(D)CFLAGS. Here $(D) evaluates to the absolute path of the directory, and the variable name is in that absolute path appended to it. This variable holds compilation flags specific to it. In this example, the only change is to append the -mkl flag.

On lines 5 and 6, the pattern rule for generating a .o object from a .cpp source is made specific to the directory. GNU make, @D is a variable that evaluates to the current directory. Therefore, the syntax

```
$($@D) CFLAGS)
```

which occurs on line 6, evaluates the variable defined on line 3. GNU make always chooses the most specific pattern rule. On lines 5 and 6, the pattern rule is made specific to the object files to be generated in the current module.

This rules.mk file defines the variable D (line 2) to be the absolute path to the directory that contains itself as well as the source files that it manages. The variable R is assumed to point to the root of the source tree. 

Wait, the OCR text has repeated sections and artifacts. Let me provide the clean merged version based on the logical flow.

### 2.3.7 Beyond recursive make

Modularity and simplicity are two virtues of recursive make. However, there are severe problems with it.¹<sup>11</sup>. It can be slow for large projects because a new shell process is created every time make is called recursively. It does not get well with parallel make using the -j option. It leads to needless compilation because all object files and libraries that may be externally built during recursive make and not those that are actually needed. It must be said that these deficiencies are not fatal. Recursive make is still used.

There appears to be a fundamental tension between the two-pass structure of the make utility and recursive invocation of make. The first pass is supposed to build a dependency graph, for example, of object files on sources and executables on object files. The second pass is supposed to invoke recursive to update targets that are out of date with their prerequisites. The recursive invocation of make happens during the second pass. The dependency graph of object files and sources in the external module is built only when its Makefile is invoked recursively. The result is to splinter the dependency graph, leading to multiple first and second passes.

It is possible to avoid recursive make entirely by building a single dependency graph for all the sources, object files, executables in the project.¹<sup>12</sup>. One way to is to include a rules.mk file in each subdirectory or submodule. The rules.mk file contains pattern rules specific to the subdirectory as well as dependencies of object files on sources in the subdirectory.

In each rules.mk, it is assumed that a variable R, which expands to the full absolute path of the root of the project, is defined. A rules.mk file in linking/linalg may look as follows:

```
1 saved := $(D)
2 D := $(R)/linking/linalg R defined externally
3 $(D)CFLAGS := $(CFLAGS) -mkl
4
5 $(D)/%.o: $(D)/%.cpp
6 $(CPP) ($@D) CFLAGS) -o $@ -c $<
7
8 $(D)/lusolve.o: $(D)/lusolve.cpp
9 $(D)/test_lusolve.o: $(D)/test_lusolve.cpp D := $(saved)
```

This rules.mk file defines the variable D (line 2) to be the absolute path to the directory that contains itself as well as the source files that it manages. The variable R is assumed to point to the root of the source tree.

On line 3, we define the variable $(D)CFLAGS. Here $(D) evaluates to the absolute path of the directory, and the variable name is in that absolute path appended to it. This variable holds compilation flags specific to it. In this example, the only change is to append the -mkl flag.

On lines 5 and 6, the pattern rule for generating a .o object from a .cpp source is made specific to the directory. GNU make, @D is a variable that evaluates to the current directory. Therefore, the syntax

```
$($@D) CFLAGS)
```

which occurs on line 6, evaluates the variable defined on line 3. GNU make always chooses the most specific pattern rule. On lines 5 and 6, the pattern rule is made specific to the object files to be generated in the current module.

The use of $(D) to evaluate the make variable D on lines 8 and 9 implies that the object and source files are given in full absolute paths. Giving object and source file names in full absolute paths is essential to the technique described.

A rules.mk file for the module utils/ written along the same lines looks like:

```
saved := $(D)
D := $(R)/utils
$(D)CFLAGS := $(CFLAGS) -fPIC
```

```
$(D)/%.o: $(D)/%.cpp
$(CPP) $(<) $(CFLAGS) -o $$ -c $$
```

```
$(D)/utils.o: $(D)/utils.cpp
$(D)/Table.o: $(D)/Table.cpp
```

```
D := $(saved)
```

A Makefile in linking/linalg builds the executable to test the LU solver looks as follows.

```
1 include ../.root.mk #define R, CPP, CFLAGS
2 D := $(R)/linking/linalg
3 LIBS := = -mkl
4
5 $(D)/%.o: $(D)/%.cpp
6 $(CPP) $(<) $(CFLAGS) -o $$ -c $$
7
8 $(D)/lusolve.o: $(D)/lusolve.cpp
9 $(D)/test_lusolve.o: $(D)/test_lusolve.cpp D := $(saved)
```

This rules.mk file defines the variable D (line 2) to be the absolute path to the directory that contains itself as well as the source files that it manages. The variable R is assumed to point to the root of the source tree.

On line 3, we define the variable $(D)CFLAGS. Here $(D) evaluates to the absolute path of the directory, and the variable name is in that absolute path appended to it. This variable holds compilation flags specific to it. In this example, the only change is to append the -mkl flag.

On lines 5 and 6, the pattern rule for generating a .o object from a .cpp source is made specific to the directory. GNU make, @D is a variable that evaluates to the current directory. Therefore, the syntax

```
$($@D) CFLAGS)
```

which occurs on line 6, evaluates the variable defined on line 3. GNU make always chooses the most specific pattern rule. On lines 5 and 6, the pattern rule is made specific to the object files to be generated in the current module.

The use of $(D) to evaluate the make variable D on lines 8 and 9 implies that the object and source files are given in full absolute paths. Giving object and source file names in full absolute paths is essential to the technique described.

## 2.3. Building programs using GNU Make

Makefiles bring order into the translation of sources to object files and the building of executables from the object files. They reflect the hierarchy of the source tree. Makefiles can get complicated when executables must be built on multiple platforms. If the source tree of figure 2.2 must be built for Linux machines using GNU, Intel, or P compilers, or if they must be built for both Linux and Windows, the Makefiles get much more complicated. In such situations, it is common to configure scripts that generate the Makefiles. Configure scripts are typically written as shell scripts, although Python is equally effective and far more pleasant to use.
