
> **警告：** 过去，有人建议将所有 JAR 文件放入 `jre/lib/ext` 目录，以完全绕过类路径。该机制在 Java 9 中已过时，但这一建议从来都不是好主意。当早已被遗忘的类从扩展目录重新加载时，很容易造成混乱。

> **注意：** 从 Java 9 开始，也可以从模块路径加载类。我们将在卷 II 的第 9 章讨论模块和模块路径。

## 4.8 JAR 文件

当你打包应用程序时，你希望给用户一个单独的文件，而不是一个装满类文件的目录结构。Java 归档（JAR）文件正是为此目的而设计的。JAR 文件既可以包含类文件，也可以包含其他文件类型，如图像和声音文件。此外，JAR 文件使用熟悉的 ZIP 压缩格式进行压缩。

### 4.8.1 创建 JAR 文件

使用 jar 工具来创建 JAR 文件。（在默认的 JDK 安装中，它位于 jdk/bin 目录。）创建新 JAR 文件最常用的命令使用以下语法：

```
jar cvf jarFileName file1 file2 ...
```

例如：

```
jar cvf CalculatorClasses.jar *.class icon.gif
```

通常，jar 命令的格式如下：

```
jar options file1 file2 ...
```

表 4.2 列出了 jar 程序的所有选项。它们类似于 UNIX tar 命令的选项。

可以将应用程序和代码库打包到 JAR 文件中。例如，如果要在 Java 程序中发送邮件，可以使用打包在 javax.mail.jar 文件中的库。

**表 4.2** jar 程序选项

| 选项 | 描述 |
|---|---|
| `c` | 创建新的或空的归档并向其中添加文件。如果指定的文件名中有目录，jar 程序会递归处理它们。 |
| `C` | 临时更改目录。例如，`jar cvf jarFileName.jar -C classes *.class` 会切换到 classes 子目录以添加类文件。 |
| `e` | 在清单中创建入口点（参见 4.8.3 节）。 |
| `f` | 将 JAR 文件名指定为第二个命令行参数。如果缺少此参数，jar 将在创建 JAR 文件时将结果写入标准输出，或在提取或列出 JAR 文件时从标准输入读取。 |
| `i` | 创建索引文件（用于加速大型归档中的查找）。 |
| `m` | 向 JAR 文件添加清单。清单是归档内容和来源的描述。每个归档都有默认清单，但如果要验证归档内容，也可以提供自己的清单。 |
| `M` | 不为条目创建清单文件。 |
| `t` | 显示目录列表。 |
| `u` | 更新现有的 JAR 文件。 |
| `v` | 生成详细输出。 |
| `x` | 提取文件。如果提供一个或多个文件名，则只提取这些文件。否则，提取所有文件。 |
| `0` | 存储而不进行 ZIP 压缩。 |

### 4.8.2 清单

除了类文件、图像和其他资源之外，每个 JAR 文件还包含一个描述归档特殊功能的清单文件。

清单文件名为 MANIFEST.MF，位于 JAR 文件特殊的 META-INF 子目录中。最小合法清单非常简单——只有

```
Manifest-Version: 1.0
```

复杂的清单可以有更多条目。清单条目被分组为若干部分。清单中的第一部分称为*主部分*。它适用于整个 JAR 文件。后续条目可以指定命名实体的属性，如单个文件、包或 URL。这些条目必须以 `Name` 条目开头。各部分之间用空行分隔。例如：

```
Manifest-Version: 1.0
lines describing this archive

Name: Woozle.class
lines describing this file
Name: com/mycompany/mypkg/
lines describing this package
```

要编辑清单，请将想要添加到清单中的行放入一个文本文件。然后运行

```
jar cfm jarFile manifestFileName ...
```

例如，要创建一个带清单的新 JAR 文件，运行

```
jar cfm MyArchive.jar manifest.mf com/mycompany/mypkg/*.class
```

要更新现有 JAR 文件的清单，请将追加内容放入一个文本文件，并使用如下命令

```
jar ufm MyArchive.jar manifest-additions.mf
```

> **注意：** 有关 JAR 和清单文件格式的更多信息，请参阅 https://docs.oracle.com/javase/10/docs/specs/jar/jar.html

