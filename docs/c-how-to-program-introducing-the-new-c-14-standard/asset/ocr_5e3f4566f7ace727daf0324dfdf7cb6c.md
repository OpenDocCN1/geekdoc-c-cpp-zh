| Function | Description |
|---|---|
| `char* strpbrk(const char* s1, const char* s2)` | Locates the first occurrence in string `s1` of any character in string `s2`. If a character from string `s2` is found, a pointer to the character in string `s1` is returned. Otherwise, a null pointer is returned. |
| `size_t strcspn(const char* s1, const char* s2)` | Determines and returns the length of the initial segment of string `s1` consisting of characters not contained in string `s2`. |
| `char* strstr(const char* s1, const char* s2)` | Locates the first occurrence in string `s1` of string `s2`. If the string is found, a pointer to the string in `s1` is returned. Otherwise, a null pointer is returned. |

Function `strchr` searches for the first occurrence of a character in a string. If the character is found, `strchr` returns a pointer to the character in the string; otherwise, `strchr` returns a null pointer. The program of **Fig. 22.35** uses `strchr` (lines 13 and 23) to search for the first occurrences of `'a'` and `'z'` in the string `"This is a test"`.