
# Big Java：后期对象

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_0_0.png)

# WileyPLUS 是一个基于研究的在线环境，旨在有效的教学和学习。

WileyPLUS 通过为学生提供清晰的路线图建立了学生的信心，因为它消除了学习中的猜测：

- 需要做什么
- 如何做
- 他们是否做得正确

它提供了互动资源以及完整的数字教科书，帮助学生学习更多。通过 WileyPLUS，学生会更加主动，因此你对他们在课堂及之外的成就将产生更大的影响。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_2_0.png)

# 了解更多信息，请访问 www.wileyplus.com

# 您和您的学生需要的所有帮助、资源和个人支持！

www.wileyplus.com/resources

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_3_0.png)

2分钟教程以及您和学生学生所需的所有资源

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_3_1.png)

来自经验丰富的学生用户的支持

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_3_2.png)

与您的同事协作，寻找导师，参加虚拟和现场活动，并查看资源 www.WhereFacultyConnect.com

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_3_3.png)

由领域专家创建的预加载、即刻用的作业和演示文

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_3_4.png)

www.wileyplus.com/support

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_3_5.png)

您的 WileyPLUS 账户经理，提供个人培训和支持

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_4_0.png)

CAY HORSTMANN

圣何塞州立大学

本书通过一套完整的在线资源和强大的 WileyPLUS 课程进行补充。访问 www.willey.com/college/horstmann 访问在线伴随资源，其中包括：

WileyPLUS 是一个在线教学学习环境，它将教材与教师及学生资源整合在一起。详情请见第 iii-xiv 页。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_9_0.png)

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_9_1.png)

# 导读 ix

## 学习辅助工具导读

书中的教学元素专注于关注和强化编程概念及基本原理，并组织了额外的提示和细节以支持和深化这些基础。除了章节目标和丰富的练习等功能外，每章还包含了针对当今视觉学习者的元素。

## 4.2 循环

在每个章节中，**边注显示了引入新概念的地方，并提供了关键思想的大纲。**

通常情况下，你想按指定的次数执行一组语句；有一个由计数器控制的简单循环，如下例所示：

由于这个原因，有一种特殊的循环称为 for 循环（参见语法 4.2）。

```
while (counter <= 10) // 检查计数器
counter++; // 计数器加
```

**附加示例代码**为学生提供了运行和修改的完整程序。

有些人可以使用 for 循环。然而，前节中的 while 循环一直运行直到事件发生；这平衡了需求。计数器控制的循环定义为：你预先知道它将执行有限次，或者用于累积目标余额。这种循环被称为确定循环。

**带注释的语法框**提供了新语言结构的快速、视觉化概述。

你可以将 for 循环想象成一个普通的步骤序列。

# 语法 4.2

## For 语句

for (initialization; condition; update)

这三部分控制着 for 循环。

初始化在循环开始之前发生。

在每次迭代之前都会检查条件。

更新在每次迭代之后发生。

```
for (int i = 1; i <= 10; i++)
```

此循环运行 10 次。

变量 `i` 是 for 循环的局部变量（参见第 141 页）。

**注释解释了所需的组件，并指向有关在使用该语法时常见的错误或最佳实践的更多信息。**

使用日常对象的类比来解释变量、数据类型、循环等概念的本质和行为。

就像计算机程序中的变量一样，停车位也有标识符和内容。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_10_0.png)

# 导读

令人难忘的照片加强了类比并帮助学生记住概念。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_11_0.png)

水果派配方可能会说使用任何种的水果。然而水果是有季节性的。苹果和樱桃是参数的示例。

# 问题解决章节教授了生成想法和评估解决方案的技术，通常使用纸笔或其他工具。这些内容强调了，离开计算机，大部分的规划和问题解决是学生成功的关键。

6.5 问题解决：通过操作物理对象发现算法 277

现在这如何帮助我们解决问题，即交换数组的前后半部分？让我们通过交换第六枚硬币来交换第一枚硬币。然而，在 Java 程序员中，我们会说交换位置 2 和 4 的硬币。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_11_1.png)

接下来，我们交换位置 1 和 5 的硬币。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_11_2.png)

# 如何 1-1

## 使用伪代码描述算法

使用伪代码描述算法

伪代码是描述算法的一种简易方法，而无需担心编程语言的严格语法。它使用自然语言来解释程序的逻辑。

