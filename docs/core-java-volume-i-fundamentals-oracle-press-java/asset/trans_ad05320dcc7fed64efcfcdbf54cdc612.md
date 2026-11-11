
根据操作系统配置，用户甚至可以通过双击 JAR 文件图标来启动应用程序。以下是各种操作系统的行为：

- 在 Windows 上，Java 运行时安装程序会为“.jar”扩展名创建文件关联，使用 `javaw -jar` 命令启动该文件。（与 `java` 命令不同，`javaw` 命令不会打开 shell 窗口。）
- 在 Mac OS X 上，操作系统会识别“.jar”文件扩展名，并在你双击 JAR 文件时执行 Java 程序。

然而，JAR 文件中的 Java 程序并不具备原生应用程序那样的体验。在 Windows 上，你可以使用第三方包装实用程序将 JAR 文件转换为 Windows 可执行文件。包装器是一个带有熟悉的 `.exe` 扩展名的 Windows 程序，它会定位并启动 Java 虚拟机（JVM），或者在找不到 JVM 时告诉用户该怎么做。有许多商业和开源产品，例如 Launch4J（http://launch4j.sourceforge.net）和 IzPack（http://izpack.org）。

### 4.9.4 多版本 JAR 文件

随着模块和包的强封装机制的引入，一些以前可访问的内部 API 不再可用。这可能需要库提供者为不同的 Java 版本分发不同的代码。Java 9 为此引入了*多版本 JAR*。

为了向后兼容，特定于版本的类文件放置在

从 Java 9 开始，`-d` 选项会在目录不存在时创建该目录。

`--release` 标志也是 Java 9 新增的。在较旧版本中，你需要使用 `-source`、`-target` 和 `-bootclasspath` 标志。JDK 现在附带 API 前两个版本的符号文件。在 Java 9 中，你可以将 `--release` 设置为 9、8 或 7 进行编译。

多版本 JAR 并非用于程序或库的不同版本。所有类的公共 API 在两个版本中都应相同。多版本 JAR 的唯一目的是使你的程序或库的特定版本能够与多个 JDK 版本配合工作。如果你添加功能或更改 API，则应改为提供新版本的 JAR。

> **注意：**
>
> `javap` 等工具并未经过改造以处理多版本 JAR 文件。如果你调用
>
> ```text
> javap -classpath MyProgram.jar Application.class
> ```
>
> 你会得到该类的基准版本（毕竟，它应当与较新版本具有相同的公共 API）。如果你必须查看较新版本，请调用
>
> ```text
> javap -classpath MyProgram.jar!/META-INF/versions/9/Application.class
> ```

### 4.9.5 关于命令行选项的说明

Java 开发工具包中命令的选项传统上使用单破折号后跟多字母选项名，例如

单字母选项的参数可以用空白分隔，也可以直接跟在选项后面：

```text
javac -p moduledir . . .
```

或

```text
javac -pmoduledir . . .
```

![](img/0e7b74ef51a065c077b42cd87b362288_305_0.png)

> **警告：**
>
> 后者目前不起作用，而且总体上也似乎是个坏主意。如果模块目录恰好是参数或处理器，为什么要招致与遗留选项的冲突呢？

不带参数的单字母选项可以组合在一起：

```text
jar -cvf MyProgram.jar -e mypackage.MyProgram */*.class
```

![](img/0e7b74ef51a065c077b42cd87b362288_305_1.png)

> **警告：**
>
> 那目前不起作用，而且必然会导致混淆。假设 `javac` 增加了一个 `-c` 选项。`javac -cp` 是指 `javac -c -p`，还是遗留的 `-cp` 优先？

这造成了一团混乱，但愿随着时间推移会得到清理。尽管我很想摆脱古老的 jar 选项，但最好还是等到尘埃落定。不过，如果你想彻底现代化，可以放心使用 jar 命令的长选项：

```text
jar --create --verbose --file jarFileName file1 file2 . . .
```

如果不组合它们，单字母选项也可以使用：

```text
jar -c -v -f jarFileName file1 file2 . . .
```

## 4.10 文档注释

JDK 包含一个非常有用的工具，称为 `javadoc`，它可以从源文件生成 HTML 文档。事实上，第 3 章描述的在线 API 文档不过是对标准 Java 库的源代码运行 `javadoc` 的结果。

