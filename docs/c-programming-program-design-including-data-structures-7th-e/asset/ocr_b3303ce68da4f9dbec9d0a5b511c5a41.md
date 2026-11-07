Notice that in this program, the variable `letter` is the loop control variable. First, it is initialized in Line 11, by the input statement, and then updated in Line 33. The expression in Line 13 checks whether `letter` is #.

> **NOTE** The statements in Lines 17 to 29 can be written using a `switch` statement by checking each letter and outputting the corresponding telephone digit as follows:

```
if (letter >= 'A' && letter <= 'Z')
    switch (letter)
    {
    case 'A':
    case 'B':
    case 'C':
        cout << 2 << endl;
        break;
    case 'D':
    case 'E':
    case 'F':
        cout << 3 << endl;
        break;
    .
    .
    .
    }
```

However, this code will be very long and occupy a considerable amount of space.

# Case 3: Flag-Controlled `while` Loops

A flag-controlled `while` loop uses a Boolean variable to control the loop. A flag variable is a `bool` variable that indicates whether a condition is `true` or `false`. It is generally named for the true state of that condition; for example, `isFound`, `isTallEnough`, and `isFull`. Suppose `isFound` is a `bool` variable. The flag-controlled `while` loop takes the following form:

```
isFound = false;        // initialize the loop control variable

while (!isFound)         // test the loop control variable
{
    .
    .
    .
    if (expression)
        isFound = true;  // update the loop control variable
    .
    .
}
```