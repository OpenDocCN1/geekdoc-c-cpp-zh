
以下示例对此作了进一步说明。

### 示例 2-30

考虑以下 C++ 程序：

```cpp
//An improperly formatted C++ program.

#include <iostream>
#include <string>
using namespace std;

int main()
{
int num; double height;
string name;
cout << "Enter an integer: "; cin >> num; cout << endl;
cout<<"num: "<<num<<endl;
cout<<"Enter the first name: "; cin>>name;
  cout<<endl; cout <<"Enter the height: ";
cin>>height; cout<<endl;

cout<<"Name: "<<name<<endl;cout<<"Height: "
<<height; cout <<endl;return 0;
}
```

该程序在语法上是正确的；C++ 编译器读取和编译该程序不会有任何困难。然而，这个程序非常难读。你编写的程序应当正确缩进并格式化。请注意重新格式化该程序后的区别：

```cpp
//A properly formatted C++ program.

#include <iostream>
#include <string>

using namespace std;

int main()
{
    int num;
    double height;
    string name;

    cout << "Enter an integer: ";
    cin >> num;
    cout << endl;
    cout << "num: " << num << endl;

    cout << "Enter the first name: ";
    cin >> name;
    cout << endl;
    cout << "Enter the height: ";
    cin >> height;
    cout << endl;

    cout << "Name: " << name << endl;
    cout << "Height: " << height << endl;

    return 0;
}
```

如你所见，这个程序更易于阅读。你的程序应当正确缩进并格式化。为了说明变量，程序员通常每行声明一个变量。此外，始终在运算符前后各放一个空格。当你使用 IDE 输入程序时，程序通常会自动缩进。

## 关于赋值语句的更多内容

到目前为止，你见到的赋值语句称为**简单赋值语句**。在某些情况下，你可以使用称为**复合赋值语句**的特殊赋值语句，以更简洁的表示法编写简单赋值语句。

对应于五个算术运算符 +、-、*、/ 和 %，C++ 分别提供五个复合运算符：+=、-=、*=、/= 和 %=。考虑以下简单赋值语句，其中 x 和 y 是 int 变量：

```cpp
x = x * y;
```

使用复合运算符 *=，该语句可以写为：

```cpp
x *= y;
```

通常，使用复合运算符 *=，你可以将以下简单赋值语句：

```cpp
variable = variable * (expression);
```

重写为：

```cpp
variable *= expression;
```

其他算术复合运算符也有类似的约定。例如，使用复合运算符 `+=`，你可以将以下简单赋值语句：

```cpp
variable = variable + (expression);
```

重写为：

```cpp
variable += expression;
```

复合赋值语句通过将算术运算符与赋值运算符组合，使你能够以简洁的方式编写简单赋值语句。

### 示例 2-31

本示例展示了若干与简单赋值语句等效的复合赋值语句。

| 简单赋值语句 | 复合赋值语句 |
|---|---|
| `i = i + 5;`<br>`counter = counter + 1;`<br>`sum = sum + number;`<br>`amount = amount * (interest + 1);`<br>`x = x / (y + 5);` | `i += 5;`<br>`counter += 1;`<br>`sum += number;`<br>`amount *= interest + 1;`<br>`x /= y + 5;` |

> **注意**
>
> 任何复合赋值语句都可以转换为简单赋值语句。但是，简单赋值语句可能无法（轻松地）转换为复合赋值语句。例如，考虑以下简单赋值语句：
>
> ```cpp
> x = x * y + z - 5;
> ```
>
> 要将该语句写为复合赋值语句，变量 `x` 必须是右侧的公因子，但这里并非如此。因此，你不能立即将该语句转换为复合赋值语句。事实上，等效的复合赋值语句是：
>
> ```cpp
> x *= y + (z - 5) / x;
> ```
>
> 这比简单赋值语句更复杂。此外，在前面的复合语句中，`x` 不能为 0。我们建议避免此类复合表达式。

## 编程示例：长度转换

![](img/d0be7fc6d804b63484835c6c8bc67a07_146_0.png)

