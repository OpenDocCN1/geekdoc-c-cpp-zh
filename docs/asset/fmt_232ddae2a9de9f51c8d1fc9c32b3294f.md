
# 程序输出

数组的内容如下：
1 2 4 8 0 0 0

如果你留一个元素未初始化，则必须留其之后的所有元素也不初始化。C++ 不提供在初始化列表中跳过元素的方法。例如，以下代码是不合法的：

```cpp
int numbers[6] = {2, 4, 8, , 12}; // 非法！
```

## 隐式数组大小

只要提供初始化列表，就可以在不指定大小的情况下定义数组。C++ 会自动使数组足够大，以容纳所有初始化值。例如，以下定义创建了一个具有五个元素的数组：

```cpp
double ratings[] = {1.0, 1.5, 2.0, 2.5, 3.0};
```

由于省略了大小声明符，C++ 会计算初始化列表中的项目数量，并为数组分配相应数量的元素。

> 注意：如果你省略了数组的大小声明符，则必须提供初始化列表。否则，编译器不知道将数组设为多大。

## 从文件读取数据到数组

将文件内容读取到数组中是简单的：打开文件并使用循环从文件中读取每个项，将每个项存储在数组元素中。循环一直持续到数组填满或到达文件末。程序 7-7 展示了这一点，它打开一个存储了 10 个数字的文件，同时将文件内容读取到数组中。

## 7.2 访问数组元素

## 程序 7-7

```cpp
// 此程序从文件读取数据到数组。

#include <iostream>
#include <fstream>

using namespace std;

int main() {
    const int ARRAY_SIZE = 10; // 数组大小
    int numbers[ARRAY_SIZE]; // 具有10个元素的数组
    int count = 0; // 计数变量
    ifstream inputFile; // 输入文件流对象

    // 打开文件。
    inputFile.open("TenNumbers.txt");

    // 将数字从文件读取到数组。
    while (count < ARRAY_SIZE && inputFile >> numbers[count])
        count++;

    // 关闭文件。
    inputFile.close();

    // 显示读取的数字：
    cout << "The numbers are: ";
    for (count = 0; count < ARRAY_SIZE; count++)
        cout << numbers[count] << " ";
    cout << endl;

    return 0;
}
```

# 程序输出

数字为：101 102 103 104 105 106 107 108 109 110

第 17 行和第 18 行的 `while` 循环从文件中读取项并将其赋值给 `numbers` 数组的元素。注意循环测试了两个由 `&&` 运算符连接的布尔表达式：

- 第一个表达式是 `count < ARRAY_SIZE`。该表达式的目的是防止循环超出数组末尾。如果表达式为真，则测试第二个布尔表达式。然而，如果表达式为假，循环停止。
- 第二个表达式是 `inputFile >> numbers[count]`。该表达式从文件中读取一个值并将其存储在 `numbers[count]` 数组元素中。如果成功从文件中读取到一个值，该表达式为真，循环继续。然而，如果无法从文件中读取任何值，该表达式为假，循环停止。

循环每次迭代时，都会在第 18 行增加 `count`。

## 将数组内容写入文件

将数组内容写入文件也是一件简单的事。使用循环遍历数组的每个元素，将其内容写入文件。程序 7-8 展示了这一点。

## 程序 7-8

```cpp
// 此程序将数组内容写入文件。

#include <iostream>
#include <fstream>

using namespace std;

int main() {
    const int ARRAY_SIZE = 10; // 数组大小
    int numbers[ARRAY_SIZE]; // 具有10个元素的数组
    int count; // 计数变量
    ofstream outputFile; // 输出流对象

    // 在数组中存储值。
    for (count = 0; count < ARRAY_SIZE; count++)
        numbers[count] = count;

    // 打开文件用于输出。
    outputFile.open("SavedNumbers.txt");

    // 将数组内容写入文件。
    for (count = 0; count < ARRAY_SIZE; count++)
        outputFile << numbers[count] << endl;

    // 关闭文件。
    outputFile.close();

    // 就这样！
    cout << "The numbers were saved to the file.\n";

    return 0;
}
```

# 程序输出

数字已保存到文件中。

## SavedNumbers.txt 内容

- 0
- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9

## 7.3 C++ 中无边界检查

概念：C++ 不阻止你覆盖数组边界。

C++ 是需要编写快速高效代码的软件开发者的流行语言。为了提高运行效率，C++ 没有提供其他语言中常见的防止非法内存访问的保护措施。例如，C++ 不进行数组边界检查。这意味着你可以编写超出特定数组边界的下标。程序 7-9 展示了这种能力。

