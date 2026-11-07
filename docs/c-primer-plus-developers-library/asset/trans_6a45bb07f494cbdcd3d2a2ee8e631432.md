

```cpp
{
    double x;              // horizontal distance from origin
    double y;              // vertical distance from origin
};

// prototypes
polar rect_to_polar(rect xypos);
void show_polar(polar dapos);

int main()
{
    using namespace std;
    rect rplace;
    polar pplace;

    cout << "Enter the x and y values: ";
    while (cin >> rplace.x >> rplace.y) // slick use of cin
    {
        pplace = rect_to_polar(rplace);
        show_polar(pplace);
        cout << "Next two numbers (q to quit): ";
    }
    cout << "Done.\n";
    return 0;
}

// convert rectangular to polar coordinates
polar rect_to_polar(rect xypos)
{
    using namespace std;
    polar answer;

    answer.distance =
        sqrt(xypos.x * xypos.x + xypos.y * xypos.y);
    answer.angle = atan2(xypos.y, xypos.x);
    return answer;        // returns a polar structure
}

// show polar coordinates, converting angle to degrees
void show_polar (polar dapos)
{
    using namespace std;
    const double Rad_to_deg = 57.29577951;

    cout << "distance = " << dapos.distance;
    cout << ", angle = " << dapos.angle * Rad_to_deg;
    cout << " degrees\n";
}
```

## 注意

有些编译器需要显式指令来搜索数学库。例如，较旧版本的 g++ 使用以下命令行：

```
g++ structfun.C -lm
```

下面是程序清单 7.12 中程序的一次示例运行：

```
Enter the x and y values: 30 40
 distance = 50, angle = 53.1301 degrees
Next two numbers (q to quit): -100 100
 distance = 141.421, angle = 135 degrees
Next two numbers (q to quit): q
```

## 程序说明

我们已经讨论过程序清单 7.12 中的两个函数，所以让我们回顾一下该程序如何使用 cin 控制 while 循环：

```
while (cin >> rplace.x >> rplace.y)
```

回想一下，cin 是 istream 类的对象。提取运算符（>>）的设计方式是，`cin >> rplace.x` 也是该类型的对象。你将在第 11 章“使用类”中看到，类运算符是通过函数实现的。使用 `cin >> rplace.x` 时真正发生的是，程序调用一个返回 istream 类型值的函数。如果你对 `cin >> rplace.x` 对象应用提取运算符（如 `cin >> rplace.x >> rplace.y`），你又会得到一个 istream 类的对象。因此，整个 while 循环测试表达式最终求值为 cin，而你可能还记得，当 cin 用在测试表达式的上下文中时，会根据输入是否成功转换为 bool 值 true 或 false。例如，在程序清单 7.12 的循环中，cin 期望用户输入两个数字。相反，如果用户输入 q，如示例输出所示，`cin >>` 会识别出 q 不是数字。它把 q 留在输入队列中，并返回一个被转换为 false 的值，从而终止循环。

将这种读取数字的方法与下面这个更简单的方法进行比较：

```
for (int i = 0; i < limit; i++)
{
    cout << "Enter value #" << (i + 1) << ": ";
    cin >> temp;
    if (temp < 0)
        break;
    ar[i] = temp;
}
```

要提前终止这个循环，你可以输入一个负数。这会把输入限制为非负值。这种限制符合某些程序的需要，但更常见的是，你会希望有一种不会排除某些数值的循环终止方式。使用 `cin >>` 作为测试条件可以消除这种限制，因为它接受所有有效的数字输入。当你需要为数字编写输入循环时，应该记住这个技巧。此外，你还应该记住，非数字输入会设置错误条件，从而阻止读取更多输入。如果程序在输入循环之后还需要输入，你必须使用 `cin.clear()` 来重置输入，然后可能还需要通过读取来清除有问题的输入。程序清单 7.7 说明了这些技巧。

## 传递结构地址

假设你想通过传递结构的地址而不是传递整个结构来节省时间和空间。这需要重写函数，使它们使用指向结构的指针。首先，让我们看看如何重写 `show_polar()` 函数。你需要做三处修改：

