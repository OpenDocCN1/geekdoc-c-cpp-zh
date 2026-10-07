

```cpp
cout << "Trying to get a big block of memory:\n";
pb = new Big[10000]; // 1,600,000,000 bytes
cout << "Got past the new request:\n";
}
catch (bad_alloc& ba)
{
    cout << "Caught the exception!\n";
    cout << ba.what() << endl;
    exit(EXIT_FAILURE);
}
cout << "Memory successfully allocated:\n";
pb[0].stuff[0] = 4;
cout << pb[0].stuff[0] << endl;
delete [] pb;
```

这是系统的输出：
Trying to get a big block of memory:
Caught the exception!
std::bad_alloc

在这种情况下，`what()` 方法返回字符串 "std::bad_alloc"。
如果程序在你的系统上运行时没有内存分配问题，你可以尝试增加请求的内存量。

## 空指针与 new

在当 `new`（旧的 `new`）在失败时返回空指针时，编写了许多代码。某些编译器通过允许用户设置标志或切换来处理向新 `new` 的过渡，以选择保留哪行为。目前标准提供了另一种形式的 `new`，它仍然返回空指针。它的用法如下：

```cpp
int * pi = new (std::nothrow) int;
int * pa = new (std::nothrow) int[500];
```

使用此函数，你可以这样重写列表 15.13 的核心部分：
Big * pb;

```cpp
pb = new (std::nothrow) Big[10000]; // 1,600,000,000 bytes
if (pb == 0)
{
    cout << "Could not allocate memory. Bye.\n";
    exit(EXIT_FAILURE);
}
```

## 异常、类与继承

异常、类和继承以几种方式相互作用。首先，你可以从一个异常类派生另一个异常类，正如标准 C++ 库所做的那。其次，你可以通过在类定义嵌套异常声明将异常引入类中。第三，这种嵌套声明可以被继承，并本身作为基类使用。

列表 15.14 带我们开始探索这些可能性能。该头文件声明了一个原始的 `Sales` 类，它包含一个值和一个包含 12 个月度销售数字的数组。`LabeledSales` 类派生自 `Sales` 并增加了一个成员来存储数据的标签。

## 列表 15.14 sales.h

```cpp
//sales.h
// exceptions and inheritance
#include <stdexcept>
#include <string>

class Sales
public:
    enum {MONTHS = 12}; // could be a static const
    class bad_index : public std::logic_error
    private:
        int bi; // bad index value
    public:
        explicit bad_index(int ix,
            const std::string & s = "Index error in Sales object\n");
        int bi_val() const throw { return bi; }
        virtual ~bad_index() throw() {}
    };
    explicit Sales(int yy = 0);
    Sales(int yy, const double * gr, int n);
    virtual ~Sales() throw() {}
    int Year() const { return year; }
    virtual double operator[](int i) const;
    virtual double &operator[](int i);
    private:
        double gross[MONTHS];
        int year;
};

class LabeledSales : public Sales
{
public:
    class nbad_index : public Sales::bad_index
    {
private:
        std::string lbl;
public:
        bad_index(const std::string& lb, int ix,
            const std::string& s = "Index error in LabeledSales object\n");
        const std::string& label_val() const { return lbl; }
        virtual ~nbad_index() throw() {};
        explicit LabeledSales(const std::string& lb = "none", int yy = 0);
        LabeledSales(const std::string& lb, int yy, const double * gr, int n);
        virtual ~LabeledSales() {}
        const std::string& Label() const { return label; }
        virtual double operator[](int i) const;
        virtual double& operator[](int i);
    private:
        std::string label;
    };
```

让我们检查列表 15.14 的几个细节。首先，符号常量位于 `Sales` 的保护部分；这使得派生类（如 `LabeledSales`）可以使用该值。接下来，`bad_index` 类嵌套在 `LabeledSales` 的公共部分，这使得该类可以作为类型用于 `catch` 块。注意，外部世界需要将该类型标识为 `Sales::bad_index`。此类派生自标准的 `logic_error` 类。`bad_index` 类具有存储和报告数组索引越界值的能力。`nbad_index` 类嵌套在 `LabeledSales` 的公共部分，使得客户端代码可以使用它。由于 `bad_index` 派生自 `logic_error`，因此 `nbad_index` 最终也派生自 `logic_error`。这两个类都具有重载的 `operator[]` 方法，用于访问单个元素并在索引越界时抛出异常。这是因为它们本质上都继承自异常类，且它的虚拟析构函数使用了 `throw()` 规范。这是 C++98 的特性；在 C++11 下，异常没有异常规范。列表 15.15 显示了未在列表 15.14 中内联定义的方法的实现。注意，嵌套类需要多次使用作用域解析运算符。

## 列表 15.15 sales.cpp

```cpp
// sales.cpp -- Sales implementation
#include "sales.h"
using std::string;

Sales::bad_index(int ix, const string & s)
    : std::logic_error(s), bi(ix) {}

Sales::Sales(int yy) : year(yy) {
    for (int i = 0; i < MONTHS; ++i)
        gross[i] = 0;

Sales::Sales(int yy, const double * gr, int n) : year(yy) {
    int lim = (n < MONTHS) ? n : MONTHS;
    int i;
    for (i = 0; i < lim; ++i)
        gross[i] = gr[i];
    for (i = lim; i < MONTHS; ++i)
        gross[i] = 0;

double Sales::operator[](int i) const {
    if (i < 0 || i >= MONTHS)
        throw bad_index(i);
    return gross[i];
}

double& Sales::operator[](int i) {
    if (i < 0 || i >= MONTHS)
        throw bad_index(i);
    return gross[i];
}
```

## 列表 15.16 use_sales.cpp

```cpp
// use_sales.cpp -- nested exceptions
#include <iostream>
#include "sales.h"

int main()
{
  Sales sales1(2008);
  double vals1[] = {0.0, 10.0, 20.0, 30.0, 40.0, 50.0, 60.0, 70.0, 80.0, 90.0, 100.0, 110.0};
  for (int i = 0; i < 12; ++i) 
    sales1[i] = vals1[i];

  LabeledSales sales2("Widget", 2009);
  double vals2[] = {0.0, 10.0, 20.0, 30.0, 40.0, 50.0, 60.0, 70.0, 80.0, 90.0, 100.0, 110.0};
  for (int i = 0; i < 12; ++i) 
    sales2[i] = vals2[i];

  try {
    cout << "First try block:\n";
    for (int i = 0; i < 12; ++i)
      cout << "Year: " << sales1.Year() << " Month: " << i << " " << sales1[i] << endl;
    for (int i = 0; i < 13; ++i)
      cout << "Year: " << sales1.Year() << " Month: " << i << " " << sales1[i] << endl;
  } catch (Sales::bad_index& ba) {
    cout << "Caught the exception!\n";
    cout << ba.what() << endl;
    exit(EXIT_FAILURE);
  }

  try {
    cout << "Second try block:\n";
    for (int i = 0; i < 12; ++i)
      cout << "Year: " << sales2.Year() << " Month: " << i << " " << sales2[i] << " Label: " << sales2.Label() << endl;
    for (int i = 0; i < 13; ++i)
      cout << "Year: " << sales2.Year() << " Month: " << i << " " << sales2[i] << " Label: " << sales2.Label() << endl;
  } catch (LabeledSales::nbad_index& ba) {
    cout << "Caught the exception!\n";
    cout << ba.what() << endl;
    exit(EXIT_FAILURE);
  } catch (Sales::bad_index& ba) {
    cout << "Caught the exception!\n";
    cout << ba.what() << endl;
    exit(EXIT_FAILURE);
  }

  return 0;
}
```

