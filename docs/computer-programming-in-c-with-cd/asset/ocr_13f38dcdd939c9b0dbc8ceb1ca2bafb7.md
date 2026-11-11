```
scanf("%c%d,&ch,&i);
```

In the preceding syntax, the characters received from keyboard are stored in variables (ch, i) corresponding to the addresses of variables obtained using the & operator. These characters are stored as character and integer values according to the specified formats (%c and %d) in the ch and i variables, respectively. Table 1 lists some of the commonly-used format specifiers:

**Table 1: Some of the Commonly Used Format Specifiers**

| Format Specifier | Type |
|---|---|
| %i | int |
| %d | int (decimal) |
| %c | char |
| %f | float |
| %lf | double |
| %s | string |

The printf() function prints a string or a value stored in a variable to the console screen according to the specified format. For example, we can use printf() function for displaying string data in two ways. The first way is to pass a string data within the printf() function and the second is to print the string data stored in the str variable. The following example shows the use of the printf() function:

```
printf("Test string"); // Example 1

printf("%s",&str); // Example 2
```

In the first example, the printf() function takes string as a parameter and prints the specified string in the console screen. On the other hand, in the second example, the printf() function takes two parameters. The first parameter is the string format specifier (%s), which tells the compiler to print string data on the console screen and the second parameter is the address of the variable, str, where the string data is stored in the memory. Listing 2 shows the use of scanf() and printf() functions (you can find this example in the Function2.cpp file on the CD in the codechapter2 folder):

# Listing 2: Using the scanf() and printf() Functions

```
#include <stdio.h>

int main() {
  int num1,num2;
  printf("Enter first number: ");
  scanf("%d",&num1);
  printf("Enter second number: ");
```