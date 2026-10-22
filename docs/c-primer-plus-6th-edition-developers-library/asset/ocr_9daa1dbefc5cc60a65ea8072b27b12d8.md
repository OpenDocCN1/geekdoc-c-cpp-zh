The numbers used to identify the array elements are called subscripts, indices, or offsets. The subscripts must be integers, and, as mentioned, the subscripting begins with 0. The array elements are stored next to each other in memory, as shown in Figure 6.7.

![](bbox=[0.27, 0.23, 0.72, 0.28])

![](bbox=[0.28, 0.31, 0.52, 0.38])

Figure 6.7 The char and int arrays in memory.

# Using a for Loop with an Array

There are many, many uses for arrays. Listing 6.19 is a relatively simple one. It’s a program that reads in 10 golf scores that will be processed later. By using an array, you avoid the need to invent 10 different variable names, one for each score. Also, you can use a for loop to do the reading. The program goes on to report the sum of the scores and their average and a handicap, which is the difference between the average and a standard score, or par.

# Listing 6.19 The scores_in.c Program

```
// scores_in.c -- uses loops for array processing
#include <stdio.h>
#define SIZE 10
#define PAR 72
int main(void)
{
    int index, score[SIZE];
    int sum = 0;
    float average;

    printf("Enter %d golf scores:\n", SIZE);
    for (index = 0; index < SIZE; index++)
        scanf("%d", &score[index]); // read in the ten scores
    printf("The scores read in are as follows:\n");
    for (index = 0; index < SIZE; index++)
        printf("%5d", score[index]); // verify input
    printf("\n");
```