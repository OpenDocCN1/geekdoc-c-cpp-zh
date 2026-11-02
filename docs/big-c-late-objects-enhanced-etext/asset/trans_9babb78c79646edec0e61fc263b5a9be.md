

```cpp
cout << noon << "\n";
```

实际含义是

```cpp
(cout << noon) << "\n";
```

也就是说

```cpp
operator<<(cout, noon) << "\n"
```

对 operator<<(cout, noon) 的调用会打印出时间 noon，然后返回 cout。接着 cout << "\n" 会打印一个换行符。专题 13.3 解释了为什么该函数的返回类型是引用 ostream&。

你还可以定义一个 operator>> 来从输入流中读取一个 Time 对象。

```cpp
istream& operator>>(istream& in, Time& a)
{
    int hours;
    char separator;
    int minutes;
    in >> hours;
    in.get(separator);  // 读取 : 字符
    in >> minutes;
    a = Time(hours, minutes);
    return in;
}
```

请注意，>> 运算符返回输入流，这与 << 运算符类似。然而，与 << 运算符不同的是，>> 运算符必须有一个类型为 Time& 的参数。当该参数被填入输入内容时，它会被修改。

基本运算符重载相对容易，而且许多人觉得它很有趣。但是，如前所述，最好不要过度使用。使用不恰当的运算符可能会使程序更难阅读。

## 示例代码

参见随附代码中的 sec01，其中有一个示例程序，为 Time 类定义了多个重载运算符。

### 13.1.4 运算符成员函数

> 运算符既可以定义为成员函数，也可以定义为非成员函数。

当定义一个第一个参数类型为类的运算符函数时，你可以选择将其变为该类的成员函数。如果你想访问该类的私有实现，这是一个优点。例如，不用函数

```cpp
Time operator+(Time a, int min)
```

你可以定义一个成员函数

```cpp
Time Time::operator+(int min) const
{
    int result_minutes = hours * 60 + minutes + min;
    return Time((result_minutes / 60) % 24, result_minutes % 60);
}
```

注意，这个成员函数被定义为 const，因为隐式参数（也就是该运算符的第一个参数）没有被修改。

当你将运算符定义为成员函数时，它仍然以运算符表达式的方式被调用。编译器会将运算符表达式转换为成员函数调用。例如，表达式

```cpp
t + 60
```

返回一个指向局部变量的引用是无效的，因为该局部变量会在函数退出时被销毁。

返回引用的另一个原因是提供对对象内部数据的写访问。例如，string 类提供了 operator[]，你可以用它来修改字符串的内容：

```cpp
string greeting = "hello";
greeting[0] = 'H';
```

表达式 greeting[0] 不能是一个 char 值，因为它出现在 = 运算符的左侧。相反，它是一个引用。下面是一个实现，假设 string 类将字符存储在一个名为 buffer 的 char[] 数组中：

```cpp
char& string::operator[](int index)
{
    return buffer[index];
}
```

operator[] 函数实际上返回的是 buffer[index] 的地址。语句 greeting[0] = 'H'; 的含义是：*(返回的指针) = 'H';

这个 operator[] 函数有一个缺点。它不能用于 const 对象。因此，string 类还有第二个版本的运算符：

```cpp
char string::operator[](int index) const
{
    return buffer[index];
}
```

![](img/d61019b035dd82beb581604273c0ee6b_671_0.png)

## 工作示例 13.1

## 分数类

学习如何实现一个表示分数（两个整数值的比值）的新数据类型。请参阅你的电子文本或访问 wiley.com/go/bc10。

## 13.2 自动内存管理

在第 7 章中，你了解了使用 new 运算符进行内存分配的概念，以及使用 delete 运算符释放已分配内存的必要性。在 C++ 中，自由存储区上的内存管理明确由程序员来掌控。然而，当你编写的类需要分配内存时，你不能指望类的用户显式地释放内存。在以下各节中，你将学习如何实现能够正确管理内存的类。

### 13.2.1 分配内存的构造函数

