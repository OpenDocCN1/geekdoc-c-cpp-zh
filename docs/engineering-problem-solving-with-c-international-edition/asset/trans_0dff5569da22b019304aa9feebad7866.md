

![](img/02c4582f051c5b51776411c92b079035_0_0.png)

## 用 C 进行工程问题求解

### 第四版

### 德洛雷斯·M·埃特尔

## 常用 C 函数

### 基础数学函数（第 66 页）

```
ceil(x) exp(x) fabs(x) floor(x)
log(x) log10(x) pow(x,y) sqrt(x)
```

### 三角函数（第 67 页）

```
acos(x) asin(x) atan(x) atan2(y,x)
cos(x) sin(x) tan(x)
```

### 字符函数（第 71 页）

```
isalnum(c) isalpha(c) iscntrl(c)
isdigit(c) isgraph(c) islower(c)
isprint(c) ispunct(c) isspace(c)
isupper(c) isxdigit(c) tolower(c)
toupper(c)
```

### 字符串函数（第 309-310 页）

```
strcat(s,t) strchr(s,c) strcmp(s,t)
strcpy(s,t) strcspn(s,t) strlen(s)
strncat(s,t,n) strncmp(s,t,n) strncpy(s,t,n)
strpbrk(s,t) strrchr(s,c) strspn(s,t)
strstr(s,t)
```

## 运算符优先级

| 优先级 | 运算符 | 结合性 | 教材页码 |
|---|---|---|---|
| 1 | ( ) [ ] | 从内向外 | 第 45, 47, 208 页 |
| 2 | ++ -- - + ! * (type) & * | 单目，从右向左 | 第 45, 46, 49, 56, 286 页 |
| 3 | * / % | 从左向右 | 第 45 页 |
| 4 | + - | 从左向右 | 第 45 页 |
| 5 | < <= > >= | 从左向右 | 第 92 页 |
| 6 | == != | 从左向右 | 第 92 页 |
| 7 | && | 从左向右 | 第 93 页 |
| 8 | || | 从左向右 | 第 93 页 |
| 9 | ?: | 从右向左 | 第 98 页 |
| 10 | = += -= *= /= %= | 从右向左 | 第 50 页 |
| 11 | , | 从左向右 | 第 96 页 |

本页故意留空

## 用 C 进行工程问题求解

### 第四版

### 德洛雷斯·M·埃特尔

电气工程系
南卫理公会大学
德克萨斯州达拉斯

## 皮尔逊

- 波士顿 哥伦布 印第安纳波利斯 纽约 旧金山 上萨德尔河 阿姆斯特丹 开普敦 迪拜 伦敦 马德里 米兰 慕尼黑 巴黎 蒙特利尔 多伦多 德里 墨西哥城 圣保罗 悉尼 香港 首尔 新加坡 台北 东京

编辑总监：Marcia Horton
执行编辑：Tracy Dunkelberger
编辑助理：Erin Duncan
市场总监：Patrice Jones
市场经理：Yez Alayan
市场协调员：Kathryn Ferranti
制作总监：Vince O'Brien
主编：Jeff Holtzman
制作编辑：Kayla Smith-Tarbox
运营主管：Alan Fischer
制造采购员：Lisa McDowell
美术总监：Anthony Gonnella
封面设计师：Anthony Gemmellaro

视觉研究经理：Karen Sanatar
照片研究员，AV/ Kay Hollian
版权与许可经理：Michael Joyce
文本许可：Nicole Cogliet
封面美术：Arin Briosch
图片许可：Katie Holibill, Bill Smith Group
媒体项目高级经理：Daniel Sandin
全方位项目管理：Integrate
副本编辑：Karen Sanatar
印刷/装订：Edwards Brothers
封面印刷：Lehigh-Phoenix Color/Hagerstown
正文字体：10/12, Times

