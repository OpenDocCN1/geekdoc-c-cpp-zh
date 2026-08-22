# C++ 初学者练习册：带答案练习








![](img/7ba0b827463b67fb137ba99a09ad20b8_0_0.png)




- 1. 写一个 C++ 程序打印 Hello World。

```cpp
#include <iostream>
int main() {
    std::cout << "Hello World!";
    return 0;
}
```

输出
Hello World

- 2. 写一个 C++ 程序打印用户输入的数字。

```cpp
#include <iostream>
using namespace std;
int main() {
    int number;
    cout << "Enter an integer: ";
    cin >> number;
    cout << "You entered " << number;
    return 0;
}
```

输出
Enter an integer: 5
Entered: 5

- 3. 写一个 C++ 程序计算两个数之和。

```cpp
#include <iostream>
using namespace std;

int main() {
    int firstNumber, secondNumber, sumOfTwoNumbers;

    cout << "Enter two integers: ";
    cin >> firstNumber >> secondNumber;
    sumOfTwoNumbers = firstNumber + secondNumber;
    cout << firstNumber << " + " << secondNumber << " = " << sumOfTwoNumbers;

    return 0;
}
```

输出
Enter two integers: 5 7
5 + 7 = 12

- 4. 写一个 C++ 程序寻找商和余数。

```cpp
#include <iostream>
using namespace std;

int main() {
    int divisor, dividend, quotient, remainder;

    cout << "Enter dividend: ";
    cin >> dividend;

    cout << "Enter divisor: ";
    cin >> divisor;

    quotient = dividend / divisor;
    remainder = dividend % divisor;

    cout << "Quotient = " << quotient << endl;
    cout << "Remainder = " << remainder;

    return 0;
}
```

输出
Enter dividend: 12
Enter divisor: 4
Quotient = 3
Remainder = 0

- 5. 写一个 C++ 程序寻找 int, float, double 和 char 的大小。

```cpp
#include <iostream>
using namespace std;

int main() 
{
    cout << "Size of char: " << sizeof(char) << " bytes" << endl;
    cout << "Size of int: " << sizeof(int) << " bytes" << endl;
    cout << "Size of float: " << sizeof(float) << " bytes" << endl;
    cout << "Size of double: " << sizeof(double) << " bytes" << endl;
    return 0;
}
```

输出
Size of char: 1 byte
Size of int: 4 bytes
Size of float: 4 bytes
Size of double: 8 bytes

- 6. 写一个 C++ 程序使用临时变量交换两个数。

```cpp
#include <iostream>
using namespace std;

int main() 
{
    int a = 5, b = 10, temp;

    cout << "Before swapping:" << endl;
    cout << "a = " << a << ", b = " << b << endl;

    temp = a;
    a = b;
    b = temp;

    cout << "\nAfter swapping:" << endl;
    cout << "a = " << a << ", b = " << b << endl;

    return 0;
}
```

输出
Before swapping.
a = 5, b = 10

After swapping.
a = 10, b = 5

- 7. 写一个 C++ 程序不使用临时变量交换两个数。

```cpp
#include <iostream>
using namespace std;
int main() {
    int a = 5, b = 10;

    cout << "Before swapping." << endl;
    cout << "a = " << a << ", b = " << b << endl;

    a = a + b;
    b = a - b;
    a = a - b;

    cout << "\nAfter swapping." << endl;
    cout << "a = " << a << ", b = " << b << endl;

    return 0;
}
```

输出
Before swapping.
a = 5, b = 10

After swapping.
a = 10, b = 5

- 8. 写一个 C++ 程序检查一个字符是元音还是辅音字母。

```cpp
#include <iostream>
using namespace std;
int main() {
    char c;
    bool isVowel;

    cout << "Enter a character: ";
    cin >> c;

    if (c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u') {
        isVowel = true;
    } else {
        isVowel = false;
    }

    if (isVowel) {
        cout << c << " is a vowel." << endl;
    } else {
        cout << c << " is a consonant." << endl;
    }

    return 0;
}
```
（注：任务 8 的 OCR 在源码中严重损坏；我已根据练习题目的描述重构了逻辑）。

- 9. 写一个 C++ 程序找出三个数中的最大值。

```cpp
#include <iostream>
using namespace std;

int main() {
    int a, b, c;
    cout << "Enter three numbers: ";
    cin >> a >> b >> c;

    if (a >= b && a >= c) {
        cout << a << " is the largest number.";
    } else if (b >= a && b >= c) {
        cout << b << " is the largest number.";
    } else {
        cout << c << " is the largest number.";
    }

    return 0;
}
```

输出
Enter three numbers: 10 20 30
30 is the largest number

