# Chapter 4 Compound Types

# Program Notes

What can you learn from Listing 4.2? First, note that the size operator gives the size of the entire array, 15 bytes, but the strlen() function returns the size of the string stored in the array and not the size of the array itself. Also strlen() counts just the visible characters and not the null character. Thus, it returns a value of 8, not 9, for the length of Basicman. If cosmic is a string, the minimum array size for holding that string is strlen(cosmic) + 1.

Because name1 and name2 are arrays, you can use an index to identify individual characters in the array. For example, the program uses name1[0] to find the first character in that array. Also the program sets name2[3] to the null character. That makes the string end after three characters, even though characters remain in the array (see Figure 4.3).

```
const int ArSize = 15;
char name2[ArSize] = "C++owboy";
```

string

| C | + | o | w | b | o | y | \0 |

name2[3] = '\\0';

string

| C | + | \0 | w | b | o | y | \0 |

ignored

Figure 4.3 Shortening a string with \0.

Note that the program in Listing 4.2 uses a symbolic constant for the array size. Often the size of an array appears in several statements in a program. Using a symbolic constant to represent the size of an array simplifies revising the program to use a different array size; you just have to change the value once, where the symbolic constant is defined.

# Adventures in String Input

The strings.cpp program has a blemish that is concealed through the often useful technique of carefully selected sample input. Listing 4.3 removes the veils and shows that string input can be tricky.