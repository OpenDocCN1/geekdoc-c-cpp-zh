
they can be concatenated in a `cout` statement. This makes the `setw()` manipulator particularly convenient when you’re displaying several columns of values. Listing 17.10 illustrates this by changing the field width and fill character several times for one output line. It also uses some of the newer standard manipulators.

> **Note**
>
> Some C++ systems don’t automatically search the math library. As mentioned before, some Unix systems require that you use the following to access the math library:
>
> ```sh
> $ cc iomanip.cpp -lm
> ```

**Listing 17.10 `iomanip.cpp`**

```cpp
// iomanip.cpp -- using manipulators from iomanip
// some systems require explicitly linking the math library
#include <iostream>
#include <iomanip>
#include <cmath>

int main()
{
    using namespace std;
    // use new standard manipulators
    cout << fixed << right;

    // use iomanip manipulators
    cout << setw(6) << "N" << setw(14) << "square root"
         << setw(15) << "fourth root\n";

    double root;
    for (int n = 10; n <= 100; n += 10)
    {
        root = sqrt(double(n));
        cout << setw(6) << setfill('.') << n << setfill(' ')
             << setw(12) << setprecision(3) << root
             << setw(14) << setprecision(4) << sqrt(root)
             << endl;
    }

    return 0;
}
```

Here is the output of the program in Listing 17.10:

```text
     N    square root    fourth root
....10       3.162         1.7783
....20       4.472         2.1147
....30       5.477       2.3403
....40       6.325       2.5149
....50       7.071       2.6591
....60       7.746       2.7832
....70       8.367       2.8925
....80       8.944       2.9907
....90       9.487       3.0801 ...
...100      10.000       3.1623
```

Now you can produce neatly aligned columns. Using the fixed manipulator causes trailing zeros to be displayed.

## Input with `cin`

Now it’s time to turn to input and getting data into a program. The `cin` object represents the standard input as a stream of bytes. Normally, you generate that stream of characters at the keyboard. If you type the character sequence 2011, the `cin` object extracts those characters from the input stream. You may intend that input to be part of a string, to be an `int` value, to be a `float` value, or to be some other type. Thus, extraction also involves type conversion. The `cin` object, guided by the type of variable designated to receive the value, must use its methods to convert that character sequence into the intended type of value.

Typically, you use `cin` as follows:

```cpp
cin >> value_holder;
```

Here `value_holder` identifies the memory location in which to store the input. It can be the name of a variable, a reference, a dereferenced pointer, or a member of a structure or of a class. How `cin` interprets the input depends on the data type for `value_holder`. The `istream` class, defined in the iostream header file, overloads the `>>` extraction operator to recognize the following basic types:

- `signed char &`
- `unsigned char &`
- `char &`
- `short &`
- `unsigned short &`
- `int &`
- `unsigned int &`
- `long &`
- `unsigned long &`
- `long long &` (C++11)
- `unsigned long long &` (C++11)
- `float &`
- `double &`
- `long double &`

These are referred to as *formatted input functions* because they convert the input data to the format indicated by the target.

A typical operator function has a prototype like the following:

```cpp
istream & operator>>(int &);
```

Both the argument and the return value are references. With a reference argument (see Chapter 8, “Adventures in Functions”), a statement such as the following causes the `operator>>()` function to work with the variable `staff_size` itself rather than with a copy, as would be the case with a regular argument:

```cpp
cin >> staff_size;
```

Because the argument type is a reference, `cin` is able to directly modify the value of a variable used as an argument. The preceding statement, for example, directly modifies the value of the `staff_size` variable. We’ll get to the significance of a reference return value in a moment. First, let’s examine the type conversion aspect of the extraction operator. For arguments of each type in the preceding list of types, the extraction operator converts the character input to the indicated type of value. For example, suppose `staff_size` is type `int`. In this case, the compiler matches

```cpp
cin >> staff_size;
```

to the following prototype:

```cpp
istream & operator>>(int &);
```

The function corresponding to that prototype then reads the stream of characters being sent to the program—say, the characters 2, 3, 1, 8, and 4. For a system using a 2-byte `int`, the function then converts these characters to the 2-byte binary representation of the integer 23184. If, on the other hand, `staff_size` were type `double`, `cin` would use `operator>>(double &)` to convert the same input into the 8-byte floating-point representation of the value 23184.0.

Incidentally, you can use the `hex`, `oct`, and `dec` manipulators with `cin` to specify that integer input is to be interpreted as hexadecimal, octal, or decimal format. For example, the following statement causes an input of 12 or 0x12 to be read as hexadecimal 12, or decimal 18, and it causes ff or FF to be read as decimal 255:

```cpp
cin >> hex;
```

The `istream` class also overloads the `>>` extraction operator for character pointer types:

- `signed char *`
- `char *`
- `unsigned char *`

For this type of argument, the extraction operator reads the next word from input and places it at the indicated address, adding a null character to make a string. For example, suppose you have this code:

```cpp
cout << "Enter your first name:\n";
char name[20];
cin >> name;
```

If you respond to the request by typing `Liz`, the extraction operator places the characters `Liz\0` in the `name` array. (As usual, `\0` represents the terminating null character.) The `name` identifier, being the name of a `char` array, acts as the address of the array’s first element, making `name` type `char *` (pointer-to-char).

The fact that each extraction operator returns a reference to the invoking object lets you concatenate input, just as you can concatenate output:

```cpp
char name[20];
float fee;
int group;
cin >> name >> fee >> group;
```

Here, for example, the `cin` object returned by `cin >> name` becomes the object that handles `fee`.

### How `cin >>` Views Input

The various versions of the extraction operator share a common way of looking at the input stream. They skip over white space (blanks, newlines, and tabs) until they encounter a non-white-space character. This is true even for the single-character modes (those in which the argument is type `char`, `unsigned char`, or `signed char`), which is not true of C’s character input functions (see Figure 17.5). In the single-character modes, the `>>` operator reads that character and assigns it to the indicated location. In the other modes, the operator reads in one unit of the indicated type. That is, it reads everything from the initial non-white-space character up to the first character that doesn’t match the destination type.

For example, consider the following code:

```cpp
int elevation;
cin >> elevation;
```

Suppose you type the following characters:

```text
-123Z
```

The operator will read the `-`, `1`, `2`, and `3` characters because they are all valid parts of an integer. But the `Z` character isn’t valid, so the last character accepted for input is the `3`. The `Z` remains in the input stream, and the next `cin` statement will start reading at that point. Meanwhile, the operator converts the character sequence `-123` to an integer value and assigns it to `elevation`.

```cpp
char philosophy[20];
int distance;
char initial;

cin >> philosophy >> distance >> initial;
```

![](img/9afc44517b591d64e2e19f623c9308ef_1110_0.png)

Figure 17.5 `cin >>` skips over white space.

It can happen that input fails to meet a program's expectation. For example, suppose you enter `Zcar` instead of `-123Z`. In that case, the extraction operator leaves the value of `elevation` unchanged and returns the value 0. (More technically, an `if` or `while` statement evaluates an `istream` object as false if it's had an error state set; we'll discuss this in more depth later in this chapter.) The false return value allows a program to check whether input meets the program requirements, as Listing 17.11 shows.

**Listing 17.11 `check_it.cpp`**

```cpp
// check_it.cpp -- checking for valid input
#include <iostream>

int main()
{
    using namespace std;
    cout << "Enter numbers: ";

    int sum = 0;
    int input;
    while (cin >> input)
    {
        sum += input;
    }

    cout << "Last value entered = " << input << endl;
    cout << "Sum = " << sum << endl;
    return 0;
}
```
