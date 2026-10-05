# 2 Variables, Constants, and Arithmetic Conversions 27

# EXERCISES

C.2.1 What is the output of the following program?

Answer: The value of i initially becomes equal to i = i+i = 100+100 = 200 and then i = 2*i = 200. Therefore, the program displays: 400 400.

C.2.2 Find the errors in the following program and fix them, so that the program runs and displays Nice.

```
#include <iostream>
int main()
{
    int j = 4.5;
    unsigned float i = 1.23;
    double j = 6.7;

    k = 10;
    cout << "Nice << '\n';
    return 5;
}
```

Answer: Assigning a floating-point value to an integer variable is not wrong, the fraction part will be truncated and j becomes 4. The declaration of i is incorrect, because floating-point variable cannot be declared unsigned because the name j has already been used. The use of k is incorrect, because it hasn't been declared. Another error is the missing " next to Nice. A program may return a non-zero value, so the return statement is acceptable.

C.2.3 Write a program that declares two integers, assigns to the values 50 and 20, and displays in separate lines their sum, difference, product, produce the result of their division (i.e., 2.5), and the remainder (i.e., 10). To find the remainder use the % operator. Use a single cout statement.

```
#include <iostream>
int main()
{
    int i = 50, j = 20;

    std::cout << "Sum:" << i+j << "\nDiff:" << i-j << "\nProd:" << i*j << "\nDiv:" << (double)i/j << "\nRem:" << i%j << '\n';
    return 0;
}
```