+   - Function **strncmp** (p. 383) is equivalent to **strcmp**, except that **strncmp** compares a specified number of characters. If one of the strings is shorter than the number of characters specified, **strncmp** compares characters until the null character in the shorter string is encountered.

# ### Section 8.8 Search Functions of the String-Handling Library

+   - Function **strchr** (p. 386) searches for the first occurrence of a character in a string. If the character is found, **strchr** returns a pointer to the character in the string; otherwise, **strchr** returns NULL.

+   - Function **strcspn** (p. 387) determines the length of the initial part of the string in its first argument that does not contain any characters from the string in its second argument. The function returns the length of the segment.

+   - Function **strpbrk** (p. 387) searches for the first occurrence in its first argument of any character in its second argument. If a character from the second argument is found, **strpbrk** returns a pointer to the character; otherwise, **strpbrk** returns NULL.

+   - Function **strrchr** (p. 388) searches for the last occurrence of a character in a string. If the character is found, **strrchr** returns a pointer to the character in the string; otherwise, **strrchr** returns NULL.

+   - Function **strspn** (p. 389) determines the length of the initial part of the string in its first argument that contains only characters from the string in its second argument. The function returns the length of the segment.

+   - Function **strstr** (p. 389) searches for the first occurrence of its second string argument in its first string argument. If the second string is found in the first string, a pointer to the location of the string in the first argument is returned.

+   - A sequence of calls to **strtok** (p. 390) breaks the first string **s1** into tokens (p. 390) that are separated by characters contained in the second string **s2**. The first call contains **s1** as the first argument, and subsequent calls to continue tokenizing the same string contain NULL as the first argument. A pointer to the current token is returned by each call. If there are no more tokens when the function is called, a NULL pointer is returned.

# ### Section 8.9 Memory Functions of the String-Handling Library

+   - Function **memcpy** (p. 392) copies a specified number of bytes from the object to which its second argument points into the object to which its first argument points. The function can receive a pointer to any type of object.

+   - Function **memmove** (p. 393) copies a specified number of bytes from the object pointed to by its second argument to the object pointed to by its first argument. Copying is accomplished as if the bytes were copied from the second argument to a temporary array and then copied from the temporary array to the first argument.

+   - Function **memcmp** (p. 394) compares the specified number of bytes of its first and second arguments.

+   - Function **memchr** (p. 394) searches for the first occurrence of a byte, represented as `unsigned char`, in the specified number of bytes of an object. If the byte is found, a pointer to the byte is returned; otherwise, a NULL pointer is returned.

+   - Function **memset** (p. 395) copies its second argument, treated as an `unsigned char`, to a specified number of bytes of the object pointed to by its first argument.

# ### Section 8.10 Other Functions of the String-Handling Library

+   - Function **strerror** (p. 396) maps an integer error number into a full text string in a locale-specific manner. A pointer to the string is returned.

+   - Function **strlen** (p. 396) takes a string as an argument and returns the number of characters in the string—the terminating null character is not included in the length of the string.