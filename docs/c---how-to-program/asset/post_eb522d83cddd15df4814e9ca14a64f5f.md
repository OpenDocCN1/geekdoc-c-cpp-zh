
### 8.8.4 Function `strrchr`

Function `strrchr` searches for the *last occurrence* of the specified character in a string. If the character is found, `strrchr` returns a pointer to the character in the string; otherwise, `strrchr` returns NULL. Figure 8.23 shows a program that searches for the last occurrence of the character 'z' in the string "A zoo has many animals including zebras".

```c
// Fig. 8.23: fig08_23.c
// Using function strrchr
#include <stdio.h>
#include <string.h>

int main(void)
{
   // initialize char pointer
   const char *string1 = "A zoo has many animals including zebras";

   int c = 'z'; // character to search for

   printf("%s\n%s'%c'%s\"%s\"\n",
      "The remainder of string1 beginning with the",
      "last occurrence of character ", c,
      " is: ", strrchr(string1, c));
}
```

```text
The remainder of string1 beginning with the
last occurrence of character 'z' is: "zebras"
```

**Fig. 8.23** | Using function `strrchr`.

### 8.8.5 Function `strspn`

Function `strspn` (Fig. 8.24) determines the length of the *initial part* of the string in its first argument that contains only characters from the string in its second argument. The function returns the length of the segment.

```c
// Fig. 8.24: fig08_24.c
// Using function strspn
#include <stdio.h>
#include <string.h>

int main(void)
{
   // initialize two char pointers
   const char *string1 = "The value is 3.14159";
   const char *string2 = "aehi lsTuv";

   printf("%s%s\n%s%s\n\n%s\n%s%zu\n",
      "string1 = ", string1, "string2 = ", string2,
      "The length of the initial segment of string1",
      "containing only characters from string2 = ",
      strspn(string1, string2));
}
```

```text
string1 = The value is 3.14159
string2 = aehi lsTuv

The length of the initial segment of string1
containing only characters from string2 = 13
```

**Fig. 8.24** | Using function `strspn`.

### 8.8.6 Function `strstr`

Function `strstr` searches for the *first occurrence* of its second string argument in its first string argument. If the second string is found in the first string, a pointer to the location of the string in the first argument is returned. Figure 8.25 uses `strstr` to find the string "def" in the string "abcdefabcdef".

```c
// Fig. 8.25: fig08_25.c
// Using function strstr
#include <stdio.h>
#include <string.h>

int main(void)
{
   const char *string1 = "abcdefabcdef"; // string to search
   const char *string2 = "def"; // string to search for

   printf("%s%s\n%s%s\n\n%s\n%s%s\n",
      "string1 = ", string1, "string2 = ", string2,
      "The remainder of string1 beginning with the",
      "first occurrence of string2 is: ",
      strstr(string1, string2));
}
```

```text
string1 = abcdefabcdef
string2 = def

The remainder of string1 beginning with the
first occurrence of string2 is: defabcdef
```

**Fig. 8.25** | Using function `strstr`. (Part 1 of 2.)

**Fig. 8.25** | Using function `strstr`. (Part 2 of 2.)

### 8.8.7 Function `strtok`

Function `strtok` (Fig. 8.26) is used to break a string into a series of tokens. A token is a sequence of characters separated by delimiters (usually spaces or punctuation marks, but a delimiter can be any character). For example, in a line of text, each word can be considered a token, and the spaces and punctuation separating the words can be considered delimiters.

```c
// Fig. 8.26: fig08_26.c
// Using function strtok
#include <stdio.h>
#include <string.h>

int main(void)
{
   // initialize array string
   char string[] = "This is a sentence with 7 tokens";

   printf("%s\n%s\n%s\n",
      "The string to be tokenized is:", string,
      "The tokens are:");

   char *tokenPtr = strtok(string, " "); // begin tokenizing sentence

   // continue tokenizing sentence until tokenPtr becomes NULL
   while (tokenPtr != NULL) {
      printf("%s\n", tokenPtr);
      tokenPtr = strtok(NULL, " "); // get next token
   }
}
```

```text
The string to be tokenized is:
This is a sentence with 7 tokens
```

**Fig. 8.26** | Using function `strtok`. (Part 1 of 2.)

![](img/d0d3b7423c2d9e5650be79209ea1885d_391_0.png)

**Fig. 8.26** | Using function `strtok`. (Part 2 of 2.)

