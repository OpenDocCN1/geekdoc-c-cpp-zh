
```cpp
x=x+y      // x = x+y
++x       // 增增：x = x+1
-=y       // x = x-y
--x       // 减：x = x-1
*=y       // 缩放：x = x*y
/=y       // 缩放：x = x/y
%=y       // x = x%y
```

### 1.4.2 初始化

在对象对象之前，必须给它赋一个值。C++ 提供了多种初始化符号，例如：

- 拷贝初始化：`int i = value;`

- 直接初始化：`int i(value);`

- 列表初始化（C++11 及以后）：`int i{value};`

列表初始化在现代 C++ 中通常是首的，因为它为所有类型提供了统一的接口并防止窄转换。

```cpp
int i = 5;   // 拷贝初始化
int j(5);    // 直接初始化
int k{5};    // 列表初始化
```

列表初始化也可用于数组和结构体：

```cpp
int arr[] = {1, 2, 3, 4, 5};
struct Point {
  int x;
  int y;
};
Point p{10, 20}; // 列表初始化
```

如果变量没有初始化，它将包含一个不确定的值。访问未初始化的局部变量会导致未定义行为。在声明处初始化变量是一个良好的习惯，可以避免此类错误。

```cpp
int i;      // i 未初始化
i = 5;      // i 现在被初始化为 5
int j = 0; // j 被初始化为 0
```

## 10 基础

## 第 1 章

```cpp
struct Record {
  string name; // name 是 Record 的名称（一个字符串成员）
  int id; // ...
};
```

一个对象在在使用之前必须被构造（初始化），并且在它的作用域结束时必须销毁。对于命名空间对象，析毁点是程序的结束。对于成员，其析毁点取决于其所属对象的析毁点。通过 `new` 创建的对象将一直“存活”直到被 `delete` 销毁为止（§5.2.2）。

## 1.6 常数

C++ 支持两种不可变性（状态不可改变的对象）的概念：

- `const`：意味着“我承诺不改变此值”。这主要用于指定接口，以便数据可以通过指针和引用传递而防止被修改。编译器通过 `const` 强制这一承诺。`const` 的值可以在运行时计算。

- `constexpr`：大致意味着“在编译时求值”。这主要用于指定常量、将数据放置在只读内存中（那里不太可能被损坏）以及为了性能。`constexpr` 的值必须由编译器计算。

例如：

| constexpr int dmv = 17; | dmv 是一个命名常量 |

| int var = 17; | var 不是一个常量 |

| const double sqv = sqrt(var); | sqv 是一个命名常量，可能在运行时计算 |

| double sum(const vector<double>&); | sum 不修改其参数 (§1.7) |

| vector<double> v={1, 2, 3, 4}; | v 不是一个常量 |

| const double s1 = sum(v); | OK：sum(v) 在运行时求值 |

| constexpr s2 = sum(v); | 错误：sum(v) 不是常量表达式 |

为了使一个函数能够在常量表达式中使用（即能够让编译器求值），它必须定义为 `constexpr` 或 `constval`。例如：

```cpp
constexpr double square(double x) { return x * x; }
```

| constexpr double max1=1.4-square(17); | OK：1.4 是常量表达式 |

| constexpr double max2=1.4-square(var); | 错误：var 不是常量，square(var) 不是常量 |

| const double max3=1.4-square(var); | OK：可能在运行时求值 |

`constexpr` 函数可以用于非常量参数，但当这样做时，结果不是常量表达式。我们允许在不需要常量表达式的语境中使用非常量表达式参数调用 `constexpr` 函数。这样，我们就不需要定义两个本质上相同的函数：一次用于常量表达式，一次用于变量。当我们希望一个函数用于编译时求值时，我们将其声明为 `constval` 而不是 `constexpr`。例如：

```cpp
constval double square(double x) { return x*x; }
```

```cpp
constexpr double max1 = 1.4*square(17);
const double max3 = 1.4*square(var); // OK：1.4*square(17) 是常量表达式
// 错误：var 不是常量
```

声明为 `constexpr` 或 `constval` 的函数是 C++ 中对纯函数的概念实现。它们不能有副作用，只能使用作为参数传递给它们的信息。特别是，它们可以修改非局部变量，但可以使用自己的局部变量。例如：

```cpp
constexpr double nth(double x, int n) // 假设 0=n
double res = 1;
int i = 0;
while (i < n) { // while循环：当条件为真时执行 (§1.7.1)
    res += x;
    i++;
}
return res;
```

在某些地方，语言规则要求常量表达式（例如数组边界 (§1.7)、分支标签 (§1.8)、模板值参数 (§7.2) 以及使用 `constexpr` 声明的常量）。在其他情况下，编译时求值对性能非常重要。忽略性能问题，不可变性（状态不可改变的对象）的概念是一个重要的设计考虑。

## 1.7 指针、数组和引用

最基础的数据集合是同类型元素的连续分配序列，称为数组。这基本上是硬件所提供的。类型为 `char` 的元素数组可以这样声明：

```cpp
char v[6]; // 一个包含 6 个字符的数组
```

同样地，指针可以这样声明：

```cpp
char *p; // 指向 char 的指针
```

在声明中，`[]` 意味着“……的数组”，`*` 意味着“指向……的指针”。所有数组的下界都是 0，`v` 有六个元素，从 `v[0]` 到 `v[5]`。数组的大小必须是一个常量表达式 (§1.6)。指针可以持有相应类型对象的地址：

```cpp
char *p = &v[3]; // p 指向 v 的第四个元素
char x = *p; // "*p 是 p 指向的对象"
```

在表达式中，一元 `*` 意味着“……的内容”，一元 `&` 意味着“……的地址”。我们可以这样图化地表示它：

![](img/c00e25f90ff6ca6a561)

考虑一个数组：

```cpp
void print()
{
    int v[10] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
    for (int i=0; i<10; ++i)
        cout << v[i] << " ";
    cout << endl;
}
```

`for` 语句可以读作“设置为……”。注意我们不需要拷贝：

```cpp
void print(int v[])
{
    for (int x : v)
        cout << x << " ";
}
```

在声明中，一元后缀 `&` 意味着“……的引用”。引用与指针相似，但你不需要前缀来访问值。

```cpp
void increment(int& i)
{
    i++;
}
```

引用对于指定函数参数特别有用。例如：

```cpp
void sort(vector<double>& v); // v 是一个 vector
```

当我们不想修改参数但仍希望避免拷贝代价时，我们使用 `const` (§1.6)；即，引用。

```cpp
double sum(const vector<double>&);
```

接收引用的函数非常常见。在声明中，运算符 `&`、`*`、`[]` 称为声明符：

```cpp
T[n]          // T[n]: a 是一个含有 n 个元素的数组
T* p           // T*: p 是指向 T 的指针
T& r            // T&: r 是 T 的引用
T(A)          // T(A): f 是一个接收 A 类型参数并返回 T 类型结果的函数
```

### 1.7.1 空指针

我们尽量确保指针始终指向对象，以便解引用是有效的。当我们没有对象可以指向，或者当我们需要表示“无可用对象”的概念（例如列表的末尾），我们赋予值 `nullptr`（“空指针”）。它被所有指针共享：

```cpp
double* pd = nullptr;
Link<Record>* l = nullptr; // 指向 Link 到 Record 的指针
int x = nullptr; // 错误：nullptr 是指针不是整数
```

检查指针是否指向某些内容通常是明智的：

```cpp
int count(const char* p, char x)
// p[] 中 x 出现的次数
// 假设 p 指向一个以零结尾的字符数组（或为空）
{
    if (p==nullptr)
        return 0;
    int count = 0;
    for (; *p !=='\0'; ++p)
        if (*p==x)
            count++;
    return count;
}
```

# 14 基础 第1章

在较旧的代码中，通常使用 0 或 NULL 代替 `nullptr`。然而，使用 `nullptr` 可以消除整数（如 0 或 NULL）与指针（如 `nullptr`）之间潜在的混淆。在 `count_x()` 示例中，我们没有使用 `for` 语句的初始化部分，因此可以使用更简单的 `while` 语句：

