```
```c
{
c = getchar ();
palin[i] = c;
i++;
}while (c != '\n');
i = i-1;
palin[i] = '\0';
count = i;
if (palindrome(palin,count) == 1)
printf ("\n entered word is not a palindrome");
else
printf ("\n entered word is a palindrome");
getch();
}
short int palindrome(char *palin, int len)
{
short int i = 0, j = 0;
for(i=0; j=len-1; i < len/2; i++,j--)
{
if (palin[i] == palin[j])
continue;
else
return(1);
}
return(0);
}
```
```

The output of the above code segment is as follows:

Enter a word: dalda  
Entered word is not a palindrome  
Enter a word: accbba  
Entered word is a palindrome.

Array of pointers to strings
Arrays may contain pointers. We can form an array of strings, referred to as a string array. Each entry in the array is a string, but in C a string is essentially a pointer to its first character, so each entry in an array of strings is actually a pointer to the first character of a string. Consider the following declaration of a string array:

```
```c
char *country[] =
{
"INDIA", "CHINA", "BANGLADESH",
"PAKISTAN", "US"
};
```
```

The *country[ ] of the declaration indicates an array of five elements. The char* of the declaration indicates that each element of the array country is of type “pointer to char”.

Thus, country[0] will point to INDIA, country[1] will point to CHINA, and so on.

Thus, even though the array country is fixed in size, it provides access to character strings of any length. However, a specified amount of memory will have to be allocated for each string later in the program, for example, country[i] = (char*) malloc(15 * sizeof (char)). The country pointer strings could have been placed into a two-dimensional array but such a data structure must have a fixed number of columns per row, and that number must be as large as the largest string. Therefore considerable memory is wasted when a large number of strings are stored with most strings shorter than the longest string.

As individual strings can be accessed by referring to the corresponding array element, individual string elements be accessed through the use of the indirection operator.

For example, *( * country + 3 ) + 2) refers to the third character in the fourth string of the array country.

# Problem 2

Write a program to enter a list of strings and rearrange them in alphabetical order, using a one-dimensional array of pointers, where each pointer indicates the beginning of a string:

# Solution

```
```c
/* Program to sort a list of strings in alphabetical
order using an array of pointers */
# include <stdio.h>
# include <conio.h>
# include <stdlib.h>
# include <string.h>
void readinput (char *[ ], int);
void writeoutput (char *[ ], int);
void reorder (char *[ ], int);
void main( )
{
char *country[ 5 ];
int i;
clrscr();
for (i = 0; i < 5; i++)
{
country[i] = (char*) malloc (15 * sizeof (char));
}
printf ("Enter five countries on a separate line\n");
```
```