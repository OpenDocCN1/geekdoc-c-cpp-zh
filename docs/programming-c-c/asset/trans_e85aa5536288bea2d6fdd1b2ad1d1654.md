

30. 编写一个 C 程序使用递归求最大公约数 (G.C.D)。

31. 编写一个 C 程序使用数组计算平均值。

32. 编写一个 C 程序查找数组中的最大元素。

33. 编写一个 C 程序相两个多维数组（矩阵）。

34. 编写一个 C 程序获取字符串的长度。

35. 编写一个 C 程序拼接两个字符串。

36. 编写一个 C 程序在不使用 `strcpy()` 的情况下复制字符串。

37. 编写一个 C 程序统计元音、辅音等的数量。

38. 编写一个 C 程序查找字符串中字符出现的频率。

39. 编写一个 C 程序使用指针访问数组元素。

40. 编写一个 C 程序来创建、初始化、赋值和访问指针变量。

41. 编写一个 C 程序使用指针交换两个数字。

42. 编写一个 C 程序使用指针统计字符串中的元音和辅音。

43. 编写一个 C 程序使用结构体存储学生信息。

44. 编写一个 C 程序使用结构体相两个距离（英寸-英制）。

45. 编写一个 C 程序声明并初始化一个联合体 (union)。

46. 编写一个 C++ 程序实现函数重载。

47. 编写一个 C++ 程序使用封装计算矩形面积。

48. 编写一个 C++ 程序使用数据抽象相两个数字。

49. 编写一个 C++ 程序重载二元运算符。

## 建议的实验编程题及答案

- 1. 编写一个 C 程序两个整数相加。

```
#include<stdio.h>
int main() {

int number1, number2, sum;

printf("Enter two integers: ");
scanf("%d %d", &number1, &number2);

// 计算总和
sum = number1 + number2;

printf("%d + %d = %d", number1, number2, sum);
return 0;
}
```

Output
Enter two integers: 12 11
12 + 11 = 23

- 2. 编写一个 C 程序打印一个整数（用户输入的）。

```
#include<stdio.h>
int main(){
int number;

printf("Enter an integer: ");

// 读取并存储输入
scanf("%d",&number);

// 显示输出
printf("You entered: %d", number);

return 0;
}
```

# Output

Enter an integer: 25
You entered: 25

- 3. **编写一个 C 程序计算两个浮点数的乘积。**
```c
#include<stdio.h>
int main() {
double a, b, product;
printf("Enter two numbers: ");
scanf("%lf %lf", &a, &b);

// 计算乘积
product = a * b;

// 使用 %2lf 显示保留两位小数的结果
printf("Product = %.2lf", product);

return 0;
}
```

Output
Enter two numbers: 2.4 and 1.12
Product = 2.69

- 4. **编写一个 C 程序获取字符的 ASCII 值。**
```c
#include<stdio.h>
int main() {
char c;
printf("Enter a character: ");
scanf("%c",&c);

// %d 显示实际字符的整数值
// %c 显示 %c = %d 的 ASCII 值
printf("ASCII value of %c = %d", c, c);

return 0;
}
```

# 实验编程

# Output

Enter a character: G
ASCII value of G = 71

## 5. 编写一个 C 程序计算商和余数。

```c
#include<stdio.h>
int main(){
    int dividend, divisor, quotient, remainder;
    printf("Enter dividend: ");
    scanf("%d", &dividend);
    printf("Enter divisor: ");
    scanf("%d", &divisor);

    // 计算商
    quotient = dividend / divisor;

    // 计算余数
    remainder = dividend % divisor;

    printf("Quotient = %d\n", quotient);
    printf("Remainder = %d\n", remainder);
    return 0;
}
```

# Output

Enter dividend: 25
Enter divisor: 4
Quotient = 6
Remainder = 1

## 6. 编写一个 C 程序查找 int, float, double 和 char 的大小。

```c
#include<stdio.h>
int main(){
    int intType;
    float floatType;
    double doubleType;
    char charType;

    // sizeof 评估变量的大小
    printf("Size of int: %d bytes\n", sizeof(intType));
    printf("Size of float: %d bytes\n", sizeof(floatType));
    printf("Size of double: %d bytes\n", sizeof(doubleType));
    printf("Size of char: %d bytes\n", sizeof(charType));

    return 0;
}
```

# Output

Size of int: 4 bytes
Size of float: 4 bytes
Size of double: 8 bytes
Size of char: 1 byte

- 7. 编写一个 C 程序使用临时变量交换两个数字。

```c
#include<stdio.h>
int main(){
    int first, second, temp;
    printf("Enter first number: ");
    scanf("%d",&first);
    printf("Enter second number: ");
    scanf("%d",&second);

    // 将 first 赋值给 temp
    temp=first;

    // 将 second 赋值给 first
    first=second;

    // 将 temp（first 的值）赋值给 second
    second=temp;

    printf("After swapping, first = %d\n", first);
    printf("After swapping, second = %d\n", second);
    return 0;
}
```

