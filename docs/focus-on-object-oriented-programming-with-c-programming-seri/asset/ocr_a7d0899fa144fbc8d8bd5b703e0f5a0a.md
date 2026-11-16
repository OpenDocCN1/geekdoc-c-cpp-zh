```
int main() {
    Distance d1, d2;
    cout << "Enter two Distance values: ";
    cin >> d1 >> d2;
    Distance d3(11, 6.25);
    cout << "d1 = " << d1 << endl;
    cout << "d2 = " << d2 << endl;
    cout << "d3 = " << d3 << endl;
    return 0;
}
```

This program asks for two distance values from the user, and then prints out these values and another value that was initialized in the program. Note that arguments are passed by reference for efficiency.

The input and output operators require, respectively, an istream and ostream object as their left operand. Both return the object upon which they operate. This allows successive input or output operators to be concatenated.

For example:

```
((((( cout << "d1 = " << d1) << "d2 = ") << d2) << endl);
```

Here, each parenthetical sub-expression returns the ostream object cout which becomes the left operand of the next outermost expression.

Because the design of iostreams, an overloaded operator<<() or operator>>() function must be a friend function and it must take arguments of an istream object (either istream or ostream, depending on the operator) followed by an object of your user-defined type. The function must return the same stream object as it takes as an argument.

Note, it's important that the stream object be passed into and out of the function so you can have expressions of the form:

```
cout << obj1 << obj2;
```

In effect, each object is passed to the stream and then the stream is passed down the line.