- 调用函数时，向它传递结构的地址（`&place`），而不是结构本身（`place`）。
- 将形参声明为指向 polar 的指针，即类型 `polar *`。因为函数不应修改结构，所以使用 `const` 修饰符。
- 因为形参是指针而不是结构，所以使用间接成员运算符（`->`）而不是成员运算符（点）。

完成这些修改后，函数如下所示：

```cpp
// show polar coordinates, converting angle to degrees
void show_polar (const polar * pda)
{
    using namespace std;
    const double Rad_to_deg = 57.29577951;

    cout << "distance = " << pda->distance;
    cout << ", angle = " << pda->angle * Rad_to_deg;
    cout << " degrees\n";
}
```

接下来，让我们修改 `rect_to_polar`。这涉及的内容更多，因为原来的 `rect_to_polar` 函数返回一个结构。为了充分利用指针的效率，你应该使用指针而不是返回值。做到这一点的方法是向函数传递两个指针。第一个指针指向要转换的结构，第二个指针指向用于保存转换结果的结构。函数不返回新结构，而是修改调用函数中的现有结构。因此，虽然第一个参数是 `const` 指针，但第二个参数不是 `const`。除此之外，你应用用于将 `show_polar()` 转换为指针参数的相同原则。程序清单 7.13 展示了改写后的程序。

## 程序清单 7.13 **strctptr.cpp**

```cpp
// strctptr.cpp -- functions with pointer to structure arguments
#include <iostream>
#include <cmath>

// structure templates
struct polar
{
    double distance;       // distance from origin
    double angle;          // direction from origin
};
struct rect
{
    double x;              // horizontal distance from origin
    double y;              // vertical distance from origin
};

// prototypes
void rect_to_polar(const rect * pxy, polar * pda);
void show_polar(const polar * pda);

int main()
{
    using namespace std;
    rect rplace;
    polar pplace;

    cout << "Enter the x and y values: ";
    while (cin >> rplace.x >> rplace.y)
    {
        rect_to_polar(&rplace, &pplace);    // pass addresses
        show_polar(&pplace);                // pass address
        cout << "Next two numbers (q to quit): ";
    }
    cout << "Done.\n";
    return 0;
}

// show polar coordinates, converting angle to degrees
void show_polar (const polar * pda)
{
    using namespace std;
    const double Rad_to_deg = 57.29577951;

    cout << " distance = " << pda->distance;
    cout << ", angle = " << pda->angle * Rad_to_deg;
    cout << " degrees\n";
}

// convert rectangular to polar coordinates
void rect_to_polar(const rect * pxy, polar * pda)
{
    using namespace std;
    pda->distance =
        sqrt(pxy->x * pxy->x + pxy->y * pxy->y);
    pda->angle = atan2(pxy->y, pxy->x);
}
```

> **注意**
> 
> 有些编译器需要显式指令来搜索数学库。例如，较旧版本的 g++ 使用以下命令行：
> 
> ```bash
> g++ structfun.C -lm
> ```

从用户的角度来看，程序清单 7.13 中的程序行为与程序清单 7.12 中的程序相同。隐藏的区别在于，程序清单 7.12 处理的是结构的副本，而程序清单 7.13 使用指针，允许函数操作原始结构。

## 函数与 `string` 类对象

尽管 C 风格字符串和 `string` 类对象的作用大致相同，但 `string` 类对象与结构的关系比与数组的关系更密切。例如，你可以将一个结构赋给另一个结构，也可以将一个对象赋给另一个对象。你可以将结构作为完整实体传递给函数，也可以将对象作为完整实体传递。如果你需要多个字符串，可以声明一个 `string` 对象的一维数组，而不是 char 的二维数组。

程序清单 7.14 提供了一个简短示例，它声明一个 string 对象数组，并将该数组传递给一个显示其内容的函数。

### 程序清单 7.14 `topfive.cpp`

```cpp
// topfive.cpp -- handling an array of string objects
#include <iostream>
#include <string>
using namespace std;
const int SIZE = 5;
void display(const string sa[], int n);
int main()
{
    string list[SIZE];    // an array holding 5 string object
    cout << "Enter your " << SIZE << " favorite astronomical sights:\n";
```

