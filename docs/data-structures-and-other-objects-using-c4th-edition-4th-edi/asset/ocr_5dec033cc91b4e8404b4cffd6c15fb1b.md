```
point p1, p2;
if (p1 == p2)
    cout << "Those points are equal." << endl;
```

Unfortunately, the == operator cannot be used with a new class—unless you define a binary function that tells exactly what == means. In fact, C++ lets you define the meaning of many operators for a new class. Defining a new meaning for an operator is called **overloading** the operator. We'll look at several common overloading examples.

# Overloading Binary Comparison Operators

The == operator that “compares to equality” can be overloaded for any new class by defining a function with a rather peculiar name. The name of the new function is operator ==, as shown in this example:

```
bool operator ==(const point& p1, const point& p2)
// Postcondition: The value returned is true if p1 and p2
// are identical; otherwise false is returned.
{
    return
    (p1.get_x( ) == p2.get_x( ))
    &&
    (p1.get_y( ) == p2.get_y( ));
}
```

In order for this function to return true, both parts of the && expression must be true—in other words, both x and y coordinates of p1 must be equal to the corresponding coordinate in p2.

Apart from the peculiar name operator ==, the function is just like any other function. It returns a boolean value that can be used as a true-or-false value, such as in an if-statement:

```
if (p1 == p2)...
```

The overloaded operator is used in a program just like any other use of ==, by putting the first argument before == and the second argument after ==

When you overload an operator, the common usages of that operator are still available. For example, we can still use == to test the equality of two integers or two doubles. In fact, in the body of our operator ==, we do use the ordinary == to compare the doubles p1.get_x( ) and p2.get_x( ). This is fine. For each use of ==, the compiler determines the data type of the objects being compared and uses the appropriate comparison function.

Once you have overloaded one operator, you can sometimes use the overloaded operator to make an easy implementation of another operator. For

> operator ==

> common usages of == are still available