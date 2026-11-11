# 5.3 Generic Array Lists

In some programming languages—in particular, in C and C++—you have to fix the sizes of all arrays at compile time. Programmers hate this because it forces them into uncomfortable tradeoffs. How many employees will be in a department? Surely no more than 100. What if there is a humongous department with 150 employees? Do we want to waste 90 entries for every department with just 10 employees?

In Java, the situation is somewhat better. You can set the size of an array at runtime.

```
int actualSize = ...;
var staff = new Employee[actualSize];
```

Of course, this code does not completely solve the problem of dynamically modifying arrays at runtime. Once you set the array size, you cannot change it easily. Instead, in Java you can deal with this common situation by using another Java class, called ArrayList. The ArrayList class is similar to an array, but it automatically adjusts its capacity as you add and remove elements, without any additional code.

ArrayList is a generic class with a type parameter. To specify the type of the element objects that the array list holds, you append a class name enclosed in angle brackets, such as ArrayList<Employee>. You will see in Chapter 8 how to define your own generic class, but you don’t need to know any of those technicalities to use the array list type.

The following sections show you how to work with array lists.

# 5.3.1 Declaring Array Lists

Here is how to declare and construct an array list that holds Employee objects:

```
ArrayList<Employee> staff = new ArrayList<Employee>();
```

As of Java 10, it is a good idea to use the var keyword to avoid duplicating the class name:

```
var staff = new ArrayList<Employee>();
```

If you don’t use the var keyword, you can omit the type parameter on the right-hand side:

```
ArrayList<Employee> staff = new ArrayList<>();
```

This is called the “diamond” syntax because the empty brackets <> resemble a diamond. Use the diamond syntax together with the new operator. The