> 警告！程序 7-9 将尝试写入数组之外的内存区域。这是一个非法操作，并可能导致程序崩溃。

## 程序 7-9

```cpp
// 警告：程序 7-9 将尝试写入数组之外的内存区域。
// 这是一个非法操作并可能导致程序崩溃。

#include <iostream>

using namespace std;

int main() {
    const int SIZE = 5;
    int numbers[SIZE] = {1, 2, 3, 4, 5};

    // 这是一个越界访问
    numbers[SIZE] = 10;

    cout << "The value at index 5 is: " << numbers[SIZE] << endl;

    return 0;
}
```

## 图 7-11 写入数组边界之外的数据

（此处应为图片描述）

# 检查点

定义以下数组：

- A) `empNums`，一个包含 100 个元素的整型数组
- B) `payRates`，一个包含 25 个元素的浮点型数组
- C) `miles`，一个包含 14 个元素的长整型数组
- D) `cityName`，一个包含 26 个元素的字符串对象数组
- E) `LightYears`，一个包含 1000 个元素的双精度浮点型数组

以下数组定义中哪些是错误的：
`int readings[-1];`
`float measurements[4.5];`
`int size;`
`string names[size];`

在一个包含 4 个元素的双精度浮点数组中，下标值是什么？

数组的声明符（declarator）和下标（subscript）之间的区别是什么？

什么是“数组边界检查”？C++ 执行此操作吗？

以下代码的输出是什么：
```cpp
int values[5]; int count;

for (count = 0; count < 5; count++)
    values[count] = count + 1;

for (count = 0; count < 5; count++)
    out << values[count] << endl;
```

以下程序骨架包含一个名为 `fish` 的包含 20 个元素的整型数组。完成后，该程序应该询问第 1 到第 20 号渔民捕到了多少条鱼，并将这些数据存储在数组中。完成该程序：
```cpp
#include <iostream>

using namespace std;

int main() {
    const int NUM_FISH = 20;
    int fish[NUM_FISH];

    // 你必须完成这个程序。它应该询问
    // 1-20 号渔民捕获了多少条鱼，
    // 并这些数据存储在 fish 数组中。

    return 0;
}
```

定义以下数组：

- A) `ages`，一个包含 10 个元素的整型数组，初始化值为 5, 9, 14, 15, 17, 18, 19 和 23。
- B) `temps`，一个包含 7 个元素的浮点型数组，初始化值为 14.7, 16.3, 18.43, 21.09, 17.9, 18.76 和 26.7。
- C) `alpha`，一个包含 8 个元素的字符型数组，初始化值为 'J', 'B', 'L', 'A', '*', '$', 'H' 和 'M'。

# 第7章 数组与向量

## 7.9 以下每个数组定义是有效的还是无效的？（如果定义无效，请解释原因）。

- A) `int numbers[10] = {0, 0, 1, 0, 0, 1, 0, 0, 1, 1};`
- B) `int matrix[5] = {1, 2, 3, 4, 5, 6, 7};`
- C) `double radii[10] = {3.2, 4.7};`
- D) `int table[7] = {2, , 27, , 45, 39};`
- E) `char codes[] = {'A', 'X', '1', '2', 's'};`
- F) `int blanks[];`

# 7.4 基于范围的 for 循环

概念：基于范围的 for 循环是一种对数组中每个元素进行迭代的循环。循环每次迭代时，它会将数组中的一个元素拷贝到变量中。基于范围的 for 循环是在 C++11 中引入的。

C++ 11 提供了 for 循环的特殊版本，在许多情况下用于简单的数组处理。它被称为基于范围的 for 循环。当你使用基于范围的 for 循环时，数组会为数组中的每个元素自动迭代一次。例如，如果你对一个包含 8 个元素的数组使用基于范围的 for 循环，循环将迭代 8 次。因为基于范围的循环会自动知道数组中的元素数量，所以你不需要像普通循环那样使用计数器来控制迭代。此外，在使用基于范围的 for 循环时，你不必超出数组边界。

基于范围的 for 循环设计用于处理内置数组。循环每次迭代时，它会将数组元素拷贝给范围变量。例如，循环第一次迭代时，范围变量将包含元素 0 的值；第二次迭代时，范围变量将包含元素 1 的值，以此类推。

这是基于范围 for 的通用格式：

```cpp
for (dataType rangeVariable : array)
    statement;
```

让我们仔细查看语法：

- `dataType` 是范围变量的类型。它必须与数组的类型相同，或者是可以转换为元素的类型。
- `rangeVariable` 是变量的名称。
- `statement` 是循环迭代期间执行的语句。

