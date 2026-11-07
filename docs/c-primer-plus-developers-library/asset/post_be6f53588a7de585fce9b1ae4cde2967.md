
```cpp
{
    cout.put(char(ch));
    ++count;
}
cout << endl << count << " characters read\n";
return 0;
}
```

> **Note**
>
> Some systems either do not support simulated EOF from the keyboard or support it imperfectly, and that may prevent the example in Listing 5.19 from running as described. If you have been using `cin.get()` to freeze the screen until you can read it, that won’t work here because detecting the EOF turns off further attempts to read input. However, you can use a timing loop like that in Listing 5.14 to keep the screen visible for a while. Or you can use `cin.clear()`, as described in Chapter 17, to reset the input stream.

Here’s a sample run of the program in Listing 5.19:

```text
The sullen mackerel sulks in the shadowy shallows.<ENTER>
The sullen mackerel sulks in the shadowy shallows.
Yes, but the blue bird of happiness harbors secrets.<ENTER>
Yes, but the blue bird of happiness harbors secrets.
<CTRL><Z><ENTER>
104 characters read
```

Let’s analyze the loop condition:

```cpp
while ((ch = cin.get()) != EOF)
```

The parentheses that enclose the subexpression `ch = cin.get()` cause the program to evaluate that expression first. To do the evaluation, the program first has to call the `cin.get()` function. Next, it assigns the function return value to `ch`. Because the value of an assignment statement is the value of the left operand, the whole subexpression reduces to the value of `ch`. If this value is `EOF`, the loop terminates; otherwise, it continues. The test condition needs all the parentheses. Suppose you leave some parentheses out:

```cpp
while (ch = cin.get() != EOF)
```

The `!=` operator has higher precedence than `=`, so first the program compares `cin.get()`’s return value to `EOF`. A comparison produces a false or true result; that bool value is converted to 0 or 1, and that’s the value that gets assigned to `ch`. Using `cin.get(ch)` with an argument for input, on the other hand, doesn’t create any type problems. Remember that the `cin.get(char)` function doesn’t assign a special value to `ch` at the EOF. In fact, it doesn’t assign anything to `ch` in that case, `ch` is never called on to hold a non-char value. Table 5.3 summarizes the differences between `cin.get(char)` and `cin.get()`.

### Table 5.3  `cin.get(ch)` Versus `cin.get()`

| Property | `cin.get(ch)` | `ch=cin.get()` |
|---|---|---|
| Method for conveying input character | Assign to argument `ch` | Use function return value to assign to `ch` |
| Function return value for character input | A class `istream` object (true after `bool` conversion) | Code for character as type `int` value |
| Function return value at EOF | A class `istream` object (false after `bool` conversion) | `EOF` |

So which should you use, `cin.get()` or `cin.get(char)`? The form with the character argument is integrated more fully into the object approach because its return value is an `istream` object. This means, for example, that you can chain uses. For example, the following code means read the next input character into `ch1` and the following input character into `ch2`:

```cpp
cin.get(ch1).get(ch2);
```

This works because the function call `cin.get(ch1)` returns the `cin` object, which then acts as the object to which `get(ch2)` is attached.

Probably the main use for the `get()` form is to let you make quick-and-dirty conversions from the `getchar()` and `putchar()` functions of `stdio.h` to the `cin.get()` and `cout.put()` methods of `iostream`. You just replace one header file with the other and globally replace `getchar()` and `putchar()` with their act-alike method equivalents. (If the old code uses a type `int` variable for input, you have to make further adjustments if your implementation has multiple prototypes for `put()`.)

## Nested Loops and Two-Dimensional Arrays

Earlier in this chapter you saw that the `for` loop is a natural tool for processing arrays. Now let’s go a step further and look at how a `for` loop within a `for` loop (nested loops) serves to handle two-dimensional arrays.

