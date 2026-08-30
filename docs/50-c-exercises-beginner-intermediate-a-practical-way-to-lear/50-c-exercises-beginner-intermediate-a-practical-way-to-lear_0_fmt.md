
# 50 道 C 语言初级与中级练习：学习 C 编程的实用方法

## C 语言概览

Dennis Ritchie 于 20 世纪 70 年代初在贝尔实验室创建了 C 编程语言，它在今天仍被广泛使用。它是作为 B 语言的扩展而开发的，具有新的数据类型和功能。多年来，C 已成为世界上使用最广泛的编程语言之一，影响了如 `C++`、`C#`、`Objective-C` 等许多现代编程语言的发展，并间接地影响了 `Java` 和 `Python` 等语言。

## C 语言的重要性

C 语言经常用于系统编程，特别是在操作系统的创建中。例如，Linux 和 Windows 内核包含了 C 代码。

C 是一种编译型语言，因此它的运行速度比解释型语言更快。结果，它适用于资源受限的环境或需要高性能的场景。

C 语言最大的优势之一是能够“一次编写，随处运行”（只需少许修改）。这意味着一个 C 程序可以在一个系统中创建，然后在另一个系统中无需或仅需少量修改即可运行。

C 遵循过程化范式，这对于需要逐步步进的任务非常有用。

现代语言的基础：学习 C 语言为理解更复杂的语言奠下了坚实的基础。C 是许多当前语言语法和概念的来源。

## 初级

### 第一部分：C 语言基础

- 基础 C 语法和操作的介绍。
- 简单的 I/O、算术计算和常量的使用。

### 第二部分：控制结构

- 条件语句的介绍。
- 使用 `if-else` 和 `switch-case` 进行决策。

### 第三部分：循环

- 迭代的介绍。

### 第四部分：函数

- 模块化编程的介绍。

### 第五部分：数组

- 数据结构的介绍。

### 第六部分：字符串与字符

- 字符串操作的介绍。

### 第七部分：指针

- 内存管理的介绍。

### 第八部分：函数

- 专注于递归。

### 第九部分：结构体

- 用户定义结构的介绍。

### 第十部分：文件与 I/O

- 文件操作的介绍。

## 初级

### 第一部分：C 语言基础

- 1-1: 编写打印“Hello, World!”的程序。
- 1-2: 编写接收输入并输出其长度的程序。
- 1-3: 编写将摄氏度转换为华氏度的程序。
- 1-4: 编写计算圆面积的程序。
- 1-5: 编写计算数字之和的程序。

### 第二部分：控制结构

- 2-1: 编写检查数字是偶数还是奇数的程序。
- 2-2: 编写打印月份名称的程序。
- 2-3: 编写检查字符是否为元音或辅音的程序。
- 2-4: 编写找到三个数中最大值的程序。
- 2-5: 编写检查是否为闰年的程序。

### 第三部分：循环

- 3-1: 编写打印前 10 个自然数的程序。
- 3-2: 编写计算数字阶乘的程序。
- 3-3: 编写打印到指定项项的斐波那契数列的程序。
- 3-4: 编写查找指定范围内质数的程序。
- 3-5: 编写输出某个数字的乘法表的程序。

### 第四部分：函数

- 4-1: 编写一个返回两个数字之和的函数。
- 4-2: 创建一个找到三个数中最大值的函数。
- 4-3: 编写一个计算数字阶乘的函数。
- 4-4: 创建一个检查数字是否为质数的函数。
- 4-5: 编写一个将字符串转换为大写的 `de` 函数。

### 第五部分：数组

- 5-1: 编写查找数组中最大和最小元素的程序。
- 5-2: 创建一个反转数组元素的程序。
- 5-3: 编写一个计算数组元素总和和平均值的程序。
- 5-4: 创建一个按升序排序数组的程序。
- 5-5: 编写一个使用线性查找在数组中寻找特定元素的程序。

## 中级

### 第六部分：字符串与字符

