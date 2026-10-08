
在之前的类定义中，我们注意到`Person`包含了默认构造函数、拷贝构造函数、重载赋值运算符和虚析构函数。在这里，我们采用了正的标准形式作为适用于未来可能作为公共基类的类的模式。

另请注意，我们添加了移动拷贝构造函数和移动赋值运算符的声明，以额外支持扩展的规范类形式。

移动拷贝构造函数`Person(Person&&);`和移动赋值运算符`Person&=(Person&&);`包含`Person &&`类型的参数。这些是右值引用的示例。可以作为左值引用的参数（例如`Person&`）将绑定到原始拷贝构造函数和重载赋值运算符，而右值引用参数将绑定到相应的移动方法。

现在让我们来看有助于扩展规范类形式的方法定义——`Person`的移动拷贝构造函数和移动赋值运算符：

```cpp
// 移动拷贝构造函数
Person::Person(Person&& p) : firstName(p.firstName),
name(p.lastName), middleInitial(p.middleInitial),
title(p.title) // 目标指针接管了源指针的内存
{
    // 接管源对象的动态分配的内存
    // 或使用简单赋值（非指针数据成员）
    // 在成员初始化列表中拷贝源对象的成员
    // 然后将源对象指向该内存的指针置空
    // 清空源对象的字符串成员，或置为空字符
    p.firstName.clear(); // 将源对象置为空字符串
    p.lastName.clear();
    p.middleInitial = '\0'; // 空字符表示不再使用
    p.title = nullptr; // 源指针为空；不共享内存
}
```

```cpp
// 移动重载赋值运算符
Person& Person::operator=(Person&& p)
{
    if (this != &p) // 检查自赋值
    {
        // 删除目标对象的指针数据成员
        delete [] title;
        // 对于指针成员：接管源对象的动态分配内存
        // 并将源对象指向该内存的指针置空
        // 对于非指针成员，简单赋值即可
        // 然后清空源数据成员
        firstName = p.firstName; // 赋值
        p.firstName.clear(); // 清空源数据成员
        lastName = p.lastName;
        p.lastName.clear();
        middleInitial = p.middleInitial; // 简单赋值
        middleInitial = '\0'; // 空字符显示不再使用
        title = p.title; // 指针赋值以接管内存
        p.title = nullptr; // 源指针置空
        return *this; // 允许级联赋值
    }
}
```

注意，在上述针对指针数据成员的移动拷贝构造中，我们在成员初始化列表中通过简单的指针赋值来接管源对象的动态分配的内存（而不是在深拷贝构造函数中那样进行内存分配）。随后我们在构造函数体中将源对象的指针数据成员设置为`nullptr`。对于非指针数据成员，我们简单地将值从源对象拷贝到目标对象，并在源对象中放置零空值（例如`p.middleInitial`的`'\0'`或对`p.firstName`使用`clear()`）以指示其后续不再使用。

在移动赋值运算符中，我们检查自赋值，然后采用相同的方案通过简单的指针赋值将动态分配的内存从源对象移动到目标对象。我们同样拷贝简单数据成员，当然，还将源对象的数据值替换为空指针(`nullptr`)或零值以指示后续不再使用。`*this`的返回值允许级联赋值。

现在，让我们看看派生类`Student`如何在利用正统和扩展规范类形式的同时，利用其基类组件来帮助实现选定的惯用方法：

```cpp
class Student: public Person {
private:
    float gpa = 0.0; // 类内初始化
    string currentCourse;
    // 一个指针数据成员用于演示深拷贝和赋值
    const char *studentid = nullptr; // 类内初始化
    static int numStudents;
public:
    Student(); // 默认构造函数
    // 假设存在常规类构造函数
    Student(const Student&); // 拷贝构造函数
    Student(Student&&) // 移动拷贝构造函数
    ~Student() override; // 虚析构函数
    // 假设存在常规访问函数
    // 以及虚重写和额外方法
    Student& operator=(const Student&); // 赋值运算符
    Student& operator=(Student&&); // 移动赋值运算符
}
```

### 拷贝构造函数

```cpp
Student::Student(const Student& s):Person(s),
    gpa(s.gpa),currentCourse(s.currentCourse)
// 使用成员初始化列表初始化基类子对象
// 同时使用成员列表设置最派生的数据成员
// 对 Student 指针数据成员执行深拷贝
    // 使用临时 - const 数据无法直接修改
    char *temp = new char[strlen(s.studentId) + 1];
    strcpy(temp, s.studentId);
    studentId = temp;
numStudents++;
}
```

### 重载赋值运算符