Multiple calls to `strtok` are required to *tokenize a string*—i.e., break it into tokens (assuming that the string contains more than one token). The first call to `strtok` (line 15) contains two arguments: a string to be tokenized, and a string containing characters that separate the tokens. In line 15, the statement

```c
char *tokenPtr = strtok(string, " "); // begin tokenizing sentence
```

assigns `tokenPtr` a pointer to the first token in `string`. The second argument, `" "`, indicates that tokens are separated by spaces. Function `strtok` searches for the first character in `string` that’s not a delimiting character (space). This begins the first token. The function then finds the next delimiting character in the string and replaces it with a null (`'\0'`) character to terminate the current token. Function `strtok` saves a pointer to the next character following the token in `string` and returns a pointer to the current token.

Subsequent `strtok` calls in line 20 continue tokenizing `string`. These calls *contain NULL as their first argument*. The NULL argument indicates that the call to `strtok` should continue tokenizing from the location in `string` saved by the last call to `strtok`. If no tokens remain when `strtok` is called, `strtok` returns NULL. You can change the delimiter string in each new call to `strtok`. Figure 8.26 uses `strtok` to tokenize the string "This is a sentence with 7 tokens." Each token is printed separately. Function `strtok` *modifies the input string* by placing `'\0'` at the end of each token; therefore, a copy of the string should be made if the string will be used after the calls to `strtok`. [*Note:* Also see CERT recommendation STR06-C, which discusses the problems with assuming that `strtok` does not modify the string in its first argument.]

## 8.9 Memory Functions of the String-Handling Library

The string-handling library functions presented in this section manipulate, compare and search blocks of memory. The functions treat blocks of memory as character arrays and can manipulate any block of data. Figure 8.27 summarizes the memory functions of the string-handling library. In the function discussions, “object” refers to a block of data. [*Note:* Each of these functions has a more secure version described in optional Annex K of the C11 standard. We mention these in the Secure C Programming section of this chapter.]

The pointer parameters are declared `void *` so they can be used to manipulate memory for any data type. Recall from Chapter 7 that any pointer can be assigned directly to a pointer of type `void *`, and a pointer of type `void *` can be assigned directly to a pointer of any other type. Because a `void *` pointer cannot be dereferenced, each function receives a size argument that specifies the number of bytes the function will process. For

| Function prototype | Function description |
|---|---|
| `void *memcpy(void *s1, const void *s2, size_t n);` | Copies n bytes from the object pointed to by s2 into the object pointed to by s1. A pointer to the resulting object is returned. |
| `void *memmove(void *s1, const void *s2, size_t n);` | Copies n bytes from the object pointed to by s2 into the object pointed to by s1. The copy is performed as if the bytes were first copied from the object pointed to by s2 into a temporary array and then from the temporary array into the object pointed to by s1. A pointer to the resulting object is returned. |
| `int memcmp(const void *s1, const void *s2, size_t n);` | Compares the first n bytes of the objects pointed to by s1 and s2. The function returns 0, less than 0 or greater than 0 if s1 is equal to, less than or greater than s2. |
| `void *memchr(const void *s, int c, size_t n);` | Locates the first occurrence of c (converted to unsigned char) in the first n bytes of the object pointed to by s. If c is found, a pointer to c in the object is returned. Otherwise, NULL is returned. |
| `void *memset(void *s, int c, size_t n);` | Copies c (converted to unsigned char) into the first n bytes of the object pointed to by s. A pointer to the result is returned. |

**Fig. 8.27** | Memory functions of the string-handling library.

For simplicity, the examples in this section manipulate character arrays (blocks of characters). The functions in Fig. 8.27 do not check for terminating null characters, because they manipulate blocks of memory that are not necessarily strings.

### 8.9.1 Function `memcpy`

Function `memcpy` copies a specified number of bytes from the object pointed to by its second argument into the object pointed to by its first argument. The function can receive a pointer to any type of object. The result of this function is undefined if the two objects overlap in memory (i.e., if they are parts of the same object)—in such cases, use `memmove`. Figure 8.28 uses `memcpy` to copy the string in array s2 to array s1.

### Performance Tip 8.1

`memcpy` is more efficient than `strcpy` when you know the size of the string you are copying.

```c
// Fig. 8.28: fig08_28.c
// Using function memcpy
#include <stdio.h>
#include <string.h>
```

**Fig. 8.28** | Using function `memcpy`. (Part 1 of 2.)
