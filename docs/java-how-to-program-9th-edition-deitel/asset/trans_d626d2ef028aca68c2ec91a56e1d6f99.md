

University of Akron), Sue McFarland Metzger (Villanova University), Shyamal Mitra (The University of Texas at Austin), Peter Pilgrim (Consultant), Manjeet Rege, Ph.D. (Rochester Institute of Technology), Manfred Riem (Java Champion, Consultant, Robert Half), Simon Ritter (Oracle), Susan Rodger (Duke University), Amr Sabry (Indiana University), José Antonio González Seco (Parliament of Andalusia), Sang Shin (Sun Microsystems), S. Sivakumar (Astra Infotech Private Limited), Raghavan “Rags” Srinivas (Intuit), Monica Sweat (Georgia Tech), Vinod Varma (Astra Infotech Private Limited) and Alexander Zuev (Sun Microsystems).

好吧，就这些了！在阅读本书时，我们非常欢迎您提出评论、批评、更正和改进建议。请将所有通信寄至：

```
deitel@deitel.com
```

我们会及时回复。希望您能喜欢使用《Java 如何编程，9/e》。祝好运！

Paul and Harvey Deitel

## 关于作者

Paul J. Deitel，Deitel & Associates, Inc. 的首席执行官兼首席技术官，是 MIT 的毕业生，在那里学习信息技术。通过 Deitel & Associates, Inc.，他已为包括 Cisco、IBM、Siemens、Sun Microsystems、Dell、Lucent Technologies、Fidelity、NASA 肯尼迪航天中心、国家严重风暴实验室、白沙导弹靶场、Rogue Wave Software、Boeing、SunGard Higher Education、Stratus、Cambridge Technology Partners、One Wave、Hyperion Software、Adra Systems、Entergy、CableData Systems、Nortel Networks、Puma、iRobot、Invensys 等在内的众多行业客户提供了数百门 Java、C++、C、C#、Visual Basic 和 Internet 编程课程。他与合著者 Dr. Harvey M. Deitel 共同是全球最畅销的编程语言教材作者。

Dr. Harvey M. Deitel，Deitel & Associates, Inc. 的董事长兼首席战略官，在计算机领域拥有 50 年经验。Deitel 博士获得 MIT 的理学学士和理学硕士学位，以及波士顿大学的博士学位。他拥有丰富的大学教学经验，包括获得终身教职并在创立 Deitel & Associates, Inc. 与其子 Paul J. Deitel 之前担任波士顿学院计算机科学系系主任。他与 Paul 共同撰写了数十本图书和 LiveLessons 多媒体套装，并仍在撰写更多作品。Deitel 的教材在国际上享有盛誉，已被翻译成日语、德语、俄语、中文、西班牙语、韩语、法语、波兰语、意大利语、葡萄牙语、希腊语、乌尔都语和土耳其语。Deitel 博士已为众多大型企业、学术机构、政府组织和军队举办了数百场专业编程研讨会。

## Deitel & Associates, Inc. 的企业培训

Deitel & Associates, Inc. 是一家国际公认的企业培训和著作文组织。该公司在全球客户现场提供讲师主导的课程，涵盖主要编程语言和平台，如 Java™、C++、Visual C++®、C、Visual C#®、Visual Basic®、XML®、Python®、面向对象技术、Internet 和 Web 编程、Android™ 和 iPhone® 应用开发，以及不断增长的其他编程和软件开发课程。Deitel & Associates 的创始人，

## 开始之前

本节包含您在使用本书前应查阅的信息以及确保计算机为使用本书做好准备的说明。我们会将更新（如有）发布到本书网站上的“开始之前”部分：

```
www.deitel.com/books/jhtp9/
```

### 字体和命名约定

我们使用字体来区分屏幕组件（如菜单名称和菜单项）与 Java 代码或命令。我们的约定是使用无衬线粗体 Helvetica 字体强调屏幕组件（例如 File 菜单），并使用无衬线 Lucida 字体强调 Java 代码和命令（例如 System.out.println()）。

### 书中使用的软件

本书所需的所有软件均可免费从网络下载。

### Java SE 软件开发工具包 (JDK) 6 和 7

我们使用免费的 Java Standard Edition Development Kit (JDK) 6 编写了《Java 如何编程，9/e》中的大部分示例，可从以下位置获取：

```
www.oracle.com/technetwork/java/javase/downloads/index.html
```

对于可选的 Java SE 7 模块，我们使用了 OpenJDK 的 JDK 7 早期访问版本，可从以下位置获取：

```
dlc.sun.com.edgesuite.net/jdk7/binaries-/index.html
```

### Java DB、MySQL 和 MySQL Connector/J

在第 28 章中，我们使用 Java DB 和 MySQL Community Edition 数据库管理系统。Java DB 是 JDK 安装的一部分。截至本书撰写时，JDK 的 64 位安装程序未能正确安装 Java DB。如果您使用的是 64 位版本的 Java，您可能需要单独安装 Java DB。您可以从以下位置下载 Java DB：

```
www.oracle.com/technetwork/java/javadb/downloads/index.html
```

