
在之前的 `Student` 类定义中，我们再次看到了用于构成该类的各种熟悉组件。此外，注意到我们使用 `override` 关键字重写并重定义了三个虚函数——析构函数、`Print()` 和 `IsA()`。这些首选定义本质上替换或覆盖了基类中为这些操作指定的默认方法。

但注意，我们选择不重定义 `void Person::Greeting(const string &)`，该函数在 `Person` 类中作为虚函数引入的。如果我们发现继承的定义对于 `Student` 类的实例是可以接受的，那么直接继承即可。

此外，注意 `Print()` 上带有额外的 `final` 修饰符。该关键字表示 `Print()` 不可以在来自 `Student` 的派生类中被重写；在 `Student` 级别重写的方法将是最终实现。

回想起 `override` 与析构函数配对时的含义是独特的，因为它并不意味着派生类析构函数替换了基类析构函数。相反，这意味着派生类（虚）析构函数是派生类实例启动的析构链的正确起点（无论它们如何存储）。虚派生类析构函数仅仅是完整析构序列的入口。

还要记住，`Student` 的派生类不需要重写在 `Person` 中定义的虚函数。如果 `Student` 认为继承的定义可以接受，它会被自动继承。虚函数允许派生类在需要时重新定义操作。接下来，让我们检查非内联的 `Student` 类函数：

```cpp
Student::Student(const string &fn, const string &ln, char mi,
    const string &t, float avg, const string &course, const string &id)
    : firstName(fn), lastName(ln), middleInitial(mi), title(t),
    gpa(avg), currentCourse(course), studentId(id)
{
    // 为指针数据成员动态分配内存
// 我们选择利用默认的拷贝构造函数。
// 如果我们想对其进行原型化/定义，方法如下：
// Student::Student(const Student &p):
//
    firstName(p.firstName), lastName(p.lastName),
    middleInitial(p.middleInitial), title(p.title),
    gpa(p.gpa), currentCourse(p.currentCourse), studentId(p.studentId)
{
    // 在此处深拷贝任何指针数据成员
}
Student::Student(const Student &s)
    : firstName(s.firstName), lastName(s.lastName),
    middleInitial(s.middleInitial), title(s.title),
    gpa(s.gpa), currentCourse(s.currentCourse), studentId(s.studentId)
{
    // 深拷贝任何指针数据成员
}
Student::~Student()
{
    // 释放任何动态分配数据成员的内存。
cout << "Student destructor <<" << firstName << " "
    << lastName << " >>" << endl;
}
void Student::EarnPhD()
{
  ModifyTitle("Dr.");
}
void Student::IsA()
{
  cout << "Student" << endl;
}
```

```cpp
int main()
{
    Person *people[MAX] = { }; // 初始化为空指针
    people[0] = new Person("Juliet", "Martinez", 'M',
Ms.");
    people[1] = new Student("Hana", "Sato", 'U', "Dr.",
3.8, "C++", "178PSU");
    people[2] = new Student("Sara", "Kato", 'B", "Dr.",
3.9, "C++", "272PSU");
    people[3] = new Person("Giselle", "LeBrun", 'R',
"Miss");
    people[4] = new Person("Linus", "Van Pelt", 'S',
"Mr.");
    // 我们很快将看到一种更安全、更现代的循环方式，
    // 使用范围循环（从第 8 章开始）。
    // 与此同时，让我们观察访问每个
    // 元素的机制。
    for (int i = 0; i < MAX; i++)
    {
        people[i]->IsA()
        cout << " \n        people[i]->Print();
    }
    for (int i = 0; i < MAX; i++)
        delete people[i]; // 触发虚析构序列
    return 0;
}
```

在这里，在 `main()` 中，我们声明了一个指向 `Person` 的指针数组。这样做，使我们能够以这种方式收集 `Person` 和 `Student` 实例。当然，这些

对于以通用方式存储的实例，我们可能应用的操作只有基类中找到的那些。

接下来，通过通用指针分配几个 `Person` 和 `Student` 实例。当一个 `Student` 以这种方式存储时，会执行到基类类型的向上转换（但实例本身不会被改变）。回想我们在第6章“实现层次结构”中查看过派生实例的内存布局，我们注意到 `Student` 实例包含了 `Person` 的内存布局，随后是 `Student` 所需的额外内存。这种向上转换仅指向这块内存的起始点。

现在，我们通过循环将 `Person` 类中的操作应用于所有多态实例。这意味着这些操作实际上是多态的。也就是说，虚函数允许通过运行时绑定调用方法的特定实现，以匹配实际对象（无论该对象是否存储在通用指针中）。

最后，使用通用指针循环删除已分配的 `Person` 和 `Student` 实例。由于我们知道 `delete()` 会调用析构函数，明智地将析构函数声明为虚函数，以便通过动态绑定在析构序列中选择合适的析构函数。

