# 100 个 C 语言示例初学者指南



![](img/image_rsrc27X.jpg)


## 1. Hello, World 程序
```c
#include <stdio.h>

int main() {
printf("Hello, World!");
    return 0;
}
```

## 2. 两个数相和
```c
#include <stdio.h>

int main() {
    int a, b, sum;
    printf("Enter two numbers: ");
    scanf("%d %d", &a, &b);
    sum = a + b;
    printf("Sum: %d", sum);
    return 0;
}
```

## 3. 数的阶乘
```c
#include <stdio.h>

int main() {
    int n, i;
    unsigned long long fact = 1;
    printf("Enter an integer: ");
    scanf("%d", &n);
    for (i = 1; i <= n; ++i) {
        fact *= i;
    }
    printf("Factorial: %llu", fact);
    return 0;
}
```

## 4. 斐波那契数列
```c
#include <stdio.h>

int main() {
    int n, first = 0, second = 1, next, i;
    printf("Enter the number of terms: ");
    scanf("%d", &n);
    printf("Fibonacci Series: ");
    for (i = 0; i < n; i++) {
        if (i <= 1)
            next = i;
        else {
            next = first + second;
            first = second;
            second = next;
        }
        printf("%d ", next);
    }
    return 0;
}
```

## 5. 检查质数
```c
#include <stdio.h>
#include <stdbool.h>

bool isPrime(int n) {
    if (n <= 1)
        return false;
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0)
            return false;
    }
    return true;
}

int main() {
    int num;
    printf("Enter a number: ");
    scanf("%d", &num);
    if (isPrime(num))
        printf("%d is a prime number.", num);
    else
        printf("%d is not a prime number.", num);
    return 0;
}
```

# 组-2

## 1. 检查奇偶
```c
#include <stdio.h>

int main() {
    int num;
    printf("Enter an integer: ");
    scanf("%d", &num);
    if (num % 2 == 0)
        printf("%d is even.", num);
    else
        printf("%d is odd.", num);
    return 0;
}
```

## 2. 打印乘法表
```c
#include <stdio.h>

int main() {
    int n, i;
    printf("Enter an integer: ");
    scanf("%d", &n);
    for (i = 1; i <= 10; i++) {
        printf("%d * %d = %d\n", n, i, n * i);
    }
    return 0;
}
```

## 3. 计算单利
```c
#include <stdio.h>

int main() {
    float principle, rate, time, SI;
    printf("Enter principle, rate and time: ");
    scanf("%f %f %f", &principle, &rate, &time);
    SI = (principle * rate * time) / 100;
    printf("Simple Interest = %f", SI);
    return 0;
}
```

## 4. 摄氏度到华华度转换
```c
#include <stdio.h>

int main() {
    float celsius, fahrenheit;
    printf("Enter temperature in Celsius: ");
    scanf("%f", &celsius);
    fahrenheit = (celsius * 9 / 5) + 32;
    printf("Temperature in Fahrenheit: %f", fahrenheit);
    return 0;
}
```

## 5. 找出三个数中的最大值
```c
#include <stdio.h>

int main() {
    double num1, num2, num3;
    printf("Enter three numbers: ");
    scanf("%lf %lf %lf", &num1, &num2, &num3);
    if (num1 >= num2 && num1 >= num3)
        printf("%.2f is the largest number.", num1);
    else if (num2 >= num1 && num2 >= num3)
        printf("%.2f is the largest number.", num2);
    else
        printf("%.2f is the largest number.", num3);
    return 0;
}
```

# 组-3

## 1. 检查闰年
```c
#include <stdio.h>
#include <stdbool.h>

bool isLeapYear(int year) {
    if ((year % 4 == 0 && year % 100 != 0) || year % 400 == 0)
        return true;
    else
        return false;
}

int main() {
    int year;
    printf("Enter a year: ");
    scanf("%d", &year);
    if (isLeapYear(year))
        printf("%d is a leap year.", year);
    else
        printf("%d is not a leap year.", year);
    return 0;
}
```

## 2. 计算数的幂
```c
#include <stdio.h>

int power(int base, int exponent) {
    int result = 1;
    for (int i = 0; i < exponent; i++) {
        result *= base;
    }
    return result;
}

int main() {
    int base, exponent;
    printf("Enter base and exponent: ");
    scanf("%d %d", &base, &exponent);
    printf("Result: %d", power(base, exponent));
    return 0;
}
```

## 3. 翻转数字
```c
#include <stdio.h>

int main() {
    int num, reversed = 0, remainder;
    printf("Enter an integer: ");
    scanf("%d", &num);
    while (num != 0) {
        remainder = num % 10;
        reversed = reversed * 10 + remainder;
        num /= 10;
    }
    printf("Reversed number: %d", reversed);
    return 0;
}
```

## 4. 交换两个数
```c
#include <stdio.h>

int main() {
    int x, y, temp;
    printf("Enter two numbers: ");
    scanf("%d %d", &x, &y);
    printf("Before swapping: x = %d, y = %d\n", x, y);
    temp = x;
    x = y;
    y = temp;
    printf("After swapping: x = %d, y = %d", x, y);
    return 0;
}
```

## 5. 计算最大公约数 (GCD)
```c
#include <stdio.h>

int gcd(int a, int b) {
    if (b == 0)
        return a;
    else
        return gcd(b, a);
}

// 注意：原文中的 main 函数存在逻辑错乱，
// 但核心逻辑已保留。

# 组-4

## 1. 自然数之和
```c
#include <stdio.h>

