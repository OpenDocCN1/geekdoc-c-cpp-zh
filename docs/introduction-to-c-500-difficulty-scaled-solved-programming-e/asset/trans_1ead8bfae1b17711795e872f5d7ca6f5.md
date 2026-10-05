
要使一个指针变量指向结构体成员，其类型必须与该成员的类型兼容。例如，成员 year 的类型是 int，那么 p2 就被声明为 **int\***。

## 结构体操作

虽然我们不能使用 `=`运算符将一个数组复制到另一个数组，但可以使用它将一个结构体拷贝到另一个。结构体的类型必须相同。考虑以下程序：

```cpp
struct Student
{
    int code;
    float grd;
}

int main()
{
    Student s1, s2;
    s1.code = 1234;
    s1.grd = 6.7;
    s2 = s1; // 结构体
    ...
}
```

语句 `s2 = s1;` 将 s1 的成员拷贝到 s2。它等同于：

```cpp
s2.code = s1.code;
s2.grd = s1.grd;
```

请注意，如果 s1 和 s2 不是相同结构体类型的变量，即使这两个类型包含完全相同的成员，语句 `s2 = s1;` 也无法编译。

同样注意，如果结构体包含一个字符数组（例如 `char name[100];`），虽然不允许编写 `s2.name = s1.name;`，但一旦结构体被拷贝（例如 `s2 = s1`），s1 数组就会被拷贝到 s2。此外，如果它包含一个指针成员，拷贝后两个指针将指向同一个地方。我们将在接下来的章节中看到原因。

除了赋值之外，不能对整个结构体执行任何其他操作。例如，`==` 和 `!=` 运算符不能测试两个结构体是否相等。因此，不允许编写：

```cpp
if(s1 == s2) or if(s1 != s2).
```

要测试两个结构体是否相等，我们需要逐个比较它们的成员。例如：

```cpp
if((s1.code == s2.code) && (s1.grd == s2.grd))
```

在序言中，我告诉过你们学习编程时可能需要什么。这里有一个例子：有一次，我必须比较两个结构体。它们不包含比较可能危险的成员，例如浮点数成员、指针或字符数组。因为结构体包含许多成员，为了节省编写时间，我使用了 `memcmp()`（我们将在第4章看到它），而不是一个一个地比较。然而，我忘记了，那些不确定的成员可能会被添加到结构体中。那么，对两个结构体的比较，即使相应的成员具有相同的值，也可能因为那些中运气中的不同值而出现问题。我很幸运的是，那些值是相同的。更幸运的是，我不需要将应用程序迁移到另一个平台。想象一下这种情况：比较在我的平台上可以运行，但在客户那里却不行，因为那里有不同的漏洞。我一想到找那个 bug 就感到害怕！有时每个程序员都需要一个运气的避风港，就像滚石滚乐队的《Gimme Shelter》。

## 包含数组的结构体

由于结构体可以包含任何类型的数据，它可能包含一个或多个数组。例如，以下程序的输出是什么？

```cpp
#include <iostream> // 示例 13.3
#include <string>
#include <cstring>
struct Student
{
    char name[50];
    float grd[2];
}
int main()
{
    Student s1, s2;
    strcpy(s1.name, "somebody");
    s1.grd[0] = 8.5;
    s1.grd[1] = 7.5;
    std::cout << s1.name << ' ' << s1.name[0] << ' ' << *s1.name << '\n';
    s2 = s1;
    std::cout << s2.name << ' ' << s2.grd[0] << ' ' << s2.grd[1] << '\n';
    return 0;
}
```

如你所示，数组成员被对待就像普通数组一样。对于示例，`strcpy(s1.name, "somebody");` 将字符串 "somebody" 拷贝到 `name`。`s1.name[0]` 的值变为 's'，`s1.name[1]` 变为 'o'，依此类推。

在使用指针运算处理数组元素时，`*` 运算符必须位于结构体名称之前。例如，由于 `s1.name` 可以用指向其第一个字符的指针，因此 `*s1.name` 等于 `s1.name[0]`，`*(s1.name+1)` 等于 `s1.name[1]`，依此类推。与普通数组一样，由于优先级原因，必须存在括号。赋值 `s2 = s1;` 拷贝了数组。因此，程序输出：

somebody s
somebody 8.5 7.5

## 包含指针的结构体

结构体可以包含一个或多个指针成员。指针成员被对待就像普通数组一样。例如，以下程序的输出是什么？

```cpp
#include <iostream> // 示例 13.4
struct Student
{
    const char *name;
    float *avg_grd;
}

int main()
{
    float grd = 8.5;
    Student s1, s2;

    s1.name = "somebody";
    s1.avg_grd = &grd;
    std::cout << s1.name+3 << ' ' << *s1.avg_grd << '\n';

    s2.name = "else";
    s2 = s1;
    grd = 3.4;
    std::cout << s2.name << ' ' << *s2.avg_grd << '\n';
    return 0;
}
```

通过语句 `s1.name = "somebody"`，编译器分配内存来存储字符串 "somebody"，然后 `name` 指向该内存的开始。语句 `s1.avg_grd = &grd` 使 `s1.avg_grd` 指向 `grd` 的地址。要访问指针成员指向的内存的内容，`*` 运算符必须位于结构体名称之前。因此，程序显示：everybody 8.5。

然后，语句 `s2 = s1;` 使 s2 的指针指向与 s1 指针相同的地方。因此，程序显示：somebody 4（这是小心的结果，不是 else）。

我放这个语句是为了警告你在拷贝包含指针的结构体时要小心。目标结构体（例如 s2）的指针的当前值将会丢失。所以，请注意，这可能会在你的程序中引起严重问题。

> 拷贝包含指针的结构体时要小心。

## 嵌套结构体

结构体可以包含一个或多个结构体。嵌套结构体必须包含它的结构体之前声明，否则编译将失败。对于以下程序，prod 包含了嵌套结构体 s_date 和 e_date。s_date 保存生产日期，e_date 保存有效期。

```cpp
#include <iostream> // 示例 13.5
#include <string>

struct Date
{
    int day;
    int month;
    int year;
}

struct Product {/* 由于 Date 类型已经声明，它可以用于声明嵌套结构体。 */
{
  std::string name;
  double price;
  Date s_date;
  Date e_date;
}

int main()
{
  Product prod;

  prod.name = "product";
  prod.s_date.day = 1;
  prod.s_date.month = 9;
  prod.s_date.year = 2018;

  prod.e_date.day = 1;
  prod.e_date.month = 9;
  prod.e_date.year = 2022;

  prod.price = 7.5;
  std::cout << "The product's life is " << prod.e_date.year - prod.s_date.year << " years";
  return 0;
}
```

请注意，为了访问嵌套结构体的成员，必须使用两次运算符。程序处理相应的成员并显示产品的寿命。通常情况下，结构体允许包含一个包含另一个结构体的结构体，依此类推。

让我们来看一个特殊情况。假设我们要声明两个相互依赖的结构体，结构体 A 和结构体 B。
