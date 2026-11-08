
## 练习

- 1. 将下列陈述标记为真或假。
  - a. 类的成员变量必须具有相同的类型。
  - b. 类的成员函数必须是公有的。
  - c. 一个类可以有多个构造函数。
  - d. 一个类可以有多个析构函数。
  - e. 构造函数和析构函数都可以有参数。

- 2. 找出以下类定义中的语法错误：

  ```cpp
  class mystery                    //Line 1
  {
  public:                           //Line 3
      void print() const;           //Line 4
      void setNum(double, double);  //Line 5
      int power();                  //Line 6
      double mystery();             //Line 7
      double mystery(double, double); //Line 8
  private:                          //Line 9
      double x;                      //Line 10
      double y                       //Line 11
  };                                //Line 12
  ```

- 3. 找出以下类定义中的语法错误：

  ```cpp
  class secret                       //Line 1
  {
  public:                            //Line 3
      bool multiply();               //Line 4
      print() const;                 //Line 5
      secret(int = 0, int = 0);      //Line 6
  private:                           //Line 7
      int one;                        //Line 8
      int two;                        //Line 9
  };                                 //Line 10
  ```

- 4. 找出以下类定义中的语法错误：

  ```cpp
  class secret                       //Line 1
  {
  public:                            //Line 3
      bool compare();                //Line 4
      void print() const;            //Line 5
      secret(int = 0, int = 0) const; //Line 6
  private:                           //Line 7
      string str;                     //Line 8
      int one;                        //Line 9
      int two;                        //Line 10
  };                                 //Line 11
  ```

练习进一步巩固学习，并确保学生确实已经掌握了这些材料。

```cpp
cin >> firstNum >> secondNum;
cout << endl;

// Missing statements
________ 0;
```

- 33. 假设 classStanding 是 char 变量，gpa 和 dues 是 double 变量。编写一个 switch 语句，按如下方式给 dues 赋值：如果 classStanding 为 'f'，则 dues 为 $150.00；如果 classStanding 为 's' 且 gpa 至少为 3.75，则 dues 为 $75.00；否则，dues 为 $120.00；如果 classStanding 为 'j' 且 gpa 至少为 3.75，则 dues 为 $50.00；否则，dues 为 $100.00；如果 classStanding 为 's'，则 dues 为 $100.00。（注意，switch 语句中的代码应包含代码 '$'，且不需要 break 语句。）

- 34. 假设 amount 是 double 变量，表示你需要向百货商店支付的金额。如果你支付最低金额，你将在下一期账单中获得 $10.00 或该账单金额的 1%（以较小者为准）作为抵扣；如果你支付至少账单金额的 50%，罚金为余额的 8%；如果你支付至少账单金额的 20% 且少于账单金额的 50%，罚金为余额的 10%；否则，罚金为余额的 20%。设计一个算法，提示用户输入账单金额和期望付款金额。然后该算法计算并输出抵扣金额或剩余余额。如果金额未全额支付，该算法还应输出罚金金额。

## 编程练习

- 1. 编写一个程序，提示用户输入一个数。然后程序应输出该数，并输出一条消息说明该数是正数、负数还是零。

- 2. 编写一个程序，提示用户输入三个数。然后程序应按升序输出这些数。

- 3. 编写一个程序，提示用户输入一个 0 到 35 之间的整数。如果该数在 0 到 9 之间，程序应输出该数；否则，应输出一个字母。例如，如果用户输入 10，程序应输出字母 A。

- 4. 以下程序中的语句顺序不正确。重新排列这些语句，使它们提示用户输入形状类型（矩形、圆形或圆柱体）以及该形状的相应尺寸。

编程练习要求学生编写具有指定结果的 C++ 程序。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_40_0.png)

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_41_0.png)

## 补充资源

### CourseMate

在一个地方获取成功所需的一切，充分利用学习时间。在线阅读教材、高亮并做笔记、复习闪卡、观看视频，并在线参加练习测验。了解更多信息，请访问 *www.cengage.com/coursemate*。

C++ 编程 CourseMate 包含以下功能：