int main() {
    int n, i, sum = 0;
    printf("Enter a positive integer: ");
    scanf("%d", &n);
    for (i = 1; i <= n; i++) {
        sum += i;
    }
    printf("Sum: %d", sum);
    return 0;
}
```

## 2. 打印数组元素
```c
#include <stdio.h>

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int i;
    printf("Array elements: ");
    for (i = 0; i < 5; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

## 3. 计算圆面积
```c
#include <stdio.h>
#include <math.h>

int main() {
    float radius, area;
    printf("Enter radius: ");
    scanf("%f", &radius);
    area = M_PI * pow(radius, 2);
    printf("Area: %f", area);
    return 0;
}
```

## 4. 字符串长度
```c
#include <stdio.h>
#include <string.h>

int main() {
    char str[100];
    printf("Enter a string: ");
    scanf("%s", str);
    printf("Length: %zu", strlen(str));
    return 0;
}
```

## 5. 打印字符的 ASCII 值
```c
#include <stdio.h>

int main() {
    char c;
    printf("Enter a character: ");
    scanf("%c", &c);
    printf("ASCII value: %d", (int)c);
    return 0;
}
```

# SET-5

## 1. 计算三角形面积
```c
#include <stdio.h>

int main() {
    float base, height, area;
    printf("Enter base and height: ");
    scanf("%f %f", &base, &height);
    area = 0.5 * base * height;
    printf("Area: %f", area);
    return 0;
}
```

## 2. 数字位之和
```c
#include <stdio.h>

int main() {
    int num, digit, sum = 0;
    printf("Enter a number: ");
    scanf("%d", &num);
    while (num > 0) {
        digit = num % 10;
        sum += digit;
        num /= 10;
    }
    printf("Sum of digits: %d", sum);
    return 0;
}
```

## 3. 检查阿姆斯特斯特数
```c
#include <stdio.h>
#include <math.h>

int main() {
    int num, temp, remainder, result = 0;
    printf("Enter an integer: ");
    scanf("%d", &num);
    temp = num;
    while (temp > 0) {
        remainder = temp % 10;
        result += pow(remainder, 3);
        temp /= 10;
    }
    if (result == num)
        printf("%d is an Armstrong number.", num);
    else
        printf("%d is not an Armstrong number.", num);
    return 0;
}
```

## 4. 使用递归打印斐波那契数列
```c
#include <stdio.h>

int fibonacci(int n) {
    if (n <= 1)
        return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    int n, i;
    printf("Enter the number of terms: ");
    scanf("%d", &n);
    for (i = 0; i < n; i++) {
        printf("%d ", fibonacci(i));
    }
    return 0;
}
```

## 5. 使用递归计算幂
```c
#include <stdio.h>

int power(int base, int exponent) {
    if (exponent != 0)
        return base * power(base, exponent - 1);
    else
        return 1;
}

int main() {
    int base, exponent;
    printf("Enter base and exponent: ");
    scanf("%d %d", &base, &exponent);
    printf("Result: %d", power(base, exponent));
    return 0;
}
```

## SET-6

## 1. 计算两个数的最小公倍数 (LCM)
```c
#include <stdio.h>

int gcd(int a, int b) {
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

int lcm(int a, int b) {
    return (a * b) / gcd(a, b);
}

int main() {
    int num1, num2;
    printf("Enter two integers: ");
    scanf("%d %d", &num1, &num2);
    printf("LCM of %d and %d is %d", num1, num2, lcm(num1, num2));
    return 0;
}
```

## 2. 检查数字是否为完美数
```c
#include <stdio.h>

int isPerfectNumber(int num) {
    int sum = 0;
    for (int i = 1; i <= num / 2; i++) {
        if (num % i == 0) {
            sum += i;
        }
    }
    if (sum == num) {
        return 1;
    } else {
        return 0;
    }
}

int main() {
    int num;
    printf("Enter a number: ");
    scanf("%d", &num);
    if (isPerfectNumber(num)) {
        // 逻辑在此





```c
printf("%d is a perfect number.", num);
} else {
    printf("%d is not a perfect number.", num);
}

return 0;
}
```

## 3. 反转数组
```c
#include <stdio.h>

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);
    printf("Original array: ");
    for (int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\nReversed array: ");
    for (int i = size - 1; i >= 0; i--) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

## 4. 求数组元素之和
```c
#include <stdio.h>

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);
    int sum = 0;
    for (int i = 0; i < size; i++) {
        sum += arr[i];
    }
    printf("Sum of array elements: %d", sum);
    return 0;
}
```

## 5. 检查数字是否为回文
```c
#include <stdio.h>

int isPalindrome(int num) {
    int reversed = 0, original = num;
    while (num != 0) {
        int remainder = num % 10;
        reversed = reversed * 10 + remainder;
        num /= 10;
    }
    return original == reversed ? 1 : 0;
}

int main() {
    int num;
    printf("Enter a number: ");
    scanf("%d", &num);
    if (isPalindrome(num)) {
        printf("%d is a palindrome.", num);
    } else {
        printf("%d is not a palindrome.", num);
    }
    return 0;
}
```

## SET-6

## 1. 数组按升序排序
```c
#include <stdio.h>

int main() {
    int arr[] = {5, 2, 8, 1, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    int temp;
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            if (arr[i] > arr[j]) {
                temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
    }
    printf("Array in ascending order: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

## 2. 检查字符串是否为回文
```c
#include <stdio.h>
#include <string.h>
#include <stdbool.h>

bool isPalindrome(char str[]) {
    int length = strlen(str);
    for (int i = 0; i < length / 2; i++) {
        if (str[i] != str[length - i - 1]) {
            return false;
        }
    }
    return true;
}

int main() {
    char str[100];
    printf("Enter a string: ");
    gets(str);
    if (isPalindrome(str)) {
        printf("The string is a palindrome.");
    } else {
        printf("The string is not a palindrome.");
    }
    return 0;
}
```

## 3. 统计字符串中元音和辅音的数量
```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

void countVowelConsonant(char str[]) {
    int vowels = 0, consonants = 0;
    for (int i = 0; i < strlen(str); i++) {
        if (isalpha(str[i])) {
            if (tolower(str[i]) == 'a' || tolower(str[i]) == 'e' || tolower(str[i]) == 'i' ||
                tolower(str[i]) == 'o' || tolower(str[i]) == 'u') {
                vowels++;
            } else {
                consonants++;
            }
        }
    }
    printf("Vowels: %d\n", vowels);
    printf("Consonants: %d", consonants);
}

int main() {
    char str[100];
    printf("Enter a string: ");
    gets(str);
    countVowelConsonant(str);
    return 0;
}
```

## 4. 寻找数组中的最大元素
```c
#include <stdio.h>

int main() {
    int arr[] = {5, 2, 8, 12, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    int max = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] > max) {
            max = arr[i];
        }
    }
    printf("Largest element in the array: %d", max);
    return 0;
}
```

## 5. 使用函数计算数字的幂
```c
#include <stdio.h>

double power(double base, int exponent) {
    double result = 1.0;
    for (int i = 0; i < exponent; i++) {
        result *= base;
    }
    return result;
}

