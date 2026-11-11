The compiler passes a new `double[] { 3.1, 40.4, -5 }` to the `max` function.

# **NOTE:**

It is legal to pass an array as the last parameter of a method with variable parameters. For example:

```
```java
System.out.printf("%d %s", new Object[] { Integer.valueOf(1),
"widgets" } );
```
```

Therefore, you can redefine an existing function whose last parameter is an array to a method with variable parameters, without breaking any existing code. For example, `MessageFormat.format` was enhanced in this way in Java 5. If you like, you can even declare the `main` method as

```
```java
public static void main(String... args)
```
```

# 5.6 Abstract Classes

As you move up the inheritance hierarchy, classes become more general and probably more abstract. At some point, the ancestor class becomes *so* general that you think of it more as a basis for other classes than as a class with specific instances you want to use. Consider, for example, an extension of our `Employee` class hierarchy. An employee is a person, and so is a student. Let us extend our class hierarchy to include classes `Person` and `Student`. Figure 5.2 shows the inheritance relationships between these classes.