从本书开头你就一直在使用 string 对象。你可能没有意识到的是，字符串的内容实际上并不存储在 string 对象本身中。相反，一个 string 类型的对象持有一个指向字符数组的指针。

### 13.2.2 析构函数

```
len = 0;
buffer = nullptr;
}
```

析构函数的作用是在对象不再使用时负责资源管理。

当对象变量超出作用域时，或者当自由存储区上的对象被删除时，析构函数会被调用。

当一个 String 对象超出作用域时，该对象所占用的内存会被复用。然而，这带来了一个问题。只有对象的实际内存（由 buffer 和 len 变量组成）被回收。但是，buffer 所指向的数组并不会被删除。当 String 对象不再可用时，就无法再定位到指向该数组的指针，于是就会发生内存泄漏（见图 2）。

C++ 语言有一种特殊机制来克服这个潜在问题。你可以定义一个析构函数，它是一个在对象变量即将超出作用域时，或者对象所占用的内存被删除时总会调用的函数。

```
void fun()
{
    String str;
} // 这里自动调用 str.~String()
```

String 类的析构函数应当通过 buffer 指针删除数组。

下面是析构函数的代码（参见语法 13.2）。注意，析构函数的名称是类名，前面加上 ~ 符号。

```
String::~String()
{
    delete[] buffer;
}
```

如果 buffer 是一个空指针，会发生什么？对 nullptr 调用 delete 是安全的——它什么也不做。因此，你不需要针对这种情况进行特殊处理。

![](img/d61019b035dd82beb581604273c0ee6b_673_0.png)

## 文档示例标题

这是一段示例文本，用于演示文档结构提取的结果。文字内容应当保持原始段落顺序，并转换为Markdown格式。

### 二级标题

- 列表项一
- 列表项二
- 列表项三

引用示例：

> > 这是一段引用文本，展示了文档中的引用样式。

### 表格标题

| 列A | 列B | 列C |
| --- | --- | --- |
| 值1 | 值2 | 值3 |
| 值4 | 值5 | 值6 |

![](img/d61019b035dd82beb581604273c0ee6b_679_0.png)

![](img/d61019b035dd82beb581604273c0ee6b_679_1.png)

```python
print("Hello, world!")
```

## 复习题

■ R13.1 对于某个特定操作，你什么时候会选择重载运算符，什么时候会选择使用函数？

■ R13.2 你是否可以重载一元取反运算符，使得 -T 将 Time 值 T 减少 60 秒？这是一个好主意吗？

■ R13.3 vector 类重载了哪些运算符？

■ R13.4 假设你定义了一个 Fraction 类，并想定义一个运算符来将一个分数提升到整数次幂。你能定义一个 ** 运算符，使得例如 f ** 2 表示 f 的平方吗？

■ R13.5 假设你定义了一个 Fraction 类，并想定义一个运算符来将一个分数提升到整数次幂。那么定义运算符 ^ 使得例如 f ^ 2 表示 f 的平方，有什么缺点？（提示：f ^ 2 ? 1 是什么？）

■ R13.6 假设你定义了一个 Fraction 类，其中包含一个相乘两个分数的 operator*、一个构造函数 Fraction(int) 以及一个类型转换 Fraction::operator double（参见专题 13.2）。那么 3 * f 的含义是什么？3 会转换为 Fraction 还是 f 会转换为 double？试一试。

■ R13.7 假设你想重载 * 运算符，使得 n * s 或 s * n 得到字符串变量 s 重复 n 次的结果。例如，如果 s 是 "hi"，那么 3 * s 就是 "hihihi"。你需要定义哪些函数？其中可以是成员函数吗？

■ R13.8 下面的类的赋值运算符犯了什么错误？

```
class String
{
public:
String(const char s[]);
String& operator=(const String& other);
private:
char* buffer;
int len;
};

String::String(const char s[])
{
len = strlen(s);
buffer = new char[len];
for (int i = 0; i < len; i++)
{
buffer[i] = s[i];
}
}

String& String::operator=(const String& other)
{
if (this != &other)
{
len = other.len;
buffer = new char[len];
for (int i = 0; i < len; i++)
{
buffer[i] = other.buffer[i];
```

