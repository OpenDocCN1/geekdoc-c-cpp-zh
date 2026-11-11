names the bytecode file `FirstSample.class` and stores it in the same directory as the source file. Finally, launch the program by issuing the following command:

```
    java FirstSample
```

(Remember to leave off the `.class` extension.) When the program executes, it simply displays the string We will not use 'Hello, World!' on the console.

When you use

```
    java ClassName
```

to run a compiled program, the Java virtual machine always starts execution with the code in the main method in the class you indicate. (The term “method” is Java-speak for a function.) Thus, you must have a main method in the source of your class for your code to execute. You can, of course, add your own methods to a class and call them from the main method. (You will see in the next chapter how to write your own methods.)

![](bbox=[0.128, 0.584, 0.179, 0.624])

# NOTE:

According to the Java Language Specification, the main method must be declared public. (The Java Language Specification is the official document that describes the Java language. You can view or download it from http://docs.oracle.com/javase/specs.)

However, several versions of the Java launcher were willing to execute Java programs even when the main method was not public. A programmer filed a bug report. To see it, visit https://bugs.openjdk.java.net/browse/JDK-4252539. In 1999, that bug was marked as “closed, will not be fixed.” A Sun engineer added an explanation that the Java Virtual Machine Specification does not mandate that main is public and that “fixing it will cause potential