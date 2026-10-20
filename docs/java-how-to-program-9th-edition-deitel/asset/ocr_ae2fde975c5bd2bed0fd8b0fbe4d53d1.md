+   - A single-type-import declaration (p. 344) specifies one class to import. A type-import-on-demand declaration (p. 344) imports only the classes that the program uses from a particular package.
+   - The compiler uses a class loader (p. 344) to locate the classes it needs in the classpath. The classpath consists of a list of directories or archive files, each separated by a directory separator (p. 344).
+   - The classpath for the compiler and JVM can be specified by providing the -classpath option (p. 345) to the javac or java command, or by setting the CLASSPATH environment variable. If classes must be loaded from the current directory, include a dot (.) in the classpath.

# Section 8.15 Package Access

+   - If no access modifier is specified for a method or variable when it’s declared in a class, the method or variable is considered to have package access (p. 345).

# Self-Review Exercise

8.1 Fill in the blanks in each of the following statements:

+   a) When compiling a class in a package, the javac command-line option ______ specifies where to store the package and causes the compiler to create the package’s directories if they do not exist.
+   b) String class static method ______ is similar to method System.out.printf, but returns a formatted String rather than displaying a String in a command window.
+   c) If a method contains a local variable with the same name as one of its class’s fields, the local variable ______ the field in that method’s scope.
+   d) The ______ method is called by the garbage collector just before it reclaims an object’s memory.
+   e) A(n) ______ declaration specifies one class to import.
+   f) If a class declares constructors, the compiler will not create a(n) ______.
+   g) An object’s ______ method is called implicitly when an object appears in code where a String is needed.
+   h) Get methods are commonly called ______ or ______.
+   i) A(n) ______ method tests whether a condition is true or false.
+   j) For every enum, the compiler generates a static method called ______ that returns an array of the enum’s constants in the order in which they were declared.
+   k) Composition is sometimes referred to as a(n) ______ relationship.
+   l) A(n) ______ declaration contains a comma-separated list of constants.
+   m) A(n) ______ variable represents classwide information that’s shared by all the objects of the class.
+   n) A(n) ______ declaration imports one static member.
+   o) The ______ states that code should be granted only the amount of privilege and access that it needs to accomplish its designated task.
+   p) Keyword ______ specifies that a variable is not modifiable.
+   q) There can be only one ______ in a Java source-code file, and it must precede all other declarations and statements in the file.
+   r) A(n) ______ declaration imports only the classes that the program uses from a particular package.
+   s) The compiler uses a(n) ______ to locate the classes it needs in the classpath.
+   t) The classpath for the compiler and JVM can be specified with the ______ option to the javac or java command, or by setting the ______ environment variable.
+   u) Set methods are commonly called ______ because they typically change a value.
+   v) A(n) ______ imports all static members of a class.
+   w) The public methods of a class are also known as the class’s ______ or ______.