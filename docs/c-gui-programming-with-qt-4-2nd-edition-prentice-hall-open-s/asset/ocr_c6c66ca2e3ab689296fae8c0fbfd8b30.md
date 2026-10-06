Conventionally, project files that are meant to be included by other project files are given a .pri (project include) extension.

In a previous example, we saw the $$lower() built-in function, which returns a lowercase version of its argument. Another useful function is $$system(): It allows us to generate strings from external applications. For example, if we need to determine which version of Unix is being used, we can write

```
OS_VERSION = $$system(uname -r).
```

We can then use the resulting variable in a condition, together with contains(): contains(OS_VERSION, SunOS):SOURCES += mythread_sun.c

In this section, we have barely skimmed the surface. The qmake tool provides many more options and features than we presented here, including support for precompiled headers, for Mac OS X universal binaries, and for user-defined compilers or tools. Refer to the online qmake manual for full details.