- 6-1: 编写一个接收字符串并输出其长度的程序。
- 6-2: 实现一个检查字符串是否为回文的程序。
- 6-3: 创建一个不使用 `strcat()` 连接两个字符串的程序。
- 6-4: 编写一个将字符串中所有空格替换为连字符的程序。
- 6-5: 实现一个统计字符串中元音和辅音数量的程序。

### 第七部分：指针

- 7-1: 编写使用指针交换两个整数值的程序。
- 7-2: 实现一个使用指针查找字符串长度的程序。
- 7-3: 创建一个使用指针反转字符串的程序。
- 7-4: 编写一个使用指针计算数组所有元素之和的程序。
- 7-5: 实现一个使用指针按升序排序整数数组的程序。

### 第八部分：函数

- 8-1: 实现一个计算第 n 斐波那契数的递归函数。
- 8-2: 编写一个使用函数实现二分查找算法的程序。
- 8-3: 实现一个使用递归函数计算数字 n 方的程序。
- 8-4: 创建一个检查数字是否为质数的函数，然后实现一个打印 n 以内质数的函数。
- 8-5: 实现一个计算两个数字最大公约数(GCD)的递归函数。

### 第九部分：结构体

- 9-1: 定义一个表示复数的结构体。实现两个复数的加、减、乘函数。
- 9-2: 创建一个表示日期（日、月、年）的结构体。编写一个计算两个日期之间差值（天）的程序。
- 9-3: 实现一个包含姓名、学号和三门科目成绩的学生结构体。编写一个计算学生平均分数的函数。
- 9-4: 编写一个使用结构体存储并显示书籍信息（书籍 ID、标题、作者、价格）的程序。
- 9-5: 创建一个名为 `Time` 的结构体，包含三个整数成员：`hours`、`minutes` 和 `seconds`。创建一个函数来计算两个时间。

### 第 10 节 文件与输入/输出

- 10-1: 编写一个程序，创建一个文本并将并将输入的字符串写入文件。
- 10-2: 实现一个程序，读取文件并统计文件中的行数、单词数和字符数。
- 10-3: 创建一个程序，将一个文件的内容复制到另一个文件中。
- 10-4: 实现一个程序，将两个文本文件合并到第三个文件中。
- 10-5: 编写一个程序，读取文件并显示文件中长的一行。

## 初学者 1 答案：

```c
#include <stdio.h>

int main() {
    // #1-1
    printf("Hello, World!\n");

    // #1-2
    double number;
    printf("Enter a number: ");
    scanf("%lf", &number);
    printf("Double of %lf is %lf\n", number, 2 * number);

    // #1-3
    double celsius, fahrenheit;
    printf("Enter temperature in Celsius: ");
    scanf("%lf", &celsius);
    fahrenheit = (celsius * 9/5) + 32;
    printf("Temperature in Fahrenheit: %lf\n", fahrenheit);

    // #1-4
    const double PI = 3.141592653589793;
    double radius;
    printf("Enter the radius of the circle: ");
    scanf("%lf", &radius);
    double area = PI * radius * radius;
    printf("Area of the circle: %lf\n", area);

    // #1-5
    double num1, num2, num3, sum, average, product;
    printf("Enter three numbers: ");
    scanf("%lf %lf %lf", &num1, &num2, &num3);
    sum = num1 + num2 + num3;
    average = sum / 3;
    product = num1 * num2 * num3;
    printf("Sum = %lf, Average = %lf, Product = %lf\n", sum, average, product);
    return 0;
}
```

## 初学者 1 输出：

#1-1

Hello, World!

#1-2

Enter a number: 5.0

Double of 5.000000 is 10.000000

#1-3

Enter temperature in Celsius: 25

Temperature in Fahrenheit: 77.000000

#1-4

Enter the radius of the circle: 5

Area of the circle: 78.539816

#1-5

Enter three numbers: 1 2 3

Sum = 6.000000, Average = 2.000000, Product = 6.000000

## 初学者 2 答案：

