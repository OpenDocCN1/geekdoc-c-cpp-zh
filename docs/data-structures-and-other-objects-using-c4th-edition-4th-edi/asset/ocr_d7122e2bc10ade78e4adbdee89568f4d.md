With this in mind, we can now write the complete postcondition:

```
ostream& operator <<(ostream& outs, const point& source);
// Postcondition: The x and y coordinates of source have been
// written to outs. The return value is the ostream outs.
```

The reason that the function returns an ostream is that C++ will then permit the “chaining” of output statements such as the following:

```
cout << "The points are " << p << " and " << q << endl;
```

This example calls five << functions, with each function changing the ostream and passing the result on to the next function call.

The complete implementation of the point’s output operator is shown at the top of Figure 2.17. Most of the work is done in this statement:

```
outs << source.get_x( ) << " " << source.get_y( );
```

The statement uses the ordinary << operator to print the coordinates of the point, with a single blank character in between.

# FIGURE 2.17 Output and Input Operations for the Point

# Function Implementations

```
ostream& operator <<(ostream& outs, const point& source)
// Postcondition: The x and y coordinates of source have been
// written to outs. The return value is the ostream outs.
// Library facilities used: iostream
{
    outs << source.get_x( ) << " " << source.get_y( );
    return outs;
}

istream& operator >>(istream& ins, point& target)
// Postcondition: The x and y coordinates of target have been
// read from ins. The return value is the istream ins.
// Library facilities used: iostream
// Friend of: point class
{
    ins >> target.x >> target.y;
    return ins;
}
```