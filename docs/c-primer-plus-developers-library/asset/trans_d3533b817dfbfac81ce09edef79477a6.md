
因此，`ps` 显示为字符串 "fox"，而 `(int *) ps` 显示为找到该字符串的地址。注意，将 `animal` 赋给 `ps` 并不会复制字符串；它复制的是地址。这会导致两个指针（`animal` 和 `ps`）指向同一内存位置和同一字符串。

要获得字符串的副本，你需要做更多工作。首先，需要分配内存来保存字符串。可以通过声明第二个数组或使用 `new` 来完成。第二种方法使你能够按字符串定制存储空间：

```
ps = new char[strlen(animal) + 1];  // get new storage
```

字符串 "fox" 并未完全填满 `animal` 数组，因此这种方法浪费空间。这段代码使用 `strlen()` 查找字符串长度；再加一得到包含空字符在内的长度。然后程序使用 `new` 分配刚好足够保存该字符串的空间。

接下来，你需要一种方法将字符串从 `animal` 数组复制到新分配的空间。将 `animal` 赋给 `ps` 行不通，因为这只会改变 `ps` 中存储的地址，从而丢失程序访问新分配内存的唯一途径。相反，需要使用 `strcpy()` 库函数：

```
strcpy(ps, animal);             // copy string to new storage
```

`strcpy()` 函数接受两个参数。第一个是目标地址，第二个是要复制的字符串的地址。你需要确保目标确实已分配，并且有足够空间容纳副本。这通过使用 `strlen()` 找到正确大小并使用 `new` 获取空闲内存来实现。

注意，通过使用 `strcpy()` 和 `new`，你会得到 "fox" 的两个独立副本：

```
fox at 0x0065fd30
fox at 0x004301c8
```

还要注意，`new` 将新存储定位在距离 `animal` 数组相当远的内存位置。

你经常会遇到需要将字符串放入数组的情况。初始化数组时使用 `=` 运算符；否则使用 `strcpy()` 或 `strncpy()`。你已经见过 `strcpy()` 函数；它的工作方式如下：

```
char food[20] = "carrots";  // initialization
strcpy(food, "flan");       // otherwise
```

注意，类似下面的代码可能会引发问题，因为 food 数组小于该字符串：

```
strcpy(food, "a picnic basket filled with many goodies");
```

在这种情况下，该函数会将字符串的其余部分复制到紧跟在数组之后的内存字节中，这可能会覆盖程序正在使用的其他内存。为避免该问题，应改用 `strncpy()`。它接受第三个参数：要复制的最大字符数。但请注意，如果该函数在到达字符串末尾之前用完空间，它不会添加空字符。因此，应这样使用该函数：

```
strncpy(food, "a picnic basket filled with many goodies", 19);
food[19] = '\0';
```

这会将最多 19 个字符复制到数组中，然后将最后一个元素设置为空字符。如果字符串短于 19 个字符，`strncpy()` 会提前添加一个空字符，以标记字符串的真正结尾。

**注意**

将字符串赋给数组时，应使用 `strcpy()` 或 `strncpy()`，而不是赋值运算符。

现在你已经了解了使用 C 风格字符串和 `cstring` 库的一些方面，就能体会到使用 C++ `string` 类型相对简单。你（通常）不必担心字符串溢出数组，并且可以使用赋值运算符而不是 `strcpy()` 或 `strncpy()`。

## 使用 new 创建动态结构

你已经看到，在运行时而不是编译时创建数组可能很有优势。结构也是如此。你只需为程序在特定运行期间所需的那么多结构分配空间。同样，new 运算符就是可用的工具。使用它，你可以创建动态结构。同样，*动态* 意味着内存在运行时分配，而不是在编译时分配。顺便说一句，因为类与结构非常相似，你也可以将本节学到的用于结构的技术用于类。

将 new 与结构一起使用分为两部分：创建结构和访问其成员。要创建结构，可将结构类型与 new 一起使用。例如，要创建一个 `inflatable` 类型的未命名结构并将其地址赋给合适的指针，可以使用以下代码：

