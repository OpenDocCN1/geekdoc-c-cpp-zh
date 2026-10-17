+   - **Practical 19:** Write a C program that displays the position or index in the string S where the string T begins, or −1 if S doesn’t contain T.

+   - **Solution:**

```
```c
#include <stdio.h>
#include <string.h>

int findSubstringIndex(const char *S, const char *T)
{
    int sLen = strlen(S);
    int tLen = strlen(T);
    for (int i = 0; i <= sLen − tLen; i++)
    {
        int j;
        for (j = 0; j < tLen; j++)
        {
            if (S[i + j] != T[j])
            {
                break;
            }
        }
        if (j == tLen)
        {
            return i; // Found the substring
        }
    }
    return −1; // Substring not found
}

int main()
{
    const char *S = “Hello, World!”;
    const char *T = “World”;
    int index = findSubstringIndex(S, T);
}
```
```