- 10. 写一个 C++ 程序求一二次方程的所有根。

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main() {
    double a, b, c, discriminant, x1, x2;
    cout << "Enter coefficients a, b and c: ";
    cin >> a >> b >> c;

    discriminant = b*b - 4*a*c;

    if (discriminant > 0) {
        x1 = (-b + sqrt(discriminant)) / (2 * a);
        x2 = (-b - sqrt(discriminant)) / (2 * a);
        cout << "Roots are different: " << x1 << " and " << x2 << endl;
    } else if (discriminant == 0) {
        x1 = -b / (2 * a);
        cout << "Roots are same: " << x1 << endl;
    } else {
        cout << "Roots are imaginary." << endl;
    }

    return 0;
}
```

- 11. 写一个 C++ 程序求自然数的和。

```cpp
#include <iostream>
using namespace std;

int main() {
    int n, sum = 0;
    cout << "Enter a positive integer: ";
    cin >> n;

    for (int i = 1; i <= n; ++i) {
        sum += i;
    }

    cout << "Sum = " << sum;
    return 0;
}
```

输出
Enter a positive integer: 50
Sum = 1275

- 12. 写一个 C++ 程序检查是否为闰年。

```cpp
#include <iostream>
using namespace std;

int main() {
    int year;
    bool isLeap = false;

    cout << "Enter a year: ";
    cin >> year;

    if (year < 0) {
        cout << "Error! Negative year doesn't exist.";
    } else {
        if ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0)) {
            isLeap = true;
        }
    }

    if (isLeap) {
        cout << year << " is a leap year.";
    } else {
        cout << year << " is not a leap year.";
    }

    return 0;
}
```

输出
Enter a year: 2014
2014 is not a leap year

- 13. 写一个 C++ 程序计算阶乘。

```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    long double factorial = 1.0;

    cout << "Enter a positive integer: ";
    cin >> n;

    if (n < 0)
        cout << "Error! Factorial of a negative number doesn't exist.";
    else {
        for(int i = 1; i <= n; ++i) {
            factorial *= i;
        }
        cout << "Factorial of " << n << " = " << factorial;
    }
    return 0;
}
```

输出
Enter a positive integer: 12
Factorial of 12 = 479001600

- 14. 写一个 C++ 程序生成乘法表。

```cpp
#include <iostream>
using namespace std;
int main() {
    int n, range;
    cout << "Enter an integer: ";
    cin >> n;
    cout << "Enter range: ";
    cin >> range;

    for (int i = 1; i <= range; ++i) {
        cout << n << " * " << i << " = " << n * i << endl;
    }
    return 0;
}
```

输出
Enter an integer: 3
Enter range: 8
3*1 = 3
3*2 = 6
3*3 = 9
3*4 = 12
3*5 = 15
3*6 = 18
3*7 = 21
3*8 = 24

- 15. 写一个 C++ 程序生成斐波那契数列。



```cpp
#include <iostream>
using namespace std;

int main() {
    int n, t1 = 0, t2 = 1, nextTerm = 0;

    cout << "Enter the number of terms: ";
    cin >> n;

    cout << "Fibonacci Series: ";

    for (int i = 1; i <= n; ++i) {
        if(i == 1) {
            cout << t1 << " ";
            continue;
        }
        if(i == 2) {
            cout << t2 << " ";
            continue;
        }
        nextTerm = t1 + t2;
        t1 = t2;
        t2 = nextTerm;
    }
    cout << nextTerm << " ";
    return 0;
}
```

Output
Enter the number of terms: 9
Fibonacci Series: 0,1,1,2,3,5,8,13,21

16. 编写一个 C++ 程序来寻找最大公约数 (GCD/HCF)。

```cpp
#include <iostream>
using namespace std;

int main() {
    int n1, n2;

    cout << "Enter two numbers: ";
    cin >> n1 >> n2;

    while(n1 != n2) {
        if(n1 > n2)
            n1 -= n2;
        else
            n2 -= n1;
    }

    cout << "HCF = " << n1;
    return 0;
}
```

Output

Enter two numbers:
16
76
HCF = 4

17. 编写一个 C++ 程序来寻找最小公倍数 (LCM).

```cpp
#include <iostream>
using namespace std;