```c
#include <stdio.h>

int main() {
    // #2-1
    int num;
    printf("Enter an integer: ");
    scanf("%d", &num);
    if (num % 2 == 0) {
        printf("%d is even\n", num);
    } else {
        printf("%d is odd\n", num);
    }

    // #2-2
    int month;
    printf("Enter month number (1-12): ");
    scanf("%d", &month);
    switch(month) {
        case 1: printf("January\n"); break;
        case 2: printf("February\n"); break;
        // ... 其他月份类似
        case 12: printf("December\n"); break;
        default: printf("Invalid month\n");
    }

    // #2-3
    char ch;
    printf("Enter a character: ");
    scanf(" %c", &ch); // 注意在 %c 前加空格以消耗换行符
    if(ch=='a' || ch=='e' || ch=='i' || ch=='o' || ch=='u' ||
        ch=='A' || ch=='E' || ch=='I' || ch=='O' || ch=='U') {
        printf("%c is a vowel\n", ch);
    } else {
        printf("%c is a consonant\n", ch);
    }

    // #2-4
    double a, b, c;
    printf("Enter three numbers: ");
    scanf("%lf %lf %lf", &a, &b, &c);
    double largest = (a > b) ? (a > c ? a : c) : (b > c ? b : c);
    printf("Largest number is %lf\n", largest);

    // #2-5
    int year;
    printf("Enter a year: ");
    scanf("%d", &year);
    if((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0)) {
        printf("%d is a leap year\n", year);
    } else {
        printf("%d is not a leap year\n", year);
    }
    return 0;
}
```

## 初学者 2 输出：

#2-1

Enter an integer: 4

4 is even

#2-2

Enter month number (1-12): 7

July

#2-3

Enter a character: e

e is a vowel

#2-4

Enter three numbers: 5 3 7

Largest number is 7.000000

#2-5

Enter a year: 2000

2000 is a leap year

## 初学者 3 答案：

```c
#include <stdio.h>

int main() {
    // #3-1
    for(int i = 1; i <= 10; i++) {
        printf("%d ", i);
    }
    printf("\n");

    // #3-2
    int n, factorial = 1;
    printf("Enter positive integer: ");
    scanf("%d", &n);
    for(int i = 1; i <= n; i++) {
        factorial *= i;
    }
    printf("Factorial of %d = %d\n", n, factorial);

    // #3-3
    int terms, t1 = 0, t2 = 1, nextTerm;
    printf("Enter number of terms: ");
    scanf("%d", &terms);
    printf("Fibonacci Series: ");
    for (int i = 1; i <= terms; i++) {
        printf("%d ", t1);
        nextTerm = t1 + t2;
        t1 = t2;
        t2 = nextTerm;
    }
    printf("\n");

    // #3-4
    int start, end;
    printf("Enter two numbers (intervals): ");
    scanf("%d %d", &start, &end);
    printf("Prime numbers between %d and %d are: ", start, end);
    for(int i = start; i <= end; i++) {
        int flag = 1;
        for(int j = 2; j <= i; j++) {
            if(i % j == 0) {
                flag = 0;
                break;
            }
        }
        if(flag && i != 1) printf("%d ", i);
    }
    printf("\n");

    // #3-5
    int multiplier;
    printf("Enter a number: ");
    scanf("%d", &multiplier);
    for(int i = 1; i <= 10; i++) {
        printf("%d = %d\n", i, multiplier * i);
    }
    return 0;
}
```

## 初学者 3 输出：

#3-1

1 2 3 4 5 6 7 8 9 10

#3-2

Enter positive integer: 5

Factorial of 5 = 120

#3-3

Enter number of terms: 7

Fibonacci Series: 0 1 1 2 3 5 8

#3-4

Enter two numbers (intervals): 10 50

Prime numbers between 10 and 50 are: 11 13 17 19 23 29 31 37 41 43 47

#3-5

Enter a number: 5

1 = 5

2 = 10

3 = 15

4 = 20

5 = 25

6 = 30

7 = 35

8 = 40

