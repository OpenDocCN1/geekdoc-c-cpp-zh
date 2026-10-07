

# 第 6 章章节复习答案

- 3. 它将输出如下：
0369
12

- 4. 它将输出如下：
6
8

- 5. 它将输出如下：
k = 8

- 6. 使用 `*=` 运算符是最简单的：
```cpp
for (int num = 1; num < 64; num *= 2)
cout << num << " ";
```

- 7. 你将语句封装在成对的大括号内以形成一个单一的复合语句或块。

- 8. 是的，第一个语句是有效的。表达式 `1,024` 包含两个表达式`1` 和 `024`——由逗号运算符连接。值是右侧表达式的值。这个值为 `024`，它是八进制的 20，因此声明将值 20 赋值给 `x`。第二个语句也是有效的。但是，运算符优先级导致它被评估为：
`(y = 1), 024;`

也就是说，左侧表达式将 `y` 设置为 1，而整个表达式的值并没有被使用（`024` 或 20）。

- 9. `cin >> ch` 形式在遇到空格、换行符和制表符时会跳过它们。另外两种形式会读取这些字符。

- 1. 两个版本给出的答案相同，但 `if else` 版本效率更高。考虑一下，例如当 `ch` 是空格时会发生什么。版本 1 在增加空格计数后会进行两次测试，因为程序已经确定了 `ch` 是空格，因此它不可能是换行符。版本 2 在相同情况下会跳过第二次测试。

- 2. `++ch` 和 `ch + 1` 具有相同的数值值。`++ch` 的类型是 `char` 并以字符形式打印，而 `ch + 1` 因为其将一个 `char` 与一个 `int` 相加，所以其类型为 `int` 并以数字形式打印。

由于程序使用了 `ch = '$'` 而不是 `ch == '$'`，组合的输入和输出如下：

```
Hi!
H$!$
$Send $10 or $20 now!
S$e$n$ $ct1 = 9, ct2 = 9
```

每个字符在第二次出现之前都被转换为 `$` 字符。此外，表达式 `ch = $` 的值是 `$` 字符的代码，因此非零，因此为真；所以 `ct2` 每次都会加1。

- a. weight >= 115 && weight <= 125
b. ch == 'q' || ch == 'Q'
c. x % 2 == 0 && x != 26
d. x % 2 == 0 && (x % 26 == 0)
e. donation >= 1000 && donation <= 2000 || guest == 1
f. (ch >= 'a' && ch <= 'z') || (ch >= 'A' && ch <= 'Z')

不一定。。例如，如果 `x` 是 10，那么 `!x` 是 0，而 `!!x` 是 1。然而，如果 `x` 是布尔变量，那么 `!!x` 就是 `x`。

```cpp
(x < 0)? -x : x
```

或
`(x >= 0)? x : -x;`

```cpp
switch (ch)
{
    case 'A': a_grade++;
        break;
    case 'B': b_grade++;
        break;
    case 'C': c_grade++;
        break;
    case 'D': d_grade++;
        break;
    default: f_grade++;
        break;
}
```

如果你使用整数标签而用户输入了如 `q` 等非整数，程序将挂起，因为整数输入无法处理字符。但如果你使用字符标签而用户输入了如 5 等整数，字符输入将处理 5。

# 附录 J 章节复习答案

9. 有一个版本：

```cpp
int line = 0;
char ch;
while (cin.get(ch) && ch != 'Q')
{
    if (ch == '\n')
        line++;
}
```

# 第 7 章章节复习

- 1. 三个步骤是定义函数、提供原型和调用函数。

- 2. a. `void igor(void);` // 或 `void igor()`
   b. `float tofu(int);` // 或 `float tofu(int)`
   c. `double mpg(double miles, double gallons);`
   d. `long summation(long h[], int size);`
   e. `double doctor(const char * str);`
   f. `void ofcourse(boss dude);`
   g. `char * plot(map *pmap);`

- 3. `void set_array(int arr[], int size, int value)`
{
   for (int i = 0; i < size; i++)
   arr[i] = value;
}

- 4. `void set_array(int * begin, int * end, int value)`
{
   for (int * pt = begin; pt != end; pt++)
   pt* = value;
}

- 5. `double biggest(const double foot[], int size)`
{
   double max;
   if (size < 1)
   cout << "Invalid array size of " << size << endl;
   cout << "Returning a value of 0\n";
   return 0;

}
else // 因为 return 会终止程序
{
    max = foot[0];
    for (int i = 1; i < size; i++)
        if (foot[i] > max)
            max = foot[i];
    return max;
}

- 6. 你使用 `const` 修饰符来保护指向的数据不被修改。当程序传递基本类型（如 `int` 或 `double`）时，它是按值传递的，函数处理的是副本。因此，原始数据已经得到了保护。

- 7. 字符串可以存储在字符数组中，可以用双引号字符串常量表示，也可以用指向字符串第一个字符的指针来表示。

- 8. `int replace(char *str, char c1, char c2)`
{
    int count = 0;
    while (*str) // 未到字符串末尾
    {
        if (*str == c1)
        {
            *str = c2;
            count++;
        }
        str++;
    }
    return count;
}

- 10. 按值传递时，使用结构体名称。按地址传递时，使用指针运算符。

- 11. `int judge(const char *);`

- 12. 注意，如果 `ap` 是指针，使用 `ap->` 访问成员。

