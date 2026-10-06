

# C++ 多线程编程指南

包含 60 多个方案，帮助你通过规则、指南和最佳实践，使用 C++ 创建极速多线程应用程序

Miloš Ljumović

![](img/412b0f5bbb36adcce2ddd2d5b7416516_1_0.png)

## C++ 多线程编程指南

版权所有 © 2014 Packt Publishing

保留所有权利。未经出版者书面许可，不得对本书的任何部分以任何形式或通过任何手段复制、存储在检索系统中或传输，但在批判性文章或评论中嵌入的简短引用除外。

在编写本书时，我们已尽一切努力确保所陈述信息的准确性。然而，书中包含的信息按现状销售，不提供任何形式的明示或暗示保证。作者、Packt Publishing 或分销商均对因本书直接或间接引起或声称引起的任何损害不承担责任。

Packt Publishing 已努力通过正确使用大写字母，对书中提到的所有公司和产品进行商标处理。然而，Packt Publishing 无法保证这些信息的准确性。

首次出版：2014年8月

制作参考号：1250714

由 Packt Publishing Ltd 出版
Livery Place
35 Livery Street
Birmingham B3 2PB, UK.
ISBN 978-1-78328-979-0

www.packtpub.com

封面图片：Radivoje Todorović (mr.todorovic@gmail.com)

## 制作致谢

| 作者 | 项目协调 |
| --- | --- |
| Miloš Ljumović | Mary Alex |

| 审稿员 | 校对员 |
| --- | --- |
| Abhishek Gupta | Simran Bhogal |
| Venkateswaran Loganathan | Kevin McGowan |
| Walt Stoneburner | Chris Smith |
| Dinesh Subedi | |

| 策划编辑 | 索引编员 |
| --- | --- |
| Edward Gordon | Hemangini Bari |
| | Mehreen Deshmukh |
| | Rekha Nair |

| 采购编辑 | 图形设计 |
| --- | --- |
| Nikhil Karkal | Disha Haria |

| 内容开发编辑 | 制作协调 |
| --- | --- |
| Akshay Nair | Komal Ramchandani |

| 技术编辑 | 封面制作 |
| --- | --- |
| Tarvi Bhatt | Komal Ramchandani |
| Faisal Siddiqui | |

| 文字编辑 |
| --- | --- |
| Janbal Dharmarajaj |
| Karuna Narayanan |
| Sayanee Mukherjee |
| Alfida Paiva |

## 关于作者

Miloš Ljumović 年于 7 月 26 日出生于欧洲黑黑山的首府波德波戈里察（Podgorica），并在那里完成了小学和中学教育。他还读过音乐学校学习吉他。他在黑黑山大学的自然科学与数学学院学习计算机科学。次年，他对操作系统产生了兴趣并以其为主修，于 2009 年 12 月获得硕士学位，并与朋友 Danilo 一起创立了他们的公司 Montenegro，拥有一支高素质团队提供高科技 IT 解决方案。因此，许多熟练的开发者加入了他们，通过这种合作，诞生了许多应用程序、系统软件、Web 应用程序和数据库系统。他的客户不仅包括黑黑山政府，还有一些国内公司；MeNet；他还开发了视频识别软件以及图像和其他数字媒体类型软件。他还开发了许多迷人的网站和其他 Web 应用程序。客户列表待在此加入。

在担任国际顾问工作几个月后，他与一家美国公司合作了一个涉及大型电子商务和互联网数据爬取的项目。这一切都是他今年 7 月初创立新公司 EXPERT.ITS.ME 的火花。该公司提供咨询服务，帮助 IT 领域的小型企业管理问题，同时激励他们志存远大。他是黑黑山国家商会（ICT）和 MENSA 的成员。在精通 HTML、PHP、SQL 等语言的同时，他喜欢用 C/C++/C 编程，并朝着拥有自己操作系统的梦想努力。

空闲时，他打网球、潜水、狩猎或下棋。他喜欢与团队在 AI 和计算机科学领域进行新鲜头脑风暴。他不断向新的起点和下一代软件解决方案迈进。他特别喜欢私教和课程教授计算机科学和数学的学生，将他们培养成合格的程序员，并帮助他们发现科学之美。欲了解他的兴趣和动态，请访问其公司网站 (http://expert.its.me) 或其个人网站 (http://milos.expert.its.me)，或通过 milos@expert.its.me 与他联系。

## 致谢

我感谢许多人帮助了这本书的编写。

我将本书献给我的父母 Radoslav 和 Slavka，以及我的姐姐 Natalija 和 Dušanka，无论发生什么，她们一直在我身边。我特别感谢我的母亲，没有她，我无法成为一名程序员。

还要感谢我美丽的妻子 Lara，感谢她的包容、对我所有的耐心和爱、无条件的支持，以及教会我永不放弃。Volim te（爱你）。

向我亲爱的朋友 Daniel 感谢，他教我如何成为一名伟大的商人，并每天推着我成为更好的程序员。

我还想感谢黑黑山大学的教授们，没有他们，我不会成为今天的专家。特别感谢 Rajko Čalasan 无数小时的教学；Miloš Tomašević 为我提供了面向对象编程的专业知识，并让我像今天一样热爱 C++；特别要感谢 Goran Šuković，这位最伟大的老师，他不断引导我并教我计算机科学的各个领域，让我每天都渴望并获得更多知识。

## 关于审稿员

**Abhishek Gupta** 是一位来自印度班加罗尔的年轻嵌入式软件工程师。过去几年他一直致力于汽车车载信息系统（IVI）软件的工作。他于 2011 年获得印度理工学院骑士格浦（IIT Kharagpur）视觉信息与嵌入式系统的硕士学位。他热于视频处理，并喜欢在嵌入式多媒体系统工作。他的技术知识主要围绕 C 和 Linux。

你可以在 www.abhitak.wordpress.com/about-me 获取更多关于他的信息。

**Venkateshwaran Loganathan** 是一位著名的软件开发人员，从事软件产品设计、开发和测试已超过 6 年。他在 11 岁时就通过 FoxPro 接触了计算机编程，然后开始学习并精通 C、C++、Python、Node.js 和 Unix 等多种计算机语言。他拥有安纳大学（Anna University）的计算机科学与工程学士学位，目前在 BITS Pilani 修读软件系统硕士。在加入 Cognizant 之前，他在 Infosys、Virtusa 和 Nuvidia 等主要的 IT 公司工作过。作为网络开发人员开启职业，他在网络、电子学习和医疗健康领域积累了专业知识。他目前在 Cognizant Technology 担任助理，参与物联网的研究开发。他对比开源技术着迷，并参与了多种技术的贡献。他还为新手工程师和大学生处理各类技术和软技能课程。他喜欢唱歌和徒步。你可以访问 http://www.venkateshwlogan.com 在线他，或通过 anandvenkat@gmail.com 与他联系。

他还出版了《PySide GUI Application》一书，Packt Publishing 出版。

