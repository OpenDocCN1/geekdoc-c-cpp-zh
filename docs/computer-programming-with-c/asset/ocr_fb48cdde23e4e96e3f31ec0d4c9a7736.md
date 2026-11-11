invoke public functions like `setA()` and `setB()` using object o1. These are public functions invoked to initialize the members a and b. They essentially provide a gateway to initialize the private member a and protected member b from outside class.

As `setA()` is a member function of class Abc, when o1 invokes the `setA()` function the control of execution is actually transferred inside class Abc as shown in the Figure 14.13. Given that `setA()` is defined inside class Abc, we can directly access the **private member** a within the body of function `setA()`. The function initializes member variable a with an argument passed to it. Hence the following statement:

```
```cpp
o1.setA(10);
```
```

will set the value of member a of object o1 as 10 as shown in the Figure 14.13.

![](bbox=[0.225, 0.317, 0.787, 0.526])

**Figure 14.13:** Invoking `setA()` function using object o1

> **NOTES**
> 
> o1 is an object of class C1, whereas the function `setA()` is defined in class Abc, you can still invoke `setA()` using o1 because C1 is a **child class** of Abc.

Similarly, we invoke a function `setB()` of a parent class using object o1 to initialize protected member b to 20 as shown in the Figure 14.14. In actuality, there is no restriction imposed by the protected access specifier for us to enter in the scope of parent class to initialize the value of member b, however we are doing it in this case because there is a function named as `setB()` already defined within the scope of class Abc, and there is no reason for us to create another function for the same reason again in the child class. Yet, if the programmers want to define a function in the child class to do the same job, they are free to do so technically, but this would be silly because you are defining the same thing again in child, which could be rather reused from parent. Don’t forget, reusability of code is one of the major reasons of implementing inheritance.

The initialization of the member c can be done directly from the `main()` function because the member c is a public member inherited by the object o1. Hence, we can initialize the value of member c directly from `main()` using the statement below:

```
```cpp
o1.c = 30;
```
```