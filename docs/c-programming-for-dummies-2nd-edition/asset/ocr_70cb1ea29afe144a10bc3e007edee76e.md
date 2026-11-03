At Line 5, the enum keyword creates a list of enumerated constants to represent values 0 through 4. Each constant refers to an element in the temps array, corresponding to a day of the week. This example shows how enumerated constants are used to make a program more readable.

# Exercise 19-11

Rewrite the code so that the two printf() statements from Listing 19-5 use pointer notation to output the values. You may use literal values or the enumerated constants in your code.

# Strings Are Pointer-Things

C lacks a string data type but it does have the char array, which is effectively the same thing. As an array, a string in C can be completely twisted, torqued, and abused by using pointers. It's a much more interesting topic than messing with numeric arrays, which is why it gets a whole section all by itself.

# Using pointers to display a string

You're most likely familiar with displaying a string in C, probably by using either the puts() or printf() function. Strings, too, can be displayed one character at a time by plodding through an array. To wit, I offer Listing 19-6.

```
Hello, String

#include <stdio.h>

int main()
{
	char sample[] = "From whence cometh my help?\n";
	int index = 0;
	while(sample[index] != '\0')
	{
		putchar(sample[index]);
		index++;
	}
	return(0);
}
```