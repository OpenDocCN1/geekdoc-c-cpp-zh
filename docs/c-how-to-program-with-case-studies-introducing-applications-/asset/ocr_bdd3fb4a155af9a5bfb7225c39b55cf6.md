```
    30
    31 // copy s2 to s1 using pointer notation
    32 void copy2(char *s1, const char *s2) {
    33     // loop through strings
    34     for (; (*s1 = *s2) != '\0'; ++s1, ++s2) {
    35         ; // do nothing in body
    36     }
    37 }
```

```
    string1 = Hello
    string3 = Good Bye
```

**Fig. 7.15** | Copying a string using array notation and pointer notation. (Part 2 of 2.)

# ### Copying with Array Subscript Notation

Function copy1 uses *array subscript notation* to copy the string in s2 to the character array s1. The function defines counter variable i as the array subscript. The for statement header (line 26) performs the entire copy operation. The statement’s body is the empty statement. The header specifies that i is initialized to zero and incremented by one during each iteration. The expression `s1[i] = s2[i]` copies one character from s2 to s1. When the null character is encountered in s2, it’s assigned to s1. Since the assignment’s value is what gets assigned to the left operand (s1), the loop terminates when an element of s1 receives the null character, which has the value 0 and therefore is false.

# ### Copying with Pointers and Pointer Arithmetic

Function copy2 uses *pointers and pointer arithmetic* to copy the string in s2 to the character array s1. Again, the for statement header (line 34) performs the copy operation. The header does not include any variable initialization. The expression `*s1 = *s2` performs the copy operation by dereferencing s2 and assigning that character to the current location in s1. After the assignment, line 34 increments s1 and s2 to point to each string’s next character. When the assignment copies the null character into s1, the loop terminates.

# ### Notes Regarding Functions copy1 and copy2

*The first argument to both copy1 and copy2 must be an array large enough to hold the second argument’s string.* Otherwise, a logic error may occur when an attempt is made to write into a memory location that’s not part of the array. In both functions, the second argument is copied into the first argument—characters are read from it one at a time, but the characters are never modified. Therefore, the second parameter is declared to point to a constant value so that the *principle of least privilege* is enforced. Neither function requires the capability of modifying the string in the second argument, so we simply disallow it.