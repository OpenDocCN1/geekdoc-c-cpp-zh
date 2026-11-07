
One important difference between a C-style string and a regular array is that the string has a built-in terminating character. (Recall that a char array containing characters but no null character is just an array and not a string.) That means you don’t have to pass the size of the string as an argument. Instead, the function can use a loop to examine each character in the string in turn until the loop reaches the terminating null character. Listing 7.9 illustrates that approach with a function that counts the number of times a given character appears in a string. Because the program doesn’t need to deal with negative values, it uses `unsigned int` as the type for counting.

### Listing 7.9 `strgfun.cpp`

```cpp
// strgfun.cpp -- functions with a string argument
#include <iostream>
unsigned int c_in_str(const char * str, char ch);
int main()
{
    using namespace std;
    char mmm[15] = "minimum";    // string in an array
    // some systems require preceding char with static to
    // enable array initialization

    char *wail = "ululate";     // wail points to string

    unsigned int ms = c_in_str(mmm, 'm');
    unsigned int us = c_in_str(wail, 'u');
    cout << ms << " m characters in " << mmm << endl;
    cout << us << " u characters in " << wail << endl;
    return 0;
}

// this function counts the number of ch characters
// in the string str
unsigned int c_in_str(const char * str, char ch)
{
    unsigned int count = 0;

    while (*str)        // quit when *str is '\0'
    {
        if (*str == ch)
            count++;
        str++;           // move pointer to next char
    }
    return count;
}
```

Here’s the output of the program in Listing 7.9:

```text
3 m characters in minimum
2 u characters in ululate
```

### Program Notes

Because the `c_in_str()` function in Listing 7.9 shouldn’t alter the original string, it uses the `const` modifier when it declares the formal parameter `str`. Then if you mistakenly let the function alter part of the string, the compiler catches your error. Of course, you can use array notation instead to declare `str` in the function header:

```cpp
unsigned int c_in_str(const char str[], char ch)  // also okay
```

However, using pointer notation reminds you that the argument doesn’t have to be the name of an array but can be some other form of pointer.

The function itself demonstrates a standard way to process the characters in a string:

```cpp
while (*str)
{
    statements
    str++;
}
```

Initially, `str` points to the first character in the string, so `*str` represents the first character itself. For example, immediately after the first function call, `*str` has the value `m`, the first character in `minimum`. As long as the character is not the null character (`\0`), `*str` is nonzero, so the loop continues. At the end of each loop, the expression `str++` increments the pointer by 1 byte so that it points to the next character in the string. Eventually, `str` points to the terminating null character, making `*str` equal to 0, which is the numeric code for the null character. That condition terminates the loop. (Why are string-processing functions ruthless? Because they stop at nothing.)

## Functions That Return C-Style Strings

Now suppose you want to write a function that returns a string. Well, a function can’t do that. But it can return the address of a string, and that’s more efficient. Listing 7.10, for example, defines a function called `buildstr()` that returns a pointer. This function takes two arguments: a character and a number. Using `new`, the function creates a string whose length equals the number, and then it initializes each element to the character. Then it returns a pointer to the new string.

### Listing 7.10 `strgback.cpp`

```cpp
// strgback.cpp -- a function that returns a pointer to char
#include <iostream>
char * buildstr(char c, int n);    // prototype
int main()
{
    using namespace std;
    int times;
    char ch;

    cout << "Enter a character: ";
    cin >> ch;
    cout << "Enter an integer: ";
    cin >> times;
    char * ps = buildstr(ch, times);
    cout << ps << endl;
    delete [] ps;                 // free memory
    ps = buildstr('+', 20);       // reuse pointer
    cout << ps << "-DONE-" << ps << endl;
    delete [] ps;                 // free memory
    return 0;
}

// builds string made of n c characters
char * buildstr(char c, int n)
{
    char * pstr = new char[n + 1];
    pstr[n] = '\0';           // terminate string
    while (n-- > 0)
        pstr[n] = c;          // fill rest of string
    return pstr;
}
```

Here’s a sample run of the program in Listing 7.10:

```text
Enter a character: V
Enter an integer: 46
VVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVV
++++++++++++++++++++-DONE-++++++++++++++++++++
```

### Program Notes

To create a string of n visible characters, you need to store n + 1 characters in order to have space for the null character. So the function in Listing 7.10 asks for n + 1 bytes to hold the string. Next, it sets the final byte to the null character. Then it fills in the rest of the array from back to front. In Listing 7.10, the following loop cycles n times as n decreases to 0, filling n elements:

```cpp
while (n-- > 0)
    pstr[n] = c;
```

At the start of the final cycle, n has the value 1. Because `n--` means use the value and then decrement it, the `while` loop test condition compares 1 to 0, finds the test to be true, and continues. But after making the test, the function decrements n to 0, so `pstr[0]` is the last element set to c. The reason for filling the string from back to front instead of front to back is to avoid using an additional variable. Using the other order would involve something like this:

```cpp
int i = 0;
while (i < n)
    pstr[i++] = c;
```

Note that the variable `pstr` is local to the `buildstr` function, so when that function terminates, the memory used for `pstr` (but not for the string) is freed. But because the function returns the value of `pstr`, the program is able to access the new string through the `ps` pointer in `main()`.

The program in Listing 7.10 uses `delete` to free memory used for the string after the string is no longer needed. Then it reuses `ps` to point to the new block of memory obtained for the next string and frees that memory. The disadvantage to this kind of design (having a function return a pointer to memory allocated by `new`) is that it makes it the programmer’s responsibility to remember to use `delete`. In Chapter 12, “Classes and Dynamic Memory Allocation,” you’ll see how C++ classes, by using constructors and destructors, can take care of these details for you.

## Functions and Structures

Let’s move from arrays to structures. It’s easier to write functions for structures than for arrays. Although structure variables resemble arrays in that both can hold several data items, structure variables behave like basic, single-valued variables when it comes to functions. That is, unlike an array, a structure ties its data in to a single entity, or data object, that will be treated as a unit. Recall that you can assign one structure to another. Similarly, you can pass structures by value, just as you do with ordinary variables. In that case, the function works with a copy of the original structure. Also a function can return a structure. There’s no funny business like the name of an array being the address of its first element. The name of a structure is simply the name of the structure, and if you want its address, you have to use the `&` address operator. (C++ and C both use the `&` symbol to denote the address operator. C++ additionally uses this operator to identify reference variables, to be discussed in Chapter 8.)

The most direct way to program by using structures is to treat them as you would treat the basic types—that is, pass them as arguments and use them, if necessary, as return values. However, there is one disadvantage to passing structures by value. If the structure is large, the space and effort involved in making a copy of a structure can increase memory requirements and slow down the system. For those reasons (and because, at first, C didn’t allow the passing of structures by value), many C programmers prefer passing the address of a structure and then using a pointer to access the structure contents. C++ provides a third alternative, called passing by reference, that is discussed in Chapter 8. Let’s examine the other two choices now, beginning with passing and returning entire structures.