```cpp
Student &Student::operator=(const Student &s)
{
    if (this != &s) // 检查自赋值
        // 调用基类赋值运算符
        Person::operator=(s);
        // 删除“this”现有的 Student 指针数据成员
        delete []studentId;
        // 对于指针成员，重新分配正确大小并从源拷贝
        // 对于非指针成员，简单赋值
        gpa = s.gpa; // 简单赋值
        currentCourse = s.currentCourse;
        // 数据是 const 的，不能直接修改
        char *temp = new char[strlen(s.studentId) + 1];
        strcpy(temp, s.studentId);
        studentId = temp;
    }
    return *this;
}
```

在前面的类定义中，我们再次看到`Student`包含默认构造函数、拷贝构造函数、重载赋值运算符和虚析构函数。然而，在`Student`拷贝构造函数中，我们通过成员初始化列表指定基类的类的。同样，在重载赋值运算符中，我们在检查自赋值后调用基类赋值运算符来帮助完成任务。

让我们看看有助于`Student`扩展形式的方法定义——移动拷贝构造函数和移动赋值运算符：

```cpp
// 移动拷贝构造函数
Student::Student(Student&& s):Person(s), gpa(s.gpa),
currentCourse(s.currentCourse),
studentId(s.studentId) // 接管源对象的资源
{
    // 首先，使用初始化列表指定基类移动
    //构造函数以初始化子对象。然后
    // 接管对象的动态分配内存。
    // 使用简单赋值（非指针数据成员）
    // 在成员初始化列表中拷贝源对象的成员。
    // 然后将源对象指向该内存的指针置空。
    // 清空源对象的字符串。在方法体内
    // 然后置空源成员。
    gpa = 0.0; // 置空源成员
    currentCourse.clear(); // 清空源成员
    studentId = nullptr; // 置空指针数据成员
    numStudents++; // 增加是一个设计选择
    // 的；源对象为空但仍然存在
}
```

```cpp
// 移动赋值运算符
Student& Student::operator=(Student&& s)
{
    // 确保我们没有将对象赋值给自己
    if (this != &s)
    {
        Person::operator=(move(s)); // 调用基类移动赋值
        delete []studentId; // 删除现有指针成员
        // 对于指针数据成员，接管源对象的内存
        // 对于非指针成员，简单赋值即可
        gpa = s.gpa; // 源到目标数据成员赋值
        gpa = 0.0; // 置空源数据成员
        currentCourse = s.currentCourse; // 字符串赋值
        currentCourse.clear(); // 清空源成员
        studentId = s.studentId; // 指针赋值
        s.studentId = nullptr; // 源指针数据成员置空
    }
    return *this; // 允许级联赋值
}
```

初始化列表。`Student`移动构造函数的其余部分与在`Person`基类中找到的相似。

同样，注意到`Student`移动赋值运算符中，对基类移动运算符`operator=`的调用为`Person::operator=(move(s))`。该方法的其余部分与基类中的实现相似。

一个经验法则是，大多数非平凡类应该至少利用**正规的规范类形式**（orthodox canonical class form）。当然，也有例外。例如，一个仅作为`protected`或`private`基类的类不需要虚析析构函数，因为派生类实例无法越过非公共的继承边界。同样，如果我们有充分理由不想要拷贝或禁止赋值，我们可以在这两个方法任一个扩展签名中使用`= delete`规范来禁止拷贝或赋值。

尽管如此，正规类形式将为采用这种惯例的类增加健壮性。程序员会非常看重利用这种惯例的类在初始化、赋值和参数传递实现上保持的一致性。

让我们继续查看一个与正规类形式互补的概念：**健壮性**（robustness）。

## 确保类是健壮的

C++的一个重要特性是能够构建广泛复用的类库。无论我们是希望实现这一目标，还是仅仅想为自己的组织提供可靠的代码，我们的代码必须是健壮的。一个健壮的类应该是经过良好测试的、遵循规范类形式（`protected`和`private`基类需要虚析构函数除外）、并且是可移植的（或包含在特定平台的库中）。任何作为复用候选或在任何专业领域使用的类都必须是健壮的。

健壮的类必须确保给定类的所有实例都已完全构造。完全构造的对象是指所有数据成员都经过适当初始的对象。给定类的所有构造函数（包括拷贝构造函数）必须经过验证以初始化所有数据成员。加载到数据成员的值应该检查其范围适用性。记住，未初始的数据成员是一个潜在的灾难！如果给构造函数没有正常完成，或者数据成员的初始值不合适，应当采取措施。

完全构造的对象可以使用多种技术进行验证。一种原始（且不建议）的技术是在每个类中嵌入一个状态数据成员（或派生/嵌入一个状态祖先类/成员）。在成员初始化列表中将状态成员设为0，并在构造函数的最后一行设为1。在实例化后探测此值。这种方法的巨大缺陷是，用户肯定会忘记探测完全构造的成功标志。

上述简单方案的替代方案是针对所有简单数据类型利用**类内初始化**，在每个备选构造函数的成员初始化列表中将这些成员重置为所需值。实例化后，可以再次探测值以确定备选构造函数是否成功完成。这离理想实现仍然很远。