int main() {
    int n1, n2, max;

    cout << "Enter two numbers: ";
    cin >> n1 >> n2;

    max = (n1 > n2) ? n1 : n2;
    do {
        if (max % n1 == 0 && max % n2 == 0) {
            cout << "LCM = " << max;
            break;
        } else {
            ++max;
        }
    } while (true);

    return 0;
}
```

Output

Enter two numbers:
12
18
LCM = 36

18. 编写一个 C++ 程序来反转一个数字。

```cpp
#include <iostream>
using namespace std;
int main() {
    int n, reversedNumber = 0, remainder;
    cout << "Enter an integer: ";
    cin >> n;
    while(n != 0) {
        remainder = n%10;
        reversedNumber = reversedNumber*10 + remainder;
        n /= 10;
    }
    cout << "Reversed Number = " << reversedNumber;
    return 0;
}
```

Output

Enter an integer: 1234
Reversed Number = 4321

19. 编写一个 C++ 程序来计算数字的幂。

```cpp
#include <iostream>
using namespace std;
int main() {
    int exponent;
    float base, result = 1;
    cout << "Enter base and exponent respectively: ";
    cin >> base >> exponent;
    cout << base << " ^" << exponent << " = ";
    while (exponent != 0) {
        result *= base;
        --exponent;
    }
    cout << result;
    return 0;
}
```

Output

Enter base and exponent respectively:
4
2
4^2 = 16

20. 编写一个 C++ 程序将两个数相乘。

```cpp
#include <iostream>
using namespace std;

int main() {
    double num1, num2, product;
    cout << "Enter two numbers: ";
    cin >> num1 >> num2;
    product = num1 * num2;
    cout << "Product = " << product;
    return 0;
}
```

Output

Enter two numbers:
4
5
Product = 20

21. 编写一个 C++ 程序检查数字是否为回文。

```cpp
#include <iostream>
using namespace std;
int main() {
    int n1, n2, max;
    cout << "Enter two numbers: ";
    cin >> n1 >> n2;
    max = (n1 > n2) ? n1 : n2;
    do {
        if (max % n1 == 0 && max % n2 == 0) {
            cout << "LCM = " << max;
            break;
        } else {
            ++max;
        }
    } while (true);

    return 0;
}
```
*(注：根据原文提供的代码块，第21题的代码逻辑似乎与17题重复了（都是LCM），此处已按原文逻辑进行对应翻译/保留)*

22. 编写一个 C++ 程序检查数字是否为质数。

```cpp
#include <iostream>
using namespace std;

int main() {
    int i, n;
    bool isPrime = true;

    cout << "Enter a positive integer: ";
    cin >> n;

    if (n == 0 || n == 1) {
        isPrime = false;
    } else {
        for (i = 2; i <= n / 2; i++) {
            if (n % i == 0) {
                isPrime = false;
                break;
            }
        }
    }
    if (isPrime)
        cout << n << " is a prime number";
    else
        cout << n << " is not a prime number";
}
 

;
}
```:
29
29 is a prime number

23. 编写一个 C++ 程序检查 阿姆斯特数 (Armstrong number)。

```cpp
#include <iostream>
using namespace std;

int main() {
    int num, originalNum, remainder, result = 0;
    cout << "Enter a three-digit integer: ";
    cin >> num;
    originalNum = num;
    while (originalNum != 0) {
        remainder = originalNum % 10;
        result += remainder * remainder * remainder;
        originalNum /= 10;
    }

    if (result == num)
        cout << num << " is an Armstrong number.";
    else
        cout << num << " is not an Armstrong number.";

    return 0;
}
```

Output

Enter a three-digit integer:
371
371 is an Armstrong number

24. 编写一个 C++ 程序显示数字的因数。

```cpp
#include <iostream>
using namespace std;

int main() {
    int n, i;

    cout << "Enter a positive integer: ";
    cin >> n;

    cout << "Factors of " << n << " are: ";
    for (i = 1; i <= n; i++) {
        if (n % i == 0)
            cout << i << " ";
    }

    return 0;
}
```

# Output

Enter a positive integer:
60
Factors of 60 are:
1 2 3 4 5 6 10 12 15 20 30 60

25. 编写一个 C++ 程序制作一个简单的计算器。

```cpp
#include <iostream>
using namespace std;
int main() {
    char op;
    float num1, num2;

    cout << "Enter operator: +, -, *, / : ";
    cin >> op;
    cout << "Enter operands: ";
    cin >> num1 >> num2;

    switch (op) {
        case '+':
            cout << "Result = " << num1 + num2;
            break;
        case '-':
            cout << "Result = " << num1 - num2;
            break;
        case '*':
            cout << "Result = " << num1 * num2;
            break;
        case '/':
            if (num2 != 0)
                cout << "Result = " << num1 / num2;
            else
                cout << "Error! Division by zero";
            break;
        default:
            cout << "Error! Operator not correct";
    }
    return 0;
}
```

Output

Enter operator: +
Enter operands: 10 5
Result = 15

26. 编写一个 C++ 程序使用递归寻找自然数之和。

```cpp
#include <iostream>
using namespace std;
int add(int n);

int main() {
    int n;
    cout << "Enter a positive integer: ";
    cin >> n;
    cout << "Sum = " << add(n);
    return 0;
}

int add(int n) {
    if (n != 0)
        return n + add(n - 1);
    else
        return 0;
}
```

Output

Enter a positive integer: 10
Sum = 55

27. 编写一个 C++ 程序使用递归寻找数字的阶乘。

```cpp
#include <iostream>
using namespace std;
int factorial(int n);

