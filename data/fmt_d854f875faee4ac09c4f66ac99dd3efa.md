
你应创建一个 `Question` 类来存储每个问题、其答案以及任何其他问题状态信息。已回答和未回答的队列应使用 `java.util.LinkedList` 类实现。你只能使用该类提供的提供队列功能的方法：移除第一个元素、在末尾追加元素、检索队列大小以及遍历列表。

`appleviewer`—一种软件工具，通过 HTML 文档中的链接解释并显示 Java 小程序。Java 开发工具包的一部分。

`application`—(1) 任何程序的通用术语。(2) 一种可以在不使用 Web 浏览器的情况下运行的 Java 程序，与 Java 小程序相对。

`Application Programming Interface (API)`—一组类，定义了程序员可用的服务。它不是语言本身的一部分，但通常被依赖以执行甚至是基本任务。另见 `class library`。

`arc angle`—在定义弧时，定义弧长度的径向距离。另见 `start angle`。

`architectural design`—一种高层设计，识别软件系统的较大部分和关键数据结构。另见 `detailed design`。

`architecture`—参见 `computer architecture`。

`array element type`—存储在数组中的值或对象的类型。

`ASCII`—许多编程语言使用的流行字符集。`ASCII` 代表 American Standard Code for Information Interchange。它是 Java 使用的 Unicode 字符集的子集。

`assembly language`—一种使用助记符表示程序命令的低级语言。

`assignment conversion`—某些数据类型可以在赋值语句中转换为另一种。参见 `widening conversion`。

`assignment operator`—导致向变量赋值的运算符。`=` 运算符执行基本赋值。许多其他赋值运算符在赋值前执行额外操作，例如 `*=` 运算符。

`association`—两个类之间的关系，其中一个使用另一个或以某种方式与其相关。另见 `operator association`, `use relationship`。

`AWT`—参见 `Abstract Windowing Toolkit`。

`background color`—(1) 图形用户界面组件的背景颜色。(2) HTML 页面的背景颜色。另见 `foreground color`。

`base`—特定数字系统所基于的数值。它决定了该数字系统中可用的数字位数以及数字中每个数字的位值。另见 `binary`, `decimal`, `hexadecimal`, `octal`, `place value`。

## APPENDIX A Glossary

**`base case`**—终止递归处理的情形，允许活动的递归方法开始返回到其调用点。

**`base class`**—参见 `superclass`。

**`behavior`**—对象的功能特性，由其方法定义。*另见* `identity`, `state`。

**`binary`**—基数-2 数字系统。现代计算机系统将信息存储为二进制数字（位）的字符串。

**`binary operator`**—使用两个操作数的运算符。

**`binary search`**—一种搜索算法，要求列表已排序。它反复将列表的“中间”元素与目标值进行比较，每次缩小搜索范围。*另见* `linear search`。

**`binary string`**—一系列二进制数字（位）。

**`binary tree`**—一种树数据结构，其中每个节点最多有两个子节点。

**`binding`**—将标识符与其所代表的构造关联起来的过程。例如，将方法名绑定到其调用的具体定义的过程。

**`bit`**—二进制数字，为 0 或 1。

**`bit shifting`**—将数据值的位向左或向右移动，在一端丢失位并在另一端插入位。

**`bits per second (bps)`**—数据传输设备的测量速率。

**`bitwise operator`**—操作值的单个位的运算符，无论是通过计算还是通过移位。

**`black-box testing`**—基于软件组件的输入和预期输出生成和评估测试用例。测试用例侧重于覆盖输入的等价类别和边界值。*另见* `white-box testing`。

**`block`**—由大括号 (`{}`) 限定的程序语句和声明组。

**`boolean`**—Java 保留字，表示只能取 `true` 或 `false` 值的逻辑原始数据类型。

**`boolean expression`**—求值为 true 或 false 结果的表达式，主要用作选择和重复语句的条件。

**`boolean operator`**—当应用于布尔操作数时，位运算符 AND (`&`)、OR (`|`) 或 XOR (`^`) 中的任意一个。结果与其逻辑对应物等价，只是布尔运算符不是短路的。

**`border`**—围绕图形用户界面组件的图形边缘，以增强其外观或在视觉上对组件进行分组。空边框在组件周围创建空间缓冲区。

