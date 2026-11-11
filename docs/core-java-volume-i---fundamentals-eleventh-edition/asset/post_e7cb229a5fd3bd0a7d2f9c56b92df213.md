
```java
/**
 * This program demonstrates enumerated types.
 * @version 1.00 2004-05-24
 * @author Cay Horstmann
 */
public class EnumTest
{
   public static void main(String[] args)
   {
      var in = new Scanner(System.in);
      System.out.print("Enter a size (SMALL, MEDIUM, LARGE, EXTRA_LARGE): ");
      String input = in.next().toUpperCase();
      Size size = Enum.valueOf(Size.class, input);
      System.out.println("size=" + size);
      System.out.println("abbreviation=" + size.getAbbreviation());
      if (size == Size.EXTRA_LARGE)
         System.out.println("Good job—you paid attention to the _.");
   }
}

enum Size
{
   SMALL("S"), MEDIUM("M"), LARGE("L"), EXTRA_LARGE("XL");

   private Size(String abbreviation) { this.abbreviation = abbreviation; }
   public String getAbbreviation() { return abbreviation; }

   private String abbreviation;
}
```

**java.lang.Enum<E>**

- `static Enum valueOf(Class enumClass, String name)`  
  returns the enumerated constant of the given class with the given name.
- `String toString()`  
  returns the name of this enumerated constant.
- `int ordinal()`  
  returns the zero-based position of this enumerated constant in the enum declaration.
- `int compareTo(E other)`  
  returns a negative integer if this enumerated constant comes before other, zero if this == other, and a positive integer otherwise. The ordering of the constants is given by the enum declaration.

## 5.7 Reflection

The *reflection library* gives you a very rich and elaborate toolset to write programs that manipulate Java code dynamically. Using reflection, Java can support user interface builders, object-relational mappers, and many other development tools that dynamically inquire about the capabilities of classes.

A program that can analyze the capabilities of classes is called *reflective*. The reflection mechanism is extremely powerful. As the next sections show, you can use it to

- Analyze the capabilities of classes at runtime
- Inspect objects at runtime—for example, to write a single `toString` method that works for *all* classes
- Implement generic array manipulation code
- Take advantage of Method objects that work just like function pointers in languages such as C++

Reflection is a powerful and complex mechanism; however, it is of interest mainly to tool builders, not application programmers. If you are interested in programming applications rather than tools for other Java programmers, you can safely skip the remainder of this chapter and return to it later.

### 5.7.1 The Class Class

While your program is running, the Java runtime system always maintains what is called *runtime type identification* on all objects. This information keeps track of the class to which each object belongs. Runtime type information is used by the virtual machine to select the correct methods to execute.

However, you can also access this information by working with a special Java class. The class that holds this information is called, somewhat confusingly, Class. The `getClass()` method in the Object class returns an instance of Class type.

```
Employee e;
...
Class cl = e.getClass();
```

Just like an Employee object describes the properties of a particular employee, a Class object describes the properties of a particular class. Probably the most commonly used method of Class is `getName`. This returns the name of the class. For example, the statement

```
System.out.println(e.getClass().getName() + " " + e.getName());
```

prints

    Employee Harry Hacker

if e is an employee, or

    Manager Harry Hacker

if e is a manager.

If the class is in a package, the package name is part of the class name:

```java
var generator = new Random();
Class cl = generator.getClass();
String name = cl.getName(); // name is set to "java.util.Random"
```

You can obtain a `Class` object corresponding to a class name by using the static `forName` method.

```java
String className = "java.util.Random";
Class cl = Class.forName(className);
```

Use this method if the class name is stored in a string that varies at runtime. This works if `className` is the name of a class or interface. Otherwise, the `forName` method throws a *checked exception*. See Section 5.7.2, “A Primer on Declaring Exceptions,” on p. 267 for how to supply an exception handler whenever you use this method.

