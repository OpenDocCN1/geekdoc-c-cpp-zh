```
#include <stdio.h>

int main(int argc, const char * argv[])
{
	unsigned long x = 255;
	printf("x is %lu.\n", x);
	
	// Octal and hex already assumed the number was unsigned
	printf("In octal, x is %lo.\n", x);
	printf("In hexadecimal, x is %lx.\n", x);
	
	return 0;
}
```

# ## Integer operations

The arithmetic operators +, -, and * work as you would expect. They also have the precedence rules that you would expect: * is evaluated before + or -. In main.c, replace the previous code with a calculation:

```
#include <stdio.h>

int main(int argc, const char * argv[])
{
	printf("3 * 3 + 5 * 2 = %d\n", 3 * 3 + 5 * 2);
	
	return 0;
}
```

You should see
3 * 3 + 5 * 2 = 19

# ## Integer division

Most beginning C programmers are surprised by how integer division works. Try it:

```
#include <stdio.h>

int main(int argc, const char * argv[])
{
	printf("3 * 3 + 5 * 2 = %d\n", 3 * 3 + 5 * 2);
	printf("11 / 3 = %d\n", 11 / 3);
	
	return 0;
}
```

You'll get 11 / 3 = 3.66667, right? Nope. You get 11 / 3 is 3. When you divide one integer by another, you always get a third integer. The system rounds off toward zero. (So, -11 / 3 is -3)

This actually makes sense if you think "11 divided by 3 is 3 with a remainder of 2." And it turns out that the remainder is often quite valuable. The modulus operator (%) is like /, but it returns the remainder instead of the quotient: