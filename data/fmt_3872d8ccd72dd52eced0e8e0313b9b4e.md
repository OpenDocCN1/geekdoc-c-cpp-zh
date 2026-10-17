
#include <iostream>

int main() {

    int sum = 0, val = 1;

    // 只要 val 小于或等于 10，就执行 while

    while (val <= 10) {

        sum += val; // 将 sum + val 赋值给 sum

        // val 加 1

    }

    std::cout << "Sum of 1 to 10 inclusive is "

              << sum << std::endl;

    return 0;

}
```
```cpp
// 只要 val 小于或等于 10，就执行 while
while (val <= 10) {
    sum += val; // 将 sum + val 赋值给 sum
    // val 加 1
}
```
```cpp
{
    sum += val; // 将 sum + val 赋值给 sum
    // val 加 1
}
```
```cpp
std::cout << "Sum of 1 to 10 inclusive is "
      << sum << std::endl;
```
```cpp
sum = sum + val;
#include <iostream>
int main() {
    int sum = 0;
    // 从 1 到 10 的数值
    for (int val = 1; val <= 10; ++val)
        sum += val; // 等同于 sum + val
```
```cpp
std::cout << "Sum of 1 to 10 inclusive is "
      << sum << std::endl;
```
```cpp
return 0;
    for (int val = 1; val <= 10; ++val)
        sum += val; // 等同于 sum + val
        int sum = 0;
        for (int i = -100; i <= 100; ++i)
            sum += i;
```
```cpp
#include <iostream>
int main() {
    int sum = 0;
    // 读取到文件结束，计算所有读取到的数值的运行总和
    while (std::cin >> value)
        sum += value; // 等同于 sum + value
    std::cout << "Sum is: "
          << sum << std::endl;
    return 0;
}
```

![](img/3a7e14b77396239ca7166fc2adb32975_1229_0.png)
```cpp
// 错误：main 的参数列表中缺少 )
int main( {
    // 错误：endl 之后使用了冒号：而非分号
    std::cout << "Read each file." << std::endl;
    // 错误：字符串字面量周围缺少引号
    std::cout << Update master. << std::endl;
    // 错误：缺少第二个输出运算符
    std::cout << "Write new master." << std::endl;
    // 错误：return 语句缺少 ;
    return 0
}
```
```cpp
#include <iostream>
int main() {
    int v1 = 0, v2 = 0;
    std::cin >> v1 >> v2; // 错误：使用了 "v" 而不是 "v1"
    // 错误：cout 未定义；应该使用 std::cout
    std::cout << v1 + v2 << std::endl;
    return 0;
}
```
```cpp
#include <iostream>
int main() {
    // currVal 是我们要计数的数字；我们将新值读入 val
    int currVal = 0, val = 0;
    // 读取第一个数字并确保我们有数据要处理
    if (std::cin >> currVal) { // 存储当前正在处理数值的计数
        int cnt = 1;
        while (std::cin >> currVal) { // 读取剩余数字
            if (val == currVal) { // 如果数值相同
                cnt++; // cnt 加 1
            } else { // 否则，打印上一个数值的计数
                std::cout << currVal << " occurs " << cnt << " times" << std::endl;
            }
            currVal = val; // 记住新值
            cnt = 1; // 重置计数器
        } // while 循环在此结束
        // 记得打印文件中最后一个数值的计数
        std::cout << currVal << " occurs " << cnt << " times" << std::endl;
    } // 最外层的 if 语句在此结束
    return 0;
}
```
```cpp
if (std::cin >> currVal) {
    //...
} // 最外层的 if 语句在此结束

if (val == currVal) // 如果数值相同
    ++cnt; // cnt 加 1.
} else { // 否则，打印上一个数值的计数
    std::cout << currVal << " occurs "
    << cnt << " times" << std::endl;
    currVal = val; // 记住新值
    cnt = 1; // 重置计数器
}
```
```cpp
#include <iostream>
#include "Sales_item.h"
int main() {
    Sales_item book;
    // 写入 book;
    // 写入 ISBN、销售数量和销售价格
    std::cin >> book;
    // 写入 ISBN、销售数量、总收入和平均价格
    std::cout << book << std::endl;
    return 0;
}
```
```cpp
#include <iostream>
#include "Sales_item.h"
int main() {
    Sales_item item1, item2;
    std::cin >> item1 >> item2;
    std::cout << item1 + item2 << std::endl; // 打印它们的和
    return 0;
}
```
```cpp
#include <iostream>
#include "Sales_item.h"
int main() {
    Sales_item item1, item2;
    std::cin >> item1 >> item2;
    // 检查 item1 和 item2 是否表示同一本书
    if (item1.isbn() == item2.isbn()) {
        std::cout << item1 << " + " << item2 << std::endl;
    } else {
        std::cerr << "Data must refer to ISBN" << std::endl;
        return -1;
    }
}
```
```cpp
#include <iostream>
#include "Sales_item.h"

int main() {
    Sales_item total; // 用于持有下一个交易
    // 读取第一个交易并确保有数据处理
    if (std::cin >> total) {
        Sales_item trans; // 用于持有运行总和
        while (std::cin >> trans) {
            // 如果仍在处理同一本书
            if (total.isbn() == trans.isbn()) {
                total += trans; // 更新运行总和
            } else {
                // 打印之前的书籍
                std::cout << total << std::endl;
                total = trans; // total 现在指向下一本书
            }
        }
        std::cout << total << std::endl; // 打印最后一个交易
    } else {
        // 无输入！
        std::cerr << "No data?" << std::endl;
        return -1;
    }
    return 0;
}
```
```cpp
bool b = 42;
int i = b;
i = 3.14;
double pi = i;
signed char c = -1;
signed char c2 = 256;
int i = 42;
if (i) { // 条件为真
    unsigned u = 0;
    std::cout << u - i << std::endl; // 打印 -84
}
unsigned u = 10;
std::cout << u + i << std::endl; // 如果是 32 位整数，429467296
unsigned ul = 42;
std::cout << ul - u << std::endl; // OK：结果为 32
std::cout << u - ul << std::endl; // OK：但结果会溢出
for (int i = 10; i > 0; --i) // 注意：u 永远小于小于0；条件始终成立
for (unsigned u = 10; u >= 0; --u)
std::cout << u << u << std::endl;
```
```cpp
unsigned u = 11; // 循环第一个元素
while (u > 0) {
    // 先递减，以便最后一次迭代打印 0
    --u;
    std::cout << u << std::endl;
}
```
```cpp
unsigned u = 10, u2 = 42;
std::cout << u2 - u << std::endl;
std::cout << u - u2 << std::endl;
```
```cpp
int i = 10, i2 = 42;
std::cout << i2 - i << std::endl;
std::cout << i - u << std::endl;
std::cout << u - i << std::endl;
```
```cpp
double decimal = 0.25; float f = 0x14; /* 十六进制 */
'3.14159' = 0.001 // 字符字面量
```
```cpp
/* 多行字符串字面量 */
"Hello!" // 字符串字面量
std::cout << "a really, really long string" << std::endl;
"that spans two lines" << std::endl; // 打印换行
```
```cpp
std::cout << '\tHi!'; // 打印制表符后 "Hi!" 和换行
7 (响铃) 12 (换行) 40 (空格)
0 (空) 64 (x);
std::cout << "\u0048Hi\n"; // 打印 Hi 后换行
std::cout << '\u115'; // 打印后换行
```
```cpp
L'a' // 宽字符字面量，类型为 char_t
u8'115' // 8 位 utf-8 编码字符
42ULL // 无符号整数字面量，类型为 unsigned long long
1E-35 // 单精度浮点字面量，类型为 float
3.14159L // 精度浮点字面量，类型为 double
```
```cpp
int sum = 0, value; // sum, value 和 units_sold 类型为 int
units_sold = 0; // sum 和 units_sold 初始值为 0
```
```cpp
Sales_item item; // 类型为 Sales_item (15.1 (p. 20))
string 是一个库类型，表示固定长度的字符序列
std::string book("price"); // 并从字符串字面量初始化
// price 在用于初始化 discount 之前定义并初始化
double price = 10.99, discount = price * 0.16;
// OK 调用 applyDiscount 并返回返回值初始化 salesPrice
double salesPrice = applyDiscount(price, discount);
```
```cpp
long double ld = 3.1415926536; // {1d}; ：需要窄转换
int a(ld), b = ld; // OK 但值会被截断
```
```cpp
std::string empty; // empty 隐式初始化为空字符串
```
```cpp
// 默认初始化的 Sales_item 对象
```
# C++ Primer，第五版
```cpp
extern int i; // 声明但未定义 i
int j; // 声明并定义 j
extern double pi = 3.1416; // 定义
// 定义四个不同的 int 
int intern, someName, SName, SOMENAME;
#include <iostream>
int main()
```
```cpp
    int sum = 0;
    // 累加从 1 到 10（包含边界）的值
    for (int val = 1; val <= 10; ++val)
        sum += val; // 等同于 sum = sum + val
    std::cout << "Sum of 1 through 10 inclusive is "
               << sum << " " << std::endl;

    return 0;
```
```cpp
#include <iostream>
// 仅用于说明目的：函数使用全局变量并定义一个同名的局部变量是不良的风格
int reused = 42; // reused 使用了全局作用域
int main() {
    int unique = 0; // unique 具有块作用域
    // 输出 #1: 使用全局的 reused；打印 42 0
    std::cout << reused << " " << unique << " " << std::endl;

    {
        int reused = 0; // 新的局部对象名为 reused，隐藏了全局的 reused
        // 输出 #2: 使用局部的 reused；打印 0 0
        std::cout << reused << " " << unique << " " << std::endl;
    }
    // 输出 #3: 显式请求全局的 reused；打印 42 0
    std::cout << ::reused << " " << unique << " " << std::endl;

    return 0;
}
```
```cpp
    int i = 100, sum = 0;
    for (int i = 0; i <= 10; ++i)
        sum += i;
    std::cout << i << " " << sum << " " << std::endl;
    int ival = 1024;
    int&refval = ival; // ref 引用（ival 的另一个名字）
    int&ref2; // 错误：引用必须初始化
    refval = 2; // 将 2 赋值给 refval 所引用的对象，即 ival
    refval = 2;
    int ii = refval; // 等同于 ii == ival
    // 正确：ii 绑定到了 refval 所绑定的对象，即 ival
    int&ref3 = refval;
    // 将 i 初始化为 refval 所绑定的对象的值
    int i = refval; // 正确：将 i 初始化为与 ival 相同的值
    int i1 = 1024, i2 = 2048; // i1 和 i2 都是 int
```
```cpp
int& r = i, r2 = 12; // r 是绑定到 i 的引用；r2 是一个 int
int i13 = 1024, &i13 = i13; // i13 是一个 int；i13 是一个绑定到 i13 的引用
int&r3 = 13, &r4 = 12; // r3 和 r4 都是引用
```
