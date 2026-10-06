We have available. We have specified that the Plotter class is a C++ "object type"; this is suitable for objects that cannot be copied, such as widgets. In contrast, the PlotSettings class is treated as a C++ "value type".

To Qt Jambi, there is no obvious difference between the two. The distinction is important when the generator makes C++ APIs to Java APIs. For example, if a "value type" is returned from a method, the generator will ensure that a new independent object is returned (to avoid side effects), but if the returned type is an object type, a reference to the original object is returned.

We will need two environment variables, one specifying the path to Qt Jambi, the other to Java. Here is how we set them on Unix systems (using the Bash shell):

```
export JAMBIPATH=$HOME/qtjambi-linux32-gpl-4.3.2_01
export JAVA=/usr/java/jdk1.6.0_02
```

On Windows, we would write

```
set JAMBIPATH=C:\QtJambi
set JAVA="C:\Program Files\Java\jdk1.6.0_02"
```

Naturally, the version numbers and directories may be different for your system. From now on, we will assume that JAMBIPATH and JAVA are available. Once we have the header and XML files, we can run the generator in a console:

```
$JAMBIPATH/bin/generator jambiglotter.h jambiglotter.xml
```

If Qt Jambi has been installed locally rather than system-wide, this may fail on some systems. The solution is to provide a suitable path to Qt Jambi's libraries:

```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$JAMBIPATH/lib
```

Again, we have used the Bash's syntax. On Mac OS X, the relevant environment variable is called DYLD_LIBRARY_PATH. On Windows, the equivalent is achieved by adding to the PATH:

```
set PATH=%PATH%;%JAMBIPATH%\lib
```

Now, on Windows, we can run the generator like this: