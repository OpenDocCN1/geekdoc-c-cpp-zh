

```
/home/user/classdir:.:/home/user/archives/archive.jar
```

假设虚拟机搜索 `com.horstmann.corejava.Employee` 类的类文件。它首先在 Java API 类中查找。它在那里找不到该类文件，因此转向类路径。然后它查找以下文件：

- `/home/user/classdir/com/horstmann/corejava/Employee.class`
- 从当前目录开始的 `com/horstmann/corejava/Employee.class`
- `/home/user/archives/archive.jar` 中的 `com/horstmann/corejava/Employee.class`

编译器定位文件比虚拟机更困难。如果你引用一个类而未指定其包，编译器首先需要找出包含该类的包。它会查询所有 `import` 指令，作为该类的可能来源。例如，假设源文件包含指令

```
import java.util.*;
import com.horstmann.corejava.*;
```

并且源代码引用了一个类 `Employee`。然后编译器会尝试查找 `java.lang.Employee`（因为 `java.lang` 包总是默认导入）、`java.util.Employee`、`com.horstmann.corejava.Employee`，以及当前包中的 `Employee`。它会在类路径的所有位置搜索这些类中的*每一个*。如果找到多个类，则会出现编译时错误。（完全限定类名必须唯一，因此 `import` 语句的顺序无关紧要。）

编译器还会更进一步。它会查看*源文件*，以判断源文件是否比类文件更新。如果是，则自动重新编译源文件。回想一下，你只能从其他包中 `import` `public` 类。一个源文件只能包含一个 `public` 类，并且文件名和 `public` 类的名称必须匹配。因此，编译器可以轻松定位 `public` 类的源文件。但是，你可以从当前包中 `import` `nonpublic` 类。这些类可能定义在名称不同的源文件中。如果你从当前包导入一个类，编译器会搜索当前包的*所有*源文件，以确定哪一个定义了该类。

### 4.8.7 设置类路径

最好使用选项 `-classpath`（或 `-cp`，或从 Java 9 开始使用 `--class-path`）来指定类路径：

```
java -classpath /home/user/classdir:.:/home/user/archives/archive.jar MyProg
```

或者

```
java -classpath c:\classdir;.;c:\archives\archive.jar MyProg
```

整个命令必须输入在一行上。最好将如此长的命令行放入 shell 脚本或批处理文件中。

使用 `-classpath` 选项是设置类路径的首选方法。另一种方法是使用 `CLASSPATH` 环境变量。具体细节取决于你的 shell。使用 Bourne Again shell（bash）时，使用命令

```
export CLASSPATH=/home/user/classdir:.:/home/user/archives/archive.jar
```

使用 Windows shell 时，使用

```
set CLASSPATH=c:\classdir;.;c:\archives\archive.jar
```

类路径会一直设置到 shell 退出为止。

**警告：**

有些人建议永久设置 `CLASSPATH` 环境变量。这通常是个坏主意。人们会忘记这个全局设置，并在他们的类未正确加载时感到惊讶。一个特别应受谴责的例子是 Windows 中 Apple 的 QuickTime 安装程序。多年来，它全局设置 `CLASSPATH` 指向它需要的一个 JAR 文件，但没有将当前目录包含在类路径中。结果，无数 Java 程序员在程序编译成功却无法运行时被搞得心烦意乱。

**警告：**

过去，有些人建议通过将所有 JAR 文件放入 `jre/lib/ext` 目录来完全绕过类路径。这种机制在 Java 9 中已过时，而且它一直是个糟糕的建议。当早已遗忘的类从扩展目录加载时，很容易让人困惑。

**注意：**

从 Java 9 开始，类还可以从*模块路径*加载。模块和模块路径将在第二卷第 9 章讨论。

## 4.9 JAR 文件

当你打包应用程序时，你希望给用户一个单独的文件，而不是充满类文件的目录结构。Java 归档（JAR）文件就是为此目的而设计的。JAR 文件可以同时包含类文件和

| 选项 | 说明 |
|---|---|
| c | 创建新的或空的归档，并向其中添加文件。如果指定的任何文件名是目录，jar 程序会递归处理它们。 |
| C | 临时更改目录。例如，<br><br>`jar cvf jarfilename.jar -C classes *.class`<br><br>切换到 classes 子目录以添加类文件。 |
| e | 在清单中创建入口点（见 4.9.3 节）。 |
| f | 将 JAR 文件名指定为第二个命令行参数。如果缺少此参数，jar 在创建 JAR 文件时会将结果写入标准输出，在提取或列出 JAR 文件内容时从标准输入读取。 |
| i | 创建索引文件（用于加速大型归档中的查找）。 |
| m | 向 JAR 文件添加*清单*。清单是对归档内容和来源的描述。每个归档都有默认清单，但如果你想要验证归档内容，可以提供自己的清单。 |
| M | 不为条目创建清单文件。 |
| t | 显示目录表。 |
| u | 更新现有的 JAR 文件。 |
| v | 生成详细输出。 |
| x | 提取文件。如果你提供一个或多个文件名，则只提取这些文件。否则，提取所有文件。 |
| 0 | 存储时不使用 ZIP 压缩。 |

### 4.9.2 清单

除了类文件、图像和其他资源外，每个 JAR 文件还包含一个*清单*文件，用于描述该归档的特殊功能。

清单文件名为 `MANIFEST.MF`，位于 JAR 文件的特殊 `META-INF` 子目录中。最小的合法清单相当乏味——只有

```
Manifest-Version: 1.0
```

复杂的清单可以包含更多条目。清单条目被分组为节。清单中的第一节称为*主节*。它适用于整个 JAR 文件。后续条目可以指定命名实体的属性，例如单个文件、包或 URL。这些条目必须以 `Name` 条目开头。各节之间用空行分隔。例如：

```
Manifest-Version: 1.0
lines describing this archive

Name: Wozzle.class
lines describing this file

Name: com/mycompany/mypkg/
lines describing this package
```

要编辑清单，请将要添加到清单中的行放入一个文本文件。然后运行

```
jar cfm jarFileName manifestFileName . . .
```

例如，要创建一个带清单的新 JAR 文件，请运行

```
jar cfm MyArchive.jar manifest.mf com/mycompany/mypkg/*.class
```

要更新现有 JAR 文件的清单，请将新增内容放入一个文本文件，并使用如下命令

```
jar ufm MyArchive.jar manifest-additions.mf
```

![](img/0e7b74ef51a065c077b42cd87b362288_300_0.png)

**注意：**

有关 JAR 和清单文件格式的更多信息，请参见 [https://docs.oracle.com/javase/10/docs/specs/jar/jar.html](https://docs.oracle.com/javase/10/docs/specs/jar/jar.html)。

### 4.9.3 可执行 JAR 文件

你可以使用 `jar` 命令的 `e` 选项来指定程序的*入口点*——通常调用 java 程序启动器时要指定的类：

```
jar cvfe MyProgram.jar com.mycompany.mypkg.MainAppClass files to add
```

或者，你可以在清单中指定程序的*主类*，包括如下形式的语句

```
Main-Class: com.mycompany.mypkg.MainAppClass
```

不要在主类名中添加 `.class` 扩展名。

![](img/0e7b74ef51a065c077b42cd87b362288_300_1.png)

**警告：**

清单中的最后一行必须以换行符结尾。否则，清单将无法正确读取。一个常见错误是生成的文本文件只包含 `Main-Class` 行而没有行终止符。

使用任一方法，用户都可以简单地这样启动程序

```
java -jar MyProgram.jar
```

