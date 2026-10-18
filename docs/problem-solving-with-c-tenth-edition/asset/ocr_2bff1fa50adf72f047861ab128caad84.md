# CHAPTER SUMMARY

+   - A friend function of a class is an ordinary function except that it has access to the private members of the class, just like the member functions do.
+   - If your classes each have a full set of accessor and mutator functions, then the only reason to make a function a friend is to make the definition of the friend function simpler and more efficient, but that is often reason enough.
+   - A parameter of a class type that is not changed by the function should normally be a constant parameter.
+   - Operators, such as `+` and `==`, can be overloaded so they can be used with objects of a class type that you define.
+   - When overloading the `>>` or `<<` operators, the type returned should be a stream type and must be a reference, which is indicated by appending an `&` to the name of the returned type.
+   - The base type of an array can be a structure or class type. A structure or class can have an array as a member variable.
+   - A **destructor** is a special kind of member function for a class. A destructor is called automatically when an object of the class passes out of scope. The main reason for destructors is to return memory to the free store so the memory can be reused.
+   - A **copy constructor** is a constructor that has a single argument that is of the same type as the class. If you define a copy constructor, it will be called automatically whenever a function returns a value of the class type and whenever an argument is “plugged in” for a call-by-value parameter of the class type. Any class that uses pointers and the operator `new` should have a copy constructor.
+   - The assignment operator `=` can be overloaded for a class so that it behaves as you wish for that class. However, it must be overloaded as a member of the class; it cannot be overloaded as a friend. Any class that uses pointers and the operator `new` should overload the assignment operator for use with that class.

# Answers to Self-Test Exercises

```
1. `bool before(DayOfYear date1, DayOfYear date2)
   {
       return ((date1.getMonth() < date2.getMonth())
            || (date1.getMonth() == date2.getMonth()
                && date1.getDay() < date2.getDay()));
   }`
```