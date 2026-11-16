

成员函数 concat() 将一个字符串追加到另一个字符串上。它可以如下调用：

```
s3.concat(s2);
```

这里，变量 str 是 s3 的数据成员，s3 是调用该成员函数的对象。传递给成员函数的参数是类 String 的一个对象。使用 strcpy() 函数，s2.str 将被追加到 s3.str。

因此，来自 main() 的调用：

```
s3.concat(s2);
```

会导致 s2 被追加到现有的 s3。

请注意，s1 = s2 有效地将对象 s2 的数据成员内容复制到对象 s1。因此，我们为字符串创建了一个赋值设施。由于我们定义了类 String，这个赋值设施已经内置。这不是由于任何成员函数。我们稍后将增强 String 类。

## 类对象的数组

正如我们可以声明常见数据类型的数组一样，我们可以声明类对象的数组。例如，我们可以声明一个包含 5 个 `Elevator` 对象的数组：

```
// e1.cpp

#include <iostream>
#include "elevator.h"

using namespace std;

int main() {
    Elevator e[5];
    ...
}
```

整个数组的存储空间在栈上分配，如下所示：

![](img/adb3588dc0dfe9f607c1d417be6bb240_123_0.png)

只需记住一条铁律：存储在数组中的类对象必须具有默认构造函数。默认构造函数可以由编译器或程序员提供。但是，如果程序员声明了构造函数但没有提供默认构造函数，编译器提供的默认构造函数就不存在了。

当类对象的数组被创建时，C++ 会为数组中的每个对象调用一次类的默认构造函数。在上面的 `Elevator` 构造函数的情况下，C++ 会调用 `Elevator` 的默认构造函数 5 次，从而将对象 `e[0]` 到 `e[4]` 初始化为正确的值。

如果你希望 C++ 调用不同的构造函数，则必须在数组声明中直接显式初始化每个数组元素：

```
// e2.cpp
#include <iostream>
#include "elevator.h"
using namespace std;
int main() {
    Elevator e[5] = {
        Elevator(),
        Elevator(),
        Elevator(2, 5),
        Elevator(7, 3),
        Elevator()
    };
    ...
}
```

请注意，有时花括号的使用就像是在初始化 `struct` 的字段，但某些编译器即使没有它们也可以正常工作。

没有简单的方法可以为一些数组化的类对象使用默认构造函数，而为另一些使用备用构造函数。如果你需要这样做，最好是为整个数组使用默认构造函数，然后根据需要重新初始化选定的对象。除了小型数组外，这可能太过繁琐，实际用处不大。

## 动态数组

类对象的数组也可以存储在堆（自由存储区）上，并通过指针寻址。下面的程序声明了一个指向 `Elevator` 对象的指针数组。指针数组的存储空间在栈上分配，而每个实际 `Elevator` 对象的存储空间在堆上分配。

```
// e3.cpp
#include <iostream>
#include "elevator.h"
using namespace std;
int main() {
    int i;
    Elevator *e[5];
    for (i = 0; i < 5; i++)
        e[i] = new Elevator;
    for (i = 0; i < 5; i++)
        cout << e[i]->getFloor() << endl;
    for (i = 0; i < 5; i++)
        delete e[i];
}
```

下面是前面程序中创建的动态数组的表示：

在栈上创建   在堆上创建

e
---
0 | •-----|------> [Elevator 对象]
1 | •-----|------> [Elevator 对象]
2 | •-----|------> [Elevator 对象]
3 | •-----|------> [Elevator 对象]
4 | •-----|------> [Elevator 对象]

在堆上动态创建类对象数组的另一种方法如下：

```
// e4.cpp
//-------------------------------------
#include <iostream>
#include "elevator.h"

using namespace std;

int main() {
   Elevator *eptr;

   eptr = new Elevator[5];
   for (int i = 0; i < 5; i++)
      cout << eptr[i].getFloor() << endl;
   delete [] eptr;
}
```

如下图所示，在栈上分配的唯一存储空间是指向 Elevator 数组的指针的存储空间。数组本身的存储空间（即每个 Elevator 对象的存储空间）在堆上分配。

| | 在栈上创建 | 在堆上创建 | |
|---|---|---|---|
| | eptr=====> | 0 | Elevator 对象 | |
| | | 1 | Elevator 对象 | |
| | | 2 | Elevator 对象 | |
| | | 3 | Elevator 对象 | |
| | | 4 | Elevator 对象 | |

在上面的程序中，请注意，我们使用直接成员选择符（.）运算符，而不是间接成员选择符（->）运算符来访问成员函数。这是因为这次我们没有指向类对象的指针数组，而是类对象本身包含在数组中。

与其他动态对象一样，我们在使用完动态类对象数组后应该将其删除。但是，删除这样的数组会导致一个问题。由于 C 和 C++ 无法区分指针和数组，程序必须使用 delete 的特殊形式（[]）来确保在删除类对象的动态数组时，这些对象的析构函数被正确调用。

如果我们简单地写了：

```
delete eptr;
```

编译器将不知道 eptr 是指向单个 Elevator 类对象还是指向 Elevator 类对象的数组。为了通知编译器 eptr 指向一个数组，我们在 delete 中添加空括号：

```
delete [] eptr;
```

这确保了数组中每个对象的类析构函数都被调用。请注意，旧编译器要求如下：

```
delete [5] eptr;
```

我们的下一个示例也在堆上创建类对象的动态数组。但这次，不仅在堆上创建了指针数组，指针所指向的 Elevator 对象也在堆上创建。

```
// e5.cpp

#include <iostream>
#include "elevator.h"

using namespace std;

int main() {
    int i;
    Elevator **eptr;

    eptr = new Elevator *[5];
    for (i = 0; i < 5; i++)
        eptr[i] = new Elevator;
    for (i = 0; i < 5; i++)
        cout << eptr[i]->getFloor() << endl;
    for (i = 0; i < 5; i++)
        delete eptr[i];
    delete [] eptr;
}
```

下面是上面程序中创建的动态数组的表示：

在栈上创建   在堆上创建   在堆上创建

eptr =======> 0 | . -------> [Elevator 对象]
             1 | . -------> [Elevator 对象]
             2 | . -------> [Elevator 对象]
             3 | . -------> [Elevator 对象]
             4 | . -------> [Elevator 对象]

## 动态内存分配

与 C 语言的 `malloc()` 函数一样，C++ 关键字 `new` 用于在执行时分配连续内存。在最简单的形式中，我们使用关键字 `new`，后跟要分配的任何数据类型。

```
char *p = new char; // allocates a single char
int *p = new int; // allocates an int
double *p = new double; // allocates a single double
```

与 `malloc()` 不同，你不再需要使用 `sizeof` 关键字来指定所需的准确字节数。相反，你只需指定特定的类型，无论是基本类型还是用户定义类型。不同类型占用不同存储量的事实由编译器自动处理。

使用 `new` 运算符分配类型 T 的对象时，第一个参数 `sizeof(T)` 会自动提供给此函数。如果 `operator new()` 无法分配请求的堆空间大小，它将返回值为零的指针。如果 `operator new()` 成功在堆上分配存储空间，则返回该空间的地址，该地址被转换为所分配类型的指针。

由于在 C++ 中能够初始化变量和对象非常重要，通过 `new` 从堆上分配的基本类型可以通过在类型名称后立即用括号括起值来用某个值进行初始化。

```
char *p = new char ('A'); // allocates a single char
int *p = new int(65); // allocates an int
double *p = new double(5.2); // allocates a single double
```

## 基本类型数组的内存分配

要为某种基本类型的数组分配内存，我们使用关键字 `new`、类型名以及用方括号括起来的数组元素个数。这个数可以是常量，也可以是某个表达式，其值

