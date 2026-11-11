Now the array is either `["Paul", "Mary", "Peter"]` or `["Mary", "Paul", "Peter"]`.

You will see in [Section 6.2, “Lambda Expressions,”](#) on p. 338 how to use a Comparator much more easily with a lambda expression.

# 6.1.9 Object Cloning

In this section, we discuss the `Cloneable` interface that indicates that a class has provided a safe clone method. Since cloning is not all that common, and the details are quite technical, you may just want to glance at this material until you need it.

To understand what cloning means, recall what happens when you make a copy of a variable holding an object reference. The original and the copy are references to the same object (see [Figure 6.1](#)). This means a change to either variable also affects the other.

```
```java
var original = new Employee("John Public", 50000);
Employee copy = original;
copy.raiseSalary(10); // oops--also changed original
```
```