**`bounding rectangle`**—界定椭圆或弧所定义区域的矩形。

**`boundary values`**—对应于等价类别边缘的输入值。用于黑盒测试。

**`bounds checking`**—确定数组索引是否在界限内的过程，给定数组的大小。Java 执行自动边界检查。

**`bps`**—参见 `bits per second`。

**`break`**—Java 保留字，用于通过跳出当前循环或 `switch` 语句中断控制流。

**`browser`**—在网络上检索 HTML 文档和其他资源并将其格式化以供查看的软件。浏览器是访问万维网的主要工具。

**`bug`**—计算机程序中缺陷或错误的俚语。

**`build-and-fix approach`**—一种软件开发方法，其中程序在没有显著规划或设计的情况下创建，然后进行修改直到达到某种接受程度。它是一种普遍但不明智的方法。

**`bus`**—计算机中一组用于在 CPU 和主内存等组件之间传输数据的导线。

**`button`**—图形用户界面组件，允许用户通过鼠标点击启动操作、设置条件或选择选项。有几种 GUI 按钮类型。另见 `check box`, `push button`, `radio button`。

**`byte`**—(1) 等于八位的二进制存储单元。(2) Java 保留字，表示使用八位以二进制补码格式存储的原始整数类型。

**`byte stream`**—管理原始二进制数据的 8 位字节的 I/O 流。另见 `character stream`。

**`bytecode`**—Java 编译器将 Java 源代码翻译成的低级格式。字节码由 Java 解释器解释和执行，可能在通过互联网传输之后。

**`capacity`**—参见 `storage capacity`。

**`case`**—(1) Java 保留字，用于在 switch 语句中标识每个唯一选项。(2) 字母字符的方向（大写或小写）。

**`case sensitive`**—区分字母的大写和小写版本。Java 是区分大小写的；因此标识符 `total` 和标识符 `Total` 被视为不同的标识符。

**`cast`**—Java 操作，使用类型或类名在括号中表示，以显式转换并返回一种数据类型的值为另一种数据类型。

**`catch`**—Java 保留字，用于指定异常处理程序，定义在 try 块之后。

**`CD-Recordable (CD-R)`**—一种使用配备适当驱动器的家用计算机可一次性存储信息的光盘。另见 `CD-Rewritable`, `CD-ROM`。

**`CD-Rewritable (CD-RW)`**—一种使用配备适当驱动器的家用计算机可多次存储和重写信息的光盘。另见 `CD-Recordable`, `CD-ROM`。

**`CD-ROM`**—一种光学二级存储介质，以类似于音乐光盘的方式存储二进制信息。

**`central processing unit (CPU)`**—控制计算机主要活动（包括信息流和命令执行）的硬件组件。

**`char`**—Java 保留字，表示原始字符类型。所有 Java 字符都是 Unicode 字符集的成员，使用 16 位存储。

**`character font`**—定义字符在打印或绘制时独特外观的规范。

**`character set`**—字符的有序列表，例如 `ASCII` 或 `Unicode` 字符集。每个字符在给定字符集中对应一个特定、唯一的数值。编程语言采用特定字符集用于字符表示和管理。

**`character stream`**—管理 16 位 Unicode 字符的 I/O 流。另见 `byte stream`。

**`character string`**—一系列有序字符。在 Java 中使用 `String` 类和字符串字面量如 `"hello"` 表示。

**`复选框（check box）`**—一种图形用户界面组件，允许用户通过鼠标点击设置布尔条件。复选框可以单独使用，也可以在其他复选框之间独立使用。另请参阅单选按钮（`radio button`）。

**`受检异常（checked exception）`**—一种必须被捕获或显式抛给调用方法的Java异常。另请参阅非受检异常（`unchecked exception`）。

**`子类（child class）`**—参见“子类”。

**`类（class）`**—（1）Java保留字，用于定义类。（2）对象的蓝图——定义实例化时对象将包含的变量和方法的模型。

**`类图（class diagram）`**—显示类之间关系的图，包括继承和使用关系。另请参阅统一建模语言（`Unified Modeling Language`）。

