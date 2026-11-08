
- 40. Given the following program segment:

```cpp
int limit = 4;
int first = 5;
int j;

for (j = 1; j <= limit; j++)
{
    cout << first * j << endl;
    first = first * (j - 1);
}
cout << endl;
```

  Write a while loop and a do...while loop that have the same output.

- 41. Consider the following program:

```cpp
#include <iostream>

using namespace std;

int main()
{
    int num1, num2;
    int temp = 0;

    cout << "Enter two integers: ";
    cin >> num1 >> num2;
    cout << endl;

    do
    {
        temp = num1 + num2;
        num1 = num2;
        num2 = temp;
        cout << temp << " ";
    }
    while (((num1 + num2) % 5) != 0);

    cout << endl;

    return 0;
}
```

  - a. What is the output if the input is 13 16?
  - b. What is the output if the input is −4 6?
  - c. What is the output if the input is 3 5?
  - d. What is the output if the input is 13 15?

- 42. To learn how nested for loops work, do a walk-through of the following program segments and determine, in each case, the exact output.

  - a.
    ```cpp
    int i, j;

    for (i = 1; i <= 5; i++)
    {
        for (j = 1; j <= 5; j++)
            cout << setw(3) << i;
        cout << endl;
    }
    ```
  - b.
    ```cpp
    int i, j;
    for (i = 1; i <= 5; i++)
    {
        for (j = (i + 1); j <= 5; j++)
            cout << setw(5) << j;
        cout << endl;
    }
    ```
  - c.
    ```cpp
    int i, j;
    for (i = 1; i <= 5; i++)
    {
        for (j = 1; j <= i; j++)
            cout << setw(3) << j;
        cout << endl;
    }
    ```
  - d.
    ```cpp
    const int M = 10;
    const int N = 10;
    int i, j;

    for (i = 1; i <= M; i++)
    {
        for (j = 1; j <= N; j++)
            cout << setw(3) << M * (i - 1) + j;
        cout << endl;
    }
    ```
  - e.
    ```cpp
    int i, j;

    for (i = 1; i <= 9; i++)
    {
        for (j = 1; j <= (9 - i); j++)
            cout << " ";
        for (j = 1; j <= i; j++)
            cout << setw(1) << j;
        for (j = (i - 1); j >= 1; j--)
            cout << setw(1) << j;
        cout << endl;
    }
    ```

- 43. What is the output of the following program segment?

```cpp
int count = 1;
do
    cout << count * (count - 2) << " ";
while (count++ <= 5);

cout << endl;
```

- 44. What is the output of the following code?

```cpp
int num = 12;

while (num >= 0)
{
    if (num % 5 == 0)
        break;

    cout << num << " ";
    num = num - 2;
}

cout << endl;
```

- 45. What is the output of the following code?

```cpp
int num = 12;

while (num >= 0)
{
    if (num % 5 == 0)
    {
        num++;
        continue;
    }

    cout << num << " ";
    num = num - 2;
}
cout << endl;
```

- 46. What does a break statement do in a loop?

## PROGRAMMING EXERCISES

- 1. Write a program that prompts the user to input an integer and then outputs both the individual digits of the number and the sum of the digits. For example, it should output the individual digits of 3456 as 3 4 5 6, output the individual digits of 8030 as 8 0 3 0, output the individual digits of 2345526 as 2 3 4 5 5 2 6, output the individual digits of 4000 as 4 0 0 0, and output the individual digits of −2345 as 2 3 4 5.
- 2. The value of π can be approximated by using the following series:

  π = 4(1 − 1/3 + 1/5 − 1/7 + 1/9 + ⋯ + 1/(2n − 1) + 1/(2n + 1)).

  The following program uses this series to find the approximate value of π. However, the statements are in the incorrect order, and there is also a bug in this program. Rearrange the statements and also find and remove the bug so that this program can be used to approximate π.

  ```cpp
  #include <iostream>
  #include <iomanip>

  using namespace std;

  int main()
  {
      double pi = 0;
      long i;
      long n;

      cin >> n;
      cout << "Enter the value of n: ";
      cout << endl;

      if (i % 2 == 0)
          pi = pi + (1 / (2 * i + 1));
      else
          pi = pi - (1 / (2 * i + 1));

      for (i = 0; i < n; i++)
      {
          pi = 0;
          pi = 4 * pi;
      }

      cout << endl << "pi = " << pi << endl;

      return 0;
  }
  ```