```cpp
int count_x(const char* p, char x)
// 统计 x 在 p[] 中出现的次数
// 假设 p 指向一个零结尾的 char 数组（或指向空）
if (p==nullptr)
  return 0;
int count = 0;
while (*p) {
  if (*p==x)
    ++count;
}
return count;
```

`while` 语句会一直执行，直到其条件变为假。

对数值值进行测试（例如 `count_x()` 中的 `while (*p)`）等同于将值与 0 比较（例如 `while (*p)!=0`）。对指针进行测试（例如 `if (p)`）等同于将值与 `nullptr` 比较（例如 `if (!nullptr)`）。

不存在“空引用”。引用必须引用一个有效对象（实现假设了如此）。有晦晦和明显的方法可以违反这一规则；不要这样做。

## 1.8 测试

C++ 提供了一套常规用于选择和循环的语句，例如 `if` 语句、`switch` 语句、`while` 循环和 `for` 循环。例如，这里有一个简单的函数提示用户并返回一个指示布尔值：

```cpp
bool accept() {
  cout << "Do you want to proceed (y or n)?"; // 写入问题
  char answer = 0;                         // 初始化为一个不会出现在输入中的值
  cin >> answer;

  if (answer == 'y')
    return true;
  return false;
}
```

为了匹配 `<<` 输出运算符“置到”，使用 `>>` 运算符“获取”用于输入；`cin` 是标准输入流（第 11 章）。`>>` 右侧操作数的类型决定了接受什么输入，而它的右侧是输入操作的目标。输出字符串末尾的 `\n` 字符代表换行（1.2.1）。

## 1.8 测试 15

注意 `answer` 的定义出现在它需要的地方（而不是在那之前）。声明可以出现在任何语句出现的地方。通过考虑 `n`（代表“no”）答案，该示例可以得到改进：

```cpp
bool accept() {
    cout << "Do you want to proceed (y or n)?\n"; // 写入问题
    char answer = 0; // 初始化为一个不会出现在输入中的值
    cin >> answer; // 读取答案

    switch (answer) {
        case 'y':
            return true;
        case 'n':
            return false;
        default:
            cout << "I'll take that for a no.\n"; 
            return false;
    }
}
```

`switch` 语句将一个值与一组常量进行测试。这些常量被称为 `case-labels`（分支标签），它们必须是唯一的，如果该值不匹配其中任何一个，则选择 `default`。该值不需要通过从包含其 `switch` 语句的函数返回来退出 `case`。通常情况下，我们只想继续执行 `switch` 语句之后的语句。我们可以使用 `break` 语句来实现。例如，考虑一个为简单的命令行视频游戏设计的、过度聪明但原始的解析器：

```cpp
void action() {
    while (true) {
        cout << "enter action:\n"; // 请求动作
        string act; // 将字符读入字符串
        cin >> act;
        Point delta(0,0); // Point 持有一对 {x,y} 对

        for (char ch : act) {
            switch (ch) {
                case 'u': // 向上
                case 'n': // 向北
                    ++delta.y;
                    break;
                case 'r': // 向右
                case 'e': // 向东
                    ++delta.x;
                    break;
            }
        }
        // ... 其他动作 ...
    }
}
```

# 16 基础

# 第1章

```cpp
default:
cout << "I freeze!\n";
move(current+delta);
```

像 `for` 语句（1.7）一样，`if` 语句也可以引入变量并对其进行测试。例如：

```cpp
void do_something(vector<int>& v)
{
    if (auto n = v.size(); n!=0) {
        // ... 到这里
    }
}
```

在这里，整数 `n` 是为 `if` 语句定义的，用 `v.size()` 初始化，并立即被 `n!=0` 条件使用。在条件中声明的名字在 `if` 语句的两个分支上都具有作用域。对于 `for` 语句，在 `if` 语句条件中声明名称的目的是限制变量的作用域，以提高可读性并尽可能地减少错误。最常见的情况是测试变量是否为 0 或 `nullptr`。要做到这一点，只需省略显式的提及。例如：

```cpp
void do_something(vector<int>& v)
{
    if (auto n = v.size()) {
        // ... 到这里
    }
}
```

可能时尽量使用这种更简洁更简单的形式。

## 1.9 映射到硬件
