| Function prototypes and descriptions |
| --- |
| **`char *strstr(const char *s1, const char *s2);`**<br>Locates the first occurrence in string s1 of string s2. If the string is found, a pointer to the string in s1 is returned. Otherwise, a NULL pointer is returned. |
| **`char *strtok(char *s1, const char *s2);`**<br>A sequence of calls to strtok breaks string s1 into tokens—logical pieces such as words in a line of text—separated by characters contained in string s2. The first call contains s1 as the first argument, and subsequent calls to continue tokenizing the same string contain NULL as the first argument. A pointer to the current token is returned by each call. If there are no more tokens when the function is called, NULL is returned. |

**Fig. 8.19** | Search functions of the string-handling library. (Part 2 of 2.)

# ### 8.8.1 Function strchr

Function `strchr` searches for the *first occurrence* of a character in a string. If the character is found, `strchr` returns a pointer to the character in the string; otherwise, `strchr` returns `NULL`. Figure 8.20 searches for the first occurrences of `'a'` and `'z'` in `"This is a test"`.

```
```c
1  // Fig. 8.20: fig08_20.c
2  // Using function strchr
3  #include <stdio.h>
4  #include <string.h>
5
6  int main(void)
7  {
8     const char *string = "This is a test"; // initialize char pointer
9     char character1 = 'a'; // initialize character1
10    char character2 = 'z'; // initialize character2
11
12    // if character1 was found in string
13    if (strchr(string, character1) != NULL) { // can remove "!= NULL"
14       printf(\"%c\" was found in \"%s\"\n",
15          character1, string);
16    }
17    else { // if character1 was not found
18       printf(\"%c\" was not found in \"%s\"\n",
19          character1, string);
20    }
21
22    // if character2 was found in string
23    if (strchr(string, character2) != NULL) { // can remove "!= NULL"
24       printf(\"%c\" was found in \"%s\"\n",
25          character2, string);
26    }
27    else { // if character2 was not found
```
```

**Fig. 8.20** | Using function strchr. (Part 1 of 2.)