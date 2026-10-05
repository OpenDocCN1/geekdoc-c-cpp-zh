

## 8.2. 标准数学函数

![](img/e326304bd50fbc4f7d5a64c1487eb635_186_0.png)

图 8.4：轨道距离问题

- 1. **问题：** 随着移动点沿圆周移动，我们重新计算其它的位置。

**解：** 给定移动点的初始位置 $(x_1,y_1)$，绕原点旋转 $\theta$ 度将得到一个新点 $(x_2,y_2)$，其中：

$x_2 = x_1\cos\theta - y_1\sin\theta$
$y_2 = x_1\sin\theta + y_1\cos\theta$

- 2. **问题：** 随着移动点移动到新位置，重新计算移动点与固定点之间的距离。

**解：** 图 8.4 中两点 $(p_x,p_y)$ 和 $(x_1,y_1)$ 之间的距离 $d_1$ 由以下公式给出：

$d_1 = \sqrt{(x_1-p_x)^2 + (y_1-p_y)^2}$

同样，图 8.4 中的距离 $d_2$：

$d_2 = \sqrt{(x_2-p_x)^2 + (y_2-p_y)^2}$

Listing 8.4 (orbitdist.cpp) 将这些数学结果输出以计算距离。

```cpp
Listing 8.4: orbitdist.cpp

#include <iostream>
#include <cmath>

using namespace std;

int main() {
    // 轨道点的位置是 (x,y)
    double x;    // 这些值随着卫星
               // 移动而改变
    double y;    //
    const double PI = 3.14159;

    // 固定点的位置始终是 (100, 0),
    // 即 (p_x, p_y)。根据需要修改这些值。
    const double p_x = 100;
    const double p_y = 0;

    // 10 度的弧度
    const double radians = 10 * PI/180;

    // 计算 10 度的余弦和正弦
    const double COS10 = cos(radians);
    const double SIN10 = sin(radians);

    // 从用户处获取起点
    cout << "Enter initial satellite coordinates (x,y):";
    cin >> x >> y;

    // 计算初始距离
    double d1 = sqrt((p_x - x)*(p_x - x) + (p_y - y)*(p_y - y));

    // 让卫星运行 10 度
    double x_old = x; // 记住 x 的原始值
    x = x + COS10 - y*SIN10; // 计算新值
    // x 的值改变了，但 y 的计算取决于
    // x 的原始值，使用 x_old 代替 x。
    y = x_old + SIN10 + y*COS10; // 根据 y_old 逻辑修正

    // 计算新距离
    double d2 = sqrt((p_x - x)*(p_x - x) + (p_y - y)*(p_y - y));

    // 输出距离差
    cout << "Difference in distances: " << d2 - d1 << endl;

    return 0;
}
```

我们使用平方根来提高程序的效率。与其尝试从 $2$ 直到 $n-1$ 的所有因子，我们只考虑直直到 $n$ 平方根的潜在因子。Listing 8.5: moreefficientprimes.cpp 使用 `sqrt` 函数减少了需要考虑的因子数量。

```cpp
#include <iostream>
#include <cmath>

using namespace std;

int main() {
    int max_value;
    cout << "Display primes up to what value?";
    cin >> max_value;
    for (int value = 2; value <= max_value; value++) {
        // 检查 value 是否为质数
        bool is_prime = true; // 暂时假设 value 是质数
        double r = value, root = sqrt(r);
        // 尝试从 2 到 value 平方
        // 的所有可能因子
        for (int trial_factor = 2; trial_factor <= root; trial_factor++) {
            if (value % trial_factor == 0) {
                is_prime = false;
                break;
            }
        }
        if (is_prime)
            cout << value << " "; // 显示质数
    }
    cout << endl; // 光标移到下一行
    return 0;
}
```

## 8.3. 最大值与最小值

`sqrt` 函数有三种形式：

```cpp
double sqrt(double)
float sqrt(float)
long double sqrt(long double)
```

函数名相同，但参数不同。我们说 `sqrt` 函数是重载的。（重载函数在第 10.3 节中有详细介绍）。当调用者传递一个 `double` 参数时，编译器会选择最匹配的原型。当调用者传递 `float` 参数时，编译器会选择 `float` 版本。当将 `int` 传递给 `sqrt` 时，编译器无法决定使用哪一个版本（`float` 还是 `long double`）。调用者需要一些帮助来解决歧义，因此我们引入了 `double` 类型。

调用者需要一些帮助来解决歧义，因此我们引入了 `double` 类型。另一种选项是使用 `double` 类型进行 `sqrt` 函数。Listing 8.6 (maxmin.cpp) 演示了这些用法。

```cpp
Listing 8.6: maxmin.cpp
#include <iostream>
#include <algorithm>

using namespace std;

int main() {
    int value1, value2;
    cout << "Enter two integers: ";
    cin >> value1 >> value2;
    cout << "Maximum: " << max(value1, value2) << endl;
    cout << "Minimum: " << min(value1, value2) << endl;
    return 0;
}
```

## 8.4. CLOCK 函数

`clock()` 函数返回程序消耗的 CPU 时钟周期。它在 `<ctime>` 头文件中定义。我们可以使用该函数来测量程序的运行时间。

```cpp
#include <iostream>
#include <ctime>

using namespace std;

int main() {
    clock_t start_time = clock();
    // 执行一些操作
    for (int i = 0; i < 1000000; i++);
    clock_t end_time = clock();
    cout << "Time taken: " << (double)(end_time - start_time) / CLOCKS_PER_SEC << " seconds" << endl;
    return 0;
}
```

`CLOCKS_PER_SEC` 是一个常量，表示每秒包含的时钟周期数。通过除以这个常量，可以将 `clock()` 返回的值转换为秒。

## 8.5. 字符函数

C 库提供了许多对 C++ 程序员非常有用的字符函数。Listing 8.9 (toupper.cpp) 将小写字母转换为大写字母。

