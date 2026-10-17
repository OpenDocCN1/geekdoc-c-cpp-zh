
```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>

template<class T = double> class fileOut{
char* fName;
bool App;
public:
    fileOut(char* fileName, bool app = 0);
    ~fileOut() {};
    void write(int nrows, int ncols, const T* const* pData) const;
};

// 方法定义
template<class T> fileOut<T>::fileOut(char* fileName, bool app){
fName = fileName;
App = app;
}

template<class T> void fileOut<T>::write(int nrows, int ncols, const T* const* pData) const {
    if(App == 0) {
        std::ofstream outFile;
        outFile.exceptions(std::ofstream::failbit |
        std::ofstream::badbit);
        try{
            outFile.open(fName);
        } catch(std::ofstream::failure e) {
            std::cout << "Error opening output file: " << e.what()
            << std::endl;
        }
        for(int i = 0; i < nrows; i++) {
            for(int j = 0; j < ncols; j++) {
                outFile << " " << pData[i][j] << " ";
            }
            outFile << std::endl;
        }
        outFile.close();
    } else {
        std::ofstream outFile(fName, std::ios::app);
        if(!outFile.is_open()){
            std::cout << "Error opening output file!" << std::endl;
        }
        for(int i = 0; i < nrows; i++) {
            for(int j = 0; j < ncols; j++) {
                outFile << " " << pData[i][j] << " ";
            }
        }
        outFile.close();
    }
}
```

该类有两个成员：输出文件 `fileName` 和一个指示输出是否追加到 `fileName` 的布尔变量 `App`。在类中 `App` 使用了 `false` 作为默认值。构造函数方法是 `write`，它将数组指针的行和列维度作为参数。注意使用了第 3.8 节中的 `T* const`，这确保了方法不会修改 `pData` 的数据。`write` 方法根据 `App` 的值以创建/覆盖或追加模式打开一个输出文件。在任何情况下，都会进行检查以确保目标文件已打开。对于 `App = 0` 的第一种情况，使用第 3.8 节中的 `try/catch` 进行检查。`App = 1` 的实例通过流成员处理，如果在连接到指定的输出时遇到问题，则该成员求值为为 `false`。现在让我们探索列表 3.20 中使用异常的一些细节。这里的标志位指示提供流状态信息的输入和输出对象。这些是名为 `ebit` 的变量（注：原文此处可能有误，指标志位变量）。

`simpleTemp` 类背后的基本思想很容易推广到构造某些有用的东西。特别是，列表 3.20 提供了一个可以用于文件输出的模板类。

该类有两个成员：输出文件 `fileName` 和一个布尔变量 `App`，指示输出是否追加到 `fileName`。在类中 `App` 使用了 `false` 作为默认值。构造函数方法是 `write`，它将数组指针的行和列维度作为参数。注意使用了第 3.8 节中的 `T* const`，这确保了方法不会修改 `pData` 的数据。`write` 方法根据 `App` 的值以创建/覆盖或追加模式打开一个输出文件。在任何情况下，都会进行检查以确保目标文件已打开。对于 `App = 0` 的第一种情况，使用第 3.8 节中的 `try/catch` 进行检查。`App = 1` 的实例通过流成员处理，如果在连接到指定的输出时遇到问题，则该成员求值为 `false`。现在让我们探索列表 3.20 中使用异常的一些细节。这里的标志位指示提供流状态信息的输入和输出对象。

*(注：由于提供的原文后半部分存在大量重复和逻辑乱码，译文已根据要求翻译并清理了重复的逻辑内容。)*

102

C++ 概览

```cpp
ifstream inFile(fileName);
```

然后使用插入运算符 `>>`（而非输出）来操作 `inFile`，这类似于使用 `istream` 对象 `cin` 的方法。具体细节留作练习题（练习 3.33）。

## 3.11 函数模板

类模板提供了一种生成通用函数的方法，这意味着类方法可以适用于创建类对象时使用的任何数据类型（无论是基本类型还是用户定义）。然而，一旦使用特定数据类型创建了模板对象，其方法就会变成特定数据类型的。例如，来自 `fileOut` 类的对象都将有一个关联的 `write` 方法。但如果尝试为处理 `int` 类型而创建的 `fileOut` 对象去写入 `double` 类型的数据，它将会失败。

函数模板提供了一种比类模板方法更灵活的手段。它们是独立的函数，不与类对象绑定，并且可以应用于同一个程序中的不同数据类型。创建函数的语法如下：