当我们查看上述程序的输出时，可以看到每个对象的特定方法都为每个虚函数被相应调用，包括析构序列。派生类对象会同时调用并执行派生类和基类的析构函数。以下是完整程序的输出：

```
Person destructor <Juliet Martinez>
Student destructor <Hana Sato> with id: 178 GPA: C++
Student destructor <Sara Kato> with id: 272 GPA: C++
Person destructor <Giselle LeBrun>
Person destructor <Linus Pelt>
```

既然我们已经利用了多态的概念和虚函数的机制，让我们来看与虚函数相关的较不常见的情况：函数隐藏。

## 函数隐藏 (Function hiding)

函数隐藏并不是 C++ 中一个经常使用的特性。事实上，它通常是无意中使用的！让我们从回顾关于继承成员函数的一个关键点开始。当基类指定某项操作时，其目的是为所有派生类方法提供用法和重定义（在虚函数的情况下）。

有时，派生类会更改本用于重定义基类指定的操作的方法签名（让我们想想虚函数）。在这种情况下，新函数由于其签名与其所在类中指定的操作不同，将不会被视为对继承操作的虚重定义。事实上，它会隐藏在类中指定的具有相同名的虚函数的继承方法。

当程序编译时，每个函数的签名都会与类定义进行对比以确保用法正确。通常，当在看似匹配实例类型的类中未找到成员函数时，将以向上方式遍历层次结构，直到找到匹配项或耗尽层次结构。让我们仔细查看一下编译器考虑的内容：

- 当找到一个与所寻函数同名的函数时，将检查其签名以查看它是否与函数调用完全匹配，或者可以应用类型转换。当找到函数但无法应用类型转换时，结束正常的遍历序列。
- 隐藏虚函数的函数通常会停止这种向上搜索序列，从而隐藏了原本可能被调用的虚函数。回想一下在编译时，我们只是在检查语法（而不是决定调用哪个版本的虚函数）。但如果我们找不到匹配项，就会标记错误。
- 函数隐藏实际上被认为是有用的，并且是语言设计意图的。如果类设计者提供了一个具有特定签名和接口的特定函数，那么该函数应该用于该类型的实例。在这种特定情况下，不应使用层次结构中上述隐藏或意外之外的函数。

考虑对我们之前的完整程序示例进行以下修改，首先说明函数隐藏，然后为管理函数隐藏提供一个更灵活的解决方案：

- 回想 `Person` 类引入了没有参数的 `virtual void Print()`。想象 `Student` 并没有重写相同签名的 `Print()`，而是将签名改为 `virtual void Print(const char *)`：

```cpp
class Person // base class
{
    // 数据成员
    public: // 成员函数等
    virtual void Print() const;
};
class Student: public Person
{
    // 数据成员
    public: // 成员函数等
    // 新引入的虚函数
    // 不是 Person::Print() 的重定义
    virtual void Print(const string &) const;
};
```

注意，`Print()` 的签名已从基类变更为派生类。派生类函数并没有重定义其基类的 `virtual void Print()`。它是一个新函数，将隐藏 `Person::Print()` 的存在。这实际上是设计意图的，因为你可能忘记了基类提供了这样的操作，如果你打算调用 `Print(const string &)` 却调用了 `Print()`，那么向上查找可能会在你的应用程序中产生意外的结果。通过添加这个新函数，派生类设计者避免了规定此接口的繁琐代码。

基类（意味着动态绑定），使用作用域解析操作符可以将此调用还原为静态绑定的函数调用。

假设我们想为一个派生类添加一个新接口，该接口的函数在其他情况下会隐藏基类函数。在了解函数隐藏机制后，最理想的情况下我们应该怎么做？我们可以简单地在派生类中使用一个新方法来重写基类中的虚函数，然后通过函数重载来添加额外的接口。是的，我们现在既在进行重写（overriding），又在重载（overloading）。也就是说，我们正在重写基类函数，并重载派生类中被重写的那个函数。

让我们来看看现在拥有了什么：

- 这里有一个更灵活的接口，可以在添加新成员函数的同时，保留原本会被隐藏的现有接口：

```cpp
class Person    // 基类
{
    // 数据成员
    public:    // 成员函数等
    virtual void Print() const;
};
class Student: public Person
{
    // 数据成员
    public:    // 成员函数等
    // 重写基类方法，以确保
    // 接口不会被下方的重载函数隐藏
void Print() const override;
// 添加额外的接口
// （它是重载的）
// 注意：此额外的 Print() 是虚函数
// 从该层次结构的此点开始开始有效
virtual void Print(const string &) const;
};
int main()
{
    Student sl("Zack", "Doone", 'A', "Dr.", 3.9,
    "C+", "769UMD");
    sl.Print(); // 此版本不再被隐藏。
    sl.Print("I got an A!"); // 同样有效
    sl.Person::Print(); // 这不再是必须的
}
```

