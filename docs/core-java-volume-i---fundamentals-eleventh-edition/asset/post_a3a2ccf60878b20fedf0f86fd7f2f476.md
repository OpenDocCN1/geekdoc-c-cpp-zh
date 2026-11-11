
| 类/方法 | 版本 | 说明 |
|---|---|---|
| `java.util.Random` | 1.0 | |
| `Random()` | | constructs a new random number generator. |
| `int nextInt(int n)` | 1.2 | returns a random number between 0 and n − 1. |

## 4.6.8 Object Destruction and the finalize Method

Some object-oriented programming languages, notably C++, have explicit destructor methods for any cleanup code that may be needed when an object is no longer used. The most common activity in a destructor is reclaiming the memory set aside for objects. Since Java does automatic garbage collection, manual memory reclamation is not needed, so Java does not support destructors.

Of course, some objects utilize a resource other than memory, such as a file or a handle to another object that uses system resources. In this case, it is important that the resource be reclaimed and recycled when it is no longer needed.

If a resource needs to be closed as soon as you have finished using it, supply a close method that does the necessary cleanup. You can call the close method when you are done with the object. In Chapter 7, you will see how you can ensure that this method is called automatically.

If you can wait until the virtual machine exits, add a “shutdown hook” with the method `Runtime.addShutdownHook`. As of Java 9, you can use the Cleaner class to register an action that is carried out when an object is no longer reachable (other than by the cleaner). These are uncommon situations in practice. See the API documentation for details on these two approaches.

> **CAUTION:** Do not use the finalize method for cleanup. That method was intended to be called before the garbage collector sweeps away an object. However, you simply cannot know when this method will be called, and it is now deprecated.

## 4.7 Packages

Java allows you to group classes in a collection called a package. Packages are convenient for organizing your work and for separating your work from code libraries provided by others. In the following sections, you will learn how to use and create packages.

### 4.7.1 Package Names

The main reason for using packages is to guarantee the uniqueness of class names. Suppose two programmers come up with the bright idea of supplying an `Employee` class. As long as both of them place their class into different packages, there is no conflict. In fact, to absolutely guarantee a unique package name, use an Internet domain name (which is known to be unique) written in reverse. You then use subpackages for different projects. For example, consider the domain `horstmann.com`. When written in reverse order, it turns into the package name `com.horstmann`. You can then append a project name, such as `com.horstmann.corejava`. If you then place the `Employee` class into that package, the “fully qualified” name becomes `com.horstmann.corejava.Employee`.

> **NOTE:** From the point of view of the compiler, there is absolutely no relationship between nested packages. For example, the packages `java.util` and `java.util.jar` have nothing to do with each other. Each is its own independent collection of classes.

### 4.7.2 Class Importation

A class can use all classes from its own package and all *public* classes from other packages.

You can access the public classes in another package in two ways. The first is simply to use the *fully qualified name*; that is, the package name followed by the class name. For example:

```
java.time.LocalDate today = java.time.LocalDate.now();
```

That is obviously tedious. A simpler, and more common, approach is to use the import statement. The point of the import statement is to give you a shorthand to refer to the classes in the package. Once you add an import, you no longer have to give the classes their full names.

You can import a specific class or the whole package. You place import statements at the top of your source files (but below any package statements). For example, you can import all classes in the `java.time` package with the statement

```
import java.time.*;
```

Then you can use

```
LocalDate today = LocalDate.now();
```

> **C++ NOTE:** C++ programmers sometimes confuse `import` with `#include`. The two have nothing in common. In C++, you must use `#include` to include the declarations of external features because the C++ compiler does not look inside any files except the one that it is compiling and its explicitly included header files. The Java compiler will happily look inside other files provided you tell it where to look.
>
> In Java, you can entirely avoid the import mechanism by explicitly naming all classes, such as `java.util.Date`. In C++, you cannot avoid the `#include` directives.
>
> The only benefit of the import statement is convenience. You can refer to a class by a name shorter than the full package name. For example, after an `import java.util.*` (or `import java.util.Date`) statement, you can refer to the `java.util.Date` class simply as `Date`.
>
> In C++, the construction analogous to the package mechanism is the namespace feature. Think of the package and import statements in Java as the analogs of the namespace and using directives in C++.

