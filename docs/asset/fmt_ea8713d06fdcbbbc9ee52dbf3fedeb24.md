
更进一步，你可以将使用声明收集在命名空间中：

```cpp
// mynames - 头文件

#include <iostream>
```
```cpp
namespace io
```
  using std::cin;
  using std::cout;
  using std::endl;
}
```
```cpp
namespace formats
```
```cpp
{
```
[PAGE 1347]
```cpp
using std::fixed;
using std::scientific;
using std::boolalpha;
}
```

那么程序就可以包含此文件并使用它需要的命名空间：
`#include "mynames"`
`using namespace io;`

## 使用 STL

STL（详见第 16 章和附录 G，“STL 方法和函数”）为许多编程需求提供了现成的解决方案，因此你应该使用它。例如，与其声明一个 `double` 或 `string` 对象的数组，不如创建一个 `vector<double>` 对象或 `vector<string>`。其优点与使用对象代替 C 风格字符串的优点相似。它定义了赋值操作，因此你可以使用赋值运算符将一个 `vector` 对象赋值给另一个。你可以通过引用传递 `vector`，接收此类对象的函数可以使用 `size()` 方法来确定 `vector` 对象中元素的数量。内置的内存管理允许你在使用 `push_back()` 方法向 `vector` 对象中添加元素时自动对其大小进行调整。当然，，它还有许多实用的类方法和通用算法供你使用。在 C++11 中，如果固定大小的数组更合适，请使用 `array<double>` 或 `array<string>`。

如果你需要列表（`list`）、双端队列（`deque`）、栈（`stack`）、普通队列、集合（`set`）或映射（`map`），STL 提供了这些模板。算法库的设计让你能够轻松地将 `vector` 的内容复制到 `list`，或者将 `set` 的内容与 `vector` 进行比较。这种设计使得 STL 成为一个工具箱，提供了你可以根据需要组装的各种单元。

广泛的算法库以效率设计为主要设计目标之一，因此你只需付出较少的编程努力就能获得顶尖的结果。而实现算法时使用的迭代器概念意味着，算法并不限于用于 STL 容器。特别是，它们也可以应用于传统的数组。

## 章节练习答案

### 第 2 章章节练习答案

1. 它们被称为函数。
2. 它导致在最终编译之前，将 `iostream` 文件的内容替换为该指令。
3. 它让 `std` 命名空间中的定义对程序可用。
4. `cout << "Hello, world\n"` 或 `cout << "Hello, world" << endl;`
5. `int cheeses;`
6. `cheeses = 32;`
7. `cin >> cheeses;`
8. `cout << "We have " << cheeses << " varieties of cheese\n";`
9. 函数 `froop()` 期望接收一个类型为 `double` 的参数，并且该函数返回一个类型的值。例如，可以这样使用：
```cpp
int gval = froop(3.14159);
```
函数 `rattle` 没有返回值并期望接收一个 `int` 参数。例如，可以这样使用：
```cpp
rattle(37);
```
函数 `prune()` 返回一个 `int` 并期望在不带参数的情况下使用。例如，可以这样使用：
```cpp
int residue = prune();
```
10. 当函数的返回类型为 `void` 时，你不需要在函数中使用 `return`。但是，如果你不提供返回值，也可以使用它：
```cpp
return;
```

### 第 3 章章节练习答案

1. 拥有多个整数类型允许你选择最适合特定需求的类型。例如，你可以使用 `short` 来节省空间，使用 `long` 来保证存储容量，或者发现某种特定类型可以加速特定的计算。

2.
```cpp
short rbis = 80; // 或 short rbis = 80;
unsigned int q = 42110; // unsigned int q = 42110;
unsigned long ants = 3000000000;
// long long ants = 3000000000;
```
注意：不要指于 `int` 足够容纳 3,000,000,000。如果你的系统支持通用列表初始化，你可以使用它：
```cpp
short rbis = {80}; // 可选
unsigned int q = {42110}; // 可以使用 = {42110}
long long ants = {3000000000};
```

3. C++ 没有提供自动保护机制来防止你超过整数限制；你可以使用 `limits` 头文件来确定限制具体是多少。

4. 常量 `33l` 是 `long` 类型，而常量 `33` 是 `int` 类型。

5. 这两个语句并不真正等价，尽管它们在某些系统上的效果相同。最重要的是，第一条语句仅在使用 ASCII 编码的系统中将字母 A 赋值给 `grade`，而第二条语句适用于其他编码。65 是 `int` 类型，而 'A' 是 `char` 类型。