9 = 45

10 = 50

## 初学者 4 答案：



下面是排版后的 Markdown 文档：

```c
#include <stdio.h>
#include <stdbool.h>

// #4-1
double sum_of_two(double a, double b) {
    return a + b;
}

// #4-2
double largest_of_three(double a, double b, double c) {
    return (a > b) ? (a > c ? a : c) : (b > c ? b : c);
}

// #4-3
int factorial_recursive(int n) {
    if (n == 0 || n == 1) {
        return 1;
    } else {
        return n * factorial_recursive(n - 1);
    }
}

// #4-4
bool is_prime(int n) {
    if (n <= 1) return false;
    for (int i = 2; i <= n; i++) {
        if (n % i == 0) return false;
    }
    return true;
}

// #4-5
void to_uppercase(char *str) {
    for (int i = 0; str[i] != '\0'; i++) {
        if (str[i] >= 'a' && str[i] <= 'z') {
            str[i] = str[i] - ('a' - 'A');
        }
    }
}

int main() {
    // #4-1 Test
    printf("Sum of 5 and 3: %lf\n", sum_of_two(5, 3));

    // #4-2 Test
    printf("Largest of 5, 3, and 7: %lf\n", largest_of_three(5, 3, 7));

    // #4-3 Test
    printf("Factorial of 5: %d\n", factorial_recursive(5));

    // #4-4 Test
    printf("Is 17 prime? %s\n", is_prime(17) ? "Yes" : "No");

    // #4-5 Test
    char str[] = "hello World!";
    to_uppercase(str);
    printf("Uppercase: %s\n", str);
    return 0;
}
```

## 初学者 4 输出：

`#4-1`  
`Sum of 5 and 3: 8.000000`

`#4-2`  
`Largest of 5, 3, and 7: 7.000000`

`#4-3`  
`Factorial of 5: 120`

`#4-4`  
`Is 17 prime? Yes`

`#4-5`  
`Uppercase: HELLO WORLD!`

## 初学者 5 答案：

```c
#include <stdio.h>

int main() {
    int arr[] = {10, 8, 5, 20, 90};

    // #5-1
    int min = arr[0], max = arr[0];
    for (int i = 1; i < 5; i++) {
        if (arr[i] < min) min = arr[i];
        if (arr[i] > max) max = arr[i];
    }
    printf("Minimum: %d, Maximum: %d\n", min, max);

    // #5-2
    int rev[5];
    for (int i = 0; i < 5; i++) {
        rev[i] = arr[4 - i];
    }
    printf("Reversed: ");
    for (int i = 0; i < 5; i++) {
        printf("%d ", rev[i]);
    }
    printf("\n");

    // #5-3
    double sum = 0, average;
    for (int i = 0; i < 5; i++) {
        sum += arr[i];
    }
    average = sum / 5;
    printf("Sum: %lf, Average: %lf\n", sum, average);

    // #5-4
    for (int i = 0; i < 5; i++) {
        for (int j = i + 1; j < 5; j++) {
            if (arr[i] > arr[j]) {
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
    }
    printf("Sorted: ");
    for (int i = 0; i < 5; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");

    // #5-5
    int search, flag = 0;
    printf("Enter a number to search: ");
    scanf("%d", &search);
    for (int i = 0; i < 5; i++) {
        if (arr[i] == search) {
            flag = 1;
            break;
        }
    }
    if (flag) {
        printf("%d found in the array.\n", search);
    } else {
        printf("%d not found in the array.\n", search);
    }
    return 0;
}
```

## 初学者 5 输出：

`#5-1`  
`Minimum: 5, Maximum: 90`

`#5-2`  
`Reversed: 90 8 5 20 10`

`#5-3`  
`Sum: 133.000000, Average: 26.600000`

`#5-4`  
`Sorted: 5 8 10 20 90`

`#5-5`  
`Enter a number to search: 20`  
`20 found in the array.`

## 中级 1 答案：

