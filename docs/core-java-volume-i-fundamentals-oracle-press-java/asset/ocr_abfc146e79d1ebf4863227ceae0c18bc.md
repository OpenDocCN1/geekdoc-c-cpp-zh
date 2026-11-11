```
```
javac com/mycompany/PayrollApp.java
java com.mycompany.PayrollApp
```
```

Note again that the compiler operates on *files* (with file separators and an extension .java), whereas the Java interpreter loads a *class* (with dot separators).

# **TIP:**

Starting with the next chapter, we will use packages for the source code. That way, you can make an IDE project for each chapter instead of each section.

# **CAUTION:**

The compiler does *not* check the directory structure when it compiles source files. For example, suppose you have a source file that starts with the directive

```
```
package com.mycompany;
```
```

You can compile the file even if it is not contained in a subdirectory com/mycompany. The source file will compile without errors *if it doesn't depend on other packages.* However, the resulting program will not run unless you first move all class files to the right place. The *virtual machine* won't find the classes if the packages don't match the directories.

**Listing 4.7** PackageTest/PackageTest.java

```
```
1  import com.horstmann.corejava.*;
2  // the Employee class is defined in that package
```
```