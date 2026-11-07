

### 程序 19.19 学生表（姓名和分数）

|  |  |
|---|---:|
| George | 71 |
| John | 52 |
| Lucie | 98 |
| Mary | 88 |
| Robert | 77 |

字符串中单词的频率。我们使用一个名为 *freq* 的 *map* 对象，其中键是文本中遇到的单词，值是单词出现的频率。注意，我们使用 Ctrl + Z 字符来标记输入文件的结束（程序 19.20）。

### 程序 19.20 文本中单词的频率

```cpp
1  /*********************************************************
2   * A program to count the number of words in a text        *
3   *********************************************************/
4  #include <map>
5  #include <string>
6  #include <iomanip>
7  #include <iostream>
8  using namespace std;
9
10 int main()
11 {
12   // Declaration of map, iterator, and a string
13   map<string, int> freq;
14   map<string, int>::iterator iter;
15   string word;
16   // Reading and storing words in the map
17   cout << "Enter a sentence to be parsed: " << endl;
18   while (cin >> word)
19   {
20       ++freq[word];
21   }
22   // Printing the words and their frequency
23   for (iter = freq.begin(); iter != freq.end(); iter++)
24   {
25       cout << left << setw(10) << iter->first << iter->second << endl;
26   }
27   return 0;
28 }

Run:
Enter a sentence to be parsed:
we are in the world of this and that and this and that
^Z
```

| 单词 | 频率 |
|---|---:|
| and | 3 |
| are | 1 |
| in | 1 |
| of | 1 |
| that | 2 |
| the | 1 |
| this | 2 |
| we | 1 |
| world | 1 |

![](img/d68f6199646ca63591a6d8419e0ed4ba_912_0.png)

**图 19.13** 作为关联数组的 map

注意，我们将所有单词都输入为小写，以便更容易看出键是按顺序排列的。单词及其频率构成一个关联数组，即索引不必是整数的数组（图 19.13）。

## 19.6 使用函数

我们可以使用库算法，也可以定义自己的算法。在这两种情况下，算法都会对容器中的若干元素执行某种操作。问题在于，如何将此操作作为参数传递给算法。可以通过两种方式实现：函数指针或函数对象（*仿函数*）。下面分别讨论这两种方法。

### 19.6.1 函数指针

我们知道，函数的定义存储在内存中。存储在内存中的每个实体都有一个地址。实际上，函数名是指向存储该函数的内存首字节的指针，就像数组名是指向数组首元素的指针一样。图 19.14 展示了数组名和函数名作为指针的情况。该图还展示了数组指针和函数指针的声明方式。

我们来看一个函数指针的示例（程序 19.21）。我们想要使用一个名为 *fun* 的函数，它将另一个函数 *print* 作为参数。我们定义这两个函数。在 *main* 中，我们调用 *fun* 两次，每次调用都会调用 *print* 函数。注意，*fun* 的定义并未指定第二个参数具体要调用哪个函数。调用语句会传递指向 *print* 函数的指针（*print* 是指向 print 函数起始位置的指针）。

![](img/d68f6199646ca63591a6d8419e0ed4ba_912_1.png)

**图 19.14** 数组指针和函数指针

### 程序 19.21 使用函数指针

```cpp
/* **************************************************************
 * Using functions that call another function                    *
 ************************************************************** */
#include <iostream>
using namespace std;

// Definition of print function
void print(int value)
{
    cout << value << endl;
}

// Definition of fun function
void fun(int x, void (*f)(int))
{
    f(x);
}

int main()
{
    fun(24, print); // Calling function fun
    fun(88, print); // Calling function fun
    return 0;
}

Run:
24
88
```

在程序 19.21 中，函数指针的声明 `void (*f)(int)` 可能看起来有些特别，但好消息是，STL 中的大多数算法都已经定义了使用函数指针（例如 `print`）的函数，我们不需要自行声明。换句话说，如果 STL 算法使用函数指针，我们在调用时只需提供函数名。

我们使用 STL 泛型算法 `for_each`，它会对容器中某个范围内的元素应用一个函数。如程序 19.22 所示，该算法会将定义为第三个参数的函数应用于范围 [first, last)。算法规定第三个参数必须是函数指针。我们传入 *print* 的名称，然后定义一个名为 *print*、带有一个参数的函数。print 函数从迭代器（*iterator*）中获取参数值。

### 程序 19.22 使用 `for_each` 和用户定义的函数

```cpp
/* **************************************************************
 * Applying a function to all elements in a range using the      *
 * algorithm for_each in the library                           *
 ************************************************************** */
#include <vector>
#include <algorithm>
#include <iostream>
using namespace std;

// Definition of the print function
void print(int value)
{
    cout << value << " ";
}

int main()
{
    // Instantiation of a vector object and storing three values
    vector<int> vec;
    vec.push_back(24);
    vec.push_back(42);
    vec.push_back(73);
    // Using a print function to print the value of each element
    for_each(vec.begin(), vec.end(), print);
    return 0;
}

Run:
24  42  73
```

### 19.6.2 函数对象（仿函数）

在第 13 章中，我们了解到可以重载*函数调用运算符*（一对圆括号），从而创建一个*函数对象*（有时称为*仿函数*）。图 19.15 展示了普通函数和函数对象的写法。

程序 19.23 展示了如何在另一个函数（*main*）中调用*仿函数*。我们创建一个名为 *Print* 的类，重载 *operator()*，创建该类的对象，然后调用该运算符。注意，调用重载运算符实际上就是调用由该类实例化的对象，并将参数放在圆括号内。实际上，我们是在第 16 行调用 *print.operator()(45)*。

![](img/d68f6199646ca63591a6d8419e0ed4ba_914_0.png)

**图 19.15** 普通函数与函数对象

### 程序 19.23 使用仿函数

```cpp
1 /*******************************************
2 * Calling a function object to print the same value
3 *******************************************/
4 #include <iostream>
5 using namespace std;
6
7 class Print
8 {
9   public:
10    void operator()(int value) {cout << value;}
11 };
12
13 int main()
14 {
15   Print print; // Instantiation of an object of type Print
16   print(45); // calling operator()
17   return 0;
18 }
```

运行结果：45

可以看出，函数对象的定义比普通函数更长，但函数对象具有一些优点，足以弥补其定义较长的不足：

- 函数对象作为对象，可以在任何能够使用对象的地方使用。特别是，它可以作为参数传递给函数，也可以从函数中返回。
- 函数对象可以拥有状态，也就是说，它可以保存从一次调用到下一次调用的信息。
- 我们可以定义一个用作函数对象的类，然后从该类继承以创建其他函数对象。

### STL 算法中的函数对象

为了方便使用算法，STL 库定义了许多函数对象。它们可以分为一元函数对象（接受一个参数）和二元函数对象（接受两个参数）。这些函数对象定义在 `<functional>` 头文件中，可以在程序中使用。表 19.5 列出其中的一些函数对象。

**表 19.5** STL 中的函数对象

| 函数对象 | 类型 | 元数 | 运算符 |
|---|---|---|---|
| `negate<T>` | 算术 | 一元 | - |
| `plus<T>` | 算术 | 二元 | + |

（续）