```c
#include <stdio.h>
#include <stdbool.h>
#include <string.h>

// #6-1
int string_length(char *str) {
    int len = 0;
    while (*str++) {
        len++;
    }
    return len;
}

// #6-2
```

```c
bool is_palindrome(char *str) {
    int len = string_length(str);
    for (int i = 0; i < len / 2; i++) {
        if (str[i] != str[len - 1 - i]) {
            return false;
        }
    }
    return true;
}

// #6-3
void concatenate_strings(char *dest, char *src) {
    while (*dest) {
        dest++;
    }
    while ((*dest++ = *src++));
}

// #6-4
void replace_spaces_with_hyphen(char *str) {
    while (*str) {
        if (*str == ' ') {
            *str = '-';
        }
        str++;
    }
}

// #6-5
void count_vowels_and_consonants(char *str, int *vowels, int *consonants) {
    *vowels = 0;
    *consonants = 0;
    while (*str) {
        if ((*str >= 'A' && *str <= 'Z') || (*str >= 'a' && *str <= 'z')) {
            switch (*str) {
                case 'A': case 'E': case 'I': case 'O': case 'U':
                case 'a': case 'e': case 'i': case 'o': case 'u':
                    (*vowels)++;
                    break;
                default:
                    (*consonants)++;
            }
        }
        str++;
    }
}

int main() {
    // #6-1 Test
    char str1[] = "Hello, World!";
    printf("Length of '%s': %d\n", str1, string_length(str1));
    // #6-2 Test
    char str2[] = "radar";
    printf("Is '%s' a palindrome? %s\n", str2, is_palindrome(str2) ? "Yes" : "No");
    // #6-3 Test
    char dest[50] = "Hello, ";
    char src[] = "World!";
    concatenate_strings(dest, src);
    printf("Concatenated: %s\n", dest);
    // #6-4 Test
    char str3[] = "Hello World!";
    replace_spaces_with_hyphen(str3);
    printf("Spaces replaced: %s\n", str3);
    // #6-5 Test
    char str4[] = "Programming in C";
    int vowels, consonants;
    count_vowels_and_consonants(str4, &vowels, &consonants);
    printf("In '%s', Vowels: %d, Consonants: %d\n", str4, vowels, consonants);
    return 0;
}
```

### 中间 1 输出：

`#6-1`  
`Length of 'Hello, World!': 13`

`#6-2`  
`Is 'radar' a palindrome? Yes`

`#6-3`  
`Concatenated: Hello, World!`

`#6-4`  
`Spaces replaced: Hello-World!`

`#6-5`  
`In 'Programming in C', Vowels: 5, Consonants: 11`

### 中间 2 解决方案：

```c
#include <stdio.h>

// #7-1
void swap_values(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

// #7-2
int string_length_pointer(char *str) {
    int len = 0;
    while (*str++) {
        len++;
    }
    return len;
}

// #7-3
void reverse_string_pointer(char *str) {
    char *start = str;
    char *end = str + string_length_pointer(str) - 1;
    while (start < end) {
        swap_values(start, end);
        start++;
        end--;
    }
}

// #7-4
int sum_array_pointer(int *arr, int len) {
    int sum = 0;
    int *end = arr + len;
    while (arr < end) {
        sum += *arr++;
    }
    return sum;
}

// #7-5
void sort_array_pointer(int *arr, int len) {
    for (int i = 0; i < len - 1; i++) {
        for (int j = i + 1; j < len; j++) {
            if (*(arr + i) > *(arr + j)) {
                swap_values(arr + i, arr + j);
            }
        }
    }
}

int main() {
    // #7-1 Test
    int x = 5, y = 8;
    printf("Before swap: x = %d, y = %d\n", x, y);
    swap_values(&x, &y);
    printf("After swap: x = %d, y = %d\n", x, y);
    // #7-2 Test
    char str1[] = "OpenAI";
    printf("Length of '%s': %d\n", str1, string_length_pointer(str1));
    // #7-3 Test
    char str2[] = "Programming";
    reverse_string_pointer(str2);
    printf("Reversed string: %s\n", str2);
    // #7-4 Test
    int arr1[] = {1, 2, 3, 4, 5};
    printf("Sum of array: %d\n", sum_array_pointer(arr1, 5));
    // #7-5 Test
    int arr2[] = {5, 12, 45, 2, 9};
    sort_array_pointer(arr2, 5);
    printf("Sorted array: ");
    for (int i = 0; i < 5; i++) {
        printf("%d ", arr2[i]);
    }
    printf("\n");
}
```

