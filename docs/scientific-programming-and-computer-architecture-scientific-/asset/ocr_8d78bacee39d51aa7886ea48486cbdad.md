# 2.3. Building programs using GNU Make

Makefiles bring order into the translation of sources to object files and the building of executables from the object files. They reflect the hierarchy of the source tree. Makefiles can get complicated when executables must be built on multiple platforms. If the source tree of figure 2.2 must be built for Linux machines using GNU, Intel, or P compilers, or if they must be built for both Linux and Windows, the Makefiles get much more complicated. In such situations, it is common to configure scripts that generate the Makefiles. Configure scripts are typically written as shell scripts, although Python is equally effective and far more pleasant to use.

# 2.3.7 Beyond recursive make

Modularity and simplicity are two virtues of recursive make. However, there are severe problems with it.¹¹ It can be slow for large projects because a new shell process is created every time make is called recursively. It does not get well with parallel make using the -j option. It leads to needless compilation because all object files and libraries that may be externally built during recursive make and not those that are actually needed. It must be said that these deficiencies are not fatal. Recursive make is still used.

There appears to be a fundamental tension between the two-pass structure of the make utility and recursive invocation of make. The first pass is supposed to build a dependency graph, for example, of object files on sources and executables on object files. The second pass is supposed to invoke recursive to update targets that are out of date with their prerequisites. The recursive invocation of make happens during the second pass. The dependency graph of object files and sources in the external module is built only when its Makefile is invoked recursively. The result is to splinter the dependency graph, leading to multiple first and second passes.

It is possible to avoid recursive make entirely by building a single dependency graph for all the sources, object files, executables in the project.¹² One way to do

> ¹¹ See Miller (Recursive make considered harmful, 1997, http://aegis.sourceforge.net/auug97.pdf).

> ¹² One to avoid recursive make was suggested by Peter Miller (Recursive Make considered harmful, 1997, http://aegis.sourceforge.net/auug97.pdf) and developed further by Emile Bergen (http://evbergen.home.xs4all.nl/nonrecursive-make.html). This method relies on stack manipulation using make variables. Another method developed by Zhongning Qu is briefly described in the text. The heart of Qu's idea is to use pattern rules for each subdirectory or submodule.