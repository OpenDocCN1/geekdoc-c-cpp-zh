

## 输入

输入的处理方式与输出非常相似。值被流向变量中。你通过用户在窗口中输入数据来获取输入。这个窗口再次被称为控制台（console），因此使用 *cin* 一词来表示你从控制台输入。

正如输出表示信息流应该从变量流向 *cout* 一，对于输入，信息将从 *cin* 向右流向变量。因此，你将使用 `>>` 来表示这一点；数据流的方向是从 *cin* 到变量。

看这段修改后的卡路里计算代码。首先，有一个用于控制台输出的**流运算符**，它指示用户如何对 (10) 进行操作。在这种情况下，用户需要输入每种类型的克数。

接下来，你有 3 行 *cin* 代码，表示你将从控制台获取的输入 (h)。

其中第一行表示用户输入的第一个内容将存储在变量 *carb_grams* 中。用户输入的第二个内容进入 *protein_grams*，第三个将进入 *fat_grams*。

```cpp
// Program 2_19
// 根据用户输入计算菜肴的热量
#include <iostream>
using namespace std;

int main() {
    int carb_grams;
    int protein_grams;
    int fat_grams;

    cout << "Enter the number of grams of carbohydrates, protein, and fat, separated by spaces." << endl;
    cin >> carb_grams;
    cin >> protein_grams;
    cin >> fat_grams;

    int calories = 4 * carb_grams + 4 * protein_grams + 9 * fat_grams;
    cout << "There are " << calories << " calories in this dish" << endl;
}
```

简而言之，现在用户可以选择每种类型的克数，而不是被固定在代码中设置的初始值。

如果你运行程序并输入值 10、20 和 30（例如），你会得到一个输出，告诉该菜肴有 390 卡路里；也就是说，一份含有 10 克碳水化合物、20 克蛋白质和 30 克脂肪的菜肴将 390 卡路里。

就像输出流可以在每行中通过多个流运算符组合一样，你可以在一行中组合多个输入流运算符。你在这里看到的输入行与之前显示的 3 行相同。

```cpp
cin >> carb_grams >> protein_grams >> fat_grams;
```

你将第一部分输入数据读入 carb_grams，第二部分读入 protein_grams，第三部分读入 fat_grams。程序给出与之前相同的输出。

如果你想用 3 个不同的问题向用户索问碳水化合物、脂肪和蛋白质的克数呢？

你可以设置 3 行不同的输出，每行显示要输入的内容，如程序 2_21 所示。每一行后面都有一个独立的行，返回每个变量中的值。

```cpp
// Program 2_21
// 提示用户进行多次输入
#include<iostream>
using namespace std;

int main() {
    int carb_grams;
    int protein_grams;
    int fat_grams;

    cout << "Enter the number of grams of carbohydrates: ";
    cin >> carb_grams;
    cout << "Enter the number of grams of protein: ";
    cin >> protein_grams;
    cout << "Enter the number of grams of fat: ";
    cin >> fat_grams;

    int calories = 4 * carb_grams + 4 * protein_grams + 9 * fat_grams;
    cout << "There are " << calories << " calories in this dish" << endl;
}
```

## 阅读材料

- a Stroustrup, Programming Principles and Practice Using C++, 第 3 章和 4.1–4.3 节。
- b Lippman, Lajoie, and Moo, C++ Primer, 2.1–2.2 节。
- c Csterhout, A Philosophy of Software Design, 第 14 章（关于命名）：

## 命名

## 练习 1 答案

## 练习 2 答案

tank_capacity 和 length2 都是有效的且具有一定的描述性。

## 有效名称
（但不是很好的选择）

给变量命名为 something 提供的关于它应该包含的内容信息太少。

i 作为变量名也是有效的。在某些情况下，你可以使用单个字母如 i，例如，在数学中，你可能有一个值如 x，并使用 i 作为下标或上标。

像 account 这样的名字并不糟糕，但它并不清楚存储的是什么值：是账户余额、账户 ID、账户名称等吗？account_balance 这样的名字要容易理解得多。

代码可能是这样的：

```cpp
// Program 2_7
// 将周转换为天数的程序
#include <iostream>
using namespace std;

int main() {
    int weeks = 28;
    int days = weeks * 7;
    cout << "There are " << weeks << " days in " << days << " weeks." << endl;
}
```

```cpp
// Program 2_8
// 在声明时初始化变量
#include <iostream>
using namespace std;

int main() {
    int weeks = 20;
    int days = weeks * 7;
    cout << "There are " << weeks << " days in " << days << " weeks." << endl;
}
```

## 或者

点击返回练习。

## 无效名称

## 练习 3 答案

不能使用关键字如 namespace。

名称中不能有空格，所以 left foot 是不允许的；如果你想分隔单词，需要使用下划线。

注意你声明了 3 个变量：x、y 和 z。x 初始化为 3。接下来，将 x 赋值给 y，然后 y 的值也是 3。接下来，z 得到 x 乘以 y 的值，即 3、0 或 9。然后，将值 5.5 赋值 x 和 y，z 不受影响。因此，当你用 cout 语句将 3 个变量的值输出时，你得到：

名称中不允许标点符号，如感叹号，所以 Success! 是错误的。

名称不能以数字开头，所以不能有 2nd_account。

5.5 3 9。

点击返回练习。

点击返回练习。

## 测验

- 1 声明了多少变量？
- 2 输出是什么？
- 3 输出是什么？
- 4 有许多可能的解决方案。这是其中之一：

## 测验答案

- 1 有 3 个变量：score, dozen 和 totalnum。
- a 输出是 236。
- 2 这是 2 行代码的示例：
- 3 这是单行代码的示例：

