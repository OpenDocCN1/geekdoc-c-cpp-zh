...cont'd

1 Begin a new program with a preprocessor instruction to include the standard input/output library functions

```
#include <stdio.h>
```

![](bbox=[0.7, 0.1, 0.85, 0.25])

2 Add a main function that declares and initializes two integer variables

```
int main()
{
    int yes = 1, no = 0;
}
```

3 Next, in the main function block, output the result of logic operations performed on the variables

```
printf("AND (no&&no): %d \n", no && no );
printf("AND (yes&&no): %d \n", yes && no );
printf("AND (yes&&yes): %d \n", yes && yes );
printf("OR (no||no): %d \n", no || no );
printf("OR (yes||no): %d \n", yes || no );
printf("OR (yes||yes): %d \n", yes || yes );
printf("NOT (yes !yes): %d %d\n", yes , !yes );
printf("NOT (no !no): %d %d\n", no , !no );
```

4 At the end of the main function block, return a zero integer value, as required by the function declaration

```
return 0;
```

5 Save the program file, then compile and execute the program to see the results of the logic operations

![](bbox=[0.15, 0.78, 0.7, 0.97])

![](bbox=[0.7, 0.6, 0.85, 0.75])

Notice that 0 && 0 returns 0 (false) -- demonstrating the anecdote “two wrongs don't make a right”.