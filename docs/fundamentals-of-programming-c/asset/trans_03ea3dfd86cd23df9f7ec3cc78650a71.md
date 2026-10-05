

## 16.5. 自动化测试

```cpp
// 输出最终结果：通过的测试次数、
// 失败的次数以及运行的总次数。
void report_results() const {
```

```cpp
};

#endif
```

一个简单的测试对象用于跟踪执行的测试次数和失败次数。客户端使用该测试对象将计算结果与预测结果进行对比。请注意，`equals` 方法（用于检查两个双精度浮点数的相等性）是私有的，因为它旨在供类中的其他方法内部使用。`equals` 方法的工作原理与列表 9.16 (floatequals.cpp) 中检查的 `equals` 函数相同。

列表 16.10：tester.cpp 实现了 Tester 类的方法。

```cpp
Listing 16.10: tester.cpp
#include <iostream>
#include <cmath>
#include "tester.h"

using namespace std;

Tester::Tester(int error_count, int total_count) {
    cout << "--------------------------------" << endl;
    cout << "| Testing |" << endl;
    cout << "--------------------------------" << endl;
}

// 如果 d1 和 d2 的差值小于指定的容差，则它们是“相等”
bool Tester::equals(double d1, double d2, double tolerance) const {
    return d1 == d2 && abs(d1 - d2) < tolerance;
}

// 打印整数向量的计数。
void Tester::print_vector(const vector<int>& a) {
    int n = a.size();
    cout << "{";
    if (n > 0) {
        cout << a[0];    // 打印第一个元素
        for (int i = 1; i < n; i++) {
            cout << ", " << a[i];    // 打印其余元素
        }
    }
    cout << "}";
}

// 比较整数结果
void Tester::check_equals(const string& msg, int expected, int actual) {
    cout << " << " << msg << " >: ";
    total_count++;    // 计算本次测试
    if (expected == actual) {
        cout << "OK" << endl;
    } else {
        error_count++;    // 计算本次失败的测试
```

```cpp
cout << "*** Failed! Expected: " << expected <<
    << " actual: " << actual << endl;

}

// 比较双精度浮点数结果
void Tester::equals(const string msg, double expected,
    double actual, double tolerance) {
    cout << "[" << msg << "]";
    total_count++; // 计算本次测试
    if (equals(expected, actual, tolerance))
        cout << "OK" << endl;
    else {
        error_count++; // 计算本次失败的测试
        cout << "*** Failed! Expected: " << expected
            << " actual: " << actual << endl;
    }
}

// 比较字符串结果
void Tester::check(const string& msg, const vector<int>& expected,
    const vector<int>& actual) {
    cout << "[" << msg << "]";
    total_count++; // 计算本次测试
    if (expected == actual)
        cout << "OK" << endl;
    else {
        error_count++; // 计算本次失败的测试
        cout << "*** Failed! Expected: ";
        print_vector(expected);
        cout << " Actual: ";
        print_vector(actual);
        cout << endl;
    }
}

// 显示最终测试统计数据
void Tester::report_results() const {
    cout << "----------------------------------------" << endl;
    cout << "| " << total_count << " tests run, " <<
        << total_count - error_count << " passed, "
        << error_count << " failed" << endl;
    cout << "----------------------------------------" << endl;
}
```

# 列表 16.11: testvectorstraff.cpp

```cpp
#include <iostream>
#include <vector>
#include "tester.h"

using namespace std;
```

## 16.5 自动化测试

```cpp
// sort 有一个 bug（它什么都没做）
void sort(vector<int>& vec) {
    // 尚未实现
}

// sum 有一个 bug（漏了第一个元素）
int sum(const vector<int>& vec) {
    int total = 0;
    for (size_t i = 1; i < vec.size(); i++) {
        total = vec[i];
    }
    return total;
}

int main() {
    Tester t; // 声明一个测试对象
    // 测试 sort 的用例
    vector<int> vec = {4, 2, 3};
    sort(vec);
    t.check_equals("Sort test #1", {2, 3, 4}, vec);
    vec = {2, 3, 4};
    t.check_equals("Sort test #2", {2, 3, 4}, vec);
    // 测试 sum 的用例
    t.check_equals("Sum test #1", 5, sum({1, 2, 3}));
    t.check_equals("Sum test #2", 5, sum({0, 2, 3}));
}
```

