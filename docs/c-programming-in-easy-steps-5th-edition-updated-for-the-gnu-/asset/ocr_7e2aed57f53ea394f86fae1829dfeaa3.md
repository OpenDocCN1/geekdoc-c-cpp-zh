# # Examining conditions

Possibly the C programmer’s favorite test operator is the ?: conditional operator, also known as the “ternary” operator. This operator first evaluates an expression for a true or false Boolean value, then executes one of two given statements depending on the result of the evaluation.

![](bbox=[0.35, 0.32, 0.65, 0.42])

The conditional operator has this syntax:

```
```
(test-expression) ? if-true-do-this : if-false-do-this ;
```
```

This operator could, for example, be used to evaluate whether a given number is odd or even by examining if there is any remainder after dividing the number by two, then output an appropriate string, like this:

```
```
(7 % 2 != 0) ? printf("Odd Number") : printf("Even Number");
```
```

In this case, dividing seven by two does not leave a zero remainder – so the expression evaluates as true; therefore the first statement is executed, correctly describing the number as odd value.

The conditional operator is also useful to ensure correct grammar in output regarding singular and plural items, thus avoiding awkward phrases like “There is 5”. The evaluation can simply be made within the printf statement to use the appropriate version:

```
```
printf("There %s %d", (num == 1) ? "is" : "are", num);
```
```

In this case, when it’s true that the num variable has a value of one, the “is” version will be used, otherwise the “are” version will be used.