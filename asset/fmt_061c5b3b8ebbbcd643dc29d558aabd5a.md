

### 输出：

```
The value is : 835
The value is : G
Size of structure : 8
The value is : 240
The value is : S
Size of structure : 8
```

### 代码解读

- 在这段代码中，我们创建了两个带有几个变量的结构体。结构体的创建使用了不同的语法。

- 创建结构体的对象来访问成员。

- 注意，整个结构体的大小变得不同，如同在类中一样。

- 代码展示了所做更改。

### 代码：使用多个结构体

```cpp
#include <iostream>
using namespace std;
struct OurStructure {
    int x;
    char c;
};
int main()
{
    struct OurStructure s1 = { 240,'S' };
    struct OurStructure* s2 = &s1;
    cout << "The value is : "<< s2->x << endl;
    cout << "The value is : "<< s2->c << endl;
    cout<<"Size of structure : "<<sizeof(s1)<<endl;
    return 0;
}
```

### 输出：

```
The value is : 240
The value is : S
Size of structure : 8
```

### 代码解读

- 在这段代码中，我们创建了两个带有几个变量的结构体。结构体的创建使用了不同的语法。

- 创建结构体的对象来访问成员。

- 注意，整个结构体的大小会发生变化，就像在类中一样。

- 代码显示了所做的更改。

## 9.3 联合体（Union）

联合体是 C++ 中另一种用户自定义数据类型。联合体将各种不同类型的对象和成员组合在一起。结构体和联合体在语法上可能看起来很相似，但它们在成员的内存分配上有所不同。联合体会为数据变量分配内存空间，该空间大小等于该联合体中占用空间最大的数据变量的大小。

联合体的语法如下：

```cpp
union UnionName
{
    //members
};
```

### 特性

- 使用关键字 `union` 定义，成员通过点运算符访问。

- 联合体的内存分配由最大的成员决定。

- 它拥有与 C++ 中其他地方使用的变量和函数类似的数据成员和函数。

- 数据成员可以被初始化，并且如果值发生变化，由于同一内存空间会受到影响，因此可以被覆盖。

- 成员通过选择运算符或点运算符来访问。

- 在 C++ 中，指向联合体的指针按如下方式使用：`->`。

### 代码：使用联合体

```cpp
#include <iostream>
using namespace std;

union OurUnion {
    int x;
    char c;
};

int main()
{
    union OurUnion u1;
    u1.x = 85;
    u1.c = 'H';
    cout << "The value is : " << u1.x << endl;
    cout << "The value is : " << u1.c << endl;
    cout << "Size of union  : " << sizeof(u1) << endl;
    return 0;
}
```

### 输出：

```text
The value is : 72
The value is : H
Size of union : 4
```

### 代码解读

- 在这段代码中，我们用几个变量创建了一个联合体。

- 然后创建联合体的对象来访问成员。

- 可以观察到，整个联合体的大小会发生变化，这与结构体类似。

- 代码显示了所做的更改。

### 代码：联合体数据类型的实现

```cpp
#include <iostream>
using namespace std;

union OurUnion {
    int x;
    char c;
    char name[12];
};

int main()
{
    union OurUnion u1;
    u1.x = 8588;
    u1.c = 'H';

    union OurUnion u2;
    u2.x = 590;
    u2.c = 'S';

    cout << "The value is x : " << u1.x << endl;
    cout << "The value is c : " << u1.c << endl;
    cout << "Size of union  : " << sizeof(u1) << endl;
    cout << "The value is x : " << u2.x << endl;
    cout << "The value is c : " << u2.c << endl;
    cout << "Size of union  : " << sizeof(u2) << endl;

    return 0;
}
```

### 输出：

```text
The value is x : 8250
The value is c : H
Size of union : 12
The value is x : 595
The value is c : S
Size of union : 12
```

### 代码解读

- 在这段代码中，我们用几个变量创建了一个联合体，并使用点运算符为成员赋值。

