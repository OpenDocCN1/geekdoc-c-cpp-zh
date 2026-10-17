```
end--;
}
}
// Function to reverse individual words in a string
void reverseWordsInString(char *str)
{
    int length = strlen(str);
    int start = 0;
    for (int end = 0; end <= length; end++)
    {
        if (str[end] == ' ' || str[end] == '\0')
        {
            reverseWord(str, start, end - 1);
            start = end + 1;
        }
    }
}
}
}
int main()
{
    char input[1000];
    printf("Enter a string: ");
    gets(input);
    reverseWordsInString(input);
    printf("Reversed string: %s\n", input);
    return 0;
}
```

+   - **Practical 30:** Write a C program to enter a number and print it in words.
+   - **Solution:**

```
#include <stdio.h>
// Function to print a number in words for the ones place
void printOnes(int num)
```