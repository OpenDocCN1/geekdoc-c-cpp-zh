

-   `IntArray` 类还应该包含一个私有数据成员，用于在实例化时存储 `IntArray` 对象的名称。该数据成员应通过调用 `setName()` 成员函数进行初始化。

我将提供一个驱动程序 `iaddr.cpp`，用于演示 `IntArray` 类的使用。驱动程序将分别演示所有操作和错误条件功能。每个测试都将说明正在演示的功能，并使用重载的 `<<` 运算符输出每个数组名称、索引和相应的元素。

请注意，对于每个数组测试数据，驱动程序将在每个数组初始化或修改后，，直接将数组索引乘以 10 并输出其内容。当你的程序遇到运行时错误时，你应该使用适当的诊断信息“模拟”停止，而不是实际上停止程序。确保所有发送到终端窗口的错误信息也发送到 `csis.txt` 文件中。

当输出数组元素时，应该输出数组名称、左括号、索引值、右括号、等号，最后是值。例如：

```
a[3] = 30
```

请注意，驱动程序沿页面垂直向下输出数组元素。这种行为不应被更改。确保你为 `IntArray` 类包含一个析构函数。驱动程序将包含以下测试：

-   1. 测试用单个整数声明的数组：
```
IntArray a(10);
```

-   2. 测试用两个整数声明的数组，其中一个为负数：
```
IntArray b(-3, 6);
```

-   3. 测试用两个非负整数声明的数组：
```
IntArray c(6, 8);
```

-   4. 测试用两个相同整数声明的数组：
```
IntArray d(5, 5);
```

-   5. 测试未用整数声明的数组：
```
IntArray z;
```

-   6. 测试用另一个 `IntArray` 类型对象声明的数组：
```
IntArray c(6, 8);
IntArray e(c);
```

-   7. 测试将数组赋值给具有不同索引的另一个数组：
```
IntArray f(1, 4);
IntArray g(5, 8);
f = g;
```

-   8. 测试具有不同索引的多次数组赋值：
```
IntArray j(3, 6);
IntArray k(6, 9);
IntArray l(1, 4);
j = k = l;
```

-   9. 测试重载的相等运算符（相同元素）：
```
IntArray m(3, 7);
IntArray n(1, 5);
m == n
```

-   10. 测试重载的相等运算符（不同元素）：
```
IntArray o(3, 7);
IntArray p(1, 5);
o == p
```

-   11. 测试重载的相等运算符（不同大小数组）：
```
IntArray q(1, 3);
IntArray r(1, 4);
q == r
```

-   12. 测试重载的不等于运算符（相同元素）：
```
IntArray s(3, 7);
IntArray t(1, 5);
s != t
```

-   13. 测试重载的不等于运算符（不同元素）：
```
IntArray u(3, 7);
IntArray v(1, 5);
u != v
```

-   14. 测试重载的不等于运算符（不同大小数组）：
```
IntArray w(1, 3);
IntArray x(1, 4);
w != x
```

-   15. 将两个数组的和赋值给第三个数组（注意：相应的数组元素会相加并赋值给第三个数组中相应的元素）：
```
IntArray a(1, 5);
IntArray b(4, 8);
IntArray c = a+b;
```

注意 `IntArray c` 应该采用调用者 `IntArray`（a）的索引。16. 将两个数组的和赋值给第一个数组（注意：相应的元素相加并赋值给第一个数组中的相应元素）：
```
IntArray d(10, 13);
IntArray e(30, 33);
d += e;
```

-   17. 测试带有非法边界的数组：
```
IntArray f(5, 2);
```

-   18. 测试索引越界的数组：
```
IntArray g(10);
g[10];
```

-   19. 测试长度不匹配的数组：
```
IntArray m(1, 4);
IntArray n(3, 7);
m = n;
```

-   20. 测试作为左值右值的下标运算符：
```
IntArray o(7, 8);
o[7] = 25;
o[8];
```

运算符重载 (IntArray) 驱动程序

```cpp
// iadrv.h

#ifndef _IADRV_H
#define _IADRV_H

#include "intarray.h"

int main();
void test1();
void test2();
void test3();
void test4();
void test5();
void test6();
void test7();
void test8();
void test9();
void test10();
void test11();
void test12();
void test13();
void test14();
void test15();
void test16();
void test17();
void test18();
void test19();
void test20();
#endif
```

```cpp
// iadrv.cpp - IntArray 的驱动程序

#include <iostream>
#include <iomanip>
#include <fstream>
#include <stdlib.h>
#include "iadrv.h"

using namespace std;

ofstream csis;

int main() {
    csis.open("csis.txt");
    test1();
    test2();
    test3();
    test4();
    test5();
    test6();
    test7();
    test8();
    test9();
    test10();
    test11();
    test12();
    test13();
    test14();
    test15();
    test16();
    test17();
    test18();
    test19();
    test20();
    csis.close();
}

void test1() {
    cout << "1. Array declared with single integer: IntArray a(10);" << endl;
    csis << "1. Array declared with single integer: IntArray a(10);" << endl;
    IntArray a(10);
    for (int i = 0; i <= a.high(); i++) {
        a[i] = i * 10;
    }
    a.setName("a");
    cout << a << endl;
    csis << a << endl;
}

void test2() {
    cout << "2. Array declared with two integers, one of which is negative: IntArray b(-3, 6);" << endl;
    csis << "2. Array declared with two integers, one of which is negative: IntArray b(-3, 6);" << endl;
    IntArray b(-3, 6);
    for (int i = 0; i <= b.high(); i++) {
        b[i] = i * 10;
    }
    b.setName("b");
    cout << b << endl;
    csis << b << endl;
}

void test3() {
    cout << "3. Array declared with two non-negative integers: IntArray c(6, 8);" << endl;
    csis << "3. Array declared with two non-negative integers: IntArray c(6, 8);" << endl;
    IntArray c(6, 8);
    for (int i = 0; i <= c.high(); i++) {
        c[i] = i * 10;
    }
    c.setName("c");
    cout << c << endl;
    csis << c << endl;
}

void test4() {
    cout << "4. Array declared with two identical integers: IntArray d(5, 5);" << endl;
    csis << "4. Array declared with two identical integers: IntArray d(5, 5);" << endl;
    IntArray d(5, 5);
    for (int i = 0; i <= d.high(); i++) {
        d[i] = i * 10;
    }
    d.setName("d");
    cout << d << endl;
    csis << d << endl;
}

void test5() {
    cout << "5. Array declared with no integers: IntArray z;" << endl;
    csis << "5. Array declared with no integers: IntArray z;" << endl;
    IntArray z;
    for (int i = 0; i <= z.high(); i++) {
        z[i] = i * 10;
    }
    z.setName("z");
    cout << z << endl;
    csis << z << endl;
}

void test6() {
    cout << "6. Array declared with another object of type IntArray: IntArray c(6, 8); IntArray e(c);" << endl;
    csis << "6. Array declared with another object of type IntArray: IntArray c(6, 8); IntArray e(c);" << endl;
    IntArray c(6, 8);
    IntArray e(c);
    // 此处省略后续逻辑实现
}

void test7() {
    cout << "7. Array assigned to another array with different indices: IntArray f(1, 4); IntArray g(5, 8); f = g;" << endl;
    csis << "7. Array assigned to another array with different indices: IntArray f(1, 4); IntArray g(5, 8); f = g;" << endl;
    IntArray f(1, 4);
    IntArray g(5, 8);
    f = g;
    // 此处省略后续逻辑实现
}

// ... 后续测试函数实现
```

