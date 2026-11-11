
要创建指针，我们使用解引用运算符（*），这将创建一个指针变量，该变量旨在保存某个内存位置的地址。下面的程序创建了一个指针，并使用引用运算符（&）将另一个普通变量的地址存入新创建的指针中。解引用运算符（*）也用于访问或更改该内存位置中的实际数据。

- 解引用运算符（*）用于创建指针，也用于更改实际值
- 引用运算符（&）用于获取指针的内存位置

必须增加缩进。

```c
//Regular variable

int var = 10;

//Pointer
int* pointer;

//Storing of var memory location
pointer = &var;

//Pointer is now effectively 'var' so
//things like this can happen
*pointer = 20;

printf("Var's value is now: %d", var);
```

输出：

> Var 的值现在是：20

## NULL 指针

创建指针时，最初并没有给它指定任何指向对象，这是危险的，因为指针在创建时会引用随机内存，而更改该内存位置中的数据可能会导致程序崩溃。为防止这种情况，我们在创建指针时将其赋值为 NULL，如下所示：

```c
int* pointer = NULL;
```

这意味着该指针的地址为“0”，这是一个保留的内存位置，用于标识空指针。可以使用 if 语句检查空指针：

```c
if (pointer){}
```

## 使用指针

现在，指针的一些实际用途是将它们作为参数传递，并实际上按引用传递它们。下面的示例将展示效果：

```c
void Change_Value(int* reference)
{
    //Changes the value in the memory location
    *reference = 20;
}

int main()
{
    //Creates pointer to variable
    int var = 10;
    int* pointer = &var;
    printf("The value before call: %d\n", var);
    //Method call
    Change_Value(pointer);

    //Prints new value
    printf("The value after call: %d\n", var);
    return 0;
}
```

输出：

> 调用前的值：10
> 调用后的值：20

这里传递的是内存位置，而不是变量的值，这意味着你拥有了可以进行更改的位置。

注意参数是 int*，这是指针类型，因此例如，指向 char 的指针将是 char*。

## 指针算术

有时将指针移动到另一个内存位置可能很有用；这正是指针算术的用武之地。如果我们执行比如 ptr++，而 ptr 是一个整型指针，那么它现在会向前移动 4 字节（int 的大小），如果再运行一次，又会移动 4 字节，依此类推。这意味着指针（如果指向有效的数组结构）可以表现得非常像数组。示例如下：

```c
int arrayInt[] = { 10, 20, 30 };

size_t arrayInt_Size = 3;

//Will point to the first array index
int* ptr = &arrayInt;
for (int i = 0; i < arrayInt_Size; i++)
{
    //Remember, *ptr gets the value in the memory location
    printf("Value of arrayInt[%d] = %d\n", i, *ptr);

    ptr++;
}
```

输出：

> arrayInt[0] 的值 = 10
> arrayInt[1] 的值 = 20
> arrayInt[2] 的值 = 30

这表明，指向数组第一个地址的指针可以沿着数组的地址递增（记住，数组的每个值都存储在相邻的内存位置中）

你也可以反过来递减指针，即让指针的值减小。

还可以使用 ==、< 和 > 等关系运算符来比较指针。最常见的用途是检查两个指针是否指向同一位置：

```c
int value;

//Assigns ptr1 and ptr2 the same value
int* ptr1 = &value;
int* ptr2 = &value;

//ptr3 is assigned another value
int* ptr3 = NULL;

if (ptr1 == ptr2)
{
    printf("ptr1 and ptr2 are equal!\n");
}

if (ptr1 != ptr3)
{
    printf("ptr1 is not equal to ptr3\n");
}
```

这会检查各个指针是否相等。使用 > 和 < 也可以进行同样的操作。

## 函数指针

就像可以对变量做的那样，你也可以对函数做同样的事；下面是一段展示如何定义函数指针的代码。关键部分将高亮显示：

```c
void printAddition(int value1, int value2)
{
    int result = value1 + value2;
    printf("The result is: %d", result);
}

int main()
{
    //Function pointer definition
    //<returnType>(*<Name>)(<Parameters>)
    void(*functionPtr)(int, int);
    functionPtr = &printAddition;
    //Invoking call to pointer function
    (*functionPtr)(100, 200);
    return 0;
}
```

定义函数指针的基本结构如下

`<Return_Type> (*<Name>) (<Parameters>)`

其中在本例中：

`<Return_Type> = void`

`<Name> = functionPtr`

`<Parameters> = int, int`

这个函数指针现在可以作为参数传递，并用于你希望改变代码行为但几乎使用相同代码的场景。

一个例子是动态选择计算器应执行什么操作（注意：这是复杂代码，应仅作为粗略示例使用，所以如果你没有完全理解也不用担心）

```c
void calculator(int value1, int value2, int(*opp)(int,int))
{
    int result = (*opp)(value1, value2);
    printf("The result from the operation: %d\n", result);
}

//Adds two values
int add(int num1, int num2)
{
    return num1 + num2;
}

//Subtracts two values
int sub(int num1, int num2)
{
    return num1 - num2;
}

int main()
{
    calculator(10, 20, &add);
    calculator(10, 20, &sub);
    return 0;
}
```

这里发生的情况是，我们将函数“add”和“sub”作为 calculator 函数的参数传递；正如你从高亮部分看到的，函数参数的定义方式与上面一样，定义了返回类型、名称和参数，传入 calculator 的只有用于函数指针的 &add 和 &sub。然后 calculator 函数会调用该指针，传入值并返回结果。

## 存储类别

在 C 中，每个变量都可以指定一个存储类别，用于定义某些特性。

这些类别是：

- 自动变量
- 静态变量
- 寄存器变量
- 外部变量

### 自动变量

到目前为止，我们定义的每个变量都是自动变量；它们在函数被调用时创建，并在函数退出时自动销毁。这些变量也称为局部变量。

```c
auto int value;
```

等同于

```c
int value;
```

### 静态变量

当你希望变量在超出作用域时不被销毁时，就可以使用 static；该变量将一直存在，直到程序结束。静态变量在整个程序生命周期中只创建一次。下面是一个使用静态变量的示例：

```c
void tick()
{
    //This will run once
    static int count = 0;
    count++;
    printf("The count is now: %d\n", count);
}

int main()
{
    tick();
    tick();
    tick();
}
```

输出：

> 当前计数为：1
> 当前计数为：2
> 当前计数为：3

高亮部分是静态定义，只会运行一次。

### 寄存器变量

register 用于定义要存储在寄存器内存中而不是常规内存中的变量，寄存器内存的优点是访问速度快得多；然而，寄存器内存只能容纳少量变量。

定义寄存器变量如下所示：

```c
register int value;
```

### 外部变量

我们之前提到过，全局变量是未在作用域中定义的变量，因此可以在任何地方使用。外部变量是在单独位置（例如另一个文件）中定义的变量，extern 关键字用于表示该变量在另一个文件中。你可以通过在文件顶部放置以下内容来包含另一个文件作为引用：

```c
#include "FileName.c"
```

这是为了告诉程序也要引用此文件。注意，这些文件需要位于同一位置。

程序 1 [File_2.c]

```c
#include <stdio.h>

#include "C_TUT.c"

int main()

{
```

