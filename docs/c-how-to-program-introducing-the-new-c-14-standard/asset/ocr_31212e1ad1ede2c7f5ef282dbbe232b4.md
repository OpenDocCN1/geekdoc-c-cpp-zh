|  | Description |
|---|---|
|  | The first argument, and subsequent calls to continue tokenizing the same string contain `NULL` as the first argument. A pointer to the current token is returned by each call. If there are no more tokens when the function is called, `NULL` is returned. |
| `size_t strlen(const char *s);` |  |
|  | Determines the length of string `s`. The number of characters preceding the terminating null character is returned. |

Several functions in **Fig. 22.21** contain parameters with data type `size_t`. This type is defined in the header `<cstring>` to be an unsigned integral type such as `unsigned int` or `unsigned long`.

![](bbox=[0.12, 0.51, 0.191, 0.564])

# # Common Programming Error 22.7

*Forgetting to include the `<cstring>` header when using functions from the string-handling library causes compilation errors.*

# ## Copying Strings with `strcpy` and `strncpy`

Function `strcpy` copies its second argument—a string—into its first argument—a character array that must be large enough to store the string *and* its *terminating null character*, (which is also copied).