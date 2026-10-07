

## 使用 STL

STL（详见第 16 章和附录 G，“STL 方法和函数”）为许多编程需求提供了现成的解决方案，因此你应该使用它。例如，与其声明一个 double 或 string 对象的数组，不如创建一个 `vector<double>` 对象或 `vector<string>`。其优点与使用对象代替 C 风格字符串的优点相似。它定义了赋值操作，因此你可以使用赋值运算符将一个 vector 对象赋值给另一个。你可以通过引用传递 vector，接收此类对象的函数可以使用 `size()` 方法来确定 vector 对象中元素的数量。内置的内存管理允许你在使用 `push_back()` 方法向 vector 对象中添加元素时自动对其大小进行调整。当然，，它还有许多实用的类方法和通用算法供你使用。在 C++11 中，如果固定大小的数组更合适，请使用 `array<double>` 或 `array<string>`。

如果你需要列表（list）、双端队列（deque）、栈（stack）、普通队列、集合（set）或映射（map），STL 提供了这些模板。算法库的设计让你能够轻松地将 vector 的内容复制到 list，或者将 set 的内容与 vector 进行比较。这种设计使得 STL 成为一个工具箱，提供了你可以根据需要组装的各种单元。

广泛的算法库以效率设计为主要设计目标之一，因此你只需付出较少的编程努力就能获得顶尖的结果。而实现算法时使用的迭代器概念意味着，算法并不限于用于 STL 容器。特别是，它们也可以应用于传统的数组。

## 章节练习答案

### 第 2 章章节练习答案

1. 它们被称为函数。
2. 它导致在最终编译之前，将 iostream 文件的内容替换为该指令。
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

