Instead, interfaces afford most of the benefits of multiple inheritance while avoiding the complexities and inefficiencies.

![](bbox=[0.193, 0.208, 0.237, 0.24])

> **C++ NOTE:** C++ has multiple inheritance and all the complications that come with it, such as virtual base classes, dominance rules, and transverse pointer casts. Few C++ programmers use multiple inheritance, and some say it should never be used. Other programmers recommend using multiple inheritance only for the “mix-in” style of inheritance. In the mix-in style, a primary base class describes the parent object, and additional base classes (the so-called mix-ins) may supply auxiliary characteristics. That style is similar to a Java class with a single superclass and additional interfaces.

# 6.1.4 Static and Private Methods

As of Java 8, you are allowed to add static methods to interfaces. There was never a technical reason why this should be outlawed. It simply seemed to be against the spirit of interfaces as abstract specifications.

Up to now, it has been common to place static methods in companion classes. In the standard library, you’ll find pairs of interfaces and utility classes such as `Collection`/`Collections` or `Path`/`Paths`.

You can construct a path to a file or directory from a URI, or from a sequence of strings, such as `Paths.get("jdk-11", "conf", "security")`. In Java 11, equivalent methods are provided in the `Path` interface:

```
```java
public interface Path
{
    public static Path of(URI uri) { . . . }
    public static Path of(String first, String... more) { . . . }
    . . .
}
```
```

Then the Paths class is no longer necessary.

Similarly, when you implement your own interfaces, there is no longer a reason to provide a separate companion class for utility methods.

As of Java 9, methods in an interface can be private. A private method can be static or an instance method. Since private methods can only be used in the methods of the interface itself, their use is limited to being helper methods for the other methods of the interface.