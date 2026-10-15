

## 成员函数 setCourseName 和 getCourseName

成员函数 setCourseName（定义在第 19–22 行）在完成任务时不返回任何数据，因此其返回类型为 void。成员函数接收一个参数——name——它代表将作为参数传递给它的课程名称（正如我们在 main 的第 55 行看到的那样）。第 21 行将 name 赋给数据成员 courseName。在此示例中，setCourseName 并未尝试验证课程名称——即函数不会检查课程名称是否遵循任何特定格式或关于“有效”课程名称的其他规则。例如，假设一所大学可以打印包含课程名称不超过 25 个字符的学生成绩单。在这种情况下，我们可能希望类 GradeBook 确保其数据成员 courseName 从不包含超过 25 个字符。我们将在第 3.10 节讨论基本的验证技术。

成员函数 getCourseName（定义在第 25–28 行）返回特定 GradeBook 对象的 courseName。成员函数具有空的参数列表，因此它不需要额外的信息来执行其任务。函数指定它返回一个 string。当一个指定返回类型不为 void 的函数被调用并完成其任务时，函数会向其调用函数返回一个结果。例如，当你去自动取款机（ATM）并请求你的账户余额时，你期望 ATM 给你返回一个代表你余额的值。类似地，当一条语句在 GradeBook 对象上调用成员函数 getCourseName 时，该语句期望接收 GradeBook 的课程名称（在这种情况下是一个 string，正如函数返回类型所指定的）。如果你有一个返回其参数平方的函数 square，那么语句

```
result = square( 2 );
```

会从函数 square 返回 4 并将值 4 赋给变量 result。如果你有一个返回三个整数参数中最大值的函数 maximum，那么语句

```
biggest = maximum( 27, 114, 51 );
```

会从函数 maximum 返回 114 并将值 114 赋给变量 biggest。

### 常见编程错误 3.7

> 忘记从本应返回值 的函数中返回值是编译错误。

请注意，第 21 行和第 27 行中的语句各自使用变量 courseName（第 39 行），即使它未在任何成员函数中声明。我们可以在类 GradeBook 的成员函数中使用 courseName，因为 courseName 是该类的一个数据成员。还请注意，成员函数的定义顺序并不决定它们在执行时被调用的时间。因此，成员函数 getCourseName 可以在成员函数 setCourseName 之前定义。

## 成员函数 displayMessage

成员函数 displayMessage（第 31–37 行）在完成任务时不返回任何数据，因此其返回类型为 void。函数不接收参数，因此其参数列表为空。第 35–36 行输出包含数据成员 courseName 值的欢迎消息。第 35 行调用成员函数 getCourseName 以获取 courseName 的值。请注意，成员函数 displayMessage 也可以直接访问数据成员 courseName，就像成员函数 setCourseName 和 getCourseName 所做的那样。我们稍后会解释为什么我们选择调用成员函数 getCourseName 来获取 courseName 的值。

## 测试类 GradeBook

main 函数（第 43–60 行）创建一个 GradeBook 类的对象并使用其每个成员函数。第 46 行创建一个名为 myGradeBook 的 GradeBook 对象。第 49–50 行通过调用对象的 getCourseName 成员函数来显示初始课程名称。请注意，输出的第一行不会显示课程名称，因为对象的 courseName 数据成员（即一个 string）初始为空——默认情况下，string 的初始值是所谓的空 string，即不包含任何字符的字符串。当显示空字符串时，屏幕上不会出现任何内容。

第 53 行提示用户输入课程名称。局部 string 变量 nameOfCourse（在第 45 行声明）被设置为用户输入的课程名称，该名称由对 getline 函数的调用（第 54 行）获得。第 55 行调用对象 myGradeBook 的 setCourseName 成员函数并提供 nameOfCourse 作为函数的参数。当函数被调用时，参数的值被复制到成员函数 setCourseName（第 19–22 行）的参数 name（第 19 行）。然后参数的值被赋给数据成员 courseName（第 21 行）。第 57 行在输出中跳过一行；然后第 58 行调用对象 myGradeBook 的 displayMessage 成员函数以显示包含课程名称的欢迎消息。

## 使用 Set 和 Get 函数进行软件工程

类的私有数据成员只能由该类的成员函数（以及我们在第 10 章中会看到的类的“友元”）操作。因此，对象的客户端——即从对象外部调用对象成员函数的任何类或函数——调用类的公共成员函数以请求该类为特定对象提供服务。这就是为什么函数 main（图 3.5，第 43–60 行）中的语句在 GradeBook 对象上调用成员函数 setCourseName、getCourseName 和 displayMessage 的原因。

