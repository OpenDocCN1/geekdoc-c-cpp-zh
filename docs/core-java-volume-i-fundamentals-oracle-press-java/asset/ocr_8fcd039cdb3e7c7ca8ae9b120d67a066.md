The library source files are delivered in the JDK as a compressed file `lib/src.zip`. Unpack that file to get access to the source code. Simply do the following:

+   1. Make sure the JDK is installed and the `jdk/bin` directory is on the executable path.
+   2. Make a directory `javsrc` in your home directory. If you like, you can do this from a terminal window.
+   3. Inside the `jdk/lib` directory, locate the file `src.zip`.
+   4. Unzip the `src.zip` file into the `javsrc` directory. In a terminal window, you can execute the commands

```
mkdir javsrc
```

```
cd javsrc
jar xvf jdk/lib/src.zip
cd ..
```