截至本书撰写时，MySQL Community Edition 的最新版本为 5.5.8。要在 Windows、Linux 或 Mac OS X 上安装 MySQL Community Edition，请参阅您平台的安装概述：

- Windows: dev.mysql.com/doc/refman/5.5/en/windows-installation.html
- Linux: dev.mysql.com/doc/refman/5.5/en/linux-installation-rpm.html
- Mac OS X: dev.mysql.com/doc/refman/5.5/en/macosx-installation.html

请仔细按照您平台的下载和安装说明进行操作。下载内容可在以下位置获取：

```
dev.mysql.com/downloads/mysql/
```

您还需要安装 MySQL Connector/J（J 代表 Java），它允许程序使用 JDBC 与 MySQL 交互。MySQL Connector/J 可从以下位置下载

```
dev.mysql.com/downloads/connector/j/
```

截至本书撰写时，MySQL Connector/J 当前的通用可用版本为 5.1.14。Connector/J 的文档位于

```
dev.mysql.com/doc/refman/5.5/en/connector-j.html
```

要安装 MySQL Connector/J，请仔细按照以下安装说明操作：

```
dev.mysql.com/doc/refman/5.5/en/connector-j-installing.html
```

我们不建议修改系统的 CLASSPATH 环境变量，该变量在安装说明中有所讨论。相反，我们将向您展示如何通过在执行应用程序时将其指定为命令行选项来使用 MySQL Connector/J。

### Java IDE 资源工具包

您的讲师可能已通过您所在学院的书店订购了《Java 如何编程，9/e》的 Value Pack 版本，该版本捆绑了 Java IDE 资源工具包。此工具包包含 Windows® 版 Java™ SE Development Kit 6 (JDK 6)、Windows® 版 Eclipse™ IDE、NetBeans™ IDE、jGRASP™ IDE、DrJava IDE、BlueJ IDE 和 Windows® 版 TextPad® 文本编辑器的 CD 或 DVD 版本。这些 IDE 的免费版本也可以从以下网站下载：

- JDK 6: www.oracle.com/technetwork/java/javase/downloads/
- Eclipse IDE: eclipse.org/downloads/
- NetBeans IDE: netbeans.org/downloads/
- jGRASP IDE: spider.eng.auburn.edu/user-cgi/grasp/grasp.pl?;dl=download_jgrasp.html
- DrJava IDE: drjava.org
- BlueJ IDE: www.bluej.org/download/download.html
- TextPad Text Editor (evaluation version): www.textpad.com/download/

### 获取代码示例

《Java 如何编程，9/e》的示例可在以下位置下载

```
www.deitel.com/books/jhtp9/
```

如果您尚未在我们的网站注册，请访问 www.deitel.com 并点击我们标志下方左上角的 Register 链接。填写您的信息。注册免费，我们不会与任何人分享您的信息。我们仅发送账户管理邮件，除非您另行注册我们的免费 Deitel® Buzz Online 电子邮件通讯，网址为 www.deitel.com/newsletter/subscribe.html。注册网站后，您将收到一封包含验证代码的确认邮件。*点击确认邮件中的链接完成注册。* 配置您的电子邮件客户端以允许来自 deitel.com 的邮件，以确保确认邮件不会被过滤为垃圾邮件。

接下来，访问 www.deitel.com 并使用我们标志下方左上角的 Login 链接登录。转到 www.deitel.com/books/jhtp9/。您将在 **Download Code Examples and Other Premium Content for Registered Users** 标题下找到下载示例的链接。记下您选择在计算机上保存 ZIP 文件的位置。

我们假设示例位于您的计算机上的 C:\Examples。 使用 WinZip (www.winzip.com) 或操作系统的内置功能提取 Examples.zip 的内容。

### 设置 PATH 环境变量

您计算机上的 PATH 环境变量指定计算机在查找应用程序时搜索的目录，例如用于编译和运行 Java 应用程序的应用程序（分别称为 javac 和 java）。*请仔细按照您平台的 Java 安装说明操作，以确保正确设置 PATH 环境变量。*

如果您未正确设置 PATH 变量，在使用 JDK 的工具时，您将收到类似以下的消息：

```
'java' is not recognized as an internal or external command,
operable program or batch file.
```

在这种情况下，请返回设置 PATH 的安装说明并重新检查您的步骤。如果您下载了更新版本的 JDK，您可能需要在 PATH 变量中更改 JDK 安装目录的名称。

### 设置 CLASSPATH 环境变量

如果您尝试运行 Java 程序并收到类似以下的消息

```
Exception in thread "main" java.lang.NoClassDefFoundError: YourClass
```

则您的系统有一个必须修改的 CLASSPATH 环境变量。要修复上述错误，请按照设置 PATH 环境变量的步骤找到 CLASSPATH 变量，然后编辑变量的值以包含本地目录——通常表示为点 (.)。在 Windows 上添加

```
.;
```

在 CLASSPATH 值开头（前后无空格）。在其他平台上，用适当的路径分隔符字符替换分号——通常是冒号 (:)

### Java 的 Nimbus 外观

Java 捆绑了一个优雅的跨平台外观，称为 Nimbus。对于具有图形用户界面的程序，我们已将系统配置为将 Nimbus 作为默认外观。

