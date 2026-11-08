# The else-if Statement

The else-if statement is another way of writing decision making programs.

Listing 1.17 shows a program written using an else-if block:

Listing 1.17: Writing the else-if Statement in C

```
```c
#include<stdio.h>

int main()
{
    int marks_obtained;
    float percentage;

    printf("\n Enter marks obtained by candidate out of 500 ");
    scanf("%d",&marks_obtained);

    percentage = marks_obtained/5;

    if(percentage > 90)
    {
        printf("\n Grade Obtained is A");
    }
    else if(percentage > 74)
    {
        printf("\n Grade Obtained is B");
    }
    else if(percentage > 49)
    {
        printf("\n Grade Obtained is C");
    }
    else if(percentage > 34)
    {
        printf("\n Grade Obtained is Just Passed");
    }
    else
        printf("\n Candidate Failed");

    getch();
}
```
```

The output of Listing 1.17 is given as follows:

```
```
Enter marks obtained by candidate out of 500 490

Grade Obtained is A
```
```

The else-if statement is another way of writing the if-else statement.

The following code snippet shows an example of a generic if-else statement:

```
```
if(expression)
{
    statements;
}
else
{
    if(expression)
        statement;
}
```
```