在前面的代码段中，`Student` 类通过 `Student::Print()` 重写了 `Person::Print()`，并通过 `Student::Print(const string &)` 重载了 `Student::Print()` 以封装额外的接口。现在，对于存储在 `Student` 变量中的 `Student` 对象，两个接口都是可用的——基类接口不再被隐藏。当然，通过 `Person` 指针引用的 `Student` 对象只有 `Person::Print()` 接口，这是预料之中的。

总的来说，函数隐藏并不经常发生，但一旦发生，它通常是一个令人遗憾的惊喜。现在你理解了可能会发生什么以及为什么，这有助于你成为一名更优秀的程序员。

既然我们已经查看了所有关于虚函数的用法，现在让我们深入底层，看看为什么虚函数能够支持将特定方法到操作的动态绑定。为了彻底理解运行时绑定，我们需要查看 v 表（虚函数表）。让我们继续吧！

## 理解动态绑定

现在我们已经看到了如何通过虚函数实现多态，从而允许操作向特定实现或方法的动态绑定，现在让我们理解为什么虚函数允许运行时绑定。

非虚函数在编译时进行静态绑定。也就是说，所涉及函数的地址是在编译时根据对当前对象的假设类型确定的。例如，如果实例化了一个类型为 `Student` 类的对象，并且找到了该函数，则函数调用将从 `Student` 类开始验证其原型；如果未找到，则将向上遍历层次结构到每个基类（如 `Person`），以寻找匹配的原型。找到后，就会补丁上正确的函数调用。这就是静态绑定的工作方式。

然而，虚函数是 C++ 中的一种函数类型，它在运行时采用动态绑定。在编译时，任何虚函数调用仅仅被替换为一个查找机制，将绑定推迟到运行时。当然，每个编译器厂商在自动处理虚函数的实现上可能有所不同。但存在一种广泛使用的实现方法，涉及虚函数指针、虚函数表以及用于每个包含虚函数的对象的类型的虚函数表项。

让我们继续研究 C++ 中通常是如何实现动态绑定的。

### 理解方法到操作的运行时绑定

我们知道虚函数允许将操作（在基类中指定）向特定实现或方法（通常在派生类中指定）的动态绑定。这是如何工作的？

当基类指定一个或多个新的虚函数（而不仅仅是祖先虚函数的重新定义）时，在该类型的内存下方创建一个**虚函数指针 (vptr)**。这是在运行时创建实例内存（在栈上）时发生的。当实例构造时，vptr 将初始化为指向该类的 v 表。给定类型的 v 表由一组函数指针（例如指针数组）组成，用于组织和初始化动态绑定函数。函数指针的特定顺序与虚函数引入的顺序对应，特定的函数指针将初始化为该特定类类型的首选版本。也就是说，函数指针可能指向在其所属类级别指定的重写方法。

然后，当实例化给定类型的对象时，该对象内部的 vptr（每个新引入——而非重新定义的虚函数层级有一个）将设置为指向该实例相应的 v 表项。

通过代码和内存图查看这些细节将非常有帮助。让我们深入底层查看代码运行情况！

#### 详细解释 v 表

为了详细说明内存模型并查看运行时设置的底层 C++ 机制，让我们考虑本节中带有基类 `Person` 和派生类 `Student` 的详细完整程序示例。作为提醒，我们将显示程序的关键元素：

- `Person` 和 `Student` 类的简写定义（为了节省空间，省略数据成员和大多数成员函数定义）：

```cpp
class Person
{
    private:   // 数据成员将如之前
    protected: // 假设所有成员函数如之前
    public:    // 但我们在这里只显示虚函数
        virtual ~Person();      // 引入了 4 个虚函数
        virtual void Print() const;   // 在 Person 类中
        virtual void IsA() const;
        virtual void Greeting(const string &) const;
}
```

```cpp
class Student: public Person
{
    private:    // 数据成员与之前相同
    public:     // 假设所有成员函数与之前相同，
               // 但在这里只显示虚函数
               ~Student() override; // 重写了 3 个虚函数
               void Print() override;
               void IsA() const override;
};
```

`Person` 和 `Student` 类的定义符合预期。假设数据成员和成员函数已完整程序示例中显示。为了简洁起见，我们只包含了在每个层级引入或重新定义的虚函数。

- 以简写形式回顾 `main()` 函数中的关键元素（减少为三个实例）：

`constexpr int MAX = 3;`

```cpp
int main()
{
    Person *people[MAX] = { }; // 初始化为空指针
    people[0] = new Person("Joy", "Lin", 'M', "Ms.");
    people[1] = new Student("Renee", "Alexander", 'Z'Dr.", 3.95, "C++", "21-MIT");
    people[2] = new Student("Gabby", "Doone", 'A'Ms.", 3.95, "C++", "18-GWU");
}
```

// 在第 8 章中，我们将升级为范围循环