- 然后创建联合体的对象来访问成员。

- 可以观察到，整个联合体的大小会发生变化，这与结构体类似。

- 代码显示了所做的更改。

## 9.4 结构体与联合体的区别

既然我们已经了解了 C++ 中这两种用户自定义数据类型，下面来看看它们之间有何不同。下表将帮助学习者在 C++ 程序中判断何时何地可以使用结构体和联合体。

**表 9.1 结构体与联合体区别表**

| 结构体 | 联合体 |

|---|---|

| 结构体是 C++ 中一种用户自定义数据类型，它将不同的数据类型组合在一起。 | 联合体帮助我们将各种不同类型的对象和成员组合在一起。 |

| C++ 中结构体的内存分配是连续的。 | 联合体的内存分配由最大的成员决定。 |

| 数据成员不能在结构体内部初始化。可以通过声明结构体来完成初始化。 | 数据成员可以被初始化，并且如果值发生变化，由于同一内存空间会受到影响，因此可以被覆盖。 |

| 在结构体中，所有数据成员都被分配独立的内存空间。 | 在联合体中，所有数据成员共享一块等于最大成员大小的内存空间。 |

| 结构体的所有数据成员都可以被初始化。 | 联合体只能初始化第一个数据成员。 |

| 结构体的所有数据成员可以同时被访问。 | 联合体的数据成员一次只能访问一个。 |

## 9.5 C++ 中的枚举（Enum）

用户自定义数据类型使我们的 C++ 程序更加灵活和用户友好。它们让用户更容易理解计算机想要表达的语言。枚举（enum）是 C++ 中一种独特的数据类型，它允许我们定义数据类型，并将我们选择的元素命名为整型常量。

枚举的语法如下：

```cpp
enum datatypename { enum values list.... };
```

### 代码：使用枚举

```cpp
#include <iostream>
using namespace std;

int main()
{
    enum Gender { max, checo = 9, lewis, kimi, mick, ocon };
    int i;
    for (i = checo; i <= ocon; i++)
        cout << i << " ";
    return 0;
}
```

### 输出：

```text
9 10 11 12 13
```

### 代码解读

- 在这段代码中，我们使用带有多个项的枚举。

- for 循环遍历数据结构，并将每个成员作为索引号输出。

- 索引为 +1，可根据需求进行更改。

## 实践练习

1. 编写一个 C++ 程序，用于处理录取报告。使用一个结构体，其中包含表示学号、姓名、出生日期（使用嵌套结构体）和分配专业等信息的元素。处理结构体成员的函数必须是结构体的一部分。报告格式如下：

    | 学号 | 姓名 | 出生日期 | 分配专业 |

    |---|---|---|---|

    | XX | xxx | dd/mm/yy | xxxxxxxxxx |

2. 编写一个 C++ 程序，使用结构体处理出生日期。要求能够处理多名学生的出生日期。

3. 编写一个 C++ 程序处理复数。程序需要执行复数的加、减、乘、除运算，并以 `x+iy` 形式输出结果。

4. 对于以下结构体声明：

```cpp
struct institution {
    struct teacher {
        int empl_no;
        char name[20];
    };
    struct student {
        int roll_no;
        char name[15];
    };
};
```

`sizeof(institution)`、`sizeof(teacher)` 和 `sizeof(student)` 的值分别是多少？

## 选择题

1. 下面代码的正确输出是什么？

```cpp
#include <iostream>
#include <math.h>
using namespace std;

struct st {
    int A = NULL;
    int B = abs(EOF + EOF);
} S;

int main()
{
    cout << S.A << " " << S.B;
    return 0;
}
```

- a. 0 2

- b. 0 0

- c. 2 0

- d. 错误

2. 下面代码的正确输出是什么？

```cpp
#include <iostream>
using namespace std;

typedef struct {
    int A = 10;
    int B = 20;
} S;

int main()
{
    cout << S.A << " " << S.B;
    return 0;
}
```

- a. 错误

- b. 10 20

- c. 10 0

- d. 0 0

3. 下面代码的正确输出是什么？

```cpp
#include <iostream>
using namespace std;

typedef struct {
    int A;
    char* STR;
} S;

int main()
{
    S ob = { 10, "india" };

    S* ptr;
    ptr = &ob;

    cout << ptr->A << " " << ptr->STR;
    return 0;
}
```

- a. 10 india

- b. 空白输出

- c. 垃圾值

- d. India 10

4. 下面代码的正确输出是什么？

```cpp
#include <iostream>
using namespace std;

int main()
{
    typedef struct {
        int A;
        char* STR;
    } S;

    S ob = { 10, "india" };
    S* ptr;
    ptr = &ob;

    cout << ptr->A << " " << ptr->STR;
    return 0;
}
```

- a. 10 in

- b. 10 d

- c. 10 india

- d. 10 n

5. 下面代码的正确输出是什么？

```cpp
#include <iostream>
using namespace std;

struct st {
    int A;
```

7. 下面代码的正确输出是什么？

```cpp
#include <iostream>
using namespace std;

struct st1 {
    int A = 10;
    struct st2 {
        char ch = 'A';
    } S;
} SS;

int main()
{
    struct st1* PTR = &SS;
    int X = 0;
    X = PTR->A + PTR->S.ch;
    cout << X;
    return 0;
}
```

- a. 65

- b. 75

- c. 97

- d. 107

8. 以下代码的输出是什么？

```cpp
#include <iostream>
#include <string.h>
using namespace std;

int main() {
    struct student {
        int num;
        char name[25];
    };

    student stu;
    stu.num = 123;
    strcpy(stu.name, "john");
    cout << stu.num << endl;
    cout << stu.name << endl;
    return 0;
}
```

- a. 123 john

- b. john john

- c. 编译时错误

- d. 运行时错误

### 9. 以下代码的输出是什么？

```cpp
#include <iostream>
using namespace std;
struct Time{
    int hours, minutes, seconds;
};
int toSeconds(Time now);
int main() {
    Time t;
    t.hours = 5;
    t.minutes = 30;
    t.seconds = 45;
    cout << "Total seconds: " << toSeconds(t) << endl;
    return 0;
}
int toSeconds (Time now){
    return 3600 * now.hours + 60 * now.minutes + now.seconds;
}
```

- a. 19845

- b. 20000

- c. 15000

- d. 19844

### 10. 以下代码的输出是什么？

```cpp
#include <iostream>
using namespace std;
int main() {
    struct ShoeType{
        string style;
        double price;
    };

    ShoeType shoe1, shoe2;
    shoe1.style = "Adidas";
    shoe1.price = 9.99;
    cout << shoe1.style << "$" << shoe1.price;
    shoe2 = shoe1;
    shoe2.price = shoe2.price / 9;
    cout << shoe2.style << "$" << shoe2.price;
    return 0;
}
```

- a. Adidas$9.99Adidas$1.11

- b. Adidas$9.99Adidas$9.11

- c. Adidas$9.99Adidas$11.11

- d. Adidas$11.11Adidas$11.11

### 11. 以下哪项是正确定义的结构体？

- a. `struct {int a;}`

- b. `struct a_struct {int a;}`

- c. `struct a_struct int a;`

- d. `struct a_struct {int a;};`

### 12. 以下哪项访问结构体指针 `*b` 中的变量？

- a. `b->var;`

- b. `b.var;`

- c. `b-var;`

- d. `b>var;`

### 13. 以下哪项本身是不同数据类型的集合？

- a. 字符串

- b. 结构体

- c. 字符

- d. 以上都不是

### 14. 哪个运算符连接结构体名称与其成员名称？

- a. `-`

- b. `->`

- c. `.`

- d. `.` 和 `->` 都可以

### 15. 以下哪项不能作为结构体成员？

- a. 函数

- b. 数组

- c. 结构体

- d. 以上都不是

