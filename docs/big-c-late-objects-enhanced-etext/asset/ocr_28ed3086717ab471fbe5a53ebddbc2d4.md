```
// Many compilers report the error in this line
...
}
```

This error can be extremely confusing to many compilers. There is syntax, now obsolete but supported for compatibility with old code, to define class types and variables of that type simultaneously. Because the compiler doesn't know that you don't use that obsolete construction, it tries to analyze the code wrongly and ultimately reports an error. Unfortunately, it may report the error several lines away from the line in which you forgot the semicolon.

If the compiler reports bizarre errors in lines that you are sure are correct, check that each of the preceding class definitions is terminated by a semicolon.

# 9.4 Designing the Data Representation

An object holds data members that are accessed by member functions.

An object stores its data in data members. These are variables that are declared inside the class.

![](bbox=[0.62, 0.57, 0.95, 0.9])

When implementing a class, you have to determine which data each object needs to store. The object needs to have all the information necessary to carry out any member function call.

Go through all member functions and consider their data requirements. It is a good idea to start with the accessor functions. For example, a CashRegister object must be able to return the correct value for the get_total function. That means, it must either store all entered prices and compute the total in the function call, or it must store the total.

Now apply the same reasoning to the get_count function. If the cash register stores all entered prices, it can count them in the get_count function. Otherwise, you need to have a variable for the count.

The data members are defined in the private section of the class definition:

```
class CashRegister
{
```