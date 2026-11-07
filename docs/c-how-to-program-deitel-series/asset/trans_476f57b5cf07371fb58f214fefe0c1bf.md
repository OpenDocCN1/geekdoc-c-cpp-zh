
`public:` 用于表示该函数“对公众可用”——也就是说，它可以被程序中的其他函数（如 `main`）以及其他类的成员函数（如果有的话）调用。访问限定符总是后跟冒号（`:`）。在本文的其余部分，当我们提到访问限定符 `public` 时，我们将像本句中那样省略冒号。第3.4节介绍了访问限定符 `private`。在本书后面，我们将学习访问限定符 `protected`。

程序中的每个函数执行一项任务，并在完成任务时可能**返回值**——例如，函数可能执行计算，然后返回计算结果。定义函数时，必须指定**返回类型**，以指示函数完成任务时返回的值的类型。在第12行中，函数名 `displayMessage` 左侧的关键字 `void` 是函数的返回类型。返回类型 `void` 表示 `displayMessage` 在完成任务时将**不**向它的**调用函数**（在本例中是 `main` 的第22行，我们稍后会看到）返回任何数据。在图3.5中，您将看到一个*确实*返回值的函数示例。

成员函数名 `displayMessage` 跟在返回类型之后（第12行）。按照惯例，我们的函数名使用*驼峰式*风格，首字母小写。成员函数名后的圆括号表示这是一个函数。一对空圆括号（如第12行所示）表示该成员函数*不*需要额外数据来执行其任务。您将在第3.3节中看到一个*确实*需要额外数据的成员函数示例。

我们在第12行将成员函数 `displayMessage` 声明为 **const**，因为在显示“欢迎使用成绩册！”的过程中，该函数*不会*也*不应该*修改调用它的 `GradeBook` 对象。将 `displayMessage` 声明为 **const** 告诉编译器：“此函数不应修改调用它的对象——如果修改了，请发出编译错误。”如果您不小心在 `displayMessage` 中插入了*可能*修改对象的代码，这可以帮助您定位错误。第12行通常称为**函数头**。

每个函数的*函数体*由左、右花括号（`{` 和 `}`）分隔，如第13行和第15行所示。*函数体*包含执行函数任务的语句。在本例中，成员函数 `displayMessage` 包含一条语句（第14行），该语句显示消息“欢迎使用成绩册！”。该语句执行完毕后，函数即完成了任务。

## 测试类 *GradeBook*

接下来，我们希望在程序中使用类 `GradeBook`。如您在第2章中所见，`main` 函数（第19–23行）开始每个程序的执行。

在这个程序中，我们希望调用类 `GradeBook` 的 `displayMessage` 成员函数来显示欢迎消息。通常，在*创建该类的对象*之前，您不能调用该类的成员函数。（正如您将在第9.14节学到的，静态成员函数是个例外。）第21行创建了一个名为 `myGradeBook` 的 `GradeBook` 类对象。该变量的类型是 `GradeBook`——即我们在第8–16行定义的类。当我们像第2章那样声明 `int` 类型的变量时，编译器知道 `int` 是什么——它是 C++“内置”的*基本类型*。然而，在第21行，编译器不会自动知道 `GradeBook` 是什么类型——它是一个*用户定义类型*。我们通过包含*类定义*（第8–16行）来告诉编译器 `GradeBook` 是什么。如果省略这些行，编译器将发出错误消息。您创建的每个类都会成为一种*新类型*，它

成员函数可以要求一个或多个参数，这些参数表示它执行任务所需的额外数据。函数调用为每个函数参数提供值——称为**实参**。例如，要向银行账户存款，假设 `Account` 类的 `deposit` 成员函数指定一个表示*存款金额*的参数。当 `deposit` 成员函数被调用时，表示存款金额的实参值被复制到该成员函数的参数中。然后该成员函数将该金额添加到账户余额中。

## 定义和测试类 GradeBook

我们的下一个示例（图3.3）重新定义了类 GradeBook（第9–18行），其中包含一个 displayMessage 成员函数（第13–17行），该函数将课程名称显示为欢迎消息的一部分。displayMessage 的新版本需要一个*参数*（第13行中的 courseName），该参数表示要输出的课程名称。

