
Book. 为了帮助你为本章以及本书后面和工业界中会遇到的更大程序做准备，我们使用一个单独的类（本例中为 GradeBookTest）包含 main 方法来测试本章中创建的每个新类。一些程序员将此类称为驱动类。

GradeBookTest 类声明（图 3.2）包含将控制应用程序执行的 main 方法。GradeBookTest 类声明从第 4 行开始，到第 15 行结束。该类与许多开始应用程序执行的类一样，只包含一个 main 方法。

```
1 // Fig. 3.2: GradeBookTest.java
2 // Creating a GradeBook object and calling its displayMessage method.

4 public class GradeBookTest
5 {
6     // main method begins program execution
7     public static void main( String[] args )
8     {
9         // create a GradeBook object and assign it to myGradeBook
10        GradeBook myGradeBook = new GradeBook();

12        // call myGradeBook's displayMessage method
13        myGradeBook.displayMessage();
14     } // end main
15 } // end class GradeBookTest
```

Welcome to the Grade Book!

Fig. 3.2 | Creating a GradeBook object and calling its displayMessage method.

第 7–14 行声明了 main 方法。使 JVM 能够定位并调用 main 方法以开始应用程序执行的关键部分是 static 关键字（第 7 行），它表示 main 是一个静态方法。静态方法很特殊，因为你可以在不先创建声明该方法的类的对象的情况下调用它。我们将在第 6 章《Methods: A Deeper Look》中讨论静态方法。

在此应用程序中，我们希望调用类 GradeBook 的 displayMessage 方法以在命令窗口中显示欢迎消息。通常，在你创建该类的对象之前，不能调用属于另一个类的 方法，如第 10 行所示。我们首先声明变量 myGradeBook。变量的类型为 GradeBook——我们在图 3.1 中声明的类。你创建的每个新类都成为一种新类型，可用于声明变量和创建对象。你可以根据需要声明新的类类型；这也是 Java 被称为可扩展语言的原因之一。

变量 myGradeBook 在第 10 行使用类实例创建表达式 new GradeBook() 的结果进行初始化。关键字 new 创建关键字右侧指定的类（即 GradeBook）的新对象。GradeBook 右侧的括号是必需的。如你在第 3.6 节中将学到的，这些与类名组合的括号代表对构造函数的调用，构造函数类似于方法，但仅在创建对象时使用以初始化对象的数据。你会看到可以在括号中放置数据以指定对象的初始值。对于现在，我们只是将括号留空。

正如我们可以使用对象 System.out 调用其方法 print、printf 和 println 一样，我们也可以使用对象 myGradeBook 调用其方法 displayMessage。第 13 行使用 myGradeBook 后跟点分隔符（.）、方法名 displayMessage 和一组空括号调用方法 displayMessage（图 3.1 的第 7–10 行）。此调用导致 displayMessage 方法执行其任务。此方法调用与第 2 章中在命令窗口显示信息的那些方法调用不同——其中每个方法调用都提供了指定要显示的数据的参数。在第 13 行开头，“myGradeBook.” 表示 main 应使用第 10 行创建的 myGradeBook 对象。图 3.1 的第 7 行表明方法 displayMessage 具有空参数列表——即 displayMessage 不需要额外信息来执行其任务。因此，方法调用（图 3.2 的第 13 行）在方法名后指定一组空括号，以表示没有向 displayMessage 方法传递参数。当 displayMessage 方法完成其任务后，main 方法在第 14 行继续执行。这是 main 方法的结束，因此程序终止。

任何类都可以包含 main 方法。JVM 仅在用于执行应用程序的类中调用 main 方法。如果应用程序有多个包含 main 的类，则被调用的是在 java 命令中命名的类中的那个。

## Compiling an Application with Multiple Classes

在你执行应用程序之前，必须先编译图 3.1 和图 3.2 中的类。首先，切换到包含应用程序源代码文件的目录。接下来，输入命令

```
javac GradeBook.java GradeBookTest.java
```

一次编译两个类。如果目录中仅包含此应用程序的文件，你可以使用命令

```
javac *.java
```

编译目录中的所有类。

星号 (*) 在 *.java 中表示应编译当前目录中以文件名扩展名 “.java” 结尾的所有文件。

## UML Class Diagram for Class GradeBook

图 3.3 展示了图 3.1 的类 GradeBook 的 UML 类图。在 UML 中，每个类在类图中都建模为一个具有三个隔间的矩形。顶部隔间包含类名，以粗体居中水平显示。中间隔间包含类的属性，对应于 Java 中的实例变量（在第 3.4 节中讨论）。在图 3.3 中，中间隔间为空，因为此 GradeBook 类没有属性。底部隔间包含

![](img/009e962758dcc71dbc43a493362e6dc0_112_0.png)

Fig. 3.3 | UML class diagram indicating that class GradeBook has a public displayMessage operation.

类的操作，对应于 Java 中的方法。UML 通过列出操作名，后跟访问修饰符（本例中为 +）并跟随一组括号来建模操作。类 GradeBook 有一个方法 displayMessage，因此图 3.3 的底部隔间列出了一个名为此的操作。displayMessage 方法不需要额外信息来执行其任务，因此类图中的方法名后面跟着的括号为空，就像在图 3.1 的第 7 行的方法声明中一样。操作名前的加号 (+) 表示在 UML 中 displayMessage 是一个公共操作（即 Java 中的公共方法）。我们经常使用 UML 类图来总结类的属性和操作。

## 3.3 Declaring a Method with a Parameter

在第 1.6 节的汽车类比中，我们讨论了按下汽车油门踏板会向汽车发送消息以执行任务——加速。但汽车应该加速多快？正如你所知，你踩下踏板的距离越远，汽车加速越快。因此，发给汽车的消息实际上包括要执行的任务以及帮助汽车执行任务的额外信息。此额外信息称为参数——参数的值有助于汽车确定加速速度。同样，一个方法可能需要一个或多个参数，表示执行其任务所需的额外信息。参数在方法名后括号内的以逗号分隔的参数列表中定义。每个参数必须指定类型和变量名。参数列表可能包含任意数量的参数，包括零个。方法名后面跟着的空括号（如图 3.1，第 7 行）表示方法不需要任何参数。

### Arguments to a Method

方法调用为方法的每个参数提供值——称为参数。例如，方法 System.out.println 需要一个参数来指定要在命令窗口中输出的数据。同样，为了向银行账户存款，deposit 方法指定一个代表存款金额的参数。当调用 deposit 方法时，表示存款金额的参数值会被分配给方法参数。然后方法存入该金额。

### Class Declaration with a Method That Has One Parameter

我们现在声明类 GradeBook（图 3.4），其 displayMessage 方法在欢迎消息中显示课程名称。（参见图 3.5 中的示例执行。）新方法需要一个参数来表示要输出的课程名称。

在讨论 GradeBook 类的新特性之前，让我们看看新的类如何从类 GradeBookTest 的 main 方法中使用（图 3.5）。第 12 行创建一个 Scanner 命名为 input 用于从用户读取课程名称。第 15 行创建 GradeBook 对象 myGradeBook。第 18 行提示用户输入课程名称。第 19 行使用 Scanner 方法 nextLine 从用户读取名称并将其分配给 nameOfCourse 变量，以执行输入。用户输入课程名称并按 Enter 提交课程名称给程序。按 Enter 会在用户键入的字符末尾插入换行符。nextLine 方法读取用户键入的字符，直到遇到换行符，然后返回一个包含字符的字符串，不包括换行符。换行符被丢弃。

