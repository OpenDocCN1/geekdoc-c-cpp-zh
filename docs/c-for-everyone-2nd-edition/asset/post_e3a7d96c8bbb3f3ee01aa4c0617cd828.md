
```cpp
}
}
```

At the end of this loop, `current_size` contains the actual number of elements in the array. Note that you have to stop accepting inputs if the size of the array reaches the capacity.

To process the gathered array elements, you again use the companion variable, not the capacity. This loop prints the partially filled array:

```cpp
for (int i = 0; i < current_size; i++)
{
    cout << values[i] << endl;
}
```

![](img/23fb3582e93ebc95909e1de029c3d388_281_0.png)

## SELF CHECK

- 1. Define an array of integers containing the first five prime numbers.
- 2. Assume the array `primes` has been initialized as described in Self Check 1. What is its contents after executing the following loop?

  ```cpp
  for (int i = 0; i < 2; i++)
  {
      primes[4 - i] = primes[i];
  }
  ```

- 3. Assume the array `primes` has been initialized as described in Self Check 1. What is its contents after executing the following loop?

  ```cpp
  for (int i = 0; i < 5; i++)
  {
      primes[i]++;
  }
  ```

- 4. Given the definition

  ```cpp
  const int CAPACITY = 10;
  double values[CAPACITY];
  ```

  write statements to put a zero into the elements of the array `values` with the lowest and the highest valid index.
- 5. Given the array defined in Self Check 4, write a loop to print the elements of the array `values` in reverse order, starting with the last element.
- 6. Define an array called `words` that can hold ten values of type `string`.
- 7. Define an array containing two strings, "Yes," and "No".

## Practice It

Now you can try these exercises at the end of the chapter: R6.1, R6.2, R6.6, P6.1.

## Common Error 6.1

### Bounds Errors

Perhaps the most common error in using arrays is accessing a nonexistent element.

```cpp
double values[10];
values[10] = 5.4;
// Error—values has 10 elements with subscripts 0 to 9
```

If your program accesses an array through an out-of-bounds subscript, there is no error message. Instead, the program will quietly (or not so quietly) corrupt some memory. Except for very short programs, in which the problem may go unnoticed, that corruption will make the program act unpredictably, and it can even cause the program to terminate. These are serious errors that can be difficult to detect.

![](img/23fb3582e93ebc95909e1de029c3d388_281_1.png)

## Programming Tip 6.1

![](img/23fb3582e93ebc95909e1de029c3d388_282_0.png)

### Use Arrays for Sequences of Related Values

Arrays are intended for storing sequences of values with the same meaning. For example, an array of test scores makes perfect sense:

```cpp
int scores[NUMBER_OF_SCORES];
```

But an array

```cpp
double personal_data[3];
```

that holds a person's age, bank balance, and shoe size in positions 0, 1, and 2 is bad design. It would be tedious for the programmer to remember which of these data values is stored in which array location. In this situation, it is far better to use three separate variables.

## Random Fact 6.1

### An Early Internet Worm

![](img/23fb3582e93ebc95909e1de029c3d388_282_1.png)

In November 1988, Robert Morris, a student at Cornell University, launched a so-called virus program that infected about 6,000 computers connected to the Internet across the United States. Tens of thousands of computer users were unable to read their e-mail or otherwise use their computers. All major universities and many high-tech companies were affected. (The Internet was much smaller then than it is now.)

The particular kind of virus used in this attack is called a worm. The virus program crawled from one computer on the Internet to the next. The worm would attempt to connect to finger, a program in the UNIX operating system for finding information on a user who has an account on a particular computer on the network. Like many programs in UNIX, finger was written in the C language. In C, as in C++, arrays have a fixed size. To store the user name to be looked up (say, walter@cs.sjsu.edu), the finger program allocated an array of 512 characters, under the assumption that nobody would ever provide such a long input. Unfortunately, C, like C++, does not check that an array index is less than the length of the array. If you write into an array using an index that is too large, you simply overwrite memory locations that belong to some other objects. In some versions of the finger program, the programmer had been lazy and had not checked whether the array holding the input characters was large enough to hold the input. So the worm program purposefully filled the 512-character array with 536 bytes. The excess 24 bytes would overwrite a return address, which the attacker knew was stored just after the line buffer. When that function was finished, it didn't return to its caller but to code supplied by the worm (see Figure 4). That code ran under the same super-user privileges as finger, allowing the worm to gain entry into the remote system. Had the programmer who wrote finger been more conscientious, this particular attack would not be possible. In C++, as in C, all programmers must be very careful not to overrun array boundaries.

