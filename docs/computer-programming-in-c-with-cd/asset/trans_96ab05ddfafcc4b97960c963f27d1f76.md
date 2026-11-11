
```c
//print the address of the variable
return 0;
}
```

**输出：**

```text
value of variable apples is stored at location 0x0012ff50
```

在清单 1 中，变量所占用的地址取决于许多因素，例如程序的类型和操作系统。每次运行代码时，输出可能与给出的输出不同。

我们已经介绍了如何使用 & 运算符获取变量的地址。现在让我们讨论如何声明指针。

## 声明指针

指针变量像普通变量一样声明。它存储另一个特定数据类型变量的地址。因此，在声明指针变量时，必须指定其数据类型。例如，要存储 `int` 变量的地址，需要一个整型指针，如下面的代码片段所示：

```c
int x;
int *ptr;
ptr=&x;
```

在前面的代码片段中，声明了一个 int 类型的变量 x。还使用星号（*）字符声明了一个 int 类型的指针变量 ptr。然后，我们将变量 x 的地址赋给整型指针变量 ptr。

声明指针变量时，* 字符的位置并不固定。要声明指针变量，可以使用以下任一代码片段：

```c
int *ptr;
```

或

```c
int * ptr;
```

或

```c
int* ptr;
```

但是，如果以下列方式声明指针，则该指针声明无效：

```c
int ptr*;
```

或

```cpp
*int ptr;
```

## 创建和使用指针

创建指针时，首先需要声明一个指针变量，然后将另一个变量的地址存储在其中。指针变量可以使用 * 运算符直接访问另一个变量中存储的值，如下面的代码片段所示：

```cpp
cout<< *ptr;
```

在前面的代码片段中，* 运算符指示编译器访问并显示由 ptr 指针变量所引用的内存位置中存储的值。

* 运算符也称为解引用运算符。解引用运算符（*）访问指针变量所指向的变量中存储的数据。可以借助图 1 理解指针变量的使用，如下所示：

![](img/8a6886c00caa6a1651a6c0e62bff341f_229_0.png)

**▲ 图 1：展示了由指针引用的变量**

在图 1 中，创建了一个指针变量 ptr，它使用 &var 表达式存储变量 var 的地址。变量 var 被初始化为 1。与 ptr 一起使用的 * 运算符（*ptr）指示编译器通过变量 var 的地址访问变量 var 中存储的数据。清单 2 展示了 * 运算符的使用（可以在 CD 的 code\chapter4 文件夹中找到 UsingPointer.cpp 文件）：

**▶ 清单 2：使用指针引用变量中存储的数据**

```cpp
#include <iostream.h>
void main()
{
    int var,*ptr; //declaring an integer and integer pointer variable
    var=1; //assign a value to the variable
    ptr = &var;// assign the address of the variable to pointer variable
    cout << "The value of variable var accessed using pointer variable is: "<<
*ptr;//print value
}
```

**输出：**

```text
The value of variable var accessed using pointer variable is: 1
```

在清单 2 中，声明了一个名为 `ptr` 的指针变量。使用 `&` 运算符访问变量 `var` 的内存地址，并将其赋给指针变量。使用 `*ptr` 表达式访问变量 `var` 中存储的数据。

除了访问所引用变量中存储的值之外，指针还可以设置其指向的变量中的数据。清单 3 展示了如何使用指针设置变量的值（可以在 CD 的 `code\chapter4` 文件夹中找到 `AssignValue.cpp` 文件）：

**▶ 清单 3：使用指针为变量赋值**

```
#include <iostream.h>
void main()
{
  int var,*ptr; //declaring an integer and integer pointer variable
  ptr = &var;// assign the address of the variable to pointer variable
  *ptr= 2; //dynamically store value to the variable referenced by pointer variable
  cout<<"The value set to the variable var using the pointer variable is:"<<*ptr;//printing the value
}
```

**输出：**

```text
The value set to the variable var using the pointer variable is:2
```

在清单 3 中，我们使用引用运算符（&）将变量 `var` 的引用赋给指针变量 `ptr`。由指针变量 `ptr` 指向的变量 `var` 被赋值为 2。使用指针变量 `ptr` 在屏幕上显示变量 `var` 的值。

### 使用其他指针类型

