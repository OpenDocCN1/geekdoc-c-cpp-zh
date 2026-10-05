The first call in the sequence searches the string pointed to by s1 for the first character that is not contained in the current separator string pointed to by s2. If no such character is found, there are no tokens in the string pointed to by s1 and the strtok function returns a null pointer. If such a character is found, it is the start of the first token.

The strtok function then searches for a character that is contained in the current separator string. If no such character is found, the current token extends to the end of the string pointed to by s1, and subsequent searches for a token will return a null pointer. If such a character is found, it is overwritten by a null character, which terminates the current token. The strtok function saves a pointer to the following character, from which the next search for a token will start.

Each subsequent call, with a null pointer as the value of the first argument, starts searching from the saved pointer and behaves as described above.

The strtok function is not required to avoid data races with other calls to the strtok function.³311 The implementation shall behave as if no library function calls the strtok function.

# Returns

The strtok function returns a pointer to the first character of a token, or a null pointer if there is no token.

# EXAMPLE

```
#include <string.h>
static char str[] = "????b
```

Forward references: The strtok_s function (K.3.7.3).

311 The strtok_s function can be used instead to avoid data races.