# Output

Enter first number: 5
Enter second number: 8

After swapping, first = 8
After swapping, second = 5

## 实验编程

## 8. 编写一个 C 程序检查数字是偶数还是奇数。

```c
#include<stdio.h>
int main(){
int num;
printf("Enter integer: ");
scanf("%d",&num);

// 如果 num 能被 2 整除则为真
if(num%2==0)
printf("%d is even.",num);
else
printf("%d is odd.",num);

return 0;
}
```

Output
Enter integer: -7
-7 is odd.

## 9. 编写一个 C 程序使用三元运算符检查奇数或偶数。

```c
#include<stdio.h>
int main(){
int num;
printf("Enter integer: ");
scanf("%d",&num);

(num%2==0)?printf("%d is even.",num):printf("%d is odd.",num);
return 0;
}
```

Output
Enter integer: 33
33 is odd.

## 10. 编写一个 C 程序检查字符是否是元音或辅音。

```c
#include<stdio.h>
int main(){
char c;
int lowercase, uppercase;
printf("Enter alphabet: ");
scanf("%c",&c);

// 如果 c 是小写则为真
lowercase=(c=='a'||c=='e'||c=='i'||c=='o');

// 如果 c 是大写则为真
uppercase=(c=='A'||c=='E'||c=='I'||c=='O');

if(lowercase || uppercase)
    printf("%c is a vowel.", c);
else
    printf("%c is a consonant.", c);

return 0;
}
```

Output
Enter alphabet: G
G is a consonant.

## **11. 编写一个 C 程序找到三个数字中的最大值。**

```c
#include <stdio.h>
int main() {
    int n1, n2, n3;
    printf("Enter three numbers: ");
    scanf("%d %d %d", &n1,&n2,&n3);

    if (n1 >= n2 && n1 >= n3)
        printf("%d is the largest.", n1);
    else if (n2 >= n1 && n2 >= n3)
        printf("%d is the largest.", n2);
    else
        printf("%d is the largest.", n3);

    return 0;
}
```

Output
Enter three numbers: 4 7 3
7 is the largest.

## 12. 编写一个 C 程序检查闰年。

```c
#include <stdio.h>
int main(){
int year;
scanf("%d", &year);

if((year%4==0 && year%100!=0) || (year%400==0))
    printf("%d is a leap year.", year);
else
    printf("%d is not a leap year.", year);

return 0;
}
```

## 13. 编写一个 C 程序检查字符是否为字母。

```c
#include <stdio.h>
int main(){
char c;
printf("Enter a character: ");
scanf("%c",&c);

 if((c>='a' && c<='z')||(c>='A' && c<='Z'))
    printf("%c is an alphabet.", c);
else
    printf("%c is not an alphabet.", c);

 return 0;
}
```

Output
Enter a character: *
* is not an alphabet

## 14. 编写一个 C 程序计算前 'n' 个自然数的和。

```c
#include <stdio.h>
int main(){
int n, i, sum=0;
printf("Enter a positive integer: ");
scanf("%d",&n);
i=1;

while(i <= n){
sum+= i;
i++;
}
printf("Sum = %d", sum);
return 0;
}
```

Output
Enter a positive integer: 100
Sum = 5050

## 15. 编写一个 C 程序找到数字的阶阶。

```c
#include <stdio.h>
int main(){
int n, i;
unsigned long long fact =1;
printf("Enter an integer: ");
scanf("%d",&n);

// 如果用户输入负整数则显示错误
if(n<0)
printf("Error! Factorial of a negative number doesn't exist.");
else
for(i=1; i <= n;++i){
fact*= i;
}
printf("Factorial of %d = %lu", n, fact);

return 0;
}
```

Output
Enter an integer: 10
Factorial of 10 = 3628800

## 16. 编写一个 C 程序生成给定数字的相法表。

```c
#include <stdio.h>
int main(){
int n, i;
printf("Enter an integer: ");
scanf("%d",&n);
for(i=1; i<=10; i++){
    printf("%d * %d = %d\n", n, i, n*i);
}
return 0;
}
```

Output
Enter an integer: 9
9 * 1 = 9
9 * 2 = 18
9 * 3 = 27
9 * 4 = 36
9 * 5 = 45
9 * 6 = 54
9 * 7 = 63
9 * 8 = 72
9 * 9 = 81
9 * 10 = 90

## 17. 编写一个 C 程序显示前 ‘n’ 个数字的斐波那契序列。

```c
#include<stdio.h>
int main(){
int i, n, t1 =0, t2 =1,nextnum;
printf("Enter the number of terms: ");
scanf("%d",&n);
printf("Fibonacci Series: %d", t1);

for(i=1; i<n; i++){
    nextnum = t1 + t2;
    t1 = t2;
    t2 = nextnum;
    printf(", %d", t1);
}
return 0;
}
```

