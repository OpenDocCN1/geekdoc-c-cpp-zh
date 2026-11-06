
### Programming Tip 7.2: Program Clearly, Not Cleverly

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_346_0.png)

Some programmers take great pride in minimizing the number of instructions, even if the resulting code is hard to understand. For example, here is a legal implementation of the sum function:

```
double sum(double* a, int size)
{
    double total = 0;
    while (size-- > 0) // Loop size times
    {
        total = total + *a++; // Add the value to which a points; increment a
    }
    return total;
}
```

This implementation uses two tricks. First, the function parameter variables a and size are variables, and it is legal to modify them. Moreover, the expressions size-- and a++ mean “decrement or increment the variable and return the old value”. In other words, the expression

```
size-- > 0
```

combines two tasks: to decrement size, and to test whether size was positive before the decrement. Similarly, the expression

```
*a++
```

increments the pointer to the next element, and it returns the element to which it pointed before the increment.

Please do not use this programming style. Your job as a programmer is not to dazzle other programmers with your cleverness, but to write code that is easy to understand and maintain.

### Common Error 7.2: Returning a Pointer to a Local Variable

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_346_1.png)

Consider this function that tries to return a pointer to an array containing two elements, the first and the last values of an array:

```
double* firstLast(double a[], int size)
{
    double result[2];
    result[0] = a[0];
    result[1] = a[size - 1];
    return result; // Error!
}
```

The function returns a pointer to the starting element of the result array. However, that array is a local variable of the firstLast function. The local variable no longer exists when the function exits. Its contents will soon be overwritten by other function calls.

You can solve this problem by passing an array to hold the answer:

```
void firstLast(const double a[], int size, double result[])
{
    result[0] = a[0];
    result[1] = a[size - 1];
}
```

Then it is the responsibility of the caller to allocate an array to hold the result.

### Special Topic 7.3: Constant Pointers

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_347_0.png)

The following definition specifies a constant pointer:

```
const double* p = &balance;
```

You cannot modify the value to which p points. That is, the following statement is illegal:

```
*p = 0; // Error
```

Of course, you can read the value:

```
cout << *p; // OK
```

A constant array parameter variable is equivalent to a constant pointer. For example, consider the function

```
double sum(const double values[], int size)
```

Recall from Section 7.2.3 that values is a pointer. The function could have been defined as

```
double sum(const double* values, int size)
```

The function can use the pointer values to read the array elements, but it cannot modify them.

## 7.3 C and C++ Strings

C++ has two mechanisms for manipulating strings. The string class supports character sequences of arbitrary length and provides convenient operations such as concatenation and string comparison. However, C++ also inherits a more primitive level of string handling from the C language, in which strings are represented as arrays of char values. In this section, we will discuss the relationships between these types.

### 7.3.1 The char Type

> A value of type `char` denotes an individual character. Character literals are enclosed in single quotes.

The `char` type denotes an individual character. Character literals are delimited by single quotes; for example,

```
char input = 'y';
```

| W | O | R | D |
|---|---|---|---|

Each character is actually encoded as an integer value. (See Appendix D for the encoding using the ASCII code, which is used on the majority of computers today.)

Note that 'y' is a single character, which is quite different from "y", a string containing the 'y' character.

Table 3 shows typical character literals.

### 7.3.2 C Strings

> A literal string (enclosed in double quotes) is an array of `char` values with a zero terminator.

In the C programming language, strings are always represented as character arrays. C++ programmers often refer to arrays of `char` values as “C strings”.

In particular, a literal string, such as "Harry", is not an object of type `string`. Instead, it is an array of `char` values. As with all arrays, a string literal can be assigned to a pointer variable that points to the initial character in the array:

```
const char* char_pointer = "Harry"; // Points to 'H'
```

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_348_0.png)

The string is declared as *const* because you are not supposed to modify a literal string. (See Special Topic 7.3 on page 320 for more information on constant pointers.)

A C string is terminated by a special character, called a *null terminator*, denoted '\0'. For example, the C string "Harry" contains six characters, namely 'H', 'a', 'r', 'r', 'y' and '\0' (See Figure 6.)

The terminator is a character that is encoded as the number zero—this is different from the character '0', the character denoting the zero digit. (Under the ASCII encoding scheme, the character denoting the zero digit is encoded as the number 48.)

Functions that operate on C strings rely on this terminator. Here is a typical example: the `strlen` function declared in the `<cstring>` header that computes the length of a character array. The function counts the number of characters until it reaches the terminator.

```
int strlen(const char s[])
{
   int i = 0;
   while (s[i] != '\0') { i++; } // Count characters before the null terminator
   return i;
}
```

The call `strlen("Harry")` returns 5.

### 7.3.3 Character Arrays

A literal string such as "Harry" is a constant. You are not allowed to modify its characters. If you want to modify the characters in a string, define a character array instead. For example:

```
char char_array[] = "Harry"; // An array of 6 characters
```

**Table 3 Character Literals**

| Literal | Description |
|---|---|
| 'y' | The character y |
| '0' | The character for the digit 0. In the ASCII code, '0' has the value 48. |
| ' ' | The space character |
| '\n' | The newline character |
| '\t' | The tab character |
| '\0' | The null terminator of a string |
| ❌ "y" | **Error:** Not a char value |

The char_array variable is an array of 6 characters, initialized with 'H', 'a', 'r', 'r', 'y', and a null terminator. The compiler counts the characters in the string that is used for initializing the array, including the null terminator.

You can modify the characters in the array:

```
char_array[0] = 'L';
```

### 7.3.4 Converting Between C and C++ Strings

Many library functions use pointers of type `char*`.

Before the C++ string class became widely available, direct manipulation of character arrays was common, but also quite challenging (see Special Topic 7.4 on page 323). If you use functions that receive or return C strings, you need to know how to convert between C strings and string objects.

For example, the `<cstdlib>` header declares a useful function

```
int atoi(const char s[])
```

The atoi function converts a character array containing digits into its integer value:

```
char year[] = "2012";
int y = atoi(year); // Now y is the integer 2012
```

This functionality is inexplicably missing from the C++ string class. The c_str member function of the string class offers an “escape hatch”. If s is a string, then s.c_str() yields a char* pointer to the characters in the string. Here is how you use that member function to call the atoi function:

You can initialize C++ string variables with C strings.

```
string year = "2012";
int y = atoi(year.c_str());
```

Conversely, converting from a C string to a C++ string is very easy. Simply initialize a string variable with any value of type char*, such as a string literal or character array. For example, the definition

```
string name = "Harry";
```

initializes the C++ string object name with the C string "Harry".

### 7.3.5 C++ Strings and the `[]` Operator

Up to this point, we have always used the `substr` member function to access individual characters in a C++ string. For example, if a string variable is defined as

```
string name = "Harry";
```

The expression

```
name.substr(3, 1)
```

yields a string of length 1 containing the character at index 3.

You can access individual characters in a C++ string object with the `[]` operator:

```
name[0] = 'L';
```

Now the string is "Larry". The `[]` operator is more convenient than the `substr` function if you want to visit a string one character at a time.

Here is a useful example. The following function makes a copy of a string and changes all characters to uppercase:
