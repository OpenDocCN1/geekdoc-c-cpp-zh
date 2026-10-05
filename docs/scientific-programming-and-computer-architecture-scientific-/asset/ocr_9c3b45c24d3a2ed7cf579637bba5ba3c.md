# 1.3. C++ review

out of scope at the end of main(), the compiler inserts calls to the destructor (line 8). The destructor is called thrice. When destroying v, the destructor notes that v is the owner of its data and releases the memory that data points to. There is nothing to be done to w1 and w2 because they do not own their data. The destructor returns as soon as it notes that they are not owners.

# References

We will step through a few C++ concepts using the public member functions of the class Vector. The first of these is these references.

A reference in C++ is another name for an object that is already in existence. For example, we may say

```
double &x = y;
```

and x becomes another name for y, which is assumed to be type double. If we say x=2 and then print y, its value will be 2.

The & operator is used to take the address of locations. It is also used for references as illustrated. Overloading the operator in this way may create confusion initially, but in fact references are really just a shorthand for the use of pointers.

We may use references in passing arguments to a function. For example, we define a function as

```
double f(double &x){
  ...
}
```

we may call it as f(z), assuming z is a variable of type double and x will become a reference to z. The call f(2.0) is not legal, however, 2.0 is a value and not the name of a double location.

References are commonly used to pass objects as arguments to functions. The Vector class holds three data items (size, data, and owner), but in general a lot of data can be packed into a single class. When a class is passed as an argument to a function, do we want a fresh copy to be made of all the data inside that object? Typically, the answer is no. First, the expense of having to copy all that data may be undesirable. Second, even if there is only a small amount of data, the semantics could be incorrect. For Vector objects, item-by-item copying results in multiple objects incorrectly owning the same data.