> **TIP:** At startup, the class containing your `main` method is loaded. It loads all classes that it needs. Each of those loaded classes loads the classes that it needs, and so on. That can take a long time for a big application, frustrating the user. You can give the users of your program an illusion of a faster start with the following trick. Make sure the class containing the `main` method does not explicitly refer to other classes. In it, display a splash screen. Then manually force the loading of other classes by calling `Class.forName`.

A third method for obtaining an object of type `Class` is a convenient shorthand. If `T` is any Java type (or the `void` keyword), then `T.class` is the matching class object. For example:

```java
Class cl1 = Random.class; // if you import java.util.*;
Class cl2 = int.class;
Class cl3 = double[].class;
```

Note that a `Class` object really describes a *type*, which may or may not be a class. For example, `int` is not a class, but `int.class` is nevertheless an object of type `Class`.

> **NOTE:** The Class class is actually a generic class. For example, `Employee.class` is of type `Class<Employee>`. We are not dwelling on this issue because it would further complicate an already abstract concept. For most practical purposes, you can ignore the type parameter and work with the raw `Class` type. See Chapter 8 for more information on this issue.

> **CAUTION:** For historical reasons, the `getName` method returns somewhat strange names for array types:
> 
> - `Double[].class.getName()` returns `"[Ljava.lang.Double;"`.
> - `int[].class.getName()` returns `"[I"`.

The virtual machine manages a unique Class object for each type. Therefore, you can use the `==` operator to compare class objects. For example:

```
if (e.getClass() == Employee.class) ...
```

This test passes if e is an instance of Employee. Unlike the condition `e instanceof Employee`, this test fails if e is an instance of a subclass such as Manager.

If you have an object of type Class, you can use it to construct instances of the class. Call the `getConstructor` method to get an object of type Constructor, then use the `newInstance` method to construct an instance. For example:

```
var className = "java.util.Random"; // or any other name of a class with
                                 // a no-arg constructor

Class cl = Class.forName(className);
Object obj = cl.getConstructor().newInstance();
```

If the class doesn’t have a constructor without arguments, the `getConstructor` method throws an exception. You will see in Section 5.7.7, “Invoking Arbitrary Methods and Constructors,” on p. 286 how to invoke other constructors.

> **NOTE:** There is a deprecated `Class.newInstance` method that also constructs an instance with the no-argument constructor. However, if the constructor throws a checked exception, the exception is rethrown without being checked. This violates the compile-time checking of exceptions. In contrast, `Constructor.newInstance` wraps any constructor exception into an `InvocationTargetException`.

> **C++ NOTE:** The `newInstance` method corresponds to the idiom of a *virtual constructor* in C++. However, virtual constructors in C++ are not a language feature but just an idiom that needs to be supported by a specialized library. The `Class` class is similar to the `type_info` class in C++, and the `getClass` method is equivalent to the `typeid` operator. The Java class is quite a bit more versatile than `type_info`, though. The C++ `type_info` can only reveal a string with the name of the type, not create new objects of that type.

**java.lang.Class** 1.0

- `static Class forName(String className)`
  - returns the Class object representing the class with name `className`.
- `Constructor getConstructor(Class... parameterTypes)` 1.1
  - yields an object describing the constructor with the given parameter types. See Section 5.7.7, “Invoking Arbitrary Methods and Constructors,” on p. 286 for more information on how to supply parameter types.

**java.lang.reflect.Constructor** 1.1

- `Object newInstance(Object... params)`
  - constructs a new instance of the constructor’s declaring class, passing `params` to the constructor. See Section 5.7.7, “Invoking Arbitrary Methods and Constructors,” on p. 286 for more information on how to supply parameter types.

**java.lang.Throwable** 1.0

- `void printStackTrace()`
  - prints the Throwable object and the stack trace to the standard error stream.

### 5.7.2 A Primer on Declaring Exceptions

We cover exception handling fully in Chapter 7, but in the meantime you will occasionally encounter methods that threaten to throw exceptions.

When an error occurs at runtime, a program can “throw an exception.” Throwing an exception is more flexible than terminating the program because you can provide a *handler* that “catches” the exception and deals with it.
