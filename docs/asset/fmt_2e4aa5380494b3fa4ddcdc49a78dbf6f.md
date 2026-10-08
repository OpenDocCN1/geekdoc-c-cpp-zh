
# 程序 9.19 Matrix 类的接口文件（续）

| 24 | int rowSize; |
| 25 | int colSize; |
| 26 | int** ptr; |
| 27 | public: |
| 28 | Matrix (int rowSize, int colSize); |
| 29 | ~Matrix(); |
| 30 | void setup(); |
| 31 | void add (const Matrix& second, Matrix& result) const; |
| 32 | void subtract (const Matrix& second, Matrix& result) const; |
| 33 | void multiply (const Matrix& second, Matrix& result) const; |
| 34 | void print () const; |
| 35 | }; |
| 36 | #endif |

实现文件 程序 9.20 显示了实现文件。注意，该成员函数随机填充矩阵，但在实际情况中，我们可以从文件中读取值。

# 程序 9.20 Matrix 类的实现文件

```cpp
/***************************************************
* 我们已经实现了在接口文件中声明的
* 所有成员函数。
* 实现遵循了之前讨论的
* 操作描述。
***************************************************

#include "matrix.h"

Matrix :: Matrix (int r, int c)
    : rowSize(r), colSize(c)
{
    ptr = new int*[rowSize];
    for (int i = 0; i < rowSize; i++) {
        ptr[i] = new int [colSize];
    }
}

// 析构函数：删除堆中的内存位置
Matrix :: ~Matrix ()
{
    for (int i = 0; i < rowSize; i++) {
        delete [] ptr[i];
    }
```
（续）

# 程序 9.20 Matrix 类的实现文件（续）

```cpp
25 }
26 delete []ptr;
27 }
// setup 用 1 到 5 之间的随机值填充单元格。
29 void Matrix :: setup() {
30 {
31 for (int i = 0; i < rowSize; i++) {
32 {
33 for (int j = 0; j < colSize; j++) {
34 {
35 ptr[i][j] = rand() % 5 + 1;
36 }
37 }
38 }
39 // add 函数将 second 加到对象并创建 result。
40 void Matrix :: add(const Matrix& second, Matrix& result) const {
41 {
42 assert(rowSize == rowSize && colSize == colSize);
43 assert(rowSize == rowSize && colSize == colSize);
44 
45 for (int i = 0; i < rowSize; i++) {
46 {
47 for (int j = 0; j < colSize; j++) {
48 {
49 result[i][j] = ptr[i][j] + second[i][j];
50 }
51 }
52 }
53 // subtract 函数从对象中减去 second。
54 void Matrix :: subtract(const Matrix& second, Matrix& result) const {
55 {
56 assert(rowSize == rowSize && colSize == colSize);
57 assert(rowSize == rowSize && colSize == colSize);
58 for (int i = 0; i < rowSize; i++) {
59 {
60 for (int j = 0; j < colSize; j++) {
61 {
62 result[i][j] = ptr[i][j] - second[i][j];
63 }
64 }
65 }
66 // multiply 函数将 second 乘以对象。
67 void Matrix :: multiply(const Matrix& second, Matrix& result) const {
68 {
```
（续）

# 程序 9.20 Matrix 类的实现（续）

```cpp
69 assert(colSize == rowSize);
70 assert(rowSize == rowSize);
71 assert(colSize == colSize);
72 for (int i = 0; i < rowSize; i++) {
73 {
74 for (int j = 0; j < colSize; j++) {
75 {
76 result[i][j] = 0;
77 for (int k = 0; k < colSize; k++) {
78 {
79 result[i][j] += ptr[i][k] * second[k][j];
80 }
81 }
82 }
83 // print 函数打印单元格的值。
84 Matrix::print() const
85 {
86 for (int i = 0; i < rowSize; i++) {
87 {
88 for (int j = 0; j < colSize; j++) {
89 {
90 cout << setw(5) << ptr[i][j];
91 }
92 }
93 cout << endl;
94 }
95 }
```
应用文件 程序 9.21 使用 Matrix 类。

```cpp
/**************************************
* 在堆中创建了几个矩阵对象，
* 并对它们进行了一些操作。
******************/
#include "matrix.h"
int main () {
// matrix1 初始化和设置
cout << "matrix1" << endl;
```
（续）

# 程序 9.21 测试 Matrix 类应用（续）

```cpp
11 matrix1.setup(3, 4);
12 matrix1.setup();
13 matrix1.print();
// 实例化并初始化 matrix2
14 cout << "matrix2" << endl;
15 matrix2(3, 4);
16 matrix2.setup();
17 matrix2.print();
// 实例化并初始化 matrix3
18 cout << "new matrix3" << endl;
19 matrix3(4, 2);
20 matrix3.setup();
21 matrix3.print();
// 将 matrix2 加到 matrix1 并打印结果矩阵
22 cout << "Result of matrix1 + matrix2" << endl;
23 matrixAdd(3, 4);
24 matrix1.add(matrix2, addResult);
25 addResult.print();
// 从 matrix1 中减去 matrix2 并打印结果矩阵
26 cout << "Result of matrix1 - matrix2" << endl;
27 matrixSub(3, 4);
28 subResult.subtract(matrix2, subResult);
29 subResult.print();
// 相乘 matrix1 和 matrix3 并打印结果矩阵
30 cout << "Result of matrix1 * matrix3" << endl;
31 mulResult(3, 2);
32 matrix1.multiply(matrix3, mulResult);
33 mulResult.print();
34 return 0;
35 }
```
```
Run:
matrix1
3 2 3 1
4 4 5 1
4 1 1 5
matrix2
4 3 1 3
3 5 1 5
4 5 1 4
matrix3
4 1
5 5
3 4
2 1
```

