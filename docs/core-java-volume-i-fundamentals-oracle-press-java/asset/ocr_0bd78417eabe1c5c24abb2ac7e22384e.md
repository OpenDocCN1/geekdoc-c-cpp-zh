```
/home/user/classdir:.:/home/user/archives/archive.jar
```

Suppose the virtual machine searches for the class file of the `com.horstmann.corejava.Employee` class. It first looks in the Java API classes. It won’t find the class file there, so it turns to the class path. It then looks for the following files:

+   - `/home/user/classdir/com/horstmann/corejava/Employee.class`
+   - `com/horstmann/corejava/Employee.class` starting from the current directory
+   - `com/horstmann/corejava/Employee.class` inside `/home/user/archives/archive.jar`

The compiler has a harder time locating files than does the virtual machine. If you refer to a class without specifying its package, the compiler first needs to find out the package that contains the class. It consults all `import` directives as possible sources for the class. For example, suppose the source file contains directives

```
import java.util.*;
import com.horstmann.corejava.*;
```

and the source code refers to a class `Employee`. The compiler then tries to find `java.lang.Employee` (because the `java.lang` package is always imported by default), `java.util.Employee`, `com.horstmann.corejava.Employee`, and `Employee` in the current package. It searches for *each* of these classes in all of the locations of the class path. It is a compile-time error if more than one class is found. (Fully qualified class names must be unique, so the order of the `import` statements doesn’t matter.)

The compiler goes one step further. It looks at the *source files* to see if the source is newer than the class file. If so, the source file is recompiled automatically. Recall that you can `import` only `public` classes from other packages. A source file can only contain one `public` class, and the names of the file and the `public` class must match. Therefore, the compiler can easily locate source files for `public` classes. However, you can `import` `nonpublic`