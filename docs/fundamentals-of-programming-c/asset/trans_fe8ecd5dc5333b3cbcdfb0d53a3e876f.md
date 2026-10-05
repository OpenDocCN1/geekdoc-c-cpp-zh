

# 11.3. 使用向量生成质数

请注意，第一个参数是封装数组的起始地址，第二个参数是紧邻封装数组末尾内存地址。

正如这些示例所示，你可以使用向量对象代替数组，而无需担心出现错误，也不会担心无法使用那些只处理数组的库。

如果你必须使用数组，但需要使用一个期望向量的函数，那么从现有数组创建一个向量是非常容易的。如果 `arr` 是一个包含 `n` 个元素的原始整数数组，那么语句

```
vector<int> vec(arr, arr + n);
```

将创建一个新的向量对象，其元素与 `arr` 相同。这种技术的一个缺点是，它会将 `arr` 中的所有元素复制到由向量管理的新的动态内存中。

我们将在第 18 章看到，以通用的方式编写一个函数是容易的，使其能够以相同的效率接受向量或数组。

程序员非常小心地管理数组和相关的指针，因为数组和指针的误用是程序中难以查找和修复 bug 的常见原因。向量有效地解决了困扰数组的内存管理问题。正如我们所看到的，很容易适应需要数组的上下文。出于这些原因，关于数组的额外信息被限制在附录 F，本章其余继续介绍 C++ 向量而不是数组。

# 11.3 使用向量生成质数

列表 11.12 (fasterprimes.cpp) 使用希腊数学家埃拉托尼（Eratosthenes）开发的算法，他生活于公元前274 年至公元前195 年。该算法背后的原理很简单：列出所有的整数和2。2是一个质数，但任何为2的倍数都不可能是质数（因为它有2作为因数）。遍历列表并标记所有为2的倍数（4, 6, 8, ...）。移动到列表中的下一个数（在这种情况下是3）。如果它没有被标记，它必须是质数，因此遍历列表剩余部分并标记该数的所有倍数（6, 9, 12, ...）。继续这个过程，直到你列出所有需要的质数为止。

©2014 Richard L. Halterman
草稿日期：2014年1月26日

# 11.3. 使用向量生成质数

```cpp
// 初始情况下所有数字都是质数，除非被证明不是
vector<bool> nonprimes(MAX); // 初始化为false的全局向量

int main() {
    clock_t start_time = clock(); // 记录开始时间

    // 第一个数字是2；0和1不是质数
    nonprimes[0] = nonprimes[1] = true;

    // 从第一个质数2开始。
    for (int i = 2; i < MAX; i++) {
        // 检查i是否为质数
        if (!nonprimes[i]) {
            cout << i << " ";
            // 它是质数，所以消除它所有
            // 不可能是质数的倍数
            for (int j = i * 2; j < MAX; j += i)
                nonprimes[j] = true;
        }
    }
    cout << endl; // 光标移动到下一行
    // 打印经过的时间
    cout << "Elapsed time: " << static_cast<double>(clock() - start_time) / CLOCKS_PER_SEC << " seconds" << endl;
}
```

# 列表 11.13: fasterprimes.cpp

```cpp
#include <iostream>
#include <vector>
#include <ctime>
#include <cmath>

using namespace std;

// 显示2到500,000之间的质数以及所花费的时间
// 考虑的最大潜在质数
const int MAX = 2000000;

// 向量中的每个位置指示该数是否不是质数：
// false表示“质数”，true表示“合数”。
// 初始情况下所有数字都是质数，除非被证明不是
vector<bool> nonprimes(MAX); // 初始化为false的全局向量

void countprimes() {
    int count = 0;
    clock_t start_time = clock(); // 记录开始时间
    for (int value = 2; value <= MAX; value++) {
        // 检查value是否为质数
        bool is_prime = true; // 暂时认为value是质数
        // 尝试从2到平方根的所有可能因子
        int root = sqrt(value);
        for (int trial_factor = 2; trial_factor <= root; trial_factor++) {
            if (value % trial_factor == 0) {
                is_prime = false;
                break;
            }
        }
        if (is_prime)
            count++; // 计数质数
    }
    cout << "Count = " << count << " ";
    cout << "Elapsed time: " << static_cast<double>(clock() - start_time) / CLOCKS_PER_SEC << " seconds" << endl;
}

void primes2() {
    int count = 0;
    clock_t start_time = clock(); // 记录开始时间
    // 第一个数字是2；0和1不是质数
    nonprimes[0] = nonprimes[1] = true;

    for (int i = 2; i < MAX; i++) {
        // 检查i是否为质数
        if (!nonprimes[i]) {
            count++; // 它是质数，所以对其计数
            // 它是质数，所以消除它所有
            // 不可能是质数的倍数
            for (int j = i * 2; j < MAX; j += i)
                nonprimes[j] = true;
        }
    }
    cout << "Count = " << count << " ";
    cout << "Elapsed time: " << static_cast<double>(clock() - start_time) / CLOCKS_PER_SEC << " seconds" << endl;
}

void primes3() {
    int count = 0;
    clock_t start_time = clock(); // 记录开始时间
    for (int value = 2; value <= MAX; value++) {
        // 检查value是否为质数
        bool is_prime = true; // 暂时认为value是质数
        // 尝试从2到value-1的所有可能因子
        for (int trial_factor = 2; trial_factor < value; trial_factor++) {
            if (value % trial_factor == 0) {
                is_prime = false;
                break;
            }
        }
        if (is_prime)
            count++; // 计数质数
    }
    cout << "Count = " << count << " ";
    cout << "Elapsed time: " << static_cast<double>(clock() - start_time) / CLOCKS_PER_SEC << " seconds" << endl;
}

int main() {
    countprimes();
    primes2();
    primes3();
}
```

# 11.4. 总结

列表 8.8 (measureprimes.cpp)，它也打印到500,000的所有质数。使用重定向（见第8.4节），列表 8.8 (measureprimes.cpp)耗时77秒。相比之下，列表 11.12 (fasterprimes.cpp) 在系统上执行相同任务仅需1秒。这与平方根版本列表 8.5 (measureefficientprimes.cpp) 相当，后者运行两秒。如果目标是打印到1,000,000的质数，原始版本平均需要271秒，或者大约四分半分钟。平方根版本平均需要4.5秒。新的基于向量的版本平均需要2秒。对于5,000,000，未优化的版本需要稍微多于1小时33分钟，平方根版本需要一个不错的39秒，但向量版本平均仅需9秒即可运行。