### 中间 2 输出：

`#7-1`  
`Before swap: x = 5, y = 8`  
`After swap: x = 8, y = 5`

`#7-2`  
`Length of 'OpenAI': 6`

`#7-3`  
`Reversed string: gnimmargP`

`#7-4`  
`Sum of array: 15`

`#7-5`  
`Sorted array: 2 5 9 12 45`

### 中间 3 解决方案：



```c
#include <stdio.h>
#include <stdbool.h>

// #8-1
int fibonacci(int n) {
    if (n <= 1) return n;
    return fibonacci(n-1) + fibonacci(n-2);
}

// #8-2
int binary_search(int arr[], int l, int r, int x) {
    if (r >= l) {
        int mid = l + (r - l) / 2;
        if (arr[mid] == x) return mid;
        if (arr[mid] > x) return binary_search(arr, l, mid-1, x);
        return binary_search(arr, mid+1, r, x);
    }
    return -1;
}

// #8-3
double power(double base, int exponent) {
    if (exponent == 0) return 1;
    else if (exponent < 0) return 1 / power(base, -exponent);
    return base * power(base, exponent-1);
}

// #8-4
bool is_prime(int n) {
    if (n <= 1) return false;
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) return false;
    }
    return true;
}

void print_primes_to_n(int n) {
    for (int i = 2; i <= n; i++) {
        if (is_prime(i)) printf("%d ", i);
    }
    printf("\n");
}

// #8-5
int gcd(int a, int b) {
    if (b == 0) return a;
    return gcd(b, a % b);
}

int main() {
    // #8-1 Test
    int n = 9;
    printf("Fibonacci number at position %d: %d\n", n, fibonacci(n));

    // #8-2 Test
    int arr[] = {2, 3, 4, 10, 40};
    int x = 10;
    int result = binary_search(arr, 0, 4, x);
    if (result == -1) printf("Element not present in array\n");
    else printf("Element %d is present at index %d\n", x, result);

    // #8-3 Test
    double base = 2.0;
    int exponent = -3;
    printf("%.2lf raised to the power %d is %.2lf\n", base, exponent, power(base, exponent));

    // #8-4 Test
    int limit = 50;
    printf("Prime numbers up to %d: ", limit);
    print_primes_to_n(limit);

    // #8-5 Test
    int num1 = 56, num2 = 98;
    printf("GCD of %d and %d is %d\n", num1, num2, gcd(num1, num2));

    return 0;
}
```

## 中间 3 输出

### #8-1

Fibonacci number at position 9: 34

### #8-2

Element 10 is present at index 3

### #8-3

2.00 raised to the power -3 is 0.12

### #8-4

Prime numbers up to 50: 2 3 5 7 11 13 17 19 23 29 31 37 41 43 47

### #8-5

GCD of 56 and 98 is 14

## 中间 4 解决方案

