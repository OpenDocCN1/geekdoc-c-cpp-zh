An Abstract Class is one which includes an abstract keyword in its declaration and it can or might not contain abstract methods. In a case where a class has an abstract method, it cannot be instantiated and the programmer will have to inherit it from another class to implement the abstract method.

# Encapsulation

Encapsulation in Java programming is the process of wrapping data and methods together. Generally, the variable of one class will be hidden from another class and it can only be accessed through the methods that are being used in their current class. The advantages of encapsulation are that a class could be made read only or write only and it can also have total control over the data stored.

# Recursion

Recursion is a technique referred to a method which calls itself within the program. The recurse() method is called from the main method and can also be called from the same recurse() method as well. This process continues until the given condition is met and if the case is not satisfied, infinite recursion occurs.

Here is a simple implementation of recursion in Java:

```
```java
class Sample {
    static void printFun(int test)
    {
        if (test < 1)
            return;

        else {
            System.out.printf("%d ", test);

            // Statement 2
            printFun(test - 1);

            System.out.printf("%d ", test);
            return;
        }
    }
}
```
```