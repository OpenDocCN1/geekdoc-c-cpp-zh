

不过，你只能有一个默认构造函数。也就是说，不能这样做：

```cpp
Klunk() { klunk_ct = 0; }      // constructor #1
Klunk(int n = 0) { klunk_ct = n; }   // ambiguous constructor #2
```

为什么这会产生歧义？请考虑下面两个声明：

```cpp
Klunk kar(10);      // clearly matches Klunk(int n)
Klunk bus;           // could match either constructor
```

第二个声明既匹配构造函数 #1（无参数），也匹配构造函数 #2（使用默认参数 0）。这会导致编译器发出错误消息。

## 复制构造函数

复制构造函数用于将一个对象复制到新创建的对象中。也就是说，它用于初始化过程，包括按值传递函数参数；而不会在普通赋值过程中使用。一个类的复制构造函数通常具有如下原型：

```cpp
Class_name(const Class_name &);
```

注意，它将一个类对象的常量引用作为参数。例如，String 类的复制构造函数可以具有如下原型：

```cpp
StringBad(const StringBad &);
```

关于复制构造函数，你必须了解两点：它在什么时候使用，以及它执行什么操作。

## 复制构造函数的使用时机

每当创建一个新对象，并使用同类的现有对象对其进行初始化时，就会调用复制构造函数。这种情况可能在多种场景下发生。最明显的情况是，显式地使用现有对象初始化新对象。例如，假设 `motto` 是一个 StringBad 对象，下面四个定义声明都会调用复制构造函数：

```cpp
StringBad ditto(motto);    // calls StringBad(const StringBad &)
StringBad metoo = motto;   // calls StringBad(const StringBad &)
StringBad also = StringBad(motto);
                          // calls StringBad(const StringBad &)
StringBad * ptrStringBad = new StringBad(motto);
                          // calls StringBad(const StringBad &)
```

具体取决于实现方式，中间的两个声明可能会直接使用复制构造函数来创建 `metoo` 和 `also`，也可能会使用复制构造函数生成临时对象，然后将这些临时对象的内容赋值给 `metoo` 和 `also`。最后一个示例使用 `motto` 初始化一个匿名对象，并将新对象的地址赋给 `ptrStringBad` 指针。

不太明显的是，每当程序生成对象的副本时，编译器也会使用复制构造函数。特别是，当函数按值传递对象时（如示例 12.3 中的 `callme2()`），或者当函数返回对象时，都会使用复制构造函数。请记住，按值传递意味着创建原始变量的副本。每当编译器生成临时对象时，也会使用复制构造函数。例如，在对三个 Vector 对象进行加法运算时，编译器可能会生成一个临时 Vector 对象来保存中间结果。编译器生成临时对象的时机各不相同，但在按值传递对象和返回对象时，都会调用复制构造函数。特别是，示例 12.3 中的以下函数调用会调用复制构造函数：

```cpp
callme2(headline2);
```

程序使用复制构造函数来初始化 `sb`，也就是 `callme2()` 函数的 StringBad 类型形式参数。

顺便说一下，按值传递对象需要调用复制构造函数，这也是应该改用按引用传递的一个重要理由。这样可以节省调用构造函数的时间，以及存储新对象所需的空间。

## 默认复制构造函数的作用

默认复制构造函数会对非静态成员执行逐成员复制（*成员逐一复制*，有时也称为*浅复制*）。每个成员都按值复制。在示例 12.3 中，语句

```cpp
StringBad sailor = sports;
```

等价于下面的语句（不过由于不允许访问私有成员，实际代码无法编译）：

```cpp
StringBad sailor;
sailor.str = sports.str;
sailor.len = sports.len;
```

如果某个成员本身是一个类对象，则会使用该类的复制构造函数，将一个成员对象复制到另一个成员对象中。静态成员（例如 `num_strings`）不会受到影响，因为它们属于整个类，而不是属于某个单独的对象。图 12.2 展示了隐式复制构造函数的工作方式。