一种更好的技术是利用**异常处理**。在每个构造函数嵌入异常处理是理想的。如果数据成员没有在合适的范围内初始化，首先尝试重新输入它们的值，或者打开一个备用数据库进行输入。作为最后手段，你可以抛出一个异常来报告未完全构造的对象。我们将在本章后面更详细地检查测试相关的异常处理。

同时，让我们继续一种严谨测试我们的类和组件的技术——创建测试类的**驱动程序**（drivers）。

## 创建测试类的驱动程序

在第5章“深入探索类”中，我们简要提到过将代码分为源文件和头文件。让我们简单回顾一下。通常，头文件将用类命名（例如`Student.h`），并包含类定义以及任何内联成员函数定义。通过将内联函数放在头文件中，如果它们的实现发生变化，它们将正确重新展开（因为头文件随后会被包含在每个源文件中，从而与该源文件产生依赖）。

每个类的方法实现将放在对应的源文件中（例如`Student.cpp`），该文件将包含其所依据的头文件（即`#include "Student.h"`）。注意，双引号意味着该头文件在我们当前的工作目录中；我们也可以指定路径来查找头文件。相比之下，C++库使用的角括号告诉预处理器在编译器预定义的目录中查找。此外，请注意每个派生类的头文件都将包含其基类的头文件（以便它能看到成员函数原型）。

注意，任何静态数据成员或方法定义将出现在它们对应的源代码文件中（这样每个应用程序将只存在一个定义）。

考虑到这种头文件和源文件结构，我们现在可以创建一个驱动程序来测试每个单独的类或每组紧密相关的类（例如通过关联或聚合相关的类）。通过继承相关的类可以在它们各自的、独立的驱动程序文件中进行测试。每个驱动程序文件可以命名为反映正在测试的类，例如`StudentDriver.cpp`。驱动程序文件将包含所测试类的相关头文件。当然，所涉及类的源文件将在编译过程的一部分被编译并链接到驱动程序文件中。

驱动程序可以仅包含一个`main()`函数作为测试平台，用于实例化目标类并作为测试每个成员函数的作用域。驱动程序将对默认实例化、典型实例化、拷贝构造、对象间的赋值以及类中的每个额外方法进行测试。如果存在虚析构函数，我们应该实例化派生类实例（在派生类中），将这些实例向上转型并使用基指针存储，然后调用虚函数以验证发生了正确的行为。在虚析构函数的情况下，我们可以通过删除动态分配的实例（或等待栈实例离开作用域）并单步执行调试器来追踪哪个析构函数是入口。

我们还可以测试对象是否完全构造；我们稍后会详细讨论这个话题。

假设我们使用常用的`Person`和`Student`类层次结构，这里有一个简单的驱动程序（包含`main`函数）来测试`Student`类。驱动可以在我们的GitHub仓库找到。要制作一个完整的程序，你还需要编译并链接同一目录下的`Student.cpp`和`Person.cpp`文件。这里是驱动程序的GitHub仓库URL：

https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/Chapter15/Chp15-Ex2.cpp

```cpp
#include "Person.h" // 类头文件
#include "Student.h"
using std::cout; // 优于 using namespace std;
using std::endl;
constexpr int MAX = 3;
int main() // 测试 Student 类的驱动，位于上方
{
    // 为了章节示例的一致性
    // 测试所有实例化，甚至是拷贝构造
    Student s0;
    // 备选构造函数
    Student s1("Jo", "Li", 'H', "Ms.", 3.7, "C++");
    cout<<"UD1234";
    Student s2("Sam", "Lo", 'A', "Mr.", 3.5, "C++");
    cout<<"UD2245";
    // 这些初始化隐式调用了拷贝构造函数。
    Student s3(s1);
    Student s4 = s2; // 这也是初始化
    // 测试赋值运算符
    Student s5("Ren", "Ze", 'A', "Dr.", 3.8, "C++");
    cout<<"BU5563";
}
```

```cpp
Student s6;
s6 = s5; // 这是一个赋值，而不是初始化
// 测试每个公共方法。这里显示了一个示例
sl.Print(); // 确保测试每个方法！

// 将派生实例泛化为基类类型
// 多态操作是否符合预期？
Person *people[MAX] = { }; // 初始化为空指针
// 用于比较的基类实例
people[0] = new Person("Juliet", "Martinez", 'M', "Ms.");

// 派生实例，通过基类指针泛化。
people[1] = new Student("Zack", "Moon", 'R', "Dr.",
3.8, "C++", "UMD1234");
people[2] = new Student("Gabby", "Doone", 'A', "Dr.",
3.9, "C++", "GWU4321");
```

```cpp
for (auto *item : people) // 遍历所有元素
    if (item->IsA()) {
        cout << " ";
        item->Print();
    }
    // 测试析构顺序（动态分配的实例）
    for (auto *item : people) // 遍历所有元素
```

