the second example of the previous section, what does the program output if we change the default case to:

```
default:
    if(i == 3)
        break;
    else
        continue;
printf("* ");
break;
```

Since the continue statement causes the next iteration to begin, the program displays nothing.

# Exercises

# C.6.4 What is the output of the following program?

```
#include <stdio.h>
int main(void)
{
    int i = 0, j = 5;
    for(i > j; i+j == 5; j < 2)
    {
        printf("One\n");
        i = 4;
        j = 2;
    }
    printf("%d %d\n", i, j);
    return 0;
}
```

Answer: The value of i > j is 0; however, this does not affect the execution of the loop. Let's trace the iterations:

First iteration. Since i is 0, the condition i+j == 5 (0+5 = 5 == 5) is true and the program outputs One. Next, i and j become 4 and 2, respectively.

Second iteration. The value of j < 2 is 0; however, this does not affect the execution. Since the condition i+j == 5 (4+2 = 6 == 5) becomes false, the loop ends.

The program displays the values of i and j, that is, 4 and 2, respectively.

# C.6.5 A test consists of 10 multiple choice questions, each of which has three possible answers. The first answer gets three points, the second one point, and the third two points. Write a program that uses the switch statement to read the test taker's 10 answers and display the final score.