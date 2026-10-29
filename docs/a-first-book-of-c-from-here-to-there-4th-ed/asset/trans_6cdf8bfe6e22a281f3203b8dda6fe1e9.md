

## 练习 4.4

```
1. switch (letterGrade)
{
    case 'A':
        cout << "The numerical grade is between 90 and 100";
        break;
    case 'B':
        cout << "The numerical grade is between 80 and 89.9";
        break;
    case 'C':
        cout << "The numerical grade is between 70 and 79.9";
        break;
    case 'D':
        cout << "How are you going to explain this one?";
        break;
    default:
        cout << "Of course I had nothing to do with the grade.";
        cout << "\nIt must have been the professor's fault.";
}
```

7. switch 语句中的表达式必须求值为整数量并进行相等性测试。程序 4.5 中的 if-else 链比较的是双精度值，违反了 switch 语句对整数关系表达式的要求。

## 第 5 章

### 练习 5.1

+   3. a. 显示了 21 个数字，其中 1 是第一个，21 是最后一个。
+      b. 参见解决方案文件 pgm5-1ex3.cpp。
+      c. 仍会打印 21 个数字，但第一个数字将是 0，最后一个将是 20。

### 练习 5.2

+   5. a. 是的，程序得出了正确的结果，因为在循环的最后一次迭代中，它对最终总和取平均值。
+      b. 将平均值计算放在循环之外更好，因为程序只执行一次计算，而不是每次循环执行时都执行。

### 练习 5.3

+   1. a. for(i = 1; i <= 20; i++)
+   b. for(icount = 1; icount <= 20; icount = icount + 2)
+   c. for(j = 1; j <= 100; j = j + 5)
+   d. for(icount = 20; icount >= 1; icount--)
+   e. for(icount = 20; icount >=1; icount = icount - 2)
+   f. for(count = 1.0; count <= 16.2; count = count + 0.2)
+   g. for(xcnt = 20.0; xcnt >= 10.0; xcnt = xcnt - 0.5)

+   2. a. 20    e. 10
+   b. 10    f. 77
+   c. 20    g. 21
+   d. 20

+   3. a. 10    d. -5
+   b. 1024   e. 40320
+   c. 75     f. 0.03125

## 第 6 章

### 练习 6.1

+   1. a. 需要一个 int 值
+   b. 需要按此顺序提供三个值：一个 int 和两个 doubles
+   c. 需要按此顺序提供三个值：一个 int 和两个 doubles
+   d. 需要按此顺序提供三个值：一个 char 和两个 floats
+   e. 需要两个 doubles
+   f. 需要按此顺序提供六个值：两个 ints、两个 chars 和两个 doubles
+   g. 需要按此顺序提供四个值：两个 ints 和两个 chars

```
2. a. void check(int num1, double num2, double num3)
{
    cout << "In check()\n";
    cout << "The value of num1 is " << num1 << endl;
    cout << "The value of num2 is " << num2 << endl;
    cout << "The value of num3 is " << num3 << endl;
    return;
}
```

```
3. a. void findAbs(double number)
{
    cout << "The absolute value of " << number << " is: ";
    if(number < 0)
        number = -number;
    cout << number << endl;
    return;
}
```

### 练习 6.2

+   2. a. void check(int num1, float num2, double num3)
+      b. double findAbs(double x)
+      c. float mult(float first, float second)
+      d. int square(int number)
+      e. int powfun(int num, int exponent)
+      f. void table(void) or void table()

```
3. a. double rightTriangle(double a, double b)
{
    return sqrt((a * a) + (b * b));
}
b. See solution file pgm6-2cx3b.cpp.
```

```
4. a. double findAbs(double number)
{
    if(number < 0)
        number = -number;
    return number;
}
b. See solution file pgm6-2cx4b.cpp.
```

### 练习 6.3

+   1. a. doubles amount
+      b. doubles price
+      c. ints minutes
+      d. chars key
+      e. doubles yield

```
2. void time(int& sec, int& min, int& hours)
```

```
3. a. void findMax(int x, int y, int& max)
{
    int maxnum;            // variable declaration

    if (x >= y)            // find the maximum number
        maxnum = x;
    else
        maxnum = y;
    max = maxnum;

    return;                // return statement
}
```

### 练习 6.4

1. a.

| 变量或常量名称 | 数据类型 | 作用域 |
|---|---|---|
| PRICE | int | 对 main()、roi() 和 step() 全局 |
| YEARS | long int | 对 main()、roi() 和 step() 全局 |
| YIELD | double | 对 main()、roi() 和 step() 全局 |
| bondtype | int | main() 局部 |
| interest | double | main() 局部 |
| coupon | double | main() 局部 |
| mat1 | int | roi() 局部 |
| mat2 | int | roi() 局部 |
| count | int | roi() 局部 |
| effectiveRate | double | roi() 局部 |
| first | double | step() 局部 |
| last | double | step() 局部 |
| numofyrs | int | step() 局部 |
| fracpart | double | step() 局部 |

