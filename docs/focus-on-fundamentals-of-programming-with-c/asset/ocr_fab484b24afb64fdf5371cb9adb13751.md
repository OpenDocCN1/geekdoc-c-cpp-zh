Here's a simple program to determine whether or not a number is odd or even:

```
int main(void) {
    int num;

    printf("Enter a number: ");
    scanf("%d", &num);
    if (num % 2 == 0) {
        printf("The number is even.\n");
    } else {
        printf("The number is odd.\n");
    }
    return 0;
}
```

Note that anyplace C allows a statement in a control structure, the statement can be a compound statement delimited by braces:

```
int main(void) {
    int num;

    printf("Enter a number: ");
    scanf("%d", &num);
    if (num % 2 == 0) {
        printf("The number entered is %d.\n", num);
        printf("The number is even.\n");
    } else {
        printf("The number entered is %d.\n");
        printf("The number is odd.\n");
    }
    return 0;
}
```