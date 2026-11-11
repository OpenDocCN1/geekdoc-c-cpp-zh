
Charset.defaultCharset()。在 Windows 上使用 `cmd` shell 时，这一点尤其明显。在美国版本中，命令 shell 使用老旧的 `IBM437` 编码，该编码起源于 1982 年的 IBM 个人计算机。没有官方 API 可用于揭示该信息。`Charset.defaultCharset()` 方法将返回 `Windows-1252` 字符集，二者差别很大。例如，欧元符号存在于 `Windows-1252` 中，但不存在于 `IBM437` 中。当你调用

```
System.out.println("100 €");
```

控制台将显示

```
100 ?
```

你可以建议用户切换控制台的字符编码。在 Windows 中，可通过 `chcp` 命令实现。例如，

```
chcp 1252
```

将控制台更改为 `Windows-1252` 代码页。

当然，理想情况下，用户应将控制台切换为 UTF-8。在 Windows 中，命令为

```
chcp 65001
```

不幸的是，仅此还不足以让 Java 在控制台中使用 UTF-8。还需要通过非官方的 `file.encoding` 系统属性设置平台编码：

```
java -Dfile.encoding=UTF-8 MyProg
```

### 7.7.4 日志文件

当 `java.util.logging` 库的日志消息发送到控制台时，会使用控制台编码写入。你已在前一节了解了如何控制这一点。但是，文件中的日志消息使用 `FileHandler`，它默认使用平台编码。

要将编码更改为 UTF-8，需要更改日志管理器设置。在日志配置文件中，设置

```
java.util.logging.FileHandler.encoding=UTF-8
```

### 7.7.5 UTF-8 字节顺序标记

正如已经提到的，只要可以，对文本文件使用 UTF-8 是个好主意。如果你的应用程序必须读取由其他程序创建的 UTF-8 文本文件，你会遇到另一个潜在问题。将“字节顺序标记”字符 U+FEFF 作为文件第一个字符是完全合法的。在 UTF-16 编码中，每个代码单元都是两字节量，字节顺序标记会告诉读取器该文件使用“大端”还是“小端”字节顺序。UTF-8 是一种单字节编码，因此无需指定字节顺序。但如果文件以字节 0xEF 0xBB 0xBF（U+FEFF 的 UTF-8 编码）开头，就强烈表明它使用 UTF-8。因此，Unicode 标准鼓励这种做法。任何读取器都应丢弃开头的字节顺序标记。

美中不足的是，Oracle Java 实现固执地拒绝遵循 Unicode 标准，理由是可能存在兼容性问题。这意味着你作为程序员必须做平台不会做的事情。当你读取文本文件并在开头遇到 \uFEFF 时，忽略它。

> **警告：** 不幸的是，JDK 实现者并未遵循这一建议。当你将一个以字节顺序标记开头的有效 UTF-8 源文件传给 `javac` 编译器时，编译会失败，并显示错误消息“illegal character: \65279”。

### 7.7.6 源文件的字符编码

你作为程序员，需要与 Java 编译器通信——而你是通过本地系统上的工具来完成这件事的。例如，你可以使用中文版记事本来编写 Java 源代码文件。生成的源代码文件不具*可移植性*，因为它们使用本地字符编码（GB 或 Big5，取决于你使用哪种中文操作系统）。只有编译后的类文件是可移植的——它们会自动对标识符和字符串使用“修改后的 UTF-8”编码。这意味着当程序编译和运行时，涉及三种字符编码：

- 源文件：平台编码
- 类文件：修改后的 UTF-8
- 虚拟机：UTF-16

（关于修改后的 UTF-8 和 UTF-16 格式的定义，见第 2 章。）

> **提示：** 你可以使用 `-encoding` 标志指定源文件的字符编码，例如，
>
> ```
> javac -encoding UTF-8 MyFile.java
> ```

