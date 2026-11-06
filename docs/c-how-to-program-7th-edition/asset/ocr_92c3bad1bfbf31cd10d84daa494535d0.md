+   - You can access individual characters in a string directly with array subscript notation.
+   - A string can be read into a character array using stream extraction with `cin`.
+   - The `setw` stream manipulator can be used to ensure that the string read into a character array does not exceed the size of the array.
+   - The `cin` object provides the member function `getline` to input an entire line of text into a character array. The function takes three arguments—a character array in which the line of text will be stored, a length and a delimiter character. The third argument has `\n` as a default value.
+   - A character array representing a null-terminated string can be output with `cout` and `<<`. The characters of the string are output until a null character is encountered.

# Section 8.11 Arrays of Pointers

+   - Arrays may contain pointers.
+   - Such a data structure can be used to form an array of pointer-based strings, referred to as a string array. Each entry in the array is a string, but in C++ a string is essentially a pointer to its first character, so each entry in an array of strings is simply a pointer to the first character of a string.
+   - String arrays are commonly used with command-line arguments that are passed to `main` when a program begins execution.

# Section 8.12 Function Pointers

+   - A pointer to a function is the address where the code for the function resides.
+   - Pointers to functions can be used to call the functions they point to, passed to functions, returned from functions, stored in arrays, assigned to other pointers.

# Terminology

| Term | Page | Term | Page |
|---|---:|---|---:|
| `*` (pointer dereference or indirection operator) | 348 | nonconstant pointer to nonconstant data | 355 |
| address operator (`&`) | 348 | null character (`'\\0'`) | 370 |
| character constant | 370 | null pointer | 347 |
| command-line arguments | 373 | offset to a pointer | 368 |
| constant pointer to constant data | 358 | pass-by-reference with pointer arguments | 350 |
| constant pointer to nonconstant data | 357 | pass-by-reference with reference arguments | 350 |
| dereferencing a pointer | 348 | pointer arithmetic | 365 |
| dereferencing operator (`*`) | 348 | pointer/offset notation | 368 |
| directly references a value | 346 | pointer/subscript notation | 368 |
| function pointer | 374 | pointer to a function | 374 |
| `getline` function of `cin` | 372 | selection sort algorithm | 358 |
| indirection | 346 | `sizeof` operator | 362 |
| indirection (`*`) operator | 348 | special character | 370 |
| indirectly references a value | 346 | string array | 373 |
| nonconstant pointer to constant data | 355 | string constant | 370 |
|  |  | string literals | 370 |

# Self-Review Exercises

+   8.1 Answer each of the following:
+   
+    a) A pointer is a variable that contains as its value the ______ of another variable.
+   
+    b) The three values that can be used to initialize a pointer are ______, ______, and ______.
+   
+    c) The only integer that can be assigned directly to a pointer is ______.