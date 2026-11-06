# 22.8 C String-Manipulation Functions

The string-handling library provides any useful functions for manipulating string data, *comparing* strings, *searching* strings for characters and other strings, *tokenizing* strings (separating strings into logical pieces such as the separate words in a sentence) and determining the *length* of strings. This section presents some common string-manipulation functions of the string-handling library (from the *C++ standard library*). The functions are summarized in **Fig. 22.21**; then each is used in a live-code example. The prototypes for these functions are located in header `<cstring>`.

# Fig. 22.21 String-manipulation functions of the string-handling library.

| Function prototype | Function description |
|---|---|
| `char* strcpy(char* s1, const char* s2);` | |
| | Copies the string `s2` into the character array `s1`. The value of `s1` is returned. |
| `char* strncpy(char* s1, const char* s2, size_t n);` | |
| | Copies at most `n` characters of the string `s2` into the character array `s1`. |