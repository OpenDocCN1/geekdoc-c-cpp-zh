

```cpp
    25
    26    // function to get the course name
    27    string getCourseName() const
    28    {
    29       return courseName; // return object's courseName
    30    } // end function getCourseName
    31
    32    // display a welcome message to the GradeBook user
    33    void displayMessage() const
    34    {
    35       // call getCourseName to get the courseName
    36       cout << "Welcome to the grade book for\n" << getCourseName()
    37          << "!" << endl;
    38    } // end function displayMessage
    39 private:
    40    string courseName; // course name for this GradeBook
    41 }; // end class GradeBook
    42
    43 // function main begins program execution
    44 int main()
    45 {
    46    // create two GradeBook objects
    47    GradeBook gradeBook1( "CS101 Introduction to C++ Programming" );
    48    GradeBook gradeBook2( "CS102 Data Structures in C++" );
    49
    50    // display initial value of courseName for each GradeBook
    51    cout << "gradeBook1 created for course: " << gradeBook1.getCourseName()
    52       << "\ngradeBook2 created for course: " << gradeBook2.getCourseName()
    53       << endl;
    54 } // end main
```

```text
gradeBook1 created for course: CS101 Introduction to C++ Programming
gradeBook2 created for course: CS102 Data Structures in C++
```

**图 16.7** | 实例化 GradeBook 类的多个对象，并使用 GradeBook 构造函数在创建每个 GradeBook 对象时指定课程名。（共 2 部分，第 2 部分。）

## 定义构造函数

图 16.7 的第 14～18 行定义了类 GradeBook 的构造函数。该构造函数与其类 GradeBook 具有*相同*的名称。构造函数在其参数列表中指定执行任务所需的数据。创建新对象时，需将这些数据放在对象名后的圆括号中（如第 47～48 行所示）。第 14 行表明类 GradeBook 的构造函数有一个名为 name 的 string 参数。我们将此构造函数声明为 explicit，因为它只接受*一个*参数——这一点很重要，原因很微妙，你将在第 18.13 节学到。目前，只需将所有单参数构造函数都声明为 explicit。第 14 行没有指定返回类型，因为构造函数*不能*返回值（甚至不能返回 void）。此外，构造函数不能声明为 const（因为初始化对象会修改该对象）。

该构造函数使用成员初始化列表（第 15 行）将 courseName 数据成员初始化为构造函数参数 name 的值。*成员初始化器*出现在构造函数的参数列表与开始构造函数体的左花括号之间。成员初始化列表与参数列表之间用冒号（`:`）分隔。成员初始化器由数据成员的*变量名*后跟包含该成员*初始值*的圆括号组成。在此示例中，courseName 用参数 name 的值初始化。如果一个类包含多个数据成员，则每个数据成员的初始化器之间用逗号分隔。成员初始化列表在构造函数体执行*之前*执行。你可以在构造函数体中执行初始化，但稍后你会了解到，使用成员初始化器更高效，而且某些类型的数据成员必须用这种方式初始化。

注意，构造函数（第 14 行）和 setCourseName 函数（第 21 行）都使用了一个名为 name 的参数。你可以在*不同*函数中使用*相同*的参数名，因为这些参数是各函数的*局部*变量——它们*不会*相互干扰。

## 测试 GradeBook 类

图 16.7 的第 44～54 行定义了 main 函数，该函数测试类 GradeBook，并演示使用构造函数初始化 GradeBook 对象。第 47 行创建并初始化 GradeBook 对象 gradeBook1。执行该行时，会以实参 "CS101 Introduction to C++ Programming" 调用 GradeBook 构造函数（第 14～18 行），以初始化 gradeBook1 的课程名。第 48 行对 GradeBook 对象 gradeBook2 重复此过程，这次传入实参 "CS102 Data Structures in C++" 来初始化 gradeBook2 的课程名。第 51～52 行使用各对象的 getCourseName 成员函数获取课程名，并表明这些课程名确实在创建对象时已被初始化。输出确认每个 GradeBook 对象都维护自己的数据成员 courseName。

## 为类提供默认构造函数的方法

任何不接受*任何参数*的构造函数都称为默认构造函数。类可以通过以下几种方式之一获得默认构造函数：

1. 编译器会在每个*没有*任何用户定义构造函数的类中*隐式*创建默认构造函数。该默认构造函数*不会初始化*类的数据成员，但*会*为每个作为另一个类对象的数据成员调用默认构造函数。未初始化的变量包含未定义的（“垃圾”）值。

2. 你*显式*定义一个不接受参数的构造函数。这样的默认构造函数会为每个作为另一个类对象的数据成员调用默认构造函数，并执行你指定的额外初始化。

3. *如果你定义了任何带参数的构造函数，C++ 将不会为该类隐式创建默认构造函数。* 稍后我们会展示，C++11 允许你强制编译器创建默认构造函数，即使你已经定义了非默认构造函数。

对于图 16.1、图 16.3 和图 16.5 中类 GradeBook 的每个版本，编译器都*隐式*定义了默认构造函数。

> **错误预防提示 16.2**
>
> *除非类的数据成员不需要任何初始化（几乎从不如此），否则应提供构造函数，以确保在创建类的每个新对象时，类的数据成员都用有意义的值初始化。*

![](img/d0d3b7423c2d9e5650be79209ea1885d_637_0.png)

## 软件工程观察 16.2

数据成员可以在构造函数中初始化，也可以在其值在对象创建后稍后设置。然而，良好的软件工程实践是确保在客户端代码调用对象的成员函数之前，对象已完全初始化。你不应依赖客户端代码来确保对象得到正确初始化。

## 将构造函数添加到 GradeBook 类的 UML 类图

图 16.8 的 UML 类图对图 16.7 的 GradeBook 类建模，该类有一个构造函数，其 name 参数的类型为 string（在 UML 中由类型 String 表示）。与操作类似，UML 在类图的第三个隔间中为构造函数建模。为了将构造函数与类的操作区分开，UML 在构造函数名称前加上由法文引号（« 和 »）括起的单词 "constructor"。按照惯例，在第三个隔间中，应将类的构造函数列在其他操作之前。

![](img/d0d3b7423c2d9e5650be79209ea1885d_638_0.png)

图 16.8 | UML 类图，表明类 GradeBook 有一个构造函数，其 name 参数为 UML 类型 String。

## 16.6 将类放入单独文件以便复用

创建类定义的好处之一是，如果打包得当，你的类可以被其他程序员复用。例如，你可以在任何 C++ 程序中复用 C++ 标准库类型 string，方法是包含头文件 `<string>`（并且，正如你将会看到的，还能链接到该库的目标代码）。

希望使用我们的 GradeBook 类的程序员不能简单地将图 16.7 中的文件包含到另一个程序中。如你所知，函数 main 开始执行每个程序，并且每个程序必须恰好有一个 main 函数。如果其他程序员包含图 16.7 中的代码，他们就会得到额外的“包袱”——我们的 main 函数——然后他们的程序将有两个 main 函数。尝试编译包含两个 main 函数的程序会产生错误。因此，将 main 与类定义放在同一个文件中会阻止该类被其他程序复用。在本节中，我们演示如何通过将类 GradeBook 分离到另一个文件（与 main 函数分开）来使其可复用。

### 头文件

本章前面的每个示例都由单个 .cpp 文件（也称为源代码文件）组成，该文件包含 GradeBook 类定义和一个 main 函数。在构建面向对象的 C++ 程序时，通常将可复用的源代码（例如类）定义在一个按惯例具有 .h 文件扩展名的文件中——这种文件称为头文件。程序使用 #include 预处理指令来包含头文件并利用