- 第 2 页：第 1 章开篇照片 © Caspar Benson | Getty Images USA, Inc.
- 第 4 页：微处理器 © Markzy Ragaç Jr | Fotolia LLC
- 第 4 页：月球登陆 © Nasa
- 第 5 页：卫星 © Nasa
- 第 5 页：诺基亚手机设计 © Urostock/Shutterstock.com
- 第 5 页：大型客机 © dell Fotolia
- 第 7 页：先进复合材料 © Dominique Landau | Shutterstock
- 第 7 页：CT 扫描 © Andesign101 | Dreamstime.com
- 第 8 页：基因工程 © Michal Różkowski | Dreamstime.com
- 第 9 页：机器人装配线 © Fotolia
- 第 9 页：光纤 © Vyacheslav Kharkin | Fotolia LLC
- 第 24 页：第 2 章开篇照片 © Ferkelich | Dreamstime.com
- 插图照片 1：指纹分析 © picture549 | Shutterstock
- 插图照片 2：手指控制 © Freedigitalphotos.net
- 插图照片 3：指纹识别、处理、扫描，仰视图 © Elis Years | Getty Images USA, Inc.
- 插图照片 4：虹膜扫描—安全系统 © Michal Mrozek | Shutterstock
- 插图照片 5：年轻人在纽约街头打电话 © Windslow Productions | Getty Images USA, Inc.
- 第 80 页：第 3 章开篇照片 © Alan Thornton | Getty Images USA, Inc.
- 第 148 页：图 3.7 | BestPhotoStudio | Shutterstock
- 第 148 页：第 4 章开篇照片 © DronG | Shutterstock
- 第 212 页：第 5 章开篇照片 © Lagun49 | Dreamstime.com
- 第 288 页：第 6 章开篇照片 © zecilla | Shutterstock
- 第 334 页：第 7 章开篇照片 © Alexandra-Radu Borzeal Shutterstock
- 第 372 页：第 8 章开篇照片 © picture549 | Shutterstock

本教材中从其他来源借用并经许可复制的致谢和鸣谢出现在版权页。

Microsoft® 和 Windows® 是 Microsoft Corporation 在美国及其他国家的注册商标。屏幕截图和图标经 Microsoft Corporation 许可重印。本书未获得 Microsoft Corporation 的赞助或认可，也与其无关。

版权所有 © 2013, 2005 Pearson Education, Inc.，以 Prentice Hall 名义出版。保留所有权利。在美国制造。本出版物受版权保护，任何禁止的复制、存储在检索系统中或以任何形式或任何方式（电子、机械、影印、录制或其他）传输，均应事先获得出版商许可。如欲获得使用本作品材料的许可，请向 Pearson Education, Inc., Permissions Department, One Lake Street, Upper Saddle River, New Jersey 07458 提交书面请求，或将请求传真至 201-236-3290。

制造商和卖家用于区分其产品的许多名称均声称为商标。当这些名称出现在本书中，且出版商知悉商标主张时，这些名称已以首字母大写或全大写形式印刷。

编目数据可应要求提供。

10 9 8 7 6 5 4 3 2 1

![](img/02c4582f051c5b51776411c92b079035_4_0.png)

ISBN 10: 0-13-608531-8
ISBN 13: 978-0-13-608531-7

本页故意留空

纪念我最亲爱的母亲，
Muerladene Janice Van Camp

## 前言

工程师使用计算机解决各种问题，范围从求解简单函数到求解非线性方程组。因此，C 语言已成为许多工程师和科学家的首选语言，不仅因为它拥有强大的命令和数据结构，还因为它可以轻松用于系统级操作。由于 C 语言是新工程师在工作中可能遇到的语言，因此它是向工程师介绍计算的良好选择。因此，本教材编写旨在介绍工程问题求解，并具有以下目标：

- 为解决工程问题开发一致的方法论；
- 介绍 C 语言的基本功能，C 语言是许多执业工程师和科学家的首选语言；以及
- 通过各种有趣的工程示例和应用，用 C 语言说明问题求解过程。

为实现这些目标，第 1 章介绍了一个五步流程，该流程在本书其余部分中用于一致地解决工程问题。第 2 至 7 章介绍了用于解决工程问题的 C 语言基本功能。第 8 章是使用 C++ 进行面向对象编程的介绍。面向对象编程在许多工程和科学领域日益流行，并且可能在工作中遇到。在所有这些章节中，我们介绍了来自许多不同工程和科学学科的大量示例。这些示例的解决方案是使用五步流程和 ANSI C（第 8 章中为 ANSI C++）开发的，这些是由美国国家标准协会制定的标准。

## 第四版的更改

- 本版的新主题是犯罪现场调查（CSI）。了解犯罪现场调查背后的技术不仅非常有趣，而且还提供了许多我们可以开发 C 程序解决方案的问题。
- 第 1.2 节已重写，以包含对云计算和内核等当前话题的讨论。
- 新增了一张四色插页，以定义犯罪现场调查的一个重要领域——生物识别技术。生物识别技术是用于描述可用于识别个人的身体或行为特征的术语。插页包括对指纹、面部识别、虹膜识别、DNA 和语音识别的讨论。
- 每章都以一张照片和关于犯罪现场调查中使用的技术的相关讨论开始。然后，在第 1 章之后的每章中，都添加了一个相关的应用部分，因此除了学习 C 语言的所有关键特性外，您还将了解法医人类学、面部识别和监控视频、虹膜识别、语音分析和语音识别、DNA 分析、指纹识别和手部识别。在这些应用部分，我们开发了与犯罪现场技术相关的问题的 C 解决方案。

