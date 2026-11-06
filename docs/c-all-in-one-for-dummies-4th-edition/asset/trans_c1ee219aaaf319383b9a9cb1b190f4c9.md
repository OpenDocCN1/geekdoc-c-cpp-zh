
也是相同的，额外输出数字的序列同样如此。因此，伪随机数生成器需要某种看起来以随机方式变化的种子。幸运的是，当前时间的秒分量是一个可变的输入，正确使用时它看起来是随机的。运行应用程序时，你很可能不会在完全相同的那一秒启动它。清单 2-7 中所示的 RandomNumber 示例展示了如何生成随机数。

### 清单 2-7：为随机数生成器设置种子

```cpp
#include <iostream>
#include <time.h>
#include <stdlib.h>

using namespace std;

int main()
{
    // Seed the random-number generator
    time_t now;
    time(&now);
    srand(now);

    // Print out a list of random numbers
    for (int i=0; i<5; i++)
    {
        cout << rand() % 100 << endl;
    }

    return 0;
}
```

该示例遵循处理随机数时经常见到的一个过程。要获取时间，必须包含 `time.h`。初始化并使用随机数生成器需要包含 `stdlib.h`。

- 通过创建一个名为 `now`、类型为 `time_t`（它只是一个数字）的特殊变量，获取当前时间以启动随机数生成器。
- 调用 `time()` 函数，传入 `now` 的地址，从而获得自 1970 年 1 月 1 日以来的秒数。
- 通过调用 `srand()`，使用时间种子初始化随机数。
- 通过调用 `rand()`，基于该种子创建一个随机数。

每次调用 `rand()`，都会得到一个新的随机 int。然而，这个数字可能不在你想要的范围内。为了将数字限制在 0 到 99 的范围内，代码使用了该数字的 *100 的模*。（也就是用该数字除以 100 后的余数。）第一次运行清单 2-7 时，你可能会看到以下输出：

```
19
69
85
83
47
```

第二次，你可能会看到以下输出。它与之前不同：

```
79
67
38
72
73
```

## 在数组中存储数据

大多数编程语言都支持一种称为数组的数据结构。*数组*是一组变量列表，所有变量并排存储在一行中。你可以通过一个名称访问它们。数组中的每个变量都必须具有相同的类型。本节以简单的方式告诉你如何为数据存储目的使用数组。关于以高级方式创建和使用数组的更详细讨论，见第 5 册第 1 章的“构建数组”一节。

创建数组时，需要指定该数组包含多少项。例如，你可以有一个包含 100 个整数的数组。或者你可以有一个包含 35 个字符串的数组，或一个包含 10 个指向 `BrokenBottle` 类的指针的数组。如果你正在处理的代码表示一种类型，就可以用它创建数组。

创建数组时，需要给它一个名称。你可以使用该名称后跟方括号中的*索引*编号来访问数组的*元素*（项）。第一个元素始终是 0。因此，如果你有一个名为 `AppendixAttacks`、包含五个整数的数组，第一个元素是 `AppendixAttacks[0]`。第二个是 `AppendixAttacks[1]`，然后是 `AppendixAttacks[2]`、`AppendixAttacks[3]`，最后是 `AppendixAttacks[4]`。

![](img/128ab511de4e7360e167e3b15cdd5dd0_322_0.png)

由于数组从元素编号 0 开始，因此数组中最后一个元素的索引比数组大小小 1。因此，一个包含 89 个元素的数组，其索引范围为 0 到 88。

### 声明和访问数组

下面是如何声明数组：

```cpp
int GrilledShrimp[10];
```

这一行声明了一个名为 `GrilledShrimp`、包含 10 个整数的数组。首先放类型（实际上是数组中每个元素的类型），然后是数组名称，最后是方括号中的元素数量。由于这声明了 10 个整数，它们的索引范围为 0 到 9。

要访问数组的第一个元素，请在数组名后的方括号中放入数字 0，如下所示：

```cpp
GrilledShrimp[0] = 10;
```

人们经常使用循环来填充数组或访问每个成员。人们通常称之为*遍历数组*。清单 2-8 中的 ArrayLoop 示例展示了如何创建和使用基本数组。

### 清单 2-8：使用循环遍历数组

```cpp
#include <iostream>

using namespace std;

int main() {
    int Values[5];
    int VSize = sizeof(Values)/sizeof(*Values);
    cout << "Array count: " << VSize << endl;

    for (int i=0; i < VSize; i++) {
        Values[i] = i * 2;
        cout << Values[i] << endl;
    }

    return 0;
}
```

