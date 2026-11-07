# **Program 13.6**  File app.cpp (Continued)

```
// Instantiation of array object with three elements
Array arr(3);
// Storing values using mutator operator [ ]
arr[0] = 22.31;
arr[1] = 78.61;
arr[2] = 65.22;
// Retrieving values using accessor operator [ ]
for (int i = 0; i < 3; i++)
{
    cout << "Value of arr [" << i << "]: " << arr[i] << endl;
}
return 0;

Run:
Value of arr [0]: 22.31
Value of arr [1]: 78.61
Value of arr [2]: 65.22
```

# ## Function Call Operator

Another unary operator that can be overloaded is the **function call operator**, as shown below:

```
name (list of arguments)
```

The overloading of the function call operator allows us to create a *function object* (sometimes called a *functor*): an instance of an object that acts like a function. If a class overloads the function call operator, the compiler allows us to instantiate an object of this class as though we are calling a function. We are actually wrapping a function in a class that has the benefit of being used in different applications. We can instantiate an object of the class to invoke the function embedded in the class.

The difference between a function object and a function is that the function object can hold its state (a function has no state). For example, a function object called *smallest* can hold the smallest value from the previous call (as a data member). In this way, we can call the function object as many times as we want, and it always gives us the smallest value as long as the object is in scope.

# **EXAMPLE 13.8**

Program 13.7 shows the interface file that declares a class called *Smallest*.

# **Program 13.7**  File smallest.h

```
/*************************************************************
 * The implementation file for the SmartPtr class              *
 *************************************************************/
#ifndef SMALLEST_H
```