### 4.8.3 可执行 JAR 文件

可以使用 `jar` 命令的 `e` 选项来指定程序的*入口点*——即通常在调用 `java` 程序启动器时指定的类：

```
jar cve MyProgram.jar com.mycompany.mypkg.MainAppClass files to add
```

或者，可以在清单中指定程序的*主类*，包括以下形式的语句

```
Main-Class: com.mycompany.mypkg.MainAppClass
```

不要在主类名后添加 `.class` 扩展名。

![](img/127bccebb2cfadea3f02579edaad63c3_221_0.png)

> **警告：** 清单的最后一行必须以换行符结尾。否则，清单将无法被正确读取。常见错误是生成了一个只包含 Main-Class 行而没有行终止符的文本文件。

使用任何一种方法，用户都可以简单地通过以下方式启动程序

```
java -jar MyProgram.jar
```

根据操作系统配置，用户甚至可以通过双击 JAR 文件图标来启动应用程序。以下是各种操作系统的行为：

- 在 Windows 上，Java 运行时安装程序会为“.jar”扩展名创建文件关联，使用 `java -jar` 命令启动该文件。（与 `java` 命令不同，`javaw` 命令不会打开 shell 窗口。）
- 在 Mac OS X 上，操作系统会识别“.jar”文件扩展名，并在双击 JAR 文件时执行 Java 程序。

然而，JAR 文件中的 Java 程序没有原生应用程序那样的体验。在 Windows 上，可以使用第三方包装工具将 JAR 文件转换为 Windows 可执行文件。包装器是一种带有熟悉的 .exe 扩展名的 Windows 程序，用于定位并启动 Java 虚拟机（JVM），或者在找不到 JVM 时告诉用户该怎么做。有许多商业和开源产品，例如 Launch4J (http://launch4j.sourceforge.net) 和 IzPack (http://izpack.org)。

### 4.8.4 多版本 JAR 文件

随着模块的引入和包的强封装，一些以前可访问的内部 API 不再可用。例如，JavaFX 8 有一个内部类 `com.sun.javafx.css.CssParser`。如果你使用它来解析样式表，那么你会发现程序不再编译。补救措施很简单——改用 `javafx.css.CssParser`，该解析器在 Java 9 中可用。但现在你遇到了一个问题。你需要为 Java 8 和 Java 9 用户分发不同的应用程序，或者需要借助类加载和反射的技巧。

为了解决这类问题，Java 9 引入了*多版本 JAR*，它可以包含不同 Java 版本的类文件。

为了向后兼容，额外的类文件放在 `META-INF/versions` 目录中：

> **注意：** 诸如 javap 之类的工具尚未经过改造以处理多版本 JAR 文件。

如果调用

```
javap -classpath MyProgram.jar Application.class
```

你会得到该类的基础版本（毕竟它应该具有与较新版本相同的公共 API）。如果必须查看较新版本，请调用

```
javap -classpath MyProgram.jar!/META-INF/versions/9/Application.class
```

### 4.8.5 关于命令行选项的说明

Java 开发工具包中命令的选项传统上使用单个短划线后跟多字母选项名称，例如

```
java -jar ...
javac -Xlint:unchecked -classpath ...
```

例外是 `jar` 命令，它遵循 `tar` 命令的经典选项格式，不带短划线：

```
jar cvf ...
```

从 Java 9 开始，Java 工具正转向更常见的选项格式，即多字母选项名称前加双短划线，并为常见选项提供单字母快捷方式。例如，Linux `ls` 命令可以使用“human-readable”选项调用，如下所示

```
ls --human-readable
```

或

```
ls -h
```

从 Java 9 开始，可以使用 `--version` 代替 `-version`，使用 `--class-path` 代替 `-classpath`。正如你将在卷 II 的第 9 章中看到的，`--module-path` 选项有快捷方式 `-p`。

可以在 http://openjdk.java.net/jeps/293 的 JEP 293 增强请求中找到详细信息。作为此次清理的一部分，作者还建议标准化选项参数。带有 `--` 和多字母的选项参数可以用空白或 `=` 号分隔：

```
javac --class-path /home/user/classdir ...
```

或

```
javac --class-path=/home/user/classdir ...
```
