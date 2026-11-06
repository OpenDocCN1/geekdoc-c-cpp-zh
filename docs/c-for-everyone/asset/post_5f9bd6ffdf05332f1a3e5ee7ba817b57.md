
## Syntax 6.1 Defining an Array

![](img/5e58fb4c840712efd6ed6fa82bb97f57_278_0.png)

![](img/5e58fb4c840712efd6ed6fa82bb97f57_278_1.png)

Here we define an array that can hold ten values:

```cpp
double values[10];
```

This is the definition of a variable `values` whose type is “array of double”. That is, `values` stores a sequence of floating-point numbers. The `[10]` indicates the size of the array. (See Figure 1.) The array size must be a constant that is known at compile time.

When we define an array, you can specify the initial values. For example,

```cpp
double values[] = { 32, 54, 67.5, 29, 34.5, 80, 115, 44.5, 100, 65 };
```

When you supply initial values, you don’t need to specify the array size. The compiler determines the size by counting the values.

| Table 1 · Defining Arrays | |
|---|---|
| `int numbers[10];` | An array of ten integers. |
| `const int SIZE = 10;`<br>`int numbers[SIZE];` | It is a good idea to use a named constant for the size.<br><br>⚠️ **Caution:** In standard C++, the size must be a constant. This array definition will not work with all compilers. |
| `int squares[5] = { 0, 1, 4, 9, 16 };` | An array of five integers, with initial values. |
| `int squares[] = { 0, 1, 4, 9, 16 };` | You can omit the array size if you supply initial values. The size is set to the number of initial values. |
| `int squares[5] = { 0, 1, 4 };` | If you supply fewer initial values than the size, the remaining values are set to 0. This array contains 0, 1, 4, 0, 0. |
| `string names[3];` | An array of three strings. |

A bounds error, which occurs if you supply an invalid array index, can corrupt data or cause your program to terminate.

The most common bounds error is the following:

```cpp
double values[10];
cout << values[10];
```

There is no `values[10]` in an array with ten elements—the legal index values range from 0 to 9.

To visit all elements of an array, use a variable for the index. Suppose `values` has ten elements and the integer variable `i` takes values 0, 1, 2, and so on, up to 9. Then the expression `values[i]` yields each element in turn. For example, this loop displays all elements.

```cpp
for (int i = 0; i < 10; i++)
{
    cout << values[i] << endl;
}
```

Note that in the loop condition the index is *less than* 10 because there is no element corresponding to `values[10]`.

### 6.1.3 Partially Filled Arrays

An array cannot change size at run time. This is a problem when you don't know in advance how many elements you need. In that situation, you must come up with a good guess on the maximum number of elements that you need to store. We call this quantity the *capacity*. For example, we may decide that we sometimes want to store more than ten values, but never more than 100:

```cpp
const int CAPACITY = 100;
double values[CAPACITY];
```

In a typical program run, only part of the array will be occupied by actual elements. We call such an array a *partially filled array*. You must keep a companion variable that counts how many elements are actually used. In Figure 3 we call the companion variable `current_size`.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_280_0.png)

*With a partially filled array, you need to remember how many elements are filled.*

![](img/5e58fb4c840712efd6ed6fa82bb97f57_280_1.png)

**Figure 3** A Partially Filled Array

With a partially filled array, keep a companion variable for the current size.

The following loop collects values and fills up the `values` array.

```cpp
int current_size = 0;
double input;
while (cin >> input)
{
    if (current_size < CAPACITY)
    {
        values[current_size] = input;
        current_size++;
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

![](img/5e58fb4c840712efd6ed6fa82bb97f57_281_0.png)

### Self Check

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
- 6. Define an array called `names` that can hold ten values of type `string`.
- 7. Define an array containing two strings, `"Yes"` and `"No"`.

**Practice It** Now you can try these exercises at the end of the chapter: R6.1, R6.2, R6.6, P6.1.

### Common Error 6.1 — Bounds Errors

Perhaps the most common error in using arrays is accessing a nonexistent element.

```cpp
double values[10];
values[10] = 5.4;
    // Error—values has 10 elements with subscripts 0 to 9
```

If your program accesses an array through an out-of-bounds subscript, there is no error message. Instead, the program will quietly (or not so quietly) corrupt some memory. Except for very short programs, in which the problem may go unnoticed, that corruption will make the program act unpredictably, and it can even cause the program to terminate. These are serious errors that can be difficult to detect.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_281_1.png)

### Programming Tip 6.1 — Use Arrays for Sequences of Related Values

![](img/5e58fb4c840712efd6ed6fa82bb97f57_282_0.png)

Arrays are intended for storing sequences of values with the same meaning. For example, an array of test scores makes perfect sense:

```cpp
int scores[NUMBER_OF_SCORES];
```

But an array

```cpp
double personal_data[3];
```

that holds a person's age, bank balance, and shoe size in positions 0, 1, and 2 is bad design. It would be tedious for the programmer to remember which of these values is stored in which array location. In this situation, it is far better to use three separate variables.

### Random Fact 6.1 — An Early Internet Worm

In November 1988, a virus program crawled from one computer on the Internet to the next. The particular kind of virus used in this attack is called a worm. The worm would attempt to connect to `finger`, a program in the UNIX operating system for finding information on a user who has an account on a particular computer on the network. Like many programs in UNIX, `finger` was written in the C language. In C, as in C++, arrays have a fixed size. To store the user name to be looked up (say, walters@cs.sjsu.edu), the `finger` program allocated an array of 512 characters, under the assumption that nobody would ever provide such a long input. Unfortunately, C, like C++, does not check that an array index is less than the length of the array. If you write into an array and an index that is too large, you simply overwrite memory locations that belong to some other objects. In some versions of the `finger` program, the programmer had not checked whether the array holding the input characters was large enough to hold the input. So the worm program purposefully filled the 512-character array with 536 bytes. The excess 24 bytes would overwrite a return address, which the attacker knew was stored just after the line buffer. When that function was finished, it didn't return to its caller but to code supplied by the worm (see Figure 4). That code ran under the same super-user privileges as `finger`, allowing the worm to gain entry into the remote system. Had the programmer who wrote `finger` been more conscientious, this particular attack would not be possible. In C++, as in C, all programmers must be very careful not to overrun array boundaries.

One may well speculate what would possess the virus author to spend many weeks to plan the antisocial act of breaking into thousands of computers and disabling them. It appears that the break-in was fully intended by the author, but the disabling of the computers was a bug, caused by continuous reinfection. Morris was sentenced to 3 years probation, 400 hours of community service, and fined $10,000.

In recent years, computer attacks have intensified and the motives have become more sinister. Instead of disabling computers, viruses often steal financial data or use the attacked computers for sending spam e-mail. Sadly, many of these attacks continue to be possible because of poorly written programs that are susceptible to buffer overrun errors.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_282_1.png)