```cpp
template<T>
returnType functionName(T t, additional arguments)
{
    // 函数体
}
```

在这里，函数的返回类型 `returnType` 以及额外参数可以是任何数据类型，也可以是泛型类 `T` 对象。与类不同，目前无法为模板函数中的模板参数提供默认值。
接下来的函数使用模板函数实现了与上一节中 `fileOut` 模板类 `write` 方法相同的操作。

```cpp
//fileTemp.cpp
#include <iostream>
#include <fstream>
template<class T>
void write(const T* p, int nrows, int ncols, char* fName, bool app){
  if(app) {
    std::ofstream fileOut(fName, std::ios::app);
    for(int i = 0; i < nrows; i++){
      for(int j = 0; j < ncols; j++) {
        fileOut << p[i][j] << " ";
      }
      fileOut << std::endl;
    }
    fileOut.close();
  } else {
  std::ofstream fileOut(fName);
  for(int i = 0; i < nrows; i++){
    for(int j = 0; j < ncols; j++) {
      fileOut << p[i][j] << " ";
    }
    fileOut << std::endl;
    }
    fileOut.close();
  }
}
```

## 练习题

```cpp
int main(int argc, char** argv) {
  int** pi = new int*[2];
  for(int i = 0; i < 2; i++)
    pi[i] = new int[2];
  for(int j = 0; j < 2; j++)
    pi[i][j] = (i + 1)*(j + 1);
  write((int**)pi, 2, 2, argv[1], 0);
  double** pd = new double*[2];
  for(int i = 0; i < 2; i++)
    pd[i] = new double[3];
  for(int j = 0; j < 3; j++)
    pd[i][j] = (double)((i + 1)*(j + 1))/6;
  write((double**)pd, 2, 2, argv[1], 1);
  for(int i = 0; i < 2; i++)
    delete[] pd[i]; 
  delete[] pd;
  return 0;
}
```

该语法有些微妙。该函数隐式地处理二维数组。第一个参数暗示传递到函数的是一个一维数组。技巧在于 `T` 本身是指向另一个泛型类 `T0` 的指针，这为我们提供了指向对象的指针；使用省略符号，但这种关系可以表示为 `T*=T0*`。模板函数包含额外的参数，指定数组的行数和列数（即 `ncols`）、用于写入的文件名，以及一个决定是否将输出追加到现有文件的逻辑变量。列表中的 `main` 函数从命令行参数获取输出文件名，并使用 `int` 类型的专用数据将二维整数数组写入文件。随后以追加模式重新打开输出文件，并写入 `double` 类型输出数据。运行此程序得到的一些结果：

```
$ gcc -Wall funTemp.cpp -o funTemp
./funTemp outFile.txt
$ cat outFile.txt
1
2
0.166667 0.333333
0.333333 0.666667
```

## 3.2 练习题

3.1 当 `x` 是一个值为 1 的整数变量时，评估并打印逻辑表达式 `(x < 1)`、`(x > 1)`、`(x >= 1)`、`(x <= 1)`、`(x != 1)` 的值。使用 `boolalpha` 格式标志以零以及 true/false 格式显示输出：

```cpp
cout << boolalpha << (x == 1) << endl;
```

如果 `x` 的值为 1，将打印 `true`。

3.2 使用循环产生与以下相同的结果：

```cpp
while(1) {
    cout << "I'm in a loop!" << endl;
}
```

警告：在尝试运行你的程序之前，可能应该阅读附录 A 的第 4 节。

3.3 从 `forWhileExp.cpp` 程序提取输出。具体而言，由于和的边界为 100，第 3.4 节中和的最终值是否产生了 108？应该如何修改程序以使和永远不会超过边界？

3.4 编写一个从键盘输入获取 `double` 值的程序。它应该允许在任何点终止，终止后返回输入数据的平均值以及关于残差的幅度最大的值：即输入值与数据平均值之间的绝对差。

3.5 质数是指只能被 1 和它本身（无余数）除的数。编写一个程序，输入要计算的质数个数，并计算显示质数的值。在此过程中，注意以下几点是有用的：

- a) 不是质数
- b) 是唯一的偶质数且
- c) C++ 取模函数返回整数除法的余数。如果 `i` 和 `j` 是两个整数，当 `i%j == 0` 且且仅当 `i == k*j`（对于某个整数 `k`）。

3.6 编写一个程序，从命令行参数获取输出文件名，并使用 `int` 类型的专用数据将二维整数数组写入文件。随后以追加模式重新打开输出文件，并写入 `double` 类型输出数据。

