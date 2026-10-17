
该语句将 `numbers` 定义为 `int` 类型的向量。注意数据类型包含在尖括号内，紧跟在 `vector` 单词之后。因为 `vector` 会随着你向其添加值而扩展，因此不需要声明大小。不过，如果你愿意，也可以声明一个起始大小。这是一个示例：

```cpp
vector<int> numbers(10);
```

该语句将 `numbers` 定义为包含 10 个 `int` 的向量，但这仅是起始大小。如果你向它添加了超过 10 个值，它的大小将会扩展。

> 注意：注意，如果你为 `vector` 指定了起始大小，大小声明符被圆括号包含，而不是方括号。

img/c095ef63c71a34f9802f104f947be57_598_0.png

当你为 `vector` 指定起始大同时，也可以指定一个初始化值。这是一个示例：

```cpp
vector<int> numbers(10, 2);
```

在该语句中，`numbers` 被定义为包含 10 个 `int` 的向量。每个元素都被初始化为 2。

你还可以使用另一个向量中的值来初始化一个 `vector`。例如，如果 `set1` 是一个已经有值的 `int` 向量，以下语句将创建一个名为 `set2` 的新 `vector`，它是 `set1` 的精确拷贝：

```cpp
vector<int> set2(set1);
```

执行该语句后，向量 `set2` 将具有 `set1` 相同数量的元素并持有相同的值。

如果你使用的是 C++11，还可以使用值列表来初始化 `vector`，如示例所示：

```cpp
vector<int> numbers {10, 20, 30, 40};
```

该语句定义了一个名为 `numbers` 的 `int` 向量。该向量包含 10, 20, 30, 40 等值，这种初始化方式使用了大括号。

| 定义 | 描述 |
|---|---|
| `vector<string> names;` | 定义了一个空字符串向量。 |
| `vector<int> scores(15);` | 定义了一个包含 15 个整数的向量。 |
| `vector<char> letters(25, 'A');` | 定义了一个包含 25 个字符的向量，每个元素初始化为 'A'。 |
| `vector<double> values2(set1);` | 定义了 `set1` 的一个双数向量。 |

# 在向量中存储和检索值

```cpp
// 此程序将工作时和薪率存储在两个并行向量中。
#include <iostream>
#include <iomanip>
#include <vector> // 需要来使用向量
using namespace std;
int main() {
    // 获取员工数据
    const int NUM_EMPS = 5;         // 员工数量
    vector<int> hours(NUM_EMPS);     // 定义整数向量
    vector<double> payRate(NUM_EMPS); // 定义双精度向量
    double grossPay;               // 员工的总薪资
    cout << "输入 " << NUM_EMPS << " 名员工的工时和小时薪率：\n";
    for (int index = 0; index < NUM_EMPS; index++) {
        cout << "员工 #" << (index + 1) << "的工作时: ";
        cin >> hours[index];
        cout << "该员工的小薪率: ";
        cin >> payRate[index];
    } // 显示每个员工的总薪资
    cout << "\n每个员工的总薪资：\n";
    cout << fixed << showpoint << setprecision(2);
    for (int index = 0; index < NUM_EMPS; index++) {
        grossPay = hours[index] * payRate[index];
        cout << "员工 #" << (index + 1) << " ";
        cout << setw(7) << grossPay << endl;
    }
    return 0;
}
```

要向已存在的 `vector` 元素存储一个值，或访问存储在 `vector` 中的数据，你可以使用下标运算符 `[]`。程序 8-24 是程序 8-15 的修改，说明了这一点。

## 在 C++ 11 中对 vector 使用范围的 for 循环

有了 C++ 11，你也可以使用范围的 for 循环来遍历 vector 的元素，就像你之前在本章中遍历数组时做的那样。程序 8-25 展示了这一点。

### 程序 8-25

```cpp
// 此程序对 vector 使用了两个范围的 for 循环。
#include <iostream>
#include <vector>
using namespace std;
int main() {
    // 定义一个初始大小为 5 个元素的 vector
    vector<int> numbers(5);
    // 获取 vector 元素的值
    // 将范围变量设为引用，以便可以
    // 更改元素引用的内容。
    for (int &val : numbers) {
        cout << "Enter an integer value: ";
        cin >> val;
    }
    // 显示 vector 元素
    cout << "\nhere the values you entered: \n";
    for (int val : numbers) {
        cout << val << " ";
    }
    cout << endl;
    return 0;
}
```

### 程序输出（示例输入用粗体显示）

Enter an integer value: 10
Enter an integer value: 20
Enter an integer value: 30
Enter an integer value: 40
Enter an integer value: 50

Here are the values you entered:
10 20 30 40 50

## 使用 push_back 成员函数

然而，你不能使用 `[]` 运算符来访问不存在的 vector 元素。要向没有初始大小或已满的 vector 存储值，你应该使用 `push_back` 成员函数。该函数接受一个值作为参数，并将其存储在 vector 末尾的新元素中。（它将值“推”到 vector 的“末尾”。）

### 第 8 章数组

以下是一个向名为 `numbers` 的 `int` vector 添加元素的示例。
`numbers.push_back(25);`

该语句创建了一个持有 25 的新元素，并将其置于 `numbers` 的末尾。
如果 `numbers` 之前没有元素，则新元素将成为它的唯一元素。