```
inflatable * ps = new inflatable;
```

这会将一块足够大、可容纳 `inflatable` 类型结构的空闲内存的地址赋给 `ps`。注意，其语法与 C++ 内置类型完全相同。

棘手之处在于访问成员。创建动态结构时，不能对结构名使用点成员运算符，因为该结构没有名称。你拥有的只是它的地址。C++ 专门为这种情况提供了一个运算符：箭头成员运算符（`->`）。该运算符由连字符后跟大于号构成，对于指向结构的指针所起的作用，就像点运算符对结构名所起的作用一样。例如，如果 `ps` 指向一个 `inflatable` 类型的结构，那么 `ps->price` 就是所指向结构的 price 成员（见图 4.11）。

![](img/9afc44517b591d64e2e19f623c9308ef_193_0.png)

图 4.11 标识结构成员。

**提示**

有时 C++ 新手会混淆何时使用点运算符、何时使用箭头运算符来指定结构成员。规则很简单：如果结构标识符是结构名，使用点运算符。如果标识符是指向结构的指针，使用箭头运算符。

访问结构成员的第二种更丑陋的方法是认识到，如果 `ps` 是指向结构的指针，那么 `*ps` 表示所指向的值——即结构本身。然后，因为 `*ps` 是一个结构，`(*ps).price` 就是该结构的 price 成员。C++ 的运算符优先级规则要求在这种构造中使用括号。

### 清单 4.21 newstrct.cpp

```cpp
// newstrct.cpp -- using new with a structure
#include <iostream>
struct inflatable   // structure definition
{
    char name[20];
    float volume;
    double price;
};
int main()
{
    using namespace std;
    inflatable * ps = new inflatable; // allot memory for structure
    cout << "Enter name of inflatable item: ";
    cin.get(ps->name, 20);              // method 1 for member access
    cout << "Enter volume in cubic feet: ";
    cin >> (*ps).volume;                 // method 2 for member access
    cout << "Enter price: $";
    cin >> ps->price;
    cout << "Name: " << (*ps).name << endl;         // method 2
    cout << "Volume: " << ps->volume << " cubic feet\n"; // method 1
    cout << "Price: $" << ps->price << endl;         // method 1
    delete ps;                            // free memory used by structure
    return 0;
}
```

下面是清单 4.21 中程序的示例运行：

```text
Enter name of inflatable item: Fabulous Frodo
Enter volume in cubic feet: 1.4
Enter price: $27.99
Name: Fabulous Frodo
Volume: 1.4 cubic feet
Price: $27.99
```

## 使用 new 和 delete 的示例

我们来看一个使用 new 和 delete 管理存储从键盘输入的字符串的示例。清单 4.22 定义了一个函数 getname()，它返回指向输入字符串的指针。该函数将输入读入一个大的临时数组，然后使用带有适当大小的 `new []` 创建一块大小适合输入字符串的内存。然后该函数返回指向该内存块的指针。对于读取大量字符串的程序，这种方法可以节省大量内存。（在现实生活中，也就是我们许多人所在的世界里，使用 string 类会更容易，因为它在设计中内置了对 new 和 delete 的使用。）

假设你的程序必须读取 1,000 个字符串，最大的字符串可能有 79 个字符长，但大多数字符串要短得多。如果用 char 数组保存这些字符串，就需要 1,000 个各含 80 个字符的数组。那就是 80,000 字节，而这块内存中的很大一部分最终会未被使用。另一种方法是，你可以创建一个包含 1,000 个指向 char 的指针的数组，然后使用 new 只分配每个字符串所需的内存量。这可以节省数万字节。你不必为每个字符串都使用一个大数组，而是让内存适应输入。更好的是，你还可以使用 new 来只查找存储所需数量指针的空间。嗯，这目前有点过于雄心勃勃了。即使使用包含 1,000 个指针的数组，目前也有点过于雄心勃勃，但清单 4.22 展示了其中一些技巧。另外，为了说明 delete 如何工作，程序使用它来释放内存以便复用。

