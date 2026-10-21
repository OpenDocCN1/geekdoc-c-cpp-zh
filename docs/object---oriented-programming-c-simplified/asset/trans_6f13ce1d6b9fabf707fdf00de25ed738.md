

# C++ 中的运算符和引用

## 4.1 引言

本章讨论 C++ 引入的所有新运算符。它还讨论了一些 C++ 支持而 C 不支持的新特性。C 和 C++ 共有的运算符已在第 3 章讨论过。C++ 的一个新特性“引用”将被讨论。C++ 的新运算符在下面的表中给出：

表 4.1：C++ 中的新运算符

| S.No. | Operator | Meaning |
|---|---|---|
| 1. | :: | 作用域解析运算符 |
| 2. | >> | 提取运算符 |
| 3. | << | 插入运算符 |
| 4. | :: * | 指向成员声明 |
| 5. | ->* | 指向成员运算符（用于解引用） |
| 6. | .* | 指向成员运算符（用于解引用） |
| 7. | new | 动态内存分配器 |
| 8. | delete | 动态内存去分配器。 |

我们已在前面章节介绍的几乎所有程序中看到过 >> 和 << 的使用。因此我们从作用域解析运算符的讨论开始。

## 4.2 作用域解析运算符

运算符 :: 在 C++ 中称为作用域解析运算符。该运算符用于两个目的：

目的-1：用于访问全局变量。

目的-2：标识类成员所属的类。

我们将理解第一个。第二个将在介绍类时讨论。在 C++ 中，可以使用 {和} 创建块。在该块内声明的任何变量仅限于该块内。现在如果在任何块内声明了一个变量并且有一个同名的全局变量，则优先使用局部变量。如果我们想在块中也使用同名的全局变量怎么办？作用域解析运算符在这些情况下有所帮助。要访问任何全局变量，例如 gb，我们可以写成 :: gb。现在如果我们有一个局部变量 gb，则可以通过引用 gb 简单地访问该变量。也就是说作用域解析运算符 :: 允许我们在局部和全局变量同名时使用全局版本的变量。

如果一个块包含在另一个块内并且两者具有相同的变量名，则会优先考虑内部块。外部块的变量可以在内部块中使用，但反之则不行。

我们下面给出作用域解析运算符使用的众多示例。

# /*PROG 4.1 作用域解析运算符 :: 的演示 VER 1*/

```
#include <iostream.h>
#include <conio.h>
int num = 100;
void main()
{
    int num = 30;
    clrscr();
    cout << "In main\n";
    cout << "Local num = " << num << "\t";
    cout << "Global num = " << :: num << endl;
    {
        int num = 40;
        cout << "In block1\n";
        cout << "Local num = " << num << "\t";
        cout << "Global num = " << :: num << endl;
    }
    {
        int num = 50;
        cout << "In block2\n";
        cout << "Local num = " << num << "\t";
        cout << "Global num = " << :: num << endl;
    }
    getch();
}
```

# # 面向对象编程 C++ 简化

- In main
- Local num =30 Global num =100
- In block1
- Local num =40 Global num =100
- In block2
- Local num =50 Global num =100

:: 如前所述称为作用域解析运算符。任何全局变量，例如 gb，可以通过写成 :: gb 在程序的任何地方访问。在程序中我们已在四个地方声明了 num，一个是全局的，第二个是在 main 函数中，第三个在一个块中，第四个是在第二个块中。块可以通过 {和} 创建。一个块的变量 num 只能在该块内使用，但 main 的 num 可以在 main 函数的任何地方使用。全局 num 可以通过写成 :: num 访问。基于此，我认为弄清楚程序的输出会很容易。

```cpp
/*PROG 4.2 作用域解析运算符 :: 的演示 VER 2*/
#include <iostream.h>
#include <conio.h>
int num =100;
void main( )
{
 int num=30;
 cout << "In main\n";
 cout << "Local num =" << num << "\t";
 cout << "Global num =" << :: num << endl;
 int copynum=num;
 {
 int num=40;
 cout << "In block 1\n";
 cout << "Local num =" << num << "\t";
 cout << "Global num =" << :: num << "\t";
 cout << "num of main =" << copynum << endl;
 }
 {
 int num=50;
 cout << "In block 2\n";
 cout << "Local num =" << num << "\t";
 cout << "Global num =" << :: num << "\t";
 cout << "Num of main =" << copynum << endl;
 }
}
```

