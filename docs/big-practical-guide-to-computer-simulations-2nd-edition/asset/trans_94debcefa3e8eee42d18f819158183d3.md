
由括号中构造函数的参数给出。如果你偷懒，不想声明参数，可以使用标准构造函数，如下所示：

```cpp
1  Histo::Histo()
2  {
3      Histo(0, 1, 10);   // Use standard values
4  }
```

这里可以看到，与数据成员一样，成员函数可以像局部变量一样，在（其他或同一个）成员函数内部直接使用/调用。如果使用标准构造函数定义对象 his2，它类似于 C 语言中的变量定义，例如：⁷

```cpp
Histo his2;
```

⁷你也可以包含空括号，明确表示没有传递任何参数。

第三种构造函数是所谓的复制构造函数。它用于通过从另一个对象复制来初始化对象时：

```cpp
Histo his3 = his;
```

原则上，你不必定义自己的复制构造函数。如果没有给出显式复制构造函数，新对象（his3）只是给定对象（his）的逐成员复制。但这意味着 his3 中的指针元素 table 指向与 his 中完全相同的内存区域。这通常不是你想要的。相反，人们希望 his3 拥有自己的 table，但其中填入与 his 相同的数字。这可以通过以下显式复制构造函数实现：

```cpp
1  Histo::Histo(const Histo &h)
2  {
3      from = h.from;              // store parameters
4      to = h.to;
5      low = h.low;
6      high = h.high;
7      n_bins = h.n_bins;
8      delta = h.delta;            // bin width
9      table = new double[n_bins]; // get memory for bins;
10
11     for(int t=0; t<n_bins; t++)  // copy bin entries
12         table[t] = h.table[t];
13 }
```

它看起来与第一个构造函数非常相似，但有一些差异。数据成员的初始值取自传递给构造函数的对象 h。形式上，它被写为参数，尽管在使用它时，数据来源对象写在 = 赋值运算符之后。h 的变量声明前面有 & 字符，这意味着变量通过引用传递。这意味着只传递地址，就好像对象作为指针传递一样。不过，通过引用传递时，可以直接访问对象，而不像指针那样使用 * 运算符。注意，对象 h 的数据元素像结构体中的元素一样被访问。这里允许这样做，因为复制构造函数是该类的成员函数，尽管被访问的对象不同于调用该成员函数的对象。

在任何地方创建的对象，在使用后都必须删除。在第 5.2 节给出的 C 实现中，这是由函数 histo_delete() 完成的。在 C++ 中，删除对象是析构函数的任务，析构函数始终是一个成员函数，其名称为类名前加 ~ 字符。在这里，析构函数必须释放 bins 的 table：

```cpp
Histo::~Histo()
{
    delete[] table;
}
```

第 3 行中 delete 的效果等价于 C 中的函数 free()。如果删除的是数组，如这里所示，必须在 delete 命令后写上 [] 括号。

接下来考虑用于插入数字的成员函数 insert()。它以要插入的数字作为参数。这里，就像普通函数一样，应声明返回类型，在本例中为 void。注意，插入数字的直方图并未作为参数显式传递，因为调用成员函数的对象可在成员函数内部通过“局部”变量访问：

```cpp
void Histo::insert(double number)
{
    if(number < from)      // insert into histogram
        low++;
    else if (number >= to)
        high++;
    else
        table[(int) floor( (number - from) / delta)]++;
}
```

要打印直方图，你可以定义另一个成员函数，例如使用 printf() 函数打印数组 table 的内容。这里展示另一种 C++ 特有的解决方案。在 C++ 中，可以通过流进行打印。一个类似于 C 中 stdout 的标准输出流是 std::cout。你可以通过以下方式将字符串 "number: " 写入标准输出，随后是变量 num 的内容，再随后是一个换行：

```cpp
std::cout << "number: " << num << std::endl;
```

这等价于 printf("number: %d\n", num)。因此，运算符 << 用于输出。要打印的多个对象可以通过多次出现 << 来分隔。注意，std::cout 属于命名空间 std。因此，std:: 并不指代类名。C++ 使用命名空间来允许不同对象在不同命名空间中具有完全相同的名称。标准命名空间 std 包含许多常用对象。如果你偷懒，可以在文件顶部的所有 #include 命令下方写上 using namespace std。现在你可以写 cout 而不是 std::cout，但前提是不存在其他名为 cout 的对象、变量或类型。最后，std::endl 是行尾标记，等价于 "\n"。

如果你想以与标准变量相同的方式将直方图写入 std::cout，例如通过使用 << 运算符。在这种情况下，必须相应地定义运算符 <<。其工作方式如下。该运算符获取要打印的流（os）和 Histo 对象（h）作为参数，并再次返回该流。再次注意，<< 可以访问 h，因为该运算符在头文件中被声明为友元。

```cpp
std::ostream& operator << (std::ostream& os, const Histo& h)
{
    os << "# below:" << h.from << std::endl;
    os << "# above: " << h.to << std::endl;
    os << "# from: " << h.from << " delta: " << h.delta;
    os << "# nbins: " << h.n_bins << std::endl;
    for(int i=0; i<h.n_bins; i++)
        os << i << " " << h.table[i] << std::endl;
    return(os);
}
```

赋值运算符 = 也常常为 C++ 类显式实现。如果没有给出实现，对象会按位复制，这可能并不理想，类似于复制构造函数的情况。对于 Histo，赋值运算符如下所示：

```cpp
Histo& Histo::operator=(const Histo &h)
{
    if(this != &h)            // no self assignment
    {
        from = h.from;        // store parameters
        to = h.to;
        n_bins = h.n_bins;
        delta = h.delta;      // bin width
        delete[] table;       // delete old table
        table = new double[n_bins];   // get memory for bins;
        low = h.low;
        high = h.high;
        for(int t=0; t<n_bins; t++)   // copy bin entries
            table[t] = h.table[t];
    }
    return (*this);
}
```

该实现看起来与复制构造函数非常相似。⁸ 注意，应禁止将对象赋值给“自身”。这通过局部变量 this 在第 3 行得到保证，该变量指向所有成员内部

⁸因此，可以使用一个私有函数 do_copying()，它在需要的地方执行复制。

注意，Histo 的成员函数 insert() 可以直接调用。在这种情况下，它也会自动针对当前对象调用，也就是调用 Histo::insert() 的对象。

练习 (2) 要求你实现一个简单的成员函数 Histo::mean()，它返回直方图中存储数字的均值。在本书范围内，不可能超出 C++ 基础知识。更多细节可在 C++ 文献 [Stroustrup (2000)] 中找到，特别是关于模板的内容，模板是无需指定参数类型的函数或类。这允许实现可处理多种类型的对象。特别重要的是容器类，它们可以存储“任何东西”。一些容器类实现在标准模板库中，第 7.2 节将介绍该库。