```c
#include <stdio.h>

// #9-1
typedef struct {
    float real;
    float imag;
} Complex;

Complex add(Complex a, Complex b) {
    Complex result;
    result.real = a.real + b.real;
    result.imag = a.imag + b.imag;
    return result;
}

Complex subtract(Complex a, Complex b) {
    Complex result;
    result.real = a.real - b.real;
    result.imag = a.imag - b.imag;
    return result;
}

Complex multiply(Complex a, Complex b) {
    Complex result;
    result.real = a.real * b.real - a.imag * b.imag;
    result.imag = a.real * b.imag + a.imag * b.real;
    return result;
}

Complex divide(Complex a, Complex b) {
    float denominator = b.real * b.real + b.imag * b.imag;
    Complex result;
    result.real = (a.real * b.real + a.imag * b.imag) / denominator;
    result.imag = (a.imag * b.real - a.real * b.imag) / denominator;
    return result;
}

// #9-2
typedef struct {
    int day;
    int month;
    int year;
} Date;

int differenceBetweenDates(Date d1, Date d2) {
    // Simplified logic for demonstration
    return (d2.year - d1.year) * 365 + (d2.month - d1.month) * 30 + (d2.day - d1.day);
}

// #9-3
typedef struct {
    char name[50];
    float marks[3];
} Student;

float averageMarks(Student s) {
    float sum = 0;
    for (int i = 0; i < 3; i++) {
        sum += s.marks[i];
    }
    return sum / 3.0;
}

// #9-4
typedef struct {
    int id;
    char title[100];
    char author[50];
    float price;
} Book;

void displayBookInfo(Book b) {
    printf("ID: %d\nTitle: %s\nAuthor: %s\nPrice: %.2f\n", b.id, b.title, b.author, b.price);
}

int main() {
    // Test cases for each part will be here

    // #9-1 Test
    Complex c1 = {2.0, 3.0};
    Complex c2 = {1.0, 2.0};
    Complex sum = add(c1, c2);
    printf("#9-1\nSum: %f + %fi\n", sum.real, sum.imag);

    // #9-2 Test
    Date d1 = {1, 1, 2021};
    Date d2 = {2, 3, 2021};
    printf("\n#9-2\nDifference between dates 01/01/2021 and 02/03/2021: %d days\n", differenceBetweenDates(d1, d2));

    // #9-3 Test
    Student john = {"John", {80.0, 75.5, 79.5}};
    printf("\n#9-3\nAverage marks for John: %.2f\n", averageMarks(john));

    // #9-4 Test
    Book sampleBook = {101, "The Great Book", "John Doe", 19.99};
    printf("\n#9-4\n");
    displayBookInfo(sampleBook);

    // #9-5 Test
    Time t1 = {2, 30, 45};
    Time t2 = {1, 20, 20};
    Time sumTime = addTimes(t1, t2); // Note: addTimes needs to be defined

    return 0;
}
```

> 注：由于提供的文本在 `#9-5` 处出现了 `Time` 类型和 `addTimes` 函数但在原始代码中未给出定义，上述翻译保留了原文的逻辑结构。

```c
printf("\n#9-5\nSum of times 2:30:45 and 1:20:20 is %d:%02d:%02d\n", sumTime.hours, sumTime.minutes, sumTime.seconds);

return 0;

}
```

## Intermediate 4 输出

### #9-1

和：3.000000 + 5.000000i

### #9-2

（使用代码中描述的近似方法）

日期 01/01/2021 和 02/03/2021 之间的差：63 天

### #9-3

John 的平均分：78.33

### #9-4

书籍 ID：101

标题：The Great Book

作者：John Doe

价格：19.99

### #9-5

时间 2:30:45 和 1:20:20 的和为 3:51:05

## Intermediate 5 解答案