**`类层次结构（class hierarchy）`**—通过继承从其他类派生出类时创建的树状结构。另请参阅接口层次结构（`interface hierarchy`）。

**`类库（class library）`**—一组为程序员提供有用服务的类。另请参阅应用程序编程接口（`Application Programming Interface`）。

**`类方法（class method）`**—一种仅使用类名即可调用的方法。与实例方法不同，不需要实例化对象。在Java程序中通过使用 `static` 保留字定义。

**`CLASSPATH（类路径）`**—一种操作系统设置，用于确定Java解释器搜索类文件的位置。

**`类变量（class variable）`**—一个类的所有对象共享的变量。也可以通过类名引用，而无需实例化该类的任何对象。在Java程序中通过使用 `static` 保留字定义。

**`客户端-服务器模型（client-server model）`**—一种基于对象（客户端）使用其他对象（服务器）提供的服务来构建软件设计的方式。

**`编码指南（coding guidelines）`**—描述程序应如何构建的一系列约定。它们使程序更易于阅读、交换和集成。有时被称为编码标准（`coding standards`），尤其是在强制执行时。

**`编码标准（coding standard）`**—参见“编码指南”。

**`内聚性（cohesion）`**—软件组件内部各部分之间关系的强度。另请参阅耦合性（`coupling`）。

**`冲突（collision）`**—两个哈希值产生相同哈希码的过程。另请参阅哈希码（`hash code`）、哈希（`hashing`）。

**`颜色选择器（color chooser）`**—一种图形用户界面组件，通常显示为对话框，允许用户选择或指定颜色。

**`组合框（combo box）`**—一种图形用户界面组件，允许用户从多个选项中选择一个。组合框显示最近的选择。另请参阅列表（`list`）。

**`命令行参数（command-line arguments）`**—命令行中程序名后面的值。在Java程序中通过 `main` 方法的字符串数组参数访问。

**`注释（comment）`**—一种编程语言结构，允许程序员将人类可读的注释嵌入源代码。另请参阅文档（`documentation`）。

**`编译器（compiler）`**—将代码从一种语言翻译为另一种语言等价代码的程序。Java编译器将Java源代码翻译为Java字节码。另请参阅解释器（`interpreter`）。

**`编译时错误（compile-time error）`**—在编译过程中发生的任何错误，通常表明程序不符合语言语法，或者尝试对不合适的数据类型进行操作。另请参阅逻辑错误（`logical error`）、运行时错误（`run-time error`）、语法错误（`syntax error`）。

**`组件（component）`**—软件系统中执行特定任务（将输入转换为输出）的任何部分。另请参阅GUI组件（`GUI component`）。

**`计算机体系结构（computer architecture）`**—计算机硬件组件的结构和交互。

**`连接（concatenation）`**—参见字符串连接（`string concatenation`）。

**`条件（condition）`**—用于确定是否应执行选择或重复语句体的布尔表达式。

**`条件覆盖（conditional coverage）`**—在白盒测试中使用的一种策略，其中执行程序中的所有条件，产生真和假两种结果。另请参阅语句覆盖（`statement coverage`）。

**`条件运算符（conditional operator）`**—Java三元运算符，根据条件计算两个表达式之一。

**`条件语句（conditional statement）`**—参见选择语句（`selection statement`）。

**`const`**—Java保留字，当前未使用。

**`常量（constant）`**—保存一个不能修改的值的标识符。用于使代码更具可读性并便于更改。在Java中使用 `final` 修饰符定义。

**`构造方法（constructor）`**—类中一种特殊的方法，在从类实例化对象时调用。用于初始化对象。

**`容器（container）`**—一种Java图形用户界面组件，可以容纳其他组件。另请参阅包含层次结构（`containment hierarchy`）。

**`包含层次结构（containment hierarchy）`**—用户界面的图形组件之间的关系。另请参阅容器（`container`）。

**`内容面板（content pane）`**—顶层容器中添加组件的部分。

**`控制字符（control characters）`**—参见不可打印字符（`nonprintable characters`）。

**`控制器（controller）`**—控制计算机系统与特定类型外设之间交互的硬件设备。

**`耦合性（coupling）`**—两个软件组件之间关系的强度。另请参阅内聚性（`cohesion`）。

**`CPU`**—参见中央处理器（`central processing unit`）。

