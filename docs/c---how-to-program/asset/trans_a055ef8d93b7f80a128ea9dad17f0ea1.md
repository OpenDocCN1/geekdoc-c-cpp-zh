
## 16.4 数据成员、set 成员函数和 get 成员函数

如你所知，在函数定义体内声明的变量称为局部变量，只能从该函数中声明它们的行开始，到声明它们的块的右花括号 } 为止使用。局部变量必须先声明，然后才能在函数中使用。局部变量不能在声明它的函数之外访问。

一个类通常由一个或多个成员函数组成，这些成员函数操作属于该类特定对象的属性。属性在类定义中表示为变量。这样的变量称为数据成员，它们在类定义内声明，但在类成员函数定义的函数体之外声明。类的每个对象都在内存中维护自己的属性。这些属性在对象的整个生命周期内存在。本节的示例演示了一个 GradeBook 类，其中包含一个 courseName 数据成员，用于表示特定 GradeBook 对象的课程名称。如果创建多个 GradeBook 对象，每个对象都将拥有自己的 courseName 数据成员，并且这些数据成员可以包含不同的值。

### 带有数据成员以及 set 和 get 成员函数的 GradeBook 类

在下一个示例中，类 GradeBook（图 16.5）将课程名称作为数据成员进行维护，以便在程序执行期间可以使用或修改它。该类包含成员函数 setCourseName、getCourseName 和 displayMessage。成员函数 setCourseName 将课程名称存储在 GradeBook 的数据成员中。成员函数 getCourseName 从该数据成员中获取课程名称。成员函数 displayMessage——现在不指定任何参数——仍然显示包含课程名称的欢迎消息。然而，正如你将看到的，该函数现在通过调用同一类中的另一个函数——getCourseName——来获取课程名称。

```cpp
1 // Fig. 16.5: fig16_05.cpp
2 // Define class GradeBook that contains a courseName data member
3 // and member functions to set and get its value;
4 // Create and manipulate a GradeBook object with these functions.
5 #include <iostream>
6 #include <string> // program uses C++ standard string class
7 using namespace std;
8
9 // GradeBook class definition
10 class GradeBook
11 {
12 public:
13     // function that sets the course name
14     void setCourseName( string name )
15     {
16         courseName = name; // store the course name in the object
17     } // end function setCourseName
18
19     // function that gets the course name
20     string getCourseName() const
21     {
22         return courseName; // return the object's courseName
23     } // end function getCourseName
24
25     // function that displays a welcome message
26     void displayMessage() const
27     {
28         // this statement calls getCourseName to get the
29         // name of the course this GradeBook represents
30         cout << "Welcome to the grade book for\n" << getCourseName() << "!";
31         cout << endl;
32     } // end function displayMessage
33 private:
34     string courseName; // course name for this GradeBook
35 }; // end class GradeBook
36
37 // function main begins program execution
38 int main()
39 {
40     string nameOfCourse; // string of characters to store the course name
41     GradeBook myGradeBook; // create a GradeBook object named myGradeBook
42
43     // display initial value of courseName
44     cout << "Initial course name is: " << myGradeBook.getCourseName()
45         << endl;
46
47     // prompt for, input and set course name
48     cout << "\nPlease enter the course name:" << endl;
49     getline( cin, nameOfCourse ); // read a course name with blanks
50     myGradeBook.setCourseName( nameOfCourse ); // set the course name
51
52     cout << endl; // outputs a blank line
53     myGradeBook.displayMessage(); // display message with new course name
54 } // end main
```

图 16.5 | 定义并测试带有数据成员以及 set 和 get 成员函数的类 GradeBook。（第 1 部分，共 2 部分。）

```
Initial course name is:

Please enter the course name:
CS101 Introduction to C++ Programming

Welcome to the grade book for
CS101 Introduction to C++ Programming!
```

图 16.5 | 定义并测试带有数据成员以及 set 和 get 成员函数的类 GradeBook。（第 2 部分，共 2 部分。）

一位典型的教师教授多门课程，每门课程都有自己的课程名称。第 34 行声明 courseName 是 string 类型的变量。由于该变量在类定义（第 10–35 行）中声明，但在类成员函数定义的函数体（第 14–17、20–23 和 26–32 行）之外，因此该变量是数据成员。类 GradeBook 的每个实例（即对象）都包含该类的每个数据成员——如果有两个 GradeBook 对象，每个对象都有自己的 courseName（每个对象一个），正如你将在图 16.7 的示例中看到的。将 courseName 设为数据成员的一个好处是，该类的所有成员函数都可以操作类定义中出现的任何数据成员（在本例中为 courseName）。

### 访问说明符 public 和 private

大多数数据成员声明出现在 private 访问说明符之后。在访问说明符 private 之后（以及下一个访问说明符之前，如果存在的话）声明的变量或函数，只能被为其声明的类的成员函数访问（或被该类的“友元”访问，正如你将在第 17 章中看到的）。因此，数据成员 courseName 只能在类 GradeBook 的成员函数 setCourseName、getCourseName 和 displayMessage 中使用（或者被该类的“友元”使用，如果有的话）。