程序 8-24 是程序 8-23 的修改版本。然而，这个版本允许用户指定员工人数。两个 vector（`hours` 和 `payRate`）在定义时没有初始大小。因为这些 vector 没有初始元素，所以使用 `push_back` 成员函数向它们存储值。

### 程序 8-24

```cpp
// 此程序在两个 vector 中存储员工的工作小时和
// 小时薪率。它演示了使用 push_back 成员
// 函数向 vector 添加新元素。
#include <iostream>
#include <iomanip>
#include <vector>                               // 使用 vector 需要引入
using namespace std;
int main() {
    vector<int> hours;                          // hours 是一个空的 int vector
    vector<double> payRate;                      // payRate 是一个空的 double vector
    int numEmployees;                           // 员工人数
    int index; // 循环计数
    // 获取员工人数
    cout << "How many employees do you have? ";
    cin >> numEmployees;
    // 输入薪资数据
    cout << "Enter the hours worked and hourly pay rates of the "
    cout << numEmployees << " employees.\n";
    for (index = 0; index < numEmployees; index++) {
        int tempHours;                              // 输入的小时数
        double tempRate;                            // 输入的薪率
        cout << "Hours worked by employee #" << (index + 1) << ": ";
        cin >> tempHours;
        hours.push_back(tempHours);                // 向 hours 添加一个元素
        cout << "Hourly pay rate for employee #" << (index + 1) << ": ";
        cin >> tempRate;
        payRate.push_back(tempRate);                // 向 payRate 添加一个元素
    }
    // (程序继续)
}
```

### 程序 8-26（接）

```cpp
37 // 显示每位员工的总薪资
38 cout << "\nHere is the gross pay for each employee:\n";
39 cout << fixed << showpoint << setprecision(2);
40 for (int index = 0; index < numEmployees; index++)
41 {
42 grossPay = hours[index] * payRate[index];
43 cout << "Employee #" << (index + 1) << endl;
44 cout << "  $" << setw(7) << grossPay << endl;
45 }
46 return 0;
```
### 程序输出（示例输入用粗体显示）

How many employees do you have? 3
Enter the hours worked by 3 employees and their hourly rates.
Hours worked by employee #1: 40
Hourly pay rate for employee #1: 12.63
Hours worked by employee #2: 25
Hourly pay rate for employee #2: 10.35
Hours worked by employee #3: 45
Hourly pay rate for employee #3: 22.65

Here is the gross pay for each employee:
Employee #1: $ 505.20
Employee #2: $ 258.75
Employee #3: $ 1019.25

注意程序 8-26 第 40 到 45 行计算总薪资，使用 `[]` 运算符访问 `hours` 和 `payRate` vector，并显示结果。

## 获取 vector 的大小

与数组不同，vector 可以报告其大小。这是通过 `size` 函数实现的。这是一个示例：

```cpp
vector<int> set;
set.push_back(10);
set.push_back(20);
cout << set.size() << endl; // 输出 2
```

# 清空 Vector

要完全清空 vector 的内容，请使用 `clear` 成员函数，如下例所示：

`numbers.clear();`

执行此语句后，`numbers` 将清空所有元素。程序 8-29 展示了该函数。

## 程序 8-29

```cpp
1 // 此程序演示了 vector clear 成员函数。
2 #include <iostream>
3 #include <vector>
4 using namespace std;
5
6 int main() {
7 {
8 vector<int> values(100);
9
10 cout << "The values vector has "
11 << values.size() << " elements.\n";
12 cout << "I will call the clear member function...\n";
13 values.clear();
14 cout << "Now the values vector has "
15 << values.size() << " elements.\n";
16 return 0;
17 }
}
```

### 程序输出

The values have 100 elements.
I will call the clear member function...
Now the values vector has 0 elements.

# 检测空 Vector

要判断一个 vector 是否为空，请使用 `empty` 成员函数。如果 vector 为空，该函数返回 `true`；如果存储了元素，则返回 `false`。假设 `numberVector` 是一个 vector，以下是用法示例：

```cpp
if (numberVector.empty())
    cout << "No values in numberVector.\n";
```

程序 8-30 显示了如何将 vector 传递给函数。名为 `avgVector` 的函数演示了 `empty` 成员函数。

## 程序 8-30

```cpp
1 // 此程序演示了 vector empty 成员函数。
2 #include <iostream>
3 #include <vector>
4 using namespace std;
5
6 // 函数原型
7 double avgVector(vector<int>);
```
## 程序 8-30（续）

```cpp
int main() {
    vector<int> values; // 定义一个存储 int 值的 vector
    int numValues; // 需要计算平均值的个数
    double average; // 存储值的平均值
    // 获取需要计算平均值的个数
    cout << "How many values do you wish to average?";
    cin >> numValues;
    // 获取值并存入 vector
    for (int count = 0; count < numValues; count++) {
        cout << "Enter an integer value: ";
        cin >> tempValue;
        values.push_back(tempValue);
    }
    // 获取并显示值的平均值
    average = avgVector(values);
    cout << "Average: " << average << endl;
    return 0;
}
double avgVector(vector<int> vec) {
    int total = 0; // 累加器
    double average = 0.0;
    if (vec.empty()) {
        cout << "No values to average.\n";
    } else {
        for (int count = 0; count < vec.size(); count++) {
            total += vec[count];
        }
        average = static_cast<double>(total)/vec.size();
    }
    return average;
}
```
