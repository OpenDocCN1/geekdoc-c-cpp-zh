

# 第17章：拷贝/移动构造函数 257

```cpp
int x;
// 通过调用 fn1() 创建 Student 对象。
// 将该对象传递给函数 fn2()。
// fn2() 返回一个整数，用于某些
// 愚的计算。
// 在期间，fn1() 返回的临时对象
// 保持有效。
x = 3 * fn2(fn1()) + 10;
// fn1() 返回的临时对象现在不再有效
// ...其他内容...
return 0;
```

这使得引用示例失效了，因为对象可能会消失，导致 `refs` 指向一个非对象。

# 永久地避免临时对象

你可能已经注意到，对象的拷贝既耗内存又耗时间。如果你不想对所有内容进行拷贝呢？最直接的解决方案是通过引用将对象传递给函数并从函数返回对象。这样做可以避免大多数的临时对象。

但如果你仍然不相信 C++ 并没有在背后巧妙地构造你一无所知的临时对象呢？或者如果你的类分配了你不希望被拷贝的唯一资源呢？你该怎么办？

你可以在拷贝构造函数中添加一条输出语句。执行程序时出现此消息会警告你刚刚发生了一次拷贝。

更聪明的方法是将拷贝构造函数声明为 `protected`，如下：

```cpp
class Student {
  protected:
    Student(Student&){
  public:
    // ...其他一切正常...
}
```

# 258 第三部分：类类论

C++ '11 标准还允许程序员删除拷贝构造函数：

```cpp
class Student
{
    Student(Student&s) = delete;

    // 其他一切正常;
};
```

通过将拷贝构造函数声明为 `protected` 或将其完全删除，都可以阻止任何外部函数（包括 C++ 语言本身）构造你的 `Student` 对象的拷贝。如果没有人调用拷贝构造函数，就不会生成任何拷贝。就如此（Voilà）。

# 移动构造函数

在某些情况下，C++ 可以创建一个对象的拷贝，该对象仅在单个语句期间有效。这些对象被称为临时对象，在表达式完成时就会被析构。对于即将被销毁的临时对象进行拷贝本身没有意义。

C++ '11 允许程序员创建一个名为移动构造函数的构造函数，它只是将资源从源位置移动到目的地，而不是进行不必要的拷贝。移动构造函数的格式为 `X:X(X&&)`。这是 `&move&` 的一种新用法。

考虑下面这个理想的示例。

C++ '11 包含了若干运行时优化以避免创建不必要的对象拷贝，而这个示例必须克服这些优化来演示移动构造函数。在第 22 章关于重载运算符的讨论中，你会看到更少争议的示例。

```cpp
// MoveCopy 展示了移动临时对象
//                     而不是创建拷贝的原理

#include <cstdio>
#include <cstdlib>
#include <iostream>
using namespace std;
class Person
{
    public:

Person(const char *pN)
{
    pName = new string(pN);
    cout << "Constructing " << *pName << endl;
}
Person(Person& p)
{
    cout << "Copying " << *p.pName << endl;
    pName = new string("Copy of ");
    *pName += *p.pName;
}
Person(Person&& p)
{
    cout << "Moving " << *p.pName << endl;
    pName = p.pName;
    p.pName = nullptr;
}
~Person()
{
    if (pName) {
        cout << "Destructing " << *pName << endl;
        delete pName;
    } else {
        cout << "Destructing null object" << endl;
    }
}
protected:
    string* pName;
};
Person fn2(Person p)
{
    cout << "Entering fn2" << endl;
    return p;
}
Person fn1(char* pName)
{
    cout << "Entering fn1" << endl;
    return fn2(new Person(pName));
}
int main(int argc, char* Args[]) {
    Person s(fn1("Scruffy"));
}
// 在程序终止前等待用户
// 让用户看到结果
```

```cpp
cout << "Press Enter to continue..." << endl;
cin.ignore(10, '\n');
cin.get();
return 0;
```

注意移动构造函数是如何将源对象的 `pName` 指针赋值给目标并将其置空的，这样析构函数在临时对象销毁时就不会释放内存。这比在堆上分配另一个字符串对象并拷贝 `p.pName` 内容要高效得多。

程序的输出如下：

```
Entering fn1
Constructing Scruffy
Copying Scruffy
Entering fn2
Moving Copy of Scruffy
Destructing null object
Press Enter to continue...
Destructing Scruffy
```

# 276

# 第18章

# 静态成员：它们有帮助吗？

+   本章内容
- 声明静态数据
- 定义和使用静态函数

默认情况下，数据成员是按对象分配的。例如，每个对象都有自己的名称。你也可以通过添加 `static` 关键字使成员被所有对象共享。这种成员被称为静态成员。本章将描述两种类型，从数据成员开始。

# 定义静态成员

静态成员是使用 `static` 存储类声明的成员，如下：

```cpp
class Student {
  public:
    Student(char *pName = "no name") : name(pName)
    {
      noOfStudents++;
    }
    ~Student() { noOfStudents--; }

    static int noOfStudents;
    string name;

  Student s1;
  Student s2;
}
```

# 为什么你需要静态成员

将此类信息存储在普通的全局变量中是非常容易的。例如，你可以使用一个简单的 `int` 变量来跟踪 `Student` 的数量。但这种解决方案的问题是，全局变量位于类外部。这就像把微波炉的调节器放在类外部一样。当然，我可以这样做，而且运行良好——但唯一的问题是我不希望我的猫弄坏电线，导致不得不把它从天花板上扯下来。

如果一个类要负责它自己的状态，那么全局变量必须带入类内部，就像调节器必须在微波炉内部一样。这就是静态成员背后的思想。

