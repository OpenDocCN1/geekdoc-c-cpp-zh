# 4.7.4  Addition of a Class into a Package

To place classes inside a package, put the name of the package at the top of your source file, before the code that defines the classes in the package. For example, the file Employee.java in Listing 4.7 starts out like this:

```
```java
package com.horstmann.corejava;

public class Employee
{
    . . .
}
```
```

If you don’t put a package statement in the source file, then the classes in that source file belong to the unnamed package. The unnamed package has no package name. Up to now, all our example classes were located in the unnamed package.

Place source files into a subdirectory that matches the full package name. For example, all source files in the com.horstmann.corejava package should be in a subdirectory com/horstmann/corejava (com\horstmann\corejava on Windows). The compiler places the class files into the same directory structure.

The program in Listings 4.6 and 4.7 is distributed over two packages: The PackageTest class belongs to the unnamed package, and the Employee class belongs to the com.horstmann.corejava package. Therefore, the Employee.java file must be in a subdirectory com/horstmann/corejava. In other words, the directory structure is as follows:

+   ```text
+   . (base directory)
+   ├── PackageTest.java
+   ├── PackageTest.class
+   └── com/
+       └── horstmann/
+           └── corejava/
+               ├── Employee.java
+               └── Employee.class
+   ```

To compile this program, simply change to the base directory and run the command

```
```text
javac PackageTest.java
```
```

The compiler automatically finds the file com/horstmann/corejava/Employee.java and compiles it.

Let’s look at a more realistic example, in which we don’t use the unnamed package but have classes distributed over several packages (com.horstmann.corejava and com.mycompany).