First, let’s examine what a two-dimensional array is. The arrays used so far in this chapter are termed one-dimensional arrays because you can visualize each array as a single row of data. You can visualize a two-dimensional array as being more like a table, having both rows and columns of data. You can use a two-dimensional array, for example, to represent quarterly sales figures for six separate districts, with one row of data for each district. Or you can use a two-dimensional array to represent the position of RoboDork on a computerized game board.

C++ doesn’t provide a special two-dimensional array type. Instead, you create an array for which each element is itself an array. For example, suppose you want to store maximum temperature data for five cities over a 4-year period. In that case, you can declare an array as follows:

```cpp
int maxtemps[4][5];
```

This declaration means that `maxtemps` is an array with four elements. Each of these elements is an array of five integers (see Figure 5.5). You can think of the `maxtemps` array as representing four rows of five temperature values each.

![](img/9afc44517b591d64e2e19f623c9308ef_259_0.png)

The expression `maxtemps[0]` is the first element of the `maxtemps` array; hence `maxtemps[0]` is itself an array of five ints. The first element of the `maxtemps[0]` array is `maxtemps[0][0]`, and this element is a single int. Thus, you need to use two subscripts to access the int elements. You can think of the first subscript as representing the row and the second subscript as representing the column (see Figure 5.6).

```cpp
int maxtemps[4][5];
```

The `maxtemps` array viewed as a table:

| | 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|---|
| maxtemps[0] | maxtemps[0][0] | maxtemps[0][1] | maxtemps[0][2] | maxtemps[0][3] | maxtemps[0][4] |
| maxtemps[1] | maxtemps[1][0] | maxtemps[1][1] | maxtemps[1][2] | maxtemps[1][3] | maxtemps[1][4] |
| maxtemps[2] | maxtemps[2][0] | maxtemps[2][1] | maxtemps[2][2] | maxtemps[2][3] | maxtemps[2][4] |
| maxtemps[3] | maxtemps[3][0] | maxtemps[3][1] | maxtemps[3][2] | maxtemps[3][3] | maxtemps[3][4] |

*Figure 5.6 — Accessing array elements with subscripts.*

Suppose you want to print all the array contents. In that case, you can use one for loop to change rows and a second, nested, for loop to change columns:

```cpp
for (int row = 0; row < 4; row++)
{
    for (int col = 0; col < 5; ++col)
        cout << maxtemps[row][col] << "\t";
    cout << endl;
}
```

For each value of row, the inner for loop cycles through all the col values. This example prints a tab character (\t in C++ escape character notation) after each value and a newline character after each complete row.

### Initializing a Two-Dimensional Array

When you create a two-dimensional array, you have the option of initializing each element. The technique is based on that for initializing a one-dimensional array. Remember that you do this by providing a comma-separated list of values enclosed in braces:

```cpp
// initializing a one-dimensional array
int btus[5] = { 23, 26, 24, 31, 28};
```

For a two-dimensional array, each element is itself an array, so you can initialize each element by using a form like that in the previous code example. Thus, the initialization consists of a comma-separated series of one-dimensional initializations, all enclosed in a set of braces:

```cpp
int maxtemps[4][5] =   // 2-D array
{
    {96, 100, 87, 101, 105},   // values for maxtemps[0]
    {96, 98, 91, 107, 104},    // values for maxtemps[1]
    {97, 101, 93, 108, 107},   // values for maxtemps[2]
    {98, 103, 95, 109, 108}    // values for maxtemps[3]
};
```

You can visualize maxtemps as four rows of five numbers each. The term {94, 98, 87, 103, 101} initializes the first row, represented by maxtemps[0]. As a matter of style, placing each row of data on its own line, if possible, makes the data easier to read.

### Using a Two-Dimensional Array

Listing 5.20 incorporates an initialized two-dimensional array and a nested loop into a program. This time the program reverses the order of the loops, placing the column loop (city index) on the outside and the row loop (year index) on the inside. Also it uses a
