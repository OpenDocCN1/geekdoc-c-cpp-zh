

在本节中，我们将讨论这些内存区域及其使用方法。了解每个区域的特性并知道如何使用它们，有助于我们编写更好的程序。

## 9.4.1 代码内存

**代码内存**用于存放程序代码。程序运行时，C++ 的运行环境会依次执行每条语句，或者跳转到另一条语句。该内存区域不存储任何对象。程序终止时，代码内存会被释放。

> **代码内存存储程序代码；**  
> **程序终止时，代码内存会被释放。**

## 9.4.2 静态内存

**静态内存**用于存放**全局对象**（不属于任何函数的对象，包括 `main`）以及程序中任意位置创建的**静态对象**（在全局区域或函数内部）。程序终止时，这些对象会自动销毁，其占用的内存也会被释放。

> **静态内存存储全局对象和静态对象；**  
> **程序终止时，静态内存会被释放。**

## 示例 9.23

程序 9.13 展示了一个非常简单的程序。三个数据变量 *first*、*second* 和 *third* 的内存位置都在静态内存中创建。第一个是全局变量，第二个和第三个是静态变量。

## **程序 9.13** 使用静态内存

```cpp
/******************************************************
* The program shows how global and static objects are visible
* at any point in the program. They last through the life of the
* program.
******************************************************/
#include <iostream>
using namespace std;

int first = 20;             // Global variable in static memory
static int second = 30;     // Static variable created in static memory

int main()
{
    static int third = 50;  // Static variable in static memory

    cout << "Value of global variable: " << first << endl;
```

当函数 *second* 返回时，系统会弹出其唯一的参数 (b) 并将其丢弃（之后不再需要）。当函数 *first* 返回时，系统会弹出其唯一的参数 (a) 并将其丢弃（之后不再需要）。当函数 *main* 返回时，系统会弹出其唯一的局部变量 (x) 并将其丢弃（之后不再需要）。程序终止时，栈内存最终再次变为空。为简单起见，我们没有在函数 *first* 或 *second* 中使用局部变量；否则，这些局部变量也会被压入栈中，并从栈中弹出。

### 优点

每个程序都会使用栈内存。栈内存的后进先出操作使其非常高效。只有当对象处于某个函数的作用域内时，它才会存储在栈内存中并保留在那里。当对象离开函数的作用域时，它会从栈中弹出并被丢弃；之后便无法再访问它。

### 限制

使用栈内存的高效性带来了两项限制：

- 对象必须在编译时具有名称。未命名对象无法存储在栈中。
- 对象的大小必须在编译时确定。除非系统知道对象的确切大小，否则无法为其分配栈内存。对于单个对象，可以根据其类型推断大小；对于对象列表（例如数组），元素数量必须在编译时确定。

根据前面的讨论，我们可以将*栈内存*称为*编译时内存*。存储在栈内存中的每个对象都必须在编译时明确定义。

> 在栈内存中创建的对象必须具有名称，并且其大小必须在编译时确定。

## 示例 9.24

假设我们需要一个大小可变的数组，这意味着每次运行程序时，都必须由用户定义数组大小，如下所示：

```cpp
#include <iostream>
using namespace std;

int main ()
{
    int size;
    cin >> size;
    double array[size];             // Compilation error
    ...
    return 0;
}
```

我们会得到上面显示的编译错误，这是因为编译器必须在为数组分配栈内存之前知道数组的大小。我们将在下一节中解决这个问题。

![](img/d68f6199646ca63591a6d8419e0ed4ba_436_0.png)

**注意：**  
指针位于栈内存中；它必须具有名称（`ptr`）。  
指针所指向的对象位于堆内存中；它不能具有名称。

## 9.4.4 堆内存

