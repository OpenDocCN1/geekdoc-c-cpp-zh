For example, when you create an instance of the `Employee` class with code like this:

```
```java
new Employee("James Bond", 100000, 1950, 1, 1)
```
```

you have set the instance fields as follows:

```
```java
name = "James Bond";
salary = 100000;
hireDay = LocalDate.of(1950, 1, 1); // January 1, 1950
```
```

There is an important difference between constructors and other methods. A constructor can only be called in conjunction with the new operator. You can’t apply a constructor to an existing object to reset the instance fields. For example,

```
```java
james.Employee("James Bond", 250000, 1950, 1, 1) // ERROR
```
```

is a compile-time error.

We will have more to say about constructors later in this chapter. For now, keep the following in mind:

+   - A constructor has the same name as the class.
+   - A class can have more than one constructor.
+   - A constructor can take zero, one, or more parameters.
+   - A constructor has no return value.
+   - A constructor is always called with the new operator.

![](bbox=[0.128, 0.797, 0.181, 0.838])

# C++ NOTE:

Constructors work the same way in Java as they do in C++. Keep in mind, however, that all Java objects are constructed on the heap and that a