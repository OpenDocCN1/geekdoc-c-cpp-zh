92

Chapter 6. Standard Input/Output

interactive programs or when precise control of the input and output streams is required.

# Summary

In this chapter, we explored essential concepts related to input and output in C. We discussed the powerful printf function for formatted output and the scanf function for formatted input, using syntax, formatting spec, and escape sequences. Additionally, we touched on character-based input and output using putchar and getchar.

# Questions

+   6.1 How do you print the value of an integer variable num using printf?
6.2 What is the purpose of the format specifier %d in printf?
6.3 What is the return type of getchar function?
6.4 How do you format and print a floating-point number num with two decimal places using printf?
6.5 How do you display a string str on the console using printf?
6.6 How do you display a string str on the console using puts?
6.7 What is the difference between printf and puts when printing strings?
6.8 How do you display the string "Hello" with the enclosing quotation marks using printf?
6.9 What is the purpose of a buffer when reading a string from the standard input?
6.10 What will be the output of the following code snippet? Explain why.

```
int num = 5;
printf("The value is: %f\n", num);
```

+   6.11 Identify the issue in the following code and suggest a fix:

```
char str[10];
canf("%s", str);
printf("You entered: %s\n", str);
```

+   6.12 Why does this code only capture the first word of input (e.g., "Hello World" becomes "Hello")? How can you fix it to read the entire line? 

```
#include <stdio.h>

int main() {
    char str[50];
    printf("Enter a sentence: ");
    scanf("%s", str);
    printf("You entered: %s\n", str);
    return 0;
}
```