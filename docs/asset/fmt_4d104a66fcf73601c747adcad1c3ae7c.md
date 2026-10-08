
`delete [] intArray;` // mark memory for deletion

`delete collectionArray;`

`return 0;`

接下来，当我们通过 `for` 循环继续此示例时，注意我们正在使用典型的数组表示法 `[]` 来访问两个数组的每个元素，尽管这些数组是动态分配的。由于 `collectionArray` 是用户定义类型的动态分配数组，我们必须同样使用 `[]` 表示访问每个数组元素中的单个数据成员。虽然使用标准的数组表示法访问动态数组非常简单，你也可以使用指针表示法访问内存。

在循环内部，注意我们使用指针表示法增量地打印 `intArray` 的元素和 `collectionArray` 的 `y` 成员。在表达式 `*(intArray + i)` 中，标识符 `intArray` 代表数组的起始地址。通过在此地址上加上 `i`，你现在位于该数组第 i 个元素的地址上。通过用 `*` 对此复合对象进行解引用，你现在将进入正确的地址检索相关的整数数据，然后使用 `cout` 和插入运算符 `<<` 进行打印。同样，通过 `*(collectionArray + i)).y`，我们首先在 `collectionArray` 的起始地址上加上 `i`，然后使用 `()` 用 `*` 解引用该地址。由于这是一个用户定义类型，我们必须使用 `.` 来选择适当的数据成员 `y`。

最后，在这个示例中，我们演示了如何使用 `delete()` 释放不再需要的内存。对于标准类型的动态分配数组，一个简单的 `delete intArray;` 语句就足够了，但我们选择 `delete [] intArray;` 以与删除用户类型动态分配数组所需保持一致。也就是说，更复杂的语句 `delete [] collectionArray;` 对于正确删除用户类型数组是必要的。在所有情况下，与每个动态分配数组关联的内存将返回给系统。

### 动态分配二维数组 – 指针数组

两个或多个维度的数组也可以被动态分配。对于二维数组，列维度可以被动态分配，而行维度可以保持固定，或者两个维度都可以被动态分配。动态分配一个或多个维度允许程序员考虑有关数组大小的运行时决策。

让我们先考虑我们具有固定行数且每行中条目数量可变（即列维度）的情况。为了简单起见，我们将假设每行的条目数量从行到行是相同的，但事实并非如此。我们可以使用指针数组来模拟具有固定行数且每行运行时确定条目数量（列维度）的二维数组。

让我们考虑一个示例来说明列维度动态分配的二维数组：

```cpp
#include <iostream>

using std::cout;

using std::cin;

using std::endl;

using std::endl;

using std::flush;

constexpr int NUMROWS = 5; // 习惯使用大写

// 因为值在编译时已知

int main()

{

    float *TwoDimArray[NUMROWS] = { }; // 初始化为 nullptr

    int numColumns = 0;

    cout << "Enter number of columns: " ";

    cin >> numColumns;

    for (int i = 0; i < NUMROWS; i++)

    {

        // 为每行分配列数量

        TwoDimArray[i] = new float [numColumns];

        // 为每个条目加载数据

        for (int j = 0; j < numColumns; j++)

        {

            TwoDimArray[i][j] = i + j + .05;

            cout << TwoDimArray[i][j] << " ";

        }

    }

}
```

```cpp
}

cout << endl; // 在行之间打印换行

}

for (int i = 0; i < NUMROWS; i++) {

    delete [] TwoDimArray[i]; // 删除每行的列

}

return 0;

}
```

在此通知中，我们最初声明了一个 `float` 类型的指针数组：`float *TwoDimArray[NUMROWS];`。为了安全起见，我们将这些指针中的每一个初始化为 `nullptr`。有时，从右到左读取指针声明是有帮助的；也就是说，我们有一个大小为 `NUMROWS` 的数组，该数组包含指向浮点数的指针。更具体地说，我们拥有一个固定大小的指针数组，每个指针条目可以指向一个或多个连续的浮点数。每行中指向的条目数量代表列维度。

接下来，我们提示用户输入列数。在这里，我们假设每行具有相同数量的条目（形成列维度）；然而，每行的总条目数可能是不同的。通过假设每行的条目数量相同，我们使用了一个带有 `i` 的简单循环为每行分配列数量：`TwoDimArray[i] = new float[numColumns];`。

在使用 `j` 作为索引的嵌套循环中，我们只需为外层循环指定的 `i` 行的每个列条目加载值。`TwoDimArray[i][j] = i + j + .05;` 的任意赋值将一个有趣的值加载到每个元素中。在索引 `j` 的嵌套循环中，我们还打印了行 `i` 的每个列条目。

最后，程序演示了如何释放动态分配的内存。由于内存是在对固定行数的循环中分配的——每次内存分配包含该行的所有列条目——因此释放内存的方式也是类似的。对于每一行，我们都使用语句：`delete [] TwoDimArray[i];`

该示例的输出如下：

```
Enter number of columns: 3
0.05 1.05 2.05
1.05 2.05 3.05
2.05 3.05 4.05
3.05 4.05 5.05
4.05 5.05 6.05
```

