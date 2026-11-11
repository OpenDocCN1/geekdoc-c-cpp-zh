This is a serious error, similar to an “index out of bounds” exception. If your program does not “catch” an exception, it is terminated. Normally, programs don’t catch these kinds of exceptions but rely on programmers not to cause them in the first place.

![](bbox=[0.128, 0.221, 0.18, 0.26])

# **TIP:**

When your program is terminated with a `NullPointerException`, the stack trace shows you in which line of your code the problem occurred. Since Java 17, the error message includes the name of the variable or method with the null value. For example, in a call

```
```java
String s = e.getHireDay().toString();
```
```

the error message tells you whether `e` was null or `getHireDay` returned null.

When you define a class, it is a good idea to be clear about which fields can be null. In our example, we don’t want the name or hireDay field to be null. (We don’t have to worry about the salary field. It has primitive type and can never be null.)

The hireDay field is guaranteed to be non-null because it is initialized with a new LocalDate object. But name will be null if the constructor is called with a null argument for n.

There are two solutions. The “permissive” approach is to turn a null argument into an appropriate non-null value:

```
```java
if (n == null) name = "unknown"; else name = n;
```
```

The Objects class has a convenience method for this purpose:

```
```java
public Employee(String n, double s, int year, int month, int day)
```
```