这里是查找列表中最大值的伪代码示例：

```
Set max to the first element of the list
For each element in the list:
    If element is greater than max:
        Set max to element
Return max
```

这种方法允许你在编写任何实际代码之前专注于算法逻辑。它是规划和向他人交流算法的有用工具。

这里是另一个示例，二分查找的伪代码：

```
Set low to 0
Set high to length of list - 1
While low <= high:
    Set mid to (low + high) / 2
    If list[mid] is target:
        Return mid
    Else if list[mid] is less than target:
        Set low to mid + 1
    Else:
        Set high to mid - 1
Return not found
```

# 逐步讲解

## 常见错误描述了学生经常犯的错误，并对错误进行了解释以及如何处理它们。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_13_0.png)

| 常见错误 4 | 数据类型 | 元素数量 |

|---|---|---|

| 数组 | int | n |

| 数组列表 | a.size() | |

| Swing | a. | |

# 编程提示 3.5

### 手工跟踪

理解代码如何运行的一种非常有效的方法是在纸上手动跟踪程序。你可以使用这种方法找到代码中的 bug，或者理解一个复杂的程序。

对于每一行，写下当前的语句。在脑海中列出变量，然后列出旧值和新值。

例如，让我们用给定的输入跟踪以下程序。前三次迭代是：

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_13_1.png)

# 编程提示解释了良好的编程实践，并鼓励学生通过手工跟踪等技巧和技术提高工作效率。

```java
for (int i=0; i<3; i++) {
  System.out.println(i);
}
```

| i | i | 输出 |

|---|---|---|

| 0 | 0 | 0 |

| 1 | 1 | 1 |

| 2 | 2 | 2 |

在第 2、3 和 4 行中，初始状态为：

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_13_2.png)

# 特别提示 2.2

### 文件框

在带有图形界面的程序中，你希望使用文件对话框。当你需要选择文件时，`JFileChooser` 类实现了一个浏览文件系统的对话框。

# 特殊专题介绍了可选主题并提供了其他解释。本笔记还涵盖了 Java 7 的特性。

> 一个允许用户选择文件的程序。

以下代码显示了如何使用 `JFileChooser` 检查用户是否选择了文件。两种方法都使用同一个对话框，但第一种允许用户选择文件，而第二种允许他们选择或创建文件。

```java
JFileChooser chooser = new JFileChooser();
int result = chooser.showOpenDialog(null);
if (result == JFileChooser.APPROVE_OPTION) {
  File file = chooser.getSelectedFile();
}
```

为了让对话框在屏幕上的位置更好，你可以指定用户组件为父容器。例如，使用 `chooser.showOpenDialog(this)`。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_13_3.png)

| fact | 值 | 状态 |

|---|---|---|

| 打开 | | |

| 保存 | | |

| 取消 | | |

# 随机知识 4.1 - 第一个 Bug

根据传说，第一个计算机 bug 是在哈佛 Mark II 的继电器中发现的一只蛾子，它是哈佛大学的第一台数字计算机。

这只蛾子是由格蕾丝·霍珀（Grace Hopper）的团队发现的，并被胶在了计算机日志中，这是记录的第一个真正的 bug。

随机知识提供了计算领域的历史和社交信息——用于增加兴趣并满足 ACM/IEEE 指南中“历史和社交”的要求。

这些先驱计算机科学家们在操作机器时发现了这只蛾子。这一事件是计算机史上一个非常著名的轶闻。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_13_4.png)

第一个 Bug

![](img/6a52d1dde3d548e31d0e6ce_13_5.png)

* 格蕾丝·霍珀

WileyPLUS 是一个支持学生和教师的在线环境。这本书的 WileyPLUS 可以补充印刷版文本，也可以完全取代它。

# 学生

不同的学习风格、不同的能力水平、不同的准备程度——每个学生都是独特的。WileyPLUS 赋予所有学生发挥特长的能力。集成的多媒体资源——包括音频和视觉演示——鼓励积极学习并提供多种学习路径。

- 练习示例应用了书中的解决问题步骤。
- 视频示例展示了作者在解决问题时通常采取的步骤。
- 动画允许学生重放关键概念的解释。
- 自测链接到文本中相关的章节。
- “在做中学学习”练习可以在实验室中使用以练习编程技能。
- “代码填空”题目使学生通过填写代码片段来获得即时反馈。

