As of Java 9, the -d option creates the directory if it doesn't exist.

The --release flag is also new with Java 9. In older versions, you needed to use the -source, -target, and -bootclasspath flags. The JDK now ships with symbol files for two prior versions of the API. In Java 9, you can compile with --release set to 9, 8, or 7.

Multi-release JARs are not intended for different versions of a program or library. The public API of all classes should be the same for both releases. The sole purpose of multi-release JARs is to enable a particular version of your program or library to work with multiple JDK releases. If you add functionality or change an API, you should provide a new version of the JAR instead.

> > **NOTE:**
> >
> > Tools such as javap are not retrofitted to handle multi-release JAR files. If you call
> >
> > ~~~
> > javap -classpath MyProgram.jar Application.class
> > ~~~
> >
> > you get the base version of the class (which, after all, is supposed to have the same public API as the newer version). If you must look at the newer version, call
> >
> > ~~~
> > javap               -classpath               MyProgram.jar\!/META-
> > INF/versions/9/Application.class
> > ~~~

# ### 4.9.5 A Note about Command-Line Options

The options of commands in the Java Development Kit have traditionally used single dashes followed by multiletter option names, such as