Once again, from the definition of the function `equalTime`, it is clear why it has only one parameter.

Let us again take a look at the definition of the function `equalTime`. Notice that within the definition of this function, the object `otherClock` accesses the member variables `hr`, `min`, and `sec`. However, these member variables are private. So is there any violation? The answer is no. The function `equalTime` is a member of the class `clockType`, and `hr`, `min`, and `sec` are the member variables. Moreover, `otherClock` is an object of type `clockType`. Therefore, the object `otherClock` can access its private member variables within the definition of the function `equalTime`.

The same is true for any member function of a class. In general, when you write the definition of a member function, say, `dummyFunction`, of a class, say, `dummyClass`, and the function uses an object, `dummyObject` of the class `dummyClass`, then within the definition of `dummyFunction`, the object `dummyObject` can access its private member variables (in fact, any private member of the class).

Once a class is properly defined and implemented, it can be used in a program. A program or software that uses and manipulates the objects of a class is called a client of that class.

When you declare objects of the class `clockType`, every object has its own copy of the member variables `hr`, `min`, and `sec`. In object-oriented terminology, variables such as `hr`, `min`, and `sec` are called instance variables of the class because every object instance has its own copy of the data.

# Accessor and Mutator Functions

Let us look at the member functions of the class `clockType`. The function `setTime` sets the values of the member variables to the values specified by the user. In other words, it alters or modifies the values of the member variables. Similarly, the functions `incrementSeconds`, `incrementMinutes`, and `incrementHours` also modify the member variables. On the other hand, functions such as `getTime`, `printTime`, and `equalTime` only access the values of the member variables. They do not modify the member variables. We can, therefore, categorize the member functions of the class `clockType` into two categories: member functions that modify the member variables and member functions that only access, but do not modify, the member variables.

This is typically true for any class. That is, every class has member functions that only access but do not modify the member variables, called accessor functions, and member functions that modify the member variables, called mutator functions.

**Accessor function:** A member function of a class that only accesses (that is, does not modify) the value(s) of the member variable(s).

**Mutator function:** A member function of a class that modifies the value(s) of the member variable(s).

Because an accessor function only accesses the values of the member variables, as a safeguard, we typically include the reserved word `const` at the end of the headings of