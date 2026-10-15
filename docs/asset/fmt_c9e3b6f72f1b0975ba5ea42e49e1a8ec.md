
如3.6节所述，当`GradeBook`类（图3.5）的对象被创建时，其数据成员`courseName`默认被初始化为空字符串。如果你希望在创建`GradeBook`对象时提供课程名称，该怎么办？你声明的每个类都可以提供一个构造函数，用于在创建对象时初始化该类的对象。构造函数是一种特殊的成员函数，必须定义为与类相同的名称，以便编译器能够将其与类的其他成员函数区分开来。构造函数与其他函数的一个重要区别是，构造函数不能返回值，因此它们不能指定返回类型（甚至不能是`void`）。通常，构造函数被声明为公有。在文献中，“构造函数”一词常被缩写为“ctor”——我们通常避免使用缩写。

C++要求为每个创建的对象调用构造函数，这有助于确保每个对象在程序中使用之前被初始化。构造函数调用在对象创建时隐式发生。如果类没有显式包含构造函数，编译器会提供一个默认构造函数——即没有参数的构造函数。例如，当图3.5中的第46行创建一个`GradeBook`对象时，会调用默认构造函数。编译器提供的默认构造函数创建一个`GradeBook`对象，但不会给对象的基本类型数据成员提供任何初始值。[注意：对于作为其他类对象的数据成员，默认构造函数会隐式调用每个数据成员的默认构造函数，以确保该数据成员被正确初始化。这就是为什么`string`数据成员`courseName`（在图3.5中）被初始化为空字符串——`string`类的默认构造函数将字符串的值设置为空字符串。你将在10.3节中了解更多关于初始化作为其他类对象的数据成员的内容。]

在图3.7的示例中，我们在创建`GradeBook`对象时为其指定课程名称（第49行）。在这种情况下，参数`"CS101 Introduction to C++ Programming"`被传递给`GradeBook`对象的构造函数（第17-20行），并用于初始化`courseName`。图3.7定义了一个修改后的`GradeBook`类，其中包含一个带`string`参数的构造函数，该参数接收初始课程名称。

```
// Fig. 3.7: fig03_07.cpp
// Instantiating multiple objects of the GradeBook class and using
// the GradeBook constructor to specify the course name
// when each GradeBook object is created.
#include <iostream>
using std::cout;
using std::endl;

#include <string> // program uses C++ standard string class
using std::string;

// GradeBook class definition
class GradeBook
{
public:
    // constructor initializes courseName with string supplied as argument
    GradeBook( string name )
    {
        setCourseName( name ); // call set function to initialize courseName
    } // end GradeBook constructor

    // function to set the course name
    void setCourseName( string name )
    {
        courseName = name; // store the course name in the object
    } // end function setCourseName

    // function to get the course name
    string getCourseName()
    {
        return courseName; // return object's courseName
    } // end function getCourseName

    // display a welcome message to the GradeBook user
    void displayMessage()
    {
        // call getCourseName to get the courseName
        cout << "Welcome to the grade book for\n" << getCourseName()
            << "!" << endl;
    } // end function displayMessage
private:
    string courseName; // course name for this GradeBook
}; // end class GradeBook
```

图3.7 | 实例化`GradeBook`类的多个对象，并使用`GradeBook`构造函数在每个`GradeBook`对象创建时指定课程名称。（第1部分，共2部分。）

```
45 // function main begins program execution
46 int main()
47 {
48     // create two GradeBook objects
49     GradeBook gradeBook1( "CS101 Introduction to C++ Programming" );
50     GradeBook gradeBook2( "CS102 Data Structures in C++" );
51
52     // display initial value of courseName for each GradeBook
53     cout << "gradeBook1 created for course: " << gradeBook1.getCourseName()
54         << "\n gradeBook2 created for course: " << gradeBook2.getCourseName()
55         << endl;
56     return 0; // indicate successful termination
57 } // end main
```

```
gradeBook1 created for course: CS101 Introduction to C++ Programming
gradeBook2 created for course: CS102 Data Structures in C++
```

图3.7 | 实例化`GradeBook`类的多个对象，并使用`GradeBook`构造函数在每个`GradeBook`对象创建时指定课程名称。（第2部分，共2部分。）