如果你向源代码中添加以特殊分隔符 `/**` 开头的注释，你也可以轻松生成看起来专业的文档。这是一种非常好的方法，因为它让你将代码和文档放在同一处。如果你将文档放入单独的文件，那么正如你可能知道的那样，代码和注释往往会随着时间推移而逐渐偏离。当文档注释与源代码位于同一文件时，更新两者并再次运行 `javadoc` 就是一件容易的事。

### 4.10.1 注释插入

`javadoc` 实用程序会提取以下各项的信息：

- 模块
- 包
- 公共类和接口
- 公共字段和受保护字段
- 公共和受保护的构造函数与方法

受保护特性在第 5 章介绍，接口在第 6 章介绍，模块在第 II 卷第 9 章介绍。

```java
/**
 * A {@code Card} object represents a playing card, such
 * as "Queen of Hearts". A card has a suit (Diamond, Heart,
 * Spade or Club) and a value (1 = Ace, 2 . . . 10, 11 = Jack,
 * 12 = Queen, 13 = King)
 */
public class Card
{
   . . .
}
```

**注意：**

没有必要在每一行前面添加 `*`。例如，以下注释同样有效：

```java
/**
   A <code>Card</code> object represents a playing card, such
   as "Queen of Hearts". A card has a suit (Diamond, Heart,
   Spade or Club) and a value (1 = Ace, 2 . . . 10, 11 = Jack,
   12 = Queen, 13 = King).
*/
```

然而，大多数 IDE 会自动提供星号，并在换行位置变化时重新排列它们。

### 4.10.3 方法注释

每个方法注释必须紧挨在它所描述的方法之前。除了通用标签外，你还可以使用以下标签：

- `@param` *变量描述*
  
  此标签向当前方法的“参数”部分添加一个条目。描述可以跨多行，并可以使用 HTML 标签。一个方法的所有 `@param` 标签必须放在一起。
- `@return` *描述*
  
  此标签向当前方法添加一个“返回值”部分。描述可以跨多行，并可以使用 HTML 标签。
- `@throws` *类描述*
  
  此标签添加一条说明，表示此方法可能抛出异常。异常是第 7 章的主题。

以下是一个方法注释的示例：

```java
/**
 * Raises the salary of an employee.
 * @param byPercent the percentage by which to raise the salary (e.g., 10 means 10%)
 * @return  the amount of the raise
 */
public double raiseSalary(double byPercent)
{
    double raise = salary * byPercent / 100;
    salary += raise;
    return raise;
}
```

### 4.10.4 字段注释

你只需要为公共字段编写文档——通常这意味着静态常量。例如：

```java
/**
 * The "Hearts" card suit
 */
public static final int HEARTS = 1;
```

### 4.10.5 通用注释

`@since` *文本* 标签会生成一个“since”条目。*文本* 可以是对引入此特性的版本的任意描述。例如，`@since 1.7.1`。

以下标签可用于类文档注释：

- `@author` *姓名*
  
  此标签会生成一个“author”条目。你可以有多个 `@author` 标签，每位作者一个。不必觉得必须使用此标签——你的版本控制系统在跟踪作者身份方面做得更彻底。
- `@version` *文本*
  
  此标签会生成一个“version”条目。*文本* 可以是对当前版本的任意描述。

你可以使用 `@see` 和 `@link` 标签，创建指向 javadoc 文档其他相关部分或外部文档的超链接。

`@see` *引用* 标签会在“另见”部分添加一个超链接。它可用于类和方法。此处，*引用* 可以是以下之一：

```text
package.class#feature label
<a href="..">label</a>
"text"
```

第一种情况最有用。你提供类、方法或变量的名称，javadoc 会插入指向文档的超链接。例如，

`@see com.horstmann.corejava.Employee#raiseSalary(double)`

会创建一个指向 `com.horstmann.corejava.Employee` 类中 `raiseSalary(double)` 方法的链接。你可以省略包名，或者同时省略包名和类名。这样，该特性将定位在当前包或类中。请注意，必须使用 `#` 而不是句点来分隔类与方法或变量名。Java
