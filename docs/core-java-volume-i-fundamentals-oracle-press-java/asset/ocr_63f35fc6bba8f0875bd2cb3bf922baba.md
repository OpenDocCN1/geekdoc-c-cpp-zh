Depending on the operating system configuration, users may even be able to launch the application by double-clicking the JAR file icon. Here are behaviors for various operating systems:

+   - On Windows, the Java runtime installer creates a file association for the “.jar” extension that launches the file with the `javaw -jar` command. (Unlike the `java` command, the `javaw` command doesn’t open a shell window.)
+   - On Mac OS X, the operating system recognizes the “.jar” file extension and executes the Java program when you double-click a JAR file.

However, a Java program in a JAR file does not have the same feel as a native application. On Windows, you can use third-party wrapper utilities that turn JAR files into Windows executables. A wrapper is a Windows program with the familiar `.exe` extension that locates and launches the Java virtual machine (JVM) or tells the user what to do when no JVM is found. There are a number of commercial and open source products, such as Launch4J (http://launch4j.sourceforge.net) and IzPack (http://izpack.org).

# #### 4.9.4 Multi-Release JAR Files

With the introduction of modules and strong encapsulation of packages, some previously accessible internal APIs are no longer available. This may require library providers to distribute different code for different Java versions. Java 9 introduces *multi-release JARs* for this purpose.

For backwards compatibility, version-specific class files are placed in the