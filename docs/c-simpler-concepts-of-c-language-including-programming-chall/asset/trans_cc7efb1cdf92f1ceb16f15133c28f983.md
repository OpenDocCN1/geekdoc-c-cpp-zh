

# 简单的 C 语言

[C 语言概念，包含编程挑战]

D.P. Kothari 博士
ME, Ph.D.
总院长
Raisoni Group of Institutions, Nagpur
VITS, Indore 名誉总院长
VIT University, Vellore 前校长
IIT Delhi 前任职院长（i/c）
VRCE, Nagpur 前任主长（代理）

Subashri V 工程师
M.Tech.
Shriram K Vasudevar 工程师
M.Tech., MBA, (Ph.D.)
经理 – 学习与开发 – 技术部
Amrita Vish Vidyapeetham University, Coimbatore

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_0_0.png)

S. CHAND
出版发行
S Chand And Company Limited
(ISO 9001 认证公司)

## S Chand And Company Limited

(ISO 9001 认证公司)
**总部：** Block B-1, House D-1, Ground Floor, Mohan Co-operative Industrial Estate, New Delhi – 110 044 | 电话：011-6667200

**注册办公室：** A-27, 2nd Floor, Mohan Co-operative Industrial Estate, New Delhi – 110 044
电话：011-49731800

www.schandpublishing.com; 电子邮箱：info@schandpublishing.com

分机构
- 阿合达德: 2754269, 2754196; ahmedabad@schandpublishing.com
- 班加罗尔: 2235408, 2226840; bangalore@schandpublishing.com
- 布加尔尔: 4274723, 4209587; bhopal@schandpublishing.com
- 布巴塞尔: 2951580; bhaneswar@schandpublishing.com
- 钦奈伊: 2363210; chennai@schandpublishing.com
- 固瓦哈蒂: 2738811, 2735640; guwahati@schandpublishing.com
- 海德拉巴: 4016018; hyderabad@schandpublishing.com
- 雅雅浦: 2291317, 2293118; jaipur@schandpublishing.com
- 雅兰德尔: 4645630; jalandhar@schandpublishing.com
- 科契: 2576207, 2576268; cochin@schandpublishing.com
- 加尔各答: 2335748, 23353914; kolkata@schandpublishing.com
- 德纳陆: 4003633; lucknow@schandpublishing.com
- 孟买: 25002297; mumbai@schandpublishing.com
- 纳格尔: 2250230; nagpur@schandpublishing.com
- 帕特纳: 2260011; patna@schandpublishing.com
- 兰奇: 2361178; ranchi@schandpublishing.com
- 萨希布巴德: 2771238; info@schandpublishing.com

© S Chand And Company Limited, 2012

版权所有。未经版权所有者书面许可，本书不得以任何材料形式（包括复印或存储在任何图形、电子或机械手段中，无论是否是本出版物其他方法的临时或偶然手段）复制或传播。任何违反此规定的行为都将导致法律行动和起诉，无需另行通知。

**管辖权：** 与本出版物的所有争议均应受印度新德里法院、法庭和论坛的管辖。

第一版 2022

**ISBN: 978-81-291-4121** 产品代码：H3CSP50ENAA120 印度打印

由 Vikas House Private Limited 出版，20/4, Site-IV, Industrial Area Sahibabad – 20110
由 S Chand And Company Limited 出版，A-27, 2nd Floor, Mohan Co-operative Industrial Estate, New Delhi – 110 044

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_0_0.png)

# 献辞

D.P. Kothari 博士
→ Seema

Subashri V 工程师
→ Veerarhavan 和 Shantha

Shriram K Vasudevan 工程师
→ Sunanda, Revathi 和 Vasathi

# 第一版序言

C-Simpler，书名本身描述了本书的内容。本书以非常适合初学者的形式解释了 C 语言。尽管非常简单，但通过编程的方式进行了解释。读完每一章后，读者将在心理上准备好面对编程挑战。这本书也可以作为那些面试面试的指南，因为它涵盖了 C 语言的要点。

以下章节的简要讨论。第一章涵盖了基础知识。第二章讨论了学习构造，以及数组。第四章介绍了 'C' 中的各种运算符。第五章讨论了最重要的函数概念。第六章讨论了存储修饰符。第七章讨论了 'C' 中最重要的指针。第八章讨论了结构体和联合体。第九章讨论了 'C' 中易于学习的字符串。第十章涵盖了文件处理。第十一章讨论了非常实用的数据结构。第十二章旨在处理命令行参数。第十三章对于在 Linux/Unix 平台上工作的人非常有帮助。它讨论了 Linux/Unix 平台上的 'C' 构造。第十四章讨论了最有趣的预处理器。最后，十五章旨在提供一些基础但强大的指南。

在每一章的结束，提供了脑力测试以检查理解程度。这对你来说是最宝贵的礼物。

我们鼓励读者提出任何疑问、问题或建议，请邮件至 vrsuba@gmail.com, Shriramkv@gmail.com。祝读者未来光辉无限！

D.P. Kothari 博士
Subhash V 工程师
Shriram K Vasudevan 工程师

免责声明：本书作者努力避免任何错误或遗漏，并尽其技能、专业知识提供准确、最新的信息。作者和 S Chand 对本出版物的任何错误或遗漏不负责。

# 目录

| 章节 | 页码 |
| :--- | :--- |
| 1. C 语言入门 | 1–15 |
| 2. 条件结构与循环 | 16–33 |
| 3. 数组 | 34–49 |

## 1. C 语言入门

- 1.1. C 语言是如何发展的？
- 1.2. C 的特性
- 1.3. 字符集 - 有什么和没有？
- 1.4. 关键字和标识符
    - 1.4.1. 标识符
- 1.5. C 中的标记 (Tokens)
- 1.6. C 变量
- 1.7. C 数据类型
    - 1.7.1. 原生（内置）数据类型
    - 1.7.2. 变量范围
- 1.8. 常数
- 1.9. 一个简单的 C 程序
- 1.10. Windows/Linux/Dos 提示符下的 C
    - 1.10.1. 使用 Linux（Solaris/Unix/Ubuntu 相同方法）
    - 1.10.2. 使用 Windows/DOS（使用 Turbo C）
- 1.11. 测

## 2. 条件结构与循环

- 2.1. 条件结构讨论
    - 2.1.1. if 条件
    - 2.1.2. if-else 条件
    - 2.1.3. 嵌套 if 条件
    - 2.1.4. switch case
- 2.2. 循环结构
    - 2.2.1. for 循环
    - 2.2.2. while 循环
    - 2.2.3. break 和 continue 语句
- 2.3. 更复杂的 C 程序
- 2.4. 测
- 2.5. 练习题

