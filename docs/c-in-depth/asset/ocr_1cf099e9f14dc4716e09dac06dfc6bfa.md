immediately after the label.

```
```c
/*P5.30 Program to print whether the number is even or odd*/
#include<stdio.h>
main()
{
    int n;
    printf("Enter the number : ");
    scanf("%d", &n);
    if(n%2==0)
        goto even;
    else
        goto odd;

even :
    printf("Number is even");
    goto end;

odd :
    printf("Number is odd");
    goto end;

end:
    printf("\n");
}
```
```

```
```
Enter the number : 14
Number is even
```
```

The label can be placed anywhere. If the label is after the goto then the control is transferred forward and it is known as forward jump or forward goto, and if the label is before the goto then the control is transferred backwards and it is known as backward jump or backward goto. In forward goto, the statements between goto and label will not be executed and in backward goto statements between goto and label will be executed repeatedly. More than one goto can be associated with the same label but we cannot have same label at more than one place.

The control can be transferred only within a function using goto statement.(Concept of functions will be introduced in further chapters)

There should always be a statement after any label. If label is at the end of program, and no statements are to be written after it, we can write the null statement (single semicolon) after the label because a program can't end with a label.

The use of 'goto' should be avoided, as it is difficult to understand where the control is being transferred. Sometimes it leads to "spaghetti" code, which is not understandable and is very difficult to debug and maintain. We can always perform all our jobs without using goto, and the use of goto is not favoured in structured programming.

Although the use of goto is not preferred but there is a situation where goto can actually make the code simpler and more readable. This situation arises when we have to exit from deeply nested loops.