类通常提供公共成员函数以允许类的客户端设置（即为其赋值）或获取（即获得值）私有数据成员。这些成员函数的名称不必以 set 或 get 开头，但这种命名约定很常见。在此示例中，设置 courseName 数据成员的成员函数称为 setCourseName，而获取 courseName 数据成员值的成员函数称为 getCourseName。请注意，set 函数有时也称为 mutators（因为它们会改变值），而 get 函数有时也称为 accessors（因为它们访问值）。

请记住，用访问说明符 private 声明数据成员会强制执行数据隐藏。提供公共 set 和 get 函数允许类的客户端间接访问隐藏的数据。客户端知道它正在尝试修改或获取对象的数据，但客户端不知道对象如何执行这些操作。在某些情况下，类可能以一种方式在内部表示数据，但以另一种方式向客户端公开该数据。例如，假设 Clock 类将一天中的时间表示为私有 int 数据成员 time，该成员存储午夜以来的秒数。然而，当客户端调用 Clock 对象的 getTime 成员函数时，对象可以以字符串形式返回时间，格式为小时、分钟和秒，格式为 "HH:MM:SS"。类似地，假设 Clock 类提供一个名为 setTime 的 set 函数，该函数接受格式为 "HH:MM:SS" 的字符串参数。利用第 18 章介绍的字符串功能，setTime 函数可以将此字符串转换为秒数，并将该函数存储在其私有数据成员中。set 函数还可以检查接收到的值是否代表有效的时间（例如，"12:30:45" 有效但 "42:85:70" 无效）。set 和 get 函数允许客户端与对象交互，但对象的私有数据仍然安全地封装（即隐藏）在对象本身中。

类的 set 和 get 函数也应由类内的其他成员函数用来操作类的私有数据，尽管这些成员函数可以直接访问私有数据。在图 3.5 中，成员函数 setCourseName 和 getCourseName 是公共成员函数，因此它们可供类的客户端以及类本身访问。成员函数 displayMessage 调用成员函数 getCourseName 来获取数据成员 courseName 的值以供显示，即使 displayMessage 可以直接访问 courseName——通过其 get 函数访问数据成员可以创建更好的、更健壮的类（即更易于维护且不太可能停止工作的类）。如果我们决定以某种方式更改数据成员 courseName，displayMessage 的定义将不需要修改——只有直接操作数据成员的 get 和 set 函数的主体需要更改。例如，假设我们决定希望将课程名称表示为两个单独的数据成员——courseNumber（例如，"CS101"）和 courseTitle（例如，"Introduction to C++ Programming"）。成员函数 displayMessage 仍然可以对成员函数 getCourseName 进行一次调用以获取要作为欢迎消息一部分显示的完整课程名称。在这种情况下，getCourseName 需要构建并返回一个包含 courseNumber 后跟 courseTitle 的字符串。成员函数 displayMessage 将继续显示完整的课程标题 "CS101 Introduction to C++ Programming"，因为它不受类数据成员更改的影响。调用类中另一个成员函数的 set 函数的好处将在我们讨论第 3.10 节中的验证时变得清晰。

### 良好编程实践 3.4

> 始终尝试通过其 get 和 set 函数访问和操作类的 数据成员，以使对类数据成员的更改的影响局部化。对数据成员名称或用于存储数据成员的数据类型的更改然后只会影响相应的 get 和 set 函数，而不会影响这些函数的调用者。

### 软件工程观察 3.3

> 类设计者不必为每个私有数据项提供 set 或 get 函数；这些功能应仅在适当时提供。如果一项服务对客户端代码有用，该服务通常应在类的公共接口中提供。

## 带有数据成员和 set 和 get 函数的 GradeBook 的 UML 类图

图 3.6 包含图 3.5 中 GradeBook 类版本的更新 UML 类图。该图将 GradeBook 的数据成员 courseName 建模为中间隔间中的属性。UML 通过列出属性名称，后跟冒号和属性类型来表示数据成员作为属性。属性 courseName 的 UML 类型是 String，对应于 C++ 中的 string。数据成员 courseName 在 C++ 中是私有的，因此类图在相应属性的名称前面列出一个减号（–）。UML 中的减号等同于 private 访问说明符