你可能发现静态成员被称为类成员；这是因为类中的所有对象共享它们。相比之下，普通成员被称为实例成员或成员对象，因为每个对象都接收这些成员的拷贝。

# 第 18 章：静态成员：柔能软剂吗？

“那么，”你问道，“如果 `noOfStudents` 的空间没有在 `Student` 类的任何对象中分配，那么它被分配在哪里了？”答案是，“没有被分配。”你必须为它专门分配空间，如下所示：

```cpp
int Student::noOfStudents = 0;
```

这种看起来有些奇特的语法为静态数据成员分配了空间，并将其初始化为 0。（在声明静态成员时你不需要初始化它；如果不初始化，C++ 将调用析构函数）。静态数据成员必须是全局的——静态变量不能是函数的局部变量。

当静态成员在类边界之外出现时，需要指明类名。

这种手动分配空间的操作有些令人困惑，但如果考虑到类定义被设计放在被多个源代码模块包含的文件中，C++ 必须知道在这些 `.cpp` 源文件的哪一个中为静态变量分配空间。对于非静态变量来说这不是问题，因为空间是在每个创建的对象中分配的。

# 引用静态数据成员

静态成员的访问规则与普通成员的访问规则相同。在类中，静态成员的引用方式与其他任何类成员一样。公共静态成员可以在类外部引用，而受良好保护的静态成员则不能。下面的代码片段使用了上一节中 `Student` 的声明，展示了两种类型的引用：

```cpp
void fn(Student& s1, Student& s2)
{
    // 引用公共静态成员
    cout << "No of students"
    << s1.noOfStudents // 从外部引用
    << endl;
}
```

在 `fn()` 中，`noOfStudents` 是通过对象 `s1` 引用的。但 `s1` 和 `s2` 共享同一个成员 `noOfStudents`。我怎么知道要选择 `s1` 呢？我为什么不使用 `s2` 呢？这没有任何区别。你可以使用该类的任何对象来引用静态成员。

事实上，你完全不需要对象。如果你愿意，可以在下面的代码中直接使用类名代替对象：

```cpp
// ...类定义与之前相同...
void fn(Student& s1, Student& s2)
{
    // 以下代码产生相同的结果
    cout << "Number of students "
    << Student::noOfStudents
    << endl;
}
```

当使用对象名访问静态成员时，C++ 只使用该对象的声明类。

这是一个细微的技术，但为了完全披露，需要说明：即使用于引用静态成员的对象是一个表达式，它也不会被求值。例如，考虑以下用例：

```cpp
class Student{
    public:
        static int noOfStudents;
        Student& nextStudent();
        //...其他诸类的内容...
};

void fn(Student& s)
{
    cout << s.nextStudent().noOfStudents << "\n";
}
```

成员函数 `nextStudent()` 并没有被实际调用。C++ 访问 `noOfStudents` 只需要类型，它可以在不费力求值表达式的情况下获取该类型。即使 `nextStudent()` 应该执行其他事情（比如洗你的鞋），这些事情也不会有任何一个被执行。虽然这个例子看起来很晦涩，但它确实会发生。这就是试图在一个表达式中塞入太多内容的代价。

# 静态数据成员的用途

静态数据成员有运行时间，让我在这里提几点。首先，你可以使用静态成员来记录对象的数量。例如在 `Student` 类中，计数初始化为 0，构造函数对其递增。

# 268 第三部分：类导论

## 这到底在关于什么？

非静态对象方法如何知道它所指的是哪个对象？换句话说，当我向 `Student` 对象请求它的名称时，`name()` 如何知道应该返回哪一个 `sName`？

当前对象的地址会作为隐含的第一个参数传递给每个非静态方法。当需要引用此对象时，C++ 将其命名为 `this`。`this` 是每个对象方法中的关键字，意为“当前名称”。下面的代码段说明了这一点：

```cpp
class SC {
public:
    void dyn(int a); // 类似于 SC::dyn(SC *this, int a)
    static void stat(int a); // 类似于 SC::stat(int a)
};

void fn(SC& s) {
    s.dyn(10); //- 转换为-> SC::dyn(&s, 10)
    s.stat(10); //- 转换为-> SC::stat(10)
}
```

也就是说，函数 `dyn()` 的解释方式几乎就像它声明为 `void SC::dyn(*this, int a)` 一样。对 `dyn()` 的调用被编译器转换为所示，并将 `s` 的地址作为第一个参数传递。（你实际上不能直接用 `this` 写调用，但这就是编译器正在做的。）

`SC::dyn()` 内部对其他非静态成员的引用会自动使用该参数作为当前对象的指针。当调用 `SC::stat()` 时，没有传递对象地址。因此，在引用非静态函数时，它没有指针可以使用，这就是为什么我说静态成员函数不与任何当前对象关联。

你可以在第 13 章中链表程序的面向对象版本中显式地看到这一点；该程序被称为 `LinkedListData`。整个程序可以在 www.dummies.com/extras/cplusplus/ 随材料获取；`NameDataSet` 类显示在此处：

```cpp
// NameDataSet - 存储人的姓名（这些对象
// 可以轻松地存储任何其他信息
//（根据需要））。
class NameDataSet {
public:
    NameDataSet(string& refName)
    : sName(refName), pNext(nullptr) { }
```

# 第 18 章：静态成员：它们可以吗？

```cpp
// 将自身添加到列表开头
void add() {
    this->pNext = pHead;
    pHead = this;
}

// 访问方法
static NameDataSet* first() { return pHead; }
static NameDataSet* next() { return pNext; }
const string& name() { return sName; }
```