有时，我们需要在运行时于内存中创建对象。当我们创建和编译程序时，如果不知道对象的大小，就会出现这种情况。**堆内存**（也称为*空闲内存*或*动态内存*）用于存储运行时创建的对象。当对象或对象集合需要大量内存，或者无法在编译期间计算所需内存量时，就会出现这种情况。在堆内存中创建的对象不能具有名称，因此，为了访问它们，我们需要在栈内存中使用一个指针，并让该指针指向它们。换句话说，为此我们同时需要栈内存和堆内存。栈内存用于存放指针（一个 4 字节的小对象）；堆内存用于存储指针所指向的对象（通常是一个较大的对象），如图 9.24 所示。

堆内存中的被指向对象不能具有名称；它通过指向它的指针来引用。另一方面，指针对象位于栈中，因此必须具有名称。换句话说，指针的名称帮助我们引用指针本身；被指向对象的地址则使我们能够访问该对象。

> 在堆内存中创建的对象不能具有名称；  
> 只能通过它的地址访问该对象，而该地址  
> 由栈内存中的指针获得。

### 两个运算符：`new` 和 `delete`

现在的问题是：如果对象没有名称，我们如何在运行时于堆中创建对象，以及在不再需要它时如何销毁对象？这通过四个运算符来完成。这些运算符在附录 C 中定义，并在表 9.6 中列出，以便快速查阅。

表 9.6 中的第一个运算符用于在堆中为单个对象创建内存。第二个运算符用于在堆中创建对象数组。第三个运算符用于使用指向单个对象的指针删除该对象。第四个运算符用于释放堆中为数组分配的内存。图 9.25 展示了用于创建 *new* 和 *delete* 表达式的四个运算符。

**表 9.6 — 堆中的内存分配和释放运算符**

| 分组 | 名称 | 运算符 | 表达式 | 优先级 | 结合性 |
|---|---|---|---|---:|:---:|
| 一元 | 分配对象<br>分配数组<br>删除对象<br>删除数组 | `new`<br>`new []`<br>`delete`<br>`delete []` | `new type`<br>`new type [size]`<br>`delete ptr`<br>`delete [] ptr` | 17 | ← |

注意，执行 *delete* 后，指针会变成悬空指针，我们将在本节稍后讨论这一点。在再次对它应用 *new* 运算符之前，不能使用该指针。

## 示例 9.25

在本示例中，我们将在堆中创建一个对象。假设我们想编写一个程序，使其在用户每次运行程序时都创建一个大小可变的数组。由于数组大小在编译时未定义，而只在运行时确定，因此无法在栈内存中创建该数组。图 9.26 展示了这种情况。

程序 9.14 展示了如何实现这种情况。在程序终止之前，我们必须删除在堆中创建的数组（第 34 行）。

![](img/d68f6199646ca63591a6d8419e0ed4ba_437_1.png)

**程序 9.14** 使用堆内存存储大小可变的数组

```cpp
/********************************************************
 * The program shows how to create and access a variable-size
 * array in the heap and use pointers to access elements.
 ********************************************************/
#include <iostream>
using namespace std;

int main ()
{
    // Declaration of array size and the pointer in the stack
    int size;
    int* pArray;
    // Validation of the size to be greater than zero
    do
    {
        cout << "Enter the array size (larger than zero): ";
        cin >> size;
    } while (size <= 0);
    // Creation of array in the heap
    pArray = new int[size];
    // Inputting the values of array
    for (int i = 0; i < size; i++)
    {
        cout << "Enter the value for element " << i << ": ";
        cin >> *(pArray + i);
    }
    // Outputting the values of the array
    cout << "The elements in the array are: " << endl;
    for (int i = 0; i < size; i++)
    {
        cout << *(pArray + i) << " ";
    }
    // Deleting the array in the heap
    delete [] pArray;
    return 0;
}
```

**运行：**

```text
Enter the array size (larger than zero): 3
Enter the value for element 0: 6
Enter the value for element 1: 12
Enter the value for element 2: 5
The elements in the array are:
6 12 5
```

### 与堆内存相关的问题

当我们使用堆内存以及相关运算符（*new* 和 *delete*）时，必须注意可能出现的一些问题。

**未分配就删除**

编程中可能出现的错误之一，是我们在使用 *new* 运算符之前就尝试使用 *delete* 运算符。这意味着我们试图

