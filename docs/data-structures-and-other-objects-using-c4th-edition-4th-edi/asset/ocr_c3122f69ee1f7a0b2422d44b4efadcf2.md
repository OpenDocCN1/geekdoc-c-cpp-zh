No doubt you would like to do the same with your impressive new point class:

```
point p;
cin >> p; <--- reads the x and y coordinates
           of p from the standard input
cout << p; <--- writes the x and y coordinates
           of p to the standard output
```

You can provide input/output power to the point class by overloading the << and >> operators. We start by overloading the output operator, which has the mysterious prototype shown here:

```
ostream& operator <<(ostream& outs, const point& source);
```

Let's demystify this problematic prototype. The function has two parameters: outs (which is an ostream) and source (which is a point). We use the function by listing the two arguments like this:

```
cout << p; <--- The first argument, cout, is an ostream.
              The second argument, p, is a point.
```

As shown, the data type of cout is ostream, which means "output stream." The ostream class is part of the iostream library facility. The facility also defines cout (the console output device or "standard output") and provides the ability for programmers to define other output streams (such as output streams connected to a disk file or a printer). In any case, our intention is for the << function to print the point named source to the ostream named outs. We can now write most of our postcondition:

```
ostream& operator <<(ostream& outs, const point& source);
// Postcondition: The x and y coordinates of source have been
// written to outs.
```

The outs parameter is a reference parameter, meaning that the function can change the output stream (by writing to it), and the change will affect the actual argument (such as the standard output stream, cout). The source parameter is a const reference parameter, meaning that the function will not alter the point that it is writing.

One last mystery remains: The return type of the function is ostream&:

```
ostream& operator <<(ostream& outs, const point& source);
```

For the most part, this return type means that the function returns an ostream. In fact, the function returns the ostream that it has just written. There is additional meaning of the & symbol (called a reference return type). But we won't use that additional meaning until Chapter 6, so it is enough to know that the output and input operators both require a reference return type.