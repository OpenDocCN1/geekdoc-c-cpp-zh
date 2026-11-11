![](bbox=[0.106, 0.15, 0.147, 0.183])

**CAUTION:** The last line in the manifest must end with a newline character. Otherwise, the manifest will not be read correctly. It is a common error to produce a text file containing just the Main-Class line without a line terminator.

With either method, users can simply start the program as

```
java -jar MyProgram.jar
```

Depending on the operating system configuration, users may even be able to launch the application by double-clicking the JAR file icon. Here are behaviors for various operating systems:

+   - On Windows, the Java runtime installer creates a file association for the “.jar” extension that launches the file with the `java -jar` command. (Unlike the `java` command, the `javaw` command doesn’t open a shell window.)
+   - On Mac OS X, the operating system recognizes the “.jar” file extension and executes the Java program when you double-click a JAR file.

However, a Java program in a JAR file does not have the same feel as a native application. On Windows, you can use third-party wrapper utilities that turn JAR files into Windows executables. A wrapper is a Windows program with the familiar .exe extension that locates and launches the Java virtual machine (JVM) or tells the user what to do when no JVM is found. There are a number of commercial and open source products, such as Launch4J (http://launch4j.sourceforge.net) and IzPack (http://izpack.org).

# 4.8.4 Multi-Release JAR Files

With the introduction of modules and strong encapsulation of packages, some previously accessible internal APIs are no longer available. For example, JavaFX 8 had an internal class `com.sun.javafx.css.CssParser`. If you used it to parse a style sheet, then you will find that your program no longer compiles. The remedy is simple—switch to `javafx.css.CssParser`, which is available in Java 9. But now you have a problem. You need to distribute different applications for Java 8 and Java 9 users, or you need to play tricks with class loading and reflection.

To solve problems such as this one, Java 9 introduces *multi-release JARs* that can contain class files for different Java releases.

For backwards compatibility, the additional class files are placed in the `META-INF/versions` directory: