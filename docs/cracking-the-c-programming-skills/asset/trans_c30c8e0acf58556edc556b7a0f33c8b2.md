
```cpp
getchar ();
return 0;
}
```

-   (a) 0 和 0
-   (b) 0 和垃圾值
-   (c) 编译错误
-   (d) 以上都不是

**答案：(a)** static 是全局变量的默认存储类。静态变量默认存储 0。上面的代码就是为了证明这一点。

**67.** 以下代码片段的输出是什么？(L3)

```cpp
#include <iostream>
using namespace std;
static int variable;
auto int variable1;
int main () {
    cout << "\n" << "static " << variable;
    cout << "\n" << "global " << variable1;
    getchar ();
    return 0;
}
```

-   (a) 0 和 0
-   (b) 垃圾值和垃圾值
-   (c) 编译错误
-   (d) 以上都不是

**答案：(c)** 全局变量不能是 auto，它们应为 static。因此，这会导致错误。

**68.** 以下代码片段的输出是什么？(L3)

```cpp
#include <iostream>
using namespace std;
int auto_verify ()
{
    static int sum = 0;
    sum = sum + 1;
    cout << "\n" << sum;
}

int main ()
{
    int i, ret;
    for (i=1;i<=5;i++)
    {
        ret = auto_verify();
    }
    getchar ();
    return 0;
}
```

-   (a) 1,1,1,1,1
-   (b) 0,0,0,0,0
-   (c) 1,2,3,4,5
-   (d) 以上都不是

**答案：(c)** 是正确答案，因为 static 会记住值，不会每次都重新初始化。

**69.** 以下代码片段的输出是什么？(L3)

```cpp
#include <iostream>
using namespace std;
int sum = 0;
int auto_verify ()
{
    sum = sum + 1;
    cout << "\n" << sum;
}

int main ()
{
    int i, ret;
    for (i=1;i<=5;i++)
    {
        ret = auto_verify();
    }
    getchar ();
    return 0;
}
```

-   (a) 1,1,1,1,1
-   (b) 0,0,0,0,0
-   (c) 1,2,3,4,5
-   (d) 以上都不是

![](img/5fbe80b655d61d9cfbc9f5d129b9fb45_92_0.png)

**75.** 以下代码片段的输出是什么？(L3)

```cpp
#include <iostream>
using namespace std;
int main (){
    register int i = 10;
    cout << i << "\n";
    getchar ();
    return 0;
}
```

-   (a) 1
-   (b) 10
-   (c) register 的使用错误
-   (d) 以上都不是

**答案：** (b) 将 register 用作存储限定符是完全合法的。但是，程序员更倾向于在需要更快访问时使用它。

**76.** 以下代码片段的输出是什么？(L3)

```cpp
#include <iostream>
using namespace std;
int main (){
    register int i ;
    cout << "\n";
    getchar ();
    return 0;
}
```

| 选项 | 内容 | 选项 | 内容 |
| --- | --- | --- | --- |
| (a) | 1 | (b) | 垃圾值 |
| (c) | 0 | (d) | 以上都不是 |

**答案：** (b) 将 register 用作存储限定符是完全合法的。但是，程序员更倾向于在需要更快访问时使用它。

**77.** 以下代码片段的输出是什么？(L3)

```cpp
#include <iostream>
using namespace std;
int main (){
    int i ;
    static int i;
    i =10;
    cout << i << "\n";
    getchar ();
    return 0;
}
```

-   (a) 1
-   (b) 垃圾值
-   (c) 编译错误
-   (d) 以上都不是

**答案：** (c) 不允许重复声明变量，因此这是一个错误。

**78.** 指出以下代码中的错误。(L4)

```cpp
#include <iostream>
using namespace std;
global int sum = 0;
int auto_verify ()
{
    sum = sum + 1;
    cout << "\n" << sum;
}
int main ()
{
    int i, ret;
    for (i=1;i<=5;i++)
    {
        ret = auto_verify();
    }
    getchar ();
    return 0;
}
```

**答案：** C 或 C++ 中不支持名为 global 的显式关键字。如果在 main 上方声明，它自然会被限定为全局存储限定符。

**79.** 以下代码片段的输出是什么？(L4)

```cpp
#include <iostream>
using namespace std;
int main ()
{
    int i = 5;
    {
        int i = 10;
        {
            auto int i = 15;
            cout << "\n" << i;
        }
        cout << "\n" << i;
    }
    cout << "\n" << i;
    getchar ();
    return 0;
}
```

-   (a) 编译错误
-   (b) 5, 10, 15
-   (c) 15, 10, 5
-   (d) 5, 5, 5

**答案：** (c) 这里通过此示例说明了 auto 存储限定符的作用域。

**80.** 以下代码片段的输出是什么？(L3)

```cpp
#include <iostream>
using namespace std;
int main ()
{
    auto int a[5] = {1};
    cout << "\n" << a[1];
    getchar ();
    return 0;
}
```

-   (a) 垃圾值
-   (b) 1
-   (c) 0
-   (d) 以上都不是

**答案：** (c) 如果数组中的一个元素被初始化，其余元素将自动初始化为 0。这称为自动数组。

## 5 动态内存分配

代码中非常重要且棘手的部分之一是内存分配。优秀的程序员应该密切关注资源，尤其是内存。动态内存分配使我们能够轻松管理内存并保持代码健壮。本章详细阐述 DMA 的术语和技术。

**1.** 以下代码片段的输出会是什么？(L2)

```cpp
#include <iostream>
using namespace std;
int main ()
{
    int *pointer;
    pointer = new int;
    cout << "return value" << pointer;
    return 0;
}
```

-   (a) 无输出
-   (b) 如果分配了内存，将打印一个地址
-   (c) 编译错误
-   (d) 0

**答案：** (b) 是正确答案。如果存储中有足够的内存，它将为整数分配内存并返回一个地址。

**2.** 假设内存分配从 1000 开始，以下代码的输出会是什么？（假设你使用的是 Dev C++ 或 G++）(L2)

```cpp
#include <iostream>
using namespace std;
int main ()
{
    int *pointer;
    pointer = new int [2];
    cout << "return value" << pointer << "\n";
    cout << "return value" << pointer+1 << "\n";
    return 0;
}
```

-   (a) 1000, 1004
-   (b) 1000, 1000
-   (c) 错误
-   (d) 将数组与 new 一起使用无效

**答案：** (a) 由于 new 和数组的用法正确，分配将从 1000 开始，并且第二个 cout 语句也会打印 1004。

**3.** 关于使用 new 进行内存分配，以下哪项是正确的？(L2)

-   (a) 将根据请求分配内存，并且 new 将返回一个地址。
-   (b) 当没有足够内存时，将显示错误。
-   (c) 当没有足够内存时，将抛出异常。
-   (d) 如果没有足够内存，它将释放已使用的内存并为当前请求分配内存。

**答案：** 'a' 和 'c' 有效。

**4.** 关于内存分配，以下哪项是正确的？(L2)

-   (a) new 必须始终与 free 一起使用，否则会抛出异常。
-   (b) new 必须始终与 delete 一起使用，否则会抛出异常。
-   (c) new 不必与 delete 关联。
-   (d) 尽管不是强制性的，但使用 delete 是一种好习惯。

**答案：** 'b'、'c' 和 'd'

**5.** 以下代码的输出是什么？(L3)

```cpp
#include <iostream>
using namespace std;
int main ()
{
    int *pointer;
    pointer = new int ;
    cout << "return value" << pointer << "\n";
    free pointer;
    return 0;
}
```

-   (a) 如果有可用空间，将返回一个地址。
-   (b) 编译错误，因为此代码中不能使用 free。
-   (c) 语法错误。
-   (d) 无输出。无错误。

**答案：** (b) 在此上下文中不允许使用 free。

**6.** 以下代码的输出是什么？(L3)

```cpp
#include <iostream>
using namespace std;
int main ()
{
    int *pointer;
    pointer = new int;
    cout << "return value" << pointer << "\n";
    delete pointer;
    return 0;
}
```

-   (a) 如果有可用空间，将返回一个地址，并且 delete 将完美执行。
-   (b) 编译错误，因为此代码中不能使用 delete。
-   (c) 语法错误。
-   (d) 无输出。无错误。

**答案：** (a) 是正确答案，因为它的使用完全正确。

**7.** 以下代码的输出是什么？(L3)

```cpp
#include <iostream>
using namespace std;
int main ()
{
    int *pointer;
    pointer = new int [2];
    cout << "return value" << pointer << "\n";
    delete [2] pointer;
    return 0;
}
```

-   (a) 如果有可用空间，将返回一个地址，并且 delete 将完美执行。
-   (b) 编译错误。
-   (c) 语法错误。
-   (d) 无输出。无错误。

**答案：** (b) 是答案。传给 'delete' 的 'int' 类型参数是错误的。

**8.** 以下代码的输出是什么？(L3)

```cpp
#include <iostream>
using namespace std;
int main ()
{
    int *pointer;
    pointer = new int [2];
    cout << "return value" << pointer << "\n";
    delete [] pointer;
    return 0;
}
```