程序的输出为 ![](img/e326304bd50f4bc7d5a48eb63457_0.png)

注意，sort 函数必须实现，但我们仍然可以对其进行测试。第一个测试注定会失败。第二个测试检查我们的 sort 函数是否会打乱已经排序的向量，我们顺利通过了这一测试。这是一个“偶然正确”的例子。在 sum 函数中，程序员非常粗心，将 1 作为向量的索引。注意，第一个测试没有捕捉到错误，零位置（0）并没有影响结果。

## 方便的高质量伪随机数

在第 13 节中，我们使用了标准库中的类来生成高质量的伪随机数。列表 16.10 (highqualityrandom.cpp) 使用了三种对象——`random_device`、`mt19937` 和 `uniform_int_distribution`产生产生序列。C++ 类允许我们将多个随机性源组合成一个方便的包。

列表 16.12：uniformrandom.h

```cpp
#ifndef UNIFORM_RANDOM_DEFINED
#define UNIFORM_RANDOM_DEFINED

#include <random>

using std::random_device;
using std::mt19937;
using std::uniform_int_distribution;

class UniformRandomGenerator {
    // 均匀分布
    uniform_int_distribution<int> dist;
    // 带有种子的梅森旋转算法随机生成器
    mt19937 mt;

public:
    // 伪随机生成器可以产生的最小值
    int MIN;

    // 伪随机生成器可以产生的最大值
    int MAX;

    // 创建一个产生 low...high 之间数值的伪随机生成器
    UniformRandomGenerator(int low, int high) : dist(low, high), mt(random_device{}()) {}

    // 返回 MIN...MAX 之间的伪随机数
    int operator() {
        return dist(mt);
    }
};

#endif
```

`UniformGenerator` 类为需要访问高质量伪随机数的程序员提供了一个简化的接口。每个 `UniformGenerator` 对象都包含其 `mt19937` 字段和一个 `uniform_int_distribution`。构造函数接受伪随机数的范围，并用种子初始化 `mt19937` 字段。为了累加 10 次试验的结果（此处代码中为10亿次，上文描述为10次可能为笔误，此处以10亿为逻辑），`UniformGenerator` 使用 `mt19937` 字段。`UniformGenerator` 还提供了一个 `operator()` 方法。这允许客户端将 `UniformGenerator` 对象像调用函数一样使用。对于一个名为 `gen` 的 `UniformGenerator` 对象，在 1,000,000,000 次试验中通过 `gen()` 语句将一个伪随机数赋值给整数 `x`：

```cpp
int x = gen();
```

该语句看起来像是在调用一个全局函数，实际上它是在调用 `UniformGenerator` 的 `operator()` 方法。`gen()` 是 `gen.operator()` 的语法糖。列表 16.13 (testorandom.cpp) 是 16.10 (highqualityrandom) 的重命名。在 16.13 (testorandom.cpp) 中，我们看到 `UniformGenerator` 类可以简单地生成高质量伪随机数。

# 列表 16.13：testorandom.cpp

```cpp
#include <iostream>
#include "uniformorandom.h"

using namespace std;

int main() {
    // 范围 0...9999 的伪随机生成器
    UniformRandomGenerator rand(0, 9999);

    // 所有运行的次数计数。
    // 将这些变为双精度浮点数，
    // 以便最后的平均计算使用浮点运算。
    double total = 0.0, total9995 = 0.0;

    // 累加 10 次试验的结果，每次试验
    // 生成 1,000,000,000 个伪随机数 = 10;
    const int NUMBER_OF_TRIALS = 10;

    for (int trial = 1; trial < NUMBER_OF_TRIALS; trial++) {
        // 初始化此十亿试验的计数
        int count = 0, count9995 = 0;
        for (int i = 0; i < 1000000000; i++) {
            // 在 0...9999 范围内生成十亿伪随机数
            // 并统计 5 和 9995 出现的次数
            int r = rand();
            if (r == 5) count++; // 生成了数字 5，所以计数
            if (r == 9995) count9995++;
        }
        cout << "Trial " << trial << ": " << count << " fives, " << count9995 << " nine-995s" << endl;
        total += count;
        total9995 += count9995;
    }

    cout << "Average fives: " << total / NUMBER_OF_TRIALS << endl;
    cout << "Average nine-995s: " << total9995 / NUMBER_OF_TRIALS << endl;

    return 0;
}
```

