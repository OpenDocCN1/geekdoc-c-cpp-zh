
> **CAUTION:** In the past, some people recommended to bypass the class path altogether, by dropping all JAR files into the jre/lib/ext directory. That mechanism is obsolete with Java 9, but it was always bad advice. It was easy to get confused when long-forgotten classes were reloaded from the extension directory.

> **NOTE:** As of Java 9, classes can also be loaded from the module path. We discuss modules and the module path in Chapter 9 of Volume II.

## 4.8 JAR Files

When you package your application, you want to give your users a single file, not a directory structure filled with class files. Java Archive (JAR) files were designed for this purpose. A JAR file can contain both class files and other file types such as image and sound files. Moreover, JAR files are compressed, using the familiar ZIP compression format.

### 4.8.1 Creating JAR files

Use the jar tool to make JAR files. (In the default JDK installation, it’s in the jdk/bin directory.) The most common command to make a new JAR file uses the following syntax:

```
jar cvf jarFileName file1 file2 ...
```

For example:

```
jar cvf CalculatorClasses.jar *.class icon.gif
```

In general, the jar command has the following format:

```
jar options file1 file2 ...
```

Table 4.2 lists all the options for the jar program. They are similar to the options of the UNIX tar command.

You can package application programs and code libraries into JAR files. For example, if you want to send mail in a Java program, you use a library that is packaged in a file javax.mail.jar.

**Table 4.2** jar Program Options

| Option | Description |
|---|---|
| `c` | Creates a new or empty archive and adds files to it. If any of the specified file names are directories, the jar program processes them recursively. |
| `C` | Temporarily changes the directory. For example, `jar cvf jarFileName.jar -C classes *.class` changes to the classes subdirectory to add class files. |
| `e` | Creates an entry point in the manifest (see Section 4.8.3). |
| `f` | Specifies the JAR file name as the second command-line argument. If this parameter is missing, jar will write the result to standard output (when creating a JAR file) or read it from standard input (when extracting or tabulating a JAR file). |
| `i` | Creates an index file (for speeding up lookups in a large archive). |
| `m` | Adds a manifest to the JAR file. A manifest is a description of the archive contents and origin. Every archive has a default manifest, but you can supply your own if you want to authenticate the contents of the archive. |
| `M` | Does not create a manifest file for the entries. |
| `t` | Displays the table of contents. |
| `u` | Updates an existing JAR file. |
| `v` | Generates verbose output. |
| `x` | Extracts files. If you supply one or more file names, only those files are extracted. Otherwise, all files are extracted. |
| `0` | Stores without ZIP compression. |

### 4.8.2 The Manifest

In addition to class files, images, and other resources, each JAR file contains a manifest file that describes special features of the archive.

The manifest file is called MANIFEST.MF and is located in a special META-INF sub-directory of the JAR file. The minimum legal manifest is quite boring—just

```
Manifest-Version: 1.0
```

Complex manifests can have many more entries. The manifest entries are grouped into sections. The first section in the manifest is called the *main section*. It applies to the whole JAR file. Subsequent entries can specify properties of named entities such as individual files, packages, or URLs. Those entries must begin with a `Name` entry. Sections are separated by blank lines. For example:

```
Manifest-Version: 1.0
lines describing this archive

Name: Woozle.class
lines describing this file
Name: com/mycompany/mypkg/
lines describing this package
```

To edit the manifest, place the lines that you want to add to the manifest into a text file. Then run

```
jar cfm jarFile manifestFileName ...
```

For example, to make a new JAR file with a manifest, run

```
jar cfm MyArchive.jar manifest.mf com/mycompany/mypkg/*.class
```

To update the manifest of an existing JAR file, place the additions into a text file and use a command such as

```
jar ufm MyArchive.jar manifest-additions.mf
```

> **NOTE:** See https://docs.oracle.com/javase/10/docs/specs/jar/jar.html for more information on the JAR and manifest file formats.

### 4.8.3 Executable JAR Files

You can use the `e` option of the `jar` command to specify the *entry point* of your program—the class that you would normally specify when invoking the `java` program launcher:

```
jar cve MyProgram.jar com.mycompany.mypkg.MainAppClass files to add
```

Alternatively, you can specify the *main class* of your program in the manifest, including a statement of the form

```
Main-Class: com.mycompany.mypkg.MainAppClass
```

Do not add a `.class` extension to the main class name.

![](img/127bccebb2cfadea3f02579edaad63c3_221_0.png)

> **CAUTION:** The last line in the manifest must end with a newline character. Otherwise, the manifest will not be read correctly. It is a common error to produce a text file containing just the Main-Class line without a line terminator.

With either method, users can simply start the program as

```
java -jar MyProgram.jar
```

Depending on the operating system configuration, users may even be able to launch the application by double-clicking the JAR file icon. Here are behaviors for various operating systems:

- On Windows, the Java runtime installer creates a file association for the “.jar” extension that launches the file with the `java -jar` command. (Unlike the `java` command, the `javaw` command doesn’t open a shell window.)
- On Mac OS X, the operating system recognizes the “.jar” file extension and executes the Java program when you double-click a JAR file.

However, a Java program in a JAR file does not have the same feel as a native application. On Windows, you can use third-party wrapper utilities that turn JAR files into Windows executables. A wrapper is a Windows program with the familiar .exe extension that locates and launches the Java virtual machine (JVM) or tells the user what to do when no JVM is found. There are a number of commercial and open source products, such as Launch4J (http://launch4j.sourceforge.net) and IzPack (http://izpack.org).

### 4.8.4 Multi-Release JAR Files

With the introduction of modules and strong encapsulation of packages, some previously accessible internal APIs are no longer available. For example, JavaFX 8 had an internal class `com.sun.javafx.css.CssParser`. If you used it to parse a style sheet, then you will find that your program no longer compiles. The remedy is simple—switch to `javafx.css.CssParser`, which is available in Java 9. But now you have a problem. You need to distribute different applications for Java 8 and Java 9 users, or you need to play tricks with class loading and reflection.

To solve problems such as this one, Java 9 introduces *multi-release JARs* that can contain class files for different Java releases.

For backwards compatibility, the additional class files are placed in the `META-INF/versions` directory:

> **NOTE:** Tools such as javap are not retrofitted to handle multi-release JAR files.

If you call

```
javap -classpath MyProgram.jar Application.class
```

you get the base version of the class (which, after all, is supposed to have the same public API as the newer version). If you must look at the newer version, call

```
javap -classpath MyProgram.jar!/META-INF/versions/9/Application.class
```

### 4.8.5 A Note about Command-Line Options

The options of commands in the Java Development Kit have traditionally used single dashes followed by multiletter option names, such as

```
java -jar ...
javac -Xlint:unchecked -classpath ...
```

The exception was the `jar` command, which followed the classic option format of the `tar` command without dashes:

```
jar cvf ...
```

Starting with Java 9, the Java tools are moving towards a more common option format where multiletter option names are preceded by double dashes, with single-letter shortcuts for common options. For example, the Linux `ls` command can be called with a "human-readable" option as

```
ls --human-readable
```

or

```
ls -h
```

As of Java 9, you can use `--version` instead of `-version` and `--class-path` instead of `-classpath`. As you will see in Chapter 9 of Volume II, the `--module-path` option has a shortcut `-p`.

You can find the details in the JEP 293 enhancement request at http://openjdk.java.net/jeps/293. As part of this cleanup, the authors also propose to standardize option arguments. Arguments of options with `--` and multiple letters are separated by whitespace or an `=` sign:

```
javac --class-path /home/user/classdir ...
```

or

```
javac --class-path=/home/user/classdir ...
```