到目前为止，您已经学习了如何在 C++ 程序中创建和使用整型指针变量。但是，并非只能使用整型指针变量；在 C++ 程序中，可以使用 C++ 支持的任何类型的指针变量，例如 float、double 和 char。创建和使用其他指针变量的过程与创建和使用整型指针变量类似。清单 4 展示了其他类型指针变量的创建和使用（可以在 CD 的 code\chapter4 文件夹中找到 `OtherPointer.cpp` 文件）：

**▶ 清单 4：创建和使用其他指针类型**

```cpp
#include <iostream.h>

int main()
{
  char MyChar, *PointerChar;
  float MyFloat, *PointerFloat;

  MyChar = 'C';
  MyFloat = 25.1456;

  PointerChar = &MyChar;
  PointerFloat = &MyFloat;

  cout<< "Value of MyChar Variable is: "<<MyChar <<"\n";
  cout<< "MyChar Variable is stored at: "<<PointerChar;

  cout<< "\n"<<"Value of MyFloat Variable is: "<<MyFloat <<"\n";
  cout<< "MyFloat Variable is stored at: "<<PointerFloat;
  return 0;
}
```

**输出：**

```text
Value of MyChar Variable is: C
MyChar Variable is stored at: Cÿ ↑
Value of MyFloat Variable is: 25.1456
MyFloat Variable is stored at: 0x0012ff64
```

在清单 4 中，我们创建了一个 `char` 指针（`PointerChar`）和一个 `float` 指针（`PointerFloat`），它们分别将 `MyChar` 和 `MyFloat` 变量的内存地址作为其值。然后，使用 `iostream.h` 库中的 `cout` 函数在屏幕上显示这些变量（包括指针变量）的值。让我们学习 C++ 中指向指针的指针的用法。

### 使用指向指针的指针

如前所述，指针是一个包含另一个变量内存地址的变量。但是，指针也可以包含另一个指针的内存地址。例如，有一个整型变量 `MyInt` 和两个整型指针变量 `MyIntP1` 和 `MyIntP2`。整型指针 `MyIntP1` 指向 `MyInt` 变量的内存地址，整型指针 `MyIntP2` 指向 `MyIntP1` 的内存地址，那么整型指针 `MyIntP2` 应称为指向指针的指针。清单 5 展示了指向指针的指针变量的创建（可以在 CD 的 code\chapter4 文件夹中找到 `PointerToPointer.cpp` 文件）：

**▶ 清单 5：创建指向指针的指针变量**

```cpp
#include <iostream.h>

int main ()
{
  int MyInt, *MyIntP1, **MyIntP2;
  MyInt = 50;
  MyIntP1 = &MyInt;
  MyIntP2 = &MyIntP1;

  cout<<"Value of MyInt is: "<<MyInt;
  cout<<"\n"<<"Memory Address of MyInt is: "<< MyIntP1;
  cout <<"\n"<<"Memory Address of MyIntP1 is: "<< MyIntP2;
  cout <<"\n"<<"Memory Address of MyIntP2 is: "<< &MyIntP2;

  cout<<"\n"<<"Value accessed using MyInt is: "<<MyInt;
  cout <<"\n"<<"Value accessed using MyIntP1 is: "<< *MyIntP1;
  cout <<"\n"<<"Value accessed using MyIntP2 is: "<< **MyIntP2;
  return 0;
}
```

**输出：**

```text
Value of MyInt is: 50
Memory Address of MyInt is: 0x0012ff68
Memory Address of MyIntP1 is: 0x0012ff64
Memory Address of MyIntP2 is: 0x0012ff60
Value accessed using MyInt is: 50
Value accessed using MyIntP1 is: 50
Value accessed using MyIntP2 is: 50
```

在清单 5 中，可以看到声明了一个整型变量 `MyInt` 和两个整型指针变量 `MyIntP1` 和 `MyIntP2`。`MyIntP1` 后跟单个 `*` 运算符，而 `MyIntP2` 后跟两个 `*` 运算符（`**`），表示 `MyIntP2` 是一个指针，用于指向另一个指针（即 `MyIntP1`）的内存地址。此外，在输出中可以看到，指针 `MyIntP1` 的内存地址（`0x0012ff64`）与 `MyIntP2` 的内存地址（`0x0012ff60`）不同。但是，当访问这些指针的值时，它们都显示了相同的值。

让我们学习如何在运行时使用指针处理内存。