# 输出：

In main
Local num = 30      Global  num = 100
In block1
Local num = 40      Global  num = 100
In block2
Local num = 50      Global  num = 100
In main
Local num = 30      Global  num = 100
In block 1
Local num = 40      Global  num = 100  num of main = 30
In block 2
Local num = 50      Global  num = 100  Num of main = 30

解释：在之前的程序中，我们无法在任何块中使用在 main 中声明的 num，并且局部变量 num 优先于 main 的 num。但在这里我们已将 main 的 num 保存到一个新的变量 copynum 中。现在，我们可以使用此 copynum 变量在任何块中打印 main 的 num 值。

```
/*PROG 4.3 作用域解析运算符 :: 的演示 VER 3*/

#include <iostream.h>
#include <conio.h>
int num = 100;
char *str = "I am Global";
void main()
{
    int num = 30;
    clrscr();
    char *str = "I am in main\n";
    cout << str;
    cout << "Local num =" << num << "\t";
    :: num = :: num + 10;
    cout << "Global num =" << :: num << endl;
    cout << "Global str =" << :: str << endl;
    {
        int num = 40;
        char *str = "I am in block1\n";
```

```
```cpp
clrscr( );
cout << "Global data\n";
cout << :: g1 << "\t" << :: g2 << "\t" << :: g3 << endl;
getch( );
}
```
```

**输出：**  
多个错误

**解释：** 全局变量必须在声明时初始化。你不能将全局变量的声明和初始化分开。你将得到 **编译错误 missing storage class or type specifies。**

```
```cpp
/*PROG 4.6 作用域解析运算符 :: 的演示 VER 6*/
#include <iostream.h>
#include <conio.h>
int num = 20;
void main( )
{
    int num = 30;
    clrscr( );
    cout << "Local num\n";
    cout << "Value =" << num << "\t" << "address =" << &num << endl;
    cout << "Global num\n";
    cout << "Value =" << :: num << "\t" << "Address =" << & :: num << endl;
    getch( );
}

OUTPUT :
Local num
Value =30        address=0x8fdcfff4
Global num
Value =20        Address =0x8fdc00aa
```
```

**解释：** 该程序简单地演示了如何获取全局数据的地址。

## 4.3 引用变量

引用变量是 C++ 中的一个新概念。引用变量是一个可以引用先前定义的变量或任何常量的变量。例如：

```
```cpp
int x = 10;
int &refx = x;
```
```

行 int & refx = x; 创建了一个引用变量 refx，其中包含变量 x 的引用。为变量创建引用意味着为该变量创建新的名称，即在上述情况下 refx 和 x 都引用相同的内存位置。对这两个变量 refx 或 x 中的任何一个进行的任何更改都会反映到另一个变量。假设 x 的初始值为 10；当我们写 x++ 并显示 refx 时我们会得到 11。如果我们现在写 refx++ 并显示 x 的值，我们会得到 12。下面给出的图显示内存位置的地址为 1020，但它有两个名称 x 和 refx。如果我们现在尝试打印 &x 或 &refx，我们会得到 1020。

![](img/ad5299318df8d4d7c6df5eaa86590ea3_142_0.png)

定义引用变量的一般语法是：

```
data_type &reference_name = referent;
```

这里 & 不是被理解为地址运算符。例如 int & 表示对 int 的引用。引用变量必须在声明时初始化，即，如果你写 int & x; 然后写 x = y 将是无效的。

```
/*PROG 4.7 引用变量的演示 VER 1*/

#include <iostream.h>
#include <conio.h>
void main()
{
int x=10;
int &refx=x;
clrscr();
refx++;
cout<<"x="<<x<<endl;
cout<<"refx="<<refx<<endl;
getch();
}
OUTPUT :
X=11
Refx=11
```

解释：语句 int &refx =x; 创建了一个引用变量 refx，其中包含变量 x 的引用。如前所述，引用变量必须初始化。你不能写 int &refx。创建引用就像为同一变量创建新名称一样，因此对 refs 所做的任何更改都会发生在 x 上，反之亦然。所以输出。

```
/*PROG 4.8 引用变量的演示 VER 2*/

#include <iostream.h>
#include <conio.h>
```

