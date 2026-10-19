usual unhelpful name x or temp). Here’s an example that shows a temporary variable that’s used for two purposes:

# C++ Example of Using One Variable for Two Purposes—Bad Practice

```
// Compute roots of a quadratic equation.
// This code assumes that (b*b-4*a*c) is positive.
temp = Sqrt( b*b - 4*a*c );
root[0] = ( -b + temp ) / ( 2 * a );
root[1] = ( -b - temp ) / ( 2 * a );
...

// swap the roots
temp = root[0];
root[0] = root[1];
root[1] = temp;
```

Cross-Reference Routine parameters should also be used for one purpose only. For details on using routine parameters, see Section 7.5, "How to Use Routine Parameters."

Question: What is the relationship between temp in the first few lines and temp in the last few? Answer: The two temps have no relationship. Using the same variable in both instances makes it seem as though they’re related when they’re not. Creating unique variables for each purpose makes your code more readable. Here’s an improvement:

# C++ Example of Using Two Variables for Two Purposes—Good Practice

```
// Compute roots of a quadratic equation.
// This code assumes that (b*b-4*a*c) is positive.
discriminant = Sqrt( b*b - 4*a*c );
root[0] = ( -b + discriminant ) / ( 2 * a );
root[1] = ( -b - discriminant ) / ( 2 * a );
...

// swap the roots
oldRoot = root[0];
root[0] = root[1];
root[1] = oldRoot;
```

# Avoid variables with hidden meanings

Another way in which a variable can be used for more than one purpose is to have different values for the variable mean different things. For example:

+   - The value in the variable pageCount might represent the number of pages printed, unless it equals -1, in which case it indicates that an error has occurred.
+   - The variable customerId might represent a customer number, unless its value is greater than 500,000, in which case you subtract 500,000 to get the number of a delinquent account.
+   - The variable bytesWritten might be the number of bytes written to an output file, unless its value is negative, in which case it indicates the number of the disk drive used for the output.

![](bbox=[0.11, 0.15, 0.19, 0.23])

![](bbox=[0.11, 0.75, 0.19, 0.83])