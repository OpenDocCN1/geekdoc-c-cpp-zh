
Each call to operator << therefore passes on its left argument as its result which becomes the left argument of the next call to operator <<.
The statement is really interpreted as:

```
(((cout << "x = " << x << ", y = " << y)) << endl;
```

It's important for operator << to return an ofstream so that several uses of it can be chained together. So for it to work, the value of cout << must be a reference to cout!

References become even more important for input. Without them, it would be impossible for:

```
cin >> x;
```

to change the value of x.

For this reason, the right argument of operator >> is always a reference.

Usually the functions we've seen tell us what value will be returned. But now, by allowing a function to return a reference, the function is allowed to be the target of an assignment, i.e., used as an lvalue (on the left-hand side of an = sign).

Here's a trivial example:

```
int& foo(int &x) {
  return x;
}
```

This function simply returns a reference to its argument. We can now write:

```
int a;
foo(a) = 7;      // sets a to 7
```

# Another example:

```
int array[100];    // static storage
int& getItem(int index) {
    return array[index];
}

int main() {
    getItem(4) = 5;    // not allowed in C
    return 0;
}
```

The function call is now an lvalue array[4] is now = 5. Function getItem() will tell you at which location a value will be assigned. For example, function getItem() returns a reference to the element of the array index and sets it to 5.

Just as passing arguments by reference prevents unnecessary copying to the stack, which can return an object by reference to avoid copying the returned object.

Check what happens when you return an object by value. For example, suppose you return a String object from a function addString() which returns the concatenation of two strings:

```
String addString(const String& s1) {
    String s;

    // append s1 and s2 to a
    ...
    
    return s;
}
```

In this case, the return statement has to copy the String s to an area of memory provided by the calling program. To do so properly, the return statement will call a special constructor, the copy constructor, which can create and initialize a new instance of an object from an existing one. After creating the copy, return calls the destructor of the String class to destroy s before returning to the calling program. This is a good example of work done behind the scenes by the C++ compiler.

Although returning by reference would save the time spent in copying the object, you cannot return a reference to String s because s is a temporary object that exists only within the function add() and is destroyed when the function returns. Note: because a reference is a pointer, you cannot return a reference to anything that is temporary!! You should never return a reference to a local variable the local variable will disappear as soon as the function returns and the reference will lead nowhere. This is called a dangling reference. Be sure that if you return a reference, it refers to an object that will still be around after the function returns.

Note that there is nothing wrong with returning a formal parameter as a reference provided that the formal parameter is itself a reference. For example:

```
// don't do this
int& foo(int x) {
    return x;
}

// but this is OK
int& foo(int& x) {
    return x;
}
```

Here the parameter x is just an alternate name for something that existed before foo() was called and will presumably exist after foo() has returned.

There would have been no problem returning a reference to a global or static variable or to a formal parameter that is itself a reference.

# ❖ References Homework

Create a function that takes a char& argument and modifies that argument. In main(), print out the value of a char variable, call your function for that variable, and print it out again to prove to yourself that it has been changed. Be sure to show all output. How does this affect program readability?

# Chapter 11. Operator Overloading

- Introduction to Operator Overloading
- Overloading Unary Operators
- Distinguishing Prefix and Postfix for ++ and -- Operators
- Overloading Binary Operators
- Overloading Arithmetic Assignment Operators
- Selecting Friend or Member Functions
- Concatenating String with + Operator
- Overloading the Comparison == Operator
- Overloading the Insertion << and Extraction >> Operators
- Updated Distance Class
- Overloading the Subscript Operator []
- Operator Overloading Homework
- Operator Overloading Lab (IntArray)
- Operator Overloading Lab (IntArray) Driver

# Introduction to Operator Overloading

Operator overloading is one of the most exciting features of object-oriented programming. It can transform complex, obscure programs into intuitively obvious ones. For example, a statement like:

```
d3.addObjects(d1, d2);
```

can be changed to the much more readable:

```
d3 = d1 + d2;
```

The term operator overloading refers to giving the normal C++ operators additional meanings when they are applied to user-defined types. We're already familiar with operator overloading:

```
c = a + b;
```

When you use the plus sign with int values, one specific set of machine language instructions is involved. When used with float values, one specific set of machine language instructions is involved.
