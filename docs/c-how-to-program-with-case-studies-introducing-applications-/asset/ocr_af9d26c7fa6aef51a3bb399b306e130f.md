set. For example, 'z' represents the letter z's integer value, and '\n' represents a new-line's integer value.

A string is a series of characters treated as a single unit. A string may include letters, digits and various special characters such as +, -, *, / and $. String literals, or string constants, are written in double quotation marks as follows:

```
~~~
"John Q. Doe"        (a name)
"99999 Main Street"  (a street address)
"Waltham, Massachusetts" (a city and state)
"(201) 555-1212"      (a telephone number)
~~~
```

# ### Strings Are Null Terminated

Every string must end with the null character ('\0'). Printing a “string” that does not contain a terminating null character is a logic error. The results of this are undefined. On some systems, printing will continue past the end of the “string” until a null character is encountered. On others, your program will terminate prematurely (i.e., “crash”) and indicate a “segmentation fault” or “access violation” error.

![](bbox=[0.863, 0.316, 0.898, 0.336])

# ### Strings and Pointers

You access a string via a pointer to its first character. A string's “value” is the address of its first character. Thus, in C, it's appropriate to say that a string is a pointer to the string's first character. This is just like arrays, because strings are simply arrays of characters.

# ### Initializing char Arrays and char \* Pointers

You can initialize a character array or a char \* variable with a string. The definitions

```
~~~c
char color[] = "blue";
const char *colorPtr = "blue";
~~~
```

initialize color and colorPtr to the string "blue". The first definition creates a 5-element array color containing the modifiable characters 'b', 'l', 'u', 'e' and '\0'. The second definition creates the pointer variable colorPtr that points to the letter 'b' in "blue", which is not modifiable.

The color array definition also can be written as

```
~~~c
char color[] = {'b', 'l', 'u', 'e', '\0'};
~~~
```

The preceding definition automatically determines the array's size based on its number of initializers (5). When storing a string in a char array, the array must be large enough to store the string and its terminating null character. Not allocating sufficient space in a character array to store the null character that terminates a string is an error. C allows you to store strings of any length. If a string is longer than the char array in which you store it, characters beyond the array's end may overwrite other data in memory.

![](bbox=[0.863, 0.844, 0.898, 0.864])