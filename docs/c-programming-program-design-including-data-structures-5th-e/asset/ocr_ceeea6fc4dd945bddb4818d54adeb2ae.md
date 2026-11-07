by overloading the operators `~` and `!` as member functions so that `~` returns the conjugate of a complex number and `!` returns the absolute value. Also, write the definitions of these operator functions.

+   24. Redo Exercise 23 so that the operators `~` and `!` are overloaded as non-member functions.

+   25. Find the error(s) in the following code:

```
template <class type>        //Line 1
class strange             //Line 2
{
    .
    .
    .
};

strange<int> s1;          //Line 3
strange<type> s2;          //Line 4
```

+   26. Consider the following declaration:

```
template <class type>
class strange
{
    .
    .
    .
private:
    type a;
    type b;
};
```

+   a. Write a statement that declares `sObj` to be an object of type `strange` such that the private member variables `a` and `b` are of type `int`.

+   b. Write a statement that shows the declaration in the class `strange` to overload the operator `==` as a member function.

+   c. Assume that two objects of type `strange` are equal if their corresponding member variables are equal. Write the definition of the function `operator==` for the class `strange`, which is overloaded as a member function.

+   27. Consider the definition of the following function template:

```
template <class Type>
Type surprise(Type x, Type y)
{
    return x + y;
}
```

What is the output of the following statements?

+   a. `cout << surprise(5, 7) << endl;`

+   b. `string str1 = "Sunny";`
+      `string str2 = "Day";`
+      `cout << surprise(str1, str2) << endl;`