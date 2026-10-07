# CHAPTER 1: App Cubby

discountPercent=15;

}

We have combined two of the examples from above. The new comparison line reads as follows: if totalSpent is greater than discountThreshold AND clubMember is true, we set the discountPercent to 15. In this order for this return True, both items need to be true. || can be used instead of & discountThreshold to say "or". We can change the line above to this:

```
if(totalSpent|| clubMember) {
    discountPercent=15;
}
```

Now this reads: if totalSpent is greater than discountThreshold OR clubMember is true, then set the discount percent. This will return True if either of the options is true.

You can continue to use the logical operations to string as many comparisons together as you need. In some cases, you may need to group comparisons using parentheses. This can be more complicated and is beyond the scope of this book.

# Using the Switch Statement

Up to this point, we've had several example of comparing data by simply using the if statement and/or the if/else statements.

```
if (some_value == SOME_CONSTANT) {
...
} else if (some_value == SOME_OTHER_CONSTANT) {
...
} else if (some_value == YET_SOME_OTHER_CONSTANT) {
...
```

If you need to compare a specific ordinal type to several constant values, you can use a different method that can simplify the comparison code: the switch statement.

> NOTE: An ordinal type is a built-in C data type that can be ordered. Examples are int, long, char, BOOL.

The switch statement allows the comparison of one or more constant values against the ordinal data type. This is important to understand. The switch statement does not allow the comparison of the ordinal type to a variable. Here is an example of a proper switch statement:

```
char value:
value = 'd';

switch (value) { // The switch statement followed by a begin brace
case 'a':      // Equivalent to if (value == 'a')
...\            // Call functions and put any other statements after the
case:
...
```