# 2.4 C Programming and Data Structures

while the statement

printf("\nSee,\n....\n....remember !");

will print out

I see,
I remember !

I
See,
.....I
......remember !

Before we proceed to discuss further examples, we must note one important point. C does make a distinction between uppercase and lowercase letters. For example, printf and PRINTF are not the same. In C, everything is written in lowercase letters. However, uppercase letters are used for symbolic names representing constants. We may also use uppercase letters in output strings like "I SEE" and "I REMEMBER".

The above example ... is one of the simplest programs. Figure 2.2 highlights the general format. All C programs need a main function.

![](bbox=[0.28, 0.72, 0.75, 0.86])

# Sample Program 2: Adding Two Numbers

Consider another program which performs addition on two numbers and displays the result. The complete program is shown in Fig. 2.3.

```
/* Program ADDITION */
/* Written by EBG */
main()
{
    int number;
    float amount;

    number = 100;

    amount = 30.75 + 75.35;
    printf("%d\n", number);
    printf("%5.2f", amount);
}
Fig. 2.3 Program to add two numbers
```