接下来，让我们看看该示例的内存布局。与之前的内存图一样，使用的内存地址是任意的——它们是 `new()` 可能会在堆上生成的示例地址。

![](img/9c4de6bb3cddfe7d5b7daa4cef2ad343_133_0.png)

图 3.3 - Chp3-Ex3.cpp 的内存模型

现在我们已经学习了如何利用指针数组来建模二维数组，让我们继续看如何使用指向指针的指针来建模二维数组，以便我们可以在运行时选择两个维度。

### 动态分配二维数组 – 指针的指针

为数组动态分配行和列维度可以为程序增加必要的运行时灵活性。为了实现这种终极灵活性，可以使用指向所需数据类型指针的指针来建模二维数组。最初，将分配代表行数的维度。接下来，对于每行，将分配每行中的元素数量。与上一个使用指针数组的示例一样，每行的元素数量（列条目）在行之间需要保持大小一致。然而，为了准确建模二维数组的概念，假设列的大小将从行到行均匀分配。

让我们考虑一个示例来说明一个行和列维度都是动态分配的二维数组：

https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/main/Chapter03/Chp3-Ex4.cpp

```cpp
#include <iostream>

using std::cout;

using std::cin;

using std::endl;

using std::flush;

int main()

{

    int numRows = 0, numColumns = 0;

    float **TwoDimArray = nullptr; // 指向指针的指针

    cout << "Enter number of rows: " << flush;

    cin >> numRows;

    TwoDimArray = new float *[numRows]; // 分配行指针

    cout << "Enter number of Columns: ";

    cin >> numColumns;

    for (int i = 0; i < numRows; i++)

    {

        // 为每行分配列数量
```

```cpp
TwoDimArray[i] = new float [numColumns];

// 为每个列条目加载数据

for (int j = 0; j < numColumns; j++) {

{

    TwoDimArray[i][j] = i + j + .05;

    cout << TwoDimArray[i][j] << " ";

}

cout << endl; // 在行之间打印换行

}

for (int i = 0; i < numRows; i++) {

    delete [] TwoDimArray[i]; // 删除每行的列

}

delete [] TwoDimArray; // 删除分配的行

return 0;

}
```

在这个示例中，注意我们最初通过以下方式声明了一个指向 float 类型的指针的指针：`float **TwoDimArray;`。从右到左读取此声明，我们看到 `TwoDimArray` 是一个指向指向 float 的指针。更具体地说，我们理解 `TwoDimArray` 将包含一个或多个连续的浮点数。现在，我们提示用户输入列数。通过 `TwoDimArray = new float *[numRows];` 这种分配创建了 `numRows` 个指针。在使用 `j` 作为索引的嵌套循环中，我们只需为外层循环指定的 `i` 行的每个列条目加载值。`TwoDimArray[i][j] = i + j + .05;` 的任意赋值将一个有趣的值加载到每个元素中。在索引 `j` 的嵌套循环中，我们还打印了行 `i` 的每个列条目。

最后，程序演示了如何释放动态分配的内存。由于内存是在对固定行数的循环中分配的——每次内存分配包含该行的所有列条目——因此释放内存的方式也是类似的。对于每一行，我们都使用语句：`delete [] TwoDimArray[i];`

该示例的输出如下：

```
Enter number of columns: 3
0.05 1.05 2.05
1.05 2.05 3.05
2.05 3.05 4.05
3.05 4.05 5.05
4.05 5.05 6.05
```

接下来，让我们看看该示例的内存布局。与之前的内存图一样，使用的内存地址是任意的——它们是 `new()` 可能会在堆上生成的示例地址。

![](img/9c4de6bb3cddfe7d5b7daa4cef2ad343_137_0.png)

图 3.3 - Chp3-Ex3.cpp 的内存模型

现在我们已经学习了如何利用指针数组来建模二维数组，让我们继续看如何使用指向指针的指针来建模二维数组，以便我们可以在运行时选择两个维度。

```cpp
return 0;

}
```

在这个示例中，注意我们使用了三层间接来指定表示三维数组的变量 `int ***ThreeDimArray;`。随后我们为每一层间接分配了所需的内存。第一次分配是 `ThreeDimArray = new int ** [dim1];`，它分配了维度 1 的指针的指针集合。在遍历 `i` 的循环中，对于维度 1 中的每个元素，我们分配了 `ThreeDimArray[i] = new int * [dim2];`，以为数组的第二维分配整数指针。在遍历 `j` 的嵌套循环中，对于维度 2 中的每个元素，我们分配了 `ThreeDimArray[i][j] = new int [dim3];`，以按 `dim3` 指定的数量分配整数本身。

与前两个示例一样，我们在内层循环中初始化了数组元素，并打印了它们的值。到此时，你无疑会注意到这个程序与其前一个程序之间的相似之处。一种分配模式正在显现。

最后，我们将以与分配层类似（但顺序相反）的方式释放这三层内存。我们使用一个遍历 `j` 的嵌套循环来释放最内层的内存，随后在遍历 `i` 的外层循环中释放内存。最后，通过简单调用 `delete [] ThreeDimArray;` 释放初始维度的内存。

