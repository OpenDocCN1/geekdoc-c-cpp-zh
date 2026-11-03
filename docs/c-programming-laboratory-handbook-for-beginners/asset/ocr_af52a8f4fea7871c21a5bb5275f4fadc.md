```
```c
#include<stdio.h>
void main()
{
    /*------------Declarations------------*/
    int number;
    float amount;
    /*------------Assignment Statement------------*/
    number=100;
    /*------------Computational Statements------------*/
    amount=30.75+75.35;
    printf("%d", number);
    printf("\n%5.2f\n", amount);
}
```
```

# **Sample Output**

```
```text
100
106.10
```
```

# **Program 3**

Write a C program to convert temperature values from Fahrenheit to degree Celsius.

```
```c
#include<stdio.h>
void main()
{
    float f, c;
    printf("\n Enter the temperature value in Fahrenheit: ");
    scanf("%f", &f);
    c= (f-32.0)/1.8;
    printf("\n The equivalent temperature value in degrees Celsius is: %.2f\n", c);
}
```
```

# **Sample Output**

```
```text
Enter the temperature value in Fahrenheit: 0
The equivalent temperature value in degrees Celsius is: -17.78
```
```

# **Program 4**

Write a C program that reads an integer and checks whether it is odd or even.

```
```c
#include<stdio.h>
void main()
{
    int num=0, remainder=0;
```
```