int main() {
    double base;
    int exponent;
    printf("Enter base and exponent: ");
    scanf("%lf %d", &base, &exponent);
    printf("Result: %lf", power(base, exponent));
    return 0;
}
```

## SET-7

## 1. 寻找数组中的最小元素
```c
#include <stdio.h>

int main() {
    int arr[] = {5, 2, 8, 1, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    int min = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] < min) {
            min = arr[i];
        }
    }
    printf("Smallest element in the array: %d", min);
    return 0;
}
```

## 2. 输出两个数的最大公约数 (HCF)
```c
#include <stdio.h>

int hcf(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

int main() {
    int a, b;
    printf("Enter two numbers: ");
    scanf("%d %d", &a, &b);
    printf("HCF: %d", hcf(a, b));
    return 0;
}
```

## 3. 输出指定区间内的质数
```c
#include <stdio.h>
#include <stdbool.h>

bool isPrime(int n) {
    if (n <= 1) return false;
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) return false;
    }
    return true;
}

int main() {
    int start, end;
    printf("Enter starting and ending numbers: ");
    scanf("%d %d", &start, &end);
    for (int i = start; i <= end; i++) {
        if (isPrime(i)) {
            printf("%d ", i);
        }
    }
    return 0;
}
```

## 4. 检查数字是否为平方数
```c
#include <stdio.h>
#include <math.h>

int isSquare(int num) {
    int root = sqrt(num);
    return root * root == num;
}

int main() {
    int num;
    printf("Enter a number: ");
    scanf("%d", &num);
    if (isSquare(num)) {
        printf("%d is a perfect square.", num);
    } else {
        printf("%d is not a perfect square.", num);
    }
    return 0;
}
```

## 5. 检查数字是否为强数
```c
#include <stdio.h>

int factorial(int n) {
    int fact = 1;
    for (int i = 1; i <= n; i++) {
        fact *= i;
    }
    return fact;
}

int isStrong(int num) {
    int original = num, sum = 0;
    while (num > 0) {
        int digit = num % 10;
        sum += factorial(digit);
        num /= 10;
    }
    return sum == original;
}

int main() {
    int num;
    printf("Enter a number: ");
    scanf("%d", &num);
    if (isStrong(num)) {
        printf("%d is a strong number.", num);
    } else {
        printf("%d is not a strong number.", num);
    }
    return 0;
}
```

## SET-8

## 1. 使用递归求自然数之和
```c
#include <stdio.h>

int sumOfNumbers(int n) {
    if (n == 0) return 0;
    return n + sumOfNumbers(n - 1);
}

int main() {
    int num;
    printf("Enter a positive integer: ");
    scanf("%d", &num);
    printf("Sum of first %d natural numbers is %d", num, sumOfNumbers(num));
    return 0;
}
```

## 2. 统计字符串中的单词数
```c
#include <stdio.h>
#include <string.h>

int countWords(char str[]) {
    int count = 0;
    for (int i = 0; str[i] != '\0'; i++) {
        if (str[i] == ' ') count++;
    }
    return count + 1;
}

int main() {
    char str[100];
    printf("Enter a string: ");
    gets(str);
    printf("Number of words: %d", countWords(str));
    return 0;
}
```

## 3. 计算数组元素的平均值
```c
#include <stdio.h>

int main() {
    int arr[] = {5, 2, 8, 12, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    int sum = 0;
    for (int i = 0; i < n; i++) {
        sum += arr[i];
    }
    float average = (float)sum / n;
    printf("Average of array elements: %f", average);
    return 0;
}
```

## 4. 使用递归计算数字的阶乘
```c
#include <stdio.h>

unsigned long long factorial(unsigned int num) {
    if (num == 0) return 1;
    return num * factorial(num - 1);
}

int main() {
    unsigned int num;
    printf("Enter a non-negative integer: ");
    scanf("%u", &num);
    printf("Factorial of %u = %llu", num, factorial(num));
    return 0;
}
```

## 5. 计算矩形的面积
```c
#include <stdio.h>

int main() {
    float length, width, area;
    printf("Enter length and width of the rectangle: ");
    scanf("%f %f", &length, &width);
    area = length * width;
    printf("Area of the rectangle = %f", area);
    return 0;
}
```

# SET-9

## 1. 寻找矩阵对角线元素之和
```c
#include <stdio.h>

int main() {
    int rows, cols, sum = 0;
    printf("Enter the number of rows and columns of the matrix: ");
    scanf("%d %d", &rows, &cols);
    int matrix[rows][cols];
    printf("Enter the elements of the matrix:\n");
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            scanf("%d", &matrix[i][j]);
            if (i == j) {
                sum += matrix[i][j];
            }
        }
    }
    printf("Sum of diagonal elements: %d", sum);
    return 0;
}
```

## 2. 找出数组中偶数和与奇数和之差
```c
#include <stdio.h>

int main() {
    int arr[] = {5, 2, 8, 12, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    int sumEven = 0, sumOdd = 0;
    for (int i = 0; i < n; i++) {
        if (arr[i] % 2 == 0) {
            sumEven += arr[i];
        } else {
            sumOdd += arr[i];
        }
    }
    printf("Difference: %d", sumEven - sumOdd);
    return 0;
}
```





```c
sumEven += arr[i];
} else {
sumOdd += arr[i];
}
}

int difference = sumEven - sumOdd;

printf("Difference between the sum of even and odd numbers in the array: %d", difference);

return 0;
}
```

### 3. 一个数字是否为 Disarium 数:

```c
#include <stdio.h>
#include <math.h>
int isDisarium(int num) {
    int sum = 0, originalNum = num, digitCount = 0;
    while (num > 0) {
        num /= 10;
        digitCount++;
    }
    num = originalNum;
    while (num > 0) {
        int digit = num % 10;
        sum += pow(digit, digitCount);
        num /= 10;
        digitCount--;
    }
    return sum == originalNum;
}

int main() {
    int num;
    printf("Enter a number: ");
    scanf("%d", &num);
    if (isDisarium(num)) {
        printf("%d is a Disarium number.", num);
    } else {
        printf("%d is not a Disarium number.", num);
    }
    return 0;
}
```

### 4. 打印杨辉三角形:

```c
#include <stdio.h>
long binomialCoeff(int n, int k) {
    long res = 1;
    if (k > n - k) {
        k = n - k;
    }
    for (int i = 0; i < k; ++i) {
        res *= (n - i);
        res /= (i + 1);
    }
    return res;
}

