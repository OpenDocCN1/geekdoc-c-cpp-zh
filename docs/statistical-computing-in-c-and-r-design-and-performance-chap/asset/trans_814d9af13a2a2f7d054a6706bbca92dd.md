
```cpp
int nRows = 2, nCols = 3;
double** pM = 0;
pM = new double*[nRows];
for(int i = 0; i < nRows; i++)
pM[i] = new double[nCols];
cout << "The value of pM is " << pM << endl;
```

```cpp
for(int i = 0; i < nRows; i++)
cout << "The address for pM[" << i << "] is " <<
&pM[i] << endl;
```

```cpp
for(int i = 0; i < nRows; i++)
cout << "The value of pM[" << i << "] is " << pM[i] << endl;
for(int j = 0; j < nCols; j++)
cout << "The address of pM[" << i << "][" << j << "] is " <<
&pM[i][j] << endl endl;
```

```cpp
for(int i = 0; i < nRows; i++)
for(int j = 0; j < nCols; j++)
pM[i][j] = i*j;
cout << "pM[" << i << "][" << j << "] = " << pM[i][j] << " ";
cout << endl endl;
```

```cpp
//memory clean up
for(int i = 0; i < nRows; i++)
delete[] pM[i];
delete[] pM;
return 0;
```

这段代码将产生类似于下面的输出：

The value of pM is 0x001150
The address for pM[0] is 0x001150
The address for pM[1] is 0x001154
The value of pM[0] is 0x001160
The address of pM[0][0] is 0x001160
The address of pM[0][1] is 0x001168
The address of pM[0][2] is 0x001170
The value of pM[1] is 0x001180
The address of pM[1][0] is 0x001180
The address of pM[1][1] is 0x001188
The address of pM[1][2] is 0x001190

代码列表 3.4 显示了一个 2x3 的双精度变量矩阵。这是通过获取一个可以存储（即接收）指向双精度浮点数指针内存地址的指针实现的。第一个循环为矩阵的两行中的每一行执行了内存分配。我们程序产生的输出确认了上述图中指示的内容：`pM` 指向（即持有）指针 `M[0]` 的地址，而 `M[0]` 又指向 `M[0]`，以此此类推。具体来说，第二个 `for` 循环证明了内存是行与行连续布局的。通常情况下，由于行与行之间的内存块之间存在间隙，我们的数组中的内存位置并不是连续的（或无法保证连续）。事实上，在 `pM[0]` 内存块与从 `pM[1]` 开始的内存块之间似乎存在间隙。实际上，这是 C++ 的一个特性，它始终为指针提供一个“一次到最后”的内存块。这块额外的内存可以被指向但不能被延迟。代码列表 3.4 证明了以指针指针格式存储的数据可以像任何其他数组一样进行操作。要为指针 `pM` 的第 (i, j) 个内存位置赋值，请使用 `pM[i][j]` 语法。列表中的最后一个循环演示了如何释放指针指针存储的内存。这种情况在技术上是不必要的，因为所有内会在程序终止时自动释放。但通常情况下，可能存在许多位于 `main` 调用的其他函数之外的情况。

如果 C++ 语言只允许将源代码放在 `main` 函数体内，限制将会很大。我们从第 2 章知道情况并非如此，在程序中包含其他函数是可能的。为了实现这一点，必须在 `main` 代码之前提供函数的原型或定义。这可以通过将原型放在与 `main` 相同的文件中，或者通过使用 `#include` 指令来实现。我们目前关注第一种方案。函数的通用结构如下：

```cpp
returnType functionName(arguments){
    body of function
    return statement
}
```

在这里，`returnType` 可以是任何基本数据类型。`return` 语句中的值必须与 `returnType` 的类型相同。下面的代码列表是一个简单的程序，它可以在 `main` 体内调用一个平方函数，对通过 2.3 节引入的输入流 `cin` 从 shell 界面提供的某些数值进行平方。

代码列表 3.5 square.cpp

```cpp
//square.cpp
#include <iostream>

using namespace std;

double square(double x);

int main() {
    double x;
    cout << "Enter a number ";
    cin >> x;
    cout << square(x) << endl;
    return 0;
}

double square(double x) {
    return x*x;
}
```

注意在 `main` 中使用之前为 `square` 提供的原型。如果没有这样做，并且没有在 `main` 之前给出 `square` 的定义，将生成类似下面的编译器错误：

```
square.cpp: In function int main() {
square.cpp:10: error: 'square' was not declared in this scope
```

编译 ` -Wall square.cpp` 会产生，例如：

```bash
$ g++ -Wall square.cpp -o square
./square
Enter a number 4
16
./square
Enter a number 1.278
1.63328
```
