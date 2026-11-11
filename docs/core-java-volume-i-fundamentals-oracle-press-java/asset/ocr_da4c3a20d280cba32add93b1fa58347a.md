Never rely on the identity of wrapper objects. Don’t compare them with `==` and don’t use them as locks (see Chapter 14).

Don’t use the wrapper class constructors. They are deprecated and scheduled for removal. For example, use `Integer.valueOf(1000)`, never `new Integer(1000)`. Or, simply rely on auto-boxing: `Integer a = 1000`.

There are a couple of other subtleties about autoboxing. First off, since wrapper class references can be `null`, it is possible for autounboxing to throw a `NullPointerException`:

```
```java
Integer n = null;
System.out.println(2 * n); // throws NullPointerException
```
```

Also, if you mix `Integer` and `Double` types in a conditional expression, then the `Integer` value is unboxed, promoted to `double`, and boxed into a `Double`:

```
```java
Integer n = 1;
Double x = 2.0;
System.out.println(true ? n : x); // prints 1.0
```
```

Finally, let us emphasize that boxing and unboxing is a courtesy of the *compiler*, not the virtual machine. The compiler inserts the necessary calls when it generates the bytecodes of a class. The virtual machine simply executes those bytecodes.

![](bbox=[0.13, 0.668, 0.172, 0.701])

# **NOTE:**

A future version of Java will allow user-defined types that are like primitive types—with values that are not stored inside objects. For example, a value of a primitive type `Point` with `double` fields `x` and `y` is simply a 16-byte block in memory, with two adjacent `double` values. You can copy it, but you can’t have a reference to it.