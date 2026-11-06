The preceding output has a couple of interesting cases:

+   * The last three lines of the preceding output are scientific notation to maintain four significant digits.
+   * The fourth line from the end, 1235 , is rounded up from 1234.9 because of this line:

```
cout << 1234.9 << endl;
```

The precision function has an associated manipulator. Instead of calling precision as a function, you can use it as a manipulator. But the manipulator's name is slightly different: It's setprecision. To use it, you include this header:

```
#include <iomanip>
```

These two lines cause the same thing to happen:

```
cout.precision(4);
```

```
cout << setprecision(4);
```

And these two lines are available for all the recent more-or-less-ANSI-compliant compilers, even those that aren't fully compliant. Yay! Just make sure you remember to add #include <iomanip>, or you will get a compiler error.

# ### Setting the width and creating fields

This is where you can start making the numbers and data all nice and neat by aligning them in columns. To align your data, use the width member function for the stream or cout, passing the width of the field, like this:

```
cout.width(10);
```

Then, when you print a number, think of the number as sitting inside a field 10 spaces wide, with the number wedged against the right side of these 10 spaces. For example, look at this:

```
cout.width(10);
cout << 20 << endl;
```

This code produces this output:

```
20
```

Although seeing this in the printed text is hard, this 20 is pushed to the right of a field of spaces 10 characters wide. That is, because the 20 takes two character spaces, there are eight spaces to the left of it.