> **错误预防提示 16.1** 将类的数据成员设为 private，并将类的成员函数设为 public，有助于调试，因为数据操作方面的问题被限制在类的成员函数或类的友元中。

> **常见编程错误 16.2** 如果一个函数不是特定类的成员（或该类的友元），却试图访问该类的 private 成员，则会导致编译错误。

类成员的默认访问权限是 private，因此类头之后、第一个访问说明符之前（如果存在的话）的所有成员都是 private。访问说明符 public 和 private 可以重复出现，但这没有必要，而且可能造成混淆。使用访问说明符 private 声明数据成员称为数据隐藏。当程序创建 GradeBook 对象时，数据成员 courseName 被封装（隐藏）在对象中，只能由该对象所属类的成员函数访问。在类 GradeBook 中，成员函数 setCourseName 和 getCourseName 直接操作数据成员 courseName。

### 成员函数 setCourseName 和 getCourseName

成员函数 setCourseName（第 14–17 行）在完成任务时不返回任何数据，因此其返回类型为 void。该成员函数接收一个参数——name——它表示将作为实参传递给它的课程名称（正如我们将在 main 的第 50 行中看到的）。第 16 行将 name 赋给数据成员 courseName，从而修改对象——因此，我们不将 setCourseName 声明为 const。在这个示例中，setCourseName 不验证课程名称——也就是说，该函数不检查课程名称是否遵循任何特定格式，也不检查其是否遵循关于“有效”课程名称应是什么样子的任何其他规则。例如，假设某所大学打印的学生成绩单只能包含 25 个或更少字符的课程名称。在这种情况下，我们可能希望类 GradeBook 确保其数据成员 courseName 绝不超过 25 个字符。我们将在第 16.8 节讨论验证。

成员函数 getCourseName（第 20–23 行）返回特定 GradeBook 对象的 courseName，而不修改该对象——因此，我们将 getCourseName 声明为 const。该成员函数具有空参数列表，因此它不需要额外数据来执行任务。该函数指定它返回一个 string。当调用一个指定返回类型不是 `void` 的函数并完成其任务时，该函数使用 return 语句（如第 22 行）将*结果返回*给调用它的函数。例如，当你去自动取款机（ATM）并请求账户余额时，你期望 ATM 给你一个表示余额的值。类似地，当一条语句在 GradeBook 对象上调用成员函数 `getCourseName` 时，该语句期望收到该 GradeBook 的课程名称（在本例中为 string，如函数返回类型所指定）。

如果你有一个函数 square，它返回其参数的平方，那么语句

```
result = square( 2 );
```

从函数 square 返回 4，并将值 4 赋给变量 result。如果你有一个函数 maximum，它返回三个整数实参中的最大值，那么语句

```
biggest = maximum( 27, 114, 51 );
```

从函数 maximum 返回 114，并将该值赋给变量 biggest。

第 16 行和第 22 行中的语句都使用了变量 courseName（第 34 行），尽管它并*未*在任何成员函数中声明。我们可以看出这一点，因为 courseName 是该类的*数据成员*，而数据成员可以从类的成员函数访问。

### 成员函数 displayMessage

成员函数 displayMessage（第 26–32 行）在完成任务时*不*返回任何数据，因此其返回类型为 void。该函数*不*接收参数，因此其参数列表为空。第 30–31 行输出一条包含数据成员 courseName 值的欢迎消息。第 30 行调用成员函数 getCourseName 来获取 courseName 的值。成员函数 displayMessage 也可以像成员函数 setCourseName 和 getCourseName 那样直接访问数据成员 courseName。我们很快就会解释，为什么从软件工程的角度来看，调用成员函数 getCourseName 来获取 courseName 的值更可取。

### 测试类 GradeBook

main 函数（第 38–54 行）创建一个类 GradeBook 的对象，并使用它的每个成员函数。第 41 行创建一个名为 myGradeBook 的 GradeBook 对象。第 44–45 行通过调用该对象的 getCourseName 成员函数显示初始课程名称。输出的第一行没有显示课程名称，因为该对象的 courseName 数据成员（即一个 string）最初为空——默认情况下，string 的初始值是所谓的空字符串，即不包含任何字符的字符串。显示空字符串时，屏幕上不会出现任何内容。

第 48 行提示用户输入课程名称。局部 string 变量 nameOfCourse（在第 40 行声明）被设置为用户输入的课程名称，该名称通过调用 getline 函数（第 49 行）获得。第 50 行调用对象 myGradeBook 的 setCourseName 成员函数，并提供 nameOfCourse 作为该函数的实参。当调用该函数时，实参值被复制到成员函数 setCourseName 的参数 name（第 14 行）。然后，参数值被赋给数据成员 courseName（第 16 行）。第 52 行跳过一行；然后第 53 行调用对象 myGradeBook 的 displayMessage 成员函数，以显示包含课程名称的欢迎消息。