### 4.7.3 Static Imports

A form of the import statement permits the importing of static methods and fields, not just classes.

For example, if you add the directive

```
import static java.lang.System.*;
```

to the top of your source file, then you can use the static methods and fields of the `System` class without the class name prefix:

```
out.println("Goodbye, World!");  // i.e., System.out
exit();                         // i.e., System.exit
```

You can also import a specific method or field:

```
import static java.lang.System.out;
```

In practice, it seems doubtful that many programmers will want to abbreviate `System.out` or `System.exit`. The resulting code seems less clear. On the other hand,

```
sqrt(pow(x, 2) + pow(y, 2))
```

seems much clearer than

```
Math.sqrt(Math.pow(x, 2) + Math.pow(y, 2))
```

### 4.7.4 Addition of a Class into a Package

To place classes inside a package, put the name of the package at the top of your source file, before the code that defines the classes in the package. For example, the file Employee.java in Listing 4.7 starts out like this:

```
package com.horstmann.corejava;

public class Employee
{
    . . .
}
```

If you don’t put a package statement in the source file, then the classes in that source file belong to the unnamed package. The unnamed package has no package name. Up to now, all our example classes were located in the unnamed package.

Place source files into a subdirectory that matches the full package name. For example, all source files in the com.horstmann.corejava package should be in a subdirectory com/horstmann/corejava (com\horstmann\corejava on Windows). The compiler places the class files into the same directory structure.

The program in Listings 4.6 and 4.7 is distributed over two packages: The PackageTest class belongs to the unnamed package, and the Employee class belongs to the com.horstmann.corejava package. Therefore, the Employee.java file must be in a subdirectory com/horstmann/corejava. In other words, the directory structure is as follows:

```
. (base directory)
├── PackageTest.java
├── PackageTest.class
└── com/
    └── horstmann/
        └── corejava/
            ├── Employee.java
            └── Employee.class
```

To compile this program, simply change to the base directory and run the command

```
javac PackageTest.java
```

The compiler automatically finds the file com/horstmann/corejava/Employee.java and compiles it.

Let’s look at a more realistic example, in which we don’t use the unnamed package but have classes distributed over several packages (com.horstmann.corejava and com.mycompany).

*Listing 4.6* (Continued)

```
    8  * @version 1.11 2004-02-19
    9  * @author Cay Horstmann
    10 */
    11 public class PackageTest
    12 {
    13    public static void main(String[] args)
    14    {
    15       // because of the import statement, we don't have to use
    16       // com.horstmann.corejava.Employee here
    17       var harry = new Employee("Harry Hacker", 50000, 1989, 10, 1);
    18
    19       harry.raiseSalary(5);
    20
    21       // because of the static import statement, we don't have to use System.out here
    22       out.println("name=" + harry.getName() + ",salary=" + harry.getSalary());
    23    }
    24 }
```

*Listing 4.7* PackageTest/com/horstmann/corejava/Employee.java

```
    1 package com.horstmann.corejava;
    2
    3 // the classes in this file are part of this package
    4
    5 import java.time.*;
    6
    7 // import statements come after the package statement
    8
    9 /**
    10  * @version 1.11 2015-05-08
    11  * @author Cay Horstmann
    12  */
    13 public class Employee
    14 {
    15    private String name;
    16    private double salary;
    17    private LocalDate hireDay;
    18
    19    public Employee(String name, double salary, int year, int month, int day)
    20    {
    21       this.name = name;
    22       this.salary = salary;
    23       hireDay = LocalDate.of(year, month, day);
    24    }
    25 }
```
