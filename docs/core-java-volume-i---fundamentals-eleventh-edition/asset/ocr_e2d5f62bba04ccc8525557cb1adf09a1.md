running program, all array lists are the same—there are no type parameters in the virtual machine. Thus, the casts (`ArrayList`) and (`ArrayList<Employee>`) carry out identical runtime checks.

There isn’t much you can do about that situation. When you interact with legacy code, study the compiler warnings and satisfy yourself that the warnings are not serious.

Once you are satisfied, you can tag the variable that receives the cast with the `@SuppressWarnings("unchecked")` annotation, like this:

```
```java
@SuppressWarnings("unchecked") ArrayList<Employee> result
    = (ArrayList<Employee>) employeeDB.find(query); // yields another warning
```
```

# 5.4 Object Wrappers and Autoboxing

Occasionally, you need to convert a primitive type like int into an object. All primitive types have class counterparts. For example, a class Integer corresponds to the primitive type int. These kinds of classes are usually called *wrappers*. The wrapper classes have obvious names: Integer, Long, Float, Double, Short, Byte, Character, and Boolean. (The first six inherit from the common superclass Number.) The wrapper classes are immutable—you cannot change a wrapped value after the wrapper has been constructed. They are also final, so you cannot subclass them.

Suppose we want an array list of integers. Unfortunately, the type parameter inside the angle brackets cannot be a primitive type. It is not possible to form an `ArrayList<int>`. Here, the Integer wrapper class comes in. It is OK to declare an array list of Integer objects.

```
```java
var list = new ArrayList<Integer>();
```
```

> **CAUTION:** An `ArrayList<Integer>` is far less efficient than an `int[]` array because each value is separately wrapped inside an object. You would only want to use this construct for small collections when programmer convenience is more important than efficiency.

Fortunately, there is a useful feature that makes it easy to add an element of type int to an `ArrayList<Integer>`. The call

```
```java
list.add(3);
```
```

is automatically translated to