| 变量或常量名称 | 数据类型 | 作用域 |
|---|---|---|
| KEY | char | 对 `main()`、`func1()` 和 `func2()` 全局 |
| NUMBER | long int | 对 `main()`、`func1()` 和 `func2()` 全局 |
| a, b, c | int | `main()` 局部 |
| x, y | double | `main()` 局部 |
| secnum | double | 对 `func1()` 和 `func2()` 全局 |
| num1, num2 | int | `func1()` 局部 |
| o, p | int | `func1()` 局部 |
| q | float | `func1()` 局部 |
| first, last | double | `func2()` 局部 |
| a, b, c, o, p | int | `func2()` 局部 |
| r | double | `func2()` 局部 |
| s, t, x | double | `func2()` 局部 |

3. 所有函数参数在其定义的函数中具有局部作用域。注意，虽然函数参数假定一个取决于调用函数的值，但这些参数在其函数中可以改变值。这使得它们表现得好像是被调用函数中的局部变量一样。

### 练习 6.5

+   1. a. 局部变量可用的存储类别是 `auto`、`static` 和 `register`。
+   
+      b. 全局变量可用的存储类别是 `extern` 和 `static`。局部 auto 变量唯一属于声明它的函数。每次调用函数时，auto 变量都会重新创建，就好像它从未存在过一样。局部 static 变量也唯一属于声明它的函数。然而，static 变量保留其上次的值，并且在再次调用其函数时不会重新创建。

+   2. 第一个函数将 `yrs` 声明为 static 变量并仅在函数编译时一次将其赋值为 1。此后每次调用函数时，`yrs` 中的值都会增加 2。第二个函数也将 `yrs` 声明为 static，但每次调用时都将其赋值为 1，并且函数结束后的 `yrs` 值将始终为 3。通过每次调用时将 `yrs` 的值重置为 1，第二个函数违背了将变量声明为 static 的目的。

## 第 7 章

### 练习 7.1

+   1. a. const int SIZE = 100;
+      int grades[SIZE];
+   b. const int SIZE = 50;
+      double temp[SIZE];
+   c. const int SIZE = 30;
+      char code[SIZE];
+   d. const int SIZE = 100;
+      int year[SIZE];

+   2. a. grades[0] 指数组中存储的第一项，grades[2] 指第三项，grades[6] 指第七项。
+      b. prices[0] 指数组中存储的第一项，prices[2] 指第三项，prices[6] 指第七项。
+      c. amounts[0] 指数组中存储的第一项，amounts[2] 指第三项，amounts[6] 指第七项。

+   3. a. cin >> grades[0];
+      cin >> grades[2];
+      cin >> grades[6];
+   b. cin >> prices[0];
+      cin >> prices[2];
+      cin >> prices[6];
+   c. cin >> amounts[0];
+      cin >> amounts[2];
+      cin >> amounts[6];

### 练习 7.2

+   1. a. const int SIZE = 10;
+      int grades[SIZE] = {89, 75, 82, 93, 78, 95, 81, 88, 77, 82};
+   b. const int SIZE = 5;
+      double amounts[SIZE] = {10.62, 13.98, 18.45, 12.68, 14.76};
+   c. const int SIZE = 100;
+      double rates[SIZE] = {6.29, 6.95, 7.25, 7.35, 7.40, 7.42};
+   d. const int SIZE = 64;
+      double temps[SIZE] = {78.2, 69.6, 68.5, 83.9, 55.4, 67.0, 49.8, 58.3, 62.5, 71.6};
+   e. const int SIZE = 15;
+      char codes[SIZE] = {'f', 'j', 'm', 'q', 't', 'w', 'z'};

```
6. char goodstr[ ] = "Good Morning";
   char goodstr[ ] = { 'G', 'o', 'o', 'd', ' ', 'M', 'o', 'r', 'n', 'i', 'n', 'g' };
   char goodstr[12] = { 'G', 'o', 'o', 'd', ' ', 'M', 'o', 'r', 'n', 'i', 'n', 'g' };
```

```
7. a. char message1[ ] = "Input the Following Data";
      char message2[ ] = "----------------------";
      char message3[ ] = "Enter the Date: ";
      char message4[ ] = "Enter the Account Number: ";
   b. See solution file pgm7-2ex7b.cpp.
```

### 练习 7.3

```
1. void sortArray(double inArray [500])
      void sortArray(double inArray [ ])

2. char findKey(char select [256])
      char findKey(char select [ ])

3. double prime (double [256])
      double prime (double [ ])
```

### 练习 7.4

```
1. a. const int NUMROWS = 6;
      const int NUMCOLS = 10;
          int val[NUMROWS][NUMCOLS];

   b. const int NUMROWS = 2;
      const int NUMCOLS = 5;
          int val[NUMROWS][NUMCOLS];

   c. const int NUMROWS = 7;
      const int NUMCOLS = 12;
          char val[NUMROWS][NUMCOLS];
```

2. 输出如下：

```
8    16    9    52    3    15    27    6    14    25    2    10
```