One may well speculate what would possess the virus author to spend many weeks to plan the antisocial act of breaking into thousands of computers and disabling them. It appears that the break-in was fully intended by the author, but the disabling of the computers was a bug, caused by continuous reinfection. Morris was sentenced to 3 years probation, 400 hours of community service, and fined $10,000.

In recent years, computer attacks have intensified and the motives have become more sinister. Instead of disabling computers, viruses often steal financial data or use the attacked computers for sending spam e-mail. Sadly, many of these attacks continue to be possible because of poorly written programs that are susceptible to buffer overrun errors.

![](img/23fb3582e93ebc95909e1de029c3d388_282_2.png)

## 6.2 Common Array Algorithms

In the following sections, we discuss some of the most common algorithms for processing sequences of values. We present the algorithms so that you can use them with fully and partially filled arrays as well as vectors (which we will introduce in Section 6.7). When we use the expression *size* of values, you should replace it with a constant or variable that yields the number of elements in the array (or the expression `values.size()` if values is a vector).

### 6.2.1 Filling

This loop fills an array with zeroes:

```cpp
for (int i = 0; i < size of values; i++)
{
    values[i] = 0;
}
```

Next, let us fill an array squares with the numbers 0, 1, 4, 9, 16, and so on. Note that the element with index 0 contains 0², the element with index 1 contains 1², and so on.

```cpp
for (int i = 0; i < size of squares; i++)
{
    squares[i] = i * i;
}
```

### 6.2.2 Copying

> To copy an array, use a loop to copy its elements to a new array.

Consider two arrays:

```cpp
int squares[5] = { 0, 1, 4, 9, 16 };
int lucky_numbers[5];
```

Now suppose you want to copy all values from the first array to the second. The following assignment is an error:

```cpp
lucky_numbers = squares; // Error
```

In C++, you cannot assign one array to another. Instead, you must use a loop to copy all elements:

```cpp
for (int i = 0; i < 5; i++)
{
    lucky_numbers[i] = squares[i];
}
```

![](img/23fb3582e93ebc95909e1de029c3d388_283_0.png)

**Figure 5** Copying Elements to Copy an Array

### 6.2.3 Sum and Average Value

You have already encountered this algorithm in Section 4.7.1. Here is the code for computing the sum of all elements in an array:

```cpp
double total = 0;
for (int i = 0; i < size of values; i++)
{
    total = total + values[i];
}
```

To obtain the average, divide by the number of elements:

```cpp
double average = total / size of values;
```

Be sure to check that the size is not zero.

### 6.2.4 Maximum and Minimum

Use the algorithm from Section 4.7.4 that keeps a variable for the largest element that you have encountered so far. Here is the implementation for arrays:

```cpp
double largest = values[0];
for (int i = 1; i < size of values; i++)
{
    if (values[i] > largest)
    {
        largest = values[i];
    }
}
```

![](img/23fb3582e93ebc95909e1de029c3d388_284_0.png)

Note that the loop starts at 1 because we initialize largest with values[0]. To compute the smallest value, reverse the comparison. These algorithms require that the array contain at least one element.

### 6.2.5 Element Separators

> When separating elements, don't place a separator before the first element.

When you display the elements of a collection, you usually want to separate them, often with commas or vertical lines, like this:

1 | 4 | 9 | 16 | 25

Note that there is one fewer separator than there are numbers. Print the separator before each element except the initial one (with index 0):

```cpp
for (int i = 0; i < size of values; i++)
{
    if (i > 0)
    {
        cout << " | ";
    }
    cout << values[i];
}
```

![](img/23fb3582e93ebc95909e1de029c3d388_284_1.png)

To print five elements, you need four separators.
