

第 12 行和第 18 行的语句都使用了 courseName，即使它在任何方法中都没有声明。我们可以在 GradeBook 的方法中使用 courseName，因为 courseName 是该类的实例变量。

### 方法 displayMessage

方法 displayMessage（第 22–28 行）在完成任务时不返回任何数据，因此其返回类型为 void。该方法不接收参数，因此参数列表为空。第 26–27 行输出包含实例变量 courseName 值的欢迎消息，该值由第 27 行对方法 getCourseName 的调用返回。请注意，一个类的方法（本例中为 displayMessage）可以通过仅使用方法名（本例中为 getCourseName）来调用同一类的另一个方法。

## 演示类 GradeBook 的类 GradeBookTest

类 GradeBookTest（图 3.8）创建一个类 GradeBook 的对象并演示其方法。第 14 行创建一个 GradeBook 对象并将其分配给类型为 GradeBook 的局部变量 myGradeBook。第 17–18 行通过调用对象的 getCourseName 方法显示初始课程名称。输出的第一行显示名称为 "null"。与未自动初始化的局部变量不同，每个字段都有一个默认初始值——当你未指定字段的初始值时，Java 提供的默认值。因此，字段在使用前无需显式初始化——除非它们必须初始化为除默认值之外的其他值。对于类型为 String 的字段（例如本例中的 courseName），默认值是 null，我们将在第 3.5 节中更详细地介绍。

第 21 行提示用户输入课程名称。局部 String 变量 theName（在第 22 行声明）使用用户输入的课程名称进行初始化，该名称由 Scanner 对象 input 的 nextLine 方法调用返回。第 23 行调用对象 myGradeBook 的 setCourseName 方法并提供 theName 作为方法参数。当调用该方法时，参数的值被赋给方法 setCourseName（图 3.7 第 10–13 行）的参数 name（图 3.7 第 10 行）。然后参数的值被赋给实例变量 courseName（图 3.7 第 12 行）。第 24 行（图 3.8）跳过输出中的一行，然后第 27 行调用对象 myGradeBook 的 displayMessage 方法以显示包含课程名称的欢迎消息。

```
1 // Fig. 3.8: GradeBookTest.java
2 // Creating and manipulating a GradeBook object.
3 import java.util.Scanner; // program uses Scanner
4 
5 public class GradeBookTest
6 {
7     // main method begins program execution
8     public static void main( String[] args )
9     {
10        // create Scanner to obtain input from command window
11        Scanner input = new Scanner( System.in );
12
13        // create a GradeBook object and assign it to myGradeBook
14        GradeBook myGradeBook = new GradeBook();
15
16      // display initial value of courseName
17      System.out.printf( "Initial course name is: %s\n\n",
18          myGradeBook.getCourseName() );
19
20      // prompt for and read course name
21      System.out.println( "Please enter the course name:" );
22      String theName = input.nextLine(); // read a line of text
23      myGradeBook.setCourseName( theName ); // set the course name
24      System.out.println(); // outputs a blank line
25
26      // display welcome message after specifying course name
27      myGradeBook.displayMessage();
28      } // end main
29      } // end class GradeBookTest
```

```
Initial course name is: null
Please enter the course name:
CS101 Introduction to Java Programming
Welcome to the grade book for
CS101 Introduction to Java Programming!
```

图 3.8 | 创建和操作 GradeBook 对象。（第 2 部分，共 2 部分。）

## set 和 get 方法

类的私有字段只能由该类的方法操作。因此，对象的客户端——即调用对象方法的任何类——调用类的公共方法来操作该类对象的私有字段。这就是为什么方法 main（图 3.8）中的语句在 GradeBook 对象上调用 setCourseName、getCourseName 和 displayMessage 方法的原因。类通常提供公共方法以允许客户端设置（即为其分配值）或获取（即获得值）私有实例变量。这些方法的名称不必以 set 或 get 开头，但这种命名约定是推荐的，并且是称为 JavaBeans 的特殊 Java 软件组件的约定，JavaBeans 可以简化许多 Java 集成开发环境（IDE）中的编程。本例中设置实例变量 courseName 的方法称为 setCourseName，而获取其值的方法称为 getCourseName。

### 带有实例变量和 set 与 get 方法的 GradeBook UML 类图

图 3.9 包含类 GradeBook 的更新 UML 类图，该类版本见图 3.7。该图将类 GradeBook 的实例变量 courseName 建模为类中部隔间中的属性。UML 通过列出属性名称，后跟冒号和属性类型来表示实例变量作为属性。属性 courseName 的 UML 类型是 String。实例变量 courseName 在 Java 中是私有的，因此类图在相应属性名称前列出减号 (-) 访问修饰符。类 GradeBook 包含三个公共方法，因此类图在第三个隔间中列出三个操作。请记住，每个操作名称前的加号 (+) 表示该操作是公共的。操作 setCourseName 有一个名为 name 的 String 参数。UML 通过在操作名称后括号之后的冒号和返回类型来表示操作的返回类型。类 GradeBook（图 3.7）的方法 getCourseName 在 Java 中的返回类型为 String，因此类图在 UML 中显示 String 返回类型。操作 setCourseName 和 displayMessage 不返回值（即在 Java 中返回 void），因此 UML 类图在这些操作的括号后不指定返回类型。

![](img/009e962758dcc71dbc43a493362e6dc0_121_0.png)

图 3.9 | UML 类图表明类 GradeBook 具有私有 courseName 属性，其 UML 类型为 String，以及三个公共操作——setCourseName（具有 UML 类型为 String 的 name 参数）、getCourseName（返回 UML 类型 String）和 displayMessage。

## 3.5 原始类型与引用类型

Java 的类型分为原始类型和引用类型。原始类型为 boolean、byte、char、short、int、long、float 和 double。所有非原始类型都是引用类型，因此类，即指定对象类型的类型，是引用类型。

原始类型变量一次只能存储其声明类型的一个值。例如，int 变量一次只能存储一个整数（例如 7）。当向该变量分配另一个值时，其初始值将被替换。原始类型实例变量默认会被初始化——类型为 byte、char、short、int、long、float 和 double 的变量初始化为 0，类型为 boolean 的变量初始化为 false。你可以通过在声明时为变量分配值来指定原始类型变量自己的初始值，如

```
private int numberOfStudents = 10;
```

请记住，局部变量默认不会被初始化。

错误预防提示 3.1 尝试使用未初始化的局部变量会导致编译错误。

程序使用引用类型变量（通常称为引用）来存储计算机内存中对象的存储位置。这样的变量据说在程序中引用一个对象。被引用的对象可能各自包含许多实例变量。图 3.8 第 14 行创建一个类 GradeBook 的对象，并且变量 myGradeBook 包含对该 GradeBook 对象的引用。引用类型实例变量默认初始化为值 null——表示“对无物的引用”的保留字。这就是为什么图 3.8 第 18 行对 getCourseName 的第一次调用返回 null 的原因——courseName 的值尚未设置，因此返回了默认初始值 null。保留字和关键字的完整列表列在附录 C 中。

当你使用另一个类的对象时，需要对该对象的引用来调用（即调用）其方法。在图 3.8 的应用程序中，方法 main 中的语句使用

