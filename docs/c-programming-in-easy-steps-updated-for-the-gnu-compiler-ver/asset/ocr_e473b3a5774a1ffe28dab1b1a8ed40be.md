1. Begin a new program with a preprocessor instruction to include the standard input/output library functions #include <stdio.h>

2. Add a main function that declares two integer variables

```
int main()
{
  int a , b;
}
```

3. Next, in the main function block, output the result of assignment operations performed on the variables

```
printf("Assigned:\n");
printf("\tVariable a = %d\n", a = 8);
printf("\tVariable b = %d\n", b = 4);
printf("Added & assigned:\n");
printf("\tVariable a += b (8+=4) a = %d\n", a += b);
printf("Subtracted & assigned:\n");
printf("\tVariable a-=b (12-=4) a = %d\n", a -= b);
printf("Multiplied & assigned:\n");
printf("\tVariable a*=b (8*=4) a = %d\n", a *= b);
printf("Divided & assigned:\n");
printf("\tVariable a/=b (32/=4) a = %d\n", a /= b);
printf("Modulated & assigned:\n");
printf("\tVariable a%%=b (8%%=4) a = %d\n", a %= b);
```

4. At the end of the main function block, return a zero integer value, as required by the function declaration

```
return 0;
```

5. Save the program file, then compile and execute the program to see the results of the assignment operations

![](bbox=[0.7, 0.1, 0.85, 0.25])

![](bbox=[0.7, 0.6, 0.82, 0.75])

Notice that %% must be used in order to display the % character with the printf() function.

![](bbox=[0.18, 0.85, 0.7, 0.98])