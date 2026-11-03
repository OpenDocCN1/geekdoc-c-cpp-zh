printf( "%d", *yPtr );

prints the value of variable y (5). Using * in this manner is called dereferencing a pointer.

**Common Programming Error 7.2**

*Dereferencing a pointer that has not been properly initialized or that has not been assigned to point to a specific location in memory is an error. This could cause a fatal execution-time error, or it could accidentally modify important data and allow the program to run to completion with incorrect results.*

# Demonstrating the & and * Operators

Figure 7.4 demonstrates the pointer operators & and *. The printf conversion specifier %p outputs the memory location as a hexadecimal integer on most platforms. (See Appendix C for more information on hexadecimal integers.) In the program's output, notice that the address of a and the value of aPtr are identical in the output, thus confirming that the address of a is indeed assigned to the pointer variable aPtr (line 8). The & and * operators are complements of one another—when they're both applied consecutively to aPtr in either order (line 18), the same result is printed. The addresses shown in the output will vary across systems. Figure 7.5 lists the precedence and associativity of the operators introduced to this point.

```
1 // Fig. 7.4: fig07_04.c
2 // Using the & and * pointer operators.
3 #include <stdio.h>
4
5 int main(void)
6 {
7    int a = 7;
8    int *aPtr = &a; // set aPtr to the address of a
9
10   printf("The address of a is %p\n"
11          "The value of aPtr is %p\n", &a, aPtr);
12
13   printf("\nThe value of a is %d\n"
14          "The value of *aPtr is %d\n", a, *aPtr);
15
16   printf("\n\nShowing that & and * are complements of "
17          "each other\n*aPtr = %p\n"
18          "\n&*aPtr = %p\n", *&aPtr, &*aPtr);
19 }
```

```
The address of a is 0028FEC0
The value of aPtr is 0028FEC0

The value of a is 7
The value of *aPtr is 7

Showing that & and * are complements of each other
&*aPtr = 0028FEC0
*&aPtr = 0028FEC0
```

Fig. 7.4 | Using the & and * pointer operators.