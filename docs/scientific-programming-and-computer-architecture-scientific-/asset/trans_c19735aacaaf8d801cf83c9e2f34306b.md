

## 1.3. C++ 复习

缓存数据、存储元数据以及其他方面。然而，它们有许多共同点。此外，每个文件系统最终都实现在不同的存储设备上。

文件系统到设备的映射也可以使用面向对象的技术进行组织。另一个例子是支持多种后端的绘图库的实现。

面向对象编程既可以用纯 C 语言完成，也可以使用函数指针。然而，这会变得费力得多。书中并没有真正涉及面向对象的技术，尽管我们在第 8 章中用到了模板。因此，我们包含了下面的模板函数的基本示例：

```cpp
template<class Num> Num sum(*arr, int len){
  Num ans;
  ans = 0;
  for(int i=0; i < len; i++)
    ans += arr[i];
  return ans;
}
```

在这个函数中，`Num` 是泛型类或类型。它可以代表 `int`、`double` 或某些重载了 `+=` 运算符并支持加法的用户定义类。如果通过将 `Num` 设置为用户定义类来实例化模板，则它必须支持空构造函数（第 2 行）以及赋值为零（第 3 行）。

模板函数可以如下所示的方式被调用。

```cpp
int x[5] = {1, 2, 3, 4, 5};
cout<<"1" + 5 << " = "<<sum(x, 5)"<<endl;
double y[5] = {6, 7, 8, 9, 10};
cout<<"6" + 10 << " = "<<sum(y, 5)"<<endl;
```

模板函数的调用就像普通函数一样，从第 2 行和第 4 行对 `sum()` 的调用可以看出。由于 `x[]` 是 `int` 数组，C++ 编译器将泛型类型 `Num` 替换为 `int` 以为新函数生成代码。在第 2 行，`sum(x,5)` 调用该函数。然而，第 4 行的 `sum(y,5)` 调用的是通过将 `Num` 替换为 `double` 生成完全不同的函数。

## 1.3.2 C++ 中的 Aitken 变换

源文件 `Aitken.cpp`、`Leibniz.cpp` 和 `Logseries.cpp` 包含了 Aitken 变换的 C++ 实现及其在莱布尼茨级数对数级数应用。下面的列表是 C++ 头文件 `Aitken.hh` 之一。

```cpp
1 #ifndef AitkenAugust09DVjli
2 #define AitkenAugust09DVjli
3 #include "Vector.h"
4 void Aitken(const Vector& seq1, Vector& seq2);
5 void Aitken(Vector& seq);
6 double Aitken(const Vector& seq, int printflag=0);
7 #endif
```

该头文件声明了三个函数，其中两个同相同。函数名 `Aitken` 被重载，参数为 `(v,w)`，其中 `v` 和 `w` 都是 `Vector`。调用后，第一个声明中的 `const` 保证了 `v` 不会被改变。使用 `const` 简化了该函数的文档说明。另一种调用函数的方式是使用。在这种用法中，变换后的序列会覆盖原始数据，并将最后项设置为 0。我们可以对不同的函数使用相同的名称，因为编译器可以通过查看参数列表来区分它们。

尽管 `Aitken()` 只有一个声明（第 6 行），但它可以使用一个或两个参数调用。如果我们以 `Aitken(v)` 的形式调用它，编译器会将该调用解释为 `Aitken(v, 0)`。`Aitken()` 的声明（第 13 行）将其第二个参数设为 `int printflag=0`，指示编译器如果省略第二个参数，则假设默认值为 0。我们也可以以 `Aitken(v,1)` 的形式调用它，其中第二个参数的值显式给出 1。通常，最好只对最后一个参数使用默认参数机制。

`Aitken` 函数反复变换序列，直到序列只剩下一个或两个数字。下面的 `Aitken(Vector& seq1)` 执行序列的单次变换。

```cpp
1 void Aitken(Vector& seq1){
2 int len = seq1.getSize();
3 for(int i=0; i < len-2; i++)
4   double a = seq1(i);
5   double b = seq1(i+1);
6   double c = seq1(i+2);
7   seq1(i) = a - (b-a)*(b-a)/(a-2*b+c);
8   }
9   seq1(len-2) = 0;//无效项
10  seq1(len-1) = 0;
11 }
```

`Vector` 对象 `seq` 的项在第 4、5、6、9 和 10 行被访问。这些访问都是使用重载的函数调用运算符解析的，而不是简单的数组查找。

下面的 `AitkenE()` 定义在源文件 `Aitken.cpp` 中。它利用了 `Vector` 类的隐藏能力。它反复变换序列，每次变换都通过第 13 行调用 `Aitken()` 实现。

```cpp
1 double AitkenE(const Vector& seq, int printflag){
2   int len = seq.getSize();
3   Vector myseq(len);
4   myseq = seq;
5   Vector v;
6   v = myseq;
7   int n = len;
8   if(n==0)
9     n--;
10  if(printflag==1)
11    n--;
12    for(int i=0; i<n; i++){
13      Aitken(v);
14      v = myseq;
15    if(printflag==1)
16      printseq(v);
17  }
18  int index = len-1;
19  return v(index);
20 }
```

（注：提供的文本中包含大量重复段落，已根据文档逻辑进行了整合。）

