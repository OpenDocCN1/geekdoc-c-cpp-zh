# 28 Introduction to C++

Comments: As we see in Chapter 4, the % operator is used to find the remainder of the division of two integer operands. The other operators are used as in math. If we omit the cast of i and write i/j, the program would output the result of division, that is, 2.

# C.2.4 What is the output of the following program?

```
#include <iostream>
int main()
{
    bool b = 18;
    int i = b+2;
    double d = i+1.99;

    i = d*2;
    std::cout << i/10 << '\n';
    return 0;
}
```

Answer: The declarations make b equal to 1, i becomes 3, the type of i is converted to double when added to 1.99, d becomes 4.99. Then, i becomes 9 and the program displays the result of the division by 8 (10 is 8 in octal), that is, 1.

# C.2.5 Write a program that assigns a two-digit positive value to an integer and displays the sum of its digits. For example, if the assigned value is 35, the program should display 8. Don't use the % operator.

```
#include <iostream>
int main()
{
    int i, j, k;

    i = 35;
    j = i/10;
    k = i - (10*j);
    std::cout << j+k << '\n';
    return 0;
}
```

Comments: The use of std::cout << i/10 calculates the value of i. Notice that we could omit the declarations of j and k, and write std::cout << i/10+(10*(i/10));

# C.2.6 What is the output of the following program?

```
#include <iostream>
int main()
{
    int k;
    float i = 3.9, j = 1.2;

    k = i + (int)j;
    std::cout << k - (int)(i + j) << '\n';
    return 0;
}
```

Answer: Since the value of (int)j is 1, we have k=3.9+1 = 4 (not 4.9, because k is int). Similarly, we have (int)((int)3.9+1.2) = (int)(3+1.2) = (int)(4.2) = 4. Therefore, the program outputs 0.