6. 这里有四种方法：
```cpp
char c = 88;
cout << c << endl; // char 类型打印为字符
cout.put(char(88)); // put() 将 char 打印为字符
cout << char(88) << endl; // 新式类型转换将值转为 char
cout << (char)88 << endl; // 旧式类型转换将值转为 char
```
答案取决于这两种类型的大小。如果 `long` 是 4 字节，则没有损失。那时 `long` 的最大值大约是 20 亿，即 10 位数字。因为 `double` 提供了至少 13 位有效数字，因此不需要舍入。另一方面，`long long` 类型可以达到 19 位，这超过了范围。

7.
```cpp
int i = 3.5;
double d = 3.5;
```
8.
```cpp
char c = 88;
cout << c << endl; // char 类型打印为字符
cout.put(char(88)); // put() 将 char 打印为字符
cout << char(88) << endl; // 新式类型转换将值转为 char
cout << (char)88 << endl; // 旧式类型转换将值转为 char
```
9.
```cpp
int gval = froop(3.14159);
```
函数 `rattle` 没有返回值并期望接收一个 `int` 参数。例如，可以这样使用：
```cpp
rattle(37);
```
10.
```cpp
return;
```

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

- a. `weight >= 115 && weight <= 125`
b. `ch == 'q' || ch == 'Q'`
c. `x % 2 == 0 && x != 26`
d. `x % 2 == 0 && (x % 26 == 0)`
e. `donation >= 1000 && donation <= 2000 || guest == 1`
f. `(ch >= 'a' && ch <= 'z') || (ch >= 'A' && ch <= 'Z')`

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

# 1346 附录 J 章节习题答案

接下来，新的 `fill()` 应该是这样的：
```cpp
void fill(std::array<double, Seasons> & pa) // 已更改
{
    using namespace std;
    for (int i = 0; i < Seasons; i++)
    {
        cout << "Enter " << Snames[i] << " * expenses: ";
        cin >> pa[i]; // 已更改
    }
}
```
注意 `(*pa)[i]` 变为更简单的 `pa[i]`。

最后，`show()` 的唯一变化是函数头：
`void show(std::array<double, Seasons> & da)`

- 6. 这可以通过为第二个参数设置默认值来实现：
  `double mass(double d, double v = 1.0);`
  它也可以通过函数重载来实现：
  `double mass(double d, double v);`
  `double mass(double d);`

- b. 你不能为返回值使用默认值，因为必须从右到左提供默认值。你可以使用重载：
  `void repeat(int times, const char * str);`
  `void repeat(const char * str);`

- c. 你可以使用函数重载：
  `int average(int a, int b);`
  `double average(double x, double y);`

- d. 你不能这样做，因为两个版本的签名将相同。

- 7.
```cpp
template<class T>
T max(T t1, T t2) // 或 max(const T & t1, const T & t2)
{
    return t1 > t2 ? t1 : t2;
}
```

- 8.
```cpp
template<> box max(box b1, box b2)
{
    return b1.volume > b2.volume ? b1 : b2;
}
```

# 1347 第 9 章节习题答案

9. `v1` 是 `float` 类型，`v2` 是 `float` 类型，`&v3` 是 `float &` 类型，`v4` 是 `int` 类型，`v5` 是 `double` 类型。字面量 `2.0` 是 `double` 类型，所以乘积 `2.0 * m` 是 `double` 类型。

# 第 9 章节习题答案

- a. `homer` 自动是一个原子变量。
- b. `secret` 应该在一个文件中定义为外部变量，并在另一个文件中使用 `extern` 进行声明。
- c. `topsecret` 可以在在外部定义前加上 `static` 关键字，将其定义为具有内部链接的静态变量。或者也可以将其定义在匿名命名空间中。
- d. `beencelled` 应该通过在函数中的声明前加上 `static` 关键字来定义为局部变量。

- 2. `using` 声明（declaration）使命名空间中的单个名称可用，其作用域与该声明所在的声明区域对应。`using` 指令（directive）使命名空间中的所有名称可用。当你使用指令时，就好像包含该 `using` 声明和命名空间区域的最小声明区域内声明了这些名称。

- 3.
```cpp
#include <iostream>
int main() 
{
    double x;
    std::cout << "Enter value: ";
    while (!(std::cin >> x))
    {
        std::cout << "Bad input. Please enter a number: ";
```