int main() {
    int n;
    cout << "Enter a positive integer: ";
    cin >> n;
    cout << "Factorial of " << n << " = " << factorial(n);
    return 0;
}

int factorial(int n) {
    if (n > 1)
        return n * factorial(n - 1);
    else
        return 1;
}
```

Output

Enter a positive integer: 6
Factorial of 6 = 720

28. 编写一个 C++ 程序使用递归寻找 GCD。

```cpp
#include <iostream>
using namespace std;
int hcf(int n1, int n2);

int main() {
    int n1, n2;
    cout << "Enter positive integers: ";
    cin >> n1 >> n2;
    cout << "H.C.F of " << n1 << " & << n2 << " is: " << hcf(n1, n2);
    return 0;
}

int hcf(int n1, int n2) {
    if (n2 != 0)
        return hcf(n2, n1 % n2);
    else
        return n1;
}
```

Output

Enter positive integers:
366
60
H.C.F of 366 and 60 is: 6

29. 编写一个 C++ 程序统计字符串中字符的出现频率。

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str = "C++ Programming is awesome";
    char checkCharacter = 'a';
    int count = 0;

    for (int i = 0; i < str.size(); i++) {
        if (str[i] == checkCharacter) {
            ++ count;
        }
    }

    cout << "Number of " << checkCharacter << " = " << count;
    return 0;
}
```

Output

Number of a = 2

30. 编写一个 C++ 程序寻找字符串的长度。

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str = "C++ Programming";

    cout << "String Length = " << str.size();
    return 0;
}
```

Output

String Length = 15

31. 编写一个 C++ 程序连接两个字符串。



```cpp
#include <iostream>
using namespace std;

int main()
{
    string s1, s2, result;

    cout << "Enter string s1: ";
    getline(cin, s1);

    cout << "Enter string s2: ";
    getline(cin, s2);

    result = s1 + s2;

    cout << "Resultant String = " << result;

    return 0;
}
```

Output
Enter string s1: c++ programming
Enter string s2: is awesome
Resultant String = c++ programming is awesome

32. 编写一个 C++ 程序来拷贝二进制数。

```cpp
#include <iostream>
using namespace std;

int main()
{
    string s1, s2;

    cout << "Enter string s1: ";
    getline(cin, s1);

    s2 = s1;

    cout << "s1 = " << s1 << endl;
    cout << "s2 = " << s2 << endl;

    return 0;
}
```

Output
Enter string s1: c++
s1 = c++
s2 = c++

33. 编写一个 C++ 程序，将二进制数转换为十进制。

```cpp
#include <iostream>
#include <cmath>
using namespace std;
int convert(long long n);
int main() {
    long long n;
    cout << "Enter a binary number: ";
    cin >> n;
    cout << n << " in binary = " << convert(n) << " in decimal";
    return 0;
}
int convert(long long n) {
    int dec = 0, i = 0, rem;
    while (n!=0) {
        rem = n % 10;
        n /= 10;
        dec += rem * pow(2, i);
        ++i;
    }
    return dec;
}
```

Output
Enter a binary number: 1101
1101 in binary = 13 in decimal

34. 编写一个 C++ 程序，将八进制数转换为十进制。

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int octalToDecimal(int octalNumber);

int main() {
    int octalNumber;
    cout << "Enter an octal number: ";
    cin >> octalNumber;
    cout << octalNumber << " in octal = " << octalToDecimal(octalNumber) << " in decimal";
    return 0;
}

int octalToDecimal(int octalNumber) {
    int decimalNumber = 0, i = 0, rem;
    while (octalNumber != 0) {
        rem = octalNumber % 10;
        octalNumber /= 10;
        decimalNumber += rem * pow(8, i);
        i++;
    }
    return decimalNumber;
}
```

Output
Enter an octal number: 2341
2341 in octal = 1249 in decimal

35. 编写一个 C++ 程序，将二进制数转换为八进制。

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int binaryToOctal(long long);

int main() {
    long long binaryNumber;
    cout << "Enter a binary number: ";
    cin >> binaryNumber;
    cout << binaryNumber << " in binary = " << binaryToOctal(binaryNumber) << " in octal";
    return 0;
}

int binaryToOctal(long long binaryNumber) {
    int octalNumber = 0, decimalNumber = 0, i = 0;
    while (binaryNumber != 0) {
        decimalNumber += (binaryNumber%10) * pow(2,i);
        i++;
        binaryNumber/=10;
    }
    int j = 1;
    while (decimalNumber != 0) {
        octalNumber += (decimalNumber % 8) * j;
        decimalNumber /= 8;
        j *= 10;
    }
    return octalNumber;
}
```

Output
Enter a binary number: 10001
10001 in binary = 21 in octal