例如，假设有以下数组定义：

```cpp
int numbers[] = {3, 6, 9};
```

你可以使用以下基于范围的循环显示数组的内容：

```cpp
for (int val : numbers)
    cout << val << endl;
```

由于 `numbers` 数组有三个元素，循环将迭代三次。第一次迭代时，范围变量将包含元素 0 的值。第二次迭代时，范围变量将包含元素 1 的值。第三次迭代时，范围变量将包含元素 2 的值。输出如下：

```
3
6
9
```

同样注意第 20 行，我们没有将 `val` 声明为引用变量（变量名前面没有写 `&` 符号）。因为循环仅仅是在显示数组元素，不需要修改数组的内容，所以没有必要将 `val` 变为引用变量。

## 范围 for 循环与普通 for 循环

在任何需要遍历数组元素且不需要使用元素下标的情况下，都可以使用范围 for 循环。然而，在由于某些目的需要使用元素下标的情况下，它将无法工作。在这些情况下，你需要使用普通的 `for` 循环。

![](img/191adf3284699566e6a7b1008ce9bdb5_435_0.png)

> 注意：你可以在引用范围变量上使用 `auto` 关键字。例如，程序 7-12 中第 12 到第 16 行的代码可以写成：
```cpp
for (auto &val : numbers) {
    cout << "Enter an integer value: ";
    cin >> val;
}
```

# 7.5 处理数组内容

> 概念：单个数组元素的处理与处理任何其他类型的变量没有区别。

处理数组元素与处理其他变量没有区别。例如，以下语句将 `hours[3]` 乘以变量 `rate`：

```cpp
pay = hours[3] * rate;
```

以下是对数组元素进行前增和后增操作的示例：

```cpp
int score[5] = {7, 8, 9, 10, 11};
++score[2]; // 对 score[2] 中的值进行前增操作
score[4]++; // 对 score[4] 中的值进行后增操作
```

![](img/191adf3284699566e6a7b1008ce9bdb5_435_1.png)

> 注意：在使用增减运算符时，小心不要将下标与数组元素混淆。例如，以下语句递减了变量 `count`，但对 `amount[count]` 中的值没有做任何操作。
```cpp
amount[count--]
```

要减少存储在 `amount[count]` 中的值，请使用以下语句：
```cpp
amount[count]--;
```

## 程序 7-13

```cpp
// 该程序在数组中存储了工作小时数，
// 这些员工的时薪都相同。

#include <iostream>
#include <iomanip>

using namespace std;

int main() {
    const int NUM_EMPLOYEES = 5; // 员工人数
    int hours[NUM_EMPLOYEES]; // 用于存储小时数的数组
    double pay; // 时薪
    double grossPay; // 用于存储总工资

    // 输入工作小时数
    cout << "Enter the hours worked by: ";
    cout << NUM_EMPLOYEES << " employees who all\n";
    cout << "Enter the same hourly rate.\n";
    for (int index = 0; index < NUM_EMPLOYEES; index++) {
        cout << "Employee #" << (index + 1) << ": ";
        cin >> hours[index];
    }

    // 输入所有员工的时薪。
    cout << "Enter the hourly pay rate for all the employees: ";
    cout << fixed << setprecision(2);

    for (int index = 0; index < NUM_EMPLOYEES; index++) {
        grossPay = hours[index] * pay;
        cout << "Employee #" << (index + 1) << ": $" << grossPay << endl;
    }

    return 0;
}
```

# 程序输出（示例输入已加粗显示）

Enter the hours worked by 5 employees who all
earn the same hourly rate.
Employee #1: **10** Enter
Employee #2: **10** Enter
Employee #3: **15** Enter
Employee #4: **20** Enter
Employee #5: **40** Enter
Enter the hourly pay rate for all the employees: **12.75** Enter
Here is the gross pay for each employee:
Employee #1: $63.75
Employee #2: $127.50
Employee #3: $191.25
Employee #4: $255.00
Employee #5: $510.00

第 33 行的语句将 `hours[index]` 乘以 `pay` 的值赋值给 `grossPay` 变量：

```cpp
grossPay = hours[index] * payRate;
```

数组元素也可以用于关系表达式。例如，以下 `if` 语句测试了 `cost[20]` 以判断其是否小于 `cost[0]`：

```cpp
if (cost[20] < cost[0])
```

以下语句设置了一个 `while` 循环，只要 `value[place]` 不等于 0 就会继续：

```cpp
while (value[place] != 0)
```
