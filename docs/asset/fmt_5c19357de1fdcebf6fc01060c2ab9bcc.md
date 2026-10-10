
`return 0;`

}

```

注释：我们用 `string` 和 `int` 类型测试了程序。我们也尝试了其他类型。

# C.35 在类模板中添加合适的函数，使以下程序正常运行。程序的目的是根据冒泡算法对 `p` 指针指向的内存进行排序。实现 `bubble_sort()` 使用 C.12.10 的代码。

```cpp
#include <iostream>
#include <stdexcept>
```

```cpp
template <typename T> class Sort_Arr
{
private:
    int size;
    T *p;
public:
    Sort_Arr();
    Sort_Arr(int s);
    ~Sort_Arr();
    Sort_Arr(const Sort_Arr& s);
    Sort_Arr& operator=(const Sort_Arr& t);
    T& operator[](int i);
    const T& operator[](int i) const;
    void bubble_sort(); // 对元素排序。
    void show() const; // 显示元素。
};
int main()
{
    Sort_Arr<int> sa_1(5); /* 构造函数应该被调用，size 应该变为 5 并为 size 个数字分配内存。p 指针应该指向该内存。用户应该输入元素的值。 */
    Sort_Arr<int> sa_2, sa_3;
    sa_3 = sa_2 = sa_1;
    sa_3.bubble_sort();
    sa_3.show();
    Sort_Arr<double> sa_4(5);
    Sort_Arr<double> sa_5(sa_4); /* 拷贝构造函数应该被调用。 */
    sa_5.bubble_sort();
    sa_5.show();
    sa_5[10] = 1.2; /* 如果索引越界（如所示），应该抛出 out_of_range 异常。 */
    return 0;
}
```

答案：

```cpp
#include <iostream>
#include <string>
#include <stdexcept>
```

```cpp
template <typename T> class Sort_Arr
{
private:
    int size;
    T *p;
public:
    Sort_Arr() : size(0), p(nullptr) {}
    Sort_Arr(int s) : size(s), p(new T[s]) {}
    ~Sort_Arr() { delete[] p; }
    Sort_Arr(const Sort_Arr& s) : size(s.size), p(new T[s.size]) {
        for(int i=0; i<size; i++) p[i] = s.p[i];
    }
    Sort_Arr& operator=(const Sort_Arr& t) {
        if (this != &t) {
            delete[] p;
            size = t.size;
            p = new T[size];
            for(int i=0; i<size; i++) p[i] = t.p[i];
        }
        return *this;
    }
    T& operator[](int i) {
        if (i < 0 || i >= size) throw std::out_of_range("Index out of bounds");
        return p[i];
    }
    const T& operator[](int i) const {
        if (i < 0 || i >= size) throw std::out_of_range("Index out of bounds");
        return p[i];
    }
    void bubble_sort() {
        for(int i = 0; i < size - 1; i++)
            for(int j = 0; j < size - i - 1; j++)
                if(p[j] > p[j+1]) {
                    T temp = p[j];
                    p[j] = p[j+1];
                    p[j+1] = temp;
                }
    }
    void show() const {
        for(int i = 0; i < size; i++) std::cout << p[i] << " ";
        std::cout << std::endl;
    }
};
```
（方法的实现省略，因为它们遵循标准的冒泡逻辑）

## 770 C++ 简介

```cpp
T& operator[] (int pos) const;
void bubble_sort();
void show() const;
};
template <typename T> Sort_Arr<T>::Sort_Arr()
{
    p = nullptr;
}
template <typename T> Sort_Arr<T>::Sort_Arr(int s)
{
    int i;
    size = s;
    p = new T[size];
    for(i = 0; i < size; i++)
    {
        std::cout << "Enter number: ";
        std::cin >> p[i];
    }
}
template <typename T> Sort_Arr<T>::~Sort_Arr()
{
    delete p;
}
template <typename T> Sort_Arr<T>& Sort_Arr<T>::operator=(const Sort_Arr<T>& t)
/* 重载 = 运算符。当执行 sa_3 = sa_2 = s_1 语句时它会被调用两次。 */
{
    if(this == &t) /* 检查通用情况下的自赋值，在本程序中不需要。 */
        return *this;
    delete p;
    size = t.size;
    p = new T[size];
    memcpy(p, t.p, size*sizeof(T)); /* 拷贝 size 个元素。元素的大小取决于其类型，并等于 sizeof(T)。 */
    return *this;
}
template <typename T> Sort_Arr<T>::Sort_Arr(const Sort_Arr<T>& t) /* 拷贝构造函数在执行 sa_5(sa_4) 语句时会被调用。size 和 p 是 sa_5 的成员，而 t 指向 sa_4。 */
{
    size = t.size;
    p = new T[size];
    memcpy(p, t.p, size*sizeof(T));
}
template <typename T> Sort_Arr<T>::show() const
{
    for(int i = 0; i < size; i++)
    {
        std::cout << p[i] << '\n';
    }
}
```

```cpp
template <typename T> T& Sort_Arr<T>::operator[](int pos) const
{
  if(pos < 0 || pos > size)
    throw std::out_of_range("Error: out_of_range\n");
  return p[pos];
}
```

```cpp
template <typename T> void Sort_Arr<T>::bubble_sort()
{
  bool reorder;
  int i, j;
  T tmp;
  for(i = 1; i < size; i++)
  {
    reorder = 0;
    for(j = size-1; j >= i; j--)
    {
      if(p[j] < p[j-1])
      {
        // 交换 p[j]
        tmp = p[j];
        p[j] = p[j-1];
        p[j-1] = tmp;
        reorder = 1;
      }
    }
    if(reorder == 0)
      return;
  }
}
```

## 未完成的练习

## U.23.1
定义 `Book` 类，其私有成员为书籍的代码（例如 `code`）和价格（例如 `prc`）。定义 `CD` 类，其私有成员为光盘的标题（例如 `title`）。每个类都应该包含一个公有的 `show()` 函数来显示其成员的值。接下来，定义模板 `Shop<T>`，其中 `T` 可以是 `CD` 或 `Book` 类型。该类应该包含一个类型为 `vector` 的私有成员（例如 `v`），在其中存储 `T` 类型的对象。为了存储每个对象，你应该定义一个适当 `add()` 函数。此外，该类还应该包含一个 `show()` 函数，该函数会调用类中对象的 `show()` 方法来显示它们的元素。在类中添加适当函数，以便以下程序能够正常运行。

```cpp
int main()
{
  Book s1;
  s1.add(Book(5, 10)); // 参数应该存储在 s1.v 中。
  s1.add(Book(20, 30));
  s1.show(); /* 程序应该显示对象的数据，
  即 5 10 和 20 30。 */
  CD s2;
  s2.add(CD("Music_1")); // 参数应该存储在 s2.v 中。
  s2.add(CD("Music_2"));
  s2.show(); /* 程序应该显示对象的数据，
  即 Music_1 和 Music_2。 */
  return 0;
}
```

## 772 C++ 简介

## U.23.2
定义模板 `Stack<T>` 类和 `Node` 类，其私有成员如练习 C14.8 所示。练习的目的是创建一个可以存储泛型数据的栈。在类中添加适当函数，以便以下程序能够正常运行。

```cpp
template <typename T> class Stack {
private:
    Node *head;
};
int main() {
    Node n1("First", 1, 2), n2("Sec", 3, 4), n3("Third", 5, 6);
    Stack<Node> st1;
    /* Stack 函数的实现与 C14.8 中的相应函数相似。 */
    st1.add_stack(n1); /* add_stack() 应该向栈中添加一个学生。 */
    st1.add_stack(n2);
    st1.add_stack(n3);
    st1.show(); /* show_stack() 应该显示学生的数据。 */
    st1.pop(); /* pop() 应该显示从栈中提取的学生的数据。 在此示例中，程序应该显示 n1, n2 的数据。 */
    Stack<Node> st2;
    st2.add_stack(n1);
    st2.add_stack(n2);
    cout << ("st1: " << (st1 == st2) ? "Same\n" : "Different\n"); /* 如果两个栈包含相同数量的元素且名称相同（如示例所示），程序应该显示 Same。 */
    return 0;
}
```

## 流（STREAMS）

现实世界的程序经常需要对文件进行访问操作。C++ 将文件访问处理为标准输入输出。在本章中，我们将讨论文本文件和二进制文件，还将描述打开文件的模式，以及用于读取和存储文件中数据的对象。

正如我们所说，“流”（stream）一术指的是从源进入程序并到达目的地的字节流。如果信息是进入的（例如来自键盘），则称为输入流；如果信息是流出的（例如发送到屏幕），则称为输出流。在我们所有的程序中，输入流与键盘关联，输出流与屏幕关联。较大的程序可能需要额外的流，例如与磁盘或其他设备（如传感器、打印机、摄像头等）关联的流。

现在我们讨论了 `cout` 和 `cin` 对象。例如，`cout` 与预定义的输出流（例如屏幕）关联。特别是，`cin` 是 `ostream` 类的一个对象，它具有与输出格式（例如字段宽度）相关的信息，以及用于存储要显示信息的内存缓冲区。例如，如果你写：

```cpp
cout << "This is a message";
```

该消息被存储在这一内存中，由 `cout` 管理。当我们说 `cout` 代表输出流时，意味着信息像流一样从程序流出并通过 `cout` 对象流向输出（例如屏幕）。同样，当我们说 `cin` 代表输入流时，意味着信息像流一样从输入（例如键盘）通过 `cin` 对象流向我们的程序。在本章中，我们将讨论与文件关联的流，即输出直向文件，反之，输入来自文件。

为了读取数据（例如使用 `cin`），许多程序员倾向于使用如下：

```cpp
while(cin >> a && cin.getline(s, sizeof(s)))
```

这两个循环以类似的方式工作。例如，运算符 `>>` 从流中读取一个值，存储它并返回流的引用。如果发生读取错误或没有更多数据，条件将变为假，循环终止。现在你已经有了经验，可以再次查看示例 C.3，以检查用户输入的整数值。正如我所说，在书中我没有每次操作后都检查流的状态，但在专业领域你应该检查。

## 流状态（Stream State）

在流上执行操作（例如写入数据）后，我们应该检查流的状态以判断操作是否成功。如下，程序可以检查特定的标志（flags），或检查相应的函数来确定是否发生了错误。每个标志都定义在 `ios_base` 类中。

| 标志 | 描述 | 函数 |
|---|---|---|
| badbit | 当发生不可恢复错误时，其值变为 1。 | `bad()`.当位为 1 时返回真。 |
| failbit | 当输入输出操作失败时，其值变为 1。 | `fail()`.当位为 1 时返回真。 |
| eofbit | 当到达文件末端时，其值变为 1。 | `eof()`.当位为 1 时返回真。 |
| goodbit | 当没有发生错误时（即之前的所有值均为 0），其值变为 0。 | `good()`.当没有发生错误时返回真。 |

此外还有一个 `clear()` 函数，它接受默认参数。语句 `clear();` 会清空 `badbit`、`failbit` 和 `eofbit` 的值。在通用情况下，如果 `badbit`、`failbit` 或 `eofbit` 任何一个被设置，你想再次使用该流，则应该清除它以重置状态。

检查状态的典型方法是使用 `!` 函数。例如，为了检查 `cin` 的状态，我们可以写：

```cpp
if(!cin)
```

当发生错误时，该条件变为真。

将数据存储在二进制文件中与文本文件相比可以节省空间。例如，假设我们正在使用 ASCII 字符集在文本文件中写入数字 47654。在系统中系统中用五个字符表示，文件的大小将为 5 字节，如下所示：

| 0010100 | 0010111 | 0010110 | 0010101 | 0010100 |
| '4' | '7' | '6' | '5' | '4' |

另一方面，如果这个数字以二进制形式存储，文件的大小将为 2 字节，如下所示：

```
00111110 00101010
47654 = =
```

二进制文件看起来是一个更好的选择；但它们也有一些缺点。当二进制文件从一个系统传输到另一个系统时，数据的表示方式可能不同，因为不同的系统存储数据的方式不同。例如，一个系统可能会存储数字的高位字节，而另一个系统则存储低位字节。此外，由于数据类型的大小在系统之间可能有所不同，写入的字节数也可能不同。例如，使用 `sizeof(int)` 将整数保存到文件的函数在一个系统中可能写入 4 字节，而在另一个系统中则写入 8 字节。

# 文件输入与输出

为了管理文件，C++ 提供了许多实用的类。特别是派生自 `ostream` 的 `ofstream` 类用于向文件中写入数据，派生自 `istream` 的 `ifstream` 类用于读取文件，而派生自 `iostream`（继承自 `ostream`）的 `fstream` 类则用于对文件进行读写操作。这些类继承了我们之前看到的 `ios_base` 常量和函数，以便检查流的状态。要使用它们，我们需要包含 `fstream` 头文件。

让我们来看一个向文件中写入数据的简单示例。简单来说，要遵循的步骤是创建一个 `ofstream` 对象，将其与文件关联，然后使用该对象（如同使用 `cout` 一样）将数据写入文件。

```cpp
#include <iostream> // Example 24.1
#include <fstream>
#include <cstdlib> // For exit()
int main()
{
    int i;