要使源文件可移植，请限制自己只使用纯 ASCII 编码。也就是说，将所有非 ASCII 字符更改为其等效的 Unicode 转义。例如，不要使用字符串 "Häuse"，而应使用 "H\u00E4use"。JDK 包含一个实用工具 native2ascii，你可以用它把本地字符编码转换为纯 ASCII。该工具只是将输入中的每个非 ASCII 字符替换为 \u 后跟该 Unicode 值的四位十六进制数字。要使用 native2ascii 程序，请提供输入和输出文件名。

```
native2ascii Myfile.java Myfile.temp
```

你可以使用 -reverse 选项进行反向转换：

```
native2ascii -reverse Myfile.temp Myfile.java
```

你可以使用 -encoding 选项指定另一种编码。

```
native2ascii -encoding UTF-8 Myfile.java Myfile.temp
```

## 7.8 资源包

本地化应用程序时，你可能会面对数量多得令人望而生畏的消息字符串、按钮标签等，它们都需要翻译。为使这项任务可行，你会希望将消息字符串定义在外部位置，通常称为*资源*。执行翻译的人员随后只需编辑资源文件，而无需改动程序的源代码。

在 Java 中，你可以使用属性文件来指定字符串资源，也可以为其他类型的资源实现类。

**注意：** Java 技术资源与 Windows 或 Macintosh 资源不同。Macintosh 或 Windows 可执行程序将菜单、对话框、图标和消息等资源存储在独立于程序代码的区域中。资源编辑器可以检查和更新这些资源，而不会影响程序代码。

**注意：** 第 I 卷第 13 章描述了 JAR 文件资源的概念，借此可以将数据文件、声音和图像放入 JAR 文件。`Class` 类的 `getResource` 方法会找到该文件、打开它，并返回指向该资源的 URL。通过将文件放入 JAR 文件，你把查找文件的工作交给了类加载器，而类加载器已经知道如何定位 JAR 文件中的项。但是，该机制不支持区域设置。

### 7.8.1 定位资源包

本地化应用程序时，你会生成一组资源包。每个包都是一个属性文件或一个类，用于描述特定于区域设置的项（例如消息、标签等）。对于每个包，你必须为想要支持的所有区域设置提供版本。

这些包需要使用特定的命名约定。例如，德国特定的资源放入文件 *bundleName_de_DE*，而所有德语国家共享的资源放入 *bundleName_de*。一般而言，所有国家/地区特定的资源使用 *bundleName_language_country*，所有语言特定的资源使用 *bundleName_language*。最后，作为回退，你可以将默认值放入不带任何后缀的文件中。

要加载资源包，请使用以下命令

```
ResourceBundle currentResources = ResourceBundle.getBundle(bundleName, currentLocale);
```

getBundle 方法会尝试加载按语言和国家/地区与当前区域设置匹配的资源包。如果未成功，则依次去掉国家/地区和语言。然后对默认区域设置应用同样的搜索，最后查询默认资源包文件。如果连这次尝试也失败，该方法会抛出 MissingResourceException。

也就是说，getBundle 方法会尝试加载以下资源包：

- *bundleName_currentLocaleLanguage_currentLocaleCountry*
- *bundleName_currentLocaleLanguage*
- *bundleName_currentLocaleLanguage_defaultLocaleCountry*
- *bundleName_defaultLocaleLanguage*
- *bundleName*

一旦 getBundle 方法定位到一个资源包（例如 *bundleName_de_DE*），它仍会继续查找 *bundleName_de* 和 *bundleName*。如果这些资源包存在，它们会在资源层次结构中成为 *bundleName_de_DE* 资源包的父级。之后，在查找资源时，如果当前资源包中查找未成功，就会搜索父级。也就是说，如果在 *bundleName_de_DE* 中未找到某个特定资源，那么也会查询 *bundleName_de* 和 *bundleName*。

这显然是一项非常有用的服务——而且是一项手工编程会很繁琐的服务。Java 编程语言的资源包机制