## 回到 StringBad：复制构造函数出错的地方

现在，你已经可以理解示例 12.3 中的双重异常了。（假设输出就是示例代码后面所显示的内容。）第一个异常是，程序输出表明被销毁的对象比被构造的对象多两个。原因是，程序确实使用默认复制构造函数创建了两个额外的对象。调用 `callme2()` 函数时，复制构造函数用于初始化形式参数；同时，它还用于将 `sailor` 对象初始化为 `sports` 的副本。默认复制构造函数不会记录自己的操作，因此不会报告对象的创建，也不会递增 `num_strings` 计数器。不过，析构函数会更新计数，并且无论对象以何种方式构造，所有对象消亡时都会调用析构函数。这种异常会造成问题，因为它意味着程序无法准确地统计对象数量。解决方法是提供一个能够更新计数的显式复制构造函数：

```cpp
StringBad::StringBad(const StringBad & s)
{
    num_strings++;
    ...// important stuff to go here
}
```

![](img/9afc44517b591d64e2e19f623c9308ef_655_0.png)

图 12.2  成员逐一复制的内部示意。

### 提示

如果类中有一个静态数据成员，并且它的值会在创建新对象时发生变化，那么应该提供一个能够处理计数的显式复制构造函数。

第二个异常更加微妙，也更加危险。其中一个症状是字符串内容出现乱码：

```
headline2: Dû°
```

原因在于，隐式复制构造函数是按值复制的。以示例 12.3 为例。请回忆一下，其效果是：

```cpp
sailor.str = sports.str;
```

这并不会复制字符串，而是复制指向字符串的指针。也就是说，在使用 `sports` 初始化 `sailor` 后，最终会得到两个指向同一个字符串的指针。当 `operator<<()` 函数使用该指针显示字符串时，这并不会造成问题。但调用析构函数时，就会出现问题。请记住，StringBad 析构函数会释放 `str` 指针所指向的内存。销毁 `sailor` 的效果如下：

```cpp
delete [] sailor.str;   // delete the string that sports.str points to
```

由于 `sailor.str` 被赋予了 `sports.str` 的值，而 `sports.str` 指向字符串 `"Spinach Leaves Bowl for Dollars"`，因此 `sailor.str` 也指向 `"Spinach Leaves Bowl for Dollars"`。所以，`delete` 语句会释放存储该字符串所占用的内存。

接下来，销毁 `sports` 的效果如下：

```cpp
delete [] sports.str;   // effect is undefined
```

此时，`sports.str` 指向的内存位置已经被 `sailor` 的析构函数释放过了，这会导致未定义且可能有害的行为。在示例 12.3 中，程序会产生乱码字符串，这通常是内存管理不当的表现。

另一个令人担忧的症状是，尝试两次删除同一块内存可能导致程序异常终止。例如，Microsoft Visual C++ 2010（调试模式）会显示一个错误消息窗口，其中写着“调试断言失败！”，而 Linux 上的 g++ 4.4.1 会报告“重复释放或损坏”，然后终止程序。其他系统可能会显示不同的消息，甚至不显示任何消息，但相同的隐患仍然存在于这些程序中。

## 通过定义显式复制构造函数解决问题

解决这种类设计问题的方法是执行*深复制*。也就是说，复制构造函数不应只复制字符串的地址，而应该复制字符串本身，并将副本的地址赋给 `str` 成员。这样，每个对象都会拥有自己的字符串，而不是引用另一个对象的字符串。每次调用析构函数时，也会释放不同的字符串，而不是重复尝试释放同一个字符串。下面是 String 复制构造函数的一种编写方式：

```cpp
StringBad::StringBad(const StringBad & st)
{
    num_strings++;              // handle static member update
    len = st.len;               // same length
    str = new char [len + 1];   // allot space
    std::strcpy(str, st.str);   // copy string to new location

