Where **first** and **second** are two strings to be compared, *n* is the number of character from which first string does not match with second string.

# ## Problem

Write a program, which returns the position of the string from where first string does not match with second string.

# ## Solution

```
```c
#include <stdio.h>
#include <string.h>
#include<conio.h>
void main()
{
char first[80], second[80];
clrscr();
printf("\nEnter first string: ");
gets(first);
printf("\nEnter second string: ");
gets(second);
printf("\nAfter %d characters there is no match", strspn(first, second));
getch();
}
```
```

The output of the above code is as follows

Enter first string: HELLOBROTHER  
Enter second string: HELLOSISTER  
After 5 characters there is no match

# ## OTHER STRING FUNCTIONS

Now we will discuss some other important string functions.

# ### strncpy () Function

The **strncpy** function same as strcpy. It copies characters of one string to another string up to the specified length.

The general syntax of strncpy () function is as follows:

```
```c
strncpy (str1, str2, No. of characters);
```
```

# ### Example

```
```c
strncpy (str1, str2, 10);
```
```

Where **str1** and **str2** are two strings. The 10 characters of string **str2** are copied onto string **str1**.

# ### strncmp Function

The **strncmp** function is same as **strcmp**, except it compares two strings up to a specified length.

The general syntax of the above function is as follows:

```
```c
n = strncmp(str1, str2, 10);
```
```

Where 10 characters of **str1** and **str2** are compared and *n* is returned value of differed characters.

# ### strstr () Function

The **strstr** function takes two arguments address of the string and second string as inputs. And returns the address from where the second string starts in first string.

The general syntax of the above function is as follows:

```
```c
cp = strstr (first, second);
```
```

where first and second are two strings, cp is character pointer.

# ## Programming Problems

# ### Problem 1

Write a program to concatenate two strings without using the strcat () function.

# ### Solution

```
```c
# include<string.h>
# include<stdio.h>
# include<conio.h>
void main ()
{
char str1 [10];
char str2 [10];
char output_str [20];
clrscr();
int i=0, j=0, k=0;
printf("\n Enter first string: ");
gets(str1);
printf("\n Enter second string: ");
gets (str2);
while (str1[i] != '\0')
output_str[k++] = str1[i++];
while(str2[j] != '\0')
output_str[k++] = str2[j++];
output_str[k] = '\0';
puts (output_str);
getch (); 
}
```
```

The output of the above program is as follows:

Enter first string Manish  
Enter second string Varshney  
ManishVarshney