**`数据流（data stream）`**—表示特定数据源或数据目的地（如文件）的I/O流。另请参阅处理流（`processing stream`）。

**`数据结构（data structure）`**—任何编程构造，无论是语言定义的还是程序员定义的，用于将数据组织成便于访问和处理的格式。数组、链表和栈都可以视为数据结构。

**`数据类型（data type）`**—指定一组值（可能无限）的指示。例如，每个变量都有一个数据类型，指定可存储的值的种类。

**`数据传输设备（data transfer device）`**—允许在计算机之间发送信息的硬件组件，例如调制解调器。

**`调试器（debugger）`**—一种软件工具，允许程序员逐步执行正在运行的程序，并在任何点检查变量的值。另请参阅 `jdb`。

**`十进制（decimal）`**—基数为10的数字系统，人类在日常生活中使用。另请参阅二进制（`binary`）。

**`default`**—Java保留字，用于指示switch语句的默认情况，在没有其他情况匹配时使用。

**`默认可见性（default visibility）`**—当没有使用显式可见性修饰符声明类、接口、方法或变量时指定的访问级别。有时称为包可见性（`package visibility`）。任何以默认可见性声明的元素仅对同一包中的类可见。

**`缺陷测试（defect testing）`**—旨在揭示程序中错误的测试。

**`分隔符（delimiter）`**—用于设置编程语言构造边界的任何符号或单词，例如用于定义Java块的花括号（`{}`）。

**`弃用（deprecated）`**—某些内容（例如Java API中的特定方法）被认为不推荐使用，不应使用。

**`派生类（derived class）`**—参见子类（`subclass`）。

**`设计（design）`**—（1）实现程序的计划，包括所用类和对象的规范以及重要程序算法的表达。（2）创建程序设计的过程。

**`桌面检查（desk check）`**—一种审查类型，开发人员仔细检查设计或程序以发现错误。

**`详细设计（detailed design）`**—（1）方法的低级算法步骤。（2）确定低级算法步骤的开发阶段。

**`开发阶段（development stage）`**—软件生命周期的阶段，在该阶段首次创建软件系统，随后是使用、维护和最终退役。

**`对话框（dialog box）`**—弹出的小图形窗口，用于进行简短、特定的用户交互。

**`数字（digital）`**—一种将信息分解为片段，再以数字形式表示这些片段的表示方式。所有现代计算机系统都是数字的。

**`数字化（digitize）`**—通过将模拟表示分解为片段将其转换为数字表示的行为。

**`有向图（digraph）`**—一种图数据结构，其中每条边都有特定的方向。

**`维数（dimension）`**—特定数组的索引级别数。

**`直接递归（direct recursion）`**—方法调用自身的过程。另请参阅间接递归（`indirect recursion`）。

**`禁用（disable）`**—使图形用户界面组件不活动，使其不能被使用。禁用组件呈灰色以指示其禁用状态。另请参阅启用（`enable`）。

**`DNS`**—参见域名系统（`Domain Name System`）。

**`do`**—Java保留字，表示一种重复构造。`do`语句执行一次或多次。另请参阅 `for`、`while`。

**`文档（documentation）`**—有关程序的补充信息，包括程序源代码中的注释和打印的报告（如用户指南）。

**`域名（domain name）`**—互联网地址中指定计算机所属组织的部分。

**`域名系统（Domain Name System，DNS）`**—使用域服务器将互联网地址转换为IP地址的软件。

**`域服务器（domain server）`**—维护互联网地址及其对应IP地址列表的文件服务器。

**`double`**—Java保留字，表示一种基本浮点数值类型，使用IEEE 754格式的64位存储。

**`双向链表（doubly linked list）`**—一种链表，每个节点有两个引用：一个引用列表中的下一个节点，一个引用列表中的上一个节点。

**`动态绑定（dynamic binding）`**—在运行时将标识符与其定义关联的过程。另请参阅绑定（`binding`）。

**`动态数据结构（dynamic data structure）`**—使用引用链接的一组对象，可在程序执行期间根据需要修改。

**`编辑器（editor）`**—一种软件工具，允许用户在计算机上输入和存储字符文件。程序员常用其输入程序的源代码。
