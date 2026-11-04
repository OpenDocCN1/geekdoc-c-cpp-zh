U.6.5 What is the output of the following program? You are reminded that printf() returns the number of the displayed characters.

```
#include <stdio.h>
int main(void)
{
    int i, sum;
    float j = 1.2345;
    sum = 0;
    for(i = 0; i < 3; i++)
        sum = sum + printf("%.2f\n", j);
    printf("Val = %d\n", sum);
    return 0;
}
```

U.6.6 Write a program that reads continuously daily temperatures and displays the percentage of those with a temperature equal, less, or more than 40°F. If the user enters 1000, the insertion of temperatures should terminate.

U.6.7 Write a program that reads up to 100 integers. If an input number is greater than the last entered, the insertion of numbers should terminate and the program should display how many numbers were entered.

U.6.8 Write a program that reads three integers (e.g., a, b, and c) one after the other, not all together. The program should force the user to enter the numbers in descending order (i.e., a > b > c).

U.6.9 Write a program that reads the initial height from which a ball is thrown and displays after how many bounces the ball reaches a height less than ¼ of the initial height. The program should prompt the user to enter the decrease height ratio (%). For example, the input value 0.1 means that each time the ball hits the ground, it bounces up to a height 10% less than the previous one.

U.6.10 Write a program that reads integers continuously until the user enters 0. Then, the program should display the largest positive and the smallest negative input numbers. If the user enters only positive or negative numbers, the program should display an informative message. Zero is counted as neither a positive nor a negative number.

U.6.11 Write a program that it is mandatory to read 10 positive numbers. If an input number is negative, the program should prompt the user to enter another one. The program should display how many negative numbers were entered, before it terminates. Use a for loop. Zero is counted as neither a positive or negative number.

U.6.12 Write a program that reads 10 integers and displays how many times the user entered successive values. For example, if the user enters: -5, 10, 17, -31, -30, -29, 75, 76, 9, -4, the program should display 3 due to the pairs: {-31, -30}, {-30, -29}, and {75, 76}.