# 程序 9.21 测试 Matrix 类应用（续）

Result of matrix1 + matrix2 |
|---|---|
| 7 | 5 |
| 8 | 6 |
Result of matrix1 - matrix2 |
|---|---|
| 1 | 2 |
| 1 | 4 |
Result of matrix1 * matrix3 |
|---|---|
| 33 | 26 |
| 54 | 18 |

# 术语

- 引用算术
- 指针数组
- 引用类型
- 悬空指针
- 引用运算符
- 间接运算符
- 按值传递
- 全局对象
- 内存泄漏
- 空指针变量
- 按引用传递

## 总结

引用类型允许使用不同的名称访问内存位置。指针是地址的类型。指针变量包含一个地址。C++ 程序使用的内存由四个区域组成：代码内存（存储程序）、静态内存（存储全局和静态对象）、栈内存（存储参数和局部对象）以及堆内存（存储运行时创建的对象）。

## 问题

### PR-1. 给定以下代码，显示输出结果。

```cpp
int x = 10;
int& y = x;
cout << x << " " << y;
```

### PR-2. 给定以下代码，显示输出结果。

```cpp
int x = 100;
int& y = x;
int&z = x;
cout << x << " " << y << " " << z;
```

### PR-3. 以下代码的错误在哪里？

```cpp
int x = 1000;
int&y = 2000;
```

### PR-4. 以下代码会打印什么？

```cpp
int x = 1;
int&y = 2;
int&z = x;
cout << x << " " << y << " " << z;
```

### PR-5. 以下代码的错误在哪里？

```cpp
const int x = 100;
double&y = x;
```

### PR-6. 以下代码的错误在哪里？

```cpp
const int x = 100;
int&y = x;
```

### PR-7. 以下代码的错误在哪里？

```cpp
int x = 1000;
int&y = x;
```

### PR-8. 以下程序会打印什么？

```cpp
#include <iostream>
using namespace std;
void fun(int& y);
int main() {
    int x = 10;
    fun(x);
    cout << x << " " << y << endl;
    return 0;
}
void fun(int& y) {
    y++;
}
```

# PR-9. 下面程序输出什么？

```cpp
#include <iostream>
using namespace std;
void fun(int &y);
int main() {
    fun(10); // 错误
    cout << x << endl;
    return 0;
}
void fun(int &y) {
    y++;
}
```

# PR-10. 下面程序输出什么？

```cpp
#include <iostream>
using namespace std;
int fun(int &yy, int &zz);
int main() {
    int x = 120;
    int y = 80;
    cout << fun(x, y);
    return 0;
}
int fun(int &yy, int &zz) {
    if (yy > zz) {
        return yy;
    }
    return zz;
}
```

# PR-11. 下面程序输出什么？

```cpp
#include <iostream>
using namespace std;
int& fun(int yy, int zz);
int main ()
{
    int x = 120;
    int y = 80;
    cout << fun (x, y);
    return 0;
}
int& fun (int yy, int &zz)
{
    if (yy > zz)
{
        return yy;
    }
    return zz;
}
```

### PR-12. 下面程序输出什么？

```cpp
#include <iostream>
using namespace std;
int& fun (int &yy, int &zz)
{
    if (yy > zz)
{
        return yy;
    }
    return zz;
}
int main ()
{
    cout << fun (120, 80);
    return 0;
}
```

### PR-13. 给定以下代码行，显示输出的内容。

```cpp
int x = 10;
int* y = &x;
cout << x << " " << *y << " " << *y;
```

### PR-14. 给出以下代码行，显示输出的内容。

```cpp
int x = 100;
int* y = &x;
int* z = &y;
cout << x << " " << *y << " " << *z << " " << z;
```

### PR-15. 以下代码行有什么什么错误？

```cpp
int* x = 25;
```

# 问题 441

**PR-16.** 以下代码行有什么什么错误？

```cpp
const int x = 100;
double* y = &x;
```

**PR-17.** 以下代码行有什么什么错误？

```cpp
const int x = 100;
int* y = &x;
```

**PR-18.** 以下代码行有什么什么错误？

```cpp
const int x = 100;
int* y = &x;
int* y = &x;
```

**PR-19.** 以下代码行有什么什么错误？

```cpp
int x = 1000;
int y = 2000;
int* const z = &x;
z = &y;
```

**PR-20.** 下面代码行输出什么？

```cpp
int sample [5] = {0, 10, 20, 30, 40};
cout << *(sample + 2);
```

**PR-21.** 下面代码行输出什么？

```cpp
int sample [5] = {5, 10, 15, 20, 25};
cout << *(sample + 2) << endl;
cout << *(sample + 2);
```

**PR-22.** 下面代码行输出什么？

```cpp
int sample [5] = {0, 10, 20, 30, 40};
cout << *(sample + 7);
```

**PR-23.** 下面程序输出什么？

```cpp
#include <iostream>
using namespace std;
void fun (int* x)
{
    cout << *(x + 2);
}
int main ()
{
    int sample [5] = {0, 10, 20, 30, 40};
    fun(sample);
    return 0;
}
```

# 第9章 引用、指针与内存管理

**PR-24.** 下述语句在堆中创建了什么？画幅图来显示堆中的对象。

```cpp
int** arr = new int* [3];
```

**PR-25.** 下述语句在堆中创建了什么？画幅图来显示堆中的对象。

```cpp
int** arr = new int* [3];
for (int i=0; i<3; i++)
{
  arr[i] = new int [5];
}
```