**记住：** 在代码中任何地方硬编码数组长度绝不是一个好主意，因为数组长度可能会变化。相反，应使用 `sizeof()` 函数计算数组的大小。该示例展示了如何完成此任务：获取 Values 的实际字节长度，并将其除以单个数组元素的大小，这需要使用 `*Values`。结果 VSize 是数组元素的数量。当你使用 for 循环遍历数组时，设置计数器变量 i，使其在等于或超过 VSize 的值时结束循环。

**警告：** 使用数组时，不要超出数组边界。由于早期 C 语言的一些旧规则，如果你编写的循环超出了数组的上边界，编译器不会警告你。运行应用程序时，你也可能不会遇到错误。

### 指针数组

数组特别适合存储指向对象的指针——指针是包含内存中某项地址的变量。如果你有许多相同类型的对象，可以将它们存储在数组中。

尽管可以将实际对象存储在数组中，但大多数人不会这样做，因为它们占用太多空间。大多数人会用指向这些对象的指针填充数组。要声明一个指向对象的指针数组，请记住在类型声明中使用星号，如下所示：

```cpp
CrackedMusicCD *missing[10];
```

清单 2–9 中所示的 ArrayPointer 示例声明了一个指针数组。在这个示例中，声明数组之后，将数组元素填充为零。记住，每个元素都是一个指针；这样，只需将其与 0 比较，就能立即知道该元素是否指向某个对象。如果它为 0，则表示未被使用。如果它不为 0，则其中有一个指针。

### 清单 2-9：使用数组存储指向对象的指针列表

```cpp
#include <iostream>

using namespace std;

class CrackedMusicCD {
public:
  string FormerName;
  int FormerLength;
  int FormerProductionYear;
};

int main() {
    CrackedMusicCD *Missing[10];
    int SMissing = sizeof(Missing)/sizeof(*Missing);

    for (int i=0; i < SMissing; i++) {
        Missing[i] = 0;
    }
    return 0;
}
```

如果你想创建一整组对象，并用指向这些对象的指针填充数组，可以这样做：

```cpp
for (int i=0; i < SMissing; i++) {
    Missing[i] = new CrackedMusicCD;
}
```

由于数组中的每个元素都是指针，如果你想访问数组所指向的某个对象的属性或方法，就需要使用 **->** 表示法来*解引用*该指针——即获取该指针所指向的值：

```cpp
Missing[0]->FormerName = "Shadow Dancing by Andy Gibb";
```

这个示例行访问地址位于数组第一个位置的对象 FormerName 属性。当你用完数组中的对象指针后，可以通过为数组的每个成员调用 `delete` 来删除这些对象，如下例所示：

```cpp
for (int i=0; i < SMissing; i++) {
    delete Missing[i];
    Missing[i] = 0;
}
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_324_0.png)

前面的代码将每个数组元素清除为 0。这样，指针会被重置为 0，并且在其对象消失后不再指向任何内容。

### 将数组传递给函数

有时你需要将整个数组传递给函数。尽管将整个对象传递给函数可能很笨拙，但传递整个数组可能很危险。数组可能非常庞大，包含数千个元素。如果每个元素都是指针，那么每个元素可能包含多个字节，这对较小的数组可行，但对于包含数千个元素的数组可能会引发问题。当你在栈上传递一个巨大的数组时，可能会*溢出*应用程序的栈——这意味着应用程序崩溃。幸运的是，编译器会自动为你将数组当作指针处理，但你仍然需要理解底层发生了什么。

与传递对象一样，最好的做法是传递数组的地址。你向函数传递一个指向该数组的指针。但将数组的地址传递给函数在编码时容易令人困惑。清单 2-10 中所示的 ArrayPassing 示例是一个传递数组的示例，它没有直接编写任何指针和地址。

### 清单 2-10：通过在函数头中声明数组来将数组传递给函数

```cpp
#include <iostream>

using namespace std;

const int MyArraySize = 10;

void Crunch(int myarray[], int size) {
    for (int i=0; i<size; i++) {
        cout << myarray[i] << endl;
    }
}

int main() {
    int BigArray[MyArraySize];

    for (int i=0; i<MyArraySize; i++)
    {
        BigArray[i] = i * 2;
    }

    Crunch(BigArray, MyArraySize);
    return 0;
}
```