该示例的输出如下：

```
Enter dim1, dim2, dim3: 2 4 3
0 1 2
1 2 3
2 3 4
3 4 5
1 2 3
2 3 4
3 4 5
```

现在我们已经看到了如何使用指向指针的指针的指针来建模三维数组，已经出现了一种模式，展示如何声明所需的级别和数量的指针来建模 N 维数组。我们也可以看到必要的分配的模式。多维数组可能会变得非常大，特别是当你被迫使用最大的可能需要的固定大小数组来建模它们时。使用指针指向指针（指向指针，等等）对每个必要的多维数组进行建模的优妙之处在于，你可以分配一个可以在运行时确定的精确大小。为了方便使用，使用 `[]` 的数组符号作为指针表示法的替代方案，来访问动态分配数组中的元素。C++ 拥有许多源自指针的灵活性。动态分配数组展示了这种灵活性之一。

让我们继续深入理解指针，并考虑它们在函数中的用法。

## 在函数中使用指针

C++ 中的函数无疑会接收参数。我们在之前的章节中已经看到了许多说明函数原型声明和函数定义的示例。现在，让我们通过将指针作为参数传递给函数，以及使用指针作为函数的返回值，来加强对函数的理解。

### 将指针作为参数传递给函数

在函数调用中，从实际参数传递到形式参数的参数默认是在栈上进行拷贝的。为了修改作为函数参数的变量的内容，必须使用指向该参数的指针作为函数参数。

在 C++ 中，每当实际参数传递给函数时，都会创建该内容的副本并通过栈传递给该函数。例如，如果将一个整数作为实际参数传递给函数，会创建该整数的副本，然后通过栈传递给函数以作为形式参数被接收。在函数作用域内更改形式参数只会更改传入函数的数据的副本。

如果我们需要修改函数参数的能力，那么就有必要将目标数据的指针作为参数传递给函数。在 C++ 中，将指针作为实际参数传递会将该地址复制到栈上，并在函数中作为形式参数接收该地址的副本。然而，通过地址的副本，我们仍然可以访问地址（通过对该指针解引用）访问目标数据并对目标数据进行更改。

重申，当你在 C++ 中传递参数时，总会有内容在栈上拷贝。如果你传递一个非指针变量，你会获得该数据的副本并通过栈传递给函数。在函数作用域内对该数据进行的更改是局部更改，在函数返回时不会持续。本地副本在函数结束时简单地从栈上弹出。然而，如果你向函数传递一个指针，虽然存储在指针变量中的地址仍被复制到栈上并传递给函数，但你仍然可以对指针副本解引用以访问目标地址处的真实数据。

你总是需要比想要修改的内容领先一步。如果你想更改一个标准数据类型，请传递该类型的指针。如果你想更改指针本身的值（地址），你必须将指向该内容的指针作为参数传递给函数。记住，某些内容的副本是通过栈传递给函数的。你无法在函数作用域之外更改该副本。传递你想要更改内容的地址——你仍然传递的是该地址的副本，但使用它将带你到达真实数据。

让我们花几分钟理解一个将指针作为参数传递给函数的示例。在这里，我们将从检查两个有助于以下完整程序示例函数开始：

https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/main/Chapter03/Chp3-Ex6.cpp

```cpp
void TryToAddOne(int arg)

{

    arg++;

}

void AddOne(int *arg)

{

    (*arg)++;

}
```

检查之前的函数，注意 `TryToAddOne` 和 `AddOne` 的区别。

x: 10 和 *y: 15*

x: 10 和 *y: 16*

x: 11 和 *y: 16*

接下来，让我们通过将指针作为函数的返回值，继续讨论在函数中使用指针。

### 将指针作为函数的返回值

函数可以通过其 `return` 语句返回数据的指针。通过函数的 `return` 语句返回指针时，请确保所指向的内存在函数调用完成后后仍然存在。不要返回指向函数局部栈内存的指针。也就是说，不要返回指向函数内栈定义的局部变量的指针。然而，返回函数内部使用 `new()` 分配的内存指针是可以接受的。因为所分配的内位于堆上，它在函数调用结束后仍会存在。

让我们来看一个例子来解释这些概念：

https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/main/Chapter03/Chp3-Ex7.cpp

```cpp
#include <iostream>

#include <iomanip>

using std::cin;

using std::cout;

using std::endl;

using std::setw;

constexpr int MAX = 20;
```

```cpp
[[nodiscard] char *createName(); // 函数原型

int main()

{

    char *name = nullptr; // 指针的声明与初始化

    // 函数将分配内存

    name = createName();

    cout << "Name: " << name << endl;

    delete [] name; // 删除分配的内存（在不同的作用域中）

    return 0; // 这可能会出错

}

[[nodiscard] char *createName()

{

    char *temp = new char[MAX];

    cout << "Enter name: " << flush;

    cin >> setw(MAX) >> temp; // 确保 temp 不溢出

    return temp;

}
```