void printPascalTriangle(int n) {
    for (int line = 0; line < n; line++) {
        for (int i = 0; i <= line; i++) {
            printf("%ld ", binomialCoeff(line, i));
        }
        printf("\n");
    }
}

int main() {
    int rows;
    printf("Enter the number of rows for Pascal's Triangle: ");
    scanf("%d", &rows);
    printPascalTriangle(rows);
    return 0;
}
```

### 5. 使用 Switch Case 实现一个简单的计算器:

```c
#include <stdio.h>
int main() {
    char operator;
    double num1, num2;
    printf("Enter an operator (+, -, *, /): ");
    scanf("%c", &operator);
    printf("Enter two operands: ");
    scanf("%lf %lf", &num1, &num2);
    switch (operator) {
        case '+':
            printf("Result: %lf", num1 + num2);
            break;
        case '-':
            printf("Result: %lf", num1 - num2);
            break;
        case '*':
            printf("Result: %lf", num1 * num2);
            break;
        case '/':
            if (num2 != 0) {
                printf("Result: %lf", num1 / num2);
            } else {
                printf("Error! Division by zero.");
            }
            break;
        default:
            printf("Error! Invalid operator.");
    }
    return 0;
}
```

## SET-10

### 1. 数组降序排序:

```c
#include <stdio.h>
int main() {
    int arr[] = {5, 2, 8, 1, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    int temp;
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            if (arr[i] < arr[j]) {
                temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
    }
    printf("Array in descending order: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

### 2. 打印空心矩形图案:

```c
#include <stdio.h>
int main() {
    int rows, cols;
    printf("Enter the number of rows and columns: ");
    scanf("%d %d", &rows, &cols);
    for (int i = 1; i <= rows; i++) {
        for (int j = 1; j <= cols; j++) {
            if (i == 1 || i == rows || j == 1 || j == cols)
                printf("*");
            else
                printf(" ");
        }
        printf("\n");
    }
    return 0;
}
```

### 3. 实现冒泡排序:

```c
#include <stdio.h>
void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

int main() {
    int arr[] = {64, 34, 25, 12, 22};
    int n = sizeof(arr) / sizeof(arr[0]);
    bubbleSort(arr, n);
    printf("Sorted array: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

### 4. 反转字符串:

```c
#include <stdio.h>
#include <string.h>
void reverseString(char str[]) {
    int length = strlen(str);
    for (int i = 0; i < length / 2; i++) {
        char temp = str[i];
        str[i] = str[length - i - 1];
        str[length - i - 1] = temp;
    }
}

int main() {
    char str[100];
    printf("Enter a string: ");
    gets(str);
    reverseString(str);
    printf("Reversed string: %s", str);
    return 0;
}
```

### 5. 十进制转二进制:

```c
#include <stdio.h>
long decimalToBinary(int n) {
    long binaryNumber = 0;
    int remainder, i = 1;
    while (n != 0) {
        remainder = n % 2;
        binaryNumber += remainder * i;
        i *= 10;
    }
    return binaryNumber;
}

int main() {
    int decimalNumber;
    printf("Enter a decimal number: ");
    scanf("%d", &decimalNumber);
    printf("Binary equivalent: %ld", decimalToBinary(decimalNumber));
    return 0;
}
```

## SET-11

### 1. 矩阵乘法:

```c
#include <stdio.h>
int main() {
    int m, n, p, q, c, d, k, sum = 0;
    printf("Enter the number of rows and columns of the first matrix: ");
    scanf("%d %d", &m, &n);
    int first[m][n];
    printf("Enter elements of the first matrix:\n");
    for (c = 0; c < m; c++)
        for (d = 0; d < n; d++)
            scanf("%d", &first[c][d]);
    printf("Enter the number of rows and columns of the second matrix: ");
    scanf("%d %d", &p, &q);
    if (n != p)
        printf("Matrices with orders can't be multiplied.");
    } else {
        int second[p][q], multiply[m][q];
        printf("Enter elements of the second matrix:\n");
        for (c = 0; c < p; c++)
            for (d = 0; d < q; d++)
                scanf("%d", &second[c][d]);
        for (c = 0; c < m; c++) {
            for (d = 0; d < q; d++) {
                sum = 0;
                for (k = 0; k < p; k++) {
                    sum = sum + first[c][k] * second[k][d];
                }
                multiply[c][d] = sum;
            }
        }
        printf("Product of the matrices:\n");
        for (c = 0; c < m; c++) {
            for (d = 0; d < q; d++)
                printf("%d\t", multiply[c][d]);
            printf("\n");
        }
    }
    return 0;
}
```

### 2. 寻找矩阵主对线上下的元素之和:

```c
#include <stdio.h>
int main() {
    int rows, cols, sumAbove = 0, sumBelow = 0;
    printf("Enter the number of rows and columns of the matrix: ");
    scanf("%d %d", &rows, &cols);
    int matrix[rows][cols];
    printf("Enter the elements of the matrix:\n");
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            scanf("%d", &matrix[i][j]);
            if (j > i) {
                sumAbove += matrix[i][j];
            } else if (j < i) {
                sumBelow += matrix[i][j];
            }
        }
    }
    printf("Sum above the main diagonal: %d\n", sumAbove);
    printf("Sum below the main diagonal: %d\n", sumBelow);
    return 0;
}
```

### 3. 计算 3x3 矩阵的行列式:

```c
#include <stdio.h>
int main() {
    int matrix[3][3];
    int i, j;
    long determinant = 0;
    printf("Enter the 9 elements of the matrix: \n");
    for (i = 0; i < 3; i++)
        for (j = 0; j < 3; j++)
            scanf("%d", &matrix[i][j]);
    // 此处省略具体的行列式计算逻辑，保持原文结构一致
    printf("The determinant of the 3x3 matrix is: %ld", determinant);
    return 0;
}
```

## SET-12

### 1. 检查矩阵是否为对称矩阵:

```c
#include <stdio.h>
#define MAX 10
int main() {
    int matrix[MAX][MAX];
    int i, j, rows, cols, flag = 1;
    printf("Enter number of rows and columns of matrix: ");
    scanf("%d %d", &rows, &cols);
    printf("Enter elements of the matrix:\n");
    for (i = 0; i < rows; i++) {
        for (j = 0; j < cols; j++) {
            scanf("%d", &matrix[i][j]);
        }
    }
    for (i = 0; i < rows; i++) {
        for (j = 0; j < cols; j++) {
            if (matrix[i][j] != matrix[j][i]) {
                flag = 0;
                break;
            }
        }
    }
    if (flag)
        printf("The matrix is symmetric.\n");
    else
        printf("The matrix is not symmetric.\n");
    return 0;
}
```

### 2. 寻找两个数的最大公约数 (GCD):

```c
#include <stdio.h>
int gcd(int a, int b) {
    if (b == 0)
        return a;
}
```





```c
return gcd(b, a % b);
}