- **视频**逐步讲解每章的程序，而集成测验提供即时反馈，以评估你的理解程度。
- **实验手册**让你通过大量实用的动手练习应用所学内容。
- **交互式测验和学习游戏**强化各章关键概念，而开放式**作业**培养批判性思维能力。
- **交互式电子书**、闪卡等！

教师可以将 CourseMate 添加到教材包中，学生也可以直接通过 *www.cengagebrain.com* 购买 CourseMate。

### 源代码

源代码采用 ANSI/ISO 标准 C++，学生可在 www.cengagebrain.com 以及通过本书提供的 CourseMate 下载。这些文件也提供给教师，位于教师资源 CD 和 login.cengage.com 上。运行某些程序所需的输入文件也包含在源代码中。

### 教师资源

当本书用于课堂环境时，可使用以下补充材料。所有教师教学工具都随本书提供在一张 CD-ROM 上。许多资源也可在 login.cengage.com 下载。

### 电子版教师手册

教师手册按章节顺序配合教材，包含帮助规划和组织有效且引人入胜的课程的材料。

该手册包括概述、章目标、教学提示、快速测验、课堂讨论主题、额外项目、额外资源和关键术语。还提供**示例教学大纲**。

### ExamView®

本教材配有 ExamView，这是一个强大的测试软件包，允许教师创建和管理打印考试、计算机（局域网）考试和互联网考试。ExamView 包含数百道与本教材所涵盖主题相对应的题目，使学生能够生成详细的学习指南，其中包含页码引用以便进一步复习。这些基于计算机和互联网的测试组件允许学生在自己的计算机上参加考试，并为教师节省时间，因为每份考试都会自动评分。题库还提供与 **Blackboard、WebCT 和 Angel** 兼容的格式。

### PowerPoint 演示文稿

本书附有配合各章的 PowerPoint 幻灯片。幻灯片可用于指导课堂演示、提供给学生用于章节复习，或打印为课堂讲义。教师可以为自己向班级介绍的其他主题添加自己的幻灯片，并使用本书完整的**图片文件**来自定义幻灯片。

### 解答文件

所有编程练习的解答文件采用 ANSI/ISO C++，可在本书配套网站 *login.cengage.com* 获取，也可在教师资源 CD-ROM 上获取。运行某些编程练习所需的输入文件也包含在解答文件中。

## 致谢

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_43_0.png)

有许多人我必须感谢，他们以各种方式为本书的成功做出了贡献。首先，我要感谢所有学生，他们在准备过程中主动告诉我某些部分是否需要改写，以便更好地理解和更清晰地阅读。其次，我要感谢那些通过电子邮件发送大量意见以改进第五版的人。我感谢 S.C. Cheng 教授和 Randall Crist 教授对本项目的持续支持。我也非常感谢审阅本书早期版本的审稿人，他们提供了许多关于如何改进本书的重要建议。

我非常感谢以下审稿人，他们为改进本版教材提供了有益而关键的建议：Gary Bricher：Lane Community College；Cliff Brozo：Monroe College；以及 Marie Pullan：Farmingdale State College。

接下来，我要感谢组稿编辑 Brandi Shailer，感谢她认识到本项目的重要性和独特性。如果没有高级产品经理 Alyssa Pratt 的周密规划，这一切都不可能实现。我向 Alyssa 以及内容项目经理 Matthew Hutchinson 表示诚挚的感谢。我特别感谢 Stephanie Lorenz，她运用自己的专业知识仔细编辑了视频。我也感谢 Integra Software Services 的 Sreemannarayana Reddy 协助我们使项目按计划进行。我要感谢 Cengage Learning 的 Chris Scriver 和 Serge Palladino 耐心而仔细地测试代码，并发现拼写错误和错误。

本书献给我的父母，感谢他们的祝福。

最后，我感谢妻子 Sadhana，尤其是女儿 Shelly 的支持。在撰写本书期间，每当我感到不堪重负时，她们都会鼓励我。欢迎对本书提出任何意见。意见可发送至以下电子邮件地址：malik@creighton.edu。

D. S. Malik

