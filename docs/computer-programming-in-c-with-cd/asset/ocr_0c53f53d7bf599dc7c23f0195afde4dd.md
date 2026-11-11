An array of characters is called string, which is stored in consecutive bytes of memory and it is terminated by null character. This null character is written as `\0` that denotes end of the string. Let’s consider the following code snippet:

```
char string1[8] = "welcome";
```

In preceding code snippet, a character array (string1) with 8 characters is created. In this character array, the `welcome` string is stored. At the time of compilation, the null character ('\0') is placed automatically by the compiler itself. Figure 1 shows the memory representation of this string (character array) as follows:

![](bbox=[0.227, 0.319, 0.846, 0.354])

▲ Figure 1: Memory Representation of Character String

In Figure 1, you can see that all the characters of the string (welcome) are stored adjacent to each other. Moreover, the null character (\0) is placed just after the last character of the string.

Listing 2 shows how to store and retrieve a string in an array (you can find the Array1.cpp file on the CD in the code/chapter3 folder):

# ▶ Listing 2: Storing and Retrieving a String Value

```
#include <iostream.h>
#include <string.h>
int main()
{
    char string1[15];
    cout<< "Enter your name :";
    cin>> string1;
    cout<< "Your name is :" <<string1;
    return 0;
}
```

**Output:**

```
Enter your name :Kumar
Your name is :Kumar
```

In Listing 2, string1[15] is declared with char type (string), when the user enters string this string get stored in `string1` variable. The value of `string1` is then retrieved by using the `cout` object.

After understanding all about an array, let’s discuss the following types of array:

+   - One-dimensional array
+   - Two-dimensional array