WileyPLUS 包含了网站上的所有教师资源，WileyPLUS 提供了识别那些落后学生的工具，使你无需等待他们的答疑时间即可进行干预。

- 练习题可以根据你的课程需要进行修改。
- 多步练习可以用于额外内容。
- 大量的选择题和测试专注于技能，而不只是术语。
- “代码填空”题目也可以添加到在线测试中。
- ISBN 978-1-18-2906-8

# 逐步讲解

学生可以阅读这本书并利用交叉链接检查他们是否掌握了基础概念。第 7 周，这段代码中的错误是什么？

```java
double[] data;
data = new double[5];
// 越界
// 未初始化
// 需要赋值
// 要求
```

学生可以通过填写代码来练习编程并获得即时反馈。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_15_0.png)

学生可以观看并听取程序流的解释。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_15_1.png)

# 画螺旋线

编写一个绘制如下螺旋线的程序：

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_15_2.png)

学生可以观看并听取作者一步步解决问题。

![](img/6a52d1dde3a219cfa39d548e31d0e6ce_15_3.png)

# 致谢

感谢 Beth Golub, John Downey, Elizabeth Miles, Thomas Kulesa, Wendy Ashenberg, Lee Gee, Andre Holm 以及 Wiley 的 John Curley 以及出版服务的 Vickie Pierce 对本项目项目的帮助。特别感谢 Cindy Johnson 的辛勤工作、明智判断和对细节的惊人关注。

感谢蒙罗大学的 Jose Cordova、Academia University 的 Rick Giles、Wisconsin Stout 的 Amitava Kumar、Washtenaw Community College 的 Khaled Mannour、Florida International University 的 Brent Sales、Columbia College 的 Donald Smith 以及 David Willoughby 在补充材料方面的卓越工作。还要感谢马德里大学的 Arturo Moro-Soto, Jesus Ricardo-Espinosa 和 Juan-Angel Case-Romero 为练习提供的贡献。

感谢提供反馈、评审稿、提出宝贵建议并提醒注意错误和遗漏的人们：

- Lynn Aaron, SUNY Rockland
- Karen Aiken, Bismarck State College
- Jay Asundy, University of Texas, Dallas
- Eugene Baek, Paul University
- William C. Trite, Trine University
- Bruce J. Barton, Suffolk County Community College
- Sanjiv K. Bhatia, University of Missouri, St. Louis
- Ann Biersczak, California State University, Channel Islands
- Jackie Bird, Northwestern University
- Eric Bishop, Northern Pioneer College
- Paul Bladek, Edmonds Community College
- Paul Logosa Bogen II, Texas&M University
- Irene Bruno, George Mason University
- Paolo Bucci, Ohio State University
- Joe Burger, College of Southern Maryland
- Robert P. Burton, Brigham Young University
- Leonello Calabresi, University of Maryland University College
- Martine Ceerio, University of Texas, El Paso
- Uday Chakraborty, University of Missouri, St. Louis
- Suchindran Chatterjee, Arizona State University
- Xuemen Chen, Texas Southern University
- Haiayan Chen, Willamette University
- Chabik Chraibi, Barry University
- Ta-Tao Chang, Guangzhou, Vincent Cicileiro, Richard Stockton College
- Mark Element, Brigham Young University
- Gerald Cohen, St. Joseph's College
- Ralph Conrad, San Antonio College
- Dave Cook, Stephen F. Austin State University
- Rebecca Crell, Community College of Allegheny County
- Leslic Dam, Vermont Technical College
- Geoffrey D. Decker, Northern Illinois University
- Khaled Deeb, Barry University, School of Adult and Continuing Education
- Akshay Dhawan, Ursinus University
- Julian Dichter, University of Bridgeport
- Mike Domaratzki, University of Miami
- Wei*

# 致谢

Philip Dorin, 洛约亚玛丽蒙特大学

Anthony J. Dos Reis, 纽约州立大学帕尔茨学院

Elizabeth Drake, 圣塔菲学院

Tom Duffy, 纽瓦克学院

Michael Eckmann, 斯基德莫学院

Sander Eller, 加州州立理工大学波姆森

Amita Engineer, 瓦伦西亚学院