### 定义构造函数

图3.7的第17-20行定义了`GradeBook`类的构造函数。注意，构造函数与其类`GradeBook`同名。构造函数在其参数列表中指定执行其任务所需的数据。创建新对象时，你将此数据放在对象名称后面的括号中（如我们在第49-50行所做的那样）。第17行表明`GradeBook`类的构造函数有一个名为`name`的`string`参数。注意，第17行没有指定返回类型，因为构造函数不能返回值（甚至不能是`void`）。

构造函数体中的第19行将构造函数的参数`name`传递给成员函数`setCourseName`，后者将值赋给数据成员`courseName`。`setCourseName`成员函数（第23-26行）只是将其参数`name`赋给数据成员`courseName`，因此你可能想知道为什么我们要在第19行调用`setCourseName`——构造函数当然可以执行赋值`courseName = name`。在3.10节中，我们将修改`setCourseName`以执行验证（确保在这种情况下`courseName`的长度不超过25个字符）。到那时，从构造函数调用`setCourseName`的好处将会变得清晰。注意，构造函数（第17行）和`setCourseName`函数（第23行）都使用名为`name`的参数。你可以在不同的函数中使用相同的参数名，因为参数对于每个函数是局部的；它们互不干扰。

### 测试GradeBook类

图3.7的第46-57行定义了测试`GradeBook`类的主函数，并演示了使用构造函数初始化`GradeBook`对象。`main`函数中的第49行创建并初始化名为`gradeBook1`的`GradeBook`对象。当该行执行时，C++隐式调用`GradeBook`构造函数（第17-20行），参数为`"CS101 Introduction to C++ Programming"`，以初始化`gradeBook1`的课程名称。第50行对名为`gradeBook2`的`GradeBook`对象重复此过程，此次传递参数`"CS102 Data Structures in C++"`来初始化`gradeBook2`的课程名称。第53-54行使用每个对象的`getCourseName`成员函数获取课程名称，并表明它们确实在对象创建时被初始化。输出证实每个`GradeBook`对象都维护着自己的一份`courseName`数据成员的拷贝。

### 为类提供默认构造函数的两种方式

任何不带参数的构造函数都称为默认构造函数。一个类可以通过以下两种方式获得默认构造函数：

- 1. 编译器会在未定义构造函数的类中隐式创建默认构造函数。这样的默认构造函数不会初始化类的成员数据，但会调用每个作为另一类对象的成员数据的默认构造函数。[注意：未初始化的变量通常包含“垃圾”值（例如，未初始化的`int`变量可能包含`-858993460`，这在大多数程序中很可能是该变量的不正确值）。]

- 2. 你显式定义一个不带参数的构造函数。这样的默认构造函数将执行你指定的初始化，并调用每个作为另一类对象的成员数据的默认构造函数。

如果你定义了一个带参数的构造函数，C++将不会为该类隐式创建默认构造函数。请注意，对于图3.1、图3.3和图3.5中的每个版本的类`GradeBook`，编译器都隐式定义了一个默认构造函数。

### 错误预防提示 3.2

除非你的类的数据成员无需初始化（几乎从不如此），请提供一个构造函数，以确保在创建类的每个新对象时，类的数据成员都使用有意义的值进行初始化。

### 软件工程观察 3.4

数据成员可以在类的构造函数中初始化，也可以在对象创建后稍后设置其值。然而，确保对象在客户端代码调用其成员函数之前已完全初始化，是一种良好的软件工程实践。通常，你不应依赖客户端代码来确保对象得到正确初始化。

### 将构造函数添加到类 GradeBook 的 UML 类图

图3.8的UML类图对图3.7的类`GradeBook`进行了建模，该类具有一个名为`name`的`string`类型参数的构造函数（在UML中表示为`String`类型）。与操作一样，UML在类图中类的第三个区段中对构造函数进行建模。为了区分构造函数和类的操作，UML在构造函数名称前放置“constructor”一词，位于尖括号（`«` 和 `»`）之间。习惯上在第三个区段中将类的构造函数列在其他操作之前。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_110_0.png)

图3.8 | UML类图指示类`GradeBook`具有一个参数为UML类型`String`的`name`的构造函数。

### 3.8 将类放在单独的文件中以实现可重用性

