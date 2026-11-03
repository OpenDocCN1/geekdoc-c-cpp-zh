# Joining strings

The combining of two strings into one single string is more precisely known as string “concatenation”.

The standard C library **string.h** header file contains two functions that can be used to concatenate strings. To make these available to a program the **string.h** header file must be added with an `#include` directive at the start of the program.

The first string concatenation function is **strcat()**, which requires two arguments to be specified stating the names of the two strings to concatenate. The string named as its second argument is appended after the string named as its first argument, then the function returns the entire concatenated first string. So, the function’s syntax looks like this:

```
strcat( first-string , string-to-add-to-first-string ) ;
```

It is important to note that the first string array must be large enough to accommodate all the characters of the concatenated strings to avoid an error.

The second string-concatenation function is the similarly named **strncat()** function (with an added “n”). This is used like the **strcat()** function but takes a third argument to specify how many characters of the second string should be appended onto the first string. Its syntax therefore looks like this:

```
strncat( first-string , string-to-add-to-first-string , length ) ;
```

The string being appended will begin with the first character of the string specified by the second argument by default, and end at the position specified by the third argument. But as the name of the string is an implied pointer to its first character, pointer arithmetic can be used to indicate a different position at which to begin appending, with this syntax:

```
strncat( first-string , (string-to-add-to-first-string+places) , length );
```

Once again, as with the **strcat()** function, it is important that the first string array must be large enough to accommodate all the characters of the concatenated strings to avoid an error when using the **strncat()** function.