This sounds like a convenient mechanism for dealing with special situations, such as an unknown name or hire date. But you need to be very careful with null values.

If you apply a method to a null value, a NullPointerException occurs.

```
```java
LocalDate birthday = null;
String s = birthday.toString(); // NullPointerException
```
```

This is a serious error, similar to an “index out of bounds” exception. If your program does not “catch” an exception, it is terminated. Normally, programs don’t catch these kinds of exceptions but rely on programmers not to cause them in the first place.

When you define a class, it is a good idea to be clear about which fields can be null. In our example, we don’t want the name or hireDay field to be null. (We don’t have to worry about the salary field. It has primitive type and can never be null.)

The hireDay field is guaranteed to be non-null because it is initialized with a new LocalDate object. But name will be null if the constructor is called with a null argument for n.

There are two solutions. The “permissive” approach is to turn a null argument into an appropriate non-null value:

```
```java
if (n == null) name = "unknown"; else name = n;
```
```

As of Java 9, the Objects class has a convenience method for this purpose:

```
```java
public Employee(String n, double s, int year, int month, int day)
{
   name = Objects.requireNonNullElse(n, "unknown");
   . . .
}
```
```

The “tough love” approach is to reject a null argument:

```
```java
public Employee(String n, double s, int year, int month, int day)
{
   Objects.requireNonNull(n, "The name cannot be null");
   name = n;
   . . .
}
```
```

If someone constructs an Employee object with a null name, then a NullPointerException occurs. At first glance, that may not seem a useful remedy. But there are two advantages: