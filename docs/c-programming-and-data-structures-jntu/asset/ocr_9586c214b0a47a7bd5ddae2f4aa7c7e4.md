# Examples:

```
m = sizeof(sum);
 n = sizeof(long int);
 k = sizeof(235L);
```

The sizeof operator is normally used to determine the lengths of arrays and structures when their sizes are not known to the programmer. It is also used to allocate memory space dynamically to variables during execution of a program.

# Example 4.3

In Fig. 4.3, the program employs different kinds of operators. The results of their evaluation are also shown for comparison.

Notice the way the increment operator ++ works when used in an expression. In the statement

```
c = ++a - b;
```

new value of a (= 16) is used thus giving the value 6 to c. That is, a is incremented by 1 before it is used in the expression. However, in the statement

```
d = b++ + a;
```

the old value of b (= 10) is used in the expression. Here, b is incremented by 1 after it is used in the expression.

We can print the character % by placing it immediately after another % character in the control string. This illustrated by the statement

```
printf("a%%b = %d\n", a%b);
```

The program also illustrates that the expression

```
c > d ? 1 : 0
```

assumes the value 0 when c is less than d and 1 when c is greater than d.

```
Program
/*****************************************************/
/* ILLUSTRATION OF OPERATORS */
/*****************************************************/
main()
{
 int a, b, c, d;
 a = 15;
 b = 10;
 c = ++a - b;
 printf("a = %d b = %d c = %d\n", a, b, c);
 d = b++ + a;
 printf("a = %d b = %d d = %d\n", a, b, d);
 printf("a/b = %d\n", a/b);
 printf("a%%b = %d\n", a%b);
 printf("a = %d b = %d\n", a, b);
 printf("%d\n", (c > d) ? 1 : 0);
 printf("%d\n", (c < d) ? 1 : 0);
}
```