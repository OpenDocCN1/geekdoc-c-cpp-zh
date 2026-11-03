
C 被描述为就像“驾驶一辆没有刹车的保时捷”——而且由于它也很快，这可能令人兴奋不已。当速度和效率至关重要时，C 往往是唯一的选择。

C 被称为“危险”的语言，因为它允许对机器进行底层访问，但这种可怕之处正是你需要理解的，因为它会让你对你将使用的高级语言心存敬畏。

许多嵌入式微型系统仍然全部用 C 编写，而用于监控和过程控制的隐形互联网的机器对机器世界也经常使用 C。

希望这一系列理由能引导你认识现代集成开发环境（IDE）日益增长的复杂性，例如 Developer Studio、Netbeans 和 Eclipse；这些 IDE 让学生产生一种错觉，以为自己知道在做什么，但实际上却造成了混淆。

我的目标是让学生建立信心并快速上手，而不必经历配置复杂工具链带来的种种噩梦。它本质上也是一种免许可证的方法，并且可在任何平台上运行。

有了对实际发生情况的基本理解，你就可以继续使用并真正理解职业生涯中需要的任何工具。

为了给人一种在做真实、有用且与时俱进的事情的感觉，重点在于开发可见且实际上具有专业质量的 Web 服务器和客户端项目并将其上线，使用：

-   Apache Web 服务器和开发库。
-   C 语言 CGI 程序（使用“make”实用程序进行 C 编程）。
-   C 语言 Apache 模块。
-   带有 C 客户端库接口的 MySQL 服务器。
-   带有 C 接口的 GD 图形库。
-   附带使用 CSS、(X)HTML、XML、JavaScript、Ajax。

本课程是为英国伦敦金斯顿大学计算机科学专业一、二年级学生设计的，并由他们进行了实验室测试。

## 设置你的系统

本书假定你使用的是 Linux 操作系统，并采用 KDE3.5、KDE4 或 Gnome 桌面。书中包含针对 Ubuntu（以及 Kubuntu）和 OpenSuse 11 的具体说明。

如果你使用 KDE 桌面，你将拥有 Konqueror 或 Dolphin 作为文件管理器，以及 kate 或 kedit 作为编辑器。

在 Gnome 中，你可能会使用 Nautilus 和 gedit。

你需要熟悉以“超级用户”身份执行某些操作的理念，这样你才有权限复制或编辑某些文件。通常的做法是在 Linux 命令前加上“sudo”并提供密码，如下例所示：

```
sudo cp hello3 /srv/www/cgi-bin/hello3
```

该命令将文件“hello3”复制到 Apache 服务器存放公共网关接口（CGI）程序的区域。

在 KDE 中，“kdesu konqueror”会以超级用户身份打开文件管理器。

在 Gnome 中，“gnomesu nautilus”会以超级用户身份打开文件管理器。

你需要安装以下软件包：

| 软件包 | Ubuntu | Open Suse |
|---|---|---|
| C 开发库 | build-essential | 基础开发（模式） |
| Apache Web 服务器 | apache2 | Web 和 LAMP 服务器（模式） |
| Apache 开发库 | apache2-prefork-dev | apache2-devel |
| MySQL 服务器、客户端和开发库 | mysql-server libmysqlclient15-dev | libmysqlclient-devel |
| GD 和开发库 | libgd2-xpm | gd<br>gd-devel |

在整本书中，你会看到对文件夹 **cgi-bin** 的引用。该文件夹的位置会因 Linux 发行版而异。默认情况下，用于 Web 程序的此文件夹是：

-   OpenSuse：**/srv/www/cgi-bin**
-   Ubuntu：**/usr/lib/cgi-bin**

要把程序放到那里，你需要超级用户权限，因此更好的做法可能是在你自己的 `home/*****/public_html/cgi-bin` 目录中创建一个文件夹，并更改 Apache 配置文件（OpenSuse）`/etc/apache2/default-server.conf` 或（Ubuntu）`/etc/apache2/default-server.conf` 中的 **ScriptAlias** 及相关 **Directory** 引用。

## 你改变世界的机会

在爱立信，我们根深蒂固地相信，我们每天所做的创新能够产生深远影响，让世界对人们、商业和社会变得更美好。加入我们吧。

在德国，我们特别寻找毕业生担任集成工程师，负责：

-   无线接入和 IP 网络
-   IMS 和 IPTV

我们期待收到你的申请！如需申请以及查看所有当前职位空缺，请访问我们的网页：www.ericsson.com/careers

![](img/a0cbda189e54d8cb1121c7e151992506_11_0.png)

## 1. 第一章：Hello World

### 1.1 Hello 程序 1

使用文件管理器（在 KDE 中为 Konqueror，在 Gnome 中为 Nautilus），在你的主目录中某处创建一个新目录，名称要适合本书中的所有示例，也许可以叫“Programming_In_Linux”，名称中不要包含任何空格。

打开一个编辑器（在 KDE 中为 kate，在 Gnome 中为 gedit），输入（或从提供的源代码 zip 压缩包中复制）以下内容：

```
/*
C Programming in Linux (c) David Haskins 2008
chapter1_1.c
*/

#include <stdio.h>

int main(int argc, char *argv[])
{
    printf("Hello, you are learning C!!\n");
    return 0;
}
```

将文本保存为 chapter1_1.c，放在你在主目录中创建的新文件夹中。

打开终端窗口并输入：`gcc -o hello chapter1_1.c`，将程序编译成可执行的形式。

现在输入 `ls -l` 列出该目录中所有文件的详细信息。你应该会看到 chapter1_1.c 在那里，以及一个名为 `hello` 的文件，它就是刚刚编写的编译后的 C 程序。

现在输入：`./hello` 来执行或运行该程序，它应该返回文本：

"Hello, you are learning C!!"

如果这成功了，恭喜你，你现在是一名程序员了！

### 程序剖析：

`/* ... */` 中的部分是注释，不会被编译，仅供参考和说明。

`#include` 部分告诉编译器需要哪些系统库，以及此程序引用了哪些头文件。在我们的例子中使用了 `printf`，它定义在 stdio.h 头文件中。

`int main(int argc, char *argv[])` 部分是实际程序的开始。这是一个入口点，大多数 C 程序都有一个 main 函数。

`int argc` 是函数 `main` 的一个参数，它是一个整数计数，表示在 `char *argv[]`（指向字符串的指针列表）中传入的字符串参数数量，这些参数可能在我们运行程序时从命令行传入。

指向某物的指针是为这类数据类型指定的一个内存地址名称。我们可以有一个指向整数的指针：`int *iptr`，或者一个指向浮点数的指针：`float *fPtr`。任何事物的列表都用 `[]` 描述，如果我们确切知道这个列表有多大，我们可以将其声明为 `[200]`。在本例中，我们知道第二个参数是一个指向字符串的指针列表。

花括号中的所有其他内容都是 main 函数，而在本例中，整个程序以多行表示。

每一行或每条语句都以分号 `;` 结尾。

我们有像 `printf(...)` 这样的函数调用，它是对定义在头文件 stdio.h 中的标准输入/输出库的调用。

在程序末尾，`return 0` 通过向系统返回零来结束程序。

返回值通常用于在程序未能正确运行时指示成功或状态。

### 1.2 Hello 程序 2

进一步扩展这个示例，检查程序开头处入口点函数的声明：`int main(int argc, char *argv[])`。

用通俗的话说，这意味着：
