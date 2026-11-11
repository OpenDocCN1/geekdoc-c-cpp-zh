prints

    Employee Harry Hacker

if e is an employee, or

    Manager Harry Hacker

if e is a manager.

If the class is in a package, the package name is part of the class name:

```
```java
var generator = new Random();
Class cl = generator.getClass();
String name = cl.getName(); // name is set to "java.util.Random"
```
```

You can obtain a `Class` object corresponding to a class name by using the static `forName` method.

```
```java
String className = "java.util.Random";
Class cl = Class.forName(className);
```
```

Use this method if the class name is stored in a string that varies at runtime. This works if `className` is the name of a class or interface. Otherwise, the `forName` method throws a *checked exception*. See Section 5.7.2, “A Primer on Declaring Exceptions,” on p. 267 for how to supply an exception handler whenever you use this method.

> > **TIP:** At startup, the class containing your `main` method is loaded. It loads all classes that it needs. Each of those loaded classes loads the classes that it needs, and so on. That can take a long time for a big application, frustrating the user. You can give the users of your program an illusion of a faster start with the following trick. Make sure the class containing the `main` method does not explicitly refer to other classes. In it, display a splash screen. Then manually force the loading of other classes by calling `Class.forName`.

A third method for obtaining an object of type `Class` is a convenient shorthand. If `T` is any Java type (or the `void` keyword), then `T.class` is the matching class object. For example:

```
```java
Class cl1 = Random.class; // if you import java.util.*;
Class cl2 = int.class;
Class cl3 = double[].class;
```
```

Note that a `Class` object really describes a *type*, which may or may not be a class. For example, `int` is not a class, but `int.class` is nevertheless an object of type `Class`.