- 3. Rewrite the program of Example 5-5, Telephone Digits. Replace the statements from Lines 10 to 28 so that the program uses only a switch structure to find the digit that corresponds to an uppercase letter.
- 4. The program Telephone Digits outputs only telephone digits that correspond to uppercase letters. Rewrite the program so that it processes both uppercase and lowercase letters and outputs the corresponding telephone digit. If the input is something other than an uppercase or lowercase letter, the program must output an appropriate error message.
- 5. To make telephone numbers easier to remember, some companies use letters to show their telephone number. For example, using letters, the telephone number 438-5626 can be shown as GET LOAN. In some cases, to make a telephone number meaningful, companies might use more than seven letters. For example, 225-5466 can be displayed as CALL HOME, which uses eight letters. Write a program that prompts the user to enter a telephone number in digits. If the user enters more than seven letters, then process only the first seven letters. Also output the - (hyphen) after the third digit. Allow the user to use both uppercase and lowercase letters as well as spaces between words. Moreover, your program should process as many telephone numbers as the user wants.
- 6. Write a program that reads a set of integers and then finds and prints the sum of the even and odd integers.
- 7. Write a program that prompts the user to input a positive integer. It should then output a message indicating whether the number is a prime number. *(Note: An even number is prime if it is 2. An odd integer is prime if it is not divisible by any odd integer less than or equal to the square root of the number.)*
- 8. Let $n=a_k a_{k-1}a_{k-2}\ldots a_1a_0$ be an integer and $t=a_0-a_1+a_2-\cdots+(-1)^k a_k$. It is known that $n$ is divisible by 11 if and only if $t$ is divisible by 11. For example, suppose that $n=8784204$. Then, $t=4-0+2-4+8-7+8=11$. Because 11 is divisible by 11, it follows that 8784204 is divisible by 11. If $n=54063297$, then $t=9-7+2-3+6-0+4-5=2$. Because 2 is not divisible by 11, 54063297 is not divisible by 11. Write a program that prompts the user to enter a positive integer and then uses this criterion to determine whether the number is divisible by 11.
- 9. Write a program that uses while loops to perform the following steps:

  - a. Prompt the user to input two integers: firstNum and secondNum (firstNum must be less than secondNum).
  - b. Output all odd numbers between firstNum and secondNum.
  - c. Output the sum of all even numbers between firstNum and secondNum.
  - d. Output the numbers and their squares between 1 and 10.
  - e. Output the sum of the square of the odd numbers between firstNum and secondNum.
  - f. Output all uppercase letters.

- 10. Redo Programming Exercise 9 using for loops.
- 11. Redo Programming Exercise 9 using do...while loops.
- 12. The program in the Programming Example: Fibonacci Number does not check whether the first number entered by the user is less than or equal to the second number and whether both the numbers are nonnegative. Also, the program does not check whether the user entered a valid value for the position of the desired number in the Fibonacci sequence. Rewrite that program so that it checks for these things.
- 13. The population of a town $A$ is less than the population of town $B$. However, the population of town $A$ is growing faster than the population of town $B$. Write a program that prompts the user to enter the population and growth rate of each town. The program outputs after how many years the population of town $A$ will be greater than or equal to the population of town $B$ and the populations of both the towns at that time. (A sample input is: Population of town $A=5000$, growth rate of town $A=4\%$, population of town $B=8000$, and growth rate of town $B=2\%$.)
- 14. Suppose that the first number of a sequence is $x$, in which $x$ is an integer. Define $a_0=x$; $a_{n+1}=a_n/2$ if $a_n$ is even; $a_{n+1}=3\times a_n+1$ if $a_n$ is odd. Then, the exercise is to find a $k$ such that $a_k=1$. Write a program that prompts the user to input the value of $x$. The program output the integer $k$ such that $a_k=1$ and the numbers $a_0$, $a_1$, $a_2$, ..., $a_k$. (For example, if $x=75$, then $k=14$, and the numbers are 75, 226, 113, 340, 170, 85, 256, 128, 64, 32, 16, 8, 4, 2, 1.) Test your program for the following values of $x$: 75, 111, 678, 732, 873, 2048, and 65535.
- 15. Enhance your program from Programming Exercise 14 by outputting the position of the largest number and the largest number of the sequence $a_0$, $a_1$, ..., $a_k$. (For example, the largest number of the sequence 75, 226, 113, 340, 170, 85, 256, 128, 64, 32, 16, 8, 4, 2, 1 is 340, and its position is 4.) Test your program for the following values of $x$: 75, 111, 678, 732, 873, 2048, and 65535.
- 16. The program in Example 5-6 implements the Number Guessing Game. However, in that program, the user is given as many tries as needed to guess the correct number. Rewrite the program so that the user has no more than five tries to guess the correct number. Your program should print an appropriate message, such as “You win!” or “You lose!”.
- 17. Example 5-6 implements the Number Guessing Game program. If the guessed number is not correct, the program outputs a message indicating whether the guess is low or high. Modify the program as follows: Suppose that the variables `num` and `guess` are declared as in Example 5-6 and `diff` is an `int` variable. Let `diff` = the absolute value of (`num − guess`). If `diff` is 0, then the guess is correct and the program outputs a message indicating that the user guessed the correct number. Suppose `diff` is not 0. Then the program outputs the message as follows:

  - a. If `diff` is greater than or equal to 50, the program outputs the message indicating that the guess is very high (if guess is greater than num) or very low (if guess is less than num).
  - b. If `diff` is greater than or equal to 30 and less than 50, the program outputs the message indicating that the guess is high (if guess is greater than num) or low (if guess is less than num).
  - c. If `diff` is greater than or equal to 15 and less than 30, the program outputs the message indicating that the guess is moderately high (if guess is greater than num) or moderately low (if guess is less than num).
  - d. If `diff` is greater than 0 and less than 15, the program outputs the message indicating that the guess is somewhat high (if guess is greater than num) or somewhat low (if guess is less than num).

  As in Programming Exercise 16, give the user no more than five tries to guess the number. (To find the absolute value of `num − guess`, use the expression `abs(num − guess)`. The function `abs` is from the header file `cstdlib`.)