从编程角度来看，我们已经将类`GradeBook`开发到目前所需的程度，因此让我们考虑一些软件工程问题。创建类定义的一个好处是，当正确打包时，我们的类可以被程序员重用——可能遍及全球。例如，我们可以通过在程序中包含头文件`<string>`来在任何C++程序中重用C++标准库类型`string`（并且，如我们将看到的，能够链接到库的对象代码）。

不幸的是，希望使用我们的`GradeBook`类的程序员不能简单地将图3.7中的文件包含到另一个程序中。正如你在第2章中学到的，函数`main`开始每个程序的执行，并且每个程序必须恰好有一个`main`函数。如果其他程序员包含图3.7中的代码，他们会得到额外的负担——我们的`main`函数——他们的程序将有两个`main`函数。当他们尝试编译程序时，编译器会指示错误。例如，在Microsoft Visual C++ 2008中尝试编译包含两个`main`函数的程序会产生错误

```
error C2084: function 'int main(void)' already has a body
```

当编译器尝试编译它遇到的第二个`main`函数时。同样，GNU C++编译器会产生错误

```
redefinition of 'int main()'
```

这些错误表明程序已经有一个`main`函数。因此，将`main`与类定义放在同一个文件中会阻止该类被其他程序重用。在本节中，我们演示了如何通过将类`GradeBook`与`main`函数分离到另一个文件中使其可重用。

#### 头文件

本章中之前的每个示例都由一个`.cpp`文件组成，也称为源代码文件，其中包含`GradeBook`类定义和`main`函数。在构建面向对象的C++程序时，通常将可重用的源代码（例如类）定义在按惯例具有`.h`文件名扩展名的文件中——称为头文件。程序使用`#include`预处理器指令包含头文件并利用可重用的软件组件，例如C++标准库提供的类型`string`和用户定义的类型如类`GradeBook`。

在下一个示例中，我们将图3.7中的代码分离到两个文件——`GradeBook.h`（图3.9）和`fig03_10.cpp`（图3.10）。当你查看图3.9中的头文件时，注意它只包含`GradeBook`类定义（第11–41行）和第3–8行，这些行允许类`GradeBook`使用`cout`、`endl`和类型`string`。使用类`GradeBook`的`main`函数在源代码文件`fig03_10.cpp`（图3.10）第10–21行中定义。为了帮助你为本书记载的更大程序以及工业界的程序做好准备，我们经常使用包含函数`main`的单独源代码文件来测试我们的类（这称为驱动程序）。你很快就会看到，包含`main`的源代码文件如何使用头文件中找到的类定义来创建类的对象。

### 包含包含用户定义类的头文件

像`GradeBook.h`（图3.9）这样的头文件不能用于开始程序执行，因为它不包含`main`函数。如果你尝试单独编译和链接`GradeBook.h`以创建可执行应用程序，Microsoft Visual C++ 2005会产生链接错误消息：

```
error LNK2019: unresolved external symbol _main referenced in
function _mainCRTStartup
```

要在Linux上使用GNU C++编译和链接，你必须先将头文件包含在`.cpp`源代码文件中，然后GNU C++会产生包含以下内容的链接错误消息：

```
undefined reference to 'main'
```

此错误表明链接器无法找到程序的`main`函数。为了测试类`GradeBook`（定义在图3.9中），你必须编写一个包含`main`函数的单独源代码文件（例如图3.10），该文件实例化并使用该类的对象。

```
// Fig. 3.9: GradeBook.h
// GradeBook class definition in a separate file from main.

#include <iostream>
using std::cout;
using std::endl;

#include <string> // class GradeBook uses C++ standard string class
using std::string;

// GradeBook class definition
class GradeBook
{
public:
    // constructor initializes courseName with string supplied as argument
    GradeBook( string name )
    {
        setCourseName( name ); // call set function to initialize courseName
    } // end GradeBook constructor

    // function to set the course name
    void setCourseName( string name )
    {
        courseName = name; // store the course name in the object
    } // end function setCourseName

    // function to get the course name
    string getCourseName()
    {
        return courseName; // return object's courseName
    } // end function getCourseName

    // display a welcome message to the GradeBook user
    void displayMessage()
    {
```
