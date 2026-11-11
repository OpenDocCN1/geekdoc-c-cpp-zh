# Output:

```
Enter a character
$
Character you entered is
$
```

The statement,

```
x=getchar();
```

waits for user to input a character. The character inputted by the user is stored in variable x. In reality, the function stores the ASCII value of the input character in the variable x and hence the function getchar() returns an integer value (as ASCII values are integers). All we need to note at this stage is that the character inputted by the user is not stored in variable x, so if user inputs say $ then x will contain $ . Remember, the function can take only 1 character as input at a time, so if you need to input another character we need to use another getchar() function.

The statement,

```
putchar(x);
```

prints the character value stored in variable x on the computer screen. So, for example, if the value of x is $, then $ will appear on the computer screen.

> **NOTES**
> 
> The functions `getchar()` and `putchar()` are declared in the header file `stdio.h`. Hence, this header file must be included before using these functions in the program.

# Quiz

+   1. Fill in the blank spaces:
+   
+      If a size of a particular data type is 10 bytes, ________ is the range of signed values and ________ is the range of unsigned values that can be stored in the variable of this type. Assume that the data type supports only numerical values without any fractional components.
+   
+   2. Determine the output of three `printf()` statements given below assuming value of variable `z` as initialized:
+   
+   3. Consider the `scanf()` statement to input values of variables `a` and `b`.

```
int z = -2000;
printf("%020d",z);
printf("%-20d",z);
printf("%#o",z);
```

```
int a,b;
scanf("%3d %2d",&a,&b);
```

Given the values of variables a and b in each of the following cases of user input

**Case 1:** User input is `32000 42000`

**Case 2:** User input is `333 10000`

**Case 3:** User input is `12 1`