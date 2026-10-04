

// 程序 8_15

程序退出比打印随机数据是更好的结果，这听起来很奇怪。但当你访问随机数据时，谁知道会发生什么呢；通过使用 `at` 函数，你可以保证程序干净地退出。而且程序中还有处理异常的方法，使其不会发生崩溃。

括号。如果你尝试为一个不属于 vector 的元素设置值，`at` 命令将抛出一个异常，就像你之前在只打印时看到的那样。

// 使用方括号和 "at" 赋值元素

```
#include <iostream>
```

```
#include <vector>
```

```
using namespace std;
```

你也可以使用 `at` 命令为 vector 元素赋值，就像使用方括号赋值一样。

```
int main() {
```

虽然 `at` 确实是访问 vector 元素更安全的方法，但它也有缺点：每当你尝试用 `at` 访问元素时，计算机都会检查数组的边界以防止你执行不该做的操作，每次访问元素都会慢一点。

```
vector<int> v = { 1, 2, 3, 4, 5 };
```

```
v[1] = 100;
```

在程序 8_15 中，你创建了一个包含 5 个元素的 vector `v`，值从 1 到 5。使用方括号，你将第二个元素 `[1]` 设置为 100。然后，你使用 `at` 命令 (10) 将第四个元素 `[3]` 设置为 500。这让你能够访问 vector 的特定元素，并为其赋值。

```
v.at(3) = 500;
```

```
for (int i = 0; i < v.size(); i++) {
```

```
cout << v.at(i) << " ";
```

```
}
```

```
cout << endl;
```

```
cout << "Made it here!" << endl;
```

```
}
```

对于大多数程序员来说，这并不是什么问题；程序运行非常快，检查一个值所花费的微秒是微不足道的。但对于对性能至关重要的应用程序——即会有数百万次访问数组或 vector 元素的尝试——每次检查边界可能成为一个重要因素。因此，方括号与 `at` 的使用并不是一致的。

当你输出这个结果时，你会发现 vector 的第二个和第四个元素已经被修改了。`at` 函数的作用与方括号一样。

> 如果你想了解更多关于 vector 的知识，请查看 http://www.cplus.com/reference/vector/vector。

## // 向量的赋值

数组不具备的另一个特性是能够复制它们。

相反，如果你使用 vector，这种操作可以正常工作（程序 8_16）。你创建了两个整型 vector `a` 和 `b`，并初始化 `a` 包含 3 个元素，值为 1, 2 和 3。然后你有一个命令 `b = a`，它将 `a` 复制到 `b`。现在 `b` 本身拥有 3 个元素，且元素的值与 `a` 相同。当你打印 vector `b` 的元素时，你会发现它们与 `a` 相同。

在程序 8_16_a 中，你创建了两个大小为 3 的整型数组，命名为 `a` 和 `b`。在这种情况下，`a` 初始化为值 1、2和3。

你可能希望让 `b` 具有与 `a` 相同的值——本质是将 `a` 复制到 `b`。如果你尝试写一行 `b = a`，将得到编译错误。你不允许这样给数组。

从以后，你将依赖 vector 作为存储大量数据的首选数据结构。

```
// 程序 8_16_a
// 错误 - 不允许尝试赋值
#include <iostream>
using namespace std;

int main() {
    int a[3] = {1, 2, 3 };
    int b[3];
    b = a;
}

// 程序 8_16
// 向量赋值
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> a = {1, 2, 3 };
    vector<int> b;
    b = a;
    for (int i = 0; i < b.size(); i++) {
        cout << b[i] << " ";
    }
    cout << endl;
}
```

## 阅读材料

- a Stroustrup, *Programming Principles and Practice Using C++*, sections 4.6, 17.2, 17.3, and 18.5.
- b Lippman, Lajoie, and Moo, *C++ Primer*, section 3.3.

## 练习 1 答案

## 练习 2 答案

#include<vector>

...

vector<float> temperatures;

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_100_0.png)

// 程序 0.5
// 无限读取值并向 vector 添加元素
#include <iostream>
#include <vector>
using namespace std;
int main() {
    vector <int> ages;
    int age;
    cout << "输入某人的年龄。输入负数以停止： ";
    cin >> age;
    while (age >= 0) {
        ages.push_back(age);
        cout << "输入另一个年龄。输入负数以停止： ";
        cin >> age;
    }
}

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_100_1.png)

## // 测验

- 1. 执行以下每个操作的命令是什么？

对于接下来的2 个问题，请将这些与你在上一节课程等效练习中获得的解决方案进行比较。

- 3. 假设你有一组产品评分，你想找出哪些产品的评分高于平均值。编写一个程序，读取 ID 和评分，直到读到 ID 为 0。

- a. 创建两个并行 vector。
- b. 使用整型 vector 存储 ID。
- c. 创建一个浮点型 vector。
- d. 使用 `push_back` 命令向 vector 末尾添加元素。
- e. 使用 `size()` 方法获取 vector 的大小。

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc)

## // 测验答案

- 1. 执行以下每个操作的命令是什么？
    - a. `vector<int> v;`
    - b. `vector<int> v;`
    - c. `vector<float> v;`
    - d. `v.push_back(value);`
    - e. `v.size();`

- 3. 假设你有一组产品评分，你想找出哪些产品的评分高于平均值。编写一个程序，读取 ID 和评分，直到读到 ID 为 0。

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> ID;
    vector<float> rating;
    float sumofrings = 0.0;
    int i;
    cout << "输入产品 ID 和对应的评分，输入 ID 为 0 以停止" << endl;
    int id;
    float r;
    cin >> id >> r;
    while (id > 0) {
        ID.push_back(id); // 存储产品 ID
        rating.push_back(r); // 存储评分
        sumofrings += r; // 累加评分
        cin >> id >> r; // 读取下一个产品
    }
    int totalnumber = ID.size();
    float averaging = sumofrings / totalnumber;
    cout << "评分高于平均值的产品有：" << endl;
    for (i = 0; i < totalnumber; i++) {
        if (rating[i] > averaging) {
            cout << ID[i] << endl;
        }
    }
}
```

