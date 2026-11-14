contain further capitals (CamelCase). Program output and commands are in light blue typewriter font.

Programs requiring C++11, C++14, C++17, or C++20 features are marked with corresponding margin boxes. Several programs making light use of a C++11 feature that is easily substituted by a C++03 expression are not explicitly marked.

Except for very short code illustrations, all programming examples in this book were tested on at least one compiler and in most cases on three compilers: `g++`, `clang++`, and Visual Studio. All examples are kept as short as possible for easier understanding. To this end, we don’t incorporate all features that would have been used in comparable production code. Obviously, we minimize the usage of features not introduced yet. It is probably a good idea to review the examples after finishing reading the book and ask yourself what you would code differently based on all the new knowledge you acquired.

For the C++20 examples, we recommend that you try them to see whether they work on your system. Most of the new features weren’t fully supported by all compilers at the time of this writing. Even the existing compiler support might not have been 100 percent correct at that time. For some new libraries, we used prototype implementations when no standard version was available on any compiler (e.g., format library).

```
=> directory/source_code.cpp
```

The location of the program example relevant to the discussed topic is indicated by an arrow and the paths of the complete programs at the beginning of the paragraph or the section. All programs are available on GitHub in the public repository https://github.com/petergottschling/dmc3 and can thus be cloned by:

Click here to view code image

```
git clone https://github.com/petergottschling/dmc3.git
```

On Windows, it might be more convenient to use TortoiseGit; see tortoisegit.org.