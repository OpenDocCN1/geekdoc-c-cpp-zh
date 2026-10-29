
15 (Program) a. Write, compile, and run a C++ program that inputs 10 double-precision numbers in an array named `raw`. After these numbers are entered in the array, your program should cycle through `raw` 10 times. During each pass through the array, your program should select the lowest value in `raw` and place it in the next available slot in an array named `sorted`. When your program is finished, the `sorted` array should contain the numbers in `raw` in sorted order from lowest to highest. (Hint: Be sure to reset the lowest value selected during each pass to a very high number so that it's not selected again. You need a second `for` loop in the first `for` loop to locate the minimum value for each pass.)

b. The method used in Exercise 15a to sort the values in the array is inefficient. Can you determine why? What might be a better method of sorting the numbers in an array?

## 7.2 Array Initialization

Array elements can be initialized in their declaration statements in the same manner as scalar variables, except the initializing elements must be included in braces, as shown in these examples:

```
int grade[5] = {98, 87, 92, 79, 85};
char code[6] = {'s', 'a', 'm', 'p', 'l', 'e'};
double width[7] = {10.96, 6.43, 2.58, 0.86, 5.89, 7.56, 8.22};
```

Initializers are applied in the order they're written, with the first value used to initialize element 0, the second value used to initialize element 1, and so on, until all values have been used. For example, in the declaration

```
const NUMELS = 5;
int grade[NUMELS] = {98, 87, 92, 79, 85};
```

`grade[0]` is initialized to 98, `grade[1]` is initialized to 87, `grade[2]` is initialized to 92, `grade[3]` is initialized to 79, and `grade[4]` is initialized to 85.

Because white space is ignored in C++, initializations can be continued across multiple lines. For example, the following declaration for `gallons[]` uses four lines to initialize all the array elements:

```
const int NUMGALS = 20;
int gallons[NUMGALS] = {19, 16, 14, 19, 20, 18,  // initializing values
12, 10, 22, 15, 18, 17,  // can extend across
16, 14, 23, 19, 15, 18,  // multiple lines
21, 5};
```

If the number of initializers is less than the declared number of elements listed in square brackets, the initializers are applied starting with array element 0. Therefore, in the declaration

```
const int ARRAYSIZE = 7;
double length[ARRAYSIZE] = {7.8, 6.4, 4.9, 11.2};
```

only `length[0]`, `length[1]`, `length[2]`, and `length[3]` are initialized with the listed values. The other array elements are initialized to 0.

Unfortunately, there's no method of indicating repetition of an initialization value or of initializing later array elements without first specifying values for earlier elements.

A unique feature of initializers is that the array size can be omitted when initializing values are included in the declaration statement. For example, the following declaration reserves enough storage room for five elements:

```
int gallons[] = {16, 12, 10, 14, 11};
```

Similarly, the following declarations are equivalent:

```
const int NUMCODES = 6;
char codes[6] = {'s', 'a', 'm', 'p', 'l', 'e'};
```

and

```
char codes[] = {'s', 'a', 'm', 'p', 'l', 'e'};
```

Both these declarations set aside six character locations for an array named `codes`. An interesting and useful simplification can also be used when initializing character arrays. For example, the following declaration uses the string "sample" to initialize the `codes` array:

```
char codes[] = "sample";  // no braces or commas
```

Recall that a string is any sequence of characters enclosed in double quotation marks. The preceding declaration creates an array named `codes` with seven elements and fills the array with the seven characters shown in Figure 7.4. The first six characters, as expected, consist of the letters s, a, m, p, l, and e. The last character, the escape sequence `\0`, is called the null character. The null character is appended automatically to all strings used to initialize a character array. This character has an internal storage code numerically equal to zero. (The storage code for the 0 character has a numerical value of decimal 48, so the computer can't confuse the two.) The null character is used as a sentinel to mark the end of a string. Strings stored in this manner, as an array of characters terminated with the null character, are known as C-strings. All the strings you've encountered so far have been C-strings. In Section 14.1, you see that C++ has another method of storing strings with the `string` data type.

![](img/202cface8244f523c2641baa2e00d7dd_323_0.png)

After values have been assigned to array elements, through initialization in the declaration statement or with interactive input, array elements can be processed as described in the previous section. For example, Program 7.3 shows the initialization of array elements in the array declaration statement, and then uses a `for` loop to locate the maximum value stored in the array.

## Program 7.3

```
#include <iostream>
using namespace std;

int main()
{
    const int MAXELS = 5;

    int i, max, nums[MAXELS] = {2, 18, 1, 27, 16};

    max = nums[0];

    for (i = 1; i < MAXELS; i++)
        if (max < nums[i])
            max = nums[i];

    cout << "The maximum value is " << max << endl;
    return 0;
}
```

The following output is produced by Program 7.3:

```
The maximum value is 27
```

## EXERCISES 7.2

1. (Practice) Write array declarations, including initializers, for the following:
   a. A list of 10 integer grades: 89, 75, 82, 93, 78, 95, 81, 88, 77, and 82
   b. A list of five double-precision amounts: 10.62, 13.98, 18.45, 12.68, and 14.76
   c. A list of 100 double-precision interest rates, with the first six rates being 6.29, 6.95, 7.25, 7.35, 7.40, and 7.42
   d. A list of 64 double-precision temperatures, with the first 10 temperatures being 78.2, 69.6, 68.5, 83.9, 55.4, 67.0, 49.8, 58.3, 62.5, and 71.6
   e. A list of 15 character codes, with the first seven codes being f, j, m, q, t, w, and z

2. (Practice) Write an array declaration statement that stores the following values in an array named `prices`: 16.24, 18.98, 23.75, 16.29, 19.54, 14.22, 11.13, and 15.39. Include these statements in a program that displays the values in the array.

## Arrays

3. (Program) Write, compile, and run a C++ program that uses an array declaration statement to initialize the following numbers in an array named `slopes`: 17.24, 25.63, 5.94, 33.92, 3.71, 32.84, 35.93, 18.24, and 6.92. Your program should locate and display the maximum and minimum values in the array.

4. (Program) Write, compile, and run a C++ program that stores the following numbers in an array named `prices`: 9.92, 6.32, 12.63, 5.95, and 10.29. Your program should also create two arrays named `units` and `amounts`, each capable of storing five double-precision numbers. Using a `for` loop and a `cin` statement, have your program accept five user-input numbers in the `units` array when the program is run. Your program should store the product of the corresponding values in the `prices` and `units` array in the `amounts` array. For example, use `amounts[1] = prices[1] * units[1]`. Your program should then display the following output (fill in the chart):

| Price | Units | Amount |
|---|---|---|
| 9.92 |  |  |
| 6.32 |  |  |
| 12.63 |  |  |
| 5.95 |  |  |
| 10.29 |  |  |
| Total: |  |  |

5. (Program) Define an array with a maximum of 20 integer values and fill the array with numbers of your own choosing as initializers. Then write, compile, and run a C++ program that reads the numbers in the array and places all zero and positive numbers in an array named `positive` and all negative numbers in an array named `negative`. Finally, have your program display the values in both the `positive` and `negative` arrays.

6. (Practice) The string of characters `Good Morning` is to be stored in a character array named `goodstr1`. Write the declaration for this array in three different ways.

7. (Practice)
   a. Write declaration statements to store the string of characters `Input the Following Data` in a character array named `message1`, the string `------------` in an array named `message2`, the string `Enter the Date:` in an array named `message3`, and the string `Enter the Account Number:` in an array named `message4`.
   b. Include the array declarations written in Exercise 7a in a program that uses a `cout` statement to display the messages. For example, the statement `cout << message1;` causes the string stored in the `message1` array to be displayed. Your program requires four of these statements to display the four messages. Using a `cout` statement to display a string requires placing the end-of-string marker `\0` in the character array used to store the string.