```c
#include <stdio.h>
#include <string.h>

// #10-1
void createFileAndWrite() {
    FILE *file;
    char str[1000];
    file = fopen("user_input.txt", "w");
    if (file == NULL) {
        printf("无法创建文件。\n");
        return;
    }
    printf("Enter 一个字符串: ");
    fgets(str, sizeof(str), stdin);
    fputs(str, file);
    fclose(file);
}

// #10-2
void countFileContents() {
    FILE *file;
    char ch;
    int lines = 0, words = 1, characters = 0;
    file = fopen("user_input.txt", "r");
    if (file == NULL) {
        printf("无法打开文件。\n");
        return;
    }
    while ((ch = fgetc(file)) != EOF) {
        characters++;
        if (ch == '\n' || ch == '\0')
            lines++;
        if (ch == ' ' || ch == '\t' || ch == '\n' || ch == '\0')
            words++;
    }
    fclose(file);
    printf("Lines: %d\nWords: %d\nCharacters: %d\n", lines, words, characters);
}

// #10-3
void copyFile() {
    FILE *srcFile, *destFile;
    char ch;
    srcFile = fopen("user_input.txt", "r");
    if (srcFile == NULL) {
        printf("无法打开源文件进行读取。\n");
        return;
    }
    destFile = fopen("copy.txt", "w");
    if (destFile == NULL) {
        printf("无法打开目标文件进行写入。\n");
        return;
    }
    ch = fgetc(srcFile);
    while (ch != EOF) {
        fputc(ch, destFile);
        ch = fgetc(srcFile);
    }
    printf("文件复制成功。\n");
    fclose(srcFile);
    fclose(destFile);
}

// #10-4
void mergeFiles() {
    FILE *file1, *file2, *file3;
    char ch;
    file1 = fopen("file1.txt", "r");
    file2 = fopen("file2.txt", "r");
    file3 = fopen("merged.txt", "w");
    if (file1 == NULL || file2 == NULL || file3 == NULL) {
        printf("打开文件出错。\n");
        return;
    }
    while ((ch = fgetc(file1)) != EOF)
        fputc(ch, file3);
    while ((ch = fgetc(file2)) != EOF)
        fputc(ch, file3);
    printf("已将 file1.txt 和 file2.txt 合并到 merged.txt\n");
    fclose(file1);
    fclose(file2);
    fclose(file3);
}

// #10-5
void displayLongestLine() {
    FILE *file;
    char line[1000], longestLine[1000] = "";
    file = fopen("user_input.txt", "r");
    if (file == NULL) {
        printf("无法打开文件。\n");
        return;
    }
    while (fgets(line, sizeof(line), file) != NULL) {
        if (strlen(line) > strlen(longestLine)) {
            strcpy(longestLine, line);
        }
    }
    fclose(file);
    printf("Longest Line: %s", longestLine);
}

int main() {
    // #10-1 测试
    printf("#10-1\n");
    createFileAndWrite();

    // #10-2 测试
    printf("\n#10-2\n");
    countFileContents();

    // #10-3 测试
    printf("\n#10-3\n");
    copyFile();

    // #10-4 测试
    printf("\n#10-4\n");
    mergeFiles();

    // #10-5 测试
    printf("\n#10-5\n");
    displayLongestLine();

    return 0;
}
```

对于 #10-1，我假设用户输入了 `"Hello, World! This is a sample string."`。

对于 #10-2，计数是基于上述字符串。行末尾计算了一个换行字符。

对于 #10-3，如果复制过程中没有出现问题，则显示成功消息。

对于 #10-4，如果 `file1.txt` 和 `file2.txt` 存在并已合并到 `merged.txt`，则显示成功消息。

对于 #10-5，如果 `user_input.txt` 中最长的行是 #10-1 中输入的同一行，则会显示该行。

## Intermediate 5 输出

### #10-1



输入一个字符串: `Hello, World! This is a sample string.`

### #10-2

Lines: 1

Words: 7

Characters: 40

### #10-3

文件复制成功。

### #10-4

已将`file1.txt`和`file2.txt`合并到`merged.txt`

### #10-5

Longest Line: `Hello, World! This is a sample string.`

我们希望您对在 Amazon 购买的商品满意！我们想借此机会提醒您，为您购买的产品留下评价很重要。您的反馈对我们以及其他潜在买家都至关重要。

通过分享您对产品的看法和经验，您可以帮助他人做出决定。您的评价可以成为其他客户的指南，确保他们选择最适合自己的产品。

如果您能抽几分钟写一条诚实的评价，我们将不胜感激。您的反馈有助于我们改进产品和服务，这对所有人来说都是双赢的。

感谢您成为我们的价值客户，并考虑编写评价。我们非常感谢您的支持。

介绍我的个人博客。保持联系！

`premiumbookself.wordpress.com/`