3.7 在 C++ 中，函数可以调用自身。这种行为可能如下：

```cpp
returnType functionName(arguments){
    statements
    if(booleanExpression)
        functionName(arguments)
}
```

3.8. 使用与 3.7 相同的方法，创建一个计算 $n!$ 的函数，对于任何 $n \ge 1$ 的整数。递归递归？

3.9 定义斐波那契数 $F_0 = 0, F_1 = 1$ 且 $F_j = F_{j-1} + F_{j-2}, j = 2, \dots$

- a) 使用递归（类似于 3.7）创建一个 C++ 函数来评估序列，使用用户输入的项数。
- b) 通过循环创建 a) 的函数的迭代版本。
- c) a) 和 b) 哪个函数更快？使用 3.8 中的时间函数进行比较。
d) 解释 c) 的结果。这对于递归说明了什么？
e) 重写斐波那契函数，使得每次评估 $F_i$ 时将其值存储在数组中。确保每次调用都检查该值是否已经评估过，如果是，则直接返回。这与原生递归相比如何？（这种技术称为记忆化。）

11. 考虑一种游戏，球中有三个白球和一个红球。从球中不放回抽取。如果在任何一点抽中了红球，则将所有球放回球中继续抽取。让 X 为 $n$ 次抽取中抽取红球的次数。

- a) 写一个使用递归（类似于 3.7）的 C++ 程序来评估 $n$ 的概率分布。
b) 计算速度受 $n$ 如何影响？（提示：对小 $n$ 值进行实验）
c) 根据 b) 的答案，你可以预测评估 $n=100$、$n=1000$n=10000$ 需要多久吗？
d) 这与 3.9 中计算斐波那契数有何不同？预计递归是高效的吗？为什么或为什么？

假设 $x \ge 1$，并 $[y]$ 表示大于等于实数 $y$ 的最大整数。

- a) 开发一个利用 `while` 循环计算 $x$ 二进制展开的算法。
- b) 将 a) 的结果与练习 2.3 的结果相结合，创建一个计算浮点数二进制表示的代码。

12. 考虑以下代码段：

```cpp
int* p;
*p = 1;
```

编写一个尝试执行这两行代码的程序，并解释你遇到的问题。然后重新思考你的程序使其运行。

13. 编写代码，动态分配和删除一个三维数组的内存，该数组存储概率密度：

$f(x, y, z) \propto z(x-y)^2 & x, y=1, \dots, z=1, \dots, \max(x,y), \ 0, & \text{其他.} $

- a) 计算使 $f$ 成为密度的常数。
- b) 计算所有变量对之间的协方差。
- c) 计算三个变量的边缘密度。
- d) 计算当 $z=3$ 时 $(x, y)$ 的条件密度，并找到 $x$ 和 $y$ 变量对应的（条件）协方差。这一结果与无条件情况相比如何？

106

C++ 概览

3.14. 创建一个函数，能够循环方式切换双精度输入变量 x、y 和 z 的值：即 x → y，y → z 和 z → x。

3.15. 构造一个函数，接受一维数组的指针作为参数，并原地反转数组元素的顺序。

3.16. 如下形式的语法

```
returnType functionName(dataType a[], arguments)
```

可用于将数组 a 传递给函数。编写一个函数，将一个 double 数组传递给另一个函数，该函数计算数组元素的平均值。该函数可以修改数组的元素吗？如果是的话，你如何确保这种情况不会发生？

3.17. 移除第 3.8.4 节中 `y.h` 头文件中 `include` 指令。然后，验证 `xy.cpp` 文件中 `include` 指令的顺序是否决定程序是否能够编译。

3.18. 编写一个程序来测试第 3.8.7 节中 `new` 的 dropbox 版本。

3.19. 重载时一个非常实用的运算符是输出插入运算符。`<<` 的原型为：

```
ostream& operator<<(ostream& out, const dataType& object)
```

第一个参数是 `ostream` 对象的引用，第二个是输出的引用。

这个简单的程序说明了如何通过重载输出插入运算符为类提供打印实用程序。

```cpp
#include <iostream>
using std::ostream; using std::cout; using std::endl;
class X{
    int I;
public:
    X(int i) : I(i) {}
    friend ostream& operator<<(ostream& out, const X& x);
};
ostream& operator<<(ostream& out, const X& x) {
    out << x;
    return out;
}
int main() {
    X x(7);
    cout << x << endl;
    return 0;
}
```
