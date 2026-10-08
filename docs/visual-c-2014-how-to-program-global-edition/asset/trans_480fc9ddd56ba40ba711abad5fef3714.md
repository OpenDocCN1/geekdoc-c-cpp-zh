

# 34

# 前言

我们非常幸能与 Pearson 高教育（Pearson Higher Education）专业的出版专家团队合作。我们非常感谢计算机科学执行主编辑 Tracy Johnson 提供的指导、智慧、活力和启发。Kristy Alaura 在招募书籍评审员和管理评审流程方面付出了卓越努力。Bob Engelhardt 在本书的出版方面工作做得非常出色。

# 评审员

本书经过了教授 C# 的学术工作者和 C# 行业专家的严谨审查。他们为改进内容呈现方式提供了无数建议。书中任何剩余的缺陷均由我们承担。

第六版评审员：陈谦（Qian Chen，萨凡纳州州立大学工程技术系：计算机科学技术专业），Oscar Hernandez（微软认证解决方案开发人员，Advanced Bionics 首席软件工程师），Jose Gonzalez Seco（安达卢西亚亚洲议会），Bradley Sward（杜波奇学院学院）和 Lucian Wisch（微软 Visual C# 团队）。

第五版评审后后续评审员：帮助我们编写第 6 版是一件很有趣的事，以下学术工作者评审了第 5 版并提供了许多有帮助的建议：陈谦（萨凡纳州立立大学），池梅美（佛罗里达农立大学），杜奎（马萨诸塞大学波士顿），James Leach（库亚加学院西校区），Victor Miller（Ramapo Loft），Gary Savoy（钱普莱学院）和 Mohammad Yusuf（新罕布郡学院）。

其他版本的评审员：Douglas B. Beck（MCSD.NET，伊利诺伊州州立大学埃德华德分校），Dan Crevier（微软），Shay Friedman（微软 Visual C# MVP），Amit K. Gosh（德克萨斯大学埃尔帕索），Manuel Guerrero Hahn（微软），Kim Hamilton（微软软件设计师及《学习 UML 2.0》合著者），胡焕辉（微软公司），Stephen Husthede（南迈阿密学院），James Edward Keyes（佛罗里达理工学院），Norges Kasiri（俄克拉荷马州立大学），Helena Horkas（微软软件架构师），Charles Luis（德克萨斯大学圣东尼奥分校），Chris Loft，Bashar Lulu（INETA 国家开发者，阿拉伯湾地区），John Midhney（空间智能：微软 MVP 开发者，Visual Basic），Jed Mead（微软 Visual Basic MVP，DevCity.net），Anand Mukherjee（Polaris Software Lab Ltd. 架构师），Hamid Remati 博士（北卡罗来纳大学格林斯堡），Timothy Ng（微软），Akira Oni（微软），Jeffrey P. Scott（黑霍克技术学院），John Stagner（微软开发者工具与平台高级经理），Erik Thompson（微软），Jesús Ubaldo Quevedo-Torres（威斯康星大学普雷里分校），Shawn Wefield（微软 MVP 及 UserGroup.tv 创始人）和杨子刚（西密歇根州立大学）。

在您阅读本书时，我们诚挚感谢您对改进内容的意见、批评、纠正和建议。请将所有信寄至：

```
deitel@deitel.com
```

编写《Visual C# to Program, 6e》是一件快乐的事——我们希望您阅读愉快！

Paul Deitel
Harvey Deitel

# 关于作者

Paul Deitel 是 Deitel & Associates, Inc. 的首席执行官兼首席技术官，在计算领域拥有 35 年经验。他是麻省理工学院（MIT）的毕业生，在那里学习了信息技术。通过 Deitel & Associates, Inc.，他向全球多个城市提供了数百门编程课程，包括 Cisco、IBM、Siemens、Sun Microsystems（现为 Oracle）、Dell、Fidelity、肯尼迪航天中心的 NASA、国家强风暴实验室、NOAA（美国国家海洋和大气管理局）、白沙导弹发射场、Rogue Wave Software、SunGuard、Nortel Networks、Puma、iRobot、Invisens。他和合著者 Harvey Deitel 是全球畅销的编程语言教材/专业书籍/视频作者。

Paul 曾在 2012-2014 年间被评为微软 C# 特别专家（MVP）。根据微软介绍，“微软 MVP 奖是一项表彰卓越社区领袖的荣誉，他们积极与用户和微软分享高质量、实用的专业知识。”他还持有 Java 认证程序员和 Java 认证开发者证书，并是 Oracle Java 冠军。

![](img/57baed2319be0bb1b5f98674846f2711_35_0.png)

Harvey Deitel 博士是 Deitel & Associates, Inc. 的主席兼首席策略官，在计算机领域拥有 55 年以上经验。Deitel 博士在麻省理工学院（MIT）获得电气工程学士和硕士学位，并在波士顿大学获得数学博士学位——在这些每个项目中都学习了计算，并在 1991 年与儿子 Paul 共同创立 Deitel & Associates, Inc. 之前，曾担任波士顿大学计算机系主任。Deitel 家族的出版物获得了国际认可，译文涵盖日语、德语、俄语、西班牙语、法语、波兰语、意大利语、简体中文、繁体中文、韩语、葡萄牙语、希腊语和土耳语。Deitel 博士为学术、企业、政府和军事客户提供了数百门编程课程。

# 全球版感谢

Pearson感谢 Komal Arora 对全球版的贡献，并感谢 Ela Kashyap（Amity University Noida）、Siddhartha Nair 和 Sandeep Singh（Jaypee Institute of Information Technology）对全球版的评审。

本页留白

# 在开始之前

在使用本书之前，请阅读本节以确保您的计算机设置正确。

# 字体和命名规范

我们使用字体来区分功能，如菜单名称、菜单项以及程序开发环境中出现的其他元素。我们的规范是：

- **使用无衬线粗体强调 Studio 功能**、属性窗口以及
- **使用等宽无衬线字体强调程序文本（例如 `bool x = true`）。**

# Visual Studio 2015 Community 版

本教材使用 Windows 10 和免费的 Microsoft Visual Studio 2015 Community 版——Visual Studio 也可以运行在旧版本的 Windows 版本上。请确保您的系统符合 Visual Studio 2015 Community 版最低硬件和软件要求，详见：

```
https://www.visualstudio.com/en-us/visual-studio-2015-community/
```

