The next day, you need a third function that returns the larger of two strings, (using the > relationship from the Standard Library string class). You'll write a third function:

```
string maximal(string a, string b)
// Postcondition: The return value is the larger of a and b.
{
   if (a > b)
      return a;
   else
      return b;
}
```

In fact, a single program can use all three of the maximal functions. When one of the functions is used, the compiler looks at the type of the arguments and selects the appropriate version of the maximal function. But with this approach, you do need to write a new function for each type of value that you want to compare.

Of course, you could write just one function, along with a typedef statement, like this:

```
typedef _______ item;
item maximal(item a, item b)
// Postcondition: The return value is the larger of a and b.
{
   if (a > b)
      return a;
   else
      return b;
}
```

Now, a programmer can fill in the typedef statement with any data type that has the > operator defined and that has a copy constructor. The copy constructor is needed because the function has two value parameters and returns an item, both of which use the copy constructor (see “Returning an object from a function” on page 196).

But the typedef approach has a problem. Suppose that a single program needs to use several different versions of the maximal function. The typedef approach does not allow this, since the program can define only one data type for the item.

The solution is a more flexible mechanism called a template function, which is similar to an ordinary function with one important difference: The definition of a template function can depend on an underlying data type. The underlying data type is given a name—such as Item—but Item is not pinned down to a specific type anywhere in the function’s implementation. When a template function is used, the compiler examines the types of the arguments and at that point the compiler automatically determines the data type of Item. Moreover, in a single program, several different usages of a template function can result in several different underlying data types.