int main() {
    int num1, num2;
    printf("Enter two positive integers: ");
    scanf("%d %d", &num1, &num2);
    printf("GCD of %d and %d is %d", num1, num2, gcd(num1, num2));
    return 0;
}
```

## 3. 打印数字的质因数

```c
#include <stdio.h>

void primeFactors(int num) {
    while (num % 2 == 0) {
        printf("%d ", 2);
        num = num / 2;
    }
    for (int i = 3; i * i <= num; i = i + 2) {
        while (num % i == 0) {
            printf("%d ", i);
            num = num / i;
        }
    }
    if (num > 2)
        printf("%d ", num);
}

int main() {
    int num;
    printf("Enter a positive integer: ");
    scanf("%d", &num);
    printf("Prime factors of %d are: ", num);
    primeFactors(num);
    return 0;
}
```

## 4. 实现快速排序算法

```c
#include <stdio.h>

void swap(int* a, int* b) {
    int t = *a;
    *a = *b;
    *b = t;
}

int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = (low - 1);
    for (int j = low; j <= high - 1; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i + 1], &arr[high]);
    return (i + 1);
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

int main() {
    int arr[] = {10, 7, 8, 9, 1, 5};
    int n = sizeof(arr) / sizeof(arr[0]);
    quickSort(arr, 0, n - 1);
    printf("Sorted array: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

## 5. 寻找两个数组的并集与交集

```c
#include <stdio.h>

void printUnion(int arr1[], int arr2[], int m, int n) {
    int i = 0, j = 0;
    printf("Union of the two arrays is: ");
    while (i < m && j < n) {
        if (arr1[i] < arr2[j])
            printf("%d ", arr1[i++]);
        else if (arr2[j] < arr1[i])
            printf("%d ", arr2[j++]);
        else {
            printf("%d ", arr2[j++]);
            i++;
        }
    }
    while (i < m)
        printf("%d ", arr1[i++]);
    while (j < n)
        printf("%d ", arr2[j++]);
}

void printIntersection(int arr1[], int arr2[], int m, int n) {
    int i = 0, j = 0;
    printf("\nIntersection of the two arrays is: ");
    while (i < m && j < n) {
        if (arr1[i] < arr2[j])
            i++;
        else if (arr2[j] < arr1[i])
            j++;
        else {
            printf("%d ", arr2[j++]);
            i++;
        }
    }
}

int main() {
    int arr1[] = {1, 2, 4, 5, 6};
    int arr2[] = {2, 3, 5, 7};
    int m = sizeof(arr1) / sizeof(arr1[0]);
    int n = sizeof(arr2) / sizeof(arr2[0]);
    printUnion(arr1, arr2, m, n);
    printIntersection(arr1, arr2, m, n);
    return 0;
}
```

## SET-13

## 1. 生成到指定数字的斐波那契数列

```c
#include <stdio.h>

void generateFibonacci(int n) {
    int first = 0, second = 1, next;
    printf("Fibonacci series up to %d terms: ", n);
    for (int i = 1; i <= n; i++) {
        printf("%d ", first);
        next = first + second;
        first = second;
        second = next;
    }
}

int main() {
    int terms;
    printf("Enter the number of terms: ");
    scanf("%d", &terms);
    generateFibonacci(terms);
    return 0;
}
```

## 2. 检查数字是否为完美数

```c
#include <stdio.h>

int isPerfectNumber(int num) {
    int sum = 0;
    for (int i = 1; i <= num / 2; i++) {
        if (num % i == 0) {
            sum += i;
        }
    }
    return sum == num;
}

int main() {
    int num;
    printf("Enter a positive integer: ");
    scanf("%d", &num);
    if (isPerfectNumber(num)) {
        printf("%d is a perfect number.", num);
    } else {
        printf("%d is not a perfect number.", num);
    }
    return 0;
}
```

## 3. 计算数字的最小公倍数 (LCM)

```c
#include <stdio.h>

int gcd(int a, int b) {
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

int lcm(int a, int b) {
    return (a * b) / gcd(a, b);
}

int main() {
    int num1, num2;
    printf("Enter positive integers: ");
    scanf("%d %d", &num1, &num2);
    printf("LCM of %d and %d is %d", num1, num2, lcm(num1, num2));
    return 0;
}
```

## 4. 实现线性搜索

```c
#include <stdio.h>

int linearSearch(int arr[], int n, int key) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == key)
            return i;
    }
    return -1;
}

int main() {
    int arr[] = {2, 3, 4, 10, 5};
    int n = sizeof(arr) / sizeof(arr[0]);
    int key = 10;
    int result = linearSearch(arr, n, key);
    if (result == -1)
        printf("Element is not present in array");
    else
        printf("Element is present at index %d", result);
    return 0;
}
```

## 5. 计算集合幂集

```c
#include <stdio.h>
#include <math.h>

void printPowerSet(char *set, int set_size) {
    unsigned int pow_size = pow(2, set_size);
    int counter, j;
    for (counter = 0; counter < pow_size; counter++) {
        for (j = 0; j < set_size; j++) {
            if (counter & (1 << j))
                printf("%c", set[j]);
        }
        printf("\n");
    }
}

int main() {
    char set[] = {'a', 'b', 'c'};
    printPowerSet(set, 3);
    return 0;
}
```

## SET-14

## 1. 计算圆的面积和周长

```c
#include <stdio.h>
#define PI 3.14159

int main() {
    float radius, area, circumference;
    printf("Enter the radius of the circle: ");
    scanf("%f", &radius);
    area = PI * radius * radius;
    circumference = 2 * PI * radius;
    printf("Area of the circle = %f\n", area);
    printf("Circumference of the circle = %f\n", circumference);
    return 0;
}
```

## 2. 实现二分查找算法

```c
#include <stdio.h>

int binarySearch(int arr[], int left, int right, int key) {
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == key)
            return mid;
        if (arr[mid] < key)
            left = mid + 1;
        else
            right = mid - 1;
    }
    return -1;
}

int main() {
    int arr[] = {2, 3, 4, 10, 14};
    int n = sizeof(arr) / sizeof(arr[0]);
    int key = 10;
    int result = binarySearch(arr, 0, n - 1, key);
    if (result == -1)
        printf("Element is not present in array");
    else
        printf("Element is present at index %d", result);
    return 0;
}
```

## 3. 实现汉诺塔问题

```c
#include <stdio.h>

void towerOfHanoi(int n, char from_rod, char to_rod, char aux_rod) {
    if (n == 1) {
        printf("Move disk 1 from rod %c to rod %c\n", from_rod, to_rod);
        return;
    }
    towerOfHanoi(n - 1, from_rod, aux_rod, to_rod);
    printf("Move disk %d from rod %c to rod %c\n", n, from_rod, to_rod);
    towerOfHanoi(n - 1, aux_rod, to_rod, from_rod);
}

int main() {
    int n = 3;
    towerOfHanoi(n, 'A', 'C', 'B');
    return 0;
}
```

## 4. 计算正弦序列

```c
#include <stdio.h>
#include <math.h>

int main() {
    float angle, radians, sum = 0;
    printf("Enter the angle in degrees: ");
    scanf("%f", &angle);
    radians = angle * 3.14159 / 180;
    for (int i = 0; i < 5; i++) {
        sum += sin(radians);
    }
    printf("Sin(%f) = %f", angle, sum);
    return 0;
}
```

## 5. 统计字符串中字符的频率

```c
#include <stdio.h>
#define MAX_SIZE 100

int main() {
    char str[MAX_SIZE];
    int i, frequency[256] = {0};
    printf("Enter a string: ");
    fgets(str, MAX_SIZE, stdin);
    for (i = 0; str[i] != '\0'; i++) {
        frequency[str[i]]++;
    }
    printf("Character frequency:\n");
    for (i = 0; i < 256; i++) {
        if (frequency[i] != 0) {
            printf("'%c' occurs %d times\n", i, frequency[i]);
        }
    }
    return 0;
}
```

## SET-15

## 1. 计算数字的平方根

```c
#include <stdio.h>
#include <math.h>

int main() {
    double num;
    printf("Enter a number: ");
    scanf("%lf", &num);
    if (num >= 0) {
        printf("Square root of %.2lf = %.2lf\n", num, sqrt(num));
    } else {
        printf("Square root of a negative number is not possible.");
    }
    return 0;
}
```

## 2. 检查数字是否为阿姆斯特斯特数

```c
#include <stdio.h>
#include <math.h>

int isArmstrong(int number) {
    int originalNumber, remainder, result = 0, n = 0;
    originalNumber = number;
    while (originalNumber != 0) {
        originalNumber /= 10;
        ++n;
    }
    originalNumber = number;
    while (originalNumber != 0) {
        remainder = originalNumber % 10;
        result += pow(remainder, n);
        originalNumber /= 10;
    }
    return result == number;
}

int main() {
    int number;
    printf("Enter a number: ");
    scanf("%d", &number);
    if (isArmstrong(number)) {
        printf("%d is an Armstrong number.", number);
    } else {
        printf("%d is not an Armstrong number.", number);
    }
    return 0;
}
```

## 3. 将十进制转换为八进制

```c
#include <stdio.h>

void decimalToOctal(int decimalNumber) {
    int octalNumber = 0, i = 1;
    while (decimalNumber != 0) {
        octalNumber += (decimalNumber % 8) * i;
        decimalNumber /= 8;
        i *= 10;
    }
    printf("Octal: %d", octalNumber);
}
```





```c
decimalNumber /= 8;

i *= 10;

}

printf("Octal equivalent: %d", octalNumber);

}

int main() {

int decimalNumber;

printf("Enter a decimal number: ");

scanf("%d", &decimalNumber);

decimalToOctal(decimalNumber);

return 0;

}
```

## 4. 找到数组中的最大值和最小元素
```c
#include <stdio.h>

int main() {

int array[] = {4, 2, 6, 8, 1, 9};
int n = sizeof(array) / sizeof(array[0]);
int max = array[0];
int min = array[0];

for (int i = 1; i < n; i++) {

if (array[i] > max) {
max = array[i];
}

if (array[i] < min) {
min = array[i];
}
}

printf("Maximum element in array: %d\n", max);
printf("Minimum element in array: %d\n", min);

return 0;

}
```

## 5. 检查字符串是否为回文
```c
#include <stdio.h>
#include <string.h>

int isPalindrome(char str[]) {

int length = strlen(str);
for (int i = 0; i < length / 2; i++) {

if (str[i] != str[length - i - 1]) {
return 0;
}
}
return 1;
}

int main() {

char str[100];
printf("Enter a string: ");
scanf("%s", str);

if (isPalindrome(str)) {
printf("%s is a palindrome.", str);
} else {
printf("%s is not a palindrome.", str);
}

return 0;
}
```

# SET-16

## 1. 检查一个数字是否为质数
```c
#include <stdio.h>

int isPrime(int num) {

if (num <= 1) {
return 0;
}
for (int i = 2; i * i <= num; i++) {

if (num % i == 0) {
return 0;
}
}
return 1;
}

int main() {

int num;
printf("Enter a positive integer: ");
scanf("%d", &num);

if (isPrime(num)) {
printf("%d is a prime number.", num);
} else {
printf("%d is not a prime number.", num);
}

return 0;
}
```

## 2. 计算数字的阶阶
```c
#include <stdio.h>

unsigned long long factorial(int n) {

if (n == 0) {
return 1;
} else {
return n * factorial(n - 1);
}
}

int main() {

int n;
printf("Enter a non-negative integer: ");
scanf("%d", &n);
printf("Factorial of %d = %llu", n, factorial(n));

return 0;
}
```

### 3. 使用插入排序排序数组
```c
#include <stdio.h>

void insertionSort(int arr[], int n) {

int i, key, j;
for (i = 1; i < n; i++) {

key = arr[i];
j = i - 1;
while (j >= 0 && arr[j] > key) {

arr[j + 1] = arr[j];
j = j - 1;
}
arr[j + 1] = key;
}
}

void printArray(int arr[], int n) {

for (int i = 0; i < n; i++) {

printf("%d ", arr[i]);
}
printf("\n");
}

int main() {

int arr[] = {12, 11, 13, 5, 6};
int n = sizeof(arr) / sizeof(arr[0]);
insertionSort(arr, n);
printf("Sorted array: \n");
printArray(arr, n);

return 0;
}
```

## 4. 使用递归计算自然数之和
```c
#include <stdio.h>

int sumOfNaturalNumbers(int n) {

if (n != 0) {
return n + sumOfNaturalNumbers(n - 1);
} else {
return n;
}
}

int main() {

int num;
printf("Enter a positive integer: ");
scanf("%d", &num);
printf("Sum of first %d natural numbers: %d", num, sumOfNaturalNumbers(num));

return 0;
}
```

## 5. 使用递归计算数字的幂
```c
#include <stdio.h>

long long power(int base, int exponent) {

if (exponent != 0) {
return (base * power(base, exponent - 1));
} else {
return 1;
}
}

int main() {

int base, exponent;
printf("Enter base and exponent: ");
scanf("%d %d", &base, &exponent);
printf("%d^%d = %lld", base, exponent, power(base, exponent));

return 0;
}
```

# SET-17

### 1. 计算两个数的的最大公约数 (GCD) 和最小公倍数 (LCM)
```c
#include <stdio.h>

int gcd(int a, int b) {

if (b == 0) {
return a;
}
return gcd(b, a % b);
}

int lcm(int a, int b) {

return (a * b) / gcd(a, b);
}

int main() {

int num1, num2;
printf("Enter positive integers: ");
scanf("%d %d", &num1, &num2);
printf("GCD of %d and %d is %d\n", num1, num2, gcd(num1, num2));
printf("LCM of %d and %d is %d", num1, num2, lcm(num1, num2));

return 0;
}
```

## 2. 无临时变量交换两个数字
```c
#include <stdio.h>

int main() {

int num1, num2;
printf("Enter numbers: ");
scanf("%d %d", &num1, &num2);
printf("Before swapping: a = %d, b = %d\n", num1, num2);
num1 = num1 + num2;
num2 = num1 - num2;
num1 = num1 - num2;
printf("After swapping: a = %d, b = %d\n", num1, num2);

return 0;
}
```

## 3. 检查一个数字是否为平方数
```c
#include <stdio.h>

int isSquare(int num) {

for (int i = 1; i * i <= num; i++) {

if (num == i * i) {
return 1;
}
}
return 0;
}

int main() {

int num;
printf("Enter a number: ");
scanf("%d", &num);

if (isSquare(num)) {
printf("%d is a perfect square.", num);
} else {
printf("%d is not a perfect square.", num);
}

return 0;
}
```

## 4. 计算数字的各位之和
```c
#include <stdio.h>

int sumOfDigits(int num) {

if (num == 0) {
return 0;
}
return (num % 10) + sumOfDigits(num / 10);
}

int main() {

int num;
printf("Enter a number: ");
scanf("%d", &num);
printf("Sum of digits of %d = %d", num, sumOfDigits(num));

return 0;
}
```

## 5. 打印字符的 ASCII 值
```c
#include <stdio.h>

int main() {

char ch;
printf("Enter a character: ");
scanf(" %c", &ch);
printf("ASCII value of %c is %d", ch, ch);

return 0;
}
```

# SET-18

## 1. 计算三角形的面积
```c
#include <stdio.h>

int main() {

float base, height, area;
printf("Enter the base of the triangle: ");
scanf("%f", &base);
printf("Enter the height of the triangle: ");
scanf("%f", &height);
area = 0.5 * base * height;
printf("Area of the triangle = %.2f", area);

return 0;
}
```

## 2. 检查数字是否为回文
```c
#include <stdio.h>

int isPalindrome(int num) {

int reversedNum = 0, originalNum = num;
while (num != 0) {

reversedNum = reversedNum * 10 + num % 10;
num /= 10;
}
return reversedNum == originalNum;
}

int main() {

int num;
printf("Enter a number: ");
scanf("%d", &num);

if (isPalindrome(num)) {
printf("%d is a palindrome.", num);
} else {
printf("%d is not a palindrome.", num);
}

return 0;
}
```

## 3. 检查一个年份是否为闰年
```c
#include <stdio.h>

int isLeapYear(int year) {

if (year % 400 == 0) {
return 1;
}
if (year % 100 == 0) {
return 0;
}
if (year % 4 == 0) {
return 1;
}
return 0;
}

int main() {

int year;
printf("Enter a year: ");
scanf("%d", &year);

if (isLeapYear(year)) {
printf("%d is a leap year.", year);
} else {
printf("%d is not a leap year.", year);
}

return 0;
}
```

## 4. 计算集合的幂集（递归方法）
```c
#include <stdio.h>
#include <math.h>

void printPowerSet(char *set, int set_size) {

unsigned int pow_set_size = pow(2, set_size);
int counter, j;
for (counter = 0; counter < pow_set_size; counter++) {

for (j = 0; j < set_size; j++) {

if (counter & (1 << j))
printf("%c", set[j]);
}
printf("\n");
}
}
}

int main() {

char set[] = {'a', 'b', 'c'};
printPowerSet(set, 3);

return 0;
}
```

## 5. 计算 N 个数的平均值和标准差
```c
#include <stdio.h>
#include <math.h>

int main() {

int n, i;
float num[100], sum = 0.0, mean, standardDeviation = 0.0;
printf("Enter the number of data: ");
scanf("%d", &n);
printf("Enter %d elements: ", n);
for (i = 0; i < n; ++i) {

scanf("%f", &num[i]);
sum += num[i];
}
mean = sum / n;
for (i = 0; i < n; ++i)
standardDeviation += pow(num[i] - mean, 2);
printf("Mean = %.2f\n", mean);
printf("Standard Deviation = %.2f", sqrt(standardDeviation / n));

return 0;
}
```

# SET-19

## 1. 计算数字的幂
```c
#include <stdio.h>

long long power(int base, int exponent) {

long long result = 1;
while (exponent != 0) {

result *= base;
--exponent;
}
return result;
}

int main() {

int base, exponent;
printf("Enter the base number: ");
scanf("%d", &base);
printf("Enter the exponent: ");
scanf("%d", &exponent);
printf("%d raised to the power of %d is %lld", base, exponent, power(base, exponent));

return 0;
}
```

## 2. 实现冒泡排序
```c
#include <stdio.h>

void bubbleSort(int array[], int size) {

for (int step = 0; step < size - 1; ++step) {

for (int i = 0; i < size - step - 1; ++i) {

if (array[i] > array[i + 1]) {

// 交换
int temp = array[i];
array[i] = array[i + 1];
array[i + 1] = temp;
}
}
}
}

int main() {

int data[] = {9, 5, 1, 4, 3};
int size = sizeof(data) / sizeof(data[0]);
bubbleSort(data, size);

return 0;
}
```





```c
bubbleSort(data, size);

printf("升序排列后的数组:\n");

for (int i = 0; i < size; ++i) {
    printf("%d  ", data[i]);
}

return 0;
}
```

### 3. 实现选择排序：

```c
#include <stdio.h>
void selectionSort(int array[], int size) {
    for (int step = 0; step < size - 1; ++step) {
        int min_idx = step;
        for (int i = step + 1; i < size; ++i) {
            if (array[i] < array[min_idx]) {
                min_idx = i;
            }
        }
        // 将找到的最小元素与第一个元素交换
        int temp = array[min_idx];
        array[min_idx] = array[step];
        array[step] = temp;
    }
}

int main() {
    int data[] = {20, 12, 10, 15, 2};
    int size = sizeof(data) / sizeof(data[0]);
    selectionSort(data, size);
    printf("升序排列的数组:\n");
    for (int i = 0; i < size; ++i) {
        printf("%d ", data[i]);
    }
    return 0;
}
```

### 4. 检查字符串是否为另一个字符串的子串：

```c
#include <stdio.h>
#include <string.h>
int isSubstring(char str1[], char str2[]) {
    if (strstr(str1, str2) != NULL) {
        return 1;
    }
    return 0;
}

int main() {
    char str1[100], str2[100];
    printf("输入第一个字符串: ");
    scanf("%s", str1);
    printf("输入第二个字符串: ");
    scanf("%s", str2);
    if (isSubstring(str1, str2)) {
        printf("%s 是 %s 的子串。", str2, str1);
    } else {
        printf("%s 不是 %s 的子串。", str2, str1);
    }
    return 0;
}
```

### 5. 实现一个简单的计算器：

```c
#include <stdio.h>
int main() {
    char operator;
    double num1, num2;
    printf("输入运算符 (+, -, *, /): ");
    scanf("%c", &operator);
    printf("输入两个数字: ");
    scanf("%lf %lf", &num1, &num2);
    switch (operator) {
        case '+':
            printf("%.1lf + %.1lf = %.1lf", num1, num2, num1 + num2);
            break;
        case '-':
            printf("%.1lf - %.1lf = %.1lf", num1, num2, num1 - num2);
            break;
        case '*':
            printf("%.1lf * %.1lf = %.1lf", num1, num2, num1 * num2);
            break;
        case '/':
            if (num2 != 0) {
                printf("%.1lf / %.1lf = %.1lf", num1, num2, num1 / num2);
            } else {
                printf("错误！除以零.");
            }
            break;
        default:
            printf("错误！无效运算符。");
    }
    return 0;
}
```

# SET-20

### 1. 使用数组实现队列：

```c
#include <stdio.h>
#define SIZE 5
int items[SIZE];
int front = -1, rear = -1;

int isFull() {
    if (front == 0 && rear == SIZE - 1) {
        return 1;
    }
    return 0;
}

int isEmpty() {
    if (front == -1) {
        return 1;
    }
    return 0;
}

void enQueue(int element) {
    if (isFull()) {
        printf("\n 队列已满");
    } else {
        if (front == -1) {
            front = 0;
        }
        rear++;
        items[rear] = element;
        printf("\n 插入 -> %d", element);
    }
}

void deQueue() {
    if (isEmpty()) {
        printf("\n 队列为空");
    } else {
        printf("\n 删除 -> %d", items[front]);
        front++;
        if (front > rear) {
            front = rear = -1;
        }
    }
}

void display() {
    int i;
    if (isEmpty()) {
        printf("\n 队列为空");
    } else {
        printf("\n 队列元素为:\n");
        for (i = front; i <= rear; i++) {
            printf("%d  ", items[i]);
        }
    }
}

int main() {
    // 队列操作
    deQueue();
    enQueue(1);
    enQueue(2);
    enQueue(3);
    enQueue(4);
    enQueue(5);
    enQueue(6);
    display();
    // deQueue 删除了先进入的元素即 1
    deQueue();
    // 现在有 4 个元素
    display();
    return 0;
}
```

### 2. 计算单利：

```c
#include <stdio.h>
int main() {
    float principle, rate, time, simpleInterest;
    printf("输入本金: ");
    scanf("%f", &principle);
    printf("输入利率: ");
    scanf("%f", &rate);
    printf("输入年限: ");
    scanf("%f", &time);
    simpleInterest = (principle * rate * time) / 100;
    printf("单利 = %f", simpleInterest);
    return 0;
}
```

### 3. 计算复利：

```c
#include <stdio.h>
#include <math.h>
int main() {
    float principle, rate, time, compoundInterest;
    printf("输入本金: ");
    scanf("%f", &principle);
    printf("输入利率: ");
    scanf("%f", &rate);
    printf("输入年限: ");
    scanf("%f", &time);
    compoundInterest = principle * pow((1 + rate / 100), time);
    printf("复利 = %f", compoundInterest);
    return 0;
}
```

### 4. 打印前 n 项斐波那契数列：

```c
#include <stdio.h>
void printFibonacci(int n) {
    int a = 0, b = 1, c, i;
    if (n <= 0)
        return;
    printf("%d ", a);
    for (i = 2; i <= n; i++) {
        printf("%d ", b);
        c = a + b;
        a = b;
        b = c;
    }
}

int main() {
    int terms;
    printf("输入项数: ");
    scanf("%d", &terms);
    printf("前 %d 项斐波那契数列: ", terms);
    printFibonacci(terms);
    return 0;
}
```

### 5. 使用迭代法计算阶阶乘：

```c
#include <stdio.h>
unsigned long long factorial(unsigned int n) {
    unsigned long long fact = 1;
    for (int i = 1; i <= n; ++i) {
        fact *= i;
    }
    return fact;
}

int main() {
    int num;
    printf("输入一个正整数: ");
    scanf("%d", &num);
    printf("%d 的阶乘 = %llu", num, factorial(num));
    return 0;
}
```