编写一个程序，输入以英尺和英寸表示的长度。然后，程序应将这些长度转换为厘米并输出。假设给定的英尺和英寸长度是整数。

**输入** 以英尺和英寸表示的长度。

**输出** 以厘米表示的等效长度。

### 问题分析与算法设计

长度以英尺和英寸给出，你需要求出以厘米表示的等效长度。1 英寸等于 2.54 厘米。程序首先需要将给定的英尺和英寸长度转换为总英寸数。然后，你可以使用换算公式 1 英寸 = 2.54 厘米，求出以厘米表示的等效长度。要将英尺和英寸长度转换为英寸，需要将英尺数乘以 12（因为 1 英尺等于 12 英寸），再加上给定的英寸数。

例如，假设输入为 5 英尺 7 英寸。那么，总英寸数计算如下：

```text
totalInches = (12 * feet) + inches
             = 12 * 5 + 7
             = 67
```

然后，你可以应用换算公式 1 英寸 = 2.54 厘米，求出以厘米表示的长度。

```text
centimeters = totalInches * 2.54
            = 67 * 2.54
            = 170.18
```

基于对问题的这一分析，可以设计如下算法：

- 1. 获取以英尺和英寸表示的长度。
- 2. 将长度转换为总英寸数。
- 3. 将总英寸数转换为厘米。
- 4. 输出厘米数。

#### 变量

程序的输入是两个数：一个表示英尺，一个表示英寸。因此，需要两个变量：一个存储英尺，另一个存储英寸。由于程序首先会将给定长度转换为英寸，因此需要另一个变量来存储总英寸数。还需要一个变量来存储以厘米表示的等效长度。总之，需要以下变量：

```cpp
int feet;            //variable to hold given feet
int inches;          //variable to hold given inches
int totalInches;     //variable to hold total inches
double centimeters;  //variable to hold length in centimeters
```

#### 命名常量

要计算以厘米表示的等效长度，需要将总英寸数乘以 2.54。与其在程序中直接使用值 2.54，不如将该值声明为命名常量。类似地，要计算总英寸数，需要将英尺数乘以 12 再加上英寸数。与其在程序中直接使用 12，不如也将该值声明为命名常量。使用命名常量使以后修改程序更容易。

```cpp
const double CENTIMETERS_PER_INCH = 2.54;
const int INCHES_PER_FOOT = 12;
```

#### 主算法

在前面的各节中，我们分析了问题并确定了用于计算的公式。我们还确定了所需的变量和命名常量。现在，我们可以扩展“问题分析与算法设计”一节中给出的算法，以解决本编程示例开头提出的问题。

- 1. 提示用户输入。（如果没有提示行，用户将面对空白屏幕，不知道该怎么办。）
- 2. 获取数据。
- 3. 回显输入——也就是说，输出程序读取到的输入内容。（如果没有这一步，程序执行后，你将不知道输入是什么。这也是确保程序正确接收输入的好方法。）
- 4. 计算以英寸表示的长度。
- 5. 输出以英寸表示的长度。
- 6. 将长度转换为厘米。
- 7. 输出以厘米表示的长度。

#### 整合起来

现在，问题已经分析完毕，算法也已经设计好，下一步是将算法转换为 C++ 代码。由于这是你编写的第一个完整的 C++ 程序，让我们按顺序回顾必要的步骤。

程序将以注释开头，说明其目的和功能。由于这个程序既有输入（以英尺和英寸表示的长度），又有输出（以厘米表示的等效长度），你将使用系统资源进行输入/输出。换句话说，程序将使用输入语句将数据读入程序，并使用输出语句打印结果。由于数据将从键盘输入，输出将显示在屏幕上，程序必须包含头文件 iostream。因此，在如上所述的注释之后，程序的第一条语句将是包含该头文件的预处理指令。

这个程序需要两类内存位置来进行数据操作：命名常量和变量。通常，命名常量保存特殊数据，例如 CENTIMETERS_PER_INCH。根据命名常量的性质，它可以

![](img/d0be7fc6d804b63484835c6c8bc67a07_147_0.png)