```cpp
// Fig. 3.3: fig03_03.cpp
// Define class GradeBook with a member function that takes a parameter,
// create a GradeBook object and call its displayMessage function.
#include <iostream>
#include <string> // program uses C++ standard string class
using namespace std;

// GradeBook class definition
class GradeBook
{
public:
   // function that displays a welcome message to the GradeBook user
   void displayMessage( string courseName ) const
   {
      cout << "Welcome to the grade book for\n" << courseName << "!"
           << endl;
   } // end function displayMessage
}; // end class GradeBook

// function main begins program execution
int main()
{
   string nameOfCourse; // string of characters to store the course name
   GradeBook myGradeBook; // create a GradeBook object named myGradeBook

   // prompt for and input course
   cout << "Please enter the course name:" << endl;
   getline( cin, nameOfCourse ); // read a course name with blanks
   cout << endl; // output a blank line

   // call myGradeBook's displayMessage function
   // and pass nameOfCourse as an argument
   myGradeBook.displayMessage( nameOfCourse );
} // end main
```

**图 3.3** | 定义一个带有接受参数的成员函数的类 GradeBook，创建一个 GradeBook 对象并调用其 displayMessage 函数。（第1部分，共2部分。）

## 关于实参和形参的更多内容

要在函数定义中指定该函数需要数据来执行任务，您需要在函数的*参数列表*中放置附加信息，参数列表位于函数名后的圆括号中。参数列表可以包含任意数量的参数，包括*根本没有参数*（如图3.1第12行中的空圆括号所示），以表明函数不需要任何参数。`displayMessage` 成员函数的参数列表（图3.3第13行）声明该函数需要一个参数。每个参数指定一个*类型*和一个*标识符*。类型 `string` 和标识符 `courseName` 表明成员函数 `displayMessage` 需要一个字符串来执行其任务。成员函数体使用参数 `courseName` 来访问函数调用（`main` 中的第33行）中传递给该函数的值。第15–16行将参数 `courseName` 的值显示为欢迎消息的一部分。参数变量的名称（第13行中的 `courseName`）可以*与*实参变量的名称（第33行中的 `nameOfCourse`）*相同*或*不同*——您将在第6章中了解原因。

函数可以通过逗号分隔多个参数来指定它们。函数调用中实参的数量和顺序*必须*与被调用成员函数头参数列表中的参数数量和顺序一致。此外，函数调用中的实参类型必须与函数头中相应参数的类型一致。（正如您将在后续章节中学到的，实参的类型与其对应参数的类型并不总是需要*完全相同*，但它们必须“一致”。）在我们的示例中，函数调用中的一个字符串实参（即 `nameOfCourse`）与成员函数定义中的一个字符串参数（即 `courseName`）*完全匹配*。

## 针对类 GradeBook 的更新后的 UML 类图

图3.4的UML类图对图3.3中的类 `GradeBook` 进行建模。与图3.1中定义的类 `GradeBook` 一样，这个 `GradeBook` 类包含公有成员函数 `displayMessage`。然而，这个版本的 `displayMessage` 有一个*参数*。UML通过列出参数名，后跟冒号和参数类型（位于操作名后的圆括号中）来对参数建模。UML拥有自己的数据类型，*类似于* C++ 的数据类型。UML是*语言无关的*——它用于许多不同的编程语言——因此其术语与C++不完全一致。例如，UML类型 `String` 对应于C++类型 `string`。类 `GradeBook` 的成员函数 `displayMessage`（图3.3第13–17行）有一个名为 `courseName` 的字符串参数，因此图3.4在操作方法名后的圆括号中列出了 `courseName : String`。这个版本的 `GradeBook` 类仍然没有任何数据成员。

![](img/b42ba5cd262b1358d16610173f975e4d_108_0.png)

**图 3.4** | UML类图，表明类 `GradeBook` 具有一个公有 `displayMessage` 操作，该操作带有一个 UML 类型为 `String` 的 `courseName` 参数。

