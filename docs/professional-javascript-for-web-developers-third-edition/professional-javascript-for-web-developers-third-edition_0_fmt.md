
# 《Web 开发人员 JavaScript 高级指南》（第三版）

![](img/9781118233092.jpg)

![image](img/9781118233092.jpg)

#我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。目录

## 第 1 章：什么是 JavaScript？

- 简史
- JavaScript 实现
- JavaScript 版本
- 总结

## 第 2 章：HTML 中的 JavaScript

- `<script>` 元素
- 内联代码与外部文件
- 文档模式
- `<noscript>` 元素
- 总结

## 第 3 章：语言基础

- 语法
- 关键字与保留字
- 变量
- 数据类型
- 运算符
- 语句
- 函数
- 总结

## 第 4 章：变量、作用域与内存

- 基本值与引用值
- 执行上下文与作用域
- 垃圾回收
- 总结

## 第 5 章：引用类型

- 对象类型
- 数组类型
- 日期类型
- RegExp 类型
- 函数类型
- 基本值包装类型
- 单例内置对象
- 总结

## 第 6 章：面向对象编程

- 理解对象
- 对象创建
- 继承
- 总结

## 第 7 章：函数表达式

- 递归
- 闭包
- 模拟块作用域
- 私有变量
- 总结

## 第 8 章：浏览器对象模型

- `window` 对象
- `location` 对象
- `Navigator` 对象
- `screen` 对象
- `history` 对象
- 总结

## 第 9 章：客户端检测

- 能力检测
- 兼容性模式检测
- User-Agent 检测
- 总结

## 第 10 章：文档对象模型（DOM）

- 节点层结构
- 操作 DOM
- 总结

## 第 11 章：DOM 扩展

- 选择器 API
- 元素遍历
- HTML5
- 私有扩展
- 总结

## 第 12 章：DOM 2 级与 3 级

- DOM 变化
- 样式
- 遍历
- 范围（Ranges）
- 总结

## 第 13 章：事件

- 事件流
- 事件处理器
- 事件对象
- 事件类型
- 内存与性能
- 模拟事件
- 总结

## 第 14 章：脚本表单

- 表单基础
- 脚本文本框
- 脚本选择框
- 表单序列化
- 富文本编辑
- 总结

## 第 15 章：使用 Canvas 图形

- 基础
- 2D 渲染
- WebGL
- 总结

## 第 16 章：HTML5 脚本

- 跨文档消息
- 原生拖放
- 媒体元素
- 历史状态
- 总结

## 第 17 章：错误处理与调试

- 浏览器报告
- 错误处理
- 调试
- Internet Explorer
- 总结

## 第 18 章：JavaScript 中的 XML

- DOM 支持
- XPath 支持
- SL 支持
- 总结

## 第 19 章：Ecmascript For

- 类型
- 通用用法
- 其他变化
- 启用
- 总结

## 第 20 章：JSON

- 语法
- 序列化
- 总结

## 第 21 章：Ajax

- `XMLHttpRequest` 对象
- `XMLHttpRequest` 2 级
- 事件
- 跨源共享
- 跨域技术
- 总结

## 第 22 章：高级技术

- 函数
- 对象
- 定计时
- 拖放
- 总结

## 第 23 章：离线应用

- 离线检测
- 应用程序缓存
- 数据存储
- 总结

## 第 24 章：最佳实践

- 可维护性
- 性能
- 部署
- 总结

## 第 25 章：新兴 API

- `requestAnimationFrame()`
- 页面可见性 API
- 地理 API
- 文件 API
- Web Timing
- Web Workers
- 总结

## 附录 A：Ecmascript Harmony

- 通用变化
- 函数
- 数组及结构
- 新对象类型
- 类
- 模块

## 附录 B：严格模式

- 开启
- 变量
- 对象
- 函数
- `eval()`
- `eval` 与参数
- `this` 的转换
- 其他变化

## 附录 C：JavaScript 库

- 通用库
- 互联网应用
- 动画与特效
- 加密

## 附录 D：JavaScript 工具

- 验证器
- 压缩器
- 单元测试
- 文档生成器
- 安全执行环境

# 第 1 章：什么是 JavaScript？

## 本章内容概览

- JavaScript 历史回顾
- 什么是 JavaScript
- JavaScript 与 ECMAScript 之间的关系
- JavaScript 的不同版本

当 JavaScript 在 1995 年首次出现时，它的主要目的是处理一些输入验证，而这些工作以前是留给如 `Perl` 等服务器端语言的。在此之前，为了确定某个必填字段是否为空或输入的值是否无效，需要与服务器进行往返通信。`Netscape Navigator` 网浏览器试图通过引入 `JavaScript` 来改变这一现状。在拨号调制解调器广泛使用的时代，在客户端处理某些基础验证的能力是一项令人兴奋的新功能。当时关联的慢速使得每次与服务器的往返都变成了一场耐心的考验。

从那时起，`JavaScript` 已经成为市场上每个主流网络浏览器的重要特性。`JavaScript` 不再局限于简单的数据验证，现在它可以与浏览器窗口及其内容的几乎所有方面交互。`JavaScript` 被认为是一门完整的编程语言，能够进行复杂的计算和交互，包括闭包、匿名（lambda）函数，甚至是元编程。`JavaScript` 已经成为 Web 中如此重要的一部分，以至于其他浏览器（包括手机浏览器和为残障人士设计的浏览器）也支持它。即使是拥有名为 `VBScript` 的客户端脚本语言的 `Microsoft`，最终也从最早版本起 `Internet Explorer` 中包含了了自己的 `JavaScript` 实现。

`JavaScript` 从一个简单的输入验证器到强大的编程语言的兴起是无法预测的。`JavaScript` 既是一门非常简单又非常复杂的语言，学习几分钟即可，但需要多年才能掌握。要开启充分利用 `JavaScript` 潜力的道路，理解它的本质、历史和局限性是非常重要的。

## 简史

随着 Web 的流行，对客户端脚本语言的需求逐渐增长。当时，大多数互联网用户通过 28.8 kbps 的调制解调器连接，尽管网页的大小和复杂度在不断增加。增加用户痛苦的是，简单的表单验证就需要与服务器进行多次往返。想象一下填写表单、点击 `Submit` 按钮，等待 30 秒进行处理，然后收到一条消息提示你忘记填写某个必填字段。当时处于技术创新前沿的 `Netscape` 开始认真考虑开发一种客户端脚本语言来处理简单的处理。

当时在 `Netscape` 工作的 Brendan Eich 开始开发一种名为 `Mocha` 的脚本语言，后来改为 `LiveScript`，用于 1995 年 `Netscape Navigator 2` 的发布，其意图将其同时用于浏览器和服务器（在服务器端将被称为 `LiveWire`）。`Netscape` 与 `Sun Microsystems` 建立了开发联盟，以确保在发布前及时完成 `LiveScript` 的实现。在 `Netscape Navigator 2` 正式发布之前，`Netscape` 将 `LiveScript` 的名称改为 `JavaScript`，以利用媒体对 `Java` 所产生的关注热度。

由于 `JavaScript 1.0` 如此成功，`Netscape` 在 `Netscape Navigator 3` 中发布了 `1.1` 版本。处于萌芽阶段的 Web 人气达到了新高度，`Netscape` 已将自己定位为市场上的领先公司。此时，`Microsoft` 决定投入更多资源开发一个名为 `Internet Explorer` 的竞争浏览器。在 `Netscape Navigator 3` 发布后，`Microsoft` 引入了 `Internet Explorer 3`，并包含一个名为 `JScript` 的 `JavaScript` 实现（之所以这样命名是为了避免与 `Netscape` 产生任何可能的许可问题）。`Microsoft` 在 1996 年 8 月进入网络浏览器领域的这一大举，现在是 `Netscape` 臭名昭著的日子，但也代表了 `JavaScript` 作为一种语言的发展的一大进步。

`Microsoft` 对 `JavaScript` 的实现意味着存在两个不同的 JavaScript 版本：`Netscape Navigator` 中的 `JavaScript` 和 `Internet Explorer` 中的 `JScript`。与 `C` 以及许多其他编程语言不同，`JavaScript` 没有规范其语法或特性的标准，三个不同的版本只凸显了这个问题。随着行业担忧的日益增加，人们决定对该语言进行标准化。

1997 年，`JavaScript 1.1` 作为提案提交给欧洲计算机制造商协会（`Ecma`）。第 39 技术委员会（`TC39`）被分配“标准化通用、跨平台、厂商中立脚本语言的语法和语义”（`[www.ecma-international.org/memento/TC39.htm](http://www.ecma-international.org/memento/TC39.htm)`）。`TC39` 由来自 `Netscape`、`Sun`、`Microsoft`、`Borland`、`NOMBAS` 以及其他对脚本未来感兴趣的公司程序员组成，他们开了数月的会议敲定了 `ECMA-262`，这是一个定义了名为 `ECMAScript`（通常读作“ek-ma-script”）的新型脚本语言的标准。

次年，国际标准化组织和国际电工委员会（`ISO/IEC`）也将 `ECMAScript` 采用为标准（`ISO/IEC-16262`）。从那时起，浏览器们尝试以不同程度的成功将 `ECMAScript` 作为其 `JavaScript` 实现的基础。

## JavaScript 实现

尽管 `JavaScript` 和 `ECMAScript` 经常被同用，但 `JavaScript` 远不止 `ECMA-262` 中定义的内容。事实上，一个完整的 `JavaScript` 实现由三个不同部分组成（参见 `图 1-1`）：

- 核心（`ECMAScript`）
- 文档对象模型（`DOM`）
- 浏览器对象模型（`BOM`）

图 1-1

![image](img/f003-01.jpg)

### ECMAScript

`ECMAScript` 是在 `ECMA-262` 中定义的语言，它并不绑定网络浏览器。事实上，该语言没有任何输入或输出方法。`ECMA-262` 将这种语言定义为基础，可以在其基础上构建更健壮的脚本语言。浏览器只是 `ECMAScript` 实现可能存在的宿主环境之一。宿主环境提供了 `ECMAScript` 的基础实现以及旨在与环境本身接口的实现扩展。扩展（如文档对象模型（`DOM`））使用 `ECMAScript` 的核心类型和语法提供更特定于环境的附加功能。其他宿主环境包括 `NodeJS`（一个服务端 `JavaScript` 平台）和 `Adobe Flash`。

如果 `ECMA-262` 不引用网络浏览器，它究竟规范了什么？在非常基础的层，它描述了语言的以下部分：

- 语法
- 类型
- 语句
- 关键字
- 预留字
- 操作符

`ECMAScript` 仅仅是实现规范中所描述的所有方面的语言描述。`JavaScript` 实现了 `ECMAScript`，但 `Adobe ActionScript` 也是。

### ECMAScript 版本

不同的 `ECMAScript` 版本被定义为版本（指的是描述该特定实现的 `ECMA-262` 版本）。最新的 `ECMA-262` 版本是第 5 版，于 2009 年发布。`ECMA-262` 的第一版基本上与 `Netscape` 的 `JavaScript 1.1` 相同，但删除了所有与浏览器相关的代码，并进行了一些微调：`ECMA-262` 要求支持 `Unicode` 标准（以支持多种语言）并要求对象与平台无关（`Netscape JavaScript 1.1` 实际上根据平台有不同的对象实现，例如 `Date` 对象）。这是 `JavaScript 1.1` 和 `1.2` 不符合 `ECMA-262` 第一版的一个主要原因。

`ECMA-262` 的第二版主要是编辑上的调整。该标准的更新是为了使其与 `ISO/IEC-16262` 达成严格一致，并没有包含任何新增、更改或遗漏。`ECMAScript` 的实现通常不将第二版作为合规性的标准。

`ECMA-262` 的第三版是该标准首次真正的更新。它对字符串处理、错误定义和数值输出进行了更新。它还添加了对正则表达式的支持、新的控制语句、`try-catch` 异常处理，并为了更好地让标准支持国际化进行了细微调整。对许多人来说，这标志着 `ECMAScript` 作为一种真正的编程语言的到来。

`ECMA-262` 的第四版是对语言的彻底重构。由于 `JavaScript` 在 Web 上的流行，开发者开始修订 `ECMAScript`，以满足全球 Web 开发日益增长的需求。作为回应，`Ecma TC39` 重新召集以决定语言的未来。由此产生的规范基于第三版定义了一个几乎完全全新的语言。第四版包含了强类型变量、新的语句和数据结构、真正的类和经典继承，以及与数据交互的新方法。

作为一种替代方案，一个名为“`ECMAScript 3.1`”的规范由 `TC39` 的一个小组委员会开发，作为语言的一种较小演进，该小组认为第四版对于语言来说跨越得太大了。结果是一个较小的提案，对 `ECMAScript` 进行了增量式更改，可以在现有的 `JavaScript` 引擎之上实现。最终，`ES3.1` 小组委员会赢得了 `TC39` 的支持，`ECMA-262` 的第四版在正式发布前被废弃。

`ECMAScript 3.1` 变为 `ECMA-262` 第五版，并于 2009 年 12 月 3 日正式发布。第五版试图澄清第三版中感知到的歧义并引入额外的功能。新功能包括用于解析和序列化 JSON 数据的原生 `JSON` 对象、用于继承和高级属性定义的方法，以及一个新“严格模式”的引入，该模式略微增强了 `ECMAScript` 引擎解释和执行代码的方式。

## ECMAScript 合规意味着什么？

`ECMA-262` 给出了 `ECMAScript` 合规的定义。要被视为 `ECMAScript` 的实现，该实现必须执行以下操作：

- 按照 `ECMA-262` 中的描述支持所有“类型、值、对象、属性、函数以及程序语法和语义”（`ECMA-262`，第 1 页）。
- 支持 Unicode 字符标准。

此外，合规的实现可以执行以下操作：

- 添加 `ECMA-262` 中未指定的“额外类型、值、对象、属性和函数”。`ECMA-262` 将这些新增描述为主要是新的对象，或规范中未给出的对象的新属性。
- 支持 `ECMA-262` 中未定义的“程序语法和正则表达式语法”（这意味着内置的正则表达式支持允许被更改和扩展）。

这些标准为实现开发者为开发基于 `ECMAScript` 的新语言提供了巨大的权力和灵活性，这在某种程度上也解释了它为何如此受欢迎。

## Web 浏览器对 ECMAScript 的支持

`Netscape Navigator 3` 于 1996 年附带 `JavaScript 1.1`。该 `JavaScript 1.1` 规范随后被提交给 `Ecma` 作为新标准 `ECMA-262` 的提案。随着 `JavaScript` 爆发性的流行，`Netscape` 非常乐于开始开发版本 `1.2`。然而，存在一个问题：`Ecma` 尚未接受 `Netscape` 的提案。

在 `Netscape Navigator 3` 发布后，微软推出了 `Internet Explorer 3`。这个版本的 `IE` 附带了 `JScript 1.0`，它本应等同于 `JavaScript 1.1`。然而，由于未记录和复制不当的功能，`JScript 1.0` 远低于 `JavaScript 1.1`。

`Netscape Navigator 4` 于 1997 年发布，附带 `JavaScript 1.2`，在此同年后期 `ECMA-262` 第一版被接受并标准化。因此，`JavaScript 1.2` 不符合 `ECMAScript` 的第一版，尽管 `ECMAScript` 原本应该是基于 `JavaScript 1.1`。

`JScript` 的下一次更新发生在 `Internet Explorer 4` 中，版本为 `JScript 3.0`（版本 `2.0` 在 `Microsoft Internet Information Server` 版本 `3.0` 中发布，但从未包含在浏览器中）。微软发布了一份新闻稿，吹捧 `JScript 3.0` 是世界上第一个真正符合 `Ecma` 标准的脚本语言。当时，`ECMA-262` 尚未定稿，因此 `JScript 3.0` 遭遇了与 `JavaScript 1.2` 相同的命运：它符合最终的 `ECMAScript` 标准。

`Netscape` 选择在 `Netscape Navigator 4.06` 中将其 `JavaScript` 实现更新为 `JavaScript 1.3`，这使得 `Netscape` 完全符合 `ECMA-262` 的第一版。`Netscape` 增加了对 `Unicode` 标准的支持，并使所有对象独立平台，同时保留了在 `JavaScript 1.2` 中引入的特性。



当 Netscape 作为 `Mozilla` 项目向公开源代码时，人们预计 `JavaScript 1.4` 将随 Netscape Navigator 5 发布。然而，一个从底部开始完全重新设计 Netscape 代码的激进决定偏离了这一努力。`JavaScript 1.4` 仅作为 Netscape 服务器端语言发布，从未进入浏览器。

到 2008 年，五大浏览器（Internet Explorer、Firefox、Safari、Chrome 和 Opera）都符合 ECMA-262 的第三版。Internet Explorer 8 是第一个实现第五版的浏览器。Firefox 4 随其后。下表列出了主流浏览器的 ECMAScript 支持情况。

| 浏览器 | ECMAScript 合规性 |
| --- | --- |
| Netscape Navigator 2 | |
| Netscape Navigator 3 | |
| Netscape Navigator 4–4.05 | |
| Netscape Navigator 4.06–4.79 | 第一版 |
| Netscape Navigator 6+ (Mozilla 0.6+) | 第三版 |
| Internet Explorer 3 | |
| Internet Explorer 4 | |
| Internet Explorer 5 | 第一版 |
| Internet Explorer 5.5–7 | 第三版 |
| Internet Explorer 8 | 第五版 |
| Internet Explorer 9+ | 第五版 |
| Opera 6–7.1 | 第二版 |
| Opera 7.2+ | 第三版 |
| Safari 1–2.0.x | 第三版 |
| Safari 3.x | 第三版 |
| Safari 4.x–5.x | 第五版 |
| Chrome 1+ | 第三版 |
| Firefox 1–2 | 第三版 |
| Firefox 3.0.x | 第三版 |
| Firefox 3.5–3.6 | 第五版 |
| Firefox 4+ | 第五版 |

*不完整的实现

## 文档对象模型 (DOM)

文档对象模型 (DOM) 是用于 XML 的应用程序编程接口 (API)，已扩展用于 HTML。DOM 将整个页面映射为节点的层次结构。HTML 或 XML 页面的每个部分都是某种类型的节点，包含不同的数据。考虑以下 HTML 页面：

```html
<html>
    <head>
        <title>示例页面</title>
    </head>
    <body>
        <p>Hello World!</p>
    </body>
</html>
```

此代码可以使用 DOM 绘制成节点层次结构图（参见图 1-2）。

通过创建树来表示文档，DOM 允许开发者对内容和结构进行前所未有的控制。通过使用 DOM API 可以轻松地删除、添加、替换和修改节点。

## 为什么 DOM 是必要的

随着 Internet Explorer 4 和 Netscape Navigator 4 分别支持不同形式的动态 HTML（DHTML），开发者首次可以在无需重新加载网页的情况下更改网页的外观和内容。这代表了网页技术的巨大飞跃，但也带来了一个巨大的问题。Netscape 和微软在开发 DHTML 方面分道扬扬，从而结束了开发者可以编写一个可被任何网页浏览器访问的单个 HTML 页面的时代。

人们决定必须采取措施来维护 Web 的跨平台特性。当时人们担心，如果不约束 Netscape 和微软，Web 将发展成两个截然不同的、仅针对特定浏览器的派系。于是，负责创建网页通信标准的组织的世界维网联盟（W3C）开始研究 DOM。

# DOM 级规范

DOM Level 1 于 1998 年 10 月成为 W3C 推荐标准。它由两个模块组成：`DOM Core`，它提供了一种将基于 `XML` 的文档结构映射的方法，以便于访问和操作文档的任何部分；以及 `DOM HTML`，它通过添加 HTML 特有的对象和方法扩展了 `DOM Core`。

![image](img/pen.gif)

请注意，`DOM` 并不是 JavaScript 特有的，实际上它已经在许多其他语言中实现。然而，对于网页浏览器，`DOM` 是使用 `ECMAScript` 实现的，现在构 JavaScript 语言的大大部分。

`DOM Level 1` 的目标是映射文档结构，而 `DOM Level 2` 的目标要广泛得多。这一对原始 `DOM` 的扩展增加了对鼠标和用户界面事件（DHTML 长期支持）、范围（ranges）、遍历（迭代 DOM 文档的方法）以及通过对象接口对级联样式表（CSS）的支持。在 Level 1 中引入的原始 `DOM Core` 也被扩展，以包含对 `XML 命名空间`的支持。

DOM Level 2 引入了以下 `DOM` 新模块来处理新类型的接口：

* `DOM Views` — 描述用于跟踪文档各种视图的接口（例如，CSS 样式化之前后的文档）
* `DOM Events` — 描述事件和事件处理的接口
* `DOM Style` — 描述处理元素 CSS 样式的接口
* `DOM Traversal and Range` — 描述遍历和操作文档树的接口

DOM Level 3 通过引入以统一方式加载和保存文档的方法（包含在一个名为 `DOM Load and Save` 的新模块中）以及验证文档的方法（`DOM Validation`）进一步扩展了 `DOM`。在 Level 3 中，`DOM Core` 被扩展以支持所有的 `XML 1.0`，包括 `XML Infoset`、`XPath` 和 `XML Base`。

![image](img/pen.gif)

在阅读关于 `DOM` 的内容时，你可能会遇到 `DOM Level 0`。请注意，并没有名为 `DOM Level 0` 的标准；它只是 DOM 历史上的一个参考点。`DOM Level 0` 被认为是 Internet Explorer 4.0 和 Netscape Navigator 4.0 支持的原始 DHTML。

# 其他 DOM

除了 `DOM Core` 和 `DOM HTML` 接口外，其他几种语言也发布了自己的 DOM 标准。列表中的语言都是基于 XML 的，每个 `DOM` 都添加了特定语言语言的方法和接口：

* 可缩矢量图形 (SVG) 1.0
* 数学标记语言 (MathML) 1.0
* 同步多媒体集成语言 (SMIL)

此外，其他语言也开发了自己的 DOM 实现，例如 Mozilla 的 XML 用户界面语言 (XUL)。然而，只有上述列表中的语言是 W3C 的标准建议。

# 浏览器中的 DOM 支持

在网页浏览器开始实现 DOM 之前，`DOM` 已经作为标准了一段时间。Internet Explorer 在版本 5 中进行了首次尝试，但在版本 5.5 之前它没有任何实际的 DOM 支持，该版本实现了 `DOM Level 1` 的大部分内容。Internet Explorer 在版本 6 和 7 中没有引入新的 DOM 功能，尽管版本 8 引入了一些错误修复。

对于 Netscape 来说，在 Netscape 6 (Mozilla 0.6.0) 推出之前不存在 DOM 支持。在 Netscape 7 之后，Mozilla 将开发重心转向 Firefox 浏览器。Firefox 3+ 支持所有的 Level 1、几乎所有的 Level 2 以及 Level 3 的部分内容。（Mozilla 开发团队的目标是构建一个 100% 符合标准的浏览器，他们的努力付出了回报。）

DOM 支持成为大多数浏览器厂商的首要任务，他们一直持续努力在每个发布版本中改进支持。下表显示了流行浏览器的 DOM 支持情况。

| 浏览器 | DOM 合规性 |
| --- | --- |
| Netscape Navigator 1.–4.x | — |
| Netscape 6+ (Mozilla 0.6.0+) | Level 1, Level 2 (几乎所有), Level 3 (部分) |
| Internet Explorer 2–4.x | — |
| Internet Explorer 5 | Level 1 (极少) |
| Internet Explorer 5.5–8 | Level 1 (几乎所有) |
| Internet Explorer 9+ | Level 1, Level 2, Level 3 |
| Opera 1–6 | — |
| Opera 7–8.x | Level 1 (几乎所有), Level 2 (部分) |
| Opera 9–9.9 | Level 1, Level 2 (几乎所有), Level 3 (部分) |
| Opera 10+ | Level 1, Level 2, Level 3 (部分) |
| Safari 1.0.x | Level 1 |
| Safari 2+ | Level 1, Level 2 (部分) |
| Chrome 1+ | Level 1, Level 2 (部分) |
| Firefox 1+ | Level 1, Level 2 (几乎所有), Level 3 (部分) |

# 浏览器对象模型 (BOM)

Internet Explorer 3 和 Netscape Navigator 3 引入了浏览器对象模型 (BOM)，允许访问和操作浏览器窗口。使用 BOM，开发者可以与其显示页面之外与浏览器交互。让 BOM 变得真正独特且经常引发问题的是，它是 JavaScript 中唯一没有标准的部分。这随着 HTML5 的引入发生了改变，HTML5 试图将大部分 BOM 规范化。

BOM 主要处理浏览器窗口和框架，但通常任何针对 JavaScript 的浏览器特定扩展都被视为 BOM 的一部分。以下是一些扩展内容：

* 弹出新浏览器窗口的能力
* 移动、调整大小和关闭浏览器窗口的能力
* `navigator` 对象，提供有关浏览器的详细信息
* `location` 对象，提供有关浏览器中加载页面的详细信息
* `screen` 对象，提供有关用户分辨率的详细信息
* 对 cookie 的支持
* 自定义对象，如 `XMLHttpRequest` 和 Internet Explorer 的 `ActiveXObject`

由于 BOM 长期没有标准，每个浏览器都有自己的实现。存在一些事实上的标准，例如窗口对象和 `navigator` 对象，但每个浏览器都为这些和其他对象定义了自己的属性和方法。随着 HTML5 的可用，预计 BOM 的实现细节将以更兼容的方式增长。关于 BOM 的详细讨论包含在第 8 章。

## JavaScript 版本

Mozilla 作为原始 Netscape 的后代，是唯一延续原始 JavaScript 版本命名序列浏览器厂商。当 Netscape 源代码拆分为开源项目（命名为 Mozilla 项目）时，最后一个浏览器版本是 1.3（如前所述，版本 1.4 仅在服务器端实现）。随着 Mozilla 基金继续开发 JavaScript，添加新功能、关键字和语法，JavaScript 版本号不断递增。下表显示了 Netscape/Mozilla 浏览器的 JavaScript 版本演进。

| 浏览器 | JavaScript 版本 |
| --- | --- |
| Netscape Navigator 2 | 1.0 |
| Netscape Navigator 3 | 1.1 |
| Netscape Navigator 4 | 1.2 |
| Netscape Navigator 4.06 | 1.3 |
| Netscape 6+ (Mozilla 0.6.0+) | 1.5 |
| Firefox 1 | 1.5 |
| Firefox 1.5 | 1.6 |
| Firefox 2 | 1.7 |
| Firefox 3 | 1.8 |
| Firefox 3.5 | 1.8.1 |
| Firefox 3.6 | 1.8.2 |

该命名方案是基于这样一个想法：`Firefox 4` 将引入 JavaScript 2.0，而在此之前版本号的每次递增都表示 JavaScript 的实现距离 2.0 提案有多有多近。尽管这是最初的计划，但 JavaScript 的演进方式使得这种方案已不再可行。目前尚无 JavaScript 2.0 的目标实现。

![image](img/pen.gif)

需要注意的是，只有 Netscape/Mozilla 浏览器遵循这一版本命名方案。例如，Internet Explorer 的 JScript 有不同的版本号。这些 JScript 版本与前表提到的 JavaScript 版本完全没有对应。此外，大多数浏览器在谈论 JavaScript 支持时，是相对于其 ECMAScript 合规性水平和 DOM 支持的。

## 总结

JavaScript 是一种旨在与网页交互的脚本语言，由以下三个不同的部分组成：

* `ECMAScript`，定义在 `ECMA-262` 中，并提供核心功能
* `文档对象模型` (`DOM`)，提供了处理网页内容的方法和接口
* `浏览器对象模型` (`BOM`)，提供了与浏览器交互的方法和接口

五大主流 浏览器（Internet Explorer、Firefox、Chrome、Safari 和 Opera）对 JavaScript 的这三个部分的支持程度各不相同。所有浏览器对 `ECMAScript 3` 的支持通常良好，对 `ECMAScript 5` 的支持正在增长，而对 `DOM` 的支持差异很大。最近在 `HTML5` 中规范化的 `BOM` 可能会随浏览器而异，尽管有一些被假设为可用的共性。

# 第 2 章：HTML 中的 JavaScript

### 本章内容包含？

* 使用 `<script>` 元素
* 比较内联脚本和外部脚本
* 检查 `document modes` 如何影响 JavaScript
* 为禁用 JavaScript 的体验做准备

JavaScript 引入网页时立即遭遇了 Web 的主导语言 `HTML`。在对 JavaScript 的早期工作中，Netscape 尝试解决如何让 JavaScript 在 HTML 页面中共存，同时又不破坏这些页面在其他浏览器中的渲染。通过尝试、错误和争议，最终做出并达成了几项决定，为 Web 带来了通用的脚本支持。Web 早期的大部分工作一直延续，并在 `HTML` 规范中正式化。

### `<SCRIPT>` 元素

将 JavaScript 插入 HTML 页面的主要方法是通过 `<script>` 元素。该元素由 Netscape 创建，并首次在 `Netscape Navigator 2` 中实现。它后来被添加到正式的 `HTML` 规范中。`<script>` 元素六六属性：

* `async` — 可选。表示脚本应立即开始下载，但不应阻止页面上的其他操作（如下载资源或等待其他脚本加载）。仅对外部脚本文件有效。
* `charset` — 可选。使用 `src` 属性指定的代码字符集。此属性很少使用，因为大多数浏览器不理会它的值。
* `defer` — 可选。表示脚本的执行可以安全地推到文档内容完全解析并显示之后。仅对外部脚本有效。`Internet Explorer 7` 及更版本也允许内联脚本。
* `language` — 已废弃。最初指示代码块使用的脚本语言（如 "JavaScript"、JavaScript1.2" 或 "VBScript"）。大多数浏览器忽略此属性；不应使用它。
* `src` — 可选。指示包含要执行代码的外部文件。
* `type` — 可选。替换 `language`；指示代码块使用的脚本语言的内容类型（也称为 MIME 类型）。传统上，此值一直是 `"text/javascript"`，尽管 `"text/javascript"` 和 `"text/ecmascript"` 均已废弃。JavaScript 文件通常使用 `"application/x-javascript"` MIME 类型提供服务，尽管在 `type` 属性中设置此值可能会导致脚本被忽略。在非 Internet Explorer 浏览器中有效的其他值是 `"application/javascript"` 和 `"application/ecmascript"`。按照惯例，`type` 属性通常仍设置为 `"text/javascript"` 以获得最大的浏览器兼容性。此属性可以安全地省略，因为在缺失时会假设为 `"text/javascript"`。

使用 `<script>` 元素有两种方式：将 JavaScript 代码直接嵌入页面中，或从外部文件引入 JavaScript。

要包含内联 JavaScript 代码，请将 JavaScript 代码直接放在 `<script>` 元素内部，如下：

```html
<script type="text/javascript">
    function sayHi(){
        alert("Hi!");
    }
</script>
```

包含在 `<script>` 元素内的 JavaScript 代码从上到下进行解析。在本例中，函数定义被解析并存储在解释器环境中。在 `<script>` 元素内的所有代码都求值之前，页面的其余内容不会加载和/或显示。

使用内联 JavaScript 代码时，请记住你不能在代码的任何地方出现字符串 `"</script>"`。例如，以下代码在加载到浏览器时会导致错误：

```html
<script type="text/javascript">
    function sayScript(){
        alert("</script>");
    }
</script>
```

由于内联脚本的解析方式，浏览器会将 `"</script>"` 视为闭合标签 `</script>`。可以通过转义 `/` 字符来轻松避免此问题，如下例所示：



```
<script type="text/javascript">
    function sayScript(){
        alert("<\/script>");
    }
</script>
```

对代码的更改使浏览器接受且不会引起任何错误。

要从外部文件引入 JavaScript，需要 `src` 属性。`src` 的值是指向代码文件的 URL，如下：

```
<script type="text/javascript" src="example.js"></script>
```

在此例中，名为 `example.js` 的外部文件被加载到页面中。文件本身只需要包含位于 `<script>` 和 `</script>` 标签之间的 JavaScript 代码。与内联 JavaScript 代码一样，解析外部文件时页面处理会停止。（下载文件也需要一些时间。）

在 XHTML 文档中，你可以省略闭合标签，如下：

```
<script type="text/javascript" src="example.js" />
```

这种语法不应在 HTML 文档中使用，因为它是无效的 HTML，且某些浏览器无法正确处理。

按照习惯，外部 JavaScript 文件具有 `.js` 扩展名。这并不是强制要求，因为浏览器不会检查引入的 JavaScript 文件的扩展名。这留下了使用 `JSP`、`PHP` 或另一种服务器端脚本语言动态生成 JavaScript 代码的可能性。但请记住，服务器通常使用文件扩展名来确定应用于响应的正确 MIME 类型。如果你不使用 `.js` 扩展名，请双检你的服务器是否返回了正确的 MIME 类型。

注意的是，使用 `src` 属性的 `<script>` 元素不应在 `<script>` 和 `</script>` 标签之间包含额外的 JavaScript 代码。如果两者都提供，脚本文件将被下载并执行，而内联代码将被忽略。

`<script>` 元素最强大且最具争议的部分之一是它包含其他域的 JavaScript 文件的能力。类似于 `<img>` 元素，`<script>` 元素的 `src` 属性可以被设置为存在 HTML 页面所在域之外的完整 URL，如下例所示：

```
<script type="text/javascript" src="http://www.somewhere.com/afile.js"></script>
```

来自外部域的代码将被加载并解析，就就像它是加载它的页面的一部分一样。这种能力允许你在必要时从各个域提供 JavaScript。但是，如果你引用了位于你不控制的服务器上的 JavaScript 文件，请务必小心。恶意程序员可能会随时替换该文件。在包含来自不同域的 JavaScript 文件时，请确保你是该域的所有者，或者该域由受信任的源所有。

无论代码如何包含，只要不存在 `defer` 和 `async` 属性，`<script>` 元素按照它们在页面中出现的顺序进行解析。第一个 `<script>` 元素的代码在第二个 `<script>` 元素开始解析之前必须被完全解析，第二个在第三个之前必须完成，依此类推。

### 标签位置

传统上，所有的 `<script>` 元素都放置在页面的 `<head>` 元素内，如下例：

```
<!DOCTYPE html>
<html>
  <head>
    <title>Example HTML Page</title>
    <script type="text/javascript" src="example1.js"></script>
    <script type="text/javascript" src="example2.js"></script>
  </head>
  <body>
    <!-- content here -->
  </body>
</html>
```

这种格式的主要目的是将外部文件引用（包括 CSS 文件和 JavaScript 文件）保持在同一个区域。然而，在文档的 `<head>` 中包含所有的 JavaScript 文件意味着在页面开始渲染之前（浏览器接收到 `<body>` 标签时开始渲染）必须下载、解析并解释所有的 JavaScript 代码。对于需要大量 JavaScript 代码的页面，这会导致页面渲染出现明显的延迟，在此期间浏览器将完全空白。由于由于原因，现代 Web 应用程序通常将所有 JavaScript 引用放在 `<body>` 元素中，位于页面内容之后，如下例：

```
<!DOCTYPE html>
<html>
  <head>
    <title>Example HTML Page</title>
  </head>
  <body>
    <!-- content here -->
    <script type="text/javascript" src="example1.js"></script>
    <script type="text/javascript" src="example2.js"></script>
  </body>
</html>
```

使用这种方法，页面在 JavaScript 代码被处理之前已经在浏览器中完全渲染。结果的用户体验被感知为更快，因为在空白浏览器窗口上花费的时间减少了。

### 延迟脚本

HTML 4.01 为 `<script>` 元素定义了一个名为 `defer` 的属性。`defer` 的目的是指示脚本在执行时不会更改页面的结构。因此，脚本可以在整个页面解析后安全地运行。在 `<script>` 元素上设置 `defer` 属性向浏览器信号应该立即开始下载，但执行应该推迟：

```
<!DOCTYPE html>
<html>
  <head>
    <title>Example HTML Page</title>
    <script type="text/javascript" defer src="example1.js"></script>
    <script type="text/javascript" defer src="example2.js"></script>
  </head>
  <body>
    <!-- content here -->
  </body>
</html>
```

尽管此示例中的 `<script>` 元素包含在文档的 `<head>` 中，但在浏览器接收到闭合的 `</html>` 标签之前它们不会执行。HTML5 规范规定脚本将按照它们出现的顺序执行，因此第一个延迟脚本会在第二个延迟脚本之前执行，两者都将在 `DOMContentLoaded` 事件之前执行（更多信息请参阅第 13 章）。然而，实际上，延迟脚本并不总是按顺序执行，或在 `DOMContentLoaded` 事件之前执行，因此在情况下最好只包含一个。

如之前所述，`defer` 属性仅支持外部脚本文件。这是 HTML5 中做出的一项说明，因此支持 HTML5 实现的浏览器在内联脚本上设置 `defer` 时将忽略它。Internet Explorer 4–7 都表现出旧行为，而 Internet Explorer 8 及以上版本则支持 HTML5 行为。

对 `defer` 属性的支持从 Internet Explorer 4、Firefox 3.5、Safari 5 和 Chrome 7 开始添加。所有其他浏览器简单地忽略此属性，并像常一样处理脚本。由于由于原因，最好仍然将延迟脚本放在页面底部。

![image](img/pen.gif)

对于 XHTML 文档，将 `defer` 属性指定为 `defer="defer"`。

### 异步脚本

HTML5 为 `<script>` 元素引入了 `async` 属性。`async` 属性类似于 `defer`，因为它改变了处理脚本的方式。同样与 `defer` 类似，`async` 仅适用于外部脚本，并向浏览器信号立即下载文件。与 `defer` 不同，标记为 `async` 的脚本不保证按照它们指定的顺序执行。例如：

```
<!DOCTYPE html>
<html>
  <head>
    <title>Example HTML Page</title>
    <script type="text/javascript" src="example1.js"></script>
    <script type="text/javascript" src="example2.js"></script>
  </head>
  <body>
    <!-- content here -->
  </body>
</html>
```

使用这种方法，页面在 JavaScript 代码被处理之前已经在浏览器中完全渲染。结果的用户体验被感知为更快，因为在空白浏览器窗口上花费的时间减少了。



对`defer`属性的支持从 Internet Explorer 4、Firefox 3.5、Safari 5 和 Chrome 7 开始添加。所有其他浏览器简单地忽略此属性，并像常一样处理脚本。由于由于原因，最好仍然将延迟脚本放在页面底部。

![image](img/pen.gif)

对于 XHTML 文档，将`defer`属性指定为`defer="defer"`。

### 异步脚本

HTML5 为`<script>`元素引入了`async`属性。`async`属性类似于`defer`，因为它改变了处理脚本的方式。同样与`defer`类似，`async`仅适用于外部脚本，并向浏览器信号立即下载文件。与`defer`不同，标记为`async`的脚本不保证按照它们指定的顺序执行。例如：

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Example HTML Page</title>
    <script type="text/javascript" src="example1.js"></script>
    <script type="text/javascript" src="example2.js"></script>
  </head>
  <body>
    <!-- content here -->
  </body>
</html>
```

使用这种方法，页面在 JavaScript 代码被处理之前已经在浏览器中完全渲染。结果的用户体验被感知为更快，因为在空白浏览器窗口上花费的时间减少了。*(注：原文此处存在逻辑重复，此处已合并逻辑翻译)*

### XHTML 中的更改

Extensible HyperText Markup Language，或 XHTML，是 HTML 作为 XML 应用的一种重构。在 XHTML 中编写代码的规则比 HTML 更严格，这影响了在使用 JavaScript 代码的`<script>`元素。虽然在 HTML 中有效，以下代码块在 XHTML 中是无效的：

```html
<script type="text/javascript">
    function compare(a, b) {
        if (a < b) {
            alert("A is less than B");
        } else if (a > b) {
            alert("A is greater than B");
        } else {
            alert("A is equal to B");
        } 
    }
</script>
```

在 HTML 中，`<script>`元素对其内容的解析有特殊规则；在 XHTML 中，这些特殊规则并不适用。这意味着语句`a < b`中的小于号（`<`）被解释为标签的开头，导致语法错误，因为小于号后面不能有空格。

修复 XHTML 语法错误有两种方法。第一种是将所有的小于号（`<`）替换为它的 HTML 实体（`&lt;`）。生成的代码如下：

```html
<script type="text/javascript">
    function compare(a, b) {
        if (a &lt; b) {
            alert("A is less than B");
        } else if (a > b) {
            alert("A is greater than B");
        } else {
            alert("A is equal to B");
        } 
    }
</script>
```

这段代码现在可以在 XHTML 页面中运行；然而，代码的可读性稍差。幸运的是，还有另一种方法。

将此代码转换为有效 XHTML 版本的另一种方法是将 JavaScript 代码封装在 CDATA 节区中。在`XHTML`（以及`XML`）中，`CDATA`节用于指示文档中包含不打算解析的自由格式文本的区域。这允许你使用任何字符（包括小于符号），而不会产生语法错误。其格式如下：

```html
<script type="text/javascript"><![CDATA[
    function compare(a, b) {
        if (a < b) {
            alert("A is less than B");
        } else if (a > b) {
            alert("A is greater than B");
        } else {
            alert("A is equal to B");
        } 
    }
]]></script> 
```

在符合`XHTML`标准的浏览器中，这解决了问题。然而，许多浏览器仍然不符合`XHTML`标准且不支持`CDATA`节区。为了解决这个问题，必须通过 JavaScript 注释来对`CDATA`标记进行偏移：

```html
<script type="text/javascript">
//<![CDATA[
    function compare(a, b) {
        if (a < b) {
            alert("A is less than B");
        } else if (a > b) {
            alert("A is greater than B");
        } else {
            alert("A is equal to B");
        } 
    }
//]]>
</script> 
```

这种格式在所有现代浏览器中均有效。虽然有一点“黑客技巧”的味道，但它可以通过`XHTML`验证并为`XHTML`之前的浏览器实现良好的降级。

![image](img/pen.gif)

当页面指定其 MIME 类型为 `"application/xhtml+xml"` 时，会触发`XHTML`模式。并不是所有浏览器都正式支持以这种方式提供的`XHTML`。

## 已弃语法

当`<script>`元素最初引入时，它标志着对传统 HTML 解析方式的偏离。在该元素内部需要应用特殊规则，这给不支持 JavaScript 的浏览器带来了麻烦（最著名的是`Mosaic`）。不支持的浏览器会将`<script>`元素的内容输出到页面上，这实际上破坏了页面的外观。

Netscape 与`Mosaic`合作想出了一种解决方案，可以向不支持 JavaScript 的浏览器隐藏嵌入的 JavaScript 代码。最终解决方案是将脚本代码封装在 HTML 注释中，如下所示：

```html
<script><!--
    function sayHi(){
        alert("Hi!");
    }
//--></script>
```

使用这种格式，像`Mosaic`这样的浏览器会安全地忽略`<script>`标签内部的内容，而支持 JavaScript 的浏览器必须寻找这种模式以识别确实有需要解析的 JavaScript 内容。

尽管这种格式仍然被所有网络浏览器正确识别和解释，但它已不再需要且不应被使用。在`XHTML`模式下，这会导致脚本被忽略，因为它位于有效的 XML 注释内部。

## 内联代码与外部文件

虽然可以直接在 HTML 文件中嵌入 JavaScript，但通常认为的最佳实践是尽可能使用外部文件包含尽可能多的 JavaScript。请记住，关于这种做法并没有硬性规定，但使用外部文件的理由如下：

- **可维护性**：散落在各个 HTML 页面中的 JavaScript 代码会使代码维护变成一个问题。为所有 JavaScript 文件建立一个目录要比现在易得多，这样开发者就可以独立于其所使用的标记来编辑 JavaScript 代码。
- **缓存**：浏览器根据特定设置缓存所有外部链接的 JavaScript 文件，这意味着如果两个页面使用同一个文件，该文件只下载一次。这最终意味着更快的页面加载速度。
- **未来性**：通过外部文件包含 JavaScript，就不需要使用之前提到的`XHTML`或注释黑客技巧了。包含外部文件的语法在 HTML 和`XHTML`中是相同的。

## 文档模式

Internet Explorer 5.5 通过切换 doctype 引入了文档模式的概念。前两种文档模式是`怪异模式`（quirks mode），它让 Internet Explorer 表现得像第 5 版本（带有若干非标准功能），以及`标准模式`（standards mode），它让 Internet Explorer 的行为更符合标准。尽管这两种模式之间的主要区别与 CSS 的内容渲染有关，但也有一些与 JavaScript 相关的副作用。这些副作用在书中各处都有讨论。

自从 Internet Explorer 首次引入文档模式概念以来，其他浏览器也纷纷效仿。随着这种采用的发生，出现了第三种名为`几乎标准模式`（almost standards mode）的模式。该模式具有`标准模式`的许多功能，但不那么严格。主要区别在于对图像周围间距的处理（当在表格中使用图像时最为明显）。

在所有浏览器中通过省略文档开头的 doctype 来实现`怪异模式`。这被认为是一种糟糕的做法，因为`怪异模式`在所有浏览器中的差异很大，在不使用黑客技巧的情况下无法实现任何程度的真实浏览器一致。

使用以下 doctype 之一会开启`标准模式`：

```html
<!-- HTML 4.01 Strict -->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
"http://www.w3.org/TR/html4/strict.dtd">

<!-- XHTML 1.0 Strict -->
<!DOCTYPE html PUBLIC
"-//W3C//DTD XHTML 1.0 Strict//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">

<!-- HTML5 -->
<!DOCTYPE html>
```

使用以下 doctype 会触发`几乎标准模式`：

```html
<!-- HTML 4.01 Transitional -->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
"http://www.w3.org/TR/html4/loose.dtd">

<!-- HTML 4.01 Frameset -->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
"http://www.w3.org/TR/html4/frameset.dtd">

<!-- XHTML 1.0 Transitional -->
<!DOCTYPE html PUBLIC
"-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<!-- XHTML 1.0 Frameset -->
<!DOCTYPE html PUBLIC
"-//W3C//DTD XHTML 1.0 Frameset//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">
```

由于`几乎标准模式`与`标准模式`非常接近，因此很少进行这种区分。谈论“标准模式”的人指的是其中任何一种，文档模式检测（稍后讨论）也没有做这种区分。在书中，`标准模式`一词是指`怪异模式`之外的任何模式。

## `<noscript>`元素

早期浏览器特别担心在不支持 JavaScript 时的页面优雅降级。为此，创建了`<noscript>`元素为无 JavaScript 的浏览器提供替代内容。该元素可以包含`<script>`之外的任何 HTML 元素。`<noscript>`元素包含的内容仅在以下两种情况下显示：

- 浏览器不支持脚本。
- 浏览器的脚本支持被关闭。

如果满足其中一个条件，`<noscript>`元素内部的内容就会渲染。在所有其他情况下，浏览器都不会渲染`<noscript>`的内容。

这是一个简单的示例：

```html
<!DOCTYPE html>
<html>
  <head>
    <title>示例 页面</title>
    <script type="text/javascript" defer="defer" src="example1.js"></script>
    <script type="text/javascript" defer="defer" src="example2.js"></script>
  </head>
  <body>
    <noscript>
      <p>此页面需要启用 JavaScript 的浏览器。</p>
    </noscript>
  </body>
</html>
```

在这个示例中，当脚本不可用时会向用户显示一条消息。对于启用了脚本的浏览器，这条消息永远可见，尽管它仍然是页面的一部分。

## 摘要

JavaScript 通过`<script>`元素插入到 HTML 页面中。该元素可以将 JavaScript 嵌入到 HTML 页面中，使其与其他标记保持内联状态，也可以包含存在于外部文件的 JavaScript。以下是关键点：

- 要包含外部 JavaScript 文件，必须将`src`属性设置为要包含的文件的 URL，该文件可以是与包含页面在同一服务器上的文件，也可能是位于完全不同域上的文件。
- 所有的`<script>`元素按照它们在页面上出现的顺序进行解释。只要不使用`defer`和`async`属性，`<script>`元素中包含的代码在下一个`<script>`元素代码开始执行之前必须被完全解释。
- 对于非延迟脚本，浏览器在继续渲染页面其他部分之前，必须完成对`<script>`元素内部代码的解释。由于这个原因，`<script>`元素通常包含在页面的末尾，位于主内容之后、闭合的`</body>`标签之前。
- 你可以使用`defer`属性将脚本的执行推迟到文档渲染之后。延迟脚本总是按照它们被指定的顺序执行。
- 你可以使用`async`属性指示脚本不需要等待其他脚本，也不会阻塞文档渲染。异步脚本不保证按照它们在页面中出现的顺序执行。

通过使用`<noscript>`元素，你可以指定只有在浏览器不支持脚本支持时才显示内容。如果浏览器启用了脚本，`<noscript>`元素中包含任何内容将不会被渲染。

# 第 3 章：语言基础

## 本章包含内容？

- 复习语法
- 处理数据类型
- 处理流程控制语句
- 理解函数

任何语言的核心都是关于其在最基础层面如何运行的描述。这种描述通常定义了语法、操作符、数据类型和内置功能，在这些基础之上可以构建复杂的解决方案。正如之前提到的，`ECMA-262`以一种名为`ECMAScript`的伪语言的形式定义了 JavaScript 的所有信息。

根据`ECMA-262`第三版定义的`ECMAScript`是浏览器中实现程度最高的版本。第五版是浏览器中下一个要实现的版本，但尽管截至 2011 年底，还没有浏览器完全实现它。因此，以下信息主要基于`ECMAScript`。

`ECMA-262`第三版定义的`ECMAScript`是 Web 浏览器中实现次数最多的版本。第五版是浏览器中下一个要实现的版本，尽管截至 2011 年底，还没有浏览器完全实现它。因此，以下信息主要基于`ECMAScript`。

## 语法

`ECMAScript`的语法大量借鉴了 C 语言。熟悉此类语言的开发者可以轻松适应`ECMAScript`的语法。

### 大小写敏感

要理解的第一个概念是它是区分大小写的；变量名、函数名等都是区分大小写的，这意味着`test`和`Test`是不同的。

### 标识符

标识符是变量、函数或属性的名称。在`ECMAScript`中，标识符遵循以下规则：

- 标识符可以是字母、数字、下划线`_`或美元符号`$`。
- 标识符不能以数字开头。
- 标识符不能是保留关键字。
- 标识符不能包含空格。

`ECMAScript`标识符遵循以下格式，例如：

```javascript
var sum = 10;
var _total = 20;
var $amount = 30;
var count2 = 40;
```

### 注释

`ECMAScript`使用单行注释和块注释。单行注释以`//`开始，例如：

```javascript
// 这是一个单行注释
```

块注释以`/*`开始，并以`*/`结束，例如：

```javascript
/* 
这是一个多行
注释 
*/
```

### 严格模式

`ECMAScript` 5 引入了严格模式的概念。严格模式改变了 JavaScript 的许多执行方式，因此在书中会指出严格模式的差异。

如果你想为整个脚本启用严格模式，可以在顶部包含以下指令（推荐做法）：

```javascript
"use strict";
```

你也可以通过在函数体顶部包含该指令来指定函数在严格模式下执行：

```javascript
function doSomething(){
    "use strict";
    // 函数体
}
```

## 语句

`ECMAScript`的语句以分号结束，尽管省略分号会让解析器确定语句的结束位置，如下所示：

```javascript
var sum = a + b        // 无分号有效，但不推荐推荐
var diff = a - b;      // 有分号有效，推荐
```



尽管语句末尾不强制要求分号，但建议始终包含。包含分号有助于防止遗漏错误（例如未完成输入），并允许开发者通过移除额外的空白符来压缩 ECMAScript 代码（这种压缩在行没有分号时会导致语法错误）。在某些情况下，包含分号还可以提高性能，因为解析器会尝试在认为应该存在的地方插入分号。

```
break              do              instanceof         typeof
case               else            new                var
catch              finally         return             void
continue           for             switch             while
debugger*          function        this               with
default            if              throw
delete             in              try
```

规范还描述了一组保留字，这些字不能用作标识符或属性名。虽然保留字在语言中没有特定的用途，但它们是被预留的。

```
`break` `do` `instanceof` `typeof`
`case` `else` `new` `var`
`catch` `finally` `return` `void`
`continue` `for` `switch` `while`
`debugger*` `function` `this` `with`
`default` `if` `throw`
`delete` `in` `try`
```

---

## 数据类型

ECMAScript 中有种简单数据类型（也称为原始类型）：`Undefined`、`Null`、`Number` 和 `String`。还有一种复杂数据类型 `Object`，它是一个键值对的无序列表。由于在 ECMAScript 中无法定义自己的数据类型，所有值都可以表示为这六种类型之一。只有六种数据类型似乎不足以表示所有数据；然而，ECMAScript 的数据类型具有动态特性，使得每个数据类型的行为都像多个类型。

### `typeof` 运算符

由于 ECMAScript 是弱类型的，因此需要一种方法来确定给定变量的数据类型。`typeof` 运算符提供了这种信息。在值上使用 `typeof` 运算符会返回以下字符串之一：

- 如果值为 `undefined`，则返回 `"undefined"`。
- 如果值为 `Boolean`，则返回 `"boolean"`。
- 如果值为 `string`，则返回 `"string"`。
- 如果值为 `number`，则返回 `"number"`。
- 如果值为 `object`（函数除外）或 `null`，则返回 `"object"`。
- 如果值为 `function`，则返回 `"function"`。

`typeof` 运算符的调用方式如下：

![image](img/logo1.gif)

```javascript
var message = "some string";
alert(typeof message);    //"string"
alert(typeof(message));   //"string"
alert(typeof 95);         //"number"
```

`TypeofExample01.htm`

在这个示例中，变量 `message` 和数字字面量都被传递给了 `typeof` 运算符。注意，由于 `typeof` 是一个运算符而不是函数，因此不需要括号（尽管可以使用括号）。

请注意，在某些情况下，`typeof` 返回的似乎是一个令人困惑但在技术上是正确的值。调用 `typeof null` 返回的值 `"object"`，因为特殊值 `null` 被认为是一个空对象引用。Safari 5 及之前的版本和 Chrome 7 及之前的版本存在一个特性，即对正则表达式调用 `typeof` 会返回 `"function"`，而所有其他浏览器都返回 `"object"`。

![image](img/pen.gif)

从技术上讲，在 ECMAScript 中，函数被视为对象，并不代表另一种数据类型。然而，它们确实具有一些特殊属性，这使得有必要通过 `typeof` 运算符将函数与其他对象区分开来。

## 未定义类型（Undefined）

`Undefined` 类型只有一个值，即特殊值 `undefined`。当使用 `var` 声明变量但未对其初始化时，它会被赋值为 `undefined`，如下所示：

![image](img/logo1.gif)

```javascript
var message;
alert(message == undefined);    //true
```

`UndefinedExample01.htm`

在这个示例中，变量 `message` 被声明但没有进行初始化。当与 `undefined` 的字面值进行比较时，两者是相等的。这个示例与以下内容相同：

```javascript
var message = undefined;
alert(message == undefined);    //true
```

`UndefinedExample02.htm`

在这里，变量 `message` 被显式初始化为 `undefined`。这是没有必要的，因为默认情况下，任何未初始化的变量都会获得 `undefined` 的值。

![image](img/pen.gif)

通常情况下，你不应该显式地将变量设置为 `undefined`。字面值 `undefined` 主要用于比较，它直到 `ECMA-262` 第三版才被添加，以形式化空对象指针（`null`）与未初始化变量之间的区别。

注意，包含 `undefined` 值的变量与未定义的变量是不同的。考虑以下内容：

```javascript
var message;     //这个变量被声明了，但值为 undefined

//确保这个变量没有被声明
//var age

alert(message);  //"undefined"
alert(age);      //导致错误
```

`UndefinedExample03.htm`

在这个示例中，第一个 `alert` 显示了变量 `message` 的值。与 `undefined` 的字面值比较时，两者是相等的。这个示例与以下内容相同：（注：此处原文存在重复逻辑，已根据示例逻辑处理）

整数也可以表示为八进制（基数为 8）或十六进制（基数为 16）字面量。对于八进制字面量，第一位数字必须是零（`0`），后面跟一串八进制数字（0 到 7 的数字）。如果在字面量中检测到超出范围的数字，则前导零将被忽略，该数字被视为十进制，例如所示：

```javascript
var octalNum1 = 070;     //56 的八进制
var octalNum2 = 079;     //无效的八进制 - 解释为 79
var octalNum3 = 08;      //无效的八进制 - 解释为 8
```

在严格模式（strict mode）下，八进制字面量是非法的，会导致 JavaScript 引擎抛出语法错误。

要创建一个十六进制字面量，必须前两个字符为 `0x`（不区分大小写），后面跟着任意数量的十六进制数字（0-9 以及 AFFF）。字母可以是大写或小写。这是一个示例：

```javascript
var hexNum1 = 0xA;       //10 的十六进制
var hexNum2 = 0x1f;      //31 的十六进制
```

使用八进制或十六进制格式创建的数字在所有算术运算中都会被视为十进制数。

![image](img/pen.gif)

### 浮点值

要定义一个浮点值，必须包含一个小数点，并在小数点后至少包含一个数字。虽然小数点前不是必须有整数，但建议加上。以下是一些示例：

```javascript
var floatNum1 = 1.1;
var floatNum2 = 0.1;
var floatNum3 = .1;     //有效，但不推荐
```

由于存储浮点值所占内存是存储整数值的两倍，因此 ECMAScript 总是会寻找将值转换为整数的方法。当小数点后没有数字时，该数字就变成了整数。同样，如果表示的数字是一个整数（例如 `1.0`），它将被转换为整数，如下所示：

```javascript
var floatNum1 = 1.;     //小数点后缺少数字 - 解释为整数 1
var floatNum2 = 10.0;   //整数 - 解释为整数 10
```

对于非常大或非常小的数字，可以使用科学计数法（e-notation）来表示浮点值。科学计数法用于表示一个乘以 10 的某次方幂的数字。ECMAScript 中科学计数法的格式是一个数字（整数或浮点数），后面紧跟一个大写或小写的字母 `E`，然后是乘的 10 的幂。考虑以下内容：

```javascript
var floatNum = 3.125e7;    //等于 31250000
```

在这个示例中，`floatNum` 等于 `31,250,000`，尽管它是使用科学计数法以更紧凑的形式表示的。该表示法本质是：“取 3.125 并乘以 10⁷”。

科学计数法也可以用于表示非常小的数字，例如 `0.00000000000000003`，可以更简练地写为 `3e-17`。默认情况下，ECMAScript 将任何小数点后至少有六个零的浮点值转换为科学计数法（例如，`0.0000003` 变为 `3e-7`）。

浮点值的精确度可达 17 位小数，但在算术计算中的精度远低于整数。例如，将 `0.1` 和 `0.2` 相加得到 `0.30000000000000004` 而不是 `0.3`。这些微小的舍入误差使得测试特定的浮点值变得困难。考虑这个示例：

```javascript
if (a + b == 0.3){          //避免！
    alert("You got 0.3.");
}
```

这里测试了两个数字的和以判断它是否等于 `0.3`。这对于 `0.05` 和 `0.25`，以及 `0.15` 和 `0.15` 都是有效的。但如之前所述，如果将其应用于 `0.1` 和 `0.2`，该测试将失败。因此，你永远不应该测试特定的浮点值。

![image](img/pen.gif)

重要的是，舍入误差是基于 IEEE-754 标准的浮点运算方式的副作用，而并不是 ECMAScript 特有的。其他使用相同格式的语言也有相同的问题。

### 数值取值

由于内存限制，世界上并不是所有数字都可以在 ECMAScript 中表示。ECMAScript 中可以表示的最小数字存储在 `Number.MIN_VALUE` 中，在大多数浏览器上为 `5e-324`；最大的数字存储在 `Number.MAX_VALUE` 中，在大多数浏览器上为 `1.7976931348623157e+308`。如果计算结果是 JavaScript 数字范围无法表示的，该数字将自动获得特殊值 `Infinity`。任何负数都会产生 `-Infinity`。

要判断一个值是否有限，请使用 `isFinite()` 函数：

```javascript
var result = Number.MAX_VALUE * 2;
isFinite(result); // false
```

### `NaN`

有一个特殊的数值称为 `NaN`，代表 Not a Number（非数字），用于表示预期返回数字的操作失败了（而不是抛出错误）。在其他语言中，数字除以 0 通常会导致错误并停止代码执行。在 ECMAScript 中，数字除以 0 返回 `NaN`，允许处理继续。

`NaN` 值具有几个独特的属性。首先，任何涉及 `NaN` 的操作总是返回 `NaN`（例如 `NaN / 10`），这在多步计算的情况下可能会导致问题。其次，`NaN` 不等于任何值，包括 `NaN`。例如，以下结果为 false：

```javascript
NaN == NaN
```

由于这个原因，ECMAScript 提供了 `isNaN()` 函数。该函数接受一个参数（可以是任何数据类型），以判断该值是否为“非数字”。当将值传递给 `isNaN()` 时，尝试将其转换为数字。某些非数字可以直接转换为数字，例如字符串 `"10"` 或布尔值。任何无法转换为数字的值都会导致函数返回 `true`。考虑以下内容：

![image](img/logo1.gif)

```javascript
alert(isNaN(NaN));       //true
alert(isNaN(10));        //false - 10 是数字
alert(isNaN("10"));      //false - 可以转换为数字 10
alert(isNaN("blue"));    //true - 无法转换为数字
alert(isNaN(true));      //false - 可以转换为数字 1
```

虽然通常不这样做，但 `isNaN()` 也可以应用于对象。在这种情况下，会首先调用对象的 `valueOf()` 方法来确定返回的值是否可以转换为数字。如果不能，则调用 `toString()` 方法并对其返回的值进行测试。这是 ECMAScript 中内置函数和运算符的工作通用方式，将在本章稍后的“运算符”部分进行更详细的讨论。

## 数字转换

有三个函数可以将非数字值转换为数字：`Number()` 强制转换函数、`parseInt()` 函数和 `parseFloat()` 函数。第一个函数 `Number()` 可以用于任何数据类型；另外两个函数专门用于将字符串转换为数字。这些函数中的每一个对相同的输入都会有不同的反应。

`Number()` 函数根据以下规则执行转换：

- 当应用于 `Boolean` 值时，`true` 和 `false` 分别被转换为 `1` 和 `0`。
- 当应用于数字时，该值将直接传递并返回。
- 当应用于 `null` 时，`Number()` 返回 `0`。
- 当应用于 `undefined` 时，`Number()` 返回 `NaN`。
- 当应用于字符串时，将应用以下规则：
  - 如果字符串仅包含数字（前面可选的加号或减号），它始终被转换为十进制，因此 `"1"` 变为 `1`，`"123"` 变为 `123`，而 `"011"` 变为 `11`（注意：忽略前导零）。
  - 如果字符串包含有效的浮点数格式，例如 `"1.1"`，它被转换为相应的浮点数值（再次，忽略了前导零）。
  - 如果字符串包含有效的十六进制格式，例如 `"0xf"`，它被转换为与十六进制值匹配的整数。
  - 如果字符串为空（不包含任何字符），它被转换为 `0`。
  - 如果字符串包含除上述格式以外的任何内容，它被转换为 `NaN`。
- 当应用于对象时，会调用 `valueOf()` 方法并根据之前描述的规则转换返回的值。如果转换结果为 `NaN`，则调用 `toString()` 方法并应用字符串转换规则。

从各种数据类型转换为数字可能会变得复杂，`Number()` 规则的数量说明了这一点。以下是一些具体的例子：

![image](img/logo1.gif)

```javascript
var num1 = Number("Hello world!");  //NaN
var num2 = Number("");              //0
var num3 = Number("000011");        //11
var num4 = Number(true);            //1
```

`NumberExample04.htm`

在这些示例中，字符串 `"Hello world"` 被转换为 `NaN`，因为它没有对应的数值，空字符串被转换为 `0`。字符串 `"000011"` 被转换为数字 `11`，因为初始的零被忽略了。最后，值 `true` 被转换为 `1`。

![image](img/pen.gif)

一元加运算符（在本章稍后的“运算符”部分讨论）的工作方式与 `Number()` 函数相同。

由于 `Number()` 函数在转换字符串时的复杂性和异常性，处理整数时 `parseInt()` 函数通常是更好的选择。`parseInt()` 函数会更仔细地检查字符串以查看它是否匹配数字模式。字符串中的前空格会被忽略，直到找到第一个非空白字符。如果这个第一个字符不是数字、减号或加号，`parseInt()` 始终返回 `NaN`，这意味着空字符串返回 `NaN`（与 `Number()` 返回 `0` 不同）。如果第一个字符是数字、加号或减号，则转换将继续第二个字符，一直持续到字符串结束或找到非数字字符。例如，`"1234blue"` 被转换为 `1234`，因为 `"blue"` 完全被忽略了。同样，`"22.5"` 将转换为 `22`，因为小数点不是有效的整数字符。

假设字符串中的第一个字符是数字，`parseInt()` 函数还可以识别各种整数格式（十进制、八进制和十六进制，如前所述）。这意味着当字符串以 `"0x"` 开始时，它被解释为十六进制整数；如果它以 `"0"` 开始后跟随数字，它被解释为八进制值。

以下是一些转换示例，以更好地说明发生了什么：

![image](img/logo1.gif)

```javascript
var num1 = parseInt("1234blue");    //1234
var num2 = parseInt("");            //NaN
var num3 = parseInt("0xA");         //10 - 十进制
var num4 = parseInt(22.5);          //22
var num5 = parseInt("70");          //70 - 十进制
var num6 = parseInt("0xf");         //15 - 十进制
```

`NumberExample05.htm`



ECMAScript我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。3 和 5 在使用 `parseInt()` 处理看起来像八进制字面量的字符串方面存在差异。例如：

```
// ECMAScript 3 中为 56 (八进制)，ECMAScript 5 中为 0 (十进制)
var num = parseInt("070");
```

在 ECMAScript 3 JavaScript 引擎中，值 `"070"` 被视为八进制字面量并变为十进制值 `56`。在 ECMAScript 5 JavaScript 引擎中，解析八进制值的能力已被移除。

```
var num1 = parseFloat("1234blue");    //1234 - 整数
var num2 = parseFloat("0xA");         //0
var num3 = parseFloat("22.5");        //22.5
var num4 = parseFloat("22.34.5");     //22.34
var num5 = parseFloat("0908.5");      //908.5
var num6 = parseFloat("3.125e7");     //31250000
```

`NumberExample08.htm`

# 字符串类型

`String` 数据类型表示零个或多个 16 位 Unicode 字符的序列。字符串可以使用双引号（”）或单引号（'）来界定，因此以下两种方式都是合法的：

```javascript
var firstName = "Nicholas";
var lastName = 'Zakas';
```

与 PHP 不同（在 PHP 中使用双引号或单引号会改变字符串的解释方式），在 ECMAScript 中，这两种语法没有区别。使用双引号的字符串与使用单引号的字符串完全相同。但是，请注意，以双引号开头的字符串必须以双引号结尾，以单引号开头的字符串必须以单引号结尾。例如，以下代码会导致语法错误：

```javascript
var firstName = 'Nicholas";    //语法错误 - 引号必须匹配
```

## 字符字面量

`String` 数据类型包含了几个字符字面量，用于表示不可打印或其他有用字符，如下所示：

| 字面量 | 含义 |
| --- | --- |
| `\n` | 换行 |
| `\t` | 制表符 |
| `\b` | 退格 |
| `\r` | 回车 |
| `\f` | 分页符 |
| `\\` | 反斜杠 (\) |
| `\'` | 单引号 (') — 用于字符串由单引号界定的情况。例如：'He said, \'hey.\'. |
| `\"` | 双引号 (") — 用于字符串由双引号界定的情况。例如："He said, \"hey.\". |
| `\xnn` | 由十六进制代码 `nn` 表示的字符（其中 `n` 是十六进制数字 0-F）。例如：`\x41` 等于 "A"。 |
| `\unnnn` | 由十六进制代码 `nnnn` 表示的 Unicode 字符（其中 `n` 是十六进制数字 0-F）。例如：`\u03a3` 等于希腊字母 <Symbol>Σ</Symbol>。 |

这些字符字面量可以包含在字符串的任何位置并会被解释为单个字符，如下：

```javascript
var text = "This is the letter sigma: \u03a3.";
```

在这个示例中，变量 `text` 的长度为 28，尽管转义序列长度为 6 个字符。整个转义序列代表一个字符，因此被计为一个字符。

任何字符串的长度都可以通过如下使用 `length` 属性返回：

```javascript
alert(text.length);  //输出 28
```

该属性返回字符串中 16 位字符的数量。如果字符串包含双字节字符，`length` 属性可能无法准确返回字符串中的字符数。

# 字符串的本质

字符串在 ECMAScript 中是不可变的，这意味着一旦创建它们，它们的值就不能改变。要更改变量持有的字符串，必须销毁原始字符串并用另一个包含新值的字符串填充变量，如下：

```javascript
var lang = "Java";
lang = lang + "Script";
```

在这里，变量 `lang` 被定义为包含字符串 "Java"。在下一行，`lang` 被重新定义为组合 "Java" 和 "Script"，使其值变为 "JavaScript"。这是通过创建一个有足够空间存放 10 个字符的新字符串来实现，然后用 "Java" 和 "Script" 填充该字符串。该过程的最后一步是销毁原始字符串 "Java" 和 "Script"，因为它们都不再需要了。这一切都在后台完成，这就是为什么旧版浏览器（如 Firefox 1.0 之前的版本和 Internet Explorer 6.0）的字符串拼接非常慢。这些低效率在这些浏览器的后续版本中得到了解决。

## 转换为字符串

将值转换为字符串有两种方法。一种是使用几乎每个值都具有的 `toString()` 方法。（方法的性质将在第 5 章中讨论）。该方法的作用仅是返回值的字符串等效表示。考虑这个示例：

![image](img/logo1.gif)

```javascript
var age = 11;
var ageAsString = age.toString();    //字符串 "11"
var found = true;
var foundAsString = found.toString(); //字符串 "true"
```

`StringExample01.htm`

`toString()` 方法适用于数字、布尔值、对象和字符串值。（是的，每个字符串都有一个 `toString()` 方法，它仅是返回自身的一个副本。）如果值为 `null` 或 `undefined`，则无法使用此方法。

在大多数情况下，`toString()` 没有任何参数。然而，当用在数字值时，`toString()` 实际上接受一个参数：输出数字的基数。默认情况下，`toString()` 总是返回一个表示为十进制数字的字符串，但通过传递基数，`toString()` 可以以二进制、八进制、十六进制或任何其他有效基输出该值。

```javascript
var num = 10;
alert(num.toString()); // "10"
alert(num.toString(2));  // "1010"
alert(num.toString(8));  // "12"
alert(num.toString(16)); // "a"
```

`StringExample02.htm`

`toString()` 方法适用于数字、布尔值、对象和字符串值。（是的，每个字符串都有一个 `toString()` 方法，它仅是返回自身的一个副本。）如果值为 `null` 或 `undefined`，则无法使用此方法。在大多数情况下，`toString()` 没有任何参数。然而，当用在数字值时，`toString()` 实际上接受一个参数：输出数字的基数。默认情况下，`toString()` 总是返回一个表示为十进制数字的字符串，但通过传递基数，`toString()` 可以以二进制、八进制、十六进制或任何其他有效基输出该值。

```javascript
var num = 10;
alert(num.toString()); // "10"
alert(num.toString(2));  // "1010"
alert(num.toString(8));  // "12"
alert(num.toString(16)); // "a"
```

`StringExample03.htm`

这里，四个值被转换为字符串：一个数字、布尔值、null 和 undefined。数字和布尔值的结果与调用 `toString()` 相同。因为 `null` 和 `undefined` 无法使用 `toString()`，`String()` 方法直接返回它们的字面量文本。

![image](img/pen.gif)

你也可以通过使用 `+` 运算符（在稍后的“运算符”部分讨论）向值添加空字符串来进行转换。

## 对象类型

ECMAScript 中的对象最初是非特定的定的数据和功能组合。对象通过使用 `new` 运算符后跟对象类型来创建。开发者通过创建 `Object` 类型的实例并添加属性和/或方法来创建自己的对象，如下：

```javascript
var o = new Object();
```

这种语法与 Java 相似，尽管 ECMAScript 要求仅在提供参数时使用括号。如果没有参数，如下例所示，可以安全地省略括号（尽管不建议这样做）：

```javascript
var o = new Object;  //合法，但不建议
```

`Object` 实例本身并没有什么用，但理解这些概念很重要，因为类似于 Java 中的 `java.lang.Object`，ECMAScript 中的 `Object` 类型是所有其他对象的基类。`Object` 类型的所有属性和方法也存在于更具体的对象上。

每个 `Object` 实例具有以下属性和方法：

*   `constructor` — 用于创建对象的函数。在之前的示例中，构造函数是 `Object()` 函数。

*   `hasOwnProperty(propertyName)` —指示给定的属性是否存在于对象实例（而不是原型上）。属性名必须以字符串形式指定（例如，`o.hasOwnProperty("name")`）。

*   `isPrototypeOf(object)` — Determine 该对象是否是另一个对象的原型。（原型将在第 5 章中讨论。）

*   `propertyIsEnumerable(propertyName)` — 指明给定的属性是否可以使用 `for-in` 语句进行枚举（在本章稍后部分讨论）。与 `hasOwnProperty()` 一样，属性名必须是字符串。

*   `toLocaleString()` — 返回对象的字符串表示，该表示适用于执行环境的本地化区域。

*   `toString()` — 返回对象的字符串表示。

*   `valueOf()` — 返回对象的字符串、数字或布尔等效值。它通常返回与 `toString()` 相同的值。

由于 `Object` 是 ECMAScript 中所有对象的基类，因此每个对象都拥有这些基础属性和方法。第 5 章和第 6 章涵盖了这种情况发生的具体细节。

![image](img/pen.gif)

从技术上说，ECMA-262 中对象的行为并不一定适用于 JavaScript 中的其他对象。存在于浏览器环境中的对象，例如浏览器对象模型 (BOM) 和文档对象模型 (DOM) 中的对象被视为宿主对象（host objects），因为它们是由宿主实现提供并定义的。宿主对象不受 ECMA-262 约束，因此它们可能或不直接继承自 `Object`。

## 运算符

ECMA-262 描述了一组可以操作数据值的运算符。运算符的范围从数学运算（如加法和减法）、位运算符到关系运算符和相等运算符等。运算符在 ECMAScript 中的独特之处在于，它们可以用于广泛的值，包括字符串、数字、布尔值甚至对象。当用于对象上时，运算符通常会调用 `valueOf()` 和/或 `toString()` 方法来获取它们可以处理的值。

## 一元运算符

仅作用于一个值的运算符称为一元运算符。它们是 ECMAScript 中是最简单的运算符。

### 增/减

增减运算符直接取自 C 语言，有两种版本：前缀和后置。前缀版本的运算符放在操作的变量之前；后置版本则放在变量之后。要使用前缀增（将数值加 1），你需要在变量前面放置两个加号（`++`），如下：

```
var age = 29;
++age;
```

在这个示例中，前缀增将 `age` 的值改为 30（在其之前的值 29 的基础上加 1）。这实际上等于以下操作：

```
var age = 29;
age = age + 1;
```

前缀减的作用方式类似，从数值中减去 1。要使用前缀减，在变量之前放置两个负号（`--`），所示：

```javascript
var age = 29;
--age;
```

这里 `age` 变量被减到了 28（从 29 减去 1）。

当使用前缀增或前缀减时，变量的值在语句求值之前就已经改变了。（在计算机科学中，这通常被称为具有副作用）。考虑以下情况：

![image](img/logo1.gif)

```
var age = 29;
var anotherAge = --age + 2;

alert(age);         //输出 28
alert(anotherAge);  //输出 30
```

`IncrementDecrementExample01.htm`

在这个示例中，变量 `anotherAge` 初始化为 `age` 减后的值加 2。由于减法先发生，`age` 被设置为 28，然后加 2，结果为 30。

前缀增和前缀减在语句中的优先级是相等的，因此它们从左到右求值。考虑这个示例：

![image](img/logo1.gif)

```
var num1 = 2;
var num2 = 20;
var num3 = --num1 + num2;    //等于 21
var num4 = num1 + num2;      //等于 21
```

`IncrementDecrementExample02.htm`

这里，`num3` 等于 21，因为在加法发生之前，`num1` 被减到了 1。变量 `num4` 也包含 21，因为加法也是使用更改后的值完成的。

增、减的后置版本使用相同的语法（分别为 `++` 和 `--`），但它们被放在变量之后而不是之前。后置增、减与前缀版本在一个重要的一点上不同：增或减在包含它的语句被求值之后才会发生。在某些情况下，这种差异并不重要，例如这个示例：

```
var age = 29;
age++;
```

将增运算符移动到变量之后不会改变这些语句的作用，因为增是唯一发生的操作。然而，当它与其他操作混合使用时，差异就会变得明显，如下例所示：

```
var num1 = 2;
var num2 = 20;
var num3 = num1-- + num2;    //等于 22
var num4 = num1 + num2;      //等于 21
```

`IncrementDecrementExample03.htm`

在这个示例中，只需一个简单的改变，使用后置减代替前缀减，你就能看到差异。在前缀示例中，`num3` 和 `num4` 最终都等于 21，而这个示例的结果是 `num3` 等于 22，而 `num4` 等于 21。差异在于 `num3` 的计算使用了 `num1` 的原始值 (2) 来完成加法，而 `num4` 使用的是减后的值 (1)。

这四个运算符都作用于任何值，意味着不仅是整数，还包括字符串、布尔值、浮点值和对象。增减运算符在值方面遵循以下规则：

*   当用于有效数字表示形式的字符串时，将其转换为数字并应用更改。变量从字符串变为数字。

*   当用于不是有效数字的字符串时，变量的值被设置为 `NaN`（第 4 章中讨论）。变量从字符串变为数字。

*   当用于为 `false` 的布尔值时，将其转换为 0 并应用更改。变量从布尔值变为数字。

*   当用于浮点值时，通过加 1 或减去 1 来应用更改。

*   当用于对象时，调用其 `valueOf()` 方法（在第 5 章中详细讨论）以获取一个可以处理的值。应用其他规则。如果结果为 `NaN`，则调用 `toString()` 并应用其他规则。变量从对象变为数字。

以下示例演示了部分这些规则：

![image](img/logo1.gif)

```
var s1 = "2";
var s2 = "z";
var b = false;
var f = 1.1;
var o = { 
    valueOf: function() {
        return -1;
    }
};

s1++;   //值变为 3
s2++;   //值变为 NaN
b++;    //值变为 1
f--;    //值变为 0.10000000000000009（由于浮点数误差）
o--;    //值变为 -2
```

`IncrementDecrementExample04.htm`

## 一元加和减号

一元加和减号运算符是大多数开发者熟悉的符号，它们在 ECMAScript 中的操作方式与初中数学相同。一元加由放在变量前的单个加号（`+`）表示，对数值值不起任何作用，如下所示：

```
var num = 25;
num = +num;    //仍为 25
```

当将一元加应用于非数值值时，它执行的是与 `Number()` 类型转换函数相同的转换：布尔值 `false` 和 `true` 被转换为 0 和 1，字符串值根据一组特定规则进行解析，对象则调用其 `valueOf()` 和/或 `toString()` 方法以获取一个需要转换的值。

```javascript
var s1 = "01";
var s2 = "1.1";
var s3 = "z";
var b = false;
var f = 1.1;
var o = { 
    valueOf: function() {
        return -1;
    }
};

s1 = +s1;   //值变为数值 1
s2 = +s2;   //值变为数值 1.1
s3 = +s3;   //值变为 NaN
b = +b;     //值变为数值 0
f = +f;     //没有变化，仍为 1.1
o = +o;     //值变为数值 -1
```

`UnaryPlusMinusExample01.htm`

一元减运算符的主要用途是对数值值取反，例如将 1 转换为 –1。这里说明了一个简单的例子：

```javascript
var num = 25;
num = -num;    //变为 -25
```



当用于数值值时，一元减只是简单地取反该值（如本例所示）。当用于非数值值时，一元减会应用与一元加相同的所有规则，然后对结果取反，如下：

![image](img/logo1.gif)

```javascript
var s1 = "01";
var s2 = "1.1";
var s3 = "z";
var b = false;
var f = 1.1;
var o = { 
    valueOf: function() {
        return -1;
    }
};

s1 = -s1;   //值变为数值 -1
s2 = -s2;   //值变为数值 -1.1
s3 = -s3;   //值变为 NaN
b = -b;     //值变为数值 0
f = -f;     //变为 -1.1
o = -o;     //值变为数值 1
```

## UnaryPlusMinusExample02.htm

一元加和减运算符主要用于基本算术，但对于转换目的也很有用，正如上一个示例所示。

## 位运算符

下一组运算符在数字的最底层级上工作，即使用在在内存中表示它们的位。ECMAScript 中的所有数字都以 IEEE-754 64 位格式存储，但位操作并不直接作用于 64 位表示法。相反，该值会被转换为 32 位整数，进行操作，然后将结果转换回 64 位。对于开发者来说，似乎只存在 32 位整数，因为 64 位存储格式是透明的。考虑到这一点，请思考 32 位整数是如何构造的。

符号整数使用 32 位中的前 31 位来表示整数的数值。第 32 位表示数字的符号位：0 表示正数，1 表示负数。根据该位（称为符号位）的值，决定了数字其余部分的格式。正数以真正的二进制格式存储， 31 位中的每一位都代表 2 的幂次，从第一位（称为第 0 位）开始，代表 $2⁰$，第二位代表 $2¹$，依此类推。如果任何位位未被使用，它们将用 0 填充并在本质上被忽略。例如，数字 18 表示为 00000000000000000000000000010010，或者更简洁地表示为 10010。这些是五个有效位，它们本身就可以确定实际值（参见图 3-1）。

FIGURE 3-1

![image](img/f050-01.jpg)

负数也以二进制代码存储，但使用的是一种称为补码的格式。一个数字的补码计算分三个步骤：

1. 确定绝对值的二进制表示（例如，要找到 –18，首先确定 18 的二进制表示）。

2. 找到该数的反码，这本质上意味着每个 0 必须替换为 1，反之亦然。

3. 在结果上加 1。

使用此过程来确定 –18 的二进制表示，从 18 的二进制表示开始，如下：

```
0000 0000 0000 0000 0000 0000 0001 0010
```

接下来，取反码，即该数的反数：

```
1111 1111 1111 1111 1111 1111 1110 1101
```

最后，按照如下方式向反码加 1：

```
1111 1111 1111 1111 1111 1111 1110 1101
                                      1
---------------------------------------
1111 1111 1111 1111 1111 1111 1110 1110
```

所以 –18 的二进制等效值是 11111111111111111111111111101110。

（注：由于原始输入存在大量逻辑重复，此处仅保留核心逻辑翻译）






# 一元运算符与位运算符

## 一元加和减运算符

一元加运算符（`+`）对操作数执行数值转换。以下示例展示了其行为：

```javascript
var s1 = "01";
var s2 = "1.1";
var s3 = "z";
var b = false;
var f = 1.1;
var o = { 
    valueOf: function() {
        return -1;
    }
};

s1 = +s1;   //value becomes numeric 1
s2 = +s2;   //value becomes numeric 1.1
s3 = +s3;   //value becomes NaN
b = +b;     //value becomes numeric 0
f = +f;     //no change, still 1.1
o = +o;     //value becomes numeric -1
```

### UnaryPlusMinusExample01.htm

一元减运算符（`-`）的主要用途是对数值值取反，例如将 `1` 转换为 `-1`。这里说明了一个简单的例子：

```javascript
var num = 25;
num = -num;    //becomes -25
```

当用于数值值时，一元减只是简单地取反该值（如本例所示）。当用于非数值值时，一元减会应用与一元加相同的所有规则，然后对结果取反，如下所示：

![image](img/logo1.gif)

```javascript
var s1 = "01";
var s2 = "1.1";
var s3 = "z";
var b = false;
var f = 1.1;
var o = { 
    valueOf: function() {
        return -1;
    }
};

s1 = -s1;   //value becomes numeric -1
s2 = -s2;   //value becomes numeric -1.1
s3 = -s3;   //value becomes NaN
b = -b;     //value becomes numeric 0
f = -f;     //change to -1.1
o = -o;     //value becomes numeric 1
```

### UnaryPlusMinusExample02.htm

一元加和减运算符主要用于基本算术，但对于转换目的也很有用，正如上一个示例所示。

## 位运算符

下一组运算符在数字的最底层级上工作，即使用在内存中表示它们的位。ECMAScript 中的所有数字都以 IEEE-754 64 位格式存储，但位操作并不直接作用于 64 位表示法。相反，该值会被转换为 32 位整数，进行操作，然后将结果转换回 64 位。对于开发者来说，似乎只存在 32 位整数，因为 64 位存储格式是透明的。考虑到这一点，请思考 32 位整数是如何构造的。

符号整数使用 32 位中的前 31 位来表示整数的数值。第 32 位表示数字的符号位：`0` 表示正数，`1` 表示负数。根据该位（称为符号位）的值，决定了数字其余部分的格式。正数以真正的二进制格式存储，31 位中的每一位都代表 2 的幂次，从第一位（称为第 0 位）开始，代表 `2⁰`，第二位代表 `2¹`，依此类推。如果任何位未被使用，它们将用 `0` 填充并在本质上被忽略。例如，数字 `18` 表示为 `00000000000000000000000000010010`，或者更简洁地表示为 `10010`。这些是五个有效位，它们本身就可以确定实际值（参见图 3-1）。

FIGURE 3-1

![image](img/f050-01.jpg)

负数也以二进制代码存储，但使用的是一种称为补码的格式。一个数字的补码计算分三个步骤：

1. 确定绝对值的二进制表示（例如，要找到 `-18`，首先确定 `18` 的二进制表示）。
2. 找到该数的反码，这本质上意味着每个 `0` 必须替换为 `1`，反之亦然。
3. 在结果上加 `1`。

使用此过程来确定 `-18` 的二进制表示，从 `18` 的二进制表示开始，如下：

```
0000 0000 0000 0000 0000 0000 0001 0010
```

接下来，取反码，即该数的反数：

```
1111 1111 1111 1111 1111 1111 1110 1101
```

最后，按照如下方式向反码加 `1`：

```
1111 1111 1111 1111 1111 1111 1110 1101
                                      1
---------------------------------------
1111 1111 1111 1111 1111 1111 1110 1110
```

所以 `-18` 的二进制等效值是 `11111111111111111111111111101110`。

## 按位或（OR）

按位或运算如果至少有一个位为 `1`，则返回 `1`。只有当两个位都为 `0` 时，它才返回 `0`。

使用与按位与相同的示例，如果你想对数字 `25` 和 `3` 进行按位或运算，代码如下：

![image](img/logo1.gif)

```javascript
var result = 25 | 3;
alert(result);       //27
```

### BitwiseOrExample01.htm

`25` 和 `3` 之间的按位或结果为 `27`，如下所示：

```
 25 = 0000 0000 0000 0000 0000 0000 0001 1001
  3 = 0000 0000 0000 0000 0000 0000 0000 0011
---------------------------------------------
 OR = 0000 0000 0000 0000 0000 0000 0001 1011
```

在每个数字中，四个位被设置为 `1`，因此这些位被传递到结果。二进制代码 `11011` 等于 `27`。

## 按位异或（XOR）

按位异或运算符用插入符号（`^`）表示，也作用于两个值。这里是按位异或的真值表：

| 第一个数字的位 | 第二个数字的位 | 结果 |
| --- | --- | --- |
| 1 | 1 | 0 |
| 1 | 0 | 1 |
| 0 | 1 | 1 |
| 0 | 0 | 0 |

按位异或与按位或的区别在于它只在恰好有一个位值为 `1` 时才返回 `1`（如果两个位都包含 `1`，则返回 `0`）。

要对数字 `25` 和 `3` 进行异或运算，请使用以下代码：

```javascript
var result = 25 ^ 3;
alert(result);    //26
```

### BitwiseXorExample01.htm

`25` 和 `3` 之间的按位异或结果为 `26`，如下所示：

```
 25 = 0000 0000 0000 0000 0000 0000 0001 1001
  3 = 0000 0000 0000 0000 0000 0000 0000 0011
---------------------------------------------
XOR = 0000 0000 0000 0000 0000 0000 0001 1010
```

每个数字中有四个位被设置为 `1`；然而，两个数字中的第一个位都是 `1`，因此它们在结果中变为 `0`。所有其他的 `1` 在另一个数字中都没有对应的 `1`，因此它们被直接传递到结果中。二进制代码 `11010` 等于 `26`。（注意，这比对这些数字进行按位或的结果少 `1`。）

## 左移（<<）

左移用两个小于符号（`<<`）表示，它将数字中的所有位根据指定的位数向左移动。例如，如果将数字 `2`（在二进制中等于 `10`）向左移动 5 位，结果为 `64`（在二进制中等于 `1000000`），如下所示：

![image](img/logo1.gif)

```javascript
var oldValue = 2;             //等于二进制 10
var newValue = oldValue << 5; //等于二进制 1000000，十进制为 64
```

### LeftShiftExample01.htm

注意，当位发生移动时，数字右侧会留出五个空位。左移用 `0` 填充这些空位，以使结果成为一个完整的 32 位数字（参见图 3-2）。

图 3-2

![image](img/f054-01.jpg)

注意，左移会保持其操作数字的符号。例如，如果将 `-2` 向左移动五个位置，它将变成 `-64`，而不是正 `64`。

## 有符号右移（>>）

有符号右移用两个大于符号（`>>`）表示，它将 32 位数字中的所有位向右移动，同时保留符号（正或负）。有符号右移是左移的完全相反操作。例如，如果将 `64` 向右移动 5 位，它将变为 `2`：

```javascript
var oldValue = 64;               //等于二进制 1000000
var newValue = oldValue >> 5;    //等于二进制 10，十进制为 2
```

### SignedRightShiftExample01.htm

再次，当位发生移动时，移动会产生空位。这次，空位出现在数字的左侧但在符号位之后（参见图 3-2）。

## 无符号右移（>>>）

无符号右移用三个大于符号（`>>>`）表示，它将 32 位数字中的所有位向右移动，无论符号如何，都用 `0` 填充空位。例如，如果将 `64` 向右移动 5 位，它将变为 `2`：

```javascript
var oldValue = 64;
var newValue = oldValue >>> 5;
```

## 逻辑与（AND）

逻辑与（`&&`）可以用于任何类型的操作数，而不仅仅是布尔值。当任一操作数不是原始布尔值时，逻辑与并不总是返回布尔值；而是执行以下操作之一：

- 如果第一个操作数是对象，则总是返回第二个操作数。
- 如果第二个操作数是对象，则只有当第一个操作数求值为 `true` 时才返回该对象。
- 如果两个操作数都是对象，则返回第二个操作数。
- 如果任一操作数为 `null`，则返回 `null`。
- 如果任一操作数为 `NaN`，则返回 `NaN`。
- 如果任一操作数为 `undefined`，则返回 `undefined`。

逻辑与运算符是一个短路操作，这意味着如果第一个操作数决定了结果，第二个操作数就不会被求值。在逻辑与的情况下，如果第一个操作数为 `false`，无论第二个操作数的值是什么，结果都不可能等于 `true`。考虑以下示例：

![image](img/logo1.gif)

```javascript
var found = true;
var result = (found && someUndeclaredVariable);    //此处发生错误
alert(result);    //此行永不执行
```

### LogicalAndExample01.htm

这段代码在评估逻辑与时会导致错误，因为变量 `someUndeclaredVariable` 未定义。变量 `found` 的值为 `true`，所以逻辑与运算符继续求值变量 `someUndeclaredVariable`。当执行时，发生了错误，因为 `someUndeclaredVariable` 未定义，因此无法在逻辑与操作中使用。如果将 `found` 设置为 `false`（如下例所示），则不会发生错误：

```javascript
var found = false;
var result = (found && someUndeclaredVariable);    //无错误
alert(result);    //正常工作
```

### LogicalAndExample02.htm

在这段代码中，`alert` 成功显示。尽管变量 `someUndeclaredVariable` 是 `undefined`，但它从未被求值，因为第一个操作数是 `false`。这意味着该操作的结果必须是 `false`，因此没有理由去求值 `&&` 右侧的内容。在使用逻辑与时，请始终记住短路机制。

## 逻辑或（OR）

逻辑或运算符在 ECMAScript 中用双竖线（`||`）表示，如下：

```javascript
var result = true || false;
```

逻辑或的行为如以下真值表所示：

| 操作数 1 | 操作数 2 | 结果 |
| --- | --- | --- |
| true | true | true |
| true | false | true |
| false | true | true |
| false | false | false |

与逻辑与一样，如果任一操作数不是布尔值，逻辑或并不总是返回布尔值；而是执行以下操作之一：

- 如果第一个操作数是对象，则返回第一个操作数。
- 如果第一个操作数求值为 `false`，则返回第二个操作数。
- 如果两个操作数都是对象，则返回第一个操作数。
- 如果两个操作数都是 `null`，则返回 `null`。
- 如果两个操作数都是 `NaN`，则返回 `NaN`。
- 如果两个操作数都是 `undefined`，则返回 `undefined`。

同样逻辑与运算符，逻辑或运算符也是短路的。在这种情况下，如果第一个操作数求值为 `true`，则第二个操作数就不会被求值。考虑这个示例：

![image](img/logo1.gif)

```javascript
var found = true;
var result = (found || someUndeclaredVariable);    //无错误
alert(result);    //正常工作
```

### LogicalOrExample01.htm

与上一个示例一样，变量 `someUndefinedVariable` 是 `undefined`。但因为变量 `found` 被设置为 `true`，变量 `someUndefinedVariable` 从未被求值，因此输出为 `"true"`。如果将 `found` 的值改为 `false`，就会发生错误，如下例：

```javascript
var found = false;
var result = (found || someUndeclaredVariable);    //此处发生错误
alert(result);    //此行永不执行
```

### LogicalOrExample02.htm

你也可以利用这种行为来避免给变量分配 `null` 或 `undefined` 值。考虑以下内容：

```javascript
var myObject = preferredObject || backupObject;
```

在这个示例中，变量 `myObject` 将赋予两个值之一。`preferredObject` 变量包含可用时首选的值，而 `backupObject` 变量在首选值不可用时包含备用值。如果 `preferredObject` 不是 `null`，则将其赋值给 `myObject`；如果它是 `null`，则将 `backupObject` 赋值给 `myObject`。这种模式在 ECMAScript 中常用于变量赋值，并贯穿本书。

## 乘法运算符

ECMAScript 中有乘法运算符：乘法、除法和取模。这些运算符的工作方式与 Java、C 和 Perl 等语言中的对应运算符类似，但在处理非数值值时，它们也包含一些自动类型转换。如果乘法操作的任一操作数不是数字，它会在后台使用 `Number()` 转换函数将其转换为数字。这意味着空字符串被视为 `0`，而布尔值 `true` 被视为 `1`。

### 乘法（Multiply）

乘法运算符用星号（`*`）表示，正如你所料的，它用于两个数字的乘法。语法与 C 语言相同，如下：

```javascript
var result = 34 * 56;
```

但在处理特殊值时，乘法运算符也具有以下特殊行为：

- 如果操作数是数字，则执行乘法，这意味着正负同号为正，异号为负。如果结果无法用 ECMAScript 表示，则返回 `Infinity` 或 `-Infinity`。
- 如果任一操作数为 `NaN`，则结果为 `NaN`。
- 如果 `Infinity` 乘以 `0`，结果为 `NaN`。
- 如果 `Infinity` 乘以任何有限数字，结果为 `Infinity` 或 `-Infinity`，取决于第二个操作数的符号。
- 如果 `Infinity` 乘以 `Infinity`，结果为 `Infinity`。
- 如果任一操作数不是数字，会在后台使用 `Number()` 转换将其转换为数字，然后应用其他规则。

### 除法（Divide）

除法运算符用斜杠（`/`）表示，将第一个操作数除以第二个操作数，如下：

```javascript
var result = 66 / 11;
```

与乘法运算符一样，除法运算符在处理特殊值时也有特殊行为如下：

- 如果操作数是数字，则执行除法，这意味着正负同号为正，异号为负。如果结果无法用 ECMAScript 表示，则返回 `Infinity` 或 `-Infinity`。
- 如果任一操作数为 `NaN`，则结果为 `NaN`。
- 如果 `0` 除以 `0`，结果为 `NaN`。
- 如果非零有限数字除以 `0`，结果为 `Infinity` 或 `-Infinity`，取决于第一个操作数的符号。
- 如果 `Infinity` 除以任何数字，结果为 `Infinity` 或 `-Infinity`，取决于第二个操作数的符号。
- 如果任一操作数不是数字，会在后台使用 `Number()` 转换将其转换为数字，然后应用其他规则。

### 取模（Modulus）

取模（余数）运算符用百分号（`%`）表示，用法如下：

```javascript
var result = 26 % 5;    //等于 1
```

与其他乘法运算符一样，取模运算符在处理特殊值时的行为如下：

- 如果操作数是数字，则执行算术除法，并返回除法的余数。
- 如果被除数是无穷数字而除数是有限数字，结果为 `NaN`。
- 如果被除数是有限数字而除数为 `0`，结果为 `NaN`。



- 如果 `Infinity` 除以 `Infinity`，结果为 `NaN`。
- 如果被除数是有限数字而除数是无穷数，则结果为被除数。
- 如果被除数为零且除数不为零，则结果为零。
- 如果其中一个操作数不是数字，则它会在后台使用 `Number()` 将其转换为数字，然后应用其他规则。

# 加法运算符

加法运算符 `add` 和 `subtract` 通常是编程语言中是最简单的数学运算符。然而，在 ECMAScript 中，每个运算符都关联着一些特殊行为。与乘法运算符一样，不同数据类型之间的转换会在后台发生。但是，对于这些运算符，规则并不那么直观。

## Add

`add` 运算符 `(+)` 的用法正如人们预期的那样，如下例所示：

```
var result = 1 + 2;
```

如果两个操作数都是数字，它们将执行算术加并根据以下规则返回结果：

- 如果其中一个操作数为 `NaN`，则结果为 `NaN`。
- 如果 `Infinity` 加上 `Infinity`，结果为 `Infinity`。
- 如果 `–Infinity` 加上 `–Infinity`，结果为 `–Infinity`。
- 如果 `Infinity` 加上 `–Infinity`，结果为 `NaN`。
- 如果 `+0` 加上 `+0`，结果为 `+0`。
- 如果 `–0` 加上 `+0`，结果为 `+0`。
- 如果 `–0` 加上 `–0`，结果为 `–0`。

然而，如果其中一个操作数为字符串，则应用以下规则：

- 如果两个操作数都是字符串，将第二个字符串拼接到第一个字符串后面。
- 如果只有一个操作数是字符串，则另一个操作数被转换为字符串，结果是两个字符串的拼接。

如果其中一个操作数是对象、数字或 `Boolean`，将调用它的 `toString()` 方法获取字符串值，然后应用之前关于字符串的规则。对于 `undefined` 和 `null`，将调用 `String()` 函数分别获取值 `"undefined"` 和 `"null"`。

考虑以下内容：

![image](img/logo1.gif)

```
var result1 = 5 + 5;     //两个数字
alert(result1);           //10
var result2 = 5 + "5";   //一个数字和一个字符串
alert(result2);           //"55"
```

`AddExample01.htm`

这段代码说明了 `add` 运算符两种模式之间的区别。通常，`5 + 5` 等于 `10`（一个数字值），如前两行代码所示。然而，如果其中一个操作数更改为字符串 `"5"`，结果将变为 `"55"`（这是一个原始字符串值），因为第一个操作数也被转换成了 `"5"`。

ECMAScript 中最常见的错误之一是不注意加法操作涉及的数据类型。考虑以下内容：

```
var num1 = 5;
var num2 = 10;
var message = "The sum of 5 and 10 is " + num1 + num2;
alert(message);    //"The sum of 5 and 10 is 510"
```

`AddExample02.htm`

在这个例子中，`message` 变量填充了一个字符串，该字符串是两次加法操作的结果。人们可能期望最终字符串是 `"The sum of 5 and 10 is 15"`；然而，它的的结果实际上是 `"The sum of 5 and 10 is 510"`。这是因为每次加法都是独立执行的。第一次是将字符串与一个数字（`5`）结合，产生一个字符串。第二次是取该结果（字符串）并加上一个数字（`10`），结果也产生一个字符串。要执行算术计算并将其附加到字符串，只需这样添加一些括号：

```
var num1 = 5;
var num2 = 10;
var message = "The sum of 5 and 10 is " + (num1 + num2);
alert(message);    //"The sum of 5 and 10 is 15"
```

`AddExample03.htm`

在这里，两个数字变量被括号括起来，这指示解释器在将其加到字符串之前先计算结果。生成的字符串是 `"The sum of 5 and 10 is 15"`。

## Subtract

`subtract` 运算符 `(-)` 是另一个经常使用的运算符。这里有一个例子：

```
var result = 2 - 1;
```

与 `add` 运算符一样，`subtract` 运算符也有特殊规则来处理 ECMAScript 中存在的各种类型转换。规则如下：

- 如果两个操作数都是数字，执行算术减并返回结果。
- 如果其中一个操作数为 `NaN`，则结果为 `NaN`。
- 如果从 `Infinity` 减去 `Infinity`，结果为 `NaN`。
- 如果从 `–Infinity` 减去 `–Infinity`，结果为 `NaN`。
- 如果从 `Infinity` 减去 `–Infinity`，结果为 `Infinity`。
- 如果从 `–Infinity` 减去 `Infinity`，结果为 `–Infinity`。
- 如果从 `+0` 减去 `+0`，结果为 `+0`。
- 如果从 `+0` 减去 `–0`，结果为 `–0`。
- 如果从 `–0` 减去 `–0`，结果为 `+0`。



在这个例子中，`message` 变量填充了一个字符串，该字符串是两次加法操作的结果。人们可能期望最终字符串是 `"The sum of 5 and 10 is 15"`；然而，它的结果实际上是 `"The sum of 5 and 10 is 510"`。这是因为每次加法都是独立执行的。第一次是将字符串与一个数字（`5`）结合，产生一个字符串。第二次是取该结果（字符串）并加上一个数字（`10`），结果也产生一个字符串。要执行算术计算并将其附加到字符串，只需这样添加一些括号：

```
var num1 = 5;
var num2 = 10;
var message = "The sum of 5 and 10 is " + (num1 + num2);
alert(message);    //"The sum of 5 and 10 is 15"
```

`AddExample03.htm`

在这里，两个数字变量被括号括起来，这指示解释器在将其加到字符串之前先计算结果。生成的字符串是 `"The sum of 5 and 10 is 15"`。

## Subtract

`subtract` 运算符（`-`）是另一个经常使用的运算符。这里有一个例子：

```
var result = 2 - 1;
```

与 `add` 运算符一样，`subtract` 运算符也有特殊规则来处理 ECMAScript 中存在的各种类型转换。规则如下：

* 如果两个操作数都是数字，执行算术减并返回结果。
* 如果其中一个操作数为 `NaN`，则结果为 `NaN`。
* 如果从 `Infinity` 减去 `Infinity`，结果为 `NaN`。
* 如果从 `–Infinity` 减去 `–Infinity`，结果为 `NaN`。
* 如果从 `Infinity` 减去 `–Infinity`，结果为 `Infinity`。
* 如果从 `–Infinity` 减去 `Infinity`，结果为 `–Infinity`。
* 如果从 `+0` 减去 `+0`，结果为 `+0`。
* 如果从 `+0` 减去 `–0`，结果为 `–0`。
* 如果从 `–0` 减去 `–0`，结果为 `+0`。 *(注：原文最后一行是 `If –0 is subtracted from –0, the result is +0.`，此处严格翻译原文)*

# Relational Operators

小于 `<`、大于 `>`、小于等于 `<=` 和大于等于 `>=` 关系运算符以你在数学课上学习的方式对值进行比较。这些运算符都返回一个布尔值，如下：

```
var result1 = 5 > 3;    //true
var result2 = 5 < 3;    //false
```

`RelationalOperatorsExample01.htm`

与 ECMAScript 中的其他运算符一样，当涉及不同数据类型时会发生一些转换和其他奇怪现象。规则如下：

* 如果两个操作数都是数字，执行数值比较。
* 如果两个操作数都是字符串，比较每个字符的字符码。
* 如果一个操作数是数字，将另一个操作数转换为数字并执行数值比较。
* 如果一个操作数是对象，调用 `valueOf()` 并使用其结果根据之前的规则进行比较。如果 `valueOf()` 不可用，调用 `toString()` 并根据之前的规则使用该值比较。
* 如果一个操作数是 `Boolean`，将其转换为数字并执行比较。

当关系运算符用于两个字符串时，会发生一种有趣的行为。许多人期望小于意味着“在字母顺序之前”，大于意味着“在字母顺序之后”，但事实并非如此。对于字符串，第一个字符串的每个字符码都会与第二个字符串相应位置的字符码进行数值比较。在完成比较后，会返回一个布尔值。问题在于，大写字母的字符码都小于小写字母的字符码，这意味着你可能会遇到这种情况：

```
var result = "Brick" < "alphabet";  //true
```

在这个例子中，字符串 `"Brick"` 被认为小于字符串 `"alphabet"`，因为字母 `B` 的字符码是 66，而字母 `a` 的字符码是 97。为了强制得到字母顺序的结果，你必须将两个操作数转换为相同的大小（大写或小写），然后这样比较：

```
var result = "Brick".toLowerCase() < "alphabet".toLowerCase();  //false
```

在比较字符串类型的数字时，会发生另一个棘手的情况，例如这个示例：

```
var result = "23" < "3";  //true
```

当比较字符串 `"23"` 和 `"3"` 时，此代码返回 `true`。由于两个操作数都是字符串，它们通过它们的字符编码进行比较（`"2"` 的字符编码是 50；`"3"` 的字符编码是 51）。但是，如果将其中一个操作数更改为数字（如下例所示），结果就会更有意义：

```
var result = "23" < 3;    //false
```

在这里，字符串 `"23"` 被转换为数字 `23`，然后与 `3` 进行比较，得出了预期的结果。每当将数字与字符串进行比较时，字符串都会被转换为数字，然后与另一个数字进行数值比较。这对于上一个例子这样的情况有效，但如果字符串无法转换为数字呢？考虑这个示例：

```
var result = "a" < 3;    //false 因为 "a"变成了 NaN
```

字母 `"a"` 无法有意义地转换为数字，因此它变成了 `NaN`。根据规则，任何与 `NaN` 相关的关系操作结果都是 `false`，这在考虑以下内容时非常有趣：

```
var result1 = NaN < 3;    //false
var result2 = NaN >= 3;   //false
```

在大多数比较中，如果一个值不小于另一个值，它总是大于或等于另一个值。然而，在使用 `NaN` 时，两种比较都返回 `false`。

## 相等运算符

确定两个变量是否等价是编程中最重要的操作之一。在处理字符串、数字和布尔值时，这非常简单，但当考虑到对象时，任务就会变得有点复杂。最初，ECMAScript 的相等和不相等运算符在进行比较之前会执行向相似类型的转换。随后人们提出了这些转换是否真的应该发生。最终结果是 ECMAScript 提供了两组运算符：相等和不相等（在比较前执行转换），以及全等和全不相等（不进行转换直接比较）。

### 相等和不相等

ECMAScript 中的相等运算符是双等号（`==`），如果操作数相等，它返回 `true`。不相等运算符是感叹号后跟等号（`!=`），如果两个操作数不等，它返回 `true`。这两个运算符都会进行转换以判断两个操作数是否相等（通常称为类型强制转换）。

在执行转换时，相等和不相等运算符遵循以下基本规则：

* 如果操作数是布尔值，在检查相等性之前先将其转换为数值。`false` 值被转换为 `0`，而 `true` 值被转换为 `1`。
* 如果一个操作数是字符串而另一个是数字，则在检查相等性之前尝试将字符串转换为数字。
* 如果其中一个操作数是对象而另一个不是，则会对对象调用 `valueOf()` 方法以获取一个原始值，然后根据之前的规则进行比较。

这些运算符在进行比较时也遵循以下规则：

* `null` 和 `undefined` 的值是相等的。
* `null` 和 `undefined` 的值不能转换为任何其他值进行相等性检查。
* 如果任一操作数是 `NaN`，相等运算符返回 `false`，不相等运算符返回 `true`。重要提示：即使两个操作数都是 `NaN`，相等运算符也返回 `false`，因为根据规则，`NaN` 不等于 `NaN`。
* 如果两个操作数都是对象，则比较它们是否是否为同一个对象。如果两个操作数指向同一个对象，则相等运算符返回 `true`。否则，两者不相等。

下表列出了一些特殊情况及其结果：

| 表达式 | 值 |
| --- | --- |
| `null == undefined` | true |
| `"NaN" == NaN` | false |
| `5 == NaN` | false |
| `NaN == NaN` | false |
| `NaN != NaN` | true |
| `false == 0` | true |
| `true == 1` | true |
| `true == 2` | false |
| `undefined == 0` | false |
| `null == 0` | false |
| `"5" == 5` | true |

`EqualityOperatorsExample01.htm`

### 全等和全不相等

全等和全不相等运算符的操作与相等和不相等运算符相同，不同之处在于它们在测试相等性之前不会转换操作数。全等运算符用三个等号（`===`）表示，并且只有当操作数在不转换的情况下相等时才返回 `true`，如下例所示：

![image](img/logo1.gif)

```
var result1 = ("55" == 55);    //true 因为转换而相等
var result2 = ("55" === 55);   //false 因为数据类型不同
```

`EqualityOperatorsExample02.htm`

在这段代码中，第一次比较使用相等运算符来比较字符串 `"55"` 和数字 `55`，结果返回 `true`。正如之前提到的，这是因为字符串 `"55"` 被转换为数字 `55`，然后与另一个数字 `55` 进行比较。第二次比较使用全等运算符在不进行转换的情况下比较字符串和数字，当然，字符串不等于数字，所以输出为 `false`。

全不相等运算符用感叹号后跟两个等号（`!==`）表示，并且只有当操作数在不转换的情况下不等时才返回 `true`。例如：

![image](img/logo1.gif)

```
var result1 = ("55" == 55);    //true 因为转换而相等
var result2 = ("55" === 55);   //false 因为数据类型不同
```

`EqualityOperatorsExample03.htm`

在这里，第一次比较使用相等运算符来比较字符串 `"55"` 和数字 `55`，结果返回 `true`。正如之前提到的，这是因为字符串 `"55"` 被转换为数字 `55`，然后与另一个数字 `55` 进行比较。第二次比较使用全等运算符在不进行转换的情况下比较字符串和数字，当然，字符串不等于数字，所以输出为 `false`。

![image](img/pen.gif)

由于相等和不相等运算符的转换问题，建议使用全等和全不相等。这有助于保持数据的完整性。

## 赋值运算符

简单赋值通过等号（`=`）完成，并将右侧的值赋值给左侧的变量，如下：

```
var num = 10;
```

复合赋值使用乘法、加法或位移运算符后跟等号（`=`）。这些赋值设计用于此类常见情况的简写：

```
var num = 10;
num = num + 10;
```

第二行代码可以用复合赋值替换：

```
var num = 10;
num += 10;
```

复合赋值运算符存在于每个主要的数学运算以及其他运算中。它们如下：

* 乘法赋值（`*=`）
* 除法赋值（`/=`）
* 取模赋值（`%=`）
* 加赋值（`+=`）
* 减赋值（`-=`）

## 赋值运算符

* 左移/赋值（`<<=`）
* 有符号右移/赋值（`>>=`）
* 无符号右移/赋值（`>>>=`）

这些运算符专门设计为实现操作的简写方式。它们不会带来任何性能上的提升。

## 逗号运算符

逗号运算符允许在单个语句中执行多个操作，如下所示：

```javascript
var num1=1, num2=2, num3=3;
```

大多数情况下，逗号运算符用于变量声明；然而，它也可以用于赋值。当以这种方式使用时，逗号运算符始终返回表达式中的最后一项，如下例所示：

```javascript
var num = (5, 1, 4, 8, 0);  //num 变为 0
```

在这个示例中，`num` 被赋值为 `0`，因为它是表达式中的最后一项。逗号以这种方式的情况并不多，但了解这种行为的存在是有帮助的。

## 语句 (STATEMENTS)

`ECMA-262` 描述了若干语句（也称为流程控制语句）。本质上说，语句定义了 ECMAScript 大部分的语法，并通常使用一个或多个关键字来完成给定的任务。语句可以是简单的，例如告诉函数退出；也可以是复杂的，例如指定要重复执行的命令数量。

### if 语句

大多数编程语言中最频繁使用的语句之一是 `if` 语句。`if` 语句具有如下语法：

```javascript
if (condition) statement1 else statement2
```

`condition` 可以是任何表达式；它不需要评估为实际布尔值。ECMAScript 会通过对表达式调用 `Boolean()` 转换函数自动将表达式的结果转换为布尔值。如果条件评估为 `true`，则执行 `statement1`；如果条件评估为 `false`，则执行 `statement2`。每个语句都可以是单行代码，也可以是一个代码块（括在大括号内的一组代码行）。考虑这个示例：

![image](img/logo1.gif)

```javascript
if (i > 25)
    alert("Greater than 25.");    //单行语句
else {
    alert("Less than or equal to 25.");  //块语句
}
```

`IfStatementExample01.htm`

最好的代码编写实践是始终使用块语句，即使只执行一行代码。这样做可以避免对每个条件下应该执行什么内容产生困惑。

你也可以像这样将 `if` 语句链在一起：

```javascript
if (condition1) statement1 else if (condition2) statement2 else statement3
```

这是一个示例：

```javascript
if (i > 25) {
    alert("Greater than 25.");
} else if (i < 0) {
    alert("Less than 0.");
} else {
    alert("Between 0 and 25, inclusive.");
}
```

`IfStatementExample02.htm`

### do-while 语句

`do-while` 语句是一种后置测试循环，这意味着退出条件只有在循环体内的代码执行后才被评估。在评估表达式之前，循环体至少会被执行一次。其语法如下：

```javascript
do {
    statement
} while (expression);
```

这里是它的用法示例：

![image](img/logo1.gif)

```javascript
var i = 0;
do {
   i += 2;
} while (i < 10);
```

`DoWhileStatementExample01.htm`

在这个示例中，只要 `i` 小于 `10`，循环就会继续。变量从 `0` 开始，并在每次循环中增加 2。

![image](img/pen.gif)

这种后置测试循环通常用于在退出前应至少执行一次循环体的情况。

### while 语句

`while` 语句是一种前置测试循环。这意味着退出条件在循环体内的代码执行之前就会被评估。正因如此，循环体可能永远不会执行。其语法如下：

```javascript
while(expression) statement
```

这里是它的用法示例：

```javascript
var i = 0;
while (i < 10) {
   i += 2;
}
```

`WhileStatementExample01.htm`

在这个示例中，变量 `i` 初始等于 `0`，并在每次循环中增加 2。只要变量小于 `10`，循环就会继续。

### for 语句

`for` 语句也是一种前置测试循环，并额外具备进入循环前进行变量初始化以及定义要执行的循环后代码的能力。其语法如下：

```javascript
for (initialization; expression; post-loop-expression) statement
```

这里是它的用法示例：

![image](img/logo1.gif)



```javascript
var count = 10;
for (var i=0; i < count; i++){
    alert(i);
}
```

`ForStatementExample01.htm`

这段代码定义了一个值为 `0` 的变量 `i`。只有当条件表达式 `(i < count)` 评估为 `true` 时，才会进入 `for` 循环，因此代码体可能不会被执行。如果执行了体，循环后表达式也会执行，从而迭代变量 `i`。这个 `for` 循环与以下代码相同：

```javascript
var count = 10;
var i = 0;
while (i < count)
```

初始化、控制表达式和循环后表达式都是可选的。通过省略这三部分可以创建一个无限循环，如下：

```javascript
for (;;)              //无限循环
    doSomething();
}
```

仅包含控制表达式实际上是将 `for` 循环转换为了 `while` 循环，如下：

![image](img/logo1.gif)

```javascript
var count = 10;
var i = 0;
for (; i < count; ){
    alert(i);
    i++;
}
```

### for-in 语句

`for-in` 语句是一种严格的迭代语句。它用于枚举对象的属性。其语法如下：

```javascript
for (property in expression) statement
```

这里是它的用法示例：

```javascript
for (var propName in window) {
     document.write(propName);
}
```

在 Safari 3 之前的版本中，`for-in` 语句存在一个 bug，会导致某些属性被返回两次。

### 标签语句 (Labeled Statements)

可以使用以下语法对语句进行标记，以便后续使用：

```
label: statement
```

这是一个示例：

```
start: for (var i=0; i < count; i++) {
    alert(i);
}
```

在这个示例中，可以通过 `break` 或 `continue` 语句在稍后引用标签 `start`。标签语句通常与嵌套循环中使用。

### break 和 continue 语句

`break` 和 `continue` 语句对循环中代码的执行提供了更严格的控制。`break` 语句会立即退出循环，强制执行继续到循环后的下一条语句。相反，`continue` 语句会立即退出循环，但执行将从循环的顶部继续。这是一个示例：

![image](img/logo1.gif)

```
var num = 0;

for (var i=1; i < 10; i++) {
    if (i % 5 == 0) {
        break;
    }
    num++;
}

alert(num);    //4
```

`BreakStatementExample01.htm`

在此代码中，`for` 循环将变量 `i` 从 1 增加到 10。在循环体内部，`if` 语句检查 `i` 的值是否能被 5 整除（使用模运算符）。如果是，则执行 `break` 语句并退出循环。变量 `num` 初始为 0，表示循环执行的次数。在触发 `break` 语句后，执行的下一行代码是 `alert`，显示显示 4。因此循环执行了四次，因为当 `i` 等于 5 时，`break` 语句在 `num` 增加之前导致了循环退出。如果将 `break` 替换为 `continue`，则可以看到不同的效果：

![image](img/logo1.gif)

```
var num = 0;

for (var i=1; i < 10; i++) {
    if (i % 5 == 0) {
        continue;
    }
    num++;
}

alert(num);    //8
```

`ContinueStatementExample01.htm`

在这里，`alert` 显示 8，即循环执行的次数。当 `i` 达到值 5 时，循环在 `num` 增加之前退出，但执行会在下一次迭代继续（此时值为 6）。循环继续继续直到自然完成（即 `i` 等于 10）。`num` 的最终值是 8 而不是 9，因为由于 `continue` 语句导致了一次未增加。

`break` 和 `continue` 语句都可以配合标签语句使用，以返回代码中的特定位置。这通常用于嵌套循环的情况，如下例所示：

```
var num = 0;

outermost:
for (var i=0; i < 10; i++) {
     for (var j=0; j < 10; j++) {
        if (i == 5 && j == 5) {
            break outermost;
        }
        num++;
    }
}

alert(num);    //55
```

`BreakStatementExample02.htm`

在这个示例中，`outermost` 标签指示第一个 `for` 语句。每个循环通常执行 10 次，这意味着 `num++` 语句通常执行 100 次，因此当执行完成时`num` 应该等于 100。这里的 `break` 语句接收一个参数：要跳出的标签。添加标签允许 `break` 语句不仅跳出内部的 `for` 语句（使用变量 `j`），还跳出外部的 `for` 语句（使用变量 `i`）。由于由于，`num` 的值为 55，因为当 `i` 和 `j` 都等于 5 时，执行停止了。`continue` 语句可以以相同的方式使用，如下例所示：

![image](img/logo1.gif)

```
var num = 0;

outermost:
for (var i=0; i < 10; i++) {
     for (var j=0; j < 10; j++) {
        if (i == 5 && j == 5) {
            continue outermost;
        }
        num++;
    }
}

alert(num);    //95
```

`ContinueStatementExample02.htm`

在这种情况下，`continue` 语句强制执行继续——不是在内部循环中，而是在外部循环中。当 `j` 等于 5 时，执行 `continue`，这意味着内部循环跳过了五次迭代，导致 `num` 等于 95。

结合 `break` 和 `continue` 使用标签语句非常强大，但如果过度使用可能会导致调试问题。请务必使用描述性强的标签，并尝试不要嵌套超过几个循环。

### with 语句

`with` 语句设置了特定对象内代码的作用域。语法如下：

```
with (expression) statement;
```

`with` 语句的创建是为了在反复对同一个对象进行编码时方便，如下例所示：

```
var qs = location.search.substring(1);
var hostName = location.hostname;
var url = location.href;
```

在这里，每行代码都使用了 `location` 对象。这段代码可以使用 `with` 语句重写如下：

```
with(location){
    var qs = search.substring(1);
    var hostName = hostname;
    var url = href;
}
```

`WithStatementExample01.htm`

在重写后的代码中，`with` 语句与 `location` 对象结合使用。这意味着语句内部每个变量首先被视为局部变量。如果发现它不是局部变量，则搜索 `location` 对象查看其是否具有同名的属性。如果是，则该变量被求值作为 `location` 的属性。

在严格模式（strict mode）下，不允许使用 `with` 语句，并且会被视为语法错误。

![image](img/cross.gif)

由于对性能的影响以及调试的困难，在生产代码中使用 `with` 语句被广泛认为是一种糟糕的做法。

### switch 语句

与 `if` 语句密切相关的是 `switch` 语句，另一种从其他语言引入的流控制语句。ECcript 中的 `switch` 语句语法类似于其他语言，如下：

```
switch (expression)
  case value: statement
    break;
  case value: statement
    break;
  case value: statement
    break;
  default: statement
```

`switch` 语句中的每个 `case` 表示：“如果表达式等于该值，则执行语句。” `break` 关键字导致代码跳出 `switch` 语句。如果没有 `break` 关键字，代码执行将渗透到下一个 `case`。`default` 关键字指示当表达式不匹配任何 case 时要的操作（实际上它相当于 `else` 语句）。

本质上，`switch` 语句让开发者无需编写这样的代码：

```
if (i == 25){
  alert("25");
} else if (i == 35) {
  alert("35");
} else if (i == 45) {
  alert("45");
} else {
  alert("Other");
}
```

等效的 `switch` 语句如下：

![image](img/logo1.gif)

```
switch (i) {
    case 25: 
        alert("25");
        break;
    case 35: 
        alert("35");
        break;
    case 45: 
        alert("45");
        break;
    default: 
        alert("Other");
}
```

`SwitchStatementExample01.htm`

最好的做法是在每个 `case` 之后都放置 `break` 语句，以避免 case 渗透到下一个。如果你需要 `case` 语句渗透，请包含一个注释说明省略 `break` 语句是有故意的，如下所示：

```
switch (i) {
    case 25: 
        /* 渗透 */
    case 35: 
        alert("25 or 35");
        break;
    case 45: 
        alert("45");
        break;
    default: 
        alert("Other");
}
```

`SwitchStatementExample02.htm`

尽管 `switch` 语句是从其他语言借用的，但它在 ECMAScript 中有一些特性。首先，`switch` 语句支持所有数据类型（在许多语言中它只支持数字），因此它可以用于字符串甚至对象。其次，case 值不需要是常量；它们可以是变量甚至是表达式。考虑以下示例：

```javascript
switch ("hello world") {
    case "hello" + " world": 
        alert("Greeting was found.");
        break;
    case "goodbye": 
        alert("Closing was found.");
        break;
    default: 
        alert("Unexpected message was found.");
}
```

### SwitchStatementExample03.htm

在这个示例中，字符串值被用于 `switch` 语句中。第一个 `case` 实际上是一个计算字符串拼接的表达式。因为此拼接的结果等于 `switch` 的参数，所以 `alert` 显示“Greeting was found.”。使用 case 表达式的能力还允许你执行如下的操作：

![image](img/logo1.gif)

```javascript
var num = 25;
switch (true) {
    case num < 0: 
        alert("Less than 0.");
        break;
    case num >= 0 && num <= 10: 
        alert("Between 0 and 10.");
        break;
    case num > 10 && num <= 20: 
        alert("Between 10 and 20.");
        break;
    default: 
        alert("More than 20.");
}
```

### SwitchStatementExample04.htm

在这里，变量 `num` 定义在 `switch` 语句之外。传入 `switch` 语句的表达式是 `true`，因为每个 `case` 都是一个返回 `Boolean` 值的条件。每个 `case` 会按顺序求值，直到找到匹配项或遇到 `default` 语句（在本例中如此）。

![image](img/pen.gif)

`switch` 语句使用全等运算符来比较值，因此不会发生类型转换（例如，字符串 "10" 不等于数字 10）。

# 函数 (FUNCTIONS)

函数是任何语言的核心，因为它们允许封装可以在任何地方任何时间运行的语句。ECMAScript 中的函数使用 `function` 关键字声明，后跟一组参数，然后是函数体。基本语法如下：

```javascript
function functionName(arg0, arg1,...,argN) {
    statements
}
```

这是一个示例：

```javascript
function sayHi(name, message) {
    alert("Hello " + name + ", " + message);
}
```

### FunctionExample01.htm

该函数可以通过使用函数名来调用，后跟在括号内的函数参数（如果有多个参数，则用逗号分隔）。调用 `sayHi()` 函数的代码如下：

```javascript
sayHi("Nicholas", "how are you today?");
```

此函数调用的输出是："Hello Nicholas, how are you today?"。命名参数 `name` 和 `message` 被用作字符串拼接的一部分最终显示在 `alert` 中。

ECMAScript 中的函数不需要指定它们是否返回数值。任何函数都可以通过使用 `return` 语句后跟要返回的值来随时返回一个值。考虑这个示例：

![image](img/logo1.gif)

```javascript
function sum(num1, num2) {
    return num1 + num2;
}
```

### FunctionExample02.htm

`sum()` 函数将两个值相加并返回结果。注意，除了 `return` 语句外，没有特殊的声明表示该函数返回数值。可以使用以下方式调用此函数：

```javascript
var result = sum(5, 10);
```

请记住，函数在遇到 `return` 语句时会停止执行并立即退出。因此，`return` 语句之后的任何代码都永远不会执行。例如：

```javascript
function sum(num1, num2) {
    return num1 + num2;
    alert("Hello world");    //永远不会执行
}
```

在这个示例中，`alert` 永远不会显示，因为它出现在 `return` 语句之后。

在函数中也可以有多个 `return` 语句，如下所示：

```javascript
function diff(num1, num2) {
    if (num1 < num2) {
        return num2 - num1;
    } else {
        return num1 - num2;
    }
}
```

### FunctionExample03.htm

在这里，`diff()` 函数确定两个数字之间的差值。如果第一个数字小于第二个数字，它从第二个中减去第一个；否则，从第一个中减去第二个。代码的每个分支都有自己的 `return` 语句来执行正确的计算。

`return` 语句也可以在不指定返回值的情况下使用。当这样这样使用时，函数立即停止执行并返回 `undefined` 作为其值。这通常用于不返回数值的函数以提前停止函数执行，如下例所示，其中 `alert` 将不会显示：

![image](img/logo1.gif)

```javascript
function sayHi(name, message) {
    return;
    alert("Hello " + name + ", " + message);    //永远不会调用
}
```

### FunctionExample04.htm

![image](img/pen.gif)

建议函数要么始终返回数值，要么从不返回数值。编写一个有时返回值的函数会引起困惑，特别是在调试期间。

严格模式对函数有几项限制：

- 任何函数不能命名为 `eval` 或 `arguments`。

- 任何命名参数不能命名为 `eval` 或 `arguments`。



两个命名参数不能同名。

如果发生这些情况，将被视为语法错误且代码将无法执行。

## 理解参数 (Understanding Arguments)

ECMAScript 中的参数的行为与其他语言中的参数并不相同。

`doAdd()` 函数仅在只有一个参数时才会给数字加 10；如果有两个参数，它们将会被简单地相加并返回。因此，`doAdd(10)` 返回 `20`，而 `doAdd(30,20)` 返回 `50`。这虽然不如函数重载完美，但它是解决这一 ECMAScript 局限性的足够替代方案。

关于参数的另一个重要点是，`arguments` 对象可以与命名参数结合使用，如下所示：

![image](img/logo1.gif)

```javascript
function doAdd(num1, num2) {
    if(arguments.length == 1) {
        alert(num1 + 10);
    } else if (arguments.length == 2) {
        alert(arguments[0] + num2);
    }
}
```

`FunctionExample08.htm`

在 `doAdd()` 函数的重写中，两个命名参数与 `arguments` 对象结合使用。命名参数 `num1` 持有的值与 `arguments[0]` 相同，因此它们可以互换使用（`num2` 和 `arguments[1]` 也是如此）。

`arguments` 的另一个有趣行为是，它的值始终与对应命名参数的值保持同步。例如：

```javascript
function doAdd(num1, num2) {
    arguments[1] = 10;
    alert(arguments[0] + num2);
}
```

`FunctionExample09.htm`

此版本的 `doAdd()` 总是会将第二个参数重写为值 `10`。由于 `arguments` 对象中的值会自动反映在对应的命名参数中，因此对 `arguments[1]` 的更改也会改变 `num2` 的值，所以它们两者的值都是 `10`。不过，这并不意味着它们访问同一个内存空间；它们的内存空间是独立的，但恰好保持了同步。这种效果是单向的：更改命名参数不会导致 `arguments` 中对应值发生变化。另一个需要记住的是：如果只传递了一个参数，那么将 `arguments[1]` 设置为值将不会反映在命名参数中。这是因为 `arguments` 对象的长度是根据传递的参数数量设置的，而不是根据函数列出的命名参数数量设置的。

任何未传递到函数的命名参数都会被自动赋值为 `undefined`。这类似于定义一个变量但未对其初始化。例如，如果只向 `doAdd()` 函数传递了一个参数，那么 `num2` 的值就是 `undefined`。

严格模式对 `arguments` 对象的使用方式进行了多项更改。首先，像上一个示例中的赋值操作不再起作用。即使 `arguments[1]` 被赋值为 `10`，`num2` 的值仍然保持为 `undefined`。其次，尝试重写 `arguments` 的值将导致语法错误（代码将不会执行）。

![image](img/pen.gif)

ECMAScript 中的所有参数都是通过值传递的。无法通过引用传递参数。

## 无重载

ECMAScript 函数无法在传统意义上进行重载。在其他语言（如 `Java`）中，只要它们的签名（接受的参数类型和数量）不同，就可以为同一个函数编写两个定义。正如恰恰所介绍的，ECMAScript 中的函数没有签名，因为参数被表示为一个包含零或多个值的数组。由于没有函数签名，真正的重载是不可能的。

如果在 ECMAScript 中定义了两个同名的函数，那么最后一个函数将成为该名称的所有者。考虑以下示例：

![image](img/logo1.gif)

```javascript
function addSomeNumber(num){
    return num + 100;
}

function addSomeNumber(num) {
    return num + 200;
}

var result = addSomeNumber(100);    //300
```

`FunctionExample10.htm`

在这里，函数 `addSomeNumber()` 被定义了两次。第一个版本向参数加 100，第二个版本加 200。当调用最后一行时，它返回 300，因为第二个函数重写了第一个。

如提到的，通过检查传递到函数的参数类型和数量并据此做出，可以模拟方法的重载。

## 总结

JavaScript 的核心语言特性定义在 ECMA-262 中，是一种名为 ECMAScript 的伪语言。ECMAScript 包含了完成基本计算任务所需的所有基本语法、运算符、数据类型和对象，尽管它没有提供输入或产生输出的方法。理解 ECMAScript 及其复杂性对于完全理解在浏览器中实现的 JavaScript 至关重要。实现最广泛的 ECMAScript 版本是 ECMA-262 第三版定义的版本，尽管许多已开始实现第五版。以下是 ECMAScript 的一些基本元素：

* ECMAScript 中的基本数据类型有 `Undefined`、`Null`、`Boolean`、`Number` 和 `String`。
* 与其他语言不同，它没有区分整数和浮点数的独立数据类型；`Number` 类型代表所有数字。
* 还有一种复杂数据类型 `Object`，它是语言中所有对象的基类型。
* 严格模式对语言中某些容易出错的部分施了限制。
* ECMAScript 提供了许多其他语言中的基本运算符，包括算术运算符、布尔运算符、关系运算符、相等运算符和赋值运算符。

# 第 4 章：变量、作用域与内存

## 本章内容

* 处理原始值和引用值
* 理解执行上下文
* 理解垃圾回收

原始值和引用值的定义方式相似：创建一个变量并为其赋值一个值。然而，一旦这些值被存储在变量中，你对这些值可以进行的操作是完全不同的。当你处理引用值时，可以随时添加、更改或删除属性和方法。考虑下面这个示例：

![image](img/logo1.gif)

```javascript
var person = new Object();
person.name = "Nicholas";
alert(person.name);    //"Nicholas"
```

`DynamicPropertiesExample01.htm`

在这里，创建了一个对象并将其存储在变量 `person` 中。接下来，添加了一个名为 `name` 的属性并为其赋值字符串值 "Nicholas"。从该点起，该新属性是可以访问的，直到对象被销毁或该属性被显式移除。

原始值无法为它们添加属性，尽管尝试这样做不会导致错误。这里有一个示例：

```javascript
var name = "Nicholas";
name.age = 27;
alert(name.age);    //undefined
```

`DynamicPropertiesExample02.htm`

在这里，在字符串 `name` 上定义了一个名为 `age` 的属性并赋值值为 27。然而，在紧接着的行，该属性消失了。只有引用值可以动态定义属性供以后使用。

## 值的复制

除了存储方式的不同之外，原始值和引用值在从一个变量拷贝到另一个变量时的行为也不同。当一个原始值从一个变量赋值给另一个变量时，存储在变量对象上的值会被创建并复制到新变量的位置。考虑以下示例：

```javascript
var num1 = 5;
var num2 = num1;
```

在这里，`num1` 包含值 5。当 `num2` 初始化为 `num1` 时，它也获得了值 5。这个值与存储在 `num1` 中的值是完全分离的，因为它是该值的拷贝。现在这些变量中的每一个都可以独立使用，而不会产生副作用。这一过程在图 4-1 中进行了图示。

FIGURE 4-1

![image](img/f087-01.jpg)

当引用值从一个变量赋值给另一个变量时，存储在变量对象上的值也会被复制到新变量的位置。区别在于，这个值实际上是指存储在堆上的对象的指针。一旦操作完成，两个变量将指向完全相同的对象，因此对其中一个修改将反映在另一个上，如下例所示：

```javascript
var obj1 = new Object();
var obj2 = obj1;
obj1.name = "Nicholas";
alert(obj2.name);    //"Nicholas"
```

在这个示例中，变量 `obj1` 被填充了一个新对象实例。然后这个值被复制到 `obj2` 中，这意味着两个变量现在都指向同一个对象。当在 `obj1` 上设置属性 `name` 时，以后可以从 `obj2` 访问，因为它们都指向同一个对象。图 4-2 显示了变量对象上的变量与堆上的对象之间的关系。

FIGURE 4-2

![image](img/f087-02.jpg)

## 参数传递

ECMAScript 中所有的函数参数都是通过值传递的。这意味着函数外部的值会被复制到函数内部的参数中，方式就像值从一个变量拷贝到另一个变量一样。如果值是原始值，它的行为就像原始变量拷贝；如果值是引用，它的行为就像引用变量拷贝。这通常是开发者感到困惑的一点，因为变量既通过值访问，也通过引用访问，但参数只通过值传递。

当参数通过值传递时，该值会被复制到局部变量中（一个具名参数，在 ECMAScript 中是 `arguments` 对象中的一个槽位）。当参数通过引用传递时，值在内存中的位置被存储在局部变量中，这意味着对局部变量的更改将反映在函数外部。（这在 ECMAScript 中是不可能的）。考虑以下示例：

![image](img/logo1.gif)

```javascript
function addTen(num) {
    num += 10;
    return num;
}

var count = 20;
var result = addTen(count);
alert(count);    //20 - no change
alert(result);   //30
```

`FunctionArgumentsExample01.htm`

在这里，函数 `addTen()` 有一个参数 `num`，它本质上是一个局部变量。当调用时，变量 `count` 被作为参数传入。该变量的值为 20，被复制到参数 `num` 中供 `addTen()` 内部使用。在函数内部，参数 `num` 的值通过加 10 被改变，但这不会改变函数外部存在的原始变量 `count`。参数 `num` 和变量 `count` 并不识别彼此；它们只是恰好具有相同的值。如果 `num` 是通过引用传递的，那么 `count` 的值将变为 30，以反映函数内部的更改。在使用数字等原始值时这一事实是显而易见的，但在使用对象时，情况就不那么明确了。以此为例：

```javascript
function setName(obj) {
    obj.name = "Nicholas";
}

var person = new Object();
setName(person);
alert(person.name);    //"Nicholas"
```

`FunctionArgumentsExample02.htm`

在这段代码中，创建了一个对象并将其存储在变量 `person` 中。然后这个对象被传递给 `setName()` 方法，并在那里被复制到 `obj`。在函数内部，`obj` 和 `person` 都指向同一个对象。结果是 `obj` 正在通过引用访问对象，尽管它是通过值传递进函数的。当在函数内部的 `obj` 上设置属性 `name` 时，这一更改将反映在函数外部，因为它指向的对象全局地存在于堆上。许多开发者错误地假设，当对对象的局部更改反映到全局时，意味着参数是通过引用传递的。为了证明对象是通过通过值传递的，请考虑以下修改后的代码：

```javascript
function setName(obj) {
    obj.name = "Nicholas";
    obj = new Object();
    obj.name = "Greg";
}

var person = new Object();
setName(person);
alert(person.name);    //"Nicholas"
```

此示例与上一个示例的区别在于 `setName()` 中添加了两行代码，它们重新定义了 `obj` 为一个新的对象。当 `person` 传入 `setName()` 时，其 `name` 属性被设置为 "Nicholas"。然后变量 `obj` 被设置为一个新的对象，其 `name` 属性被设置为 "Greg"。如果 `person` 是通过引用传递的，那么 `person` 将自动指向名为 "Greg" 的对象。然而，当再次访问 `person.name` 时，它的值是 "Nicholas"，这表明即使参数内部的值改变了，原始引用仍然保持完整。当 `obj` 在函数内部被重写时，它变成了指向局部对象的指针。该局部对象在函数执行结束时被销毁。

![image](img/pen.gif)

将 ECMAScript 中的函数参数仅仅视为局部变量。

## 确定类型

上一章引入的 `typeof` 运算符是判断变量是否为原始类型的最佳方法。具体来说，它是判断变量是否为字符串、数字、布尔或未定义的最佳方法。如果值是对象或 null，`typeof` 返回 "object"，如下所示：

![image](img/logo1.gif)

```javascript
var s = "Nicholas";
var b = true;
var i = 22;
var u;
var n = null;
var o = new Object();

alert(typeof s);   //string
alert(typeof i);   //number
alert(typeof b);   //boolean
alert(typeof u);   //undefined
alert(typeof n);   //object
alert(typeof o);   //object
```

`DeterminingTypeExample01.htm`

虽然 `typeof` 对于原始值作用良好，但对于引用值来说它的作用有限。通常情况下，你并不关心一个值是否是对象——你真正想知道的是它是什么种类型的对象。为了辅助这种识别，`ECMAScript` 提供了 `instanceof` 运算符，其语法如下：

```javascript
result = variable instanceof constructor
```

如果 `variable` 是给定引用类型的实例（通过其原型链进行识别，如第 6 节中讨论的），则 `instanceof` 运算符返回 `true`。考虑以下示例：

```javascript
alert(person instanceof Object);   //变量 person 是一个 Object 吗？
alert(colors instanceof Array);    //变量 colors 是一个 Array 吗？
alert(pattern instanceof RegExp);  //变量 pattern 是一个 RegExp 吗？
```

根据上所有的引用值都是 `Object` 的实例，因此当 `instanceof` 运算符与引用值和 `Object` 构造函数配合时，它始终返回 `true`。同样，如果将 `instanceof` 用于原始值，它将始终返回 `false`，因为原始值不是对象。

![image](img/pen.gif)

当 `typeof` 运算符用于函数时，它也会返回“function”。在 Safari（版本 5 之前）和 Chrome（版本 7 之前）中用于正则表达式时，`typeof` 返回“function”是由于一个实现细节。`ECMA-262` 规定任何实现内部 `[[Call]]` 方法的对象应该通过 `typeof` 返回“function”。由于正则表达式在这些浏览器中实现了该方法，因此 `typeof` 返回“function”。在 Internet Explorer 和 Firefox 中，`typeof` 对正则表达式返回“object”。

## 执行上下文与作用域

执行上下文（execution context）的概念，简单地称为 `context`，在 JavaScript 中至关重要。变量或函数的执行上下文定义了它可以访问哪些其他数据，以及它应该如何表现。每个执行上下文都关联一个变量对象，所有定义的变量和函数都存在于该对象上。该对象无法被代码访问，但在后台用于处理数据。

全局执行上下文是最外层的。根据 `ECMAScript` 实现的宿主环境，代表此上下文的对象可能会不同。在 Web 浏览器中，全局上下文被认为是 `window` 对象（第 8 节讨论），因此所有全局变量和函数都是作为 `window` 对象的属性和方法创建的。当一个执行上下文执行完所有代码后，它就会被销毁，并带走其中定义的所有变量和函数（全局上下文直到应用程序退出时才会被销毁，例如关闭网页或关闭 浏览器）。

每个函数调用都有自己的执行上下文。每当代码执行进入函数时，函数的上下文就会被推入上下文栈（context stack）中。在函数执行完毕后，栈会被弹出，将控制权返回给之前执行的上下文。这种机制控制了整个 `ECMAScript` 程序的执行流。

当代码在上下文中执行时，会创建一个变量对象的作用域链（scope chain）。作用域链的作用为执行上下文可以访问的所有变量和函数提供有序的访问。作用域链的前端始终是执行代码的上下文的变量对象。如果该上下文是函数，则使用激活对象（activation object）作为变量对象。激活对象始于一个名为 `arguments` 的定义变量（这在全局上下文中不存在）。链中的下一个变量对象来自包含它的上下文，再下一个则来自下一个包含它的上下文。这种模式一直持续到到达全局上下文；全局上下文的变量对象始终是作用域链的最后一个。



标识符通过在作用域链中搜索标识符名称来解析。搜索始终从链的前端开始，并向后端移动，直到找到标识符。（如果没有找到标识符，通常会发生错误。）

考虑以下代码：

![image](img/logo1.gif)

```
var color = "blue";

function changeColor(){
我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。 if (color === "blue"){
        color = "red";
    } else {
        color = "blue";
    }
}

changeColor();
```

`ExecutionContextExample01.htm`

在这个简单的示例中，函数`changeColor()`拥有一个包含两个对象的作用域链：它自己的变量对象（在其定义了`arguments`对象）和全局上下文的变量对象。因此，变量`color`在函数内部是可以访问的，因为可以在作用域链中找到它。

此外，局部定义的变量在局部上下文中可以与全局变量交替使用。这里有一个示例：

```
var color = "blue";

function changeColor(){
    var anotherColor = "red";

    function swapColors(){
        var tempColor = anotherColor;
        anotherColor = color;
        color = tempColor;

        //color, anotherColor, 和 tempColor 在这里都是可访问的
    }

    //color 和 anotherColor 在这里可以访问，但 tempColor 不行        
    swapColors();
}

//这里这里可以访问 color
changeColor();
```

这段代码中有三个执行上下文：全局上下文、`changeColor()`的局部上下文以及`swapColors()`的局部上下文。全局上下文有一个变量`color`和一个函数`changeColor()`。`changeColor()`的局部上下文有一个名为`anotherColor`的变量和一个名为`swapColors()`的函数，但它也可以访问来自全局上下文的变量`color`。`swapColors()`的局部上下文有一个名为`tempColor`的变量，它仅在该上下文中可访问。全局上下文和`swapColors()`的局部上下文都访问`tempColor`。尽管如此，在`swapColors()`内部，其他上下文的变量是可以完全访问的，因为它们是父上下文。图 4-3 表示了上述示例的作用域链。

图 4-3

![image](img/f092-01.jpg)

在图中，矩形代表特定的执行上下文。内部上下文可以通过作用域链访问所有外部上下文，但外部上下文无法访问内部上下文的任何内容。上下文之间的连接是线性且有序的。每个上下文都可以向上作用域链搜索变量和函数，但没有上下文可以向下搜索另一个执行上下文。`swapColors()`局部上下文的作用域链中有三个对象：`swapColors()`变量对象、来自`changeColor()`的变量对象以及全局变量对象。`swapColors()`的局部上下文从自己的变量对象开始搜索变量和函数，然后沿着链移动。`changeColor()`上下文的作用域链只有两个对象：它自己的变量对象和全局变量对象。这意味着它无法访问`swapColors()`的上下文。

尽管尽管只有两种主要的执行上下文类型（全局和函数，第三种存在于`eval()`的调用内部），还有其他增强作用域链的方法。某些语句会导致作用域链前端临时添加内容，并在代码执行后将其移除。这种情况发生两次，具体是在执行进入以下任一处时：

*   `try-catch`语句中的`catch`块

*   `with`语句

这两个语句都会在作用域链的前端添加一个变量对象。对于`with`语句，指定的对象会被添加到作用域链中；对于`catch`语句，会创建一个新的变量对象，并包含对抛出的错误对象的声明。考虑以下内容：

![image](img/logo1.gif)

```
function buildUrl() {
    var qs = "?debug=true";

    with(location){
        var url = href + qs;        
    }

    return url;
}
```

`ExecutionContextExample03.htm`

在这个示例中，`with`语句作用于`location`对象，因此`location`本身被添加到作用域链的前端。在`buildUrl()`函数中定义了一个变量`qs`。当引用变量`href`时，它实际上引用的是`location.href`，它位于自己的变量对象中。当引用变量`qs`时，它引用的是`buildUrl()`中定义的变量，该变量位于函数上下文的变量对象中。`with`语句内部有一个对`url`的变量声明，它变成了函数上下文的一部分，因此可以作为函数值返回。

![image](img/pen.gif)

在 Internet Explorer 8 之前的 JavaScript 实现中存在偏差，`catch`语句中捕获的错误会被添加到执行上下文的变量对象，而不是`catch`语句的变量对象，这使得即使在`catchblock`外部也可以访问。这在 Internet Explorer 9 中被修复。

## 无块级作用域

JavaScript 缺乏块级作用域是一个常见的困惑来源。在其他类 C 语言中，用括号括起来的代码块拥有它们的作用域（更准确的描述是在 ECMAScript 中拥有它们各自的执行上下文），允许变量的条件定义。例如，以下代码的行为可能不符合预期：

```
if (true) {
    var color = "blue";
}

alert(color);    //"blue"
```

在这里，变量`color`定义在`if`语句内部。在 C、C++ 和 Java 等语言中，该变量在`if`语句执行后就会销毁。但在 JavaScript 中，变量声明会将变量添加到当前的执行上下文中（在本例中为全局上下文）。在处理`for`语句时需要记住这一点，该语句通常写成这样：

```
for (var i=0; i < 10; i++){
    doSomething(i);
}

alert(i);    //10
```

在具有块级作用域的语言中，`for`语句的初始化部分定义的变量仅存在于循环上下文中。在 JavaScript 中，变量`i`是`for`语句创建的，并在语句执行后继续存在于循环外部。

## 变量声明

当使用`var`声明变量时，它会被添加到最直接的上下文中。在函数中，最直接的是函数的本地上下文；在`with`语句中，最直接的是函数上下文。如果一个变量在没有先声明的情况下被初始化，它会被自动添加到全局上下文，如下例所示：

![image](img/logo1.gif)

```
function add(num1, num2) {
    var sum = num1 + num2;
    return sum;
}

var result = add(10, 20);  //30
alert(sum);                //会导致错误，因为 sum 不是有效变量
```

`ExecutionContextExample04.htm`

在这里，函数`add()`定义了一个名为`sum`的本地变量，包含加法操作的结果。该值作为函数值返回，但变量`sum`在函数外部不可用。如果在这个示例中省略了`var`关键字，则在`add()`被调用后`sum`变得可用，如下所示：

```
function add(num1, num2) {
    sum = num1 + num2;
    return sum;
}

var result = add(10, 20);  //30
alert(sum);                //30
```

`ExecutionContextExample05.htm`

在这里，变量`sum`初始化为一个值但从未使用`var`声明。当调用`add()`时，`sum`在全局上下文中创建，并在函数完成后仍继续存在，允许你稍后访问它。

![image](img/pen.gif)

在不声明的情况下初始化变量是 JavaScript 编程中非常常见的错误，可能会导致错误。建议在初始化变量之前始终声明变量以避免此类问题。在严格模式下，不声明而初始化变量会导致错误。

## 标识符查找

当在特定上下文中为了读取或写入标识符时，必须进行查找以确定该标识符代表什么。查找从作用域链的前端开始，寻找具有给定名称的标识符。如果在本地上下找到了该标识符名称，则停止查找并设置变量；如果查找没有找到变量名，则沿着作用域链继续查找（注意作用域链中的对象也有原型链，因此查找可能包括每个对象的原型链）。此过程一直持续，直到查找到达全局上下文的变量对象。如果在那里没有找到该标识符，说明它未被声明。

为了更好地说明标识符查找是如何发生的，请考虑以下示例：

![image](img/logo1.gif)

```
var color = "blue";

function getColor(){
    return color;
}

alert(getColor());  //"blue"
```

`ExecutionContextExample06.htm`

当调用示例中的`getColor()`时，引用了变量`color`。此时，开始了双步查找。首先搜索`getColor()`的变量对象中名为`color`的标识符。如果没有找到，则跳转到下一个变量对象（来自全局），然后搜索名为`color`的标识符。因为该变量对象是变量定义所在，查找结束。图 4-4 描述了这一查找过程。

图 4-4

![image](img/f095-01.jpg)

由于这种查找过程，引用本地变量会自动停止进入另一个变量对象。这意味着如果本地上下存在同名标识符，则无法引用父上下文中的标识符，如下例所示：

```
var color = "blue";

function getColor(){
    var color = "red";
    return color;
}

alert(getColor());  //"red"
```

`ExecutionContextExample07.htm`

在修改后的代码中，`getColor()`函数内部声明了一个名为`color`的本地变量。当函数被调用时，该变量被声明。当执行函数的第二行时，它知道必须使用名为`color`的变量。查找从本地上下文开始，在并在找到了值为 "red" 的变量。因为找到了变量，查找停止并使用了本地变量，这意味着函数返回 "red"。在声明`color`为本地变量之后出现的任何代码，在不指定为`window.color`的情况下都无法访问全局`color`变量。

变量查找并非没有代价的。访问本地变量比全局变量更快，因为不需要沿作用域链进行查找。不过，JavaScript 引擎正在不断优化标识符查找，因此这种差异在未来可能会变得微不足道。

## 垃圾回收

JavaScript 是一种带垃圾回收的语言，这意味着执行环境负责管理代码执行期间所需的内存。在`C`和`C++`等语言中，跟踪内存使用是一个首要考虑的问题，也是开发者面临许多问题的根源。JavaScript 通过自动分配所需的内存并回收不再被使用的内存，让开发者免于了内存管理的烦恼。其基本思想非常简单：找出哪些变量将不再被使用，并释放与它们相关的内存。这个过程是周期性的，垃圾回收器会在指定的间隔（或代码执行过程中预定义的收集时机）运行。

考虑函数内部局部变量的正常生命周期。变量在函数执行期间产生。此时，系统会在栈上（可能也在堆上）分配内存，以为该值提供存储空间。变量在函数内部被使用，然后函数结束。此时，该变量已不再被需要，因此它的内存可以被回收以供以后使用。在这种情况下，变量不再被需要是显而易见的，但并非所有情况都如此明显。垃圾回收器必须跟踪哪些变量可以使用、哪些不能使用，以便识别出可能的内存回收候选对象。识别未使用变量的策略可能根据实现方式而异，尽管浏览器中传统上使用了两种策略。

### 标记-清除 (Mark-and-Sweep)

JavaScript 最流行的垃圾回收形式被称为“标记-清除”。当一个变量进入上下文时（例如当在函数内部声明变量时），它会被标记为“在上下文中”。从逻辑上讲，处于上下文中的变量内存永远不应该被释放，因为只要该上下文继续执行，它们就一直可能被使用。当一个变量离开上下文时，它也会被标记为“不在上下文”。

变量可以以任何方式被标记。当变量在上下文中时，可能会翻转某个特定的位，也可能存在“在上下文”的变量列表和一个“不在上下文”的变量列表，变量在它们之间移动。标记的实现方式并不重要，关键在于理论。

当垃圾回收器运行时，它会标记所有存储在内存中的变量（再次，通过任何一种方式）。然后，它会清除处于上下文中的变量以及被这些上下文变量引用的变量的标记。之后被标记的变量被认为可以删除，因为它们无法通过任何上下文中的变量到达。随后，垃圾回收器会执行内存扫描，销毁每个标记的值并回收与它们相关的内存。

截至 2008 年，Internet Explorer、Firefox、Opera、Chrome 和 Safari 在其 JavaScript 实现中都使用了标记-清除垃圾回收（或其变体），尽管垃圾回收的时机有所不同。

### 引用计数 (Reference Counting)

第二种不那么流行的垃圾回收类型是引用计数。其核心思想是每个值都跟踪指向它的引用次数。当声明一个变量并分配一个引用值时，引用计数为 1。如果随后将另一个变量赋值为该值，引用计数就会加 1。同样，如果一个指向该值的变量被另一个值覆盖，引用计数就会减 1。当一个值的引用计数达到零时，就没有方法可以到达该值，回收相关的内存是安全的。垃圾回收器在下次运行时会释放引用计数为 0 的值的内存。

引用计数最初被 Netscape Navigator 3.0 使用，并立即遇到了一个严重问题：循环引用。当对象 A 有指向对象 B 的指针，而对象 B 有指向对象 A 的引用时，就会发生循环引用，例所示：

```javascript
function problem(){
    var objectA = new Object();
    var objectB = new Object();

    objectA.someOtherObject = objectB;
    objectB.anotherObject = objectA;
}
```

在这个示例中，`objectA`和`objectB`通过它们的属性互相引用，这意味着每个对象的引用计数都是 2。在标记-清除系统中，这不是一个问题，因为在函数完成后，两个对象都超出了作用域。但在引用计数系统中，`objectA`和`objectB`在函数退出后将继续存在，因为它们的引用计数永远不会达到零。如果反复调用这个函数，将导致大量内存永远无法回收。由于这个原因，Netscape 在 4.0 版本中放弃了引用计数的垃圾回收程序，转而采用标记-清除的实现。遗憾的是，引用计数问题并未到此结束。

Internet Explorer 8 及更早版本中的所有对象并不是原生的 JavaScript 对象。浏览器对象模型 (BOM) 和文档对象模型 (DOM) 中的对象是在 C++ 中实现为 COM（组件对象模型）对象的，而 COM 对象使用引用计数进行垃圾回收。因此，尽管 Internet Explorer 的 JavaScript 引擎使用了标记-清除实现，在 JavaScript 中访问的任何 COM 对象仍然使用引用计数，这意味着当涉及 COM 对象时，循环引用仍然是一个问题。下面的简单示例演示了带有 COM 对象的循环引用：

```javascript
var element = document.getElementById("some_element");
var myObject = new Object();
myObject.element = element;
element.someObject = myObject;
```

这个示例在 DOM 元素 (`element`) 和原生 JavaScript 对象 (`myObject`) 之间建立了一个循环引用。`myObject`变量有一个名为`element`的属性指向`element`，而`element`变量有一个名为`someObject`的属性指向`myObject`。由于这种循环引用，即使 DOM 元素从页面上移除，它的内存也永远不会被回收。

为了避免这种循环引用问题，在使用完这些元素后应该切断原生 JavaScript 对象与 DOM 元素之间的连接。例如，以下代码清理了之前示例中的循环引用：

```javascript
myObject.element = null;
element.someObject = null;
```

将变量设置为`null`可以有效地切断变量与其之前引用的值之间的连接。下垃圾垃圾回收器运行时，这些值将被删除，内存将被回收。

Internet Explorer 9 通过将 BOM 和 DOM 对象转换为真正的 JavaScript 对象，解决了其中的一些问题，从而避免了存在两种不同垃圾回收算法的问题，并消除了常见的内存泄漏问题。

![image](img/pen.gif)

还有其他可能导致循环引用的模式，将在书中贯穿介绍。

### 性能 (Performance)



垃圾回收器定期运行，如果内存中存在大量的变量分配，这可能是一个开销巨大的过程，因此垃圾回收过程的时机非常重要。Internet Explorer 在与垃圾回收运行频率相关的性能问题上臭名昭著——它是基于分配次数运行的，具体为 256 次变量分配、4096 个对象/数组字面量和数组槽，或 64kb 的字符串。如果达到任何一个阈值，垃圾回收器就会运行。这种实现方式的问题在于，拥有这么多变量的脚本在其生命周期内可能一直拥有这么多变量，这意味着垃圾回收器将运行得非常频繁。这个问题导致了严重的性能问题，并引发了 Internet Explorer 7 中垃圾回收程序的改进。

随着 Internet Explorer 7 的发布，JavaScript 引擎的垃圾回收程序经过调整，可以动态更改变量、字面量和/或数组槽触发垃圾回收的分配阈值。Internet Explorer 7 的初始阈值与 Internet Explorer 6 相同。如果垃圾回收程序回收的分配内存小于 15%，则变量、字面量和/或数组槽的阈值将翻倍。如果该程序回收了高达 85% 的分配内存，则阈值将重置为默认值。这一简单的改进极大提升了浏览器在 JavaScript 密集型网页上的性能。

![image](img/pen.gif)

在某些浏览器中，可以触发垃圾回收过程，尽管并不建议这样做。在 Internet Explorer 中，`window.CollectGarbage()` 方法会立即触发垃圾回收。在 Opera 7 及更高版本中，调用 `window.opera.collect()` 会启动垃圾回收过程。

# 内存管理

在具有垃圾回收机制的编程环境中，开发者不需要不需要内存管理。然而，JavaScript 运行在一个内存管理和垃圾回收运行方式独特的环境中。浏览器中可用内存通常远少于桌面应用程序的可用内存。这更多是一种安全特性，确保运行 JavaScript 的网页不会因为耗尽所有系统内存而导致操作系统崩溃。内存限制不仅影响变量分配，还影响调用栈以及单线程中可以执行的语句数量。

将已用内存量保持在最低可以获得更好的页面性能。优化内存使用的最佳方法是确保你只保留执行代码时所必需的数据。当数据不再需要时，最好将其值设为 `null` 以释放引用——这被称为对值进行“解引用”（dereferencing）。这一建议主要适用于全局值和全局对象的属性。局部变量在离开作用域时会自动解引用，如下例所示：

```
function createPerson(name){
    var localPerson = new Object();
    localPerson.name = name;
    return localPerson;
}

var globalPerson = createPerson("Nicholas");

// 对 globalPerson 执行某些操作

globalPerson = null;
```

在这段代码中，变量 `globalPerson` 被填充了从 `createPerson()` 函数返回的值。在 `createPerson()` 内部，`localPerson` 创建了一个对象并为其添加了 `name` 属性。变量 `localPerson` 作为函数的返回值返回并赋值给 `globalPerson`。由于 `localPerson` 在 `createPerson()` 执行完成后离开了作用域，因此不需要显式地解引用。因为 `globalPerson` 是一个全局变量，当它不再需要时应该对其进行解引用，这正是最后一行所做的。

请记住，解引用一个值并自动回收与其相关的内存。解引目的是目的是该值已离开作用域，并在下次发生垃圾回收时被回收。

## 总结

JavaScript 变量可以存储两种类型的值：原始值（primitive values）和引用值（reference values）。原始值具有五种原始数据类型之一：Undefined、Null、Boolean、Number 和 String。原始值和引用值具有以下特征：

*   原始值的大小是固定的，因此存储在内存的栈（stack）中。

*   将原始值从一个变量复制到另一个变量会创建值的副本。

*   引用值是对象，存储在内存的堆（heap）中。

*   包含引用值的变量实际上只包含指向该对象的指针，而不是对象本身。

*   将引用值复制到另一个变量中只会复制指针，因此两个变量最终都引用同一个对象。

*   `typeof` 运算符确定值的原始类型，而 `instanceof` 运算符用于确定值的引用类型。

所有变量（原始引用和引用）都存在于执行上下文（也称为作用域）中，它决定了变量的生命周期以及代码哪些部分可以访问它。执行上下文可以总结如下：

*   执行上下文存在于全局（称为全局上下文）和函数内部。

*   每当进入一个新的执行上下文时，它都会创建一个作用链来搜索变量和函数。

*   函数局部的上下文不仅可以访问该作用域内的变量，还可以访问任何包含上下文以及全局上下文中的变量。

*   全局上下文只能访问全局上下文中的变量和函数，不能直接访问局部上下文中的任何数据。

*   变量的执行上下文有助于确定内存何时被释放。

JavaScript 是一种具有垃圾回收的编程环境，开发者无需担心内存分配或回收。JavaScript 的垃圾回收程序可以总结如下：

*   离开作用域的值将被自动标记为回收，并在垃圾回收过程中被删除。

*   主要的垃圾回收算法被称为“标记-清除”（mark-and-sweep），它标记当前未使用的值，然后回过头回收内存。

*   另一种算法是引用计数（reference counting），它跟踪指向特定值的引用数量。JavaScript 引擎不再使用这种算法，但由于在 JavaScript 中访问了非原生 JavaScript 对象（如 DOM 元素），它仍然影响 Internet Explorer。

*   当代码中存在循环引用时，引用计数会导致问题。

*   解引用变量不仅有助于处理循环引用，也有助于垃圾回收。为了辅助内存回收，全局对象、全局对象上的属性以及循环引用在不再需要时都应该被解引用。

# 第 5 章

## 引用类型

### 本章内容包括？

*   操作对象

*   创建和操作数组

*   理解基础 JavaScript 数据类型

*   处理原始值和原始包装

引用值（对象）是特定引用类型的实例。在 ECMAScript 中，引用类型是用于组织数据和功能的结构，通常被称为类（classes）。尽管技术上是面向对象的语言，但 ECMAScript 缺少一些与面向对象关联的基本构造，包括类和接口。引用类型有时称为对象定义，因为它们描述了对象应该具有的属性和方法

![image](img/pen.gif)

尽管引用类型与类相似，但这两个概念并不等同。为了避免混淆，书中其余部分将不再使用“类”一词。

再次，对象被视为特定引用类型的实例。通过使用 `new` 运算符加上构造函数来创建新对象。构造函数只是一个用于创建对象的函数。考虑以下行代码：

```
var person = new Object();
```

这段代码创建了一个 Object 引用的新实例并将其存储在变量 `person` 中。使用的构造函数是 `Object()`，它创建一个仅具有默认属性和方法的简单对象。

## 对象类型

到此为止，大多数引用值示例都使用了 `Object` 类型，它是 `ECMAScript` 中最常用的类型之一。虽然 `Object` 实例并没有多少功能，但它们非常适合在整个应用程序中存储和传输数据。

有两种方法可以显式创建 `Object` 实例。第一种是使用 `new` 运算符配合 `Object` 构造函数，如下所示：

![image](img/logo1.gif)

```
var person = new Object();
person.name = "Nicholas";
person.age = 29;
```

`ObjectTypeExample01.htm`

另一种方法是使用对象字面量符号。对象字面量符号是对象定义的简写形式，旨在简化具有许多属性的对象的创建。例如，下面的代码使用对象字面量符号定义了上一个示例中相同的 `person` 对象：

```
var person = {
    name : "Nicholas",
    age : 29
};
```

`ObjectTypeExample02.htm`

在这个示例中，左大括号（`{`）表示对象字面量的开始，因为它出现在表达式上下文中。`ECMAScript` 中的表达式上下文是指期望值（表达式）的上下文。赋值运算符表示后续期望一个值，因此左大括号表示表达式的开始。同样的大括号当出现在语句上下文中（例如跟在 `if` 语句条件之后），则表示块语句的开始。

接下来，指定了 `name` 属性，后面跟着一个冒号，然后是属性的值。对象字面量中使用逗号来分隔属性，因此字符串 `"Nicholas"` 之后有一个逗号，但在值 `29` 之后没有逗号，因为 `age` 是对象中的最后一个属性。在最后一个属性后包含逗号会导致 Internet Explorer 7 及之前的版本以及 Opera 产生错误。

在使用对象字面量符号时，属性名也可以指定为字符串或数字，如示例所示：

```
var person = {
    "name" : "Nicholas",
    "age" : 29,
    5: true
};
```

此示例产生了一个具有 `name` 属性、`age` 属性和属性 `"5"` 的对象。注意，数字属性名会自动转换为字符串。

还可以使用对象字面量符号通过留空大括号之间的空间来创建一个仅包含默认属性和方法的对象，如下所示：

```
var person = {};                    //同于 new Object()
person.name = "Nicholas";
person.age = 29;
```

这个示例等同于本部分的第一个，尽管它看起来有点奇怪。建议仅在需要指定属性以提高可读性时使用对象字面量符号。

![image](img/pen.gif)

通过对象字面量符号定义对象时，实际上不会调用 `Object` 构造函数（Firefox 2 及之前的版本确实调用过该构造函数；这在 Firefox 3 中被更改）。

虽然使用两种方法创建 `Object` 实例都是接受的，但开发者倾向于使用对象字面量符号，因为它的代码更少，并且视觉上封装了所有相关数据。事实上，对象字面量已成为向函数传递大量可选参数的优选方式，如示例所示：

![image](img/logo1.gif)

```
function displayInfo(args) {
    var output = "";

    if (typeof args.name == "string"){
        output += "Name: " + args.name + "\n";
    }

    if (typeof args.age == "number") {
        output += "Age: " + args.age + "\n";
    }

    alert(output);
}

displayInfo({ 
    name: "Nicholas", 
    age: 29
});

displayInfo({
    name: "Greg"
});
```

`ObjectTypeExample04.htm`

在这里，函数 `displayInfo()` 接受一个名为 `args` 的单个参数。该参数可能带有 `name` 或 `age` 属性，或者两者都有，或者两者都没有。该函数被设计为使用 `typeof` 运算符测试每个属性的存在，然后根据可用性构建要显示的消息。该函数随后被调用两次，每次都在对象字面量中指定不同的数据。该函数在两种情况下都能正常工作。

![image](img/pen.gif)

这种参数传递模式在当有大量可以传递给函数的可选参数时效果最好。泛而言之，命名参数更容易处理，但当有许多可选参数时，可能会变得臃肿。最佳方法是对于必需的参数使用命名参数，并使用对象字面量包含多个可选参数。

虽然对象属性通常使用点符号进行访问（这是许多面向对象语言的共同特征），但也可以通过括号符号访问属性。当你使用括号符号时，在括号之间放置一个包含属性名的字符串，如此示例所示：

```
alert(person["name"]);    //"Nicholas"
alert(person.name);       //"Nicholas"
```

从功能上讲，这两种方法没有区别。括号符号的主要优势是它允许使用变量进行属性访问，如示例所示：

```
var propertyName = "name";
alert(person[propertyName]);    //"Nicholas"
```

当属性名包含可能导致语法错误或关键字/保留字的字符时，你也可以使用括号符号。例如：

```
person["first name"] = "Nicholas";
```

由于名称 `"first name"` 包含空格，你无法使用点符号来访问它。属性名也可以包含非字母数字字符，只需要使用括号符号来访问。

泛而言之，除非需要变量，否则首选点符号。

## 数组类型

继 `Object` 类型，`Array` 类型可能是 `ECMAScript` 中最常用的类型。`Array` 与大多数语言中的数组非常不同。与其他语言一样，`ECMAScript` 数组是数据的有序列表，但每个槽位可以持有任何类型的数据。这意味着可以创建一个第一个是字符串、第二个是数字、第三个是对象的数组。`ECMAScript` 数组也是动态大小的，会自动适应任何添加的数据。

数组有两种基本创建方法。第一种是使用 `Array` 构造函数，如下：

```
var colors = new Array();
```

如果你知道数组将包含多少项，可以将数量传递给构造函数，并将具有该值的 `length` 属性。例如，下面的代码创建一个初始值为 `20` 的数组：

```
var colors = new Array(20);
```

`Array` 构造函数也可以传递包含在数组中的项。以下代码创建一个包含三个字符串值的数组：

```
var colors = new Array("red", "blue", "green");
```

可以通过向构造函数传递单个值创建一个数组。这有点复杂，因为提供单个数字总是创建一个具有指定数量项目的数组，而任何其他类型的参数创建一个包含指定值的单项数组。这是一个示例：

![image](img/logo1.gif)

```
var colors = new Array(3);      //创建一个包含三项的数组
var names = new Array("Greg");  //创建一个包含字符串 "Greg" 的单项数组
```

`ArrayTypeExample01.htm`

在使用 `Array` 构造函数时，可以省略 `new` 运算符。结果相同，如下所示：

```
var colors = Array(3);      //创建一个包含三项的数组
var names = Array("Greg");  //创建一个包含字符串 "Greg" 的单项数组
```

创建数组的第二种方法是使用数组字面量符号。数组字面量通过使用方括号并在它们之间放置逗号分隔的项列表来指定，如示例所示：

```javascript
var colors = ["red", "blue", "green"]; //创建一个包含三个字符串的数组
var names = [];                        //创建一个空数组
var values = [1,2,];                   //避免！创建一个包含 2 个或 3 个元素的数组
var options = [,,,,,];                 //避免！创建一个包含 5 个或 6 个元素的数组
```

### ArrayTypeExample02.htm

在这段代码中，第一行创建了一个包含三个字符串值的数组。第二行通过空方括号创建了一个空数组。第三行显示了在数组字面量的最后一个值之后遗留逗号的影响：在 Internet Explorer 8 及更早版本中，`values` 变为了一个包含值 1、2 和 `undefined` 的三元素数组；在所有其他浏览器中，`values` 是一个包含值 1 和 2 的二元素数组。这是由于 Internet Explorer 在该浏览器第 8 版本的 ECMAScript 实现中关于数组字面量的一个 bug 导致的。该 bug 的另一个实例显示在最后一行，它创建了一个包含 5 个（在 Internet Explorer 9+、Firefox、Opera、Safari 和 Chrome 中）或 6 个（在 Internet Explorer 8 及更早版本中）元素的数组。通过省略逗号之间的值，每个元素都会获得 `undefined` 值，这在逻辑上等同于调用 `Array` 构造函数并传递元素的数量。然而，由于早期 Internet Explorer 版本的实现不一致，强烈不建议使用这种语法。

![image](img/pen.gif)

与对象一样，当使用数组字面量符号创建数组时，不会调用 `Array` 构造函数（版本 3 之前的 Firefox 除外）。

要获取和设置数组值，您可以使用方括号并提供值的从零开始的数值索引，如下：

```javascript
var colors = ["red", "blue", "green"];           //定义一个字符串数组
alert(colors[0]);                                //显示第一项
colors[2] = "black";                             //更改第三项
colors[3] = "brown";                             //添加第四项
```



方括号内提供的索引表示正在被访问的值。如果索引小于数组中的元素数量，则它将返回存储在对应项中的值，例如在本例中`colors[0]`显示 "red"。设置值的方式相同，它会替换指定位置的值。如果将值设置到一个超出数组末尾的索引，例如在本例中的`colors[3]`，则数组长度会自动扩展为该索引加 1（因此在本例中长度变为 4，因为所使用的索引是 3）。

数组中的元素数量存储在`length`属性中，它始终返回 0 或更多，如下例所示：

```javascript
var colors = ["red", "blue", "green"];    //创建一个包含三个字符串的数组
var names = [];                           //创建一个空数组

alert(colors.length);    //3
alert(names.length);     //0
```

`length`的一个特性是它不是只读的。通过设置`length`属性，可以轻松地从数组中删除项或向末尾添加项。考虑这个示例：

![image](img/logo1.gif)

```javascript
var colors = ["red", "blue", "green"];    //创建一个包含三个字符串的数组
colors.length = 2;
alert(colors[2]);        //undefined
```

### ArrayFilterExample03.htm

在这里，数组`colors`初始有三个值。将长度设置为 2 会删除最后一项（位置 2），使其不再能通过`colors[2]`访问。如果将长度设置为大于数组中元素数量的数字，则每个新项都将用`undefined`值填充，例如例所示：

![image](img/logo1.gif)

```javascript
var colors = ["red", "blue", "green"];    //创建一个包含三个字符串的数组
colors.length = 4;
alert(colors[3]);        //undefined
```

### ArrayFilterExample04.htm

这段代码将`colors`数组的长度设置为 4，尽管它只包含三个项。数组中不存在位置 3，因此尝试访问其值将导致返回特殊值`undefined`。

`length`属性在向数组末尾添加项时也很有帮助，例如例所示：

```javascript
var colors = ["red", "blue", "green"];    //创建一个包含三个字符串的数组
colors[colors.length] = "black";          //添加一个颜色（位置 3）
colors[colors.length] = "brown";          //添加另一个颜色（位置 4）
```

### ArrayFilterExample05.htm

数组中的最后一项始终位于位置`length - 1`，因此下一个可用的空位位于位置`length`。每当在数组最后一项之后添加项时，`length`属性会自动更新以反映变化。这意味着`colors[colors.length]`在此例的第二行将值赋值给位置 3，在最后一行赋值给位置 4。当项被放置在当前数组大小之外的位置时，新长度会自动计算，这是通过在该位置加 1 完成的，如例所示：

```javascript
var colors = ["red", "blue", "green"];    //创建一个包含三个字符串的数组
colors[99] = "black";                     //添加一个颜色（位置 99）
alert(colors.length); //100
```

### ArrayFilterExample6.htm

在此代码中，`colors`数组在位置 99 插入了一个值，导致长度为 100（99+1）。位置 3 到 98 的项实际上不存在，因此访问时返回`undefined`。

![image](img/pen.gif)

数组最多可以包含 4,294,967,295 个项，对于几乎所有的编程需求都足够了。如果你尝试创建一个超过该数量的数组，将会发生异常。尝试接近此最大值会导致脚本错误。

### 检测数组

自 ECMAScript 3 定义以来，经典问题之一是真正判断一个给定对象是否为数组。在处理单个网页（因此是全局作用域）时，`instanceof`运算符效果良好：

```javascript
if (value instanceof Array){
    //对数组进行操作
}
```

`instanceof`的一个问题是它假设了唯一的执行上下文。如果你在网页中处理多个帧，你实际上在处理两个不同的全局执行上下文，因此有两个版本的`Array`构造函数。如果你将数组从一个帧传递到第二个帧，该数组的构造函数不同在第二个帧原生创建的。

为了解决这个问题，ECMAScript 5 引入了`Array.isArray()`方法。该方法的目的是无论在哪个执行上下文中创建，都能确定判断给定值是否为数组。用法示例：

```javascript
if (Array.isArray(value)){
    //对数组进行操作
}
```

Internet Explorer 9+、Firefox 4+、Safari 5+、Opera 10.5+ 和 Chrome 都已实现`Array.isArray()`。对于尚未实现此方法的器的确定性数组检测，请参见第 22 章“安全类型检测”部分。

### 转换方法

如之前所述，所有对象都有`toLocaleString()`、`toString()`和`valueOf()`方法。在数组上调用时，`toString()`和`valueOf()`返回相同的值。结果是一个逗号分隔的字符串，包含数组中每个值的字符串等价物，也就是说每个项都调用了其`toString()`方法来创建最终字符串。看这个示例：

```javascript
var colors = ["red", "blue", "green"];    //创建一个包含三个字符串的数组

alert(colors.toString());    //red,blue,green
alert(colors.valueOf());     //red,blue,green
alert(colors);               //red,blue,green
```

ArrayFilterExample07.htm

在这段代码中，首先显式地调用`toString()`和`valueOf()`方法来返回数组的字符串表示，该表示会将字符串组合，并用逗号分隔。最后一行将数组直接传递给`alert()`。由于`alert()`期望接收一个字符串，它会在后台调用`toString()`，从而获得与直接调用`toString()`相同的结果。

`toLocaleString()`方法返回的值可能与`toString()`和`valueOf()`相同，但并不总是如此。当在数组上调用`toLocaleString()`时，它会创建一个由逗号分隔的数组值字符串。它与其他两种方法的唯一区别在于`toLocaleString()`调用的是每个项的`toLocaleString()`而不是`toString()`来获取其字符串值。考虑以下示例：

![image](img/logo1.gif)

```javascript
var person1 = {
    toLocaleString : function () {
        return "Nikolaos";
    },
    toString : function() {
        return "Nicholas";
    }
};

var person2 = {
    toLocaleString : function () {
        return "Grigorios";
    },
    toString : function() {
        return "Greg";
    }
};

var people = [person1, person2];
alert(people);                      //Nicholas,Greg
alert(people.toString());           //Nicholas,Greg
alert(people.toLocaleString());     //Nikolaos,Grigorios
```

ArrayTypeExample08.htm

在这里，定义了两个对象`person1`和`person2`。每个对象都定义了`toString()`方法和`toLocaleString()`方法，它们返回不同的值。创建了一个数组`people`来包含这两个对象。当传递给`alert()`时，输出是 "Nicholas,Greg"，因为数组中的每个项都调用了`toString()`方法（与下一行显式调用`toString()`相同）。当在数组上调用`toLocaleString()`时，结果是 "Nikolaos,Grigorios"，因为这会对每个数组项调用`toLocaleString()`方法。

继承的方法`toLocaleString()`、`toString()`和`valueOf()`分别将数组项作为用逗号分隔的字符串返回。可以使用`join()`方法构造一个具有不同分隔符的字符串。`join()`方法接受一个参数，即要使用的字符串分隔符，并返回一个包含所有项的字符串。考虑这个示例：

```javascript
var colors = ["red", "green", "blue"];
alert(colors.join(","));      //red,green,blue
alert(colors.join("||"));     //red||green||blue
```

ArrayTypeJoinExample01.htm

在这里，在`colors`数组上使用`join()`方法来复制`toString()`的输出。通过传递一个逗号，结果是一个用逗号分隔的值列表。在最后一行，传递了双竖线，导致生成字符串 "red||green||blue"。如果没有向`join()`方法传递任何值或`undefined`，则将将使用逗号作为分隔符。Internet Explorer 7 及更早版本错误地使用字符串 "undefined" 作为分隔符。

![image](img/pen.gif)

如果数组中的项为`null`或`undefined`，则在`join()`、`toLocaleString()`、`toString()`和`valueOf()`的结果中它们将由空字符串表示。

# 栈方法 (Stack Methods)

ECMAScript 数组的有趣之处之一是它们提供了一种方法，让数组的行为像其他数据结构。数组对象可以像栈一样工作，栈是限制项插入和删除的数据结构组之一。栈被称为“后进先出”（LIFO）结构，这意味着最近添加的项是第一个被移除的项。栈中项的插入（称为`push`）和移除（称为`pop`）只发生在一个点：栈顶。ECMAScript 数组专门提供了`push()`和`pop()`方法来允许类似栈的行为。

`push()`方法接受任意数量的参数并将它们添加到数组末尾，返回数组的新长度。相反，`pop()`方法移除数组中的最后一个项，减小数组长度并返回该项。考虑这个示例：

![image](img/logo1.gif)

```javascript
var colors = new Array();                      //创建一个数组
var count = colors.push("red", "green");       //推入两个项
alert(count);  //2

count = colors.push("black");                  //再推入一个项
alert(count);  //3

var item = colors.pop();                       //获取最后一个项
alert(item);   //"black"
alert(colors.length);  //2
```

ArrayTypeExample09.htm

在这段代码中，创建了一个数组用作栈（注意，不需要特殊代码即可使其工作；`push()`和`pop()`是数组上的默认方法）。首先，使用`push()`将两个字符串推入数组末尾，结果存储在变量`count`中（其取值为 2）。然后，再推入另一个值，结果再次存储在`count`中。由于数组中现在有三个项，`push()`返回 3。当调用`pop()`时，它返回数组中的最后一个项，即字符串 "black"。然后数组只剩下两个项。

栈方法也可以与所有其他数组方法结合使用，如下例所示：

![image](img/logo1.gif)

```javascript
var colors = ["red", "blue"];
colors.push("brown");              //添加一个项
colors[3] = "black";               //添加一个项
alert(colors.length);  //4

var item = colors.pop();           //获取最后一个项
alert(item);  //"black"
```

ArrayTypeExample10.htm

在这里，初始化了两个值。通过`push()`添加了第三个值。当调用`pop()`时，它返回最后添加的值 "black"。

# 队列方法 (Queue Methods)

正如栈在 LIFO 数据结构中限制访问一样，队列在先进先出（FIFO）数据结构中限制访问。队列在列表末尾添加项并从前端检索项。`shift()`方法移除数组中的第一个项并返回它，同时减少数组长度。将`shift()`与`push()`使用可以将数组作为队列：

```javascript
var colors = new Array();                      //创建一个数组
var count = colors.push("red", "green");       //推入两个项
alert(count);  //2

count = colors.push("black");                  //再推入一个项
alert(count);  //3

var item = colors.shift();                     //获取第一个项
alert(item);   //"red"
alert(colors.length);  //2
```

ArrayTypeExample11.htm

此示例使用`push()`方法创建三个颜色的数组。高亮行显示使用`shift()`方法获取数组中的第一个项，即 "red"。移除该项后，“green" 移动到第一位置，“black" 移动到第二位置，数组留下了两个项。

ECMAScript 还为数组提供了`unshift()`方法。正如名称所示，`unshift()`是`shift()`的相反：它将任意数量的项添加到数组开头并返回数组的新长度。通过将`unshift()`与`pop()`使用，可以模拟反向的队列，即新值添加到数组开头，从末尾检索值，如下例：

```javascript
var colors = new Array();                      //创建一个数组
var count = colors.unshift("red", "green");    //推入两个项
alert(count);  //2

count = colors.unshift("black");               //再推入一个项
alert(count);  //3

var item = colors.pop();                       //获取第一个项
alert(item);   //"green"
alert(colors.length);  //2
```

ArrayTypeExample12.htm

在这段代码中，创建了一个数组并使用`unshift()`进行填充。首先将 "red" 和 "green" 添加到数组中，然后添加 "black"，导致顺序为 "black", "red", "green"。当调用`pop()`时，它移除最后一个项 "green" 并将其返回。

![image](img/pen.gif)

Internet Explorer 7 及更早版本在执行`unshift()`时，总是返回`undefined`，而不是数组的新长度。Internet Explorer 8 在不处于兼容模式时可以正确返回长度。

## 排序方法

有两种方法可以直接处理对数组中已有项的重新排序：`reverse()`和`sort()`。正如预期的那样，`reverse()`方法简单地反转数组中项的顺序。请看这段代码：

![image](img/logo1.gif)

```javascript
var values = [1, 2, 3, 4, 5];
values.reverse();
alert(values);       //5,4,3,2,1
```



`ArrayTypeExample13.htm`

在这里，数组的值最初被设置为 1, 2, 3, 4 和 5。在数组上调用`reverse()`会将顺序反转为 5, 4, 3, 2, 1。这个方法非常直接，但没有提供太大的活性，这正是`sort()`方法派用用场。

默认情况下，`sort()`方法将项按升序排列——最小的值在前，最大的值在后。为了做到这一点，`sort()`方法会对每个项调用`String()`强制转换函数，然后比较字符串以确定正确的顺序。即使数组中的所有项都是数字，如此示例所示：

```
var values = [0, 1, 5, 10, 15];

values.sort();

alert(values);    //0,1,10,15,5
```

`ArrayTypeExample14.htm`

尽管这个示例中的值最初按正确的数字顺序排列，但`sort()`方法会根据它们的字符串等价值改变该顺序。因此，即使 5 小于 10，在进行字符串比较时，字符串 "10" 排在 "5" 之前，所以数组会相应更新。显然，这在很多情况下并不是最优解决方案，因此`sort()`方法允许传递一个比较函数，指示哪个值应该排在哪个值之前。

比较函数接受两个参数，如果第一个参数应该在第二个参数之前，则返回负数；如果参数相等，则返回零；如果第一个参数应该在第二个参数之后，则返回正数。这是一个简单的比较函数的示例：

![image](img/logo1.gif)

```
function compare(value1, value2) {

    if (value1 < value2) {

        return -1;

    } else if (value1 > value2) {

        return 1;

    } else {

        return 0;

    }

}
```

`ArrayTypeExample15.htm`

此比较函数适用于大多数数据类型，并可以通过将其作为参数传递给`sort()`方法来使用，如下例：

```
var values = [0, 1, 5, 10, 15];

values.sort(compare);

alert(values);    //0,1,5,10,15
```

当将比较函数传递给`sort()`方法时，数字将保持正确的顺序。当然，如果你只是像这样交换返回值，比较函数也可以产生降序的结果：

```javascript
function compare(value1, value2) {

    if (value1 < value2) {

        return 1;

    } else if (value1 > value2) {

        return -1;

    } else {

        return 0;

    }

}

var values = [0, 1, 5, 10, 15];

values.sort(compare);

alert(values);    //15,10,5,1,0
```

`ArrayTypeExample16.htm`

在这个修改后的示例中，如果第一个值应该在第二个值之后，则返回 1，如果第一个值应该在第二个值之前，则返回 -1。交换这些意味着较大的值将在前，数组将按降序排序。当然，如果你只想反转数组中项的顺序，`reverse()`是比排序快多的替代方案。

![image](img/pen.gif)

`reverse()`和`sort()`都返回它们所应用的数组的引用。

更简单的比较函数可以用于数值类型，以及`valueOf()`方法返回数值的对象（例如`Date`对象）。在任何情况下，你都可以像这里所示，从第一个值中减去第二个值：

```
function compare(value1, value2){

    return value2 - value1;

}
```

由于比较函数通过返回小于零、零或大于零的数字来工作，因此减法操作恰当地处理了所有情况。

## 操作方法

有多种方法可以处理数组中包含的项。例如，`concat()`方法允许根据当前数组中的所有项创建一个新数组。该方法首先创建一个数组的副本，然后将方法参数附加到末尾并返回新构建的数组。当没有传递参数时，`concat()`只是克隆数组并返回它。如果传递了一个或多个数组，`concat()`将这些数组中的每个项附加到结果的末尾。如果值不是数组，它们将被简单附加到结果数组的末尾。考虑这个示例：

![image](img/logo1.gif)

```
var colors = ["red", "green", "blue"];

var colors2 = colors.concat("yellow", ["black"]);

alert(colors);     //red,green,blue

alert(colors2);    //red,green,blue,yellow,black
```

`ArrayTypeConcat01.htm`

在这里，`colors`数组包含三个值。`concat()`方法在`colors`上调用，传入了 "yellow" 和数组 ["black"]。结果`colors2`包含 "red", "green", "blue", "yellow", "black"。

### 替换 (Replacement)

如果你指定了三个参数，可以在删除项目的同时在特定位置插入项目：起始位置、要删除的项目数量，以及要插入的任意数量的项目。插入的项目数量不需要与删除的项目数量匹配。例如，`splice(2, 1, "red", "green")`会删除位置 2 处的一个项目，然后在位置 2 处向数组插入字符串`"red"`和`"green"`。

`splice()`方法始终返回一个数组，其中包含从数组中删除的任何项目（如果没有删除任何项目，则返回一个空数组）。下面的代码演示了这三种用例：

![image](img/logo1.gif)

```
var colors = ["red", "green", "blue"];

var removed = colors.splice(0,1);                  //删除第一个项目

alert(colors);     //green,blue

alert(removed);    //red - 包含一个元素的数组

removed = colors.splice(1, 0, "yellow", "orange"); //在位置 1 插入两个项目

alert(colors);     //green,yellow,orange,blue

alert(removed);    //空数组

removed = colors.splice(1, 1, "red", "purple");    //插入两个值，删除一个

alert(colors);     //green,red,purple,orange,blue

alert(removed);    //yellow - 包含一个元素的数组
```

`ArrayTypeSpliceExample01.htm`

此示例从包含三个项目的`colors`数组开始。当第一次调用`splice`时，它仅删除了第一个项目，使`colors`剩下项目`"green"`和`"blue"`。第二次调用`splice()`时，它在位置 1 处插入两个项目，导致`colors`包含`"green"`、`"yellow"`、`"orange"`和`"blue"`。此时没有项目被删除，因此返回空数组。最后一次调用`splice()`时，它从位置 1 开始删除一个项目，并插入`"red"`和`"purple"`。在执行完这些代码后，`colors`数组包含`"green"`、`"red"`、`"purple"`、`"orange"`和`"blue"`。

### 位置方法 (Location Methods)

ECMAScript 5 为数组实例增加了两个项目位置方法：`indexOf()`和`lastIndexOf()`。这两个方法每个都接受两个参数：要查找的项目以及从何开始查找的可选索引。`indexOf()`方法从数组的开头（项目 0）开始搜索并持续到末尾，而`lastIndexOf()`则从数组的最后一个项目开始并持续向前。

这些方法分别返回项目在数组中的位置，如果项目不在数组中，则返回`-1`。在将第一个参数与数组中的每个项目比较时，使用的是恒等比较，这意味着项目之间必须严格相等，就像使用`===`进行比较一样。以下是这种用法的一些示例：

```
var numbers = [1,2,3,4,5,4,3,2,1];

alert(numbers.indexOf(4));        //3

alert(numbers.lastIndexOf(4));    //5

alert(numbers.indexOf(4, 4));     //5

alert(numbers.lastIndexOf(4, 4)); //3

var person = { name: "Nicholas" };

var people = [{ name: "Nicholas" }];

var morePeople = [person];

alert(people.indexOf(person));     //-1

alert(morePeople.indexOf(person)); //0
```

`ArrayIndexOfExample01.htm`

`indexOf()`和`lastIndexOf()`方法使得在数组内部定位特定项目变得简单，并且支持 Internet Explorer 9+、Firefox 2+、Safari 3+、Opera 9.5+ 以及 Chrome。

### 迭代方法 (Iterative Methods)

ECMAScript 5 为数组定义了五种迭代方法。每个方法都接受两个参数：一个在每个项目上运行的函数，以及一个运行该函数的可选作用域对象（影响`this`的值）。传递给这些方法之一的函数将接收三个参数：数组项目值、项目在数组中的位置以及数组对象本身。根据方法的具体类型，该函数的执行结果可能会也可能不影响方法的返回值。迭代方法如下：

*   `every()`：在数组的每个项目上运行给定的函数，如果该函数对每个项目都返回`true`，则返回`true`。
*   `filter()`：在数组的每个项目上运行给定的函数，并返回一个包含所有函数返回`true`的项目的数组。
*   `forEach()`：在数组的每个项目上运行给定的函数。该方法没有返回值。
*   `map()`：在数组的每个项目上运行给定的函数，并将每个函数调用的结果返回一个数组。
*   `some()`：在数组的每个项目上运行给定的函数，如果该函数对任意一个项目返回`true`，则返回`true`。

这些方法不会改变数组中包含的值。

在这些方法中，最相似的是`every()`和`some()`，它们都用于查询数组中符合某些标准的项目。对于`every()`，传递的函数必须对每个项目都返回`true`，该方法才会返回`true`；否则它返回`false`。另一方面，`some()`方法即使只有一个项目导致传递的函数返回`true`，它也会返回`true`。

![image](img/logo1.gif)

```
var numbers = [1,2,3,4,5,4,3,2,1];

var everyResult = numbers.every(function(item, index, array){

    return item > 2;

});

alert(everyResult);       false

var someResult = numbers.some(function(item, index, array){

    return item > 2;

});

alert(someResult);       true
```

`ArrayEverySome01.htm`

此代码调用了`every()`和`some()`，并传入了一个判断项目是否大于 2 的函数。对于`every()`，结果为 false，因为只有部分项目符合条件。对于`some()`，结果为 true，因为至少有一个项目大于 2。

下一个方法是`filter()`，它使用给定的函数确定项目是否应该包含在数组中。例如，为了返回大于 2 的数字数组，可以使用以下代码：

![image](img/logo1.gif)

```
var numbers = [1,2,3,4,5,4,3,2,1];

var filterResult = numbers.filter(function(item, index, array){

    return item > 2;

});

alert(filterResult);   [3,4,5,4,3]
```

`ArrayFilterExample01.htm`

`map()`方法也返回一个数组。数组中的每个项目都是原始项目运行函数的结果。例如，你可以将数组中的每个数字乘以二，并返回这些结果的数组：

```
var numbers = [1,2,3,4,5,4,3,2,1];

var mapResult = numbers.map(function(item, index, array){

    return item * 2;

});

alert(mapResult);   [2,4,6,8,10,8,6,4,2]
```

`ArrayMapExample01.htm`

最后一个方法是`forEach()`，它简单地在数组的每个项目上运行给定的函数。它没有返回值，本质等同于使用 for 循环遍历数组。这是一个示例：

```
var numbers = [1,2,3,4,5,4,3,2,1];

numbers.forEach(function(item, index, array){

    //在此处执行某些操作

});
```

### 归约方法 (Reduction Methods)

ECMAScript 5 还增加了两个归约方法：`reduce()`和`reduceRight()`。这两个方法都会遍历数组中的所有项目并构建出一个最终返回的值。`reduce()`方法从第一个项目开始向最后一个项目执行此操作，而`reduceRight()`则从最后一个项目开始向第一个项目执行。

两种方法都接受两个参数：一个在每个项上调用的函数，以及一个可选的作为减少的基础初始值。传递给`reduce()`或`reduceRight()`的函数接受四个参数：上一个值、当前值、项的索引以及数组对象。函数返回的任何值将自动作为下一个项目的第一个参数传递。第一次迭代发生在数组的第二个项上，因此第一个参数是数组中的第一个项，第二个参数是数组中的第二个项。

你可以使用`reduce()`方法执行诸如计算数组中所有数字和的操作。这里有一个示例：

![image](img/logo1.gif)

```
var values = [1,2,3,4,5];

var sum = values.reduce(function(prev, cur, index, array){

    return prev + cur;

});

alert(sum); //15
```

`ArrayReductionExample01.htm`

第一次执行回调函数时，`prev`是 1，`cur`是 2。第二次，`prev`是 3（1 加 2 的结果），`cur`是 3（数组中的第三个项）。该序列持续持续，直到所有项都被访问并返回结果。

`reduceRight()`方法的工作方式相同，只是方向相反。考虑以下示例：

```
var values = [1,2,3,4,5];

var sum = values.reduceRight(function(prev, cur, index, array){

    return prev + cur;

});

alert(sum); //15
```

在这一版本的代码中，第一次执行回调函数时，`prev`是 5，`cur`是 4。当然，结果是相同的，因为操作是简单的加法。

使用`reduce()`还是`reduceRight()`的决定完全取决于数组项应该被访问的方向。在其他所有方面，它们是完全相等的。

这些减少方法支持 Internet Explorer 9+、Firefox 3+、Safari 4+、Opera 10.5 和 Chrome。

# DATE 类型 (日期类型)

ECMAScript`Date`类型基于 Java 早期版本的`java.util.Date`。因此，`Date`类型将日期存储为自 UTC 1970 年 1 月 1 日午夜（通用时间代码）为止的毫秒数。使用这种数据存储格式，`Date`类型可以准确表示 1970 年 1 月 1 日之前或之后 285,616 年的日期。

要创建一个日期对象，使用`new`运算符结合`Date`构造函数，如下：

![image](img/logo1.gif)

```
var now = new Date();
```



# DateTypeExample01.htm

当不使用任何参数调用`Date`构造函数时，创建的对象将被分配当前的日期和时间。要根据另一个日期或时间创建日期，你必须传入日期的毫秒表示（自 UTC 1970 年 1 月 1 日午夜后的毫秒数）。为了辅助这一过程，ECMAScript 提供了两个方法：`Date.parse()`和`Date.UTC()`。

`Date.parse()`方法接受一个表示日期的字符串参数。它尝试将字符串转换为日期的毫秒表示。ECMA-262 第五版定义了`Date.parse()`应该支持的日期格式，填补了第三版留下的空白。所有实现现在必须支持以下日期格式：

- 月/日/年（例如 6/13/2004）
- 月份 日，年（例如 January 12, 2004）
- 星期 月份 日 年 时:分:秒 时区（例如 Tue May 25 2004 00:00:00 GMT-0700）
- ISO 8601 扩展格式 YYYY-MM-DDTHH:mm:ss.sssZ（例如 2004-05-25T00:00:00）。这仅在符合 ECMAScript 5 的实现中有效。

例如，为 2004 年 5 月 25 日创建一个日期对象，你可以使用以下代码：

```javascript
var someDate = new Date(Date.parse("May 25, 2004"));
```

# DateTypeExample01.htm

如果传递给`Date.parse()`的字符串不是日期，则它返回`NaN`。如果直接传递字符串，`Date`构造将在后台调用`Date.parse()`，这意味着下面的代码与之前的示例相同：

```javascript
var someDate = new Date("May 25, 2004");
```

此代码产生的结果与之前的示例相同。

![image](img/pen.gif)

关于`Date`类型及其在各种浏览器中的实现有很多怪癖。它倾向于将超出范围的值替换为当前值以产生输出，因此当尝试解析 "January 32, 2007" 时，某些浏览器将其解释为 "February 1, 2007"，而 Opera 则倾向于插入当前月份的今天，返回 "January current_day, 2007"。这意味着在 9 月 21 日运行代码将返回 "January 21, 2007"。

`Date.UTC()`方法也返回日期的毫秒表示。`Date.UTC()`的参数是年、月、日、时、分、秒、毫秒。月份是从 0 开始的（0 代表 1 月，11 代表 12 月）。日期是从 1 开始的。以下是`Date.UTC()`的示例：

![image](img/logo1.gif)

```javascript
//UTC 2000 年 1 月 1 日午夜
var y2k = new Date(Date.UTC(2000, 0));

//UTC 2005 年 5 月 5 日 17:55:55 555 毫秒
var allFives = new Date(Date.UTC(2005, 4, 5, 17, 55, 55));
```

# DateTypeUTC01.htm

此代码创建了与之前示例相同的两个日期，但这次这两个日期是在系统设置的本地区域。第一个日期是 UTC 2000 年 1 月 1 日午夜，第二个日期是 UTC 2005 年 5 月 5 日 17:55:55。

与其他引用类型一样，`Date`类型也重写了`toLocaleString()`、`toString()`和`valueOf()`，但与之前的类型不同，每个方法返回的内容各不相同。`Date`类型的`toLocaleString()`方法返回适用于浏览器运行地区域语言格式的日期和时间。这通常意味着格式中包含时间的`AM`或`PM`，并且不包含任何时区信息（具体格式随浏览器而异）。`toString()`方法通常返回带有时区信息的日期和时间，且时间通常以 24 小时制表示（小时范围从 0 到 23）。以下列表显示了各种浏览器在“en-US”语言区域下表示 2007 年 2 月 1 日午夜 PST（太平洋标准时间）日期/时间时，对`toLocaleString()`和`toString()`使用的格式：

### Internet Explorer 8

- `toLocaleString()` – Thursday, February 01, 2007 12:00:00 AM
- `toString()` – Thu Feb 1 00:00:00 PST 2007

### Firefox 3.5

- `toLocaleString()` – Thursday, February 01, 2007 12:00:00 AM
- `toString()` – Thu Feb 01 2007 00:00:00 GMT-0800 (Pacific Standard Time)

### Safari 4

- `toLocaleString()` – Thursday, February 01, 2007 00:00:00
- `toString()` – Thu Feb 01 2007 00:00:00 GMT-0800 (Pacific Standard Time)

### Chrome 4

- `toLocaleString()` – Thu Feb 01 2007 00:00:00 GMT-0800 (Pacific Standard Time)
- `toString()` – Thu Feb 01 2007 00:00:00 GMT-0800 (Pacific Standard Time)

### Opera 10

- `toLocaleString()` – 2/1/2007 12:00:00 AM
- `toString()` – Thu, 01 Feb 2007 00:00:00 GMT-0800

如你所见，浏览器为每个方法返回的格式之间存在某些显著差异。这些差异意味着`toLocaleString()`和`toString()`实际上仅用于调试，而不用于显示。

`Date`类型的`valueOf()`方法完全不返回字符串，因为它被重写为返回日期的毫秒表示，以便运算符（如小于号和大于号）能够对日期值正常工作。考虑这个示例：

![image](img/logo1.gif)

```javascript
var date1 = new Date(2007, 0, 1);          //"January 1, 2007"
var date2 = new Date(2007, 1, 1);          //"February 1, 2007"

alert(date1 < date2);  //true
alert(date1 > date2);  //false
```

`DateTypeValueOfExample01.htm`

2007 年 1 月 1 日在 2007 年 2 月 1 日之前，因此说前者小于后者是合理的。因为 2007 年 1 月 1 日的毫秒表示小于 2007 年 2 月 1 日的毫秒表示，所以当比较日期时，小于运算符返回`true`，这为确定日期顺序提供了一种简单的方法。

## 日期格式化方法

有几个`Date`类型方法专门用于将日期格式化为字符串。它们如下：

- `toDateString()` — 以特定于实现的格式显示日期的星期、月份、日期和年份。
- `toTimeString()` — 以特定于实现的格式显示日期的小时、分钟、秒和时区。
- `toLocaleDateString()` — 以特定于实现和区域的格式显示日期的星期、月份、日期和年份。
- `toLocaleTimeString()` — 以特定于实现的格式显示日期的小时、分钟和秒。
- `toUTCString()` — 以特定实现的格式显示完整的 UTC 日期。

这些方法的输出与`toLocaleString()`和`toString()`一样，不同浏览器之间差异巨大，因此不能在用户界面中用于一致的日期显示。

![image](img/pen.gif)

还有一个名为`toGMTString()`的方法，它等同于`toUTCString()`并为了向后兼容而提供。然而，规范建议新代码专门使用`toUTCString()`。

## 日期/时间组件方法

`Date`类型的其余方法（列在下表）直接处理获取和设置日期值的特定部分。注意，对 UTC 日期的引用是指在不考虑时区偏移的情况下解释的日期值（转换为 GMT 时的日期）。

| METHOD | DESCRIPTION |
| --- | --- |
| `getTime()` | 返回日期的毫秒表示；与`valueOf()`相同。 |
| `setTime(milliseconds)` | 设置日期的毫秒表示，从而改变整个日期。 |
| `getFullYear()` | 返回四位年份（2007 而不仅仅是 07）。 |
| `getUTCFullYear()` | 返回 UTC 日期的四位年份。 |
| `setFullYear(year)` | 设置四位年份。如果年份在 0-99 之间则进行调整。 |
| `getUTCMonth()` | 返回 UTC 日期的月份（0-11）。 |
| `setUTCMonth(month)` | 设置 UTC 日期的月份。如果超出范围将调整日期。 |
| `getDate()` | 返回日期的几（1-31）。 |
| `getUTCDate()` | 返回 UTC 日期的几（1-31）。 |
| `setDate(day)` | 设置日期的几。如果超出范围将调整月份和年份。 |
| `getUTCDay()` | 返回 UTC 日期的星期（0-6）。 |
| `setUTCDay(day)` | 设置 UTC 日期的星期并更改日期。 |
| `getHours()` | 返回日期的小时（0-23）。 |
| `getUTCHours()` | 返回 UTC 日期的小时（0-23）。 |
| `setHours(hours)` | 设置日期的小时。如果超出范围将调整日期。 |
| `getMinutes()` | 返回日期的分钟（0-59）。 |
| `getUTCMinutes()` | 返回 UTC 日期的分钟（0-59）。 |
| `setMinutes(minutes)` | 设置日期的分钟。如果超出范围将调整小时。 |
| `getSeconds()` | 返回日期的秒（0-59）。 |
| `getUTCSeconds()` | 返回 UTC 日期的秒（0-59）。 |
| `setSeconds(seconds)` | 设置日期的秒。如果超出范围将调整分钟。 |
| `getMilliseconds()` | 返回日期的毫秒（0-999）。 |
| `getUTCMilliseconds()` | 返回 UTC 日期的毫秒（0-999）。 |
| `setMilliseconds(ms)` | 设置日期的毫秒。如果超出范围将调整秒。 |

## RegExp 类型

ECMAScript 通过`RegExp`类型支持正则表达式。可以使用类似于 Perl 的语法轻松地创建正则表达式，如下：

```javascript
var expression = /pattern/flags;
```

表达式的模式部分可以是任何简单或复杂的正则表达式，包括字符类、量化符、分组、正向断言和反向引用。每个表达式可以有零或多个标志，用于指示表达式的行为。支持的三个标志表示匹配模式，如下：

- `g` — 表示全局模式，意味着模式将应用于整个字符串，而不是在找到第一个匹配项后停止。
- `i` — 表示不区分大小写模式，意味着在确定匹配时会忽略模式和字符串的大小写。
- `m` — 表示多行模式，意味着模式在到达一行文本的末尾后将继续寻找匹配项。

正则表达式是通过模式和这些标志的组合来创建的，以产生不同的结果，如下例所示：

```javascript
/*
 * 匹配字符串中所有的 "at" 实例。
 */
var pattern1 = /at/g;

/*
 * 匹配第一个 "bat" 或 "cat"，不区分大小写。
 */
var pattern2 = /\[bc]at/i;

/*
 * 匹配所有以 "at" 结尾的三字符组合，不区分大小写。
 */
var pattern3 = /.at/gi;
```

与其他语言中的正则表达式一样，所有的元字符在作为模式的一部分使用时都必须进行转义。元字符如下：

```text
( [ { \ ^ $ | ) ] } ? * + .
```

每个元字符在正则表达式语法中都有一个或多个用途，因此当你想要匹配字符串中的该字符时，必须使用反斜杠进行转义。以下是一些示例：

```javascript
/*
 * 匹配第一个 "bat" 或 "cat"，不区分大小写。
 */
var pattern1 = /[bc]at/i;

/*
 * 匹配第一个 "[bc]at"，不区分大小写。
 */
var pattern2 = /\[bc]at/i;

/*
 * 匹配所有以 "at" 结尾的三字符组合，不区分大小写。
 */
var pattern3 = /.at/gi;

/*
 * 匹配所有的 ".at" 实例，不区分大小写。
 */
var pattern4 = /\.at/gi;
```

在这段代码中，`pattern1`匹配所有的 "bat" 或 "cat" 实例，不区分大小写。要直接匹配"[bc]at"，两个方括号都需要用反斜杠进行转义，如`pattern2`所示。在`pattern3`中，点表示任何字符都可以出现在 "at" 之前形成匹配。如果你想匹配".at"，那么点需要被转义，如`pattern4`所示。

前面的示例都是使用字面量形式（literal form）定义正则表达式。正则表达式也可以通过`RegExp`构造函数创建，它接受两个参数：一个用于匹配的模式字符串和一个可选的标志字符串。任何可以使用字面量语法定义的正则表达式都可以使用构造函数定义，如下例所示：

```javascript
/*
 * 匹配第一个 "bat" 或 "cat"，不区分大小写。
 */
var pattern1 = /[bc]at/i;

/*
 * 与 pattern1 相同，只是使用了构造函数。
 */
var pattern2 = new RegExp("[bc]at", "i");
```

在这里，`pattern1`和`pattern2`定义了等效的正则表达式。注意`RegExp`构造函数的两个参数都是字符串（不应将正则表达式字面量传递给`RegExp`构造函数）。由于`RegExp`构造函数的模式参数是字符串，在某些情况下你需要对字符进行双重转义。所有的元字符都必须双重转义，已经转义的字符也是如此，例如`\n`（` `字符，它在字符串中通常被转义为`\\`，当在正则表达式字符串中使用时会变为`\\\\`）。下面的表格显示了一些字面量形式的模式以及使用`RegExp`构造函数时所需的等效字符串。

| LITERAL PATTERN | STRING EQUIVALENT |
| --- | --- |
| `/\[bc\]at/` | `"\\\[bc\\]at"` |
| `/\.at/` | `"\\.at"` |
| `/name\/age/` | `"name\\/age"` |
| `/\d.\d{1,2}/` | `"\\d.\\d{1,2}"` |
| `/\w\\hello\\123/` | `"\\w\\\\hello\\\\123"` |

记住，使用字面量创建正则表达式与使用`RegExp`构造函数创建正则表达式并不完全相同。在 ECMAScript 3 中，正则表达式字面量始终共享同一个`RegExp`实例，而通过构造函数创建新的`RegExp`则总是产生一个新实例。考虑以下代码：

```javascript
var re = null,
    i;

for (i=0; i < 10; i++){
    re = /cat/g;
    re.test("catastrophe");
}

for (i=0; i < 10; i++){
    re = new RegExp("cat", "g");
    re.test("catastrophe");
}
```

在第一个循环中，只有一个`/cat/`的`RegExp`实例，尽管在循环体内指定了它。实例属性（在下一节介绍）不会重置，因此调用`test()`在循环每隔一次就会失败一次。这是因为在第一次调用`test()`时找到了 "cat"，但第二次调用从索引 3（上一次匹配的结束位置）开始搜索，找不到它。由于找到了字符串末尾，随后的`test()`调用将从头开始。

第二个循环使用`RegExp`构造函数在每次循环中都创建正则表达式。每次调用`test()`都返回`true`，因为每次迭代都创建了一个新的`RegExp`实例。

### RegExp Instance Properties

每个`RegExp`实例都有以下属性，允许你获取有关模式的信息：

- `global`: 一个布尔值，表示是否设置了`g`标志。
- `ignoreCase`: 一个布尔值，表示是否设置了`i`标志。
- `lastIndex`: 一个整数，表示源中下次尝试匹配的字符位置。该值初始始终为 0。
- `multiline`: 一个布尔值，表示是否设置了`m`标志。
- `source`: 正则表达式的字符串源。它始终以字面量形式返回（不带开头和斜杠），而不是传入构造函数的字符串。

这些属性对于识别正则表达式的某些方面很有帮助；但它们通常没有太大用，因为这些信息在模式声明中已经可用。这里有一个例子：

```javascript
var pattern1 = /\[bc]at/i;

alert(pattern1.global);     //false
alert(pattern1.ignoreCase); //true
alert(pattern1.multiline);  //false
alert(pattern1.lastIndex);  //0
```



`alert(pattern1.source);     //"[bc]at"`

`var pattern2 = new RegExp("\[bc]at", "i");`

`alert(pattern2.global);     //false`

`alert(pattern2.ignoreCase); //true`

`alert(pattern2.multiline); //false`

`alert(pattern2.lastIndex);  //0`

`alert(pattern2.source);     //"[bc]at"`

### RegExp Instance Methods

`RegExp` 对象的主要方法是 `exec()`，它旨在配合捕获组使用。该方法接受一个参数，应用于模式的字符串，并返回关于第一个匹配项的信息数组，如果没有找到匹配项则返回 `null`。返回的数组虽然是 `Array` 的实例，但包含两个额外的属性：`index`（模式匹配在字符串中的位置）和 `input`（运行表达式的字符串）。在数组中，第一项是匹配整个模式的字符串。任何额外的项表示表达式内部的捕获组（如果模式中没有捕获组，则数组只有一个项）。

```javascript
var text = "mom and dad and baby";

var pattern = /mom( and dad( and baby)?)?/gi;

var matches = pattern.exec(text);

alert(matches.index);    //0

alert(matches.input);    //"mom and dad and baby"

alert(matches[0]);       //"mom and dad and baby"

alert(matches[1]);       //" and dad and baby"

alert(matches[2]);       //" and baby"
```

#### RegExpExecExample01.htm

在这个示例中，`pattern` 有两个捕获组。最内层的一个组匹配 `" and baby"`，其包含的组匹配 `" and dad"` 或 `" and dad and baby"`。当在字符串上调用 `exec()` 时，找到了匹配项。由于整个字符串都匹配 `pattern`，因此 `matches` 数组上的 `index` 属性被设置为 `0`。数组中的第一个项是整个匹配字符串，第二个项包含第一个捕获组的内容，第三项包含第二个捕获组的内容（注：原文此处为第三个捕获组，实则为第二个）。

即使 `pattern` 是全局的，`exec()` 方法也一次返回关于一次匹配的信息。当未指定全局标志时，多次对同一字符串调用 `exec()` 将始终返回关于第一次匹配的信息。当 `pattern` 上设置了 `g` 标志时，每次调用 `exec()` 都会向字符串深处移动以寻找匹配项，例如例所示：

```javascript
var text = "cat, bat, sat, fat";        

var pattern1 = /.at/;

var matches = pattern1.exec(text);        

alert(matches.index);        //0

alert(matches[0]);           //cat

alert(pattern1.lastIndex);   //0

matches = pattern1.exec(text);        

alert(matches.index);        //0

alert(matches[0]);           //cat

alert(pattern1.lastIndex);   //0

var pattern2 = /.at/g;

var matches = pattern2.exec(text);        

alert(matches.index);        //0

alert(matches[0]);           //cat

alert(pattern2.lastIndex);   //0

matches = pattern2.exec(text);        

alert(matches.index);        //5

alert(matches[0]);           //bat

alert(pattern2.lastIndex);   //8
```

#### RegExpExecExample02.htm

此示例中的第一个模式 `pattern1` 不是全局的，因此每次调用 `exec()` 只返回第一个匹配项（`"cat"`）。第二个模式 `pattern2` 是全局的，因此每次调用 `exec()` 都会返回字符串中的下一个匹配项，直到到达字符串结束。还要注意 `pattern` 的 `lastIndex` 属性是如何受到影响的。在全局匹配模式下，`lastIndex` 在每次调用 `exec()` 后都会增加，但在非全局模式下保持不变。

![image](img/pen.gif)

Internet Explorer 对 JavaScript 的实现差异导致 `lastIndex` 总是被更新，即使在非全局模式下也是如此。

正则表达式的另一种方法是 `test()`，它接受一个字符串参数，并如果 `pattern` 匹配该参数则返回 `true`，否则返回 `false`。当你只想知道模式是否被匹配但不需要实际的匹配文本时，此方法非常有用。`test()` 方法经常用于 `if` 语句中，例如：

```javascript
var text = "000-00-0000";        

var pattern = /\d{3}-\d{2}-\d{4}/;

if (pattern.test(text)) {

    console.log("match found");

}
```

在示例中，`text` 为 `"000-00-0000"`，`pattern` 为 `/\d{3}-\d{2}-\d{4}/`。`test()` 方法返回 `true`，因为模式匹配了字符串。

#### RegExpConstructorPropertiesExample03.htm

在此示例中，创建了一个带有两个匹配组的模式并对其对字符串进行测试。尽管 `test()` 仅返回一个布尔值，但 `$1` 和 `$2` 属性会在 `RegExp` 构造函数被填充。

### 模式局限性

尽管 ECMAScript 对正则表达式的支持已经非常完善，但它确实缺乏 Perl 等语言中提供的一些高级正则表达式功能。以下功能在 ECMAScript 正则表达式中不受支持（更多信息请参阅 [www.regular-expressions.info](http://www.regular-expressions.info)）：

- `\A` 和 `\Z` 锚（分别匹配字符串的开始或结束）
- 后行断言（Lookbehinds）
- 并集和交集类（Union and intersection classes）
- 原子分组（Atomic grouping）
- Unicode 支持（除一次匹配单个字符外）
- 命名捕获组（Named capturing groups）
- `s`（单行）和 `x`（自由空格）匹配模式
- 条件语句（Conditionals）
- 正则表达式注释

尽管有这些限制，ECMAScript 的正则表达式支持已经强大到足以处理大多数模式匹配任务。

### 函数类型

ECMAScript 最有趣的部分之一是它的函数，主要因为函数实际上是对象。每个函数都是 `Function` 类型的实例，像任何其他引用类型一样拥有属性和方法。由于函数是对象，函数名仅仅是指向函数对象的指针，并不一定与函数本身绑定。函数通常使用函数声明语法定义，如下例所示：

```javascript
function sum (num1, num2) {

    return num1 + num2;

}
```

这与使用函数表达式几乎完全等价，如下：

```javascript
var sum = function(num1, num2){

    return num1 + num2;

};
```

在这段代码中，定义了一个变量 `sum` 并将其初始化为函数。注意，在 `function` 关键字之后没有包含名称，因为这不是需要的——函数可以通过变量 `sum` 来引用。同时注意，函数结束之后有一个分号，就像任何变量初始化之后都会有一个分号一样。

定义函数的最后一种方法是通过 `Function` 构造函数，它可以接受任意数量的参数。最后一个参数始终被视为函数体，而之前的参数则列举了新函数的参数。参考此示例：

```javascript
var sum = new Function("num1", "num2", "return num1 + num2");   //不推荐
```

这种语法是不被推荐的，因为它导致了代码的双重解释（一次针对普通的 ECMAScript 代码，另一次针对传入构造函数的字符串），从而会影响性能。然而，将函数视为对象、将函数名视为指针是非常重要的——这种语法非常很好地体现了这一概念。

由于函数名仅仅是指向函数的指针，它们的行为就像任何其他包含对象指针的变量一样。这意味着一个特定的函数可以有多个名称，如下例所示：

![image](img/logo1.gif)

```javascript
function sum(num1, num2){

    return num1 + num2;

}        

alert(sum(10,10));    //20

var anotherSum = sum;        

alert(anotherSum(10,10));  //20

sum = null;        

alert(anotherSum(10,10));  //20
```

#### FunctionTypeExample01.htm

这段代码定义了一个名为 `sum()` 的函数，用于将两个数字相加。声明了一个变量 `anotherSum` 并将其赋值为 `sum`。注意，在不带括号的情况下使用函数名访问的是函数指针而不是执行函数。此时，`anotherSum` 和 `sum` 都指向同一个函数，这意味着 `anotherSum()` 可以被调用并返回结果。当 `sum` 被置为 `null` 时，它断开了与函数之间的关系，尽管 `anotherSum()` 仍然可以没有任何问题地被调用。

### 不支持重载（重温）

将函数名视为指针也解释了为什么 ECMAScript 中不能有函数重载。回想第 3 章中的以下示例：

```javascript
function addSomeNumber(num){

    return num + 100;

}

function addSomeNumber(num) {

    return num + 200;

}

var result = addSomeNumber(100);    //300
```

在这个示例中，显而易见，声明两个同名的函数会导致最后一个函数覆盖之前的函数。这段代码与以下内容几乎完全等价：

```javascript
var addSomeNumber = function (num){

    return num + 100;

};

addSomeNumber = function (num) {

    return num + 200;

};

var result = addSomeNumber(100);    //300
```

在经过重写后的代码中，更容易看到到底发生了什么。当创建第二个函数时，变量 `addSomeNumber` 仅仅被覆盖了。

### 函数声明与函数表达式

在整个范围内，函数声明和函数表达式被认为是几乎等价的。这种说法是因为 JavaScript 引擎将数据加载到执行上下文的方式有一个主要区别。函数声明在任何代码执行之前就会读取并存在于执行文中，而函数表达式在执行到达该行代码之前是不完全的。考虑以下内容：

![image](img/logo1.gif)

```javascript
alert(sum(10,10));

function sum(num1, num2){

    return num1 + num2;

}
```

#### FunctionDeclarationExample01.htm

这段代码运行完美，因为函数声明通过被称为提升的过程在代码运行之前被读取并添加到执行上下文中。在评估代码时，JavaScript 引擎会先对函数声明进行扫描并将其移动到顶部。因此，即使函数声明出现在源代码的使用位置之后，引擎也会将其提升到顶部。将函数声明更改为等效的函数表达式（如下例），在执行期间会导致错误：

![image](img/logo1.gif)

```javascript
alert(sum(10,10));

var sum = function(num1, num2){

    return num1 + num2;

};
```

#### FunctionInitializationExample01.htm

更新后的代码会导致错误，因为函数是初始化语句的一部分，而不是函数声明的一部分。这意味着在执行高亮行之前，变量 `sum` 是不可用的，因为第一行会导致“意外标识符”错误。

除了函数名称可用时间的差异外，这两种语法是等价的。

![image](img/pen.gif)

存在像声明一样的命名函数表达式，例如 `var sum = function sum()`。更多讨论请参见第 7 章。

### 作为的值

由于 ECMAScript 中的函数名仅仅是变量，因此函数可以在任何其他值可以使用的地方使用。这意味着不仅可以将函数作为参数传递给另一个函数，还可以将函数作为另一个函数的返回值。考虑以下函数：

```javascript
function callSomeFunction(someFunction, someArgument){

    return someFunction(someArgument);

}
```

该函数接受两个参数。第一个参数应该是一个函数，第二个参数应该是传递给该函数的值。随后任何函数都可以如下所示传入：

```javascript
function add10(num){

    return num + 10;

}

var result1 = callSomeFunction(add10, 10);

alert(result1);   //20

function getGreeting(name){

    return "Hello, " + name;

}

var result2 = callSomeFunction(getGreeting, "Nicholas");

alert(result2);   //"Hello, Nicholas"
```

#### FunctionAsAnArgumentExample01.htm

`callSomeFunction()` 函数是泛型的，因此传入作为第一个参数的函数并不重要——结果将始终从被执行的第一个参数返回。请记住，要访问函数指针而不是执行函数，必须省略括号，因此变量 `add10` 和 `getGreeting` 被传递给 `callSomeFunction()`，而不是将它们的结果传递进去。

从函数中返回另一个函数也是可能的并且非常有用。例如，假设有一个对象数组并想要根据任意属性对数组进行排序。数组的 `sort()` 方法接受两个参数，即要比较的值，但实际上你需要一种方法指示根据哪个属性进行排序。这个问题可以通过定义一个基于属性名称的比较函数来解决，如下所示：

![image](img/logo1.gif)

```javascript
function createComparisonFunction(propertyName) {

    return function(object1, object2){

        var value1 = object1[propertyName];

        var value2 = object2[propertyName];

        if (value1 < value2){

            return -1;

        } else if (value1 > value2){

            return 1;

        } else {

            return 0;

        }

    };

}
```

#### ReturningFunctionExample01.htm

这种函数的语法看起来很复杂，但本质上它只是一个位于 `return` 操作符内部的函数。`propertyName` 参数可以从内部函数访问，并使用括号表示获取给定属性的值。一旦获取了属性值，就可以进行简单的比较。该函数可以如下例所示：

```javascript
var data = [{name: "Zachary", age: 28}, {name: "Nicholas", age: 29}];

data.sort(createComparisonFunction("name"));

alert(data[0].name); // Nicholas

data.sort(createComparisonFunction("age"));

alert(data[0].name); // Zachary
```



在此代码中，创建了一个名为`data`的数组，包含两个对象。每个对象都有一个`name`属性和一个`age`属性。在默认情况下，`sort()`方法会调用每个对象的`toString()`来确定顺序，在这种情况下不会产生逻辑结果。调用`createComparisonFunction("name")`会创建一个基于`name`属性排序的比较函数，这意味着第一个项将名为"Nicholas"，年龄为29。当调用`createComparisonFunction("age")`时，它创建一个基于`age`属性排序的比较函数，这意味着第一个项将名为"Zachary"，年龄为28。

## Internals

函数内部有两个特殊对象：`arguments`和`this`。`arguments`对象（在第3章讨论过）是一个类似于数组的对象，包含了传递函数的所有参数。尽管它的主要用途是表示函数参数，但`arguments`对象还有一个名为`callee`的属性，它是指向拥有该函数的指针。考虑以下经典的factorial函数：

```javascript
function factorial(num){
    if (num <= 1) {
        return 1;
    } else {
        return factorial(num-1)
    }
}
```

`factorial`函数通常定义为递归，例如所示，当函数名设置时它可以正常工作。然而，此函数的正确执行与函数名`"factorial"`密耦合。可以使用`arguments.callee`将其解耦：

![image](img/logo1.gif)

```javascript
function factorial(num){
    if (num <= 1) {
        return 1;
    } else {
        return arguments.callee(num-1)
    }
}
```

`FunctionTypeArgumentsExample01.htm`

在重写版本的`factorial()`函数中，函数体内不再有对`"factorial"`的引用，这确保了无论如何引用函数，递归调用都会发生在正确的函数上。考虑以下：

```javascript
var trueFactorial = factorial;
factorial = function(){
    return 0;
};
alert(trueFactorial(5)); //120
alert(factorial(5)); //0
```

在这里，变量`trueFactorial`被赋值`factorial`的值，有效地将函数指针存储在第二个位置。`factorial`变量随后被赋值为一个简单返回0的函数。如果没有在原始`factorial()`函数体中使用`arguments.callee`，对`trueFactorial()`的调用将返回0。然而，通过与函数名解耦，`trueFactorial()`正确计算阶乘，而`factorial()`是唯一返回0的函数。

另一个特殊对象是`this`，它的类似于Java和C#中的`this`对象，尽管并不完全相同。它是函数正在操作的上下文对象的引用——当在网页的全局作用范围内调用函数时，`this`对象指向`window`。考虑以下：

![image](img/logo1.gif)

```javascript
window.color = "red";
var o = { color: "blue" };
function sayColor(){
    alert(this.color);
}
sayColor();     //"red"
o.sayColor = sayColor;
o.sayColor();   //"blue"
```

`FunctionTypeThisExample01.htm`

`sayColor()`函数定义在全局但引用了`this`对象。`this`的值在函数被调用时才确定，因此它的值在整个代码中可能是不一致。当在全局范围内调用`sayColor()`时，输出"red"，因为`this`指向`window`，这意味着`this.color`对应`window.color`。通过将函数赋值给对象`o`然后调用`o.sayColor()`，`this`指向`o`，因此`this.color`对应`o.color`并显示"blue"。

![image](img/pen.gif)

记住函数名只是包含指针的变量，因此即使在不同的上下文中执行，全局的`sayColor()`和`o.sayColor()`也指向同一个函数。

ECMAScript 5在函数对象上正式化了一个额外的属性：`caller`。虽然在ECMAScript 3中没有定义，但除了早期版本的Opera外，所有浏览器都支持此属性，它包含调用此函数的引用，如果函数是从全局作用范围调用的，则为`null`。例如：

```javascript
function outer(){
    inner();
}
function inner(){
    alert(inner.caller);
}
outer();
```

`FunctionTypeArgumentsExample01.htm`

因为`outer()`调用了`inner()`，所以`inner.caller`指回`outer()`。为了更松的耦合，你也可以通过`arguments.callee.caller`访问相同的信息：

![image](img/logo1.gif)

```javascript
function outer(){
    inner();
}
function inner(){
    alert(arguments.callee.caller);
}
outer();
```

`FunctionTypeArgumentsExample02.htm`

`caller`属性在Internet Explorer、Firefox、Chrome、Safari以及Opera 9.6的所有中都支持。在严格模式下，访问`arguments.callee`会导致错误。ECMAScript 5还定义了`arguments.caller`，它在严格模式下也会导致错误，并且在严格模式之外始终为`undefined`。这是为了消除`arguments.caller`与函数的`caller`属性之间的混淆。这些更改是作为语言的安全增强而做的，以便第三方代码无法检查相同上下文中运行的其他代码。

```javascript
function sayName(name){
    alert(name);
}      
function sum(num1, num2){
    return num1 + num2;
}
function sayHi(){
    alert("hi");
}
alert(sayName.length);  //1
alert(sum.length);      //2
alert(sayHi.length);    //0
```

`FunctionTypeLengthPropertyExample01.htm`

这段代码定义了三个函数，每个都有不同数量的命名参数。`sayName()`函数指定了一个参数，因此它的`length`属性被设置为1。同样，`sum()`指定两个参数，所以它的`length`属性为2，而`sayHi()`没有命名参数，所以它的`length`为0。

`prototype`属性可能是ECMAScript核心中最有趣的部分。`prototype`是引用类型所有实例方法的实际所在位置，这意味着像`toString()`和`valueOf()`等方法实际上存在于`prototype`上，然后通过对象实例进行访问。该属性在定义你自己的引用类型和继承时非常重要。（这些主题将在第6章中介绍。）在ECMAScript 5中，`prototype`属性是不可枚举的，因此无法通过`for-in`找到。

函数有两个额外的方法：`apply()`和`call()`。这两个方法都会用特定的`this`值调用函数，从而有效地设置函数体内部`this`对象的值。`apply()`方法接受两个参数：函数内部的`this`值和一个参数数组。第二个参数可以是`Array`的实例，但也可以是`arguments`对象。考虑以下内容：

![image](img/logo1.gif)

```javascript
function sum(num1, num2){
    return num1 + num2;
}
function callSum1(num1, num2){
    return sum.apply(this, arguments);    //传入arguments对象
}
function callSum2(num1, num2){
    return sum.apply(this, [num1, num2]); //传入数组
}
alert(callSum1(10,10));   //20
alert(callSum2(10,10));   //20
```

`FunctionTypeApplyMethodExample01.htm`

在这个示例中，`callSum1()`执行了`sum()`方法，将`this`作为`this`值传入（因为是在全局作用范围内调用的，所以等于`window`），同时也传入了`arguments`对象。`callSum2()`方法也调用了`sum()`，但它传入的是参数数组。两个函数都会执行并返回正确的结果。

![image](img/pen.gif)

在严格模式下，不带上下文对象调用的函数`this`值不会被强制转换为`window`。相反，除非通过显式地将函数绑定到对象或使用`apply()`或`call()`，否则它将变为`undefined`。

`call()`方法的行为与`apply()`相同，但传递参数的方式不同。第一个参数是`this`值，但剩余参数直接传递给函数。使用`call()`参数时必须具体地列出，如示例所示：

![image](img/logo1.gif)

```javascript
function sum(num1, num2){
    return num1 + num2;
}
function callSum(num1, num2){
    return sum.call(this, num1, num2);
}
alert(callSum(10,10));   //20
```

`FunctionTypeCallMethodExample01.htm`

使用`call()`方法，`callSum()`必须显式地传递它的每一个参数。结果与使用`apply()`相同。选择`apply()`还是`call()`的决定完全取决于你向函数传递参数最简单的方法。如果你打算直接传入`arguments`对象，或者你已经有一个要传递的数据数组，那么`apply()`是更好的选择；否则，`call()`可能是更合适的选择。（如果没有参数要传递，这些方法是等价的。）

`apply()`和`call()`的真正威力不在于它们传递参数的能力，而在于它们增强函数内部`this`值的能力。考虑以下示例：

```javascript
window.color = "red";
var o = { color: "blue" };
function sayColor(){
    alert(this.color);
}
sayColor();            //red
sayColor.call(this);   //red
sayColor.call(window); //red
sayColor.call(o);      //blue
```

`FunctionTypeCallExample01.htm`

这个示例是用于说明`this`对象的修改版本。再次，`sayColor()`被定义为全局函数，当在全局作用范围内调用它时，它显示"red"，因为`this.color`求值为`window.color`。你可以通过使用`sayColor.call(this)`和`sayColor.call(window)`在全局范围内显式调用该函数，它们都会显示"red"。运行`sayColor.call(o)`会切换函数的上下文，使得`this`指向`o`，导致显示"blue"。

使用`call()`（或`apply()`）增强作用域的好处是对象不需要知道关于方法的任何信息。在这个示例的第一个版本中，`sayColor()`在调用之前直接放在对象上；在更新后的示例中，这一步不再需要。

ECMAScript 5定义了一个名为`bind()`的额外方法。`bind()`方法创建一个新的函数实例，其`this`值绑定到传入的值上。例如：

![image](img/logo1.gif)

```javascript
window.color = "red";
var o = { color: "blue" };
function sayColor(){
    alert(this.color);
}
var boundColor = sayColor.bind(o);
boundColor(); //blue
```

`FunctionTypeBindMethodExample01.htm`

在这里，通过传入对象`o`从`sayColor()`创建了一个新函数`boundColor`。调用它得到"blue"。

## 原始包装类型

三种特殊的引用类型旨在简化原始值的交互：`Boolean`类型、`Number`类型和`String`类型。这些类型可以像本章描述的其他引用类型一样工作，但它们与其原始类型等价值的特殊行为。每当读取原始值时，后台都会创建一个对应的原始包装类型对象，允许访问任意的方法。考虑以下示例：

```javascript
var s1 = "some text";
var s2 = s1.substring(2);
```

这种行为允许原始字符串值像对象一样工作。对于布尔值和数值，也会分别使用`Boolean`和`Number`类型重复这相同的三个步骤。

引用类型与原始包装类型之间的主要区别在于对象的生命周期。当你使用`new`运算符实例化引用类型时，它将一直留在内存中，直到超出作用域；而自动创建的原始包装对象只存在一行代码就会被销毁。这意味着不能在运行时添加属性和方法。例如所示：

```javascript
var s1 = "some text";
s1.color = "red";
alert(s1.color);   //undefined
```

在这里，第二行尝试给字符串`s1`添加一个`color`属性。然而，当在第三行访问`s1`时，`color`属性已经消失。这是因为在第二行中创建的`String`对象在执行到第三行时已经被销毁。第三行创建了它自己的`String`对象，该对象没有`color`属性。

可以使用`Boolean`、`Number`和`String`构造函数显式地创建原始包装对象。这应该只在绝对必要时这样做，因为这通常会让开发者感到困惑，不知道他们处理的是原始值还是引用值。对原始包装类型的实例调用`typeof`会返回`"object"`，并且所有的原始包装对象都会转换为布尔值`true`。

`Object`构造函数也充当工厂方法，并能够根据传入构造函数的数值类型返回原始包装的实例。例如：

```javascript
var obj = new Object("some text");
alert(obj instanceof String);   //true
```

当将字符串传递给`Object`构造函数时，会创建一个`String`实例；数字参数会产生一个`Number`实例，而`Boolean`参数则返回一个`Boolean`实例。

请记住，使用`new`调用原始包装构造函数与调用同名的转换函数是不一样的。例如：

```javascript
var value = "25";
var number = Number(value);   //casting function
alert(typeof number);   //"number"
var obj = new Number(value);    //constructor
alert(typeof obj);              //"object"
```

在这个示例中，变量`number`被填充为原始数字值`25`，而变量`obj`被填充为`Number`的实例。更多关于转换函数的信息，请参阅第3章。

尽管不建议显式创建原始包装对象，但它们的功能对于操作原始值非常重要。每个原始包装类型都有让数据操作变得更容易的方法。

## Boolean类型 (Boolean Type)

`Boolean`类型是对应布尔值的引用类型。要创建一个`Boolean`对象，请使用`Boolean`构造函数并传入`true`或`false`，如下例：

```javascript
var booleanObject = new Boolean(true);
```



`Boolean` 实例重写了`valueOf()`方法以返回`true`或`false`的原始值。`toString()`方法也被重写为在调用时返回`"true"`或`"false"`字符串。遗憾的是，`Boolean`对象在 ECMAScript 中不仅用得很少，而且实际上可能非常令人困惑。问题通常发生在尝试在布尔表达式中使用布尔对象时，例如所示：

![image](img/logo1.gif)

```javascript
var falseObject = new Boolean(false);

var result = falseObject && true;

alert(result);  //true

var falseValue = false;

result = falseValue && true;

alert(result);  //false
```

`BooleanTypeExample01.htm`

在这段代码中，创建了一个值为`false`的布尔对象。该对象随后与原始值`true`进行 AND 逻辑运算。在布尔数学中，`false` AND `true`等于`false`。但在这行代码中，被求的是名为`falseObject`的对象，而不是它的值（`false`）。正如之前讨论的，所有对象在布尔表达式中都会自动转换为`true`，因此`falseObject`在表达式中实际上被赋予了`true`。然后，`true` AND `true`等于`true`。

原始 Boolean 类型和引用 Boolean 类型之间还有其他区别。`typeof`运算符对原始类型返回`"boolean"`，对引用类型返回`"object"`。此外，`Boolean`对象是`Boolean`类型的实例，在使用`instanceof`运算符时会返回`true`，而原始值则返回`false`，如下所示：

```javascript
alert(typeof falseObject);   //object

alert(typeof falseValue);    //boolean

alert(falseObject instanceof Boolean);  //true

alert(falseValue instanceof Boolean);   //false
```

理解原始 Boolean 值与 Boolean 对象之间的区别非常重要——建议永远不要使用后者。

## Number 类型（Number Type）

Number 类型是数值的引用类型。要创建一个`Number`对象，请使用`Number`构造函数并传入任何数字。这是一个示例：

![image](img/logo1.gif)

```javascript
var numberObject = new Number(10);
```

`NumberTypeExample01.htm`

与 Boolean 类型一样，`Number`类型重写了`valueOf()`、`toLocaleString()`和`toString()`。`valueOf()`方法返回对象所代表的原始数值，而另外两个方法将数字作为字符串返回。正如第 3 章中提到的，`toString()`方法可选地接受一个参数，指示表示数字的进制，如下所示：

```javascript
var num = 10;

alert(num.toString());       //"10"

alert(num.toString(2));      //"10"

alert(num.toString(8));      //"12"

alert(num.toString(10));     //"10"

alert(num.toString(16));     //"a"
```

`NumberTypeExample01.htm`

除了继承的方法外，`Number`类型还有几个用于将数字格式化为字符串的额外方法。

### `toFixed()`方法

`toFixed()`方法返回一个具有指定小数位数的数字字符串表示，如下所示：

```javascript
var num = 10;

alert(num.toFixed(2)); // "10.00"
```

`NumberTypeExample01.htm`

在这里，`toFixed()`方法被赋予了参数`2`，指示显示多少小数。作为结果，该方法返回字符串`"10.00"`，用零填充空位数。如果数字超过指定的位数，结果将舍入到最近的位数，如下所示：

```javascript
var num = 10.005;

alert(num.toFixed(2)); // "10.01"
```

`toFixed()`的舍入特性对于处理货币的应用可能有用，但需要注意的是，该方法的舍入在不同浏览器之间存在差异。Internet Explorer 8 版本在向`toFixed()`传递零时会错误地舍入范围在`{(-0.94,−0.5], 0.5,0.94)}`内的数字。在这些情况下，Internet Explorer 返回 0，而应该返回`-1`或`1`（取决于符号）；其他浏览器的行为符合预期，Internet Explorer 9 修复了这个问题。

![image](img/logo1.gif)

`toFixed()`方法可以表示具有 0 到 20 位小数的数字。某些浏览器支持更大的范围，但这是典型的范围。

### `toExponential()`方法

另一个与格式化数字的方法是`toExponential()`方法，它返回以指数法（也称为 e 表示法）格式化的数字字符串。与`toFixed()`类似，`toExponential()`接受一个参数，即输出的小数位数。考虑这个示例：

```javascript
var num = 10;

alert(num.toExponential(1)); // "1.0e+1"
```

这段代码输出的结果为`"1.0e+1"`。通常，这个较小的数字不会使用指数法表示。如果你希望获得数字合适的形式，应该使用`toPrecision()`方法。

`toPrecision()`方法返回数字的固定计数法表示或指数计数法表示，取决于哪种方式更为合理。该方法接受一个参数，即表示该数字时使用的总位数（不包括指数）。这里是一个示例：

![image](img/logo1.gif)

```javascript
var num = 99;

alert(num.toPrecision(1)); // "1e+2"

alert(num.toPrecision(2)); // "99"

alert(num.toPrecision(3)); // "99.0"
```

`NumberTypeExample01.htm`

在这个示例中，第一个任务是用单个数字表示数字 99，结果为`"1e+2"`，即数字 100。由于 99 无法仅用一个数字准确表示，该方法将其四舍五入到 100，而 100 只需要一个数字即可表示。用两个数字表示 99 得到`"99"`，三个数字则返回`"99.0"`。`toPrecision()`方法本质上根据你正在处理的数值来决定调用`toFixed()`还是`toExponential()`；这三种方法都会进行四舍五入或向上取整，以正确的位数准确表示数字。

![image](img/pen.gif)

`toPrecision()`方法可以表示带有 1 到 21 位小数的数字。某些浏览器可能支持更大的范围，但这是典型的实现的范围。

与`Boolean`对象类似，`Number`对象为数值提供了重要功能，但由于存在相同的潜在问题，真的不应该直接实例化。如以下示例所示，`typeof`和`instanceof`运算符在处理原始类型数字与引用数字时的工作方式不同：

```javascript
var numberObject = new Number(10);

var numberValue = 10;

alert(typeof numberObject);   //"object"

alert(typeof numberValue);    //"number"

alert(numberObject instanceof Number);  //true

alert(numberValue instanceof Number);   //false
```

对原始类型数字调用`typeof`时，始终返回`"number"`，而`Number`对象则返回`"object"`。同样，一个`Number`对象是`Number`的实例，但原始类型数字不是。

## String 类型

`String`类型是字符串的对象的表示，使用`String`构造函数创建如下：

![image](img/logo1.gif)

```javascript
var stringObject = new String("hello world");
```

`StringTypeExample01.htm`

`String`对象的方法在所有字符串原始类型上都可用。所有三个继承的方法——`valueOf()`、`toLocaleString()`和`toString()`——都返回对象的原始字符串值。

每个`String`实例都包含一个属性`length`，它指示字符串中的字符数。考虑以下示例：

```javascript
var stringValue = "hello world";

alert(stringValue.length); // "11"
```

此示例输出`"11"`，即`"hello world"`中的字符数。请注意，即使字符串包含双字节字符（与仅使用一个字节的 ASCII 字符相比），每个字符仍被计为一个。

`String`类型有大量方法，用于在 ECMAScript 中对字符串进行分解和操作。

### 字符方法

有两个方法可以访问字符串中的特定字符：`charAt()`和`charCodeAt()`。这些方法各接受一个参数，即字符从 0 开始计算的位置。`charAt()`方法简单返回给定位置上的字符作为单字符字符串。（ECMAScript 中没有字符类型。）例如：

```javascript
var stringValue = "hello world";

alert(stringValue.charAt(1)); // "e"
```

`"hello world"`位置 1 上的字符是`"e"`，因此调用`charAt(1)`返回`"e"`。如果你想要字符的编码而不是实际字符，那么调用`charCodeAt()`是合适的选择，如下例所示：

```javascript
var stringValue = "hello world";

alert(stringValue.charCodeAt(1)); // outputs "101"
```

此示例输出`"101"`，这是小写字母`"e"`的字符编码。

ECMAScript 5 定义了另一种访问单个字符的方法。支持的实现允许使用带有数字索引的括号法来访问字符串中的特定字符，如下例所示：

```javascript
var stringValue = "hello world";

alert(stringValue[1]); // "e"
```

使用括号法访问单个字符在 Internet Explorer 8 以及所有当前版本的 Firefox、Safari、Chrome 和 Opera 中均受支持。如果在 Internet Explorer 7 或更早版本中使用此语法，结果将是`undefined`（而不是特殊值`undefined`）。

### 字符串操作方法

有几个方法可以操作字符串的值。这些方法中的第一个是`concat()`，用于将一个或多个字符串连接到另一个字符串上，并将连接后的字符串作为结果。考虑以下示例：

```javascript
var stringValue = "hello ";

var result = stringValue.concat("world");

alert(result);  // "hello world"

alert(stringValue); // "hello"
```

在此示例中在`stringValue`上调用`concat()`方法的结果是`"hello world"`——`stringValue`的值保持不变。`concat()`方法接受任意数量的参数，因此它可以从任意数量的其他字符串创建一个字符串，如下：

```javascript
var stringValue = "hello ";

var result = stringValue.concat("world", "!");

alert(result);  // "hello world!"

alert(stringValue); // "hello"
```

修改后的示例将`"world"`和`"!"`连接到`"hello "`的末尾。虽然`concat()`方法用于字符串连接，但加法运算符（`+`）使用更多，且在大多数情况下优于`concat()`方法。

## 字符串定位方法

有两种方法用于在另一个字符串中定位子字符串：`indexOf()`和`lastIndexOf()`。这两个方法都会在字符串中搜索指定的子字符串并返回其位置（如果未找到子字符串则返回`-1`）。它们之间的区别在于，`indexOf()`方法从字符串的开头开始查找子字符串，而`lastIndexOf()`方法则从字符串的结尾开始查找。考虑这个示例：

![image](img/logo1.gif)

```javascript
var stringValue = "hello world";

alert(stringValue.indexOf("o")); // 4

alert(stringValue.lastIndexOf("o")); // 7
```

在这里，字符串`"o"`的第一次出现位于位置 4，即`"hello"`中的`"o"`。字符串`"o"`的最后一次出现在单词`"world"`中，位于位置 7。如果字符串中只出现了一次`"o"`，那么`indexOf()`和`lastIndexOf()`返回相同的位置。

每个方法都接受一个可选的第二个参数，用于指定从字符串内部哪个位置开始搜索。这意味着`indexOf()`方法将从该位置开始搜索并向字符串末尾移动，忽略起始位置之前的所有内容；而`lastIndexOf()`则从给定位置开始搜索并继续向字符串开头搜索，忽略给定位置与字符串结尾之间的所有内容。这里有一个示例：

```javascript
var stringValue = "hello world";

alert(stringValue.indexOf("o", 6)); // 7

alert(stringValue.lastIndexOf("o", 6)); // 4
```

当将 6 作为第二个参数传入每个方法时，结果与上一个示例相反。这次，`indexOf()`返回 7，是因为它从位置 6（字母`"w"`）开始搜索字符串，并继续到位置 7，在该处找到了`"o"`。`lastIndexOf()`方法返回 4，是因为搜索从位置 6 开始并向字符串开头回溯搜索，在回处遇到了`"hello"`中的`"o"`。使用这个第二个参数，你可以通过循环调用`indexOf()`或`lastIndexOf()`来定位子字符串的所有实例，如下例所示：

![image](img/logo1.gif)

```javascript
var stringValue = "Lorem ipsum dolor sit amet, consectetur adipisicing elit";

var positions = new Array();

var pos = stringValue.indexOf("e");

while (pos > -1) {
    positions.push(pos);

    pos = stringValue.indexOf("e", pos + 1);
}

alert(positions); // "3,24,32,35,52"
```

`StringTypeLocationMethodsExample02.htm`

这个示例通过不断增加`indexOf()`应开始的位置来遍历字符串。它首先获取字符串中`"e"`的初始位置，然后进入一个循环，不断将上一个位置加 1 传递给`indexOf()`，确保搜索在上一个子字符串实例之后继续。每个位置都存储在`positions`数组中，以便稍后使用。

## `trim()`方法

ECMAScript 5 在所有字符串上引入了`trim()`。`trim()`方法创建一个字符串的副本，移除所有开头和结尾的空格，然后返回结果。例如：

```javascript
var stringValue = "    hello world    ";

var trimmedValue = stringValue.trim();

alert(stringValue); // "    hello world    "

alert(trimmedValue); // "hello world"
```



注意，`trim()`已经在 Internet Explorer 9+、Firefox 3+、Safari 5+ 中实现，Chrome 8+ 也支持非标准的 `trimLeft()` 和 `trimRight()` 方法，它们分别只移除字符串开头或结尾的空格。

## 字符串大小写方法

下一组方法涉及大小转换。有四个方法执行大小转换：`toLowerCase()`、`toLocaleLowerCase()`、`toUpperCase()` 和 `toLocaleUpperCase()`。`toLowerCase()` 和 `toUpperCase()` 是原始方法，模仿了 `java.lang.String` 中的相同方法。`toLocaleLowerCase()` 和 `toLocaleUpperCase()` 方法旨在根据特定的区域（locale）进行实现。在许多区域中，特定区域的方法与通用方法是相同的；但某些语言（如土耳其语）对 Unicode 大写应用了特殊规则，这需要使用特定区域的方法进行正确转换。以下是一些示例：

![image](img/logo1.gif)

```javascript
var stringValue = "hello world";
alert(stringValue.toLocaleUpperCase()); //"HELLO WORLD"
alert(stringValue.toUpperCase());       //"HELLO WORLD"
alert(stringValue.toLocaleLowerCase()); //"hello world"
alert(stringValue.toLowerCase());     //"hello world"
```

`StringTypeCaseMethodExample01.htm`

这段代码对 `toLocaleUpperCase()` 和 `toUpperCase()` 都输出 "HELLO WORLD"，正如 `toLocaleLowerCase()` 和 `toLowerCase()` 都输出 "hello world" 一样。通常情况下，如果你不知道代码将在什么语言环境下运行，使用特定区域的方法更安全。

## 字符串模式匹配方法

`String` 类型有几个设计用于在字符串内进行模式匹配的方法。这些方法中的第一个是 `match()`，它本质上相当于调用 `RegExp` 对象的 `exec()` 方法。`match()` 方法接受一个参数，该参数可以是正则表达式字符串或 `RegExp` 对象。考虑这个示例：

```javascript
var text = "cat, bat, sat, fat";        
var pattern = /.at/;
//same as pattern.exec(text)
var matches = text.match(pattern);
alert(matches.index); //0
alert(matches[0]);    //"cat"
alert(pattern.lastIndex); //0
```

`StringTypePatternMatchingExample01.htm`

`match()` 返回的数组与用字符串调用 `RegExp` 对象的 `exec()` 方法时返回的数组相同：第一个项目是匹配整个模式的字符串，每个其他项目（如果适用）代表表达式中的捕获组。

另一种查找模式的方法是 `search()`。该方法的唯一参数与 `match()` 的参数相同：一个由字符串或 `RegExp` 对象指定的正则表达式。`search()` 方法返回模式在字符串中首次出现的索引，如果未找到，则返回 -1。`search()` 总是从字符串的开头开始查找模式。考虑下面这个示例：

![image](img/logo1.gif)

```javascript
var text = "cat, bat, sat, fat";        
var pos = text.search(/at/);
alert(pos);   //1
```

`StringTypePatternMatchingExample01.htm`

在这里，`search(/at/)` 返回 1，这是 `"at"` 在字符串中的第一个位置。

为了简化子字符串的替换，ECMAScript 提供了 `replace()` 方法。该方法接受两个参数。第一个参数可以是 `RegExp` 对象或字符串（字符串不会转换为正则表达式），第二个参数可以是字符串或函数。如果第一个参数是字符串，则只替换子字符串的第一次出现。替换所有子字符串实例的唯一方法是提供一个指定了全局标志（global flag）的正则表达式，如例所示：

```javascript
var text = "cat, bat, sat, fat";        
var result = text.replace("at", "ond");
alert(result);    //"cond, bat, sat, fat"
result = text.replace(/at/g, "ond");
alert(result);    //"cond, bond, sond, fond"
```

`StringTypePatternMatchingExample01.htm`

在这个示例中，字符串 `"at"` 首先被传递给 `replace()`，替换文本为 `"ond"`。操作的结果是将 `"cat"` 变为 `"cond"`，但字符串的其他部分保持不变。通过将第一个参数更改为带有全局标志的正则表达式，每个 `"at"` 实例都被替换为 `"ond"`。

当第二个参数是字符串时，有几个特殊字符序列可以用于插入正则表达式操作的值。ECMA-262 规定了以下值表。

| 序列 | 替换文本 |
| --- | --- |
| `$$` | `$` |
| `$&` | 匹配整个模式的子字符串。等同于 `RegExp.lastMatch`。 |
| `$'` | 匹配子字符串之前的字符串部分。等同于 `RegExp.rightContext`。 |
| `` $` `` | 匹配子字符串之后的字符串部分。等同于 `RegExp.leftContext`。 |
| `$n` | 第 n 次捕获，其中 n 是值 0−9。例如，`$1` 是第一个捕获，`$2` 是第二个，依此类推。如果没有捕获，则使用空字符串。 |
| `$nn` | 第 nn 次捕获，其中 nn 是值 01−99。例如，`$01` 是第一个捕获，`$02` 是第二个，依此类推。如果没有捕获，则使用空字符串。 |

使用这些特殊序列允许使用关于最后一次匹配的信息进行替换，如本例所示：

![image](img/logo1.gif)

```javascript
var text = "cat, bat, sat, fat";        
result = text.replace(/(.at)/g, "word ($1)");
alert(result);    //word (cat), word (bat), word (sat), word (fat)
```

`StringTypePatternMatchingExample01.htm`

在这里，每个以 `"at"` 结尾的单词都被替换替换为 `"word"`，后面紧跟括号并使用 `$1` 序列替换被替换的内容。

`replace()` 的第二个参数也可以是一个函数。当存在单个匹配时，函数将接收三个参数：匹配的字符串、匹配在字符串中的位置以及整个字符串。当有多个捕获组时，每个匹配的字符串都将作为参数传递，最后两个参数是模式匹配在字符串中的位置以及原始字符串。函数应该返回一个字符串，指示匹配应该被替换为什么。使用函数作为第二个参数允许对替换文本进行更细粒度的控制，如例所示：

```javascript
function htmlEscape(text){
    return text.replace(/[<>"&]/g, function(match, pos, originalText){
        switch(match){
            case "<":
                return "&lt;";
            case ">":
                return "&gt;";
            case "&":
                return "&amp;";
            case "\"":
                return "&quot;";
        }             
    });
}
alert(htmlEscape("<p class=\"greeting\">Hello world!</p>")); 
//"&lt;p class=&quot;greeting&quot;&gt;Hello world!&lt;/p&gt;";
```

`StringTypePatternMatchingExample01.htm`

在这里，定义了函数 `htmlEscape()` 用于对插入 HTML 的四个字符进行转义：小于号、大于号、& 符号和双引号都必须被转义。实现此点的最简单方法是使用正则表达式查找这些字符，然后定义一个函数为每个匹配的字符返回特定的 HTML 实体。

用于处理模式的最后一个字符串方法是 `split()`，它根据分隔符将字符串分割为子字符串数组。分隔符可以是字符串或 `RegExp` 对象。（对于此方法，字符串不被视为正则表达式）。可选的第二个参数——数组限制，确保了返回的数组不会超过某个特定大小。考虑下面这个示例：

![image](img/logo1.gif)

```javascript
var colorText = "red,blue,green,yellow";
var colors1 = colorText.split(","); //["red", "blue", "green", "yellow"]
var colors2 = colorText.split(",", 2); //["red", "blue"]
var colors3 = colorText.split(/,+/); //"]
```

`StringTypePatternMatchingExample01.htm`

在这个示例中，`colorText` 是一个用逗号分隔的颜色字符串。`split(",")` 获取这些颜色，分割字符串。为了将结果限制为两项，指定了第二个参数 2。最后，使用正则表达式，可能会得到空字符串。这是因为由正则表达式指定的分隔符出现在字符串开头（"red"）。

浏览器对 `split()` 方法中正则表达式的支持存在差异。虽然简单模式的行为相同，但未找到匹配的模式以及带有捕获组的模式表现完全不同。一些显著差异如下：

- Internet Explorer 8 及之前的版本忽略捕获组。ECMA-262 指出组应被插入结果数组中。Internet Explorer 9 正确地包含了捕获组。
- Firefox 3.6 及之前的版本在捕获组没有匹配时会在结果中包含空字符串；ECMA-262 规定未匹配的捕获组应表示为 `undefined`。

在正则表达式中使用捕获组时还存在其他细微差异。在使用此类正则表达式时，请确保在多种浏览器中进行彻底测试。

![image](img/pen.gif)

关于 `split()` 和正则表达式中捕获组的跨浏览器问题的讨论，请参见 Steven Levithan 写的“JavaScript split bugs: Fixed!”[`blog.stevenlevithan.com/archives/cross-browser-split`](http://blog.stevenlevithan.com/archives/cross-browser-split)。

### `localeCompare()` 方法

最后一个方法是 `localeCompare()`，它比较一个字符串另一个字符串并返回以下三个值之一：

- 如果字符串在字母顺序上于参数之前，返回一个负数（通常是 -1，但具体数值取决于实现）。
- 如果字符串与参数相等，返回 0。
- 如果字符串在字母顺序上于参数之后，返回一个正数（通常是 1，但再次，这取决于具体的实现）。

这里有一个示例：

![image](img/logo1.gif)

```javascript
var stringValue = "yellow";       
alert(stringValue.localeCompare("brick"));  //1
alert(stringValue.localeCompare("yellow")); //0
alert(stringValue.localeCompare("zoo"));    //-1
```

`StringTypeLocaleCompareExample01.htm`

在此段代码中，字符串 "yellow" 与三个不同的值进行了比较："brick","yellow" 和 "zoo"。由于 "brick" 在字母顺序上于 "yellow" 之前，`localeCompare()` 返回 1；"yellow" 等于 "yellow"，因此该行的 `localeCompare()` 返回 0；"zoo" 在 "yellow" 之后，因此该行的 `localeCompare()` 返回 -1。再次，由于值取决于具体实现，最好像本示例所示使用 `localeCompare()`：

```javascript
function determineOrder(value) {
    var result = stringValue.localeCompare(value);
    if (result < 0){
        alert("The string 'yellow' comes before the string '" + value + "'.");
    } else if (result > 0) {
        alert("The string 'yellow' comes after the string '" + value + "'.");
    } else {
        alert("The string 'yellow' is equal to the string '" + value + "'.");
    }
}
determineOrder("brick");
determineOrder("yellow");
determineOrder("zoo");
```

`StringTypeLocaleCompareExample01.htm`

通过使用这种结构，你可以确保代码在所有实现中都能正常工作。

`localeCompare()` 的独特之处在于，实现所在的区域设置（国家和语言）精确地决定了该方法的运行方式。在美国，英语是 ECMAScript 实现的标准语言，`localeCompare()` 是区分大小写的的，它判定大写字母在字母顺序上位于小写字母之后。然而，在其他区域设置中可能并非如此。

### `fromCharCode()` 方法

`String` 构造函数上有一个方法：`fromCharCode()`。该方法的作用是接收一个或多个字符编码将其转换为字符串。本质上，这是 `charCodeAt()` 实例方法的反向操作。考虑这个示例：

![image](img/logo1.gif)

```javascript
alert(String.fromCharCode(104, 101, 108, 108, 111)); //"hello"
```



`StringTypeFromCharCodeExample01.htm`

在此段代码中，`fromCharCode()` 是对来自单词 "hello" 字母的一系列字符编码进行调用的。

### HTML 方法

浏览器厂商很早就意识到需要使用 JavaScript 动态格式化 HTML。因此，他们扩展了规范，包含了几个专门用于帮助常见 HTML 格式化任务的方法。下表列出了 HTML 方法。但请注意，通常这些方法不会被使用，因为它们倾向于创建非语义化的标记。

| 方法 | 输出 |
| --- | --- |
| `anchor(name)` | `<a name="name">string</a>` |
| `big()` | `<big>string</big>` |
| `bold()` | `<b>string</b>` |
| `fixed()` | `<tt>string</tt>` |
| `fontcolor(color)` | `<font color="color">string</font>` |
| `fontsize(size)` | `<font size="size">string</font>` |
| `italics()` | `<i>string</i>` |
| `link(url)` | `<a href="url">string</a>` |
| `small()` | `<small>string</small>` |
| `strike()` | `<strike>string</strike>` |
| `sub()` | `<sub>string</sub>` |
| `sup()` | `<sup>string</sup>` |

## 单例内置对象

ECMA-262 将内置对象定义为“任何由 ECMAScript 实现提供的、独立依赖于宿主环境的对象，该对象在 ECMAScript 程序执行开始时就已经存在”。这意味着开发者不需要显式地实例化内置对象；它已经被实例化了。你已经学习了大多数内置对象，例如 `Object`、`Array` 和 `String`。ECMA-262 定义了两个单例内置对象：`Global` 和 `Math`。

### Global 对象

`Global` 对象在 ECMAScript 中是最独特的，因为它无法被显式访问。ECMA-262 将 `Global` 对象指定为那些没有其他所有者对象的属性和方法的某种“大纳统”。实际上，不存在所谓的全局变量或全局函数；所有在全局范围内定义的变量和函数都会成为 `Global` 对象的属性。本书早些介绍的函数，如 `isNaN()`、`isFinite()`、`parseInt()` 和 `parseFloat()` 实际上都是 `Global` 对象的方法。除了这些，`Global` 对象上还有其他几个可用方法。

### URI 编码方法

`encodeURI()` 和 `encodeURIComponent()` 方法用于对 URI（统一资源标识符）进行编码以便传递给浏览器。为了有效，URI 不能包含某些字符，例如空格。URI 编码方法对 URI 进行编码，以便浏览器能够接受并理解它们，将所有无效字符替换为特殊的 UTF-8 编码。

`encodeURI()` 方法设计用于处理整个 URI（例如 `www.wrox.com/illegal value.htm`），而 `encodeURIComponent()` 设计仅用于处理 URI 的片段（例如上一个 URI 中的 `illegal value.htm`）。两种方法的主要区别在于，`encodeURI()` 不编码 URI 中的特殊字符（如冒号、斜杠、问号和井号），而 `encodeURIComponent()` 会编码这些字符。考虑这个示例：

![image](img/logo1.gif)

```javascript
var uri = "http://wrox.com/illegal value.htm";

//http://wrox.com/illegal%20value.htm
alert(encodeURI(uri));

//http%3A%2F%2Fwrox.com%2Fillegal%20value.htm
alert(encodeURIComponent(uri));
```

`GlobalObjectURIEncodingExample01.htm`

在此示例中，`encodeURI()` 保留了除了空格替换为 `%20` 以外的所有值。`encodeURIComponent()` 方法替换了所有非标准字符。这就是为什么前者可以用于完整的 URI，而 `encodeURIComponent()` 只能用于附加在 URI 末尾的字符串。

![image](img/pen.gif)

通常情况下，你使用 `encodeURIComponent()` 的频率远高于 `encodeURI()`，因为单独编码查询字符串更为常见。

### 解码方法

`encodeURI()` 和 `encodeURIComponent()` 的对应方法是 `decodeURI()` 和 `decodeURIComponent()`。`decodeURI()` 方法仅解码被 `encodeURI()` 替换的字符。例如，`%20` 被替换为空格，但 `%23` 不会被替换，因为它代表井号 (#)。同样，`decodeURIComponent()` 会解码由 `encodeURIComponent()` 编码的所有字符，本质上它会解码所有特殊值。考虑这个示例：

![image](img/logo1.gif)

```javascript
var uri = "http%3A%2F%2Fwrox.com%2Fillegal%20value.htm%23start";

//http://wrox.com/illegal value.htm#start
alert(decodeURI(uri)); // 此字符串由于 # 的存在不是合法的 URI
```

`GlobalObjectURIDecodingExample01.htm`

在此示例中，使用 `decodeURI()` 仅将 `%20` 替换为空格。`decodeURIComponent()` 则替换所有特殊字符并输出一个没有转义的字符串。

![image](img/pen.gif)

URI 方法 `encodeURI()`、`encodeURIComponent()`、`decodeURI()` 和 `decodeURIComponent()` 替换了在 ECMA-262 第三版中已弃用的 `escape()` 和 `unescape()` 方法。URI 方法总是更好的，因为它们可以编码所有 Unicode 字符，而原始方法只能正确编码 ASCII 字符。在生产代码中避免使用 `escape()` 和 `unescape()`。

### eval() 方法

最后一个可能是整个 ECMAScript 语言中最强大的方法：`eval()` 方法。该方法运行像一个整个 ECMAScript 解释器，并接受一个参数，即要执行的 ECMAScript（或 JavaScript）字符串。这里有一个示例：

```javascript
eval("alert('hi')");
```

这一行在功能上等同于以下代码：

```javascript
alert("hi");
```

当解释器发现 `eval()` 调用时，它会将参数解释为实际的 ECMAScript 语句，然后将其插入相应位置。通过 `eval()` 执行的代码被视为调用发生处执行上下文的一部分，且执行的代码与该上下文具有相同的作用域链。这意味着在包含上下文中定义的变量可以在 `eval()` 调用内部被引用，例如例所示：

```javascript
var msg = "hello world";
eval("alert(msg)");    //"hello world"
```

在这里，变量 `msg` 定义在 `eval()` 用的上下文之外，但对 `alert()` 的调用仍然显示了文本 "hello world"，因为第二行被替换成了一行真实的代码。同样地，你可以在 `eval()` 调用内部定义函数或变量，并在外部代码中引用它们，如下所示：

```javascript
eval("function sayHi() { alert('hi'); }");
sayHi();
```

在这里，`sayHi()` 函数在 `eval()` 调用内部定义。由于该调用被替换为实际的函数，因此可以在下一行调用 `sayHi()`。变量的情况也是一样：

```javascript
eval("var msg = 'hello world';");
alert(msg);  //"hello world"
```

在 `eval()` 内部创建的变量或函数都不会被提升（hoisted），因为它们在代码解析时包含在字符串中。它们只在 `eval()` 执行时才创建。

在严格模式下，`eval()` 内部创建的变量和函数无法从外部访问，因此最后两个示例会导致错误。此外，在严格模式下，为 `eval` 赋值会导致错误：

```javascript
"use strict";
eval = "hi";  //导致错误
```

![image](img/pen.gif)

解释代码字符串的能力非常强大但也非常危险。使用 `eval()` 时要极其小心，尤其是当将用户输入的数据传递进去时。恶意的用户可能会插入破坏你网站或应用程序安全的值。（这被称为代码注入。）

## 全局对象属性

`Global` 对象拥有许多属性，其中一些已经在书中提到过。`undefined`、`NaN` 和 `Infinity` 特殊值都是 `Global` 对象的属性。此外，所有原生引用类型构造函数（如 `Object` 和 `Function`）都是 `Global` 对象的属性。下表列出了所有属性。

| 属性 | 描述 |
| --- | --- |
| `undefined` | 特殊值 `undefined` |
| `NaN` | 特殊值 `NaN` |
| `Infinity` | 特殊值 `Infinity` |
| `Object` | `Object` 的构造函数 |
| `Array` | `Array` 的构造函数 |
| `Function` | `Function` 的构造函数 |
| `Boolean` | `Boolean` 的构造函数 |
| `String` | `String` 的构造函数 |
| `Number` | `Number` 的构造函数 |
| `Date` | `Date` 的构造函数 |
| `RegExp` | `RegExp` 的构造函数 |
| `Error` | `Error` 的构造函数 |
| `EvalError` | `EvalError` 的构造函数 |
| `RangeError` | `RangeError` 的构造函数 |
| `ReferenceError` | `ReferenceError` 的构造函数 |
| `SyntaxError` | `SyntaxError` 的构造函数 |
| `TypeError` | `TypeError` 的构造函数 |
| `URIError` | `URIError` 的构造函数 |

在 ECMAScript 5 中，明确禁止给 `undefined`、`NaN` 和 `Infinity` 赋值。这样做即使在非严格模式下会导致错误。

## Window 对象

尽管 ECMA-262 没有指示直接访问 `Global` 对象的方法，但浏览器对其进行了实现，使得 `window` 是 `Global` 对象的代理。因此，在全局作用域声明的所有变量和函数都成为 `window` 上的属性。考虑这个示例：

![image](img/logo1.gif)

```javascript
var color = "red";
function sayColor(){
    alert(window.color);
}
window.sayColor();  //"red"
```

`GlobalObjectWindowExample01.htm`

在这里定义了一个名为 `color` 的全局变量和一个名为 `sayColor()` 的全局函数。在 `sayColor()` 内部，通过 `window.color` 访问 `color` 变量，证明全局变量已成为 `window` 的属性。然后通过 `window` 对象直接调用函数 `window.sayColor()`，弹出警告框。

![image](img/pen.gif)

`window` 对象在 JavaScript 中的作用远不止实现 ECMAScript 全局对象。`window` 对象和浏览器对象模型（BOM）的细节将在第八章讨论。

获取 `Global` 对象的另一种方法是使用以下代码：

```javascript
var global = function(){
    return this;
}();
```

这段代码创建了一个立即执行的函数表达式，返回 `this` 的值。如前所述，当函数在没有指定式 `this` 值的情况下执行时（无论是作为对象方法还是通过 `call()`/`apply()`），`this` 的值等同于 `Global` 对象。因此，调用一个仅返回 `this` 的函数是在任何执行环境中获取 `Global` 对象的的一种一致方法。

## Math 对象

`Math` 对象包含许多用于执行简单和复杂数学计算的方法。`Math` 对象提供了许多属性。

### Math 对象属性

`Math` 对象有几个由特殊值属性。下表描述了这些属性。

| 属性 | 描述 |
| --- | --- |
| `Math.E` | e 的值 |
| `Math.LN10` | 10 的自然对数 |
| `Math.LN2` | 2 的自然对数 |
| `Math.LOG2E` | 以 2 为底的 e |
| `Math.LOG10E` | 以 10 为底的 e |
| `Math.PI` | π 的值 |
| `Math.SQRT1` | ½ 的平方根 |
| `Math.SQRT2` | 2 的平方根 |

### min() 和 max() 方法

`min()` 和 `max()` 方法确定一组数中的最小值或最大值。这些方法接受任意数量的参数，如下所示：

![image](img/pen.gif)

```javascript
var max = Math.max(3, 54, 32, 16);
alert(max);    //54
var min = Math.min(3, 54, 32, 16);
alert(min);    //3
```

`MathObjectMinMaxExample01.htm`

要找到数组中的最大值或最小值，可以使用 `apply()` 方法：

```javascript
var values = [1, 2, 3, 4, 5, 6, 7, 8];
var max = Math.max.apply(Math, values);
```

这种技术的关键是将 `Math` 对象作为 `apply()` 的第一个参数，以便正确设置 `this` 值。

### 四舍五入方法

下一组方法与将小数四舍五入为整数有关。三种方法——`Math.ceil()`、`Math.floor()` 和 `Math.round()` 以如下方式处理四舍五入：

*   `Math.ceil()` 方法代表上取函数，始终向上取整到最近的整数。
*   `Math.floor()` 方法代表下取函数，始终向下取整到最近的整数。
*   `Math.round()` 方法代表标准的四舍五入函数，如果数字距离下一个整数至少有一半（0.5 或更高），则向上取整，否则向下取整。

```javascript
alert(Math.ceil(25.9));     //26
alert(Math.ceil(25.5));     //26
alert(Math.ceil(25.1));     //26
alert(Math.round(25.9));    //26
alert(Math.round(25.5));    //26
alert(Math.round(25.1));    //25
alert(Math.floor(25.9));    //25
alert(Math.floor(25.5));    //25
alert(Math.floor(25.1));    //25
```

`MathObjectRoundingExample01.htm`对于 25 到 26 之间的所有值（不包含边界），`Math.ceil()` 总是返回 `26`，因为它始终会向上舍入。`Math.round()` 方法仅在数字为 `25.5` 或更大时才返回 `26`；否则返回 `25`。最后，`Math.floor()` 对于 25 到 26 之间的所有数字（不包含边界）均返回 `25`。

### random() 方法

`Math.random()` 方法返回一个 0 到 1 之间的随机数，不包括 0 或 1。这是网站在用户进入时尝试显示随机引言或随机事实的常用工具。你可以使用以下公式通过 `Math.random()` 来选择特定整数范围内的数字：

```javascript
number = Math.floor(Math.random() * total_number_of_choices + first_possible_value)
```

在这里使用 `Math.floor()` 方法是因为 `Math.random()` 总是返回小数，这意味着将其乘以一个数并加上另一个数仍然得到一个小数。因此，如果你想选择一个 1 到 10 之间的数字，代码将如下：

```javascript
var num = Math.floor(Math.random() * 10 + 1);
```

`MathObjectRandomExample01.htm`你看到有 10 个可能的值（1 到 10），第一个可能的值是 `1`。如果你想选择一个 2 到 10 之间的数字，代码将如下：

```javascript
var num = Math.floor(Math.random() * 9 + 2);
```



`MathObjectRandomExample02.htm`从 2 数到 10 只有九个数字，所以选项总数为九个，第一个可能的值是`2`。很多时候，直接使用一个处理总选项数和第一个可能值计算的函数更简单，例如所示：

```javascript
function selectFrom(lowerValue, upperValue) {
    var choices = upperValue - lowerValue + 1;
    return Math.floor(Math.random() * choices + lowerValue);
}

var num = selectFrom(2,10);
alert(num);  // 2 到 10 之间的数字，包含边界
```

`MathObjectRandomExample03.htm`在这里，函数`selectFrom()`接受两个参数：应该返回的最小值和应该返回的最大值。选项的数量通过将这两个值相减并加 1，然后对这些数字应用之前的公式计算得出的。因此，通过调用`selectFrom(2,10)`可以选择一个 2 到 10 之间（包含边界）的数字。使用该函数可以很容易地从数组中选择随机项目，如下：

```javascript
var colors = ["red", "green", "blue", "yellow", "black", "purple", "brown"];
var color = colors[selectFrom(0, colors.length-1)];
```

`MathObjectRandomExample03.htm`在这个示例中，`selectFrom()`的第二个参数是数组的长度减 1，即数组的最后一个位置。

### 其他方法

`Math`对象有许多与各种简单和高级数学运算相关的方法。讨论每个方法的细节或它们可能使用的场景超出了本书的范围，但下表列出了`Math`对象的其余方法。

| 方法 | 描述 |
| --- | --- |
| `Math.abs(num)` | 返回`num`的绝对值 |
| `Math.exp(num)` | 返回`Math.E`的`num`次幂 |
| `Math.log(num)` | 返回`num`的自然对数 |
| `Math.pow(num, power)` | 返回`num`的`power`次方 |
| `Math.sqrt(num)` | 返回`num`的平方根 |
| `Math.acos(x)` | 返回`x`的反余弦 |
| `Math.asin(x)` | 返回`x`的反正弦 |
| `Math.atan(x)` | 返回`x`的反正切 |
| `Math.atan2(y, x)` | 返回`y/x`的反正切 |
| `Math.cos(x)` | 返回`x`的余弦 |
| `Math.sin(x)` | 返回`x`的正弦 |
| `Math.tan(x)` | 返回`x`的正切 |

尽管这些方法是由 ECMA-262 定义的，但处理正弦、余弦和正切的结果取决于实现，因为可以用许多不同的方式计算每个值。因此，结果的精度在不同实现之间可能会有所不同。

## 总结

JavaScript 中的对象被称为引用值，可以使用几种内置引用类型来创建特定类型的对象，如下：

* 引用类型类似于编程中的类。
* `Object`类型是所有类型继承的基类。
* `Array`类型表示值的有序列表。
* `Date`类型提供有关日期和时间的信息。
* `RegExp`类型是支持正则表达式的接口。

JavaScript 的独特方面之一是函数实际上是`Function`类型的实例，这意味着函数是对象。由于包装类型的存在，原始值可以像对象一样被访问。有三种包装类型：

* 每个包装类型都映射到同名的原始类型。
* 当访问原始值时，会实例化一个包装对象以供其使用。
* 一旦执行了涉及原始值的语句，包装对象就会被销毁。

代码开始时还存在两个内置对象：`Global`和`Math`。`Global`对象在大多数实现中是无法访问的；然而，浏览器将它实现为`window`对象。`Global`对象将所有全局变量和函数作为属性包含。`Math`对象包含了辅助复杂计算的属性和方法。

# 第 6 章：面向对象编程

## 本章内容

* 理解对象属性
* 理解并创建对象
* 理解继承

面向对象 (OO) 语言通常通过使用类来创建多个具有相同属性和方法的对象来加以标识。正如之前提到的，ECMAScript 没有类概念，因此对象与基于类的语言中的对象不同。

ECMA-262 将对象定义为“一个无序属性集合，每个属性包含一个原始值、对象或函数”。严格来说，这意味着对象是一个没有特定顺序的值数组。每个属性或方法都通过一个映射到值的名称来标识。由于原因（以及其他待讨论的原因），将 ECMAScript 对象想成哈希表是有帮助的：它无非是键值对的组合，其中值可以是数据或函数。

## 理解对象

每个对象都是基于引用类型创建的，可以是前一节中讨论的内置类型之一，也可以用户定义的类型。

创建自定义对象的简单方法是创建一个`Object`的新实例，并向其添加属性和方法，如下例：

```javascript
var person = new Object();
person.name = "Nicholas";
person.age = 29;
person.job = "Software Engineer";
person.sayName = function(){
    alert(this.name);
};
```

`CreatingObjectsExample01.htm`

此示例创建了一个名为`person`的对象，它具有三个属性（`name`、`age`和`job`）和一个方法（`sayName()`）。`sayName()`方法显示`this.name`的值，该值解析为`person.name`。早期的 JavaScript 开发者经常使用这种模式来创建新对象。几年后，对象字面量变成了创建此类对象的首选模式。上一个示例可以使用对象字面量符号重写如下：

```javascript
var person = {
    name: "Nicholas",
    age: 29,
    job: "Software Engineer",
    sayName: function(){
        alert(this.name);
    }
};
```

此示例中的`person`对象与上一个示例中的`person`对象等效，具有相同的属性和方法。这些属性都是通过某些特性创建的，这些定义了它们在 JavaScript 中的行为。

# 属性类型

ECMA-262 第五版通过使用内部属性描述了属性的特性。这些属性由规范定义以便在 JavaScript 引擎中实现，因此这些属性在 JavaScript 中无法直接访问。要指示一个属性是内部的，请用两对方括号括属性名称，例如`[[Enumerable]]`。尽管 ECMA-262 第三版有不同的定义，但本书仅引用第五版的描述。

属性分为两种类型：数据属性和访问器属性。

## 数据属性

数据属性包含一个存储数据值的单一位置。值从该位置读取并写入该位置。数据属性有四个描述其行为的属性：

* `[[Configurable]]` — 指示该属性是否可以通过`delete`删除属性、更改属性属性或将属性更改为访问器属性来重新定义。默认情况下，所有直接定义在对象上的属性均为 true，如上一个示例所示。
* `[[Enumerable]]` — 指示该属性是否会在`for-in`循环中返回。默认情况下，所有直接定义在对象上的属性均为 true，如上一个示例所示。
* `[[Writable]]` — 指示该属性的值是否可以更改。默认情况下，所有直接定义在对象上的属性均为 true，如上一个示例所示。
* `[[Value]]` — 包含属性的实际数据值。这是读取属性值的位置以及保存新值的位置。该属性的默认值为`undefined`。

当像上一个示例那样显式将属性添加到对象时，`[[Configurable]]`、`[[Enumerable]]`和`[[Writable]]`都被设置为 true，而`[[Value]]`属性被设置为分配的值。例如：

```javascript
var person = {
    name: "Nicholas"
};
```

在这里，创建了名为`name`的属性并分配了为 "Nicholas" 的值。这意味着`[[Value]]`被设置为 "Nicholas"，并且对该值的任何更改都存储在此位置。

要更改任何默认属性属性，你必须使用 ECMAScript 5 的`Object.defineProperty()`方法。该方法接受三个参数：要添加或修改属性的对象、属性的名称以及一个描述符对象。描述符对象上的属性与属性名称匹配：`configurable`、`enumerable`、`writable`和`value`。你可以设置这些值中的一个或全部，以更改对应的属性值。例如：

![image](img/logo1.gif)

```javascript
var person = {};
Object.defineProperty(person, "name", {
    writable: false,
    value: "Nicholas"
});

alert(person.name);    //"Nicholas"
person.name = "Greg";
alert(person.name);    //"Nicholas"
```

`DataPropertiesExample01.htm`

此示例创建了一个名为`name`的属性，值为 "Nicholas"，它是只读的。该属性的值无法更改，在非严格模式下，任何分配新值的尝试都会被忽略。在严格模式下，尝试更改只读属性的值时会抛出错误。

创建不可配置属性也遵循类似的规则。例如：

```javascript
var person = {};
Object.defineProperty(person, "name", {
    configurable: false,
    value: "Nicholas"
});

alert(person.name);    //"Nicholas"
delete person.name;
alert(person.name);    //"Nicholas"
```

`DataPropertiesExample02.htm`

在这里，将`configurable`设置为`false`意味着无法从对象中删除该属性。在非严格模式下对属性调用`delete`没有影响，在严格模式下会抛出错误。此外，一旦属性被定义为不可配置的，它就无法再次变为可配置。任何调用`Object.defineProperty()`并更改`writable`以外任何属性的尝试都会导致错误：

![image](img/logo1.gif)

```javascript
var person = {};
Object.defineProperty(person, "name", {
    configurable: false,
    value: "Nicholas"
});

//抛出错误
Object.defineProperty(person, "name", {
    configurable: true,
    value: "Nicholas"
});
```

`DataPropertiesExample03.htm`

因此，尽管你可以对同一个属性多次调用`Object.defineProperty()`，但一旦`configurable`被设置为`false`，就会存在限制。

当你使用`Object.defineProperty()`时，除非另有指定，`configurable`、`enumerable`和`writable`的值认为`false`。在大多数情况下，你可能不需要`Object.defineProperty()`提供的强大选项，但为了良好理解 JavaScript 对象，这些概念是重要的。

![image](img/pen.gif)

Internet Explorer 8 是第一个实现`Object.defineProperty()`的版本。遗憾的是，实现非常有限。该方法只能用于 DOM 对象且只能创建访问器属性。由于实现不完整，建议在 Internet Explorer 8 中避免使用`Object.defineProperty()`。

## 访问器属性

访问器属性不包含数据值。相反，它们包含 getter 函数和 setter 函数的组合（尽管两者并非必须）。当读取访问器属性时，会调用 getter 函数，该函数负责返回一个有效值；当写入访问器属性时，会调用函数，该函数决定如何响应数据。访问器属性有四个属性：

* `[[Configurable]]` — 指示该属性是否可以通过`delete`删除属性、更改属性属性或将属性更改为数据属性来重新定义。默认情况下，所有直接定义在对象上的属性均为 true。
* `[[Enumerable]]` — 指示该属性是否会在`for-in`循环中返回。默认情况下，所有直接定义在对象上的属性均为 true。
* `[[Get]]` — 读取属性时调用的函数。默认值为`undefined`。
* `[[Set]]` — 写入属性时调用的函数。默认值为`undefined`。

无法显式地定义访问器属性；你必须使用`Object.defineProperty()`。这是一个简单的示例：

![image](img/logo1.gif)

```javascript
var book = {
    _year: 2004,
    edition: 1
};

Object.defineProperty(book, "year", {
    get: function(){
        return this._year;
    },
    set: function(newValue){
        if (newValue > 2004) {
            this._year = newValue;
            this.edition += newValue - 2004;
        }
    }
});

book.year = 2005;
alert(book.edition);   //2
```

`AccessorPropertiesExample01.htm`

在此代码中，创建了一个对象`book`，它包含两个默认属性：`_year`和`edition`。`_year`前的下划线是一种常见的表示法，指示该属性不希望在对象方法之外被访问。`year`属性被定义为一个访问器属性，其 getter 函数简单地返回`_year`的值，而 setter 函数则通过进行一些计算来确定正确的`edition`。因此，将`year`属性更改为 2005 会导致`_year`和`edition`均变为 2。这是访问器属性的一个典型用例，即设置属性值会导致其他某些变化。

没有必要同时赋值 getter 和 setter。只赋值 getter 意味着该属性是不可写入的，任何写入尝试都将被忽略。在严格模式下，尝试写入一个只有 getter 的属性会抛出错误。同样，只有 setter 的属性无法被读取，在非严格模式下将返回值`undefined`，而在严格模式下这样做会抛出错误。

在 ECMAScript 5 方法出现（该方法适用于 Internet Explorer 9+（Internet Explorer 8 仅有部分实现）、Firefox 4+、Safari 5+、Opera 12+ 和 Chrome）之前，使用了两种非标准方法来创建访问器属性：`__defineGetter__()`和`__defineSetter__()`。这些最初由 Firefox 开发，后来被 Safari 3、Chrome 1 和 Opera 9.5 复制。上一个示例可以使用这些遗留方法重写如下：

![image](img/logo1.gif)

```javascript
var book = {
    _year: 2004,
    edition: 1
};

//旧访问器支持
book.__defineGetter__("year", function(){
    return this._year;    
});

book.__defineSetter__("year", function(newValue){
    if (newValue > 2004) {
        this._year = newValue;
        this.edition += newValue - 2004;
    }    
});

book.year = 2005;
alert(book.edition);   //2
```

`AccessorPropertiesExample02.htm`

在不支持`Object.defineProperty()`的浏览器中，没有办法修改`Configurable`或`Enumerable`。

## 定义多个属性

由于你很有可能需要在对象上定义多个一个属性，ECMAScript 5 提供了`Object.defineProperties()`方法。该方法允许你一次性使用描述符（descriptors）定义多个属性。它接受两个参数：要添加或修改属性的对象，以及一个其属性名与要添加或修改的属性名相对应的对象。例如：

```javascript
var book = {};
Object.defineProperties(book, {
    _year: {



`value:我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。2004`

`edition: { value: 1 }`

`year: { get: function(){ return this._year; }, set: function(newValue){ if (newValue > 2004) { this._year = newValue; this.edition += newValue - 2004; } } }`

`MultiplePropertiesExample01.htm`

这段代码在`book`对象上定义了两个数据属性`_year`和`edition`，以及一个名为`year`的访问器属性。生成的对象与上一节中的示例完全相同。唯一的区别是所有这些属性都是同时创建的。

`Object.defineProperties()`方法支持 Internet Explorer 9+、Firefox 4+、Safari 5+、Opera 12+ 和 Chrome。

## 读取属性属性

可以使用 ECMAScript 5 的`Object.getOwnPropertyDescriptor()`方法获取给定属性的属性描述符。该方法接受两个参数：属性所属的对象以及要获取描述符的属性名称。返回值是一个对象，对于访问器属性包含`configurable`、`enumerable`、`get`和`set`属性；对于数据属性则包含`configurable`、`enumerable`、`writable`和`value`属性。例如：

![image](img/logo1.gif)

```
var book = {};

Object.defineProperties(book, {
    _year: {
        value: 2004
    },
    edition: {
        value: 1
    },
    year: {            
        get: function(){
            return this._year;
        },
        set: function(newValue){
            if (newValue > 2004) {
                this._year = newValue;
                this.edition += newValue - 2004;
            }                  
        }            
    }        
});

var descriptor = Object.getOwnPropertyDescriptor(book, "_year");

alert(descriptor.value);          //2004
alert(descriptor.configurable);   //false
alert(typeof descriptor.get);     //"undefined"

var descriptor = Object.getOwnPropertyDescriptor(book, "year");

alert(descriptor.value);          //undefined
alert(descriptor.enumerable);     //false
alert(typeof descriptor.get);     //"function"
```

`GetPropertyDescriptorExample01.htm`

对于数据属性`_year`，`value`等于原始值，`configurable`为`false`，且`get`为`undefined`。对于访问器属性`year`，`value`为`undefined`，`enumerable`为`false`，且`get`是指向指定 getter 函数的指针。

`Object.getOwnPropertyDescriptor()`方法可以用于 JavaScript 中的任何对象，包括 DOM 和 BOM 对象。该方法支持 Internet Explorer 9+、Firefox 4+、Safari 5+、Opera 12+ 和 Chrome。

## 对象创建

虽然使用`Object`构造函数或对象字面量创建单个对象是方便的方法，但有一个明显的缺点：创建多个对象需要大量的代码重复。为了解决这个问题，开发者开始使用工厂模式的变体。

### 工厂模式

工厂模式是软件工程中常用的设计模式，用于抽象创建对象的过程。（其他设计模式及其在 JavaScript 中的实现将在书中后面讨论。）由于 ECMAScript 中没有定义类的方法，开发者创建了函数来封装具有特定接口的对象创建，如下例所示：

![image](img/logo1.gif)

```
function createPerson(name, age, job){
    var o = new Object();
    o.name = name;
    o.age = age;
    o.job = job;
    o.sayName = function(){
        alert(this.name);
    };    
    return o;
}

var person1 = createPerson("Nicholas", 29, "Software Engineer");
var person2 = createPerson("Greg", 27, "Doctor");
```

`FactoryPatternExample01.htm`

在这里，`createPerson()`函数接收参数以构建一个包含表示`Person`对象所需所有信息的对象。该函数可以根据不同的参数多次调用，并仍然返回一个具有三个属性和一个方法的对象。

### 构造模式

如前面的章节中提到的，ECMAScript 中的构造函数用于创建特定类型的对象。有原生构造函数，例如`Object`和`Array`，它们在运行时执行环境中可用。也可以定义自定义构造函数，为你自己的对象类型定义属性和方法。例如，上一个示例可以使用构造模式重写如下：

![image](img/logo1.gif)

```
function Person(name, age, job){
    this.name = name;
    this.age = age;
    this.job = job;
    this.sayName = function(){
        alert(this.name);
    };    
}

var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor");
```

`ConstructorPatternExample01.htm`

在这个示例中，`Person()`函数取代了工厂函数`createPerson()`。注意`Person()`内部的代码与`createPerson()`内部的代码相同，唯一的异常是：

*   没有显式创建对象。
*   属性和方法被直接赋值到`this object`上。
*   没有返回语句。

另外请注意，函数名为`Person`，首字母`P`大写。按照惯例，构造函数始终以大写字母开头，而非构造函数则以小写字母开头。这种惯例借自其他面向对象的语言，并有助于区分 ECMAScript 中的函数用途，因为构造函数本质上就是创建对象的函数。

要创建`Person`的新实例，请使用`new`运算符。以这种方式调用构造函数本质上会执行以下四个步骤：

1. 创建一个新对象。
2. 将构造函数的`this`值赋值给新对象（因此`this`指向该新对象）。
3. 执行构造函数内部的代码（向新对象添加属性）。
4. 返回新对象。

在上一个示例的结束处，`person1`和`person2`分别填充了不同的`Person`实例。这些对象中的每一个都有一个指向`Person`的`constructor`属性，如下：

```
alert(person1.constructor == Person);  //true
alert(person2.constructor == Person);  //true
```

`constructor`属性最初旨在用于识别对象类型。然而，`instanceof`运算符被认为是确定类型更安全的方法。示例中的每个对象都被认为既是`Object`的实例也是`Person`的实例，如使用`instanceof`运算符所示：

```
alert(person1 instanceof Object);  //true
alert(person1 instanceof Person);  //true
alert(person2 instanceof Object);  //true
alert(person2 instanceof Person);  //true
```

定义你自己的构造函数可以确保以后可以将实例识别为特定类型，这与工厂模式相比是一个巨大的优势。在例示例中，`person1`和`person2`被视为`Object`的实例，因为所有自定义对象都继承自`Object`（这些细节将在稍后讨论）。

![image](img/pen.gif)

以这种方式定义的构造函数定义在`Global`对象上（Web 浏览器中的`window`对象）。浏览器对象模型（BOM）将在第 8 章中进一步讨论。

### 作为函数的构造函数

构造函数与其他函数之间的唯一区别在于调用它们的方式。毕竟，构造函数只是函数；没有特殊的语法来定义构造函数使其自动表现得像构造。任何使用`new`运算符调用的函数都充当构造函数，而任何不使用它的函数表现得就像你预期的普通函数调用一样。例如，上一个示例中的`Person()`函数可以用以下任一方式调用：

![image](img/logo1.gif)

```
//作为构造函数使用
var person = new Person("Nicholas", 29, "Software Engineer");
person.sayName();   //"Nicholas"

//作为函数调用
Person("Greg", 27, "Doctor");  //添加到 window
window.sayName();   //"Greg"

// 在另一个对象的作用范围内调用
var o = new Object();
Person.call(o, "Kristen", 25, "Nurse");
o.sayName();    //"Kristen"
```

`ConstructorPatternExample02.htm`

此示例的第一部分显示了构造函数的典型用法，通过`new`运算符创建新对象。第二部分显示了在不使用`new`运算符调用`Person()`函数时发生了什么：属性和方法被添加到`window`对象上。记住，当调用函数时没有显式设置`this`值（通过作为对象方法或通过`call()`、`apply()`），`this`对象始终指向`Global`对象（Web 浏览器中的`window`）。因此，在调用函数后，可以在`window`对象上调用`sayName()`方法，它将返回 "Greg"。`Person()`函数也可以使用`call()`（或`apply()`）在特定对象的作用范围内调用。在这种情况下，它是带入对象`o`的`this`值调用的，该对象随后被分配所有的属性和`sayName()`方法。

### 构造函数的问题

尽管构造函数范式很有用，但它并非没有缺陷。构造函数的主要缺点是为每个实例都创建一次方法。因此，在上一个示例中，`person1`和`person2`都有名为`sayName()`的方法，但这些方法不是同一个`Function`实例。记住，函数在 ECMAScript 中是对象，所以每次定义函数时，实际上都是实例化了一个对象。从逻辑上讲，构造函数实际上像这样：

```
function Person(name, age, job){
    this.name = name;
    this.age = age;
    this.job = job;
    this.sayName = new Function("alert(this.name)"); //逻辑等效 
}
```

这样思考构造函数就很清楚，每个`Person`实例都得到了自己的`Function`实例，该实例恰好显示 name 属性。明确的是，这种方式创建函数在作用域链和标识符解析方面是不同的，但创建`Function`新实例的机制是相同的。因此，不同实例上的同名函数是不等价的，如下所示代码证明：

```
alert(person1.sayName == person2.sayName);  //false
```

拥有两个执行相同操作`Function`实例是没有意义的，特别是当`this`对象使得可以在运行时避免将函数绑定到特定对象时。可以通过将函数定义移动到构造函数之外来规避此限制，如下：

![image](img/logo1.gif)

```
function Person(name, age, job){
    this.name = name;
    this.age = age;
    this.job = job;
    this.sayName = sayName;
}

function sayName(){
    alert(this.name);
}

var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor");
```

`ConstructorPatternExample03.htm`

在此示例中，`sayName()`函数定义在构造函数之外。在构造函数内部，`sayName`属性被设置为全局`sayName()`函数。由于`sayName`属性现在仅包含指向函数的指针，`person1`和`person2`最终共享了在全局作用域中定义的`sayName()`函数。这解决了重复创建相同函数的问题，但通过引入一个实际上只能与对象相关的使用的函数，在全局作用域中创建了一些混乱。如果对象需要多个方法，这意味着会有多个全局函数，突然之间自定义引用类型的定义不再在代码中整齐地分组。这些问题通过使用原型模式来解决。

### 原型模式

每个函数在创建时都带有一个`prototype`属性，它是一个包含属性和方法的对象，这些属性和方法对特定引用类型的实例可用。这个对象字面上是调用构造函数后要创建对象的原型。使用原型的用处是它的所有属性和方法都在对象实例之间共享。与其在构造函数中分配对象信息，不如将它们直接分配到原型，如例所示：

```
function Person(){
}

Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function(){
    alert(this.name);
};

var person1 = new Person();
person1.sayName();   //"Nicholas"

var person2 = new Person();
person2.sayName();   //"Nicholas"

alert(person1.sayName == person2.sayName);  //true
```



`PrototypePatternExample01.htm`

在这里，属性和`sayName()`方法被直接添加到`Person`的`prototype`属性上，使构造函数保持为空。然而，仍然可以调用构造函数来创建一个新对象，并拥有这些属性和方法。与构造函数模式不同，属性和方法在所有实例之间共享的，因此`person1`和`person2`访问的是同一组属性和同一个`sayName()`函数。要理解其工作原理，你必须理解 ECMAScript 中原型（prototype）的本质。

## 原型是如何工作的

每当创建一个函数时，它的`prototype`属性也会根据一组特定的规则被创建。默认情况下，所有的原型都会自动获得一个名为`constructor`的属性，该属性指向拥有该属性的函数。例如，在上一个例子中，`Person.prototype.constructor`指向`Person`。然后，根据构造函数的不同，可能会向原型上添加其他属性和方法。

在定义自定义构造函数时，原型默认只获得`constructor`属性；所有其他方法都从`Object`继承。每当调用构造函数创建一个新实例时，该实例都有一个指向构造函数原型的内部指针。在 ECMA-262 第五中，这被称为`[[Prototype]]`。目前没有标准方法从脚本访问`[[Prototype]]`，但 Firefox、`Safari`和`Chrome`都支持每个对象上都有一个名为`__proto__`的属性；在其他实现中，该属性对脚本完全隐藏。重要的理解点是：实例与构造函数原型之间存在直接链接，但实例与构造函数之间没有。

考虑之前使用`Person`构造函数和`Person.prototype`的示例。示例中对象之间的关系如图图 6-1 所示。

图 6-1

![image](img/f185-01.jpg)

图 6-1 显示了`Person`构造函数、`Person`的原型以及存在的两个`Person`实例之间的关系。注意，`Person.prototype`指向原型对象，但`Person.prototype.constructor`指回`Person`。原型包含了`constructor`属性以及添加的其他属性。每个`Person`实例（`person1`和`person2`）都只有一个指向`Person.prototype`的内部属性；它们与构造函数没有直接关系。另请注意，尽管这两个实例都没有属性或方法，但`person1.sayName()`仍然可以工作。这是由于对象属性的查找机制导致的。

尽管在所有实现中都无法访问`[[Prototype]]`，但可以使用`isPrototypeOf()`方法来判断对象之间是否存在这种关系。本质上，如果`[[Prototype]]`指向调用方法时的原型，`isPrototypeOf()`将返回`true`，如下：

```
alert(Person.prototype.isPrototypeOf(person1));  //true
alert(Person.prototype.isPrototypeOf(person2));  //true
```

在这段代码中，在`person1`和`person2`上调用了原型的`isPrototypeOf()`方法。由于两个实例都有到`Person.prototype`的链接，因此返回`true`。

ECMAScript 5 增加了一个名为`Object.getPrototypeOf()`的新方法，它在所有支持的实现中都返回`[[Prototype]]`的值。例如：

```
alert(Object.getPrototypeOf(person1) == Person.prototype);  //true
alert(Object.getPrototypeOf(person1).name);  //"Nicholas"
```

这段代码的第一行简单确认了从`Object.getPrototypeOf()`返回的对象实际上是该对象的原型。第二行获取了原型上`name`属性的值，该值为值为`"Nicholas"`。使用`Object.getPrototypeOf()`，你可以轻松地检索对象的原型，这在你想要使用原型实现继承时（在本章稍后部分讨论）将变得至关重要。该方法支持 Internet Explorer 9+、`Firefox 3.5+`、`Safari 5+`、`Opera 12+`和`Chrome`。

每当对对象上的属性进行读取访问时，就会开始搜索以找到同名的属性。搜索从对象实例本身开始。如果在实例上找到了同名的属性，则返回该值；如果未找到该属性，则将沿指针向上继续到原型，并在原型中搜索同名的属性。如果在原型上找到了该属性，则返回该值。因此，当调用`person1.sayName()`时，会发生两步过程。首先，JavaScript 引擎询问：“实例`person1`是否有一个名为`sayName`的属性？”答案是否，于是它继续搜索并询问：“`person1`的原型是否有一个名为`sayName`的属性？”答案是是，因此访问了存储在原型上的函数。当调用`person2.sayName()`时，会执行相同的搜索，并得到相同的结果。这就是原型如何用于在多个对象实例之间共享属性和方法。

![image](img/pen.gif)

之前提到的`constructor`属性仅存在于原型上，因此可以从对象实例访问。

虽然可以从对象实例读取原型上的值，但无法覆盖它们。如果你在实例上添加了一个与原型上属性同名的属性，你就在实例上创建了该属性，该属性随后会遮蔽（mask）原型上的该属性。这里有一个示例：

![image](img/logo1.gif)

```
function Person(){
}

Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function(){
    alert(this.name);
};

var person1 = new Person();
var person2 = new Person();

person1.name = "Greg";
alert(person1.name);     //"Greg" - 来自实例
alert(person2.name);     //"Nicholas" - 来自原型
```

`PrototypeExample02.htm`

在这个示例中，`person1`的`name`属性被一个新值遮蔽了。`person1.name`和`person2.name`仍然可以正常工作，分别返回`"Greg"`（来自实例）和`"Nicholas"`（来自原型）。在`alert()`中访问`person1.name`时，它的值被读取，因此开始在实例上搜索名为`name`的属性。由于属性存在，因此直接使用，而不搜索原型。以相同的方式访问`person2.name`时，搜索在实例上没有找到该属性，因此继续搜索原型，并在那里找到了`name`属性。一旦属性被添加到对象实例，它就会遮蔽原型上任何同名的属性，这意味着它阻止了对原型上属性的访问。即使将属性设置为`null`，也只是设置了实例上的属性，并没有恢复与原型的链接。然而，`delete`运算符会完全删除实例属性，并允许如下所示再次访问原型属性：

```
function Person(){
}

Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function(){
    alert(this.name);
};

var person1 = new Person();
var person2 = new Person();

person1.name = "Greg";
alert(person1.name);   //"Greg" - 来自实例
alert(person2.name);     //"Nicholas" - 来自原型

delete person1.name;
alert(person1.name);   //"Nicholas" - 来自原型
```

`PrototypeExample03.htm`

在这个修改后的示例中，对`person1.name`尽了`delete`，该属性之前被用`"Greg"`值遮蔽了。这恢复了与原型`name`属性的链接，因此当下次访问`person1.name`时，返回的是原型属性的值。

`hasOwnProperty()`方法用于判断属性是否存在于实例上或原型链上。该方法继承自`Object`，只有当给定名称的属性存在于对象实例时，它才会返回 true，如例所示：

```javascript
function Person(){
}

Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function(){
    alert(this.name);
};

var person1 = new Person();
var person2 = new Person();

alert(person1.hasOwnProperty("name"));  //false

person1.name = "Greg";
alert(person1.name);   //"Greg" - 来自自实例
alert(person1.hasOwnProperty("name"));  //true

alert(person2.name);   //"Nicholas" - 来自自原型
alert(person2.hasOwnProperty("name"));  //false

delete person1.name;
alert(person1.name);   //"Nicholas" - 来自自原型
alert(person1.hasOwnProperty("name"));  //false
```

通过在此示例中注入对`hasOwnProperty()`的调用，可以清楚地看到何时访问了实例属性，何时访问了原型属性。只有在`person1`的 name 被覆盖后，调用`person1.hasOwnProperty("name")`才会返回 true，这表明它现在拥有一个实例属性而不是原型属性。图 6-2 展示了此示例中所采取的各个步骤。（为了简单起这里省略了与`Person`构造函数的关系。）

图 6-2

![image](img/f189-01.jpg)![image](img/pen.gif)

ECMAScript 5 `Object.getOwnPropertyDescriptor()`方法仅适用于实例属性；要检索原型属性的描述符，必须直接在原型对象上调用`Object.getOwnPropertyDescriptor()`。

### 原型与 in 操作符

使用`in`操作符有两种方式：单独使用或作为`for-in`循环的一部分使用。当单独使用时，`in`操作符在对象可以访问给定名称的属性时返回 true，这意味着该属性可能存在于实例上，也可能存在于原型上。考虑以下示例：

![image](img/logo1.gif)

```javascript
function Person(){
}

Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function(){
    alert(this.name);
};

var person1 = new Person();
var person2 = new Person();

alert(person1.hasOwnProperty("name"));  //false
alert("name" in person1);  //true

person1.name = "Greg";
alert(person1.name);   //"Greg" - 来自自实例
alert(person1.hasOwnProperty("name"));  //true
alert("name" in person1);  //true

alert(person2.name);   //"Nicholas" - 来自自原型
alert(person2.hasOwnProperty("name"));  //false
alert("name" in person2);  //true

delete person1.name;
alert(person1.name);   //"Nicholas" - 来自自原型
alert(person1.hasOwnProperty("name"));  //false
alert("name" in person1);  //true
```

`PrototypePatternExample04.htm`

在这段代码的执行过程中，属性名在每个对象上都是可用的（直接或原型）。因此，在`person1`中调用`"name"`始终返回 true，无论该属性是否存在于实例上。可以通过将`hasOwnProperty()`的调用与`in`操作符结合使用，来判断对象的属性是否存在于原型上：

![image](img/logo1.gif)

```javascript
function hasPrototypeProperty(object, name){
    return !object.hasOwnProperty(name) && (name in object);
}
```

由于`in`操作符只要对象可以访问该属性就始终返回 true，而`hasOwnProperty()`只在属性存在于实例上时返回 true，因此当`in`操作符返回 true 但`hasOwnProperty()`返回 false 时，就可以确定这是一个原型属性。考虑以下示例：

```javascript
function Person(){
}

Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function(){
    alert(this.name);
};

var person = new Person();        

alert(hasPrototypeProperty(person, "name"));  //true

person.name = "Greg";
alert(hasPrototypeProperty(person, "name"));  //false 
```

`PrototypePatternExample05.htm`

在此代码中，name 属性首先存在于原型上，因此`hasPrototypeProperty()`返回 true。一旦 name 属性被覆盖，它就存在于实例上，因此`hasPrototypeProperty()`返回 false。即使 name 属性仍然存在于原型上，它不再被使用，因为现在已经有了实例属性。

使用`for-in`循环时，所有对象可以访问且可以枚举的属性都将被返回，这包括实例和原型上的属性。遮蔽了不可枚举原型属性（即`[[Enumerable]]`设置为 false 的属性）的实例属性会在`for-in`循环中返回，因为根据规则，所有用户定义的属性都是可枚举的，Internet Explorer 8 及更早版本除外。

旧版本的 Internet Explorer 有一个 bug，导致遮蔽了不可枚举属性不会出现在`for-in`循环中。这里有一个示例：

![image](img/logo1.gif)

```javascript
var o = {
    toString : function(){
        return "My Object";
    }
};

for (var prop in o){
    if (prop == "toString"){
        alert("Found toString");
    }
}
```

`PrototypePatternExample06.htm`

运行此代码时，应该显示一条提示表示找到了`toString()`方法。对象`o`拥有一个名为`toString()`的实例属性，它遮蔽了原型方法。在 Internet Explorer 中，由于显示相同的 bug 影响了所有默认不可枚举的属性：`hasOwnProperty()`、`propertyIsEnumerable()`、`toString()`和`valueOf()`。

要获取对象上所有枚举属性的列表，可以使用 ECMAScript 5 的`Object.keys()`方法，它接受一个对象作为参数，并返回包含所有属性名称的数组。例如：

![image](img/logo1.gif)

```javascript
function Person(){
}

Person.prototype.name = "Nicholas";
```



`Person.prototype.age = 29;`

`Person.prototype.job = "Software Engineer";`

`Person.prototype.sayName = function(){`

    `alert(this.name);`

`};`

`var keys = Object.keys(Person.prototype);`

`alert(keys);       //"name,age,job,sayName"`

`var p1 = new Person();`

`p1.name = "Rob";`

`p1.age = 31;`

`var p1keys = Object.keys(p1);`

`alert(p1keys);    //"name,age"`

`ObjectKeysExample01.htm`

在这里，`keys` 变量被填充为包含 `"name"`、`"age"`、`"job"` 和 `"sayName"` 的数组。这是它们在使用 `for-in` 时通常出现的顺序。在 `Person` 实例上调用时，`Object.keys()` 返回 `name` 和 `age` 数组，这是唯一的两个实例属性。

如果你想要所有实例属性列表（无论是否可枚举），可以用相同的方式使用 `Object.getOwnPropertyNames()`：

```javascript
var keys = Object.getOwnPropertyNames(Person.prototype);
alert(keys);   //"constructor,name,age,job,sayName"
```

`ObjectPropertyNamesExample01.htm`

注意结果列表中包含了不可枚举的构造属性。`Object.keys()` 和 `Object.getOwnPropertyNames()` 都可以作为替代 `for-in` 的合适方案。这些方法在 Internet Explorer 9+、Firefox 4+、Safari 5+、Opera 12+ 以及 Chrome 中均支持。

你可能已经在上一个示例中注意到，每个属性和方法都需要显式编写 `Person.prototype`。为了减少这种冗余并在原型上更好地实现视觉封装，现在常见的做法是直接用一个包含所有属性和方法的对象字面量来覆盖原型，如下例所示：

![image](img/logo1.gif)

```javascript
function Person(){
}

Person.prototype = {
    name : "Nicholas",
    age : 29,
    job : "Software Engineer",
    sayName : function () {
        alert(this.name);
    }
};
```

`PrototypePatternExample07.htm`

在这个重写后的示例中，`Person.prototype` 属性被赋值为一个使用对象字面量创建的新对象。最终结果是相同的，但有一个例外：`constructor` 属性不再指向 `Person`。当创建一个函数时，会创建它的原型对象并自动分配 `constructor`。从本质上，这种语法完全覆盖了默认的原型对象，这意味着 `constructor` 属性等于一个完全新对象（`Object` 构造函数），而不是函数本身。尽管 `instanceof` 运算符仍然可靠工作，但你不能像这个示例所示那样依赖 `constructor` 来指示对象的类型：

```javascript
var friend = new Person();
alert(friend instanceof Object);      //true
alert(friend instanceof Person);      //true
alert(friend.constructor == Person);  //false
alert(friend.constructor == Object);  //true
```

`PrototypePatternExample07.htm`

在这里，`instanceof` 对于 `Object` 和 `Person` 仍然返回 `true`，但 `constructor` 属性现在等于 `Object` 而不是 `Person`。如果 `constructor` 的值很重要，你可以将其特意地设置回适当的值，如下所示：

```javascript
function Person(){
}

Person.prototype = {
    constructor: Person,
    name : "Nicholas",
    age : 29,
    job : "Software Engineer",
    sayName : function () {
        alert(this.name);
    }
};
```

`PrototypePatternExample08.htm`

这段代码专门包含了一个 `constructor` 属性并将其赋值为 `Person`，确保了该属性包含适当的值。

请记住，以这种方式恢复 `constructor` 会创建一个 `[[Enumerable]]` 标记为 `true` 的属性。原生构造函数属性默认是不可枚举的，因此如果你在使用符合 ECMAScript 5 标准的 JavaScript 引擎，你可能更倾向于使用 `Object.defineProperty()`：

```javascript
function Person(){
}

Person.prototype = {
    name : "Nicholas",
    age : 29,
    job : "Software Engineer",
    sayName : function () {
        alert(this.name);
    }
};

//仅限 ECMAScript 5 - 恢复 constructor
Object.defineProperty(Person.prototype, "constructor", {
    enumerable: false,
    value: Person
});
```

## 原型的动态性质

由于在原型上查找值的过程是一个搜索过程，在任何时候对原型进行的更改都会立即反映在实例上，即使是修改发生之前就已经存在的实例。这里有一个例子：

![image](img/logo1.gif)

```javascript
var friend= new Person();
Person.prototype.sayHi = function(){
    alert("hi");
};
friend.sayHi();   //"hi" - 正常工作！
```

`PrototypePatternExample09.htm`

在此代码中，创建了一个 `Person` 实例并将其存储在 `friend` 中。下一条语句向 `Person.prototype` 添加了一个名为 `sayHi()` 的方法。尽管 `friend` 实例在此更改之前就已经创建，但它仍然可以访问新方法。这是由于实例和原型之间松散的链接。当调用 `friend.sayHi()` 时，实例会首先搜索名为 `sayHi` 的属性；当未找到时，搜索将继续到原型。由于实例和原型之间的链接仅仅是一个指针而不是拷贝，因此搜索在原型上找到了新的 `sayHi` 属性并返回了存储在那里的函数。

尽管可以随时向原型中添加属性和方法，并且它们会立即反映在所有对象实例上，但你不能覆盖整个原型并期望获得相同的行为。`[[Prototype]]` 指针是在调用构造函数时分配的，因此将原型更改为不同的对象会断开构造函数与原始原型之间的联系。记住：实例只指向原型，而不指向构造函数。请考虑以下情况：

![image](img/logo1.gif)

```javascript
function Person(){
}

var friend = new Person();

Person.prototype = {
    constructor: Person,
    name : "Nicholas",
    age : 29,
    job : "Software Engineer",
    sayName : function () {
        alert(this.name);
    }
};

friend.sayName();   //error
```

`PrototypePatternExample10.htm`

在这个示例中，在原型对象被覆盖之前创建了一个 `Person` 的新实例。当调用 `friend.sayName()` 时，会导致错误，因为 `friend` 指向的原型并不包含同名的属性。图 6-3 解释了为什么会发生这种情况。

图 6-3

![image](img/f195-01.jpg)

在构造函数上覆盖原型意味着新实例将引用新原型，而任何先存在的对象实例仍然引用旧原型。

## 原生对象原型

原型模式不仅对于定义自定义类型很重要，而且它是实现所有原生引用类型时所使用的模式。这些每一个类型（包括 `Object`、`Array`、`String` 等）的方法都定义在构造函数的原型上。例如，可以在 `Array.prototype` 上找到 `sort()` 方法，在 `String.prototype` 上找到 `substring()` 方法，如下所示：

![image](img/logo1.gif)

```javascript
alert(typeof Array.prototype.sort);         //"function"
alert(typeof String.prototype.substring);   //"function"
```

通过原生对象原型，可以获取所有默认方法的引用并定义新方法。原生对象原型可以像对象原型一样被修改，因此可以随时添加方法。例如，以下代码为 `String` 原生包装添加了一个名为 `startsWith()` 的方法：

```javascript
String.prototype.startsWith = function (text) {
    return this.indexOf(text) == 0;
};

var msg = "Hello world!";
alert(msg.startsWith("Hello"));   //true
```

`PrototypePatternExample11.htm`

示例中的 `startsWith()` 方法在文本出现在字符串开头时返回 `true`。该方法被赋值给 `String.prototype`，使得环境中的所有字符串可用。由于 `msg` 是一个字符串，后台会创建 `String` 原生包装，使得 `startsWith()` 可用。

![image](img/pen.gif)

虽然可行，但不建议在生产环境中修改原生对象原型。这通常会导致困惑，并且如果某个在某个浏览器中不存在的方法在另一个浏览器中原生实现，则可能会产生命名冲突。同时也可能意外覆盖原生方法。

## 原型存在的问题

原型模式并非没有缺陷。首先，它消除了在构造函数中传递初始化参数的能力，这意味着所有实例默认获得相同的属性值。尽管这是一种不便，但并不是原型最大的问题。主要问题源于它们的共享性质。

原型上的所有属性在实例间共享，这对于函数来说是理想的。包含原始值值的属性通常也运行良好，如之前的示例所示，可以通过在实例上分配同名属性来隐藏原型属性。当属性包含引用值时，就会出现真正的问题。请考虑以下示例：

![image](img/logo1.gif)

```javascript
function Person(){
}

Person.prototype = {
    constructor: Person,
    name : "Nicholas",
    age : 29,
    job : "Software Engineer",
    friends : ["Shelby", "Court"],
    sayName : function () {
        alert(this.name);
    }
};

var person1 = new Person();
var person2 = new Person();

person1.friends.push("Van");
alert(person1.friends);    //"Shelby,Court,Van"
alert(person2.friends);    //"Shelby,Court,Van"
alert(person1.friends === person2.friends);  //true
```

`PrototypePatternExample12.htm`

在这里，`Person.prototype` 对象有一个名为 `friends` 的属性，它包含一个字符串数组。随后创建了两个 `Person` 实例。通过添加另一个字符串修改了 `person1.friends` 数组。由于 `friends` 数组存在于 `Person.prototype` 上，而不是 `person1` 上，因此所做的更改也会反映在 `person2.friends` 中（它们指向同一个数组）。如果目的是为了让所有实例共享一个数组，那么这个结果是可以接受的。但通常，实例希望拥有所有属性的自己的副本。这就是为什么原型模式很少单独使用。

## 构造函数/原型模式结合 (Combination Constructor/Prototype Pattern)

定义自定义类型常用的方法是将构造函数模式和原型模式结合。构造模式定义实例属性，而原型模式定义方法和共享属性。通过这种方法，每个实例最终都拥有自己的实例属性副本，但它们都共享对方法的引用，从而节省内存。这种模式还允许将参数传递给构造函数，有效地结合了每种模式的优点。之前的示例现在可以重写如下：

```javascript
function Person(name, age, job){
    this.name = name;
    this.age = age;
    this.job = job;
    this.friends = ["Shelby", "Court"];
}

Person.prototype = {
    constructor: Person,
    sayName : function () {
        alert(this.name);
    }
};

var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor");

person1.friends.push("Van");
alert(person1.friends);    //"Shelby,Court,Van"
alert(person2.friends);    //"Shelby,Court"
alert(person1.friends === person2.friends);  //false
alert(person1.sayName === person2.sayName);  //true
```

`HybridPatternExample01.htm`

注意，实例属性现在完全定义在构造函数中，而共享属性构造函数和方法 `sayName()` 则定义在原型上。当通过添加新字符串来增强 `person1.friends` 时，`person2.friends` 不受影响，因为它们各自拥有独立的数组。

混合构造函数/原型模式是 ECMAScript 中定义自定义引用类型最广泛使用和最受认可的做法。总的来说，这是定义引用类型的默认模式。

## 动态原型模式 (Dynamic Prototype Pattern)

来自其他面向对象语言的开发者可能会发现构造函数和原型之间的视觉分离让他们困惑。动态原型模式试图通过在构造函数内部封装所有信息来解决这个问题，同时通过在构造函数内部初始化原型（仅在需要时）来保持使用构造函数和原型的优势。你可以通过检查应该可用的方法是否存在来判断原型是否需要初始化。考虑这个示例：

![image](img/logo1.gif)

```javascript
function Person(name, age, job){
    //properties
    this.name = name;
    this.age = age;
    this.job = job;

    //methods
    if (typeof this.sayName != "function"){
        Person.prototype.sayName = function(){
            alert(this.name);
        };
    }
}

var friend = new Person("Nicholas", 29, "Software Engineer");
friend.sayName();
```



`DynamicPrototypeExample01.htm`

构造函数内部高亮的代码部分在 `sayName()` 方法尚不存在时会添加该方法。此块代码仅在第一次调用构造函数时执行。此后，原型已经初始化，不再需要任何进一步修改。记住，对原型的更改会立即反映在所有实例中，因此这种方法非常完美。`if` 语句可以检查初始化后将存在的任何属性或方法——不需要使用多个 `if` 语句来检查每个属性或方法；检查任何一个即可。这种模式保留了使用 `instanceof` 来确定创建了什么类型对象的功能。

![image](img/pen.gif)

在使用动态原型模式时，不能使用对象字面量重写原型。如之前所述，当实例已存在时重写原型会实际上切断该实例与新原型的联系。

## 寄生构造函数模式 (Parasitic Constructor Pattern)

寄生构造函数模式通常是当其他模式失败时的备用方案。该模式的基本思想是创建一个构造函数，它只是封装了另一个对象的创建和返回，同时看起来像一个典型的构造函数。这是一个示例：

![image](img/logo1.gif)

```javascript
function Person(name, age, job){

    var o = new Object();

    o.name = name;

    o.age = age;

    o.job = job;

    o.sayName = function(){

        alert(this.name);

    };    

    return o;

}

var friend = new Person("Nicholas", 29, "Software Engineer");

friend.sayName();  //"Nicholas"
```

`HybridFactoryExample01.htm`

在这个示例中，`Person` 构造函数创建一个新对象，对其属性和方法初始化，然后返回该对象。这与工厂模式完全相同，只是使用 `new` 运算符作为构造函数调用的。当构造函数没有返回值时，它会返回新实例。在构造函数末尾添加 `return` 语句允许你覆盖返回值。

这种模式允许你创建其他可能可能的构造函数。例如，你可能想创建一个带有额外方法的数组。由于无法直接访问 `Array` 构造函数，这种模式可以运行：

![image](img/logo1.gif)

```javascript
function SpecialArray(){       

    //create the array

    var values = new Array();

    //add the values

    values.push.apply(values, arguments);

    //assign the method

    values.toPipedString = function(){

        return this.join("|");

    };

    //return it

    return values;        

}

var colors = new SpecialArray("red", "blue", "green");

alert(colors.toPipedString()); //red|blue|green"
```

`HybridPatternExample02.htm`

Douglas Crockford 在 JavaScript 中提出了 `durable objects`（持久对象）一术语，指那些没有公共属性且其方法不引用 `this` 对象的对象。`Durable objects` 最适用于安全环境（禁止使用 `this` 和 `new` 的环境），或用于保护数据不受应用程序其他部分的影响（例如在 mash 中）。`durable constructor`（持久构造函数）是一种遵循类似于 `parasitic constructor pattern`（寄生构造函数模式）模式的构造函数，但有两个不同：创建的对象上的实例方法不引用 `this`，且构造函数永远不会使用 `new` 运算符调用。上一节中的 `Person` 构造函数可以重写为 `durable constructor`：

```javascript
function Person(name, age, job){

    //创建要返回的对象

    var o = new Object();

    //可选项：在这里定义私有变量/函数

    //挂载方法

    o.sayName = function(){

        alert(name);

    };    

    //返回对象

    return o;

}
```

注意，从返回的对象无法访问 `name` 的值。`sayName()` 方法可以访问它，但其他任何方法都不行。`Person` 持久构造函数的用法如下：

```javascript
var friend = Person("Nicholas", 29, "Software Engineer");

friend.sayName();  //"Nicholas"
```

`person` 变量是一个 `durable object`，在不调用方法的情况下，无法访问其任何数据成员。即使其他代码向该对象添加了方法或数据成员，也无法访问传递到构造函数的原始数据。这种安全性使得 `durable constructor pattern` 在处理安全执行环境时非常有用，例如由 `ADsafe` ([www.adsafe.org](http://www.adsafe.org)) 或 `Caja` ([`code.google.com/p/google-caja/`](http://code.google.com/p/google-caja/)) 提供的环境。

![image](img/pen.gif)

与 `parasitic constructor pattern` 一样，构造函数与对象实例之间没有关系。

## 继承

## 原型链

### 原型链

（注：由于原文中存在大量重复的乱码文本，已根据要求提取了核心技术内容进行翻译。）

```javascript
alert(Object.prototype.isPrototypeOf(instance));    //true

alert(SuperType.prototype.isPrototypeOf(instance)); //true

alert(SubType.prototype.isPrototypeOf(instance));   //true
```

### PrototypeChainingExample01.htm

#### 使用方法

子类通常需要重写父类方法，或者引入父类中不存在的新方法。为了实现这一点，必须在原型赋值之后，再将方法添加到原型中。请考虑这个示例：

![image](img/logo1.gif)

```javascript
function SuperType(){

    this.property = true;

}

SuperType.prototype.getSuperValue = function(){

    return this.property;

};

function SubType(){

    this.subproperty = false;

}

//继承自 SuperType

SubType.prototype = new SuperType();

//新方法

SubType.prototype.getSubValue = function (){

    return this.subproperty;

};

//重写现有方法

SubType.prototype.getSuperValue = function (){

    return false;

};

var instance = new SubType();

alert(instance.getSuperValue());   //false
```

### PrototypeChainingExample02.htm

在此代码中，高亮区域显示了两个方法。第一个是 `getSubValue()`，它是 `SubType` 的一个新方法。第二个是 `getSuperValue()`，它已经存在于原型链中，但在此处被屏蔽（shadowed）。当在 `SubType` 实例上调用 `getSuperValue()` 时，它将调用这一个，但 `SuperType` 的实例仍然会调用原始方法。需要注意的是，这两个方法都是在原型赋值为 `SuperType` 实例之后定义的。

另一个需要理解的重要点是，使用对象字面量的方法来创建原型方法不能与原型链结合使用，因为你最终会覆盖掉整个原型链。这里有一个示例：

![image](img/logo1.gif)

```javascript
function SuperType(){

    this.property = true;

}

SuperType.prototype.getSuperValue = function(){

    return this.property;

};

function SubType(){

    this.subproperty = false;

}

//继承自 SuperType

SubType.prototype = new SuperType();

//尝试添加新方法 - 这会使上一行代码

SubType.prototype = {

    getSubValue : function (){

        return this.subproperty;

    },

    someOtherMethod : function (){

        return false;

    }

};

var instance = new SubType();

alert(instance.getSuperValue());   //error!
```

### PrototypeChainingExample03.htm

在此代码中，原型在被赋值为 `SuperType` 实例后，又被重新赋值为一个对象字面量。现在原型包含的是 `Object` 的新实例，而不是 `SuperType` 的实例，因此原型链被断开了——`SubType` 和 `SuperType` 之间没有了关系。

#### 原型链的问题

尽管原型链是强大的继承工具，但它并非没有问题。主要问题围绕包含引用值的原型。回想之前，包含引用值的原型属性是所有实例共享的；这就是为什么属性通常在构造函数内部定义，而不是在原型上。在使用原型实现继承时，原型实际上变成了另一个类型的实例，这意味着曾经是实例属性的内容现在变成了原型属性。下面的示例突出了这个问题：

![image](img/logo1.gif)

```javascript
function SuperType(){

    this.colors = ["red", "blue", "green"];

}

function SubType(){            

}

//继承自 SuperType

SubType.prototype = new SuperType();

var instance1 = new SubType();

instance1.colors.push("black");

alert(instance1.colors);    //"red,blue,green,black"

var instance2 = new SubType();

alert(instance2.colors);    //"red,blue,green,black"
```

### PrototypeChainingExample04.htm

在此示例中，`SuperType` 构造函数定义了一个包含数组（引用值）的属性 `colors`。每个 `SuperType` 实例都有自己的 `colors` 属性，包含它们自己的数组。当 `SubType` 通过原型链继承自 `SuperType` 时，`SubType.prototype` 变成了 `SuperType` 的实例，因此它获得了自己的 `colors` 属性，这类似于专门创建了 `SubType.prototype.colors`。最终结果是：`SubType` 的所有实例共享同一个 `colors` 属性。这一点表现为：对 `instance1.colors` 的更改反映在了 `instance2.colors` 上。

原型链的第二个问题是，在创建子类实例时，无法向父类构造函数传递参数。事实上，没有办法可以在不影响所有对象实例的情况下向父类构造函数传递参数。由于这个问题以及上述原型上引用值的问题，原型链很少单独使用。

#### 构造函数窃取（Constructor Stealing）

为了解决原型上引用值的继承问题，开发者开始使用一种名为构造函数窃取（有时称为对象伪装或经典继承）的技术。基本思想非常简单：在子类构造函数内部调用父类构造函数。考虑到函数只是在特定上下文中执行代码的对象，可以使用 `apply()` 和 `call()` 方法在新创建的对象上执行构造函数，如下例所示：

```javascript
function SuperType(){

    this.colors = ["red", "blue", "green"];

}

function SubType(){  

    //继承自 SuperType

    SuperType.call(this);

}

var instance1 = new SubType();

instance1.colors.push("black");

alert(instance1.colors);    //"red,blue,green,black"

var instance2 = new SubType();

alert(instance2.colors);    //"red,blue,green"
```

### ConstructorStealingExample01.htm

示例中的高亮行显示了构造函数窃取中使用的单个调用。通过使用 `call()` 方法（或者使用 `apply()`），在新创建的实例上下文中调用 `SuperType` 构造函数。这样做实际上是在新的 `SubType` 对象上运行了 `SuperType()` 函数的所有对象初始化代码。结果是每个实例都有 `colors` 属性的副本。

#### 参数传递

构造函数窃取相对于原型链的一个优势是可以从子类构造函数向父类构造函数传递参数。考虑以下内容：

![image](img/logo1.gif)

```javascript
function SuperType(name){

    this.name = name;

}

function SubType(){  

    //传递参数继承自 SuperType

    SuperType.call(this, "Nicholas");

    //实例属性

    this.age = 29;

}

var instance = new SubType();

alert(instance.name);    //"Nicholas";

alert(instance.age);     //29
```

### ConstructorStealingExample02.htm

完全使用构造函数窃取的缺点是，它引入了与自定义类型使用构造函数模式相同的问题：方法必须定义在构造函数内部，因此没有函数复用。此外，定义在父类原型上的方法在子类上无法访问，因此所有类型都只能使用构造函数模式。由于这些问题，构造函数窃取很少单独使用。

## 组合继承

组合继承（Combination inheritance，有时也称为伪类继承）结合了原型链和构造函数借用（constructor stealing），以兼顾两者的优点。其基本思想是使用原型链来继承原型上的属性和方法，并使用构造函数借用来继承实例属性。这允许通过在原型上定义方法来实现函数复用，并允许每个实例都拥有自己的属性。考虑以下代码：

![image](img/logo1.gif)

```javascript
function SuperType(name){

    this.name = name;

    this.colors = ["red", "blue", "green"];

}

SuperType.prototype.sayName = function(){

    alert(this.name);

};

function SubType(name, age){  

    //继承属性

    SuperType.call(this, name);

    this.age = age;

}

//继承方法

SubType.prototype = new SuperType();

SubType.prototype.sayAge = function(){

    alert(this.age);

};

var instance1 = new SubType("Nicholas", 29);

instance1.colors.push("black");

alert(instance1.colors);  //"red,blue,green,black"

instance1.sayName();      //"Nicholas";

instance1.sayAge();       //29

var instance2 = new SubType("Greg", 27);

alert(instance2.colors);  //"red,blue,green"

instance2.sayName();      //"Greg";

instance2.sayAge();       //27
```



`CombinationInheritanceExample01.htm`

在这个示例中，`SuperType` 构造函数定义了两个属性 `name` 和 `colors`，而 `SuperType` 原型有一个名为 `sayName()` 的方法。`SubType` 构造函数调用了 `SuperType` 构造函数并传递了参数 `name`，同时定义了自己的属性 `age`。此外，`SubType` 的原型被赋值为 `SuperType` 的一个实例，然后定义了一个新方法 `sayAge()`。通过这段代码，可以创建两个独立的 `SubType` 实例，它们拥有自己的属性（包括 `colors` 属性），但都使用相同的方法。

组合继承解决了原型链和构造函数借用的缺点，是 JavaScript 中最常用的继承模式。它还保留了 `instanceof` 和 `isPrototypeOf()` 的行为，用于识别对象的组成情况。

## 原型继承（Prototypal Inheritance）

2006 年，Douglas Crockford 编写了一篇名为《JavaScript 中的原型继承》的文章，在其中引入了一种不涉及使用严格定义构造函数的继承方法。他的前提是，原型允许你基于现有对象创建新对象，而无需定义自定义类型。他为此引入的函数如下：

![image](img/logo1.gif)

```javascript
function object(o){

    function F(){}

    F.prototype = o;

    return new F();

}
```

`object()` 函数创建了一个临时构造函数，将给定的对象赋值为构造函数的原型，并返回该临时类型的新实例。本质上，`object()` 对传入的任何对象执行了影子拷贝。考虑以下代码：

```javascript
var person = {

    name: "Nicholas",

    friends: ["Shelby", "Court", "Van"]

};

var anotherPerson = object(person);

anotherPerson.name = "Greg";

anotherPerson.friends.push("Rob");

var yetAnotherPerson = object(person);

yetAnotherPerson.name = "Linda";

yetAnotherPerson.friends.push("Barbie");

alert(person.friends);   //"Shelby,Court,Van,Rob,Barbie"
```

`PrototypalInheritanceExample01.htm`

这正是 Crockford 提倡使用原型继承的方式：你有一个想要作为另一个对象基础的对象。该对象应该被传递给 `object()`，并对结果对象进行相应的修改。在这个示例中，`person` 对象包含了应该在另一个对象上可用的信息，因此它被传入 `object()` 函数，该函数返回一个新对象。新对象以 `person` 为其原型，意味着它在原型上同时拥有一个原始值属性和一个引用值属性。这也意味着 `person.friends` 不仅被 `person` 共享，还与 `anotherPerson` 和 `yetAnotherPerson` 共享。实际上，这段代码创建了 `person` 的两个克隆。

ECMAScript 5 通过添加 `Object.create()` 方法正式化了原型继承的概念。该方法接受两个参数：一个作为新对象原型的对象，以及一个定义应用到新对象的额外属性的可选对象。当使用一个参数时，`Object.create()` 的行为与 `object()` 方法相同：

![image](img/logo1.gif)

```javascript
var person = {

    name: "Nicholas",

    friends: ["Shelby", "Court", "Van"]

};

var anotherPerson = Object.create(person);

anotherPerson.name = "Greg";

anotherPerson.friends.push("Rob");

var yetAnotherPerson = Object.create(person);

yetAnotherPerson.name = "Linda";

yetAnotherPerson.friends.push("Barbie");

alert(person.friends);   //"Shelby,Court,Van,Rob,Barbie"
```

`PrototypalInheritanceExample02.htm`

`Object.create()` 的第二个参数与 `Object.defineProperties()` 的第二个参数格式相同：每个要定义的额外属性都与其属性描述符一起指定。以这种方式指定的任何属性将遮蔽原型对象上同名的属性。例如：

```javascript
var person = {

    name: "Nicholas",

    friends: ["Shelby", "Court", "Van"]

};

var anotherPerson = Object.create(person, {

    name: {

        value: "Greg"

    }

});

alert(anotherPerson.name);  //"Greg"
```

`PrototypalInheritanceExample03.htm`

`Object.create()` 方法支持 Internet Explorer 9+、Firefox 4+、Safari 5+、Opera 12+ 以及 Chrome。原型继承在不需要构造函数的开销但仍需要类似对象时非常有用。注意，包含引用值的属性将始终共享这些值，类似于使用原型。

## 寄生继承（Parasitic Inheritance）

与原型继承密切相关的是寄生继承，这是另一种由 Crockford 推广的模式。寄生继承背后的思想与寄生构造和工厂模式相似：创建一个函数执行继承，以某种方式增强对象，然后像这样做一样返回对象。基本的寄生继承模式如下：

```javascript
function createAnother(original){

    var clone = object(original);     //通过调用函数创建新对象

    clone.sayHi = function(){         //某种方式增强对象

        alert("hi");

    };

    return clone;                     //返回对象

}
```

在代码中，`createAnother()` 函数接收一个参数，即作为新对象基础的对象。该对象 `original` 被传入 `object()` 函数，结果赋值给 `clone`。接下来，修改 `clone` 对象以包含一个名为 `sayHi()` 的新方法。最后一步是返回对象。`createAnother()` 函数可以如下所示使用：

```javascript
var person = {

    name: "Nicholas",

    friends: ["Shelby", "Court", "Van"]

};

var anotherPerson = createAnother(person);

anotherPerson.sayHi();  //"hi"
```

此示例中的代码返回了一个基于 `person` 的新对象。`anotherPerson` 对象拥有 `person` 的所有属性和方法，但增加了一个名为 `sayHi()` 的新方法。

寄生继承是在主要关注对象而不是自定义类型和构造函数时的另一种模式。寄生继承不需要 `object()` 方法；任何返回新对象的函数都符合该模式。

注意，使用寄生继承向对象添加函数会导致与函数复用相关的低效问题，类似于构造函数模式。

## 寄生组合继承（Parasitic Combination Inheritance）

组合继承（Combination inheritance）是 JavaScript 中最常用的继承模式，尽管它并非没有低效之处。该模式最低效的部分是超类型的构造函数总是被调用两次：一次用于创建子类的原型（prototype），另一次是在子类构造函数内部。本质上，子类原型最终拥有超类型对象的所有实例属性，但在子类构造函数执行时，这些属性又会被覆盖。再次考虑组合继承的示例：

```javascript
function SuperType(name){

    this.name = name;

    this.colors = ["red", "blue", "green"];

}

SuperType.prototype.sayName = function(){

    alert(this.name);

};

function SubType(name, age){  

    SuperType.call(this, name);          // 第二次调用 SuperType()

    this.age = age;

}

SubType.prototype = new SuperType();     //第一次调用 SuperType()

SubType.prototype.constructor = SubType;                   

SubType.prototype.sayAge = function(){

    alert(this.age);

};
```

高亮的代码行表示了 `SuperType` 构造函数的执行时机。当这段代码执行时，`SubType.prototype` 最终拥有两个属性：`name` 和 `colors`。这些是 `SuperType` 的实例属性，但它们现在位于 `SubType` 的原型上。当调用 `SubType` 构造函数时，`SuperType` 构造函数也会被调用，这会在新对象上创建实例属性 `name` 和 `colors`，从而遮蔽原型上的属性。图 6-6 阐了这个过程。

图 6-6

![image](img/f213-01.jpg)

你可以看到存在两组 `name` 和 `colors` 属性：一组在实例上，一组在 `SubType` 原型上。这是调用两次 `SuperType` 构造函数的结果。幸运的是有一种解决方法。

寄生组合继承（Parasitic combination inheritance）使用构造函数窃（constructor stealing）来继承属性，但使用原型链的混合形式来继承方法。其基本思想是：不再通过调用超类型构造函数来分配子类的原型，你只需要超类型原型的副本。本质上，使用寄生继承从超类型的原型进行继承，然后将结果分配给子类的原型。寄生组合继承的基本模式如下：

```javascript
function inheritPrototype(subType, superType){

    var prototype = object(superType.prototype);   // 创建对象

    prototype.constructor = subType;               // 修改对象

    subType.prototype = prototype;                 // 分配对象

}
```

`inheritPrototype()` 函数实现了基础的寄生组合继承。该函数接受两个参数：子类构造函数和超类型构造函数。在函数内部，第一步是创建一个超类型型的克隆。接下来，将 `constructor` 属性分配给 `prototype`，以补偿原型被覆盖时丢失默认构造函数属性。最后，将子类的原型分配给新创建。调用 `inheritPrototype()` 可以替换之前示例中的子类原型赋值，如下：

![image](img/logo1.gif)

```javascript
function SuperType(name){

    this.name = name;

    this.colors = ["red", "blue", "green"];

}

SuperType.prototype.sayName = function(){

    alert(this.name);

};

function SubType(name, age){  

    SuperType.call(this, name);

    this.age = age;

}

inheritPrototype(SubType, SuperType);

SubType.prototype.sayAge = function(){

    alert(this.age);

};
```

`ParasiticCombinationInheritanceExample01.htm`

这个示例效率更高，因为 `SuperType` 构造函数只调用了一次，避免了在 `SubType.prototype` 上产生不需要且未使用的属性。此外，原型链保持完完整，因此 `instanceof` 和 `isPrototypeOf()` 的行为与正常一致。寄生组合继承被认为是引用类型最优的继承范式。

![image](img/pen.gif)

Yahoo! 用户界面 (YUI) 库首次通过 `Y.extend()` 方法在广泛分发的 JavaScript 库中包含了寄生组合继承。有关 YUI 的更多信息，请访问 [`yuilibrary.com/`](http://yuilibrary.com/)。

## 总结

ECMAScript 支持不使用类或接口的面向对象（OO）编程。对象在代码执行的任何一点被创建和增强，使对象成为动态实体而非严格定义的实体。在创建对象时，使用了以下模式代替类：

*   工厂模式（factory pattern）使用简单的函数来创建对象、分配属性和方法，然后返回对象。该模式在构造函数模式出现后不再受到青睐。
*   使用构造函数模式，可以定义自定义的引用类型，可以使用 `new` 运算符像创建内置对象实例一样创建它们。然而，构造函数模式有一个缺点，即它的任何成员（包括函数）都没有被重用。由于函数可以以松类型的方式编写，没有理由它们不能被多个对象实例共享。
*   原型模式（prototype pattern）考虑了这一点，使用构造函数的 `prototype` 属性来分配应该共享的属性和方法。组合构造/原型模式使用构造函数定义实例属性，使用原型模式定义共享属性和方法。

JavaScript 中的继承主要通过原型链的概念实现。原型链涉及将构造函数的原型赋值为另一个类型的实例。通过这种方式，子类假设超类型的所有属性和方法，类似于基于类的继承。原型链的问题是所有继承的属性和方法在对象实例间共享，因此单独使用它并不理想。构造函数窃模式解决了这些问题，在子类构造函数内部调用超类型构造函数。这允许每个实例拥有自己的属性，但强制要求使用构造函数模式定义类型。还有其他的继承模式：

*   原型继承（prototypal inheritance）在不需要预定义构造的情况下实现继承，本质上是对给定对象进行浅克隆操作。操作的结果可以进一步增强。
*   与之密切相关的是寄生继承（parasitic inheritance），它是基于另一个对象或某些信息创建对象、增强并返回对象的模式。该模式也被重新用于组合继承，以消除与超类型构造函数调用次数相关的低效。
*   寄生组合继承被认为是实现类型继承的最有效方式。

# 第 7 章：函数表达式

## 本章内容

*   函数表达式的特点
*   函数的递归
*   使用闭包的私有变量

JavaScript 中最强大且经常令人困惑的部分之一是函数表达式。正如第 5 章提到的，定义函数有两种方式：函数声明和函数表达式。第一种是函数声明，其形式如下：

```javascript
function functionName(arg0, arg1, arg2) {

    //函数体

}
```

函数名紧跟在 `function` 关键字之后，这就是函数命名的方式。Firefox、Safari、Chrome 和 Opera 都在函数上提供了一个非标准的 `name` 属性，用于暴露赋值的名称。该值始终等于紧跟在 `function` 关键字之后的标识符：

![image](img/logo1.gif)

```javascript
//仅在 Firefox, Safari, Chrome 和 Opera 中有效

alert(functionName.name);    //"functionName"
```

`FunctionNameExample01.htm`

函数声明的一个关键特性是**函数声明提升**（function declaration hoisting），即函数声明在代码执行之前就会被读取。这意味着函数声明可以出现在调用它的代码之后，并且仍然正常工作：

![image](img/logo1.gif)

```javascript
sayHi();

function sayHi(){

    alert("Hi!");

}
```

`FunctionDeclarationHoisting01.htm`

这个示例不会报错，因为函数声明在代码开始执行之前被首先读取。

创建函数的另一种方法是使用**函数表达式**（function expression）。函数表达式有多种形式，最常见如下：

```javascript
var functionName = function(arg0, arg1, arg2){

    //函数体

};
```

这种函数表达式模式看起来像普通的变量赋值。一个函数被创建并赋值给变量 `functionName`。创建的函数被认为是一个**匿名函数**，因为在 `function` 关键字之后没有标识符。（匿名函数有时也被称为 lambda 函数。）这意味着 `name` 属性是一个空字符串。

函数表达式的作用与其他表达式类似，因此必须在使用之前对其进行赋值。以下代码会导致错误：

```javascript
sayHi();    //错误 - 函数尚不存在

var sayHi = function(){

    alert("Hi!");

};
```



理解函数提升是理解函数声明与函数表达式之间差异的关键。例如，以下代码的结果可能会令你大乎意料：

```
//千万不要这样做！

if(condition){

    function sayHi(){

        alert("Hi!");

    }

} else {

    function sayHi(){

        alert("Yo!");

    }

}
```

`FunctionDeclarationsErrorExample01.htm`

代码似乎表明，如果`condition`为真，则对`sayHi()`使用一种定义；否则，使用另一个不同的定义。事实上，这在 ECMAScript 中并不是有效的语法，因此 JavaScript 引擎会尝试纠错到一个适当的状态。问题在于，浏览器在在这种情况下并不会一致地进行纠错。大多数浏览器无论`condition`是如何，都会返回第二个声明；而 Firefox 在`condition`为真时返回第一个声明。这种模式是危险的，不应该被使用。然而，以这种方式使用函数表达式是完全可以：

```
//这是可以的

var sayHi;

if(condition){

    sayHi = function(){

        alert("Hi!");

    };

} else {

    sayHi = function(){

        alert("Yo!");

    };

}
```

这个示例的行为符合你的预期，根据`condition`的值将正确的函数表达式赋值给变量`sayHi`。

创建函数并赋值给变量的能力还允许你将函数作为其他函数的返回值。回想一下第 5 章中的`createComparisonFunction()`示例：

```
function createComparisonFunction(propertyName) {

    return function(object1, object2){

        var value1 = object1[propertyName];

        var value2 = object2[propertyName];

        if (value1 < value2){

            return -1;

        } else if (value1 > value2){

            return 1;

        } else {

            return 0;

        }

    };

}
```

`createComparisonFunction()`返回了一个匿名函数。返回的函数可能会被赋值给变量或在其他调用，但在`createComparisonFunction()`内部它是匿名的。每当函数被用作值时，它就是一个函数表达式。然而，这些并不是函数表达式的唯一用途，正如本章后续内容所示。

## 递归 (RECURION)

递归函数通常在函数通过名称调用自身时形成，如下例所示：

![image](img/logo1.gif)

```
function factorial(num){

    if (num <= 1){

        return 1;

    } else {

        return num * factorial(num-1);

    }

}
```

`RecursionExample01.htm`

这是一个经典的递归阶乘函数。虽然它最初可以工作，但如果在其之后立即运行以下代码，可能会阻止其运行：

```
var anotherFactorial = factorial;

factorial = null;

alert(anotherFactorial(4));  //错误！
```

`RecursionExample01.htm`

在这里，`factorial()`函数被存储在一个名为`anotherFactorial`的变量中。然后将`factorial`变量设置为`null`，因此只留了一个对原始函数的引用。当调用`anotherFactorial()`时，将会导致错误，因为它会尝试执行`factorial()`，而它已经不再是一个函数了。使用`arguments.callee`可以缓解这个问题。

回想`arguments.callee`是指向正在执行的函数的指针，因此可以使用它来递归地调用函数，如下所示：

```
function factorial(num){

    if (num <= 1){

        return 1;

    } else {

        return num * arguments.callee(num-1);

    }

}
```

`RecursionExample02.htm`

将高亮行改为使用`arguments.callee`而不是函数名，可以确保无论如何访问，该函数都能正常工作。在编写递归函数时，建议始终使用函数名的`arguments.callee`。

`arguments.callee`的值在严格模式下运行的脚本中是不可访问的，如果尝试读取它将导致错误。相反，你可以使用命名函数表达式来实现相同的结果。例如：

```
var factorial = (function f(num){

    if (num <= 1){

        return 1;

    } else {

        return num * f(num-1);

    }

});
```

在此代码中，创建了一个命名函数表达式`f()`并赋值给变量`factorial`。即使函数被赋值给另一个变量，`f`的名称保持不变，因此递归调用始终正确执行。

## 闭包 (CLOSURES)

匿名函数和闭包经常被混用。闭包是可以访问另一个函数作用域变量的。这通常通过在函数内部创建函数来实现，正如之前`createComparisonFunction()`示例中的以下高亮行所示：

```
function createComparisonFunction(propertyName) {

    return function(object1, object2){

        var value1 = object1[propertyName];

        var value2 = object2[propertyName];

        if (value1 < value2){

            return -1;

        } else if (value1 > value2){

            return 1;

        } else {

            return 0;

        }

    };

}
```

此示例中的高亮行是内部函数（匿名函数）的一部分，它正在访问来自外部函数的变量（`propertyName`）。即使在内部函数被返回并在其他地方使用后，它仍然可以访问该变量。这是因为内部函数的作用链包含了`createComparisonFunction()`的作用域。为了理解为什么这是可能的，请考虑函数第一次被调用时发生了什么。

第 4 章引入了作用域链的概念。作用链如何创建和使用的细节对于良好理解闭包很重要。当函数被调用时，会创建一个执行上下文并创建其作用域链。函数的激活对象用参数和任何命名参数进行初始化。外部函数的激活对象是作用链中的第二个对象。

当函数执行时，会在作用域链中查找变量以读取或写入值。考虑以下代码：

```javascript
function compare(value1, value2){

    if (value1 < value2){

        return -1;

    } else if (value1 > value2){

        return 1;

    } else {

        return 0;

    }

}

var result = compare(5, 10);
```

这段代码定义了一个名为`compare()`的函数，并在全局执行上下文中调用。当第一次调用`compare()`时，会创建一个新的激活对象，其中包含参数`value1`和`value2`。全局执行上下文的变量对象紧随位于`compare()`执行上下文的作用域链中，该链包含了`result`和`compare`。图 7-1 阐了这种关系。

图 7-1

![image](img/f222-01.jpg)

在幕后，一个对象代表每个执行上下文中的变量。全局上下文的变量对象始终存在，而局部上下文变量对象（如`compare()`的对象）仅在函数执行期间存在。当`compare()`被定义时，它的作用域链被创建，并预加载全局变量对象，然后保存到内部的`[[Scope]]`属性中。当函数被调用时，会创建一个执行上下文，并通过复制函数`[[Scope]]`属性中的对象来构建其作用域链。之后，会创建一个激活对象（同时也充当变量对象）并将其推到上下文作用域链的最前端。在这个示例中，这意味着`compare()`函数的执行上下文的作用域链中有两个变量对象：局部激活对象和全局变量对象。请注意，作用域链本质上是一个指向变量对象的指针列表，并不物理上包含这些对象。

每当在函数内部访问变量时，都会在作用域链中搜索具有给定名的变量。一旦函数完成，局部激活对象就会被销毁，内存中只留下全局作用域。然而，闭包的行为则不同。

定义在另一个函数内部的函数会将包含该函数的函数的激活对象添加到其作用域链中。因此，在`createComparisonFunction()`中，匿名函数的作用域链实际上包含了对`createComparisonFunction()`激活对象的引用。图 7-2 在执行以下代码时阐明了这种关系：

图 7-2

![image](img/f223-01.jpg)

```javascript
var compare = createComparisonFunction("name");

var result = compare({ name: "Nicholas" }, { name: "Greg" });
```

当匿名函数从`createComparisonFunction()`返回时，它的作用域链已初始化为包含来自`createComparisonFunction()`的激活对象和全局变量对象。这使得匿名函数可以访问`createComparisonFunction()`的所有变量。另一个有趣的副作用是，一旦函数执行完毕，`createComparisonFunction()`的激活对象无法被销毁，因为在匿名函数的作用域链中仍然存在引用。在`createComparisonFunction()`完成后，其执行上下文的作用域链会被销毁，但其激活对象将一直留在内存中，直到匿名函数被销毁，如下所示：

```javascript
//创建函数

var compareNames = createComparisonFunction("name");

//调用函数

var result = compareNames({ name: "Nicholas" }, { name: "Greg"});

// 取消函数引用 - 现在可以回收内存

compareNames = null;
```

在这里，比较函数被创建并存储在变量`compareNames`中。将`compareNames`设置为`null`会取消对函数的引用并允许垃圾回收程序对其进行清理。随后作用域链将被销毁，所有的作用域（全局作用域外）都可以被安全地销毁。图 7-2 显示了在此示例中调用`compareNames()`时发生的作用域链关系。

![image](img/pen.gif)

由于闭包携带了包含它的函数的作用域，它们占用的内存比其他函数更多。过度使用闭包会导致内存消耗过度，因此建议仅在绝对必要时才使用它们。JavaScript 引擎（如 V8）会尝试回收因闭包而被捕获的内存，但仍建议在使用闭包时保持小心。

### 闭包与变量

这种作用域链配置有一个显著的副作用。闭包总是获取包含它的函数的任何变量的最后一个值。记住，闭包存储的是整个变量对象的引用，而不仅仅是某个特定的变量。这个问题在以下示例中得到了清楚的展示：

![image](img/logo1.gif)

```javascript
function createFunctions(){

    var result = new Array();

    for (var i=0; i < 10; i++){

        result[i] = function(){

            return i;

        };

    }

    return result;

}
```

`ClosureExample01.htm`

此函数返回一个函数数组。似乎每个函数应该只返回其索引的值，因此位置 0 的函数返回 0，位置 1 的函数返回 1，依此类推。实际上，每个函数都返回 10。由于每个函数的作用域链中都有`createFunctions()`的激活对象，它们都引用同一个变量`i`。当`createFunctions()`运行时，`i`的值为 10，由于每个函数都引用存在`i`的变量对象，因此每个函数内部的`i`值都是 10。然而，你可以通过如下创建另一个函数来强制闭包按预期行为：

```javascript
function createFunctions(){

    var result = new Array();

    for (var i=0; i < 10; i++){

        result[i] = function(num){

            return function(){

                return num;

            };

        }(i);

    }

    return result;

}
```

`ClosureExample02.htm`

在这个版本的`createFunctions()`中，每个函数返回不同的数字。我们没有直接将闭包赋值给数组，而是定义并立即调用了一个匿名函数。匿名函数有一个参数`num`，它是结果函数应该返回的数字。变量`i`作为参数传递给匿名函数。由于函数参数按值传递，`i`的当前值被复制到参数`num`中。在匿名函数内部，创建并返回了一个访问`num`的闭包。现在结果数组中的每个函数都有自己的`num`副本，因此可以返回不同的数字。

### this 对象

`this`绑定。在全局函数运行时，非严格模式下`this`等于`window`，在严格模式下为`undefined`；而当作为对象方法调用时，`this`等于该对象。匿名函数在此上下文中没有绑定到对象，这意味着`this`对象指向`window`，除非在严格模式下执行（此时`this`为`undefined`）。然而，由于闭包的编写方式，这一事实并不显而易见。考虑以下内容：

![image](img/logo1.gif)

```javascript
var name = "The Window";

var object = {

    name : "My Object",

    getNameFunc : function(){

        return function(){

            return this.name;

        };

    }

};

alert(object.getNameFunc()());  //"The Window" (非严格模式下)
```

`ThisObjectExample01.htm`

在这里，创建了一个名为`name`的全局变量，并创建了一个包含名为`name`属性的对象。该对象包含一个名为`getNameFunc()`的方法，该方法返回一个匿名函数，该函数返回`this.name`。由于`getNameFunc()`返回的是一个函数，调用`object.getNameFunc()()`会立即调用返回的函数，该函数返回一个字符串。然而，在这种情况下，它返回的是 "The Window"，这是全局变量`name`的值。为什么匿名函数没有获取包含它的作用域的`this`对象呢？

记住，每个函数在被调用时会自动获得两个特殊变量：`this`和`arguments`。内部函数永远无法从外部函数直接访问这些变量。可以通过将`this`存在闭包可以访问的另一个变量中，允许闭包访问不同的`this`对象，例如所示：

![image](img/logo1.gif)

```
var name = "The Window";

var object = {

    name : "My Object",

    getNameFunc : function(){

        var that = this;

        return function(){

            return that.name;

        };

    }

};

alert(object.getNameFunc()());  //"My Object"
```



### ThisObjectExample02.htm

高亮的两行显示了此示例与上一个的区别。在定义匿名函数之前，一个名为`that`的变量被赋值为`this`对象。当定义闭包时，它可以访问`that`，因为它是包含函数中唯一命名的变量。即使在函数返回后，`that`仍然绑定到`object`，因此调用`object.getNameFunc()()`返回的是"My Object"。

![image](img/pen.gif)

`this`和`arguments`的行为都是如此。如果你想访问包含作用域的`arguments`对象，你需要将引用保存到另一个闭包可以访问的变量中。

在某些少数特殊情况下，`this`的值最终可能与你预期的值不同。考虑对上一个示例进行以下修改：

```
var name = "The Window";

var object = {

    name : "My Object",

    getName: function(){

        return this.name;

    }

};
```

`getName()`方法简单地返回`this.name`的值。以下是调用`object.getName()`的各种方式及其结果：

```
object.getName();     //"My Object"

(object.getName)();   //"My Object"

(object.getName = object.getName)();   //"The Window" 在非严格模式
```

### ThisObjectExample03.htm

第一行以你通常的方式调用`object.getName()`，因此返回"My Object"，因为`this.name`与`object.name`相同。第二行在调用`object.getName`之前在其周围加上了括号。虽然这看起来像只是对函数的引用，但`this`的值被保留了，因为`object.getName`和`(object.getName)`被定义为等价的。第三行执行了赋值然后调用了结果。由于此赋值表达式的值是函数本身，`this`值没有被保留，因此返回了"The Window"。

你不太可能有意使用第二行或第三行中的模式，但了解当语法发生细微变化时，`this`的值可能会以意想不到的方式发生变化是有帮助的。

## 内存泄漏

由于闭包的工作机制在第9版之前的Internet Explorer中导致了特定问题，因为JScript对象和COM对象使用了不同的垃圾回收例（在第4章中讨论）。存储一个HTML元素的作用域可以有效地确保该元素无法被销毁。考虑以下内容：

```
function assignHandler(){

    var element = document.getElementById("someElement");

    element.onclick = function(){

        alert(element.id);

    };

}
```

这段代码在`element`上创建了一个作为事件处理程序的闭包，这反过来创建了一个循环引用（事件在第13章中讨论）。匿名函数保留了`assignHandler()`函数激活对象的引用，这阻止了`element`引用数的减少。只要匿名函数存在，`element`的引用计数将至少为1，这意味着内存永远不会被回收。这种情况可以通过稍微修改代码来解决，如下所示：

```javascript
function assignHandler(){

    var element = document.getElementById("someElement");

    var id = element.id;

    element.onclick = function(){

        alert(id);

    };

    element = null;

}
```

在这个版本的代码中，`element`的ID副本被存储在闭包使用的变量中，消除了循环引用。然而，仅此一步还不足以防止内存问题。记住：闭包拥有对包含函数的整个激活对象的引用，其中包含了`element`。即使闭包没有直接引用`element`，引用仍然存储在包含函数的激活对象中。因此，将`element`变量设为`null`是必要的。这消除了对COM对象的引用并减少了它的引用计数，确保了内存在适当的时候可以被回收。

## 模拟块作用域

如之前所述，JavaScript没有块级作用域的概念，这意味着在块语句内部定义的变量实际上创建在包含它的函数，而不是语句内部。考虑以下内容：

![image](img/logo1.gif)

```javascript
function outputNumbers(count){

    for (var i=0; i < count; i++){

        alert(i);

    }

    alert(i);   //count

}
```

### BlockExample01.htm

在这个函数中定义了一个for循环，变量`i`被初始化为0。对于Java和C++等语言，变量`i`只定义在块语句中，因此当循环结束时变量就会被销毁。然而在JavaScript中，`i`被定义为`outputNumbers()`激活对象的一部分，这意味着从那时起在函数内部是可以访问的。即使是后面对变量的错误声明也不会清除它的值：

```javascript
function outputNumbers(count){

    for (var i=0; i < count; i++){

        alert(i);

    }

    var i;  //变量重声明

    alert(i);   //count

}
```

BlockExample02.htm

JavaScript永远不会告诉你多次声明了同一个变量；它只是忽略随后的声明（尽管它会尊重初始化）。匿名函数可以模拟块作用域并避免此类问题。

作为块作用域（通常称为私有作用域）使用的匿名函数的基本语法如下：

```
(function(){

    //块代码

})();
```

这种语法定义了一个立即调用的匿名函数，称为立即执行函数。像函数声明的形式被括号括起来以表示它实际上是一个函数表达式。该函数通过最后的第二组括号进行调用。如果这种语法让你感到困惑，请考虑以下示例：

```javascript
var count = 5;

outputNumbers(count);
```

在这个示例中，变量`count`被初始化为5。当然，由于值是直接传递给函数的，所以这个变量是不必要的。为了让代码更简洁，在调用函数时可以用值5替换变量`count`：

```
outputNumbers(5);
```

这与上一个示例的效果相同，因为变量只是另一个值的表示，所以可以用实际值替换变量，且代码运行良好。现在考虑以下内容：

```
var someFunction = function(){

    //块代码

};

someFunction();
```

在这个示例中，定义了一个函数并立即调用了它。创建了一个匿名函数并将其赋值给变量`someFunction`。然后通过在函数名后加上括号来调用该函数，变为`someFunction()`。记得在上一个示例中，变量`count`可以被替换为它的实际值；在这里也可以进行相同的操作。然而，以下代码将无法运行：

```
function(){

    //block code here

}();   //error!
```

这段代码会导致语法错误，因为JavaScript将`function`关键字视为函数声明的开始，而函数声明后面不能紧跟括号。然而，函数表达式（Function expressions）后面可以紧跟括号。要将函数声明转换为函数表达式，你只需要像这样用括号将其括起来即可：

```
(function(){

    //block code here

})();
```

这些私有作用域可以在任何需要临时变量的地方使用，例如示例所示：

![image](img/logo1.gif)

```
function outputNumbers(count){

    (function () {

        for (var i=0; i < count; i++){

            alert(i);

        }

    })();

    alert(i);   //causes an error

}
```

BlockScopeExample03.htm

在重写后的`outputNumbers()`函数中，`for`循环周围插入了一个私有作用域。在匿名函数内部定义的任何变量在执行完成后都会被销毁，因此变量`i`在循环中使用后会被销毁。`count`变量在私有作用域内部是可以的，因为匿名函数是一个闭包，具有访问包含作用域变量的完全权限。

这种技术通常用于函数外部的全局作用域，以限制添加到全局作用域的变量和函数的数量。通常你希望避免向全局作用域添加变量和函数，特别是在有多个开发者的大型应用程序中，以避免命名冲突。私有作用域允许每个开发者使用自己的变量而不必担心污染全局作用域。考虑这个示例：

```
(function(){

    var now = new Date();

    if (now.getMonth() == 0 && now.getDate() == 1){

        alert("Happy new year!");

    }

})();
```

将此代码放在全局作用域中，可以提供判断今天是否为1月1日的功能，如果是，则向用户显示消息。变量`now`变成了一个匿名函数的局部变量，而不是在全局作用域中创建。

![image](img/pen.gif)

这种模式限制了闭包内存问题，因为没有对匿名函数的引用。因此，在函数完成后，作用域链可以立即被销毁。

## 私有变量

严格来说，JavaScript没有私有成员的概念；所有对象属性都是公共的。然而，存在私有变量的概念。任何定义在函数内部的变量都被视为私有的，因为它们在函数外部是不可访问的。这包括函数参数、局部变量以及定义在其他函数内部的函数。考虑以下：

```
function add(num1, num2){

    var sum = num1 + num2;

    return sum;

} 
```

在这个函数中，有三个私有变量：`num1`、`num2`和`sum`。这些变量在函数内部可以访问，但在函数外部无法访问。如果在这个函数内部创建一个闭包，它将通过其作用域链访问这些变量。利用这一知识，你可以创建可以访问私有变量的公共方法。

特权方法（Privileged method）是一种可以访问私有变量和/或私有函数的公共方法。在对象上创建特权方法有两种方法。第一是在构造函数内部进行，如示例所示：

```
function MyObject(){

    //private variables and functions

    var privateVariable = 10;

    function privateFunction(){

        return false;

    }

    //privileged methods

    this.publicMethod = function (){

        privateVariable++;

        return privateFunction();

    };

}
```

这种模式在构造函数内部定义了所有私有变量和函数。然后创建特权方法来访问这些私有成员。这之所以有效，是因为特权方法在构造函数内部定义时，它们变成了闭包，具有访问构造函数作用域内定义的所有变量和函数的完全权限。示例中，变量`privateVariable`和函数`privateFunction()`仅被`publicMethod()`访问。一旦创建了`MyObject`的实例，就没有办法直接访问`privateVariable`和`privateFunction()`；你只能通过`publicMethod()`。

你可以定义私有和特权成员来隐藏不应被直接修改的数据，如示例所示：

![image](img/logo1.gif)

```
function Person(name){

    this.getName = function(){

        return name;

    };

    this.setName = function (value) {

        name = value;

    };

}

var person = new Person("Nicholas");

alert(person.getName());   //"Nicholas"

person.setName("Greg");

alert(person.getName());   //"Greg"
```

PrivilegedMethodExample01.htm

代码中的构造函数定义了两个特权方法：`getName()`和`setName()`。每个方法在构造函数外部都是可访问的，并访问私有变量`name`。在`Person`构造函数外部，无法访问`name`。由于两个方法都定义在构造函数内部，它们是闭包，并通过作用域链访问`name`。私有变量`name`对于每个`Person`实例都是唯一的，因为每调用一次构造函数，方法都会重新创建。然而，一个缺点是，你必须使用构造函数模式来实现这一结果。

## 静态私有变量

也可以通过使用私有作用域定义私有变量或函数来创建特权方法。模式如下：

```
(function(){

    //private variables and functions

    var privateVariable = 10;

    function privateFunction(){

        return false;

    }

    //constructor

    MyObject = function(){

    };

    //public and privileged methods

    MyObject.prototype.publicMethod = function(){

        privateVariable++;

        return privateFunction();

    };

})();
```

在这个模式中，创建了一个私有作用域来封装构造函数及其方法。首先定义私有变量和函数，然后是构造函数和公共方法。公共方法定义在原型上，正如典型的原型模式一样。注意这种模式不是通过函数声明定义构造函数的，而是使用函数表达式。函数声明总是创建局部函数，这在情况下是不希望的。出于相同的原因，对`MyObject`没有使用`var`关键字。记住：初始化一个未声明的变量总是创建一个全局变量，因此`MyObject`变成全局并在私有作用域外部可用。同时请记住，在严格模式下向未声明的变量赋值会导致错误。

这种模式与之前模式的主要区别是，私有变量和函数在实例之间共享。由于特权方法定义在原型上，所有实例都使用同一个函数。特权方法作为闭包，始终持有对包含其作用域的引用。考虑以下：

![image](img/logo1.gif)

```javascript
(function(){

    var name = "";

    Person = function(value){                

        name = value;                

    };

    Person.prototype.getName = function(){

        return name;

    };

    Person.prototype.setName = function (value){

        name = value;

    };

})();

var person1 = new Person("Nicholas");

alert(person1.getName());   //"Nicholas"

person1.setName("Greg");

alert(person1.getName());   //"Greg"

var person2 = new Person("Michael");

alert(person1.getName());   //"Michael"

alert(person2.getName());   //"Michael"
```



### PrivilegedMethodExample02.htm我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。此示例中的 `Person` 构造函数可以访问私有变量 `name`，`getName()` 和 `setName()` 方法也是如此。使用这种模式，`name` 变量变成了静态的，并将在所有实例之间共享。这意味着在某个实例上调用 `setName()` 会影响所有其他实例。调用 `setName()` 或创建一个新的 `Person` 实例都会将 `name` 变量设置为新值。这导致所有实例都返回相同的值。

通过这种方式创建静态私有变量允许通过原型实现更好的代码复用，尽管每个实例并没有自己的私有变量。最终，使用实例或静态私有变量的决定取决于你的个人需求。

![image](img/pen.gif)

由于闭包和私有变量的使用，变量在作用域链中的查找越深，查找速度就越慢。

### 模块模式（The Module Pattern）

之前的模式为自定义类型创建了私有变量和特权方法。Douglas Crockford 描述的模块模式对单例执行了相同的操作。单例是指只会有一个实例的对象。传统上，JavaScript 中使用对象字面量符号创建单例，如下例所示：

```javascript
var singleton = {
    name: value,

    method: function () {
        // 此处编写方法代码
    }
};
```

模块模式增强了基础单例，允许拥有私有变量和特权方法，采用以下格式：

```javascript
var singleton = function () {
    // 私有变量和函数
    var privateVariable = 10;

    function privateFunction() {
        return false;
    }

    // 特权/公共方法和属性
    return {
        publicProperty: true,

        publicMethod: function () {
            privateVariable++;
            return privateFunction();
        }
    };
}();
```

模块模式使用一个返回对象的匿名函数。在匿名函数内部，首先定义私有变量和函数。之后，将一个对象字面量作为函数的返回值返回。该对象字面量仅包含应该是公的属性和方法。由于对象定义在匿名函数内部，因此所有公共方法都可以访问私有变量和函数。本质上，该对象字面量定义了单例的公共接口。当单例需要某种初始化并访问私有变量时（如本例所示），这种方法非常有用：

![image](img/logo1.gif)

```javascript
var application = function () {
    // 私有变量和函数
    var components = new Array();

    // 初始化
    components.push(new BaseComponent());

    // 公共接口
    return {
        getComponentCount: function () {
            return components.length;
        },

        registerComponent: function (component) {
            if (typeof component == "object") {
                components.push(component);
            }
        }
    };
}();
```

### ModulePatternExample01.htm

在 Web 应用程序中，有一个管理应用层级信息的单例是非常常见的。这个简单的示例创建了一个管理组件的应用程序对象。当对象首次被创建时，会创建一个私有的 `components` 数组，并将一个新的 `BaseComponent` 实例添加到其列表中。（`BaseComponent` 的代码并不重要；它仅用于在示例中演示初始化。）`getComponentCount()` 和 `registerComponent()` 方法是具有访问 `components` 数组权限的特权方法。前者简单返回已注册组件的数量，后者则注册一个新组件。

模块模式适用于此类情况：必须创建一个对象并用某些数据对其进行初始化，并暴露可以访问私有数据的公共方法。以这种方式创建的每个单例都是 `Object` 的实例，因为根结底一个对象字面量代表了它。这并不重要，因为单例通常是全局访问的，而不是作为参数传递给函数，这消除了使用 `instanceof` 运算符确定对象类型的需求。

### 模块增强模式（The Module-Augmentation Pattern）

对模块模式的另一种处理方式是在返回对象之前对其进行增强。当单例对象需要是特定类型的实例，但必须被增强额外的属性和/或方法时，这种模式非常有用。考虑以下示例：

```javascript
var singleton = function () {
    // 私有变量和函数
    var privateVariable = 10;

    function privateFunction() {
        return false;
    }

    // 创建对象
    var object = new CustomType();

    // 添加特权/公共属性和方法
    object.publicProperty = true;

    object.publicMethod = function () {
        privateVariable++;
        return privateFunction();
    };

    // 返回对象
    return object;
}();
```

如果模块模式示例中的 `application` 对象必须是 `BaseComponent` 的实例，则可以使用以下代码：

![image](img/logo1.gif)

```javascript
var application = function () {
    // 私有变量和函数
    var components = new Array();

    // 初始化
    components.push(new BaseComponent());

    // 创建 application 的本地副本
    var app = new BaseComponent();

    // 公共接口
    app.getComponentCount = function () {
        return components.length;
    };

    app.registerComponent = function (component) {
        if (typeof component == "object") {
            components.push(component);
        }
    };

    // 返回它
    return app;
}();
```

### ModuleAugmentationExample01.htm

在这个重写的应用程序单例版本中，首先定义私有变量，与上一个示例相同。主要区别是创建了一个 `BaseComponent` 的实例变量 `app`。这是将成为应用程序对象的本地版本。随后在 `app` 对象上添加公共方法以访问私有变量。最后一步是返回 `app` 对象，将其赋值给 `application`。

## 总结

函数表达式是 JavaScript 编程中非常有用的工具。它们允许进行不需要命名的动态编程。这些匿名函数（也称为 lambda 函数）是使用 JavaScript 函数的强大方式。以下是函数表达式的总结：

- 函数表达式与函数声明不同。函数声明需要名称，而函数表达式不需要。
- 由于没有确定引用函数的方法，递归变得变得复杂。
- 在非严格模式下运行的递归函数可以使用 `arguments.callee` 来递归调用自己，而不是使用函数名称，而名称可能会变化。

闭包在函数定义在另一个函数内部时创建，允许闭包访问包含函数内部的所有变量，如下：

- 在后台，闭包的作用域链包含一个自身的、包含内部的以及全局上下文的变量对象。
- 通常在函数执行完毕后，其作用域和所有变量都会被销毁。
- 当闭包从该函数返回时，它的作用域将保留在内存中，直到该闭包不再存在。

通过闭包，可以在 JavaScript 中模拟并不存在的块级作用域（block scoping），如下：

- 可以创建并立即调用一个函数，执行其内部代码，但不会留下对函数的任何引用。
- 这导致函数内部的所有变量都被销毁，除非它们被特地赋值给包含作用域中的一个变量。

闭包还可以用于在对象中创建私有变量，如下：

- 尽管 JavaScript 没有正式的对象私有属性概念，但可以使用闭包来实现公共方法，这些方法可以访问在包含作用域定义的变量。
- 访问私有变量的公共方法被称为特权方法（privileged methods）。
- 特权方法可以使用构造函数或原型模式在自定义类型上实现，也可以通过模块或模块增强模式在单例上实现。

函数表达式和闭包在 JavaScript 中非常强大，可以完成许多任务。请记住，闭包会在内存中维护额外的作用域，因此过度使用它们可能会导致内存消耗增加。

# 第 8 章：浏览器对象模型

## 本章内容

## 理解 `BOM` 的核心 `window` 对象

- 控制窗口、框架（frames）和弹出窗口
- 来自 `location` 对象的页面信息
- 使用 `navigator` 对象了解浏览器

尽管 ECMAScript 将描述为 JavaScript 的核心，但浏览器对象模型（`BOM`）真的是 Web 上使用 JavaScript 的核心。`BOM` 提供的对象暴露了独立于任何网页内容的浏览器功能。多年来，由于缺乏任何真实的规范，`BOM` 既变得有趣又充满问题，因为浏览器厂商可以根据自己的意愿对其进行扩展。浏览器之间的共性变成了事实上的标准，这些标准在浏览器开发过程中为了互操作性而保留了下来。现在 HTML5 规范的一部分已涵盖了 `BOM` 的主要方面，因为 W3C 正在对浏览器中 JavaScript 最基础的部分之一进行标准化。

## window 对象

`BOM` 的核心是 `window` 对象，它代表浏览器的实例。`window` 对象在浏览器中具有双重作用：既充当浏览器窗口的 JavaScript 接口，又作为 ECMAScript 全局对象。这意味着在网页中定义的每个对象、变量和函数都使用 `window` 作为其全局对象，并可以访问如 `parseInt()` 等方法。

### 全局作用域

由于 `window` 对象兼任 ECMAScript 全局对象，所有全局定义的变量和函数都会成为 `window` 对象的属性和方法。考虑这个示例：

```javascript
var age = 29;

function sayAge() {
    alert(this.age);
}

alert(window.age); // 29
sayAge(); // 29
window.sayAge(); // 29
```

在这里，一个名为 `age` 的变量和一个名为 `sayAge()` 的函数定义在全局作用域中，这会自动将它们放置在 `window` 对象上。因此，变量 `age` 可以通过 `window.age` 访问，函数 `sayAge()` 也可以通过 `window.sayAge()` 访问。由于 `sayAge()` 存在于全局作用域中，`this.age` 映射到 `window.age`，并显示正确的结果。尽管全局变量变成了 `window` 对象的属性，但定义全局变量与直接在 `window` 上定义属性之间存在细微区别：全局变量不能使用 `delete` 操作符删除，而直接定义在 `window` 上的属性可以删除。例如：

![image](img/logo1.gif)

```javascript
var age = 29;

window.color = "red";

// 在 IE < 9 中抛错误，在所有其他浏览器中返回 false
delete window.age;

// 在 IE < 9 中抛错误，在所有其他浏览器中返回 true
delete window.color; // 返回 true

alert(window.age); // 29
alert(window.color); // undefined
```

### DeleteOperatorExample01.htm

通过 `var` 语句添加的 `window` 属性的 `Configurable` 属性设置为 false，因此可能无法通过 `delete` 操作符删除。Internet Explorer 8 及之前的版本通过在对 `window` 属性使用 `delete` 操作符时抛错误来强制执行，无论它们最初是如何创建的。Internet Explorer 9 及更高版本不会报错。

另一个需要牢的点是：尝试访问未声明的变量会引发错误，但可以通过查看 `window` 对象来检查可能未声明的变量是否存在。例如：

```javascript
// 这会报错，因为 oldValue 是未声明的
var newValue = oldValue;

// 这不会报错，因为它是一个属性查找
// newValue 被设置为 undefined
var newValue = window.oldValue;
```

记住这一点，JavaScript 中有很多对象被认为是全局的，例如 `location` 和 `navigator`（两者将在本章后文讨论），但它们实际上是 `window` 对象的属性。

![image](img/pen.gif)

Windows Mobile 版 Internet Explorer 不允许通过 `window.property = value` 直接在 `window` 对象上创建新属性或方法。然而，所有全局声明的变量和函数仍然成为 `window` 的成员。

## Window 关系与框架

如果页面包含框架（frames），每个框架都有自己的 `window` 对象并存储在 `frames` 集合中。在 `frames` 集合中，`window` 对象既通过数字（从 0 开始，从左到右，然后按行计数）也通过框架名称进行索引。每个 `window` 对象都有一个 `name` 属性包含框架的名称。考虑以下：

![image](img/logo1.gif)

```html
<html>
<head>
    <title>Frameset Example</title>
</head>
<frameset rows="160,*">
    <frame src="frame.htm" name="topFrame">
    <frameset cols="50%,50%">
        <frame src="anotherframe.htm" name="leftFrame">
        <frame src="etanotherframe.htm" name="rightFrame">
    </frameset>
</frameset>
</html>
```

### FramesetExample01.htm

此代码创建了一个顶部有一个框架、下方有两个框架的框架。在这里，顶部框架可以通过 `window.frames[0]` 或 `window.frames["topFrame"]` 引用；然而你可能会使用 `top` 对象代替 `window` 来引用这些框架（例如 `top.frames[0]`）。`top` 对象始终指向最顶部（最外层）的框架，即浏览器窗口。这确保你指向正确的框架以访问其他框架。在框架内编写的任何引用 `window` 对象的代码都是指向该框架的唯一实例，而不是顶部的那个。图 8-1

图 8-1

![image](img/f242-01.jpg)

另一个窗口对象被称为 `parent`。`parent` 对象始终指向当前框架的直接父框架。在某些情况下，`parent` 可能等于 `top`，当没有框架时，`parent` 等于 `top`（两者都等于 `window`）。考虑以下示例：

![image](img/logo1.gif)

```html
<html>
<head>
    <title>Frameset Example</title>
</head>
<frameset rows="100,*">
    <frame src="frame.htm" name="topFrame">
    <frameset cols="50%,50%">
        <frame src="anotherframe.htm" name="leftFrame">
        <frame src="anotherframeset.htm" name="rightFrame">
    </frameset>
</frameset>
</html>
```

### frameset1.htm

这个框架包含一个包含另一个框架的框架，其代码如下：

```html
<html>
<head>
    <title>Frameset Example</title>
</head>
<frameset cols="50%,50%">
    <frame src="red.htm" name="redFrame">
    <frame src="blue.htm" name="blueFrame">
</frameset>
</html>
```



当第一个 `frameset` 加载浏览器时，它会将另一个 `frameset` 加到 `rightFrame` 中。如果代码写在 `redFrame`（或 `blueFrame`）内部，父对象指向 `rightFrame`。然而，如果代码写在 `topFrame` 中，那么 `parent` 指向 `top`，因为它的直接父级是最外层的帧。图 8-2 显示了当此示例加载到网络浏览器时，各种窗口对象的值。

图 8-2

![image](img/f243-01.jpg)

请注意，除非像本章稍后讨论的那样使用 `window.open()` 打开窗口，否则最顶层的窗口永远不会为 `name` 设置值。

还有一个最后的窗口对象，称为 `self`，它始终指向 `window`。事实上，这两者可以互换。尽管它没有独立的值，但为了与 `top` 和 `parent` 对象保持一致，包含了 `self`。

这些对象中的每一个实际上都是 `window` 对象的属性，可以通过 `window.parent`、`window.top` 等访问。这意味着可以将窗口对象链在一起，例如 `window.parent.parent.frames[0]`。

![image](img/pen.gif)

每当使用帧时，浏览器中就会存在多个 `Global` 对象。在每个帧中定义的全局变量被定义为该帧 `window` 对象的属性。由于每个窗口对象包含原生类型构造函数，因此每个帧都有自己的版本的构造函数，且它们是不相等的。例如，`top.Object` 不等于 `top.frames[0].Object`，这会影响在跨帧传递对象时 `instanceof` 的使用。

## 窗口位置

窗口对象的位置可以使用各种属性和方法进行确定和更改。Internet Explorer、Safari、Opera 和 Chrome 都提供了 `screenLeft` 和 `screenTop` 属性，分别指示窗口相对于屏幕左侧和顶部的位置。Firefox 通过 `screenX` 和 `screenY` 属性提供此功能，这两个属性在 Safari 和 Chrome 中也支持。Opera 支持 `screenX` 和 `screenY`，但你应该避免在 Opera 中使用它们，因为它们并不对应于 `screenLeft` 和 `screenTop`。以下代码确定了跨浏览器的窗口左和顶部位置：

![image](img/logo1.gif)

```
var leftPos = (typeof window.screenLeft == "number") ?
window.screenLeft : window.screenX;

var topPos = (typeof window.screenTop == "number") ?
window.screenTop : window.screenY;
```

`WindowPositionExample01.htm`

此示例使用三元运算符来确定 `screenLeft` 和 `screenTop` 属性是否存在。如果它们存在（在 Internet Explorer、Safari、Opera 和 Chrome 中如此），则使用它们。如果它们不存在（如 Firefox 中），则使用 `screenX` 和 `screenY`。

使用这些值存在一些特殊之处。在 Internet Explorer、Opera 和 Chrome 中，`screenLeft` 和 `screenTop` 是从屏幕左侧和顶部到 `window` 代表的页面区域的距离。如果窗口对象是最顶层对象且浏览器窗口位于屏幕的最顶部（y 坐标为 0），则 `screenTop` 值将是出现在页面区域上方的浏览器工具栏的像素高度。Firefox 和 Safari 将这些坐标视为与整个浏览器窗口相关的，因此将窗口放在屏幕上 y 坐标 0 处返回的顶部位置为 0。

为了增加复杂性，Firefox、Safari 和 Chrome 始终对页面上的每个帧返回 `top.screenX` 和 `top.screenY` 的值。即使页面由于某些边距而偏移，每次相对于窗口对象使用 `screenX` 和 `screenY` 时，都会返回这些相同的值。Internet Explorer 和 Opera 提供了帧相对于屏幕边缘位置的准确坐标。

最终结果是，你无法跨所有浏览器准确确定浏览器窗口的左侧和顶部坐标。然而，可以使用 `moveTo()` 和 `moveBy()` 方法准确地将窗口移动到新位置。每个方法接受两个参数。`moveTo()` 期望移动到的 `x` 和 `y` 坐标，而 `moveBy()` 期望在每个方向移动的像素数。考虑此示例：

```
//将窗口移动到左上角坐标
window.moveTo(0,0);

// 将窗口向下移动 100 像素
window.moveBy(0, 100);

// 将窗口移动到位置 (200, 300)
window.moveTo(200, 300);

// 将窗口向左移动 50 像素
window.moveBy(-50, 0);
```

这些方法可能会被浏览器禁用，并且在 Internet Explorer 7+、Chrome 和 Opera 的主浏览器窗口中默认是禁用的。这些方法对帧不起作用；它们仅作用于最顶层窗口对象。

## 窗口大小

跨浏览器确定窗口大小并不是简单的。Internet Explorer 9+、Firefox、Safari、Opera 和 Chrome 都提供了四个属性：`innerWidth`、`innerHeight`、`outerWidth` 和 `outerHeight`。在 Internet Explorer 9+、Safari、Firefox 和 Chrome 中，`outerWidth` 和 `outerHeight` 返回浏览器本身的尺寸（无论它是用于最顶层窗口对象还是帧）。在 Opera 中，`innerWidth` 和 `innerHeight` 值是页面视口的大小。Internet Explorer 8 及更早版本没有获取浏览器窗口尺寸的方法；但它们通过 DOM 提供页面可视区域的信息。

`document.documentElement.clientWidth` 和 `document.documentElement.clientHeight` 属性在 Internet Explorer、Opera 和 Chrome 中提供了页面视口的宽度和高度。在 Internet Explorer 6 中，浏览器必须处于标准模式这些属性才可用；在怪模式下，信息可以通过 `document.body.clientWidth` 和 `document.body.clientHeight` 获取。当 Chrome 处于怪模式时，`document.documentElement` 的 `clientWidth` 和 `clientHeight` 视口尺寸。

最终结果是，没有准确的方法可以确定浏览器本身的大小，但可以获取页面视口的尺寸，如下所示：

![image](img/logo1.gif)

```
var pageWidth = window.innerWidth,
pageHeight = window.innerHeight;

if (typeof pageWidth != "number"){
if (document.compatMode == "CSS1Compat"){
pageWidth = document.documentElement.clientWidth;
pageHeight = document.documentElement.clientHeight;
} else {
pageWidth = document.body.clientWidth;
pageHeight = document.body.clientHeight;
}
}
```

`WindowSizeExample01.htm`

在此代码中，`pageWidth` 和 `pageHeight` 分别赋值为 `window.innerWidth` 和 `window.innerHeight`。然后检查 `pageWidth` 的值是否为数字；如果不是，则通过使用 `document.compatMode` 确定页面是否处于标准模式。（该属性在第 11 章中进行了充分讨论。）如果是，则使用 `document.documentElement.clientWidth` 和 `document.documentElement.clientHeight`；否则，则使用 `document.body.clientWidth` 和 `document.body.clientHeight`。

对于移动设备，`window.innerWidth` 和 `window.innerHeight` 是视觉视口的尺寸，即页面在屏幕上的可见区域。移动版 Internet Explorer 不这些属性，但在 `document.documentElement.clientWidth` 和 `document.documentElement.clientHeight` 上提供相同的信息。这些值会随着你放大或缩小页面而发生变化。

在其他移动浏览器中，`document.documentElement` 的测量提供了布局视口（layout viewport）的测量，这是渲染页面的实际尺寸（相对于视觉视口，后者只是整个页面的一小部分）。移动版 Internet Explorer 将此信息存储在 `document.body.clientWidth` 和 `document.body.clientHeight` 中。这些值在放大或缩小时不会改变。

由于这些与桌面浏览器的差异，在决定使用并并遵循哪些测量值之前，你可能需要先判断用户是否在移动设备上。

![image](img/pen.gif)

移动视口主题是一个复杂的课题，有各种异常和注意事项。移动端开发顾问 Peter-Paul Koch 在 [`quirksmode.org/mobile/viewports2.html`](http://quirksmode.org/mobile/viewports2.html) 中概述了他所有的研究内容。如果你正在为移动设备开发程序，这是推荐的读物。

可以使用 `resizeTo()` 和 `resizeBy()` 方法调整浏览器窗口的大小。每个方法都接受两个参数：`resizeTo()` 期望一个新的宽度和高度，而 `resizeBy()` 期望每个维度上的差异。这里有一个示例：

```javascript
//调整为 100 x 100
window.resizeTo(100, 100);

//调整为 200 x 150
window.resizeBy(100, 50);

//调整为 300 x 300
window.resizeTo(300, 300);
```

与窗口移动方法一样，调整大小的方法可能会被浏览器禁用，并且在 Internet Explorer 7+、Chrome 和 Opera 中默认是禁用的。同样，类似于移动方法，这些方法仅适用于顶层窗口对象。

## 导航和打开窗口

`window.open()` 方法既可以导航到特定的 URL，也可以用于打开新的浏览器窗口。该方法接受四个参数：要加载的 URL、窗口目标（target）、一个特性字符串，以及一个指示新页面是否替换浏览器历史记录中当前加载页面的布尔值。通常只使用前三个参数；最后一个参数仅在不打开新窗口时生效。

如果传递给 `window.open()` 的第二个参数是已存在的窗口或帧的，则 URL 将加载到该名称的窗口或帧中。这里有一个示例：

```javascript
//相当于 <a href="http://www.wrox.com" target="topFrame"></a>
window.open("http://www.wrox.com/", "topFrame");
```

这行代码的作用相当于用户点击了一个 `href` 属性设置为 `[`www.wrox.com`](http://www.wrox.com)` 且 `target` 属性设置为 "topFrame" 的链接。如果存在名为 "topFrame" 的窗口或帧，则 URL 将加载到那里；否则，将创建一个新窗口并命名为 "topFrame"。第二个参数也可以是任何特殊窗口名称：`_self`、`_parent`、`_top` 或 `_blank`。

## 弹出窗口

当第二个参数没有识别出已有的窗口或帧时，将根据第三个参数传递的字符串创建一个新窗口或标签页。如果缺少第三个参数，将打开具有所有默认浏览器窗口设置的新浏览器窗口（或根据浏览器设置打开标签页）。（工具栏、地址栏和状态栏都是根据浏览器的默认设置设置的。）在不打开新窗口时，第三个参数会被忽略。

第三个参数是一个逗号分隔的设置字符串，指示新窗口的显示信息。下表描述了各种选项。

| 设置 | 值(s) | 描述 |
| --- | --- | --- |
| `fullscreen` | `"yes"` 或 `"no"` | 表示创建时浏览器窗口是否应最大化。仅限 Internet Explorer。 |
| `height` | 数字 | 新窗口的初始高度。此值不能小于 100。 |
| `left` | 数字 | 新窗口的初始左坐标。不能为负数。 |
| `location` | `"yes"` 或 `"no"` | 表示是否显示地址栏。默认值根据浏览器而异。设置为 `"no"` 时，地址栏可能会隐藏或禁用（取决于浏览器）。 |
| `menubar` | `"yes"` 或 `"no"` | 表示是否显示菜单栏。默认值为 `"no"`。 |
| `resizable` | `"yes"` 或 `"no"` | 表示新窗口是否可以通过拖动边框调整大小。默认为 `"no"`。 |
| `scrollbars` | `"yes"` 或 `"no"` | 表示如果内容无法适应视口，新窗口是否允许滚动。默认为 `"no"`。 |
| `status` | `"yes"` 或 `"no"` | 表示是否显示状态栏。默认值根据浏览器而异。 |
| `toolbar` | `"yes"` 或 `"no"` | 表示是否显示工具栏。默认值为 `"no"`。 |
| `top` | 数字 | 新窗口的初始顶部坐标。不能为负数。 |
| `width` | 数字 | 新窗口的初始宽度。此值不能小于 100。 |

这些设置中的任何或全部都可以指定为逗号分隔的键-值对集合。键-值对通过等号指示（特性字符串中不允许有空格）。考虑以下示例：

```javascript
window.open("http://www.wrox.com/","wroxWindow",
"height=400,width=400,top=10,left=10,resizable=yes");
```

此段代码打开了一个可调整大小的新窗口，尺寸为 400 x 400，并位于屏幕顶部和左侧 10 像素处。

`window.open()` 方法返回新创建的窗口的引用。该对象与任何其他窗口对象相同，不同之处你通常对它有更多的控制权。例如，某些默认不允许你调整或移动主浏览器窗口大小的浏览器，可能允许你调整或移动你使用 `window.open()` 创建的窗口。此对象可以像操作任何其他窗口一样操作新打开的窗口，例所示：

```javascript
var wroxWin =window.open("http://www.wrox.com/","wroxWindow",
"height=400,width=400,top=10,left=10,resizable=yes");

//调整大小
wroxWin.resizeTo(500, 500);

//移动位置
wroxWin.moveTo(100, 100);
```

可以通过 `close()` 方法关闭新打开的窗口：

```javascript
wroxWin.close();
```

该方法仅适用于通过 `window.open()` 创建的弹出窗口。无法没有用户确认的情况下关闭主浏览器窗口。然而，弹出窗口可以通过调用 `top.close()` 自己关闭。一旦窗口关闭，窗口引用仍然存在，但只能用于检查 `closed` 属性，如下：

```javascript
wroxWin.close();
alert(wroxWin.closed); //true
```

新创建的窗口对象通过 `opener` 属性拥有指向打开它的窗口的引用。该属性仅定义在弹出窗口的顶层窗口对象（`top`）上，指向调用 `window.open()` 的窗口或帧。例如：

```javascript
var wroxWin =window.open("http://www.wrox.com/","wroxWindow",
"height=400,width=400,top=10,left=10,resizable=yes");

alert(wroxWin.opener == window); //true
```

尽管弹出窗口指向打开它的窗口，但没有反向关系。窗口不会跟踪它们生成的弹出窗口，因此如有需要由你自己跟踪。

某些浏览器（如 Internet Explorer 8+ 和 Google Chrome）尝试将浏览器中的每个标签页作为独立的进程运行。当一个标签页打开另一个时，窗口对象需要相互通信，因此标签不能在独立进程中运行。Chrome 允许你通过将 `opener` 属性设置为 `null` 来指示新创建的标签页应在独立进程中运行，例所示：

```javascript
var wroxWin =window.open("http://www.wrox.com/","wroxWindow",
"height=400,width=400,top=10,left=10,resizable=yes");

wroxWin.opener = null;
```



将`opener`设置为`null`会告诉浏览器新创建的标签页不需要与打开它的标签页进行通信，因此它可能会在单独进程中运行。一旦此连接被断开，就无法恢复。

## 安全限制

弹窗曾经历过在线广告商过度使用的时期。弹窗通常被伪装成系统对话框，以引导用户点击广告。由于这些弹窗网页的样式看起来像系统对话框，用户无法判断该对话框是否合规。为了帮助进行判断，浏览器开始对弹窗的配置实施限制。

Windows XP Service Pack 2 上的 Internet Explorer `6` 对弹窗实施了多项安全功能，包括不允许创建弹窗或将其移动到屏幕之外，并确保状态栏无法关闭。从 Internet Explorer `7` 开始，地址栏无法关闭，且默认情况下弹窗无法移动或调整大小。Firefox `1` 关闭了抑制状态栏的功能，因此无论传递给`window.open()`的特征字符串，所有弹窗都必须显示状态栏。Firefox `3` 强制弹窗上始终显示地址栏。Opera 仅在其主浏览器窗口内打开弹窗，但不允许它们存在于可能与系统对话框混淆的位置。

此外，浏览器仅在用户操作后才允许创建弹窗。例如，在页面仍在加载时调用`window.open()`将不会执行，并可能向用户显示错误。弹窗只能根据点击或按键打开。

Chrome 使用了不同的方法来处理非用户发起的弹窗。它不是阻塞它们，而是只显示弹窗的标题栏并将其放置在浏览器窗口的右下角。

![image](img/pen.gif)

Internet Explorer 在显示存储在计算机硬盘上的网页时，会解除对弹窗的一些限制。相同的代码在服务器上运行时，将触发弹窗限制。

## 弹窗拦截器

大多数浏览器都内置了弹窗拦截软件，对于没有内置的浏览器，像 Yahoo! Toolbar 等工具也有内置的拦截器。结果是大多数意外的弹窗都被拦截了。当弹窗被拦截时，会发生两种情况之一。如果浏览内置弹窗拦截器停止了弹窗，那么`window.open()`可能返回`null`。在这种情况下，可以通过检查返回值来判断弹窗是否被拦截，例如所示：

```
var wroxWin = window.open("http://www.wrox.com", "_blank");

if (wroxWin == null){

alert("The popup was blocked!");

}
```

当浏览器插件或其他程序拦截弹窗时，`window.open()`通常会抛出一个错误。因此，为了准确检测弹窗何时被拦截，你必须检查返回值并将`window.open()`的调用封装在`try-catch`块中，如示例所示：

![image](img/logo1.gif)

```
var blocked = false;

try {

var wroxWin = window.open("http://www.wrox.com", "_blank");

if (wroxWin == null){

blocked = true;

}

} catch (ex){

blocked = true;

}

if (blocked){

alert("The popup was blocked!");

}
```

PopupBlockerExample01.htm

此代码可以准确检测弹窗拦截器是否拦截了`window.open()`的调用，无论使用什么方法。注意，检测弹窗是否被拦截并阻止浏览器显示其关于弹窗被拦截的消息。

## 间隔器与超时

浏览器中的 JavaScript 执行是单线程的，但允许通过使用超时和间隔来调度代码在特定时间运行。超时（Timeouts）在指定时间后执行某些代码，而间隔（intervals）则重复执行代码，并在每次执行之间等待特定的时间。

你使用窗口的`setTimeout()`方法设置超时，该方法接受两个参数：要执行的代码以及在尝试执行代码之前等待的时间（以毫秒计）。第一个参数可以是包含 JavaScript 代码的字符串（如在使用`eval()`时所用），也可以是一个函数。例如，以下两种方式都会在 1 秒后显示警报：

![image](img/logo1.gif)

```
//避免使用！
setTimeout("alert('Hello world!') ", 1000);

//推荐做法
setTimeout(function() {

alert("Hello world!");

}, 1000);
```

TimeoutExample01.htm

尽管这两个语句都能正常工作，但将字符串作为第一个参数被认为是不良实践，因为它会带来性能损失。

第二个参数（等待的毫秒数）并不意味着指定代码一定执行的时间。JavaScript 是单线程的，因此一次只能执行一段代码。为了管理执行，存在一个 JavaScript 任务执行队列。任务按照它们被添加到队列的顺序执行。`setTimeout()`的第二个参数告诉 JavaScript 引擎在指定的毫秒后将此任务添加到队列中。如果队列为空，则立即执行该代码；如果队列不为空，代码必须轮候。

当调用`setTimeout()`时，它返回一个用于超时的数字 ID。该 ID 是用于取消超时的唯一标识符。要取消超时，使用`clearTimeout()`方法并传入超时 ID，如下例：

```
//设置超时
var timeoutId = setTimeout(function() {

alert("Hello world!");

}, 1000);

//忽略 - 取消
clearTimeout(timeoutId);
```

TimeoutExample02.htm

只要在指定时间过去调用`clearTimeout()`，超时就可以被取消。在代码执行后调用`clearTimeout()`没有影响。

![image](img/pen.gif)

超时执行的代码运行在全局作用域，因此在非严格模式下运行时，函数内部的这个值始终指向`window`。

间隔的工作方式与超时相同，区别在于它们会在间隔被取消或页面卸之前重复执行代码。`setInterval()`方法让你设置间隔，它接受与`setTimeout()`相同的参数：要执行的代码（字符串或函数）以及执行之间的等待毫秒数。这是一个示例：

![image](img/logo1.gif)

```
//避免使用！
setInterval("alert('Hello world!') ", 1000);

//推荐做法
setInterval(function() {

alert("Hello world!");

}, 10000);
```

IntervalExample01.htm

`setInterval()`方法还会返回一个间隔 ID，可以在未来的某个时刻取消间隔。可以使用`clearInterval()`方法配合此 ID 取消所有等待中的间隔。这种能力对于间隔比超时更重要，因为如果不检查，它们将一直执行到页面卸载。这是一个常见的间隔用法示例：

```
var num = 0;

var max = 10;

var intervalId = null;

function incrementNumber() {

num++;

//如果达到最大值，取消所有等待中的执行
if (num == max) {

clearInterval(intervalId);

alert("Done");

}

}

intervalId = setInterval(incrementNumber, 500);
```

IntervalExample02.htm

在这个示例中，变量`num`每半秒增加一次，直到最终达到最大数字，此时间隔被取消。这种模式也可以使用超时来实现，如下所示：

![image](img/logo1.gif)

```
var num = 0;

var max = 10;

function incrementNumber() {

num++;

//如果还没有达到最大值，设置另一个超时
if (num < max) {

  setTimeout(incrementNumber, 500);

} else {

  alert("Done");

}

}

setTimeout(incrementNumber, 500);
```

TimeoutExample03.htm

注意，当你使用超时时，没有必要跟踪超时 ID，因为执行会自动停止，只有在设置了另一个超时时才会继续。这种模式被认为是在不实际使用间隔器（intervals）的情况下设置间隔任务的最佳实践。在生产环境中，很少使用真正的间隔器，因为上一个间隔结束到下一个间隔开始之间的时间并不一定保证，而且某些间隔可能会被跳过。像前一个示例那样使用超时，可以确保这种情况不会发生。通常情况下，最好避免使用间隔器。

## 系统对话框

浏览器能够通过`alert()`、`confirm()`和`prompt()`方法调用系统对话框来向用户显示内容。这些对话框与浏览器中显示的网页无关，且不包含 HTML。它们的显示由操作系统和/或浏览器设置决定，而不是由 CSS。此外，这些对话框中的每一个都是同步且模态的（modal），这意味着当显示对话框时代码执行会停止，并在其被关闭后恢复。

### alert()

`alert()`方法在书中一直被使用。它仅接受一个字符串并显示给用户。当调用`alert()`时，系统消息框会向用户显示指定的文本，随后跟着一个 OK 按钮。例如，在 Windows XP 的 Internet Explorer 上使用`alert("Hello world!")`时会渲染如 图 8-3 所示的对话框。

FIGURE 8-3

![image](img/f253-01.jpg)

Alert 对话框通常用于必须让用户意识到某些他们无法控制的事情，例如错误。用户唯一的选择是在阅读消息后关闭对话框。

### confirm()

第二种对话框是通过调用`confirm()`调用的。confirm 对话框看起来与 alert 对话框相似，因为它也会向用户显示消息。两者之间的主要区别在于除了 OK 按钮外还有一个 Cancel（取消）按钮，这允许用户指示是否应该执行给定的操作。例如，`confirm("Are you sure?")`会显示如 图 8-4 所示的确认对话框。

FIGURE 8-4

![image](img/f254-01.jpg)

为了确定用户点击的是 OK 还是 Cancel，`confirm()`方法返回一个布尔值：点击 OK 则返回`true`，如果点击 Cancel 或通过点击右上角的 X 关闭对话框则返回`false`。confirm 对话框的典型用法如下：

```
if (confirm("Are you sure?")) {

alert("I'm so glad you're sure! ");

} else {

alert("I'm sorry to hear you're not sure. ");

}
```

在这个示例中，确认对话框在第一行显示给用户，这是`if`语句的条件。如果用户点击 OK，将显示一个 alert 说：“I'm so glad you're sure!”。然而，如果点击了 Cancel 按钮，将显示一个 alert 说：“I'm sorry to hear you're not sure.”。这种模式通常用于用户尝试删除某些内容时，例如电子邮件。

### prompt()

最后一种对话框通过调用`prompt()`显示，它会提示用户进行输入。除了 OK 和 Cancel 按钮外，该对话框还有一个文本框，用户可以在其中输入某些数据。`prompt()`方法接受两个参数：显示给用户的文本以及文本框的默认值（可以是空字符串）。调用`prompt("What's your name?", "Michael")`会产生如 图 8-5 所示的对话框。

FIGURE 8-5

![image](img/f254-02.jpg)

如果点击 OK 按钮，`prompt()`返回文本框中的值；如果点击 Cancel 或在未点击 OK 的情况下关闭关闭对话框，函数将返回`null`。这是一个示例：

```
var result = prompt("What is your name? ", "");

if (result !== null) {

alert("Welcome, " + result);

}
```

这些系统对话框对于向用户显示信息和确认决策很有帮助。由于它们不需要加载 HTML、CSS 或 JavaScript，它们是增强 Web 应用快速快捷的方法。

Chrome 和 Opera 对这些系统对话框引入了一个特殊功能。如果正在运行的脚本在执行期间产生了两个或多个系统对话框，则第一个之后的后续对话框都会显示一个复选框，允许用户在页面刷新之前禁用任何后续对话框（参见 图 8-6）。

FIGURE 8-6

![image](img/f255-01.jpg)

当勾选复选框并关闭对话框后，所有后续系统对话框（alerts、confirms 和 prompts）都会被阻塞，直到页面刷新。Chrome 并没有告知开发者对话框是否已显示。每当浏览器空闲时，对话计数器就会重置，因此如果两个独立的用户操作产生一个 alert，则其中一个都不会显示复选框；如果单个用户操作连续产生两个 alert，则第二个将包含复选框。自从首次引入以来，此功能已进入了 Internet Explorer 9 和 Firefox 4。

另外两种类型的对话框可以通过 JavaScript 显示：find 和 print。这两个对话框都是异步的，会将控制权返回给脚本。使用 window 对象上的方法如下：

```
// 显示 print 对话
window.print();

// 显示 find 对话
window.find();
```

这两个方法无法指示用户是否对对话框做了什么，因此很难很好利用它们。此外，由于它们是异步的，它们不会增加 Chrome 的对话计数器，也不会受到用户选择禁用后续对话的影响。

## location 对象

最有用的 BOM 对象之一是`location`，它提供了当前加载文档的信息以及通用的导航功能。`location`对象的独特之处在于它是 window 和 document 的属性；`window.location`和`document.location`指向同一个对象。`location`不仅了解当前加载的文档，还将 URL 解析为可以通过一系列属性访问的离散部分。这些属性如表所示（假设 location 前缀）。

| 属性名称 | 示例 | 描述 |
| --- | --- | --- |
| `hash` | `#contents` | URL 哈（井号后跟零或多个字符），如果 URL 没有哈则返回空字符串。 |
| `host` | [www.wrox.com:80](http://www.wrox.com:80) | 服务器名称和端口号（如果存在）。 |
| `hostname` | [www.wrox.com](http://www.wrox.com) | 无端口号的服务器名称。 |
| `href` | [`www.wrox.com`](http://www.wrox.com) | 当前加载页面的完整 URL。location 的`toString()`方法返回此值。 |
| `pathname` | `/WileyCDA/` | URL 的目录和/或文件名。 |
| `port` | `8080` | URL 中指定的请求端口。如果 URL 不包含端口，则该属性返回空字符串。 |
| `protocol` | `http:` | 页面使用的协议。通常为 "http:" 或 "https:"。 |
| `search` | `?q=javascript` | URL 的查询字符串。它返回一个以问号开头的字符串。 |

### 查询字符串参数

`location`中的大部分信息都可以通过这些属性轻松获取。URL 中未提供的部分是一个易于使用的查询字符串（query string）。尽管`location.search`返回从问号开始到 URL 末尾的所有内容，但无法直接逐个访问查询字符串参数。get 函数`getQueryStringArgs()`解析查询字符串并返回一个包含每个参数条目的对象的对象：

![image](img/logo1.gif)

```javascript
function getQueryStringArgs(){

//获取不带初始问号 ? 的查询字符串
var qs = (location.search.length > 0 ? location.search.substring(1) : ""),

//用于存储数据的对象
args = {},

//获取单个项目
items = qs.length ? qs.split("&") : [],

item = null,

name = null,

value = null,

//用于 for 循环
i = 0,

len = items.length;

//将每个项目赋值给 args 对象
for (i=0; i < len; i++){

item = items[i].split("=");

name = decodeURIComponent(item[0]);

value = decodeURIComponent(item[1]);

if (name.length) {

args[name] = value;

}

}

return args;

}
```



`LocationExample01.htm`

该函数的第一个步是去掉查询字符串开头的问号。这只有在`location.search`拥有一个或多个字符时才会发生。参数将存储在`args`对象中，该对象是使用对象字面量格式创建的。接下来，使用与字符对查询字符串进行分割，返回一个`name=value`格式的字符串数组。`for`循环遍历此数组，然后根据等号分割每个项目，返回一个数组，其中第一个项目是参数名称，第二个项目是值。名称和值都使用`decodeURIComponent()`进行解码（因为查询字符串参数本应该是经过编码的）。最后，将名称赋值为`args`对象的属性，并将其值设置为`value`。该函数的用例如下：

```javascript
//假设查询字符串为 ?q=javascript&num=10
var args = getQueryStringArgs();
alert(args["q"]); //"javascript"
alert(args["num"]); //"10"
```

现在每个查询字符串参数都是返回对象的属性，这提供了对每个参数的快速访问。

### 操作 Location

可以使用`location`对象以多种方式更改浏览器位置。第一种也是常用的方法是使用`assign()`方法并传入一个 URL，例如所示：

```javascript
location.assign("http://www.wrox.com");
```

这会立即开始导航到新 URL 的过程并在浏览器的历史堆栈中创建一个条目。如果将`location.href`或`window.location`设置为 URL，则会使用该值调用`assign()`方法。例如，以下两种操作的行为都与显式调用`assign()`相同：

```javascript
window.location = "http://www.wrox.com";
location.href = "http://www.wrox.com";
```

在更改浏览器位置的三种方法中，设置`location.href`在代码中最为常见。

更改`location`对象上的各种属性也可以修改当前加载的页面。`hash`、`search`、`hostname`、`pathname`和`port`属性可以设置为新值以更改当前 URL，例如所示：

```javascript
//假设起始于 http://www.wrox.com/WileyCDA/
//将 URL 为 "http://www.wrox.com/WileyCDA/#section1"
location.hash = "#section1";
//更改 URL 为 "http://www.wrox.com/WileyCDA/?q=javascript"
location.search = "?q=javascript";
//更改 URL 为 "http://www.yahoo.com/WileyCDA/"
location.hostname = "www.yahoo.com";
//更改 URL 为 "http://www.yahoo.com/mydir/"
location.pathname = "mydir";
//更改 URL 为 "http://www.yahoo.com:8080/WileyCDA/"
```

每当更改`location`上的属性时（除`hash`外），页面都会使用新 URL 重新加载。

![image](img/pen.gif)

更改`hash`的值会导致 Internet Explorer 8+、Firefox 2+、Opera 9+ 和 Chrome 在浏览器历史记录中记录一个新条目。在较早的 Internet Explorer 版本中，`hash`属性并不是在点击“后退”或“前进”时更新，而是只有在点击包含哈希 URL 的链接时才会更新。

当使用前面提到的方法之一更改 URL 时，浏览器历史堆栈中会创建一个条目，以便用户点击“后退”按钮导航到上一个页面。可以使用`replace()`方法来禁止这种行为。该方法接受单个参数（即要导航到的 URL），但不会在历史堆栈中创建条目。调用`replace()`后，用户无法返回上一个页面。考虑此示例：

![image](img/logo1.gif)

```html
<!DOCTYPE html>
<html>
<head>
<title>你将无法回到这里</title>
</head>
<body>
<p>请享受这个页面几秒钟，因为你不会回到这里了。</p>
<script type="text/javascript">
setTimeout(function () {
location.replace("http://www.wrox.com/");
}, 1000);
</script>
</body>
</html>
```

`LocationReplace01.htm`

如果使用上述方法之一更改 URL，浏览器历史堆栈中就会创建一个条目，用户可以点击“后退”按钮导航到上一个页面。可以使用`replace()`方法来禁止这种行为。该方法接受单个参数（即要导航到的 URL），但不会在历史堆栈中创建条目。调用`replace()`后，用户无法返回上一个页面。考虑此示例：

![image](img/logo1.gif)

```html
<!DOCTYPE html>
<html>
<head>
<title>你将无法回到这里</title>
</head>
<body>
<p>请享受这个页面几秒钟，因为你不会回到这里了。</p>
<script type="text/javascript">
setTimeout(function () {
location.replace("http://www.wrox.com/");
}, 1000);
</script>
</body>
</html>
```

（注：此处原文中`replace`描述逻辑与示例代码一致，已根据翻译逻辑微调了示例中混乱的 HTML 标签以保持结构完整）

注：此处重复了上述描述的属性和方法。

`navigator`对象的属性通常用于确定运行网页的浏览器类型（在第 9 章有详细讨论）。

### 检测插件

最常见的检测程序之一是确定浏览器是否安装了特定的插件。对于 Internet Explorer 以外的浏览器，可以使用`plugins`数组来确定。数组中的每个项目包含以下属性：

*   `name` — 插件的名称
*   `description` — 插件的描述
*   `filename` — 插件的文件名
*   `length` — 该插件处理的 MIME 类型数量

通常，`name`包含了标识插件所需的所有信息，尽管这不是一门精确的科学。插件检测是通过遍历可用插件并将插件名称与给定的名称进行比较完成的，如下所示：

![image](img/logo1.gif)

```javascript
//插件检测 - 在 Internet Explorer 中不起
function hasPlugin(name){
name = name.toLowerCase();
for (var i=0; i < navigator.plugins.length; i++){
if (navigator.plugins[i].name.toLowerCase().indexOf(name) > -1){
return true;
}
}
return false;
}
//检测 flash
alert(hasPlugin("Flash"));
//检测 quicktime
alert(hasPlugin("QuickTime"));
```

`PluginDetectionExample01.htm`

`hasPlugin()`示例接受一个参数：要检测的插件名称。第一步是将该名称转换为小写，以便于比较。接下来，遍历`plugins`数组，并通过`indexOf()`检查每个`name`属性，查看传入的名称是否出现在该字符串的某个位置。此比较在全小写状态下进行，以避免大小写错误。参数应尽可能具体，以避免混淆。诸如 "Flash" 和 "QuickTime" 这样的字符串足够独特，不应该产生什么混淆。此方法适用于检测 Firefox、Safari、Opera 和 Chrome 中的插件。

![image](img/pen.gif)

每个插件对象也是一个`MimeType`对象的数组，可以使用方括号符号访问。每个`MimeType`对象有四个属性：`description`，是 MIME 类型的描述；`enabledPlugin`，是指向插件对象的指针；`suffixes`，是该 MIME 类型文件扩展名列表（以逗号分隔的字符串）；以及`type`，是完整的 MIME 类型字符串。

在 Internet Explorer 中检测插件更为困难，因为它不支持 Netscape 风格的插件。在 Internet Explorer 中检测插件的唯一方法是使用专有的`ActiveXObject`类型并尝试实例化特定的插件。插件在 Internet Explorer 中使用 COM 对象实现，这些对象通过唯一字符串标识。因此，要检查特定插件，你必须知道它的 COM 标识符。例如，Flash 的标识符是 "ShockwaveFlash.ShockwaveFlash"。有了这些信息，你可以编写一个函数来判断 Internet Explorer 是否安装了该插件，如下所示：

![image](img/logo1.gif)

```javascript
//Internet Explorer 插件检测
function hasIEPlugin(name){
try {
new ActiveXObject(name);
return true;
} catch (ex){
return false;
}
}
//检测 flash
alert(hasIEPlugin("ShockwaveFlash.ShockwaveFlash"));
//检测 quicktime
alert(hasIEPlugin("QuickTime.QuickTime"));
```

### PluginDetectionExample02.htm

在此示例中，`hasIEPlugin()`函数接受 COM 标识符作为其唯一参数。在函数内部，尝试创建一个新的`ActiveXObject`实例。这被封装在一个 try-catch 语句中，因为尝试创建未知 COM 对象将抛出错误。因此，如果尝试成功，函数返回`true`。如果发生错误，则执行 catch 块并返回`false`。该代码随后检查 Internet Explorer 中是否有 Flash 和 QuickTime 插件。

由于这两种插件检测方法截然不同，通常的做法是创建测试特定插件的函数，而不是使用之前描述的通用方法。考虑此示例：

```javascript
//为所有浏览器检测 flash
function hasFlash(){
var result = hasPlugin("Flash");
if (!result){
result = hasIEPlugin("ShockwaveFlash.ShockwaveFlash");
}
return result;
}
//为所有浏览器检测 quicktime
function hasQuickTime(){
var result = hasPlugin("QuickTime");
if (!result){
result = hasIEPlugin("QuickTime.QuickTime");
}
return result;
}
//检测 flash
alert(hasFlash());
//检测 quicktime
alert(hasQuickTime());
```

### PluginDetectionExample03.htm

此代码定义了两个函数：`hasFlash()`和`hasQuickTime()`。每个函数首先尝试使用非 Internet Explorer 的插件检测代码。如果该方法返回`false`（对于 Internet Explorer 来说确实如此），则调用 Internet Explorer 插件检测方法。如果 Internet Explorer 插件检测方法也返回`false`，则整个方法的结果为`false`。如果任一插件检测函数返回`true`，则整个方法返回`true`。

![image](img/pen.gif)

`plugins`集合有一个名为`refresh()`的方法，它可以刷新插件以反映任何新安装的插件。该方法接受一个参数：一个布尔值，指示是否应该重加载页面。设置为`true`时，所有包含插件的页面都将重新加载；否则更新`plugins`集合，但不重加载页面。

## 注册处理器 (Registering Handlers)

Firefox 2 为`navigator`对象引入了`registerContentHandler()`和`registerProtocolHandler()`方法。（这些方法现在正式定义在 HTML 5 中。）这些方法允许网站标明它可以处理特定类型的信息。随着在线 RSS 阅读器和在线电子邮件应用程序的兴起，这是让这些应用程序像桌面应用程序一样被默认使用的的一种方法。

`registerContentHandler()`方法接受三个参数：要处理的 MIME 类型、可以处理该 MIME 类型的页面 URL 以及应用程序名称。例如，要将一个站点注册为 RSS 馈的处理器，可以使用以下代码：

```javascript
navigator.registerContentHandler("application/rss+xml",
"http://www.somereader.com?feed=%s", "Some Reader");
```

第一个参数是 RSS 馈的 MIME 类型。第二个参数是应该接收 RSS 馈 URL 的地址。在第二个参数中，`%s`代表 RSS 馈的 URL，浏览器会自动插入它。当下一次对 RSS 馈发出请求时，浏览器将导航到指定的 URL，网页应用程序可以用适当的方式处理请求。

![image](img/pen.gif)

从版本 4 的 Firefox 允许在`registerContentHandler()`中使用三种 MIME 类型："application/rss+xml"、application/atom+xml" 和 "application/vnd.Mozilla.feed"。这三种的作用都是注册所有的 RSS 馈。

可以使用`registerProtocolHandler()`对协议进行类似的调用，它也接受三个参数：要处理的协议（例如 "mailto" 或 "ftp"）、处理该协议的页面 URL 以及应用程序名称。例如，要将 Web 应用程序注册为默认邮件客户端，可以使用以下：

```javascript
navigator.registerProtocolHandler("mailto",
"http://www.somemailclient.com?cmd=%s", "Some Mail Client");
```

在此示例中，为`mailto`协议注册了一个处理器，它现在将指向一个 Web 电子邮件客户端。再次，第二个参数是处理请求的 URL，`%s`代表原始请求。

![image](img/pen.gif)

在 Firefox 2 中，`registerProtocolHandler()`已经实现但不起作用。Firefox 3 完全实现了该方法。

## screen 对象 (screen Object)

`screen`对象（也是`window`的属性）是少数几个没有编程用途的 JavaScript 对象之一；它仅作为客户端能力的指示。此对象提供了浏览器窗口之外显示的信息，包括像素宽度和高度等。每个浏览器在`screen`对象上提供不同的属性。下表显示了属性及其支持的浏览器。

![image](img/f266-01.jpg)

这些信息通常会被测量能力的站点跟踪工具聚合，但通常不会影响功能。这些信息有时被用于调整浏览器以占据屏幕上的可用空间，如下：

```javascript
window.resizeTo(screen.availWidth, screen.availHeight);
```

如之前所述，许多浏览器关闭了调整浏览器窗口的功能，因此此代码在所有情况下可能都无法工作。移动设备在屏幕尺寸方面的行为略有不同。运行 iOS 的设备始终返回设备处于竖持模式的尺寸（1024 × 768）。相反，Android 设备会正确调整`screen.width`和`screen.height`的值。

## history 对象 (The history Object)

`history`对象代表了自给定的窗口首次使用以来的用户导航历史。由于`history`是`window`的属性，每个浏览器窗口、标签页和框架（frame）都有其特定的`history`对象，专门对应于该窗口对象。出于安全考虑，无法确定用户访问过的 URL。但是，可以在不知道确切 URL 的情况下，在用户访问过的列表中向前向后导航。

`go()`方法可以在向后或向前两个方向上通过历史记录进行导航。该方法接受单个参数，这是一个整数，表示向后或向前移动的页数。负数表示向后历史移动（类似于点击浏览器的“后退”按钮），正数表示向前移动（类似于点击浏览器的“前进”按钮）。以下是一个示例：

```javascript
// 后退一页
history.go(-1);
// 前进一页
history.go(1);
// 前进两页
history.go(2);
```

`go()`方法的参数也可以是字符串，在这种情况下，浏览器将导航到历史中包含给定字符串的第一个位置。最近的位置可能是向后，也可能是向前。如果历史中没有匹配该字符串的记录，则该方法将不执行任何操作，例如所示：

```javascript
// 跳转到最近的 wrox.com 页面
```



`history.go("wrox.com");`

//我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。跳转到最近的 nczonline.net 页面

`history.go("nczonline.net");`

可以使用两个快捷方法 `back()` 和 `forward()` 来代替 `go()`。正如你所预期的，它们模拟了浏览器的后退和前进按钮，如下所示：

```
// 后退一页
history.back();

// 前进一页
history.forward();
```

`history` 对象还有一个属性 `length`，它指示历史记录栈中有多少项。该属性反映了历史记录栈中的所有项目，包括向后移动和向前移动的项目。对于加载到窗口、标签页或框架的第一页，`history.length` 等于 0。通过像此处所示测试此值，可以判断用户的起始点是否为你的页面：

```javascript
if (history.length == 0){
    // 这是用户窗口中的第一个页面
}
```

尽管并不经常使用，但 `history` 对象通常用于创建自定义的“后退”和“前进”按钮，并用于判断页面是否是用户历史记录中的第一个。HTML5 进一步增强了 `history` 对象。更多信息请见第 16 章。

![image](img/pen.gif)

每当页面 URL 发生时，历史记录栈中就会产生记录。对于 Internet Explorer 8+、Opera、Firefox、Safari 3+ 以及 Chrome，这包括 URL hash 的更改（因此，设置 `location.hash` 会导致这些浏览器的历史记录栈中插入新记录）。

## 总结

浏览器对象模型 (BOM) 基于 `window` 对象，该对象代表浏览器窗口和可见页面区域。`window` 对象兼作 ECMAScript 全局对象，因此所有全局变量和函数都成为它的属性，且所有原生构造函数和函数最初都存在于上面。本章讨论了 BOM 的以下元素：

* 当使用框架时，每个框架都有自己的 `window` 对象以及所有原生构造函数和函数的副本。每个框架都存储在 `frames` 集合中，通过位置和名称进行索引。
* 要引用其他框架（包括父框架），有多个 `window` 指针。
* `top` 对象始终指向最外层的框架，它代表整个浏览器窗口。
* `parent` 对象代表包含它的框架，`self` 指回 `window`。
* `location` 对象允许程序化访问浏览器的导航系统。通过设置属性，可以逐部分或全部更改浏览器的 URL。
* `replace()` 方法允许导航到新的 URL 并替换浏览器历史记录中当前显示的页面。
* `navigator` 对象提供了有关浏览器的信息。所提供的信息类型在很大程度上取决于所使用的浏览器，尽管某些常用属性（如 `userAgent`）在所有浏览器中都是可用的。

BOM 中其他两个可用对象的功能非常有限。`screen` 对象提供了有关客户端显示的信息。这些信息通常用于网站的指标收集。`history` 对象提供了对浏览器历史记录栈的有限窥视，允许开发者确定历史记录栈中有多少个网站，并赋予他们回退或前进到历史记录中任何页面的能力。

# 第 9 章：客户端检测

### 本章内容简介？

* 使用能力检测
* User-agent（用户代理）检测的历史
* 何时使用每种检测类型

尽管浏览器厂商已经共同努力实现通用接口，但事实仍然是每个浏览器都呈现出自己的能力和缺陷。跨平台的浏览器通常会有不同的问题，即使它们在技术上是相同版本。这些差异迫使 Web 开发者为最低标准进行设计，或者更常见的使用各种客户端检测方法来处理或绕过局限性。

客户端检测仍然 Web 开发中最具争议的话题之一。浏览器应该支持通用功能的观点贯穿于关于该主题的大多数讨论中。在理想世界中，情况确实如此。但在现实中，存在足够的浏览器差异和特性，使得客户端检测不仅是事后考虑，而且是开发策略至关重要的部分。

确定所使用的 Web 客户端有多种方法，每种方法都有优缺点。重要的是，客户端检测应该是解决问题的最后一步。当存在更常见的解决方案时，应使用该解决方案。针对通用解决方案进行设计，然后再进行扩展。

## 能力检测

最常用且广泛接受的客户端检测形式被称为能力检测（Capability Detection）。能力检测（也称为功能检测）的目标不是识别特定的浏览器，而是识别浏览器的能力。这种方法假设不需要特定的浏览器知识，而是通过判断所需的项是否存在来找到解决方案。能力检测的基本模式如下：

```
if (object.propertyInQuestion){
    //使用 object.propertyInQuestion
}
```

例如，在 Internet Explorer 5 之前，并不存在 DOM 方法 `document.getElementById()`。该方法在早期版本中并不存在，尽管可以使用非标准的 `document.all` 属性实现相同的功能。这导致了如下的能力检测分支：

```javascript
function getElement(id){
    if (document.getElementById){
        return document.getElementById(id);
    } else if (document.all){
        return document.all[id];
    } else {
        throw new Error("无法获取元素!");
    }
}
```

`getElement()` 函数的目的是返回一个具有给定 ID 的元素。由于 `document.getElementById()` 是实现此目标的标准方法，因此首先对其进行测试。如果该函数存在（未为 undefined），则使用它。否则，检查 `document.all` 是否可用，如果是，则使用它。如果两种方法都不可用（这极罕见），则抛出异常以指示函数无法工作。

能力检测中有两个重要的概念需要理解。正如刚才提到的，应该首先测试实现结果最常见的方法。在之前的示例中，这意味着在测试 `document.all` 之前测试 `document.getElementById()`。测试最常见的解决方案可以确保在常见情况下避免多次条件测试，从而优化代码执行效率。

第二个重要的概念是，你必须针对你想要使用的功能进行精确测试。仅仅因为某个功能存在并不意味着另一个功能也存在。考虑以下示例：

```javascript
function getWindowWidth(){
    if (document.all){ //假设为 IE
        return document.documentElement.clientWidth; // 错误用法！！！
    } else {
        return window.innerWidth;
    }
}
```

这个示例展示了能力检测的错误用法。`getWindowWidth()` 函数首先检查 `document.all` 是否存在。它确实存在，因此函数返回了 `document.documentElement.clientWidth`。正如第 8 章所讨论，Internet Explorer 8 及更早版本不支持 `window.innerWidth` 属性。这段代码中的问题在于，对 `document.all` 的测试并不一定意味着浏览器是 Internet Explorer。事实上，它可能是早期版本的 Opera，它同时支持 `document.all` 和 `window.innerWidth`。

## 更安全的能力检测

当你不仅验证功能是否存在，还验证该功能是否可能以恰当的方式行为时，能力检测才是最充分的。前一节中的示例依赖于对被测试对象的成员进行类型转换来判断其是否存在。虽然这可以告诉你该对象成员是否存在，但无法表明该成员是否就是你预期的那一个。考虑以下函数，它尝试判断一个对象是否可排序：

```javascript
// 避免！错误的能力检测 - 仅检查存在性
function isSortable(object){
    return !!object.sort;
}
```

该函数尝试通过检查 `sort()` 方法是否存在来判断一个对象是否可以排序。问题是，任何带有 `sort` 属性的对象都会返回 `true`：

```javascript
var result = isSortable({ sort: true });
```

仅仅测试属性是否存在并不能确定地表明该对象是可排序的。更好的方法是检查 `sort` 实际上是一个函数：

```javascript
// 更好 - 检查 sort 是否为函数
function isSortable(object){
    return typeof object.sort == "function";
}
```

这段代码中使用了 `typeof` 运算符来确定 `sort` 实际上是一个函数，因此可以调用它来对其中包含的数据进行排序。

尽可能使用 `typeof` 进行能力检测，但它并非万无一失。特别是宿主对象（host objects），并没有义务为 `typeof` 返回理性的值。最极端的例子发生在 Internet Explorer 中。在大多数浏览器中，如果 `document.createElement()` 存在，以下代码将返回 `true`：

```javascript
// 在 Internet Explorer <= 8 中无法正常工作
function hasCreateElement(){
    return typeof document.createElement == "function";
}
```

在 Internet Explorer 8 及更早版本中，该函数返回 `false`，因为 `typeof document.createElement` 返回 `"object"` 而不是 `"function"`。如之前提到的，DOM 对象是宿主对象，而在 Internet Explorer 8 及更早版本中，宿主对象是通过 COM 而不是 JScript 实现的。因此，实际函数 `document.createElement()` 被实现为一个 COM 对象，此时 `typeof` 返回 `"object"`。Internet Explorer 9 为 DOM 方法正确返回了 `"function"`。

Internet Explorer 还有其他使用 `typeof` 时行为不符合预期的例子。ActiveX 对象（仅在 Internet Explorer 中支持）的行为与其他对象非常不同。例如，在不使用 `typeof` 的情况下测试属性可能会导致错误，如下所示：

```javascript
// 在 Internet Explorer 中导致错误
var xhr = new ActiveXObject("Microsoft.XMLHttp");
if (xhr.open){ // 此处发生错误
    // 执行某些操作
}
```

仅仅像属性一样访问函数（如此示例所示）会导致 JavaScript 错误。使用 `typeof` 更安全；然而，Internet Explorer 对 `typeof xhr.open` 返回的是 `"unknown"`。这意味着，在浏览器环境中测试任何对象上函数存在的最完整方法是类似于如下的函数：

```javascript
// 来源：Peter Michaux
function isHostMethod(object, property) {
    var t = typeof object[property];
    return t=='function' ||
    (!!(t=='object' && object[property])) ||
    t=='unknown';
}
```

你可以如下所示使用该函数：

```javascript
result = isHostMethod(xhr, "open"); //true
result = isHostMethod(xhr, "foo"); //false
```

在了解浏览器特殊性的情况下，`isHostMethod()` 函数是今天最安全的使用。注意，宿主对象没有义务维护其当前的实现细节，或模拟已有的宿主对象行为。由于由于，如果实现发生变化，无法保证此函数或任何其他函数将继续保持准确。作为开发者，你必须根据尝试实现的功能来评估你的风险忍度。

![image](img/pen.gif)

关于 JavaScript 中能力检测细节的详尽讨论，请参阅 Peter Michaux 的文章“Feature Detection: State of the Art Browser Scripting”，地址为 [`peter.michaux.ca/articles/feature-detection-state-of-the-art-browser-scripting`](http://peter.michaux.ca/articles/feature-detection-state-of-the-art-browser-scripting)。

## 能力检测不是浏览器检测

检测特定的能力或一组能力并不一定意味着正在使用的浏览器。以下“浏览器检测”代码（或类似代码可以在许多网站上找到，它们是不恰当能力检测的示例：

```javascript
// 避免！不够具体
var isFirefox = !!(navigator.vendor && navigator.vendorSub);

// 避免！做了太多假设
var isIE = !!(document.all && document.uniqueID);
```

## 兼容模式检测

与能力检测类似，兼容性检测（quirks detection）旨在识别浏览器的特定行为。然而，兼容性检测并不是寻找被支持的功能，而是尝试找出哪些功能没有正常工作（“quirk”字面意思就是“缺陷”）。这通常涉及运行一短代码来确定某个功能未正常运行。例如，`Internet Explorer 8` 及更早版本中的一个 bug 会导致与原型属性同名的实例属性（如果其 `Enumerable` 属性被设置为 `false`）不会显示在 `for-in` 循环中。可以使用以下代码来测试这种兼容性：

![image](img/logo1.gif)

```
var hasDontEnumQuirk = function(){
    var o = { toString : function(){} };
    for (var prop in o){
        if (prop == "toString"){
            return false;
        }
    }
    return true;
}();
```

`QuirksDetectionExample01.htm`

这段代码使用匿名函数来测试该兼容性。创建了一个定义了 `toString()` 方法的对象。在标准的 ECMAScript 实现中，`toString` 应该作为一个属性在 `for-in` 循环中返回。

另一个常见的测试兼容性是 `3` 之前的 `Safari` 版本会枚举被遮的属性。可以通过以下方式进行测试：

```
var hasEnumShadowsQuirk = function(){
    var o = { toString : function(){} };
    var count = 0;
    for (var prop in o){
        if (prop == "toString"){
            count++;
        }
    }
    return (count > 1);
}();
```

`QuirksDetectionExample01.htm`

如果浏览器具有这种兼容性，一个带有自定义 `toString()` 方法的对象会导致 `for-in` 循环中出现两个 `toString` 实例。

兼容性通常是特定浏览器的，且通常被视为在后续版本中可能修复也可能不修复的 bug。由于兼容性检测需要运行代码，建议仅对你有直接影响的兼容性进行测试，并在脚本开始时完成，以避免后续干扰。

# 用户代理（User-Agent）检测

第三种也是最有争议的客户端检测方法称为 user-agent 检测。user-agent 检测使用浏览器的 user-agent 字符串来确定正在使用的具体浏览器。user-agent 字符串作为每个 HTTP 请求的响应头发送，并通过 JavaScript 中的 `navigator.userAgent` 访问。在服务端，查看 user-agent 字符串以确定使用的浏览器并采取相应操作是一种常见且被接受的做法。然而在客户端，user-agent 检测通常被认为是在能力检测和/或兼容性检测无法使用时的最后手段。

user-agent 字符串的争议之处在于其悠久的伪造历史，浏览器试图通过在 user-agent 字符串中包含错误或误导性信息来欺骗服务器。要理解这个问题，必须回顾自 Web 出现以来 user-agent 字符串的变。

## 历史

HTTP 规范（1.0 和 1.1 版本）均指出浏览器应该发送指定浏览器名称和版本的短 user-agent 字符串。`RFC 2616`（HTTP 1.1 协议规范）这样描述 user-agent 字符串：

产品令牌（Product tokens）允许通信应用程序通过软件名称和版本来识别自身。大多数使用产品令牌的字段还允许列出构成应用程序重要组成部分的子产品，并用空格分隔。按照惯例，产品按其对识别应用程序的重要性顺序列出。

规范进一步规定，user-agent 字符串应以 `token/product version` 的形式规定为产品列表。然而在现实中，user-agent 字符串从未那么简单。

## 早期浏览器

第一个网页浏览器 `Mosaic` 于 1993 年由国家超级计算机应用中心（NCSA）发布。它的 user-agent 字符串相当简单，格式类似于：

```
Mosaic/0.9
```



虽然这会根据操作系统和平台而异，但基本格式是简单且直观的。斜杠之前的文本表示产品名称（有时显示为`NCSA Mosaic`或其他衍生体），斜杠后的文本是产品版本。

当`Netscape Communications`开始开发其网页浏览器时，其代号为`Mozilla`（“Mosaic 杀手”的缩写）。第一个公开版本`Netscape Navigator 2`的 user-agent 字符串格式如下：

```
Mozilla/Version [Language] (Platform; Encryption)
```

Netscape 了将产品名称和版本作为 user-agent 字符串第一部分的传统，但在之后添加了以下信息：

- `Language` — 表示应用程序预期使用区域的语言代码。
- `Platform` — 运行应用程序的操作系统和/或平台。
- `Encryption` — 包含的安全加密类型。可能值为`U`（128 位加密）、`I`（40 位加密）和`N`（无加密）。

来自`Netscape Navigator 2`的典型 user-agent 字符串如下所示：

```
Mozilla/2.02 [fr] (WinNT; I)
```

该字符串表示正在使用`Netscape Navigator 2.02`，它是为法语国家编译的，运行在带有 40 位加密的`Windows NT`上。在当时，通过查看 user-agent 字符串中的产品名称很容易确定使用的是什么浏览器。

### Netscape Navigator 3 和 Internet Explorer 3

1996 年，`Netscape Navigator 3`发布并成为最流行的浏览器，超越了`Mosaic`。user-agent 字符串仅经历了细微变化，移除了语言令牌并允许包含有关操作系统或 CPU 的可选信息。格式变为：

```
Mozilla/Version (Platform; Encryption)
```

Windows 系统上`Netscape Navigator 3`的典型 user-agent 字符串如下：

```
Mozilla/3.0 (Win95; U)
```

该字符串表示`Netscape Navigator 3`运行在`Windows 95`上并带有 128 位加密。注意，当浏览器在 Windows 系统上运行时，省略了 OS 描述。

`Netscape Navigator 3`发布后不久，`Microsoft`发布了其第一个版本的网页浏览器`Internet Explorer 3`。由于当时`Netscape`是主导浏览器，许多服务器在提供页面之前会专门检查它。在`Internet Explorer`中无法访问页面将危及这一新兴浏览器的普及，因此决定创建一个与`Netscape` user-agent 字符串兼容的 user-agent 字符串。结果是采用了如下格式：

```
Mozilla/2.0 (compatible; MSIE Version; Operating System)
```

例如，运行在`Windows 95`上的`Internet Explorer 3.02`有此 user-agent 字符串：

```
Mozilla/2.0 (compatible; MSIE 3.02; Windows 95)
```

由于大多数浏览器嗅探只查看 user-agent 字符串的产品名称部分，`Internet Explorer`成功地自识别为`Mozilla`，与`Netscape Navigator`相同。此举引起了一些争议，因为它打破了浏览器识别的惯例。此外，真实的浏览器版本埋在字符串中间。

该字符串的另一个有趣部分是识别为`Mozilla 2.0`而不是`3.0`。由于`3.0`是当时的主导浏览器，使用它会更合理。实际原因仍然是一个谜——它更有可能是一个疏忽而非其他。

1997 年 8 月，`Netscape Communicator 4`发布。`Netscape`选择保留了版本 3 的以下 user-agent 字符串格式：

```
Mozilla/4.0 (Win98; I)
```

在`Windows 98`上使用版本 4 时，user-agent 字符串看起来所示。

当 Netscape 发布其浏览器的补丁和修复时，版本号会随之增加，如下 4.79 版本的 user-agent 字符串所示：

```
Mozilla/4.79 (Win98; I)
```

当微软发布 Internet Explorer 4 时，user-agent 字符串采用了更新后的版本，采用以下格式：

```
Mozilla/4.0 (compatible; MSIE Version; Operating System)
```

例如，运行在 Windows 98 上的 Internet Explorer 4 返回了以下 user-agent 字符串：

```
Mozilla/4.0 (compatible; MSIE 4.0; Windows 98)
```

通过这一更改，报告的 Mozilla 版本与 Internet Explorer 的实际版本实现了同步，从而能够识别这些第四代浏览器。遗憾的是，这种同步到此结束了。当 Internet Explorer 4.5（仅针对 Mac 发布）亮相时，Mozilla 版本仍保持为 4，而 Internet Explorer 版本发生了如下变化：

```
Mozilla/4.0 (compatible; MSIE 4.5; Mac_PowerPC)
```

在从版本 4 到版本 7 的 Internet Explorer 中，一直保持以下模式：

```
Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1)
```

Internet Explorer 8 引入了一个名为`Trident`的额外标记，它是渲染引擎的。格式变为：

```
Mozilla/4.0 (compatible; MSIE Version; Operating System; Trident/TridentVersion)
```

例如：

```
Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 5.1; Trident/4.0)
```

额外的`Trident`标记旨在帮助开发者判断 Internet Explorer 8 是否在兼容模式下运行。在这种情况下，MSIE 版本会变为 7，但 Trident 版本仍保留在 user-agent 字符串中：

```
Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; Trident/4.0)
```

添加这个额外的标记使得判断浏览器是 Internet Explorer 7（在这种情况下没有`Trident`标记）还是在兼容模式下运行的 Internet Explorer 8 成为可能。

Internet Explorer 9 稍微更改了这一格式。Mozilla 版本增加到 5.0，Trident 版本也增加到 5.0。Internet Explorer 9 的默认 user-agent 字符串如下所示：

```
Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Trident/5.0)
```

当 Internet Explorer 9 在兼容模式下运行时，旧的 Mozilla 版本和 MSIE 版本会恢复，而 Trident 版本仍保持为 5.0。例如，以下 user-agent 字符串是运行在 Internet Explorer 7 兼容模式下的 Internet Explorer 9：

```
Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.1; Trident/5.0)
```

所有这些更改都是为了确保旧的 user-agent 检测脚本能够继续工作，同时让新脚本能够获取额外信息。

## Gecko

Gecko 渲染引擎是 Firefox 的核心。当 Gecko 最初被开发时，它是作为成为 Netscape 6 的通用 Mozilla 浏览器的一部分存在的。Netscape 6 编写了一份规范，指示了未来所有版本中 user-agent 字符串应该如何构建。新格式与其在 4.x 版本之前使用的相对简单的 user-agent 字符串相比，发生了巨大的变化。格式如下：

```
Mozilla/MozillaVersion (Platform; Encryption; OS-or-CPU; Language;
PrereleaseVersion)Gecko/GeckoVersion
ApplicationProduct/ApplicationProductVersion
```

这个极其复杂的 user-agent 字符串倾注了心血。下表列出了每个部分的含义。

| 字符串 | 是否需要 | 描述 |
| --- | --- | --- |
| `MozillaVersion` | 是 | Mozilla 的版本。 |
| `Platform` | 是 | 浏览器运行的平台。可能的值包括 Windows、Mac 和 X11（用于 Unix X-windows 系统）。 |
| `Encryption` | 是 | 加密能力：U 代表 128 位，I 代表 40 位，N 代表无加密。 |
| `OS-or-CPU` | 是 | 浏览器运行的操作系统或运行浏览器的计算机处理器类型。如果平台是 Windows，则这是 Windows 版本（如 WinNT、Win95 等）。如果平台是 Macintosh，那么这就是 CPU（68k、用于 PowerPC 的 PPC 或 MacIntel）。如果平台是 X11，则这是通过 Unix 命令`uname -sm`获取的 Unix 操作系统名称。 |
| `Language` | 是 | 浏览器创建时使用的语言。 |
| `Prerelease Version` | 否 | 最初用于 Mozilla 的预发布版本号，现在表示 Gecko 渲染引擎的版本号。 |
| `GeckoVersion` | 是 | 以 yyyymmdd 格式表示的 Gecko 渲染引擎版本。 |
| `ApplicationProduct` | 否 | 使用 Gecko 的产品名称。可能是 Netscape、Firefox 等。 |
| `ApplicationProductVersion` | 否 | `ApplicationProduct`的版本；这独立于`MozillaVersion`和`GeckoVersion`。 |

为了更好地理解 Gecko user-agent 字符串格式，请考虑来自各种基于 Gecko 的浏览器的 user-agent 字符串。

Windows XP 上的 Netscape 6.21：

```
Mozilla/5.0 (Windows; U; Windows NT 5.1) Gecko/2001128 Netscape/6.21
```

Linux 上的 SeaMonkey 1.1：

```
Mozilla/5.0 (X11; U; Linux) Gecko/20060823 SeaMonkey/1.1
```

Windows XP 上的 Firefox 2.0.1：

```
Mozilla/5.0 (Windows NT 5.1; rv:2.0.1) Gecko/20071127 Firefox/2.0.1
```

OS X 上的 Camino 1.5：

```
Mozilla/5.0 (Macintosh; U; OS X; en; rv:1.8.6) Gecko/2007809 Camino/1.5
```

## WebKit

2003 年，苹果宣布将发布自己的浏览器，名为 Safari。Safari 的渲染引擎被称为 WebKit，最初是基于 Linux 的 Konqueror 浏览器使用的 KHTML 渲染引擎分支。几年后，WebKit 分离成一个独立的开源项目，专注于渲染引擎的开发。

这种新浏览器和渲染引擎的开发者面临着与 Internet Explorer 3 的问题：如何确保浏览器不被网站排除？答案是在 user-agent 字符串中放入足够的信息，以说服网站该浏览器与另一个流行的浏览器兼容。这导致了如下格式的 user-agent 字符串：

```
Mozilla/5.0 (Platform; Encryption; OS-or-CPU; Language)
AppleWebKit/AppleWebKitVersion (KHTML, like Gecko) Safari/SafariVersion
```

例如：

```
Mozilla/5.0 (Macintosh; U; PPC Mac OS X; en) AppleWebKit/124 (KHTML, like Gecko) Safari/125.1
```

正如你所看到的，这是另一个长 user-agent 字符串。它不仅考虑了 Apple WebKit 的版本，还考虑了 Safari 的版本。关于是否将浏览器标识为`Mozilla`的争议，出于兼容性考虑很快得到了解决。现在，所有基于 WebKit 的浏览器都将自己标识为`Mozilla 5.0`，与所有基于 Gecko 的浏览器相同。Safari 的版本通常是浏览器的构建号，而不一定代表发布版本号。因此，尽管`Safari 1.25`在 user-agent 字符串中包含`125.1`数字，但它们之间并不总是有一一的对应关系。

这个 user-agent 字符串中最有趣且具有争议的部分是在`Safari`1.0 之前的版本中加入了`(KHTML, like Gecko)`字符串。Apple 遭许多开发者的反对，他们认为这是在故意欺骗客户端和服务器，让它们认为 Safari 实际上是 Gecko（仿佛仅仅添加`Mozilla/5.0`还还不够似的）。Apple 的回应与 Internet Explorer user-agent 字符串受到批评时的微软非常类似：Safari 兼容`Mozilla`，网站不应该屏蔽 Safari 用户，因为他们看起来在使用不支持的浏览器。

当版本 3 发布时，Safari 的 user-agent 字符串略有扩展。现在使用以下版本标记来标识正在使用的 Safari 实际版本：

```
Mozilla/5.0 (Macintosh; U; PPC Mac OS X; en) AppleWebKit/522.15.5
(KHTML, like Gecko) Version/3.0.3 Safari/522.15.5
```

注意，此更改仅针对 Safari 而未针对 WebKit，因此其他基于 WebKit 的浏览器可能没有此更改。通常情况下，与 Gecko 一样，判断一个浏览器是基于 WebKit 的比尝试专门识别 Safari 更为常见。

## Konqueror

Konqueror 是与 KDE Linux 桌面环境捆带的浏览器，基于`KHTML`开源渲染引擎。虽然只在 Linux 上可用，但 Konqueror 拥有活跃的用户群。为了获得的兼容性，Konqueror 选择在 Internet Explorer 之后按如下格式化其 user-agent 字符串：

```
Mozilla/5.0 (compatible; Konqueror/Version; OS-or-CPU)
```

然而，Konqueror 3.2 引入了一项更改，以配合 WebKit user-agent 字符串的更改，如下所示标识自己为`KHTML`：

```
Mozilla/5.0 (compatible; Konqueror/Version; OS-or-CPU) KHTML/KHTMLVersion
(like Gecko)
```

这是一个示例：

```
Mozilla/5.0 (compatible; Konqueror/3.5; SunOS) KHTML/3.5.0 (like Gecko)
```

Konqueror 和`KHTML`的版本号往往一致，或在小数点位之差，例如 Konqueror`3.5`使用`KHTML`3.5.1。

## Chrome

Google 的 Chrome 浏览器使用 WebKit 作为其渲染引擎，但使用了不同的 JavaScript 引擎。Chrome 的 user-agent 字符串携带了来自 WebKit 的所有信息，还有一个用于 Chrome 版本的额外部分。格式如下：

```
Mozilla/5.0 (Platform; Encryption; OS-or-CPU; Language)
AppleWebKit/AppleWebKitVersion (KHTML, like Gecko)
Chrome/ChromeVersion Safari/SafariVersion
```

Chrome 7 的完整 user-agent 字符串如下：

```
Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US) AppleWebKit/534.7
(KHTML, like Gecko) Chrome/7.0.517.44 Safari/534.7
```

此后 WebKit 版本和 Safari 版本可能会一直保持同步，尽管这无法保证。

## Opera

在 user-agent 字符串方面，Opera 是最受争议的网页浏览器之一。Opera 的默认 user-agent 字符串是所有现代浏览器中最符合逻辑的，它正确地标识了自己及其版本。在版本 8 之前，Opera 的 user-agent 字符串采用以下格式：

```
Opera/Version (OS-or-CPU; Encryption) [Language]
```

在 Windows XP 电脑上使用 Opera`7.54`时，user-agent 字符串如下：



`Opera/7.54 (Windows NT 5.1; U) [en]`

随着 `Opera 8` 的发布，user-agent 字符串的语言部分变为了：

```
Opera/Version (OS-or-CPU; Encryption)
```

在 Windows XP 上使用 `Opera 8`，user-agent 字符串如下：

```
Opera/8.0 (Windows NT 5.1; U; en)
```

默认情况下，`Opera` 的 user-agent 字符串返回如下。为了通过其他浏览器，它被标识为 `Firefox` 或 `Internet Explorer`。`Opera 9` 的 user-agent 字符串如下：

```
Mozilla/5.0 (Windows NT 5.1; U; en)
```

`Opera 9.5` 的 user-agent 字符串包含了 `Opera` 版本，并将 `Opera 9.5` 标识为 `Firefox` 或 `Internet Explorer`。为了更好地兼容其他 `Opera`，更改了 user-agent 字符串。从 `Opera 9` 开始，有两种方法可以更改 user-agent 字符串。一种方法是将其标识为 `Firefox` 或 `Internet Explorer`。使用此选项时，user-agent 字符串会带有 `Mozilla` 和版本号。这里有一个示例：

```
Mozilla/5.0 (Windows NT 5.1; U; en) rv:20061208 Firefox/2.0
Opera/50
Mozilla/5.0 (Windows NT 5.1; U; en) Opera/50
```

第一种 user-agent 字符串将 `Opera 9.5` 标识为 `Firefox`，同时保留 `Opera` 版本。第二种字符串将 `Opera 9.5` 标识为 `Internet Explorer` 并包含 `Opera` 版本。尽管这些 user-agent 字符串可以通过 `Firefox` 或 `Internet Explorer` 的测试，但识别 `Opera` 的可能性是存在的。识别 `Opera` 的另一种方法是伪装成 `Firefox` 或 `Internet Explorer`。进一步增加难度的是 `Opera` 倾向于设置特定的 user-agent 字符串而不通知用户。例如，访问雅虎网站（`http://my.yahoo.com`）会导致 `Opera` 自动伪装。这使得通过 user-agent 字符串识别 `Opera` 变得非常困难。

![image](img/pen.gif)

## iOS 和 Android

`iOS` 和 `Android` 移动操作系统的默认浏览器都基于 `WebKit`，因此与它们的桌面版本共享相同的基本 user-agent 字符串格式。`iOS` 设备遵循此基本格式：

```
Mozilla/5.0 (Platform; Encryption; OS-or-CPU like Mac OS X; Language)
AppleWebKit/AppleWebKitVersion (KHTML, like Gecko) Version/BrowserVersion
Mobile/MobileVersion Safari/SafariVersion
```

注意这里添加了 `"like Mac OS X"` 用于检测 `Mac` 操作系统，并添加了 `Mobile` 标记（token）。`Mobile` 标记的版本号通常用不大，主要用于判断是移动端还是桌面端的 `WebKit`。根据设备不同，平台可能是 `"iPhone"`、`"iPod"` 或 `"iPad"`。例如：

```
Mozilla/5.0 (iPhone; U; CPU iPhone OS 3_0 like Mac OS X; en-us)
AppleWebKit/528.18 (KHTML, like Gecko) Version/4.0 Mobile/7A341 Safari/528.16
```

注意，在 `iOS 3` 之前，操作系统版本号并没有出现在用户代理（user-agent）字符串中。

默认 `Android` 浏览器通常遵循 `iOS` 设定的格式，但没有 `Mobile` 版本（`Mobile` 标记仍然存在）。例如：

```
Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91)
AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1
```

这个用户代理字符串来自一部 `Google Nexus One` 手机，但其他 `Android` 设备也遵循相同的模式。

## 使用用户代理检测（User-Agent Detection）

使用用户代理字符串来检测特定浏览器可能会变得复杂，因为由于现代浏览器中用户代理字符串的历史和用法。通常需要先确定你对浏览器信息的详细程度需求如何。通常情况下，知道渲染引擎和最低版本就足够确定正确的操作方案。例如，以下方法是不推荐的：

```javascript
if (isIE6 || isIE7) { //避免！！！
    //code
}
```

在这个示例中，如果浏览器是 `Internet Explorer` 版本 6 或 7，则执行该代码。这段代码非常脆弱，因为它依赖于特定的浏览器版本来决定做什么。版本 8 应该发生什么？每当 `Internet Explorer` 发布新版本时，这段代码都必须更新。然而，使用如下示例所示的相对版本号可以避免这个问题：

```javascript
if (ieVer >= 6){
    //code
}
```

这个重写的示例检查 `Internet Explorer` 版本是否至少为 6，以确定正确的操作方案。这样做确保了该代码在未来能够继续正常运行。浏览器检测脚本专注于这种识别浏览器的方法论。

## 识别渲染引擎

如前所述，浏览器的确切名称和版本并没有使用的渲染引擎重要。如果 `Firefox`、`Camino` 和 `Netscape` 都使用相同版本的 `Gecko`，它们的功能就是相同的。同样，任何使用与 `Safari 3` 相同版本 `Web` 的浏览器都可能具有相同的功能。因此，此脚本侧重于检测五大主流渲染引擎：`Internet Explorer`、`Gecko`、`WebKit`、`KHTML` 和 `Opera`。

该脚本使用模块增强模式（module-augmentation pattern）来封装检测脚本，避免添加不必要的全局变量。基础代码结构如下：

```javascript
var client = function(){
    var engine = {
        //渲染引擎
        ie: 0,
        gecko: 0,
        webkit: 0,
        khtml: 0,
        opera: 0,
        //特定版本
        ver: null
    };
    //在此处检测渲染引擎/平台/设备
    return {
        engine: engine
    };
}();
```

在代码中，声明了一个名为 `client` 的全局变量来存储信息。匿名函数内部有一个名为 `engine` 的局部变量，它包含一个带有默认设置的对象字面量。每个渲染引擎由一个设置为 0 的属性表示。如果检测到特定引擎，该引擎的版本将以浮点数值放入相应的属性中。渲染引擎的完整版本（字符串）被放入 `ver` 属性中。这种设置允许类似下面的代码：

```javascript
if (client.engine.ie) { //如果是 IE，client.engine.ie 大于 0
    //IE 特有代码
} else if (client.engine.gecko > 1.5){
    if (client.engine.ver == "1.8.1"){
        //执行针对该版本的特定操作
    }
}
```

每当检测到渲染引擎时，它在 `client.engine` 上的属性会被设置为大于 0 的数字，这会转换为布尔值 `true`。这允许在 `if` 语句中使用属性来确定正在使用的渲染引擎，即使不需要特定版本。由于每个属性都包含一个浮点值，可能会丢失某些版本信息。例如，字符串 `"1.8.1"` 在传递给 `parseFloat()` 时变为数字 `1.8`。`ver` 属性确保在必要时可以使用完整版本。

要识别正确的渲染引擎，你需要按照正确的顺序进行测试。由于用户代理的不一致性，乱测试可能会导致错误的结果。由于此原因，第一步是识别 `Opera`，因为它的用户代理字符串可能会完全模拟其他浏览器。`Opera` 的用户代理字符串是不可靠的，因为它在所有情况下都不会自标识为 `Opera`。

要识别 `Opera`，你需要寻找 `window.opera` 对象。该对象存在于 `Opera 5` 及之后版本中，用于识别浏览器信息并与浏览器直接交互。在 `7.6` 之后的版本中，一个方法返回浏览器版本。

```javascript
if (window.opera){
    engine.ver = window.opera.version();
    engine.opera = parseFloat(engine.ver);
}
```

下一个逻辑检测引擎是 `WebKit`。由于 `WebKit` 的用户代理字符串包含 `"WebKit"`，它是最符合逻辑的检查项。以下是如何操作的示例：

```javascript
var ua = navigator.userAgent;
if (window.opera){
    engine.ver = window.opera.version();
    engine.opera = parseFloat(engine.ver);
} else if (/AppleWebKit\/(\S+)/.test(ua)){
    engine.ver = ua["1"];
    engine.webkit = parseFloat(engine.ver);
}
```

有时候 `Safari` 的版本与 `WebKit` 的版本并不完全对应，可能存在次版本级别的差异。上一个表格指示了最可能的 `WebKit` 版本，但并非精确值。

下一个要测试的渲染引擎是 `KHTML`。再次，此用户代理（user-agent）字符串包含了 `"Gecko"`，因此在没有排除 `KHTML` 之前，你无法准确检测出基于 `Gecko` 的浏览器。`KHTML` 版本以类似于 `WebKit` 的格式包含在用户代理字符串中，因此使用了类似的正则表达式。此外，由于 `Konqueror 3.1` 及更早版本没有专门包含 `KHTML` 版本，因此使用了 `Konqueror` 的版本。这是一个示例：

```
var ua = navigator.userAgent;
if (window.opera){
    engine.ver = window.opera.version();
    engine.opera = parseFloat(engine.ver);
} else if (/AppleWebKit\/(\S+)/.test(ua)){
    engine.ver = RegExp["$1"];
    engine.webkit = parseFloat(engine.ver);
} else if (/KHTML\/(\S+)/.test(ua) || /Konqueror\/([^;]+)/.test(ua)){
    engine.ver = RegExp["$1"];
    engine.khtml = parseFloat(engine.ver);
}
```

再次，由于 `KHTML` 版本号与下一个标记之间用空格隔开，因此使用非空白字符来获取版本号的所有字符。然后将字符串版本的版本存储在 `engine.ver` 中，将浮点版本存储在 `engine.khtml` 中。如果用户代理字符串中没有 `KHTML`，则匹配 `Konqueror`，其后面紧跟一个斜杠，然后是所有非分号的字符。

如果 `WebKit` 和 `KHTML` 都已被排除，那么检查 `Gecko` 就是安全的。实际的 `Gecko` 版本并没有出现在用户代理中字符串 `"Gecko"` 之后，而是出现在字符串 `"rv:"` 之后。这需要比之前的测试更复杂的正则表达式，如例例所示：

```
var ua = navigator.userAgent;
if (window.opera){
    engine.ver = window.opera.version();
    engine.opera = parseFloat(engine.ver);
} else if (/AppleWebKit\/(\S+)/.test(ua)){
    engine.ver = RegExp["$1"];
    engine.webkit = parseFloat(engine.ver);
} else if (/KHTML\/(\S+)/.test(ua)){
    engine.ver = RegExp["$1"];
    engine.khtml = parseFloat(engine.ver);
} else if (/rv:([^\)]+)\) Gecko\/\d{8}/.test(ua)){
    engine.ver = RegExp["$1"];
    engine.gecko = parseFloat(engine.ver);
}
```

`Gecko` 版本号出现在 `"rv:"` 和右括号之间，因此为了提取版本号，正则表达式寻找所有非右括号的字符。正则表达式还寻找字符串 `"Gecko/"` 后面跟八个数字。如果模式匹配，则提取版本号并将其存储在相应的属性中。`Gecko` 版本号与 `Firefox` 版本相关，详如下表。

| Firefox 版本 | 最小 Gecko 版本 |
| --- | --- |
| 1.0 | 1.7.5 |
| 1.5 | 1.8.0 |
| 2.0 | 1.8.1 |
| 3.0 | 1.9.0 |
| 3.5 | 1.9.1 |
| 3.6 | 1.9.2 |
| 4.0 | 2.0.0 |

![image](img/pen.gif)

与 `Safari` 和 `WebKit` 一样，`Firefox` 和 `Gecko` 版本号之间的匹配并不精确。

`Internet Explorer` 是最后一个要检测的渲染引擎。版本号位于 `"MSIE"` 之后且分号之前，因此正则表达式非常简单，如下例所示：

```
var ua = navigator.userAgent;
if (window.opera){
    engine.ver = window.opera.version();
    engine.opera = parseFloat(engine.ver);
} else if (/AppleWebKit\/(\S+)/.test(ua)){
    engine.ver = RegExp["$1"];
    engine.webkit = parseFloat(engine.ver);
} else if (/KHTML\/(\S+)/.test(ua)){
    engine.ver = RegExp["$1"];
    engine.khtml = parseFloat(engine.ver);
} else if (/rv:([^\)]+)\) Gecko\/\d{8}/.test(ua)){
    engine.ver = RegExp["$1"];
    engine.gecko = parseFloat(engine.ver);
} else if (/MSIE ([^;]+)/.test(ua)){
    engine.ver = RegExp["$1"];
    engine.ie = parseFloat(engine.ver);
}
```

该渲染引擎检测脚本的最后部分在正则表达式中使用否定字符类来获取所有非分号的字符。尽管 `Internet Explorer` 通常将版本号保持为标准的浮点值，但并不总是如此。使用否定字符类 `[^;]` 是为了允许多个小数点和可能的字母。

### 识别浏览器

在大多数情况下，识别浏览器的渲染引擎已足以确定一个正确的行动方案。然而，仅凭渲染引擎并不意味着存在 `JavaScript` 功能。苹果的 `Safari` 浏览器和谷歌的 `Chrome` 浏览器都使用 `WebKit` 作为它们的渲染引擎，但使用不同的 `JavaScript` 引擎。这两个浏览器都会为 `engine.webkit` 返回一个值，但这不足以识别浏览器，如下所示：

```
var ua = navigator.userAgent;
if (window.opera){
    engine.ver = window.opera.version();
    engine.opera = parseFloat(engine.ver);
} else if (/AppleWebKit\/(\S+)/.test(ua)){
    engine.ver = RegExp["$1"];
    engine.webkit = parseFloat(engine.ver);
    //判断是 Chrome 还是 Safari
    if (/Chrome\/(\S+)/.test(ua)){
        browser.ver = RegExp["$1"];
        browser.chrome = parseFloat(browser.ver);
    } else if (/Version\/(\S+)/.test(ua)){
        browser.ver = RegExp["$1"];
        browser.safari = parseFloat(browser.ver);
    } else {
        //估算版本
        var safariVersion = 1;
        if (engine.webkit < 100){
            safariVersion = 1;
        } else if (engine.webkit < 312){
            safariVersion = 1.2;
        } else if (engine.webkit < 412){
            safariVersion = 1.3;
        } else {
            safariVersion = 2;
        }
        browser.safari = safariVersion;
    }
} else if (/KHTML\/(\S+)/.test(ua) || /Konqueror\/([^;]+)/.test(ua)){
```



`engine.ver = RegExp["$1"];`

`engine.khtml = parseFloat(engine.ver);`

```
} else if (/rv:([^\)]+)\) Gecko\/\d{8}/.test(ua)){
engine.ver = RegExp["$1"];
engine.gecko = parseFloat(engine.ver);
//确定是否为 Firefox
if (/Firefox\/(\S+)/.test(ua)){
browser.ver = RegExp["$1"];
browser.firefox = parseFloat(browser.ver);
}
} else if (/MSIE ([^;]+)/.test(ua)){
engine.ver = RegExp["$1"];
engine.ie = parseFloat(engine.ver);
}
```

对于 Firefox 版本，会找到字符串 `"Firefox/"`，并将其其后的数字提取为版本号。这只有在检测到的渲染引擎为 `Gecko` 时才会发生。

使用这段代码，你现在可以编写如下逻辑：

```
if (client.engine.webkit) { //如果是 WebKit
if (client.browser.chrome){
//为 Chrome 执行某些操作
} else if (client.browser.safari){
//为 Safari 执行某些操作
}
} else if (client.engine.gecko){
if (client.browser.firefox){
//为 Firefox 执行某些操作
} else {
//为其他 Gecko 浏览器执行某些操作
}
}
```

## 识别平台

很多情况下，只需知道渲染引擎就足够让你的代码运行了。但在某些情况下，平台特别受到关注。跨平台的浏览器（如 Safari、Firefox 和 Opera）在不同平台上可能会有不同的问题。三大平台是 Windows、Mac 和 Unix（包括 Linux 的变体）。为了能够检测这些平台，请如下所示向 `client` 添加一个新对象：

```
var client = function(){
var engine = {
//渲染引擎
ie: 0,
gecko: 0,
webkit: 0,
khtml: 0,
opera: 0,
//特定版本
ver: null
};
var browser = {
//浏览器
ie: 0,
firefox: 0,
safari: 0,
konq: 0,
opera: 0,
chrome: 0,
//特定版本
ver: null
};
var system = {
win: false,
mac: false,
x11: false
};
//在此处检测渲染引擎/平台/设备
return {
engine: engine,
browser: browser,
system: system
};
}();
```

这段代码引入了一个具有三个属性的 `system` 变量。`win` 属性表示平台是否为 Windows，`mac` 表示 Mac，`x11` 表示 Unix。与渲染引擎不同，平台信息通常非常有限，无法访问操作系统或版本。在这三个平台中，浏览器通常只报告 Windows 版本。因此，这些属性中的每个最初都用布尔值 `false` 表示，而不是数字（如渲染引擎属性那样）。

要确定平台，查看 `navigator.platform` 比查看 user-agent 字符串容易得多，因为后者在不同浏览器中表示平台信息的方式不同。`navigator.platform` 的可能值为 `"Win32"`、`"Win64"`、`"MacPPC"`、`"MacIntel"`、`"X11"` 和 `"Linux i686"`，它们是一致的。平台检测代码非常直观，如下所示：

```
var p = navigator.platform;
system.win = p.indexOf("Win") == 0;
system.mac = p.indexOf("Mac") == 0;
system.x11 = (p.indexOf("X11") == 0) || (p.indexOf("Linux") == 0);
```

这段代码使用 `indexOf()` 方法查看平台字符串的开头。要检测 Windows，平台检测代码只需查找平台字符串开头的字符串 `"Win"`（涵盖 `"Win32"` 和 `"Win64"`）。对 Mac 平台的测试以相同的方式进行，以兼容 `"MacPPC"` 和 `"MacIntel"`。对 Unix 的测试查找平台字符串开头的 `"X11"` 和 `"Linux"`，以确保这段代码能够应对其他变体。

![image](img/pen.gif)

早期的版本的 `Gecko` 对所有 Windows 平台返回 `"Windows"`，对所有 Mac 平台返回 `"Macintosh"`。这发生在 Firefox 1 发布之前，该版本稳定了 `navigator.platform` 的值。

### 识别 Windows 操作系统

如果平台是 Windows，可以从 user-agent 字符串中获取特定的操作系统信息。在 Windows XP 之前，有两个 Windows 版本：一个家庭用，一个商业用。家庭版简单地称为 Windows，并有特定的 95、98 和 ME 版本。商业版被称为 Windows NT，最终作为 Windows 2000 营销。Windows XP 代表了这两个产品线合并到从 Windows NT 演变而来的通用代码库。随后 Windows Vista 是在 Windows XP 上构建的。

这些信息很重要，因为 Windows 操作系统在 user-agent 字符串中的表示方式。下表显示了不同浏览器中表示各种 Windows 操作系统的不同字符串。

![image](img/f296-01.jpg)

由于 Windows 操作系统在 user-agent 字符串中的表示方式多种，检测并不完全简单。好消息是，自 Windows 2000 以来，字符串表示基本保持不变，只有版本号在变化。要检测不同的 Windows 操作系统，你需要一个正则表达式。记住，7 之前的 Opera 版本不再被广泛使用，因此没有必要为它们做准备。

第一步是匹配 Windows 95 和 Windows 98 的字符串。`Gecko` 与其他浏览器返回的字符串之间的区别在于缺少了 `"dows"` 以及在 `"Win"` 与版本号之间的空格。这是一个相当简单的正则表达式，在此处所示：

```
/Win(?:dows )?([^do]{2})/
```

使用这个正则表达式，捕获组返回操作系统版本。

在 2006–2007 年间，移动设备上浏览器的使用呈爆炸式增长。所有主流浏览器都有移动版本，也有运行在其他设备上的版本，因此识别这些情况至关重要。第一步是为所有需要检测的移动添加属性，如下所示：

```
var client = function(){
var engine = {
//rendering engines
ie: 0,
gecko: 0,
webkit: 0,
khtml: 0,
opera: 0,
//specific version
ver: null
};
var browser = {
//browsers
ie: 0,
firefox: 0,
safari: 0,
konq: 0,
opera: 0,
chrome: 0,
//specific version
ver: null
};
var system = {
win: false,
mac: false,
x11: false,
//mobile devices
iphone: false,
ipod: false,
ipad: false,
ios: false,
android: false,
nokiaN: false,
winMobile: false
};
//detection of rendering engines/platforms/devices here
return {
engine: engine,
browser: browser,
system: system
};
}();
```

检测 iOS 设备只需搜索字符串 `"iPhone"`、`"iPod"` 和 `"iPad"`：

```
system.iphone = ua.indexOf("iPhone") > -1;
system.ipod = ua.indexOf("iPod") > -1;
system.ipad = ua.indexOf("iPad") > -1;
```

除了知道 iOS 设备外，知道 iOS 的版本也很有帮助。在 iOS 3 之前，用户-agent 字符串简单地显示为 `"CPU like Mac OS X"`，而后来 iPhone 更改为 `"CPU iPhone OS 3_0 like Mac OS X"`，iPad 更改为 `"CPU OS 3_2 like Mac OS X"`。这意味着检测 iOS 需要一个正则表达式来考虑这些变化：

```
//determine iOS version
if (system.mac && ua.indexOf("Mobile") > -1){
if (/CPU (?:iPhone )?OS (\d+_\d+)/.test(ua)){
system.ios = parseFloat(RegExp.$1.replace("_", "."));
} else {
system.ios = 2; //can't really detect - so guess
}
}
```

检查系统是否为 Mac OS 且字符串中是否存在 `"Mobile"`，可以确保无论版本如何，`system.ios` 都会为非零。之后，使用正则表达式来确定用户-agent 字符串中是否存在 iOS 版本。如果是，则将 `system.ios` 设置为该版本的浮点值；否则，版本被硬编码为 `2`。（由于没有办法确定实际版本，因此选择上一个版本对于使此值有用是安全的。）

检测 Android 操作系统只需简单地搜索字符串 `"Android"` 并立即获取随其后的版本号：

```
//determine Android version
if (/Android (\d+.\d+)/.test(ua)){
system.android = parseFloat(RegExp.$1);
}
```

由于 Android 的所有版本都包含版本号，该正则表达式可以准确检测到所有版本并将 `system.android` 设置为正确的值。

诺基 N 系列手机也使用 WebKit。其用户-agent 字符串与其他基于 WebKit 的手机非常相似，例如：

```
Mozilla/5.0 (SymbianOS/9.2; U; Series60/3.1 NokiaN95/11.0.026;
Profile MIDP-2.0 Configuration/CLDC-1.1) AppleWebKit/413 (KHTML, like Gecko)
Safari/413
```

请注意，尽管诺基 N 系列手机在用户-agent 字符串中报告 `"Safari"`，但浏览器实际上并不是 Safari，尽管它是基于 WebKit 的。如所示，在用户-agent 字符串中简单检查 `"NokiaN"` 即可检测此系列手机：

```
system.nokiaN = ua.indexOf("NokiaN") > -1;
```

有了这些设备信息，可以使用如下代码来确定用户如何通过 WebKit 访问页面：

```
if (client.engine.webkit){
if (client.system.ios){
//iOS stuff
} else if (client.system.android){
//android stuff
} else if (client.system.nokiaN){
//nokia stuff
}
}
```

最后一个主要的移动设备平台是 Windows Mobile（以前称为 Windows CE），它适用于口袋 PC 和智能手机。由于这些设备在技术上属于 Windows 平台，因此 Windows 平台和操作系统将返回正确的值。对于 Windows Mobile 5.0 及之前的版本，这两种设备的用户-agent 字符串非常相似，如下：

```
Mozilla/4.0 (compatible; MSIE 4.01; Windows CE; PPC; 240x320)
Mozilla/4.0 (compatible; MSIE 4.01; Windows CE; Smartphone; 176x220)
```

第一个是口袋 PC 上的移动 Internet Explorer 4.01，第二个是智能手机上的相同浏览器。当对这两个字符串运行操作系统检测脚本时，`client.system.win` 将填充为 `"CE"`，因此可以使用此值对早期的 Windows Mobile 设备进行检测。注意，尽管诺基 N 系列手机在用户-agent 字符串中报告 `"Safari"`，但浏览器实际上并不是 Safari，尽管它是 WebKit 的。

### 识别游戏系统

浏览器变得日益流行的另一个领域是游戏系统。Wii 和 Playstation 3 都有内置或可下载的浏览器。这些浏览器的用户-agent 字符串如下：

```
Opera/9.10 (Nintendo Wii;U;1621; en)
Mozilla/5.0 (PLAYSTATION 3;2.00)
```

第一个是运行在 Wii 上的 Opera。它遵循原始 Opera 用户-agent 字符串。第二个来自 Playstation 3，它报告为大写，引发了对未来版本可能会更改大小的担忧。

在检测这些设备之前，你必须在 `client.system` 对象中添加相应的属性：

```
var client = function(){
var engine = {
//rendering engines
ie: 0,
gecko: 0,
webkit: 0,
khtml: 0,
opera: 0,
//specific version
ver: null
};
var browser = {
//browsers
ie: 0,
firefox: 0,
safari: 0,
konq: 0,
opera: 0,
chrome: 0,
//specific version
ver: null
};
var system = {
win: false,
mac: false,
x11: false,
//mobile devices
iphone: false,
ipod: false,
ipad: false,
ios: false,
android: false,
nokiaN: false,
winMobile: false,
//game systems
wii: false,
ps: false
};
//detection of rendering engines/platforms/devices here
return {
engine: engine,
browser: browser,
system: system
};
}();
```

以下代码可以检测每个这些游戏系统：

```
system.wii = ua.indexOf("Wii") > -1;
system.ps = /playstation/i.test(ua);
```

对于 Wii，简单测试字符串 `"Wii"` 就足够了。其余代码将识别出浏览器为 Opera 并在 `client.browser.opera` 中返回正确的版本号。对于 Playstation，使用正则表达式以不区分大小写的方式对用户-agent 字符串进行测试。

### 完整脚本

完整的 user-agent 检测脚本，包括渲染引擎、平台、Windows 操作系统、移动设备和游戏系统如下：

![image](img/logo1.gif)

```javascript
var client = function(){
//rendering engines
var engine = {
ie: 0,
gecko: 0,
webkit: 0,
khtml: 0,
opera: 0,
//complete version
ver: null
};
//browsers
var browser = {
//browsers
ie: 0,
firefox: 0,
safari: 0,
konq: 0,
opera: 0,
chrome: 0,
//specific version
ver: null
};
//platform/device/OS
var system = {
win: false,
mac: false,
x11: false,
//mobile devices
iphone: false,
ipod: false,
ipad: false,
ios: false,
android: false,
nokiaN: false,
winMobile: false,
//game systems
wii: false,
ps: false
};
//detect rendering engines/browsers
var ua = navigator.userAgent;
if (window.opera){
engine.ver = browser.ver = window.opera.version();
```



`engine.opera = browser.opera = parseFloat(engine.ver);`

```
} else if (/AppleWebKit\/(\S+)/.test(ua)){
engine.ver = RegExp["$1"];
engine.webkit = parseFloat(engine.ver);
//figure out if it's Chrome or Safari
if (/Chrome\/(\S+)/.test(ua)){
browser.ver = RegExp["$1"];
browser.chrome = parseFloat(browser.ver);
} else if (/Version\/(\S+)/.test(ua)){
browser.ver = RegExp["$1"];
browser.safari = parseFloat(browser.ver);
} else {
//approximate version
var safariVersion = 1;
if (engine.webkit < 100){
safariVersion = 1;
} else if (engine.webkit < 312){
safariVersion = 1.2;
} else if (engine.webkit < 412){
safariVersion = 1.3;
} else {
safariVersion = 2;
}
browser.safari = browser.ver = safariVersion;
}
} else if (/KHTML\/(\S+)/.test(ua) || /Konqueror\/([^;]+)/.test(ua)){
engine.ver = browser.ver = RegExp["$1"];
engine.khtml = browser.konq = parseFloat(engine.ver);
} else if (/rv:([^\)]+)\) Gecko\/\d{8}/.test(ua)){
engine.ver = RegExp["$1"];
engine.gecko = parseFloat(engine.ver);
//determine if it's Firefox
if (/Firefox\/(\S+)/.test(ua)){
browser.ver = RegExp["$1"];
browser.firefox = parseFloat(browser.ver);
}
} else if (/MSIE ([^;]+)/.test(ua)){
engine.ver = browser.ver = RegExp["$1"];
engine.ie = browser.ie = parseFloat(engine.ver);
}
//detect browsers
browser.ie = engine.ie;
browser.opera = engine.opera;
//detect platform
var p = navigator.platform;
system.win = p.indexOf("Win") == 0;
system.mac = p.indexOf("Mac") == 0;
system.x11 = (p == "X11") || (p.indexOf("Linux") == 0);
//detect windows operating systems
if (system.win){
if (/Win(?:dows )?([^do]{2})\s?(\d+.\d+)?/.test(ua)){
if (RegExp["$1"] == "NT"){
switch(RegExp["$2"]){
case "5.0":
system.win = "2000";
break;
case "5.1":
system.win = "XP";
break;
case "6.0":
system.win = "Vista";
break;
case "6.1":
system.win = "7";
break;
default:
system.win = "NT";
break;
}
} else if (RegExp["$1"] == "9x"){
system.win = "ME";
} else {
system.win = RegExp["$1"];
}
}
}
//mobile devices
system.iphone = ua.indexOf("iPhone") > -1;
system.ipod = ua.indexOf("iPod") > -1;
system.ipad = ua.indexOf("iPad") > -1;
system.nokiaN = ua.indexOf("NokiaN") > -1;
//windows mobile
if (system.win == "CE"){
system.winMobile = system.win;
} else if (system.win == "Ph"){
if(/Windows Phone OS (\d+.\d+)/.test(ua)){;
system.win = "Phone";
system.winMobile = parseFloat(RegExp["$1"]);
}
}
//determine iOS version
if (system.mac && ua.indexOf("Mobile") > -1){
if (/CPU (?:iPhone )?OS (\d+_\d+)/.test(ua)){
system.ios = parseFloat(RegExp.$1.replace("_", "."));
} else {
system.ios = 2;
}
}
}
```

任何 HTML 或 XML 文档都可以使用 `DOM` 表示为节点的层次结构。有几种节点类型，每种类型都代表文档中不同的信息和/或标记。每种节点类型具有不同的特征、数据和方法，且每个节点都可能与其他节点存在关系。这些关系形成了一个层次结构，允许标记被表示为以特定节点为根的树。例如，考虑以下 HTML：

```
<<html>
    <head>
        <title>Sample Page</title>
    </head>
    <body>
        <p>Hello World!</p>
    </body>
</html>
```

这个简单的 HTML 文档可以以层次结构表示出来，如图图 10-1

![image](img/f310-01.jpg)

`document` 节点将每个文档表示为根。在这个示例中，`document` 节点的唯一节点是 `html` 元素，它被称为文档元素。文档元素是文档中最外层的元素，所有其他元素都存在于其中。每个文档只能有一个文档元素。在 HTML 页面中，文档元素始终是 `html` 元素。在 XML 中，由于没有预定义的元素，任何元素都可以作为文档元素。

每一处标记都可以通过树中的节点来表示：HTML 元素由元素节点表示，属性由属性节点表示，文档类型由文档类型节点表示，注释由注释节点表示。总共有 12 种节点类型，它们都继承自一个基础类型。

## 节点类型

DOM Level 1 描述了一个名为 `Node` 的接口，`DOM` 中的所有节点类型都应该实现该接口。`Node` 接口在 JavaScript 中实现为 `Node` 类型，在 Internet Explorer 之外的所有浏览器中都可以访问。JavaScript 中所有的节点类型都继承自 `Node`，因此所有节点类型共享相同的基本属性和方法。

每个节点都有一个 `nodeType` 属性，指示它是哪种节点。节点类型由 `Node` 类型上的以下 12 个数字常量之一表示：

- `Node.ELEMENT_NODE` (1)
- `Node.ATTRIBUTE_NODE` (2)
- `Node.TEXT_NODE` (3)
- `Node.CDATA_SECTION_NODE` (4)
- `Node.ENTITY_REFERENCE_NODE` (5)
- `Node.ENTITY_NODE` (6)
- `Node.PROCESSING_INSTRUCTION_NODE` (7)
- `Node.COMMENT_NODE` (8)
- `Node.DOCUMENT_NODE` (9)
- `Node.DOCUMENT_TYPE_NODE` (10)
- `Node.DOCUMENT_FRAGMENT_NODE` (11)
- `Node.NOTATION_NODE` (12)

通过与这些常量之一进行比较，很容易确定节点的类型，如下：

```
if (someNode.nodeType == Node.ELEMENT_NODE){   //在 IE < 9 中不起作用
    alert("Node is an element.");
}
```

此示例将 `someNode.nodeType` 与 `Node.ELEMENT_NODE` 常量进行比较。如果它们相等，说明 `someNode` 实际上是一个元素。遗憾的是，由于 Internet Explorer 8 及更版本没有暴露 `Node` 类型构造函数，此代码会导致错误。为了跨浏览器兼容性，最好将 `nodeType` 属性与数值进行比较，如下所示：

```
if (someNode.nodeType == 1){   //在所有浏览器中均有效
    alert("Node is an element.");
}
```

并不是所有的节点类型都受浏览器支持。开发者通常处理的是元素节点和文本节点。本章后面的部分将讨论每种节点类型的支持程度和用法。

## nodeName 和 nodeValue 属性

`nodeName` 和 `nodeValue` 两个属性提供了关于节点的特定信息。这些属性的值完全取决于节点类型。在使用其中任何一个值之前，最好先测试节点类型，如下面代码所示：

```
if (someNode.nodeType == 1){
    value = someNode.nodeName;   //将是元素的标签名
}
```

在例例中，检查了节点类型以判断节点是否为元素。如果是，则将 `nodeName` 值赋值给变量。对于元素，`nodeName` 始终等于元素的标签名，而 `nodeValue` 始终为 `null`。

## 节点关系

文档中的所有节点都与其他节点有关系。这些关系是用传统的家庭关系来描述的，就像文档树是一个家族树一样。在 HTML 中，`body` 元素被认为是 `html` 元素的元素；同样，`html` 元素被认为是 `body` 元素的父元素。`head` 元素被认为是 `body` 元素的兄弟，因为它们共享同一个直接父元素 `html` 元素。

每个节点都有一个 `childNodes` 属性，包含一个 `NodeList`。`NodeList` 是一个类数组对象，用于存储一个可以通过位置访问的节点有序列表。请记住，`NodeList` 并不是 `Array` 的实例，尽管可以使用括号符号访问其值，并且存在 `length` 属性。`NodeList` 对象的独特之处在于，它们实际上是针对 `DOM` 结构运行的查询，因此更改将反映在 `NodeList` 对象中。通常说 `NodeList` 是一个活的视图，而不是它首次访问时的快照。

以下示例展示了如何通过括号符号或使用 `item()` 方法访问在 `NodeList` 中的节点：

```
var firstChild = someNode.childNodes[0];
var secondChild = someNode.childNodes.item(1);
var count = someNode.childNodes.length;
```

注意，如前所述，可以使用 `Array.prototype.slice` 将 `NodeList` 对象转换为数组。考虑以下示例：

```javascript
//在 IE8 中不起作用
arrayOfNodes = Array.prototype.slice.call(someNode.childNodes,0);
```

这在 Internet Explorer 8 之外的所有浏览器中均有效，8 会抛出错误，因为 `NodeList` 实现为 COM 对象，因此在需要 JScript 对象的地方无法使用。下面的函数：

```javascript
function convertToArray(nodes){
    var array = null;
    try {
        array = Array.prototype.slice.call(nodes, 0);  非 IE 及 IE9+
    } catch (ex) {
        array = new Array();
        for (var i=0, len=nodes.length; i < len; i++){
            array.push(nodes[i]);
        }
    }
    return array;
}
```

每个节点都有一个 `parentNode` 属性，指向其在文档树中的父节点。`childNodes` 包含的所有节点都有相同的节点，因此它们的每个 `parentNode` 属性都指向同一个节点。此外，`childNodes` 列表中的每个节点都被认为是同一列表中其他节点的兄弟。可以通过 `previousSibling` 和 `nextSibling` 属性从列表中的一个节点导航到另一个节点。列表中的第一个节点的 `previousSibling` 属性值为 `null`，而列表中的最后一个节点的 `nextSibling` 属性值值为 `null`，如下所示：

```javascript
if (someNode.nextSibling === null){
    alert("Last node in the parent's childNodes list.");
} else if (someNode.previousSibling === null){
    alert("First node in the parent's childNodes list.");
}
```

注意，如果只有一个子节点，`nextSibling` 和 `previousSibling` 都将为 `null`。

父节点与其第一个、最后一个子节点之间存在另一种关系。`firstChild` 和 `lastChild` 属性分别指向 `childNodes` 列表中的第一个和最后一个节点。`someNode.firstChild` 的值始终等于 `someNode.childNodes[0]`，而 `someNode.lastChild` 的值始终等于 `someNode.childNodes[someNode.childNodes.length-1]`。如果只有一个子节点，`firstChild` 和 `lastChild` 指向同一个节点；如果没有子节点，则 `firstChild` 和 `lastChild` 均为 `null`。所有这些关系都有助于在文档结构中的节点之间轻松导航。图 10-2 解释了这些关系。

图 10-2

![image](img/f313-01.jpg)

有了所有这些关系，`childNodes` 属性与其说是必要的，倒不如说是方便，因为只需简单地使用关系指针就可以到达文档树中的任何节点。另一个方便的方法是 `hasChildNodes()`，如果节点具有一个或多个子节点，它返回 `true`，并且比查询 `childNodes` 列表的长度更高效。

每个节点都共有的最后一个关系是 `ownerDocument`。它是指向代表整个文档的文档节点的指针。节点被认为由创建它们的文档所所有（通常与它们所在的文档是同一个），因为节点不能同时存在于两个或多个文档中。该属性提供了一种快速访问文档节点的方法，而无需向上遍历节点层次结构直到到达顶部。

![image](img/pen.gif)

尽管所有节点类型都继承自 `Node`，但并不是所有节点类型都可以拥有子节点。节点类型之间的差异将在本章稍后部分讨论。

## 节点操作

由于所有关系指针都是只读的，因此有几种方法可以操作节点。最常用的方法是 `appendChild()`，它将一个节点添加到 `childNodes` 列表的末尾。这样做会更新新添加节点、父节点以及 `childNodes` 列表中上一个最后一个子节点中的所有关系指针。完成后，`appendChild()` 返回新添加的节点。以下是一个示例：

```
var returnedNode = someNode.appendChild(newNode);
alert(returnedNode == newNode);         //true
alert(someNode.lastChild == newNode);   //true
```

如果传递到 `appendChild()` 的节点已经是文档的一部分，它将从之前的位置被移除并置于新位置。尽管 DOM 树是由系列指针连接的，但任何 DOM 节点在文档中不能存在于一个以上的位置。因此，如果你调用 `appendChild()` 并传入父节点的第一个子节点（如下例所示），它将成为最后一个子节点：

```javascript
//假设 someNode 有多个子节点
var returnedNode = someNode.appendChild(someNode.firstChild);
alert(returnedNode == someNode.firstChild);  //false
alert(returnedNode == someNode.lastChild);   //true
```



当需要将节点放置在`childNodes`列表中的特定位置（而不仅仅是末尾）时，可以使用`insertBefore()`方法。`insertBefore()`方法接受两个参数：要插入的节点和一个参考节点。要插入的节点将成为参考节点的前一个兄弟，并最终由该方法返回。如果参考节点为`null`，则`insertBefore()`的作用与`appendChild()`相同，如下例所示：

```javascript
//作为最后一个子节点插入
returnedNode = someNode.insertBefore(newNode, null);
alert(newNode == someNode.lastChild);  //true

//作为新的第一个节点插入
returnedNode = someNode.insertBefore(newNode, someNode.firstChild);
alert(returnedNode == newNode);         //true
alert(newNode == someNode.firstChild);  //true

//在最后一个子节点之前插入
returnedNode = someNode.insertBefore(newNode, someNode.lastChild);
alert(newNode == someNode.childNodes[someNode.childNodes.length-2]);  //true
```

`appendChild()`和`insertBefore()`在插入节点时都不会移除任何节点。`replaceChild()`方法接受两个参数：要插入的节点和要替换的节点。被替换的节点由函数返回，并从文档树中完全移除，而插入的节点占据其位置。以下是一个示例：

```javascript
//替换第一个子节点
var returnedNode = someNode.replaceChild(newNode, someNode.firstChild);

//替换最后一个子节点
returnedNode = someNode.replaceChild(newNode, someNode.lastChild);
```

当使用`replaceChild()`插入节点时，所有的关系指针都会从它被替换的节点那里复制。尽管被替换的节点在技术上仍属于同一个文档，但它不再在文档中具有特定的位置。

若要在不替换节点的情况下移除节点，你可以使用`removeChild()`方法。该方法接受一个参数，即要移除的节点。被移除的节点将作为函数的返回值返回，如下例所示：

```javascript
//移除第一个子节点
var formerFirstChild = someNode.removeChild(someNode.firstChild);

//移除最后一个子节点
var formerLastChild = someNode.removeChild(someNode.lastChild);
```

与`replaceChild()`类似，通过`removeChild()`移除的节点仍然由文档所有，但在文档中没有特定的位置。

这四种方法都作用于特定节点的直接子节点，这意味着要使用它们，你必须知道其直接父节点（可以通过之前提的`parentNode`属性访问）。并不是所有节点类型都可以拥有子节点，如果你尝试在不支持子节点的节点上使用这些方法，它们将抛出错误。

## 其他方法

所有节点类型共有的另外两个方法中的是`cloneNode()`，它会在调用该方法的节点上创建一个精确的克隆。`cloneNode()`方法接受一个布尔参数，指示是否执行深拷贝。当参数为`true`时，使用深拷贝，克隆节点及其整个子树；当参数为`false`时，仅克隆初始节点。返回的克隆节点由文档所有，但没有分配父节点。因此，克隆节点是一个孤儿，在通过`appendChild()`、`insertBefore()`或`replaceChild()`添加之前，它不存在于文档中。例如，考虑以下HTML：

```html
<ul>
    <li>item 1</li>
    <li>item 2</li>
    <li>item 3</li>
</ul>
```

（注：修正了原文错误的标签符号）如果将此`<ul>`元素的引用存储在名为`myList`的变量中，下面的代码显示了`cloneNode()`方法的两种模式：

```javascript
var deepList = myList.cloneNode(true);
alert(deepList.childNodes.length);     //3 (IE < 9) 或 7 (others)

var shallowList = myList.cloneNode(false);
alert(shallowList.childNodes.length);  //0
```

在此示例中，`deepList`填充了`myList`的深拷贝。这意味着`deepList`有三个列表项，每个项都包含文本。变量`shallowList`包含`myList`的浅拷贝，因此它没有子节点。`deepList.childNodes.length`的差异由于Internet Explorer 8及更早版本与其他浏览器处理空白字符的方式不同。在版本9之前的Internet Explorer不为空白字符创建节点。

`cloneNode()`方法不会复制你添加到DOM节点上的JavaScript属性，例如事件处理器。该方法仅复制属性和（可选的）子节点。其他内容都会丢失。Internet Explorer存在一个bug，事件处理器也会被克隆，因此建议在克隆之前移除事件处理器。

最后剩余的方法是`normalize()`。它的唯一工作是处理文档子树中的文本节点。由于解析器的实现或DOM操作，可能会产生不包含任何文本的文本节点，或者互为兄弟节点的文本节点。当在节点上调用`normalize()`时，会搜索该节点的后代以检查这两种情况。如果发现空文本节点，则会将其删除；如果文本节点是紧相邻的兄弟节点，它们将合并为了单个文本节点。该方法将在本章稍后部分进一步讨论。

# 文档类型 (Document Type)

JavaScript通过`Document`类型表示文档节点。在浏览器中，文档对象是`HTMLDocument`的实例（它继承自`Document`），代表整个HTML页面。文档对象是`window`的一个属性，因此可以全局访问。`Document`节点具有以下特征：

* `nodeType`为9。
* `nodeName`为`"#document"`。
* `nodeValue`为`null`。
* `parentNode`为`null`。
* `ownerDocument`为`null`。
* 子节点可以是`DocumentType`（最多一个）、`Element`（最多一个）、`ProcessingInstruction`（处理指令）或`Comment`（注释）。

`Document`类型可以表示HTML页面或其他基于XML的文档，尽管最常见的用法是通过`document`对象的`HTMLDocument`实例。文档对象可以获取有关页面的信息，并操作其外观和底层结构。

![image](img/pen.gif)

在Firefox、Safari、Chrome和Opera的脚本中可以使用`Document`类型构造函数和原型。版本9之前的Internet Explorer仍然没有暴露`Document`。`HTMLDocument`类型构造函数和原型在所有浏览器中均可用，包括从版本8开始的Internet Explorer。

# 文档节点 (Document Children)

尽管DOM规范规定`Document`节点可以是`DocumentType`、`Element`、`ProcessingInstruction`或`Comment`，但对于子节点有两个内置快捷方式。第一个是`documentElement`属性，它始终指向HTML页面中的`<html>`元素。文档元素始终出现在`childNodes`列表中，但`documentElement`属性提供了更快速、更直接的元素访问方式。考虑以下简单页面：

```html
<html>
    <body>
    </body>
</html>
```

当此页面被浏览器解析时，文档只有一个子节点，即`<html>`元素。该元素既可以通过`documentElement`通过`childNodes`列表访问，如下：

```javascript
var html = document.documentElement;      //获取 <html> 的引用
alert(html === document.childNodes[0]);   //true
alert(html === document.firstChild);      //true
```

此示例显示`documentElement`、`firstChild`和`childNodes[0]`的值都是相同的——三者都指向`<html>`元素。

作为`HTMLDocument`的实例，文档对象还有一个`body`属性，直接指向`<body>`元素。由于这是开发者最常用的元素，`document.body`在JavaScript中往往被频繁地使用，如下示例所示：

```javascript
var body = document.body;    //获取 <body> 的引用
```

`document.documentElement`和`document.body`在所有主流浏览器中都受支持。

`Document`的另一个可能的子节点是`DocumentType`。`<!DOCTYPE>`标签被视为与文档其他部分独立的实体，其信息可以通过`doctype`属性（浏览器中的`document.doctype`）访问，如下：

```javascript
var doctype = document.doctype;   //获取 <!DOCTYPE> 的引用
```

浏览器对`document.doctype`的支持差异很大，描述如下：

* Internet Explorer 8及更早版本 —— 文档类型如果存在，会被误解为注释并被视为`Comment`节点。`document.doctype`始终为`null`。
* Internet Explorer 9+及Firefox —— 文档类型如果存在，它是文档的第一个子节点。`document.doctype`是一个`DocumentType`节点，可以通过`document.firstChild`或`document.childNodes[0]`访问相同的节点。
* Safari、Chrome和Opera —— 文档类型如果存在，会被解析，但不会被视为文档的子节点。`document.doctype`是一个`DocumentType`节点，但该节点不会出现在`document.childNodes`中。

由于浏览器对`document.doctype`的支持不一致，它的用处有限。

出现在`<html>`元素之外的注释从技术上讲是文档的子节点。再次，浏览器对于这些注释是否能被正确识别和表示存在差异巨大。考虑以下HTML页面：

```html
<!-- first comment -->
<html>
    <body>
    </body>
</html>
<!-- second comment -->
```

此页面似乎有三个子节点：一个注释、一个`<html>`元素和另一个注释。逻辑上，你期望`document.childNodes`拥有三个项，对应于代码中出现的内容。但在实践中，浏览器处理`<html>`元素之外注释的方式有三种非常不同的方法：

* Internet Explorer 8及更早版本、Safari 3.1及后续版本、Opera和Chrome会为第一个注释创建一个注释节点，但不会为第二个注释创建。第一个注释成为`document.childNodes`中的第一个节点。
* Internet Explorer 9及后续版本会为第一个注释创建一个作为`document.childNodes`部分的注释节点。它们也会为第二个注释创建一个作为`document.childNodes`部分。
* Firefox和3.1之前的Safari会忽略所有注释。

再次，由于行为不一致，访问`<html>`元素之外的注释基本上没有用。

在大多数情况下，`appendChild()`、`removeChild()`和`replaceChild()`方法不用于`document`，因为文档类型（如果存在）是只读的，且只能有一个子节点。

# 文档信息 (Document Information)

文档对象作为`HTMLDocument`的实例，拥有一些标准`Document`对象没有的属性。这些属性提供了有关加载页面的信息。第一个此类属性是`title`，它包含`<title>`元素的文本，并显示在浏览器标题栏或标签页上。该属性用于获取当前页面标题并修改，使更改反映在浏览器标题栏中。更改`title`属性的值不会改变`<title>`元素。示例如下：

```javascript
//获取文档标题
var originalTitle = document.title;

//设置文档标题
document.title = "新标题";
```

接下来的三个属性都与页面请求有关：`URL`、`domain`和`referrer`。`URL`属性包含完整完整URL（地址栏中的URL），`domain`属性仅包含域名，而`referrer`属性提供链接到此页面的URL。如果没有引用页，`referrer`属性可能为空字符串。所有这些信息在请求头中都是可用的，并通过这些属性在JavaScript中提供，如下：

```javascript
//获取完整 URL
var url = document.URL;

//获取域名
var domain = document.domain;

//获取引用页
var referrer = document.referrer;
```

`URL`和`domain`属性是相关的。例如，如果`document.URL`是[`www.wrox.com/WileyCDA/`](http://www.wrox.com/WileyCDA/)，那么`document.domain`将是[www.wrox.com](http://www.wrox.com)。

在这三个属性中，`domain`属性是唯一可以设置的。由于安全问题，对`domain`的赋值值某些限制。如果URL包含子域名，例如[p2p.wrox.com](http://p2p.wrox.com)，则`domain`只能设置为`wrox.com`（当URL包含“www,”时情况也是如此，例如[www.wrox.com](http://www.wrox.com)）。该属性永远不能设置为URL中不包含的域名，如下所示：

```
//page from p2p.wrox.com
document.domain = "wrox.com";        //成功 (succeeds)
document.domain = "nczonline.net";   //错误 (error!)
```

当页面上存在来自不同子域名的`frame`或`iframe`时，设置`document.domain`的能力非常有用。由于跨域安全限制，来自不同子域名的页面无法通过JavaScript相互通信。通过将每个页面中的`document.domain`设置为相同的值，页面就可以互相访问对方的JavaScript对象。例如，如果页面从[www.wrox.com](http://www.wrox.com)加载，并且它包含一个从[p2p.wrox.com](http://p2p.wrox.com)加载的`iframe`，每个页面的`document.domain`字符串将是不同的，外部页面和内部页面限制访问彼此的JavaScript对象。如果每个页面中的`document.domain`值设置为`wrox.com`，页面就可以进行通信。

浏览器的进一步限制允许在`domain`属性被放宽后不再对其进行收紧。这意味着你不能将`document.domain`设置为`wrox.com`，然后尝试将其设回`p2p.wrox.com`，因为后者会导致错误，如下所示：

```
//page from p2p.wrox.com
document.domain = "wrox.com";        //放宽 -loosen - 成功
document.domain = "p2p.wrox.com";    //收紧 -tighten - 错误!
```



此限制存在于所有浏览器中，但从 Internet Explorer 8 版本开始实现。

## 定位元素

也许最常见的 DOM 活动是获取特定元素或一组元素的引用，以执行某些操作。这种能力通过`document`对象上的多个方法提供。`Document`类型提供了两种方法来实现此目的：`getElementById()`和`getElementsByTagName()`。

`getElementById()`方法接受单个参数——要检索的元素的`ID`——如果找到，它将返回该元素；如果不存在具有该`ID`的元素，则返回`null`。`ID`必须与页面上元素的`id`属性完全匹配，包括字符的大小写。请考虑以下元素：

```html
<div id="myDiv">Some text</div>
```

可以使用以下代码获取此元素：

```javascript
var div = document.getElementById("myDiv");    //获取对 <div> 的引用
```

然而，以下代码在 Internet Explorer 7 及更早版本之外的所有浏览器中都将返回`null`：

```javascript
var div = document.getElementById("mydiv");    //无法工作 (在 IE <= 7 中除外)
```

8 之前的版本，版本 8 之前的 Internet Explorer 将 ID 视为不区分大小写的，因此 "myDiv" 和 "mydiv" 被视为同一个元素 ID。

如果页面中存在多个具有相同`ID`的元素，`getElementById()`返回文档中首先出现的元素。Internet Explorer 7 及更早版本在此处增加了一个有趣的特性，还会返回`name`属性匹配给定`ID`的表单元素（`<input>`、`<textarea>`、`<button>`和`<select>`）。如果这些表单元素之一的`name`属性等于指定的`ID`，并且它在文档中出现在给定`ID`的元素之前，Internet Explorer 将返回该表单元素。这是一个示例：

```html
<input type="text" name="myElement" value="Text field">
<div id="myElement">A div</div>
```

使用此 HTML，在 Internet Explorer 7 中调用`document.getElementById()`会返回`<input>`元素的引用，而在所有其他浏览器中，相同的调用返回`<div>`元素的引用。为了避免 Internet Explorer 中出现这个问题，你应该确保表单字段没有等同于其他元素 ID 的`name`属性。

`getElementsByTagName()`方法是另一个常用的检索元素引用的方法。它接受单个参数——要检索的元素的标签名称——并返回一个包含零或多个元素的`NodeList`。在 HTML 文档中，此方法返回一个`HTMLCollection`对象，它与`NodeList`非常相似，因为它被视为“动态”（live）集合。例如，以下代码检索页面中的所有`<img>`元素并返回一个`HTMLCollection`：

```javascript
var images = document.getElementsByTagName("img");
```

此代码将`HTMLCollection`对象存储在`images`变量中。与`NodeList`对象一样，`HTMLCollection`对象中的项目可以使用括号符号或`item()`方法进行访问。对象中的元素数量可以通过`length`属性获取，如下示例所示：

```javascript
alert(images.length);        //输出图片数量
alert(images[0].src);        //输出第一张图片的 src 属性
alert(images.item(0).src);   //输出第一张图片的 src 属性
```

`HTMLCollection`对象还有一个额外方法`namedItem()`，它允许你通过名称引用集合中的项目。例如，假设你在页面中有如下的`<img>`元素：

```html
<img src="myimage.gif" name="myImage">
```

可以从`images`变量中检索到此`<img>`元素的引用：

```javascript
var myImage = images.namedItem("myImage");
```

通过这种方式，`HTMLCollection`除了索引项目外，还让你访问命名项目，从而更容易获取你精确需要的元素。你也可以使用括号符号访问命名项目，如以下示例所示：

对于`HTMLCollection`对象，括号符号可以使用数字或字符串索引。在后台，数字索引调用`item()`，字符串索引调用`namedItem()`。

要检索文档中的所有元素，向`getElementsByTagName()`传递 "*"。星号在 JavaScript 和层样式表（CSS）中通常被理解为“所有”。这是一个示例：

```javascript
var allElements = document.getElementsByTagName("*");
```

此行代码返回一个包含所有元素的`HTMLCollection`，按它们出现的顺序排列。因此第一个项目是`<html>`元素，第二个是`<head>`元素，依此类推。Internet Explorer 8 及之前的实现实际上将注释视为元素，因此调用`getElementsByTagName("*")`时浏览器将返回注释节点。Internet Explorer 9 不将注释视为元素，因此不返回它们。

![image](img/pen.gif)

尽管规范规定标签名是区分大小写的，但为了与最大的兼容性，`getElementsByTagName()`方法是不区分大小写的。在 XML 页面（包括 XHTML）中使用，`getElementsByTagName()`将切换到区分大小写的模式。

第三种方法仅定义在`HTMLDocument`类型上是`getElementsByName()`。顾其名，该方法返回所有具有给定`name`属性的元素。`getElementsByName()`方法通常用于单选按钮，所有这些按钮必须具有相同的`name`以确保将正确的值发送到服务器，如下示例所示：

```html
<fieldset>
    <legend>你喜欢哪种颜色?</legend>
    <ul>
        <li><input type="radio" value="red" name="color" id="colorRed">
            <label for="colorRed">红色</label></li>
        <li><input type="radio" value="green" name="color" id="colorGreen">
            <label for="colorGreen">绿色</label></li>
        <li><input type="radio" value="blue" name="color" id="colorBlue">
            <label for="colorBlue">蓝色</label></li>
    </ul>
</fieldset>
```

在这段代码中，单选框的`name`属性均为 "color"，尽管它们的`id`不同。`id`允许将`<label>`元素应用于单选框，而`name`属性则确保三个值中只有一个会被发送到服务器。然后可以使用以下代码获取所有这些单选框：

```javascript
var radios = document.getElementsByName("color");
```

与`getElementsByTagName()`一样，`getElementsByName()`方法返回一个`HTMLCollection`。然而，在此上下文中，`namedItem()`方法始终检索第一个项目（因为所有项目具有相同的名称）。

## 特殊集合

`document`对象具有几个特殊的集合。这些集合中的每一个都是`HTMLCollection`对象，并提供了更快速访问文档常用部分的方法，如下：

- `document.anchors` — 包含文档中所有带有`name`属性的`<a>`元素。
- `document.applets` — 包含文档中所有的`<applet>`元素。该集合已废弃，因为不再推荐使用`<applet>`元素。
- `document.forms` — 包含文档中所有的`<form>`元素。与`document.getElementsByTagName("form")`相同。
- `document.images` — 包含文档中所有的`<img>`元素。与`document.getElementsByTagName("img")`相同。
- `document.links` — 包含文档中所有带有`href`属性的`<a>`元素。

这些特殊集合在`HTMLDocument`对象上始终可用，并且像所有的`HTMLCollection`对象一样，不断更新以匹配当前文档的内容。

## DOM 符合性检测

由于 DOM 有多个层级和多个部分，因此有确定浏览器具体实现了 DOM 的哪些部分变得很有必要。`document.implementation`属性是一个对象，包含了直接与浏览器 DOM 实现相关的信息和功能。DOM Level 1 仅在`document.implementation`上规定了一个方法，即`hasFeature()`。`hasFeature()`方法接受两个参数：要检查的 DOM 特性的名称和版本。如果浏览器支持该命名的特性和版本，该方法将返回 true，如下例所示：

```javascript
var hasXmlDom = document.implementation.hasFeature("XML", "1.0");
```

可以测试的各种值列在下表中。

| 特性 | 支持的版本 | 说明 |
| --- | --- | --- |
| Core | 1.0, 2.0, 3.0 | 基础 DOM，规定了使用层级树表示文档 |
| XML | 1.0, 2.0, 3.0 | Core 的 XML 扩展，增加了对 CDATA 节、处理指令和实体的支持 |
| HTML | 1.0, 2.0 | XML 的 HTML 扩展，增加了对 HTML 特定元素和实体的支持 |
| Views | 2.0 | 根据某些样式对文档进行格式化 |
| StyleSheets | 2.0 | 将样式表与文档关联 |
| CSS | 2.0 | 支持层级样式表 Level 1 |
| CSS2 | 2.0 | 支持层级样式表 Level 2 |
| Events | 2.0, 3.0 | 通用 DOM 事件 |
| UIEvents | 2.0, 3.0 | 用户界面事件 |
| MouseEvents | 2.0, 3.0 | 由鼠标引起的事件（点击、鼠标悬停等） |
| MutationEvents | 2.0, 3.0 | DOM 树改变时触发的事件 |
| HTMLEvents | 2.0 | HTML 4.01 事件 |
| Range | 2.0 | 操作 DOM 树中范围的对象和方法 |
| Traversal | 2.0 | 遍历 DOM 树的方法 |
| LS | 3.0 | 文件与 DOM 树之间的同步加载和保存 |
| LS-Async | 3.0 | 文件与 DOM 树之间的异步加载和保存 |
| Validation | 3.0 | 修改 DOM 树并仍保持其有效的方法 |

虽然这是一个很方便的特性，但使用`hasFeature()`的缺点是实现者可以决定实现是否确实符合 DOM 规范的各个部分。非常容易让此方法对任何和所有值返回 true，但这并不意味着该实现符合它所声称的所有规范。例如，Safari 2.x 及更早版本对某些未完全实现的特性返回 true。在大多数情况下，在使用 DOM 的特定部分之前，除了`hasFeature()`之外，使用能力检测是一个好主意。

## 文档写入

`document`对象较旧的功能之一是向 Web 页面的输出流写入内容的能力。这种能力以四个方法的形式出现：`write()`、`writeln()`、`open()`和`close()`。`write()`和`writeln()`方法各接受一个字符串参数以写入输出流。`write()`仅仅是原样添加文本，而`writeln()`则在字符串末尾追加一个换行符（`\n`）。这两个方法可以在页面加载时动态地向页面添加内容，如下例：

![image](img/logo1.gif)

```html
<html>
<head>
    <title>document.write() 示例</title>
</head>
<body>
    <p>当前日期和时间是：
    <script type="text/javascript">
        document.write("<strong>" + new Date().toString() + "</strong>");
    </script>
</body>
</html>
```

## DocumentWriteExample1.htm

此示例在页面加载时输出当前日期和时间。日期被`<strong>`元素包裹。`write()`和`writeln()`方法通常用于动态包含 JavaScript 文件。在包含 JavaScript 文件时，必须确保不要包含`</script>`字符串，否则它会被解释为脚本块的结束，如下所示：

```html
<html>
<head>
    <title>document.write() 示例</title>
</head>
<body>
    <script type="text/javascript">
        document.write("<script type=\"text/javascript\" src=\"file.js\">");
    </script>
</body>
</html>
```

## DocumentWriteExample2.htm

尽管此文件看起来是正确的，但`</script>`字符串被解释为匹配外层的`<script>`标签，这意味着`");`将出现在页面上。为了避免这种情况，只需要更改字符串，如第 2 章所述所示：

```html
<html>
<head>
    <title>document.write() 示例</title>
</head>
<body>
    <script type="text/javascript">
        document.write("<script type=\"text/javascript\" src=\"file.js\">" + "</script>");
    </script>
</body>
</html>
```

## DocumentWriteExample3.htm

字符串`</script>`不再注册为外层`<script>`标签的结束标记，因此页面上没有额外的内容输出。之前的示例使用`document.write()`在页面渲染时直接向页面输出内容。如果`document.write()`在页面完全加载后调用，它将覆盖整个页面，如下例所示：

```html
<html>
<head>
    <title>document.write() 示例</title>
</head>
<body>
    <p>这是一些你无法看到的内容，因为它会被覆盖。</p>
    <script type="text/javascript">
        window.onload = function(){
            document.write("Hello world!");
        };
    </script>
</body>
</html>
```



## DocumentWriteExample4.htm

在此示例中，使用`window.onload`事件处理程序来推迟函数的执行，直到页面完全加载（事件在第 13 章中讨论）。当这发生时，“Hello world!” 字符串将覆盖整个页面内容。

`open()`和`close()`方法分别用于打开和关闭 Web 页输出流。在页面加载过程中使用`write()`或`writeln()`时，不需要使用任何一个方法。

严格的 XHTML 文档不支持文档写入。对于那些使用`application/xml+xhtml`内容类型提供的页面，这些方法将无法工作。

## 元素类型 (Element Type)

在`Document`类型之外，`Element`类型在 Web 编程中最常用。`Element`类型表示一个 XML 或 HTML 元素，提供了访问其标签名、子节点和属性等信息的能力。`Element`节点具有以下特征：

- `nodeType`为`1`。
- `nodeName`是元素的标签名。
- `nodeValue`为`null`。
- `parentNode`可能是一个`Document`或`Element`。
- 子节点可能是`Element`、`Text`、`Comment`、`ProcessingInstruction`、`CDATASection`或`EntityReference`。

元素的标签名可以通过`nodeName`属性或使用`tagName`属性来访问；这两个属性返回相同的值（后者通常用于提高代码可读性）。考虑以下元素：

```html
<div id="myDiv"></div>
```

可以通过以下方式获取此元素并访问其标签名：

```javascript
var div = document.getElementById("myDiv");
alert(div.tagName);    //"DIV"
alert(div.tagName == div.nodeName);   //true
```

该元素的标签名为`div`，ID 为 "myDiv"。但请注意，`div.tagName`实际上输出 "DIV" 而不是 "div"。当用于 HTML 时，标签名始终以全大写形式表示；当用于 XML（包括 XHTML）时，标签名始终与源代码的大小写匹配。如果你不确定脚本将运行在 HTML 还是 XML 文档上，最好在比较之前将标签名转换为统一的大小写，如下例所示：

```javascript
if (element.tagName == "div"){  // 避免！易出错！
    // 在处执行某些操作
}

if (element.tagName.toLowerCase() == "div"){ // 推荐 - 适用于所有文档
    // 在处执行某些操作
}
```

此示例展示了对`tagName`属性的两种比较方式。第一种非常容易出错，因为它在 HTML 文档中无法工作。第二种方法（将标签名转换为全小写）是优的，因为它同时适用于 HTML 和 XML 文档。

![image](img/pen.gif)

`Element`类型构造函数和原型在所有现代浏览器中都可以通过脚本访问，包括 8 版本的 Internet Explorer。较旧的浏览器（如 2 版本之前的 Safari 和 8 版本之前的 Opera）不暴露`Element`类型构造函数。

## HTML 元素 (HTML Elements)

所有的 HTML 元素都通过`HTMLElement`类型表示，直接表示或通过子类型表示。`HTMLElement`直接继承自`Element`并添加了几个属性。每个属性代表每个 HTML 元素上可用的以下标准属性之一：

- `id` — 文档中元素的唯一标识符。
- `title` — 关于元素的额外信息，通常以工具提示的形式表示。
- `lang` — 元素内容的语言代码（很少使用）。
- `dir` — 语言方向，"ltr"（从左到右）或 "rtl"（从右到左）；也很少使用。
- `className` — `class`属性的等价，用于指定元素上的 CSS 类。该属性不能命名为`class`，因为`class`是 ECMAScript 的保留字（关于保留字的信息请参见第 1 章）。

这些属性中的每一个都可以用于获取相应的属性值，也可以更改该值。考虑以下 HTML 元素：

![image](img/logo1.gif)

```html
<div id="myDiv" class="bd" title="Body text" lang="en" dir="ltr"></div>
```

HTMLElementsExample01.htm

此元素指定的所有信息都可以通过以下 JavaScript 代码获取：

```javascript
var div = document.getElementById("myDiv");
alert(div.id);         //"myDiv"
alert(div.className);  //"bd"
alert(div.title);      //"Body text"
alert(div.lang);       //"en"
alert(div.dir);        //"ltr"
```

还可以使用以下代码通过给属性分配新值来更改每个属性：

```javascript
div.id = "someOtherId";
div.className = "ft";
div.title = "Some other text";
div.lang = "fr";
div.dir ="rtl";
```

HTMLElementsExample01.htm

并不是所有属性在覆盖时都会对页面产生影响。对`id`或`lang`的更改对用户来说是透明的（假设没有基于这些值的 CSS 样式），而对`title`的更改只有在鼠标移动到元素上时可见。对`dir`的更改会在属性写入后立即导致页面上的文本左对或右对。如果该类与之前的具有不同的 CSS 样式信息，对`className`的更改可能会立即生效。

如前所述，所有的 HTML 元素都由`HTMLElement`的实例或更具体的子类型表示。下表列出了每个 HTML 元素及其关联类型（斜体元素为已弃用）。请注意，这些类型可以通过 JavaScript 在 Opera、Safari、Chrome 和 Firefox 中访问，但在 8 版本之前的 Internet Explorer 中无法访问。

![image](img/f328-01.jpg) ![image](img/f329-01.jpg) ![image](img/f330-01.jpg)

## 获取属性 (Getting Attributes)

每个元素可能具有零或多个属性，通常用于提供有关特定元素的额外信息。处理属性的三个 DOM 方法是`getAttribute()`、`setAttribute()`和`removeAttribute()`。这些方法适用于任何属性，包括定义在`HTMLElement`上的属性。这里是一个示例：

```javascript
var div = document.getElementById("myDiv");
alert(div.getAttribute("id"));         //"myDiv"
alert(div.getAttribute("class"));      //"bd"
alert(div.getAttribute("title"));      //"Body text"
alert(div.getAttribute("lang"));       //"en"
alert(div.getAttribute("dir"));        //"ltr"
```

注意，传入`getAttribute()`的属性名与实际属性名完全相同（而作为对象属性访问时使用的是`className`）。如果不存在给定的属性，`getAttribute()`始终返回`null`。

`getAttribute()`方法还可以检索不属于正式 HTML 语言的自定义属性值。考虑以下元素：

```html
<div id="myDiv" my_special_attribute="hello!"></div>
```

在此元素中，名为`my_special_attribute`的自定义属性定义值为 "hello!"。像任何其他属性一样使用`getAttribute()`获取此值，如下：

```javascript
var value = div.getAttribute("my_special_attribute");
```

注意属性名不区分大小写，因此 "ID" 和 "id" 是同一个属性。此外注意，根据 HTML5，自定义属性应该以`data-`开头以便验证。

元素上的所有属性也可以作为 DOM 元素本身的属性访问。当然，`HTMLElement`上定义了五个属性直接映射到相应的属性，但所有识别（非自定义）属性都会作为属性添加到对象中。考虑以下元素：

```html
<div id="myDiv" align="left" my_special_attribute="hello"></div>
```

由于`id`和`align`是 HTML 中`<div>`元素的识别属性，它们将作为元素对象的属性表示。`my_special_attribute`属性是自定义的，因此在 Safari、Opera、Chrome 或 Firefox 中不会显示为元素的属性。 8 版本的 Internet Explorer 也会为自定义属性创建属性，此示例所示：

![image](img/logo1.gif)

```javascript
alert(div.id);                    //"myDiv"
alert(div.my_special_attribute);  //undefined（IE 除外）
alert(div.align);                 //"left"
```

ElementAttributesExample02.htm

有两种属性，其属性名称与`getAttribute()`返回的相同并不直接对应。第一种属性是`style`，它使用 CSS 来指定元素的样式信息。当通过`getAttribute()`访问时，`style`属性包含 CSS 文本，而通过返回对象的属性访问时，它返回的是一个对象。`style`属性用于程序化访问元素的样式（在第 12 节中讨论），因此它不直接映射到`style`属性。

第二类行为表现不同的属性是事件处理程序属性，例如`onclick`。当在元素上使用时，`onclick`属性包含 JavaScript 代码，使用`getAttribute()`时会返回该代码字符串。然而，当访问`onclick`属性时，它返回一个 JavaScript 函数（如果未指定该属性，则返回`null`）。这是因为`onclick`和其他事件处理属性的设计初衷是允许向它们分配函数。

由于这些差异，开发者在用 JavaScript 编写 DOM 时倾向于放弃`getAttribute()`，转而完全使用对象属性。`getAttribute()`方法主要用于获取自定义属性的值。

![image](img/pen.gif)

在 Internet Explorer 7 及之前的版本中，针对`style`属性和`onclick`等事件处理属性的`getAttribute()`方法始终返回与通过属性访问时相同的值。因此，`getAttribute("style")`返回一个对象，而`getAttribute("onclick")`返回一个函数。尽管这在 Internet Explorer 8 中得到了修复，但这种不一致性是避免对 HTML 属性使用`getAttribute()`的另一个原因。

## 设置属性

`getAttribute()`的兄弟方法是`setAttribute()`，它接受两个参数：要设置的属性名称和设置的值。如果属性已存在，`setAttribute()`将其值替换为指定的值；如果属性不存在，`setAttribute()`将创建它并设置其值。以下是一个示例：

![image](img/logo1.gif)

```javascript
div.setAttribute("id", "someOtherId");
div.setAttribute("class", "ft");
div.setAttribute("title", "Some other text");
div.setAttribute("lang","fr");
div.setAttribute("dir", "rtl");
```

ElementAttributesExample01.htm

`setAttribute()`方法对 HTML 属性和自定义属性的作用相同。使用此方法设置属性时，属性名称会被归一化为小写，因此 "ID" 最终会变成 "id"。

由于所有属性都是属性，直接赋值给属性可以设置属性值，如下所示：

```javascript
div.id = "someOtherId";
div.align = "left";
```

请注意，如下示例所示，向 DOM 元素添加自定义属性并不会使其成为该元素的属性：

```javascript
div.mycolor = "red";
alert(div.getAttribute("mycolor"));   //null（在 Internet Explorer 中除外）
```

此示例添加了一个名为`mycolor`的自定义属性并将其设置为 "red"。在大多数浏览器中，该属性不会自动变成元素上的属性，因此调用`getAttribute()`获取同名属性会返回`null`。然而，在 Internet Explorer 中，自定义属性被视为元素的属性，反之亦然。

![image](img/pen.gif)

Internet Explorer 7 及之前的版本在`setAttribute()`方面存在异常行为。尝试设置`class`或`style`属性没有效果，这与使用`setAttribute()`设置事件处理属性类似。尽管这些问题在 Internet Explorer 8 中已解决，但最好的做法始终使用属性设置这些属性。

最后一个方法是`removeAttribute()`，它会从元素中完全移除属性。这不仅仅是清除属性的值；它会从元素中完全删除该属性，如下所示：

```javascript
div.removeAttribute("class");
```

此方法并不频繁使用，但在序列化 DOM 元素时精确指定要包含哪些属性可能非常有用。

![image](img/pen.gif)

Internet Explorer 6 及之前的版本不支持`removeAttribute()`。

## attributes 属性

`Element`类型是唯一使用`attributes`属性的 DOM 节点类型。`attributes`属性包含一个`NamedNodeMap`，这是一个类似于`NodeList`的“动态集合”。元素上的每个属性都由一个`Attr`节点表示，每个节点都存储在`NamedNodeMap`对象中。`NamedNodeMap`对象具有以下方法：

- `getNamedItem(name)` — 返回`nodeName`属性等于`name`的节点。
- `removeNamedItem(name)` — 从列表中移除`nodeName`属性等于`name`的节点。
- `setNamedItem(node)` — 将节点添加到列表中，通过其`nodeName`属性对其进行索引。
- `item(pos)` — 返回数字位置`pos`的节点。

`attributes`属性中的每个节点都是一个`nodeName`为属性名且`nodeValue`为属性值的节点。要获取元素的`id`属性，您可以使用以下代码：

```javascript
var id = element.attributes.getNamedItem("id").nodeValue;
```

以下是使用中括号符号通过名称访问属性的简写符号：

```javascript
var id = element.attributes["id"].nodeValue;
```

也可以用这种表示法来设置属性值，如示例所示，获取属性节点然后将`nodeValue`设置为新值：

```javascript
element.attributes["id"].nodeValue = "someOtherId";
```

`removeNamedItem()`方法的功能与元素上的`getAttribute()`方法相同——它简单地移除了指定的属性。以下示例显示`removeNamedItem()`返回了代表该属性的`Attr`节点：

```javascript
var oldAttr = element.attributes.removeNamedItem("id");
```

`setNamedItem()`是一个很少使用的方法，通过传入属性节点向元素添加新属性，如下所示：

```javascript
element.attributes.setNamedItem(newAttr);
```

通常情况下，由于其简单性，`getAttribute()`、`removeAttribute()`和`setAttribute()`方法优于使用上述属性方法。

`attributes`属性的一个用途是遍历属性。这通常发生在将 DOM 结构序列化为 XML 或 字符串时。以下代码遍历元素上的每个属性并构造`name="value" name="value"`格式的字符串：

![image](img/logo1.gif)

```javascript
function outputAttributes(element){
```



```javascript
var pairs = new Array(),

    attrName,

    attrValue,

    i,

    len;

for (i = 0, len = element.attributes.length; i < len; i++) {

    attrName = element.attributes[i].nodeName;

    attrValue = element.attributes[i].nodeValue;

    pairs.push(attrName + "=\"" + attrValue + "\"");

}

return pairs.join(" ");

}
```

`ElementAttributesExample03.htm`

此函数使用数组存储键值对直到最后，用空格将它们连接。（这种技术在序列化为长字符串时经常使用。）使用`attributes.length`属性，for 循环遍历每个属性，并将名称和值输出到字符串。关于此代码的工作方式，有几点需要注意：

- 浏览器在返回`attributes`对象中的属性顺序上不同。属性在 HTML 或 XML 代码中的出现顺序并不与其在`attributes`对象中的出现顺序一致。
- Internet Explorer 7 及之前的版本会返回 HTML 元素的所有可能属性，即使它们未被指定。这意味着通常会返回超过 100 个属性。

之前的函数可以进行扩展，以确保只包含指定的属性，从而解决 Internet Explorer 7 及更早版本的问题。每个属性节点都有一个名为`specified`的属性，当属性作为 HTML 属性或通过`setAttribute()`方法指定时，该属性被设置为`true`。对于 Internet Explorer，这些额外属性的该值值为`false`，而在其他浏览器中不存在这些额外属性（因此，对于任何属性节点，`specified`始终为`true`）。代码可以如下所示扩展：

![image](img/logo1.gif)

```javascript
function outputAttributes(element) {

    var pairs = new Array(),

        attrName,

        attrValue,

        i,

        len;

    for (i = 0, len = element.attributes.length; i < len; i++) {

        attrName = element.attributes[i].nodeName;

        attrValue = element.attributes[i].nodeValue;

        if (element.attributes[i].specified) {

            pairs.push(attrName + "=\"" + attrValue + "\"");

        }

    }

    return pairs.join(" ");

}
```

`ElementAttributesExample04.htm`

此修订后的函数确保了对于 Internet Explorer 7 及更早版本只返回指定的属性。

## 创建元素

可以使用`document.createElement()`方法创建新元素。该方法接受一个参数，即要创建的元素的标签名。在 HTML 文档中，标签名是不区分大小写的，而在 XML 文档（包括 XHTML）中是区分大小写的。要创建一个`<div>`元素，可以使用以下代码：

```javascript
var div = document.createElement("div");
```

使用`createElement()`方法创建一个新元素并设置其`ownerDocument`属性。此时，你可以操作元素的属性、为它添加更多子元素等。请考虑以下示例：

```javascript
div.id = "myNewDiv";

div.className = "box";
```

在新元素上设置这些属性仅分配信息。由于该元素不是文档树的一部分，因此它不会影响浏览器的显示。可以使用`appendChild()`、`insertBefore()`或`replaceChild()`将元素添加到文档树中。以下代码将新创建的元素添加到文档的`<body>`元素中：

```javascript
document.body.appendChild(div);
```

`CreateElementExample01.htm`

一旦元素被添加到文档树中，浏览器会立即渲染。此后对元素进行的任何更改都会被浏览器反映。

Internet Explorer 允许`createElement()`的另一种用法，允许你像此示例所示指定一个完整的元素（包括属性）：

```javascript
var div = document.createElement("<div id=\"myNewDiv\" class=\"box\"></div>");
```

这种用法有助于规避在 Internet Explorer 7 及更早版本中关于动态创建元素的一些问题。已知问题如下：

- 动态创建的`<iframe>`元素无法设置其`name`属性。
- 动态创建的`<input>`元素不会通过表单的`reset()`方法重置（在 14 章中讨论）。
- 动态创建的`type`属性为`"reset"`的`<button>`元素不会重置表单。
- 具有相同`name`的动态创建的单选按钮之间没有关系。具有相同`name`的单选按钮应该是同一选项的不同值，但动态创建的单选按钮会丢失这种关系。

这些问题中的每一个都可以通过在`createElement()`中指定标签的完整 HTML 来解决，如下所示：

```javascript
if (client.browser.ie && client.browser.ie <= 7) {

    // 创建带有名称的 iframe

    var iframe = document.createElement("<iframe name=\"myframe\"></iframe>");

    // 创建 input 元素

    var input = document.createElement("<input type=\"checkbox\">");

    // 创建按钮

    var button = document.createElement("<button type=\"reset\"></button>");

    // 创建单选按钮

    var radio1 = document.createElement("<input type=\"radio\" name=\"choice\"" +
        " value=\"1\">");

    var radio2 = document.createElement("<input type=\"radio\" name=\"choice\"" +
        " value=\"2\">");

}
```

与使用`createElement()`的传统方式一样，这样使用它会返回一个 DOM 元素引用，可以将其添加到文档并进行其他扩展。只有在处理 Internet Explorer 7 及更早版本中的这些特定问题之一时才推荐这种用法，因为需要检测浏览器。注意，没有其他浏览器支持这种用法。

## 元素节点

元素可以有任意数量的子元素和后代，因为元素可以是元素的子元素。`childNodes`属性包含元素的所有直接儿子，这些可能是其他元素、文本节点、注释或处理指令。不同浏览器在识别这些节点方面存在显著差异。例如，考虑以下代码：

```html
<ul id="myList">

    <li>Item 1</li>

    <li>Item 2</li>

    <li>Item 3</li>

</ul>
```

当此代码在 Internet Explorer 8 及更早版本中解析时，`<ul>`元素有三个子节点，每个`<li>`元素对应一个节点。在所有其他浏览器中，`<ul>`元素有七个元素：三个`<li>`元素和四个表示`<li>`元素之间空白符的文本节点。如果删除了元素之间的空白符（如下示例所示），所有浏览器都会返回相同数量的子节点：

```html
<ul id="myList"><li>Item 1</li><li>Item 2</li><li>Item 3</li></ul>
```

使用此代码，所有浏览器都为`<ul>`元素返回三个子节点。在使用`childNodes`导航节点时，请记住这些浏览器之间的差异。通常在执行操作之前需要检查`nodeType`，如下示例所示：

```javascript
for (var i = 0, len = element.childNodes.length; i < len; i++) {

    if (element.childNodes[i].nodeType == 1) {

        // 执行操作

    }

}
```

此代码遍历元素的每个子节点，仅当`nodeType`为 1 时执行操作。

为了获取特定标签的子节点和其他后代，元素也支持`getElementsByTagName()`方法。在元素上使用该方法与文档版本完全相同，只是搜索是以元素为根，因此只返回该元素的后代。在本节早前的`<ul>`代码中，可以使用以下代码获取`<li>`元素：

```javascript
var ul = document.getElementById("myList");

var items = ul.getElementsByTagName("li");
```

请记住，这样做是因为`<ul>`元素只有一层后代。如果有更多层次，将返回所有层级的`<li>`元素。

## 文本类型

文本节点由 Text 类型表示并包含纯文本，这些文本被字面解释，可以包含转义 HTML 字符但不包含 HTML 代码。文本节点具有以下特征：

- `nodeType`为 3。
- `nodeName`为`"#text"`。
- `nodeValue`为节点包含的文本。
- `parentNode`为元素。
- 不支持子节点。

文本节点包含的文本可以通过`nodeValue`属性或`data`属性访问，两者都包含相同的值。对`nodeValue`或`data`的更改也会反映在另一个属性中。以下方法允许对节点中的文本进行操作：

- `appendData(text)`——在节点末尾追加文本。
- `deleteData(offset, count)`——从偏移量开始删除`count`个字符。
- `insertData(offset, text)`——在偏移量处插入文本。
- `replaceData(offset, count, text)`——将从`offset`到`offset + count`的文本替换为`text`。
- `splitText(offset)`——在偏移量处将文本节点拆分为两个分离的文本节点。
- `substringData(offset, count)`——从文本中提取从位置`offset`开始到`offset + count`结束的字符串。

除了这些方法外，`length`属性返回节点中的字符数。此值与使用`nodeValue.length`或`data.length`相同。

默认情况下，每个可能包含内容的元素在存在内容时，最多只有一个文本节点。这里有一个示例：

```html
<!-- 没有内容，所以没有文本节点 -->

<div></div>

<!-- 包含空白字符内容，所以有一个文本节点 -->

<div> </div>

<!-- 有内容，所以有一个文本节点 -->

<div>Hello World!</div>
```

这段代码中的第一个`<div>`元素没有内容，因此没有文本节点。起始标签和结束标签之间的任何内容都意味着必须创建一个文本节点，因此第二个`<div>`元素即使内容是空白字符，也只有一个文本节点作为子节点。该文本节点的`nodeValue`是单个空格。第三个`<div>`也有一个文本节点，其`nodeValue`为`"Hello World!"`。以下代码允许你访问此节点：

```javascript
var textNode = div.firstChild; // or div.childNodes[0]
```

一旦获取了文本节点的引用，就可以像这样进行更改：

![image](img/logo1.gif)

```javascript
div.firstChild.nodeValue = "Some other message";
```

`TextNodeExample01.htm`

只要节点当前在文档树中，对文本节点的更改就会立即反映。关于更改文本节点值的另一个注意事项是，该字符串经过了 HTML 或 XML 编码（取决于文档类型），这意味着任何小于号、大于号或引号都会被转义，如示例所示：

![image](img/logo1.gif)

```javascript
// 输出为 "Some &lt;strong&gt;other&lt;/strong&gt; message"

div.firstChild.nodeValue = "Some strong>other</strong> message";
```

`TextNodeExample02.htm`

这是在字符串插入 DOM 文档之前对其实进行 HTML 编码的有效方法。

![image](img/pen.gif)

在 Internet Explorer 8、Firefox、Safari、Chrome 和 Opera 中，可以在脚本中访问`Text`类型构造函数和原型。

### 创建文本节点

可以使用`document.createTextNode()`方法创建新的文本节点，该方法接受一个参数——即要插入节点中的文本。与设置现有文本节点的值一样，文本将经过 HTML 或 XML 编码，如示例所示：

```javascript
var textNode = document.createTextNode("<strong>Hello</strong> world!");
```

当创建新的文本节点时，其`ownerDocument`属性会被设置，但在其被添加到文档树中的节点之前，它不会显示在浏览器窗口中。以下代码创建了一个新的`<div>`元素并为其添加了一条消息：

```javascript
var element = document.createElement("div");

element.className = "message";

var textNode = document.createTextNode("Hello world!");

element.appendChild(textNode);

document.body.appendChild(element);
```

`TextNodeExample03.htm`

此示例创建了一个新的`<div>`元素并为其分配了类`"message"`。然后创建了一个文本节点并添加到该元素中。最后一步是将元素添加到文档的体（body）中，这使得元素和文本节点都显示在浏览器中。

通常，元素只有一个文本节点作为子节点。然而，可能会有多个文本节点作为子节点，如下示例所示：

![image](img/logo1.gif)

```javascript
var element = document.createElement("div");

element.className = "message";

var textNode = document.createTextNode("Hello world!");

element.appendChild(textNode);

var anotherTextNode = document.createTextNode("Yippee!");

element.appendChild(anotherTextNode);

document.body.appendChild(element);
```

`TextNodeExample04.htm`

当文本节点作为另一个文本节点的兄弟节点被添加时，这些节点中的文本将显示，它们之间没有任何空格。

### 规范化文本节点

在 DOM 文档中，兄弟文本节点可能会令人困惑，因为没有简单的文本字符串无法用单个文本节点表示。尽管如此，在 DOM 文档中遇到兄弟文本节点并不常见，因此有一种方法可以将兄弟文本节点合并在一起。该方法称为`normalize()`，它存在于`Node`类型（因此所有节点类型都可用）。当在两个或多个文本节点的父节点上调用`normalize()`时，这些节点将合并为一个文本节点，其`nodeValue`等于每个文本节点的`nodeValue`属性的拼接。这是一个示例：

```javascript
var element = document.createElement("div");

element.className = "message";

var textNode = document.createTextNode("Hello world!");

element.appendChild(textNode);

var anotherTextNode = document.createTextNode("Yippee!");

element.appendChild(anotherTextNode);
```



`document.body.appendChild(element);`

`alert(element.childNodes.length);` //2

`element.normalize();`

`alert(element.childNodes.length);` //1

`alert(element.firstChild.nodeValue);` //"Hello world!Yippee!"

```
TextNodeExample05.htm
```

当浏览器解析文档时，永远不会创建兄弟文本节点。兄弟文本节点只会通过程序化的 DOM 操作出现。

![image](img/pen.gif)

`normalize()` 方法在某些情况下会导致 IE 6 崩溃，尽管在 IE 7 或更高版本中已修复。

### 拆分文本节点

`Text` 类型有一个与 `normalize()` 相反的方法：`splitText()` 方法将文本节点拆分为两个文本节点，根据指定的偏移量。原始文本节点包含偏移量之前的文本，新文本节点包含剩余文本。该方法返回新节点，它与原始节点具有相同的 `parentNode`。考虑以下示例：

![image](img/logo1.gif)

```javascript
var element = document.createElement("div");
element.className = "message";
var textNode = document.createTextNode("Hello world!");
element.appendChild(textNode);
document.body.appendChild(element);
var newNode = element.firstChild.splitText(5);
alert(element.firstChild.nodeValue);  //"Hello"
alert(newNode.nodeValue);             //" world!"
alert(element.childNodes.length);     //2
```

`TextNodeExample06.htm`

在此示例中，包含 `"Hello world!"` 的文本节点在位置 `5` 处拆分为两个文本节点。位置 5 包含了 `"Hello"` 和 `"world!"` 之间的空格，因此原始文本节点为 `"Hello"`，新节点为 `" world!"`（包括空格）。拆分文本节点通常用于从文本节点提取数据的 DOM 解析技术。

### 注释类型

注释由 `Comment` 类型表示。`Comment` 节点具有以下特征：

* `nodeType` 为 `8`。
* `nodeName` 为 `"#comment"`。
* `nodeValue` 为注释的内容。
* `parentNode` 为 `Document` 或 `Element`。
* 不支持子节点。

`Comment` 类型继承自与 `Text` 类型相同的基类，因此具有所有除 `splitText()` 以外的字符串处理方法。同样类似于 `Text` 类型，可以使用 `nodeValue` 或 `data` 属性获取注释的实际内容。注释节点可以从父节点作为子节点访问。考虑以下 HTML 代码：

![image](img/logo1.gif)

```html
<div id="myDiv"><!-- A comment --></div>
```

在这种情况下，注释是 `<div>` 元素的子节点，这意味着可以这样访问它：

```javascript
var div = document.getElementById("myDiv");
var comment = div.firstChild;
alert(comment.data);    //"A comment"
```

`CommentNodeExample01.htm`

注释也可以使用 `document.createComment()` 方法并传入注释文本来创建，如下代码所示：

```javascript
var comment = document.createComment("A comment");
```

不出意外的是，注释节点（comment nodes）很少被访问或创建，因为它们在算法上几乎没有用途。此外，浏览器不识别结束标签 `</html>` 之后的注释。如果你需要访问注释节点，请确保它们作为 `<html>` 元素的后代出现。

![image](img/pen.gif)

`Comment` 类型构造函数和原型在 Firefox、Safari、Chrome 和 Opera 中均可直接访问。Internet Explorer 8 的注释节点被认为是一个标签名为 `"!"` 的元素。这意味着可以通过 `getElementsByTagName()` 获取注释节点。Internet Explorer 9 通过一个名为 `HTMLCommentElement` 的自定义构造函数来表示注释，尽管它并没有将注释视为元素。

# CDATASection 类型

CDATA 节是 XML 文档特有的，通过 `CDATASection` 类型表示。与 `Comment` 类似，`CDATASection` 类型继承自基类 `Text` 类型，因此它拥有除 `splitText()` 之外的所有同属性的字符串处理方法。一个 `CDATASection` 节点具有以下特征：

* `nodeType` 为 `4`。
* `nodeName` 为 `"#cdata-section"`。
* `nodeValue` 为 CDATA 节的内容。
* `parentNode` 是一个 `Document` 或 `Element`。
* 不支持子节点。

CDATA 节仅在 XML 文档中有效，因此大多数浏览器会错误地将 CDATA 节解析为 `Comment` 或 `Element`。考虑以下情况：

```html
<div id="myDiv"><![CDATA[This is some content.]]></div>
```

在这个示例中，一个 `CDATASection` 节点应该作为 `<div>` 的第一个子节点存在；然而，四大浏览器中没有一个将其解释为这种形式。即使在有效的 XHTML 页面中，浏览器也无法正确支持嵌入的 CDATA 节。

真正的 XML 文档允许使用 `document.createCDataSection()` 创建 CDATA 节并传入节点的内容。

![image](img/pen.gif)

`CDATASection` 类型构造函数和原型在 Firefox、Safari、Chrome 和 Opera 中均可访问。Internet Explorer 直到第 9 版仍然不支持这种类型。

# DocumentType 类型

`DocumentType` 类型在浏览器中并不常用，且仅在 Firefox、Safari 和 Opera 中支持。`DocumentType` 对象包含所有关于文档 `doctype` 的信息，并具有以下特征：

* `nodeType` 为 `10`。
* `nodeName` 为 doctype 的名称。
* `nodeValue` 为 `null`。
* `parentNode` 是一个 `Document`。
* 不支持子节点。

`DocumentType` 对象无法在 DOM Level 1 中动态创建；它们仅在解析文档代码时创建。对于支持该类型的浏览器，`DocumentType` 对象存储在 `document.doctype` 中。DOM Level 1 描述了 `DocumentType` 对象的三个属性：`name`，即 doctype 的名称；`entities`，由 doctype 描述的实体的 `NamedNodeMap`；以及 `notations`，由 doctype 描述的符号的 `NamedNodeMap`。由于浏览器中的文档通常使用 HTML 或 XHTML doctype，因此 `entities` 和 `notations` 列表通常是空的（它们只在内联 doctype 中被填充）。从任何意义上，`name` 属性都是唯一可用的属性。该属性填充了 doctype 的名称，即紧跟在 `<!DOCTYPE` 之后的文本。考虑以下 HTML 4.01 严格 doctype：

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" 
  "http://www.w3.org/TR/html4/strict.dtd">
```

对于此 doctype，`name` 属性为 `"HTML"`：

```javascript
alert(document.doctype.name); //"HTML"
```

Internet Explorer 8 及之前的版本不支持 `DocumentType` 类型，因此 `document.doctype` 始终为 `null`。此外，这些浏览器会将 doctype 误解为注释并实际上为它创建一个注释节点。Internet Explorer 9 正确地为 `document.doctype` 分配了一个对象，但仍然暴露 `DocumentType` 类型。

# DocumentFragment 类型

在所有节点类型中，`DocumentFragment` 类型是唯一一个在标记中没有表示的。DOM 将文档碎片定义为一个“轻量级”文档，能够包含并操作节点，而无需完整文档的所有额外开销。`DocumentFragment` 节点具有以下特征：

* `nodeType` 为 `11`。
* `nodeName` 为 `"#document-fragment"`。
* `nodeValue` 为 `null`。
* `parentNode` 为 `null`。
* 子节点可以是 `Element`、`ProcessingInstruction`、`Comment`、`Text`、`CDATASection` 或 `EntityReference`。

文档碎片不能直接添加到文档中。相反，它充当可能需要添加到文档中的其他节点的仓库。文档碎片使用 `document.createDocumentFragment()` 方法创建，如下所示：

```javascript
var fragment = document.createDocumentFragment();
```

文档碎片继承自 `Node` 的所有方法，通常用于执行将应用到文档的 DOM 操作。如果将文档中的某个节点添加到文档碎片中，该节点将从文档树中移除且不会被浏览器渲染。添加到文档碎片的新节点也不属于文档树的一部分。文档碎片的内容可以通过 `appendChild()` 或 `insertBefore()` 添加到文档中。考虑以下 HTML：

```html
<ul id="myList"></ul>
```

假设你想向这个 `<ul>` 元素添加列表项。直接将每个项目添加到元素会导致浏览器重新渲染页面。为了避免这种情况，下面的代码示例使用文档碎片一次性创建列表项：

![image](img/logo.gif)

```javascript
var fragment = document.createDocumentFragment();
var ul = document.getElementById("myList");
var li = null;
for (var i=0; i < 3; i++){
    li = document.createElement("li");
    li.appendChild(document.createTextNode("Item " + (i+1)));
    fragment.appendChild(li);
}
ul.appendChild(fragment);
```

`DocumentFragmentExample01.htm`

此示例首先创建一个文档碎片并获取 `<ul>` 元素的引用。for 循环创建三个列表项，每个项都有说明其内容的文本。这样做是创建一个 `<li>` 元素，然后创建一个文本节点并添加到元素。然后将 `<li>` 元素添加到文档碎片。当循环完成后，通过 `appendChild()` 并传入碎片将所有项目添加到 `<ul>` 元素。

# Attr 类型

属性在 DOM 中由 `Attr` 类型表示。`Attr` 类型构造函数和原型在包括 IE 8 在内的所有浏览器中均可访问。从技术上讲，属性是元素 `attributes` 属性节点。属性节点具有以下特征：

* `nodeType` 为 `11`。
* `nodeName` 为属性名称。
* `nodeValue` 为属性值。
* `parentNode` 为 `null`。
* HTML 中不支持子节点。
* 在 XML 中子节点可以是 `Text` 或 `EntityReference`。

尽管属性是节点，但并不被认为是 DOM 文档树的一部分。属性节点很少被直接引用，大多数开发者倾向于使用 `getAttribute()`、`setAttribute()` 和 `removeAttribute()`。

`Attr` 对象上有三个属性：`name`，即属性名称（同 `nodeName`）；`value`，即属性值（同 `nodeValue`）；以及 `specified`，这是一个布尔值，用于指示属性是通过代码指定的还是默认值。

可以使用 `document.createAttribute()` 并传入属性名称来创建新的属性节点。例如，要为元素添加 `align` 属性，可以使用以下代码：

![image](img/logo1.gif)

```javascript
var attr = document.createAttribute("align");
attr.value = "left";
element.setAttributeNode(attr);
alert(element.attributes["align"].value);       //"left"
alert(element.getAttributeNode("align").value); //"left"
alert(element.getAttribute("align"));           //"left"
```

`AttrExample01.htm`

在此示例中，创建了一个新的属性节点。`name` 属性是通过调用 `createAttribute()` 赋值的，因此随后不需要直接对其进行赋值。随后，将 `value` 属性赋值为 `"left"`。要将新创建的属性添加到元素中，可以使用元素的 `setAttributeNode()` 方法。一旦添加了属性，可以通过多种方式访问它：通过 `attributes` 属性、使用 `getAttributeNode()` 或使用 `getAttribute()`。`attributes` 和 `getAttributeNode()` 都会返回该属性的实际 `Attr` 节点，而 `getAttribute()` 只返回属性值。

![image](img/pen.gif)

实际上没有充分理由直接访问属性节点。与操作属性节点相比，`getAttribute()`、`setAttribute()` 和 `removeAttribute()` 方法更优。

## 操作 DOM

在许多情况下，操作 DOM 是相当直接的，这使得使用 JavaScript 重新创建通常使用 HTML 代码创建的内容变得容易。然而，有时使用 DOM 并不看起来那么简单。浏览器充满了隐藏的陷阱和不兼容性，这使得编写 DOM 的某些部分比编写其他部分更复杂。

## 动态脚本

`<script>` 元素用于将 JavaScript 代码插入页面，可以使用 `src` 属性包含外部文件，也可以在元素内部包含文本。动态脚本是指那些在页面加载时不存在，但随后通过 DOM 包含的脚本。与 HTML 元素一样，这样做有两种方法：引入外部文件或直接插入文本。

动态加载外部 JavaScript 文件的工作方式如你所预期。考虑以下 `<script>` 元素：

```html
<script type="text/javascript" src="client.js"></script>
```

该 `<script>` 元素包含了第 9 章客户端检测脚本的文本。创建此节点的 DOM 代码如下：

```javascript
var script = document.createElement("script");
script.type = "text/javascript";
script.src = "client.js";
document.body.appendChild(script);
```

如你所示，DOM 代码完全镜像了它所代表的 HTML 代码。注意，在最后一行将 `<script>` 元素添加到页面之前，外部文件不会被下载。该元素也可以添加到 `<head>` 元素中，尽管效果相同。这一过程可以总结为以下函数：

```javascript
function loadScript(url){
    var script = document.createElement("script");
    script.type = "text/javascript";
    script.src = url;
    document.body.appendChild(script);
}
```

现在可以通过以下调用来加载外部 JavaScript 文件：

```javascript
loadScript("client.js");
```

从逻辑上讲，以下 DOM 代码应该可以工作：

![image](img/logo1.gif)

```javascript
var style = document.createElement("style");
style.type = "text/css";
```



`style.appendChild(document.createTextNode("body{background-color:red}"));`

`var head = document.getElementsByTagName("head")[0];`

`head.appendChild(style);`

`DynamicStyleExample01.htm`

这段代码在 Firefox、Safari、Chrome我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。和 Opera 中可以工作，但在 Internet Explorer 中不行。Internet Explorer 将 `<style>` 节点视为特殊节点，类似于 `<script>` 节点，因此不允许访问其子节点。实际上，Internet Explorer 抛出的错误与尝试向 `<script>` 元素添加子节点时的错误相同。Internet Explorer 的解决方法是访问元素的 `styleSheet` 属性，该属性又有一个名为 `cssText` 的属性，可以设置为 CSS 代码（这两个属性将在第 12 章中进一步讨论），如下代码示例所示：

```javascript
var style = document.createElement("style");
style.type = "text/css";
try{
    style.appendChild(document.createTextNode("body{background-color:red}"));
} catch (ex){
    style.styleSheet.cssText = "body{background-color:red}";
}
var head = document.getElementsByTagName("head")[0];
head.appendChild(style);
```

与动态添加内联脚本的代码类似，这段新代码使用 `try-catch` 语句来捕获 Internet Explorer 抛出的错误，然后通过使用 Internet Explorer 特有的设置样式进行响应。通用的解决方案如下：

![image](img/logo1.gif)

```javascript
function loadStyleString(css){
    var style = document.createElement("style");
    style.type = "text/css";
    try{
        style.appendChild(document.createTextNode(css));
    } catch (ex){
        style.styleSheet.cssText = css;
    }
    var head = document.getElementsByTagName("head")[0];
    head.appendChild(style);
}
```

`DynamicStyleExample02.htm`

该函数可以如下所示调用：

```javascript
loadStyleString("body{background-color:red}");
```

通过这种方式指定的样式会立即添加到页面中，因此应该立即看到变化。

![image](img/pen.gif)

如果你专门为 Internet Explorer 编写代码，请小心使用 `styleSheet.cssText`。如果你复用同一个 `<style>` 元素并尝试多次设置此属性，它可能会导致浏览器崩溃。此外，将 `cssText` 设置为空字符串也有导致浏览器崩溃的可能性。这是浏览器中的一个 bug，希望将来能够得到修复。

## 操作表格

HTML 中最复杂的结构之一是 `<table>` 元素。创建新表格通常意味着许多用于表格行、表格单元格、表头等的标签。由于这种复杂性，使用核心 DOM 方法来创建和更改表格可能需要大量的代码。假设你想使用 DOM 创建以下 HTML 表格：

```html
<table border="1" width="100%">
    <tbody>
        <tr>
            <td>Cell 1,1</td>
            <td>Cell 2,1</td>
        </tr>
        <tr>
            <td>Cell 1,2</td>
            <td>Cell 2,2</td>
        </tr>
    </tbody>
</table>
```

要使用核心 DOM 方法实现此此代码看起来像这样：

```javascript
//创建表格
var table = document.createElement("table");
table.border = 1;
table.width = "100%";
//创建 tbody
var tbody = document.createElement("tbody");
table.appendChild(tbody);
//创建第一行
var row1 = document.createElement("tr");
tbody.appendChild(row1);
var cell1_1 = document.createElement("td");
cell1_1.appendChild(document.createTextNode("Cell 1,1"));
row1.appendChild(cell1_1);
var cell2_1 = document.createElement("td");
cell2_1.appendChild(document.createTextNode("Cell 2,1"));
row1.appendChild(cell2_1);
//创建第二行
var row2 = document.createElement("tr");
tbody.appendChild(row2);
var cell1_2 = document.createElement("td");
cell1_2.appendChild(document.createTextNode("Cell 1,2"));
row2.appendChild(cell1_2);
var cell2_2= document.createElement("td");
cell2_2.appendChild(document.createTextNode("Cell 2,2"));
row2.appendChild(cell2_2);
//将表格添加到文档主体
document.body.appendChild(table);
```

这段代码非常冗长，且有些难以阅读。为了方便构建表格，HTML DOM 为 `<table>`、`<tbody>` 和 `<tr>` 元素增加了多个属性和方法。

`<table>` 元素增加了以下内容：

*   `caption` — 指向 `<caption>` 元素的指针（如果存在）。
*   `tBodies` — `<tbody>` 元素的 `HTMLCollection`。
*   `tFoot` — 指向 `<tfoot>` 元素的指针（如果存在）。
*   `tHead` — 指向 `<thead>` 元素的指针（如果存在）。
*   `rows` — 表格中所有行的 `HTMLCollection` 。
*   `createTHead()` — 创建 `<thead>` 元素。
*   `createTFoot()` — 创建 `<tfoot>` 元素。
*   `createCaption()` — 创建 `<caption>` 元素。
*   `insertRow(index)` — 在指定索引处创建 `<tr>` 元素。
*   `deleteRow(index)` — 删除指定索引处的 `<tr>` 元素。

`<tbody>` 元素增加了以下内容：

*   `rows` — 所有 `<tr>` 元素的 `HTMLCollection`。
*   `insertRow(index)` — 在指定索引处创建 `<tr>` 元素。
*   `deleteRow(index)` — 删除指定索引处的 `<tr>` 元素。

`<tr>` 元素增加了以下内容：

*   `cells` — 所有 `<td>` 元素的 `HTMLCollection`。
*   `insertCell(index)` — 在指定索引处创建 `<td>` 元素。
*   `deleteCell(index)` — 删除指定索引处的 `<td>` 元素。

这些属性和方法可以大幅减少创建表格的代码量。例如，之前的代码可以使用这些方法重写（高亮代码已更新）：

```javascript
//创建表格
var table = document.createElement("table");
table.border = 1;
table.width = "100%";
//创建 tbody
var tbody = document.createElement("tbody");
table.appendChild(tbody);
//创建第一行
tbody.insertRow(0);
tbody.rows[0].insertCell(0);
tbody.rows[0].cells[0].appendChild(document.createTextNode("Cell 1,1"));
tbody.rows[0].insertCell(1);
tbody.rows[0].cells[1].appendChild(document.createTextNode("Cell 2,1"));
//创建第二行
tbody.insertRow(1);
tbody.rows[1].insertCell(0);
tbody.rows[1].cells[0].appendChild(document.createTextNode("Cell 1,2"));
tbody.rows[1].insertCell(1);
tbody.rows[1].cells[1].appendChild(document.createTextNode("Cell 2,2"));
//将表格添加到文档主体
document.body.appendChild(table);
```

使用这些属性和方法创建表格使代码更符合逻辑且易于读，尽管技术上两组代码都是正确的。

## 使用 NodeLists

# 理解 `NodeList` 对象及其相关对象 `NamedNodeMap` 和 `HTMLCollection`，对于深入理解整个 DOM 至关重要。这些集合中的每一个都被认为是“活的的”（live），这意味着当文档结构发生变化时，它们会更新，从而始终包含最准确的最新信息。实际上，所有的 `NodeList` 对象都是在每次访问时针对 DOM 文档执行的查询。例如，以下代码会导致无限循环：

```javascript
var divs = document.getElementsByTagName("div"),
    i,
    div;
for (i=0; i < divs.length; i++){
    div = document.createElement("div");
    document.body.appendChild(div);
}
```

这段代码的第一部分获取文档中所有 `<div>` 元素的 `HTMLCollection`。由于该集合是“活的的”，每当页面上添加一个新的 `<div>` 元素时，它都会被添加到集合中。由于浏览器不希望保留所有已创建集合的列表，该集合仅在再次被访问时才会更新。这在像示例中的循环中产生了一个有趣的问题。循环每次执行时，都会评估条件 `i < divs.length`。这意味着获取所有 `<div>` 元素的查询被重新执行。因为循环体创建了一个新的 `<div>` 元素并将其添加到文档中，`divs.length` 的值在每次循环中都会递增；因此，由于两者都在增加，`i` 永远不会等于 `divs.length`。

当你想要遍历 `NodeList` 时，最好的方法是初始化第二个变量来存储长度，然后将迭代器与该变量进行比较，如下例所示：

```javascript
var divs = document.getElementsByTagName("div"),
    i,
    len,
    div;
for (i=0, len=divs.length; i < len; i++){
    div = document.createElement("div");
    document.body.appendChild(div);
}
```

在这个示例中，初始化了第二个变量 `len`。由于 `len` 包含了循环开始时 `divs.length` 的快照，它防止了上一个示例中出现的无限循环。这种技术在整个章节中被用来演示遍历 `NodeList` 对象的首选方法。

通常来说，最好限制与 `NodeList` 交互的次数。因为每次访问都会对文档执行查询，请尝试缓存从 `NodeList` 获取的频繁使用的值。

## 总结

文档对象模型（DOM）是一种用于访问和操作 HTML 和 XML 文档的语言无关的 API。DOM Level 1 处理将 HTML 和 XML 文档表示为节点的层次结构，可以通过 JavaScript 对其进行操作以更改底层文档的外观和结构。

DOM 由一系列节点类型组成，如下：

- 基础节点类型是 `Node`，它是文档各个部分的抽象表示；所有其他类型都继承自 `Node`。
- `Document` 类型表示整个文档，是层次结构中的根节点。在 JavaScript 中，`document` 对象是 `Document` 的实例，允许以多种不同的方式查询和检索节点。
- `Element` 节点代表文档中所有的 HTML 或 XML 元素，可以用于操作它们的内容和属性。
- 还有其他节点类型，用于文本内容、注释、文档类型、CDATA 段和文档片段。

在大多数情况下，DOM 访问按预期工作，但在处理 `<script>` 和 `<style>` 元素时通常会遇到复杂性。由于这些元素分别包含脚本和样式信息，浏览器对它们的对待通常与其他元素不同。

关于 DOM 可能最重要的的一点是它如何影响整体性能。DOM 操作是 JavaScript 中可以执行的最昂贵的操作之一，其中 `NodeList` 对象特别棘手。`NodeList` 对象是“活的”，意味着每次访问该对象时都会运行查询。由于这些问题，最好尽量减少 DOM 操作的次数。

# 第 11 章：DOM 扩展

## 本章内容简介

- 理解 Selectors API
- 使用 HTML5 DOM 扩展
- 使用私有 DOM 扩展

尽管 DOM 是一个定义相当良好的 API，但它也经常通过基于标准和私有的扩展进行增强以提供额外功能。在 2008 年之前，浏览器中发现几乎所有的 DOM 扩展都是私有的。从那时起，W3C 开始将一些成为事实标准的私有扩展编码为正式规范。

指定 DOM 扩展的两个主要标准是 Selectors API 和 `HTML5`。它们都源于开发社区的需求以及对某些方法和 API 标准化的愿望。还有一个较小的 `Element Traversal`（元素遍历）规范，带有额外的 DOM 属性。尽管这两个规范（尤其是 `HTML5`）涵盖了大量的 DOM 扩展，但私有扩展仍然存在。本章也涵盖了私有扩展。

## SELECTORS API

JavaScript 库最流行的功能之一是根据使用 CSS 选择器指定的模式检索多个匹配的 DOM 元素。事实上，`jQuery` 库（[www.jquery.com](http://www.jquery.com)）完全围绕 DOM 文档的 CSS 选择器查询构建，以便获取元素的引用，而不是使用 `getElementById()` 和 `getElementsByTagName()`。

Selectors API（[www.w3.org/TR/selectors-api](http://www.w3.org/TR/selectors-api)）由 W3C ，用于指定浏览器对 CSS 查询的原生支持。实现此功能的 JavaScript 库都必须通过编写原始的 CSS 解析器，然后使用现有的 DOM 方法导航文档并识别匹配节点。尽管库开发者努力工作以加速此类处理的性能，但在代码在 JavaScript 中运行时，所能做的是有限的。通过将其变为原生 API，解析和树形导航可以在浏览器级别完成，从而极大地提高了此类性能。

Selectors API Level 1 的核心有两个方法：`querySelector()` 和 `querySelectorAll()`。在符合标准的浏览器中，这些方法在 `Document` 类型和 `Element` 类型上均可用。Selectors API Level 1 在 Internet Explorer 8+、Firefox 3.5+、Safari 3.1+、Chrome 和 Opera 10+ 中完全实现。

### querySelector() 方法

`querySelector()` 方法接受一个 CSS 查询并返回第一个匹配模式的后代元素，如果没有匹配的元素则返回 `null`。示例如下：

![image](img/logo1.gif)

```javascript
// 获取 body 元素
var body = document.querySelector("body");
// 获取 ID 为 "myDiv" 的元素
var myDiv = document.querySelector("#myDiv");
// 获取类名为 "selected" 的元素
var selected = document.querySelector(".selected");
// 获取带有类 "button" 的图像
```



`var img = document.body.querySelector("img.button");`

`SelectorsExample01.htm`

当`querySelector()`方法用于`Document`类型时，它从文档元素开始尝试匹配模式；当用于`Element`类型时，查询仅尝试从该元素的后代中进行匹配。

CSS查询可以根据需要变得复杂或简单。如果查询中存在语法错误或不支持的选择器，则`querySelector()`会抛出错误。

### queryAll()方法

`querySelectorAll()`方法接受与`querySelector()`相同的单个参数——CSS查询，但返回所有匹配的节点而不是仅一个。该方法返回一个`NodeList`的静态实例。

需要澄清的是，返回值实际上是一个包含所有预期属性和方法的`NodeList`，但其底层实现表现为元素的**快照**，而不是一个针对文档不断重新执行的动态查询。这种实现消除了与使用`NodeList`对象相关的大部分性能开销。

任何带有有效CSS查询的`querySelectorAll()`调用都会返回一个`NodeList`对象，无论匹配的元素数量多少；如果没有找到匹配项，则该`NodeList`为空。与`querySelector()`来说，`querySelectorAll()`方法在`Document`、`DocumentFragment`和`Element`类型上均可用。以下是一些示例：

![image](img/logo1.gif)

```
//获取 <div> 中所有的 <em> 元素（类似于 getElementsByTagName("em")）
var ems = document.getElementById("myDiv").querySelectorAll("em");

//获取所有类名为 "selected" 的元素
var selecteds = document.querySelectorAll(".selected");

//获取 <p> 元素内部的所有 <strong> 元素
var strongs = document.querySelectorAll("p strong");
```

`SelectorsAPIExample02.htm`

生成的`NodeList`对象可以使用`item()`或方括号符号进行迭代以检索单个元素。这是一个示例：

```
var i, len, strong;
for (i=0, len=strongs.length; i < len; i++){
    strong = strongs[i]; //或 strongs.item(i)
    strong.className = "important";
}
```

与`querySelector()`类似，当浏览器不支持该CSS选择器或选择器存在语法错误时，`querySelectorAll()`会抛出错误。

### `matchesSelector()`方法

`Selectors API Level 2`规范在`Element`类型上引入了另一个名为`matchesSelector()`方法。该方法接受单个参数（即CSS选择器），如果给定元素匹配该选择器则返回`true`，否则返回`false`。例如：

```
if (document.body.matchesSelector("body.page1")){
    //true
}
```

该方法允许在你已经拥有元素引用的情况下，轻松地检查该元素是否会被`querySelector()`或`querySelectorAll()`返回。

截至2011年年中，还没有浏览器原生支持`matchesSelector()`；但有几个浏览器支持实验性实现。`Internet Explorer 9+`通过`msMatchesSelector()`支持该方法，`Firefox 3.6+`通过`mozMatchesSelector()`支持它，`Safari 5+`和`Chrome`通过`webkitMatchesSelector()`支持它。为了现在使用此方法，你可能想要创建一个封装函数，例如：

```
function matchesSelector(element, selector){
    if (element.matchesSelector){
        return element.matchesSelector(selector);
    } else if (element.msMatchesSelector){
        return element.msMatchesSelector(selector);
    } else if (element.mozMatchesSelector){
        return element.mozMatchesSelector(selector);
    } else if (element.webkitMatchesSelector){
        return element.webkitMatchesSelector(selector);
    } else {
        throw new Error("Not supported.");
    }
}

if (matchesSelector(document.body, "body.page1")){
    //do something
}
```

`SelectorsAPIExample03.htm`

## 元素遍历

在第9版本之前，`Internet Explorer`不会返回元素之间空白的文本节点，而所有其他浏览器都会返回。这导致了在使用`childNodes`等属性时行为上的差异。为了平衡DOM，`HTML5`引入了许多属性：

*   `childCount`:返回子节点的数量。
*   `firstElementChild`:指向第一个子元素。
*   `lastElementChild`:指向最后一个子元素。
*   `previousElementSibling`:指向上一个兄弟元素。
*   `nextElementSibling`:指向下一个兄弟元素。

在类名（class name）操作中，`className`属性用于添加、删除和替换类名。由于`className`包含单个字符串，因此在每次需要更改时都必须设置它的值，即使字符串中某些部分是不受影响。例如，考虑以下HTML代码：

```
<div class="bd user disabled">...</div>
```

该`<div>`元素被分配了三个类。要移除其中一个类，你需要将`class`属性拆分为单独的类，移除不需要的类，然后创建一个包含剩余类的字符串。以下是一个示例：

```javascript
//移除 "user" 类
//首先，获取类名列表
var classNames = div.className.split(/\s+/);

//找到要移除的类名
var pos = -1,
    i,
    len;
for (i=0, len=classNames.length; i < len; i++){
    if (classNames[i] == "user"){
        pos = i;
        break;
    }
}

//移除该类名
classNames.splice(i,1);

//将类名设置回元素
div.className = classNames.join(" ");
```

所有这些代码对于从`<div>`元素的`class`属性中移除"user"类都是必要的。替换类名和检测类名是否已应用于元素时，必须使用类似的算法。添加类名可以通过字符串拼接完成，但必须进行检查以确保你没有多次应用同一个类。许多JavaScript库都实现了辅助这些这些行为的方法。

HTML5通过为所有元素添加`classList`属性，引入了一种更简单、更安全的方法来操作类名。`classList`属性是一个名为`DOMTokenList`的新类型集合的实例。与其他DOM集合一样，`DOMTokenList`具有一个`length`属性来表示它包含多少项，并且可以通过`item()`方法或使用括号表示法检索单个项目。它还具有以下额外方法：

*   `add(value)` — 将给定的字符串值添加到列表中。如果该值已存在，则不会添加。
*   `contains(value)` — 指明给定的值是否存在于列表中（存在则为true；否则为false）。
*   `remove(value)` — 从列表中移除给定的字符串值。
*   `toggle(value)` — 如果该值已存在于列表中，则将其移除。如果值不存在，则将其添加。

上一个示例中的整个代码块可以简单地替换为以下内容：

```javascript
div.classList.remove("user");
```

使用此代码可以确保其他类名不受更改的影响。其他方法也大大降低了基本操作的复杂性，如下示例所示：

```javascript
//移除 "disabled" 类
div.classList.remove("disabled");

//添加 "current" 类
div.classList.add("current");

//切换 "user" 类的状态
div.classList.toggle("user");

//确定元素上现在有什么
if (div.classList.contains("bd") && !div.classList.contains("disabled")){
    //执行某些操作
}

//遍历所有类名
for (var i=0, len=div.classList.length; i < len; i++){
    doSomething(div.classList[i]);
}
```

`classList`属性的添加使得没有必要访问`className`属性，除非你打算完全移除或完全覆盖元素的`class`属性。`classList`属性在Firefox 3.6+和Chrome中实现。

## 焦点管理

HTML5增加了辅助DOM焦点管理的功能。第一个功能是`document.activeElement`，它始终包含一个指向当前具有焦点的DOM元素的指针。元素可以在页面加载时自动接收焦点、通过用户输入（通常使用Tab键）或通过编程使用`focus()`方法接收焦点。例如：

```javascript
var button = document.getElementById("myButton");
button.focus();
alert(document.activeElement === button); //true
```

默认情况下，当文档首次加载时，`document.activeElement`被设置为`document.body`。在文档完全加载之前，`document.activeElement`为`null`。

第二个新增是`document.hasFocus()`，它返回一个布尔值，表示文档是否具有焦点：

```javascript
var button = document.getElementById("myButton");
button.focus();
alert(document.hasFocus()); //true
```

确定文档是否具有焦点允许你判断用户正在与页面交互。这种能够查询文档以确定哪个元素拥有焦点并能够询问文档其是否具有焦点的结合对于Web应用程序的可访问性（accessibility）至关重要。可访问Web应用程序的关键组件之一是恰当的焦点管理，而能够确定哪些元素当前具有焦点是相对于过去猜测行为的重大改进。

这些属性在Internet Explorer 4+、Firefox 3+、Safari 4+、Chrome和Opera 8+中实现。

## HTMLDocument的更改

HTML5扩展了`HTMLDocument`类型以包含更多功能。与HTML5中指定的其他DOM扩展一样，这些更改基于在各个浏览器中得到良好支持的私有扩展。因此，尽管这些扩展的标准化较新，但某些浏览器已经支持这些功能一段时间了。

### readyState属性

Internet Explorer 4是第一个在`document`对象上引入`readyState`属性的浏览器。其他浏览器随后效仿，该属性最终在HTML5中被正式化。`document`的`readyState`属性具有两个可能的值：

*   `loading` — 文档正在加载。
*   `complete` — 文档已完全加载。

使用`readyState`属性的最佳方法是作为文档加载指示。在该属性广泛可用之前，你需要添加`onload`事件处理程序来设置文档已加载。基本用法：

```javascript
if (document.readyState == "complete"){
    //执行某些操作
}
```

`readyState`属性在Internet Explorer 4+、Firefox 3.6+、Safari、Chrome和Opera 9+中实现。

### 兼容模式

随着Internet Explorer 6的引入以及以标准模式或怪模式（quirks mode）渲染文档的能力，确定以何种模式渲染变得必要。Internet Explorer在`document`上添加了一个名为`compatMode`的属性，其唯一工作是指示浏览器所在的渲染模式。如下例所示，在标准模式下，`document.compatMode`等于`"CSS1Compat"`；在怪模式下，`document.compatMode`为`"BackCompat"`：

```javascript
if (document.compatMode == "CSS1Compat"){
    alert("标准模式");
} else {
    alert("怪模式");
}
```

该属性后来由Safari 3.1+、Opera和Chrome实现。因此，该属性被添加到HTML5以使其正式化。

### head属性

HTML5引入了`document.head`来指向文档的`<head>`元素，以补充`document.body`（后者指向文档的`<body>`元素）。你可以使用此属性或回退方法获取对`<head>`元素的引用：

```javascript
var head = document.head || document.getElementsByTagName("head")[0];
```

此代码在可用时使用`document.head`，否则回退到使用`getElementsByTagName()`的旧方法。

`document.head`属性在Chrome和Safari 5中实现。

### 字符集属性

HTML5描述了几个与文档字符集相关的新属性。`charset`属性指示文档实际使用的字符集，也可以用于指定新的字符集。默认情况下，此值为`"UTF-16"`，但可以通过`<meta>`元素、响应头或直接设置`charset`属性来对其更改。以下是一个示例：

```javascript
alert(document.charset); //"UTF-16"
document.charset = "UTF-8";
```

`defaultCharset`属性表示根据默认浏览器和系统设置，文档应该使用的默认字符集是什么。如果文档没有使用默认字符集，`charset`和`defaultCharset`的值可能会不同，如下例所示：

```
if (document.charset != document.defaultCharset){
    alert("Custom character set being used.");
}
```

这些属性允许人们更深入地了解并控制文档上使用的字符编码。如果使用得当，这可以让Web开发人员确保他们的页面或应用程序能够正确显示。

`document.charset`属性受Internet Explorer、`Firefox`、`Safari`、`Opera`和`Chrome`支持。`document.defaultCharset`属性受Internet Explorer、`Safari`和`Chrome`支持。

# 自定义数据属性

HTML允许元素指定带有`data-`前缀的非标准属性，以提供元素渲染或语义化所不需要的信息。这些属性可以根据需要添加并进行任意命名，只要名称以`data-`开头即可。这是一个示例：

```html
<div id="myDiv" data-appId="12345" data-myname="Nicholas"></div>
```

当定义了自定义数据属性时，可以通过元素的`dataset`属性进行访问。`dataset`属性包含一个`DOMStringMap`实例，它是键值对的映射。每个格式为`data-name`的属性都由一个与属性名等效但但不包含`data-`前缀的属性表示（例如，属性`data-myname`由一个名为`myname`的属性表示）。示例用法：

```javascript
//此示例中使用的方法仅用于说明目的
var div = document.getElementById("myDiv");

// 获取值
var appId = div.dataset.appId;
var myName = div.dataset.myname;

// 设置值
div.dataset.appId = 23456;
div.dataset.myname = "Michael";

// 存在 "myname" 值吗？
if (div.dataset.myname){
```



`alert("Hello, " + div.dataset.myname);`

当需要将非视觉化数据绑定到元素上以便进行其他形式的处理时，自定义数据属性非常有用。这是用于链接追踪和页面混搭（mashups）的常用技术，以便更好地识别页面的部分。

截至本文写作时，只有 `Firefox 6+` 和 `Chrome` 实现了这一功能。

# 标记插入

尽管 DOM 为文档中的节点提供了细粒度的控制，但在尝试向文档中注入大量新 HTML 时，它可能会变得繁琐。与其创建一系列 DOM 节点并按照正确的顺序连接它们，不如使用一种标记插入功能来注入一段 HTML 字符串要简单得多（也更快）。以下 DOM 扩展在 HTML5 中已标准化，以实现此目的。

## innerHTML 属性

在读模式下使用时，`innerHTML` 返回表示所有节点（包括元素、注释和文本节点）的 HTML。在写模式下使用时，`innerHTML` 根据指定的值用一个新的 DOM 子树完全替换元素中的所有子节点。考虑以下 HTML 代码：

```html
<div id="content">
<p>This is a <strong>paragraph</strong> with a list following it.</p>
<ul>
<li>Item 1</li>
<li>Item 2</li>
<li>Item 3</li>
</ul>
</div>
```

对于示例中的 `<div>` 元素，`innerHTML` 属性返回以下字符串：

```html
<p>This is a <strong>paragraph</strong> with a list following it.</p>
<ul>
<li>Item 1</li>
<li>Item 2</li>
<li>Item 3</li>
</ul>
```

`innerHTML` 返回的准确文本因浏览器而异。`Internet Explorer` 和 `Opera` 倾向于将所有标签转换为大写，而 `Safari`、`Chrome` 和 `Firefox` 则按照文档中指定的方式返回 HTML，包括空格和缩进。你不能依赖 `innerHTML` 的返回值在不同浏览器之间完全相同。

### 使用 innerHTML 写入

在写模式下使用时，`innerHTML` 将给定字符串解析为 DOM 子树，并用它替换所有现有子节点。由于字符串被视为 HTML，所有标签都会按照浏览器处理 HTML 的标准方式转换为元素（再次，这因浏览器而异）。如下所示设置不带任何 HTML 标签的简单文本将设置纯文本：

```javascript
div.innerHTML = "Hello world!";
```

将 `innerHTML` 设置为包含 HTML 的字符串行为大不同，因为 `innerHTML` 会对其进行解析。考虑以下示例：

```javascript
div.innerHTML = "Hello & welcome, <b>\"reader\"!</b>";
```

该操作的结果如下：

```html
<div id="content">Hello &amp; welcome, <b>&quot;reader&quot;!</b></div>
```

设置 `innerHTML` 后，你可以像访问文档中任何其他节点一样访问新创建的节点。

![image](img/pen.gif)

设置 `innerHTML` 会导致浏览器将 HTML 字符串解析为适当的 DOM 树。这意味着设置 `innerHTML` 然后读取它通常会导致返回一个不同的字符串。这是因为返回的字符串是为原始 HTML 创建的 DOM 子树序列化的结果。

### innerHTML 的局限性

`innerHTML` 有一些局限性。对于，在大多数浏览器中无法通过 `innerHTML` 插入 `<script>` 元素。`Internet Explorer` 8 及更早版本允许这种操作，但只要指定了 `defer` 属性且 `<script>` 元素之前有一个作用域元素即可。`<script>` 元素被视为 `NoScope` 元素，这意味着它在页面上没有视觉表示，就像 `<style>` 元素或注释一样。`Internet Explorer` 会剥离 `innerHTML` 字符串开头的所有 `NoScope` 元素，这意味着以下内容无效：

```javascript
div.innerHTML = "<script defer>alert('hi');</script>"; //无效
```

在这种情况下，`innerHTML` 字符串以 `NoScope` 元素开头，因此它是空的。为了让脚本正常工作，你必须在其之前一个作用域元素，例如文本节点。以下行均有效：

```javascript
div.innerHTML = "_<script defer>alert('hi');</script>";
div.innerHTML = "<div> </div><script defer>alert('hi');</script>";
div.innerHTML = "<input type=\"hidden\"><script defer>alert('hi');</script>";
```

Firefox 对于通过 `application/xhtml+xml` 内容类型传输的 XHTML 文档，其对 `innerHTML` 的支持更为严格。在 XHTML 文档中使用 `innerHTML` 时，你必须指定格式良好的 XHTML 代码。如果代码不符合格式，设置 `innerHTML` 将静默失败。

每当你使用 `innerHTML` 从代码外部源插入 HTML 时，在将其传递给 `innerHTML` 之前对 HTML 进行清理是非常关重要的。Internet Explorer 8 为此目的添加了 `window.toStaticHTML()` 方法。该方法接受一个参数（即 HTML 字符串），并返回一个清理后的版本，该版本已从源中移除所有的脚本节点和脚本事件处理程序属性。以下是一个示例：

```javascript
var text = "<a href=\"#\" onclick=\"alert('hi')\">Click Me</a>";
var sanitized = window.toStaticHTML(text); //Internet Explorer 8 only
alert(sanitized); //"<a href=\"#\">Click Me</a>"
```

此示例通过 `toStaticHTML()` 运行了一个 HTML 链接字符串。清理后的文本不再包含 `onclick` 属性。尽管 Internet Explorer 8 是唯一具有此原生功能的浏览器，但在使用 `innerHTML` 时，仍建议谨慎操作，并在可能的情况下插入之前手动检查文本。

## outerHTML 属性

当在读模式下调用 `outerHTML` 时，它会返回调用它的元素的 HTML 及其子节点。当在写模式下调用时，`outerHTML` 将调用它的节点替换为从解析给定 HTML 字符串中创建的 DOM 子树。考虑以下 HTML 代码：

![image](img/logo1.gif)

```html
<div id="content">
<p>This is a <strong>paragraph</strong> with a list following it.</p>
<ul>
<li>Item 1</li>
<li>Item 2</li>
<li>Item 3</li>
</ul>
</div>
```

`OuterHTMLExample01.htm`

当在此示例中对 `<div>` 运行 `outerHTML` 时，将返回相同的代码，包括 `<div>` 本身的代码。请注意，根据浏览器解析和解释 HTML 代码的方式，可能会存在差异。（这些是在使用 `innerHTML` 时也会注意到的相同差异。）

可以使用以下方式使用 `outerHTML` 设置值：

```javascript
div.outerHTML = "<p>This is a paragraph.</p>";
```

这段代码执行的操作与以下 DOM 代码相同：

```javascript
var p = document.createElement("p");
p.appendChild(document.createTextNode("This is a paragraph."));
div.parentNode.replaceChild(p, div);
```

新的 `<p>` 元素替换了 DOM 树中的原始 `<div>` 元素。

`outerHTML` 属性被 Internet Explorer 4+、Safari 4+、Chrome 和 Opera 8+ 支持。Firefox 从版本 7 开始仍然不支持 `outerHTML`。

## insertAdjacentHTML() 方法

最后添加的标记插入方法是 `insertAdjacentHTML()` 方法。该方法同样源于 Internet Explorer，接受两个参数：插入的位置和要插入的 HTML 文本。第一个参数必须是以下值之一：

*   `"beforebegin"` — 在元素之前之前作为前一个兄弟节点插入。
*   `"afterbegin"` — 在元素内部，作为第一个元素之前的新子元素或一系列子元素插入。
*   `"beforeend"` — 在元素内部，作为最后一个元素之前的新子元素或一系列子元素插入。
*   `"afterend"` — 在元素之后立即作为后一个兄弟节点插入。

注意 `insertAdjacentHTML()` 是不区分大小写的。例如：

```javascript
element.insertAdjacentHTML("beforebegin", "<div>before element</div>");
element.insertAdjacentHTML("afterbegin", "<div>after start</div>");
element.insertAdjacentHTML("beforeend", "<div>before end</div>");
element.insertAdjacentHTML("afterend", "<div>after element</div>");
```

## 内存与性能

`insertAdjacentHTML()` 方法被 Internet Explorer、Firefox、Safari、Opera 和 Chrome 支持。

频繁使用 `innerHTML` 或 `outerHTML` 会导致性能问题。当设置 `innerHTML` 时，浏览器必须解析 HTML 字符串并重建 DOM 子树，这是一项昂贵的操作，特别是对于大型结构。

例如，在循环内部使用 `innerHTML` 是无效的：

```javascript
for (var i = 0; i < values.length; i++){
  ul.innerHTML += "<li>" + values[i] + "</li>";
}
```

这段代码效率很低，因为每次迭代都会访问并重新解析 `innerHTML`。更好的方法是单独构建字符串并像这样赋值一次：

```javascript
var itemsHtml = "";
for (var i = 0; i < values.length; i++){
  itemsHtml += "<li>" + values[i] + "</li>";
}
ul.innerHTML = itemsHtml;
```

这种方法更有效，因为它将 `innerHTML` 的赋值限制为仅一次。

## scrollIntoView() 方法

DOM 规范未解决的问题之一是如何滚动页面的区域。为了填补这一空白，浏览器实现了几种以不同方式控制滚动的方法。在各种专有方法中，只有 `scrollIntoView()` 被选中包含在 HTML5 中。

例如，使用了如下代码：

```javascript
//确保此元素可见
document.forms[0].scrollIntoView();
```

`scrollIntoView()` 方法存在于所有 HTML 元素上，它会滚动浏览器窗口或容器元素，使该元素在视口可见。如果提供了 `true` 参数或省略该参数，窗口将滚动到元素的顶部位于视口顶部（如果可行的话）；否则，元素将滚动到使其在视口内完全可见。

## 专有扩展

尽管所有浏览器厂商都理解遵循标准的重要性，但它们都有向 DOM 添加专有扩展的历史，以填补功能上的感知空白。尽管这在表面似乎是一件坏事，但专有扩展为 Web 开发社区提供了许多重要功能，这些功能后来被编码进 HTML5 等标准中。

仍有大量 DOM 扩展属于私有性质，尚未被纳入标准。这并不意味着它们以后不会被采用为标准，只是在编写此时，它们仍然是私有的，并且仅被部分浏览器采用。

## 文档模式 (Document Mode)

Internet Explorer 8 引入了一个名为 `document mode` 的新概念。页面的文档模式决定了它可以访问哪些功能。这意味着它具有特定级别的 CSS 支持、可以通过 JavaScript 脚本的特定数量的功能以及处理文档类型（doctype）的特定方式。从 Internet Explorer 9 开始，共有四种不同的文档模式：

- `Internet Explorer 5` — 以兼容模式（quirks mode）渲染页面（Internet Explorer 5 的默认模式）。Internet Explorer 8 及更高版本的新功能不可用。
- `Internet Explorer 7` — 以 Internet Explorer 7 标准模式渲染页面。Internet Explorer 8 及更高版本的新功能不可用。
- `Internet Explorer 8` — 以 Internet Explorer 8 标准模式渲染页面。可以使用 Internet Explorer 8 的新功能，你可以访问 `Selectors API`、更多 CSS 2 选择器、某些 CSS3 特性以及某些 HTML 5 特性。Internet Explorer 9 的功能不可用。
- `Internet Explorer 9` — 以 Internet Explorer 9 标准模式渲染页面。可以使用 Internet Explorer 9 的新功能，如 `ECMAScript 5`、完整的 CSS3 支持和更多的 HTML5 特性。这种文档模式被认为是最先进的。

文档模式的概念对于理解 Internet Explorer 8 及更高版本的工作原理非常重要。

你可以通过使用 `X-UA-Compatible` HTTP 头部或等等的 `<meta>` 标签来强制指定的文档模式：

```html
<meta http-equiv="X-UA-Compatible" content="IE=IEVersion">
```

该字段中的 Internet Explorer 版本有几个不同的可能值，它们并不一定映射到四种文档模式：

- `Edge` — 始终将文档放入可用的最新文档模式中。忽略 `Doctype`。对于 Internet Explorer 8，这将强制将文档模式始终设置为 Internet Explorer 8 标准；对于 Internet Explorer 9，文档模式被强制为 Internet Explorer 9 标准模式。
- `EmulateIE9` — 如果存在 doctype，则将文档模式设置为 Internet Explorer 9 标准，否则将文档模式设置为 Internet Explorer 5。
- `EmulateIE8` — 如果存在 doctype，则将文档模式设置为 Internet Explorer 8 标准，否则将文档模式设置为 Internet Explorer 5。
- `EmulateIE7` — 如果存在 doctype，则将文档模式设置为 Internet Explorer 7 标准，否则将文档模式设置为 Internet Explorer 5。
- `9` — 强制文档模式为 Internet Explorer 9 标准。忽略 `Doctype`。
- `8` — 强制文档模式为 Internet Explorer 8 标准。忽略 `Doctype`。
- `7` — 强制文档模式为 Internet Explorer 7 标准。忽略 `Doctype`。
- `5` — 强制文档模式为 Internet Explorer 5。忽略 `Doctype`。

例如，要让文档模式的行为像在 Internet Explorer 7 中一样，可以使用以下代码：

```html
<meta http-equiv="X-UA-Compatible" content="IE=EmulateIE7">
```

而无论 doctype 如何，要强制使用 Internet Explorer 7 标准模式，请使用此：

```html
<meta http-equiv="X-UA-Compatible" content="IE=7">
```

你并不要求在页面上设置 `X-UA-Compatible` 字段。默认情况下，浏览器使用 doctype 来决定文档模式应该是最佳可用标准模式还是兼容模式。

你可以使用 `document.documentMode` 属性来确定给定页面的文档模式，这是 Internet Explorer 8 的一个新功能，它返回正在使用的文档模式版本（在版本 9 中，值可以是 5, 7, 8 或 9）：

```javascript
var mode = document.documentMode;
```



使用此属性可以给你一个关于页面将如何行为的提示。该属性在所有文档模式下可用。

## children 属性 (The children Property)

Internet Explorer 在 9 版本之前与其他浏览器解释文本节点中空白字符的方式差异导致了`children`属性的创建。`children`属性是一个`HTMLCollection`，它只包含也是元素的元素的子节点。否则，`children`属性与`childNodes`相同，当一个元素只有元素作为子节点时，它可能包含相同的项。`children`属性的访问方式如下：

```
var childCount = element.children.length;
var firstChild = element.children[0];
```

`children`集合在 Internet Explorer 5、Firefox 3.5、Safari 2（有 Bug）、Safari 3（完整）、Opera 8 和 Chrome（所有版本）中支持。Internet Explorer 8 及早期版本也会在`children`集合中返回注释（而 Internet Explorer 9 及更高版本则不会）。

## contains() 方法 (The contains() Method)

通常需要确定给定节点是否是另一个节点的后代。Internet Explorer 首次引入`contains()`方法作为提供此类信息的方法，而无需向上遍历 DOM 文档树。`contains()`方法在应该开始搜索的祖先节点上调用，并接受一个参数，即怀疑的后代节点。如果该节点作为根节点的后代存在，则方法返回`true`；否则返回`false`。这里有一个示例：

```
document.documentElement.contains(document.body)
```

此示例测试`<body>`元素是否是`<html>`元素的后代，在格式良好的 HTML 页面中返回`true`。`contains()`方法支持 Internet Explorer、Firefox 9+、Safari、Opera 和 Chrome。

另一种确定关系的方法是使用 DOM Level 3 `compareDocumentPosition()`方法，该方法支持 Internet Explorer 9+、Firefox、Safari 和 Chrome。该方法确定节点之间的关系并返回一个掩码。掩码的值所示：

| 掩码 | 节点之间的关系 |
| --- | --- |
| 1 | 断开（传入节点不在文档中） |
| 2 | 在之前（传入节点在 DOM 文档树中位于参考节点之前） |
| 4 | 在之后（传入节点在 DOM 文档树中位于参考节点之后） |
| 8 | （传入节点是参考节点的祖先） |
| 16 | 被包含（传入节点是参考节点的后代） |

为了模仿`contains()`方法，你会感兴趣 16 掩码。`compareDocumentPosition()`的结果可以通过位与运算来确定参考节点是否包含给定节点。这里有一个示例：

```
var result = document.documentElement.compareDocumentPosition(document.body);
alert(!!(result & 16));
```

当执行此代码时，结果变为 20（4 代表“在之后”加 16 代表“被包含”）。对结果应用 16 掩码会返回一个非零数字，两个非（NOT）运算符会将该值转换为布尔值。

可以通过浏览器和能力检测的一点帮助来创建一个通用的`contains`函数，如下所示：

![image](img/logo1.gif)

```
function contains(refNode, otherNode){
  if (typeof refNode.contains == "function" &&
      (!client.engine.webkit || client.engine.webkit >= 522)){
    return refNode.contains(otherNode);
  } else if (typeof refNode.compareDocumentPosition == "function"){
    return !!(refNode.compareDocumentPosition(otherNode) & 16);
  } else {
    var node = otherNode.parentNode;
    do {
      if (node === refNode){
        return true;
      } else {
        node = node.parentNode;
      }
    } while (node !== null);
    return false;
  }
}
```

ContainsExample02.htm

此函数结合了三种判断节点是否为另一个节点的后代的方法。第一个参数是引用节点，第二个参数是待检查的节点。在函数体中，第一个检查是查看`refNode`上是否存在`contains()`方法（能力检测）。这部分代码还检查了所使用的 WebKit 版本。如果函数存在且不是 WebKit（`!client.engine.webkit`），则代码可以继续。同样，如果浏览器是 WebKit 且至少是 Safari 3（`WebKit 522` 及更高版本），则代码可以继续。低于 522 的 WebKit 具有`contains()`方法，但无法正常工作。

接下来是检查是否存在`compareDocumentPosition()`方法，函数的最后部分从`otherNode`开始向上遍历 DOM 结构，递归地获取`parentNode`并检查它是否等于`refNode`。在文档树的最顶端，`parentNode`将为`null`，循环将结束。这是针对旧版本 Safari 的备用策略。

## 标记插入 (Markup Insertion)

虽然 HTML5 从 Internet Explorer 采纳了`innerHTML`和`outerHTML`标记插入属性，但还有两个属性未被采纳。HTML5 中排除的另外两个属性是`innerText`和`outerText`。

### innerText 属性

`innerText`属性作用于元素内包含的所有文本内容，无论这些文本在子树中的深度有多深。当用于读取值时，`innerText`按深度优先的顺序拼接子树中所有文本节点的值。当用于写入值时，`innerText`会移除元素的所有子节点并插入一个包含给定值的文本节点。考虑以下 HTML 代码：

```html
<div id="content">
  <p>This is a <strong>paragraph</strong> with a list following it.</p>
  <ul>
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
  </ul>
</div>
```

`InnerTextExample01.htm`

对于示例中的`<div>`元素，`innerText`属性返回以下字符串：

```
This is a paragraph with a list following it.
Item 1
Item 2
Item 3
```

注意，不同的浏览器处理空白字符的方式不同，因此格式可能包含也可能不包含原始 HTML 代码中的缩进。

使用`innerText`属性设置`<div>`元素的内容只需这一行代码：

```javascript
div.innerText = "Hello world!";
```

`InnerTextExample02.htm`

执行此行代码后，页面的 HTML 实际上变为了以下内容：

```html
<div id="content">Hello world!</div>
```

设置`innerText`会移除之前存在的所有子节点，完全改变 DOM 子树。此外，设置`innerText`会对文本中可能出现的所有 HTML 语法字符（小于号、大于号、引号和和符号）进行编码。这是一个示例：

```javascript
div.innerText = "Hello & welcome, <b>\"reader\"!</b>";
```

`InnerTextExample03.htm`

该操作的结果如下：

```html
<div id="content">Hello &amp; welcome, &lt;b&gt;&quot;reader&quot;!&lt;/b&gt;</div>
```

设置`innerText`永远不会产生除容器的文本节点以外的结果，因此必须对文本进行 HTML 编码以保持该单个文本节点。`innerText`属性也用于提取 HTML 标签。通过如下所示，将`innerText`设置为其自身的`innerText`：

```javascript
div.innerText = div.innerText;
```

执行此代码会将容器的内容替换为仅已存在的文本。

`innerText`属性支持 Internet Explorer 4+、Safari 3+、Opera 8+ 以及 Chrome。Firefox 不支持`innerText`，但它支持一个名为`textContent`的对应属性。`textContent`属性在 DOM Level 3 中规范，并受 Internet Explorer 9+、Safari 3+、Opera 10+ 以及 Chrome 支持。为了跨浏览器兼容，使用以下函数来检查哪个属性可用是有帮助的：

```javascript
function getInnerText(element){
  return (typeof element.textContent == "string") ?
    element.textContent : element.innerText;
}

function setInnerText(element, text){
  if (typeof element.textContent == "string"){
    element.textContent = text;
  } else {
    element.innerText = text;
  }
}
```

`InnerTextExample05.htm`

这些方法每个都期望传入一个元素。然后检查该元素是否具有`textContent`属性。如果是，则`typeof element.textContent`应该是`"string"`。如果`textContent`不可用，每个函数都将使用`innerText`。可以如下所示调用它们：

```javascript
setInnerText(div, "Hello world!");
alert(getInnerText(div)); //"Hello world!"
```

使用这些函数可以确保根据浏览器可用属性使用正确的属性。

`innerText`返回的内容与`textContent`返回的内容之间存在细微差异。`innerText`会跳过内联样式和脚本块，而`textContent`会返回任何内联样式或脚本代码以及其他文本。避免浏览器差异的最佳方法是在浅层 DOM 子树上或在没有内联样式或内联脚本的 DOM 部分读取文本。

### outerText 属性

`outerText`属性的工作方式与`innerText`相同，但它包含了调用它的节点本身。对于读取文本值，`outerText`和`innerText`的行为基本相同。但在写入模式下，`outerText`的行为非常不同。它不是仅替换所用元素的子节点，`outerText`实际上替换了整个元素。考虑以下内容：

```javascript
div.outerText = "Hello world!";
```

这一行代码等同于以下两行：

```javascript
var text = document.createTextNode("Hello world!");
div.parentNode.replaceChild(text, div);
```

本质上，新的文本节点完全替换了设置`outerText`的元素。从那个时刻起，该元素不再存在于文档中，且无法访问。

`outerText`属性支持 Internet Explorer 4+、Safari 3+、Opera 8+ 以及 Chrome。此属性通常不使用，因为它修改了被访问的元素。建议尽可能避免使用。

## 滚动 (Scrolling)

如之前提到的，滚动是 HTML5 之前不存在规范的领域。虽然`scrollIntoView()`在 HTML5 中标准化，但在各种浏览器中仍有专用方法。以下每个方法作为`HTMLElement`类型的扩展，因此在所有元素上可用：

- `scrollIntoViewIfNeeded(alignCenter)`：滚动浏览器窗口或容器元素，使元素在不在视口内时可见；如果元素已经在视口中，此方法将不执行任何操作。可选的`alignCenter`参数如果设置为 true，将尝试将元素放在视口中心。该方法在 Safari 和 Chrome 中实现。
- `scrollByLines(lineCount)`：根据给定行数的高度滚动元素的内容，行数可以是正数也可以负数。该方法在 Safari 和 Chrome 中实现。
- `scrollByPages(pageCount)`：根据页面的高度滚动元素的内容，页面高度由元素的高度决定。该方法在 Safari 和 Chrome 中实现。

请记住，`scrollIntoView()`和`scrollIntoViewIfNeeded()`作用于元素的容器，而`scrollByLines()`和`scrollByPages()`影响元素本身。以下是这些用法示例：

```javascript
// 按行滚动五行
document.body.scrollByLines(5);

// 确保此元素在不在时可见
document.images[0].scrollIntoViewIfNeeded();

// 向上滚动一页纸
document.body.scrollByPages(-1);
```

由于`scrollIntoView()`是所有浏览器都支持的方法，因此它通常是唯一使用的方法。

## 总结

虽然 DOM 定义了与 XML 和 HTML 文档交互的核心 API，但有几项规范为标准 DOM 提供了扩展。许多扩展是基于专有扩展的，当其他浏览器开始模拟它们的功能时，这些扩展后来变成了事实上的标准。本章涵盖的三个规范是：

*   选择器 API（Selectors API）：定义了两种根据 CSS 选择器检索 DOM 元素的方法：`querySelector()`和`querySelectorAll()`。
*   元素遍历（Element Traversal）：在 DOM 元素上定义了额外的属性，允许轻松地遍历到下一个相关的 DOM 元素。这种需求的出现是因为 DOM 对空白字符的处理，这些空白字符在元素之间创建了文本节点。
*   HTML5：为标准 DOM 提供了大量的扩展。这些包括对`innerHTML`等事实性标准的标准化，以及用于处理焦点管理、字符集、滚动等的额外功能。

目前 DOM 扩展的数量较少，但几乎可以肯定，随着 Web 技术的演进，这个数量将继续增长。浏览器仍在尝试专有扩展，如果这些扩展成功，最终可能会成为伪标准，或被纳入未来版本的规范中。

# 第 12 章：DOM Level 2 和 3

## 本章内容

*   第 2 和 3 级中引入的 DOM 更改
*   用于操作样式的 DOM API
*   DOM 遍历和范围（ranges）的使用

DOM 第一级侧重于定义 HTML 和 XML 文档的底层结构。DOM 第二级和 3 级在该结构的基础上引入了更多的交互性和对更高级 XML 特征的支持。因此，DOM 第二级和 3 级实际上由多个模块组成，这些模块虽然相关，但描述的是 DOM 的非常具体的子集。这些模块如下：

*   DOM 核心（DOM Core）：基于第一级核心，为节点添加了方法和属性。
*   DOM 视图（DOM Views）：根据样式信息为文档定义不同的视图。
*   DOM 事件（DOM Events）：解释如何使用事件将交互性绑定到 DOM 文档。
*   DOM 样式（DOM Style）：定义了如何通过程序访问和更改 CSS 样式信息。
*   DOM 遍历和范围（DOM Traversal and Range）：引入了遍历 DOM 文档和选择其特定部分的新接口。
*   DOM HTML（DOM HTML）：基于第一级 HTML，添加了属性、方法和新接口。

本章将探索这些模块中的每一个，DOM Events 除外，后者将在第 13 章中详细介绍。

![image](img/pen.gif)

DOM Level 3 还包含 XPath 模块以及加载与保存（Load and Save）模块。这些将在第 18 章讨论。

## DOM 更改

DOM Level 2 和 3 核心的目的是扩展 DOM API 以涵盖 XML 的所有需求，并提供更好的错误处理和特性检测。在大多数情况下，这意味着支持 XML 命名空间的概念。DOM Level 2 核心没有引入任何新类型；它只是增强了 DOM Level 1 中定义的类型，包含了新的方法和属性。DOM Level 3 核心进一步扩展了现有类型，并引入了几个新类型。

同样，DOM Views 和 HTML 扩展了 DOM 接口，提供了新的属性和方法。这两个模块相当较小，因此与核心部分放在一起，讨论对基础 JavaScript 对象的更改。你可以使用以下代码判断哪些浏览器支持这些 DOM 的部分：



`var supportsDOM2Core = document.implementation.hasFeature("Core", "2.0");`

`var supportsDOM3Core = document.implementation.hasFeature("Core", "3.0");`

`var supportsDOM2HTML = document.implementation.hasFeature("HTML", "2.0");`

`var supportsDOM2Views = document.implementation.hasFeature("Views", "2.0");`

`var supportsDOM2XML = document.implementation.hasFeature("XML", "2.0");`

![image](img/pen.gif)

本章仅涵盖浏览器已实现的 DOM 部分；尚未被任何浏览器实现的部分将不提及。

## XML 命名空间

XML 命名空间允许来自不同基于 XML 语言的元素混合在一个良好的文档中，而不担心元素名称冲突。从技术上讲，HTML 不支持 XML 命名空间但在 XHTML 中支持；因此，本节的示例使用的是 XHTML。

命名空间使用 `xmlns` 属性指定。XHTML 的命名空间是 `http://www.w3.org/1999/xhtml`，并且应该包含在任何良好的 XHTML 页面的 `<html>` 元素上，如下例所示：

```
<html xmlns="http://www.w3.org/1999/xhtml">
    <head>
        <title>Example XHTML page</title>
    </head>
    <body>
        Hello world!
    </body>
</html>
```

对于此示例，所有元素默认被认为是 XHTML 命名空间的一部分。你可以使用 `xmlns` 显式地为 XML 命名空间创建一个前缀，后跟一个冒号，然后是前缀，如下例所示：

```
<xhtml:html xmlns:xhtml="http://www.w3.org/1999/xhtml">
    <xhtml:head>
        <xhtml:title>Example XHTML page</xhtml:title>
    </xhtml:head>
    <xhtml:body>
        Hello world!
    </xhtml:body>
</xhtml:html>
```

在这里，XHTML 的命名空间使用 `xhtml` 前缀定义，要求所有 XHTML 元素都以该前缀开头。属性也可以进行命名空间处理以避免语言之间的混淆，如下例所示：

```
<html xmlns:xhtml="http://www.w3.org/1999/xhtml">
    <xhtml:head>
        <xhtml:title>Example XHTML page</xhtml:title>
    </xhtml:head>
    <xhtml:body xhtml:class="home">
        Hello world!
    </xhtml:body>
</xhtml:html>
```

在此示例中，`class` 属性带有 `xhtml` 前缀。当文档中只使用一种语言时，命名空间并不是必要的；但在混合两种语言时，它非常有用。考虑以下这个包含 XHTML 和 SVG 的文档：

```
<html xmlns="http://www.w3.org/1999/xhtml">
    <head>
        <title>Example XHTML page</title>
    </head>
    <body>
        <svg xmlns="http://www.w3.org/2000/svg" version="1.1"
             viewBox="0 0 100 100" style="width:100%; height:100%">
            <rect x="0" y="0" width="100" height="100" style="fill:red" />
        </svg>
    </body>
</html>
```

在此示例中，`<svg>` 元素通过设置自己的命名空间被指示为异包含文档。`<svg>` 元素的所有子元素以及所有属性都被认为属于 `http://www.w3.org/2000/svg` 命名空间。尽管文档技术上是 XHTML 文档，由于使用了命名空间，SVG 代码被认为是有效的。

此类文档有趣的问题在于，当调用文档方法与文档中的节点交互时会发生什么。创建新元素时，它属于哪个命名空间？查询特定标签名时，哪些命名空间应该包含在结果中？DOM 第二级核心通过为大多数 DOM Level 1 方法提供命名空间特定的版本来回答这些问题。

## Node 的更改

`Node` 类型在 DOM 2 中演变为包含以下命名空间特定的属性：

- `localName`：不带命名空间前缀的节点名。
- `namespaceURI`：节点的命名空间 URI，未指定则为 `null`。
- `prefix`：命名空间前缀，未指定则为 `null`。

当节点使用命名空间前缀时，`nodeName` 等同于 `prefix` + ":" + `localName`。考虑以下示例：

![image](img/logo1.gif)

```
<html xmlns="http://www.w3.org/1999/xhtml">
    <head>
        <title>Example XHTML page</title>
    </head>
    <body>
        <s:svg xmlns:s="http://www.w3.org/2000/svg" version="1.1"
             viewBox="0 0 100 100" style="width:100%; height:100%">
            <s:rect x="0" y="0" width="100" height="100" style="fill:red" />
        </s:svg>
    </body>
</html>
```

### NamespaceExample.xml

对于 `html` 元素，`localName` 和 `tagName` 为 `"html"`，`namespaceURI` 为 `"http://www.w3.org/1999/xhtml"`，前缀为 `null`。对于 `s:svg` 元素，`localName` 为 `"svg"`，`tagName` 为 `"s:svg"`，`namespaceURI` 为 `"http://www.w3.org/2000/svg"`，前缀为 `"s"`。

DOM Level 3 更进了一步，并引入了以下方法来处理命名空间：

- `isDefaultNamespace(namespaceURI)` — 当指定的 `namespaceURI` 是节点的默认命名空间时，返回 `true`。
- `lookupNamespaceURI(prefix)` — 返回给定前缀的命名空间 URI。
- `lookupPrefix(namespaceURI)` — 返回给定 `namespaceURI` 的前缀。

在上例示例中，可以执行以下代码：

```
alert(document.body.isDefaultNamespace("http://www.w3.org/1999/xhtml")); //true

//假设 svg 包含对 <s:svg> 的引用
alert(svg.lookupPrefix("http://www.w3.org/2000/svg"));  //"s"
alert(svg.lookupNamespaceURI("s"));  //"http://www.w3.org/2000/svg"
```

这些方法在你拥有一个节点引用但不知道它与文档其他部分之间的关系时非常有用。

### 文档的更改

`Document` 类型在 DOM Level 2 中被更改，包含了以下特定命名空间的方法：

- `createElementNS(namespaceURI, tagName)` — 创建一个新元素，其 `tagName` 是 `namespaceURI` 所指命名空间的一部分。
- `createAttributeNS(namespaceURI, attributeName)` — 创建一个新的属性节点，其作为 `namespaceURI` 所指命名空间的一部分。
- `getElementsByTagNameNS(namespaceURI, tagName)` — 返回具有给定 `tagName` 的元素 `NodeList`，这些元素也是 `namespaceURI` 所指命名空间的一部分。

这些方法通过传入要使用的命名空间的空间 URI（而不是命名空间前缀）来使用，如下例所示：

```
//创建一个新的 SVG 元素
var svg = document.createElementNS("http://www.w3.org/2000/svg","svg");

//为随机命名空间创建新属性
var att = document.createAttributeNS("http://www.somewhere.com", "random");

//获取所有 XHTML 元素
var elems = document.getElementsByTagNameNS("http://www.w3.org/1999/xhtml", "*");
```

只有当一个给定的文档中存在两个或多个命名空间时，这些特定命名空间的方法才是必要的。

### 元素的更改

DOM Level 2 Core 中对 `Element` 的更改大部分与属性有关。引入了以下新方法：

- `getAttributeNS(namespaceURI, localName)` — 从 `namespaceURI` 代表的命名空间中获取名称为 `localName` 的属性。
- `getAttributeNodeNS(namespaceURI, localName)` — 从 `namespaceURI` 代表的命名空间中获取名称为 `localName` 的属性节点。
- `getElementsByTagNameNS(namespaceURI, tagName)` — 返回具有给定 `tagName` 的后代元素 `NodeList`，这些元素也是 `namespaceURI` 所指命名空间的一部分。
- `hasAttributeNS(namespaceURI, localName)` — 确定元素是否具有来自 `namespaceURI` 代表的命名空间且名称为 `localName` 的属性。注意：DOM Level 2 Core 还增加了一个用于不带命名空间使用的 `hasAttribute()` 方法。
- `removeAttributeNS(namespaceURI, localName)` — 从 `namespaceURI` 代表的命名空间中移除名称为 `localName` 的属性。
- `setAttributeNS(namespaceURI, qualifiedName, value)` — 设置 `namespaceURI` 代表的命名空间中名称为 `qualifiedName` 且等于 `value` 的属性。
- `setAttributeNodeNS(attNode)` — 设置来自 `namespaceURI` 代表的命名空间的属性节点。

这些方法的行为与它们的 DOM Level 1 对应方法相同，不同在于第一个参数，第一个参数始终是命名空间 URI（`setAttributeNodeNS()` 除外）。

### NamedNodeMap 的更改

`NamedNodeMap` 类型也引入了以下处理命名空间的方法。由于属性是由 `NamedNodeMap` 表示的，因此这些方法主要适用于属性。

- `getNamedItemNS(namespaceURI, localName)` — 从 `namespaceURI` 代表的命名空间中获取名称为 `localName` 的项。
- `removeNamedItemNS(namespaceURI, localName)` — 从 `namespaceURI` 代表的命名空间中移除名称为 `localName` 的项。
- `setNamedItemNS(node)` — 添加 `node`，该节点应具有命名空间信息。

这些方法很少使用，因为属性通常直接从元素访问。

### 其他更改

DOM Level 2 对 DOM 的某些部分做了一些细微更改。这些更改与命名空间无关，而是指向 API 的健性和完整性。

### DocumentType 的更改

`DocumentType` 类型增加了三个属性：`publicId`、`systemId` 和 `internalSubset`。`publicId` 和 `systemId` 属性表示在 Level 1 中是无法访问的数据。考虑以下 HTML doctype：

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" 
     "http://www.w3.org/TR/html4/loose">
```

在此 doctype 中，`publicId` 为 `"//W3C//DTD HTML 4.01//EN"`，`systemId` 为 `"http://www.w3.org/TR/html4/loose"`。支持 DOM 2 的浏览器能够运行以下 JavaScript 代码：

```javascript
alert(document.doctype.publicId);
alert(document.doctype.systemId);
```

访问这些信息很少需要。`internalSubset` 属性访问包含在 doctype 中的额外定义：

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" 
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<!ELEMENT name (#PCDATA)>
```

对于这段代码，`document.doctype.internalSubset` 返回 `"<!ELEMENT name (#PCDATA)>"`。内部集在 HTML 中很少使用，但在 XML 中更为常见。

#### Document 的更改

`Document` 上唯一不相关的命名空间的新方法是 `importNode()`。该方法的目的是从另一个文档获取节点并将其导入到新文档中，以便将其添加到文档结构中。记住，每个节点都有一个 `ownerDocument` 属性指示它所属的文档。如果调用 `appendChild()` 等方法并传入一个不同 `ownerDocument` 的节点，则会发生错误。对另一个文档调用 `importNode()` 会返回一个属于相应文档的新节点。

`importNode()` 方法类似于元素上的 `cloneNode()` 方法。它接受两个参数：要克隆的节点以及一个指示是否也复制子节点的布尔值。结果是适用于文档的节点副本。这里有一个示例：

```javascript
var newNode = document.importNode(oldNode, true);   //导入节点及其所有子节点
document.body.appendChild(newNode);
```

该方法在 HTML 文档中并不常用；在 XML 文档中使用得更多（在第 18 章有进一步讨论）。

# 视图 (Views)

DOM Level 2 视图增加了一个名为 `defaultView` 的属性，它是指向拥有给定文档的窗口（或帧）的指针。视图规范没有提供关于何时可以使用其他视图的细节，因此这是新增的属性。`defaultView` 属性在所有浏览器中都支持（Internet Explorer 8 及更高版本除外）。有一个等效的属性名为 `parentWindow`，它在 Internet Explorer 8 及更高版本以及 Opera 中支持。因此，要确定文档的所属窗口，可以使用以下代码：

```javascript
var parentWindow = document.defaultView || document.parentWindow;
```

除了这一个方法和属性外，DOM Level 2 Core 中指定的 `document.implementation` 对象还发生了两处变化，形式为两个新方法：`createDocumentType()` 和 `createDocument()`。`createDocumentType()` 方法用于创建新的 `DocumentType` 节点，并接受三个参数：doctype 的名称、`publicId` 和 `systemId`。例如，以下代码创建了一个新的 HTML 4.01 Strict doctype：

```javascript
var doctype = document.implementation.createDocumentType("html",
                  "-//W3C//DTD HTML 4.01//EN",
                  "http://www.w3.org/TR/html4/strict.dtd");
```



现有文档的 `doctype` 无法更改，因此 `createDocumentType()` 仅在创建新文档时有用，这可以通过 `createDocument()` 完成。该方法接受三个参数：文档元素的 `namespaceURI`、文档元素的 `tagName` 以及新文档的 `doctype`。可以像示例所示创建一个新的空白 XML 文档：

```javascript
var doc = document.implementation.createDocument("", "root", null);
```

此代码创建了一个没有命名空间且文档元素为 `<root>` 且未指定 `doctype` 的新文档。要创建一个 XHTML 文档，可以使用以下代码：

```javascript
var doctype = document.implementation.createDocumentType("html",
                  "-//W3C//DTD XHTML 1.0 Strict//EN",
                  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd");

var doc = document.implementation.createDocument("http://www.w3.org/1999/xhtml",
              "html", doctype);
```

在这里，创建了一个具有适当命名空间和 `doctype` 的新 XHTML 文档。该文档只有一个文档元素 `<html>`；其他所有内容必须手动添加。

DOM Level 2 HTML 模块还向 `document.implementation` 添加了一个名为 `createHTMLDocument()` 的方法。该方法的目的是创建一个完整的 HTML 文档，包括 `<html>`、`<head>`、`<title>` 和 `<body>` 元素。该方法接受一个参数，即新创建文档的标题（放入 `<title>` 元素的字符串），并如下返回新的 HTML 文档：

![image](img/logo1.gif)

```javascript
var htmldoc = document.implementation.createHTMLDocument("New Doc");

alert(htmldoc.title);         //"New Doc"

alert(typeof htmldoc.body);   //"object"
```

`CreateHTMLDocumentExample.htm`

通过调用 `createHTMLDocument()` 创建的对象是 `HTMLDocument` 实例，因此包含了与之相关的所有属性和方法，包括 `title` 和 `body` 属性。此方法在 Internet Explorer 9+、Firefox 4+、Safari、Chrome 和 Opera 中支持。

# Node 的变化

`Node` 类型中唯一与命名空间相关的变化是增加了 `isSupported()` 方法。类似于 DOM Level 1 中引入的 `document.implementation` 上的 `hasFeature()` 方法，`isSupported()` 方法指示了节点可以的操作。此方法接受相同的两个参数：功能名称和功能版本。当功能已实现并能够被给定节点执行时，`isSupported()` 返回 `true`。以下是一个示例：

```javascript
if (document.body.isSupported("HTML", "2.0")){

    //执行只有使用 DOM Level 2 HTML 才能的操作

}
```

该方法的用处有限，并且面临着与 `hasFeature()` 类似的问题，即实现由自己决定对于每个功能返回 `true` 还是 `false`。能力检测是检测特定功能是否可用的更佳方法。

# DOM Level 3

DOM Level 3 引入了两个方法来帮助比较节点：`isSameNode()` 和 `isEqualNode()`。这两个方法都接受一个节点作为参数，如果该节点与引用节点相同或相等，则返回 `true`。当两个节点引用同一个对象时，它们是相同的（same）。当两个节点具有相同类型且属性相等（`nodeName`、`nodeValue` 等），并且它们的属性和 `childNodes` 属性等效（在相同位置包含等效值）时，它们是相等的（equal）。以下是一个示例：

```javascript
var div1 = document.createElement("div");

div1.setAttribute("class", "box");

var div2 = document.createElement("div");

div2.setAttribute("class", "box");

alert(div1.isSameNode(div1));    //true

alert(div1.isEqualNode(div2));   //true

alert(div1.isSameNode(div2));    //false
```

在这里，创建了两个具有相同属性的 `<div>` 元素。这两个元素彼此等效，但不是相同的。

DOM Level 3 还引入了为 DOM 节点附加数据的方法。`setUserData()` 方法为节点分配数据并接受三个参数：要设置的键、实际数据（可以是任何数据类型）以及一个处理函数。可以使用以下代码为节点分配数据：

```javascript
document.body.setUserData("name", function(){});
```

然后可以使用 `getUserData()` 并传入相同的键来获取信息，如下所示：

```javascript
var value = document.body.getUserData("name");
```

`setUserData()` 的处理函数会在数据的节点被克隆、删除或导入到另一个文档时被调用，并让你有机会决定这些情况下用户数据的处理方式。处理函数接受五个参数：指示操作类型的数字（1 表示克隆，2 表示导入，3 表示删除，4 表示命名）、数据键、数据值、源节点和目标节点。节点被删除时，源节点为 `null`，除非节点被克隆，否则目标节点为 `null`。你可以决定如何存储数据。以下是一个示例：

![image](img/logo1.gif)

```javascript
var div = document.createElement("div");

div.setUserData("name", "Nicholas", function(operation, key, value, src, dest){

    if (operation == 1){

        dest.setUserData(key, value, function(){});

    }

});

var newDiv = div.cloneNode(true);

alert(newDiv.getUserData("name"));    //"Nicholas"
```

`UserDataExample.htm`

# 帧（Frames）的变化

帧（Frames）和内联帧（iframes）分别由 `HTMLFrameElement` 和 `HTMLIFrameElement` 表示，它们在 DOM Level 2 HTML 中有了一个新属性 `contentDocument`。该属性包含指向代表帧内容的文档对象的指针。在此之前，无法直接通过元素检索文档对象；必须使用 `frames` 集合。可以使用该属性，如下例所示：

![image](img/logo1.gif)

```javascript
var iframe = document.getElementById("myIframe");

var iframeDoc = iframe.contentDocument;   //在 IE < 8 中不起作用
```

`IFrameElementExample.htm`

`contentDocument` 属性是 `Document` 的实例，可以像任何其他 HTML 文档一样使用，包括所有的属性和方法。该属性在 Opera、Firefox、Safari 和 Chrome 中均受支持。8 之前的 Internet Explorer 不支持 frame 上的 `contentDocument`，但支持一个名为 `contentWindow` 的属性，该属性返回 frame 的 `window` 对象，该对象包含一个 `document` 属性。因此，要在所有四个浏览器中访问 `iframe` 的文档对象，可以使用以下代码：

```javascript
var iframe = document.getElementById("myIframe");

var iframeDoc = iframe.contentDocument || iframe.contentWindow.document;
```

`IFrameElementExample2.htm`

`contentWindow` 属性在所有浏览器中均可用。

![image](img/pen.gif)

对 frame 或 iframe 文档对象的访问受跨域安全限制的限制。如果你尝试访问包含从不同域名、子域加载或使用不同协议的页面的 frame 文档对象，将会导致错误。

## 样式

样式在 HTML 中有三种定义方式：通过 `<link>` 元素引入外部样式表、使用 `<style>` 元素定义内联样式，以及使用 `style` 属性定义元素特定样式。DOM Level 2 样式为这三种样式机制提供了一个 API。你可以使用以下代码判断浏览器是否支持 DOM Level 2 CSS 能力：

```javascript
var supportsDOM2CSS = document.implementation.hasFeature("CSS", "2.0");

var supportsDOM2CSS2 = document.implementation.hasFeature("CSS2", "2.0");
```

## 访问元素样式

任何支持 `style` 属性的 HTML 元素在 JavaScript 中都暴露了一个 `style` 属性。`style` 对象是 `CSSStyleDeclaration` 的实例，包含了 HTML `style` 属性指定的所有样式信息，但不包含从引入或内联样式表中级联的样式信息。`style` 属性中指定的任何 CSS 属性都表示为 `style` 对象上的属性。由于 CSS 属性名使用横线命名法（使用横线分隔单词，例如 `background-image`），在 JavaScript 中运行时必须将其转换为驼峰命名（camel case）。下表列了一些常见的 CSS 属性以及在 `style` 对象上对应的属性名。

| CSS PROPERTY | JAVASCRIPT PROPERTY |
| --- | --- |
| `background-image` | `style.backgroundImage` |
| `color` | `style.color` |
| `display` | `style.display` |
| `font-family` | `style.fontFamily` |

在大多数情况下，属性名只需更改属性名的格式即可直接转换。唯一无法直接转换的 CSS 属性是 `float`。由于 `float` 是 JavaScript 中的保留字，因此不能作为属性名。DOM Level 2 样式规范规定，`style` 对象上对应的属性应该是 `cssFloat`，它在 Internet Explorer 9、Firefox、Safari、Opera 和 Chrome 中受支持。Internet Explorer 8 及更版本则使用 `styleFloat` 代替。

只要有有效的 DOM 元素引用，就可以随时使用 JavaScript 设置样式。以下是一些示例：

```javascript
var myDiv = document.getElementById("myDiv");

// 设置背景颜色

myDiv.style.backgroundColor = "red";

// 改变尺寸

myDiv.style.width = "100px";

myDiv.style.height = "200px";

// 分配边框

myDiv.style.border = "1px solid black";
```

当以此方式更改样式时，元素的显示会自动更新。

![image](img/pen.gif)

在标准模式下，所有测量值必须包含测量单位。在兼容模式（quirks mode）下，你可以将 `style.width` 设置为 `"20"`，它将假设你的意思是 `"20px"`；标准模式下，将 `style.width` 设置为 `"20"` 将忽略，因为没有单位。在实践中，最好始终包含测量单位。

`style` 属性中指定的样式也可以通过 `style` 对象获取。考虑以下 HTML：

```html
<div id="myDiv" style="background-color: blue; width: 10px; height: 25px"></div>
```

可以通过以下代码获取此元素样式属性的信息：

```javascript
alert(myDiv.style.backgroundColor);   // "blue"

alert(myDiv.style.width);             // "10px"

alert(myDiv.style.height);            // "25px"
```

如果元素上没有指定样式属性，`style` 对象可能包含一些默认值，但无法提供关于元素样式的任何准确信息。

## DOM 样式属性和方法

DOM Level 2 样式规范还在 `style` 对象上定义了几个属性和方法。这些属性和方法提供了元素样式属性内容的信息并允许更改。它们如下：

- `cssText` — 如前所述，提供了访问样式属性 CSS 代码的方法。
- `length` — 应用于元素的 CSS 属性数量。
- `parentRule` — 代表 CSS 信息的 `CSSRule` 对象。`CSSRule` 类型将在后面的章节中讨论。
- `getPropertyCSSValue(propertyName)` — 返回一个包含给定属性值的 `CSSValue` 对象。
- `getPropertyPriority(propertyName)` — 如果给定属性使用 `!important` 设置，则返回 `"important"`否则返回空字符串。
- `getPropertyValue(propertyName)` — 返回给定属性的字符串值。
- `item(index)` — 返回给定位置的 CSS 属性的名称。
- `removeProperty(propertyName)` — 从样式中移除指定的属性。
- `setProperty(propertyName, value, priority)` — 使用优先级（`"important"` 或空字符串）将给定属性设置为给定值。

`cssText` 属性允许访问样式的 CSS 代码。在读模式下使用时，`cssText` 返回浏览器对样式属性中 CSS 代码的内部表示。在写模式下使用时，赋值给 `cssText` 的值将覆盖整个样式，这意味着之前所有的样式信息都会丢失。例如，如果元素通过样式属性指定了边框，而你用不包含边框的规则覆盖 `cssText`，边框将从元素中移除。`cssText` 属性用法如下：

```javascript
myDiv.style.cssText = "width: 25px; height: 100px; background-color: green";

alert(myDiv.style.cssText);
```

设置 `cssText` 属性是更改样式最快的方法，因为所有更改都是同时应用的。

`length` 属性设计用于与 `item()` 方法配合使用，遍历元素上定义的 CSS 属性。通过这些属性，`style` 对象实际上变成了一个集合，可以使用中括号符号代替 `item()` 来获取给定位置的 CSS 属性名，如下例所示：

```javascript
for (var i=0, len=myDiv.style.length; i < len; i++){

    alert(myDiv.style[i]); // 或 myDiv.style.item(i)

}
```

使用中括号符号或 `item()`，你可以获取 CSS 属性名（`"background-color"`，而不是 `"backgroundColor"`）。该属性名随后可以使用 `getPropertyValue()` 来获取属性的实际值，如下例所示：

```javascript
var prop, value, i, len;

for (i=0, len=myDiv.style.length; i < len; i++){

    prop = myDiv.style[i]; // 或 myDiv.style.item(i)

    value = myDiv.style.getPropertyValue(prop);

    alert(prop + " : " + value);

}
```



`getPropertyValue()` 方法始终检索 CSS 属性值的字符串表示。如果你需要更多信息，`getPropertyCSSValue()` 会返回一个 `CSSValue` 对象，该对象包含两个属性：`cssText` 和 `cssValueType`。`cssText` 属性与 `getPropertyValue()` 返回的值相同。`cssValueType` 属性是一个数值常量，表示所代表的值的类型：`0` 表示继承值，`1` 表示原始值，`2` 表示列表，或 `3` 表示自定义值。以下代码输出了 CSS 属性值和值类型：

![image](img/logo1.gif)

```
var prop, value, i, len;

for (i=0, len=myDiv.style.length; i < len; i++){

    prop = myDiv.style[i];     //or myDiv.style.item(i)

    value = myDiv.style.getPropertyCSSValue(prop);

    alert(prop + " : " + value.cssText + " (" + value.cssValueType + ")");

}
```

`DOMStyleObjectExample.htm`

在实践中，`getPropertyCSSValue()` 的用性不如 `getPropertyValue()`。此方法在 Internet Explorer 9+、Safari 3+ 和 Chrome 中支持。Firefox 直到第 7 版本提供了该方法，但调用始终返回 `null`。

`removeProperty()` 方法用于从元素的样式中删除特定的 CSS 属性。使用此方法移除属性意味着该属性的任何默认样式（从其他样式表级联）将将被应用。例如，要移除在样式属性中设置的边框属性，可以使用以下代码：

```
myDiv.style.removeProperty("border");
```

当你不确定给定 CSS 属性的默认值时，此方法非常有帮助。只需删除该属性即可使用默认值。

![image](img/pen.gif)

除非另有说明，本节中的属性和方法在 Internet Explorer 9+、Firefox、Safari、Opera 9+ 和 Chrome 中支持。

### 计算样式 (Computed Styles)

`style` 对象提供了有关支持该属性元素样式属性的信息，但不包含任何从样式表级联并影响元素的样式信息。DOM Level 2 Style 扩展了 `document.defaultView` 以提供一个名为 `getComputedStyle()` 的方法。该方法接受两个参数：要获取计算样式的元素，以及一个伪元素字符串（例如 `:after`）。如果不需要伪元素信息，第二个参数可以为 `null`。`getComputedStyle()` 方法返回一个 `CSSStyleDeclaration` 对象（与 `style` 属性类型相同），其中包含元素的所有计算样式。考虑以下 HTML 页面：

![image](img/logo1.gif)

```
<!DOCTYPE html>

<html>

<head>

    <title>Computed Styles Example</title>

    <style type="text/css">

        #myDiv {

            background-color: blue;

            width: 100px;

            height: 200px;

        }

    </style>

</head>

<body>

    <div id="myDiv" style="background-color: red; border: 1px solid black"></</div>

</body>

</html>
```

`ComputedStylesExample.htm`

在此示例中，`<div>` 元素同时了来自内联样式表（`<style>` 元素）和样式属性的样式。`style` 对象拥有 `backgroundColor` 和 `border` 的值，但对于通过样式表规则应用的 `width` 和 `height` 则没有任何值。以下代码检索了元素的计算样式：

![image](img/logo1.gif)

```
var myDiv = document.getElementById("myDiv");

var computedStyle = document.defaultView.getComputedStyle(myDiv, null);

alert(computedStyle.backgroundColor);   //"red"

alert(computedStyle.width);             //"100px"

alert(computedStyle.height);            //"200px"

alert(computedStyle.border);            //"1px solid black" in some browsers
```

`ComputedStylesExample.htm`

当检索此元素的计算样式时，背景颜色报告为 "red"，宽度为 "100px"，高度为 "200px"。注意，背景颜色不是 "blue"，因为该样式在元素本身上被覆盖了。`border` 属性可能也也可能返回样式表中的精确边框规则（Opera 返回了它，但其他浏览器不返回）。这种不一致性源于浏览器解释组合属性（如 `border`）的方式，这些属性实际上设置了许多其他属性。当你设置 `border` 时，你实际上是在设置四个边框的边框宽度、颜色和样式（`border-left-width`、`border-top-color`、`border-bottom-style` 等）。因此，即使 `computedStyle.border` 在所有浏览器中可能不返回值，但 `computedStyle.borderLeftWidth` 会返回。

![image](img/pen.gif)

注意，尽管某些浏览器支持此功能，但值的表示方式可能不同。例如，Firefox 和 Safari 将所有颜色转换为 RGB 形式（例如红色的 `rgb(255,0,0)`），而 Opera 则将所有颜色转换为其十六进制表示（红色的 `#ff0000`）。在使用 `getComputedStyle()` 时，最好的办法始终在多个浏览器上测试你的功能。

Internet Explorer 不支持 `getComputedStyle()`，尽管它有一个相似的概念。每个具有 `style` 属性的元素都有 `currentStyle` 属性。`currentStyle` 属性是 `CSSStyleDeclaration` 的实例，包含了元素的所有计算样式。可以像示例所示检索样式：

```
var myDiv = document.getElementById("myDiv");

var computedStyle = myDiv.currentStyle;

alert(computedStyle.backgroundColor);   //"red"

alert(computedStyle.width);             //"100px"

alert(computedStyle.height);            //"200px"

alert(computedStyle.border);            //undefined
```

`IEComputedStyles.htm`

与 DOM 版本一样，边框样式在 Internet Explorer 中不返回，因为它是一个组合属性。

关于所有浏览器中计算样式的重要点是它是只读的；你无法在计算样式上更改 CSS 属性。此外，计算样式包含了内部样式信息，因此任何具有默认值的 CSS 属性都会体现在计算样式中。例如，`visibility` 属性在所有浏览器中都有默认值，但该值随实现而异。某些浏览器默认将 `visibility` 设置为 "visible"，而其他则为 "inherit"。你不能依赖 CSS 属性的默认值跨浏览器是相同的。如果你需要元素具有特定的默认值，你应该在样式表中手动指定。

### 使用样式表 (Working with Style Sheets)

`CSSStyleSheet` 类型表示使用 `<link>` 元素包含或在 `<style>` 元素定义的 CSS 样式表。注意元素本身分别由 `HTMLLinkElement` 和 `HTMLStyleElement` 类型表示。`CSSStyleSheet` 类型足够通用，可以表示在 HTML 中如何定义的样式表。此外，特定的元素类型允许修改 HTML 属性，而 `CSSStyleSheet` 对象除一个属性外，都是只读接口。可以使用以下代码判断浏览器是否支持 DOM Level 2 样式表：

```
var supportsDOM2StyleSheets = 

                   document.implementation.hasFeature("StyleSheets", "2.0");
```

`CSSStyleSheet` 类型继承自 `StyleSheet`，后者可以作为基类定义非 CSS 样式表。以下属性继承自 `StyleSheet`：

*   `disabled` — 一个布尔值，表示样式表是否已禁用。此属性是可读可写的，因此将其值设置为 `true` 将禁用样式表。
*   `media` — 此样式表支持的媒体类型集合。与所有 DOM 集合一样，该集合具有 `length` 属性和 `item()` 方法。像其他 DOM 集合一样，你可以使用括号表示法访问集合中的特定项目。空列表表示该样式表适用于所有媒体。在 Internet Explorer 8 及更早版本中，`media` 是反映 `<link>` 或 `<style>` 元素 `media` 属性的字符串。
*   `ownerNode` — 指向拥有样式表的节点，在 HTML 中可以是 `<link>` 或 `<style>` 元素（XML 中可以是一个处理指令）。如果样式表通过 `@import` 包含在另一个样式表中，则该属性为 `null`。Internet Explorer 8 及更早版本不支持此属性。
*   `parentStyleSheet` — 当通过 `@import` 包含样式表时，此属性指向导入该样式表的样式表指针。
*   `title` — `ownerNode` 上的 `title` 属性值。
*   `type` — 表示样式表类型的字符串。对于 CSS 样式表，此值值为 `"text/css"`。

除 `disabled` 之外，其余属性均为只读。`CSSStyleSheet` 类型支持所有属性以及以下属性和方法：

*   `cssRules` — 样式表中包含的规则集合。Internet Explorer 8 及更早版本不支持此属性，但有一个名为 `rules` 的可比属性。Internet Explorer 9 同时支持 `cssRules` 和 `rules`。
*   `ownerRule` — 如果样式表是通过 `@import` 包含的，则此属性指向代表该导入的规则；否则为 `null`。Internet Explorer 不支持此属性。
*   `deleteRule(index)` — 删除 `cssRules` 集合中指定位置的规则。Internet Explorer 8 及更早版本不支持此方法，但它有一个名为 `removeRule()` 的类似方法。Internet Explorer 9 同时支持 `deleteRule()` 和 `removeRule()`。
*   `insertRule(rule, index)` — 在 `cssRules` 集合的指定位置插入给定的字符串规则。Internet Explorer 8 及更早版本不支持此方法，但有一个名为 `addRule()` 的类似方法。Internet Explorer 9 同时支持 `insertRule()` 和 `addRule()`。

文档上可用的样式表由 `document.styleSheets` 集合表示。可以使用 `length` 属性获取文档上的样式表数量，并可以使用 `item()` 方法或括号表示法访问每个单独的样式表。示例下：

![image](img/logo1.gif)

```
var sheet = null;

for (var i=0, len=document.styleSheets.length; i < len; i++){

    sheet = document.styleSheets[i];

    alert(sheet.href);

}
```

`StyleSheetsExample.htm`

此代码输出文档中使用的每个样式表的 `href` 属性（`<style>` 元素没有 `href`）。

`document.styleSheets` 返回的样式表随浏览器而异。所有浏览器都包含 `<style>` 元素和 `rel` 设置为 `"stylesheet"` 的 `<link>` 元素。Internet Explorer 和 Opera 还包含 `rel` 设置为 `"alternate stylesheet"` 的 `<link>` 元素。

也可以直接从 `<link>` 或 `<style>` 元素获取 `CSSStyleSheet` 对象。DOM 规定了一个名为 `sheet` 的属性，其中包含 `CSSStyleSheet` 对象，除 Internet Explorer 以外的所有浏览器都支持该属性。Internet Explorer 支持一个名为 `styleSheet` 的属性，实现相同的功能。为了跨浏览器获取样式表对象，可以使用以下代码：

```
function getStyleSheet(element){

    return element.sheet || element.styleSheet;

}

//获取第一个 <link/> 元素的样式表

var link = document.getElementsByTagName("link")[0];

var sheet = getStyleSheet(link);
```

`StyleSheetsExample2.htm`

从 `getStyleSheet()` 返回的对象与 `document.styleSheets` 集合中存在的对象是同一个。

### CSS 规则

`CSSRule` 对象代表样式表中的每条规则。`CSSRule` 类型实际上是其他几种类型继承的基类型，但最常用的是 `CSSStyleRule`，它代表样式信息（其他规则包括 `@import`、`@font-face`、`@page` 和 `@charset`，尽管这些规则很少通过脚本访问）。`CSSStyleRule` 对象上可用以下属性：

*   `cssText` — 返回整个规则的文本。由于浏览器内部处理样式表的方式，此文本可能与样式表中的实际文本不同；Safari 总是将所有内容转换为小写。Internet Explorer 不支持此属性。
*   `parentRule` — 如果此规则被导入，则其为导入规则；否则为 `null`。Internet Explorer 不支持此属性。
*   `parentStyleSheet` — 该规则所属的样式表。Internet Explorer 不支持此属性。
*   `selectorText` — 返回规则的选择器文本。由于浏览器内部处理样式表的方式，此文本可能与样式表中的实际文本不同。此属性在 Firefox、Safari、Chrome 和 Internet Explorer 中为只读（在 IE 中会抛出错误）。Opera 允许更改 `selectorText`。
*   `style` — 一个 `CSSStyleDeclaration` 对象，允许设置和获取规则的特定样式值。
*   `type` — 表示规则类型的常量。对于样式规则，此值始终为 `1`。Internet Explorer 不支持此属性。

最常用的属性是 `cssText`、`selectorText` 和 `style`。`cssText` 属性与 `style.cssText` 相似但不完全相同。前者包含选择器文本和周围的大括号；后者仅包含样式信息。此外，`cssText` 是只读的，而 `style.cssText` 可以被覆盖。

大多数情况下，`style` 属性就是操作样式规则所需的。该对象可以像元素上的对象一样读取或更改样式信息。考虑以下 CSS 规则：

![image](img/logo1.gif)

```css
div.box {

    background-color: blue;

    width: 100px;

    height: 200px;

}
```

`CSSRulesExample.htm`

假设此规则位于第一个样式表中且唯一的样式，可以使用以下代码检索其所有信息：

![image](img/logo1.gif)

```
var sheet = document.styleSheets[0];

var rules = sheet.cssRules || sheet.rules;    //获取规则列表

var rule = rules[0];                          //获取第一条规则

alert(rule.selectorText);                     //"div.box"

alert(rule.style.cssText);                    //完整的 CSS 代码

alert(rule.style.backgroundColor);            //"blue"
```



`alert(rule.style.width);` //"100px"

`alert(rule.style.height);` //"200px"

### 创建规则

使用这种技术，可以像确定元素的内联样式信息一样，确定规则相关的样式信息。与元素一样，也可以更改样式信息，如下例：

```
var sheet = document.styleSheets[0];
var rules = sheet.cssRules || sheet.rules;    //获取规则列表
var rule = rules[0];                          //获取第一条规则
rule.style.backgroundColor = "red"
```

`CSSRulesExample.htm`

注意，通过这种方式更改规则会影响页面上所有适用于规则的元素。如果有两个具有 `box` 类的 `<div>` 元素，它们都会受到此更改的影响。

DOM 规定使用 `insertRule()` 方法向现有样式表添加新规则。该方法接受两个参数：规则的文本和插入规则的索引。示例如下：

```
sheet.insertRule("body { background-color: silver }", 0);    //DOM 方法
```

此示例插入了一个更改文档背景颜色的规则。该规则作为样式表中的第一条规则（位置 0）插入——规则顺序对于决定规则如何级联到文档至关重要。`insertRule()` 方法在 Internet Explorer 9+ 以及所有现代版本的 Firefox、Safari、Opera 和 Chrome 中均受支持。

Internet Explorer 8 及更早版本有一个名为 `addRule()` 的类似方法，它接受两个参数：选择器文本和 CSS 样式信息。可选的第三个参数指定要插入规则的位置。上一个示例的 Internet Explorer 等效写法如下：

```
sheet.addRule("body", "background-color: silver", 0);        //IE 专用
```

该方法的文档表明，你可以使用 `addRule()` 添加多达 4,095 条样式规则。任何额外的调用都将导致错误。

要以跨浏览器的方式向样式表添加规则，可以使用以下方法。它接受四个参数：要添加规则的样式表，随后是与 `addRule()` 相同的三个参数，如下例所示：

![image](img/logo1.gif)

```
function insertRule(sheet, selectorText, cssText, position){
    if (sheet.insertRule){
        sheet.insertRule(selectorText + "{" + cssText + "}", position);
    } else if (sheet.addRule){
        sheet.addRule(selectorText, cssText, position);
    }
}
```

`CSSRulesExample2.htm`

随后可以通过以下方式调用此函数：

```
insertRule(document.styleSheets[0], "body", "background-color: silver", 0); 
```

虽然可以通过这种方式添加规则，但当需要添加的规则很多时，操作会很快变得繁琐。在这种情况下，最好使用第 10 章中讨论的动态样式加载技术。

### 删除规则

从样式表中删除规则的 DOM 方法是 `deleteRule()`，它接受一个参数：要删除规则的索引。要删除样式表中的第一条规则，可以使用以下代码：

```
sheet.deleteRule(0);    //DOM 方法
```

Internet Explorer 8 及更早版本支持名为 `removeRule()` 的方法，其用法相同，所示：

```
sheet.removeRule(0);    //IE 专用
```

以下函数以跨浏览器的方式处理规则删除。第一个参数是要执行操作的样式表，第二个参数是待删除的索引，如下例：

```
function deleteRule(sheet, index){
    if (sheet.deleteRule){
        sheet.deleteRule(index);
    } else if (sheet.removeRule){
        sheet.removeRule(index);
    }
}
```

`CSSRulesExample2.htm`

该函数可以使用以下方式使用：

```
deleteRule(document.styleSheets[0], 0); 
```

与添加规则一样，删除规则在 Web 开发中并不是常见做法，应该谨慎使用，因为 CSS 的级联效应可能会受到影响。

### 元素尺寸

以下属性和方法不属于 DOM Level 2 样式规范，但与 HTML 元素的样式相关。DOM 并没有描述确定页面上元素实际尺寸的方法。Internet Explorer 最初引入了几个属性来向开发者公开尺寸信息。这些属性现在已已整合到所有主流浏览器中。

#### 偏移尺寸 (Offset Dimensions)

第一组属性处理偏移尺寸，它包含了元素在屏幕上占据的所有视觉空间。元素在页面上的视觉空间由其高度和宽度组成，包括所有内边距、滚动条和边框（但不包括外边距）。以下四个属性用于获取偏移尺寸：

* `offsetHeight` — 元素占据的垂直空间（像素为单位），包括其高度、水平滚动条的高度（如果可见）、顶部边框的高度和底部边框的高度。
* `offsetLeft` — 元素外部左边框与包含元素内部左边框之间的像素数。
* `offsetTop` — 元素外部顶部边框与包含元素内部顶部边框之间的像素数。
* `offsetWidth` — 元素占据的水平空间（像素为单位），包括其宽度、垂直滚动条的宽度（如果可见）、左边框宽度和右边框宽度。

`offsetLeft` 和 `offsetTop` 属性相对于包含元素，该包含元素存储在 `offsetParent` 属性中。`offsetParent` 不一定等于 `parentNode`。例如，`<td>` 元素的 `offsetParent` 是其祖先的 `<table>` 元素，因为 `<table>` 是层级中提供尺寸的第一个元素。图 12-1 展示了这些属性所代表的各种尺寸。

图 12-1

![image](img/f402-01.jpg)

元素在页面上的偏移量可以通过获取 `offsetLeft` 和 `offsetTop` 属性，并将它们加到 `offsetParent` 的相同属性上来大致确定，一直逐层向上直到直到到达根元素。这是一个示例：

![image](img/logo1.gif)

```
function getElementLeft(element){
    var actualLeft = element.offsetLeft;
    var current = element.offsetParent;
    while (current !== null){        
        actualLeft += current.offsetLeft;
        current = current.offsetParent;
    }
    return actualLeft;
}

function getElementTop(element){
    var actualTop = element.offsetTop;
    var current = element.offsetParent;
    while (current !== null){        
        actualTop += current.offsetTop;
        current = current.offsetParent;
    }
    return actualTop;
}
```

`OffsetDimensionsExample.htm`

这两个函数通过 `offsetParent` 属性在 DOM 层级中爬升，并累加每一层的偏移属性。对于使用基于 CSS 布局的简单页面布局，这些函数非常准确。对于使用表格和 iframe 的页面布局，由于这些元素的实现方式不同，返回的值在跨浏览器方面的准确性较低。通常，所有仅包含在 `<div>` 元素中的元素都有 `<body>` 作为它们的 `offsetParent`，因此 `getElementLeft()` 和 `getElementTop()` 返回的值与 `offsetLeft` 和 `offsetTop` 相同。

![image](img/pen.gif)

所有的偏移尺寸属性都是只读的，并且在每次访问时都会重新计算。因此，你应该尝试避免多次调用这些任何属性；相反，将需要的值存储在局部变量中以避免性能损失。

#### 客户端尺寸 (Client Dimensions)

元素的客户端尺寸包含了元素内容及其内边距占据的空间。与客户端尺寸相关的属性只有：`clientWidth` 和 `clientHeight`。`clientWidth` 属性是内容区域的宽度加上左右内边距的宽度。`clientHeight` 属性是内容区域的高度加上顶部底部内边距的高度。图 12-2 展示了这些属性。

图 12-2

![image](img/f403-01.jpg)

客户端尺寸字面上意思是元素内部的空间，因此不计算滚动条占据的空间。这些属性最用途是确定浏览器视口大小，如第 8 章所述。这是通过使用 `document.documentElement` 或 `document.body`（Internet Explorer 6 及更早版本）的 `clientWidth` 和 `clientHeight` 来实现的，如下所示：

```javascript
function getViewport(){
    if (document.compatMode == "BackCompat"){
        return {
            width: document.body.clientWidth,
            height: document.body.clientHeight
        };        
    } else {
        return {
            width: document.documentElement.clientWidth,
            height: document.documentElement.clientHeight
        };        
    }
}
```

该函数通过检查 `document.compatMode` 属性来判断浏览器是否运行在兼容模式（quirks mode）下。Internet Explorer 8+、Chrome、Safari、Opera 和 Firefox 大多数运行在标准模式，因此它们也会执行 `else` 语句。该函数返回一个包含两个属性的对象：`width` 和 `height`。这些属性代表视口（`<html>` 或 `<body>` 元素）的尺寸。

![image](img/pen.gif)

偏移尺寸（offset dimensions）一样，客户端尺寸（client dimensions）是只读的，并且每次访问时都会重新计算。

### 滚动尺寸 (Scroll Dimensions)

最后一组尺寸是滚动尺寸，它们提供了关于内容滚动的元素的信息。某些元素（例如 `<html>` 元素）在不需要任何额外代码的情况下会自动滚动，而其他元素可以通过 CSS 的 `overflow` 属性来实现滚动。这四个滚动尺寸属性如下：

* `scrollHeight` — 如果不存在滚动条，内容的总高度。
* `scrollLeft` — 内容区域左侧隐藏的像素数。该属性可以被设置以更改元素的滚动位置。
* `scrollTop` — 内容区域顶部隐藏的像素数。该属性可以被设置以更改元素的滚动位置。
* `scrollWidth` — 如果不存在滚动条，内容的总宽度。

图 12-3 阐释了这些属性。

图 12-3

![image](img/f405-01.jpg)

`scrollWidth` 和 `scrollHeight` 属性对于确定给定元素内内容的实际尺寸有用。例如，`<html>` 元素被认为是 Web 浏览器中滚动视口的元素（在 Internet Explorer 5.5 及之前的版本中，`<body>` 元素是滚动视口的元素）。因此，具有垂直滚动条的整个网页的高度为 `document.documentElement.scrollHeight`。

对于不进行滚动的文档，`scrollWidth`、`scrollHeight` 与 `clientWidth` 和 `clientHeight` 之间的关系并不明确。在 `document.documentElement` 上检查这些属性会导致跨浏览器结果不一致，如下所示：

* Firefox 保持这些属性相等，但其尺寸与文档内容的实际大小有关，而不是视口的大小。
* Opera、Safari 3.1 及更高版本以及 Chrome 保持这些属性不同，其中 `scrollWidth` 和 `scrollHeight` 等于视口大小，而 `clientWidth` 和 `clientHeight` 等于文档内容。
* Internet Explorer（标准模式下）保持这些属性不同，其中 `scrollWidth` 和 `scrollHeight` 等于文档内容的尺寸，而 `clientWidth` 和 `clientHeight` 等于视口大小。

在尝试确定文档的总高度（包括基于视口的最小高度）时，你必须取 `scrollWidth/clientWidth` 和 `scrollHeight/clientHeight` 的最大值，以确保跨浏览器结果的准确性。这里是一个示例：

```javascript
var docHeight = Math.max(document.documentElement.scrollHeight,
                         document.documentElement.clientHeight);
var docWidth = Math.max(document.documentElement.scrollWidth,
                        document.documentElement.clientWidth);
```

注意，对于兼容模式下的 Internet Explorer，你需要在 `document.body` 上使用相同的测量值，而不是 `document.documentElement`。

`scrollLeft` 和 `scrollTop` 属性既可以确定当前的滚动设置，也可以用于设置它们。当元素没有滚动时，`scrollLeft` 和 `scrollTop` 的值均为 0。如果元素发生了垂直滚动，`scrollTop` 大于 0，表示顶部隐藏的内容；如果元素发生了水平滚动，`scrollLeft` 大于 0，表示左侧隐藏的内容。以下代码显示了如何将元素置到顶部：

```javascript
function scrollToTop(element){
    if (element.scrollTop != 0){
        element.scrollTop = 0;
    }
}
```

### 元素尺寸 (Determining Dimensions)

Internet Explorer、Firefox 3+、Safari 4+、Opera 9+ 以及 Chrome 提供了一个名为 `getBoundingClientRect()` 的方法，它返回一个包含 `left`、`top`、`right` 和 `bottom` 属性的对象。这些属性相对于视口的位置。Internet Explorer 8 及之前的版本将左上角视为 (2,2)，而其他实现方式则使用 (0,0) 作为起始点。这里是一个示例：

![image](img/logo.gif)

```javascript
function getBoundingClientRect(element){
    if (typeof arguments.callee.offset != "number"){
        var scrollTop = document.documentElement.scrollTop;
        var temp = document.createElement("div");
        temp.style.cssText = "position:absolute;left:0;top:0;";
        document.body.appendChild(temp);
        arguments.callee.offset = temp.getBoundingClientRect().top - scrollTop;
        document.body.removeChild(temp);
        temp = null;
    }
    var rect = element.getBoundingClientRect();
    var offset = arguments.callee.offset;
    return {
        left: rect.left + offset,
        right: rect.right + offset,
        top: rect.top + offset,



`bottom: rect.bottom + offset`

};

}

```



```

`function getBoundingClientRect(element)`{

    `var scrollTop = document.documentElement.scrollTop`;

    `var scrollLeft = document.documentElement.scrollLeft`;

    if (`element.getBoundingClientRect`){

        if (typeof `arguments.callee.offset` != "number"){

            `var temp = document.createElement("div")`;

            `temp.style.cssText = "position:absolute;left:0;top:0;"`;

            `document.body.appendChild(temp)`;

            `arguments.callee.offset = -temp.getBoundingClientRect().top - 

                                      scrollTop`;

            `document.body.removeChild(temp)`;

            `temp = null`;

        }

        `var rect = element.getBoundingClientRect()`;

        `var offset = arguments.callee.offset`;

        return {

            `left: rect.left + offset`,

            `right: rect.right + offset`,

            `top: rect.top + offset`,

            `bottom: rect.bottom + offset`

        };

    } else {

        `var actualLeft = getElementLeft(element)`;

        `var actualTop = getElementTop(element)`;

        return {

            `left: actualLeft - scrollLeft`,

            `right: actualLeft + element.offsetWidth - scrollLeft`,

            `top: actualTop - scrollTop`,

            `bottom: actualTop + element.offsetHeight - scrollTop`

        }

    }

}

```

`GetBoundingClientRectExample.htm`

此函数在原生 `getBoundingClientRect()` 方法可用时会使用它，在不可用时默认为计算尺寸。在某些情况下，这些值在浏览器中会有所不同，例如使用表格或滚动元素的布局。

![image](img/pen.gif)

由于使用了 `arguments.callee`，该方法在严格模式（strict mode）下无法工作。

## 遍历

DOM Level 2 遍历（Traversal）和范围（Range）模块定义了两种辅助顺序遍历 DOM 结构的类型。这两种类型 `NodeIterator` 和 `TreeWalker` 根据给定的起始点对 DOM 结构进行深度优先遍历。这些对象类型在符合 DOM 标准的浏览器可用，包括 Internet Explorer 9+、`Firefox`、`Safari`、`Opera` 和 `Chrome`。Internet Explorer 8 及更早版本不支持 DOM 遍历。你可以使用以下代码测试对 DOM Level 2 遍历的支持情况：

```

var supportsTraversals = document.implementation.hasFeature("Traversal", "2.0");

var supportsNodeIterator = (typeof document.createNodeIterator == "function");

var supportsTreeWalker = (typeof document.createTreeWalker == "function");

```

如前所述，DOM 遍历是对 DOM 结构的深度优先遍历，允许在至少两个方向上移动（取决于所使用的类型）。遍历根于给定的节点，并且无法到达该根节点更高的 DOM 树位置。考虑以下 HTML 页面：

```html

<!DOCTYPE html>

<html>

    <head>

        <title>Example</title>

    </head>

    <body>

        <p><b>Hello</b> world!</p>

    </body>

</html>

```

该页面评估结果为 图 12-4 所示的 DOM 树。

FIGURE 12-4

![image](img/f409-01.jpg)

任何节点都可以作为遍历的根。假设，`<body>` 元素是遍历的根。那么遍历可以访问 `<p>` 元素、`<b>` 元素以及 `<body>` 的后代的两个文本节点；然而，遍历永远无法到达 `<html>` 元素、`<head>` 元素或不在 `<body>` 元素子树中的任何节点。另一方面，根为 `document` 的遍历可以访问 `document` 中的所有节点。图 12-5 描述了以 `document` 为根的 DOM 树的深度优先遍历。

FIGURE 12-5

![image](img/f409-02.jpg)

从 `document` 开始顺序移动，第一个访问的节点是 `document`，最后一个访问的节点是包含 " world!" 的文本节点。从文档末尾最后一个文本节点开始，遍历可以反向回到树上。在这种情况下，第一个访问的节点是包含 " world!" 的文本节点，最后一个访问的是 `document` 节点本身。`NodeIterator` 和 `TreeWalker` 都以这种方式进行遍历。

## NodeIterator

`NodeIterator` 类型是两者中较简单的，可以使用 `document.createNodeIterator()` 方法创建新实例。该方法接受以下四个参数：

* `root` — 你想要从树中的哪个节点开始搜索。
* `whatToShow` — 一个用于指示应该访问哪些节点的数字代码。
* `filter` — 一个 `NodeFilter` 对象或函数，指示特定节点是否应该被接受或拒绝。
* `entityReferenceExpansion` — 一个布尔值，指示是否应该展开实体引用。这在 HTML 页面中没有影响，因为实体引用永远不会被展开。

`whatToShow` 参数是一个位掩码，通过应用一个或多个过滤器来决定访问哪些节点。此参数的可能值作为常量包含在 `NodeFilter` 类型中：

* `NodeFilter.SHOW_ALL` — 显示所有节点类型。
* `NodeFilter.SHOW_ELEMENT` — 显示元素节点。
* `NodeFilter.SHOW_ATTRIBUTE` — 显示属性节点。这实际上无法使用，因为由于 DOM 结构的限制。
* `NodeFilter.SHOW_TEXT` — 显示文本节点。
* `NodeFilter.SHOW_CDATA_SECTION` — 显示 CDATA 节点。
* `NodeFilter.SHOW_ENTITY_REFERENCE` — 显示实体引用节点。
* `NodeFilter.SHOW_ENTITY` — 显示实体节点。
* `NodeFilter.SHOW_PROCESSING_INSTRUCTION` — 显示处理指令节点。
* `NodeFilter.SHOW_COMMENT` — 显示注释节点。
* `NodeFilter.SHOW_DOCUMENT` — 显示文档节点。
* `NodeFilter.SHOW_DOCUMENT_TYPE` — 显示文档类型节点。
* `NodeFilter.SHOW_DOCUMENT_FRAGMENT` — 显示文档碎片节点。
* `NodeFilter.SHOW_NOTATION` — 显示符号节点。

除了 `NodeFilter.SHOW_ALL` 之外，你可以使用位或运算符组合多个选项，如下例所示：

```

var whatToShow = NodeFilter.SHOW_ELEMENT | NodeFilter.SHOW_TEXT;

```

`createNodeIterator()` 的 `filter` 参数可以指定自定义的 `NodeFilter` 对象或过滤器函数。`NodeFilter` 对象只有一个方法 `acceptNode()`，如果给节点应该被访问则返回 `NodeFilter.FILTER_ACCEPT`，如果不应该被访问则返回 `NodeFilter.FILTER_SKIP`。由于 `NodeFilter` 是一个抽象类型，无法创建它的实例。相反，只需创建一个带有 `acceptNode()` 方法的对象并将其传递给 `createNodeIterator()`。以下代码接受 `<p>` 元素：

```javascript

var filter = {

    acceptNode: function(node){

        return node.tagName.toLowerCase() == "p" ? 

               NodeFilter.FILTER_ACCEPT :

               NodeFilter.FILTER_SKIP;

    }

};

var iterator = document.createNodeIterator(root, NodeFilter.SHOW_ELEMENT, 

                   filter, false);

```

第三参数也可以是采用 `acceptNode()` 方法形式的函数，如下所示：

```javascript

var filter = function(node){

        return node.tagName.toLowerCase() == "p" ? 

               NodeFilter.FILTER_ACCEPT :

               NodeFilter.FILTER_SKIP;

};

var iterator = document.createNodeIterator(root, NodeFilter.SHOW_ELEMENT, 

                   filter, false);

```

通常，这是在 JavaScript 中使用的形式，因为它更简单且与 JavaScript 的其他部分工作一致。如果不需要过滤器，应将第三参数设置为 `null`。

要创建一个访问所有节点类型的简单 `NodeIterator`，请使用以下代码：

```javascript

var iterator = document.createNodeIterator(document, NodeFilter.SHOW_ALL, 

                   null, false);

```



`NodeIterator` 的两个主要方法是 `nextNode()` 和 `previousNode()`。`nextNode()` 方法在 DOM 子树的深度优先遍历中向前移动一步，而 `previousNode()` 则在遍历中向后移动一步。当 `NodeIterator` 首次创建时，内部指针指向根节点，因此第一次调用 `nextNode()` 会返回根节点。当遍历到达 DOM 子树的最后一个节点时，`nextNode()` 返回 `null`。`previousNode()` 方法的工作原理类似。当遍历到达 DOM 子树的最后一个节点时，在 `previousNode()` 返回遍历的根节点之后，它将将返回 `null`。

考虑以下 HTML 片段：

![image](img/logo1.gif)

```html

<div id="div1">

    <p><b>Hello</b> world!</p>

    <ul>

        <li>List item 1</li>

        <li>List item 2</li>

        <li>List item 3</li>

    </ul>

</div>

```

### NodeIteratorExample1.htm

假设你想遍历 `<div>` 元素内部的所有元素。可以使用以下代码实现：

```javascript

var div = document.getElementById("div1");

var iterator = document.createNodeIterator(div, NodeFilter.SHOW_ELEMENT, 

                   null, false);

var node = iterator.nextNode();

while (node !== null) {

    alert(node.tagName);         //输出标签名

    node = iterator.nextNode();

}

```

NodeIteratorExample1.htm

在此示例中，第一次调用 `nextNode()` 返回 `<p>` 元素。由于 `nextNode()` 在到达 DOM 子树末尾时会返回 `null`，因此 `while` 循环会在每次循环调用 `nextNode()` 时检查是否返回了 `null`。当执行此代码时，将显示带有以下标签名的框：

```

DIV

P

B

UL

LI

LI

LI

```

也许这些信息太多了，你实际上只想返回遍历中出现的 `<li>` 元素。可以通过过滤器来实现，如下例所示：

```javascript

var div = document.getElementById("div1");

var filter = function(node){

    return node.tagName.toLowerCase() == "li" ? 

        NodeFilter.FILTER_ACCEPT :

        NodeFilter.FILTER_SKIP;

};

var iterator = document.createNodeIterator(div, NodeFilter.SHOW_ELEMENT, 

                   filter, false);

var node = iterator.nextNode();

while (node !== null) {

    alert(node.tagName);         //输出标签名

    node = iterator.nextNode();

}

```

NodeIteratorExample2.htm

在此示例中，迭代器将仅返回 `<li>` 元素。

`nextNode()` 和 `previousNode()` 方法通过 DOM 结构中的 `NodeIterator` 内部指针工作，因此结构的变化会反映在遍历中。

![image](img/pen.gif)

3.5 之前的 Firefox 版本没有实现 `createNodeIterator()` 方法，但正如下一节讨论的，它们支持 `createTreeWalker()`。

### TreeWalker

`TreeWalker` 是 `NodeIterator` 的高级版本。它具有相同的功能，包括 `nextNode()` 和 `previousNode()`，并增加了以下方法以便在不同的方向遍历 DOM 结构：

- `parentNode()` — 移动到当前节点的父节点。
- `firstChild()` — 移动到当前节点的第一个子节点。
- `lastChild()` — 移动到当前节点的最后一个子节点。
- `nextSibling()` — 移动到当前节点的下一个兄弟节点。
- `previousSibling()` — 移动到当前节点的上一个兄弟节点。

`TreeWalker` 对象使用 `document.createTreeWalker()` 方法创建，该方法接受与 `document.createNodeIterator()` 相同的三个参数：开始遍历的根节点、要显示的节点类型、过滤器，以及一个指示是否应展开实体引用的布尔值。由于这些相似性，`TreeWalker` 始终可以替代 `NodeIterator`，如下例：

![image](img/logo1.gif)

```javascript

var div = document.getElementById("div1");

var filter = function(node){

    return node.tagName.toLowerCase() == "li" ? 

        NodeFilter.FILTER_ACCEPT :

        NodeFilter.FILTER_SKIP;

};

var walker = document.createTreeWalker(div, NodeFilter.SHOW_ELEMENT, 

                   filter, false);

var node = iterator.nextNode();



`while (node !== null) {`

```
    alert(node.tagName);         //输出标签名

    node = iterator.nextNode();
}
```

`TreeWalkerExample1.htm`

一个区别在于过滤器可以返回的值。除了 `NodeFilter.FILTER_ACCEPT` 和 `NodeFilter.FILTER_SKIP` 之外，还有 `NodeFilter.FILTER_REJECT`。当与 `NodeIterator` 对象一起使用时，`NodeFilter.FILTER_SKIP` 和 `NodeFilter.FILTER_REJECT` 的作用相同：它们都会跳过该节点。当与 `TreeWalker` 对象一起使用时，`NodeFilter.FILTER_SKIP` 跳过该节点并继续子树中的下一个节点，而 `NodeFilter.FILTER_REJECT` 则会跳过该节点及其整个子树。例如，将上一个示例中的过滤器改为返回 `NodeFilter.FILTER_REJECT` 而不是 `NodeFilter.FILTER_SKIP` 将导致没有任何节点被访问。这是因为返回的元素是 `<div>`，它的标签名不是 "li"，因此返回了 `NodeFilter.FILTER_REJECT`，这意味着整个子树都应该跳过。由于 `<div>` 元素是根节点，这意味着遍历停止在 `<li>`。

当然，`TreeWalker` 的真正威力在于它可以在 DOM 中移动。与其指定过滤器，可以使用 `firstChild()` 进行导航，如下所示：

![image](img/pen.gif)

```javascript
var div = document.getElementById("div1");

var walker = document.createTreeWalker(div, NodeFilter.SHOW_ELEMENT, null, false);

var node = walker.firstChild(); //到 <p>

while (node !== null) {

    alert(node.tagName);

    node = walker.nextSibling();
}
```

`TreeWalker2.htm`

`TreeWalker` 类型还具有名为 `currentNode` 的属性，用于指示通过任何遍历方法最后返回的节点。该属性也可以设置，以更改遍历从哪里继续，如下例所示：

```javascript
var node = walker.nextNode();

alert(node === walker.currentNode);  //true

walker.currentNode = document.body;  //从这里开始
```

如果浏览器支持，可以使用 `createRange()` 创建一个 DOM 范围（range），所示：

```javascript
var range = document.createRange();
```

与节点（nodes）类似，新创建的范围直接与其创建的文档绑定，不能在其他文档中使用。随后，可以使用此范围在后台选择文档的特定部分。一旦创建了范围并设置了其位置，就可以对范围内的内容执行许多不同的操作，从而对底层的 DOM 树进行更细粒度的操作。

每个范围都由 `Range` 类型的实例表示，该类型具有多个属性和方法。以下属性提供了范围在文档中位置的信息：

- `startContainer` — 范围开始的节点（选择内容中第一个节点的父节点）。
- `startOffset` — 范围开始在 `startContainer` 内的偏移量。如果 `startContainer` 是文本节点、注释节点或 CData 节点，则 `startOffset` 是范围开始前跳过的字符数；否则，该偏移量是范围内第一个子节点的索引。
- `endContainer` — 范围结束的节点（选择内容中最后一个节点的父节点）。
- `endOffset` — 范围结束在 `endContainer` 内的偏移量（遵循与 `startOffset` 相同的规则）。
- `commonAncestorContainer` — 文档中同时 `startContainer` 和 `endContainer` 为后代的的最深节点。

当范围被放置在文档的特定位置时，这些属性会被填充。

### DOM 范围中的简单选择

使用范围选择文档部分最简单的方法是使用 `selectNode()` 或 `selectNodeContents()`。这两个方法每个都接受一个参数（即一个 DOM 节点），并用该节点的信息填充范围。`selectNode()` 方法选择整个节点（包括其子节点），而 `selectNodeContents()` 则仅选择节点的子节点。例如，考虑以下 HTML：

```html
<!DOCTYPE html>

<html>

    <body>

        <p id="p1"><b>Hello</b> world!</p>

    </body>

</html>
```

可以使用以下 JavaScript 访问此代码：

![image](img/logo1.gif)

```javascript
var range1 = document.createRange(),

    range2 = document.createRange(),

    p1 = document.getElementById("p1");

range1.selectNode(p1);

range2.selectNodeContents(p1);
```

`DOMRangeExample.htm`

此示例中的两个范围包含文档的不同部分：`range1` 包含 `<p>` 元素及其所有子元素，而 `range2` 包含 `<b>` 元素、文本节点 "Hello" 和文本节点 " world!"。参见图 12-6。

图 12-6

![image](img/f416-01.jpg)

当调用 `selectNode()` 时，`startContainer`、`endContainer` 和 `commonAncestorContainer` 都等于传入节点的父节点；在示例示例中，这些都将等于 `document.body`。`startOffset` 属性等于给定节点在父级 `childNodes` 集合中的索引（在本示例中为 1 —— 记住，符合 DOM 标准的浏览器会将空格视为文本节点），而 `endOffset` 等于 `startOffset` 加一（因为只选择了一个节点）。

当调用 `selectNodeContents()` 时，`startContainer`、`endContainer` 和 `commonAncestorContainer` 等于传入的节点，在本示例中是 `<p>` 元素。`startOffset` 属性始终等于 0，因为范围从给定节点的第一个孩子开始，而 `endOffset` 等于子节点的数量（`node.childNodes.length`），在本示例中为 2。

通过使用以下范围方法，可以对包含在选择中的节点进行更细粒度的控制：

- `setStartBefore(refNode)` — 将范围的起始点设置在 `refNode` 之前，因此 `refNode` 是选择内容中的第一个节点。`startContainer` 属性被设置为 `refNode.parentNode`，`startOffset` 属性设置为 `refNode` 在其父级 `childNodes` 集合中的索引。
- `setStartAfter(refNode)` — 将范围的起始点设置在 `refNode` 之后，因此 `refNode` 不在选择范围内；相反，它的下一个兄弟节点是选择中的第一个节点。`startContainer` 属性被设置为 `refNode.parentNode`，`startOffset` 属性设置为 `refNode` 在其父级 `childNodes` 集合中的索引加一。
- `setEndBefore(refNode)` — 将范围的终点设置在 `refNode` 之前，因此 `refNode` 不在选择范围内；它的上一个兄弟节点是选择中的最后一个节点。`endContainer` 属性设置为 `refNode.parentNode`，`endOffset` 属性设置为 `refNode` 在其父级 `childNodes` 集合中的索引。
- `setEndAfter(refNode)` — 将范围的终点设置在 `refNode` 之前（此处原文可能有误，逻辑上应为之后），因此 `refNode` 是选择中的最后一个节点。`endContainer` 属性设置为 `refNode.parentNode`，`endOffset` 属性设置为 `refNode` 在其父级 `childNodes` 集合中的索引。

由于选择应该从 "Hello" 中的 "e" 之后开始，因此将 `helloNode` 传入 `setStart()`，偏移量为 2（"e" 之后的位置，其中 "H" 位于位置 0）。要设置选择的结束位置，将 `worldNode` 传入 `setEnd()`，偏移量为 3，这表示不应被选中的第一个字符，即位置 3 的 "r”（位置 0 处实际上有一个空格）。参见图 12-7。

图 12-7

![image](img/f418-01.jpg)

由于 `helloNode` 和 `worldNode` 都是文本节点，它们成为了该范围的 `startContainer` 和 `endContainer`，这样 `startOffset` 和 `endOffset` 就能准确地查看每个节点包含的文本，而不是去查找子节点（当传入元素时就会发生这种情况）。`commonAncestorContainer` 是 `<p>` 元素，它是包含这两个节点的第一个祖先。

当然，仅仅选择文档的部分内容并不好用，除非你能与该选择进行交互。

### 与 DOM 范围内容交互

当范围（range）被创建时，它内部会创建一个文档片段节点（document fragment node），选择中的所有节点都附加在该节点上。范围内容必须是良好的（well-formed）才能执行这一过程。在上一个例子中，该范围并没有表示一个良好的 DOM 结构，因为选择开始在一个文本节点内部并结束于另一个文本节点，这在 DOM 中无法表示。然而，范围可以识别缺失的起始和结束标签，因此能够重构出有效的 DOM 结构进行操作。

在上述的例子中，范围计算出选择内部缺少一个 `<b>` 开始标签，因此范围在后台动态地添加了它，并连同一个新的 `</b>` 结束标签以包裹 "He"，从而将 DOM 修改为如下所示：

```
<p><b>He</b><b>llo</b> world!</p>
```

此外，“world!" 文本节点被拆分为两个文本节点，一个包含 " wo"，另一个包含 "rld!"。生成的 DOM 树如图 12-8 所示，以及该范围的文档片段内容。

图 12-8

![image](img/f419-01.jpg)

范围创建后，可以使用多种方法对范围的内容进行操作。（注意，范围内部文档片段中的所有节点都指向文档中节点的指针。）

第一种方法是最容易理解和使用的：`deleteContents()`。该方法简单地从文档中删除范围的内容。这是一个示例：

![image](img/logo1.gif)

```javascript
var p1 = document.getElementById("p1"),

    helloNode = p1.firstChild.firstChild,

    worldNode = p1.lastChild,

    range = document.createRange();

range.setStart(helloNode, 2);

range.setEnd(worldNode, 3);

range.deleteContents();
```

`DOMRangeExample4.htm`

执行这段代码会在页面上显示以下 HTML：

```
<p><b>He</b>rld!</p>
```

由于范围选择过程修改了底层的 DOM 结构以保持良好状态，因此在删除内容后，生成的 DOM 结构仍然良好。

`extractContents()` 与 `deleteContents()` 类似，它也会从文档中移除范围选择。区别在于 `extractContents()` 将范围的文档片段作为函数的返回值。这允许你将范围的内容插入到其他地方。这是一个示例：

![image](img/logo1.gif)

```javascript
var p1 = document.getElementById("p1"),

    helloNode = p1.firstChild.firstChild,

    worldNode = p1.lastChild,

    range = document.createRange();

range.setStart(helloNode, 2);

range.setEnd(worldNode, 3);

var fragment = range.extractContents();

p1.parentNode.appendChild(fragment);
```

`DOMRangeExample5.htm`

在这个示例中，片段被提取并添加到到文档 `<body>` 元素的末尾。（记住，当将文档片段传递给 `appendChild()` 时，只有片段的节点会被添加，而不是片段本身。）生成的 HTML 如下：

```
<p><b>He</b>rld!</p>

<b>llo</b> wo
```

另一个选项是保持范围在原位，但使用 `cloneContents()` 创建它的克隆，并将其插入到文档的其他位置，如下例所示：

```javascript
var p1 = document.getElementById("p1"),

    helloNode = p1.firstChild.firstChild,

    worldNode = p1.lastChild,

    range = document.createRange();

range.setStart(helloNode, 2);

range.setEnd(worldNode, 3);

var fragment = range.cloneContents();

p1.parentNode.appendChild(fragment);
```

`DOMRangeExample6.htm`

这种方法与 `extractContents()` 非常相似，因为它们都返回一个文档片段。主要区别在于 `cloneContents()` 返回的文档片段包含了范围内节点的克隆，而不是实际的节点。通过此操作，页面中的 HTML 保持不变：

```
<p><b>He</b> world!</p>
```

### 插入范围内容

范围可以用于移除或克隆内容（如上一节所示），并操作 HTML。`insertNode()` 方法允许你在范围的开头插入一个节点。作为一个示例，假设你想插入以下 HTML：

```
<span style="color: red">Inserted text</span>
```

以下代码完成了此操作：

![image](img/logo1.gif)

```javascript
var p1 = document.getElementById("p1"),

    helloNode = p1.firstChild.firstChild,

    worldNode = p1.lastChild,

    range = document.createRange();

range.setStart(helloNode, 2);

range.setEnd(worldNode, 3);

var span = document.createElement("span");

span.style.color = "red";

span.appendChild(document.createTextNode("Inserted text"));

range.insertNode(span);
```

`DOMRangeExample7.htm`

运行这段 JavaScript 实际上创建了如下 HTML：

```
<p id="p1"><b><span style="color: red">Inserted text</span>llo world</p>
```

注意 `<span>` 被插入在 "llo" 之前。注意原始 HTML 没有添加或移除 `<b>` 元素，因为没有使用上一节介绍的方法。除了向范围插入内容外，还可以通过 `surroundContents()` 方法包裹范围内容。该方法接受一个参数，即包裹范围内容的节点。在后台，执行了以下步骤：

1. 提取范围内容（类似于使用 `extractContents()`）。
2. 将给定的节点插入到原始文档范围所在的位置。
3. 将片段的内容添加到给定的节点中。

这种功能用于在网页上高亮某些单词，如下：

![image](img/logo1.gif)

```javascript
var p1 = document.getElementById("p1"),

    helloNode = p1.firstChild.firstChild,

    worldNode = p1.lastChild,

    range = document.createRange();

range.selectNode(helloNode);

var span = document.createElement("span");

span.style.backgroundColor = "yellow";

range.surroundContents(span);
```

`DOMRangeExample8.htm`

这段代码用黄色背景高亮了范围选择。生成的 HTML 如下：



<p><b><span style="background-color:yellow">Hello</span></b> world!</p>

```
为了插入 `<span>`，范围必须包含一个完整的 DOM 选择。（它不能只部分选择 DOM 节点。）
```

### 折叠 DOM 范围

当一个范围（`range`）没有选择文档的任何部分时，它被称为“折叠的”（`collapsed`）。范围的折叠行为类似于文本框的行为。当文本框中有文字时，你可以使用鼠标高亮整个单词。然而，如果你再次左键点击鼠标，选择将被移除，光标将位于两个字母之间。当你折叠一个范围时，它的位置会被设置在文档的部分之间，是在范围选择的起始处或结束处。图 12-9 展示了范围被折叠时发生的情况。

图 12-9

![image](img/f422-01.jpg)

你可以使用`collapse()`方法来折叠范围，该方法接受一个参数：一个布尔值，表示要折叠到范围的哪一。如果参数为`true`，则范围将折叠到起点；如果为`false`，则范围将折叠到终点。要判断一个范围是否已经折叠，你可以如下使用`collapsed`属性：

```javascript
range.collapse(true);      //折叠到起点

alert(range.collapsed);    //输出 "true"
```

测试范围是否已折叠对于你不确定范围内的两个节点是否相邻的情况是有帮助的。例如，考虑以下 HTML 代码：

```html
<p id="p1">段落 1</p><p id="p2">段落 2</p>
```

如果你不知道这段代码的精确组成（例如，如果它是自动生成的），你可能会尝试创建这样的范围：

```javascript
var p1 = document.getElementById("p1"),

    p2 = document.getElementById("p2"),

    range = document.createRange();

range.setStartAfter(p1);

range.setStartBefore(p2);

alert(range.collapsed);    //输出 "true"
```

在这种情况下，创建的范围是折叠的，因为在`p1`的结束和`p2`的开始之间没有任何内容。

### 比较 DOM 范围

如果你有多个范围，可以使用`compareBoundaryPoints()`方法来确定这些范围是否具有共同的边界（起始或结束）。该方法接受两个参数：要比较的范围以及比较方式。它应该是以下常量值之一：

* `Range.START_TO_START (0)` — 比较第一个范围的起始点和第二个范围的起始点。
* `Range.START_TO_END (1)` — 比较第一个范围的起始点和第二个范围的终点。
* `Range.END_TO_END (2)` — 比较第一个范围的终点和第二个范围的终点。
* `Range.END_TO_START (3)` — 比较第一个范围的终点和第二个范围的起始点。

如果第一个范围的点在第二个范围的点之前，`compareBoundaryPoints()`方法返回 -1；如果点相等，则返回 0；如果第一个范围的点在第二个范围的点之后，则返回 1。这里有一个示例：

![image](img/logo1.gif)

```javascript
var range1 = document.createRange();

var range2 = document.createRange();

var p1 = document.getElementById("p1");

range1.selectNodeContents(p1);

range2.selectNodeContents(p1);

range2.setEndBefore(p1.lastChild);

alert(range1.compareBoundaryPoints(Range.START_TO_START, range2));  //0

alert(range1.compareBoundaryPoints(Range.END_TO_END, range2));      //1
```

DOMRangeExample9.htm

在此代码中，两个范围的起始点完全相同，因为它们都使用了来自`selectNodeContents()`的默认值；因此，该方法返回 0。然而对于`range2`，终点使用`setEndBefore()`被更改，使得`range1`的终点位于`range2`终点之后（参见图 12-10），因此该方法返回 1。

图 12-10

![image](img/f424-01.jpg)

### 克隆 DOM 范围

可以通过调用`cloneRange()`方法克隆范围。该方法会创建被调用时范围的精确副本：

```javascript
var newRange = range.cloneRange();
```

新范围包含与原始范围相同的所有属性，并且可以修改终点而不会对原始范围产生任何影响。

### 清理

当你完成范围的使用后，最好调用`detach()`方法，它会将范围从其创建的文档中分离出来。在调用`detach()`之后，范围可以安全地取消引用，从而可以通过垃圾回收释放内存。这里有一个示例：

```javascript
range.detach();  //从文档中分离

range = null;    //取消引用
```

遵循这两个步骤是结束范围使用的最合适方法。一旦分离，范围将无法再次被使用。

### Internet Explorer 8 及更早版本中的范围

虽然 Internet Explorer 9 支持 DOM 范围，但 8 及更早版本不支持。然而，早期版本支持名为“文本范围”（`text ranges`）的类似概念。文本范围是 Internet Explorer 特有的。

通过按特定的增量移动范围选择区域，可以在 Internet Explorer 中创建复杂的范围。这可以通过四种方法实现：`move()`、`moveStart()`、`moveEnd()`和`expand()`。这些方法每个都接受两个参数：要移动的单位类型和移动的单位数量。要移动的单位类型是以下字符串值之一：

* `"character"` — 将点移动一个字符。
* `"word"` — 将点移动一个单词（一串非空白字符的序列）。
* `"sentence"` — 将点移动一个句子（一串以句号、问号或感叹号结尾的字符序列）。
* `"textedit"` — 将点移动到当前范围选择选择的起始或结束位置。

`moveStart()`方法根据指定的单位数量移动范围的起始点，而`moveEnd()`方法根据指定的单位数量移动范围的结束点，如下例所示：

```
range.moveStart("word", 2);       //将起始点移动两个单词

range.moveEnd("character", 1);    //将结束点移动一个字符
```

你还可以使用`expand()`方法来归一化范围。`expand()`方法确保任何部分选中的单位都变为完全选中。例如，如果你只选择了一个单词中间的两个字符，可以调用`expand("word")`来确保整个单词都被包含在范围内。

`move()`方法首先折叠范围（使起始点和结束点相等），然后按指定的单位数量移动范围，如下例：

```
range.move("character", 5);   //移动五个字符
```

在使用`move()`之后，起始点和结束点是相等的，因此你必须使用`moveStart()`或`moveEnd()`来再次进行选择。

## 与 Internet Explorer 范围内容的交互

在 Internet Explorer 中与范围内容进行交互可以通过`text`属性或`pasteHTML()`方法完成。`text`属性之前用于获取范围的文本内容，也可以用于设置范围的文本内容。这里是一个示例：

```
var range = document.body.createTextRange();

range.findText("Hello");

range.text = "Howdy";
```

如果你对之前显示的“Hello world!”代码运行这段代码，HTML 结果如下：

```
<p id="p1"><b>Howdy</b> world!</p>
```

注意，在设置`text`属性时，所有的 HTML 标签都保持完好。

要向范围内插入 HTML 代码，可以使用`pasteHTML()`方法，如下例：

![image](img/logo1.gif)

```
var range = document.body.createTextRange();

range.findText("Hello");

range.pasteHTML("<em>Howdy</em>");
```

IERangeExample3.htm

执行此代码后，生成的 HTML 如下：

```
<p id="p1"><b><em>Howdy</em></b> world!</p>
```

当范围包含 HTML 代码时，你不应该使用`pasteHTML()`，因为这会导致不可预测的结果，并且你可能会得到格式不错误的 HTML。

### 折叠 Internet Explorer 范围

Internet Explorer 中的范围有一个`collapse()`方法，它的工作方式与 DOM 方法完全相同：传递`true`将范围折叠到开头，传递`false`将范围折叠到末尾。这里有一个示例：

```
range.collapse(true);    //折叠到起始
```

遗憾的是，没有对应的折叠属性可以告诉你范围是否已经折叠。相反，你必须使用`boundingWidth`属性，它返回范围的宽度（像素）。如果`boundingWidth`等于 0，则范围已如下折叠：

```
var isCollapsed = (range.boundingWidth == 0);
```

`boundingHeight`、`boundingLeft`和`boundingTop`属性也提供了关于范围位置的信息，尽管它们没有`boundingWidth`帮助。

### 比较 Internet Explorer 范围

Internet Explorer 中的`compareEndPoints()`方法类似于 DOM 范围的`compareBoundaryPoints()`方法。该方法接受两个参数：比较类型和要比较的范围。比较类型由以下字符串值之一指示：`"StartToStart"`、`"StartToEnd"`、`"EndToEnd"`和`"EndToStart"`。这些比较等于 DOM 范围中的对应值。

同样与 DOM 类似，如果第一个范围边界在第二个范围边界之前，`compareEndPoints()`返回 -1；如果它们相等，则返回 0；如果第一个范围边界在第二个范围边界之后，则返回 1。再次使用上一个示例中的“Hello world!”代码，以下代码创建了范围：一个选择“Hello world!”（包括`b`标签），另一个选择“Hello”：

```
var range1 = document.body.createTextRange(),

    range2 = document.body.createTextRange();

range1.findText("Hello world!");

range2.findText("Hello");

alert(range1.compareEndPoints("StartToStart", range2));  //0

alert(range1.compareEndPoints("EndToEnd", range2));      //1
```

IERangeExample5.htm

第一个和第二个范围共享相同的起点，因此使用`compareEndPoints()`比较它们返回 0。`range1`的结束点发生在`range2`的结束点之后，因此`compareEndPoints()`返回 1。

Internet Explorer 还有两个用于比较范围的其他方法：`isEqual()`用于判断两个范围具有相同的起始和结束点，`inRange()`用于判断一个范围是否在另一个范围内。这里是一个示例：

![image](img/logo1.gif)

```
var range1 = document.body.createTextRange();

var range2 = document.body.createTextRange();

range1.findText("Hello world!");

range2.findText("Hello");

alert("range1.isEqual(range2): " + range1.isEqual(range2)); //false

alert("range1.inRange(range2): " + range1.inRange(range2)); //true
```



`IERangeExample6.htm`

此示例使用了之前示例中的相同范围来说明这些方法。由于结束点不同，因此`isEqual()`返回`false`。然而，`range2`实际上在`range1`内部，因为它的结束点发生在`range1`的结束点之前，但在`range1`的起始点之后。因此`range2`被认为在`range1`内部，`inRange()`返回`true`。

### 克隆 Internet Explorer 范围

可以使用`duplicate()`方法在 Internet Explorer 中克隆文本范围，该方法会范围范围的精确副本，如下：

原始范围的所有属性都会复制到新范围中。

## 总结

DOM Level 2 规范定义了多个扩展了 DOM Level 1 功能的模块。DOM Level 2 Core 为各种 DOM 类型引入了许多与 XML 命名空间相关的新方法。这些更改仅在使用 XML 或 XHTML 文档时有效；对 HTML 文档没有用。与 XML 命名空间无关的方法包括通过程序创建新的`Document`实例以及启用创建`DocumentType`对象。

DOM Level 2 Style 模块规定了如何与元素的样式信息进行交互：

* 每个元素都有一个关联的`style`对象，可用于确定和更改内联样式。
* 要确定元素的计算样式（包括应用到它的所有 CSS 规则），可以使用`getComputedStyle()`方法。
* Internet Explorer 不支持此方法，但在所有元素上提供了`currentStyle`属性来返回相同的信息。
* 也可以通过`document.styleSheets`集合访问样式表。
* 样式表被 Internet Explorer 8 及更早版本以外的所有浏览器支持，它们为几乎所有 DOM 功能提供了类似的属性和方法。

DOM Level 2 Traversals and Range 模块规定了与 DOM 结构交互的不同方式：

* 遍历通过`NodeIterator`或`TreeWalker`对 DOM 树进行深度优先遍历。
* `NodeIterator`接口非常简单，仅允许单步增量的向前和向后移动。`TreeWalker`接口支持相同的行为，并在 DOM 结构的所有其他方向移动，包括父元素、兄弟元素和子元素。
* `Ranges`是选择 DOM 结构特定部分以某种方式对其进行增强的方法。
* 范围选择（Selections of ranges）可用于删除文档的部分同时保留良好的文档结构，或用于克隆文档的部分。
* Internet Explorer 8 及更早版本不支持 DOM Level 2 遍历和`Range`，尽管它们提供了一个专有的文本范围对象可用于简单的基于文本的范围操作。Internet Explorer 9 完全支持 DOM 遍历。

# 第 13 章：事件

## 本章内容
* 理解事件流
* 使用事件处理程序（handlers）
* 检查不同类型的事件

JavaScript 与 HTML 的交互通过事件来处理，事件指示了文档或浏览器窗口中何时发生了感兴趣的时刻。可以使用监听器（也称为处理程序）来订阅事件，这些监听器仅在事件发生时执行。这种模型在传统软件工程中被称为观察者模式，允许页面的行为（由 JavaScript 定义）与页面的外观（由 HTML 和 CSS 定义）之间存在松耦合。

事件最早出现在 Internet Explorer 3 和 Netscape Navigator 2 中，作为将某些表单处理从服务器转移到浏览器的方法。当 Internet Explorer 4 和 Netscape 4 发布时，每个浏览器都提供了相似但不同的 API，这些 API 持续了数代。DOM Level 2 是首次尝试以逻辑方式标准化 DOM 事件 API 的尝试。Internet Explorer 9、Firefox、Opera、Safari 和 Chrome 均实现了 DOM Level 2 事件的核心部分。Internet Explorer 8 是最后一个使用纯专有事件系统的主流浏览器。

浏览器事件系统是一个复杂的系统。尽管所有主流浏览器都实现了 DOM Level 2 事件，但规范并没有涵盖所有事件类型。`BOM`也支持事件，由于长期缺乏文档，这些事件与 DOM 事件之间的关系往往令人生困惑（HTML5 曾试图澄清这一点）。进一步使问题变得复杂的是 DOM Level 3 对 DOM 事件 API 的增强。处理事件可能相对简单，也可能非常复杂，取决于你的需求。尽管如此，仍有一些核心概念是理解理解。

## 事件流

当开发第四代网页浏览器（Internet Explorer 4 和 Netscape Communicator 4）时，浏览器开发团队遇到了一个有趣的问题：页面的哪个部分拥有特定的事件？为了理解这个问题，请考虑纸上画的一系列同心圆。当你把手指放在中心时，它不仅位于一个圆内，而且位于纸上所有的圆内。两个开发团队以相同的方式看待浏览器事件。他们得出结论：当你点击一个按钮时，你不仅点击了按钮，还点击了它的容器以及整个页面。

事件流描述了事件在页面上接收的顺序，有趣的是，Internet Explorer 和 Netscape 开发团队提出了一种近乎完全相反的事件流概念。Internet Explorer 支持事件冒泡（bubbling）流，而 Netscape Communicator 则支持事件捕获（capturing）流。

### 事件冒泡

Internet Explorer 事件流被称为事件冒泡，因为事件认为从最特定的元素（文档树中尽可能深点）开始，然后向上流向最不特定的节点（文档）。考虑以下 HTML 页面：

```
<!DOCTYPE html>
<html>
<head>
    <title>Event Bubbling Example</title>
</head>
<body>
    <div id="myDiv">Click Me</div>
</body>
</html>
```

当你点击页面中的`<div>`元素时，点击事件按以下顺序发生：

1. `<div>`
2. `<body>`
3. `<html>`
4. `document`

点击事件首先在`<div>`上触发，这是被点击的元素。然后点击事件沿 DOM 树向上移动，在路径上的每个节点上触发，直到到达文档对象。图 13-1 释了这种效果。

图 13-1

![image](img/f432-01.jpg)

所有现代浏览器都支持事件冒泡，尽管在实现方式上存在差异。Internet Explorer 5.5 及更早版本跳过了到`<html>`元素的冒泡（直接从`<body>`跳到`document`）。Internet Explorer 9、Firefox、Chrome 和 Safari 继续将事件冒泡持续到`window`对象。

### 事件捕获

Netscape Communicator 团队提出了一种替代事件流，称为事件捕获。事件捕获的理论是：最不特定的节点应该先接收事件，而最特定的节点应该最后接收事件。事件捕获真正的设计目的是在事件到达预期目标之前将其拦截。如果在上一个示例中使用事件捕获，点击`<div>`元素将按以下顺序触发点击事件：

1. `document`
2. `<html>`
3. `<body>`
4. `<div>`

通过事件捕获，点击事件首先由`document`接收，然后继续向下通过 DOM 树到达事件的目标`<div>`元素。这种流在 图 13-2 中进行了阐释。

图 13-2

![image](img/f433-01.jpg)

虽然这是 Netscape Communicator 唯一的事件流，但目前 Internet Explorer 9、Safari、Chrome、Opera 和 Firefox 均支持事件捕获。它们实际上都从`document`开始进行事件捕获。

### DOM 事件流

DOM Level 2 事件规范指定的事件流有三个阶段：事件捕获阶段、目标目标阶段（at target）和事件冒泡阶段。事件捕获首先发生，提供了必要时拦截事件的机会。接下来，实际目标接收事件。最后一个阶段是冒泡，允许对事件做出最后的响应。考虑之前使用的简单 HTML 示例，点击`<div>`会按 图 13-3 所示的顺序触发事件。

图 13-3

![image](img/f433-02.jpg)

在 DOM 事件流中，实际目标（`<div>`元素）在捕获阶段期间不接收事件。这意味着捕获阶段从`document`移动到`<html>`再到`<body>`然后停止。下一个阶段是“目标阶段”，它在`<div>`上触发，并且从事件处理的角度来看，被认为是冒泡阶段的一部分（稍后讨论）。然后，发生冒泡阶段，事件传回文档。

事件是由用户或浏览器本身执行的确定动作。这些事件具有如`click`、`load`和`mouseover`之类的名称。响应事件调用的函数称为事件处理器（event handler）或事件监听器（event listener）。事件处理器的名称以 "on" 开头，因此`click`事件的事件处理器被称为`onclick`，`load`事件的事件处理器被称为`onload`。分配事件处理器可以通过多种不同的方式实现。

## HTML 事件处理器

特定元素支持的每个事件都可以使用名称与事件处理器相同的 HTML 属性进行分配。该属性的值应该是一段要执行的 JavaScript 代码。例如，为了在点击按钮时执行某些 JavaScript，您可以使用以下代码：

```
<input type="button" value="Click Me" onclick="alert('Clicked')" />
```

当点击此按钮时，会显示一个警报框。这种交互通过指定`onclick`属性并将某些 JavaScript 代码作为值来定义。注意，由于 JavaScript 代码是一个属性值，除非对它们进行转义，否则您不能使用 HTML 语法字符，如和符号`&`、双引号、小于号或大于号。在这种情况下，使用了单引号而不是双引号，以避免使用 HTML 实体。要使用双引号，您将代码更改为：

```
<input type="button" value="Click Me" onclick="alert(&quot;Clicked&quot;)" />
```

在 HTML 中定义的事件处理器可以包含要执行的精确操作，也可以调用页面上其他地方定义的脚本，如下例所示：

![image](img/logo1.gif)

```
<script type="text/javascript">
    function showMessage(){
        alert("Hello world!");
    }
</script>
<input type="button" value="Click Me" onclick="showMessage()" />
```

`HTMLEventHandlerExample01.htm`

在此代码中，按钮在被点击时会调用`showMessage()`。`showMessage()`函数定义在一个单独的`<script>`中，也可以包含在外部文件中。作为事件处理器执行的代码可以访问全局作用域中的所有内容。

通过这种方式分配的事件处理器有一些独特之处。首先，会创建一个封装了属性值的函数。该函数有一个特殊的局部变量称为`event`，它是事件对象（在本章稍后将讨论）：

```
<!-- outputs "click" -->
<input type="button" value="Click Me" onclick="alert(event.type)">
```

这使得您无需自己定义即可访问事件对象，也不需要从闭包函数的参数列表中提取它。

函数内部的`this`值等同于事件的目标元素，例如：

```
<!-- outputs "Click Me" -->
<input type="button" value="Click Me" onclick="alert(this.value)">
```

这个动态创建的函数的另一个有趣方面是它是如何增强作用域链的。在函数内部，`document`的成员和元素本身的成员都可以像局部变量一样被访问。函数通过使用`with`增强作用域链来实现这一点：

```javascript
function(){
    with(document){
        with(this){
            //attribute value
        }
    }
}
```

这意味着事件处理器可以轻松地访问自己的属性。以下代码在功能上与之前的示例相同：

```html
<!-- outputs "Click Me" -->
<input type="button" value="Click Me" onclick="alert(value)">
```

如果该元素是一个表单输入元素，那么作用域链还包含一个父表单元素的条目，使得该函数等同于以下：

```javascript
function(){
    with(document){
        with(this.form){
            with(this){
                //attribute value
            }
        }
    }
}
```

基本上，这种增强允许事件处理器代码在不引用表单元素本身的情况下访问同一个表单的其他成员。例如：

![image](img/logo1.gif)

```html
<form method="post">
    <input type="text" name="username" value="">
    <input type="button" value="Echo Username" onclick="alert(username.value)">
</form>
```

`HTMLEventHandlerExample04.htm`

点击此示例中的按钮会将文本框中的文本显示出来。注意，它只是直接引用了`username`。

在 HTML 中分配事件处理器有几个缺点。第一个是时机问题：HTML 元素可能在事件处理器代码准备好之前出现在页面上并被用户交互。在之前的示例中，假设有一种场景，即`showMessage()`函数在页面稍后的位置（按钮代码之后）才定义。如果用户在`showMessage()`定义之前点击了按钮，就会发生错误。由于由于原因，大多数 HTML 事件处理器被封装在`try-catch`块中，以便它们静默失败，如下例所示：

```html
<input type="button" value="Click Me" onclick="try{showMessage();}catch(ex){}">
```

如果在`showMessage()`函数定义之前点击此按钮，就不会发生 JavaScript 错误，因为错误在浏览器处理之前就被捕获了。

另一个缺点是事件处理器函数中的作用域链增强在不同的浏览器中会导致不同的结果。JavaScript 引擎之间遵循的标识符解析规则略有不同，因此访问未限定的对象成员可能会导致错误。

使用 HTML 分配事件处理器的最后一个缺点是它将 HTML 与 JavaScript 密耦合。如果需要更改事件处理器，您可能需要更改两个处的代码。这是许多开发者倾向于使用 JavaScript 分配事件处理器而不是 HTML 处理器的主要原因。

![image](img/pen.gif)

关于 HTML 事件处理器的更多信息，请查看 Garrett Smith 的 [Event Handler (www.jibbering.com/event_handler.html)](http://www.jibbering.com/event_handler.html))。

你可以通过将事件处理程序属性的值设置为`null`来移除通过 DOM Level 0 方式分配的事件处理器，如下例所示：

```
btn.onclick = null;    //移除事件处理器
```

一旦事件处理器被设置为`null`，该按钮在被点击时将不再执行任何操作。

![image](img/pen.gif)

如果你使用 HTML 分配了事件处理器，那么`onclick`属性上的值将是一个包含包含 HTML 属性中指定代码的函数。这些事件处理器也可以通过将该属性设置为`null`来移除。

## DOM Level 2 事件处理器

DOM Level 2 事件定义了两种处理事件处理器分配和移除的方法：`addEventListener()`和`removeEventListener()`。这些方法存在于所有 DOM 节点上，并接受三个参数：要处理的事件名称、事件处理函数，以及一个指示在捕获阶段（`true`）还是冒泡阶段（`false`）调用事件期间调用事件处理器的布尔值。

要为按钮的`click`事件添加事件处理器，可以使用以下代码：

```javascript
var btn = document.getElementById("myBtn");
btn.addEventListener("click", function(){
    alert(this.id);
}, false);
```

此代码为按钮添加了一个`onclick`事件处理器，该处理器将在冒泡阶段触发（因为最后一个参数是`false`）。与 DOM Level 0 方式一样，事件处理器在它所挂载的元素作用域内运行。使用 DOM Level 2 方法添加事件处理器的主要优势是可以添加多个事件处理器。考虑以下示例：

![image](img/logo1.gif)

```javascript
var btn = document.getElementById("myBtn");
btn.addEventListener("click", function(){



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`。

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

---

```
alert(this.id);
}, false);

btn.addEventListener("click", function(){
    alert("Hello world!");
}, false);
```

`DOMLevel2EventHandlerExample01.htm`

在这里，按钮被添加了两个事件处理器。事件处理器按照它们被添加的顺序触发，因此第一个`alert`显示元素的ID，第二个`alert`显示消息“Hello world!”。

通过`addEventListener()`添加的事件处理器只能通过使用`removeEventListener()`才能移除，并且必须传入与添加处理器时使用的相同的参数。这意味着使用`addEventListener()`添加的匿名函数是无法移除的，如本例所示：

```javascript
var btn = document.getElementById("myBtn");

btn.addEventListener("click", function(){
    alert(this.id);
}, false);

//此处有其他代码

btn.removeEventListener("click", function(){   //不起作用！
    alert(this.id);
}, false);
```

在此示例中，使用`addEventListener()`添加了一个匿名函数作为事件处理器。对`removeEventListener()`的调用看起来像是使用了相同的参数，但实际上，第二个参数与`addEventListener()`中使用的函数是完全不同的。传递给`removeEventListener()`的事件处理器函数必须与在`addEventListener()`中使用的同一个，如下例所示：

![image](img/logo1.gif)

```javascript
var btn = document.getElementById("myBtn");

var handler = function(){
    alert(this.id);
};

btn.addEventListener("click", handler, false);

//此处有其他代码

btn.removeEventListener("click", handler, false);  //生效了！
```

`DOMLevel2EventHandlerExample02.htm`

这个重写后的示例按预期工作，因为`addEventListener()`和`removeEventListener()`使用了同一个函数。

在大多数情况下，事件处理器被添加到事件流的冒泡阶段，因为这提供了最广泛的跨浏览器支持。如果你需要在事件到达预期目标之前拦截它们，那么最好在捕获阶段挂载事件处理器。如果这并非必要，建议避免事件捕获。

![image](img/pen.gif)

Internet Explorer 9、Firefox、Safari、Chrome 和 Opera 都支持 DOM Level 2 事件处理器。

## Internet Explorer 事件处理器

Internet Explorer 实现了类似于 DOM 的类似方法，称为`attachEvent()`和`detachEvent()`。这些方法接受相同的两个参数：事件处理器名称和事件处理器函数。由于 Internet Explorer 8 及之前的版本仅支持事件冒泡，因此使用`attachEvent()`添加的事件处理器是在冒泡阶段挂载的。

使用`attachEvent()`为按钮的`click`事件添加事件处理器，可以使用以下代码：

```javascript
var btn = document.getElementById("myBtn");

btn.attachEvent("onclick", function(){
    alert("Clicked");
});
```

`IEEventHandlerExample01.htm`

注意`attachEvent()`的第一个参数是`"onclick"`，而不是 DOM 的`addEventListener()`方法中的`"click"`。

在 Internet Explorer 中使用`attachEvent()`与使用 DOM Level 0 方式之间的主要区别在于事件处理器的作用域。使用 DOM Level 0 时，事件处理器运行时的`this`值等于它所挂载的元素；当使用`attachEvent()`时，事件处理器在全局上下文中运行，因此等同于`window`。这里有一个示例：

```javascript
var btn = document.getElementById("myBtn");

btn.attachEvent("onclick", function(){
    alert(this === window);   //true
});
```

在编写跨浏览器代码时，理解这种差异非常重要。

`attachEvent()`方法类似于`addEventListener()`，可以用于向单个元素添加多个事件处理器。考虑以下示例：

![image](img/logo1.gif)

```javascript
var btn = document.getElementById("myBtn");

btn.attachEvent("onclick", function(){
    alert("Clicked");
});

btn.attachEvent("onclick", function(){
    alert("Hello world!");
});
```

`IEEventHandlerExample01.htm`

在这里，`attachEvent()`被调用了两次，为同一个按钮添加了两个不同的事件处理器。但与 DOM 方法不同，事件处理器的触发顺序与它们的添加顺序相反。当点击此示例中的按钮时，第一个`alert`显示“Hello world!”，第二个显示“Clicked”。

使用`attachEvent()`添加的事件只要提供了相同的参数，就可以通过`detachEvent()`移除。与 DOM 方法一样，这意味着一旦添加了匿名函数就无法移除。只要可以将同一个函数的引用传递给`detachEvent()`，事件处理器就可以被移除。这里有一个示例：

```javascript
var btn = document.getElementById("myBtn");

var handler = function(){
    alert("Clicked");
};

btn.attachEvent("onclick", handler);

//此处有其他代码

btn.detachEvent("onclick", handler);
```

`IEEventHandlerExample02.htm`

这个示例添加了存储在变量`handler`中的事件处理器。随后使用`detachEvent()`移除了同一个函数。

![image](img/pen.gif)

Internet Explorer 事件处理器支持 Opera。

## 跨浏览器事件处理器

为了以跨浏览器的方式处理事件，许多开发者最终选择使用抽象差异的 JavaScript 库，或者编写自定义代码来使用最合适的事件处理方法。编写自己的代码相当简单，因为其依赖于功能检测（见第 9 章）。为了确保事件处理代码能够以尽可能兼容的方式运行，你需要它仅在冒泡阶段工作。

要创建的方法是`addHandler()`，它的任务是根据可用性，使用 DOM Level 0 方法、DOM Level 2 方法或 Internet Explorer 方法来添加事件。该方法挂载在一个名为`EventUtil`的对象上，该对象将在整个书中用于辅助处理跨浏览器差异。`addHandler()`方法接受三个参数：要操作的元素、事件名称和事件处理函数。

`addHandler()`的对应方法是`removeHandler()`，它接受相同的三个参数。该方法的作用是使用任何可用方法移除之前添加的事件处理程序，如果没有其他方法可用，则默认为 DOM Level 0。

`EventUtil`的完整代码如下：

![image](img/logo1.gif)

```javascript
var EventUtil = {
    addHandler: function(element, type, handler){
        if (element.addEventListener){
            element.addEventListener(type, handler, false);
        } else if (element.attachEvent){
            element.attachEvent("on" + type, handler);
        } else {
            element["on" + type] = handler;
        }
    },
    removeHandler: function(element, type, handler){
        if (element.removeEventListener){
            element.removeEventListener(type, handler, false);
        } else if (element.detachEvent){
            element.detachEvent("on" + type, handler);
        } else {
            element["on" + type] = null;
        }
    }
};
```

`EventUtil.js`

这两个方法首先检查传入的元素上是否存在 DOM Level 2 方法。如果存在 DOM Level 2 方法，则使用它，并传入事件类型和事件处理程序函数，以及第三个参数`false`（表示冒泡阶段）。如果可用 Internet Explorer 的方法，则将其作为备选方案。注意，为了在 Internet Explorer 8 及更早版本中正常工作，事件类型必须加上`"on"`前缀。最后的手段是使用 DOM Level 0 方法（在现代浏览器中代码永远不会执行到此处）。注意使用方括号表示法将属性名赋值给事件处理程序或`null`。

此工具对象可以使用以下方式使用：

![image](img/logo1.gif)

```javascript
var btn = document.getElementById("myBtn");

var handler = function(){
    alert("Clicked");
};

EventUtil.addHandler(btn, "click", handler);

//other code here

EventUtil.removeHandler(btn, "click", handler);
```

`CrossBrowserEventHandlerExample01.htm`

`addHandler()`和`removeHandler()`方法并不能让所有浏览器的功能完全相等（例如 Internet Explorer 的作用域问题），但它确实允许无缝地添加和移除事件处理程序。请记住，DOM Level 0 的支持仅限于每个事件仅有一个事件处理程序。幸运的是，DOM Level 0 浏览器已不再流行，因此这不会对你产生影响。

## 事件对象

当与 DOM 相关的事件触发时，所有相关信息都会被收集并存储在一个名为`event`的对象中。该对象包含基本信息，例如引发事件的元素、发生的事件类型以及任何可能与特定事件相关的数据。例如，由鼠标动作触发的事件会产生鼠标位置的信息，而由键盘动作触发的事件会产生关于按下按键的信息。所有浏览器都支持事件对象，尽管方式不同。

## DOM 事件对象

在符合 DOM 标准的浏览器中，事件对象作为唯一的参数传递给事件处理程序。无论使用 DOM Level 0 还是 DOM Level 2 方法分配事件处理程序，事件对象都会被传递。以下是一个示例：

```javascript
var btn = document.getElementById("myBtn");

btn.onclick = function(event){
    alert(event.type);    //"click"
};

btn.addEventListener("click", function(event){
    alert(event.type);    //"click"
}, false);
```

示例中的两个事件处理程序都通过使用`event.type`属性弹出警框，指示正在触发的事件类型。该属性始终包含触发的事件类型，例如`"click"`（这与你传递`addEventListener()`和`removeEventListener()`的值相同）。

当使用 HTML 属性分配事件处理程序时，事件对象将作为名为`event`的变量可用。以下是一个示例：

```html
<input type="button" value="Click Me" onclick="alert(event.type)">
```

通过这种方式提供事件对象允许 HTML 属性事件处理程序执行与 JavaScript 函数相同的操作。

事件对象包含了与导致它的特定事件相关的属性和方法。可用的属性和方法取决于触发的事件类型，但所有事件都具有下表列出的成员。

![image](img/f443-01.jpg)

![image](img/f444-01.jpg)

在事件处理程序内部，`this`对象始终等于`currentTarget`的值，而`target`只包含事件的实际目标。如果事件处理程序直接分配在目标元素上，那么`this`、`currentTarget`和`target`都具有相同的值。以下是一个示例：

![image](img/logo1.gif)

```javascript
var btn = document.getElementById("myBtn");

btn.onclick = function(event){
    alert(event.currentTarget === this);   //true
    alert(event.target === this);          //true
};
```

`DOMEventObjectExample01.htm`

此代码检查了`currentTarget`和`target`相对于`this`的值。由于点击事件的目标是按钮，因此三者均相等。如果事件处理程序存在于按钮的父节点（例如`document.body`），这些值将是不同的。考虑以下示例：

```javascript
document.body.onclick = function(event){
    alert(event.currentTarget === document.body);   //true
    alert(this === document.body);                  //true
    alert(event.target === document.getElementById("myBtn")); //true
};
```

`DOMEventObjectExample02.htm`

在示例中点击按钮时，`this`和`currentTarget`都等于`document.body`，因为事件处理程序注册在那里。然而，`target`属性等于按钮元素，因为它是事件的真实目标。由于按钮本身没有分配事件处理程序，点击事件冒泡到`document.body`并在那里被处理。

`type`属性在想要将单个函数分配给多个事件时非常有用。以下是一个示例：

![image](img/logo1.gif)

```javascript
var btn = document.getElementById("myBtn");

var handler = function(event){
    switch(event.type){
        case "click":
            alert("Clicked");
            break;
        case "mouseover":
            event.target.style.backgroundColor = "red";
            break;
        case "mouseout":
            event.target.style.backgroundColor = "";
            break;                        
    }
};

btn.onclick = handler;
btn.onmouseover = handler;
btn.onmouseout = handler;
```

`DOMEventObjectExample03.htm`

`preventDefault()`方法用于防止特定事件的默认行为。例如，链接的默认行为是在点击时跳转到`href`属性中指定的 URL。如果你想防止该跳转发生，可以使用`onclick`事件处理程序来取消该行为，如下例所示：

```javascript
var link = document.getElementById("myLink");

link.onclick = function(event){
    event.preventDefault();
};
```



`DOMEventObjectExample04.htm`

任何可以使用 `preventDefault()` 取消的事件，其 `cancelable` 属性都会设置为 `true`。

`stopPropagation()` 方法立即停止事件在 DOM 结构中的流传，取消发生之前任何后续的事件捕获或冒泡。例如，直接添加到按钮上的事件处理器可以调用 `stopPropagation()` 来防止 `document.body` 上的事件处理器被触发，如下例所示：

![image](img/logo1.gif)

```
var btn = document.getElementById("myBtn");

btn.onclick = function(event){
    alert("Clicked");
    event.stopPropagation();
};

document.body.onclick = function(event){
    alert("Body clicked");
};
```

`DOMEventObjectExample05.htm`

在该示例中，如果不调用 `stopPropagation()`，当点击按钮时将显示两个警框。然而，点击事件永远不会到达 `document.body`，因此 `onclick` 事件处理器永远不会执行。

`eventPhase` 属性有助于确定当前处于事件流的哪一个活跃阶段。如果事件处理器在捕获阶段被调用，`eventPhase` 为 1；如果事件处理器位于目标元素，`eventPhase` 为 2；如果事件处理器处于冒泡阶段，`eventPhase` 为 3。注意，尽管“位于目标”发生在冒泡阶段，但 `eventPhase` 始终为 2。这里有一个示例：

```
var btn = document.getElementById("myBtn");

btn.onclick = function(event){
    alert(event.eventPhase);   //2
};

document.body.addEventListener("click", function(event){
    alert(event.eventPhase);   //1
}, true);

document.body.onclick = function(event){
    alert(event.eventPhase);   //3
};
```

`DOMEventObjectExample06.htm`

当点击此示例中的按钮时，第一个触发的事件处理器是捕获阶段 `document.body` 上的处理器，它会弹出一个显示 `eventPhase` 为 1 的警框。接下来，按钮本身的事件处理器被触发，此时 `eventPhase` 为 2。最后一个触发的事件处理器是冒泡阶段 `document.body` 上的处理器，此时 `eventPhase` 为 3。每当 `eventPhase` 等于 2 时，`this`、`target` 和 `currentTarget` 总是相等的。

![image](img/pen.gif)

事件对象仅在事件处理器仍在执行时存在；一旦所有事件处理器执行完毕，事件对象就会被销毁。

## Internet Explorer 事件对象

与 DOM 事件对象不同，Internet Explorer 事件对象可以根据分配事件处理器的方式通过不同的方式访问。当使用 DOM Level 0 方法分配事件处理器时，事件对象仅作为 `window` 对象的属性存在。这里有一个示例：

```
var btn = document.getElementById("myBtn");

btn.onclick = function(){
    var event = window.event;
    alert(event.type);    //"click"
};
```

在这里，从 `window.event` 获取事件对象，然后用它来确定触发的事件类型（Internet Explorer 的 `type` 属性与 DOM 版本相同）。然而，如果使用 `attachEvent()` 分配事件处理器，则事件对象将作为函数的唯一参数传递进来，如下所示：

```
var btn = document.getElementById("myBtn");

btn.attachEvent("onclick", function(event){
    alert(event.type);    //"click"
});
```

使用 `attachEvent()` 时，与 DOM Level 0 方法一样，事件对象在 `window` 对象上也是可用的。为了方便起见，它也被作为参数传递进来。

如果通过 HTML 属性分配事件处理器，则事件对象作为名为 `event` 的变量可用（与 DOM 模型相同）。这里有一个示例：

```
<input type="button" value="Click Me" onclick="alert(event.type)">
```

Internet Explorer 事件对象还包含与导致创建它的特定事件相关的属性和方法。其中许多直接映射到或与 DOM 属性或方法相关。与 DOM 事件对象一样，可用的属性和方法取决于触发的事件类型，但所有事件都使用下表中定义的属性和方法。

![image](img/f447-01.jpg)

由于事件处理器的作用域由其分配方式决定，因此不能总是假设其值等于事件目标，所以始终使用 `event.srcElement` 是更好的主意。这里有一个示例：

![image](img/logo1.gif)

```
var btn = document.getElementById("myBtn");

btn.onclick = function(){
    alert(window.event.srcElement === this);      //true
};

btn.attachEvent("onclick", function(event){
    alert(event.srcElement === this);             //false
});
```

`IEEventObjectExample01.htm`

在第一个使用 DOM Level 0 方法分配的事件处理器中，`srcElement` 属性等于 `this`，但在第二个事件处理器中，这两个值是不同的。

`returnValue` 属性等于 DOM 的 `preventDefault()` 方法，因为它取消了给定事件的默认行为。你只需要将 `returnValue` 设置为 `false` 来阻止默认操作。考虑以下示例：

```
var link = document.getElementById("myLink");

link.onclick = function(){
    window.event.returnValue = false;
};
```

`IEEventObjectExample02.htm`

在此示例中，在 `onclick` 事件处理器中使用 `returnValue` 停止链接的默认操作。与 DOM 不同，无法使用 JavaScript 确定事件是否可以被取消。

`cancelBubble` 属性执行的操作与 DOM 的 `stopPropagation()` 方法相同：它停止事件向上冒泡。由于 Internet Explorer 8 及之前的版本不支持捕获阶段，因此仅冒泡被取消。这里有一个示例：

```
var btn = document.getElementById("myBtn");

btn.onclick = function(){
    alert("Clicked");
    window.event.cancelBubble = true;
};

document.body.onclick = function(){
    alert("Body clicked");
};
```

`IEEventObjectExample03.htm`

通过在按钮的 `onclick` 事件处理器中将 `cancelBubble` 设置为 `true`，它可以阻止事件冒泡到 `document.body` 事件处理器。结果是点击按钮时显示一个警框。

## 跨浏览器事件对象

尽管 DOM 和 Internet Explorer 的事件对象不同，但它们的相似性足以实现跨浏览器解决方案。Internet Explorer 事件对象的所有信息在 DOM 对象中存在，只是形式不同。这些相似之处允许两者之间的轻松映射。之前描述的 `EventUtil` 对象可以通过方法进行扩展：

![image](img/logo1.gif)

```
var EventUtil = {
    addHandler: function(element, type, handler){
        //code removed for printing
    },
    getEvent: function(event){
        return event ? event : window.event;
    },
    getTarget: function(event){
        return event.target || event.srcElement;
    },
    preventDefault: function(event){
        if (event.preventDefault){
            event.preventDefault();
        } else {
            event.returnValue = false;
        }
    },
    removeHandler: function(element, type, handler){
        //code removed for printing
    },
    stopPropagation: function(event){
        if (event.stopPropagation){
            event.stopPropagation();
        } else {
            event.cancelBubble = true;
        }
    }
};
```

`EventUtil.js`

在此代码中，为 `EventUtil` 添加了四个新方法。第一个是 `getEvent()`，它返回事件对象的引用。由于事件对象的位置在 Internet Explorer 中不同，该方法可以用于无论使用何种事件处理器分配方法获取事件对象。使用此方法时，你必须假设事件对象传递到了事件处理器并将该变量传递给方法。这里有一个示例：

![image](img/logo1.gif)

```
btn.onclick = function(event){
    event = EventUtil.getEvent(event);
};
```

`CrossBrowserEventObjectExample01.htm`

当在符合 DOM 的浏览器中使用时，事件变量会被直接透传并返回。在 Internet Explorer 中，事件参数将为 `undefined`，因此会返回 `window.event`。在事件处理程序的开头添加此行代码可以确保无论使用哪种浏览器，事件对象始终可用。

第二种方法是 `getTarget()`，它返回事件的 Target。在方法内部，它会检查事件对象以查看 `target` 属性是否可用，如果是，则返回其值；否则，使用 `srcElement` 属性。该方法可以使用如下方式：

```javascript
btn.onclick = function(event){
    event = EventUtil.getEvent(event);
    var target = EventUtil.getTarget(event);
};
```

`CrossBrowserEventObjectExample01.htm`

第三种方法是 `preventDefault()`，它停止事件的默认行为。当传入事件对象时，会检查是否存在 `preventDefault()` 方法，如果是，则调用它。如果 `preventDefault()` 不可用，该方法将 `returnValue` 设置为 `false`。以下是一个示例：

```javascript
var link = document.getElementById("myLink");

link.onclick = function(event){
    event = EventUtil.getEvent(event);
    EventUtil.preventDefault(event);
};
```

`CrossBrowserEventObjectExample02.htm`

此代码防止在所有主流浏览器中点击链接时跳转到另一个页面。首先使用 `EventUtil.getEvent()` 获取事件对象，然后将其传递给 `EventUtil.preventDefault()` 以停止默认行为。

第四种方法 `stopPropagation()` 的工作原理类似。它首先尝试使用 DOM 方法来停止事件流，并在必要时使用 `cancelBubble`。以下是一个示例：

![image](img/logo1.gif)

```javascript
var btn = document.getElementById("myBtn");

btn.onclick = function(event){
    alert("Clicked");
    event = EventUtil.getEvent(event);
    EventUtil.stopPropagation(event);
};

document.body.onclick = function(event){
    alert("Body clicked");
};
```



`CrossBrowserEventObjectExample03.htm`

在这里，使用`EventUtil.getEvent()`获取事件对象，然后将其传递给`EventUtil.stopPropagation()`。请记住，根据浏览器，此方法可能会停止事件冒泡或同时停止事件冒泡和捕获。

## 事件类型

Web 浏览器中发生许多类别的事件。如前所述，触发的事件类型决定了关于该事件的可用信息。DOM Level 3 事件规定了以下事件组：

- 用户界面（UI）事件是通用的浏览器事件，可能与 BOM 有某些交互。
- 焦点事件（Focus events）在元素获得或失去焦点时触发。
- 鼠标事件（Mouse events）在使用鼠标在页面上执行操作时触发。
- 鼠标滚轮事件（Wheel events）在使用鼠标滚轮（或类似设备）时触发。
- 文本事件（Text events）在向文档中输入文本时触发。
- 键盘事件（Keyboard events）在使用键盘在页面上执行操作时触发。
- 输入法编辑器组合事件（Composition events）在为输入法编辑器（IME）输入字符时触发。
- 变异事件（Mutation events）在底层 DOM 结构发生变化时触发。
- 变异名称事件（Mutation name events）在元素或属性名称发生更改时触发。这些事件已废弃，且未被任何浏览器实现，因此在本章中特意省略了。

除了这些类别外，HTML5 定义了另一组事件，浏览器经常在 DOM 和 BOM 上都实现私有事件。这些私有事件通常由开发者需求而非规范驱动，因此在不同浏览器中的实现可能有所不同。

DOM Level 3 事件重新定义了 DOM Level 2 事件的分组并添加了额外的事件定义。所有主流浏览器都支持 DOM Level 2 事件，包括 Internet Explorer 9。Internet Explorer 9 也支持 DOM Level 3 事件。

## UI 事件

UI 事件是那些不一定与用户相关的事件。这些事件在 DOM 规范之前以前某种形式存在，并为了向后兼容而被保留。UI 事件如下：

- `DOMActivate` — 当元素通过某些用户操作（鼠标或键盘）被激活时触发（比`click`或`keydown`更通用）。该事件在 DOM Level 3 事件中已废弃，并在 Firefox 2+ 和 Chrome 中支持。由于跨浏览器实现差异，建议不要使用此事件。
- `load` — 当页面完全加载时，在`window`上触发；当所有帧完全加载时，在`frameset`上触发；当`<img>`元素完全加载时，在其上触发；当`<object>`元素完全加载时，在其上触发。
- `unload` — 当页面完全卸载时，在`window`上触发；当所有帧完全卸载时，在`frameset`上触发；当`<object>`元素完全卸载时，在其上触发。
- `abort` — 如果在用户停止下载过程之前`<object>`元素未完全加载，则触发。
- `error` — 当发生 JavaScript 错误时，在`window`上触发；如果指定的图像无法加载，在`<img>`元素上触发；如果`<object>`无法加载，在其上触发；如果一个或多个帧无法加载，在`frameset`上触发。此事件在第 17 章中讨论。
- `select` — 当用户在文本框（`<input>`或`<textarea>`）中选择一个或多个字符时触发。此事件在第 14 章中讨论。
- `resize` — 当`window`或`frame`调整大小时触发。
- `scroll` — 当用户滚动具有滚动条的元素时触发。`<body>`元素包含加载页面的滚动条。

大多数 HTML 事件要么与`window`对象相关，要么与表单控件相关。

除了`DOMActivate`外，这些事件都是 DOM Level 2 事件中的 HTML 组（`DOMActivate`属于 UI 事件）。要判断浏览器是否支持 DOM Level 2 事件定义的 HTML 事件，可以使用以下代码：

```javascript
var isSupported = document.implementation.hasFeature("HTMLEvents", "2.0");
```

注意，只有当浏览器根据 DOM Level 2 实现这些事件时才会返回 true。浏览器可能以非标准方式支持这些事件并返回 false。要判断浏览器是否支持 DOM Level 3 定义的事件，请使用：

```javascript
var isSupported = document.implementation.hasFeature("UIEvent", "3.0");
```

## `load`事件

`load`事件可能是 JavaScript 中最常用的事件。对于`window`对象，当整个页面加载完成（包括所有外部资源如图像、JavaScript 文件和 CSS 文件）时，触发`load`事件。可以通过两种方式定义`onload`事件处理器。第一种是使用 JavaScript，所示如下：

![image](img/logo1.gif)

```javascript
EventUtil.addHandler(window, "load", function(event) {
    alert("Loaded!");
});
```

这是使用 JavaScript 分配处理器的方法，使用了本章之前讨论的跨浏览器`EventUtil`对象。与其他事件一样，事件对象会被传递到事件处理器。此类事件对象不提供额外信息，但有趣的是，符合 DOM 的浏览器会将`event.target`设置为`document`，而 v8 之前的 Internet Explorer 不会为此事件设置`srcElement`属性。

分配`onload`事件处理器的另一种方法是在`<body>`元素上添加`onload`属性，如下所示：

```html
<!DOCTYPE html>
<html>
<head>
    <title>Load Event Example</title>
</head>
<body onload="alert('Loaded!')">
</body>
</html>
```

`LoadEventExample02.htm`

通常情况下，任何在窗口上发生的事件都可以通过`<body>`元素上的属性进行分配，因为在 HTML 中无法访问`window`元素。这实际上是为了向后兼容的一种变通方法（hack），但在所有浏览器中都得到了良好支持。建议尽可能使用 JavaScript 方法。

![image](img/pen.gif)

根据 DOM 2 级事件，`load`事件本应该在`document`上触发，而不是`window`上。然而，为了向后兼容，所有浏览器都在`window`上实现了`load`事件。

`load`事件也会在图像上触发，包括那些在 DOM 中的图像和不在 DOM 中的图像。你可以直接使用 HTML 为文档中的任何图像分配`onload`事件处理程序，代码如下所示：

```html
<img src="smile.gif" onload="alert('Image loaded.')">
```

### `LoadEventExample03.htm`

此示例在给定图像加载后会显示警框。也可以使用以下 JavaScript 代码来实现：

![image](img/logo1.gif)

```javascript
var image = document.getElementById("myImage");

EventUtil.addHandler(image, "load", function(event) {
    event = EventUtil.getEvent(event);
    alert(EventUtil.getTarget(event).src);
});
```

### `LoadEventExample04.htm`

在这里，使用 JavaScript 分配了`onload`事件处理程序。传入了事件对象，尽管它没有多少有用的信息。事件的目标是`<img>`元素，因此可以访问并显示其`src`属性。

创建新的`<img>`元素时，可以分配一个事件处理程序来指示图像何时加载。在这种情况下，在分配`src`属性之前分配事件是非常重要的，如下例所示：

```javascript
EventUtil.addHandler(window, "load", function() {
    var image = document.createElement("img");

    EventUtil.addHandler(image, "load", function(event) {
        event = EventUtil.getEvent(event);
        alert(EventUtil.getTarget(event).src);
    });

    document.body.appendChild(image);
    image.src = "smile.gif";
});
```

### `LoadEventExample05.htm`

此示例的第一部分是为`window`分配一个`onload`事件处理程序。由于示例涉及向 DOM 添加新元素，你必须确保页面已完全加载，因为在页面完全加载之前尝试操作`document.body`可能会导致错误。创建了一个新的图像元素并设置了它的`onload`事件处理程序。然后，将图像添加到页面并分配其`src`。请注意，图像下载不需要等待元素添加到文档即可开始；一旦`src`属性被设置，下载就会开始。

这种相同的技术也可以用于 DOM 0 级`Image`对象。在 DOM 出现之前，`Image`对象被用于在客户端预加载图像。它的用法方法与`<img>`元素相同，区别在于它不能被添加到 DOM 树中。考虑以下示例：

```javascript
EventUtil.addHandler(window, "load", function() {
    var image = new Image();

    EventUtil.addHandler(image, "load", function(event) {
        alert("Image loaded!");
    });

    image.src = "smile.gif";
});
```

### `LoadEventExample06.htm`

在这里，使用`Image`构造函数创建一个新图像并分配了事件处理程序。某些浏览器将`Image`对象实现为`<img>`元素，但并非所有都是如此，因此最好将它们视为独立的。

![image](img/pen.gif)

Internet Explorer 8 及更早版本在为非 DOM 文档部分的图像触发`load`事件时，不会生成事件对象。这既适用于从未被添加到文档的`<img>`元素，也适用于`Image`对象。这在 Internet Explorer 9 中得到了修复。

其他元素也以非标准的方式支持`load`事件。`<script>`元素在 Internet Explorer 9+、Firefox、Opera、Chrome 和 Safari 3+ 中会触发`load`事件，允许你确定动态加载的 JavaScript 文件何时完全加载。与图像不同，JavaScript 文件只有在分配了`src`属性并将元素添加到文档后才会开始下载，因此分配事件处理程序和`src`属性的顺序并不重要。下图图说明了如何为`<script>`元素分配事件处理程序：

![image](img/logo1.gif)

```javascript
EventUtil.addHandler(window, "load", function() {
    var script = document.createElement("script");
    script.type = "text/javascript";

    EventUtil.addHandler(script, "load", function(event) {
        alert("Loaded");
    });

    script.src = "example.js";
    document.body.appendChild(script);
});
```

### `LoadEventExample07.htm`

此示例使用跨浏览器`EventUtil`对象为新创建的`<script>`元素分配`onload`事件处理程序。在大多数浏览器中，事件对象的目标是`<script>`节点。Internet Explorer 8 及更早版本不支持`<script>`元素的`load`事件。

Internet Explorer 和 Opera 支持`<link>`元素的`load`事件，允许你确定样式表何时加载。例如：

```javascript
EventUtil.addHandler(window, "load", function() {
    var link = document.createElement("link");
    link.type = "text/css";
    link.rel = "stylesheet";

    EventUtil.addHandler(link, "load", function(event) {
        alert("css loaded");
    });

    link.href = "example.css";
    document.getElementsByTagName("head")[0].appendChild(link);
});
```

### `LoadEventExample07.html`

与`<script>`元素类似，样式表只有在分配了`href`属性并将元素添加到文档后才会开始下载。

## `unload`事件

作为`load`事件的对应，`unload`事件在文档完全卸载时触发。`unload`事件通常在页面间跳转时触发，通常用于清理引用以避免内存泄漏。与`load`事件类似，有两种方式分配`onunload`事件处理程序。一种是使用 JavaScript，如下所示：

```javascript
EventUtil.addHandler(window, "unload", function(event) {
    alert("Unloaded!");
});
```

在 DOM 标准浏览器中，该事件会生成事件对象，但除了`target`（设为`document`）之外没有包含其他有用的属性。

分配事件处理器的另一种方法（类似于`load`事件）是在`<body>`元素上添加属性，如下例所示：

![image](img/logo1.gif)

```html
<!DOCTYPE html>
<html>
<head>
    <title>Unload Example</title>
</head>
<body onunload="alert('Unloaded!')">
</body>
</html>
```

### `UnloadEvent01.htm`

无论你使用哪种方法，在使用`onunload`事件处理程序内部执行的代码要小心。由于`unload`事件在所有内容都卸载后触发，页面加载时某些对象可能不再可用。尝试操作 DOM 节点的位置或外观可能会导致错误。

![image](img/pen.gif)

根据 DOM 2 级事件，`unload`事件本应该在`<body>`上触发，而不是`window`上。然而，为了向后兼容，所有浏览器都在`window`上实现了`unload`事件。

## `resize`事件

当浏览器窗口大小调整为新的高度或宽度时，`resize`事件触发。该事件在`window`上触发，因此可以通过 JavaScript 或通过`<body>`元素上的`onresize`属性分配事件处理程序。如前所述，建议使用所示的 JavaScript 方法：

```javascript
EventUtil.addHandler(window, "resize", function(event) {
    alert("Resized");
});
```



与窗口上发生的其他事件类似，在 DOM 标准浏览器中会创建事件对象，其`target`为`document`，而 Internet Explorer 8 及更早版本不提供任何有用的属性。

不同浏览器之间触发`resize`事件的时机存在一些重要差异。Internet Explorer、Safari、Chrome 和 Opera 在浏览器窗口大小改变 1 像素时就会触发`resize`事件，并在用户调整浏览器窗口大小时反复触发该事件。而 Firefox 仅在用户停止调整浏览器窗口大小后才会触发`resize`事件。由于这些差异，您应该避免在该事件的事件处理程序中编写计算密集型代码，因为它们会被频繁执行，并导致浏览器明显变慢。

![image](img/pen.gif)

`resize`事件在浏览器窗口被最小化或最大化时也会触发。

## 滚动事件 (The Scroll Event)

尽管`scroll`事件发生在窗口上，但它实际上指的是相应的页面级元素的变化。在怪异模式（quirks mode）下，可以通过`<body>`元素的`scrollLeft`和`scrollTop`观察到变化；在标准模式（standards mode）下，除 Safari 以外的所有浏览器，变化都发生在`<html>`元素上（Safari 仍然在`<body>`上跟踪滚动位置）。例如：

![image](img/logo1.gif)

```
EventUtil.addHandler(window, "scroll", function(event){
    if (document.compatMode == "CSS1Compat"){
        alert(document.documentElement.scrollTop);
    } else {
        alert(document.body.scrollTop);
    }
});
```

`ScrollEventExample01.htm`

此代码分配了一个事件处理程序，根据渲染模式输出页面的垂直滚动位置。由于 Safari 3.1 之前不支持`document.compatMode`，旧版本会退回到第二种情况。

- 与`resize`类似，`scroll`事件在文档滚动时会反复触发，因此最好保持事件处理程序尽可能简单。

## 焦点事件 (Focus Events)

当页面元素获得或失去焦点时，会触发焦点事件。这些事件与`document.hasFocus()`和`document.activeElement`属性协同工作，以了解用户是如何导航页面的。共有六种焦点事件：

- `blur` — 当元素失去焦点时触发。此事件不冒泡，并在所有浏览器支持。
- `DOMFocusIn` — 当元素获得焦点时触发。这是`focus`HTML 事件的冒泡版本。Opera 是唯一支持此事件的主要浏览器。DOM Level 3 事件废弃了`DOMFocusIn`并取用`focusin`。
- `DOMFocusOut` — 当元素失去焦点时触发。这是`blur`HTML 事件的通用版本。Opera 是唯一支持此事件的主要浏览器。DOM Level 3 事件废弃了`DOMFocusOut`并取用`focusout`。
- `focus` — 当元素获得焦点时触发。此事件不冒泡，并在所有浏览器支持。
- `focusin` — 当元素获得焦点时触发。这是`focus`HTML 事件的冒泡版本，并在 Internet Explorer 5.5+、Safari 5.1+、Opera 11.5+ 以及 Chrome 中。
- `focusout` — 当元素失去焦点时触发。这是`blur`HTML 事件的通用版本，并在 Internet Explorer 5.5+、Safari 5.1+、Opera 11.5+ 以及 Chrome 中。

组中的两个主要事件是`focus`和`blur`，它们从 JavaScript 早期起一直被浏览器支持。这些事件最大的问题之一是它们不冒泡。这导致了 Internet Explorer 引入了`focusin`和`focusout`，以及 Opera 引入了`DOMFocusIn`和`DOMFocusOut`。Internet Explorer 的方法已经在 DOM Level 3 事件中标准化。

当焦点从页面上的一个元素移动到另一个元素时，遵循以下事件顺序：

1. `focusout`在失去焦点的元素上触发。
2. `focusin`在获得焦点的元素上触发。
3. `blur`在失去焦点的元素上触发。
4. `DOMFocusOut`在失去焦点的元素上触发。
5. `focus`在获得焦点的元素上触发。
6. `DOMFocusIn`在获得焦点的元素上触发。

`blur`、`DOMFocusOut`和`focusout`的事件目标是失去焦点的元素，而`focus`、`DOMFocusIn`和`focusin`的事件目标是获得焦点的元素。

您可以通过以下代码判断浏览器是否支持这些事件：

```
var isSupported = document.implementation.hasFeature("FocusEvent", "3.0");
```

![image](img/pen.gif)

尽管`focus`和`blur`不冒泡，但它们可以在捕获阶段被监听。Peter-Paul Koch 在此主题上有一篇非常好的文章：[www.quirksmode.org/blog/archives/2008/04/delegating_the.html](http://www.quirksmode.org/blog/archives/2008/04/delegating_the.html)。

## 鼠标和滚动事件 (Mouse and Wheel Events)

鼠标事件是 Web 上最常用的事件组，因为鼠标是主要的导航设备。DOM Level 3 事件定义了九种鼠标事件。它们如下：

- `click` — 当用户点击主鼠标键（通常是左键）或当用户按下回车键时触发。对于可访问性来说这是一个重要事实，因为`onclick`事件处理程序可以使用键盘和鼠标执行。
- `dblclick` — 当用户双击主鼠标键（通常是左键）时触发。此事件在 DOM Level 2 事件中未定义。
- `mousedown` — 当按下任何鼠标键时触发。
- `mouseenter` — 当鼠标指针从元素边界之外移动到元素内部时触发。事件不冒泡，且在移动到子元素时不会触发。此事件在 DOM Level 2 事件中未定义，但在 DOM Level 3 事件中已添加。
- `mouseleave` — 当鼠标指针从元素内部移动到边界之外时触发。此事件不冒泡，且在移出子元素时不会触发。此事件在 DOM Level 2 事件中未定义，但在 DOM Level 3 事件中已添加。
- `mousemove` — 当鼠标指针在元素周围移动时反复触发。
- `mouseout` — 当鼠标指针从一个元素移动到另一个元素时触发。目标元素可能是原元素的外部，也可能是原元素的子。
- `mouseover` — 当鼠标指针从元素边界之外移动到元素内部时触发。
- `mouseup` — 当用户释放鼠标键时触发。

页面上的所有元素都支持鼠标事件。除了`mouseenter`和`mouseleave`之外，所有鼠标事件都会冒泡，并且都可以被取消，这会影响浏览器的默认行为。由于事件之间的关系，取消鼠标事件的默认行为可能会影响其他事件。

`click`事件只有在触发了`mousedown`事件并在在同一元素上随后触发了`mouseup`事件后才能触发；如果取消了`mousedown`或`mouseup`，则`click`事件将不会触发。同样，需要两次`click`事件才能触发`dblclick`事件。如果任何情况阻止了这两个`click`事件的触发（取消其中一个`click`事件或取消任何`mousedown`或`mouseup`），则`dblclick`事件将不会触发。这四个鼠标事件总是按照以下顺序触发：

1. `mousedown`
2. `mouseup`
3. `click`
4. `mousedown`
5. `mouseup`
6. `click`
7. `dblclick`

Internet Explorer 直到 8 版本有一个微小的实现 Bug，在双击期间会跳过第二个`mousedown`和`click`事件。顺序为：

## 鼠标事件

1. `mousedown`
2. `mouseup`
3. `click`
4. `mouseup`
5. `dblclick`

Internet Explorer 9 修复了此 Bug，使得事件顺序是正确的。

你可以使用以下代码来判断是否支持 DOM Level 2 事件（上述列出的事件但不包括`dblclick`、`mouseenter`和`mouseleave`）：

```
var isSupported = document.implementation.hasFeature("MouseEvents", "2.0");
```

要判断浏览器是否支持上述所有的所有的事件，请使用以下代码：

```
var isSupported = document.implementation.hasFeature("MouseEvent", "3.0")
```

请注意，DOM Level 3 的特性名称为`"MouseEvent"`而不是`"MouseEvents"`。

还有一组称为`wheel events`（滚轮事件）的鼠标事件。滚轮事件实际上只是单一事件`mousewheel`，它监控鼠标滚轮或类似设备（如 Mac 触摸板）的交互。

## 客户端坐标 (Client Coordinates)

鼠标事件均发生在浏览器视口内的特定位置。这些信息存储在事件对象的`clientX`和`clientY`中。这些属性表示事件发生时鼠标光标在视口中的位置，并被所有浏览器支持。图 13-4 展示了视口中的客户端坐标。

图 13-4

![image](img/f461-01.jpg)

你可以通过以下方式获取鼠标事件的客户端坐标：

![image](img/logo1.gif)

```
var div = document.getElementById("myDiv");
EventUtil.addHandler(div, "click", function(event){
    event = EventUtil.getEvent(event);
    alert("Client coordinates: " + event.clientX + "," + event.clientY);        
});
```

`ClientCoordinatesExample01.htm`

此示例为`<div>`元素分配了一个`onclick`事件处理器。当元素被点击时，会显示事件的客户端坐标。请记住，这些坐标没有考虑页面的滚动位置，因此这些数字并不指示光标在页面上的位置。

## 页面坐标 (Page Coordinates)

如果说客户端坐标提供了事件发生在视口何处的信息，那么页面坐标则通过事件对象的`pageX`和`pageY`属性告诉你事件发生在页面的什么位置。这些属性表示鼠标光标在页面上的位置，因此坐标相对于页面自身的左侧和顶部而非视口。

你可以通过以下方式获取鼠标事件的页面坐标：

![image](img/logo1.gif)

```
var div = document.getElementById("myDiv");
EventUtil.addHandler(div, "click", function(event){
    event = EventUtil.getEvent(event);
    alert("Page coordinates: " + event.pageX + "," + event.pageY);        
});
```

`PageCoordinatesExample01.htm`

当页面未滚动时，`pageX`和`pageY`的值与`clientX`和`clientY`相同。

Internet Explorer 8 及之前的版本不支持事件对象的页面坐标，但你可以使用客户端坐标和滚动信息来计算它们。你需要使用`document.body`（在怪异模式下）或`document.documentElement`（在标准模式下）上的`scrollLeft`和`scrollTop`属性。计算方式如下：

```
var div = document.getElementById("myDiv");
EventUtil.addHandler(div, "click", function(event){
    event = EventUtil.getEvent(event);
    var pageX = event.pageX,
        pageY = event.pageY;
    if (pageX === undefined){
        pageX = event.clientX + (document.body.scrollLeft || 
                document.documentElement.scrollLeft);
    }
    if (pageY === undefined){
        pageY = event.clientY + (document.body.scrollTop || 
                document.documentElement.scrollTop);
    }
    alert("Page coordinates: " + pageX + "," + pageY);        
});
```

`PageCoordinatesExample01.htm`

## 屏幕坐标 (Screen Coordinates)

鼠标事件不仅相对于浏览器窗口发生，还相对于整个屏幕。通过`screenX`和`screenY`属性可以确定鼠标相对于整个屏幕的位置。图 13-5 展示了浏览器中的屏幕坐标。

图 13-5

![image](img/f463-01.jpg)

你可以通过以下方式获取鼠标事件的屏幕坐标：

![image](img/logo1.gif)

```
var div = document.getElementById("myDiv");
EventUtil.addHandler(div, "click", function(event){
    event = EventUtil.getEvent(event);
    alert("Screen coordinates: " + event.screenX + "," + event.screenY);        
});
```

`ScreenCoordinatesExample01.htm`

与之前的示例类似，此代码为`<div>`元素分配了一个`onclick`事件处理器。当元素被点击时，会显示事件的屏幕坐标。

## 修饰键 (Modifier Keys)

尽管鼠标事件主要通过使用鼠标触发，但某些键盘键的状态对于确定要执行的操作可能非常重要。修饰键`Shift`、`Ctrl`、`Alt`和`Meta`经常用于改变鼠标事件的行为。DOM 指定了指示这些修饰键状态的属性：`shiftKey`、`ctrlKey`、`altKey`和`metaKey`。每个属性都包含一个布尔值，如果按下则为 true，未按下则为 false。当鼠标事件发生时，你可以通过检查这些属性确定各种键的状态。考虑以下示例：

```
var div = document.getElementById("myDiv");
EventUtil.addHandler(div, "click", function(event){
    event = EventUtil.getEvent(event);
    var keys = new Array();
    if (event.shiftKey){
        keys.push("shift");
    }
    if (event.ctrlKey){
        keys.push("ctrl");
    }
    if (event.altKey){
        keys.push("alt");
    }
    if (event.metaKey){
        keys.push("meta");
    }
    alert("Keys: " + keys.join(","));
});
```



# `ModifierKeysExample01.htm`

在此示例中，`onclick` 事件处理器检查修饰键的状态。`keys` 数组包含了按下的修饰键名称。对于每个为 true 的属性，键名会被添加到 `keys` 中。在事件处理器结束时，会在框中显示键。

![image](img/pen.gif)

Internet Explorer 9、Firefox、Safari、Chrome 和 Opera 支持所有的键。Internet Explorer 8 及之前的版本不支持 `metaKey` 属性。

## 相关元素 (Related Elements)

对于 `mouseover` 和 `mouseout` 事件，存在与事件相关的其他元素。这两个事件都涉及鼠标光标从一个元素的边界移动到另一个元素的边界。对于 `mouseover` 事件，事件的主目标是获取光标的元素，相关元素是丢失光标的元素。同样，对于 `mouseout`，目标是丢失光标的元素，相关元素是获取光标的元素。考虑以下示例：

![image](img/logo1.gif)

```
<!DOCTYPE html>
<html>
<head>
    <title>Related Elements Example</title>
</head>
<body>
    <div id="myDiv" style="background-color:red;height:100px;width:100px;</div>>
</body>
</html>
```

`RelatedElementsExample01.htm`

此页面在页面上渲染了单个 `<div>`。如果鼠标光标从 `<div>` 上开始并移动到外部，则会在 `<div>` 上触发 `mouseout` 事件，相关元素是 `<body>` 元素。同时，会在 `<body>` 上触发 `mouseover` 事件，相关元素是 `<div>`。

DOM 通过事件对象上的 `relatedTarget` 属性提供了有关相关元素的信息。该属性仅在 `mouseover` 和 `mouseout` 事件中包含值；对于所有其他事件，它为 `null`。Internet Explorer 8 及更版本不支持 `relatedTarget` 属性，但可以使用其他属性对相关元素进行类似的访问。当 `mouseover` 事件触发时，Internet Explorer 提供一个包含相关元素的 `fromElement` 属性；当 `mouseout` 事件触发时，Internet Explorer 提供一个包含相关元素的 `toElement` 属性（Internet Explorer 9 支持所有属性）。可以像这样向 `EventUtil` 添加一个获取相关元素的跨浏览器方法：

![image](img/logo1.gif)

```javascript
var EventUtil = {
    //more code here
    getRelatedTarget: function(event){
        if (event.relatedTarget){
            return event.relatedTarget;
        } else if (event.toElement){
            return event.toElement;
        } else if (event.fromElement){
            return event.fromElement;
        } else {
            return null;
        }
    },
    //more code here    
};
```

`EventUtil.js`

与之前的跨浏览器方法一样，这种方法使用特性检测来确定返回哪个值。`EventUtil.getRelatedTarget()` 方法可以如下使用：

```javascript
var div = document.getElementById("myDiv");
EventUtil.addHandler(div, "mouseout", function(event){
    event = EventUtil.getEvent(event);
    var target = EventUtil.getTarget(event);
    var relatedTarget = EventUtil.getRelatedTarget(event);
    alert("Moused out of " + target.tagName + " to " + relatedTarget.tagName);   
});
```

`RelatedElementsExample01.htm`

此示例为 `<div>` 元素注册了 `mouseout` 事件的句程序。当事件触发时，会显示一个警框，指示鼠标离开的位置和进入的位置。

### 按钮 (Buttons)

`click` 事件只有在点击元素的主鼠标按钮时（或按下键盘上的 Enter 键时）才会触发，因此不需要按钮信息。对于 `mousedown` 和 `mouseup` 事件，事件对象上有一个 `button` 属性，用于指示按下或释放的按钮。DOM `button` 属性有以下三个可能的值：`0` 表示主鼠标按钮，`1` 表示中间鼠标按钮（通常是滚轮按钮），`2` 表示次鼠标按钮。在传统设置中，主鼠标按钮是左键，次按钮是右键。

从版本 8 的 Internet Explorer 也提供了一个 `button` 属性，但其值完全不同，描述如下：

- `0` 表示没有按下任何按钮。
- `1` 表示按下了主鼠标按钮。
- `2` 表示按下了次鼠标按钮。
- `3` 表示主按钮和次按钮都已按下。
- `4` 表示按下了中间按钮。
- `5` 表示主按钮和中间按钮已按下。
- `6` 表示次按钮和中间按钮已按下。
- `7` 表示三个按钮都已按下。

如你所见，`button` 属性的 DOM 模型比 Internet Explorer 模型简单得多，而且可以说更有用，因为多键鼠标的使用非常稀少。将模型归一化为 DOM 方法是典型的做法，因为除了 Internet Explorer 8 及更版本外，所有浏览器都原生实现了它。主键、中键和次键的映射非常直接；所有其他 Internet Explorer 选项将翻译为按下其中一个按钮，并且在所有情况下都以主键为优先。因此，如果 Internet Explorer 返回 `5` 或 `7`，它在 DOM 模型中将转换为 `0`。

由于仅通过能力检测无法判断差异（因为两者都具有 `button` 属性），你必须使用另一种方法。支持 DOM 版本鼠标事件的浏览器可以使用 `hasFeature()` 方法进行检测，因此在 `EventUtil` 上编写一个归一化的 `getButton()` 方法可以如下所示：

![image](img/logo1.gif)

```javascript
var EventUtil = {
    //more code here
    getButton: function(event){
        if (document.implementation.hasFeature("MouseEvents", "2.0")){
            return event.button;
        } else {
            switch(event.button){
                case 0:
                case 1:
                case 3:
                case 5:
                case 7:
                    return 0;
                case 2:
                case 6:
                    return 2;
                case 4: 
                    return 1;
            }
        }
    },
    //more code here
};
```

`EventUtil.js`

检查特性 `"MouseEvents"` 用于判断事件中已有的 `button` 属性是否包含正确的值。如果测试失败，则该浏览器可能是 Internet Explorer，必须对值进行归一化。该方法可以如下使用：

![image](img/logo1.gif)

```javascript
var div = document.getElementById("myDiv");
EventUtil.addHandler(div, "mousedown", function(event){
    event = EventUtil.getEvent(event);
    alert(EventUtil.getButton(event));       
});
```

`ButtonExample01.htm`

在此示例中，为 `<div>` 元素添加了一个 `onmousedown` 事件处理器。当按下元素上的鼠标按钮时，警框会显示该按钮的代码。

![image](img/pen.gif)

注意，当与 `onmouseup` 事件处理器配合使用，`button` 的值刚刚释放的按钮。

### 额外的事件信息 (Additional Event Information)

DOM Level 2 事件规范在事件对象上提供了 `detail` 属性，用于提供事件的额外信息。对于鼠标事件，`detail` 包含一个数字，表示点击发生的次数。点击被视为在同一位置发生 `mousedown` 事件后跟随 `mouseup` 事件。`detail` 的值从 1 开始，每发生一次点击加 1。如果鼠标在 `mousedown` 和 `mouseup` 之间移动，则 `detail` 将重置为 0。

Internet Explorer 还为每个鼠标事件提供了以下额外信息：

- `altLeft` 是一个布尔值，表示左 Alt 键按下。如果 `altLeft` 为 true，则 `altKey` 也为 true。
- `ctrlLeft` 是一个布尔值，表示左 Ctrl 键按下。如果 `ctrlLeft` 为 true，则 `ctrlKey` 也为 true。
- `offsetX` 是鼠标相对于元素边界的 x 坐标。
- `offsetY` 是鼠标相对于元素边界的 y 坐标。
- `shiftLeft` 是一个布尔值，表示左 Shift 键按下。如果 `shiftLeft` 为 true，则 `shiftKey` 也为 true。

这些属性的价值有限，因为它们仅在 Internet Explorer 中可用，且提供的信息并非必须，或者可以通过其他方式计算。

### mousewheel 事件 (mousewheel Event)

Internet Explorer 6 首次实现了 `mousewheel` 事件。从那时起，Opera、Chrome 和 Safari 也引入了它。当用户与鼠标滚轮交互并在垂直方向滚动时，会触发 `mousewheel` 事件。该事件在每个元素上触发并冒泡到 `document`（Internet Explorer 8）和 `window`（Internet Explorer 9+,Opera、Chrome 和 Safari）。`mousewheel` 事件对象包含所有鼠标事件的标准信息，以及一个名为 `wheelDelta` 的额外属性。当鼠标滚轮向前滚动时，`wheelDelta` 是 120 的正倍数；当鼠标滚轮向后滚动时，`wheelDelta` 是 120 的负倍数。见图 13-6。

可以将 `onmousewheel` 事件处理程序分配给页面上的任何元素或文档，以处理所有的鼠标滚轮交互。以下是一个示例：

```
EventUtil.addHandler(document, "mousewheel", function(event){
    event = EventUtil.getEvent(event);
    alert(event.wheelDelta);
});
```

此示例在事件触发时仅简单显示 `wheelDelta` 值。在大多数情况下，你只需要知道鼠标滚轮向哪个方向旋转，这可以通过 `wheelDelta` 值的正负号轻松判断。

有一点需要注意：在版本 9.5 之前的 Opera 中，`wheelDelta` 的值是反反的。如果你计划支持早期版本的 Opera，则需要使用浏览器检测来确定实际值，如下例所示：

![image](img/logo1.gif)

```
EventUtil.addHandler(document, "mousewheel", function(event){
    event = EventUtil.getEvent(event);
    var delta = (client.engine.opera && client.engine.opera < 9.5 ? 
                 -event.wheelDelta : event.wheelDelta);
    alert(delta);
});
```

`MouseWheelEventExample01.htm`

此代码使用了第 9 章中创建的 `client` 对象来检查浏览器是否为早期版本的 Opera。

![image](img/pen.gif)

`mousewheel` 事件被添加到 HTML5 中，反映了它在大多数浏览器中的普及性和可用性。

Firefox 支持一个名为 `DOMMouseScroll` 的类似事件，该事件在鼠标滚轮旋转时触发。与 `mousewheel` 一样，该事件被视为鼠标事件，并具有所有的常规鼠标事件属性。关于鼠标滚轮的信息在 `detail` 属性中，当滚轮向鼠标前方滚动时，该值为 3 的负倍数；当向鼠标后方滚动时，值为 3 的正倍数。参见图 13-7。

FIGURE 13-7

![image](img/f469-01.jpg)

`DOMMouseScroll` 事件可以附加到页面上的任何元素，并冒泡到 window 对象。你可以像下面的例一样附加事件处理程序：

```
EventUtil.addHandler(window, "DOMMouseScroll", function(event){
    event = EventUtil.getEvent(event);
    alert(event.detail);
});
```

`DOMMouseScrollEventExample01.htm`

这个简单的事件处理程序在每次滚动鼠标滚轮时都会输出 `detail` 属性的值。

为了实现跨浏览器解决方案，第一步是创建一个可以获取鼠标滚轮增量归一化值的方法。可以如下所示将其添加到 `EventUtil` 对象中：

```
var EventUtil = {
    //更多代码在此
    getWheelDelta: function(event){
        if (event.wheelDelta){
            return (client.engine.opera && client.engine.opera < 9.5 ? 
                    -event.wheelDelta : event.wheelDelta);
        } else {
            return -event.detail * 40;
        }
    },
    //更多代码在此
};
```

`EventUtil.js`

`getWheelDelta()` 方法检查事件对象是否具有 `wheelDelta` 属性，如果是，则使用浏览器检测代码来确定正确的值。如果 `wheelDelta` 不存在，则假设值在 `detail` 属性中。由于 Firefox 的值不同，因此首先对其取反，然后乘以 40，以确保其值与其他浏览器相同。完成此方法后，你可以将相同的事件处理程序同时分配给 `mousewheel` 和 `DOMMouseScroll`，如下所示：

![image](img/logo1.gif)

```
(function(){
    function handleMouseWheel(event){
        event = EventUtil.getEvent(event);
        var delta = EventUtil.getWheelDelta(event);
        alert(delta);
    }
    EventUtil.addHandler(document, "mousewheel", handleMouseWheel);
    EventUtil.addHandler(document, "DOMMouseScroll", handleMouseWheel);
})();
```




`CrossBrowserMouseWheelExample01.htm`

此代码存在于私有作用域内，以免用额外的函数污染全局作用域。`handleMouseWheel()` 函数是两个事件的事件处理程序。（当将事件处理程序分配给一个不存在的事件时，赋值会静默失败。）使用 `EventUtil.getWheelDelta()` 方法允许事件处理程序在两种情况下都能无缝工作。

### 触摸设备支持

运行 iOS 或 Android 的触摸设备具有有趣的实现方式，因为当然，没有鼠标可以进行交互。在为触摸设备开发时，请记住以下几点：

- 完全不支持 `dblclick` 事件。在浏览器窗口上双击会放大，且没有方法可以覆盖该行为。
- 点击可点击元素会导致 `mousemove` 事件触发。如果内容由于此操作而发生变化，则不会触发后续事件；如果屏幕没有发生变化，则 `mousedown`、`mouseup` 和 `click` 事件将按顺序触发。点击不可点击元素时不会触发任何事件。可点击元素定义为那些点击时具有默认操作的元素（如链接）或分配了 `onclick` 事件处理程序的元素。
- `mousemove` 事件还会触发 `mouseover` 和 `mouseout` 事件。
- 当手指在屏幕上导致页面滚动时会触发 `mousewheel` 和 `scroll` 事件。

### 无障碍问题

如果你的网络应用程序或网站必须对残障人士（特别是使用屏幕阅读器的用户）可用，那么在使用鼠标事件时需要小心。以下是使用鼠标事件的一些建议：

- 使用 `click` 执行代码。有些人认为使用 `mousedown` 执行代码会感觉更快，这对于视力用户是事实。但对于屏幕阅读器，这种代码是不可用的，因为无法触发 `mousedown` 事件。
- 避免使用 `mouseover` 显示新选项。再次，屏幕阅读器没有触发此事件的方法。如果你必须这样做显示新选项，请考虑添加快捷键来显示相同的信息。
- 避免使用 `dblclick` 执行重要操作。键盘无法触发此事件。

遵循这些简单的提示可以大大提高网络应用程序或网站的无障碍性。

![image](img/pen.gif)

要了解更多关于网页无障碍的知识，请访问 [www.webaim.org](http://www.webaim.org) 和 [`accessibility.yahoo.com`](http://accessibility.yahoo.com)。

### 键盘和文本事件

当用户与键盘交互时会触发键盘事件。DOM Level 2 事件规范了键盘事件，但在规范确定之前该部分已被删除。因此，键盘事件很大程度上基于原始的 DOM Level 0 实现。

DOM Level 3 事件提供了键盘事件规范，该规范在 Internet Explorer 9 中首次完全实现。其他浏览器也开始工作实现该标准，但仍有很多遗留实现。

有三种键盘事件，描述如下：

- `keydown` —— 当用户按下键盘按键时触发，并在按住时重复触发。
- `keypress` —— 当用户按下产生字符的键盘按键时触发，并在按住时重复触发。该事件也会触发 Esc 键。DOM Level 3 事件弃用了 `keypress` 事件，取而代之的是 `textInput` 事件。
- `keyup` —— 当用户释放键盘按键时触发。

这些事件在用户在文本框输入时最容易观察到，尽管所有元素都支持它们。

只有一个文本事件，其名为 `textInput`。该事件是按键事件（`keypress`）的增强，旨在以便在文本显示给用户之前更容易拦截文本输入。`textInput` 事件在文本插入到文本框正之前触发。

当用户在键盘上按一次字符键时，首先触发 `keydown` 事件，接着是 `keypress` 事件，然后是 `keyup` 事件。请注意，`keydown` 和 `keypress` 都在文本框发生任何变化之前触发，而 `keyup` 事件在文本框发生变化之后（此处原文应为在文本框发生变化后）触发。如果按下并按住字符键，`keydown` 和 `keypress` 将重复触发，直到释放按键为止。

对于非字符键，在键盘上按一次按键会触发 `keydown` 事件，紧接着触发 `keyup` 事件。如果按住非字符键，`keydown` 事件会重复触发，直到释放按键，此时触发 `keyup` 事件。

![image](img/pen.gif)

键盘事件支持与鼠标事件相同的修饰键集。`shiftKey`、`ctrlKey`、`altKey` 和 `metaKey` 属性均适用于键盘事件。Internet Explorer 8 及更早版本不支持 `metaKey`。

### 键码（Key Codes）

对于 `keydown` 和 `keyup` 事件，事件对象的 `keyCode` 属性被填充为映射到键盘上特定键的代码。对于字母数字键，`keyCode` 与该键上小写字母或数字的 ASCII 值相同，因此 `7` 键的 `keyCode` 为 `55`，`A` 键的 `keyCode` 为 `65`，无论 `Shift` 键如何。DOM 和 Internet Explorer 事件对象都支持 `keyCode` 属性。以下是一个示例：

![image](img/logo1.gif)

```javascript
var textbox = document.getElementById("myText");

EventUtil.addHandler(textbox, "keyup", function(event){

    event = EventUtil.getEvent(event);

    alert(event.keyCode);     

});
```

`KeyUpEventExample01.htm`

在此示例中，每当触发 `keyup` 事件时，都会显示 `keyCode`。非字符键的键码完整列表如表所示。

![image](img/f472-01.jpg)

![image](img/f473-01.jpg)

关于 `keydown` 和 `keyup` 事件有一个异常情况。Firefox 和 Opera 返回的分号键 `keyCode` 为 `59`（这是分号的 ASCII 码），而 Internet Explorer、Chrome 和 Safari 返回的 `186`（这是键盘按键的代码）。

### 字符码（Character Codes）

当发生 `keypress` 事件时，意味着按键影响了屏幕上文本的显示。所有浏览器都会为插入或删除字符的按键触发 `keypress` 事件；其他按键取决于浏览器。由于 DOM Level 3 事件规范才开始实现，不同浏览器之间存在显著的实现差异。

Internet Explorer 9+、Firefox、Chrome 和 Safari 支持事件对象上的名为 `charCode` 的属性，该属性仅在 `keypress` 事件时填充，并包含与所按按键相关的字符的 ASCII 码。在这种情况下，`keyCode` 通常等于 `0`，也可能等于所按按键的键码。Internet Explorer 8 及更早版本以及 Opera 使用 `keyCode` 来传递字符的 ASCII 码。因此，为了以跨浏览器的方式获取字符码，你必须首先检查是否使用了 `charCode` 属性，如果没有使用，则使用 `keyCode`，如下例所示：

![image](img/logo1.gif)

```javascript
var EventUtil = {

    //更多代码在此

    getCharCode: function(event){

        if (typeof event.charCode == "number"){

            return event.charCode;

        } else {

            return event.keyCode;

        }

    },

    //更多代码在此

};
```

`EventUtil.js`

该方法检查 `charCode` 属性是否为数字（对于不支持的浏览器，它为 `undefined`），如果是，则返回该值。否则，返回 `keyCode` 值。该方法可以使用如下方式：

```javascript
var textbox = document.getElementById("myText");

EventUtil.addHandler(textbox, "keypress", function(event){

    event = EventUtil.getEvent(event);

    alert(EventUtil.getCharCode(event));     

});
```

`KeyPressEventExample01.htm`

一旦获取了字符码，就可以使用 `String.fromCharCode()` 方法将其转换为实际字符。

### DOM Level 3 变化

尽管所有浏览器都实现了某种形式的键盘事件，但 DOM Level 3 事件发生了多处更改。例如，`charCode` 属性并不是键盘事件 DOM Level 3 事件规范的一部分。相反，规范定义了两个额外的属性：`key` 和 `char`。

`key` 属性旨在替代 `keyCode` 并包含一个字符串。当按下字符键时，`key` 的值等于文本字符（例如，“k”或“M”）；当按下非字符键时，`key` 的值为按键的名称（例如，“Shift”或“Down”）。`char` 属性在按下字符键时的行为与 `key` 相同，并在按下非字符键时设置为 `null`。

Internet Explorer 9 支持 `key` 属性但不支持 `char` 属性。Safari 5 和 Chrome 支持一个名为 `keyIdentifier` 的属性，在非字符键情况下返回与 `key` 相同的值。对于字符键，`keyIdentifier` 返回以“U+0000”格式表示的值。

![image](img/logo1.gif)

```javascript
var textbox = document.getElementById("myText");

EventUtil.addHandler(textbox, "keypress", function(event){

    event = EventUtil.getEvent(event);

    var identifier = event.key || event.keyIdentifier;

    if (identifier){

        alert(identifier);    

    }

});
```

`DOMLevel3KeyPropertyExample01.htm`

由于缺乏跨浏览器支持，建议使用 `key`、`keyIdentifier` 或 `char`。

DOM Level 3 事件还添加了一个名为 `location` 的属性，这是一个指示按键位置的数值。可能的值有：`0` 代表默认，`1` 代表左侧（例如左 Alt），`2` 代表右侧（例如右 Shift），`3` 代表数字键盘，`4` 代表移动端（指示虚拟键盘），或 `5` 代表摇杆（例如 Wii 控制器）。Internet Explorer 9 支持此属性。Safari 5 和 Chrome 支持一个相同的属性 `keyLocation`，但由于 Bug，除非按键在数字键盘上（此时为 `3`），否则该值始终为 `0`；它永远不会为 `1`、`2`、`4` 或 `5`。

```javascript
var textbox = document.getElementById("myText");

EventUtil.addHandler(textbox, "keypress", function(event){

    event = EventUtil.getEvent(event);

    var loc = event.location || event.keyLocation;

    if (loc){

        alert(loc);    

    } 

});
```

`DOMLevel3LocationPropertyExample01.htm`

与 `key` 属性一样，`location` 属性并未广泛支持，因此不建议在跨浏览器开发中使用。

对象的最后一个添加是 `getModifierState()` 方法。该方法接受单个参数，即等于 `Shift`、`Control`、`Alt`、`AltGraph` 或 `Meta` 的字符串，指示要检查的修饰键。如果给定的修饰键处于激活（按下），则返回 `true`，否则返回 `false`：

![image](img/logo1.gif)

```javascript
var textbox = document.getElementById("myText");

EventUtil.addHandler(textbox, "keypress", function(event){

    event = EventUtil.getEvent(event);

    if (event.getModifierState){

        alert(event.getModifierState("Shift"));    

    } 

});
```

`DOMLevel3LocationGetModifierStateExample01.htm`

你已经可以使用事件对象上的 `shiftKey`、`altKey`、`ctrlKey` 和 `metaKey` 属性来获取部分此类信息。Internet Explorer 9 是唯一支持 `getModifierState()` 方法的浏览器。

DOM Level 3 事件规范引入了一个名为 `textInput` 的事件，该事件在可编辑区域输入字符时触发。它被设计为 `keypress` 的替代品，但 `textInput` 事件的行为略有不同。不同之处在于，`keypress` 在任何可以获取焦点的元素上触发，而 `textInput` 仅在可编辑区域触发。另一个区别是，`textInput` 只对会导致插入新字符的按键触发，而 `keypress` 则会对任何影响文本的按键触发（包括 Backspace）。

由于 `textInput` 事件主要关注字符，它在事件对象上提供了一个 `data` 属性，其中包含插入的字符（而不是字符代码）。`data` 的值始终是插入的精确字符，因此，如果没有按下 Shift 就按下 `S` 键，`data` 为 "s"，但如果在按住 Shift 的情况下按下同一个键，则 `data` 为 "S"。

`textInput` 事件可以如下使用：

```javascript
var textbox = document.getElementById("myText");

EventUtil.addHandler(textbox, "textInput", function(event){

    event = EventUtil.getEvent(event);

    alert(event.data);     

});
```

`TextInputEventExample01.htm`

在此示例中，插入到文本框中的字符将显示在警框中。

事件对象上还有另一个属性名为 `inputMethod`，它指示文本输入到控件的方式。可能的值有：

- `0` 表示浏览器无法确定输入方式。
- `1` 表示使用了键盘。
- `2` 表示文本是粘贴的。
- `3` 表示文本是作为拖放操作的一部分落入的。
- `4` 表示文本是使用 IME（输入法编辑器）输入的。
- `5` 表示文本是通过在表单中选择选项输入的。
- `6` 表示文本是通过手写输入的（例如使用手写笔）。
- `7` 表示文本是通过语音命令输入的。
- `8` 表示文本是通过多种方法的组合输入的。
- `9` 表示文本是通过脚本输入的。

使用此属性，你可以确定文本是如何输入到控件的，用以验证其有效性。

`textInput` 事件在 Internet Explorer 9+、Safari 和 Chrome 中受支持。只有 Internet Explorer 支持 `inputMethod` 属性。

### 设备上的键盘事件

当按下 Wii 遥控器上的按钮时，Nintendo Wii 会触发键盘事件。虽然你无法访问 Wii 遥控器所有的按钮，但有几个按钮会触发键盘事件。图 13-8 显示了表示特定按钮按下的键码。

图 13-8

![image](img/f477-01.jpg)

当按下交叉方向（键码 175–178）、减（170）、加（174）、1（172）或 2（173）按钮时，会触发键盘事件。无法判断是否按过电源按钮、A、B 或 Home 按钮。

iOS Safari 和 Android WebKit 使用屏幕键盘时会触发键盘事件。

### 组合事件

组合事件首次在 DOM Level 3 事件中引入，用于处理通常出现在 IME 中的复杂输入序列。IME 允许用户输入物理键盘上不存在的字符。例如，使用字母键盘的用户仍然可以在计算机输入日语字符。IME 通常需要同时按下多个键，但最终只输入一个字符。组合事件有助于检测和处理此类输入。有三种组合事件：

- `compositionstart` — 当 IME 的文本组合系统打开时触发，表示输入即将开始。
- `compositionupdate` — 当新字符被插入到输入字段中时触发。
- `compositionend` — 当文本组合系统关闭时触发，表示返回到正常的键盘输入。

组合事件在许多方面与文本事件相似。当组合事件触发时，目标是接收文本的输入字段。唯一额外的事件属性是 `data`，它包含以下内容之一：

- 在 `compositionstart` 期间访问时，包含正在编辑的文本（例如，如果文本已被选中且现在将进行替换）。
- 在 `compositionupdate` 期间访问时，包含新插入的字符。
- 在 `compositionend` 期间访问时，包含在此次组合会话期间输入的所有内容。

与文本事件一样，在需要时可以使用组合事件来过滤输入。这些事件可以如下所示使用：

![image](img/logo1.gif)

```javascript
```




```javascript
var textbox = document.getElementById("myText");

EventUtil.addHandler(textbox, "compositionstart", function(event) {
    event = EventUtil.getEvent(event);
    alert(event.data);
});

EventUtil.addHandler(textbox, "compositionupdate", function(event) {
    event = EventUtil.getEvent(event);
    alert(event.data);
});

EventUtil.addHandler(textbox, "compositionend", function(event) {
    event = EventUtil.getEvent(event);
    alert(event.data);
});
```

`CompositionEventsExample01.htm`

截至 2011 年，Internet Explorer 9+ 是唯一支持组合事件的浏览器。由于缺乏这种支持，组合事件对于需要跨浏览器支持的 Web 开发人员意义不大。你可以使用以下代码判断浏览器是否支持组合事件：

```javascript
var isSupported = document.implementation.hasFeature("CompositionEvent", "3");
```

### 变异事件（Mutation Events）

Level 2 变异事件在 DOM 部分发生变化时提供通知。变异事件设计用于任何 XML，不特定于语言。Level 2 定义的变异事件如下：

- `DOMSubtreeModified` — 当 DOM 发生任何变化时触发。这是一个捕获性事件，在其他任何事件后触发。
- `DOMNodeInserted` — 当节点作为另一个节点的子节点被插入后触发。
- `DOMNodeRemoved` — 在节点从父节点中移除之前触发。
- `DOMNodeInsertedIntoDocument` — 当节点直接或通过插入其子树进入文档后触发。该事件在 `DOMNodeInserted` 之后触发。该事件在 DOM 3 事件中已废弃，不应使用。
- `DOMNodeRemovedFromDocument` — 在节点直接或通过移除其子树从文档移除之前触发。该事件在 `DOMNodeRemoved` 之后触发。该事件在 DOM 3 事件中已废弃，不应使用。
- `DOMAttrModified` — 当属性被修改时触发。该事件在 DOM 3 事件中已废弃，不应使用。
- `DOMCharacterDataModified` — 当文本节点的值发生变化时触发。该事件在 DOM 3 事件中已废弃，不应使用。

你可以使用以下代码判断浏览器是否支持 Level 2 变异事件：

```javascript
var isSupported = document.implementation.hasFeature("MutationEvents", "2.0");
```

Internet Explorer 8 及更早版本不支持任何变异事件。下表描述了尚未废弃的各种变异事件的浏览器支持情况。

![image](img/f479-01.jpg)

由于许多变异事件在 DOM 3 事件中已废弃，本节重点关注未来将继续支持的事件。

#### 节点移除

当使用 `removeChild()` 或 `replaceChild()` 从 DOM 中移除节点时，首先触发 `DOMNodeRemoved` 事件。此事件的目标是被移除的节点，`event.relatedNode` 属性包含一个指向父节点的引用。在该事件触发时，节点尚未从其父节点中移除，因此其 `parentNode` 属性指向父节点（与 `event.relatedNode` 相同）。此事件会冒泡，因此可以在 DOM 的任何级别进行处理。

如果被移除的节点具有任何子节点，已弃用的 `DOMNodeRemovedFromDocument` 事件会在这些子节点中的每一个上触发，然后在被移除的节点上触发。此事件不会冒泡，因此只有当事件处理器直接附加到其中一个子节点上时，它才会被调用。此事件的目标是子节点或被移除的节点，且事件对象不提供额外信息。

之后，会触发 `DOMSubtreeModified` 事件。此事件的目标是被移除节点的父节点。事件对象不提供关于此事件的额外信息。

为了理解这在实践中是如何工作的，请考虑以下简单的 HTML 页面：

```html
<!DOCTYPE html>
<html>
<head>
    <title>Node Removal Events Example</title>
</head>
<body>
    <ul id="myList">
        <li>Item 1</li>
        <li>Item 2</li>
        <li>Item 3</li>
    </ul>
</body>
</html>
```

在这个示例中，考虑移除 `<ul>` 元素。当这种情况发生时，会按以下顺序触发事件：

1. 在 `<ul>` 元素上触发 `DOMNodeRemoved`。`relatedNode` 属性为 `document.body`。
2. 在 `<ul>` 上触发 `DOMNodeRemovedFromDocument`。
3. 在每个 `<li>` 元素以及每个 `<ul>` 元素的子文本节点上触发 `DOMNodeRemovedFromDocument`。
4. 在 `document.body` 上触发 `DOMSubtreeModified`，因为 `<ul>` 是 `document.body` 的直接子节点。

你可以在页面中运行以下 JavaScript 代码来测试这一点：

```javascript
EventUtil.addHandler(window, "load", function(event) {
    var list = document.getElementById("myList");

    EventUtil.addHandler(document, "DOMSubtreeModified", function(event) {
        alert(event.type);
        alert(event.target);
    });

    EventUtil.addHandler(document, "DOMNodeRemoved", function(event) {
        alert(event.type);
        alert(event.target);
        alert(event.relatedNode);
    });

    EventUtil.addHandler(
        list.firstChild,
        "DOMNodeRemovedFromDocument",
        function(event) {
            alert(event.type);
            alert(event.target);
        }
    );

    list.parentNode.removeChild(list);
});
```

这段代码为 `document` 添加了 `DOMSubtreeModified` 和 `DOMNodeRemoved` 的事件处理器，以便它们处理页面上的所有此类事件。由于 `DOMNodeRemovedFromDocument` 不冒泡，因此其事件处理器直接附加到 `<ul>` 元素的第一个子节点上（在符合 DOM 标准的浏览器中这是一个文本节点）。一旦设置好事件处理器，`<ul>` 元素就会从文档中移除。

#### 节点插入

当使用 `appendChild()`、`replaceChild()` 或 `insertBefore()` 将节点插入 DOM 时，会首先触发 `DOMNodeInserted` 事件。此事件的目标是插入的节点，且 `event.relatedNode` 属性包含指向父节点的引用。在此事件触发时，该节点已经添加到了新的父节点中。此事件会冒泡，因此可以在 DOM 的任何层级上处理该事件。

接下来，已弃用的 `DOMNodeInsertedIntoDocument` 事件会在新插入的节点上触发。此事件不会冒泡，因此事件处理器必须在节点插入之前附加到该节点上。此事件的目标是插入的节点，且事件对象不提供额外信息。

最后一个触发的事件是 `DOMSubtreeModified`，它会在新插入节点的父节点上触发。

考虑到上一节中使用的 HTML 文档，以下 JavaScript 代码指示了事件的顺序：

```javascript
EventUtil.addHandler(window, "load", function(event) {
    var list = document.getElementById("myList");
    var item = document.createElement("li");

    item.appendChild(document.createTextNode("Item 4"));

    EventUtil.addHandler(document, "DOMSubtreeModified", function(event) {
        alert(event.type);
        alert(event.target);
    });

    EventUtil.addHandler(document, "DOMNodeInserted", function(event) {
        alert(event.type);
        alert(event.target);
        alert(event.relatedNode);
    });

    EventUtil.addHandler(
        item,
        "DOMNodeInsertedIntoDocument",
        function(event) {
            alert(event.type);
            alert(event.target);
        }
    );

    list.appendChild(item);
});
```

这段代码首先创建一个包含文本 `"Item 4"` 的新 `<li>` 元素。由于 `DOMSubtreeModified` 和 `DOMNodeInserted` 事件会冒泡，它们的事件处理器被添加到 `document` 上。在将项目添加到其父元素之前，为它添加了 `DOMNodeInsertedIntoDocument` 的事件处理器。最后一步是使用 `appendChild()` 添加项目，此时事件开始触发。`DOMNodeInserted` 事件在新的 `<li>` 项目上触发，此时 `relatedNode` 是 `<ul>` 元素。然后在新的 `<li>` 项目上触发 `DOMNodeInsertedIntoDocument`，最后在 `<ul>` 元素上触发 `DOMSubtreeModified` 事件。

### HTML5 事件

DOM 规范并没有涵盖所有浏览器支持的事件。许多浏览器根据用户需求或特定用例，为各种目的实现了自定义事件。HTML5 详尽地列出了所有应该被浏览器支持的事件（并不是完整的列表）。本节将讨论若干被浏览器良好支持的 HTML5 事件。（其他事件将在书中后续讨论。）

#### `contextmenu` 事件

Windows 95 通过右键点击为 PC 用户引入了右键菜单的概念。很快，这种范式在 Web 上被模拟出来。开发者面临的问题是如何检测应该显示右键菜单。通常，使用 `oncontextmenu` 事件处理器显示自定义右键菜单，并使用 `onclick` 事件处理器再次隐藏。考虑以下 HTML 页面：

```html
<!DOCTYPE html>
<html>
<head>
    <title>ContextMenu Event Example</title>
</head>
<body>
    <div id="myDiv">
        右键点击或 Ctrl+点击我获取自定义右键菜单。
        点击其他地方获取默认右键菜单。
    </div>

    <ul
        id="myMenu"
        style="position:absolute;visibility:hidden;background-color:silver"
    >
        <li><a href="http://www.ncz.net">Nicholas' site</a></li>
        <li><a href="http://www.wrox.com">Wrox site</a></li>
        <li><a href="http://www.yahoo.com">Yahoo!</a></li>
    </ul>
</body>
</html>
```

`ContextMenuEvent01.htm`

在这段代码中，创建一个带有自定义右键菜单的 `<div>`。`<ul>` 元素作为自定义右键菜单且初始为隐藏状态。使此示例运行的 JavaScript 代码如下：

```javascript
EventUtil.addHandler(window, "load", function(event) {
    var div = document.getElementById("myDiv");

    EventUtil.addHandler(div, "contextmenu", function(event) {
        event = EventUtil.getEvent(event);
        EventUtil.preventDefault(event);

        var menu = document.getElementById("myMenu");
        menu.style.left = event.clientX + "px";
        menu.style.top = event.clientY + "px";
        menu.style.visibility = "visible";
    });

    EventUtil.addHandler(document, "click", function(event) {
        document.getElementById("myMenu").style.visibility = "hidden";
    });
});
```

`ContextMenuEventExample01.htm`

在这里，为 `<div>` 定义了一个 `oncontextmenu` 事件处理器。该事件处理器的起始操作是取消默认行为，确保不会显示系统的右键菜单。接下来，根据事件对象的 `clientX` 和 `clientY` 属性将 `<ul>` 元素放置在相应的位置。最后一步通过将其可见性设置为 `"visible"` 来显示菜单。随后，在文档上添加一个 `onclick` 事件处理器，以便在每次发生点击时隐藏菜单（这等同于系统右键菜单的行为）。

尽管这个示例非常基础，但它是 Web 上所有自定义右键菜单的基础。对此示例中的右键菜单应用一些额外的 CSS 可以获得极佳的效果。

`contextmenu` 事件在 Internet Explorer、Firefox、Safari、Chrome 和 Opera 11+ 中均受支持。

### `beforeunload` 事件

`beforeunload` 事件在 `window` 上触发，旨在为开发者提供一种防止页面被卸载的方法。该事件在页面开始从浏览器卸载之前触发，如果页面最终没有被卸载，则允许继续使用该页面。你不能直接取消此事件，因为那等同于将用户劫持在页面上。相反，该事件赋予你向用户显示消息的能力。该消息指示页面即将被卸载，显示消息并询问用户是想继续关闭页面还是留在页面（参见图 13-9）。

FIGURE 13-9

![image](img/f484-01.jpg)

为了让此对话框弹出，你必须将 `event.returnValue` 设置为要在对话框中显示的字符串（针对 Internet Explorer 和 Firefox），并将其作为函数的返回值（针对 Safari 和 Chrome），如例所示：

![image](img/logo1.gif)

```javascript
EventUtil.addHandler(window, "beforeunload", function(event) {
    event = EventUtil.getEvent(event);

    var message = "I'm really going to miss you if you go.";

    event.returnValue = message;
    return message;
});
```



## BeforeUnloadEventExample01.htm

Internet Explorer、Firefox、Safari 和 Chrome 都支持`beforeunload`事件，并弹出对话框确认用户是否想要离开。Opera 从版本 11 起不再支持`beforeunload`。

## DOMContentLoaded 事件

`window`的`load`事件在页面上的所有内容完全加载后触发，对于具有大量外部资源的页面，这可能需要一些时间。`DOMContentLoaded`事件在 DOM 树完全形成后立即触发，而不考虑图像、JavaScript 文件、CSS 文件或其他此类资源。与`load`事件相比，`DOMContentLoaded`允许在页面下载过程的更早阶段附加事件处理器，这意味着用户交互的时间更短。

要处理`DOMContentLoaded`事件，你可以在`document`上或`window`上附加事件处理器（该事件的实际目标是`document`，尽管它会冒泡到`window`）。以下是一个示例：

```
EventUtil.addHandler(document, "DOMContentLoaded", function(event){
    alert("Content loaded");
});
```

## DOMContentLoadedEventExample01.htm

`DOMContentLoaded`的事件对象不提供任何额外信息（目标为`document`）。

`DOMContentLoaded`事件在 Internet Explorer 9+、Firefox、Chrome、Safari 3.1+ 和 Opera 9+ 中受支持，通常用于附加事件处理器或执行其他 DOM 操作。此事件始终在`load`事件之前触发。

对于不支持`DOMContentLoaded`的浏览器，建议在页面加载期间设置一个毫秒延迟为 0 的超时，如例所示：

```
setTimeout(function(){
    //在此处附加事件处理器
}, 0);
```

这段代码本质上是说：“一旦当前 JavaScript 进程完成，立即运行此函数”。在页面下载和构建时，只有一个 JavaScript 进程在运行，因此超时将在该之后触发。这是否直接与`DOMContentLoaded`的时机重合，取决于所使用的浏览器以及页面上的其他代码。为了正常工作，这必须是页面上设置的第一个超时，即使如此，也无法保证在所有情况下超时都会在`load`事件之前运行。

## readystatechange 事件

Internet Explorer 首先在 DOM 文档的多个部分上定义了一个名为`readyStatechange`的事件。这个有些神秘的事件旨在提供有关文档或元素加载状态的信息，尽管它的行为往往不稳定。每个支持`readyStatechange`事件的对象都有一个`readyState`属性，该属性可以具有以下五个可能的字符串值之一：

* `uninitialized` — 对象存在但尚未初始化。
* `loading` — 对象正在加载数据。
* `loaded` — 对象已完成数据加载。
* `interactive` — 对象可以进行交互，但尚未完全加载。
* `complete` — 对象已完全加载。

尽管这看起来很直观，但并不是所有对象都会经过所有的`readyState`阶段。文档指出，如果某个阶段不适用，对象可能会完全跳过它，但没有指示哪些阶段适用于哪些对象。这意味着`readyStatechange`事件触发次数少于四次，且`readyState`值并不总是遵循相同的进展顺序。

在`document`上使用时，`readyState`为`"interactive"`会触发`readyStatechange`事件，其触发时机类似于`DOMContentLoaded`。此时整个 DOM 树已加载，因此可以进行交互。图像和其他资源在此时可能不可用。`readyStatechange`事件可以这样处理：

```
EventUtil.addHandler(document, "readystatechange", function(event){
    if (document.readyState == "interactive"){
        alert("Content loaded");
    }
});
```

此事件的事件对象不提供任何额外信息（未设置目标）。

当与`load`事件结合使用时，这些事件的触发顺序是不保证的。对于具有大量或大型外部资源的页面，`interactive`阶段在`load`事件之前很久就已经达到了；对于资源较小的页面，`readyStatechange`事件可能在`load`事件之后才触发。

更令人困惑的是，`interactive`阶段可能出现在`complete`阶段之前或之后；这种顺序不是固定的。对于外部资源较页面，`interactive`阶段可能会在`complete`阶段之前发生，而在资源较少的页面，`complete`阶段可能会在`interactive`阶段之前发生。因此，为了确保获取尽可能的时刻，有必要检查`interactive`和`complete`阶段，如例所示：

```
EventUtil.addHandler(document, "readystatechange", function(event){
    if (document.readyState == "interactive" || document.readyState == "complete"){
        EventUtil.removeHandler(document, "readystatechange", arguments.callee); 
        alert("Content loaded");                      
    }
});
```

当`readyStatechange`事件在此代码中触发时，会检查`document.readyState`属性以判断是否处于`interactive`或`complete`阶段。如果是，则移除事件处理器，以确保它不会在另一个阶段再次执行。注意，由于事件处理器是匿名函数，因此使用`arguments.callee`作为指向函数的指针。之后，显示警框指示内容已加载。这种结构允许你尽可能接近`DOMContentLoaded`事件。

`document`上的`readyStatechange`事件在 Internet Explorer、Firefox 4+ 和 Opera 中受支持。

![image](img/pen.gif)

尽管你可以通过`readystatechangechange`尽可能模拟`DOMContentLoaded`，但它们并不完全相同。`load`事件和`readystatechangechange`事件的触发顺序在不同页面之间是不一致的。

`readystatechangechange`事件也会在`<script>`（Internet Explorer 和 Opera）和`<link>`（仅限 Internet Explorer）标签上触发，这允许你确定外部 JavaScript 和 CSS 文件何时加载完成。与其他浏览器一样，动态创建的元素在被添加到页面之前，并不会开始下载外部资源。该事件在元素上的行为同样令人困惑，因为`readyState`属性可能是 "loaded" 或 "complete"，用以表示资源已就绪。有时`readyState`会停留在 "loaded" 而永远不会变为 "complete"，而另时候它又会跳过 "loaded" 直接变为 "complete"。因此，有必要使用与`document`相同的结构。例如，以下代码加载了一个外部 JavaScript 文件：

![image](img/logo1.gif)

```
EventUtil.addHandler(window, "load", function(){
    var script = document.createElement("script");
    EventUtil.addHandler(script, "readystatechange", function(event){
        event = EventUtil.getEvent(event);
        var target = EventUtil.getTarget(event);
        if (target.readyState == "loaded" || target.readyState == "complete"){
            EventUtil.removeHandler(target, "readystatechange", arguments.callee);
            alert("Script Loaded");
        }
    });
    script.src = "example.js";
    document.body.appendChild(script);
});
```

### ReadyStateChangeEventExample01.htm

此示例为新创建的`<script>`节点分配了一个事件处理器。事件的目标是节点本身，因此当`readystatechangechange`事件触发时，会检查目标的`readyState`属性以判断其是否为 "loaded" 或 "complete"。如果处于其中两个阶段之一，就会移除事件处理器（以防止其可能被执行两次），然后显示警框。此时，你可以开始执行从外部文件中加载的函数。

相同的结构也可以通过`<link>`元素加载 CSS 文件，如下例所示：

![image](img/logo1.gif)

```
EventUtil.addHandler(window, "load", function(){  
    var link = document.createElement("link");
    link.type = "text/css";
    link.rel= "stylesheet";
    EventUtil.addHandler(script, "readystatechange", function(event){
        event = EventUtil.getEvent(event);
        var target = EventUtil.getTarget(event);
        if (target.readyState == "loaded" || target.readyState == "complete"){
            EventUtil.removeHandler(target, "readystatechange", arguments.callee);
            alert("CSS Loaded");
        }
    });
    link.href = "example.css";
    document.getElementsByTagName("head")[0].appendChild(link);
});
```

### ReadyStateChangeEventExample02.htm

再次强调，测试两种`readyState`值并在调用一次后移除事件处理器是非常关重要的。

## pageshow 和 pagehide 事件

Firefox 和 Opera 引入了一种名为后退前进缓存（bfcache）的功能，旨在加速使用浏览器的“后退”和“前进”按钮时的页面切换。该缓存不仅存储页面数据，还存储了 DOM 和 JavaScript 状态，有效地将整个页面留在内存中。如果页面位于 bfcache 中，当导航到该页面时，`load`事件将不会触发。这通常不会引起问题，因为整个页面状态都已存储。然而，Firefox 决定提供一些事件来提高 bfcache 行为的可见性。

第一个事件是`pageshow`，每当页面显示时都会触发，无论是否来自 bfcache。在新加载的页面上，`pageshow`在`load`事件之后触发；对于在 bfcache 中的页面，`pageshow`在页面状态完全恢复后立即触发。请注意，尽管该事件的目标是`document`，但事件处理器必须绑定到`window`上。考虑以下代码：

```
(function(){
    var showCount = 0;
    EventUtil.addHandler(window, "load", function(){
        alert("Load fired");            
    });
    EventUtil.addHandler(window, "pageshow", function(){
        showCount++;
        alert("Show has been fired " + showCount + " times.");            
    });
})();
```

此示例使用私有作用域来防止`showCount`变量被引入全局作用域。当页面首次加载时，`showCount`的值为 0。每当`pageshow`事件触发时，`showCount`就会递加并显示警框。如果你离开包含此代码的页面，然后点击“后退”按钮恢复它，你会发现`showCount`的值每次都会增加。这是因为变量状态以及整个页面状态都存储在内存中，并在你导航回页面时被取回。如果你点击浏览器的“刷新”按钮，`showCount`的值将重置为 0，因为页面将完全重新加载。

除了常规属性外，`pageshow`的事件对象包含一个名为`persisted`的属性。这是一个布尔值，如果页面存储在 bfcache 中，则设置为 true，否则设置为 false。可以在事件处理器中按如下方式检查该属性：

![image](img/logo1.gif)

```
(function(){
    var showCount = 0;
    EventUtil.addHandler(window, "load", function(){
        alert("Load fired");
    });
    EventUtil.addHandler(window, "pageshow", function(event){
        showCount++;
        alert("Show has been fired " + showCount + " times. Persisted? " + event.persisted);
    });
})();
```

### PageShowEventExample01.htm

`persisted`属性允许你根据页面在 bfcache 中的状态确定是否需要采取不同的操作。

`pagehide`事件是`pageshow`的伴侣事件，每当页面从浏览器卸载时都会触发，在`unload`事件之前立即触发。与`pageshow`事件一样，`pagehide`虽然在`document`上触发，但事件处理器必须绑定到`window`上。事件对象也包含`persisted`属性，尽管在用法上略有不同。考虑以下代码：

![image](img/logo1.gif)

```
EventUtil.addHandler(window, "pagehide", function(event){
    alert("Hiding. Persisted? " + event.persisted);
});
```

### PageShowEvent01.htm

你可能会根据`pagehide`触发时`persisted`的值来决定采取不同的操作。对于`pageshow`事件，如果页面是从 bfcache 加载的，则`persisted`被设置为 true；对于`pagehide`事件，如果页面卸载后将存储在 bfcache 中，则`persisted`被设置为 true。因此，第一次触发`pageshow`时，`persisted`始终为 false，而第一次触发`pagehide`时，`persisted`将为 true（除非页面不会存储在 bfcache 中）。

`pageshow`和`pagehide`事件受 Firefox、Safari 5+、Chrome 和 Opera 支持。Internet Explorer 直到 9 版本不支持这些事件。

![image](img/pen.gif)

分配了`onunload`事件处理器的页面会自动排除在 bfcache 之外，即使事件处理器为空。理由是，`onunload`通常用于撤销使用`onload`所执行的操作，因此在下次显示页面时跳过`onload`可能会导致程序崩溃。

## hashchange 事件

HTML5 引入了`hashchange`事件，用于在 URL 哈希（URL 中井号 # 之后的所有内容）发生变化时通知开发者。这种引入是因为开发者经常在 Ajax 应用中使用 URL 哈希来存储状态信息或导航信息。

`onhashchange`事件处理程序必须绑定到`window`上，每当 URL hash 发生变化时它就会被调用。事件对象应该有两个额外的属性：`oldURL`和`newURL`。这些属性存储了变化前后的包含 hash 的完整 URL。例如：

```javascript
EventUtil.addHandler(window, "hashchange", function(event){
```



`alert("Old URL: " + event.oldURL + "\nNew URL: " + event.newURL);`

`HashChangeEventExample01.htm`

`hashchange` 事件支持 Internet Explorer 8+、`Firefox 3.6+`、`Safari 5+`、`Chrome` 以及 `Opera 10.6+`。在这些浏览器中，只有 `Firefox 6+`、`Chrome` 和 `Opera` 支持 `oldURL` 和 `newURL` 属性。因此，最好使用 `location` 对象来确定当前的 hash：

```javascript
EventUtil.addHandler(window, "hashchange", function(event){
    alert("Current hash: " + location.hash);
});
```

你可以使用以下代码检测是否支持 `hashchange` 事件：

```javascript
var isSupported = ("onhashchange" in window);    //buggy
```

Internet Explorer 8 有一个特性，即使在 Internet Explorer 7 文档模式下运行，此代码也会返回 `true`，尽管它并不可用。为了绕过这个问题，请使用以下更健壮的检测方法：

```javascript
var isSupported = ("onhashchange" in window) && (document.documentMode === 
                  undefined || document.documentMode > 7);
```

# 设备事件 (Device Events)

随着智能手机和平板设备的出现，用户与浏览器交互的方式出现了一系列新方法。因此，发明了一类新的事件。设备事件允许你确定设备是如何使用的。2011 年，W3C 启动了一项关于设备事件的新草案（[`dev.w3.org/geo/api/spec-source-orientation.html`](http://dev.w3.org/geo/api/spec-source-orientation.html)），以涵盖日益增多的寻求实现设备相关的设备。节涵盖了草案中定义的 API 以及特定特定的事件。

## orientationchange 事件

Apple 在移动版 Safari 上创建了 `orientationchange` 事件，以便开发者确定用户何时将设备从横屏切换到竖屏模式。移动版 Safari 上有一个 `window.orientation` 属性，包含三个值之一：`0` 表示竖屏模式，`90` 表示向左旋转时的横屏模式（Home 键在右侧），`-90` 表示向右旋转时的横屏模式（Home 键在左侧）。文档还提到如果设备倒置，则值为 `180`，但到目前为止该配置尚不支持支持。图 13-10 展示了 `window.orientation` 的各种值。

FIGURE 13-10

![image](img/f490-01.jpg)

每当用户从一种模式切换到另一种模式时，就会触发 `orientationchange` 事件。事件对象不包含有用信息，因为唯一的相关信息可以通过 `window.orientation` 获取。该事件的典型用法如下：

![image](img/logo1.gif)

```javascript
EventUtil.addHandler(window, "load", function(event){
    var div = document.getElementById("myDiv");
    div.innerHTML = "Current orientation is " + window.orientation;
    EventUtil.addHandler(window, "orientationchange", function(event){
        div.innerHTML = "Current orientation is " + window.orientation;
    });
});
```

`OrientationChangeEventExample01.htm`

在此示例中，当 `load` 事件触发时，会显示初始方向。然后为 `orientationchange` 分配事件处理程序。每当事件触发时，页面上的消息就会更新以指示新的方向。

所有 iOS 设备都支持 `orientationchange` 事件和 `window.orientation` 属性。

![image](img/pen.gif)

由于 `orientationchange` 被视为窗口事件，你也可以通过向 `<body>` 元素添加 `onorientationchange` 属性来分配事件处理程序。

## MozOrientation 事件

Firefox 3.6 引入了一个名为 `MozOrientation` 的新事件来检测设备方向。（前缀 `Moz` 表示它是厂商特定事件而不是标准事件。）当设备加速度计检测到设备方向的变化时，该事件会定期触发。注意，这与 iOS 的 `orientationchange` 不同，后者只提供一个维度的运动。`MozOrientation` 事件在 `window` 对象上触发，因此可以使用以下代码进行处理：

```javascript
EventUtil.addHandler(window, "MozOrientation", function(event){
    //respond to event
});
```

事件对象具有三个带有加速度数据的属性：`x`、`y` 和 `z`。每个值都是 1 到 –1 之间的数字，代表不同的轴。当静止时，`x` 为 `0`，`y` 为 `0`，`z` 为 `1`（表示设备直立）。向右倾斜会减少 `x` 的值，而向左倾斜会增加该值。同样，向远离你的方向倾斜会减少 `y` 值，而向你的方向倾斜（如读报纸）则会增加它。`z` 值是垂直方向，静止时为 `1`，当设备运动时会减小。这是一个输出三个值的简单示例：

```javascript
EventUtil.addHandler(window, "MozOrientation", function(event){
    var output = document.getElementById("output");
    output.innerHTML = "X=" + event.x + ", Y=" + event.y + ", Z=" + event.z;
});
```

`MozOrientationExample01.htm`

`MozOrientation` 事件仅支持带有加速度计的设备，包括 Macbook、Lenovo Thinkpad 以及 Windows Mobile 和 Android 设备。应该注意，这是一个实验性 API，未来可能会被取代。

## deviceorientation 事件

`deviceorientation` 事件在 DeviceOrientation 规范中定义，性质与 `MozOrientation` 事件相似。当加速度信息可用并发生变化时，该事件在 `window` 上触发，支持同样的 `MozOrientation`。请记住 `deviceorientation` 的目的是告知设备在空间中的方向而不是运动。

设备被认为存在于三维空间，沿着 `x` 轴、`y` 轴和 `z` 轴。当设备处于水平面上时，这些值都为 0。`x` 轴从设备的左侧到右侧，`y` 轴从设备的底部到顶部，`z` 轴从设备的后部到正面（参见图 13-11）。

FIGURE 13-11

![image](img/f492-01.jpg)

当 `deviceorientation` 触发时，它返回每个轴的值相对于静止设备的变化信息。事件对象有五个属性：

*   `alpha`：绕 `z` 轴旋转的角度差（侧向倾斜）；一个在 0 到 360 之间的浮点数。
*   `beta`：绕 `x` 轴旋转的角度差（前后倾斜）；一个在 –180 到 180 之间的浮点数。
*   `gamma`：绕 `y` 轴旋转的角度差（扭转倾斜）；一个在 –90 到 90 之间的浮点数。
*   `absolute`：一个布尔值，指示设备是否返回绝对值。
*   `compassCalibrated`：一个布尔值，指示设备的指南针是否已正确校准。

图 13-12 展示了 `alpha`、`beta` 和 `gamma` 值的计算方式。

```javascript
EventUtil.addHandler(window, "deviceorientation", function(event){
    var output = document.getElementById("output");
    output.innerHTML = "Alpha=" + event.alpha + ", Beta=" + event.beta + 
                       ", Gamma=" + event.gamma + "<br>";
});
```

### DeviceOrientationEventExample01.htm

你可以使用这些信息根据设备方向的变化来重新排列或更改屏幕上的元素。例如，这段代码会根据设备方向旋转一个元素：

```javascript
EventUtil.addHandler(window, "deviceorientation", function(event){
    var arrow = document.getElementById("arrow");
    arrow.style.webkitTransform = "rotate(" + Math.round(event.alpha) + "deg)";
});
```

### DeviceOrientationEventExample01.htm

此示例仅在移动 WebKit 浏览器上有效，因为它使用了私有的 `webkitTransform` 属性（CSS 标准 `transform` 属性的临时版本）。元素“arrow”随着 `event.alpha` 的值旋转，产生类似指南针的感觉。使用了 CSS3 旋转变换并配合取整后的值以确保流畅度。

截至 2011 年，Safari for iOS 4.2+、Chrome 和 WebKit for Android 是 `deviceorientation` 事件的唯一实现。

### The devicemotion Event

`DeviceOrientationEvent` 规范还包含一个 `devicemotion` 事件。该事件旨在当设备实际发生移动时通知你，而不仅仅是在方向发生改变时。例如，`devicemotion` 用于判断设备正在掉落或正被正在行走的人拿着。

当 `devicemotion` 事件触发时，事件对象包含以下附加属性：

* `acceleration` — 一个包含 `x`、`y` 和 `z` 属性的对象，它告诉你在不考虑重力的情况下每个维度上的加速度。
* `accelerationIncludingGravity` — 一个包含 `x`、`y` 和 `z` 属性的对象，它告诉你每个维度上的加速度，包括 `z` 轴上的自然重力加速度。
* `interval` — 在下一次 `devicemotion` 事件触发之前将经过的毫秒数。该值在各个事件之间应该是恒定的。
* `rotationRate` — 一个包含 `alpha`、`beta` 和 `gamma` 属性的对象，指示设备的方向。

如果无法提供 `acceleration`、`accelerationIncludingGravity` 或 `rotationRate`，则属性值为 `null`。因此，在使用任何这些属性之前，你应该始终检查值是否为 `null`。例如：

![image](img/logo1.gif)

```javascript
EventUtil.addHandler(window, "devicemotion", function(event){
    var output = document.getElementById("output");
    if (event.rotationRate !== null){
        output.innerHTML += "Alpha=" + event.rotationRate.alpha + ", Beta=" + 
                            event.rotationRate.beta + ", Gamma=" + 
                            event.rotationRate.gamma;        
    }
});
```

### DeviceMotionEventExample01.htm

与 `deviceorientation` 类似，Safari for iOS 4.2+、Chrome 和 WebKit for Android 是 `devicemotion` 事件的唯一实现。

### Touch and Gesture Events

Safari for iOS 引入了多个专用事件，用于在特定事件发生时通知开发者。由于 iOS 设备没有鼠标和键盘，普通的鼠标和键盘事件根本不足以创建一个专为移动 Safari 设计的完全交互式的网页。随着 Android WebKit 的引入，许多专用事件变成了事实上的标准，并导致了 W3C 触摸事件 规范的产生（可以在 [`dvcs.w3.org/hg/webevents/raw-file/tip/touchevents.html`](https://dvcs.w3.org/hg/webevents/raw-file/tip/touchevents.html)找到）。以下事件仅在基于触摸的设备上运行。

### Touch Events

当 iPhone 3G 发布 iOS 2.0 系统时，包含了一个新版本的 Safari。这个新的移动 Safari 暴露了几个与触摸交互相关的新事件。Android 浏览器后来实现了相同的事件。当手指触摸屏幕、在屏幕上滑动或从屏幕移除时会触发触摸事件。触摸事件如下：

* `touchstart` — 当手指触摸屏幕时触发，即使另一个手指已经触摸了屏幕也会触发。
* `touchmove` — 当手指在屏幕上移动时持续触发。在此事件期间调用 `preventDefault()` 可以防止滚动。
* `touchend` — 当手指离开屏幕时触发。
* `touchcancel` — 当系统停止跟踪触摸时触发。文档中不清楚这种情况何时发生。

这些事件中的每一个都会冒泡并可以被取消。尽管触摸事件不是 DOM 规范的一部分，但它们是以兼容 DOM 的方式实现的。因此，每个触摸事件的事件对象提供了鼠标事件常用的属性：`bubbles`、`cancelable`、`view`、`clientX`、`clientY`、`screenX`、`screenY`、`detail`、`altKey`、`shiftKey`、`ctrlKey` 和 `metaKey`。

除了这些常用的 DOM 属性外，触摸事件还有以下三个用于跟踪触摸的属性：

* `touches` — `Touch` 对象数组，表示当前正在跟踪的触摸。
* `targetTouches` — 事件目标特定的 `Touch` 对象数组。
* `changedTouches` — 上一次用户操作中发生变化的 `Touch` 对象数组。

每个 `Touch` 对象又有以下属性：

* `clientX` — 触摸目标在视口中的 x 坐标。
* `clientY` — 触摸目标在视口中的 y 坐标。
* `identifier` — 触摸的唯一 ID。
* `pageX` — 页面上触摸目标的 x 坐标。
* `pageY` — 页面上触摸目标的 y 坐标。
* `screenX` — 触摸目标在屏幕上的 x 坐标。
* `screenY` — 触摸目标在屏幕上的 y 坐标。
* `target` — 触摸的 DOM 目标。

这些属性可以用于跟踪屏幕周围触摸。例如：

![image](img/logo1.gif)

```javascript
function handleTouchEvent(event){
    //仅针对单触摸
    if (event.touches.length == 1)
        var output = document.getElementById("output");
        switch(event.type){
            case "touchstart":
                output.innerHTML = "Touch started (" + event.touches[0].clientX + 
                                   "," + event.touches[0].clientY + ")";
                break;
            case "touchend":
                output.innerHTML += "<br>Touch ended (" + 
                                    event.changedTouches[0].clientX + 
                                    "," + event.changedTouches[0].clientY + ")";
                break;
            case "touchmove":
                event.preventDefault();  //防止滚动
```



`output.innerHTML += "<br>Touch moved (" + event.changedTouches[0].clientX + "," + event.changedTouches[0].clientY + ")";`

`break;`

`}`

`}`

`}`

`EventUtil.addHandler(document, "touchstart", handleTouchEvent);`

`EventUtil.addHandler(document, "touchend", handleTouchEvent);`

`EventUtil.addHandler(document, "touchmove", handleTouchEvent);`

### TouchEventsExample01.htm

这段代码跟踪屏幕周围的单触摸。为了保持简单，它仅在存在单个活跃触摸时输出信息。当`touchstart`事件发生时，它将触摸位置输出到`div`。当`touchmove`事件触发时，取消其默认行为以防止滚动（移动触摸通常会滚动页面），然后输出关于变化触摸的信息。`touchend`事件输出触摸的最后信息。注意，在`touchend`事件期间`touches`集合中没有任何内容，因为不再有活跃的触摸；必须使用`changedTouches`集合。

这些事件会在文档的所有元素上触发，因此你可以单独操作页面的不同部分。点击元素时触发的事件顺序（包括鼠标事件）如下：

1. `touchstart`
2. `mouseover`
3. `mousemove`（一次）
4. `mousedown`
5. `mouseup`
6. `click`
7. `touchend`

iOS 版 Safari、Android 版 WebKit、bada 的 Dolfin、OS6+ 的 BlackBerry WebKit、Opera Mobile 10.1+ 以及 LG 专用系统的 Phantom 浏览器都支持触摸事件。只有 iOS 上的 Safari 支持同时多点触摸。桌面端的 Firefox 6+ 和 Chrome 也支持触摸事件。

## 手势事件

iOS 2.0 版本的 Safari 还引入了一类手势事件。当两个手指触摸屏幕时就会发生手势，这通常会导致显示项目的缩放或旋转变化。这里描述了三类手势事件：

* `gesturestart` — 当一个手指已经在屏幕上，另一只手指放在屏幕上时触发。
* `gesturechange` — 当屏幕上任一手指的位置发生变化时触发。
* `gestureend` — 当其中一个手指从屏幕上移除时触发。

这些事件仅在两个手指都触摸到事件接收者时才会触发。在单个元素上设置事件处理器意味着两只手指都必须在该元素的范围内，手势事件才会触发（该元素将是目标）。由于这些事件会冒泡，你也可以在文档层级上放置事件处理器来处理所有手势事件。当你使用这种方法时，事件目标将是两只手指都在其边界内的元素。

触摸事件和手势事件之间存在关系。当一个手指放在屏幕上时，触发`touchstart`事件。当另一只手指放在屏幕上时，首先触发`gesturestart`事件，紧接着触发该手指的`touchstart`事件。如果移动了一个或两个手指，则会触发`gesturechange`事件。一旦其中一个手指被移除，就会触发`gestureend`事件，随后触发该手指的`touchend`事件。

与触摸事件一样，每个手势事件对象都包含了所有的标准鼠标事件属性：`bubbles`、`cancelable`、`view`、`clientX`、`clientY`、`screenX`、`screenY`、`detail`、`altKey`、`shiftKey`、`ctrlKey`和`metaKey`。事件对象中新增的两个是`rotation`和`scale`。`rotation`属性表示手指旋转的度数，负数表示逆时针旋转，正数表示顺时针旋转（该值值为 0）。`scale`属性表示手指之间距离变化量（产生捏合动作）。它从 1 开始，并随着距离增加而增大，随着距离减小而减小。

这些事件可以如下使用：

![image](img/logo1.gif)

```javascript
function handleGestureEvent(event){        
    var output = document.getElementById("output");
    switch(event.type){
        case "gesturestart":
            output.innerHTML = "Gesture started (rotation=" + event.rotation + 
                               ",scale=" + event.scale + ")";
            break;
        case "gestureend":
            output.innerHTML += "<br>Gesture ended (rotation=" + event.rotation +  
                                ",scale=" + event.scale + ")";
            break;
        case "gesturechange":
            output.innerHTML += "<br>Gesture changed (rotation=" + event.rotation + 
                                ",scale=" + event.scale + ")";
            break;
    }
}
document.addEventListener("gesturestart", handleGestureEvent, false);
document.addEventListener("gestureend", handleGestureEvent, false);
document.addEventListener("gesturechange", handleGestureEvent, false);
```

`GestureEventsExample01.htm`

与触摸事件示例一样，这段代码简单是将每个事件绑定到单个函数，然后输出关于每个事件的信息。

![image](img/pen.gif)

触摸事件也会返回`rotation`和`scale`属性，但它们只有在两个手指都接触屏幕时才会发生变化。通常情况下，使用两个手指使用手势事件，比通过触摸事件管理所有交互要容易得多。

## 内存与性能

由于事件处理器为现代 Web 应用程序提供了交互支持，许多开发者错误地在页面上添加了大量的处理器。在创建 GUI 的语言（如 C#）中，习惯性做法是为 GUI 中的每个按钮添加一个`onclick`事件处理器，这样做并没有实际的性能代价。在 JavaScript 中，页面上事件处理器的数量直接关系到页面的整体性能。这种情况由于以下几个原因：首先，每个函数都是一个对象并占用内存；内存中的对象越多，性能就越慢。其次，预先分配所有事件处理器所需的 DOM 访问会延迟整个页面的交互性。你有很多方法可以通过留心对事件处理器的使用来提高性能。

### 事件委托

解决“事件处理器过多”问题的方案被称为“事件委托”。事件委托利用事件冒泡机制，分配单个事件处理器来管理所有特定类型的所有事件。例如，`click`事件会一直冒泡到文档层级。这意味着可以为整个页面分配一个`onclick`事件处理器，而不是为每个可点击元素分配一个。考虑以下 HTML：

![image](img/logo1.gif)

```html
<ul id="myLinks">
    <li id="goSomewhere">Go somewhere</li>
    <li id="doSomething">Do something</li>
    <li id="sayHi">Say hi</li>
</ul>
```

`EventDelegationExample01.htm`

此示例中的 HTML 包含三个在点击时应执行操作的项。传统的做法是简单地挂载三个事件处理器，如下所示：

```javascript
var item1 = document.getElementById("goSomewhere");
var item2 = document.getElementById("doSomething");
var item3 = document.getElementById("sayHi");

EventUtil.addHandler(item1, "click", function(event){
    location.href = "http://www.wrox.com";
});
EventUtil.addHandler(item2, "click", function(event){
    document.title = "I changed the title";
});
EventUtil.addHandler(item3, "click", function(event){
    alert("hi");
});
```

如果在一个复杂的 Web 应用中对所有可点击元素重复这种场景，结果将是一段极其冗长的代码，仅用于挂载事件处理器。事件委托通过在 DOM 树中尽可能高的点挂载单个事件处理器来解决这个问题，如示例所示：

![image](img/logo1.gif)

```javascript
var list = document.getElementById("myLinks");
EventUtil.addHandler(list, "click", function(event){
    event = EventUtil.getEvent(event);
    var target = EventUtil.getTarget(event);
    switch(target.id){
        case "doSomething":
            document.title = "I changed the title";
            break;
        case "goSomewhere":
            location.href = "http://www.wrox.com";
            break;
        case "sayHi":
            alert("hi");
            break;
    }
});
```

`EventDelegationExample01.htm`

在此段代码中，使用事件委托在`ul`元素上挂载单个`onclick`事件处理器。由于所有的列表项都是该元素的子元素，它们的事件会冒泡并由该函数处理。事件目标是被点击的列表项，因此你可以检查`id`属性来确定相应的操作。与之前未使用事件委托的代码相比，这段代码的预开销更小，因为它只需要获取一个 DOM 元素并挂载一个事件处理器。对于用户来说最终结果相同，但这种方法所需的内存少得多。所有使用按钮的事件（大多数鼠标事件和键盘事件）都是这种技术的候选对象。

如果可行，你可能希望考虑在`document`上挂载单个事件处理器，用它可以处理特定类型的所有页面事件。与传统技术相比，这种方法具有以下优势：

* `document`对象是立即可用的，并且可以在页面生命周期内的任何时间为其分配事件处理器（无需等待`DOMContentLoaded`或`load`事件）。这意味着只要可点击元素一被渲染，它就能正常工作而不会产生延迟。
* 在页面上设置事件处理器花费的时间更少。分配一个事件处理器所需的 DOM 引用更少，花费也更短。
* 整个页面的内存占用更低，从而提高了整体性能。

事件委托的最佳候选者是`click`、`mousedown`、`mouseup`、`keydown`、`keyup`和`keypress`。`mouseover`和`mouseout`事件会冒泡，但处理起来比较复杂，通常需要计算元素的位置才能进行适当处理（因为从一个元素移动到其子节点之一，或者移动到元素外部时，都会触发`mouseout`）。

## 移除事件处理器

当事件处理器被分配给元素时，浏览器中运行的代码与与页面交互的 JavaScript 代码之间就会建立一种连接。这种连接越多，页面的性能就越慢。处理此问题的方法是通过事件委托来限制建立的连接数量。另一种管理问题的方法是在事件处理器不再需要时将其移除。悬空事件处理器（dangling event handlers），即在必要之后仍留在内存中的处理器，是 Web 应用中内存和性能问题的主要来源。

这个问题发生在页面生命周期中的两个特定点。第一个是当元素在附有事件处理器的情况下被从`document`中移除时。这可能是由于涉及`removeChild()`或`replaceChild()`的真实 DOM 操作引起的，但最常见于使用`innerHTML`替换页面部分时。任何分配给通过`innerHTML`调用消除的元素的事件处理器都可能无法被正确垃圾回收。考虑以下示例：

```html
<div id="myDiv">
    <input type="button" value="Click Me" id="myBtn">
</div>
<script type="text/javascript">
    var btn = document.getElementById("myBtn");
    btn.onclick = function(){
        //do something
        document.getElementById("myDiv").innerHTML = "Processing...";  //Bad!!!
    };
</script>
```

在这里，`div`元素内部存在一个按钮。当按钮被点击时，它会被移除并替换为一条消息以防止双击，这是网站上非常常见的范式。问题是，按钮在从页面上移除时仍然附带有事件处理器。在`div`上设置`innerHTML`彻底删除了按钮，但事件处理器仍然附着在上面。某些浏览器（特别是 Internet Explorer 8 及更早版本）在这种情况下会遇到困难，并且很可能元素和事件处理器的引用都会残留在内存中。如果你知道某个元素将被移除，最好由你手动移除事件处理器，如示例所示：

```html
<div id="myDiv">
    <input type="button" value="Click Me" id="myBtn">
</div>
<script type="text/javascript">
    var btn = document.getElementById("myBtn");
    btn.onclick = function(){
        //do something
        btn.onclick = null;   //remove event handler
        document.getElementById("myDiv").innerHTML = "Processing..."; 
    };
</script>
```



在这段重写代码中，在设置 `div` 元素的 `innerHTML` 之前移除了按钮的事件处理器。这确保了内存会被回收，并且按钮可以安全地从 DOM 中移除。

同样注意，在事件处理器中移除按钮会防止事件的冒泡。只有当事件目标仍然存在于 `document` 中时，事件才会冒泡。

![image](img/pen.gif)

事件委托也有助于解决这个问题。如果你知道页面的某部分将使用 `innerHTML` 替换，请不要向该部分内的元素挂载事件处理器。相反，在更高层次上挂载事件处理器，以处理该区域的事件。

悬空事件处理器问题的另一个时间是页面卸载时。再次，Internet Explorer 8 及更早版本在这种情况下有很多问题，尽管这似乎以某种方式影响了所有浏览器。如果在页面卸载之前没有清理事件处理器，它们将留在内存中。此后浏览器每次加载和卸载页面（由于离开并返回或点击刷新按钮），内存中的对象数量就会增加，因为事件处理器的内存没有被回收。

总的来说，在页面卸载之前使用 `onunload` 事件处理器移除所有事件处理器是一个好主意。这是事件委托有帮助的另一个领域，因为当处理器较少时，更容易跟踪需要移除的事件处理器。考虑这种技术的良好方法是：任何使用 `onload` 事件处理器执行的操作，都必须使用 `onunload` 进行反转。

![image](img/pen.gif)

请记住，挂载 `onunload` 事件处理器意味着你的页面将不会存储在 bfcache（后历史缓存）中。如果你担心这一点，可能只想在 Internet Explorer 中使用 `onunload` 来移除事件处理器。

## 模拟事件

事件的设计是为了指示网页中特定的时刻。这些事件通常根据用户交互或其他浏览器功能触发。一个鲜为人知的事实是，可以使用 JavaScript 在任何时候触发特定事件，这些事件的处理方式与浏览器创建的事件相同。这意味着事件会适当冒泡，并导致浏览器执行处理该事件的事件处理器。这种能力在测试 Web 应用时非常有用。DOM 3 规范指示了模拟特定类型的方法，Internet Explorer 9、Opera、Firefox 和 Safari 都支持它。Internet Explorer 8 及更早版本有自己的模拟事件方法。

### DOM 事件模拟

可以使用 `document` 上的 `createEvent()` 方法随时创建事件对象。该方法接受一个字符串，该字符串指示要创建的事件类型。在 DOM 2 中，这些字符串都是复数形式，而 DOM 3 将它们改为了单数。该字符串可能是以下之一：

- `UIEvents` —— 通用 UI 事件。鼠标事件和键盘事件继承自 UI 事件。对于 DOM 3，使用 `UIEvent`。
- `MouseEvents` —— 通用鼠标事件。对于 DOM 3，使用 `MouseEvent`。
- `MutationEvents` —— 通用 DOM 变变事件。对于 DOM 3，使用 `MutationEvent`。
- `HTMLEvents` —— 通用 HTML 事件。没有对应的 DOM 3 事件（HTML 事件分散到了其他分组中）。

注意，键盘事件在 DOM 2 事件中没有专门描述，直到后来在 DOM 3 事件中才引入。Internet Explorer 9 是目前唯一支持 DOM 3 键盘事件的浏览器。然而，可以使用其他浏览器中可用的方法来模拟键盘事件。

一旦创建了事件对象，就需要用事件的信息对其进行初始化。每个类型的事件对象都有一个特定的方法用于使用适当的数据对其初始化。方法的名称取决于与 `createEvent()` 使用的参数。

事件模拟的最后一步是触发事件。这是通过使用所有支持事件的 DOM 节点上存在的 `dispatchEvent()` 方法来实现的。`dispatchEvent()` 方法接受一个参数，代表要触发的事件对象。从那时起，事件将变为“正式”的，开始冒泡并导致事件处理程序的执行。

### 模拟鼠标事件

可以通过创建一个新的鼠标事件对象并为其分配必要的信息来模拟鼠标事件。通过向 `createEvent()` 方法传递 `"MouseEvents"` 可以创建一个鼠标事件对象。返回的对象有一个名为 `initMouseEvent()` 的方法，用于分配鼠标相关信息。该方法接受 15 个参数，每个参数对应鼠标事件中通常可用的一个属性。参数如下：

- `type` (string) — 要触发的事件类型，例如 `"click"`。
- `bubbles` (Boolean) — 指明事件是否应该冒泡。为了准确模拟鼠标事件，应将其设置为 `true`。
- `cancelable` (Boolean) — 指明事件是否可以被取消。为了准确模拟鼠标事件，应将其设置为 `true`。
- `view` (AbstractView) — 与事件关联的视图。这几乎总是 `document.defaultView`。
- `detail` (integer) — 事件的额外信息。这仅由事件处理程序使用，尽管它通常被设置为 `0`。
- `screenX` (integer) — 事件相对于屏幕的 x 坐标。
- `screenY` (integer) — 事件相对于屏幕的 y 坐标。
- `clientX` (integer) — 事件相对于视口的 x 坐标。
- `clientY` (integer) — 事件相对于视口的 y 坐标。
- `ctrlKey` (Boolean) — 指明是否按下 Ctrl 键。默认为 `false`。
- `altKey` (Boolean) — 指明是否按下 Alt 键。默认为 `false`。
- `shiftKey` (Boolean) — 指明是否按下 Shift 键。默认为 `false`。
- `metaKey` (Boolean) — 指明是否按下 Meta 键。默认为 `false`。
- `button` (integer) — 指明按下哪个按钮。默认为 `0`。
- `relatedTarget` (object) — 与事件相关的对象。这仅在模拟 `mouseover` 或 `mouseout` 时使用。

显而易见，`initMouseEvent()` 的参数直接映射到鼠标事件的事件对象属性。前四个参数是事件正确执行所的关键参数，因为它们被浏览器使用；其他参数仅供事件处理程序使用。事件对象的 `target` 属性在它被传递给 `dispatchEvent()` 方法时会自动设置。例如，以下代码使用默认值模拟了对按钮的点击：

![image](img/logo1.gif)

```javascript
var btn = document.getElementById("myBtn");

//创建事件对象
var event = document.createEvent("MouseEvents");

//初始化事件对象
event.initMouseEvent("click", true, true, document.defaultView, 0, 0, 0, 0, 0,
                     false, false, false, false, 0, null);

//触发事件
btn.dispatchEvent(event);
```

`SimulateDOMClickExample01.htm`

在符合 DOM 标准的浏览器中，所有鼠标事件（包括 `dblclick`）都可以使用相同的技术进行模拟。

### 模拟键盘事件

如之前所述，键盘事件被排除在 DOM Level 2 事件之外，因此模拟键盘事件并不简单。键盘事件曾包含在 DOM Level 2 事件的草案中，但在最终确定之前被移除。Firefox 实现了键盘事件的草案版本。值得注意的是，DOM Level 3 中的键盘事件与最初包含在 DOM Level 2 中的草案版本有很大不同。

DOM Level 3 创建键盘事件的方法是通过向 `createEvent()` 方法传递 `"KeyboardEvent"`。这样做会创建一个带有 `initKeyboardEvent()` 方法的事件对象。该方法具有以下参数：

- `type` (string) — 要触发的事件类型，例如 `"keydown"`。
- `bubbles` (Boolean) — 指明事件是否应该冒泡。为了准确模拟鼠标事件，应将其设置为 `true`。
- `cancelable` (Boolean) — 指明事件是否可以被取消。为了准确模拟鼠标事件，应将其设置为 `true`。
- `view` (AbstractView) — 与事件关联的视图。这几乎总是 `document.defaultView`。
- `key` (string) — 按下的按键的字符串代码。
- `location` (integer) — 按下按键的位置。0 表示默认键盘，1 表示左侧，2 表示右侧，3 表示数字小键盘，4 表示移动设备（指示虚拟键盘），5 表示摇 jo 杆。
- `modifiers` (string) — 用空格分隔的修饰符列表，例如 `"Shift"`。
- `repeat` (integer) — 该键连续被按下的次数。

请记住，DOM Level 3 事件废弃了 `keypress` 事件，因此你只能使用此技术模拟 `keydown` 和 `keyup` 事件：

![image](img/logo1.gif)

```javascript
var textbox = document.getElementById("myTextbox"),
    event;

//使用 DOM Level 3 方式创建事件对象
if (document.implementation.hasFeature("KeyboardEvents", "3.0")){
    event = document.createEvent("KeyboardEvent");

    //初始化事件对象
    event.initKeyboardEvent("keydown", true, true, document.defaultView, "a", 0, "Shift", 0);
}
```

触发事件

`SimulateDOMKeyEvent01.htm`

此示例模拟了在按住 Shift 键时按下 A 键。在尝试使用 `document.createEvent("KeyboardEvent")` 之前，你应该始终检查是否支持 DOM Level 3 事件；其他浏览器会返回非标准的 `KeyboardEvent` 对象。

Firefox 允许通过向 `createEvent()` 传递 `"KeyEvents"` 来创建键盘事件。这返回一个带有 `initKeyEvent()` 方法的事件对象，该方法接受以下 10 个参数：

- `type` (string) — 要触发的事件类型。
- `bubbles` (Boolean) — 指明事件是否应该冒泡。为了准确模拟鼠标事件，应将其设置为 `true`。
- `cancelable` (Boolean) — 指明事件是否可以被取消。为了准确模拟鼠标事件，应将其设置为 `true`。
- `view` (AbstractView) — 与事件关联的视图。这几乎总是 `document.defaultView`。
- `ctrlKey` (Boolean) — 指明是否按下 Ctrl 键。默认为 `false`。
- `altKey` (Boolean) — 指明是否按下 Alt 键。默认为 `false`。
- `shiftKey` (Boolean) — 指明是否按下 Shift 键。默认为 `false`。
- `metaKey` (Boolean) — 指明是否按下 Meta 键。默认为 `false`。
- `keyCode` (integer) — 按下或释放的按键代码。这用于 `keydown` 和 `keyup`。默认为 `0`。
- `charCode` (integer) — 按键按下生成的字符的 ASCII 码。这用于 `keypress`。默认为 `0`。

然后可以通过将此事件对象传递给 `dispatchEvent()` 来触发键盘事件，如下例所示：

```javascript
//仅限 Firefox
var textbox = document.getElementById("myTextbox");

//创建事件对象
var event = document.createEvent("KeyEvents");

//初始化事件对象
event.initKeyEvent("keydown", true, true, document.defaultView, false, false,
                   true, false, 65, 65);

//触发事件
textbox.dispatchEvent(event);
```

`SimulateFFKeyEventExample01.htm`

```javascript
var textbox = document.getElementById("myTextbox");

//create event object
var event = document.createEvent("Events");

//initialize the event object
event.initEvent(type, bubbles, cancelable);

event.view = document.defaultView;

event.altKey = false;
event.ctrlKey = false;
event.shiftKey = false;
event.metaKey = false;

event.keyCode = 65;
event.charCode = 65;

//fire the event
textbox.dispatchEvent(event);
```

这段代码创建了一个通用事件，通过 `initEvent()` 对其进行初始化，然后分配了键盘事件信息。有必要使用通用事件而不是 UI 事件，因为 UI 事件会阻止向事件对象添加新属性（Safari 除外）。通过以这种方式模拟事件会导致键盘事件触发，但文本不会被放入文本框中，因为这并没有准确地模拟键盘事件。

### 模拟其他事件

鼠标事件和键盘事件是浏览器中最经常模拟的事件，尽管也可能模拟变异事件（mutation events）和 HTML 事件。要模拟变异事件，请使用 `createEvent("MutationEvents")` 创建一个新的变异事件对象，该对象具有 `initMutationEvent()` 方法。该事件的参数为 `type`、`bubbles`、`cancelable`、`relatedNode`、`prevValue`、`newValue`、`attrName` 和 `attrChange`。模拟变异事件的形式如下：

```javascript
var event = document.createEvent("MutationEvents");

event.initMutationEvent("DOMNodeInserted", true, false, someNode, "", "", "", 0);

target.dispatchEvent(event);
```

这段代码模拟了 `DOMNodeInserted` 事件。所有其他变异事件可以使用相同的代码代码并更改参数来模拟。

HTML 事件通过创建事件对象、使用 `createEvent("HTMLEvents")` 然后使用 `initEvent()` 初始化事件对象来实现模拟。这是一个示例：

```javascript
var event = document.createEvent("HTMLEvents");

event.initEvent("focus", true, false);

target.dispatchEvent(event);
```

此示例在给定的目标上触发 `focus` 事件。其他 HTML 事件也可以以相同的方式模拟。

![image](img/pen.gif)

变异事件和 HTML 事件在浏览器中很少使用，因为它们的用途有限。

### 自定义 DOM 事件

DOM Level 3 规定了一类被称为自定义事件的事件。自定义事件不会由 DOM 原生触发，但提供它们是为了让开发者可以创建自己的事件。你通过调用 `createEvent("CustomEvent")` 创建一个新的自定义事件。返回的对象有一个名为 `initCustomEvent()` 的方法，它接受四个参数：

- `type`（字符串）—— 要触发的事件类型，例如 `"keydown"`。
- `bubbles`（布尔值）—— 表示事件是否冒泡。
- `cancelable`（布尔值）—— 表示事件是否可以被取消。
- `detail`（对象）—— 任意值。这会填充事件对象的 `detail` 属性。

创建的事件可以像任何其他事件一样在 DOM 中分发。例如：

![image](img/logo1.gif)

```javascript
var div = document.getElementById("myDiv"),
    event;

EventUtil.addHandler(div, "myevent", function(event){
    alert("DIV: " + event.detail);
});

EventUtil.addHandler(document, "myevent", function(event){
    alert("DOCUMENT: " + event.detail);
});

if (document.implementation.hasFeature("CustomEvents", "3.0")){
    event = document.createEvent("CustomEvent");
    event.initCustomEvent("myevent", true, false, "Hello world!");
    div.dispatchEvent(event);
}
```



`SimulateDOMCustomEventExample01.htm`

此示例创建了一个名为 `"myevent"` 的冒泡事件。`event.detail` 的值被设置为简单的字符串，然后在 `<div>` 元素和文档级别上对其进行监听。因为使用 `initCustomEvent()` 将事件指定为冒泡，浏览器会处理将事件冒泡到文档级别。

自定义 DOM 事件仅在 Internet Explorer 9+ 和 Firefox 6+ 中支持。

## Internet Explorer 事件模拟

Internet Explorer 8 及更早版本中的事件模拟遵循与 DOM 中事件模拟相似的模式：你创建一个事件对象，分配适当的信息，然后使用该对象触发事件。当然，Internet Explorer 有不同的方法来执行每一步操作。

`document` 的 `createEventObject()` 方法创建一个事件对象。与 DOM 不同，该方法不接受参数并返回一个通用事件对象。之后，你必须手动分配你想要在对象上拥的所有属性。（没有方法可以实现这一点。）最后一步是在 `target` 上调用 `fireEvent()`，它接受两个参数：事件处理程序的名称和事件对象。当调用 `fireEvent()` 时，`srcElement` 和 `type` 属性会自动分配给事件对象；所有其他属性都必须手动分配。这意味着 Internet Explorer 支持的所有事件都是使用相同的算法模拟的。例如，以下代码在按钮上触发了点击事件：

![image](img/logo1.gif)

```javascript
var btn = document.getElementById("myBtn");

//create event object
var event = document.createEventObject();

//initialize the event object
event.screenX = 100;
event.screenY = 0;
event.clientX = 0;
event.clientY = 0;
event.ctrlKey = false;
event.altKey = false;
event.shiftKey = false;
event.button = 0;

//fire the event
btn.fireEvent("onclick");
```

`SimulateIEClickExample01.htm`

Internet Explorer 8 及更早版本中的事件模拟遵循与 DOM 模拟模拟相似的模式：你创建一个事件对象，分配适当的信息，然后使用该对象触发事件。当然，Internet Explorer 有不同的方法来执行每一步操作。

`document` 的 `createEventObject()` 方法创建一个事件对象。与 DOM 不同，该方法不接受参数并返回一个通用事件对象。之后，你必须手动分配你想要在对象上拥的所有属性。（没有方法可以实现这一点。）最后一步是在 `target` 上调用 `fireEvent()`，它接受两个参数：事件处理程序的名称和事件对象。当调用 `fireEvent()` 时，`srcElement` 和 `type` 属性会自动分配给事件对象；所有其他属性都必须手动分配。这意味着 Internet Explorer 支持的所有事件都是使用相同的算法模拟的。例如，以下代码在按钮上触发了点击事件：

![image](img/logo1.gif)

```javascript
var textbox = document.getElementById("myTextbox");

//create event object
var event = document.createEventObject();

//initialize the event object
event.altKey = false;
event.ctrlKey = false;
event.shiftKey = false;
event.keyCode = 65;

//fire the event
textbox.fireEvent("onkeypress");
```

`SimulateIEKeyEventExample01.htm`

由于鼠标、键盘或其他事件的事件对象之间没有区别，注意，与键盘事件模拟一样，即使事件处理程序会触发，文本框中也不会显示模拟按键的结果。

## 总结

事件是 JavaScript 与网页页面绑定的主要方式。大多数常见事件定义在 DOM Level 3 事件规范或 HTML5 中。尽管对基础事件有规范，但许多浏览器已经超出了规范并实现了专用事件，以便开发者对用户交互有更深入洞察。

关于事件有一些内存和性能考虑，例如：

* 最好限制页面上事件处理器的数量，因为它们会占用更多内存并使页面响应不敏感。
* 可以使用事件委托利用事件冒泡来限制事件处理器的数量。
* 在页面卸载之前移除所有添加的事件处理器是一个好习惯。

可以使用 JavaScript 在浏览器中模拟事件。DOM Level 2 和 3 事件规范提供了对所有事件的模拟，使其轻松模拟所有定义的事件。通过结合其他技术，也可以在一定程度上模拟键盘事件。

事件是 JavaScript 中最重要的主题之一，深入了解它们的工作原理以及对性能的影响至关重要。

# 本章内容

* 了解表单基础知识
* 文本框验证与交互
* 与其他表单控件配合工作

JavaScript 的原始用途之一是将表单处理的某些职责交由浏览器，而不是依赖服务器来完成所有工作。尽管 Web 和 JavaScript 自那以后经历了演变，但 Web 表单在很大程度上保持不变。由于 Web 表单未能为常见问题提供开箱即用的解决方案，导致开发者使用 JavaScript 不仅是为了表单验证，为了增强标准表单控件的默认行为。

## 表单基础

Web 表单由 HTML 中的 `<form>` 元素表示，并在 JavaScript 中的 `HTMLFormElement` 类型表示。`HTMLFormElement` 类型继承自 `HTMLElement`，因此具有与其他 HTML 元素相同的所有默认属性。然而，`HTMLFormElement` 还具有以下额外的属性和方法：

* `acceptCharset`: 服务器可以处理的字符集；等同于 HTML 的 `accept-charset` 属性。
* `action`: 发送请求的 URL；等同于 HTML 的 `action` 属性。
* `elements`: 表单中所有控件的 `HTMLCollection`。
* `enctype`: 请求的编码类型；等同于 HTML 的 `enctype` 属性。
* `length`: 表单中控件的数量。
* `method`: 要发送的 HTTP 请求类型，通常为 `"get"` 或 `"post"`;等同于 HTML 的 `method` 属性。
* `name`: 表单的名称；等同于 HTML 的 `name` 属性。
* `reset()`: 将所有表单字段重置为默认值。
* `submit()`: 提交表单。
* `target`: 用于发送请求和接收响应的窗口名称；等同于 HTML 的 `target` 属性。

可以通过多种不同的方法获取 `<form>` 元素的引用。最常见的方法是将它们视为任何其他元素并分配 `id` 属性，允许像下面的示例所示使用 `getElementById()`：

```javascript
var form = document.getElementById("form1");
```

页面上的所有表单也可以从 `document.forms` 集合中获取。可以通过数字索引和名称访问此集合中的每个表单，如下示例所示：

```javascript
var firstForm = document.forms[0];      //获取页面上的第一个表单
var myForm = document.forms["form2"];   //获取名称为 "form2" 的表单
```

旧浏览器或具有严格向后兼容性的浏览器还会将每个具名的表单作为 `document` 对象的属性添加。例如，名为 `"form2"` 的表单可以通过 `document.form2` 访问。不建议使用这种方法，因为它很容易出错并且可能在未来从浏览器中移除。

注意，表单可以同时拥有 `id` 和 `name`，且这些值不需要相同。

## 提交表单

当用户交互提交按钮或图像按钮时，表单会被提交。提交按钮使用 `<input>` 元素或 `type` 属性为 `"submit"` 的 `<button>` 元素定义，图像按钮使用 `type` 属性为 `"image"` 的 `<input>` 元素定义。以下所有内容在点击时都会提交其所在的表单：

```html
<!-- 通用提交按钮 -->
<input type="submit" value="Submit Form">

<!-- 自定义提交按钮 -->
<button type="submit">Submit Form</button>

<!-- 图像按钮 -->
<input type="image" src="graphic.gif">
```

如果这些类型按钮中的任何一个位于具有提交按钮的表单内，在表单控件获得焦点时按下键盘上的 Enter 键也会提交表单。（唯一的例外是 `textarea`，在其中按 Enter 会创建一个新行文本。）注意，没有提交按钮的表单在按下 Enter 键时不会提交。

当以这种方式提交表单时，`submit` 事件会在请求发送到服务器之前触发。这给了你一个机会来验证表单数据并决定是否允许表单提交。阻止事件的默认行为可以取消表单提交。例如，以下代码可以防止表单被提交：

```javascript
var form = document.getElementById("myForm");

EventUtil.addHandler(form, "submit", function(event){
    //获取事件对象
    event = EventUtil.getEvent(event);

    //阻止表单提交
    EventUtil.preventDefault(event);
});
```

此代码使用了上一章中的 `EventUtil` 对象来提供跨浏览器事件处理。`preventDefault()` 方法停止表单提交。通常，当表单中的数据无效且不应发送到服务器时使用此功能。

可以通过 JavaScript 调用 `submit()` 方法程序化地提交表单。该方法可以随时调用以提交表单，且不需要表单中存在提交按钮即可正常工作。这是一个示例：

```javascript
var form = document.getElementById("myForm");

//提交表单
form.submit();
```

当通过 `submit()` 提交表单时，`submit` 事件不会触发，因此务必在调用该方法之前进行数据验证。

表单提交最大的问题之一是可能会重复提交表单。用户在看起来没有发生任何事情时有时会失去耐心，并多次点击提交按钮。结果可能是恼人的的（因为服务器会处理重复请求）或具有破坏性的（如果用户尝试购买并最终下了多个订单）。解决这个问题本质上有两种方法：在表单提交后禁用提交按钮，或者使用 `ons` 事件处理程序取消后续提交。

## 重置表单

当用户点击重置按钮时，表单会被重置。重置按钮使用 `<input>` 元素或 `type` 属性为 `"reset"` 的 `<button>` 元素创建，如下示例所示：

```html
<!-- 通用重置按钮 -->
<input type="reset" value="Reset Form">

<!-- 自定义重置按钮 -->
<button type="reset">Reset Form>
```

这两个按钮中的任何一个都可以重置表单。当重置表单时，所有的表单字段将设置回最初渲染时的值。如果某个字段最初为空，它将再次变为空，而具有默认值的字段将恢复到该值。

当用户通过点击重置按钮重置表单时，`reset` 事件会触发。该事件给了你必要时取消重置的机会。例如，以下代码可以防止表单被重置：

```javascript
var form = document.getElementById("myForm");

EventUtil.addHandler(form, "reset", function(event){
    //获取事件对象
    event = EventUtil.getEvent(event);

    //阻止表单重置
    EventUtil.preventDefault(event);
});
```

与表单提交一样，可以通过 JavaScript 使用 `reset()` 方法来实现表单重置，如下所示：

```javascript
var form = document.getElementById("myForm");

//重置表单
form.reset();
```

与 `submit()` 方法的功能不同，`reset()` 触发事件与点击重置按钮相同。

![image](img/pen.gif)

表单重置通常被认为是一种不受欢迎的 Web 表单设计方法。它通常会让用户感到困惑，并且在意外触发时会令人非常沮丧。几乎不需要重置表单。提供一个取消按钮带用户返回上一个页面，通常比显式地重置表单中的所有值足够了。

## 表单字段

可以使用原生 DOM 方法像访问页面上的任何其他元素一样访问表单元素。此外，所有表单元素都是元素集合的一部分，该集合是每个表单的属性。`elements` 集合是表单中所有表单字段引用的有序列表，包含了所有的 `<input>`、`<textarea>`、`<button>`、`<select>` 和 `<fieldset>` 元素。每个表单字段按照其在标记中的顺序出现在 `elements` 集合，并通过位置和名称进行索引。以下是一些示例：

```javascript
var form = document.getElementById("form1");

//获取表单中的第一个字段
var field1 = form.elements[0];

//获取名为 "textbox1" 的字段
var field2 = form.elements["textbox1"];

//获取字段数量
var fieldCount = form.elements.length;
```

如果一个名称被多个表单控件使用（如单选按钮所示），则会返回一个包含所有该名称元素的 `HTMLCollection`。例如，考虑以下 HTML 代码段：

![image](img/logo1.gif)

```html
<form method="post" id="myForm">
    <ul>
        <li><input type="radio" name="color" value="red">Red</li>
        <li><input type="radio" name="color" value="green">Green</li>
        <li><input type="radio" name="color" value="blue">Blue</li>
    </ul> 
</form>
```

`FormFieldsExample01.htm`

此 HTML 中的表单有三个名为 `"color"` 的单选控件，这把字段关联在一起。当访问 `elements["color"]` 时，会返回一个包含所有三个元素的 `NodeList`；然而，当访问 `elements[0]` 时，只返回第一个元素。考虑这个示例：

```javascript
var form = document.getElementById("myForm");
var colorFields = form.elements["color"];

alert(colorFields.length);  //3

var firstColorField = colorFields[0];
var firstFormField = form.elements[0];

alert(firstColorField === firstFormField);   //true
```

`FormFieldsExample01.htm`

这段代码表明通过 `form.elements[0]` 访问的第一个表单字段与 `form.elements["color"]` 中包含的第一个元素是同一个。

![image](img/pen.gif)

也可以作为表单的属性访问元素，例如使用 `form[0]` 获取第一个表单字段，使用 `form["color"]` 获取命名字段。这些属性返回的内容始终与其在 `elements` 集合中的等效内容相同。提供这种方法是为了兼容旧版浏览器，应尽可能避免使用，而是使用 `elements`。

### 常用的表单字段属性

除了 `<fieldset>` 元素外，所有表单字段共享一组公共属性。由于 `<input>` 类型代表许多表单字段，某些属性仅用于特定的字段类型，而其他属性无论字段类型如何都可以使用。常用的表单字段属性和方法如下：

* `disabled` — 布尔值，表示字段是否被禁用。
* `form` — 指向字段所属表单的指针。该属性是只读的。
* `name` — 字段的名称。
* `readOnly` — 布尔值，表示字段是否为只读。
* `tabIndex` — 指定字段的制表顺序。
* `type` — 字段类型：`"checkbox"`、`"radio"` 等。
* `value` — 将提交到服务器的字段值。对于文件输入字段，此属性为只读，仅包含文件在计算机上的路径。

除了 `form` 属性外，JavaScript 可以动态更改所有其他属性。考虑这个示例：

```javascript
var form = document.getElementById("myForm");
```



`var field = form.elements[0];`

```javascript
//更改值
field.value = "Another value";

//检查表单的值
alert(field.form === form);   //true

//为字段设置焦点
field.focus();

// 禁用字段
field.disabled = true;

// 更改字段类型（不推荐，但对 <input> 可行）
field.type = "checkbox";
```

动态更改表单字段属性的能力允许你随时、以几乎任何方式更改表单。例如，Web 表单的一个常见问题是用户往往倾向于双击点击提交按钮。这在涉及信用卡订单时是一个大问题，因为可能导致重复收费。解决此问题的一个常用方法是在点击提交按钮后将其禁用，这可以通过监听`submit`事件并在其发生时禁用提交按钮来实现。以下代码实现了这一点：

![image](img/logo1.gif)

```javascript
// 防止多次提交表单的代码
EventUtil.addHandler(form, "submit", function(event){
    event = EventUtil.getEvent(event);
    var target = EventUtil.getTarget(event);

    //获取提交按钮
    var btn = target.elements["submit-btn"];

    // 禁用它
    btn.disabled = true;
});
```

`FormFieldsExample02.htm`

这段代码在表单上绑定了`submit`事件的事件处理器。当事件触发时，会获取提交按钮并将其`disabled`属性设置为`true`。

### 常用的表单字段方法

每个表单字段有两个公共方法：`focus()`和`blur()`。`focus()`方法将浏览器焦点设置到表单字段，这意味着该字段变为激活状态并响应键盘事件。例如，接收焦点的文本框会显示光标并准备好接受输入。`focus()`方法通常用于将注意力引导到页面的某个位置。例如，在页面加载时将焦点移动到表单的第一个字段是非常常见的。这可以通过监听`load`事件并对第一个字段调用`focus()`来完成，如下例：

```javascript
EventUtil.addHandler(window, "load", function(event){
    document.forms[0].elements[0].focus();
});
```

注意，如果第一个表单字段是类型为`"hidden"`的`<input>`元素，或者使用 CSS 属性`display`或`visibility`隐藏了字段，此代码会导致错误。

HTML5 为表单字段引入了`autofocus`属性，支持浏览器会自动为该元素设置焦点，而无需使用 JavaScript。例如：

```html
<input type="text" autofocus>
```

为了让之前的代码与`autofocus`正常工作，你必须先检测是否设置了该属性，如果是，则不要调用`focus()`：

![image](img/logo1.gif)

```javascript
EventUtil.addHandler(window, "load", function(event){
    var element = document.forms[0].elements[0];
    if (element.autofocus !== true){
        element.focus(); 
        console.log("JS focus");
    }
});
```

`FocusExample01.htm`

由于`autofocus`是一个布尔属性，在支持的浏览器中，`autofocus`属性的值将为`true`。（在不支持的浏览器中它将为空字符串。）因此，这段代码仅在`autofocus`属性不等于`true`时调用`focus()`，以确保向后兼容。`autofocus`属性受 Firefox 4+、Safari 5+、Chrome 和 Opera 9.6+ 支持。

![image](img/pen.gif)

默认情况下，只有表单元素可以设置焦点。通过将其`tabIndex`属性设置为`-1`然后调用`focus()`，可以允许任何元素拥有焦点。唯一不支持这种技术的浏览器是 Opera。

`focus()`的反操作是`blur()`，它会移除元素上的焦点。当调用`blur()`时，焦点不会移动到任何特定的元素上；它只是从调用它的字段中被移除了。在 Web 开发早期，这种方法被用于在`readonly`属性引入之前创建只读字段。虽然极少不需要调用`blur()`，但如有需要，可以使用。这里有一个示例：

```javascript
document.forms[0].elements[0].blur();
```

### 常见表单字段事件

所有表单字段除了鼠标、键盘、变变和 HTML 事件外，还支持以下三个事件：

* `blur` — 当字段失去焦点时触发。
* `change` — 当字段失去焦点且值发生变化时，对于`<input>`和`<textarea>`元素触发；当`<select>`元素的选定选项改变时也会触发。
* `focus` — 当字段获得焦点时触发。

`blur`和`focus`事件的触发是因为用户手动更改了字段焦点，以及分别调用了`blur()`和`focus()`方法。这两个事件在所有表单字段中的工作方式相同。然而，`change`事件在不同控件上的触发时间不同。对于`<input>`和`<textarea>`元素，`change`事件在字段失去焦点且值自控件获得焦点以来发生变化时触发。但对于`<select>`元素，每当用户更改选定选项时`change`事件就会触发；控件不需要失去焦点即可触发`change`。

`focus`和`blur`事件通常用于以某种方式更改用户界面，提供视觉提示或额外功能（例如为文本框显示选项下拉菜单）。`change`事件通常用于验证输入到字段的数据。例如，考虑一个只允许输入数字的文本框。`focus`事件可以用于更改背景颜色，以更清楚地指示该字段已获得焦点，`blur`事件可以用于移除该背景颜色，如果输入了非数字字符，`change`事件可以将背景颜色更改为红色。以下代码实现了这一点：

![image](img/logo1.gif)

```javascript
var textbox = document.forms[0].elements[0];

EventUtil.addHandler(textbox, "focus", function(event){
    event = EventUtil.getEvent(event);
    var target = EventUtil.getTarget(event);
    if (target.style.backgroundColor != "red"){
        target.style.backgroundColor = "yellow";
    }
});

EventUtil.addHandler(textbox, "blur", function(event){
    event = EventUtil.getEvent(event);
    var target = EventUtil.getTarget(event);
    if (/[^\d]/.test(target.value)){
        target.style.backgroundColor = "red";
    } else {
        target.style.backgroundColor = "";
    }
});

EventUtil.addHandler(textbox, "change", function(event){
    event = EventUtil.getEvent(event);
    var target = EventUtil.getTarget(event);
    if (/[^\d]/.test(target.value)){
        target.style.backgroundColor = "red";
    } else {
        target.style.backgroundColor = "";
    }
});
```

`FormFieldEventsExample01.htm`

`onfocus`事件处理器简单地将文本框的背景颜色更改为黄色，以更清楚地指示它是活动字段。`onblur`和`onchange`事件处理器在发现任何非数字字符时会将背景颜色更改为红色。要测试非数字字符，请对文本框的值使用简单的正则表达式。此项功能必须同时存在于`onblur`和`onchange`事件处理器中，以确保无论文本框如何变化，行为保持一致。

![image](img/pen.gif)

`blur`和`change`事件之间的关系并没有严格定义。在某些浏览器中，`blur`事件在`change`之前触发；在另一些浏览器中则相反。你不能依赖这些事件触发的顺序，因此在需要它们时要务必小心。

## 脚本文本框

在 HTML 中表示文本框有两种方式：使用`<input>`元素的单行版本和使用`<textarea>`的多行版本。这两个控件非常相似，在大多数情况下行为也相似。

默认情况下，`<input>`元素显示一个文本框，即使省略了`type`属性（默认值为`"text"`）。然后可以使用`size`属性来指定文本框在可见字符数上的宽度。`value`属性指定了文本框的初始值，`maxlength`属性指定了文本框中允许的最大字符数。因此，要创建一个一次可以显示 25 个字符但最大长度为 50 个字符的文本框，可以使用：

```html
<input type="text" size="25" maxlength="50">
```

`<textarea>`始终渲染多行文本框。要指定文本框的大小，可以使用`rows`属性（以字符数指定高度）和`cols`属性（以字符数指定宽度），类似于`<input>`的`size`属性。与`<input>`不同，`<textarea>`的初始值必须封装在`<textarea>`和`</textarea>`之间，如下：

```html
<textarea rows="25" cols="50">initial value</textarea>
```

此外，不像`<input>`元素，`<textarea>`无法指定最大字符数。两种控件都将其内容存储在`value`属性中。`value`可用于读取和设置文本框值，如本例所示：

```javascript
var textbox = document.forms[0].elements["1"];
alert(textbox.value);
textbox.value = "Some new value";
```

建议使用`value`属性来读取或写入文本框值，而不是使用 DOM 方法。例如，不要使用`setAttribute()`来设置`<input>`元素的`value`属性，不要尝试修改`<textarea>`元素的第一个子节点。`value`属性的变化并不总是反映在 DOM 中。

### 文本选择

两种文本框都支持`select()`方法，用于选择文本框中的所有文本。调用该方法时，大多数会将焦点设置到文本框上（Opera 除外）。该方法不接受参数，可以随时调用。这里有一个示例：

```javascript
var textbox = document.forms[0].elements["1"];
textbox.select();
```

当文本框获得焦点时选择其中的所有文本是常见做法，特别是当文本框有默认值时。这种做法是为了让用户更方便，他们不需要单独删除文本。这种模式通过以下代码实现：

```javascript
EventUtil.addHandler(textbox, "focus", function(event){
    event = EventUtil.getEvent(event);
    var target = EventUtil.getTarget(event);
    target.select();
});
```

与`select()`方法对应的是一个`select`事件。`select`事件在文本框中的文本被选中时触发。事件触发的确切时机因浏览器而异。在 Internet Explorer 9+、`Opera`、`Firefox`、`Chrome`和`Safari`中，`select`事件在用户完成文本选择后触发；而在 Internet Explorer 8 及更早版本中，它在选中任意一个字母时就会触发。调用`select()`方法时也会触发`select`事件。这里有一个简单的示例：

![image](https://images/logo1.gif)

```javascript
var textbox = document.forms[0].elements["textbox1"];
EventUtil.addHandler(textbox, "select", function(event){
    var alert("Text selected: " + textbox.value);
});
```

`SelectEventExample01.htm`

## 获取被选文本

虽然`select`事件对于理解何时选中文本很有用，但它并没有提供任何关于选中了什么文本的信息。HTML5 通过引入一些扩展解决了这个问题，允许能够更好地获取被选文本。规范方法为文本框添加了两个属性：`selectionStart`和`selectionEnd`。这些属性包含从零开始的数字，表示文本选择的边界（分别为文本选择起始的偏移量和文本选择结束的偏移量）。因此，要获取文本框中的被选文本，可以使用以下代码：

```javascript
function getSelectedText(textbox){
    return textbox.value.substring(textbox.selectionStart, textbox.selectionEnd);
}
```

由于`substring()`方法作用于字符串偏移量，可以直接传递`selectionStart`和`selectionEnd`的值来获取被选文本。

此解决方案适用于 Internet Explorer 9+、`Firefox`、`Safari`、`Chrome`和`Opera`。Internet Explorer 8 及更早版本不支持这些属性，因此需要不同的方法。

旧版本的 Internet Explorer 有一个`document.selection`对象，它包含整个文档的文本选择信息，这意味着你无法确定被选文本在页面上的位置。然而，与`select`事件配合使用时，你可以确保选择是在触发事件的文本框内。要获取被选文本，必须先创建一个范围（在第 12 节中讨论），然后从中提取文本，如下所示：

```javascript
function getSelectedText(textbox){
    if (typeof textbox.selectionStart == "number"){
        return textbox.value.substring(textbox.selectionStart, 
                                       textbox.selectionEnd);                
    } else if (document.selection){
        return document.selection.createRange().text;
    }
}
```

`TextboxGetSelectedTextExample01.htm`

该函数经过修改，以判断是否使用 Internet Explorer 方法处理被选文本。注意，`document.selection`完全不需要`textbox`参数。

## 部分文本选择

HTML5 还规定了一个额外的功能，用于辅助在文本框中部分选择文本。`setSelectionRange()`方法最初由`Firefox`实现，现在除了`select()`方法外，所有文本框上都可用。该方法接受两个参数：要选择的第一个字符的索引，以及停止选择的索引（与字符串的`substring()`方法相同）。以下是一些示例：

```javascript
textbox.value = "Hello world!"

//选择所有文本
textbox.setSelectionRange(0, textbox.value.length);    //"Hello world!"

//选择前三个字符
textbox.setSelectionRange(0, 3);    //"Hel"

//选择第 4 到第 6 个字符
textbox.setSelectionRange(4, 7);    //"o w"
```



要看到选择结果，必须在调用`setSelectionRange()`之前或之后为文本框设置焦点。这种方法适用于 Internet Explorer 9、`Firefox`、`Safari`、`Chrome`和`Opera`。

Internet Explorer 8 及更早版本通过使用范围（在第 12 节中讨论）允许部分文本选择。要选择文本框中的部分文本，必须先创建一个范围，并使用 Internet Explorer 在文本框提供的`createTextRange()`方法将其放置在正确位置，同时使用`moveStart()`和`moveEnd()`范围方法将范围移动到位。但在调用这些方法之前，你需要使用`collapse()`将范围折叠到文本框的起始。之后，`moveStart()`将范围的起点和终点都移动到同一位置。然后你可以将选择的字符总数作为参数传递给`moveEnd()`。最后一步是使用范围的`select()`方法来选择文本，如示例所示：

```
textbox.value = "Hello world!";

var range = textbox.createTextRange();

//选择所有文本
range.collapse(true);
range.moveStart("character", 0);
range.moveEnd("character", textbox.value.length);   //"Hello world!"
range.select();

//选择前三个字符
range.collapse(true);
range.moveStart("character", 0);
range.moveEnd("character", 3);
range.select();                        //"Hel"

//选择第 4 到第 6 个字符
range.collapse(true);
range.moveStart("character", 4);
range.moveEnd("character", 3);
range.select();                        //"o w"
```

与其他浏览器一样，文本框必须拥有焦点，选择内容才会可见。

这两种技术可以组合成一个函数以便跨浏览器使用，如下例所示：

![image](https://images/logo1.gif)

```
function selectText(textbox, startIndex, stopIndex){
    if (textbox.setSelectionRange){
        textbox.setSelectionRange(startIndex, stopIndex);
    } else if (textbox.createTextRange){
        var range = textbox.createTextRange();
        range.collapse(true);
        range.moveStart("character", startIndex);
        range.moveEnd("character", stopIndex);
        range.select();
    }
    textbox.focus();
}
```

`TextboxPartialSelectionExample01.htm`

## 输入过滤

部分文本选择对于实现提供自动完成建议的高级文本框很有用。

文本框通常期望特定类型的数据或格式。可能数据需要包含某些字符或匹配特定的模式。由于文本框默认不提供很多验证功能，必须使用 JavaScript 来此类输入过滤。通过结合事件和其他 DOM 能力，你可以将普通文本框转换为理解其所处理数据的文本框。

### 阻塞字符

某些类型的输入要求特定字符必须存在或不存在。例如，电话号码文本框不应允许插入非数字。`keypress`事件负责向文本框插入字符。可以通过阻止该事件的默认行为来阻塞字符。例如，以下代码阻止了所有的按键：

```
EventUtil.addHandler(textbox, "keypress", function(event){
    event = EventUtil.getEvent(event);
    EventUtil.preventDefault(event);
});
```

运行此代码会导致文本框实际上变为只读状态，因为所有的按键都被阻塞了。要仅阻塞特定字符，你需要检查事件的字符码并确定正确的响应。例如，以下代码仅允许数字：

```
EventUtil.addHandler(textbox, "keypress", function(event){
    event = EventUtil.getEvent(event);
    var target = EventUtil.getTarget(event);
    var charCode = EventUtil.getCharCode(event);
    if (!/\d/.test(String.fromCharCode(charCode))){
        EventUtil.preventDefault(event);
    }
});
```

在此示例中，使用`EventUtil.getCharCode()`获取字符码以实现跨浏览器兼容性。使用`String.fromCharCode()`将字符码转换为字符串，并使用正则表达式`/\d/`对结果进行测试，该正则匹配所有数字字符。如果该测试失败，则使用`EventUtil.preventDefault()`阻塞事件的发生。这确保了文本框会忽略非数字键。

尽管`keypress`事件理论上只应在按下字符键时触发，但某些浏览器也会对其他键触发它。Firefox 和 Safari（3.1 之前的版本）会对向上键、向下键、Backspace 和 Delete 等键触发`keypress`；而 Safari 3.1 及更高版本则不会对这些键触发`keypress`事件。这意味着简单地阻塞所有非数字字符是不够的，因为你也会阻塞掉这些非常有用且必要的按键。幸运的是，你可以轻松检测何时按下了这些按键中的一个。在 Firefox 中，所有触发`keypress`事件的非字符键的字符码均为`0`，而 Safari 3 之前的版本中它们的字符码均为`8`。为了通用的处理这种情况情况，你不希望阻塞任何小于 10 的字符码。该函数可以更新如下：

```
EventUtil.addHandler(textbox, "keypress", function(event){
    event = EventUtil.getEvent(event);
    var target = EventUtil.getTarget(event);
    var charCode = EventUtil.getCharCode(event);
    if (!/\d/.test(String.fromCharCode(charCode)) && charCode > 9){
        EventUtil.preventDefault(event);
    }
});
```

现在，事件处理器在所有浏览器中的行为都是正确的：它阻塞了非数字字符，但允许所有同样触发`keypress`的基础按键。

还有一个问题需要处理：复制、粘贴以及任何涉及`Ctrl`键的函数。在 Internet Explorer 之外的所有浏览器中，之前的代码都会允许`Ctrl+C`、`Ctrl+V`以及任何使用`Ctrl`键的组合快捷键通过。因此，最后的检查是确保`Ctrl`键未被按下，如下例所示：

![image](img/logo1.gif)

```
EventUtil.addHandler(textbox, "keypress", function(event){
    event = EventUtil.getEvent(event);
    var target = EventUtil.getTarget(event);
    var charCode = EventUtil.getCharCode(event);
    if (!/\d/.test(String.fromCharCode(charCode)) && charCode > 9 && 
            !event.ctrlKey){
        EventUtil.preventDefault(event);
    }
});
```

`TextboxInputFilteringExample01.htm`

这一最终更改确保了所有默认文本框行为都能正常工作。这种技术可以自定义，以允许或禁止文本框中的任何字符。

## 处理剪贴板

Internet Explorer 是第一个支持与剪贴板相关的事件以及通过 JavaScript 访问剪贴板数据的浏览器。随着 Safari 2、Chrome 和 Firefox 3 实现了类似的事件和剪贴板访问，Internet Explorer 的实现成为了事实上的标准（Opera 截至 11 版本仍不支持 JavaScript 剪贴板支持），剪贴板事件后来被添加到 HTML5 中。以下六个事件与剪贴板相关：

* `beforecopy` — 在复制操作发生之前触发。
* `copy` — 在复制操作发生时触发。
* `beforecut` — 在剪切操作发生之前触发。
* `cut` — 在剪切操作发生时触发。
* `beforepaste` — 在粘贴操作发生之前触发。
* `paste` — 在粘贴操作发生时触发。

由于这是一个管理剪贴板访问的较新标准，事件及相关对象的行为在不同浏览器之间存在差异。在 Safari、Chrome 和 Firefox 中，`beforecopy`、`beforecut`和`beforepaste`事件仅在文本框右键菜单显示时触发（预判剪贴板事件），但 Internet Explorer 会在那种情况下触发它们，并在触发`copy`、`cut`和`paste`事件之前立即触发。`copy`、`cut`和`paste`事件在所有浏览器中都会在你预期的时刻触发，无论是从右键菜单中选择还是使用键盘快捷键时。

`beforecopy`、`beforecut`和`beforepaste`事件让你有机会在实际事件发生之前更改发送到剪贴板或从剪贴板获取的数据。然而，取消这些事件并不会取消剪贴板操作——你必须取消`copy`、`cut`或`paste`事件来防止操作发生。

剪贴板数据可以通过`clipboardData`对象访问，该对象存在于`window`对象上（Internet Explorer 中）或`event`对象上（Firefox 4+、Safari 和 Chrome 中）。在 Firefox、Safari 和 Chrome 中，`clipboardData`对象仅在剪贴板事件期间可用，以防止未经授权的剪贴板访问；Internet Explorer 则始终暴露`clipboardData`对象。为了跨浏览器兼容，最好只在剪贴板事件期间使用此对象。

`clipboardData`对象上有三个方法：`getData()`、`setData()`和`clearData()`。`getData()`方法从剪贴板检索字符串数据并接受单个参数，即要检索的数据格式。Internet Explorer 规定了两个选项：`text`和`URL`。Firefox、Safari 和 Chrome 期望 MIME 类型，但会将`text`等同于`text/plain`。

`setData()`方法类似：它的第一个参数是数据类型，第二个参数是要放置在剪贴板上的文本。再次强调，Internet Explorer 支持`text`和`URL`，而 Safari 和 Chrome 期望 MIME 类型。但与`getData()`不同，Safari 和 Chrome 不会识别`text`类型。只有 Internet Explorer 8 及更早版本允许调用`setData`；其他浏览器直接忽略该调用。为了消除差异，你可以向`EventUtil`中添加以下跨浏览器方法：

![image](img/logo1.gif)

```
var EventUtil = {
    //more code here
    getClipboardText: function(event){
        var clipboardData = (event.clipboardData || window.clipboardData);
        return clipboardData.getData("text");
    },
    //more code here
    setClipboardText: function(event, value){
        if (event.clipboardData){
            return event.clipboardData.setData("text/plain", value);
        } else if (window.clipboardData){
            return window.clipboardData.setData("text", value);
        }
    },
    //more code here
};
```

`EventUtil.js`

`getClipboardText()`方法相对简单。它只需要识别`clipboardData`对象的位置，然后使用`text`类型调用`getData()`。它的伴侣方法`setClipboardText()`稍微复杂一些。一旦确定了 clipboardData 对象，就会根据不同的实现调用相应的`setData()`（Firefox、Safari 和 Chrome 使用`text/plain`；Internet Explorer 使用`text`）。

```
EventUtil.addHandler(textbox, "paste", function(event){
    event = EventUtil.getEvent(event);
    var text = EventUtil.getClipboardText(event);
    if (!/^\d*$/.test(text)){
        EventUtil.preventDefault(event);
    }
});
```

`TextboxClipboardExample01.htm`

此`onpaste`处理器确保了只有数值可以被粘贴到文本框中。如果剪贴板的值与模式不匹配，则会取消粘贴。Firefox、Safari 和 Chrome 仅允许在`onpaste`事件处理器中使用`getData()`方法。

由于并非所有浏览器都支持剪贴板访问，因此阻止一个或多个剪贴板操作通常简单。在支持`copy`、`cut`和`paste`事件的浏览器（Internet Explorer、Safari、Chrome 和 Firefox 3+）中，很容易阻止事件的默认行为。对于 Opera，你需要阻止触发事件的按键并阻止上下文菜单的显示。

# 自动 Tab 键跳转

JavaScript 可以通过多种方式提高表单字段的可用性。最常见的方法之一是在当前字段完成后，自动将焦点移动到下一个字段。这在输入已知适当长度的数据时非常常见，例如电话号码。在美国，电话号码通常分为三部分：区号、交换机代码，然后是四位数字。网页上将其表示为三个文本框是非常常见的，如下所示：

```html
<input type="text" name="tel1" id="txtTel1" maxlength="3">
<input type="text" name="tel2" id="txtTel2" maxlength="3">
<input type="text" name="tel3" id="txtTel3" maxlength="4">
```

`TextboxTabForwardExample01.htm`

为了提高可用性并加快数据输入过程，你可以在输入最大字符数后自动将焦点移动到下一个元素。因此，一旦用户在第一个文本框中输入三个字符，焦点就会移动到第二个；一旦用户在第二个文本框中输入三个字符，焦点就会移动到第三个。这种“Tab 向跳转”行为可以使用以下代码实现：

![image](img/logo1.gif)

```javascript
(function(){
    function tabForward(event){            
        event = EventUtil.getEvent(event);
        var target = EventUtil.getTarget(event);
        if (target.value.length == target.maxLength){
            var form = target.form;
            for (var i=0, len=form.elements.length; i < len; i++) {
                if (form.elements[i] == target) {
                    if (form.elements[i+1]){
                        form.elements[i+1].focus();
                    }
                    return;
                }
            }



```javascript
        }

    }

    var textbox1 = document.getElementById("txtTel1");

    var textbox2 = document.getElementById("txtTel2");

    var textbox3 = document.getElementById("txtTel3");

    EventUtil.addHandler(textbox1, "keyup", tabForward);

    EventUtil.addHandler(textbox2, "keyup", tabForward);

    EventUtil.addHandler(textbox3, "keyup", tabForward);

})();
```

`TextboxTabForwardExample01.htm`

`tabForward()` 函数是该功能的关键。它通过将值与 `maxlength` 属性进行比较，检查文本框是否达到了最大长度。如果它们相等（因为浏览器强制了最大限制，所以不可能更大），则需要通过遍历元素集合来找到下一个表单元素，找到文本框后将焦点设置到下一个位置的元素。该函数然后被赋值为每个文本框的 `onkeyup` 处理器。由于 `keyup` 事件在向文本框插入新字符后触发，因此这是检查文本框内容长度的理想时机。在填写此简单表单时，用户将永远不需要按 `Tab` 键在字段之间移动并提交表单。

请记住，此代码专门针对上述提到的标记，并且没有考虑可能存在的隐藏字段。

# HTML5 约束验证 API（Constraint Validation API）

HTML5 引入了浏览器在提交到服务器之前对表单数据验证的能力。这种能力使得在 JavaScript 不可用或加载失败时也能进行基础验证。浏览器本身会根据代码中的规则处理验证，并在其上自行显示相应的错误信息（不需要额外的 JavaScript）。当然，此功能仅在支持 HTML5 此部分的浏览器中有效，包括 Firefox 4+、Safari 5+、Chrome 和 Opera 10+。

验证仅在特定条件下应用于表单字段。你可以使用 HTML 标记来指定特定字段的约束，这将导致浏览器自动执行表单验证。

## 必填字段（Required Fields）

第一个条件是表单字段具有 `required` 属性，例如所示：

```html
<input type="text" name="username" required>
```

任何标记为 `required` 的字段必须有值才能提交表单。此属性适用于 `<input>`、`<textarea>` 和 `<select>` 字段（Opera 11 之前的版本不支持 `<select>` 上的 `required`）。你可以在 JavaScript 中通过使用元素相应的 `required` 属性来检查表单字段是否必填：

```javascript
var isUsernameRequired = document.forms[0].elements["username"].required;
```

你也可以使用以下代码测试浏览器是否支持 `required` 属性：

```javascript
var isRequired = "required" in document.createElement("input");
```

此代码使用简单的功能检测来判断新创建的 `<input>` 元素是否存在 `required` 属性。

请记住，当表单字段必填时，不同浏览器的表现不同。Firefox 4 和 Opera 11 阻止表单提交并在下方弹出一个帮助框，而 Safari（5 版本）和 Chrome（9 版本）则无所作为且阻止表单提交。

## 替代输入类型（Alternate Input Types）

HTML5 为 `<input>` 元素的 `type` 属性指定了多个额外的值。这些类型属性不仅提供了关于预期数据类型的额外信息，还提供了一些默认验证。两种被广泛支持的数字输入类型是 `email` 和 `url`，它们都带有一个浏览器执行的自定义验证。例如：

```html
<input type="email" name="email">

<input type="url" name="homepage">
```

`email` 类型确保输入文本符合电子邮件地址的模式，而 `url` 类型确保输入文本符合 URL 的模式。注意，本节之前提到的所有浏览器在正确的模式匹配上都存在一些问题。最值得注意的是，文本 `-@-` 被认为是有效的电子邮件地址。此类问题仍在浏览器厂商的解决中。

你可以通过在 JavaScript 中创建一个元素并将 `type` 属性设置为 `email` 或 `url`，然后读取该值来检测浏览器是否支持这些新类型。旧浏览器会自动将未知值设为 `text`，而支持的浏览器会返回正确的值。例如：

```javascript
var input = document.createElement("input");

input.type = "email";

var isEmailSupported = (input.type == "email");
```

请记住，除非应用了 `required` 属性，否则空字段也被认为是有效的。此外，指定特殊的输入类型并阻止用户输入无效值，它仅提供了默认验证。

# 数字范围（Numeric Ranges）

除了 `email` 和 `url`，HTML5 中还定义了其他几种新的输入元素类型。这些都是期望某种基于数字输入的数值类型：`number`、`range`、`datetime`、`datetime-local`、`date`、`month`、`week` 和 `time`。这些类型在浏览器中的支持并不良好，因此应谨慎使用，或者不使用。浏览器厂商目前正在致力于更好的跨兼容性和更符合逻辑的功能。因此，本节的信息更具前瞻性，而不是对现有功能的解释。

对于这些数值类型中的每一种，你可以指定 `min` 属性（最小值）、`max` 属性（最大值）和一个 `step` 属性（从 `min` 到 `max` 刻度上每个步长之间的差）。例如，要允许 0 到 100 之间仅限 5 的倍数，你可以：

```html
<input type="number" min="0" max="100" step="5" name="count">
```

根据浏览器的不同，你可能会看到或看不到计数器（向上和向下按钮）来自动增加或减少值。

每个属性在元素上都有对应的属性，可以通过 JavaScript 访问（并更改）。此外，还有两个方法：`stepUp()` 和 `stepDown()`。这两个方法都接受一个可选参数：从当前值中减去或增加的数字（默认情况下，它们递增或递减一）。浏览器尚未实现这些方法，但它们将像示例那样可以使用：

```javascript
input.stepUp();      // 增加一

input.stepUp(5);     // 增加五

input.stepDown();    // 减少一

input.stepDown(10);  // 减少十
```

## 输入模式

`pattern` 属性在 HTML5 中为文本字段引入。该属性指定了一个正则表达式，输入值必须匹配该表达式。例如，要允许文本字段中仅包含数字，以下代码应用了这一约束：

```html
<input type="text" pattern="\d+" name="count">
```

注意，`^` 和 `$` 分别假设位于模式的开头和结尾。这意味着输入必须从头到尾完全匹配模式。

与其他备用输入类型一样，指定模式并防止用户输入无效文本。模式应用于值，然后浏览器就知道该值是否有效。你可以通过访问 `pattern` 属性来读取模式：

```javascript
var pattern = document.forms[0].elements["count"].pattern;
```

你也可以使用此代码段测试浏览器是否支持 `pattern` 属性：

```javascript
var isPatternSupported = "pattern" in document.createElement("input");
```

## 检查有效性

你可以使用 `checkValidity()` 方法检查表单上的任何给定字段是否有效。该方法在所有元素上都提供，如果字段值有效则返回 `true`，否则返回 `false`。字段是否有效基于本节之前提到的条件，因此，没有值的必填（`required`）字段被视为无效，且值不匹配 `pattern` 属性的字段也被视为无效。例如：

```javascript
if (document.forms[0].elements[0].checkValidity()) {

    // 字段有效，继续执行

} else {

    // 字段无效

}
```

要检查整个表单是否有效，你可以在表单本身使用 `checkValidity()` 方法。如果所有表单字段都有效，则返回 `true`；即使有一个无效，也返回 `false`：

```javascript
if (document.forms[0].checkValidity()) {

    // 表单有效，继续执行

} else {

    // 表单字段无效

}
```

虽然 `checkValidity()` 简单地告诉你字段是否有效，但 `validity` 属性指示了字段有效或无效的确切原因。该对象有一系列返回布尔值的属性：

- `customError` — 如果设置了 `setCustomValidity()`，则为 `true`，否则为 `false`。
- `patternMismatch` — 如果值不匹配指定的 `pattern` 属性，则为 `true`。
- `rangeOverflow` — 如果值大于 `max` 值，则为 `true`。
- `rangeUnderflow` — 如果值小于 `min` 值，则为 `true`。
- `stepMisMatch` — 如果结合 `step` 属性以及 `min` 和 `max` 值不正确，则为 `true`。
- `tooLong` — 如果值的字符数超过 `maxlength` 属性允许的范围，则为 `true`。某些浏览器（如 Firefox 4）会自动限制字符数，因此此值可能始终为 `false`。
- `typeMismatch` — 值不符合 `email` 或 `url` 的要求格式。
- `valid` — 如果其他所有属性均为 `false`，则为 `true`。该值与 `checkValidity()` 的结果相同。
- `valueMissing` — 如果字段被标记为必填且没有值，则为 `true`。

因此，你可能希望使用 `validity` 检查表单字段的有效性以获取更具体的信息，如下所示：

```javascript
if (input.validity && !input.validity.valid) {

    if (input.validity.valueMissing) {

        alert("请指定一个值.");

    } else if (input.validity.typeMismatch) {

        alert("请输入电子邮件地址.");

    } else {

        alert("值无效。");

    }

}
```

## 禁用验证

你可以通过指定 `novalidate` 属性指示表单不应用任何验证：

```html
<form method="post" action="signup.php" novalidate>

    <!-- 此处为表单元素 -->

</form>
```

可以使用 JavaScript 属性 `noValidate` 获取或设置此值，如果存在该属性则设置为 `true`，如果省略该属性则设置为 `false`：

```javascript
document.forms[0].noValidate = true;
```

如果表单中有多个提交按钮，你可以通过向按钮添加 `formnovalidate` 属性，指定当使用特定提交按钮时表单不进行验证：

```html
<form method="post" action="foo.php">

    <!-- 此处为表单元素 -->

    <input type="submit" value="普通提交">

    <input type="submit" formnovalidate name="btnNoValidate"
           value="不验证提交">

</form>
```

在此示例中，第一个提交按钮将导致表单按常进行验证，而第二个按钮将禁用验证。你也可以使用 JavaScript 设置此属性：

```javascript
document.forms[0].elements["btnNoValidate"].formNoValidate = true;
```

## 脚本化选择框

选择框使用 `<select>` 和 `<option>` 元素创建。为了方便与控件交互，`HTMLSelectElement` 类型除了所有表单字段可用的属性外，还提供了以下属性和方法：

- `add(newOption, relOption)` — 在相关选项之前向控件添加新的 `<option>` 元素。
- `multiple` — 一个布尔值，表示是否允许多选；等同于 HTML 的 `multiple` 属性。
- `options` — 控制中 `<option>` 元素的 `HTMLCollection`。
- `remove(index)` — 移除指定位置的选项。
- `selectedIndex` — 被选中选项的从零开始的索引，如果没有选中任何选项则为 `-1`。对于允许多选的选择框，这始终是选择中的第一个选项。
- `size` — 选择框中可见的行数；等同于 HTML 的 `size` 属性。

选择框的 `type` 属性为 `"select-one"` 或 `"select-multiple"`，取决于 `multiple` 属性是否存在。根据当前选中的选项决定了选择框的 `value` 属性，遵循以下规则：

- 如果没有选中任何选项，选择框的值为空字符串。
- 如果选中了一个选项且其指定了 `value` 属性，则选择框的 `value` 为该被选中选项的 `value` 属性。即使 `value` 属性为空字符串也是如此。
- 如果选中了一个选项且没有指定 `value` 属性，则选择框的 `value` 为该选项的文本。
- 如果选择了多个选项，则根据前两个规则，选择框的值将从第一个被选中的选项获取。

考虑以下选择框：

```html
<select name="location" id="selLocation">

    <option value="Sunnyvale, CA">Sunnyvale</option>

    <option value="Los Angeles, CA">Los Angeles</option>

    <option value="Mountain View, CA">Mountain View</option>

    <option value="">China</option>

    <option>Australia</option>

</select>
```

如果选择了此选择框中的第一个选项，则字段的值为 `"Sunnyvale, CA"`。如果选择了文本为 `"China"` 的选项，则该字段的值为空字符串，因为 `value` 属性是空的。如果选择了最后一个选项，则值为 `"Australia"`，因为在 `<option>` 上没有指定 `value` 属性。

每个 `<option>` 元素在 DOM 中都由一个 `HTMLOptionElement` 对象表示。`HTMLOptionElement` 类型增加了以下属性，以便于访问数据：

- `index` — 选项在 `options` 集合中的索引。
- `label` — 选项的标签；等同于 HTML 的 `label` 属性。
- `selected` — 布尔值，用于指示该选项是否被选中。将此属性设置为 `true` 以选中某个选项。
- `text` — 选项的文本。
- `value` — 选项的值（等同于 HTML 的 `value` 属性）。

大多数 `<option>` 属性用于快速访问选项数据。可以使用标准的 DOM 功能来访问这些信息，但效率非常低，正如示例所示：

```javascript
var selectbox = document.forms[0].elements["location"];

// 不推荐

var text = selectbox.options[0].firstChild.nodeValue;     // 选项文本

var value = selectbox.options[0].getAttribute("value");   // 选项值
```

这段代码使用标准的 DOM 技术获取选择框中第一个选项的文本和值。将其与使用特殊的选项属性进行对比：

```javascript
var selectbox = document.forms[0].elements["location"];

// 推荐做法

var text = selectbox.options[0].text;     // 选项文本

var value = selectbox.options[0].value;   // 选项值
```



在处理选项时，最好使用特定的选项属性，因为它们在所有浏览器中都得到了良好的支持。在操作 DOM 节点时，表单控件的具体交互可能会随浏览器而异。不建议使用标准的 DOM 技术更改 `<option>` 元素的文本或值。

最后说明，`change` 事件在选择框中的用法有所不同。与其他表单字段不同（表单字段在值改变且字段失去焦点后触发 `change` 事件），选择框在一旦选了某个选项时，就会立即触发 `change` 事件。

![image](img/pen.gif)

不同浏览器之间 `value` 属性返回的内容存在差异。在所有浏览器中，`value` 属性始终等于 `value` 属性。当未指定 `value` 属性时，Internet Explorer 8 及更早版本返回空字符串，而 Internet Explorer 9+、Safari、Firefox、Chrome 和 Opera 返回与文本相同的值。

## 选项选择

对于只允许选择一个选项的选择框，访问被选中选项的最简单方法是使用选择框的 `selectedIndex` 属性来获取选项，如下例所示：

```javascript
var selectedOption = selectbox.options[selectbox.selectedIndex];
```

这可以用来显示关于被选中选项的所有信息，如示例所示：

![image](img/logo1.gif)

```javascript
var selectedIndex = selectbox.selectedIndex;
var selectedOption = selectbox.options[selectedIndex];
alert("Selected index: " + selectedIndex + "\nSelected text: " + 
      selectedOption.text + "\nSelected value: " + selectedOption.value);
```

`SelectboxExample01.htm`

在这里，弹出一个警告框显示选中索引以及被选中选项的文本和值。

在允许多选的选择框中使用时，`selectedIndex` 属性的作用就像只允许一个选择一样。设置 `selectedIndex` 会移除所有选择并仅选中指定的单个选项，而获取 `selectedIndex` 则仅返回第一个被选中的选项的索引。

也可以通过获取选项的引用并将其 `selected` 属性设置为 `true` 来选择选项。例如，以下代码选中了选择框中的第一个选项：

```javascript
selectbox.options[0].selected = true;
```

与 `selectedIndex` 不同，在多选选择框中使用，设置选项的 `selected` 属性不会移除其他选择，允许你动态地选择任意数量的选项。如果单选选择框中选项的 `selected` 属性被更改，则所有其他选择将被移除。值得注意的是，在单选选择框中将 `selected` 属性设置为 `false` 没有效果。

`selected` 属性有助于判断选择框中哪些选项被选中。要获取所有选中的选项，你可以遍历 `options` 集合并测试 `selected` 属性。考虑这个示例：

```javascript
function getSelectedOptions(selectbox){
    var result = new Array();
    var option = null;
    for (var i=0, len=selectbox.options.length; i < len; i++){
        option = selectbox.options[i];
        if (option.selected){
            result.push(option);
        }
    }
    return result;
}
```

`SelectboxExample03.htm`

函数返回选择框中被选中的选项数组。首先创建一个结果数组。然后遍历选项并测试 `selected` 属性。如果选项被选中，则将其添加到结果数组中。最后一步是返回选项数组。然后可以使用 `getSelectedOptions()` 函数来获取被选中选项的信息，如下：

![image](img/logo1.gif)

```javascript
var selectbox = document.getElementById("selLocation");
var selectedOptions = getSelectedOptions(selectbox);
var message = "";
for (var i=0, len=selectedOptions.length; i < len; i++){
    message += "Selected index: " + selectedOptions[i].index + 
 "\nSelected text: " + selectedOptions[i].text + 
 "\nSelected value: " + selectedOptions[i].value + "\n\n";
}
alert(message);
```

`SelectboxExample03.htm`

在此示例中，从选择框获取选中的选项。使用 `for` 循环构建包含所有选中选项信息的消息，包括每个选项的索引、文本和值。这适用于单选或多选择框。

## 添加选项

有多种方法可以使用 JavaScript 动态创建并将它们添加到选择框中。第一种方法是 DOM：

```javascript
var newOption = document.createElement("option");
newOption.appendChild(document.createTextNode("Option text"));
newOption.setAttribute("value", "Option value");
selectbox.appendChild(newOption);
```

`SelectboxExample04.htm` 根据上下文修正。

也可以使用 `Option` 构造函数创建新选项，这是以前浏览器的遗留写法。`Option` 构造函数接受两个参数，文本和值，尽管第二个参数是可选的。尽管此构造函数用于创建 `Object` 实例，但符合 DOM 的浏览器会返回 `<option>` 元素。这意味着你仍然可以使用 `appendChild()` 将添加到选择框中。考虑以下：

```javascript
var newOption = new Option("Option text", "Option value");
selectbox.appendChild(newOption);    //在 IE <= 8 中有问题
```

这种方法在 Internet Explorer 8 及更早版本的浏览器中均可正常工作。由于一个 Bug，在使用此方法时，浏览器无法正确设置新选项的文本。

添加新选项另一种方法是使用选择框的 `add()` 方法。DOM 规定该方法接受两个参数：要添加的新选项，以及新选项应该插入到在该选项之前的选项。若要在列表末尾添加选项，第二个参数应为 `null`。Internet Explorer 8 及更早版本的 `add()` 实现略有不同，其不同之处在于第二个参数是可选的，且它必须是要插入新选项之前的那个选项的索引。符合 DOM 标准的浏览器要求第二个参数，因此为了实现跨浏览器兼容方案，你不能只使用一个参数（Internet Explorer 9 是符合 DOM 标准的）。相反，将 `undefined` 作为第二个参数传递可以确保在所有浏览器中都将选项添加到列表末尾。这里有一个示例：

![image](img/logo1.gif)

```javascript
var newOption = new Option("Option text", "Option value");
selectbox.add(newOption, undefined);    //最佳解决方案
```

`SelectboxExample04.htm`

这段代码在所有版本的 Internet Explorer 和符合 DOM 标准的浏览器中都能正常工作。如果你需要将新选项插入到最后一个以外的位置，应该使用 DOM 技术和 `insertBefore()`。

![image](img/pen.gif)

与 HTML 中一样，你并不被要求为选项赋值。`Option` 构造函数只需要一个参数（即选项文本）。

## 移除选项

与添加选项一样，有多种方法可以移除选项。你可以使用 DOM 的 `removeChild()` 方法并传入要移除的选项，如下所示：

```javascript
selectbox.removeChild(selectbox.options[0]);   //移除第一个选项
```

第二种方法是使用选择框的 `remove()` 方法。该方法接受单个参数，即要移除选项的索引，如下所示：

```javascript
selectbox.remove(0);   //移除第一个选项
```

最后一种方法是简单地将选项设置为 `null`。这也是前 DOM 时代浏览器的遗留写法。这里有一个示例：

```javascript
selectbox.options[0] = null;     //移除第一个选项
```

要清空选择框中的所有选项，你需要遍历所有选项并移除每一个，如示例所示：

```javascript
function clearSelectbox(selectbox){
    for(var i=0, len=selectbox.options.length; i < len; i++){
        selectbox.remove(0);
    }
}
```

此函数只是反复移除选择框中的第一个选项。由于移除第一个选项会自动将所有选项向上移动，因此这移除了所有选项。

## 移动和重新排序选项

在 DOM 之前，将选项从一个选择框移动到另一个选择框是一个相当困难的过程，涉及到从第一个选择框中移除选项、创建一个相同名称和值的新选项，然后将该新选项添加到第二个选择框中。使用 DOM 方法，可以通过 `appendChild()` 方法字面上地将选项从第一个选择框移动到第二个选择框中。如果你向此方法传递一个已经存在于元素的元素，该元素将从其父元素中移除并放到指定的位置。例如，以下代码将第一个选项从一个选择框移动到另一个选择框。

![image](img/logo1.gif)

```javascript
var selectbox1 = document.getElementById("selLocations1");
var selectbox2 = document.getElementById("selLocations2");
selectbox2.appendChild(selectbox1.options[0]);
```

`SelectboxExample05.htm`

移动选项与移除选项相同，因为每个选项的 `index` 属性都会被重置。

重新排序选项非常相似，DOM 方法是实现此点的最佳方式。若要将选项移动到选择框中的特定位置，`insertBefore()` 方法是最合适的，尽管 `appendChild()` 方法可以将任何选项移动到最后一个位置。要将选项在选择框中向上移动一个位置，可以使用以下代码：

```javascript
var optionToMove = selectbox.options[1];
selectbox.insertBefore(optionToMove, selectbox.options[optionToMove.index-1]);
```

`SelectboxExample06.htm`

在这段代码中，选取一个选项进行移动，然后将其插入到位于上一个索引的选项之前。第二行代码足够通用，适用于选择框中除第一个以外的任何选项。以下类似的代码可将选项向下移动一个位置：

```javascript
var optionToMove = selectbox.options[1];
selectbox.insertBefore(optionToMove, selectbox.options[optionToMove.index+2]);
```

`SelectboxExample06.htm`

这段代码适用于选择框中的所有选项，包括最后一个。

![image](img/pen.gif)

Internet Explorer 7 中存在重绘问题，有时会导致使用 DOM 方法重新排序的选项需要几秒钟才能正确显示。

## 表单序列化

随着 Ajax 的出现（将在第 21 章中进一步讨论），表单序列化已成为一项常见需求。在 JavaScript 中，可以使用表单字段的 `type` 属性结合 `name` 和 `value` 属性对表单进行序列化。在编写代码之前，你需要了解浏览器如何确定在表单提交期间发送到服务器的内容：

*   字段名和值经过 URL 编码，并使用 `&` 分隔。
*   禁用的字段完全不会发送。
*   复选框或单选框仅在被选中时才会被发送。
*   类型为 "reset" 或 "button" 的按钮永远不会被发送。
*   多选择字段为每个选中的值有一个条目。
*   当通过提交按钮提交表单时，会发送该提交按钮；否则不发送提交按钮。任何类型为 "image" 的 `<input>` 元素都被视为提交按钮。
*   `<select>` 元素的值是选中的 `<option>` 元素的 `value` 属性。如果 `<option>` 元素没有 `value` 属性，则值值为该 `<option>` 元素的文本。

表单序列化通常不包含任何按钮字段，因为生成的字符串极可能会以其他方式提交。应遵循所有其他规则。实现表单序列化的代码如下：

![image](img/logo1.gif)

```javascript
function serialize(form){        
    var parts = [],
        field = null,
        i,
        len,
        j,
        optLen,
        option,
        optValue;

    for (i=0, len=form.elements.length; i < len; i++){
        field = form.elements[i];
        switch(field.type){
            case "select-one":
            case "select-multiple":
                if (field.name.length){
                    for (j=0, optLen = field.options.length; j < optLen; j++){
                        option = field.options[j];
                        if (option.selected){
                            optValue = "";
                            if (option.hasAttribute){
                                optValue = (option.hasAttribute("value") ? 
                                            option.value : option.text);
                            } else {
                                optValue = (option.attributes["value"].specified ? 
                                            option.value : option.text);
                            }
                            parts.push(encodeURIComponent(field.name) + "=" + 
                                       encode((optValue));
                        }
                    }
                }
                break;
            case undefined:     //fieldset
            case "file":        //file input
            case "submit":      //submit button
            case "reset":       //reset button
            case "button":      //custom button
                break;
            case "radio":       //radio button
            case "checkbox":    //checkbox
                if (!field.checked){
                    break;
                }
                /* falls through */
            default:
                //don't include form fields without names
                if (field.name.length){



`parts.push(encodeURIComponent(field.name) + "=" + encodeURIComponent(field.value));`

```
}
```

`return parts.join("&");`

## FormSerializationExample01.htm

`serialize()` 函数首先定义一个名为`parts`的数组，用于存储将创建的字符串部分。接下来，通过`for`循环遍历每个表单字段，并将其存储在变量`field`中。一旦获取了字段引用，将使用`switch`语句检查其类型。序列化过程中最复杂的字段是`<select>`元素，无论是单选还是多选模式。序列化通过遍历控件中所有的`options`完成，如果某个选项被选中，则添加其值。对于单选控件，只会有一个选项被选中，而多选控件可能选中了零个或多个选项。同一段代码可以同时用于这两种选择类型，因为对选择数量的限制是由浏览器强制的。当某个选项被选中时，你需要确定使用哪种值。如果不存在`value`属性，则应该使用文本内容，尽管值为空字符串的`value`属性也是完全有效的。为了检查这一点，你需要在符合 DOM 标准的浏览器中使用`hasAttribute()`，并在 Internet Explorer 8 及更早版本中使用该属性的`specified`属性。

如果表单中包含`<fieldset>`元素，它会出现在元素集合中，但没有`type`属性。因此，如果`type`为`undefined`，则无需进行序列化。对于所有类型的按钮和文件输入字段也是如此。（文件输入字段在表单提交时包含文件内容；但是，这些字段是被模拟，因此在序列化时通常会被省略。）对于单选框和复选框控件，会检查`checked`属性，如果设置为`false`，则退出`switch`语句。如果`checked`为`true`，则代码继续执行`default`语句，该语句会对字段的`name`和`value`进行编码并将其添加到`parts`数组中。注意在所有情况下，没有名称的表单字段都不会包含在序列化中，以模拟浏览器的表单提交行为。函数的最后部分使用`join()`在字段之间使用与符号来正确格式化字符串。

`serialize()`函数输出查询字符串格式的字符串，尽管它可以轻松调整以将表单序列化为另一种格式。

## 富文本编辑 (RICH TEXT EDITING)

Web 应用请求最高的功能之一是在网页上编辑富文本的能力（也称为“所见即所得”，即 WYSIWYG 编辑）。尽管没有规范涵盖此功能，但最初由 Internet Explorer 引入的功能已形成了一种事实上的标准，现在已由 Opera、Safari、Chrome 和 Firefox 支持。基本技术是在页面中嵌入一个包含空白 HTML 文件的`iframe`。通过`designMode`属性，可以将此空白文档设为可编辑，此时你正在编辑页面`<body>`元素的 HTML。`designMode`属性有两个可能的值：`"off"`（默认）和`"on"`。当设置为`"on"`时，整个文档将变得可编辑（显示光标），允许你像使用文字处理器一样编辑文本，并具有用于使文本加粗、斜体等的按键操作。

使用一个非常简单的空白 HTML 页面作为`iframe`的源。这里是一个示例：

```html
<!DOCTYPE html>
<html>
    <head>
        <title>用于富文本编辑的空白页面</title>
    </head>
    <body>
    </body>
</html>
```

该页面像任何其他页面一样加载到`iframe`内部。为了允许它被编辑，你必须将`designMode`设置为`"on"`，但这只能在文档完全加载后才能发生。在包含它的页面中，你需要使用`onload`事件处理程序来指示设置`designMode`的时机，如下所示：

```html
<iframe name="richedit" style="height: 100px; width: 100px" src="blank.htm">
</iframe>

<script type="text/javascript">
EventUtil.addHandler(window, "load", function(){
    frames["richedit"].document.designMode = "on";
});
</script>
```

一旦加载此代码，你将在页面上看到一个像文本框的东西。该框具有与任何网页相同的默认样式，但可以通过对空白页面应用 CSS 来进行调整。

### 使用 contenteditable

另一种与富文本交互的方法（同样最早由 Internet Explorer 实现）是使用一个名为`contenteditable`的特殊属性。`contenteditable`属性可以应用于页面上的任何元素，并能立即让该元素变为用户可编辑。这种方法受到青睐是因为它不需要`iframe`、空白页面和 JavaScript 的开销。相反，你只需要向元素添加该属性：

```html
<div class="editable" id="richedit" contenteditable></div>
```

元素中已有的任何文本都会自动允许用户编辑，使其行为类似于`<textarea>`元素。你也可以通过设置元素上的`contentEditable`属性来开启或关闭编辑模式：

```javascript
var div = document.getElementById("richedit");
richedit.contentEditable = "true";
```

`contentEditable`有三个可能的值：`"true"`开启、`"false"`关闭，或`"inherit"`继承父元素的设置（因为可以在`contenteditable`元素内部创建或销毁元素）。`contentEditable`属性支持 Internet Explorer、Firefox、Chrome、Safari 和 Opera。对于移动设备`contenteditable`支持 iOS 5+ 的 Safari 以及 Android 3+ 的 WebKit。

与富文本编辑器交互的主要方法是通过使用`document.execCommand()`。该方法在`document`上执行命名的命令，并可用于应用大多数格式更改。`document.execCommand()`有三个可能的参数：要执行的命令名称、一个指示浏览器是否应为该命令提供用户界面的布尔值，以及执行该命令所需的值（如果不需要则为`null`）。为了实现跨浏览器兼容性，第二个参数应始终设为`false`，因为 Firefox 在传递`true`时会抛出错误。

每个浏览器都支持不同的命令集。最常用的命令列如下表所示。

| COMMAND | 值（第三个参数） | 描述 |
| --- | --- | --- |
| `backcolor` | 颜色字符串 | 设置文档的背景颜色。 |
| `bold` | `null` | 切换选中文本的加粗状态。 |
| `copy` | `null` | 对选中文本执行剪贴板复制。 |
| `createlink` | URL 字符串 | 将当前选中文本转换为指向给定 URL 的链接。 |
| `cut` | `null` | 对选中文本执行剪贴板剪切。 |
| `delete` | `null` | 删除当前选中的文本。 |
| `fontname` | 字体名称 | 将选中文本更改为指定的字体。 |
| `fontsize` | 1 到 7 | 更改选中文本的字体大小。 |
| `forecolor` | 颜色字符串 | 更改选中文本的字体颜色。 |
| `formatblock` | 包围区块的 HTML 标签；例如`<h1>` | 使用特定的 HTML 标签对选中的整个文本框进行格式化。 |
| `indent` | `null` | 缩进文本。 |
| `inserthorizontalrule` | `null` | 在光标处插入`<hr>`元素。 |
| `insertimage` | 图片 URL | 在光标处插入图片。 |
| `insertorderedlist` | `null` | 在光标处插入`<ol>`元素。 |
| `insertparagraph` | `null` | 在光标处插入`<p>`元素。 |
| `insertunorderedlist` | `null` | 在光标处插入`<ul>`元素。 |
| `italic` | `null` | 切换选中文本的斜体状态。 |
| `justifycenter` | `null` | 使光标所在的文本块居中对齐。 |
| `justifyleft` | `null` | 使光标所在的文本块左对齐。 |
| `outdent` | `null` | 取消文本缩进。 |
| `paste` | `null` | 对选中文本执行剪贴板粘贴。 |
| `removeformat` | `null` | 移除光标所在区块的区块格式。这是`formatblock`的反操作。 |
| `selectall` | `null` | 选取文档中的所有文本。 |
| `underline` | `null` | 切换选中文本的下划线。 |
| `unlink` | `null` | 移除文本链接。这是`createlink`的反操作。 |

剪贴板命令高度取决于浏览器。Opera 没有实现任何剪贴板命令，而 Firefox 默认禁用了它们（你必须更改用户偏好来启用它们）。Safari 和 Chrome 实现了`cut`和`copy`，但没有实现`paste`。注意，尽管这些命令无法通过`document.execCommand()`使用，但它们通过相应的键盘快捷键仍然有效。

这些命令可以随时用于修改 iframe 富文本区域的外观，如下例所示：

![image](img/logo1.gif)

```javascript
// 在 iframe 中切换加粗文本
frames["richedit"].document.execCommand("bold", false, null);

// 在 iframe 中切换斜体文本
frames["richedit"].document.execCommand("italic", false, null);

// 在 iframe 中创建到 www.wrox.com 的链接
frames["richedit"].document.execCommand("createlink", false, 
                                        "http://www.wrox.com");

// 在 iframe 中格式化为一级标题
frames["richedit"].document.execCommand("formatblock", false, "<h1>");
```

RichTextEditingExample01.htm

你可以使用相同的方法来操作页面上的`contenteditable`部分，只需使用当前窗口的`document`对象而不是引用 iframe 即可：

```javascript
// 切换加粗文本
document.execCommand("bold", false, null);

// 切换斜体文本
document.execCommand("italic", false, null);

// 创建到 www.wrox.com 的链接
document.execCommand("createlink", false, 
                                        "http://www.wrox.com");

// 格式化为一级标题
document.execCommand("formatblock", false, "<h1>");
```

RichTextEditingExample01.htm

注意，即使命令在所有浏览器中都支持，命令产生的 HTML 往往也不同。例如，应用`bold`命令时，在 Internet Explorer 和 Opera 中文本会被`<strong>`包围，在 Safari 和 Chrome 中是`<b>`，而在 Firefox 中则是`<span>`。你不能依赖富文本编辑器生成的 HTML 具有一致性，因为这不仅取决于命令的实现，还取决于`innerHTML`所做的转换。

还有其他一些与命令相关的方法。第一个是`queryCommandEnabled()`，它用于判断根据当前的选中文本或光标位置是否可以执行某个命令。该方法接受一个参数，即要检查的命令名称，如果根据编辑区域的状态允许该命令则返回`true`，否则返回`false`。考虑此示例：

```javascript
var result = frames["richedit"].document.queryCommandEnabled("bold");
```

如果`"bold"`命令可以执行，此代码将返回`true`。注意`queryCommandEnabled()`指明了是否可以使用该命令执行当前选择。在 Firefox 中，`queryCommandEnabled("cut")`会返回`true`。

`queryCommandState()`方法可以让你判断某个命令是否已应用于选中文本。例如，要判断当前选择是否加粗，可以使用以下代码：

![image](img/logo1.gif)

```javascript
var isBold = frames["richedit"].document.queryCommandState("bold");
```

RichTextEditingExample01.htm

如果`"bold"`命令之前应用于选中文本，则代码将返回`true`。这是全功能富文本编辑器能够更新加粗、斜体等按钮的方法。

最后一个方法是`queryCommandValue()`，它旨在返回执行命令时的值（即`execCommand`中的第三个参数）。例如，应用`fontsize`命令且值为`7`的文本范围会从此处返回`"7"`：

```javascript
var fontSize = frames["richedit"].document.queryCommandValue("fontsize");
```

RichTextEditingExample01.htm

该方法可以判断命令是如何应用于选择的，从而确定下一个命令是否适合执行。

### 富文本选择

你可以通过 iframe 的`getSelection()`方法来确定富文本编辑器中的精确选择。该方法在`document`对象和`window`对象上可用，并返回一个表示当前选择文本的`Selection`对象。每个`Selection`对象都有以下属性：

- `anchorNode`: 选择开始的节点。
- `anchorOffset`: 在`anchorNode`中选择开始前跳过的字符数。
- `focusNode`: 选择结束的节点。
- `focusOffset`: 在`focusNode`中包含在选择中的字符数。
- `isCollapsed`: 布尔值，表示选择的起点和终点是否相同。
- `rangeCount`: 选择中 DOM 范围的数量。

`Selection`的属性并不包含很多有用信息。幸运的是，以下方法提供了更多信息并允许操作选择：

- `addRange(range)`: 将给定的 DOM 范围添加到选择中。
- `collapse(node, offset)`: 将选择折叠到给定节点内的指定偏移量处。
- `collapseToEnd()` — 将选区折叠到末尾。
- `collapseToStart()` — 将选区折叠到起始。
- `containsNode(node)` — 确定给定节点是否包含在选区内。
- `deleteFromDocument()` — 从文档中删除选区文本。这等同于`execCommand("delete", false, null)`。
- `extend(node, offset)` — 通过将`focusNode`和`focusOffset`移动到指定的值来扩展选区。
- `getRangeAt(index)` — 返回选区中指定索引处的 DOM 范围。
- `removeAllRanges()` — 移除选区中所有的 DOM 范围。这实际上移除了选区，因为选区中至少包含一个范围。
- `removeRange(range)` — 从选区中移除指定的 DOM 范围。
- `selectAllChildren(node)` — 清除选区，然后选中给定节点的所有子节点。
- `toString()` — 返回选区的文本内容。

`Selection`对象的方法非常强大，它们广泛利用 DOM 范围（在第 12 章中讨论过）来管理选区。访问 DOM 范围允许你比使用`execCommand()`更精细地修改富文本编辑器的内容，因为你可以直接操作所选文本的 DOM。考虑以下示例：

![image](img/logo1.gif)

```javascript
var selection = frames["richedit"].getSelection();

// 获取选中的文本
var selectedText = selection.toString();

// 获取代表选区的范围
var range = selection.getRangeAt(0);

// 高亮选中的文本
var span = frames["richedit"].document.createElement("span");
span.style.backgroundColor = "yellow";
```



`range.surroundContents(span);`

`RichTextEditingExample01.htm`

这段代码在富文本编辑器中选中的文本周围添加黄色高亮。通过默认选区中的 DOM 范围，`surroundContents()` 方法用一个背景颜色为黄色的 `<span>` 元素包裹选区。

`getSelection()` 方法在 HTML5 中标准化，并已在 Internet Explorer 9、Firefox、Safari、Chrome 和 Opera 8 中实现。Firefox 3.6+ 由于遗留的性问题，`document.getSelection()` 会错误地返回一个字符串。在 Firefox 3.6+ 中，你可以使用 `window.getSelection()` 方法来获取 `Selection` 对象。Firefox 8 修复了 `document.getSelection()`，使其返回与 `window.getSelection()` 相同的值。

Internet Explorer 8 及早期版本不支持 DOM 范围，但它们允许通过专有的选择对象与选中文进行交互。`selection` 对象是 `document` 的属性，正如本章前面讨论的那样。要在富文本编辑器中获取选中文，你必须先创建一个文本范围（在第 12 章讨论过），然后如下所示使用 `text` 属性：

```javascript
var range = frames["richedit"].document.selection.createRange();
var selectedText = range.text;
```

使用 Internet Explorer 文本范围进行 HTML 操作不如使用 DOM 范围那样安全，但这是可能的。要实现与 DOM 范围描述的相同的高亮效果，你可以结合使用 `htmlText` 属性和 `pasteHTML()` 方法：

```javascript
var range = frames["richedit"].document.selection.createRange();
range.pasteHTML("<span style=\"background-color:yellow\">" + range.htmlText +  
                "</span>");
```

这段代码使用 `htmlText` 获取当前选区的 HTML，然后用 `<span>` 包裹它，并使用 `pasteHTML()` 将其插回选区。

## 表单中的富文本

由于富文本编辑是使用 `iframe` 或 `contenteditable` 元素而不是表单控件实现的，因此富文本编辑器在技术上不属于表单的一部分。这意味着除非你手动提取 HTML 并自行提交，否则 HTML 将不会提交到服务器。这通常通过一个隐藏的表单字段来实现，该字段会根据来自 `iframe` 或 `contenteditable` 元素的 HTML 进行更新。在表单提交之前，会从 `iframe` 或元素中提取 HTML 并插入到隐藏字段中。例如，在使用 `iframe` 时，可以在表单的 `onsubmit` 事件处理器中执行以下操作：

![image](img/logo1.gif)

```javascript
EventUtil.addHandler(form, "submit", function(event){
    event = EventUtil.getEvent(event);
    var target = EventUtil.getTarget(event);
    target.elements["comments"].value = frames["richedit"].document.body.innerHTML;
});
```

`RichTextEditingExample01.htm`

在这里，通过 `document` body 的 `innerHTML` 属性从 `iframe` 获取 HTML，并将其插入名为 "comments" 的表单字段中。这样做确保了 "comments" 字段在表单提交之前被填充。如果你正在使用 `submit()` 方法手动提交表单，请注意提前执行此操作。你可以对 `contenteditable` 元素执行类似的操作：

```javascript
EventUtil.addHandler(form, "submit", function(event){
    event = EventUtil.getEvent(event);
    var target = EventUtil.getTarget(event);
    target.elements["comments"].value = 
        document.getElementById("richedit").innerHTML;
});
```

## 总结

尽管 HTML 和 Web 应用自诞生以来已经发生了巨大变化，但 Web 表单仍保持基本不变。可以使用 JavaScript 增强现有的表单字段，以提供新的功能和易用性增强。为了实现这一点，表单具有用于 JavaScript 的属性、方法和事件。以下是本章介绍的概念：

* 使用标准和非标准方法选择文本框中的全部或部分文本。
* 所有的浏览器都采用了 Firefox 处理选区的方式，使其成为标准。
* 通过监听事件并检查输入的字符，可以更改文本框以允许或禁止某些字符。

除了 Opera 之外的所有浏览器都支持剪贴板事件，包括复制、剪切和粘贴。其他浏览器的实现方式差异如下：

* Internet Explorer、Firefox、Chrome 和 Safari 允许访问剪贴板数据，而 Opera 不允许。
* 即使在 Internet Explorer、Chrome 和 Safari 之间也存在差异。
* Firefox、Safari 和 Chrome 仅在粘贴事件期间允许读取剪贴板，而 Internet Explorer 没有这种限制。
* Firefox、Safari 和 Chrome 将剪贴板信息的可用性限制在剪贴板事件中，而 Internet Explorer 允许随时访问。

拦截剪贴板事件在需要限制文本框内容为某些字符时非常有用。

* 绘制简单的 2D 图形
* 使用 WebGL 进行 3D 绘制

毫无疑问，HTML5 最流行的新增是 `<canvas>` 元素。该元素指定了页面上的一个区域，可以使用 `JavaScript` 动态创建图形。`<canvas>` 最初由 Apple 提用于 Dashboard 组件，很快被添加到 HTML5 中并在浏览器中获得了极快的普及率。Internet Explorer 9+、Firefox 1.5+、Safari 2+、Opera 9+、Chrome、Safari for iOS 以及 Android 版 WebKit 都在某种程度上支持 `<canvas>`。

与浏览器环境的其他部分类似，`<canvas>` 由一组 API 组成，并不是所有浏览器都支持所有 API Set。它有一个具有基本绘制能力的 2D 上下文和一个名为 `WebGL` 的 3D 上下文。支持浏览器的最新版本现在支持 2D 上下文和文本 API；`WebGL` 的支持仍在演进，但由于 `WebGL` 仍然处于实验阶段，完全支持可能需要更长时间。Firefox 4+ 和 Chrome 支持 `WebGL` 规范的早期版本，尽管即使存在这些浏览器，Windows XP 等旧版操作系统也缺少启用 `WebGL` 所需的图形驱动程序。

## 基本用法

`<canvas>` 元素至少需要设置其 `width` 和 `height` 属性以指示要创建的图形的大小。出现在起始和结束标签之间的任何内容都是回退数据，只有在不支持 `<canvas>` 元素时才会显示。例如：

```
<canvas id="drawing" width="200" height="200">A drawing of something.</canvas>
```

与其他元素一样，`width` 和 `height` 属性也可以作为 DOM 元素对象的属性存在，并可以随时更改。整个元素可以使用 CSS 进行样式化，在元素被设置样式或进行绘制之前，它是不可见的。

要在画布上开始绘制，你需要获取一个绘制上下文。使用 `getContext()` 方法并传递上下文名称来获取绘制上下文引用。例如，传递 `"2d"` 会获取一个 2D 上下文对象：

```javascript
var drawing = document.getElementById("drawing");

//确保 <canvas> 被完全支持
if (drawing.getContext){
    var context = drawing.getContext("2d");
    // 此处有更多代码
}
```

在使用 `<canvas>` 元素时，测试 `getContext()` 方法是否存在非常重要。某些浏览器会为并非 HTML 正式部分的元素创建默认的 HTML 元素对象。在这种情况下，即使 `drawing` 包含一个有效的元素引用，`getContext()` 方法也是不可用的。

在 `<canvas>` 元素上创建的图像可以使用 `toDataURL()` 方法导出。该方法接受单个参数，即生成的图像的 MIME 类型格式，并且无论使用何种上下文创建图像都适用。例如，要从画布返回 PNG 格式的图像，请使用以下代码：

```javascript
var drawing = document.getElementById("drawing");

//确保 <canvas> 被完全支持
if (drawing.getContext){
    //获取图像的数据 URI
    var imgURI = drawing.toDataURL("image/png");

    //显示图像
    var image = document.createElement("img");
    image.src = imgURI;
    document.body.appendChild(image);    
}
```

`2DDataUrlExample01.htm`

默认情况下，除非另有说明，浏览器会将图像编码为 PNG。Firefox 和 Opera 还通过 `"image/jpeg"` 支持 JPEG 编码。由于该方法是在过程后期添加的，因此在支持的浏览器后续版本中被采用，包括 Internet Explorer 9、Firefox 3.5 和 Opera 10。

如果在画布上绘制来自不同域的图像，`toDataURL()` 方法将抛出错误。本章稍后会提供更多细节。

## 2D 上下文

2D 绘制上下文提供了绘制简单 2D 形状（如矩形、弧和路径）的方法。2D 上下文中的坐标从 `<canvas>` 元素的左上角开始，被视为点 `(0,0)`。所有坐标值都相对于该点计算，`x` 向右增加，`y` 向下。默认情况下，`width` 和 `height` 表示每个方向可用的像素数。

### 填充与描边

2D 上下文上有两个基本绘制操作：`fill` 和 `stroke`。`fill` 自动用特定样式（颜色、渐变或图像）填充形状，而 `stroke` 只为边缘上色。大多数 2D 上下文操作都有 `fill` 和 `stroke` 变体，它们的显示方式取决于两个属性：`fillStyle` 和 `strokeStyle`。

这两个属性都可以设置为字符串、渐变对象或模式对象，且默认值均为 `"#000000"`。字符串值表示使用各种 CSS 颜色格式之一定义的颜色：名称、十六代码、`rgb`、`rgba`、`hsl` 或 `hsla`。例如：

```javascript
var drawing = document.getElementById("drawing");

//确保 <canvas> 被完全支持
if (drawing.getContext){
    var context = drawing.getContext("2d");
    context.strokeStyle = "red";
    context.fillStyle = "#0000ff";
}
```

此代码将 `strokeStyle` 设置为 `"red"`（命名 CSS 颜色）并将 `fillStyle` 设置为 `"#0000ff"`（蓝色）。所有涉及描边和填充的绘制操作将使用这些样式，直到属性再次更改。这些属性也可以设置为渐变或模式，这两者将在本章稍后进行讨论。

### 绘制矩形

可以直接在 2D 绘制上下文上绘制的唯一形状是矩形。有三种处理矩形的方法：`fillRect()`、`strokeRect()` 和 `clearRect()`。这些方法每个都接受四个参数：矩形的 `x-coordinate`、矩形的 `y-coordinate`、矩形的 `width` 和矩形的 `height`。

`fillRect()` 方法用于在画布上绘制一个填充特定颜色的矩形。填充颜色使用 `fillStyle` 属性指定，例如：

```javascript
var drawing = document.getElementById("drawing");

//确保 <canvas> 被完全支持
if (drawing.getContext){
    var context = drawing.getContext("2d");

    /*
     * 根据 Mozilla 的文档： 
     * http://developer.mozilla.org/en/docs/Canvas_tutorial:Basic_usage
     */

    //绘制一个矩形
    context.fillStyle = "#ff0000";
    context.fillRect(10, 10, 50, 50);

    //绘制一个半透明的矩形
    context.fillStyle = "rgba(0,0,255,0.5)";
    context.fillRect(30, 30, 50, 50);
}
```

`2DFillRectExample01.htm`

此代码首先将 `fillStyle` 设置为红色，并在 `(10,10)` 处绘制一个高宽均为 50 像素的矩形。接下来，它使用 `rgba()` 格式将 `fillStyle` 设置为半透明蓝色，并绘制另一个矩形。结果你可以透过蓝色矩形看到红色矩形（参见图 15-1）。

`strokeRect()` 方法使用 `strokeStyle` 属性指定的颜色绘制矩形轮廓。这是一个示例：

```javascript
var drawing = document.getElementById("drawing");

//确保 <canvas> 被完全支持
if (drawing.getContext){
    var context = drawing.getContext("2d");

    /*
     * 根据 Mozilla 的文档： 
     * http://developer.mozilla.org/en/docs/Canvas_tutorial:Basic_usage
     */

    //绘制红色描边矩形
    context.strokeStyle = "#ff0000";
    context.strokeRect(10, 10, 50, 50);

    //绘制一个半透明的蓝色描边矩形
    context.strokeStyle = "rgba(0,0,255,0.5)";
    context.strokeRect(30, 30, 50, 50);
}
```

`2DStrokeRectExample01.htm`

这段代码还绘制了两个重叠的矩形；然而，它们只是轮廓而不是填充矩形（参见图 15-2）。

图 15-2

![image](img/f555-01.jpg)![image](img/pen.gif)

笔画的大小由 `lineWidth` 属性控制，它可以设置为任何整数。同样，`lineCap` 属性描述了线端应使用的形状（`"butt"`、`"round"` 或 `"square"`），而 `lineJoin` 指明了线条如何连接（`"round"`、`"bevel"` 或 `"miter"`）。

你可以使用 `clearRect()` 方法擦除画布的一个区域。该方法用于使绘图上下文的区域透明。通过绘制形状然后清除特定区域，你可以创建出有趣的效果，例如切掉另一个形状的部分。这里是一个示例：

![image](img/logo1.gif)

```javascript
var drawing = document.getElementById("drawing");

//make sure <canvas> is completely supported
if (drawing.getContext){
    var context = drawing.getContext("2d");

    /*
     * Based on Mozilla's documentation: 
     * http://developer.mozilla.org/en/docs/Canvas_tutorial:Basic_usage
     */

    //draw a red rectangle
    context.fillStyle = "#ff0000";
    context.fillRect(10, 10, 50, 50);

    //draw a blue rectangle that's semi-transparent
    context.fillStyle = "rgba(0,0,255,0.5)";
    context.fillRect(30, 30, 50, 50);
}
```



//clear a rectangle that overlaps both of the previous rectangles

`context.clearRect(40, 40, 10, 10);`

}

`2DClearRectExample01.htm`

在这里，两个填充矩形相互重叠，然后在该重叠区域内清除了一个小矩形。图 15-3 显示了结果。

图 15-3

![image](img/f556-01.jpg)

### 绘制路径

2D 绘图上下文支持多种在画布上绘制路径的方法。路径允许你创建复杂的形状和线条。要开始创建路径，你必须首先调用 `beginPath()` 来指示新路径的开始。之后，可以调用以下方法来创建路径：

*   `arc(x, y, radius, startAngle, endAngle, counterclockwise)`—以点 `(x,y)` 为中心，以给定的半径在 `startAngle` 和 `endAngle` 之间（以弧度表示）绘制圆弧。最后一个参数是布尔值，指示 `startAngle` 和 `endAngle` 是否应该按逆时针而非顺时针计算。
*   `arcTo(x1, y1, x2, y2, radius)`—从上一个点到 `(x2, y2)` 绘制弧，经过 `(x1, y1)` 并使用指定的半径。
*   `bezierCurveTo(c1x, c1y, c2x, c2y, x, y)`—使用控制点 `(c1x, c1y)` 和 `(c2x, c2y)` 从上一个点到点 `(x, y)` 绘制曲线。
*   `lineTo(x, y)` —从上一个点到点 `(x, y)` 绘制一条线。
*   `moveTo(x, y)` —将绘图光标移动到点 `(x, y)` 而不绘制线。
*   `quadraticCurveTo(cx, cy, x, y)`—使用控制点 `(cx, cy)` 从上一个点到点 `(x, y)` 绘制二次曲线。
*   `rect(x, y, width, height)` —在点 `(x, y)` 处以给定的宽度和高度绘制矩形。这与 `strokeRect()` 和 `fillRect()` 的区别在于它创建一个路径而不是独立的形状。

一旦创建了路径，你就有几种选择。要绘制一条返回路径起点的线，你可以调用 `closePath()`。如果路径已经完成且你想用 `fillStyle` 填充它，请调用 `fill()` 方法。另一个选项是调用 `stroke()` 方法描边路径，它会使用 `strokeStyle`。最后一个选项是调用 `clip()`，它会根据路径创建一个新的裁剪区域。

作为一个示例，考虑以下用于绘制没有数字的时钟脸的代码：

![image](img/logo1.gif)

```
var drawing = document.getElementById("drawing");

//make sure <canvas> is completely supported

if (drawing.getContext){

    var context = drawing.getContext("2d");

    //start the path

    context.beginPath();

    //draw outer circle

    context.arc(100, 100, 99, 0, 2 * Math.PI, false);

    //draw inner circle

    context.moveTo(194, 100);

    context.arc(100, 100, 94, 0, 2 * Math.PI, false);

    //draw minute hand

    context.moveTo(100, 100);

    context.lineTo(100, 15);

    //draw hour hand

    context.moveTo(100, 100);

    context.lineTo(100, 50);

    //stroke the path

    context.stroke();

}
```

`2DPathExample01.htm`

### 绘制文本

由于经常需要将文本与图形混合，2D 绘图上下文提供了绘制文本的方法。有两种绘制文本的方法：`fillText()` 和 `strokeText()`，它们都接受四个参数：要绘制的字符串、x 坐标、y 坐标以及可选的绘制宽度。这两个方法都基于以下三个属性进行绘制：

*   `font`—以与 CSS 相同的方式指定字体样式、大小和族，例如 `"10px Arial"`。
*   `textAlign`—指示文本的对齐方式。可能的值有 `"start"`、`"end"`、`"left"`、`"right"` 和 `"center"`。使用 `"start"` 和 `"end"` 代替 `"left"` 和 `"right"`，因为这些更符合从左到右和从右到左语言的渲染。
*   `textBaseline`—指示文本的基线。可能的值有 `"top"`、`"hanging"`、`"middle"`、`"alphabetic"`、`"ideographic"` 和 `"bottom"`。

这些属性都有默认值，因此每次想绘制文本时都不需要设置它们。`fillText()` 方法使用 `fillStyle` 属性绘制文本，而 `strokeText()` 方法使用 `strokeStyle` 属性。你可能大部分时间都会使用 `fillText()`，因为它模拟了网页上的普通文本。例如，以下代码在上一节创建的时钟顶部绘制了一个“12”：

```
context.font = "bold 14px Arial";

context.textAlign = "center";

context.textBaseline = "middle";

context.fillText("12", 100, 20);
```

由于 `textAlign` 被设置为 `"center"` 且 `textBaseline` 被设置为 `"middle"`，坐标 `(100,80)` 表示文本的水平和垂直中心点以及顶部坐标。如果 `textAlign` 为 `"start"`，则 x 坐标将代表从左到右语言中文本的左侧坐标，而 `"end"` 则会使 x 坐标代表从左到右语言中文本的右侧。例如：

```
//normal

context.font = "bold 14px Arial";

context.textAlign = "center";

context.textBaseline = "middle";

context.fillText("12", 100, 20);

//start-aligned

context.textAlign = "start";

context.fillText("12", 100, 40);

//end-aligned

context.textAlign = "end";

context.fillText("12", 100, 60);
```

`2DTextExample02.htm`

字符串 `"12"` 被绘制了三次，每次都使用相同的 x 坐标，但使用了三个不同的 `textAlign` 值。y 坐标值也相应递增，以确保字符串不会重叠渲染。生成的图像如图 15-6 所示。

图 15-6

![image](img/f559-01.jpg)

时钟的垂直线直接位于中心，因此文本的对齐变得非常明显。你同样可以通过更改 `textBaseline` 来调整文本的垂直对齐方式。设置为 `"top"` 意味着 y 坐标是文本的顶部，`"bottom"` 意味着底部，而 `"hanging"`、`"alphabetic"` 和 `"ideographic"` 则指的是字体特定的基线坐标。

由于绘制文本是非常复杂的，尤其是当你想要让文本在特定区域内渲染时，2D 上下文提供了一个额外的帮助，通过 `measureText()` 方法来确定文本的尺寸。该方法接受单个参数（即要绘制的文本），并返回一个 `TextMetrics` 对象。返回的对象目前只有一个属性 `width`，但意图是在未来提供更多度量指标。

`measureText()` 方法使用 `font`、`textAlign` 和 `textBaseline` 的当前值来计算指定文本的大小。例如，假设你想将文本“Hello world!”放入一个宽度为 140 像素的矩形内。以下代码从 100 像素的字体大小开始，递减直到文本适应为止：

![image](img/logo1.gif)

```
var fontSize = 100;

context.font = fontSize + "px Arial";

while(context.measureText("Hello world!").width > 140){

    fontSize--;

    context.font = fontSize + "px Arial";

}

context.fillText("Hello world!", 10, 10);

context.fillText("Font size is " + fontSize + "px", 10, 50); 
```

`2DTextExample03.htm`

`fillText()` 和 `strokeText()` 都有第四个参数，即文本的最大宽度。该参数是可选的，并且尚未在所有浏览器中实现（Firefox 4 是第一个实现它的）。当提供时，使用无法放入最大宽度内的字符串调用 `fillText()` 或 `strokeText()` 会导致文本以正确的字符高度绘制，但字符将进行水平缩放以适应宽度。图 15-7。

图 15-7

![image](img/f559-02.jpg)

文本绘制是较为复杂的绘制操作之一，因此，并不是所有支持 `<canvas>` 元素的浏览器都实现了 API 的所有部分。

## 变换

上下文变换允许对绘制在画布上的图像进行操作。2D 绘制上下文支持所有的基本绘制变换。当创建绘制上下文时，变换矩阵被初始化为默认值，这使得所有绘制操作都按照描述的方式直接应用。对绘制上下文中应用变换会导致操作使用不同的变换矩阵进行应用，从而产生不同的结果。

可以使用任何以下方法来扩展变换矩阵：

* `rotate(angle)`——围绕原点按 `angle` 弧度旋转图像。
* `scale(scaleX, scaleY)`——在 x 维度上按 `scaleX` 倍，在 y 维度上按 `scaleY` 倍缩放图像。`scaleX` 和 `scaleY` 的默认值均为 1.0。
* `translate(x, y)`——将原点移动到点 `(x, y)`。执行此操作后，坐标 `(0, 0)` 位于之前描述的 `(x, y)` 点。
* `transform(m1_1, m1_2, m2_1, m2_2, dx, dy)`——通过乘以如下所示的矩阵直接更改变换矩阵：

```
m1_1 m1_2 dx

m2_1 m2_2 dy

0    0    1
```

* `setTransform(m1_1, m1_2, m2_1, m2_2, dx, dy)`——将变换矩阵重置为默认状态，然后调用 `transform()`。

变换可以根据需要变得简单，也可以复杂。例如，通过……来绘制上一个示例中的时钟指针可能会更容易。

```javascript
context.fillStyle = "#ff0000";

context.save();

context.fillStyle = "#00ff00";

context.translate(100, 100);

context.save();

context.fillStyle = "#0000ff";

context.fillRect(0, 0, 100, 200);   //在 (100, 100) 绘制蓝色矩形

context.restore();

context.fillRect(10, 10, 100, 200);   //在 (110, 110) 绘制绿色矩形

context.restore();

context.fillRect(0, 0, 100, 200);    //在 (0,0) 绘制红色矩形
```

### 2DSaveRestoreExample01.htm

在这段代码中，`fillStyle` 被设置为红色，然后调用了 `save()`。接下来将 `fillStyle` 更改为绿色并将并将平移到 `(100,100)`。再次调用 `save()` 保存这些设置。随后将 `fillStyle` 属性设置为蓝色并绘制一个矩形。因为坐标被平移了，矩形实际上绘制在 `(100,100)` 处。当调用 `restore()` 时，`fillStyle` 恢复为绿色，因此绘制的下一个矩形是绿色的。由于平移仍然有效，这个矩形绘制在 `(110,110)` 处。当再次调用 `restore()` 时，平移被移除且 `fillStyle` 恢复为红色。最后一个矩形绘制在 `(0,0)` 处。

注意，`save()` 只保存应用于绘图上下文的设置和变换，而不会保存绘图上下文的内容。

### 绘制图像

2D 绘图上下文对处理图像有内置支持。如果你有一张想要在画布上绘制的现有图像，可以使用 `drawImage()` 方法来实现。根据所需的结果，可以使用三组不同的参数来调用此方法。最简单的调用是传递一个 HTML `<img>` 元素以及目标 x 坐标和 y 坐标，这会将图像绘制在指定位置。以下是一个示例：

![image](img/logo1.gif)

```javascript
var image = document.images[0];

context.drawImage(image, 10, 10);
```

### 2DDrawImageExample01.htm

此代码获取文档中的第一个图像并将其绘制在位置 `(10,10)` 处的上下文中。图像以原图相同的比例绘制。你可以通过添加两个参数（目标宽度和目标高度）来更改图像的绘制方式。这会缩放图形而不影响上下文的变换矩阵。这里是一个示例：

```javascript
context.drawImage(image, 50, 10, 20, 30);
```

### 2DDrawImageExample01.htm

当执行此代码时，图像将被缩放为宽 20 像素、高 30 像素。

你也可以只选择图像的某个区域绘制到上下文中。这是通过向 `drawImage()` 提供九个参数实现的：要绘制的图像、源 x 坐标、源 y 坐标、源宽度、源高度、目标 x 坐标、目标 y 坐标、目标宽度和目标高度。使用 `drawImage()` 的这个重载版本可以让你获得最大的控制权。考虑这个示例：

```javascript
context.drawImage(image, 0, 10, 50, 50, 0, 100, 40, 60);
```

### 2DDrawImageExample01.htm

在这里，画布上只绘制了图像的一部分。图像的这部分始于点 `(0,10)`，宽 50 像素，高 50 像素。图像被绘制到上下文的 `(0,100)` 点，并缩放到适应 40×60 的区域。

这些绘制操作允许你创建有趣的效果，例如 图 15-9 所示。

FIGURE 15-9

![image](img/f563-01.jpg)

除了将 HTML `<img>` 元素作为第一个参数外，你还可以传递另一个 `<canvas>` 元素，将一个画布的内容绘制到另一个画布上。

`drawImage()` 方法与其他方法结合使用，可以轻松执行基本的图像处理，结果可以使用 `toDataURL()` 获取。然而，有一种情况下这起不起作用：如果将一个来自页面不同源的图像绘制到上下文中。在这种情况下，调用 `toDataURL()` 会抛出错误。例如，如果托管在 [www.example.com](http://www.example.com) 的页面绘制一个托管在 [www.wrox.com](http://www.wrox.com) 的图像，则上下文被认为是“脏”的并抛出错误。

### 阴影

2D 上下文将根据几个属性的值，沿着形状或路径自动绘制阴影：

* `shadowColor` — 绘制阴影的 CSS 颜色。默认是黑色。
* `shadowOffsetX` — 距离形状或路径 x 坐标的 x 坐标偏移量。默认是 0。
* `shadowOffsetY` — 距离形状或路径 y 坐标的 y 坐标偏移量。默认是 0。
* `shadowBlur` — 模糊的像素数。默认是 0。

这些属性都可以在 2D 上下文中读取和写入。例如：

![image](img/logo1.gif)

```javascript
var context = canvas.getContext("2d");

context.shadowColor = "rgba(0,0,0,0.5)";

context.shadowOffsetX = 5;

context.shadowOffsetY = 5;

context.shadowBlur = 5;

context.fillStyle = "#ff0000";

context.fillRect(10, 10, 100, 200);
```



### 2DFillShadowExample01.htm

对于阴影的支持存在一些差异。Internet Explorer 9、Firefox 4 和 Opera 11 具有这种行为。Chrome（版本 10）会将阴影应用于填充形状。

### 渐变

渐变由`CanvasGradient`实例表示，并在 2D 上文中创建和修改。要创建一个线性渐变，调用`createLinearGradient()`方法。此方法接受四个参数：起始 x 坐标、起始 y 坐标、结束 x 坐标和结束 y 坐标。调用后，该方法会创建一个新的`CanvasGradient`对象并返回实例。

一旦有了渐变对象，下一步是使用`addColorStop()`方法分配颜色停止点。此方法接受两个参数：颜色停止点的位置和 CSS 颜色。颜色停止点的位置是 0（第一种颜色）到 1（最后一种颜色）之间的数字。例如：

![image](img/logo1.gif)

```javascript
var gradient = context.createLinearGradient(30, 30, 70, 70);
gradient.addColorStop(0, "white");
gradient.addColorStop(1, "black");
```

### 2DFillGradientExample01.htm

渐变对象现在代表从画布上的点 (30,30) 到点 (70,70) 的渐变。起始颜色是白色，停止颜色是黑色。你现在可以将`fillStyle`或`strokeStyle`属性设置为此值，以使用渐变绘制形状：

```javascript
//绘制红色矩形
context.fillStyle = "#ff0000";
context.fillRect(10, 10, 100, 200);

//绘制渐变矩形
context.fillStyle = gradient;
context.fillRect(30, 30, 50, 50);
```

### 2DFillGradientExample01.htm

为了让渐变绘制在整个矩形上不仅仅是部分，坐标需要匹配。此代码产生了图 15-11 所示的图形。

![image](img/f565-01.jpg)

如果矩形没有恰好绘制在这一位置，那么只会显示渐变的一部分。例如：

```javascript
context.fillStyle = gradient;
context.fillRect(50, 50, 50, 50);
```

### 2DFillRectGradientExample02.htm

这段代码创建了一个矩形，该矩形只有在左上角仅有少量的白色。这是因为矩形是在渐变的中点绘制的，那里颜色过渡几乎已经完成。由于渐变是不重复的，因此矩形大部分是黑色的。保持渐变与形状对齐非常重要，有时使用函数来计算合适的坐标是非常有用的。例如：

![image](img/logo1.gif)

```javascript
function createRectLinearGradient(context, x, y, width, height){
    return context.createLinearGradient(x, y, x+width, y+height);
}
```

### 2DFillRectGradientExample03.htm

此函数根据起始的 x 和 y 坐标以及宽度和高度创建一个渐变，这样就可以将相同的数字用于`fillRect()`：

```javascript
var gradient = createRectLinearGradient(context, 30, 30, 50, 50);
gradient.addColorStop(0, "white");
gradient.addColorStop(1, "black");

//绘制渐变矩形
context.fillStyle = gradient;
context.fillRect(30, 30, 50, 50);
```

### 2DFillRectGradientExample03.htm

跟踪坐标是使用 canvas 时一个重要且复杂的方面。像`createRectLinearGradient()`这样的辅助函数可以减轻管理坐标痛苦。

径向渐变是通过`createRadialGradient()`方法创建的。该方法接受六个参数，对应圆心及其半径。前三个参数定义起始圆的中心（`x`和`y`）和半径，而后三个参数定义结束圆的相同属性。在考虑径向渐变时，将其想象成一个长圆柱体会有帮助，你正在定义两端圆的大小。通过让一个圆变小而另一个圆变大，你实际上制造了一个锥体，并通过移动每个圆的中心来旋转该锥体。

要创建一个从形状中心开始并向外延伸的径向渐变，你需要将两个圆的中心设置为同一个原点。例如，为了在上一个示例的矩形中心创建一个径向渐变，两个圆都必须居中于 (55,55)。这是因为矩形是从点 (30,30) 到点 (80,80) 绘制的。以下是代码：

```javascript
var gradient = context.createRadialGradient(55, 55, 10, 55, 55, 30);
gradient.addColorStop(0, "white");
gradient.addColorStop(1, "black");

//绘制一个红色矩形
context.fillStyle = "#ff0000";
context.fillRect(10, 10, 50, 50);

//绘制渐变矩形
context.fillStyle = gradient;
context.fillRect(30, 30, 50, 50);
```

### 2DFillRectGradientExample04.htm

运行此代码将得到图 15-12 所示的图形。

图 15-12

![image](img/f567-01.jpg)

径向渐变由于其创建过程的复杂性处理起来稍微困难一些，但通常你会对起始圆和结束圆使用相同的中心，只需更改圆的半径来实现大多数基本效果。

## 模式 (Patterns)

模式简单来说就是重复图像，用于填充或描边形状。要创建一个新模式，调用`createPattern()`方法并传递两个参数：一个 HTML `<img>`元素和一个指示图像如何重复的字符串。第二个参数与 CSS 的`background-repeat`属性值相同："repeat"、"repeat-x"、"repeat-y"和"no-repeat"。例如：

![image](img/logo1.gif)

```javascript
var image = document.images[0],
    pattern = context.createPattern(image, "repeat");

//绘制一个矩形
context.fillStyle = pattern;
context.fillRect(10, 10, 150, 150);
```

### 2DFillRectPatternExample01.htm

请记住，和渐变一样，模式实际上是从画布上的点 (0,0) 开始的。将填充样式设置为模式意味着是在指定位置显示模式，而不是从该位置开始绘制。这段代码生成的页面看起来像图 15-13。

图 15-13

![image](img/f567-02.jpg)

`createPattern()`的第一个参数也可以是`<video>`元素或其他`<canvas>`元素。

## 处理图像数据 (Working with Image Data)

2D 上文中更强大的功能之一是使用`getImageData()`方法获取原始图像数据。该方法接受四个参数：要获取数据的第一个像素的左侧和顶部位置，以及要获取的像素宽度和像素高度。例如，要获取 50x50 区域的图像数据，请以下代码：

```javascript
var imageData = context.getImageData(10, 5, 50, 50);
```

返回的对象是`ImageData`实例。`data`属性是一个包含像素信息的`Uint8ClampedArray`。每个像素由四个项目表示：红、绿、蓝和透明度。数组中的每个值都是 0 到 255 之间的数字。访问原始数据允许你以各种方式处理图像。例如，可以通过以下方式创建一个灰度滤镜：

![image](img/logo.gif)

```javascript
var drawing = document.getElementById("drawing");

// 确保支持 <canvas>
if (drawing.getContext){
    var context = drawing.getContext("2d"),
        image = document.images[0],
        imageData, data,
        i, len, average,
        red, green, blue, alpha;

    //绘制原始图像
    context.drawImage(image, 0, 0);

    //获取图像数据
    imageData = context.getImageData(0, 0, image.width, image.height);
    data = imageData.data;

    for (i=0, len=data.length; i+=4){
        red = data[i];
        green = data[i+1];
        blue = data[i+2];
        alpha = data[i+3];

        // 获取 rgb 的平均值
        average = Math.floor((red + green + blue) / 3);

        // 设置颜色，保持透明度不变
        data[i] = average;
        data[i+1] = average;
        data[i+2] = average;
    }

    // 写回图像数据并显示
    imageData.data = data;
    context.putImageData(imageData, 0, 0);
}
```

### 2DImageDataExample01.htm

此示例将图像绘制到画布上，然后获取其图像数据。for 循环遍历图像数据中的每个像素。注意每次循环`i`的值都会加 4。一旦获取了红、绿、蓝值，就会对它们取平均值以得到新值。然后将这些值都设置为该平均值，从而消除了颜色，在原位置留下了亮度相似的灰色。

所有在 2D 上下文中进行的绘制操作都有两个属性：`globalAlpha`和`globalCompositionOperation`。`globalAlpha`属性是一个 0 到 1 之间的数字（包含边界），用于指定所有绘制透明度（alpha 值）。默认值为 0。如果后续的所有绘制都应该使用相同的透明度，请将`globalAlpha`设置为适当的值，执行绘制，然后将`globalAlpha`设置回 0。例如：

![image](img/logo1.gif)

```javascript
//draw a red rectangle
context.fillStyle = "#ff0000";
context.fillRect(10, 10, 50, 50);

//change the global alpha
context.globalAlpha = 0.5;

//draw a blue rectangle
context.fillStyle = "rgba(0,0,255,1)";
context.fillRect(30, 30, 50, 50);

//reset
context.globalAlpha = 0;
```

### 2DGlobalAlphaExample01.htm

在这个示例中，蓝色矩形被绘制在红色矩形之上。由于在绘制蓝色矩形之前将`globalAlpha`设置为 0.5，它变得部分透明，使得透过蓝色可以看到红色矩形。

`globalCompositionOperation`属性指示了新绘制的形状应如何与上下文中已存在的图像合并。该属性是以下值之一的字符串值：

*   `source-over`（默认）—— 新绘制的内容绘制在现有图像之上。
*   `source-in` —— 新绘制的内容仅在与现有图像叠加的地方绘制。其他部分均变为透明。
*   `source-out` —— 新绘制的内容仅在与现有图像不重叠的地方绘制。其他部分均变为透明。
*   `source-atop` —— 新绘制的内容仅在与现有图像重叠的地方绘制。现有图像其他情况下不受影响。
*   `destination-over` —— 新绘制的内容绘制在现有图像下方，仅通过之前透明的像素可见。
*   `destination-in` —— 新绘制的内容绘制在现有图像下方，且两个图像不重叠的所有地方变为透明。
*   `destination-out` —— 新绘制的内容会擦除现有图像中重叠的部分。
*   `destination-atop` —— 新绘制的内容绘制在现有图像之后。在与新绘制没有重叠的地方，现有图像变为透明。
*   `lighter` —— 通过将新绘制的值与现有图像的值相加来绘制内容，从而创建一个更亮的图像。
*   `copy` —— 新绘制的内容擦除现有图像并完全替换它。
*   `xor` —— 通过将图像数据与现有图像进行异或（XOR）运算来绘制。

这些复合操作的描述很难用语言或黑白图像表示。为了更好地演示每个操作，请查看[`developer.mozilla.org/samples/canvas-tutorial/6_1_canvas_composite.html`](https://developer.mozilla.org/samples/canvas-tutorial/6_1_canvas_composite.html)。建议在 Internet Explorer 9+ 或 Firefox 4+ 中访问此网站，因为它们拥有 canvas 最完整的实现。这里有一个简单的示例：

![image](img/logo1.gif)

```javascript
//draw a red rectangle
context.fillStyle = "#ff0000";
context.fillRect(10, 10, 50, 50);

//set composite operation
context.globalCompositeOperation = "destination-over";

//draw a blue rectangle
context.fillStyle = "rgba(0,0,255,1)";
context.fillRect(30, 30, 50, 50);
```

### 2DGlobalCompositeOperationExample01.htm

尽管蓝色矩形通常会绘制在红色矩形上方，但将`globalCompositeOperation`设置为"destination-over"意味着红色矩形实际上位于蓝色矩形之上。

在使用`globalCompositionOperation`时，请确保在多种浏览器中进行测试。这些操作在跨浏览器实现上仍然存在显著差异。Safari 和 Chrome 在这些操作上仍存在若干问题，可以通过访问上述 URL 并将其渲染结果与 Internet Explorer 或 Firefox 进行对比来观察。

## WEBGL

WebGL 是 canvas 的 3D 上下文。与其他 Web 技术不同，WebGL 由 W3C 规范。相反，Khronos Group 正在开发该规范。根据其网站，"Khronos Group 是一个非营利的、成员资助的财团，专注于为各种平台和设备创建用于并行计算、图形和动态媒体的免版开放标准。"Khronos Group 还致力于过其他图形 API，例如 OpenGL ES 2.0，它是浏览器中 WebGL 的基础。

像 OpenGL 等 3D 图形语言是复杂的课题，涵盖所有概念超出了本书的范围。建议在使用 WebGL 时熟悉 OpenGL ES 2.0，因为许多概念是直接对应的。

本节假设你已具备 OpenGL ES 2.0 概念的知识，仅尝试描述 OpenGL ES 2.0 的某些部分如何在 WebGL 中实现。有关 OpenGL 的更多信息，请访问[www.opengl.org](http://www.opengl.org)，有关极佳的 WebGL 教程，请访问[www.learningwebgl.com](http://www.learningwebgl.com)。

## 类型数组 (Typed Arrays)

由于 WebGL 处理的是需要可预测精度的复杂计算，标准的 JavaScript 数字并不能起作用。相反，WebGL 引入了类型数组（typed arrays）的概念，其数组项被设置为特定类型的数组。类型数组的核心是名为`ArrayBuffer`的类型。`ArrayBuffer`对象表示固定长度的原始二进制缓冲区。

```javascript
var buffer = new ArrayBuffer(20);
alert(buffer.byteLength);
```

### 视图 (Views)

数组视图是使用缓冲区内字节的一种方式。最通用的视图是`DataView`，它允许你选择字节集。要这样做，创建一个`DataView`实例，并传入`ArrayBuffer`、一个可选的字节偏移量以及可选的字节数。

```javascript
// 创建整个缓冲区的视图
var view = new DataView(buffer);

// 从字节 9 开始创建视图
var view = new DataView(buffer, 9);
```



// 从字节 9 到 18 创建视图

```
var view = new DataView(buffer, 9, 10);
```

```javascript
alert(view.byteOffset);
alert(view.byteLength);
```

这些属性让你以后轻松检查视图。你也可以通过`buffer`属性检索缓冲区。

读取和写入`DataView`根据你处理的数据类型通过一系列 getter 和 setter 方法完成。下表列出了支持的数据类型及其关联方法：

| 数据类型 | getter 方法 | setter 方法 |
| --- | --- | --- |
| 有符号 8 位整数 | `getInt8(byteOffset)` | `setInt8(byteOffset, value)` |
| 无符号 8 位整数 | `getUint8(byteOffset)` | `setUint8(byteOffset, value)` |
| 有符号 16 位整数 | `getInt16(byteOffset, littleEndian)` | `setInt16(byteOffset, value, littleEndian)` |
| 无符号 16 位整数 | `getUint16(byteOffset, littleEndian)` | `setUint16(byteOffset, value, littleEndian)` |
| 有符号 32 位整数 | `getInt32(byteOffset, littleEndian)` | `setInt32(byteOffset, value, littleEndian)` |
| 无符号 32 位整数 | `getUint32(byteOffset, littleEndian)` | `setUint32(byteOffset, value, littleEndian)` |
| 32 位浮点数 | `getFloat32(byteOffset, littleEndian)` | `setFloat32(byteOffset, value, littleEndian)` |
| 64 位浮点数 | `getFloat64(byteOffset, littleEndian)` | `setFloat64(byteOffset, value, littleEndian)` |

每个方法都期望第一个参数是用于读取或写入的字节偏移（byte offset）。请记住，取决于数据类型，数据的存储可能需要超过一个字节。一个无符号 8 位整数占用一个字节存储，而一个 32 位浮点数则占用四个字节。使用`DataView`，你需要自己管理这些，确保你确切知道你的数据需要多少字节，并使用正确的方法。例如：

![image](img/logo1.gif)

```
var buffer = new ArrayBuffer(20),
    view = new DataView(buffer),
    value;

view.setUint16(0, 25);
view.setUint16(2, 50);   //不要从 1 开始，16 位整数占用两个字节
value = view.getUint16(0);
```

DataViewExample01.htm

这段代码将两个无符号 16 位整数保存到数组缓冲区中。由于每个 16 位整数占用两个字节，因此，第一个数字存储在字节偏移 0 处，而第二个数字存储在字节偏移 2 处。

每个处理 16 位或更大数字的方法都有一个名为`littleEndian`的可选参数。这是一个布尔值，指示该值是否应该以小端序（最低位字节是第一个字节）而不是大端序（最低位字节是最后一个字节）进行读取或写入。如果你不确定使用哪一个，请省略此选项以使用默认的大端序存储模式。

由于你处理的是字节偏移而不是项目索引，因此可以通过不同的方式访问相同的字节。例如：

![image](img/logo1.gif)

```
var buffer = new ArrayBuffer(20),
    view = new DataView(buffer),
    value;

view.setUint16(0, 25);
value = view.getInt8(0);
alert(value);    //0
```

DataViewExample02.htm

在这个示例中，数字 25 被写入一个从字节偏移 0 开始的 16 位无符号整数中。尝试将该值作为 8 位有符号整数进行读取会导致返回值为 0。这是因为 25 的二进制形式在第一个字节中全为 0（请参见图 15-14）。

FIGURE 15-14

![image](img/f573-01.jpg)

因此，虽然`DataView`让你访问数组缓冲区中的字节级数据，但你需要跟踪数据存储的位置以及它需要多少字节。这可能是一大量工作，因此也提供了类型视图（typed views）。

### 类型视图

类型视图通常被称为类型数组（typed arrays），因为它们的作用类似于普通数组，不同之处在于元素必须是特定数据类型。有几种类型视图，并且它们都继承自`DataView`：

*   `Int8Array` —— 用 8 位带补码整数表示数字。
*   `Uint8Array` —— 用 8 位无符号整数表示数字。
*   `Int16Array` —— 用 16 位带补码整数表示数字。
*   `Uint16Array` —— 用 16 位无符号整数表示数字。
*   `Int32Array` —— 用 32 位带补码整数表示数字。
*   `Uint32Array` —— 用 32 位无符号整数表示数字。
*   `Float32Array` —— 用 32 位 IEEE 浮点值表示数字。
*   `Float64Array` —— 用 64 位 IEEE 浮点值表示数字。

每个视图以不同的方式表示数据，每条数据可能需要占用一个或多个字节来表示。例如，一个 20 字节的`ArrayBuffer`在`Int8Array`或`Uint8Array`中将包含 20 个值；在`Int16Array`或`Uint16Array`中包含 10 个值；在`Int32Array`、`Uint32Array`或`Float32Array`中包含 5 个值；或者在`Float64Array`中包含 2 个值。

由于这些类型都继承自`DataView`，你可以使用相同的构造函数参数实例化它们：使用的`ArrayBuffer`对象、起始字节偏移（默认为 0）以及包含的字节数。只需要第一个参数。一些示例：

```
//创建一个使用整个缓冲区的新数组
var int8s = new Int8Array(buffer);

//仅使用从字节 9 开始的字节
var int16s = new Int16Array(buffer, 9);

//仅使用从 9 开始到 18 的字节
var uint16s = new Uint16Array(buffer, 9, 10);
```

能够指定缓冲区的子集意味着你可以在同一个缓冲区内存储不同的数值类型。例如，以下允许在缓冲区开头存储 8 位整数，在剩余部分存储 16 位整数：

```
//使用缓冲区的一部分存储 8 位整数，部分存储 16 位整数
var int8s = new Int8Array(buffer, 0, 10);
var uint16s = new Uint16Array(buffer, 11, 10);
```

每个视图构造函数都有一个名为`BYTES_PER_ELEMENT`的属性，它指示类型数组每个元素所需的字节数……（此处由于原文存在大量重复乱码，已按核心逻辑处理）。

支持的浏览器中的 WebGL 上下文名称为 "experimental-webgl"，因为 WebGL 规范仍在开发中。一旦开发完成，上下文名称将简单变为 "webgl"。如果浏览器不支持 WebGL，则尝试获取 WebGL 上下文将返回 null。在尝试使用上下文之前，你应该始终检查返回的值：

![image](img/logo1.gif)

```
var drawing = document.getElementById("drawing");

//make sure <canvas> is completely supported
if (drawing.getContext){
    var gl = drawing.getContext("experimental-webgl");
    if (gl){
        //proceed with WebGL
    }
}
```

WebGLExample01.htm

# WebGL 上下文对象

WebGL 上下文对象通常命名为`gl`。大多数 WebGL 应用和示例使用这种约定，因为 OpenGL ES 2.0 方法和值通常以 "gl" 开头。这样做意味着 JavaScript 代码读起来更像 OpenGL 程序。

一旦建立了 WebGL 上下文，你就可以开始 3D 绘画。如前所述，由于 WebGL 是 OpenGL ES 2.0 的 Web 版本，本节讨论的概念实际上是在 JavaScript 中实现的 OpenGL 概念。

# WebGL 上下文选项

你可以通过向`getContext()`传递第二个参数来指定 WebGL 上下文选项。该参数是一个包含以下一个或多个属性的对象：

*   `alpha` — 设置为 true 时，为上下文创建一个 alpha 通道缓冲区。默认为 true。
*   `depth` — 设置为 true 时，提供一个 16 位深度缓冲区。默认为 true。
*   `stencil` — 设置为 true 时，提供一个 8 位模板缓冲区。默认为 false。
*   `antialias` — 设置为 true 时，将使用默认机制进行抗锯齿处理。默认为 true。
*   `premultipliedAlpha` — 设置为 true 时，假设绘制缓冲区具有预乘法后的 alpha 值。默认为 true。
*   `preserveDrawingBuffer` — 设置为 true 时，在绘制完成后保留绘制缓冲区。默认为 false。只有在你确切知道此操作的作用时才建议更改，因为这可能会对性能产生影响。

选项对象的传递方式如下：

![image](img/logo1.gif)

```
var drawing = document.getElementById("drawing");

//make sure <canvas> is completely supported
if (drawing.getContext){
    var gl = drawing.getContext("experimental-webgl", { alpha: false});
    if (gl){
        //proceed with WebGL
    }
}
```

WebGLExample01.htm

大多数上下文选项是用于高级用的。在许多情况下，默认值就可以满足你的需求。

如果无法通过`getContext()`创建 WebGL 上下文，某些浏览器可能会抛出错误。因此，最好将该调用封装在 try-catch 块中：

```
Insert IconMargin [download]var drawing = document.getElementById("drawing"),
    gl;

//make sure <canvas> is completely supported
if (drawing.getContext){
    try {
        gl = drawing.getContext("experimental-webgl");
    } catch (ex) {
        //noop
    }
    if (gl){
        //proceed with WebGL
    } else {
        alert("WebGL context could not be created.");
    }
}
```

WebGLExample01.htm

# 常量

如果你熟悉 OpenGL，那么你就熟悉用于操作的大量常量。这些常量在 OpenGL 中带有`GL_`前缀。在 WebGL 中，每个常量都可以直接位于 WebGL 上下文对象上，无需`GL_`前缀。例如，`GL_COLOR_BUFFER_BIT`常量可以通过`gl.COLOR_BUFFER_BIT`访问。WebGL 以这种方式支持大多数 OpenGL 常量（某些常量不可用）。

# 方法命名

OpenGL 以及 WebGL 中的许多方法名称倾向于包含有关与该方法使用的数据类型的信息。如果一个方法可以接受不同类型和数量的参数，则会带有后缀以指示预期的输入。该方法将指示参数的数量（1 到 4），随后跟上数据类型（`f`表示浮点数，`i`表示整数）。例如，`gl.uniform4f()`期望传入四个浮点数，而`gl.uniform3i()`期望传入三个整数。

许多方法还允许传递数组而不是单个参数。这通过字母`v`表示，它是 vector（向量）的缩写。因此`gl.uniform3iv()`接受一个包含三个值的整数数组。在整个 WebGL 讨论过程中请记住这一约定。

# 准备绘制

在处理 WebGL 上文时，要做的步骤之一是用纯色清除`<canvas>`以为绘制做准备。要做到这一点，你必须首先通过`clearColor()`方法指定要使用的颜色。该方法接受四个参数：红、绿、蓝和 alpha。每个参数必须是 0 到 1 之间的数字，用于定义作为最终颜色部分的强度值。考虑以下示例：

![image](img/logo1.gif)

```
gl.clearColor(0,0,0,1);    //black
gl.clear(gl.COLOR_BUFFER_BIT);
```

WebGLExample01.htm

此代码将清除颜色缓冲区的值设置为黑色，然后调用`clear()`方法，这等同于 OpenGL 中的`glClear()`。提供参数`gl.COLOR_BUFFER_BIT`告诉 WebGL 清理颜色缓冲区。

# 视口与坐标

为了开始，定义 WebGL 视口是一个好习惯。默认情况下，视口设置为使用整个`<canvas>`。要更改视口，调用`viewport()`方法并传入视口的`x`、`y`、`width`和`height`。例如，此调用使用了整个`<canvas>`：

```
gl.viewport(0, 0, drawing.width, drawing.height);
```

视口是通过与网页使用的不同的坐标系定义的。`x-`和`y-`坐标从视口的左下角`(0,0)`开始，并向顶部和右侧增加，可以定义为`–1,–1)`（参见图 15-5）。

图 15-5

知道如何定义视口允许你使用`<canvas>`元素的局部进行绘制。考虑以下示例：

```
//视口是 <canvas> 左下角的分之一
gl.viewport(0, 0, drawing.width/2, drawing.height/2);

//视口是 <canvas> 左上角的分之一
gl.viewport(0, drawing.height/2, drawing.width/2, drawing.height/2);

//视口是 <canvas> 右下角的分之一
gl.viewport(drawing.width/2, 0, drawing.width/2, drawing.height/2);
```

视口内的坐标系与定义视口的坐标系不同。在视口内部，坐标从视口的中心`(0,0)`开始。左下角为`(–1,–1)`，而右上角为`(1,1)`（参见图 15-6）。

图 15-6

![image](img/f579-0.jpg)

如果在绘制操作中使用视口外的坐标，则绘制将沿视口进行裁剪。例如，尝试绘制一个具有`(1,2)`顶点的形状将导致形状在视口右侧被截断。

# 缓冲区

顶点信息存储在 JavaScript 的类型数组中，必须转换为 WebGL 缓冲区才能使用。缓冲区通过调用`gl.createBuffer()`创建，然后使用`gl.bindBuffer()`将其绑定到 WebGL 上下文。一旦完成，你就可以向缓冲区填充数据。例如：

```
var buffer = gl.createBuffer();
gl.bindBuffer(gl.ARRAY_BUFFER, buffer);
gl.bufferData(gl.ARRAY_BUFFER, new Float32Array([0, 0.5, 1]), gl.STATIC_DRAW);
```



调用`gl.bindBuffer()`将`buffer`设置为上下文当前的缓冲区。从该点开始，所有的缓冲区操作都将直接在`buffer`上进行。因此，`gl.bufferData()`的调用虽然没有包含对`buffer`的直接引用，但仍然对其进行操作。最后一行使用来自`Float32Array`的信息初始化`buffer`（你通常会使用`Float32Array`来处理所有顶点信息）。如果你打算使用`drawElements()`输出缓冲区内容，也可以使用`gl.ELEMENT_ARRAY_BUFFER`。

`gl.bufferData()`的最后一个参数指示了缓冲区将如何被使用。它是以下常量之一：

- `gl.STATIC_DRAW`: 数据将被加载一次，并用于多次绘制。
- `gl.STREAM_DRAW`: 数据将被加载一次，并仅用于绘制绘制几次。
- `gl.DYNAMIC_DRAW`: 数据将被反复修改，并用于多次绘制。

除非你是一个经验丰富的 OpenGL 程序员，否则你可能会对大多数缓冲区使用`gl.STATIC_DRAW`。

缓冲区会一直留在内存中，直到包含它的页面被卸载。如果你不再需要某个缓冲区，最好的方法是调用`gl.deleteBuffer()`来释放其内存：

```
gl.deleteBuffer(buffer);
```

### 错误

大多数 JavaScript 与 WebGL 之间的区别之一是，WebGL 操作通常不会抛出错误。相反，你必须在调用可能失败的方法后调用`gl.getError()`方法。该方法返回一个常量值，指示所发生的错误类型。这些常量如下：

- `gl.NO_ERROR`: 上次操作期间没有发生错误（值为 0）。
- `gl.INVALID_ENUM`: 向期望其中一个 WebGL 常量的方法传递了错误的参数。
- `gl.INVALID_VALUE`: 在只接受无符号数的地方传递了负数。
- `gl.INVALID_OPERATION`: 无法在当前状态下完成该操作。
- `gl.OUT_OF_MEMORY`: 没有足够的内存来完成该操作。
- `gl.CONTEXT_LOST_WEBGL`: 由于外部事件（如设备掉电），WebGL 上下文已丢失。

每次调用`gl.getError()`都会返回一个错误值。在初始调用之后，下一次调用`gl.getError()`可能会返回另一个错误值。如果存在多个错误，此过程将一直持续，直到`gl.getError()`返回`gl.NO_ERROR`。如果你执行了多次操作，你可能希望在循环中调用`getError()`，例如：

```
var errorCode = gl.getError();

while(errorCode){

    console.log("Error occurred: " + errorCode);

    errorCode = gl.getError();

}
```

如果你的 WebGL 脚本没有产生正确的输出，那么在脚本中加入几次`gl.getError()`调用可能有助于调试问题。

### 着色器

着色器是 OpenGL 的另一个概念。WebGL 中有两种着色器：顶点着色器和片元着色器。顶点着色器用于将 3D 顶点转换为渲染的 2D 点。片元着色器用于计算绘制单个像素的颜色。WebGL 着色器的独特且挑战性的之处在于它们不是用 JavaScript 编写的。着色器使用 OpenGL 着色语言 (GLSL) 编写，这是一种与 C 或 JavaScript 完全不同的语言。

#### 编写着色器

GLSL 是一种类 C 语言，专门用于定义 OpenGL 着色器。由于 WebGL 是 OpenGL ES 2 的实现，OpenGL 中使用的着色器可以直接用于 WebGL，从而可以将桌面图形轻松移植到 Web 端。

每个着色器都有一个名为`main()`的方法，在绘制期间反复执行。向着色器传递数据有两种方法：属性（attributes）和统一变量（uniforms）。属性用于将顶点传递给顶点着色器，而统一变量用于向类型的着色器传递常量值。属性和统一变量在`main()`外部通过关键字`attribute`或`uniform`分别定义。在值类型关键字之后，指定数据类型，然后是名称。这是一个简单的顶点着色器示例：

![image](img/logo1.gif)

```
//OpenGL Shading Language
//Shader by Bartek Drozdz in his article at
//http://www.netmagazine.com/tutorials/get-started-webgl-draw-square
attribute vec2 aVertexPosition;

void main() {
        gl_Position = vec4(aVertexPosition, 0.0, 1.0);
}
```

WebGLExample02.htm

此顶点着色器定义了一个名为`aVertexPosition`的单一属性。该属性是一个包含两个项目的数组（`vec2`数据类型），代表 x 坐标和 y 坐标。顶点着色器始终将一个四部分的顶点分配给特殊变量`gl_Position`，即使只传递了两个坐标。此着色器创建了一个新的四项数组（`vec4`）并填充了缺失的坐标，有效地将 2D 坐标转换为 3D 坐标。

片元着色器与顶点着色器类似，但你只能通过统一变量传递数据。这是一个片元着色器示例：

```
//OpenGL Shading Language
//Shader by Bartek Drozdz in his article at
//http://www.netmagazine.com/tutorials/get-started-webgl-draw-square
uniform vec4 uColor;

void main() {
        gl_FragColor = uColor;
}
```

WebGLExample02.htm

片元着色器的结果是将一个值赋值给`gl_FragColor`，这指示了绘制时使用的四部分（`vec4`）颜色`uColor`。

![image](img/pen.gif)

OpenGL 着色语言是这里表示更复杂的语言。

#### 创建着色器程序

GLSL 无法被浏览器原生理解，因此你必须准备好一个字符串用于编译和链接到着色器程序。为了方便使用，着色器通常通过`<script>`元素包含在页面中。使用类型属性防止浏览器尝试解释`<script>`内容，同时允许你访问。例如：

![image](img/logo1.gif)

```
<script type="x-webgl/x-vertex-shader" id="vertexShader">
attribute vec2 aVertexPosition;

void main() {
        gl_Position = vec4(aVertexPosition, 0.0, 1.0);
}
</script>

<script type="x-webgl/x-fragment-shader" id="fragmentShader">
uniform vec4 uColor;

void main() {
        gl_FragColor = uColor;
}
</script>
```

WebGLExample02.htm

你可以使用`text`属性提取`<script>`元素的内容：

```
var vertexGlsl = document.getElementById("vertexShader").text,
    fragmentGlsl = document.getElementById("fragmentShader").text;
```

更复杂的 WebGL 可能会选择使用 Ajax 动态下载着色器（见第 21 章）。关键点是你需要 GLSL 字符串才能使用着色器。

一旦有了 GLSL 字符串，下一步是创建着色器对象。这是通过调用`gl.createShader()`方法并传入要创建的着色器类型（`gl.VERTEX_SHADER`或`gl.FRAGMENT_SHADER`）完成的之后，使用`gl.shaderSource()`应用着色器源码并使用`gl.compileShader()`编译着色器。这是一个示例：

```
var vertexShader = gl.createShader(gl.VERTEX_SHADER);
gl.shaderSource(vertexShader, vertexGlsl);
gl.compileShader(vertexShader);

var fragmentShader = gl.createShader(gl.FRAGMENT_SHADER);
gl.shaderSource(fragmentShader, fragmentGlsl);
gl.compileShader(fragmentShader);
```

WebGLExample02.htm

这段代码创建了两个着色器并将它们存储在`vertexShader`和`fragmentShader`中。然后可以使用以下代码将这两个对象链接到着色器程序。

```javascript
var program = gl.createProgram();
gl.attachShader(program, vertexShader);
gl.attachShader(program, fragmentShader);
gl.linkProgram(program);
```

### WebGLExample02.htm

第一行创建了一个程序，然后使用`attachShader()`包含两个着色器。调用`gl.linkProgram()`将两个着色器封装到变量`program`中。程序链接完成后，你可以通过`gl.useProgram()`方法指示 WebGL 上下文使用该程序：

```javascript
gl.useProgram(program);
```

在调用`gl.useProgram()`后，所有后续绘制操作都将使用指定的`program`。

### 向着色器传递值

之前定义的每个着色器都有一个必须传入的值以完成着色器的工作。要向着色器传递值，你必须首先找到需要填充值的变量。对于 uniform 变量（统一变量变量），这是通过`gl.getUniformLocation()`完成的，它返回一个表示该 uniform 变量在内存中位置的对象。然后你可以使用该位置来分配数据。例如：

![image](img/logo1.gif)

```javascript
var uColor = gl.getUniformLocation(program, "uColor");
gl.uniform4fv(uColor, [0, 0, 0, 1]);
```

WebGLExample02.htm

此示例在`program`中定位 uniform 变量`uColor`并返回其内存位置。第二行使用`gl.uniform4fv()`为`uColor`分配一个值。

顶点着色器中的属性变量（attribute variables）遵循类似的过程。要获取属性变量的位置，请使用`gl.getAttribLocation()`。一旦获取了位置，就可以像示例那样使用：

```javascript
var aVertexPosition = gl.getAttribLocation(program, "aVertexPosition");
gl.enableVertexAttribArray(aVertexPosition);
gl.vertexAttribPointer(aVertexPosition, itemSize, gl.FLOAT, false, 0, 0);
```

WebGLExample02.htm

在这里，获取了`aVertexPosition`的位置，以便通过`gl.enableVertexAttribArray()`启用其使用。最后一行在通过`gl.bindBuffer()`指定最后一个缓冲区中创建一个指针，并将其存储在`aVertexPosition`中，供顶点着色器使用。

### 调试着色器和程序

与 WebGL 中的其他操作一样，着色器操作可能会失败且静默失败。如果你认为发生了错误，需要手动向 WebGL 上下文询问着色器或程序的信息。

对于着色器，调用`gl.getShaderParameter()`在尝试编译后获取着色器的编译状态：

![image](img/logo1.gif)

```javascript
if (!gl.getShaderParameter(vertexShader, gl.COMPILE_STATUS)){
    alert(gl.getShaderInfoLog(vertexShader));
}
```

WebGLExample02.htm

此示例检查`vertexShader`的编译状态。如果着色器编译成功，则`gl.getShaderParameter()`返回`true`。如果返回`false`，则编译过程中发生了错误，你可以使用`gl.getShaderInfoLog()`并传入着色器来获取错误。该方法返回一个指示问题的字符串消息。`gl.getShaderParameter()`和`gl.getShaderInfoLog()`都可以用于顶点着色器和片段着色器。

程序也可能失败，并有一个类似的方法`gl.getProgramParameter()`来检查状态。最常见的程序失败发生在链接过程中，你可以使用以下代码进行检查：

```javascript
if (!gl.getProgramParameter(program, gl.LINK_STATUS)){
    alert(gl.getProgramInfoLog(program));
}
```

WebGLExample02.htm

与`gl.getShaderParameter()`一样，`gl.getProgramParameter()`返回`true`表示链接成功，或返回`false`表示失败。还有`gl.getProgramInfoLog()`，用于在失败期间获取有关程序的信息。

这些方法主要用于开发期间以辅助调试。只要没有外部依赖，在生产环境中移除它们是安全的。

### 绘制

WebGL 只能绘制三种类型的形状：点、线和三角形。所有其他形状都必须通过在三维空间中绘制这三种基本形状的组合组成。绘制通过使用`drawArrays()`或`drawElements()`方法执行；前者作用于数组缓冲区（array buffers），后者作用于元素数组缓冲区（element array buffers）。

`gl.drawArrays()`和`drawElements()`的第一个参数都是指示要绘制形状类型的常量。常量如下：

* `gl.POINTS` — 将每个顶点视为一个要绘制的点。
* `gl.LINES` — 将数组视为一组顶点，在这些顶点之间绘制线。每组顶点是一个起点和一个终点，因此为了进行所有绘制，数组中的顶点数量必须是偶数。
* `gl.LINE_LOOP` — 将数组视为一组顶点，在这些顶点之间绘制线。线从第一个顶点画到第二个，从第二个画到第三个，以此此类推，直到到达最后一个顶点。然后从最后一个顶点画到第一个顶点。这在实际上创建了一个形状的轮廓。
* `gl.LINE_STRIP` — 与`gl.LINE_LOOP`相同，但不会从最后一个顶点回到第一个顶点画线。
* `gl.TRIANGLES` — 将数组视为一组顶点，在其中绘制三角形。每个三角形都是独立绘制的，除非显式指定。
* `gl.TRIANGLES_STRIP` — 与`gl.TRIANGLES`相同，但前三个顶点之后的顶点被单独处理。
* `gl.FAN` — 与`gl.TRIANGLES_STRIP`相同，但所有三角形共享第一个顶点。

`gl.drawArrays()`方法接受这些值中的一个作为其第一个参数，数组缓冲区中的起始索引作为第二个参数，数组中包含的集合作为第三个参数。以下代码使用`drawArrays()`在画布上绘制一个三角形：

![image](img/logo1.gif)

```javascript
//假设已使用着色器清理了口
//定义三个顶点，每个点的 x 和 y
var vertices = new Float32Array([ 0, 1, 1, -1, -1, -1 ]),
    buffer = gl.createBuffer(),
    vertexSetSize = 2,
    vertexSetCount = vertices.length/2,
    uColor, aVertexPosition;

//将数据放入缓冲区
gl.bindBuffer(gl.ARRAY_BUFFER, buffer);
gl.bufferData(gl.ARRAY_BUFFER, vertices, gl.STATIC_DRAW);

//将颜色传递给片段着色器
uColor = gl.getUniformLocation(program, "uColor");
gl.uniform4fv(uColor, [ 0, 0, 0, 1 ]);

//将顶点信息传递给着色器
aVertexPosition = gl.getAttribLocation(program, "aVertexPosition");
gl.enableVertexAttribArray(aVertexPosition);
gl.vertexAttribPointer(aVertexPosition, vertexSetSize, gl.FLOAT, false, 0, 0);

//绘制三角形
```



```javascript
gl.drawArrays(gl.TRIANGLES, 0, vertexSetCount);
```

### WebGLExample02.htm

此示例定义了一个包含三组双点顶点的 `Float32Array`。跟踪大小和数量以便后续计算是非常重要的。`vertexSetSize` 被设置为 2，`vertexSetCount` 被计算出来。顶点信息存储在缓冲区中。

最后一步是使用 `gl.drawArrays()` 绘制三角形。通过将第一个参数指定为 `gl.TRIANGLES`，将绘制从 (0,1) 到 (1,–1) 再到 (–1,–1) 的三角形，并用传递给片段色器的颜色进行填充。第二个参数是缓冲区中的起始偏移，最后一个参数是要读取的顶点集总数。此绘制操作的结果显示在图 15-17 中。

图 15-17

![image](img/f586-01.jpg)

通过更改 `gl.drawArrays()` 的第一个参数，你可以改变三角形的绘制方式。图 15-18 显示了更改第一个参数后其他可能的输出。

图 15-18

![image](img/f586-02.jpg)

## 纹理

WebGL 纹理与 DOM 中的图像协同工作。你使用 `gl.createTexture()` 创建新纹理，然后将图像绑定到该纹理上。如果图像尚未加载，你可能需要创建一个新的 `Image` 实例来动态加载它。在图像完全加载之前，纹理不会被初始化，因此纹理设置步骤必须在加载事件触发后完成。例如：

```javascript
var image = new Image(),
    texture;

image.src = "smile.gif";

image.onload = function(){

    texture = gl.createTexture();

    gl.bindTexture(gl.TEXTURE_2D, texture);

    gl.pixelStorei(gl.UNPACK_FLIP_Y_WEBGL, true);

    gl.texImage2D(gl.TEXTURE_2D, 0, gl.RGBA, gl.RGBA, gl.UNSIGNED_BYTE, image);

    gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_MAG_FILTER, gl.NEAREST);

    gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_MIN_FILTER, gl.NEAREST);

    //clear current texture

    gl.bindTexture(gl.TEXTURE_2D, null);

}
```

除了使用 DOM 图像外，在 OpenGL 中创建纹理的这些步骤是相同的。最大的区别在于使用 `gl.pixelStorei()` 设置像素存储格式。常量 `gl.UNPACK_FLIP_Y_WEBGL` 是 WebGL 特有的，在加载基于 Web 的图像时，大多数情况下必须使用。这是因为 GIF、JPEG 和 PNG 图像使用的坐标系统与 WebGL 内部坐标系不同。如果没有此标志，图像将以倒置的方式解释。

用于纹理的图像必须与包含它的页面同源，否则必须存在于开启了图像跨源资源共享（CORS）的服务器上。CORS 在第 21 章中讨论。

![image](img/pen.gif)

纹理源可以是图像、加载到 `<video>` 元素中的视频，甚至是另一个 `<canvas>` 元素。跨源资源的相同限制也视频。

## 读取像素

与 2D 上下文一样，从 WebGL 上下文中读取像素。`readPixels()` 方法的参数与 OpenGL 中的相同，不同之处最后一个参数必须是一个类型数组（typed array）。像素信息从帧缓冲区读取并放入类型数组中。`readPixels()` 的参数为 `x`、`y`、`width`、`height`、图像格式、`type` 和类型数组。前四个参数指定了要读取像素的位置。图像格式参数几乎总是 `gl.RGBA`。`type` 参数是要将存储在类型数组中的数据类型，并具有以下限制：

- 如果 `type` 为 `gl.UNSIGNED_BYTE`，则类型数组必须是 `Uint8Array`。
- 如果 `type` 为 `gl.UNSIGNED_SHORT_5_6_5`、`gl.UNSIGNED_SHORT_4_4_4_4` 或 `gl.UNSIGNED_SHORT_5_5_5_1`，则类型数组必须是 `Uint16Array`。

这是一个简单的示例：

```javascript
var pixels = new Uint8Array(25*25);

gl.readPixels(0, 0, 25, 25, gl.RGBA, gl.UNSIGNED_BYTE, pixels);
```

这段代码读取帧缓冲区的 25 × 25 区域并将像素信息存储在 `pixels` 数组中。每个像素颜色表示为四个数组项，分别代表红、绿、蓝和 Alpha。这些值是 0 到 255 的整数（包含边界）。不要忘记根据预期返回的数据量来初始化类型数组。

在浏览器绘制更新后的 WebGL 图像之前调用 `readPixels()` 将按预期工作。在绘图发生后，帧缓冲区将恢复到原始的清除状态，调用 `readPixels()` 将导致像素数据与清除状态匹配。如果你想在绘制发生后读取像素，则必须使用之前讨论过的 `preserveDrawingBuffer` 选项初始化 WebGL 上下文：

```javascript
var gl = drawing.getContext("experimental-webgl", { preserveDrawingBuffer: true; });
```

设置此标志将强制帧缓冲区保持在最后状态，直到下次绘制发生。此选项会有一些性能开销，因此尽量避免使用。

## 支持

WebGL API 已经在 Firefox 4+ 和 Chrome 中实现。Safari 5.1 实现了 WebGL，但默认是禁用的。较旧的计算机（例如运行 Windows XP 的计算机）通常具有过时的驱动程序，因此 WebGL 在浏览器中会被禁用。因此，专门检查支持情况比检查特定浏览器更重要。

XDM 的核心是 `postMessage()` 方法。该方法名除了 XDM 之外还用于 HTML5 的许多部分，并且始终用于同一个目的：将数据传递到另一个位置。在 XDM 的情况下，该另一个位置是页面拥有的 `<iframe>` 元素或弹出窗口。

`postMessage()` 方法接受两个参数：一个消息和一个指示预期接收者源（origin）的字符串。出于安全考虑，第二个参数非常重要，它限制了浏览器递送消息的位置。请考虑这个示例：

```javascript
//note: 所有支持 XDM 的浏览器也都支持 iframe contentWindow 

var iframeWindow = document.getElementById("myframe").contentWindow;

iframeWindow.postMessage("A secret", "http://www.wrox.com");
```

最后一行尝试向 `iframe` 发送消息，并指定源必须是 `http://www.wrox.com`。如果源匹配，则消息将递送到 `iframe` 中；否则 `postMessage()` 将静默地什么都不做。这种限制可以保护您的信息，以防窗口位置在您不知情的情况下发生变化。虽然通过向 `postMessage()` 的第二个参数传递 `*` 可以允许向任何源发送消息，但并不推荐这样做。

当接收到 XDM 消息时，窗口会触发消息事件（message event）。此消息是异步触发的，因此发送消息的时间与接收窗口触发消息事件的时间之间存在延迟。传递给 `onmessage` 事件处理器的对象包含三个重要信息：

- `data` — 作为第一个参数传递给 `postMessage()` 的字符串数据。
- `origin` — 发送消息的文档的源，例如 `http://www.wrox.com`。
- `source` — 发送消息的文档窗口对象的代理。该代理对象主要用于在发送最后消息的窗口上执行 `postMessage()` 方法。如果发送窗口具有相同的源，则这可能是实际窗口对象。

在接收消息时，验证发送窗口的源是非常重要的。就像指定 `postMessage()` 的第二个参数可以确保数据不会无意中传递给未知页面一样，在 `onmessage` 期间检查源可以确保正在传递的数据来自正确的地方。基本模式如下：

```javascript
EventUtil.addHandler(window, "message", function(event){

    // 确保发送者是预期的

    if (event.origin == "http://www.wrox.com"){

        // 对数据进行处理

        processMessage(event.data);

        // 可选：向原始窗口发回消息

        event.source.postMessage("Received!", "http://p2p.wrox.com");

    }

});
```

请记住，在大多数情况下，`event.source` 是窗口的代理而不是实际的窗口对象，因此你无法访问所有的窗口信息。最好的方法是直接使用 `postMessage()`，它始终存在且始终可调用。

XDM 有一些与人而异的细微之处（或称特殊之处，quirks）。首先，`postMessage()` 的第一个参数最初实现为总是字符串。该第一个参数的定义变为允许传递任何结构化数据；然而，并非所有浏览器都实现了这一变化。出于此原因，最好始终使用 `postMessage()` 传递字符串。如果你需要传递结构化数据，最佳方法是对数据调用 `JSON.stringify()`，将生成的字符串传递给 `postMessage()`，然后在 `onmessage` 事件处理程序中调用 `JSON.parse()`。

当尝试使用不同域的 `iframe` 对内容进行沙箱化处理时，XDM 极其有用。这种方法经常用于聚合应用（mashups）和社交网络应用程序。包含页面能够通过 XDM 与嵌入的 iframe 通信，从而保护自己免受恶意内容的影响。XDM 也可以用于同域页面。

Internet Explorer 8+、Firefox 3.5+、Safari 4+、Opera、Chrome、iOS Safari 以及 Android 的 WebKit 都支持 XDM。XDM 已分离到自己的规范中，现在被称为 Web Messaging，可以在 `http://dev.w3.org/html5/postmsg/` 找到。

## 原生拖放

Internet Explorer 4 首次引入了对网页拖放功能的 JavaScript 支持。当时，网页上只有两个项目可以启动系统拖放：图像或某些文本。拖动图像时，你只需按住鼠标按钮并移动它；对于文本，你首先高亮一些文本，然后就可以像拖动图像一样拖动它。在 Internet Explorer 4 中，唯一的有效放置目标是文本框。在 5 版本中，Internet Explorer 通过添加新事件扩展了其拖放功能，并允许网页上的几乎任何内容成为放置目标。5.5 版本更进了一步，允许几乎任何内容都变成可拖取的。（Internet Explorer 6 也支持此功能。）HTML5 使用 Internet Explorer 的拖放实现作为其拖放规范的基础。Firefox 3.5、Safari 3+ 和 Chrome 也根据 HTML5 规范实现了原生拖放。

拖放支持可能最有趣的一点是，元素可以跨帧（frames）、浏览器窗口，有时甚至是其他应用程序进行拖放。浏览器中的拖放支持允许你利用该功能。

## 拖放事件

为拖放提供的事件允许你控制拖放操作的几乎每个方面。棘之处在于确定每个事件在何处触发：某些事件在拖拽的项目上触发，另一些在放置目标上触发。当拖拽项目时，触发的事件顺序如下：

1. `dragstart`
2. `drag`
3. `dragend`

当你按住鼠标按钮并开始移动时，`dragstart` 事件在拖拽的项目上触发。光标会变为禁止符号（带斜线的圆），表示该项目无法放置在自身。你可以使用 `ondragstart` 事件处理器在拖放开始时运行 JavaScript 代码。

在 `dragstart` 事件触发后，`drag` 事件触发，只要对象在被拖动，它就会持续触发。这类似于 `mousemove`，鼠标移动时也会反复触发。当拖放停止（因为你将项目放置在有效或无效的目标上），`dragend` 事件触发。

所有三个事件的目标都是被拖拽的元素。默认情况下，浏览器在拖放期间不会更改被拖拽元素外观，因此由你来更改外观。然而，大多数浏览器会创建一个拖拽元素的半透明克隆，它始终位于光标正下方。

当项目拖到有效放置目标上方时，会发生以下事件序列：

1. `dragenter`
2. `dragover`
3. `dragleave` 或 `drop`

`dragenter` 事件（类似于 `mouseover` 事件）在项目拖过放置目标时立即触发。在 `dragenter` 事件触发后，`dragover` 事件触发，只要项目在放置目标的边界内拖动，它就会持续触发。当项目拖出放置目标边界时，`dragover` 停止触发并触发 `dragleave` 事件。如果拖拽的项目实际上被放置在目标上，则触发 `drop` 事件而不是 `dragleave`。这些事件的目标是放置目标元素。

## 自定义放置目标

当你尝试将某些内容拖到无效的放置目标上时，你会看到一个特殊的光标（一个带斜线的圆圈），表示你无法放置。尽管所有元素都支持放置目标事件，但默认情况下是不允许放置的。如果你将一个元素拖到某个不允许放置的对象上方，无论用户如何操作，`drop`（放置）事件永远都不会触发。然而，你可以通过重写 `dragenter` 和 `dragover` 事件的默认行为，将任何元素转换为有效的放置目标。例如，如果你有一个 ID 为 `"droptarget"` 的 `<div>` 元素，你可以使用以下代码将其转换为放置目标：

```javascript
var droptarget = document.getElementById("droptarget");

EventUtil.addHandler(droptarget, "dragover", function(event){

    EventUtil.preventDefault(event);

});

EventUtil.addHandler(droptarget, "dragenter", function(event){

    EventUtil.preventDefault(event);

});
```

做出这些更改后，你会发现在拖拽元素时，光标现在显示允许在放置目标上放置。此外，`drop` 事件将会触发。

在 Firefox 3.5+ 中，`drop` 事件的默认行为是导航到放置在放置目标上的 URL。这意味着将图像放置到放置目标上会导致页面导航到图像文件，而放置在放置目标上的文本则会导致无效的 URL 错误。为了支持 Firefox，你必须取消 `drop` 事件的默认行为，以防止这种导航发生：

```javascript
EventUtil.addHandler(droptarget, "drop", function(event){

    EventUtil.preventDefault(event);

});
```

### dataTransfer 对象

除非实际上影响了数据，否则仅仅的拖动和释放没有任何用处。为了辅助通过拖放操作传输数据，Internet Explorer 5 引入了 `dataTransfer` 对象，它作为 `event` 的属性存在，用于将字符串数据从被拖拽的项目传输到放置目标。由于它是 `event` 的属性，因此在拖放事件的事件处理程序作用域之外，`dataTransfer` 对象是不存在的。在事件处理程序作用域内，你可以使用该对象的属性和方法来处理你的拖放功能。`dataTransfer` 对象现在是 HTML5 工作草案的一部分。

`dataTransfer` 对象有两个主要方法：`getData()` 和 `setData()`。正如你所预期的，`getData()` 能够检索由 `setData()` 保存的值。`setData()` 的第一个参数，也是 `getData()` 的唯一参数，是一个指示所设置数据类型的字符串：可以是 `"text"` 或 `"URL"`，如下所示：

```javascript
// 处理文本

event.dataTransfer.setData("text", "some text");

var text = event.dataTransfer.getData("text");

// 处理 URL

event.dataTransfer.setData("URL", "http://www.wrox.com/");

var url = event.dataTransfer.getData("URL");
```



尽管 Internet Explorer 初始仅引入了`"text"`和`"URL"`作为有效数据类型，但 HTML5 扩展了这一点，允许指定任何 MIME 类型。为了向兼容，HTML5 将支持`"text"`和`"URL"`，但它们被映射到`"text/plain"`和`"text/uri-list"`。

`dataTransfer`对象每个 MIME 类型可以恰好包含一个值，这意味着你可以同时存储文本和 URL 而不会覆盖其中任何一个。如果你没有在`ondrop`事件处理程序中检索数据，`dataTransfer`对象将被销毁，数据也将丢失。

当你从文本框中拖动文本时，浏览器会调用`setData()`并将拖拽的文本存储为`"text"`格式。同样，当拖动链接或图像时，会调用`setData()`并存储 URL。当数据放置在目标上时，使用`getData()`获取这些值是可行的。你也可以在`dragstart`事件期间手动调用`setData()`来存储以后可能想要检索的自定义数据。

视为文本的数据与视为 URL 的数据存在区别。当你指定将数据存储为文本时，它不会受到任何特殊处理。然而，当你指定将数据存储为 URL 时，它会被处理得像网页链接一样，这意味着如果你将其放置到另一个浏览器窗口中，浏览器将导航到该 URL。

5 版本及之前的 Firefox 没有正确地将`"url"`别名为`"text/uri-list"`或将`"text"`别名为`"text/plain"`。但是，它确实将`"Text"`（大写 T）别名为`"text/plain"`。为了确保从`dataTransfer`获取数据时具有最佳跨浏览器兼容性，你需要对 URL 检查两个值，并对纯文本使用`"Text"`：

![image](img/logo1.gif)

```
var dataTransfer = event.dataTransfer;

// 读取一个 URL

var url = dataTransfer.getData("url") ||dataTransfer.getData("text/uri-list");

// 读取文本

var text = dataTransfer.getData("Text");
```

`DataTransferExample01.htm`

先尝试简短的数据名称是重要的，因为 10 版本及之前的 Internet Explorer 不支持扩展名称，并且当数据名称未被识别时会抛出错误。

## dropEffect 和 effectAllowed

`dataTransfer`对象不仅可以用于往来传输数据，还可以用于确定被拖拽项目和放置目标之间可以执行什么类型的操作。你通过使用两个属性来实现：`dropEffect`和`effectAllowed`。

`dropEffect`属性用于告诉浏览器允许哪些类型的放置行为。该属性有以下可能的值：

- `"none"`：被拖拽的项目不能在此处放置。这是除文本框外所有内容的默认值。
- `"move"`：被拖拽的项目应该移动到放置目标。
- `"copy"`：被拖拽的项目应该复制到放置目标。
- `"link"`：表示放置目标将导航到被拖拽的项目（仅当它是 URL 时）。

这些值中的每一个都会在项目拖动到放置目标上方时显示不同的光标。然而，实际触发光标所指示的操作取决于你。换句话说，如果没有你的干预，没有任何东西会自动移动、复制或链接。你唯一“免费”获得的仅仅是光标的变化。为了使用`dropEffect`属性，你必须在放置目标的`dragenter`事件处理程序中设置它。

除非你也设置了`effectAllowed`，否则`dropEffect`属性是没用的。该属性指示被拖拽项目允许哪些`dropEffect`。可能的值如下：

- `"uninitialized"`：未为被拖拽项目设置任何操作。
- `"none"`：对被拖拽项目不允许任何操作。
- `"copy"`：仅允许`dropEffect "copy"`。
- `"link"`：仅允许`dropEffect "link"`。
- `"move"`：仅允许`dropEffect "move"`。
- `"copyLink"`：允许`dropEffect "copy"`和`"link"`。
- `"copyMove"`：允许`dropEffect "copy"`和`"move"`。
- `"linkMove"`：允许`dropEffect "link"`和`"move"`。
- `"all"`：允许所有的`dropEffect`值。

此属性必须在`dragstart`事件处理程序内部设置。

假设你想允许用户将文本从文本框移动到`<div>`。要实现这一点，你必须将`dropEffect`和`effectAllowed`都设置为`"move"`。文本不会自动移动，因为`<div>`上放置事件的默认行为是什么都不做。如果你重写了默认行为，文本会自动从文本框中移除。然后由你将其插入到`<div>`中以完成操作。如果你将`dropEffect`和`effectAllowed`改为`"copy"`，文本框中的文本将不会自动移除。

5 版本及之前的 Firefox 在`effectAllowed`上存在一个问题，当在代码中设置此值时，放置事件可能不会触发。

默认情况下，图像、链接和文本都是可拖拽的，这意味着不需要额外的代码即可允许用户开始拖拽它们。文本只有在被高亮后才是可拖拽的，而图像和链接可以在任何时间进行拖拽。

可以使其他元素也变为可拖拽。HTML5 在所有 HTML 元素上指定了`draggable`属性，用于指示该元素是否可以被拖拽。图像和链接的`draggable`被设置为`true`，而其他所有内容的默认值为`false`。可以通过设置此属性来允许其他元素变为可拖拽，或确保图像或链接不可被拖拽。例如：

```
<!--关闭此图像的拖拽功能 -->

<img src="smile.gif" draggable="false" alt="Smiley face">

<!--开启此元素的拖拽功能 -->

<div draggable="true">...</div>
```

`draggable`属性支持 Internet Explorer 10+、Firefox 4+、Safari 5+ 和 Chrome。Opera 从 11.5 版本开始不支持 HTML5 拖放。为了让 Firefox 启动拖拽，你还必须添加一个`ondragstart`事件处理器，在`dataTransfer`对象上设置某些信息。

![image](img/pen.gif)

Internet Explorer 9 及更早版本允许你在`mousedown`事件期间通过调用`dragDrop()`方法使任何元素变为可拖拽。Safari 4 及更早版本需要添加 CSS 样式`-khtml-user-drag: element`来使元素变为可拖拽。

## 附加成员

HTML5 规范在`dataTransfer`对象上指定了以下附加方法：

- `addElement(element)` — 将元素添加到拖拽操作中。这纯粹用于数据目的，不会影响拖拽操作的外观。截至本文编写，还没有浏览器实现此方法。
- `clearData(format)` — 清除存储的特定格式的数据。这已在 Internet Explorer、Firefox 3.5+、Chrome 和 Safari 4+ 中实现。
- `setDragImage(element, x, y)` — 允许你在拖拽发生时指定一个在光标下方显示的图像。该方法接受三个参数：一个要显示的 HTML 元素，以及图像上光标应该放置的`x`和`y`坐标。该 HTML 元素可以是图像（在这种情况下显示图像），也可以任何其他元素（在这种情况下显示该元素的渲染图）。Firefox 3.5+、Safari 4+ 和 Chrome 都支持此方法。
- `types` — 当前正在存储的数据类型列表。该集合像数组一样，并将数据类型以字符串（如`"text"`）的形式存储。Internet Explorer 10+、Firefox 3.5+ 和 Chrome 实现此属性。

## 媒体元素

随着嵌入式音频和视频在 Web 上爆炸式的流行，大多数内容生产者被迫使用 Flash 以获得最佳的跨浏览器兼容性。HTML5 引入了两个媒体相关的元素，能够在无需任何插件的情况下实现跨浏览音频和视频嵌入：`<audio>`和`<video>`。

这两个元素都允许 Web 开发人员轻松地将媒体文件嵌入页面中，并提供常用功能的 JavaScript 钩子，允许为媒体创建自定义控件。这些元素用法如下：

```
<!-- 嵌入视频 -->

<video src="conference.mpg" id="myVideo">视频播放器不可。</video>

<!-- 嵌入音频文件 -->

<audio src="song.mp3" id="myAudio">音频播放器不可。</audio>
```

这些元素每个至少需要一个`src`属性，指示要加载的媒体文件。你还可以指定`width`和`height`属性来指示视频播放器的预期尺寸，以及一个`poster`属性，它是一个在视频内容加载期间显示的图像 URI。如果存在`controls`属性，则表示浏览器应该显示一个 UI，允许使用户直接与媒体交互。起始标签和结束标签之间的任何内容都被视为在媒体播放器不可用时的备用内容。

你可以选择地指定多个不同的媒体源，因为并不是所有的浏览器都支持所有的媒体格式。为此，请从元素中省略`src`属性，而是包含一个或多个`<source>`元素，如下所示：

```
<!-- 嵌入视频 -->

<video id="myVideo">

  <source src="conference.webm" type="video/webm; codecs='vp8, vorbis'">

  <source src="conference.ogv" type="video/ogg; codecs='theora, vorbis'">

  <source src="conference.mpg">

  视频播放器不可。

</video>

<!-- 嵌入音频文件 -->

<audio id="myAudio">

  <source src="song.ogg" type="audio/ogg">

  <source src="song.mp3" type="audio/mpeg">

  音频播放器不可。

</audio>
```

讨论用于视频和音频的各种编码器超出了本书的范围，但只需说明浏览器支持不同范围的编码器，因此通常需要多个源文件。媒体元素支持 Internet Explorer 9+、Firefox 3.5+、Safari 4+、Opera 10.5+、Chrome、Safari for iOS 以及 WebKit for Android。

## 属性

`<video>`和`<audio>`元素提供了强大的 JavaScript 接口。这两个元素共享许多属性，可以通过评估它们来确定媒体的当前状态，如下所示。

| 属性名称 | 数据类型 | 描述 |
| --- | --- | --- |
| `autoplay` | Boolean | 获取或设置自动播放标记。 |
| `buffered` | TimeRanges | 指示已缓冲时间范围的对象。 |
| `bufferedBytes` | ByteRanges | 指示已下载字节范围的对象。 |
| `bufferingRate` | Integer | 从下载的每秒比特数。 |
| `bufferingThrottled` | Boolean | 指示缓冲是否被浏览器限制。 |
| `controls` | Boolean | 获取或设置控件属性，显示或隐藏浏览器的内置控件。 |
| `currentLoop` | Integer | 媒体播放的循环次数。 |
| `currentSrc` | String | 当前播放媒体的 URL。 |
| `currentTime` | Float | 已播放的秒数。 |
| `defaultPlaybackRate` | Float | 获取或设置默认播放速率。默认值为 1.0 秒。 |
| `duration` | Float | 媒体的总秒数。 |
| `ended` | Boolean | 指示媒体是否已播放完毕。 |
| `loop` | Boolean | 获取或设置媒体在完成后是否循环回到开始。 |
| `muted` | Boolean | 获取或设置媒体是否静音。 |
| `networkState` | Integer | 指示媒体的网络连接状态：0 空闲，1 加载，2 加载元数据，3 加载第一帧，4 已加载。 |
| `paused` | Boolean | 指示播放器是否暂停。 |
| `playbackRate` | Float | 获取或设置当前播放速率。这可能会受用户影响导致媒体播放变快或变慢，而`defaultPlaybackRate`在开发者更改它之前保持不变。 |
| `played` | TimeRanges | 直到目前已播放的时间范围。 |
| `readyState` | Integer | 指示媒体是否准备好播放。0 表示数据不可用，1 表示当前帧可以显示，2 表示媒体可以开始播放，3 表示媒体可以从头到尾播放。 |
| `seekable` | TimeRanges | 可用于查找的时间范围。 |
| `seeking` | Boolean | 指示播放器正在移动到媒体文件的新位置。 |
| `src` | String | 媒体文件源。这可以在任何时间重写。 |
| `start` | Float | 获取或设置从媒体文件中开始播放的位置（以秒为单位）。 |
| `totalBytes` | Integer | 资源的总字节数（如果已知）。 |
| `videoHeight` | Integer | 返回视频的高度（不一定等于元素的高度）。仅用于`<video>`。 |
| `videoWidth` | Integer | 返回视频宽度（不一定是元素的宽度）。仅用于`<video>`。 |
| `volume` | Float | 获取或设置当前音量，值为 0.0 到 1.0 之间的值。 |

这些属性中的许多也可以作为属性指定在`<audio>`或`<video>`元素上。

## 事件

除了许多属性外，这些媒体元素上还存在了许多可以触发的事件。这些事件监控所有由于媒体播放和用户与播放器交互而改变的不同属性。这些事件列在下表中。

| 事件名称 | 触发时机 |
| --- | --- |
| `abort` | 下载已中止。 |
| `canplay` | 播放可以开始；`readyState`为 2。 |
| `canplaythrough` | 播放可以进行且不应中断；`readyState`为 3。 |
| `canshowcurrentframe` | 当前帧已下载；`readyState`为 1。 |
| `dataunavailable` | 因为没有数据，无法播放；`readyState`为 0。 |
| `durationchange` | 持续时间属性值已更改。 |
| `emptied` | 网络连接已关闭。 |
| `empty` | 发生错误阻止了媒体下载。 |
| `ended` | 媒体已完全播放并停止。 |
| `error` | 下载过程中发生网络错误。 |
| `load` | 所有媒体均已加载。此事件被认为已弃；请用`canplaythrough`代替。 |
| `loadeddata` | 媒体的第一帧已加载。 |
| `loadedmetadata` | 媒体的元数据已加载。 |
| `loadstart` | 下载开始。 |
| `pause` | 播放已暂停。 |
| `play` | 请求开始播放媒体。 |
| `playing` | 媒体已实际开始播放。 |
| `progress` | 正在下载中。 |
| `ratechange` | 媒体播放速度已改变。 |
| `seeked` | 调整已结束。 |
| `seeking` | 播放正在移动到新位置。 |
| `stalled` | 浏览器正尝试下载，但没有接收到任何数据。 |
| `timeupdate` | `currentTime`以不规则或意外的方式更新。 |
| `volumechange` | `volume`属性值或`muted`属性值已更改。 |
| `waiting` | 暂停播放以下载更多数据。 |

这些事件的设计尽可能具体，以便 Web 开发人员仅用 HTML 和 JavaScript 就可以自定义音频/视频播放器（而不是创建一个新的 Flash 电影）。

## 自定义媒体播放器

你可以使用`<audio>`和`<video>`上可用的`play()`和`pause()`方法手动控制媒体文件的播放。将属性、事件和这些方法结合起来可以轻松创建一个自定义媒体播放器，如下所示：

![image](img/logo1.gif)

```html
<div class="mediaplayer">

    <div class="video">

        <video id="player" src="movie.mov" poster="mymovie.jpg" 

               width="300" height="200">

            视频播放器不可用。

        </video>

    </div>

    <div class="controls">

        <input type="button" value="Play" id="video-btn">

        <span id="curtime">0</span>/<span id="duration">0</span>

    </div>

</div>
```



`VideoPlayerExample01.htm`

然后可以使用 JavaScript 创建一个简单的视频播放器来让这个基础 HTML 动起来，如下：

```javascript
// 获取元素的引用
var player = document.getElementById("player"),
    btn = document.getElementById("video-btn"),
    curtime = document.getElementById("curtime"),
    duration = document.getElementById("duration");

// 更新持续时间
duration.innerHTML = player.duration;

// 为按钮附加事件处理器
EventUtil.addHandler(btn, "click", function(event){
    if (player.paused){
        player.play();
        btn.value = "Pause";
    } else {
        player.pause();
        btn.value = "Play";
    }
});

// 定期更新当前时间
setInterval(function(){
    curtime.innerHTML = player.currentTime;
}, 250);
```

`VideoPlayerExample01.htm`

这里的 JavaScript 代码简单地为按钮附加了一个事件处理器，根据其当前状态暂停或播放视频。然后，为 `<video>` 元素的加载事件设置了一个事件处理器，以便显示持续时间。最后，设置了一个循环的定时器来更新当前时间的显示。你可以通过监听更多事件并利用更多属性来扩展此自定义视频播放器的功能。相同的代码也可以用于 `<audio>` 元素创建自定义音频播放器。

## 解码器支持检测

如之前所述，并不是所有的浏览器都支持 `<video>` 和 `<audio>` 的所有解码器，这通常意味着你必须提供多个媒体源。还有一个 JavaScript API 可用于判断给定的格式和解码器是否被浏览器支持。两个媒体元素都有一个名为 `canPlayType()` 的方法，它接受一个格式/解码器字符串并返回 `"probably"`、`"maybe"` 或 `""`（空字符串）的字符串值。空字符串表示不支持。

```javascript
// 返回 "probably", "maybe" 或 ""
```

例如：

```javascript
if (audio.canPlayType("audio/mpeg")){
    // 执行操作
}
```

## 媒体元素属性

| 属性 | 值类型 | 说明 |
| --- | --- | --- |
| `videoWidth` | `Integer` | 返回视频宽度（不一定是元素的宽度）。仅用于 `<video>`。 |
| `volume` | `Float` | 获取或设置当前音量，值为 0.0 到 1.0 之间的值。 |

这些属性中的许多也可以作为属性指定在 `<audio>` 或 `<video>` 元素上。

## 事件

除了许多属性外，这些媒体元素上还存在了许多可以触发的事件。这些事件监控所有由于媒体播放和用户与播放器交互而改变的不同属性。这些事件列在下表中。

| 事件名称 | 触发时机 |
| --- | --- |
| `abort` | 下载已中止。 |
| `canplay` | 播放可以开始；`readyState` 为 2。 |
| `canplaythrough` | 播放可以进行且不应中断；`readyState` 为 3。 |
| `canshowcurrentframe` | 当前帧已下载；`readyState` 为 1。 |
| `dataunavailable` | 因为没有数据，无法播放；`readyState` 为 0。 |
| `durationchange` | 持续时间属性值已更改。 |
| `emptied` | 网络连接已关闭。 |
| `empty` | 发生错误阻止了媒体下载。 |
| `ended` | 媒体已完全播放并停止。 |
| `error` | 下载过程中发生网络错误。 |
| `load` | 所有媒体均已加载。此事件被认为已弃；请用 `canplaythrough` 代替。 |
| `loadeddata` | 媒体的第一帧已加载。 |
| `loadedmetadata` | 媒体的元数据已加载。 |
| `loadstart` | 下载开始。 |
| `pause` | 播放已暂停。 |
| `play` | 请求开始播放媒体。 |
| `playing` | 媒体已实际开始播放。 |
| `progress` | 正在下载中。 |
| `ratechange` | 媒体播放速度已改变。 |
| `seeked` | 调整已结束。 |
| `seeking` | 播放正在移动到新位置。 |
| `stalled` | 浏览器正尝试下载，但没有接收到任何数据。 |
| `timeupdate` | `currentTime` 以不规则或意外的方式更新。 |
| `volumechange` | `volume` 属性值或 `muted` 属性值已更改。 |
| `waiting` | 暂停播放以下载更多数据。 |

这些事件的设计尽可能具体，以便 Web 开发人员仅用 HTML 和 JavaScript 就可以自定义音频/视频播放器（而不是创建一个新的 Flash 电影）。

## 自定义媒体播放器

你可以使用 `<audio>` 和 `<video>` 上可用的 `play()` 和 `pause()` 方法手动控制媒体文件的播放。将属性、事件和这些方法结合起来可以轻松创建一个自定义媒体播放器，如下所示：

![image](img/logo1.gif)

```html
<div class="mediaplayer">
    <div class="video">
        <video id="player" src="movie.mov" poster="mymovie.jpg" 
               width="300" height="200">
            视频播放器不可用。
        </video>
    </div>
    <div class="controls">
        <input type="button" value="Play" id="video-btn">
        <span id="curtime">0</span>/<span id="duration">0</span>
    </div>
</div>
```

`VideoPlayerExample01.htm`

然后可以使用 JavaScript 创建一个简单的视频播放器来让这个基础 HTML 动起来，如下：

```javascript
// 获取元素的引用
var player = document.getElementById("player"),
    btn = document.getElementById("video-btn"),
    curtime = document.getElementById("curtime"),
    duration = document.getElementById("duration");

// 更新持续时间
duration.innerHTML = player.duration;

// 为按钮附加事件处理器
EventUtil.addHandler(btn, "click", function(event){
    if (player.paused){
        player.play();
        btn.value = "Pause";
    } else {
        player.pause();
        btn.value = "Play";
    }
});

// 定期更新当前时间
setInterval(function(){
    curtime.innerHTML = player.currentTime;
}, 250);
```

`VideoPlayerExample01.htm`

这里的 JavaScript 代码简单地为按钮附加了一个事件处理器，根据其当前状态暂停或播放视频。然后，为 `<video>` 元素的加载事件设置了一个事件处理器，以便显示持续时间。最后，设置了一个循环的定时器来更新当前时间的显示。你可以通过监听更多事件并利用更多属性来扩展此自定义视频播放器的功能。相同的代码也可以用于 `<audio>` 元素创建自定义音频播放器。

## 解码器支持检测

如之前所述，并不是所有的浏览器都支持 `<video>` 和 `<audio>` 的所有解码器，这通常意味着你必须提供多个媒体源。还有一个 JavaScript API 可用于判断给定的格式和解码器是否被浏览器支持。两个媒体元素都有一个名为 `canPlayType()` 的方法，它接受一个格式/解码器字符串并返回 `"probably"`、`"maybe"` 或 `""`（空字符串）的字符串值。空字符串表示不支持。

```javascript
// 返回 "probably", "maybe" 或 ""
```

例如：

```javascript
if (audio.canPlayType("audio/mpeg")){
    // 执行操作
}
```

## Audio 类型

`<audio>` 元素还有一个名为原生 JavaScript 构造函数 `Audio`，允许在任何时间播放音频。`Audio` 类型与 `Image` 类似，它等同于 DOM 元素，但不需要插入文档即可工作。只需创建一个新实例并传入音频源文件：

```javascript
var audio = new Audio("sound.mp3");
EventUtil.addHandler(audio, "canplaythrough", function(event){
    audio.play();
});
```

创建 `Audio` 新实例会开始下载指定文件的过程。一旦就绪，你就可以调用 `play()` 开始播放。

在 iOS 上调用 `play()` 方法会弹出对话框请求用户许可播放声音。为了连续播放声音，你必须在 `onfinish` 事件处理器中立即调用 `play()`。

## 历史状态管理

现代 Web 应用编程中最困难方面之一是历史管理。每个操作都将用户带到完全新页面的时代已经过去了，这意味着“后退”和“前进”按钮已不再是用户熟悉的“切换到不同状态”的方式。解决这一问题的第一步是 `hashchange` 事件（在第 13 章中讨论）。HTML5 更新了 `history` 对象以提供简单的状态管理。

`hashchange` 事件仅仅是在 URL hash 发生变化时通知你并让你采取相应的行动，而状态管理 API 实际上允许你在不加载新页的情况下更改浏览器 URL。要实现这一点，使用 `history.pushState()` 方法。该方法接受三个参数：一个数据对象、新状态的标题以及可选的相对 URL。例如：

```
history.pushState({name:"Nicholas"}, "Nicholas' page", "nicholas.html");
```

一旦 `pushState()` 执行，状态信息就会被推送到历史栈中，浏览器的地址栏会随之改变以反映新的相对 URL。尽管发生了这种变化，浏览器并没有向服务器发送请求，即使查询 `location.href` 返回的内容与地址栏中的内容完全相同。第二个参数目前没有任何实现在使用，因此将其留空字符串或提供一个简短标题都是安全的。第一个参数应该包含在必要时正确初始化此页面状态所需的所有。

由于 `pushState()` 创建了新的历史记录，你会发现“后退”按钮被激活。当按下后退按钮时，window 对象上会触发 `popstate` 事件。`popstate` 的事件对象有一个名为 `state` 的属性，它包含了作为第一个参数传递给 `pushState()` 的对象：

```
EventUtil.addHandler(window, "popstate", function(event){
    var state = event.state;
    if (state){   //在首次加载页面时 state 为 null
        processState(state);
    }
});
```

使用此状态后，你必须将页面重置为 `state` 对象中数据所代表的状态（因为浏览器不会为你自动完成）。请记住，当页面首次加载时没有状态，因此一直点击后退按钮直到回到原始页面状态将导致 `event.state` 为 `null`。

你可以通过 `replaceState()` 并传递与 `pushState()` 相同的两个参数来更新当前的状态信息。这样做不会在历史记录中创建新条目，而只是覆盖当前状态：



`history.replaceState({name:"Greg"}, "Greg's page");`

HTML5 历史状态管理在 Firefox 4+、Safari 5+、Opera 11.5+ 和 Chrome 中支持。在 Safari 和 Chrome 中，传递给 `pushState()` 或 `replaceState()` 的状态对象不能包含任何 DOM 元素。Opera 也支持 `history.state` 属性，它返回当前状态的状态对象。

![image](img/pen.gif)

使用 HTML5 历史状态管理时，请确保你使用 `pushState()` 创建的任何“伪”URL 都有 Web 服务器上真实的物理 URL 支撑。否则，点击刷新按钮将导致 404 错误。

## 总结

HTML5 除了定义了新的标记规则外，还定义了若干 JavaScript API。这些 API 旨在实现更好的 Web 界面，能够媲桌面应用程序的功能。本章涵盖的 API 如下：

- `跨文档消息传递`提供了在不同源文档之间发送消息的能力，同时保持同源策略的安全性。
- `原生拖放`允许你轻松指示某个元素是可拖拽的，并像操作系统一样对释放操作做出响应。你可以创建自定义的可拖拽元素和放置目标。
- 新的媒体元素 `<audio>` 和 `<video>` 拥有它们与音频和视频交互的独立 API。并非所有浏览器都支持所有媒体格式，因此请利用 `canPlayType()` 方法来正确检测浏览器支持情况。
- `历史状态管理`允许你在不卸载当前页的情况下更改浏览器历史栈。这允许使用后退和前进按钮的用户在完全由 JavaScript 处理的页面状态之间移动。

# 第 17 章：错误处理与调试

## 本章内容概览

- 理解浏览器错误报告
- 处理错误
- 调试 JavaScript 代码

JavaScript 传统上被认为是最难调试的编程语言之一，因为它的动态特性以及多年来缺乏适当的开发工具。错误通常会导致令人困惑的浏览器信息，例如“object expected”，这些信息几乎或完全没有提供上下文信息。ECMAScript 第三版旨在改善这种局面，引入了 `try-catch` 和 `throw` 语句以及各种错误类型，以帮助开发者在错误发生时进行处理。几年后，针对浏览器的 JavaScript 调试器和调试工具开始出现。到 2008 年，大多数网络浏览器已支持某些 JavaScript 调试功能。

在拥有适当的语言支持和开发工具后，Web 开发者现在能够实现正确的错误处理流程并找出问题原因。

## 浏览器错误报告

所有主要的网络浏览器——Internet Explorer、Firefox、Safari、Chrome 和 Opera——都有某种方式向用户报告 JavaScript 错误。默认情况下，所有浏览器都会隐藏这些信息，因为这对开发者以外的人几乎没有用。在开发基于浏览器的 JavaScript 解决方案时，请确保启用 JavaScript 错误报告，以便在发生错误时收到通知。

### Internet Explorer

Internet Explorer 是唯一默认在浏览器界面（chrome）中显示 JavaScript 错误指示器的浏览器。当发生 JavaScript 错误时，浏览器左下角会出现一个小黄色图标，旁边带有“Error on page”字样。如果不预期，这个图标很容易被忽略。双击图标时会显示一个对话框，其中包含错误消息并允许查看其他相关信息，如行号、字符数、错误代码和文件名（始终是你正在查看的 URL）（参见图 17-1）。

FIGURE 17-1

![image](img/f608-01.jpg)

这种默认行为对于普通用户是可以的，但对于 Web 开发是不够的。可以更改设置为每次发生错误都显示错误对话框。要进行此更改，点击“工具”菜单，然后选择“Internet ”。对话框出现后，点击“高级”选项卡并勾选“对每个脚本错误显示通知”旁边的框（参见图 17-2）。点击“确定”保存设置。

FIGURE 17-2

![image](img/f608-02.jpg)

更新此设置后，通常双击黄色图标显示的对话框将在每次发生错误时默认显示。

如果启用了脚本调试（默认禁用），并且你将浏览器设置为始终显示错误通知，那么你可能会看到另一个对话框，询问你是否想要调试该错误（参见图 17-3）。

FIGURE 17-3

![image](img/f608-03.jpg)

要启用脚本调试，你必须先安装一个与 Internet Explorer 兼容的脚本调试器。（版本 8 和 9 自带了调试器。）调试器将在本章稍后部分讨论。

在 Internet Explorer 7 及更早版本中，如果错误是由外部文件中的脚本引起的，错误消息中的行号通常会偏移一位。由内联脚本引起的错误行号是准确的。Internet Explorer 8 及更高版本修复了此问题，使得所有行号都是准确的。

### Firefox

默认情况下，当发生 JavaScript 错误时，Firefox 对用户界面不做任何更改。相反，它会将错误静默地记录到错误控制台中。点击 `Tools` 菜单然后选择 `Error Console` 来显示错误控制台（参见图 17-4）。注意，错误控制台还包含关于 JavaScript、CSS 和 HTML 的警告和信息，因此过滤结果可能会很有用。

图 17-4

![image](img/f609-01.jpg)

当发生 JavaScript 错误时，它会被作为一个错误记录下来，包含错误消息、发生错误的 URL 以及行号。点击文件名会打开导致错误的脚本的只读视图，并高亮显示出错行。

Firebug 疑是 Web 开发人员最流行的浏览器插件，它增强了 Firefox 默认的 JavaScript 错误行为。Firebug 可于 [www.getfirebug.com](http://www.getfirebug.com)，她在 Firefox 状态栏右下方添加了一个显示 JavaScript 信息的区域。默认情况下，该位置显示一个绿色勾选图标。当发生 JavaScript 错误时，图标会变为红色 X 并显示错误数量。点击红色 X 会打开 Firebug 控制台，其中显示错误消息、导致错误的代码行（脱离上下文）、发生错误的 URL 以及行号（参见图 17-5）。

图 17-5

![image](img/f610-01.jpg)

在 Firebug 中点击导致错误的行时，它会打开一个新的 Firebug 视图，在整个脚本文件的上下文中高亮显示该行。

![image](img/pen.gif)

Firebug 除了显示错误消息外，还有许多用途。它是 Firefox 的全功能调试环境，提供了调试 JavaScript、CSS、DOM 和网络信息的方法。

### Safari

Windows 和 Mac OS 上的 Safari 默认隐藏所有 JavaScript 错误信息。为了访问这些信息，必须启用“开发”菜单。为此，选择 `Edit ⇒ Preferences` 然后点击 `Advanced` 选项卡。有一个标题为“Show develop menu in menu bar”的复选框应当勾选。一旦启用设置，Safari 菜单栏中会出现一个名为 `Develop` 的菜单（参见图 17-6）。

图 17-6

![image](img/f611-01.jpg)

`Develop` 菜单为调试以及其他处理当前加载页面提供了多个选项。你可以点击 `Show Error Console` 来显示 JavaScript 及其他错误的列表。控制台显示错误消息、错误的 URL 以及错误的行号（参见图 17-7）。

图 17-7

![image](img/f611-02.jpg)

当你点击错误消息时，会被带到导致错误的源代码。除了输出到控制台外，JavaScript 错误不会导致 Safari 窗口发生任何变化。

### Opera

Opera 默认也隐藏 JavaScript 错误。所有错误都记录在错误控制台中，可以通过选择 `Page` 菜单，然后 `Page ⇒ Developer Tools ⇒ Error Console` 来显示。与 Firefox 类似，Opera 错误控制台不仅包含 JavaScript 错误信息，还包含 HTML、CSS、XML、XSLT 以及其他来源的错误或警告。你可以使用左下角的下拉框按你想查看的消息类型进行过滤（参见图 17-8）。

图 17-8

![image](img/f612-01.jpg)

错误消息出现时带有导致错误的 URL 信息以及发生错误的线程。在某些情况下，还会提供堆栈跟踪。除了错误控制台中显示的详细信息外，没有办法获取有关错误的额外数据。

可以设置在每次发生 JavaScript 错误时弹出错误控制台。要这样做，进入 `Settings` 菜单并点击 `Preferences`。点击 `Advanced` 选项卡，然后从左菜单选择 `Content`。点击 `JavaScript Options` 按钮弹出 `JavaScript Options` 对话框（见图 17-9）。

图 17-9

![image](img/f612-02.jpg)

确保“Open console on error”旁边的复选框已勾选，然后点击 OK。现在每当有 JavaScript 错误时，错误控制台都会弹出。也可以按网站进行，选择 `Tools ⇒ Quick Preferences ⇒ Edit Site Preferences`，选择 `Scripting` 选项卡并勾选“Open console on error”复选框。

### Chrome

与 Safari 和 Opera 一样，Chrome 默认隐藏 JavaScript 错误。

```javascript
try {
    window.someNonexistentFunction();
} catch (error) {
    alert("An error happened!");
}
```

如果在语句的 `try` 部分在任何一点发生错误，代码执行将立即退出并在 `catch` 部分恢复执行。语句的 `catch` 部分将接收一个包含所发生错误信息的对象。与其他语言不同，即使你不打算使用该错误对象，也必须为错误对象定义一个名称。此对象上可用的具体信息随浏览器而异，但至少包含一个持有错误信息的 `message` 属性。ECMA-262 还规定了用于定义错误类型的 `name` 属性；该属性在所有当前用支持的浏览器中都是可用的。因此，在必要时你可以显示实际的浏览器消息，如下例所示：

![image](img/logo1.gif)

```javascript
try {
    window.someNonexistentFunction();
} catch (error) {
    alert(error.message);
}
```

#### TryCatchExample01.htm

此示例在向用户显示错误消息时使用了 `message` 属性。`message` 属性是唯一保证在 Internet Explorer、Firefox、Safari、Chrome 和 Opera 中存在的属性，尽管每个浏览器都添加了其他信息。Internet Explorer 添加了一个 `description` 属性，其值始终等于 `message`，还添加了一个提供内部错误代码的 `number` 属性。Firefox 添加了 `fileName`、`lineNumber` 和 `stack`（包含堆栈跟踪）。Safari 添加了 `line`（用于行号）、`sourceId`（内部错误代码）和 `sourceURL`。再次，为了实现跨浏览器兼容性，最好仅依赖 `message` 属性。

#### finally 子句

`try-catch` 语句中可选的 `finally` 子句无论发生什么都会执行其代码。如果 `try` 部分的代码完全运行，则执行 `finally` 子句；如果发生错误并执行了 `catch` 部分，`finally` 部分仍然会执行。在语句的 `try` 或 `catch` 部分中，没有任何操作可以防止 `finally` 中代码的执行，这包括使用 `return` 语句。请考虑以下函数：

![image](img/logo1.gif)

```javascript
function testFinally() {
    try {
        return 2;
    } catch (error) {
        return 1;
    } finally {
        return 0;
    }
}
```

#### TryCatchExample02.htm

此函数仅在 `try-catch` 语句的每个部分都放置了一个 `return` 语句。看起来函数似乎应该返回 `2`，因为它在 `try` 部分且不会引起错误。然而，由于 `finally` 子句的存在，导致该返回被忽略；无论如何调用，该函数都会返回 `0`。如果删除了 `finally` 子句，函数将返回 `2`。

如果提供了 `finally`，则 `catch` 变为可选（两者中二选一即可）。Internet Explorer 7 及更早版本有一个 bug，除非同样有 `catch`，否则 `finally` 中的代码永远不会执行。如果你仍在处理较早版本的 Internet Explorer，那么解决方法是即使它是空的，也提供一个 `catch` 子句。这在版本 8 中已经修复了。

![image](img/pen.gif)

非常重要的一点是，如果代码中包含了 `finally` 子句，那么 `try` 或 `catch` 部分中的任何 `return` 语句都被忽略。在使用 `finally` 时，务必双检代码的预期行为。

#### 错误类型

在代码执行过程中可能会发生几种不同的错误。每种错误类型都有在发生错误时抛出的相应对象类型。ECMA-262 定义了以下七种错误类型：

- `Error`
- `EvalError`
- `RangeError`
- `ReferenceError`
- `SyntaxError`
- `TypeError`
- `URIError`

`Error` 类型是所有其他错误类型继承的基类型。由于由于，所有错误类型共享相同的属性（错误对象上的唯一方法是默认对象方法）。浏览器很少抛出 `Error` 类型的错误；它主要提供给开发者抛出自定义错误。

当在使用 `eval()` 函数时发生异常会抛出 `EvalError`。ECMA-262 规定，“如果 `eval` 属性的值用于直接调用以外的任何方式（即不是通过显式使用其名称作为 `Identifier`，即 `CallExpression` 中的 `MemberExpression`），或者对 `eval` 属性进行赋值，将抛出此错误。”这基本上意味着将 `eval()` 用于函数调用以外的任何形式，例如：

```javascript
new eval();     //抛出 EvalError

eval = foo;     //抛出 EvalError
```

在实践中，浏览器并不总是会在应该的时候抛出 `EvalError`。例如，Firefox 4+ 和 Internet Explorer 8 在第一情况下抛出 `TypeError`，但第二种情况成功且没有错误。由于这种情况以及这些模式不太可能使用，你极可能遇到这种错误类型。

当数字超出其范围边界时会发生 `RangeError`。例如，当尝试定义一个不支持数量项目的数组时，可能会发生此错误，例如 `-20` 或 `Number.MAX_VALUE`，如下：

```javascript
var items1 = new Array(-20);                //抛出 RangeError

var items2 = new Array(Number.MAX_VALUE);   //抛出 RangeError 
```

范围错误在 JavaScript 中发生得很少。

`ReferenceError` 类型在预期对象时使用（这正是著名的“预期对象”浏览器错误的原因）。这种类型的错误通常发生在访问不存在的变量时，如下例：

```javascript
var obj = x;    //当 x 不存在时抛出 ReferenceError
```

`SyntaxError` 对象通常发生在传递给 `eval()` 的 JavaScript 字符串存在语法错误时，如下例：

```javascript
eval("a ++ b");     //抛出 SyntaxError
```

在使用 `eval()` 之外，`SyntaxError` 类型很少使用，因为 JavaScript 代码中的语法错误会停止执行。

`TypeError` 类型在 JavaScript 中最常用，当变量类型异常或尝试访问不存在的方法时会发生。这可能由于许多原因引起，通常当对错误的类型使用特定类型的操作时。这里是一些示例：

```javascript
var o = new 10;                  //抛出 TypeError

alert("name" in true);           //抛出 TypeError

Function.prototype.toString.call("name");   //抛出 TypeError 
```

类型错误最经常发生在未验证类型就使用了函数参数。

最后一种错误类型是 `URIError`，它仅在使用格式错误的 URI 使用 `encodeURI()` 或 `decodeURI()` 时。这种错误可能是 JavaScript 中最少观察到的，因为这些函数非常健壮。

不同的错误类型可以提供更多关于异常的信息，允许适当的错误处理。你可以通过 `instanceof` 运算符来确定 `try-catch` 语句中 `catch` 部分抛出的错误类型，如下所示：

```javascript
try {
    someFunction();
} catch (error) {
    if (error instanceof TypeError) {
```



//处理类型错误

} else if (error instanceof ReferenceError){

    //处理引用错误

} else {

    //处理所有其他错误类型

}

```

检查错误类型是跨浏览器确定适当行动方案的最简单方法，因为`message`属性包含的错误消息随浏览器而异。

当`try-catch`语句内部发生错误时，浏览器会认为该错误已被处理，因此它不会使用本章之前讨论的机制报告该错误。这对于那些不具备技术背景且无法理解错误何时发生的用户的 Web 应用程序来说是理想的。`try-catch`语句允许你针对特定的错误类型实现自己的错误处理机制。

`try-catch`语句最好的用法是用于可能发生你无法控制的错误的地方。例如，如果你正在使用某个大型 JavaScript 库内部的函数，该函数可能会故意或无意地抛出错误。由于你无法修改库的代码，将该调用封装在`try-catch`语句中是恰当的，以防发生错误并随后对错误进行恰当的处理。

如果你明确知道你的代码会发生错误，那么使用`try-catch`语句是不恰当的。例如，如果一个函数在传入字符串而不是数字时会失败，你应该检查参数的数据类型并采取相应的措施；在这种情况下，没有需要使用`try-catch`语句。

## 抛出错误

`try-catch`语句的伴侣是`throw`操作符，它可以在任何时间抛出自定义错误。`throw`操作符必须配合一个值使用，但对值的类型没有限制。以下所有行都是合法的：

```javascript
throw 12345;
throw "Hello world!";
throw true;
throw { name: "JavaScript"};
```

当使用`throw`操作符时，代码执行会立即停止，只有当`try-catch`语句捕获了抛出的值时，执行才会继续。

通过使用内置错误类型之一可以更准确地模拟浏览器错误。每个错误类型的构造函数都接受一个参数，即准确的错误消息。以下是一个示例：

```javascript
throw new Error("Something bad happened.");
```

这段代码抛出了一个带有自定义错误消息的通用错误。浏览器处理该错误的方式就像是由浏览器本身生成的一样，这意味着它将以通常的方式报告该错误，并显示你的自定义错误消息。你可以使用其他错误类型实现相同的结果，如示例所示：

```javascript
throw new SyntaxError("I don't like your syntax.");
throw new TypeError("What type of variable do you take me for?");
throw new RangeError("Sorry, you just don't have the range.");
throw new EvalError("That doesn't evaluate.");
throw new URIError("Uri, is that you?");
throw new ReferenceError("You didn't cite your references properly.");
```

最常用的自定义错误消息错误类型是`Error`、`RangeError`、`ReferenceError`和`TypeError`。

你还可以通过原型链（第 6 章讨论）继承`Error`来创建自定义错误类型。你应该在你的错误类型上同时提供`name`属性和`message`属性。以下是一个示例：

![image](img/logo1.gif)

```javascript
function CustomError(message){
    this.name = "CustomError";
    this.message = message;
}
CustomError.prototype = new Error();
throw new CustomError("My message");
```

ThrowingErrorsExample01.htm

继承自`Error`的自定义错误类型被浏览器视为任何其他错误。当你需要捕获自己抛出的错误并需要将其与浏览器生成的错误区分开来，创建自定义错误类型很有帮助。

![image](img/pen.gif)

Internet Explorer 仅在抛出`Error`对象时才显示自定义错误消息。对于所有其他类型，它仅显示“exception thrown and not caught”（抛出异常但未捕获）。

## 何时抛出错误

抛出自定义错误是提供关于函数为何失败的更多信息的极佳方法。当存在特定的已知错误条件导致函数无法正常执行时，应该抛出错误。也就是说，在特定条件下，浏览器在执行此函数时将抛出错误。例如，如果参数不是数组，以下函数将失败：

![image](img/logo1.gif)

```javascript
function process(values){
    values.sort();
    for (var i=0, len=values.length; i < len; i++){
        if (values[i] > 100){
            return values[i];
        }
    }
    return -1;
}
```

ThrowingErrorsExample02.htm

如果使用字符串作为参数运行此函数，则`sort()`调用将失败。每个浏览器都会给出一个不同的（尽管有些晦涩）的错误消息，如下：

- Internet Explorer — Property or method doesn’t exist（属性或方法不存在）。
- Firefox — `values.sort()` is not a function（`values.sort()` 不是一个函数）。
- Safari — Value undefined (result of expression values.sort) is not an object（值 undefined（表达式 values.sort 的结果）不是对象）。
- Chrome — Object name has no method 'sort'（对象名没有方法 'sort'）。
- Opera — Type mismatch (usually a non-object value used where an object is required）（类型不匹配（通常在需要对象的地方使用了非对象值））。

尽管 Firefox、Chrome 和 Safari 至少指示了导致错误的代码部分，但没有任何一个错误消息在说明发生了什么或如何修复它方面特别清晰。在处理单个函数时（如前面的示例所示），通过这些错误消息进行调试足够容易。然而，当你正在开发一个具有数千行 JavaScript 代码的复杂 Web 应用程序时，寻找错误源将变得困难得多。这时，带有适当信息的自定义错误将对代码的可维护性产生巨大贡献。考虑以下示例：

![image](img/logo1.gif)

```javascript
function process(values){
    if (!(values instanceof Array)){
        throw new Error("process(): Argument must be an array.");
    }
    values.sort();
    for (var i=0, len=values.length; i < len; i++){
        if (values[i] > 100){
            return values[i];
        }
    }
    return -1;
}
```

ThrowingErrorsExample02.htm

在这个重写的版本中，如果`values`参数不是数组，则会抛出一个错误。错误消息提供了函数名称以及错误发生原因的清晰描述。如果此错误发生在复杂的 Web 应用程序中，你将更清楚地知道问题所在。

任何未被`try-catch`处理的错误都会导致在`window`对象上触发错误事件。该事件是浏览器最早支持的事件之一，为了向后兼容，其格式在 Internet Explorer、Firefox 和 Chrome 中一直保持不变。（Opera 或 Safari 不支持错误事件）。在任何浏览器中，`onerror`事件处理程序都不会创建事件对象，相反，它接收三个参数：错误消息、发生错误的`URL`以及错误所在的行号（line number）。在大多数情况下，只有错误消息是相关的，因为`URL`与文档的位置相同，且行号可能是针对内联 JavaScript 或外部文件中的代码。`onerror`事件处理程序需要使用此处所示的 DOM Level 0 技术进行赋值，因为它不符合 DOM Level 2 事件的标准格式：

```javascript
window.onerror = function(message, url, line){
    alert(message);
};
```

当发生任何错误时（无论是浏览器生成的还是非浏览器生成的），错误事件就会触发，并执行该事件处理程序。随后，浏览器的默认行为将接管，并像往常一样显示错误消息。你可以通过返回`false`来阻止浏览器的默认错误报告，如下所示：

![image](img/logo1.gif)

```javascript
window.onerror = function(message, url, line){
    alert(message);
    return false;
};
```

OnErrorExample01.htm

通过返回`false`，该函数实际上变成了整个文档的`try-catch`语句，捕获所有未处理的运行时错误。该事件处理程序是防止浏览器报告错误的最后一道防线，理想情况下，它永远不应该被使用。正确使用`try-catch`语句意味着没有错误到达浏览器层，因此不应触发错误事件。

![image](img/pen.gif)

浏览器使用此事件处理错误的方式存在显著差异。当错误事件在 Internet Explorer 中发生时，正常的代码执行会继续；所有变量和数据都会保留，并可以在`onerror`事件处理程序内部访问。然而，在 Firefox 中，正常的代码执行会结束，错误发生前存在的所有变量和数据都会被销毁，这使得难以真正评估错误。

图片也支持错误事件。每当图片`src`属性中的`URL`未返回识别的图像格式时，错误事件就会触发。该事件遵循 DOM 格式，通过返回一个以图片为目标的事件对象来实现。这是一个示例：

![image](img/logo1.gif)

```javascript
var image = new Image();
EventUtil.addHandler(image, "load", function(event){
    alert("Image loaded!");
});
EventUtil.addHandler(image, "error", function(event){
    alert("Image not loaded!");
});
image.src = "smilex.gif";  //不存在该文件
```

OnErrorExample02.htm

在此示例中，当图片加载失败时会显示一个警告框。需要理解的是，一旦错误事件触发，图片的下载过程已经结束，且不会恢复。

# 错误处理策略

传统上，Web 应用程序的错误处理策略局限于服务器。对于错误和错误处理通常会投入大量的思考，包括日志记录和监控系统。此类工具的作用是分析错误模式，希望追踪根源并理解错误影响了多少用户。

为 Web 应用程序的 JavaScript 层拥有一错误处理策略同样重要。由于任何 JavaScript 错误都可能导致网页无法使用，因此了解错误在何时以及为何发生至关重要。大多数 Web 应用程序的用户并非技术人员，当某些运行不符合预期时，他们很容易感到困惑。他们可能会尝试重新加载页面来解决问题，或者直接停止尝试。作为开发者，你应该深入了解代码可能在何时以及如何失败，并有一套系统来跟踪此类问题。

## 识别可能发生错误的地方

错误处理最重要的部分是首先识别代码中可能发生错误的地方。由于 JavaScript 是弱类型且函数参数未经过验证，因此很多错误只有在代码执行时才会变得明显。通常，有三类错误需要关注：

*   类型转换错误
*   数据类型错误
*   通信错误

这些错误中的每一个在使用特定模式或未进行充分的值检查时都会发生。

## 类型转换错误

类型转换错误的发生是由于使用了会自动更改值数据类型的运算符或其他语言结构（language construct）导致的。最常见的两种类型转换错误是由于使用了相等 (`==`) 或不等于 (`!=`) 运算符，并且在`if`、`for`和`while`等流程控制语句中使用非布尔值导致的。

在第 3 章中讨论的相等和不等于运算符在执行比较之前会自动转换不同类型的值。由于在非动态语言中，相同的符号通常执行直接比较，开发者经常在 JavaScript 中误用这些运算符相同的方式。在大多数情况下，最好使用全相等 (`===`) 和全不相等 (`!==`) 运算符来避免类型转换。这是一个示例：

```javascript
alert(5 == "5");           //true
alert(5 === "5");          //false
alert(1 == true);          //true
alert(1 === true);         //false
```

在这段代码中，数字`5`和字符串`"5"`分别使用相等运算符和全相等运算符进行比较。相等运算符首先将字符串`"5"`数字`5`，然后与另一个数字`5`进行比较，结果为`true`。全相等运算符注意到两个数据类型不同，并直接返回`false`。对于`1`和`true`，情况也是类似的：相等运算符认为它们相等，但全相等运算符认为它们不相等。类型转换错误发生的第二个地方是流程控制语句。`if`等语句在确定下一步之前会自动将任何值转换为布尔值。`if`语句经常以错误的方式使用。考虑以下示例：

```javascript
function concat(str1, str2, str3){
    var result = str1 + str2;
    if (str3){  //避免这样做
        result += str3;
    }
    return result;
}
```

该函数的意图是拼接两个三个字符串并返回结果。第三个字符串是一个可选参数，因此必须进行检查。正如第 3 章提到的，未使用的命名变量会被赋值为`undefined`。`undefined`值会转换为布尔值`false`，因此该函数中`if`语句的意图是在提供第三个参数时进行拼接。问题在于，`undefined`不是唯一转换为`false`的值，字符串也不是唯一转换为`true`的值。例如，如果第三方参数是数字`0`，`if`条件将失败，而值`1`则会导致条件通过。

在流程控制语句中使用非布尔值作为条件是非常常见的错误原因。为了避免此类错误，请始终确保作为条件传递的是布尔值。这通常通过进行某种比较来实现。例如，之前的函数可以重写如下所示：

```javascript
function concat(str1, str2, str3){
    var result = str1 + str2;
    if (typeof str3 == "string"){  //正确的比较
        result += str3;
    }
    return result;
}
```

在这个函数的更新版本中，`if`语句的条件根据比较返回布尔值。这个函数安全得多，且受错误值的影响较小。

# 数据类型错误

由于 JavaScript 是弱类型语言，变量和函数参数不会通过比较来确保使用了正确类型的数据。作为开发者开发者，你有责任进行适当程度的数据类型检查，以确保不会发生错误。数据类型错误通常是由于向函数传递了意外之外的值导致的。

在上一个示例中，检查了第三个参数的数据类型以确保它是字符串，但另外两个参数完全没有进行任何检查。如果函数必须返回字符串，那么传入两个数字并省略第三个参数很容易导致其崩溃。在下面的函数中存在类似的情况：

```javascript
//不安全的函数，任何非字符串值都会导致错误
function getQueryString(url){
    var pos = url.indexOf("?");
    if (pos > -1){
        return url.substring(pos +1);
    }
    return "";
}
```

该函数的目的是返回给定 URL 的查询字符串。为了实现这一点，它首先使用`indexOf()`在字符串中查找问号，如果找到，则使用`substring()`方法返回问号之后的所有内容。此示例中使用的两个方法是针对字符串的，因此传入任何其他数据类型都会导致错误。以下简单的类型检查使此函数更不容易出错：

```javascript
function getQueryString(url){
    if (typeof url == "string"){      //带有类型检查更安全
        var pos = url.indexOf("?");
        if (pos > -1){
            return url.substring(pos +1);
        }
    }
    return "";
}
```



在函数的这个重写版本中，第一步是检查传递的值是否实际上是字符串。这确保了函数永远因为非字符串值而导致错误。

正如上一节所讨论的，将非布尔值作为流程控制语句的条件是一个坏主意，因为存在类型转换。这也是一种会导致数据类型错误的坏做法。考虑以下函数：

```javascript
//不安全的函数，非数组值会导致错误
function reverseSort(values){
    if (values){  //避免！！！
        values.sort();
        values.reverse();
    }
}
```

`reverseSort()` 函数使用 `sort()` 和 `reverse()` 方法按反序对数组进行排序。由于 `if` 语句中的控制条件，任何转换为 `true` 的非数组值都会导致错误。另一个常见的错误是将参数与 `null` 进行比较，如下例所示：

```javascript
//仍然不安全，非数组值会导致错误
function reverseSort(values){
    if (values != null){  //避免！！！
        values.sort();
        values.reverse();
    }
}
```

将值与 `null` 进行比较只能保护代码免受两个值的影响：`null` 和 `undefined`（这等同于使用相等和不等运算符）。与 `null` 比较不足以确保该值是合适的；因此，应该避免这种技术。同样建议你不要将值与 `undefined` 进行比较，原因相同。

另一个糟糕的选择是仅对所使用的功能之一进行特征性检测（feature detection）。这里有一个示例：

```javascript
//仍然不安全，非数组值会导致错误
function reverseSort(values){
    if (typeof values.sort == "function"){  //避免！！！
        values.sort();
        values.reverse();
    }
}
```

在这个示例中，代码检查了参数上是否存在 `sort()` 方法。这留下了可能性，即传入了一个带有 `sort()` 函数但不是数组的对象，在这种情况下，对 `reverse()` 的调用会导致错误。当你确定预期的对象精确类型时，最好使用 `instanceof`（如后续示例所示）来判断该值是正确的类型：

```javascript
//安全的，忽略了非数组值
function reverseSort(values){
    if (values instanceof Array){  //修复
        values.sort();
        values.reverse();
    }
}
```

`reverseSort()` 的最后一个版本是安全的——它测试了 `values` 参数以检查它是否是 `Array` 的实例。通过这种方式，函数确保了任何非数组值都会被忽略。

通常情况下，本应是原始类型的值应该使用 `typeof` 进行检查，而本应是对象的值应该使用 `instanceof` 进行检查。取决于函数如何使用，可能没有必要检查每个参数的数据类型，但任何面向公共的 API 绝对应该执行类型检查以确保正确执行。

## 通信错误

自从 Ajax 编程出现以来（第 21 节已讨论），Web 应用在整个应用程序生命周期内动态加载信息或功能已变得普遍。JavaScript 与服务器之间的任何通信都是可能发生错误的机会。

第一类通信错误涉及格式不正确的 URL 或 POST 数据。这通常发生在数据在发送到服务器之前没有使用 `encodeURIComponent()` 编码时。例如，下面的 URL 不正确：

```
http://www.yourdomain.com/?redir=http://www.someotherdomain.com?a=b&c=d
```

通过对 `"redir="` 之后的所有内容使用 `encodeURIComponent()` 可以修复此 URL，产生如下结果：

```
http://www.example.com/?redir=http%3A%2F%2Fwww.someotherdomain.com%3Fa%3Db%26c%3Dd
```

对于查询字符串参数，应该始终使用 `encodeURIComponent()` 方法。为了确保这一点，你有时会发现定义一个处理查询字符串的函数很有帮助，如下所示：

```javascript
function addQueryStringArg(url, name, value){
    if (url.indexOf("?") == -1){
        url += "?";
    } else {
        url += "&";
    }
    url += encodeURIComponent(name) + "=" + encodeURIComponent(value);
    return url;
}
```

该函数接受三个参数：添加查询字符串参数的 URL、参数名称以及参数值。该函数可以如下例所示：

```javascript
var url = "http://www.somedomain.com";
var newUrl = addQueryStringArg(url, "redir", "http://www.someotherdomain.com?a=b&c=d");
alert(newUrl);
```

使用此函数而不是手动构建 URL 可以确保正确的编码并避免相关错误。

当服务器响应不符合预期时，也会发生通信错误。在使用动态脚本加载或动态样式加载时（第 10 节已讨论），可能请求资源不可用。Firefox、Chrome 和 Safari 在未返回资源时静默失败，而 Internet Explorer 和 Opera 都会报错。遗憾的是，在使用这些技术判断错误发生时，无能为力。在某些情况下，使用 Ajax 通信可以就错误状况提供更多信息。

![image](img/pen.gif)

在使用 Ajax 通信时可能发生通信错误。围绕 Ajax 的问题和错误将在第 21 节讨论。

## 区分致命错误和非致命错误

错误处理策略最重要的部分之一是判断错误是否致命。具有以下一个或多个特征可以识别非致命错误：

*   它不会干扰用户的主要任务。
*   它只影响页面的部分。
*   是可以恢复的。
*   重复操作可能会导致成功。

### 错误处理

从本质上，非致命错误并不令人担心。例如，Yahoo! Mail（[`mail.yahoo.com`](http://mail.yahoo.com)）具有一个功能，允许用户从界面发送短信（SMS）。如果由于某种原因短信无法工作，这是一个非致命错误，因为这并不是应用程序的主要功能。Yahoo! Mail 的主要用例是读取和撰写电子邮件，只要用户可以执行该操作，就没有理由中断用户体验。非致命错误不需要你向用户发送显式消息——你可能可以使用一条指示该功能不可用的消息来替换受影响的页面区域，但没有必要中断用户。

### 致命错误

另一方面，致命错误通过以下一个或多个特征进行识别：

* 应用程序完全无法继续运行。
* 错误严重干扰了用户的主要目标。
* 导致了其他错误的发生。

了解 `JavaScript` 中何时发生致命错误至关重要，以便采取适当的措施。当发生致命错误时，你应该立即向用户发送消息，让他们知道他们将无法继续正在的操作。如果必须重新加载页面才能使应用程序运行，你应该告诉用户这一点，并提供一个自动刷新页面的按钮。

你还必须确保你的代码不要规定什么是致命错误以及不是。非致命错误和致命错误主要通过它们对用户的影响来指示。良好的代码设计意味着应用程序某部分的错误不应不必要地影响另一个在实际上完全不相关的部分。例如，考虑像一个个性化首页，例如 My Yahoo!（[`my.yahoo.com`](http://my.yahoo.com)），该页面上有多个独立的模块。如果每个模块都必须使用 `JavaScript` 调用进行初始化，你可能会看到类似下面的代码：

```javascript
for (var i=0, len=mods.length; i < len; i++){
    mods[i].init();    //可能发生致命错误
}
```

从表面上看，这段代码看起来很好：每个模块上都调用了 `init()` 方法。问题是，任何模块的 `init()` 方法中的错误将导致数组中其后的所有模块都无法初始化。如果错误发生在第一个模块上，那么页面上的所有模块都无法初始化。从逻辑上讲，这是不通的，因为每个模块都是独立的实体，其功能不依赖于任何其他模块。是代码的结构导致这种错误变成了致命的。幸运的是，可以将代码重写如下，使任何一个模块中的错误变为非致命的：

```javascript
for (var i=0, len=mods.length; i < len; i++){
    try {
        mods[i].init();
    } catch (ex){
        //在此处处理错误
    }
}
```

通过在 `for` 循环中添加 `try-catch`语句，模块初始化时的任何错误都不会阻止其他模块的初始化。当这段代码发生错误时，可以独立地处理，并以不干扰用户体验的方式。

## 将错误记录到服务器

Web 应用程序的一种做法是设置一个集中错误日志，其中为了跟踪目的写入重要错误。数据库和服务器错误会定期写入日志，并通过一些常用的 API 进行分类。对于复杂的 Web 应用程序，建议也将 `JavaScript` 错误记录回服务器。这种想法是将错误记录到用于服务器端错误的相同系统中，并将它们归类为来自前端。使用相同的系统允许无论错误来源如何，都能对数据进行相同的分析。

要建立 `JavaScript` 错误日志系统，你首先需要在服务器上有一个可以处理错误数据的页面或入口点。该页面只需要执行从查询字符串中获取数据并将其保存到错误日志中的操作。该页面随后可以使用如下代码配合：

```javascript
function logError(sev, msg){
    var img = new Image();
    img.src = "log.php?sev=" + encodeURIComponent(sev) + "&msg=" + 
              encodeURIComponent(msg);
}
```

`logError()` 函数接受两个参数：严重程度和错误消息。严重程度可以是数字或字符串，取决于你使用的系统。使用 `Image` 对象发送请求是因为它的灵活性，正如此处所述：

* `Image` 对象在所有浏览器中都可用，即使是那些不支持 `XMLHttpRequest` 对象的浏览器。
* 不受跨域限制。通常有一个服务器负责处理来自多个服务器的错误日志，在这种情况下 `XMLHttpRequest` 将无法工作。
* 在记录错误的过程中发生错误的概率较小。大多数 Ajax 通信都是通过 `JavaScript` 库提供的功能封装处理的。如果该库的代码失败，而你又尝试使用它来记录错误，则消息可能永远无法记录。

每当使用 `try-catch` 语句时，错误很可能应该被记录。这是一个示例：

```javascript
for (var i=0, len=mods.length; i < len; i++){
    try {
        mods[i].init();
    } catch (ex){
        logError("nonfatal", "Module init failed: " + ex.message);
    }
}
```

在此代码中，当模块初始化失败时会调用 `logError()`。第一个参数是 `"nonfatal"`，表示严重程度，消息提供了上下文信息。记录到服务器的错误消息应尽可能提供上下文信息。

## 调试技术

在 `JavaScript` 调试器可用之前，开发者必须使用创意的方法来调试代码。这导致了专门设计用于输出调试信息的代码放置。最常见的调试技术是在代码中插入 `alert`，这既繁琐（因为调试后需要清理），而且如果遗留在生产环境的代码中会很困扰。`alert` 不再推荐用于调试，因为有了其他更优雅的解决方案。

### 消息到控制台

Internet Explorer 8+、`Firefox`、`Opera`、`Chrome` 和 `Safari` 都有用于查看 `JavaScript` 错误的控制台。所有这些都允许从代码直接写入控制台。为了在 `Firefox` 3.6 或更早版本中实现此功能，你需要安装 `Firebug`（[www.getfirebug.com](http://www.getfirebug.com)），因为 `Firefox` 使用的是 `Firebug` 控制台。Internet Explorer 8+、`Firefox`、`Chrome`、`Safari` 和 `Opera 10.5` 允许通过 `console` 对象写入 `JavaScript` 控制台，该对象有以下方法：

* `error(message)` —— 向控制台记录错误消息
* `info(message)` —— 向控制台记录信息消息
* `log(message)` —— 向控制台记录通用消息
* `warn(message)` —— 向控制台记录警告消息

在 Internet Explorer 8、`Firebug`、`Chrome`、`Safari` 和 `Opera` 中，错误控制台上的显示取决于记录消息的方法。错误消息包含红色图标，而警告包含黄色图标。可以使用控制台消息，如下所示函数所示：

```javascript
function sum(num1, num2){
    console.log("Entering sum(), arguments are " + num1 + "," + num2);
    console.log("Before calculation");
    var result = num1 + num2;
    console.log("After calculation");
    console.log("Exiting sum()");
    return result;
}
```

当 `sum()` 函数被调用时，会有若干消息输出到 JavaScript 控制台以辅助调试。可以通过“开发”菜单（之前讨论过）打开 Safari JavaScript 控制台；Chrome JavaScript 控制台通过点击“控制此页”按钮并选择“开发者 JavaScript 控制台”来打开（之前也讨论过）；Firebug 控制台可以通过点击 Firefox 状态栏右下角的图标访问。Internet Explorer 8 控制台是“开发者工具”扩展的一部分，可在“工具”菜单下可用；控制台位于“脚本”选项卡上。

在 10.5 版本之前，Opera 的 JavaScript 控制台只能通过 `opera.postError()` 方法进行访问。该方法接受一个参数，即要写入控制台的消息，其用方式如下：

```javascript
function sum(num1, num2){
    opera.postError("Entering sum(), arguments are " + num1 + "," + num2);
    opera.postError("Before calculation");
    var result = num1 + num2;
    opera.postError("After calculation");
    opera.postError("Exiting sum()");
    return result;
}
```

尽管 `opera.postError()` 方法的名字如此，但它仍可用于将任何类型的信息写入 JavaScript 控制台。

另一个选项是使用 LiveConnect，即从 JavaScript 运行 Java 代码的能力。Firefox、Safari 和 Opera 都支持 LiveConnect 并可能与 Java 控制台交互。可以通过以下代码使用 JavaScript 向 Java 控制台写入消息：

```javascript
java.lang.System.out.println("Your message");
```

它可以替代 `console.log()` 或 `opera.postError()`，如例例所示：

```javascript
function sum(num1, num2){
    java.lang.System.out.println("Entering sum(), arguments are " + num1 + "," + num2);
    java.lang.System.out.println("Before calculation");
    var result = num1 + num2;
    java.lang.System.out.println("After calculation");
    java.lang.System.out.println("Exiting sum()");
    return result;
}
```



根据系统设置，一旦调用 LiveConnect，可能会显示 Java 控制台。在 Firefox 的“工具”菜单下可以找到 Java 控制台，在 Opera 的“工具 ⇒ 高级”菜单下可以找到。Safari 没有内置打开 Java 控制台的支持；你必须单独运行它。

由于目前没有真正的跨浏览器支持来写入 JavaScript 控制台，以下函数均化了接口：

![image](img/logo1.gif)

```javascript
function log(message) {
    if (typeof console == "object") {
        console.log(message);
    } else if (typeof opera == "object") {
        opera.postError(message);
    } else if (typeof java == "object" && typeof java.lang == "object") {
        java.lang.System.out.println(message);
    }
}
```

`ConsoleLoggingExample01.htm`

`log()`函数检测可用的 JavaScript 控制台接口并使用相应的接口。此函数可以在所有浏览器中安全地使用而不会引起任何错误，如下例所示：

```javascript
function sum(num1, num2) {
    log("Entering sum(), arguments are " + num1 + "," + num2);
    log("Before calculation");

    var result = num1 + num2;

    log("After calculation");
    log("Exiting sum()");

    return result;
}
```

`ConsoleLoggingExample01.htm`

将消息到 JavaScript 控制台对调试代码很有帮助，但在代码进入生产环境时应移除所有消息。这可以通过部署过程中的代码处理步骤自动完成，也可以手动完成。

![image](img/pen.gif)

记录消息被认为比使用`alert`更好的调试方法，因为`alert`会中断程序的执行，这可能会影响代码的结果，因为异步过程的时机会受到影响。

## 向页面记录消息

另一种记录调试消息的常用方法是指定页面上一个写入消息的区域。这可能是一个始终包含但仅用于调试目的元素，也可能是仅在需要时创建的元素。例如，可以将`log()`函数更改为：

![image](img/logo1.gif)

```javascript
function log(message) {
    var console = document.getElementById("debuginfo");

    if (console === null) {
        console = document.createElement("div");
        console.id = "debuginfo";
        console.style.background = "#dedede";
        console.style.border = "1px solid silver";
        console.style.padding = "5px";
        console.style.width = "400px";
        console.style.position = "absolute";
        console.style.right = "0px";
        console.style.top = "0px";

        document.body.appendChild(console);
    }

    console.innerHTML += "<p>" + message + "</p>";
}
```

`PageLoggingExample01.htm`

在`log()`的新版本中，代码首先检查调试元素是否已存在。如果没有，则创建一个`<div>`元素并分配样式信息将其与页面其他部分隔离开。之后，使用`innerHTML`将消息写入`<div>`中。结果是页面上一个显示日志信息的小区域。当在 Internet Explorer 7 及更早版本或其他不支持 JavaScript 控制台的浏览器中调试代码时，这种方法可能有用。

![image](img/pen.gif)

正如控制台日志一样，页面日志代码在进入生产环境之前应移除。

### 错误

如所述，抛出错误是调试代码的极佳方法。如果错误消息是具体的，看到错误可能就能确定问题。良好的错误消息的关键在于它们提供关于原因的准确信息，从而使额外的调试工作降至最低。考虑以下函数：

```javascript
function divide(num1, num2) {
    return num1 / num2;
}
```

这个简单函数除以两个数字，但如果两个参数中的一个不是数字，它将返回`NaN`。在这种情况下，你可以检查每个参数的类型。考虑以下示例：

```javascript
function divide(num1, num2) {
    if (typeof num1 != "number" || typeof num2 != "number") {
        throw new Error("divide(): Both arguments must be numbers.");
    }

    return num1 / num2;
}
```

在这里，如果两个参数不是数字，就会抛出一个错误。错误消息提供了函数名称和错误的准确原因。当浏览器报告此错误消息时，它立即为你提供了查找问题的起点以及问题的基本概述。这比处理不明确的浏览器错误消息要容易得多。

在大型应用程序中，通常使用`assert()`函数抛出自定义错误。此类函数接受一个应该为真的条件，如果条件为假，则抛出错误。以下是一个非常基础的`assert()`函数：

![image](img/logo1.gif)

```javascript
function assert(condition, message) {
    if (!condition) {
        throw new Error(message);
    }
}
```

`AssertExample01.htm`

`assert()`函数可以用来替代函数中的多个`if`语句，并可以作为错误日志的良好位置。该函数的用方式如下：

```javascript
function divide(num1, num2) {
    assert(
        typeof num1 == "number" && typeof num2 == "number",
        "divide(): Both arguments must be numbers."
    );

    return num1 / num2;
}
```

`AssertExample01.htm`

使用`assert()`函数减少了抛出自定义错误所需的代码量，与之前的示例相比，代码更具可读性。

## 常见的 INTERNET EXPLORER 错误

Internet Explorer 传统上一直是最难调试 JavaScript 错误的浏览器之一。该浏览器的错误信息通常简短且令人困惑，提供的上下文很少或没有。由于 Internet Explorer 是最流行的网页浏览器，它的错误往往会受到最多的关注。以下章节列出了可能发生的常见且难以调试的 JavaScript 错误列表。

## 操作中止（Operation Aborted）

`8`之前的 Internet Explorer 版本可能拥有所有浏览器中最令人困惑、恼人且最难调试的错误之一：`operation aborted`错误。

当页面中尚未完全加载的部分正在被修改时，就会发生`operation aborted`错误。结果是弹出一个显示“Operation aborted”的模态对话框。点击 OK 按钮后，整个网页将卸载并被空白屏幕替换，这使得调试变得非常困难。以下示例页面会导致`operation aborted`错误：

```html
<!DOCTYPE html>
<html>
<head>
    <title>Operation Aborted Example</title>
</head>
<body>
    <p>以下代码在 8 之前的 IE 版本中应该导致 Operation Aborted 错误。</p>
    <div>
        <script type="text/javascript">
            document.body.appendChild(document.createElement("div"));
        </script>
    </div>
</body>
</html>
```

`OperationAbortedExample01.htm`

此示例中的问题是 JavaScript 代码试图在`document.body`完全加载之前对其进行修改，并且`<script>`元素不是`<body>`元素的直接子元素。具体来说，每当`<script>`节点包含在某个元素内部，且 JavaScript 代码尝试使用`appendChild()`、`innerHTML`或任何假设元素已完全加载的 DOM 方法来修改该元素的父元素或祖元素时，就会发生此错误。

你可以通过两种方式解决此问题：等待元素完全加载后再尝试对其进行操作，或者使用不同的操作方法。例如，在`document.body`中添加在页面上绝对定位的覆盖层是非常常见的。这些额外的元素通常是通过使用`appendChild()`添加的，但可以很容易更改为使用`insertBefore()`。之前的示例可以通过更改一行代码来重写，以避免`operation aborted`错误，如下所示：

![image](img/logo1.gif)

```html
<!DOCTYPE html>
<html>
<head>
    <title>Operation Aborted Example</title>
</head>
<body>
    <p>以下代码在 8 之前的 IE 版本中不应导致 Operation Aborted 错误。</p>
    <div>
        <script type="text/javascript">
            document.body.insertBefore(
                document.createElement("div"),
                document.body.firstChild
            );
        </script>
    </div>
</body>
</html>
```

`OperationAbortedExample02.htm`

在此示例中，新的`<div>`元素被添加到`document.body`的开头而不是末尾。这不会导致错误，因为在脚本运行时，完成操作所需的所有信息都是可用的。

另一个选项是移动`<script>`元素，使其成为`<body>`的直接子元素。考虑以下示例：

![image](img/logo1.gif)

```html
<!DOCTYPE html>
<html>
<head>
    <title>Operation Aborted Example</title>
</head>
<body>
    <p>以下代码在 8 之前的 IE 版本中不应导致 Operation Aborted 错误。</p>
    <div>
    </div>
    <script type="text/javascript">
        document.body.appendChild(document.createElement("div"));
    </script>
</body>
</html>
```

`OperationAbortedExample03.htm`

在这里，没有发生`operation aborted`错误，因为脚本修改的是它的直接父元素而不是祖元素。

Internet Explorer `8`及更高版本不再抛出`operation aborted`错误，而是抛出带有以下消息的普通 JavaScript 错误：

```text
HTML Parsing Error: Unable to modify the parent container element before the child element is closed (KB927917).
```

尽管浏览器的反应不同，解决问题的方法相同。

## 无效字符（Invalid Character）

JavaScript 文件的语法必须由某些字符组成。当在 JavaScript 文件中检测到无效字符时，IE 会抛出“invalid character”错误。无效字符是任何未定义为 JavaScript 语法一部分的字符。

例如，有一个字符看起来像减号，但由 Unicode 值`8211`（`\u2013`）表示。该字符不能代替普通的减号（ASCII 码为`45`），因为它不属于 JavaScript 语法的一部分。

这种特殊字符经常被自动插入 Microsoft Word 文档中，因此如果你将在 Word 中编写的代码复制到文本编辑器中然后在 Internet Explorer 中运行，就会得到非法字符错误。其他浏览器的反应类似：Firefox 抛出“illegal character”错误，Safari 报告语法错误，Opera 报告`ReferenceError`，因为它将该字符解释为未定义的标识符。

## 成员未找到（Member Not Found）

如前所述，Internet Explorer 中的所有 DOM 对象都实现为 COM 对象，而不是原生 JavaScript。这在涉及垃圾回收时可能会导致一些非常奇怪的行为。“member not found”错误是 Internet Explorer 中不匹配的垃圾回收程序的直接结果。

此错误通常发生在你尝试在对象已经被销毁后给对象属性赋值时。该对象必须是 COM 对象才会出现特定的错误消息。最典型的例子是使用事件对象时。

Internet Explorer 事件对象作为`window`的属性存在，并在事件发生时创建，在最后一个事件处理程序执行后销毁。因此，如果你在稍后执行的闭包中使用事件对象，对属性的任何尝试都会导致错误，如下所示：

```javascript
document.onclick = function() {
    var event = window.event;

    setTimeout(function() {
        event.returnValue = false;    // 成员未找到错误
    }, 1000);
};
```

在此代码中，为`document`分配了一个点击处理程序。它将`window.event`的引用存储在局部变量`event`中。然后该事件变量被传递给`setTimeout`的闭包。

当`onclick`事件处理程序退出时，事件对象被销毁，因此闭包中的引用指向一个不存在的对象。为`returnValue`赋值会导致“member not found”错误，因为你无法写入已销毁成员的 COM 对象。

## 未知运行时错误（Unknown Runtime Error）

当通过以下方式使用`innerHTML`或`outerHTML`属性赋值 HTML 时，会发生未知运行时错误：如果块元素被插入到内联元素，或者你在表格的任何部分（`<table>`、`<tbody>`等）访问这些属性。

例如，`<p>`标签技术上不能包含`<div>`等块级元素，因此以下代码会导致未知运行时错误：

```javascript
p.innerHTML = "<div>Hi</div>";   // 其中 p 包含一个 <p> 元素
```



其他浏览器在块元素插入到无效位置时会尝试纠错以防止发生错误，但 `Internet Explorer` 在这方面严格得多。

# 语法错误 (Syntax Error)

通常当 `Internet Explorer` 报告语法错误时，原因是显而易见的。你通常可以将错误追溯到缺失的分号或错误的右括号。然而，还有另一种发生语法错误的情况，但其原因可能并不显而易见。

如果你引用的外部 JavaScript 文件由于某种原因返回了非 JavaScript 代码，`Internet Explorer` 就会抛出语法错误。例如，如果你将 `<script>` 标签的 `src` 属性指向一个 HTML 文件，就会发生语法错误。语法错误通常被报告为脚本的第一行和第一个字符。`Opera` 和 `Safari` 也会报告语法错误，但它们还会报告导致问题的被引用文件。`Internet Explorer` 未提供此类信息，因此你需要双检每个外部引用的 JavaScript 文件。`Firefox` 则简单地忽略像 JavaScript 一样包含的非 JavaScript 文件中的任何解析错误。

这类错误通常发生在服务器端组件动态生成 JavaScript 的时候。许多服务器端语言在发生运行时错误时，会自动将 HTML 插入到输出中，而这种输出会明显破坏 JavaScript 语法。如果你在追踪语法错误时遇到困难，请双检每个外部 JavaScript 文件，以确保其中不包含服务器因为错误而插入的 HTML。

# 系统找不到指定的资源

也许最没用的错误消息之一就是“系统找不到指定的资源”。当使用 JavaScript 通过 URL 请求资源，且 URL 长度超过了 `Internet Explorer` 2083 个字符的最大 URL 长度时，就会发生此错误。此 URL 长度限制不仅适用于 JavaScript，也适用于整个 `Internet Explorer`。（其他浏览器对 URL 长度限制并不严格。）此外还有 2048 个字符的 URL 路径限制。以下示例会导致此错误：

```
function createLongUrl(url){
    var s = "?";
    for (var i=0, len=2500; i < len; i++){
        s += "a";
    }
    return url + s;
}
var x = new XMLHttpRequest();
x.open("get", createLongUrl("http://www.somedomain.com/"), true);
x.send(null);
```

`LongURLErrorExample01.htm`

在此段代码中，`XMLHttpRequest` 对象尝试对超过最大 URL 限制的 URL 发起请求。错误在调用 `open()` 时发生。此类错误的一种变通是缩短请求成功所需的查询字符串，可以通过减小命名查询字符串参数的大小或删除不必要的数据来实现。另一种变通是将请求更改为 `POST`，并将数据作为请求体发送，而不是放在查询字符串中。`Ajax`、`XMLHttpRequest` 对象以及此类问题将在第 21 章中详细讨论。

## 总结

JavaScript 中的错误处理对于当今复杂的 Web 应用至关重要。未能预判错误可能发生的位置以及如何从中恢复，会导致糟糕的用户体验，并可能让用户感到沮丧。大多数浏览器默认不会向用户报告 JavaScript 错误，因此在开发和调试时你需要启用错误报告。然而，在生产环境中，不应以这种方式报告任何错误。

可以使用以下方法防止浏览器对 JavaScript 错误做出反应：

* 可以在可能发生错误的地方使用 `try-catch` 语句，这让你有机会以适当的方式响应错误，而不是让浏览器来处理错误。
* 另一个选项是使用 `window.onerror` 事件处理程序，它可以接收所有未被 `try-catch` 处理的错误（仅限 `Internet Explorer`、`Firefox` 和 `Chrome`）。

每个 Web 应用都应该经过检查，以确定错误可能发生的地方以及应该如何处理这些错误。

* 需要预先确定什么是致命错误，什么是非致命错误。
* 之后，可以对代码进行评估，以确定最可能发生错误的地方。JavaScript 中的错误通常由于以下因素引起：
    * 类型强制转换
    * 数据类型检查不足
    * 向服务器发送或从服务器接收了错误的数据

`Internet Explorer`、`Firefox`、`Chrome`、`Opera` 和 `Safari` 各都有 JavaScript 调试器，它们随浏览器自带，也可以作为插件下载。每个调试器都提供了设置断点、控制代码执行以及在运行时检查变量值的能力。

# 第 18 章：JavaScript 中的 XML

## 本章主要内容

* 检查浏览器对 XML DOM 的支持
* 理解 JavaScript 中的 XPath
* 使用 XSLT 解析器

在某个时期，XML 是互联网上结构化数据存储和传输的标准。XML 的演进紧密反映了 Web 技术的演进，因为 `DOM` 的开发不仅用于 Web 浏览器，还用于桌面和服务器应用程序，以处理 XML 数据结构。许多开发者开始在 JavaScript 中编写自己的 XML 解析器，以解决缺乏内置解决方案的问题。从那时起，所有浏览器都引入了对 XML、`XML DOM` 以及许多相关原生支持。

## 浏览器中的 XML DOM 支持

由于浏览器厂商在正式标准创建之前就开始实现 XML 解决方案，因此每种厂商提供的不仅有不同程度的支持，还有不同的实现。`DOM Level 2` 是第一个引入动态 XML DOM 创建概念的规范。这一能力在 `DOM Level 3` 中得到了扩展，包含了解析和序列化。然而，在 `DOM Level 3` 确定时，大多数浏览器已经实现了自己的解决方案。

### DOM Level 2 核心

正如第 12 章提到的，`DOM Level 2` 引入了 `document.implementation` 的 `createDocument()` 方法。`Internet Explorer 9+`、`Firefox`、`Opera`、`Chrome` 和 `Safari` 都支持此方法。你可能记得可以使用以下语法创建一个空白 XML 文档：

```
var xmldom = document.implementation.createDocument(namespaceUri, root, doctype);
```

在 JavaScript 中处理 XML 时，通常只使用 `root` 参数，因为它定义了 XML DOM 根元素的标签名。`namespaceUri` 参数很少使用，因为命名空间在 JavaScript 中很难管理。`doctype` 参数极少、甚至从未使用。

要创建一个根元素为 `<root>` 的 XML 文档，可以使用以下代码：

```
var xmldom = document.implementation.createDocument("", "root", null);
alert(xmldom.documentElement.tagName);  //"root"
var child = xmldom.createElement("child");
xmldom.documentElement.appendChild(child);
```

`DOM2CoreExample01.htm`

此示例创建一个没有默认命名空间和类型的 XML 文档。注意，即使不需要命名空间和类型，必须传递这些参数。`xmldom` 包含 `Level 2 Document` 类型的实例，包含了第 12 章讨论的所有 DOM 方法和属性。在此示例中，显示了元素的标签名，然后创建并添加了一个子元素。

可以使用以下代码检查浏览器是否启用了 `DOM Level 2 XML` 支持：

```
var hasXmlDom = document.implementation.hasFeature("XML", "2.0");
```

在实践中，很少从零开始创建一个 XML 文档然后使用 DOM 方法系统地构建它。更有可能的情况是将 XML 文档解析为 DOM 结构，反之亦然。由于 `DOM Level 2` 没有提供此类功能，出现了一些事实上的标准。

### DOMParser 类型

Firefox 引入了 `DOMParser` 类型，专门用于将 XML 解析为 DOM 文档，后来被 `Internet Explorer 9`、`Safari`、`Chrome` 和 `Opera` 采用。要使用它，你必须先创建一个 `DOMParser` 实例，然后调用 `parseFromString()` 方法。该方法接受两个参数：要解析的 XML 字符串和内容类型，内容类型应始终为 `"text/xml"`。返回值是一个 `Document` 实例。请考虑以下示例：

```
var parser = new DOMParser();
var xmldom = parser.parseFromString("<root><child/></root>", "text/xml");
alert(xmldom.documentElement.tagName);  //"root"
alert(xmldom.documentElement.firstChild.tagName); //"child"
var anotherChild = xmldom.createElement("child");
xmldom.documentElement.appendChild(anotherChild);
var children = xmldom.getElementsByTagName("child");
alert(children.length);   //2
```

`DOMParserExample01.htm`

在这个示例中，一个简单的 XML 字符串被解析为一个 DOM 文档。DOM 结构以 `<root>` 作为文档元素，并有一个单个 `<child>` 元素作为其子元素。你可以使用 DOM 方法与返回的文档进行交互。

`DOMParser` 只能解析格式良好的 XML，因此无法将 HTML 解析为 HTML 文档。遗憾的是，浏览器在发生解析错误时的行为不同。当 `Firefox`、`Opera`、`Safari` 和 `Chrome` 发生解析错误时，`parseFromString()` 仍然返回一个 `Document` 对象，但其文档元素是 `<parsererror>`，该元素的内容是对解析错误的描述。这是一个示例：

```
<parsererror xmlns="http://www.mozilla.org/newlayout/xml/parsererror.xml">XML Parsing Error: no element found Location: file:///I:/My%20Writing/My%20Books/Professional%20JavaScript/Second%20Edition/Examples/Ch15/DOMParserExample2.htm Line Number 1, Column 7:<sourcetext>&lt;root&gt; ------^</sourcetext></parsererror>
```

`Firefox` 和 `Opera` 都以这种格式返回文档。`Safari` 和 `Chrome` 返回的文档在解析错误发生的地方嵌入了一个 `<parsererror>` 元素。`Internet Explorer 9` 在调用 `parseFromString()` 的点会抛出解析错误。由于这些差异，确定是否发生解析错误的最佳方法是使用 `try-catch` 块，如果没有错误，则通过 `getElementsByTagName()` 在文档的任何地方查找 `<parsererror>` 元素，如下：

```
var parser = new DOMParser(),
    xmldom, 
    errors;
try {
    xmldom = parser.parseFromString("<root>", "text/xml");
    errors = xmldom.getElementsByTagName("parsererror");
    if (errors.length > 0){
        throw new Error("Parsing error!");
    }
} catch (ex) {
    alert("Parsing error!");
}
```

`DOMParserExample02.htm`

在这个示例中，要解析的字符串缺少闭合的 `</root>` 标签，导致了解析错误。在 `Internet Explorer 9+` 中，这会抛出一个错误。在 `Firefox` 和 `Opera` 中，`<parsererror>` 元素作为文档元素，而在 `Chrome` 和 `Safari` 中，它是第一个子元素 `<root>`。调用 `getElementsByTagName("parsererror")` 涵盖了两种情况。如果此方法调用返回了任何元素，则说明发生了错误并会显示警报。你还可以进一步，从该元素中提取错误信息。

### XMLSerializer 类型

作为 `DOMParser` 的伴侣，`Firefox` 还引入了 `XMLSerializer` 类型以提供反向功能：将 DOM 文档序列化为 XML 字符串。从那时起，`XMLSerializer` 被 `Internet Explorer 9+`、`Opera`、`Chrome` 和 `Safari` 采用。

要序列化 DOM 文档，你必须创建一个 `XMLSerializer` 实例，然后将文档传递给 `serializeToString()` 方法，如下：

```
var serializer = new XMLSerializer();
var xml = serializer.serializeToString(xmldom);
alert(xml);
```

`XMLSerializerExample01.htm`

`serializeToString()` 返回的值是一个没有经过格式化的字符串，因此肉眼阅读可能困难。

`XMLSerializer` 能够序列化任何有效的 DOM 对象，包括单个节点和 HTML 文档。当将 HTML 文档传递给 `serializeToString()` 时，会被视为 XML 文档，因此生成的代码是格式良好的。

如果将非 DOM 对象传递给 `serializeToString()` 方法，则会抛出错误。

### Internet Explorer 8 及更早版本中的 XML

`Internet Explorer` 实际上是第一个实现原生 XML 处理支持的浏览器，它是通过使用 ActiveX 对象实现的。微软创建了 `MSXML` 库为桌面应用程序开发者提供 XML 处理能力，而不是为 JavaScript 创建不同的对象，他们只是通过浏览器启用了对相同对象的访问。

在第 8 章中，你接触了 `ActiveXObject` 类型，它用于在 JavaScript 中实例化 ActiveX 对象。使用 `ActiveXObject` 构造函数创建 XML 文档实例，并传入 XML 文档版本的字符串标识符。有六种不同的 XML 文档对象，如下：

*   `Microsoft.XmlDom` —— IE 发布时的初始版本；不应使用。
*   `MSXML2.DOMDocument` —— 更新版本，用于脚本目的，但仅作为应急备选。
*   `MSXML2.DOMDocument.3.0` —— JavaScript 使用的最低推荐。
*   `MSXML2.DOMDocument.4.0` —— 不认为安全用于脚本。
*   `MSXML2.DOMDocument.5.0` —— 同样不安全用于脚本。
*   `MSXML2.DOMDocument.6.0` —— 最新且最健壮的版本。

你可以通过尝试创建每个版本并观察错误来确定哪个版本可用。例如：

```
function createDocument(){
    if (typeof arguments.callee.activeXString != "string"){
        var versions = ["MSXML2.DOMDocument.6.0", "MSXML2.DOMDocument.3.0",
                        "MSXML2.DOMDocument"],
            i, len;
        for (i=0,len=versions.length; i < len; i++){
            try {
                new ActiveXObject(versions[i]);
                arguments.callee.activeXString = versions[i];
                break;
            } catch (ex){
                //跳过
            }
        }
    }
    return new ActiveXObject(arguments.callee.activeXString);
}
```



`IEXmlDomExample01.htm`

在这个函数中，使用 `for` 循环遍历可能的 `ActiveX` 版本。如果版本不可用，创建新 `ActiveXObject` 的调用会抛出错误，此时 `catch` 语句捕获错误并继续循环。如果没有发生错误，则将该版本存储在函数的 `activeXString` 属性中，这样每次调用函数时就不需要重复此过程，并返回所创建的对象。

要解析 XML 字符串，你必须先创建一个 DOM 文档，然后调用 `loadXML()` 方法。当文档首次创建时，它是完全空的，因此无法与之交互。将 XML 字符串传递给 `loadXML()` 将 XML 解析到 DOM 文档中。

一旦 DOM 文档填充了 XML 内容，就可以像处理任何其他 DOM 文档一样进行交互，包括所有的方法和属性。

解析错误由 `parseError` 属性表示，该属性是一个包含多个与解析问题相关属性的对象。这些属性如下：

- `errorCode` — 表示发生错误种类型的数字代码，如果没有错误，则为 0。
- `filePos` — 错误发生在文件中的位置。
- `line` — 发生错误的行号。
- `linepos` — 发生错误行中在所在行中的字符位置。
- `reason` — 错误的错误纯文本说明。
- `srcText` — 导致错误的代码。
- `url` — 导致错误的文件 URL（如果可用）。

`parseError` 的 `valueOf()` 方法返回 `errorCode` 的值，因此你可以使用以下代码来检查是否发生了解析错误：

```
if (xmldom.parseError != 0){
    alert("Parsing error occurred.");
}
```

错误代码可能是正数也可能是负数，因此你只需要检查它是否不等于 0。解析错误的详细信息很容易获取，并可用于指示更有用的错误信息，如下所示：

![image](img/logo1.gif)

```
if (xmldom.parseError != 0){
    alert("An error occurred:\nError Code: "
          + xmldom.parseError.errorCode + "\n"
          + "Line: " + xmldom.parseError.line + "\n"
          + "Line Pos: " + xmldom.parseError.linepos + "\n"
          + "Reason: " + xmldom.parseError.reason);
}
```

`IEXmlDomExample02.htm`

你应该在调用 `loadXML()` 之后、在尝试查询 XML 文档更多信息之前立即检查解析错误。

### XML 序列化

Internet Explorer 中的 DOM 文档内置了 XML 序列化。每个节点都有一个 `xml` 属性，可以获取表示该节点的 XML 字符串，例如所示：

```
alert(xmldom.xml);
```

这种简单的序列化方法适用于文档中的每个节点，允许你序列化整个文档或特定的子树。

### 加载 XML 文件

Internet Explorer 中的 XML 文档对象还可以从服务器加载文件。与 DOM Level 3 功能一样，XML 文件必须位于与运行 JavaScript 代码相同的服务器上。同样类似于 DOM Level 3，文档可以同步或异步加载。要确定使用哪种方法，将 `async` 属性设置为 `true` 或 `false`（默认为 `true`）。这是一个示例：

```
var xmldom = createDocument();
xmldom.async = false;
```

一旦确定了加载 XML 文档的模式，调用 `load()` 就会启动下载过程。该方法接受一个参数，即要加载的 XML 文件的 URL。在同步模式下运行时，调用 `load()` 后可以立即检查解析错误和其他 XML 处理，如下所示：

![image](img/logo1.gif)

```
var xmldom = createDocument();
xmldom.async = false;
xmldom.load("example.xml");
if (xmldom.parseError != 0){
    //handle error
} else {
    alert(xmldom.documentElement.tagName);  //"root"
    alert(xmldom.documentElement.firstChild.tagName); //"child"
    var anotherChild = xmldom.createElement("child");
    xmldom.documentElement.appendChild(anotherChild);
    var children = xmldom.getElementsByTagName("child");
    alert(children.length);   //2        
    alert(xmldom.xml);        
}
```

`IEXmlDomExample03.htm`

因为 XML 文件是同步处理的，代码执行将停止直到解析完成，这允许了简单的编码流程。虽然这可能很方便，但如果下载时间比预期长，可能会导致长时间延迟。XML 文档通常异步加载以避免此类问题。

当 XML 文件被异步加载时，你需要为 XML DOM 文档分配一个 `onreadystatechange` 事件处理器。有四种不同的就绪状态：

- 1 — DOM 正在加载数据。
- 2 — DOM 已完成数据加载。
- 3 — DOM 可以，尽管某些部分可能不可用。
- 4 — DOM 已完全加载并准备好使用。

在实际上，唯一感兴趣的就绪状态是 4，它表示 XML 文件已完全下载并解析为 DOM。你可以通过 `readyState` 属性获取 XML 文档的就绪状态。异步加载 XML 文件通常使用以下模式：

![image](img/logo1.gif)

```
var xmldom = createDocument();
xmldom.async = true;
xmldom.onreadystatechange = function(){
    if (xmldom.readyState == 4){
        if (xmldom.parseError != 0){
            alert("An error occurred:\nError Code: "
                  + xmldom.parseError.errorCode + "\n"
                  + "Line: " + xmldom.parseError.line + "\n"
                  + "Line Pos: " + xmldom.parseError.linepos + "\n"
                  + "Reason: " + xmldom.parseError.reason);
        } else {
            alert(xmldom.documentElement.tagName);  //"root"
            alert(xmldom.documentElement.firstChild.tagName); //"child"
            var anotherChild = xmldom.createElement("child");
            xmldom.documentElement.appendChild(anotherChild);
            var children = xmldom.getElementsByTagName("child");
            alert(children.length);   //2        
            alert(xmldom.xml);        
        }
    }
};
```

`IEXmlDomExample04.htm`

注意，`onreadystatechange` 事件处理器的分配必须在调用 `load()` 之前发生，以确保它能及时调用。一旦文档的就绪状态达到 4，你就可以安全地检查是否存在解析错误并开始 XML 处理。

![image](img/pen.gif)

### 跨浏览器 XML 处理

由于可能，很少有开发者可以为单一浏览器开发，因此经常需要为 XML 创建跨浏览的函数。对于 XML 解析，以下函数在所有主流浏览器中都有效：

![image](img/logo1.gif)

```
function parseXml(xml){
    var xmldom = null;
    if (typeof DOMParser != "undefined"){
        xmldom = (new DOMParser()).parseFromString(xml, "text/xml");
        var errors = xmldom.getElementsByTagName("parsererror");
        if (errors.length){
            throw new Error("XML parsing error:" + errors[0].textContent);
        }                   
    } else if (typeof ActiveXObject != "undefined"){
        xmldom = createDocument();
        xmldom.loadXML(xml);
        if (xmldom.parseError != 0){
            throw new Error("XML parsing error: " + xmldom.parseError.reason);
        }
    } else {
        throw new Error("No XML parser available.");
    }
    return xmldom;
}
```

`CrossBrowserXmlExample01.htm`

`parseXml()` 函数接受一个参数，即要解析的 XML 字符串，然后使用功能检测确定使用哪种 XML 解析模式。由于 `DOMParser` 类型是最广泛的解决方案，函数首先测试它是否可用。如果是，则创建一个新的 `DOMParser` 对象并将 XML 字符串解析到 `xmldom` 变量中。由于 `DOMParser` 在 Internet Explorer 9 之前不会为解析错误抛出异常，因此会对返回的文档进行检查，如果发现错误，则抛出异常。

函数的最后一部分检查是否支持 `ActiveX`，并使用之前定义的 `createDocument()` 函数使用正确的签名创建一个 XML 文档。与 `DOMParser` 一样，会对结果进行解析错误检查。如果发现了错误，则会抛出一个指示所报告描述的错误。

如果没有可用的 XML 解析器，该函数将简单地抛出一个错误，指示无法继续。

此函数可以用于解析任何 XML 字符串，并且应该始终封装在 `try-catch` 语句中，以防发生解析错误。这是一个示例：

![image](img/logo1.gif)

```
var xmldom = null;
try {
    xmldom = parseXml("<root><child/></root>");
} catch (ex){
    alert(ex.message);
}
//进一步处理
```

`CrossBrowserXmlExample01.htm`

### XML 序列化

对于 XML 序列化，可以遵循相同的步骤编写一个可在四个主要浏览器运行的函数。例如：

```javascript
function serializeXml(xmldom){
    if (typeof XMLSerializer != "undefined"){
        return (new XMLSerializer()).serializeToString(xmldom);
    } else if (typeof xmldom.xml != "undefined"){
        return xmldom.xml;
    } else {
        throw new Error("Could not serialize XML DOM.");
    }
}
```

`CrossBrowserXmlExample02.htm`

`serializeXml()` 函数接受一个参数，即要序列化的 XML DOM 文档。与 `parseXml()` 函数一样，第一步是检查最广泛使用的解决方案，即 `XMLSerializer`。如果该类型可用，则使用它来返回文档的 XML 字符串。由于 `ActiveX` 方法简单地使用 `xml` 属性，该函数会专门检查该属性。如果这三次尝试都失败了，则该方法将抛出一个错误，指示无法进行序列化。通常情况下，如果你正在为浏览器使用适当的 XML DOM 对象，序列化尝试不应该失败，因此没有必要将对 `serializeXml()` 的调用封装在 `try-catch` 中。相反，你只需要使用以下代码：

```javascript
var xml = serializeXml(xmldom);
```

注意，由于序列化逻辑的差异，不同浏览器之间的序列化结果可能并不完全相同。

### 浏览器中的 XPath 支持

XPath 的创建是为了在 DOM 文档中定位特定节点，因此它对 XML 处理至关重要。直到 DOM Level 3，XPath 的 API 并不是规范的一部分，它引入了 DOM Level 3 XPath 建议。许多浏览器选择实现此规范，但 Internet Explorer 决定以自己的方式实现支持。

#### DOM Level 3 XPath

DOM Level 3 XPath 规范定义了在 DOM 中评估 XPath 表达式的接口。要确定浏览器是否支持 DOM Level 3 XPath，请使用以下 JavaScript 代码：

```javascript
var supportsXPath = document.implementation.hasFeature("XPath", "3.0");
```



虽然规范中定义了多种类型，最重要的两个是`XPathEvaluator`和`XPathResult`。`XPathEvaluator`用于在特定上下评估XPath表达式。该类型具有以下三个方法：

* `createExpression(expression, nsresolver)` — 将XPath表达式及其命名空间信息计算为`XPathExpression`，这是查询的编译版本。如果需要多次运行相同的查询，这将非常有用。
* `createNSResolver(node)` — 根据节点的命名空间信息创建新的`XPathNSResolver`对象。在对使用命名空间的XML文档进行评估时，需要一个`XPathNSResolver`对象。
* `evaluate(expression, context, nsresolver, type, result)` — 在给定的上下文和特定的命名空间信息下评估XPath表达式。额外的参数指示了如何返回结果。

在Firefox、Safari、Chrome和Opera中，`Document`类型通常通过`XPathEvaluator`接口实现。因此，你可以创建一个`XPathEvaluator`的新实例，也可以使用位于`Document`实例上的方法（适用于XML和HTML文档）。

在三个方法中，`evaluate()`是最常用的。该方法接受五个参数：XPath表达式、上下文节点、命名空间解析器、要返回的结果类型以及用于填充结果的`XPathResult`对象（通常为`null`，因为结果也作为函数的返回值返回）。第三个参数命名空间解析器仅在XML代码使用XML命名空间时才是必要的。如果没有使用命名空间，则应将其设置为`null`。第四个参数要返回的结果类型类型是以下10个常量值之一：

* `XPathResult.ANY_TYPE` — 返回适用于XPath表达式的数据类型。
* `XPathResult.NUMBER_TYPE` — 返回数值。
* `XPathResult.STRING_TYPE` — 返回字符串。
* `XPathResult.BOOLEAN_TYPE` — 返回布尔值。
* `XPathResult.UNORDERED_NODE_ITERATOR_TYPE` — 返回匹配节点的节点集，尽管顺序可能与文档内节点的顺序不一致。
* `XPathResult.ORDERED_NODE_ITERATOR_TYPE` — 按照节点在文档中出现的顺序返回匹配节点的节点集。这是最常用的结果类型。
* `XPathResult.UNORDERED_NODE_SNAPSHOT_TYPE` — 返回节点集快照，捕获文档之外的节点以便任何进一步的文档修改都不会影响该节点集。节点集中的节点不保证顺序。
* `XPathResult.ORDERED_NODE_SNAPSHOT_TYPE` — 返回节点集快照，捕获文档之外的节点以便任何进一步的文档修改都不会影响该节点集。节点集中的节点与其在文档中出现的顺序一致。
* `XPathResult.ANY_TYPE`（此处重复项） — 返回匹配节点的节点集，尽管顺序可能与文档内节点的顺序不一致。
* `XPathResult.FIRST_ORDERED_NODE_TYPE` — 返回一个节点的节点集，即文档中的第一个匹配节点。

指定的结果类型决定了如何获取结果的值。这是一个典型的示例：

![image](img/logo1.gif)

```javascript
var result = xmldom.evaluate("employee/name", xmldom.documentElement, null, 
                                  XPathResult.ORDERED_NODE_ITERATOR_TYPE, null);
if (result !== null) {
    var element = result.iterateNext();
    while(element) {
        alert(element.tagName);
        element = result.iterateNext();
    }
}
```

`DomXPathExample01.htm`

此示例使用了`XPathResult.ORDERED_NODE_ITERATOR_TYPE`结果，这是最常用的结果类型。如果没有节点匹配XPath表达式，`evaluate()`返回`null`；否则它返回一个`XPathResult`对象。`XPathResult`具有获取特定类型结果属性和方法。如果结果是节点迭代器（无论有序还是无序），必须使用`iterateNext()`方法获取结果中的每个匹配节点。当没有更多匹配节点时，`iterateNext()`返回`null`。

如果你指定了快照结果类型（无论是有序还是无序），必须使用`snapshotItem()`方法和`snapshotLength`属性，如下例：

```javascript
var result = xmldom.evaluate("employee/name", xmldom.documentElement, null, 
                                  XPathResult.ORDERED_NODE_SNAPSHOT_TYPE, null);
if (result !== null) {
    for (var i=0, len=result.snapshotLength; i < len; i++) {
        alert(result.snapshotItem(i).tagName);
    }
}
```

`DomXPathExample02.htm`

在此示例中，`snapshotLength`返回快照中的节点数量，`snapshotItem()`返回快照中指定位置的节点（类似于`NodeList`中的`length`和`item()`）。

`XPathResult.FIRST_ORDERED_NODE_TYPE`结果返回第一个匹配的节点，可以通过结果的`singleNodeValue`属性访问。例如：

![image](img/logo1.gif)

```javascript
var result = xmldom.evaluate("employee/name", xmldom.documentElement, null, 
                                  XPathResult.FIRST_ORDERED_NODE_TYPE, null);
if (result !== null) {
    alert(result.singleNodeValue.tagName);
}
```

`DomXPathExample03.htm`

与其他查询一样，当没有匹配的节点时，`evaluate()`返回`null`。如果返回了节点，则使用`singleNodeValue`属性进行访问。`XPathResult.FIRST_ORDERED_NODE_TYPE`也是如此。

## 简单类型结果

也可以使用`XPathResult`的`Boolean`、`number`和`string`类型从XPath获取简单的非节点数据类型。这些结果类型分别通过`booleanValue`、`numberValue`和`stringValue`属性返回单个值。对于`Boolean`类型，如果至少有一个节点匹配XPath表达式，评估通常返回`true`，否则返回`false`。考虑以下内容：

```javascript
var result = xmldom.evaluate("employee/name", xmldom.documentElement, null, 
                                  XPathResult.BOOLEAN_TYPE, null);
alert(result.booleanValue);
```

`DomXPathExample04.htm`

在此示例中，如果任何节点匹配"employee/name"，则`booleanValue`属性将等于`true`。

对于`number`类型，XPath表达式必须使用返回数字的XPath函数，例如`count()`，它计算所有匹配给定模式的节点。这是一个示例：

```javascript
var result = xmldom.evaluate("count(employee/name)", xmldom.documentElement, 
                                  null, XPathResult.NUMBER_TYPE, null);
alert(result.numberValue);
```

`DomXPathExample05.htm`

此代码输出了匹配"employee/name"的节点数量（为2）。如果你尝试在不使用特殊XPath函数之一的情况下使用此方法，`numberValue`将等于`NaN`。

对于`string`类型，`evaluate()`方法会找到匹配XPath表达式的第一个节点，然后返回第一个子节点的值，假设第一个子节点是文本节点。如果不是，结果为空字符串。

![image](img/logo1.gif)

```javascript
var result = xmldom.evaluate("employee/name", xmldom.documentElement, null, 
                                  XPathResult.STRING_TYPE, null);
alert(result.stringValue);
```

`DomXPathExample06.htm`

在此示例中，代码输出了匹配"element/name"的第一个元素下的第一个文本节点包含的字符串。

## 默认类型结果

所有XPath表达式会自动映射到特定的结果类型。设置特定的结果类型会限制表达式的输出。然而，你可以使用`XPathResult.ANY_TYPE`常量允许返回自动结果类型。通常，结果类型最终为`Boolean`值、`number`值、`string`值或无序节点迭代器。要确定返回了哪种结果类型，可以使用评估结果上的`resultType`属性，如示例所示：

```javascript
var result = xmldom.evaluate("employee/name", xmldom.documentElement, null, 
                                  XPathResult.ANY_TYPE, null);
if (result !== null) {
    switch(result.resultType) {
        case XPathResult.STRING_TYPE:
            //处理字符串类型
            break;
        case XPathResult.NUMBER_TYPE:
            //处理数字类型
            break;
        case XPathResult.BOOLEAN_TYPE:
            //处理布尔类型
            break;
        case XPathResult.UNORDERED_NODE_ITERATOR_TYPE:
            //处理无序节点迭代器类型
            break;
        default:
            //处理其他可能的结果类型
    }
}
```

使用`XPathResult.ANY_TYPE`常量可以更自然地使用XPath，但可能在结果返回后需要额外的处理代码。

## 命名空间支持

对于使用命名空间的XML文档，必须告知`XPathEvaluator`命名空间信息以便进行适当评估。有多种方法可以。考虑以下XML代码：

```xml
<?xml version="1.0" ?>
<wrox:books xmlns:wrox="http://www.wrox.com/">
    <wrox:book>
        <wrox:title>Professional JavaScript for Web Developers</wrox:title>
        <wrox:author>Nicholas C. Zakas</wrox:author>
    </wrox:book>
    <wrox:book>
        <wrox:title>Professional Ajax</wrox:title>
        <wrox:author>Nicholas C. Zakas</wrox:author>
        <wrox:author>Jeremy McPeak</wrox:author>
        <wrox:author>Joe Fawcett</wrox:author>
    </wrox:book>
</wrox:books>
```

在此XML文档中，所有元素都是`http://www.wrox.com/`命名空间的一部分，由`wrox`前缀标识。如果你想在该文档中使用XPath，需要定义正在使用的命名空间；否则评估将失败。

处理命名空间的第一种方法是通过`createNSResolver()`方法创建`XPathResolver`对象。该方法接受单个参数，即文档中包含命名定义的节点。在之前的示例中，该节点是`<wrox:books>`，它具有`xmlns`属性。可以将该节点传递给`evaluate()`，如下所示：

![image](img/logo1.gif)

```javascript
var nsresolver = xmldom.createNSResolver(xmldom.documentElement);
var result = xmldom.evaluate("wrox:book/wrox:author", 
                             xmldom.documentElement, nsresolver,
                             XPathResult.ORDERED_NODE_SNAPSHOT_TYPE, null);
alert(result.snapshotLength);
```

`DomXPathExample07.htm`

处理命名空间的第二种方法是定义一个接受命名空间前缀并返回关联URI的函数，如示例所示：

```javascript
var nsresolver = function(prefix){
    switch(prefix){
        case "wrox": return "http://www.wrox.com/";
        //其他
    }
};
var result = xmldom.evaluate("count(wrox:book/wrox:author)", 
                xmldom.documentElement, nsresolver, XPathResult.NUMBER_TYPE, null);
alert(result.numberValue);
```

`DomXPathExample08.htm`

当你不确定文档的哪个节点包含命名空间定义时，定义命名空间解析函数非常有帮助。只要知道前和URI，就可以返回这些信息，并将其作为第三参数传递给`evaluate()`。

## Internet Explorer 中的 XPath

XPath支持内置在Internet Explorer基于ActiveX的XML文档对象中，但在`DOMParser`返回的DOM对象中没有。要在Internet Explorer 9中使用XPath，必须使用ActiveX实现。该接口在每个节点上定义了两个额外方法：`selectSingleNode()`和`selectNodes()`。`selectSingleNode()`方法接受XPath模式，如果找到则返回第一个匹配节点，如果没有则返回`null`。例如：

![image](img/logo1.gif)

```javascript
var element = xmldom.documentElement.selectSingleNode("employee/name");
if (element !== null){
    alert(element.xml);
}
```

`IEXPathExample01.htm`

在这里，返回匹配"employee/name"的第一个节点。上下文节点是`xmldom.documentElement`，即调用`selectSingleNode()`的节点。由于该方法可能返回`null`值，因此在尝试使用节点方法之前，始终应该检查值是否为`null`。

`selectNodes()`方法也接受XPath模式作为参数，但它返回所有匹配模式的节点的`NodeList`（如果没有节点匹配，则返回一个零项的`NodeList`）。

```javascript
var elements = xmldom.documentElement.selectNodes("employee/name");
alert(elements.length);
```



### IEXPathExample02.htm

在此示例中，所有匹配`"employee/name"`的元素都将以`NodeList`的形式返回。由于不存在返回空值的可能，你可以安全地开始使用该结果。请记住，由于结果是一个`NodeList`，它是一个动态集合，每次访问时都会不断更新。

Internet Explorer 对 XPath 的支持非常基础。无法获取节点或`NodeList`以外的结果类型。

#### Internet Explorer 中的命名空间支持

要在 Internet Explorer 中处理包含命名空间的 XPath 表达式，你需要知道你正在使用哪些命名空间，并按照以下格式创建一个字符串：

```
"xmlns:prefix1='uri1' xmlns:prefix2='uri2' xmlns:prefix3='uri3'"
```

然后，必须将此字符串传递给 Internet Explorer 中 XML DOM 对象的特殊方法`setProperty()`，该方法接受两个参数：要设置的属性名称和属性值。在这种情况下，属性名为`"SelectionNamespaces"`，值为之前提到的格式的字符串。因此，可以使用以下代码来评估 DOM XPath 命名空间示例中使用的 XML 文：

![image](img/logo1.gif)

```
xmldom.setProperty("SelectionNamespaces", "xmlns:wrox='http://www.wrox.com/'");

var result = xmldom.documentElement.selectNodes("wrox:book/wrox:author");            

alert(result.length); 
```

### IEXPathExample03.htm

与 DOM XPath 示例一样，未提供命名空间解析信息会导致在评估表达式时产生错误。

#### 跨浏览器 XPath

由于 Internet Explorer 中的 XPath 功能非常有限，跨浏览器 XPath 使用必须保持在 Internet Explorer 可以执行的评估范围内。这本质上意味着要使用 DOM Level 3 XPath 对象在其他浏览器中重建`selectSingleNode()`和`selectNodes()`方法。第一个函数是`selectSingleNode()`，它接受三个参数：上下文节点、XPath 表达式以及可选的命名空间对象。命名空间对象应该是如下形式的字面量：

```
{
    prefix1: "uri1",
    prefix2: "uri2",
    prefix3: "uri3"
}
```

通过这种方式提供命名空间信息，可以轻松转换为特定浏览器的命名空间解析格式。`selectSingleNode()`的完整代码如下：

```
function selectSingleNode(context, expression, namespaces){
    var doc = (context.nodeType != 9 ? context.ownerDocument : context);
    if (typeof doc.evaluate != "undefined"){
        var nsresolver = null;
        if (namespaces instanceof Object){
            nsresolver = function(prefix){
                return namespaces[prefix];
            };
        }
        var result = doc.evaluate(expression, context, nsresolver, 
                                  XPathResult.FIRST_ORDERED_NODE_TYPE, null);
        return (result !== null ? result.singleNodeValue : null);
    } else if (typeof context.selectSingleNode != "undefined"){
        //create namespace string
        if (namespaces instanceof Object){
            var ns = "";
            for (var prefix in namespaces){
                if (namespaces.hasOwnProperty(prefix)){
                    ns += "xmlns:" + prefix + "='" + namespaces[prefix] + "' ";
                }
            }
            doc.setProperty("SelectionNamespaces", ns);
        }
        return context.selectSingleNode(expression);
    } else {
        throw new Error("No XPath engine found.");
    }
}
```

### CrossBrowserXPathExample01.htm

该函数的第一步是确定要在哪个 XML 文档上评估表达式。由于上下文节点可以是文档，有有检查`nodeType`属性。变量`doc`在执行此检查后持有 XML 文档的引用。此时，你可以检查文档是否存在`evaluate()`方法，这表示支持 DOM Level 3 XPath。如果支持，下一步是检查是否传递了命名空间对象。这是通过使用`instanceof`运算符完成的，因为`typeof`对空值和对象会返回`"object"`。变量`nsresolver`被初始化为`null`，如果有命名空间信息，则用一个函数覆盖它。该函数是一个闭包，使用传入的命名空间对象来返回命名空间 URI。之后，调用`evaluate()`方法并检查结果，以确定在返回值之前是否返回了节点。

该函数的 Internet Explorer 分支检查上下文节点上是否存在`selectSingleNode()`方法。与 DOM 分支一样，第一步是为选择构建命名空间信息。如果传递了命名空间对象，则遍历其属性以创建适当格式的字符串。请注意使用`hasOwnProperty()`方法，以确保对`Object.prototype`的任何修改都不会被此函数获取。然后调用原生的`selectSingleNode()`方法并返回结果。

如果两种方法都不支持，则函数将抛出一个错误，指示没有可用的 XPath 引擎。`selectSingleNode()`函数用法如下：

![image](img/logo1.gif)

```
var result = selectSingleNode(xmldom.documentElement, "wrox:book/wrox:author", 
                              { wrox: "http://www.wrox.com/" }); 
alert(serializeXml(result)); 
```

### CrossBrowserExample01.htm

跨浏览器`selectNodes()`函数是以非常相似的方式创建的。它与`selectSingleNode()`函数接收相同的三个参数，大部分逻辑也是相似的。为了方便阅读，以下显示了函数之间的差异：

```
function selectNodes(context, expression, namespaces){
    var doc = (context.nodeType != 9 ? context.ownerDocument : context);
    if (typeof doc.evaluate != "undefined"){
        var nsresolver = null;
        if (namespaces instanceof Object){
            nsresolver = function(prefix){
                return namespaces[prefix];
            };
        }
        var result = doc.evaluate(expression, context, nsresolver, 
                                  XPathResult.ORDERED_NODE_SNAPSHOT_TYPE, null);
        var nodes = new Array();
        if (result !== null){
            for (var i=0, len=result.snapshotLength; i < len; i++){
                nodes.push(result.snapshotItem(i));
            }
        }
        return nodes;
    } else if (typeof context.selectNodes != "undefined"){
        //create namespace string
        if (namespaces instanceof Object){
            var ns = "";
            for (var prefix in namespaces){
                if (namespaces.hasOwnProperty(prefix)){
                    ns += "xmlns:" + prefix + "='" + namespaces[prefix] + "' ";
                }
            }
            doc.setProperty("SelectionNamespaces", ns);
        }
        var result = context.selectNodes(expression);
        var nodes = new Array();
        for (var i=0,len=result.length; i < len; i++){
            nodes.push(result[i]);
        }
        return nodes;
    } else {
        throw new Error("No XPath engine found.");
    }
}
```

如你所见，许多逻辑与`selectSingleNode()`相同。在代码的 DOM 部分，使用了一个有序快照结果类型并将其存储在数组中。为了匹配 Internet Explorer 的实现，即使没有找到结果，该函数也应该返回一个数组，因此始终返回`nodes`数组。在代码的 Internet Explorer 分支中，调用了`selectNodes()`方法，并将结果复制到数组中。由于 Internet Explorer 返回的是`NodeList`，最好将节点复制到数组中，这样无论使用哪种浏览器，函数返回类型都是相同的。该函数可以如下所示使用：

![image](img/logo1.gif)

```
var result = selectNodes(xmldom.documentElement, "wrox:book/wrox:author", 
                              { wrox: "http://www.wrox.com/" });            
alert(result.length); 
```

CrossBrowserXPathExample02.htm

为了获得最佳的跨浏览器兼容性，最好在 JavaScript 中专门使用这两个方法进行 XPath 处理。

## 浏览器对 XSLT 的支持

XSLT 是 XML 的辅助技术，它利用 XPath 将一个文档表示转换为另一个。与 XML 和 XPath 不同，XSLT 没有与之关联的正式 API，而且完全没有体现在正式 DOM 中。这导致浏览器厂商以自己的方式来实现支持。第一个在 JavaScript 中添加 XSLT 处理的浏览器是 Internet Explorer。

### Internet Explorer 中的 XSLT

与 Internet Explorer 中的其他 XML 功能一样，XSLT 支持是通过使用 ActiveX 对象提供的。从`MSXML 3.0`（随 Internet Explorer 6 发行）开始，可以通过 JavaScript 获得完整的 XSLT 1.0 支持。在 Internet Explorer 9 中，对于使用`DOMParser`创建的 DOM 文档不支持 XSLT。

### 简单的 XSLT 转换

使用 XSLT 样式表转换 XML 文档的最简单方法是将每个加载到 DOM 文档中，然后使用`transformNode()`方法。该方法存在于文档中的每个节点上，并接受单个参数，即包含 XSLT 样式表的文档。`transformNode()`方法返回一个包含转换结果的字符串。这是一个示例：

![image](img/logo1.gif)

```
// 加载 XML 和 XSLT (IE 特有)
xmldom.load("employees.xml");
xsltdom.load("employees.xslt");

// 转换
var result = xmldom.transformNode(xsltdom);
```

IEXsltExample01.htm

此示例加载了一个带有 XML 的 DOM 文档和一个带有 XSLT 样式表的 DOM 文档。然后对 XML 文档节点上调用`transformNode()`并传入 XSLT。变量`result`然后被由转换产生的字符串填充。注意，转换是从文档节点级别开始的，因为`transformNode()`是在该处调用的。XSLT 转换也可以通过在你想开始转换的节点上调用`transformNode()`在文档的任何地方进行。这是一个示例：

```
result = xmldom.documentElement.transformNode(xsltdom);
result = xmldom.documentElement.childNodes[1].transformNode(xsltdom);
result = xmldom.getElementsByTagName("name")[0].transformNode(xsltdom);
result = xmldom.documentElement.firstChild.lastChild.transformNode(xsltdom);
```

如果你在文档元素以外的任何地方调用`transformNode()`，则从该位置开始转换。然而，XSLT 样式表仍然可以访问该节点所在的完整 XML 文档。

### 复杂的 XSLT 转换

`transformNode()`方法提供了基础的 XSLT 转换能力，但还有更复杂的使用该语言的方法。要这样做，你必须使用 XSL 模板和 XSL 处理器。第一步是将 XSLT 样式表加载到线程安全的 XML 文档版本中。这是通过使用`MSXML2.FreeThreadedDOMDocument` ActiveX 对象实现的，它支持与 Internet Explorer 中普通 DOM 文档相同的所有接口。该对象也需要使用最新版本创建。例如：

```
function createThreadSafeDocument(){
    if (typeof arguments.callee.activeXString != "string"){
        var versions = ["MSXML2.FreeThreadedDOMDocument.6.0", 
                        "MSXML2.FreeThreadedDOMDocument.3.0",
                        "MSXML2.FreeThreadedDOMDocument"],
            i, len;
        for (i=0,len=versions.length; i < len; i++){
            try {
                new ActiveXObject(versions[i]);
                arguments.callee.activeXString = versions[i];
                break;
            } catch (ex){
                // skip
            }
        }
    }
    return new ActiveXObject(arguments.callee.activeXString);
}
```

IEXsltExample02.htm

除了签名不同，使用线程安全的 XML DOM 文档与使用普通类型相同，所示：



`var xsltdom = createThreadSafeDocument();`

`xsltdom.async = false;`

`xsltdom.load("employees.xslt");`

在创建并加载自由线程 DOM 文档后，必须将其分配给 XSL 模板，这是另一个 ActiveX 对象。该模板用于创建 XSL 处理器对象，该处理器对象随后可以用于转换 XML 文档。再次，必须创建最新版本，如下：

![image](img/logo1.gif)

```
function createXSLTemplate(){

    if (typeof arguments.callee.activeXString != "string"){

        var versions = ["MSXML2.XSLTemplate.6.0", 

                        "MSXML2.XSLTemplate.3.0",

                        "MSXML2.XSLTemplate"],

            i, len;

        for (i=0,len=versions.length; i < len; i++){

            try {

                new ActiveXObject(versions[i]);

                arguments.callee.activeXString = versions[i];

                break;

            } catch (ex){

                // skip

            }

        }

    }

    return new ActiveXObject(arguments.callee.activeXString);

}
```

等等，我指的是：

`IEXsltExample02.htm`

你可以使用 `createXSLTemplate()` 函数创建最新版本的对象，如下所示：

```
var template = createXSLTemplate();

template.stylesheet = xsltdom;

var processor = template.createProcessor();

processor.input = xmldom;

processor.transform();

var result = processor.output;
```

创建 XSL 处理器时，必须将要转换的节点分配给 `input` 属性。该值可以是文档或文档中的任何节点。调用 `transform()` 执行转换并将结果存储在 `output` 属性中（字符串形式）。这段代码重复了 `transformNode()` 提供的功能。

![image](img/pen.gif)

XSL 模板对象的 3.0 和 6.0 版本之间存在显著差异。在 3.0 中，`input` 属性必须是完整的文档；使用节点会抛出错误。在 6.0 中，你可以使用文档中的任何节点。

此样式表定义了一个名为 `message` 的参数，然后将该参数输出到转换结果中。要设置 `message` 的值，你需要在调用 `transform()` 之前使用 `addParameter()` 方法。`addParameter()` 方法接受两个参数：要设置的参数名称（如 `<xsl:param>` 的 `name` 属性所示）以及要分配的值（通常是字符串，但也可以数字或布尔值）。以下是一个示例：

![image](img/logo1.gif)

```
processor.input = xmldom.documentElement;

processor.addParameter("message", "Hello World!");

processor.transform();
```

`IEXsltExample03.htm`

当你为参数设置一个值时，输出将反映该值。

XSLT 处理器的另一个高级功能是设置运行模式（mode）的能力。在 XSLT 中，可以使用 `mode` 属性为模板定义模式。当定义了模式后，除非在使用 `<xsl:apply-templates>` 时使用了匹配的 `mode` 属性，否则该模板不会运行。请考虑以下示例：

```xml
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">

    <xsl:output method="html" />

    <xsl:param name="message" />

    <xsl:template match="/">

       <ul>

           <xsl:apply-templates select="*" />

       </ul>

       <p>Message: <xsl:value-of select="$message" /></p>

    </xsl:template>

    <xsl:template match="employee">

        <li><xsl:value-of select="name" />, <em><xsl:value-of select="@title" /></em></li>

    </xsl:template>

    <xsl:template match="employee" mode="title-first">

        <li><em><xsl:value-of select="@title" /></em>, <xsl:value-of select="name" /></li>

    </xsl:template>

</xsl:stylesheet>
```

`employees3.xslt`

此样式表定义了一个模板，其 `mode` 属性被设置为 `"title-first"`。在该模板内部，首先输出员工的职位，然后输出员工姓名。为了使用此模板，`<xsl:apply-templates>` 元素的 `mode` 也必须设置为 `"title-first"`。如果你使用此样式表，默认情况下它的输出与上一个相同，先显示员工姓名，后显示职位。然而，如果你使用此样式表并通过 JavaScript 将 `mode` 设置为 `"title-first"`，它将首先输出员工的职位。可以在 JavaScript 中使用所示的 `setStartMode()` 方法来实现：

![image](img/logo1.gif)

```
processor.input = xmldom;

processor.addParameter("message", "Hello World!");  

processor.setStartMode("title-first");              

processor.transform(); 
```

`IEXsltExample05.htm`

`setStartMode()` 方法仅接受一个参数，即要为处理器设置的模式。与 `addParameter()` 一样，这必须在 `transform()` 之前调用。

如果你打算使用同一个样式表进行多次转换，你可以在每次转换后重置处理器。当你调用 `reset()` 方法时，输入和输出属性会被清空，同时起始模式和任何指定的参数也会被清除。该方法的语法如下：

```
processor.reset();   //为下一次使用做准备
```

由于处理器已经编译了 XSLT 样式表，因此进行重复转换比使用 `transformNode()` 更快。

![image](img/pen.gif)

MSXML 仅支持 XSLT 1.0。由于微软的重心已转向 .NET Framework，MSXML 的开发已经停止。预计在未来的某个时刻，JavaScript 将能够访问 XML 和 XSLT .NET 对象。

## XSLTProcessor 类型

Mozilla 在 Firefox 中通过创建一个新类型实现了对 XSLT 的 JavaScript 支持。`XSLTProcessor` 类型允许开发者以类似于 Internet Explorer 中 XSL 器的方式，使用 XSLT 转换 XML 文档。自首次实现以来，Chrome、Safari 和 Opera 都复制了该实现，使 `XSLTProcessor` 成为 JavaScript 支持 XSLT 转换的事实标准。

与 Internet Explorer 的实现一样，第一步是加载两个 DOM 文档，一个包含 XML，另一个包含 XSLT。之后，创建一个新的 `XSLTProcessor` 并使用 `importStylesheet()` 方法将 XSLT 赋值给它，如示例所示：

```
var processor = new XSLTProcessor()

processor.importStylesheet(xsltdom);
```

`XsltProcessorExample01.htm`

最后一步是执行转换。这可以通过两种方式完成。如果你想返回一个完整的 DOM 文档作为结果，调用 `transformToDocument()`。你也可以通过调用 `transformToFragment()` 获取一个文档碎片对象作为结果。通常来说，使用 `transformToFragment()` 的唯一理由是你打算将结果添加到另一个 DOM 文档中。

使用 `transformToDocument()` 时，只需传入 XML DOM 并结果作为另一个完全不同的 DOM 即可。这是一个示例：

![image](img/logo1.gif)

```
var result = processor.transformToDocument(xmldom);

alert(serializeXml(result));
```

`XsltProcessorExample01.htm`

`transformToFragment()` 方法接受两个参数：要转换的 DOM 以及应该拥有结果碎片的文档。这确保了新碎片在目标文档是有效的。因此，你可以通过传递 `document` 作为第二个参数来创建碎片并添加到页面。考虑以下示例：

```
var fragment = processor.transformToFragment(xmldom, document);

var div = document.getElementById("div");

div.appendChild(fragment);
```

`XsltProcessorExample02.htm`

在这里，处理器创建了一个属于文档的碎片。这将碎片添加到页面上的 `<div>` 元素。

当 XSLT 样式表的输出格式为 `"xml"` 或 `"html"` 时，创建文档或碎片是有意义的。但当输出格式为 `"text"` 时，你通常只需要转换的结果。遗憾的是，没有直接返回文本的方法。当输出为 `"text"` 时调用 `transformToDocument()` 会返回一个 XML 文档，但该文档的内容在浏览器之间不同。例如，Safari 返回整个 HTML 文档，而 Opera 和 Firefox 返回包含文本的单元素文档。

解决方案是调用 `transformToFragment()`，它返回一个包含结果文本的文档碎片。因此，你可以通过以下代码获取文本：

```
var fragment = processor.transformToFragment(xmldom, document);

var text = fragment.firstChild.nodeValue;

alert(text);
```

这段代码在每个支持的浏览器中工作方式相同，并能正确返回转换的文本输出。

## 使用参数

`XSLTProcessor` 还允许使用 `setParameter()` 设置 XSLT 参数，该方法接受三个参数：命名空间 URI、参数本地名称和要设置的值。通常，命名空间 URI 为 `null`，本地名称即为参数名称。此方法必须在调用 `transformToDocument()` 或 `transformToFragment()` 之前调用。这是一个示例：

```
var processor = new XSLTProcessor()

processor.importStylesheet(xsltdom);

processor.setParameter(null, "message", "Hello World!");

var result = processor.transformToDocument(xmldom);
```

`XsltProcessorExample03.htm`

还有两个与参数的方法：`getParameter()` 和 `removeParameter()`，分别用于获取的当前值和移除参数值。每个方法都接收命名空间 URI（再次通常为 `null`）和参数的本地名称。例如：

```javascript
var processor = new XSLTProcessor()

processor.importStylesheet(xsltdom);

processor.setParameter(null, "message", "Hello World!");

alert(processor.getParameter(null, "message"));    //outputs "Hello World!"

processor.removeParameter(null, "message");

var result = processor.transformToDocument(xmldom);
```

这些方法并不经常使用，主要是为了方便起见提供的。

### 重置处理器

每个 `XSLTProcessor` 实例都可以多次重用，用于对不同 XSLT 样式表的转换。`reset()` 方法会移除处理器中所有的参数和样式表，允许你再次调用 `importStylesheet()` 来加载不同的 XSLT 样式表，如下例所示：

```javascript
var processor = new XSLTProcessor()

processor.importStylesheet(xsltdom);

// 执行一些转换

processor.reset();

processor.importStylesheet(xsltdom2);

// 执行更多转换
```

在使用多个样式表执行转换时，复用单个 `XSLTProcessor` 可以节省内存。

### 跨浏览器 XSLT

Internet Explorer 的 XSLT 转换与 `XSLTProcessor` 方法非常不同，因此重建每个方法中所有可用功能是不现实的。XSLT 转换最简单的跨浏览器技术是返回字符串结果。对于 Internet Explorer，这意味着只需在上下文节点上调用 `transformNode()`，而其他浏览器需要对 `transformToDocument()` 操作的结果进行序列化。以下函数可以在 Internet Explorer、Firefox、Chrome、Safari 和 Opera 中使用：

![image](img/logo1.gif)

```javascript
function transform(context, xslt){

    if (typeof XSLTProcessor != "undefined"){

        var processor = new XSLTProcessor();

        processor.importStylesheet(xslt);

        var result = processor.transformToDocument(context);

        return (new XMLSerializer()).serializeToString(result);

    } else if (typeof context.transformNode != "undefined") {

        return context.transformNode(xslt);

    } else {

        throw new Error("No XSLT processor available.");

    }

}
```

`CrossBrowserXsltExample01.htm`

`transform()` 函数接受两个参数：执行转换的上下文节点和 XSLT 文档对象。首先，代码检查 `XSLTProcessor` 类型是否定义，如果是，则使用它来处理转换。调用 `transformToDocument()` 方法并将结果序列化为字符串返回。如果上下文节点具有 `transformNode()` 方法，则使用该方法返回结果。与本章中的其他跨浏览器函数一样，如果没有可用的 XSLT 处理器，`transform()` 将抛出一个错误。该函数的使用方法如下：

```javascript
var result = transform(xmldom, xsltdom);
```



使用 Internet Explorer 的`transformNode()`方法可以确保你不需要使用线程安全的 DOM 文档进行转换。

![image](img/pen.gif)

请注意，由于浏览器中的 XSLT 引擎不同，从转换中得到的结果在不同浏览器之间可能会存在微小或巨大的差异。你永远不要依赖于 JavaScript 中 XSLT 的绝对转换结果。

## 总结

JavaScript 对 XML 及相关技术有大量的支持。遗憾的是，由于早期缺乏规范，通用功能有多种实现。DOM Level 2 提供了创建空 XML 文档的 API，但没有提供解析或序列化。由于缺乏这些功能，浏览器厂商开始创建自己的方法。Internet Explorer 采取了以下方法：

* Internet Explorer 通过 ActiveX 对象引入了 XML 支持，这些对象同样可以用于构建桌面应用程序。
* `MSXML`库随 Windows 一起发布，并可以通过 JavaScript 访问。
* 该库包含了对基础 XML 解析、序列化的支持，以及对 XPath 和 XSLT 等补充技术的支持。

另一方面，Firefox 实现了以下两种新类型来处理 XML 解析和序列化：

* `DOMParser`类型是一个简单的对象，用于将 XML 字符串解析为 DOM 文档。
* `XMLSerializer`类型执行相反的操作，将 DOM 文档序列化为 XML 字符串。

由于这些对象的简单性和流行，Internet Explorer 9、Opera、Chrome 和 Safari 都复制了这些功能，这些类型已成为 Web 开发中事实上的标准。

DOM Level 3 引入了 XPath API 的规范，Firefox、Safari、Chrome 和 Opera 均已实现它。该 API 允许 JavaScript 对 DOM 文档运行任何 XPath 查询，并无论数据类型如何都能检索结果。Internet Explorer 以两种方法的形式实现了自己的 XPath 支持：`selectSingleNode()`和`selectNodes()`。尽管比 DOM Level 3 API 限制得多，但这些方法提供了基本的 XPath 功能，用于定位 DOM 文档中的节点或节点集。

最后一种相关技术是 XSLT，它没有定义其用法 API 的公共规范。Firefox 创建了`XSLTProcessor`类型通过 JavaScript 处理转换，并很快被 Safari、Chrome 和 Opera 效仿。Internet Explorer 实现了自己的解决方案，既通过简单的`transformNode()`方法，也通过更复杂的模板/处理器方法。

XML 现在在 Internet Explorer、Firefox、Chrome、Safari 和 Opera 中都得到了良好支持。尽管 Internet Explorer 与其他浏览器之间的实现差异巨大，但仍存在足够的共性来创建合理的跨浏览器功能。

# 第 19 章：用于 XML 的 ECMAScript

### 本章内容简介

* E4X 引入的额外类型
* 使用 E4X 进行 XML 操作
* 语法变化

2002 年，由 BEA Systems 领导的团体建议对 ECMAScript 进行扩展以添加原生 XML 支持。2004 年 6 月，ECMAScript for XML（E4X）作为 ECMA-357 发布，并在 2005 年 12 月进行了修订。E4X 并不是一门独立的语言，而是 ECMAScript 的一种可选扩展。作为扩展，E4X 引入了处理 XML 的新语法，以及针对 XML 的对象。

尽管浏览器采用速度缓慢，但 Firefox 1.5 及更高版本几乎支持整个 E4X 标准。本章关注 Firefox 的实现。

### E4X 类型

作为 ECMAScript 的扩展，E4X 引入了以下全局类型：

* `XML` —— XML 结构的任何单个部分
* `XMLList` —— XML 对象集合
* `Namespace` —— 命名空间前缀与命名空间 URI 映射
* `QName` —— 由本地名称和命名空间 URI 组成的限定名称

通过这四种类型，E4X 能够通过将每个类型（特别是`XML`和`XMLList`）映射到多个 DOM 类型来表示 XML 文档。

### XML 类型

`XML`类型是 E4X 引入的最重要的新类型，因为它可以表示 XML 结构的任何单个部分。`XML`实例可以是元素、属性、注释、处理指令或文本节点。`XML`类型继承自`Object`类型，因此它继承了所有对象的默认属性和方法。有几种方法可以创建新的 XML 对象，第一种是像这样调用构造函数：

```javascript
var x = new XML();
```

此行代码创建了一个可以填充数据的 XML 对象。你也可以向构造函数传递 XML 字符串，如下例所示：

```javascript
var x = new XML("<employee position=\"Software Engineer\"><name>Nicholas Zakas</name></employee>");
```

传递构造函数的 XML 字符串将被解析为 XML 对象层次结构。此外，你还可以将 DOM 文档或节点传递给构造函数并以 E4X 形式表示其数据：

```javascript
var x = new XML(xmldom);
```

尽管这些构造方法非常有用，但最强大且有趣的方法是通过 XML 字面量（XML literal）将 XML 数据直接赋值给变量。XML 字面量只是嵌入到 JavaScript 代码中的 XML 代码。这里有一个示例：

![image](img/logo1.gif)

```javascript
var employee = <employee position="Software Engineer">
                    <name>Nicholas C. Zakas</name>
               </employee>;
```

`XMLTypeExample01.htm`

在这里，XML 数据结构被直接赋值给变量。这种增强语法创建了一个 XML 对象并将其赋值给`employee`变量。

![image](img/pen.gif)

Firefox 对 E4X 的实现不支持解析 XML 序言（prologs）。如果`<?xml version="1.0"?>`出现在传递给 XML 构造函数的文本中，或者作为 XML 字面量的一部分，就会发生语法错误。

`toXMLString()`方法返回表示该对象及其子元素的 XML 字符串。相比之下，`toString()`方法的行为根据 XML 对象的内容而不同。如果内容是简单的（纯文本），则返回文本；否则`toString()`的行为与`toXMLString()`相同。考虑以下示例：

```javascript
var data = <name>Nicholas C. Zakas</name>;
alert(data.toString());     //"Nicholas C. Zakas"
alert(data.toXMLString());  //"<name>Nicholas C. Zakas</name>"
```

在这两种方法之间可以满足大多数 XML 序列化需求。

### XMLList 类型

`XMLList`类型表示 XML 对象的有序集合。`XMLList`的 DOM 等价物是`NodeList`，尽管`XML`和`XMLList`之间的差异与`Node`和`NodeList`之间的差异刻意得很小。要显式创建一个新的`XMLList`对象，你可以使用以下`XMLList`构造函数：

```javascript
var list = new XMLList();
```

与 XML 构造函数一样，你可以传递一个 XML 字符串进行解析。该字符串不需要包含单个根元素，如下代码所示：

```javascript
var list = new XMLList("<item/><item/>");
```

`XMLListTypeExample01.htm`

在这里，`list`变量被填充了一个包含两个 XML 对象的`XMLList`，每个`<item/>`元素对应一个。

一个`XMLList`对象也可以通过`+`运算符组合两个或多个 XML 对象来创建。该运算符在 E4X 中被重载以执行`XMLList`的创建，如下例所示：

```javascript
var list = <item/> + <item/>;
```

此示例使用`+`运算符将两个 XML 字面量组合成`XMLList`。使用特殊的`<>`和`</>`语法并省略`+`运算符也可以实现相同的效果，如下：

```javascript
var list = <><item/><item/></>;
```

虽然可以创建独立的`XMLList`对象，但它们通常作为解析较大 XML 结构的一部分而被创建。考虑以下：

![image](img/logo1.gif)

```javascript
var employees = <employees>
    <employee position="Software Engineer">
        <name>Nicholas C. Zakas</name>
    </employee>
    <employee position="Salesperson">
        <name>Jim Smith</name>
    </employee>
</employees>;
```

`XMLListTypeExample02.htm`

这段代码定义了一个`employees`变量，它变成了一个代表`<employees/>`元素的 XML 对象。由于有两个子`<employee/>`元素，因此创建了一个`XMLList`对象并存储在`employees.employee`中。可以使用括号表示法和其位置访问每个元素，如下：

```javascript
var firstEmployee = employees.employee[0]; 
var secondEmployee = employees.employee[1];
```

每个`XMLList`对象还有一个`length()`方法，返回它所包含的项的数量。例如：

```javascript
alert(employees.employee.length());   //2
```

注意`length()`是一个方法，而不是属性。这与数组和`NodeLists`有意之区别。

E4X 的一个有趣部分是刻意模糊了 XML 和`XMLList`类型之间的界限。事实上，XML 对象与包含单个 XML 对象的`XMLList`之间没有明显的区别。为了最小化这些差异，每个 XML 对象也有一个`length()`方法和一个通过`[0]`引用的属性（该属性返回 XML 对象本身）。

XML 和`XMLList`之间的兼容性使得 E4X 的使用变得更加容易，因为某些方法可能会返回其中一种类型。

`XMLList`对象的`toString()`和`toXMLString()`方法返回相同的字符串值，即它包含的所有 XML 对象的连接序列化结果。

### 命名空间类型

命名空间在 E4X 中通过`Namespace`对象表示。`Namespace`对象通常用于将命名空间前缀映射到命名空间 URI，尽管前缀并非总是必需。你可以如下使用`Namespace`构造函数创建`Namespace`对象：

```javascript
var ns = new Namespace();
```

你也可以使用 URI 或前缀和 URI 来初始化`Namespace`对象，如下：

![image](img/logo1.gif)

```javascript
var ns = new Namespace("http://www.wrox.com/");    //无前缀的命名空间
var wrox = new Namespace("wrox", "http://www.wrox.com/");  //wrox 命名空间
```

`NamespaceTypeExample01.htm`

`Namespace`对象中的信息可以通过`prefix`和`uri`属性获取，如下：

```javascript
alert(ns.uri);                //"http://www.wrox.com/"
alert(ns.prefix);             undefined
alert(wrox.uri);              //"http://www.wrox.com/"
alert(wrox.prefix);           //"wrox"
```

`NamespaceTypeExample01.htm`

每当没有赋值给`Namespace`对象时，其前缀属性被设置为 undefined。要创建默认命名空间，你应该将前缀设置为空字符串。

如果 XML 字面量包含命名空间或通过 XML 构造函数解析命名空间字符串，会自动创建一个`Namespace`对象。你可以通过`namespace()`方法并指定前缀来获取`Namespace`引用。考虑以下示例：

![image](img/logo1.gif)

```javascript
var xml = <wrox:root xmlns:wrox="http://www.wrox.com/">
            <wrox:message>Hello World!</wrox:message>
          </wrox:root>;
var wrox = xml.namespace("wrox");
alert(wrox.uri);
alert(wrox.prefix);
```

`NamespaceTypeExample02.htm`

在此示例中，包含命名空间的 XML 片段作为 XML 字面量创建的。通过`namespace("wrox")`可以获取来自`wrox`命名空间的`Namespace`对象，此后你可以访问`uri`和`prefix`属性。

`Namespace`对象的`toString()`方法始终返回命名空间 URI。

### QName 类型

`QName`类型表示 XML 对象的限定名，即命名空间和本地名的组合。你可以使用`QName`构造函数手动创建一个新的`QName`对象并传入名称或`Namespace`对象和名称，如下所示：

```javascript
var wrox = new Namespace("wrox", "http://www.wrox.com/");
var wroxMessage = new QName(wrox, "message");    //代表 "wrox:message"
```

`QNameTypeExample01.htm`

对象创建后，有两个可以访问的属性：`uri`和`localName`。`uri`属性返回创建对象时指定的命名空间（如果没有指定命名空间则返回空字符串），`localName`属性返回限定名的本地名部分，如下例所示：

```javascript
alert(wroxMessage.uri);        //"http://www.wrox.com/"
alert(wroxMessage.localName);  //"message"
```

`QNameTypeExample01.htm`

这些属性是只读的，尝试更改它们的值会产生错误。`QName`对象重写了`toString()`方法以返回`uri::localName`格式的字符串，例如上例中的“http://www.wrox.com/::message”。

在解析 XML 结构时，代表元素或属性的 XML 对象会自动创建`QName`对象。你可以使用 XML 对象的`name()`方法返回与该 XML 对象关联的`QName`引用，如下例所示：

![image](img/logo1.gif)

```javascript
var xml = <wrox:root xmlns:wrox="http://www.wrox.com/">
            <wrox:message>Hello World!</wrox:message>
          </wrox:root>;
var wroxRoot = xml.name();
alert(wroxRoot.uri);           //"http://www.wrox.com/"
alert(wroxRoot.localName);     //"root"
```

`QNameTypeExample02.htm`

即使没有指定命名空间信息，XML 结构中的每个元素和属性都会创建一个`QName`对象。

你可以通过使用`setName()`方法并传递一个新的`QName`对象来更改 XML 对象的限定名，如下所示：

```javascript
xml.setName(new QName("newroot"));
```

此方法通常用于更改元素的标签名，或者作为命名空间一部分的属性名。如果名称不属于命名空间，你可以简单地使用`setLocalName()`方法来更改本地名称：

```javascript
xml.setLocalName("newtagname");
```

## 通用用法

当 XML 对象、元素、属性和文本组合成一个对象层次结构时，你可以使用点表示法结合属性和标签名来导航该结构。每个子元素都表示为其父元素的一个属性，该属性名等于子元素的本地名称。如果该子元素仅包含文本，则每次访问该属性时都会返回该文本，如下例：

```javascript
var employee = <employee position="Software Engineer">
                    <name>Nicholas C. Zakas</name>
               </employee>;
```



`alert(employee.name);` //"Nicholas C. Zakas"

代码中的`<name/>`元素仅包含文本。该文本通过`employee.name`获取，它导航到`<name/>`元素并返回它。由于在传递给`alert`时隐式调用了`toString()`方法，`<name/>`中包含的文本会被显示。这种能力使得访问 XML 文档中包含的文本数据变得简单。如果有多个具有相同标签名的元素，则返回一个`XMLList`。考虑以下示例：

```
var employees = <employees>
    <employee position="Software Engineer">
        <name>Nicholas C. Zakas</name>
    </employee>
    <employee position="Salesperson">
        <name>Jim Smith</name>
    </employee>
</employees>;

alert(employees.employee[0].name);    //"Nicholas C. Zakas"
alert(employees.employee[1].name);    //"Jim Smith"
```

此示例访问每个`<employee/>`元素并输出它们的`<name/>`元素值。如果你不确定子元素的本地名称，或者你想无论名称如何都检索所有子元素，可以使用星号`*`，如下所示：

![image](img/logo1.gif)

```
var allChildren = employees.*;      //无论本地名称如何，返回所有子元素
alert(employees.*[0].name);         //"Nicholas C. Zakas"
```

### UsageExample01.htm

与其他属性一样，星号可能会返回单个`XML`对象或一个`XMLList`对象，这取决于 XML 结构。

`child()`方法的行为与属性访问完全相同。可以将任何属性名或索引传递给`child()`方法，它将返回相同的值。考虑此用例：

```
var firstChild = employees.child(0);           //与 employees.*[0] 相同
var employeeList = employees.child("employee");  //与 employees.employee 相同
var allChildren = employees.child("*");          //与 employees.* 相同
```

为了增加方便，提供了一个`children()`方法，它始终返回所有子元素。这是一个示例：

```
var allChildren = employees.children(); //与 employees.* 相同
```

还有一个`elements()`方法，它的行为与`child()`类似，不同之处在于它返回代表元素的`XML`对象。例如：

```
var employeeList = employees.elements("employee");  //与 employees.employee 相同
var allChildren = employees.elements("*");          //与 employees.* 相同
```

这些方法为 JavaScript 开发人员提供了一种更熟悉的语法来访问 XML 数据。

可以使用`delete`运算符删除子元素，如下所示：

```
delete employees.employee[0];
alert(employees.employee.length());   //1
```

这是将子节点视为属性的主要优势之一。

### 访问属性

也可以使用点表示法访问属性，尽管语法稍有扩展。为了区分属性名和子元素标签名，你必须在名称之前添加一个"at"字符（`@`）。这种语法借自`XPath`，`XPath`也使用`@`来区分属性和字符名称。结果是一种看起来稍微有点奇怪的语法，正如此示例所示：

![image](img/logo1.gif)

```
var employees = <employees>
    <employee position="Software Engineer">
        <name>Nicholas C. Zakas</name>
    </employee>
    <employee position="Salesperson">
        <name>Jim Smith</name>
    </employee>
</employees>;

alert(employees.employee[0].@position);  //"Software Engineer"
```

### AttributesExample01.htm

与元素一样，每个属性都表示为可以使用此简写符号访问的属性。代表属性的`XML`对象被返回，其`toString()`方法始终返回属性值。要获取属性名称，使用对象的`name()`方法。

你也可以使用`child()`方法通过在属性名称前加缀`@`来访问属性，如下所示：

```
alert(employees.employee[0].child("@position"))); //Software Engineer
```

由于任何`XML`对象属性名都可以用于`child()`，因此需要区分标签名和属性名。

可能可以使用`attribute()`方法并传入属性名称来仅访问属性。与`child()`不同，不需要在属性名称前加缀`@`。这是一个示例：

```
alert(employees.employee[0].attribute("position")); //Software Engineer
```

这三种访问属性的方法适用于`XML`和`XMLList`类型。用于`XML`对象时，返回代表该属性的`XML`对象；用于`XMLList`对象时，返回一个`XMLList`。在之前的示例中，`employees.employee.@position`将返回一个包含两个对象的`XMLList`——一个是第一个`<employee/>`元素的位置属性，一个是第二个。

要检索`XML`或`XMLList`对象中的所有属性，可以使用`attributes()`方法。该方法返回代表所有属性的`XMLList`。这与使用`@*`模式相同，如示例所示：

```
//两行代码都获取所有属性
var atts1 = employees.employee[0].@*;
var atts2 = employees.employee[0].attributes();
```

在 E4X 中更改属性值与更改属性值一样简单。只需像这样给属性赋值一个新值：

```
employees.employee[0].@position = "Author"; //更改位置属性
```

更改随后会反映在内部，因此当你序列化 XML 对象时，属性值会被更新。同样的技术也可用于添加新属性，如下例所示：

```
employees.employee[0].@experience = "8 years"; //添加经验属性
employees.employee[0].@manager = "Jim Smith"; //添加经理属性
```

由于属性表现像任何其他 ECMAScript 属性一样，你还可以使用`delete`运算符来删除属性：

```
delete employees.employee[0].@position; //删除位置属性
```

属性的属性访问使得与底层 XML 结构的交互变得非常简单。

### 其他节点类型

E4X 能够表示 XML 文档的所有部分，包括注释和处理指令。默认情况下，E4X 不解析注释或处理指令，因此它们不会显示在对象层次结构中。若要强制解析器识别它们，你必须在`XML`构造函数上设置以下两个属性：

```
XML.ignoreComments = false;
XML.ignoreProcessingInstructions = false;
```

设置这些标志后，E4X 将会将注释和处理指令解析到 XML 结构中。

由于`XML`类型代表了所有的节点类型，因此需要一种方法来区分它们。`nodeKind()`方法指示 XML 对象代表什么种类型的节点，并返回 "text"、"element"、"comment"、"processing-instruction" 或 "attribute"。考虑以下 XML 对象：

![image](img/logo1.gif)

```javascript
var employees = <employees>
    <?Dont forget the donuts?>
    <employee position="Software Engineer">
        <name>Nicholas C. Zakas</name>
    </employee>
    <!-- just added -->
    <employee position="Salesperson">
        <name>Jim Smith</name>
    </employee>
</employees>;
```

给定此 XML，下表显示了`nodeKind()`的返回值，取决于哪个节点在作用域内。

| STATEMENT | RETURNS |
| --- | --- |
| `employees.nodeKind()` | "element" |
| `employees.*[0].nodeKind()` | "processing-instruction" |
| `employees.employee[0].@position.nodeKind()` | "attribute" |
| `employees.employee[0].nodeKind()` | "element" |
| `employees.*[2].nodeKind()` | "comment" |
| `employees.employee[0].name.*[0].nodeKind()` | "text" |

`nodeKind()`方法不能在包含多个 XML 对象的`XMLList`上调用；若如此操作将抛出错误。

可以使用以下方法之一来仅获取特定类型的节点：

*   `attributes()` — 返回 XML 对象的所有属性。
*   `comments()` — 返回 XML 对象的所有子注释。
*   `elements(tagName)` — 返回 XML 对象的所有子元素。你可以通过提供想要返回的元素的`tagName`来过滤结果。
*   `processingInstructions(name)` — 返回 XML 对象的所有子处理指令。你可以通过提供要返回的处理指令的`name`来过滤结果。
*   `text()` — 返回 XML 对象的所有文本节点节点。

这些方法每个都返回一个包含相应 XML 对象的`XMLList`。

你可以使用`hasSimpleContent()`和`hasComplexContent()`方法来判断 XML 对象是仅包含文本还是更复杂的内容。如果子节点只有文本节点，则前者返回`true`，而如果存在任何非文本节点的子节点，则后者返回`true`。这里有一个示例：

```javascript
alert(employees.employee[0].hasComplexContent());   //true
alert(employees.employee[0].hasSimpleContent());    //false
alert(employees.employee[0].name.hasComplexContent());   //false
alert(employees.employee[0].name.hasSimpleContent());    //true
```

当这些方法与其他方法结合使用时，可以帮助在 XML 结构中查询相关数据。

### 查询

事实上，E4X 提供了一种在许多方面与 XPath 相似的查询语法。获取元素或属性值的简单操作是一种基础类型的查询。表示 XML 结构各个部分的 XML 对象直到进行查询时才被创建。实际上，`XML`或`XMLList`对象的所有属性都仅仅是查询的一部分。这意味着引用一个不代表 XML 结构部分的属性仍然返回一个`XMLList`，只是它里面没有任何。例如，如果对之前的 XML 示例运行以下代码，将不会返回任何内容：

![image](img/logo1.gif)

```javascript
var cats = employees.cat;
alert(cats.length());     //0 
```

QueryingExample01.htm

此查询在`<employees/>`下寻找`<cat/>`元素。第一行返回一个没有任何内容的`XMLList`。这种行为允许进行查询而不必担心发生异常。

之前的示例大部分涉及使用使用点表示法来处理节点的直接子节点。你可以使用两个点将查询扩展到所有后代，如下所示：

```javascript
var allDescendants = employees..*;     //获取 <employees/> 的所有后代
```

在这段代码中，返回了`<employees/>`元素的所有后代。结果限制为元素、文本、注释和处理指令，后两者的包含仅取决于`XML`构造函数上指定的标志（在前节中讨论过）；将不会包含属性。要仅获取特定标签名称的元素，请将星号替换为实际的标签名称如下：

```javascript
var allNames = employees..name;       //获取 <employees/> 的所有 <name/> 后代
```

可以使用`descendants()`方法执行相同的查询。在不带任何参数使用时，该方法返回所有后代（这与使用`..*`相同），你也可以提供名称作为参数来限制结果。以下是两者的示例：

```javascript
var allDescendants = employees.descendants();     //所有后代
var allNames = employees.descendants("name");     //所有 <name/> 后代
```

可以使用以下任一方法获取所有后代的属性：

```javascript
var allAttributes = employees..*;             //获取后代的所有属性
var allAttributes2 = employees.descendants("*"); //相同
```

就像元素一样，你可以通过提供完整名称而不是星号来限制结果。例如：

```javascript
var allAttributes = employees..@position; //获取位置属性
var allAttributes2 = employees.descendants("@position");
```

除了访问后代，你还可以指定一个必须满足的条件。例如，为了返回位置属性为 "salesperson" 的`<employee/>`元素，可以使用以下查询：

```javascript
var salespeople = employees.employee.(@position == "Salesperson");
```

这种语法也可用于更改 XML 结构的部分。例如，只需以下一行即可将第一个销售员的位置属性更改为 "Senior Salesperson"：

```javascript
employees.employee.(@position == "Salesperson")[0].@position= "Senior Salesperson";
```

注意括号中的表达式返回一个`XMLList`，因此括号返回写入`@position`属性的项目。

你可以使用`parent()`方法返回 XML 结构，该方法返回 XML 对象父节点的 XML 对象。如果在`XMLList`上调用，`parent()`方法返回列表中所有对象的共同父。考虑此示例：

```javascript
var employees2 = employees.employee.parent();
```

在这里，`employees2`变量的值与`employees`变量相同。`parent()`方法在处理未知来源的 XML 对象时最有用。

### XML 构建与操作

将 XML 数据获取到 XML 对象有许多选择。如之前所述，你可以将 XML 字符串传递给`XML`构造函数或使用 XML 字面量。通过在大括号`{}`中嵌入 JavaScript 变量，可以使 XML 字面量变得有用。变量可以使用 XML 字面量中的任何地方，如下例：

![image](img/logo1.gif)

```javascript
var tagName = "color";
var color = "red";
var xml = <{tagName}>{color}</{tagName}>;
alert(xml.toXMLString());    "<color>red</color>"
```




## XML 构造示例

`XMLConstructionExample01.htm`

在这段代码中，XML 字面量的标签名和文本值都是通过使用大括号插入变量来指定的。这种能力使得无需字符串拼接即可构建 XML 结构变得简单。

E4X 还使得使用标准的 JavaScript 语法来构建整个 XML 结构变得非常简单。如前所述，大多数操作都是查询，即使元素或属性不存在，也不会抛出错误。更进一步，如果你给一个不存在的元素或属性赋值，E4X 会先创建底层的结构，然后执行赋值。以下是一个示例：

```javascript
var employees = <employees/>;

employees.employee.name = "Nicholas C. Zakas";

employees.employee.@position = "Software Engineer";
```

`XMLConstructionExample02.htm`

此示例从一个 `<employees/>` 元素开始并在此基础上构建。第二行创建了一个 `<employee/>` 元素并在内部创建一个 `<name/>` 元素，并分配了文本值。下一行添加了 `position` 属性并为其分配了值。最后，结构如下：

```xml
<employees>
    <employee position="Software Engineer">
        <name>Nicholas C. Zakas</name>
    </employee>
</employees>
```

可以使用 `+` 运算符添加第二个 `<employee/>` 元素，如下所示：

![image](img/logo1.gif)

```javascript
employees.employee += <employee position="Salesperson">
                          <name>Jim Smith</name>
                      </employee>;
```

`XMLConstructionExample02.htm`

这将导致最终的 XML 结构如下：

```xml
<employees>
    <employee position="Software Engineer">
        <name>Nicholas C. Zakas</name>
    </employee>
    <employee position="Salesperson">
        <name>Jim Smith</name>
    </employee>
</employees>
```

除了这种基础的 XML 构建语法外，还可以使用以下类似 DOM 的方法：

- `appendChild(child)` — 将给定的子节点附加到代表节点子节点的 `XMLList` 的末尾。
- `copy()` — 返回 `XML` 对象的副本。
- `insertChildAfter(refNode, child)` — 在代表节点子节点的 `XMLList` 中 `refNode` 之后插入 `child`。
- `insertChildBefore(refNode, child)` — 在代表节点子节点的 `XMLList` 中 `refNode` 之前插入 `child`。
- `prependChild(child)` — 将给定的子节点插入到代表节点子节点的 `XMLList` 的开头。
- `replace(propertyName, value)` — 用给定的 `value` 替换名为 `propertyName` 的属性（属性可能是元素或属性）。
- `setChildren(children)` — 用 `children` 替换所有当前子节点，`children` 可以是一个 `XML` 对象或一个 `XMLList` 对象。

这些方法非常有用且易于使用。以下代码说明了其中一些方法：

![image](img/logo1.gif)

```javascript
var employees = <employees>
    <employee position="Software Engineer">
        <name>Nicholas C. Zakas</name>
    </employee>
    <employee position="Salesperson">
        <name>Jim Smith</name>
    </employee>
</employees>;

employees.appendChild(<employee position="Vice President">
                     <name>Benjamin Anderson</name>
                 </employee>);

employees.prependChild(<employee position="User Interface Designer">
                     <name>Michael Johnson</name>
                  </employee>);

employees.insertChildBefore(employees.child(2),
                            <employee position="Human Resources Manager">
                                <name>Margaret Jones</name>
                            </employee>);

employees.setChildren(<employee position="President">
                         <name>Richard McMichael</name>
                      </employee> +
                      <employee position="Vice President">
                          <name>Rebecca Smith</name>
                      </employee>);
```

`XMLConstructionExample03.htm`

首先，代码在员工列表的底部添加了一个名为 Benjamin Anderson 的副总裁。其次，在员工列表的顶部添加了一个名为 Michael Johnson 的用户界面设计师。第三，将一个名为 Margaret Jones 的人力资源经理添加在位置为 2 的员工之前，此时位置 2 的员工是 Jim Smith（因为现在 Michael Johnson 和 Nicholas C. Zakas 都在他前面）。最后，所有子节点都被替换为总统 Richard McMichael 和新副总裁 Rebecca Smith。生成的 XML 如下所示：

```xml
<employees>
    <employee position="President">
        <name>Richard McMichael</name>
    </employee>
    <employee position="Vice President">
        <name>Rebecca Smith</name>
    </employee>
</employees>
```

使用这些技术和方法，你可以使用 E4X 执行任何 DOM 风格的操作。

## 解析与序列化选项

E4X 解析和序列化数据的方式由 XML 构造函数上的几个设置来控制。以下三个设置与 XML 解析有关：

- `ignoreComments` — 表示解析器应该忽略标记中的注释。默认设置为 `true`。
- `ignoreProcessingInstructions` — 表示解析器应该忽略标记中的处理指令。默认设置为 `true`。
- `ignoreWhitespace` — 表示解析器应该忽略元素之间的空白字符，而不是创建文本节点来表示它们。默认设置为 `true`。

这三个设置会影响传递给 XML 构造函数的 XML 字符串以及 XML 字面量的解析。

此外，以下两个设置与 XML 数据的序列化有关：

- `prettyIndent` — 表示在序列化 XML 时每个缩进使用的空格数。默认为 2。
- `prettyPrinting` — 表示 XML 应以易于读的格式输出，每个元素单独占一行并缩进。默认设置为 `true`。

这些设置会影响 `toString()` 和 `toXML()` 的输出。可以通过 `settings()` 方法获取一个设置对象，如下所示：

![image](img/logo1.gif)

```javascript
var settings = XML.settings();

alert(settings.ignoreWhitespace); //true

alert(settings.ignoreComments);   //true
```

`ParsingAndSerialization01.htm`

通过将对象传递给 `setSettings()` 方法可以一次分配多个设置。当你想要临时更改设置时如下所示：

```javascript
var settings = XML.settings();

XML.prettyIndent = 8;

XML.ignoreComments = false;

//进行一些处理

XML.setSettings(settings); //还原到之前的设置
```

始终可以使用 `defaultSettings()` 方法获取包含默认设置的对象，因此你可以随时使用以下行重置设置：

```javascript
XML.setSettings(XML.defaultSettings());
```

## 命名空间

E4X 使用命名空间非常方便。如之前所述，可以使用 `namespace()` 方法获取特定前的 Namespace 对象。你可以使用 `setNamespace()` 方法并传入 Namespace 对象来为给元素设置命名空间。这里有一个示例：

```javascript
var messages = <messages>
    <message>Hello world!</message>
</messages>;

messages.setNamespace(new Namespace("wrox", "http://www.wrox.com/"));
```

当调用 `setNamespace()` 时，命名空间仅应用于调用它的元素。序列化 `messages` 变量的结果如下：

```xml
<wrox:messages xmlns:wrox="http://www.wrox.com/">
    <message>Hello world!</message>
</wrox:messages>
```

由于调用了 `setNamespace()`，`<messages/>` 元素带有 wrox 命名空间缀，而 `<message/>` 元素保持不变。

要在不更改元素的情况下添加命名空间声明，请使用 `addNamespace()` 方法并传入 Namespace 对象，如下所示：

```javascript
messages.addNamespace(new Namespace("wrox", "http://www.wrox.com/"));
```

当此代码应用于原始的 `messages` XML 时，将创建如下 XML 结构：

```xml
<messages xmlns:wrox="http://www.wrox.com/">
    <message>Hello world!</message>
</messages>
```

通过调用 `removeNamespace()` 并传入一个 `Namespace` 对象，可以移除具有给定命名名前缀和 URI 的命名空间声明；不需要传递代表该命名空间的精确 `Namespace` 对象。请考虑此示例：

```javascript
messages.removeNamespace(new Namespace("wrox", "http://www.wrox.com/"));
```

这段代码移除了 `wrox` 命名空间。请注意，引用该前缀的限定名（qualified names）不会受到影响。

有两种方法可以返回与节点相关的 `Namespace` 对象的数组。第一个方法是 `namespaceDeclarations()`，它返回在给定节点上声明的所有命名空间的数组。第二个方法是 `inScopeNamespaces()`，它返回在给定节点作用范围内的所有命名空间的数组，这意味着它们要么在节点本身上声明，要么在祖先节点上声明。考虑此示例：

```javascript
var messages = <messages xmlns:wrox="http://www.wrox.com/">
    <message>Hello world!</message>
</messages>;

alert(messages.namespaceDeclarations());    //"http://www.wrox.com"

alert(messages.inScopeNamespaces());        //",http://www.wrox.com"

alert(messages.message.namespaceDeclarations());    ""

alert(messages.message.inScopeNamespaces());        //",http://www.wrox.com"
```

在这里，当调用 `namespaceDeclarations()` 时，`<message/>` 元素返回包含一个命名空间的数组；当调用 `inScopeNamespaces()` 时，返回包含两个命名空间的数组。这两个作用域内的命名空间是默认命名空间（用空字符串表示）和 `wrox` 命名空间。当在 `<message/>` 元素上这些方法时，`namespaceDeclarations()` 返回空数组，而 `inScopeNamespaces()` 返回相同。

`Namespace` 对象还可以通过双冒号（`::`）查询 XML 结构中特定命名空间下的元素。例如，要检索 `wrox` 命名空间中的所有 `<message/>` 元素，可以使用以下代码：

```javascript
var messages = <messages xmlns:wrox="http://www.wrox.com/">
    <wrox:message>Hello world!</wrox:message>
</messages>;

var wroxNS = new Namespace("wrox", "http://www.wrox.com/");

var wroxMessages = messages.wroxNS::message;
```

双冒号表示返回的元素应该存在的命名空间。请注意，使用的是 JavaScript 变量名，而不是命名空间前缀。

你还可以为给定作用范围内创建的所有 XML 对象设置默认命名空间。要这样做，请使用默认 xml namespace 语句并分配 `Namespace` 对象或简单的命名空间 URI。这是一个示例：

```javascript
default xml namespace = "http://www.wrox.com/";

function doSomething(){

    // 仅为此函数设置默认命名空间

    default xml namespace = new Namespace("your", "http://www.yourdomain.com");

}
```

全局作用范围的默认 XML 命名空间未设置。当给定作用范围内的所有 XML 数据都使用特定命名空间时，此语句非常有用，可以避免频繁引用命名空间本身。

## 其他更改

为了与标准的 ECMAScript 无缝协作，E4X 对基础语言进行了更改。其中一项更改是引入了 `for-each-in` 循环。与遍历每个属性并返回属性名的 `for-in` 循环不同，`for-each-in` 循环遍历每个属性并返回属性的值，如下示例所示：

![image](img/logo1.gif)

```javascript
var employees =  <employees>
                    <employee position="Software Engineer">
                        <name>Nicholas C. Zakas</name>
                    </employee>
                    <employee position="Salesperson">
                        <name>Jim Smith</name>
                    </employee>
                </employees>;

for each (var child in employees){
    alert(child.toXMLString());
}
```

`ForEachInExample01.htm`

此示例中的 `for-each-in` 循环用 `<employees/>` 的每个子节点填充 `child` 变量，这些可能包括注释、处理指令和/或文本节点。除非你使用属性的 `XMLList`（如下所示），否则循环中不会返回属性：

```javascript
for each (var attribute in employees.@*){ // 遍历属性
    alert(attribute);
}
```

尽管 `for-each-in` 循环被定义为 E4X 的一部分，但它也可以用于普通的数组和对象，如下所示：




`var colors = ["red","green","blue"];`

```
for each(var color in colors){
    alert(color);
}
```

`ForEachInExample01.htm`

对于数组，`for-each-in` 循环返回每个数组项。对于非 XML 对象，它返回每个属性的值。

`E4X` 还增加了一个全局函数 `isXMLName()`，它接受一个字符串，并在该名称是元素或属性的有效本地名时返回 `true`。这是为了给开发者提供便利，因为他们可能会使用未知的字符串数据来构建 XML 数据结构。这是一个示例：

```
alert(isXMLName("color"));        //true
alert(isXMLName("hello world"));  //false
```

如果你不确定应作为本地名的字符串来源，最好先使用 `isXMLName()` 来确定该字符串是否有效或是否会导致错误。

曾有一段时间，`XML` 是互联网传输结构化数据的默认标准。网络服务的首次迭代很大程度上基于 `XML`，这突显了其服务器到服务器通信的目标。然而，`XML` 并非没有反对者。有些人认为这种语言过于冗长且多余。虽然出现了一些解决方案来应对这些问题，但 Web 已经开始向新的方向发展。

`Douglas Crockford` 在 2006 年首次将 JavaScript 对象表示（`JSON`）规范为 `IETF RFC 4627`，尽管它在 2001 年就已经被使用了。`JSON` 是 JavaScript 的严格子集，利用 JavaScript 中发现的几种模式来表示结构化数据。`Crockford` 提出 `JSON` 是在 JavaScript 中访问结构化数据的更好替代方案，因为它可以直接传递给 `eval()` 且不需要创建 `DOM`。

理解 `JSON` 最重要的一点是它是一种数据格式，而不是一种编程语言。尽管 `JSON` 与 JavaScript 共享语法，但它并不是 JavaScript 的一部分。`JSON` 也不仅供 JavaScript 使用，因为它是一种数据格式。许多编程语言中都提供了相应的解析器和序列化器。

## 语法

`JSON` 语法允许表示三种类型的值：

*   简单值 — 字符串、数字、`Booleans` 和 `null` 都可以用与 JavaScript 相同的语法在 `JSON` 中表示。不支持特殊值 `undefined`。
*   对象 — 第一种复杂数据类型，对象表示有序的键值对。每个值可以可以是原始类型，也可以是复杂类型。
*   数组 — 第二种复杂数据类型，数组表示一个可以通过数字索引访问的有序值列表。值可以是任何类型，包括简单值、对象甚至其他数组。

`JSON` 中没有变量、函数或对象实例。`JSON` 核心在于表示结构化数据，尽管它与 JavaScript 共享语法，但不应将其与 JavaScript 范式混淆。

### 简单值

在最简单的形式下，`JSON` 表示少数几个简单值。例如，以下是有效的 `JSON`：

```
5
```

这是表示数字 5 的 `JSON`。同样，以下也是表示字符串的有效 `JSON`：

```
"Hello world!"
```

JavaScript 字符串与 `JSON` 字符串之间的巨大区别在于，`JSON` 字符串必须使用双引号才有效（使用单引号会导致语法错误）。

`Boolean` 值和 `null` 作为独立的 `JSON` 恰恰是有效的。但在实践中，`JSON` 最常用于表示更复杂的数据结构，其中简单值仅代表整体信息的一个部分。

## 对象

对象使用对象字面量表示法的略微修改来表示。JavaScript 中的对象字面量看起来像这样：

```
var person = {
    name: "Nicholas",
    age: 29
};
```

虽然这是开发者创建对象字面量的标准方式，但 `JSON` 中使用的是带引号属性格式。以下与之前的示例完全相同：

```
var object = {
    "name": "Nicholas",
    "age": 29
};
```

该相同对象的 `JSON` 表示为：

```json
{
    "name": "Nicholas",
    "age": 29
}
```

与 JavaScript 示例有几处不同。首先，没有变量声明（`JSON` 中不存在变量）。其次，没有尾随分号（因为这不是 JavaScript 语句，不需要分号）。再次强调，属性名周围的引号是使其成为有效 `JSON` 的必须。值可以是任何简单或复杂值，允许您在对象中嵌入对象，例如：

```json
{
    "name": "Nicholas",
    "age": 29,
    "school": {
        "name": "Merrimack College",
        "location": "North Andover, MA"
    }
}
```

此示例将学校信息嵌入顶层对象中。尽管有两个名为 "name" 的属性，但它们位于两个不同的对象中，因此是允许的。你应该避免在同一个对象中有两个同名的属性。

与 JavaScript 不同，`JSON` 中的对象属性名必须始终使用双引号。手动编写 `JSON` 时不带这些双引号或使用单引号是一个常见的错误。

### 数组

`JSON` 中的第二种复杂类型是数组。`JSON` 中使用 JavaScript 的数组字面量表示表示数组。例如，这是 JavaScript 中的一个数组：

```javascript
var values = [25, "hi", true];
```

你可以使用相似的语法在 `JSON` 中表示相同的数组：

```json
[25, "hi", true]
```

再次注意缺少变量或分号。数组和对象可以一起使用表示更复杂的数据集合，例如：

```json
[
    {
        "title": "Professional JavaScript",
        "authors": [
            "Nicholas C. Zakas"
        ],
        "edition": 3,
        "year": 2011
    },
    {
        "title": "Professional JavaScript",
        "authors": [
            "Nicholas C. Zakas"
        ],
        "edition": 2,
        "year": 2009
    },
    {
        "title": "Professional Ajax",
        "authors": [
            "Nicholas C. Zakas",
            "Jeremy McPeak",
            "Joe Fawcett"
        ],
        "edition": 2,
        "year": 2008
    },
    {
        "title": "Professional Ajax",
        "authors": [
            "Nicholas C. Zakas",
            "Jeremy McPeak",
            "Joe Fawcett"
        ],
        "edition": 1,
        "year": 2007
    }
]
```

## 解析与序列化

`JSON` 的兴起并不一定是因为它使用了熟悉的语法。更多是因为数据可以被解析为 JavaScript 对象。这与 `XML` 形成了鲜明对比，`XML` 被解析为 `DOM`，使得 JavaScript 开发者提取数据相当麻烦。例如，上一节中的 `JSON` 代码包含一个书籍列表，你可以轻松地获取第三本书的标题：

```javascript
books[2].title
```

这假设数据结构存储在变量 `books` 中。将其与典型的 `DOM` 遍历对比：

```javascript
doc.getElementsByTagName("book")[2].getAttribute("title")
```

考虑到所有额外的方法调用，`JSON` 在 JavaScript 开发者中变得如此流行并不意外。之后，`JSON`成为了网络服务的默认标准。

### JSON 对象

早期的 `JSON` 解析器几乎仅仅是使用了 JavaScript 的 `eval()` 函数。由于 `JSON` 是 JavaScript 语法的子集，`eval()` 可以解析、解释并返回数据 JavaScript 对象和数组。ECMAScript 5 将 JSON 解析形式化为名为 `JSON` 的原生全局对象。该对象支持 Internet Explorer 8+、Firefox 3.5+、Safari 4+、Chrome 和 Opera 10.5+。旧浏览器的 shim 可以在 [`github.com/douglascrockford/JSON-js`](https://github.com/douglascrockford/JSON-js) 找到。在旧浏览器中评估 JSON 时，重要的是不要单独使用 `eval()`，因为存在执行代码的风险。对于没有原生 JSON 解析的浏览器，`JSON` shim 是最佳选择。

`JSON` 对象有两个方法：`stringify()` 和 `parse()`。在简单用法下，这些方法分别将 JavaScript 对象序列化为 JSON 字符串，并将 JSON 解析为原生 JavaScript 值。例如：

![image1](img/logo1.gif)

```
var book = {
               title: "Professional JavaScript",
                authors: [
                    "Nicholas C. Zakas"
                ],
                edition: 3,
                year: 2011
           };
var jsonText = JSON.stringify(book);
```

### JSONStringifyExample01.htm

此示例使用 `JSON.stringify()` 将 JavaScript 对象序列化为 JSON 字符串并将其存储在 `jsonText` 中。默认情况下，`JSON.stringify()` 输出的 JSON 字符串不包含额外的空格或缩进，因此存储在 `jsonText` 中的值为：

```
{"title":"Professional JavaScript","authors":["Nicholas C. Zakas"],"edition":3,
"year":2011}
```

在序列化 JavaScript 对象时，所有的函数和原型成员都会被刻意地从结果中排除。此外，任何值值为 `undefined` 的属性也会被跳过。你将只剩下属于 JSON 数据类型之一的实例属性的表示。

JSON 字符串可以直接传递给 `JSON.parse()`，它会创建一个相应的 JavaScript 值。例如，你可以使用以下代码创建一个与 `book` 对象类似的对象：

```
var bookCopy = JSON.parse(jsonText);
```

注意，`book` 和 `bookCopy` 是两个独立的对象，尽管它们共享相同的属性，它们之间没有任何关系。

如果传递给 `JSON.parse()` 的文本不是有效的 JSON，则会抛出错误。

### 序列化选项

`JSON.stringify()` 方法除了要序列化的对象外，实际上接收两个参数。这些参数允许你指定序列化 JavaScript 对象的替代方法。第一个参数是过滤器，可以是数组或函数；第二个参数是用于生成的 JSON 字符串的缩进选项。单独使用或结合使用时，它们为控制 JSON 序列化提供了非常实用的功能。

#### 过滤结果

如果参数是一个数组，那么 `JSON.stringify()` 将仅包含在数组列出的对象属性。考虑以下情况：

![image](img/logo1.gif)

```
var book = {
               "title": "Professional JavaScript",
                "authors": [
                    "Nicholas C. Zakas"
                ],
                edition: 3,
                year: 2011
           };
var jsonText = JSON.stringify(book, ["title", "edition"]);
```

### JSONStringifyExample01.htm

`JSON.stringify()` 的第二个参数是一个包含两个字符串的数组："title" 和 "edition"。这些对应于被序列化对象的属性，因此只有这些属性会出现在生成的 JSON 字符串中：

```
{"title":"Professional JavaScript","edition":3}
```

当第二个参数是一个函数时，行为略有不同。提供的函数接收两个参数：属性键名（key）和属性值（value）。你可以查看键名来决定如何处理该属性。键始终是一个字符串，但如果某个值不是键值对的一部分，它可能是一个空字符串。

为了更改对象的序列化结果，请返回应该包含在该键中的值。请记住，返回 `undefined` 将导致该属性从结果中删除。这里有一个示例：

![image](img/logo1.gif)

```
var book = {
               "title": "Professional JavaScript",
                "authors": [
                    "Nicholas C. Zakas"
                ],
                edition: 3,
                year: 2011
           };
var jsonText = JSON.stringify(book, function(key, value){
    switch(key){
        case "authors":
            return value.join(",")
        case "year":
            return 5000;
        case "edition":
            return undefined;
        default:
            return value;
    }
});
```

### JSONStringifyExample02.htm

该函数根据键进行过滤。"authors" 键从数组转换为字符串，"year" 键被设置为 5000，而 "edition" 键通过返回 `undefined` 被完全移除。提供一个返回传入值的默认行为是重要的，这样所有其他值都将传递到结果中。此函数的第一次调用中，key 实际上等于空字符串，且 value 被设置为 `book` 对象。生成的 JSON 字符串为：

```
{"title":"Professional JavaScript","authors":"Nicholas C. Zakas","year":5000}
```

请记住，过滤器应用于待序列化对象中包含的所有对象，因此一个包含这些属性的多个对象的数组将导致每个对象只包含 "title" 和 "edition" 属性。

Firefox 3.5–3.6 在 `JSON.stringify()` 的实现中存在一个 bug，当使用函数作为第二个参数时会出现该问题。该函数只能作为过滤器：返回 `undefined` 意味着跳过该属性，而返回其他任何内容都会导致该属性被包含。此行为在 Firefox 4 中已修复。

#### 字符串缩进

`JSON.stringify()` 的第三个参数控制缩进和空格。当此参数为数字时，它代表每层缩进的空格数。例如，要让每层缩进四个空格，请使用以下：

![image](img/logo1.gif)

```
var book = {
               "title": "Professional JavaScript",
                "authors": [
                    "Nicholas C. Zakas"
                ],
                edition: 3,
                year: 2011
           };
var jsonText = JSON.stringify(book, null, 4);
```

### JSONStringifyExample03.htm

存储在 `jsonText` 中的字符串为：

```
{
    "title": "Professional JavaScript",
    "authors": [
        "Nicholas C. Zakas"
    ],
    "edition": 3,
    "year": 2011
}
```



你可能注意到`JSON.stringify()`也会向 JSON 字符串插入换行符以便阅读。这对于所有有效的缩进值都会发生。（没有换行的缩进并不常用。）数值缩进的最大值为 10；传入大于 10 的值设置为 10。

如果缩进参数不是数字而是字符串，则该字符串将作为 JSON 字符串的缩进字符。使用字符串，可以将缩进字符设置为任意内容，例如两个破折号：

```
var jsonText = JSON.stringify(book, null, " -");
```

此时`jsonText`的值变为：

```
{
--"title": "Professional JavaScript",
--"authors": [
----Nicholas C. Zakas"
--],
--"edition": 3,
--"year": 2011
}
```

如果使用的字符串超过十个字符，将被截断为前十个字符。

## toJSON 方法

有时对象需要`JSON.stringify()`无法实现的自定义序列化。在这种情况下，你可以为对象添加一个`toJSON()`方法，并让它返回自身的 JSON 表示。事实上，原生的`Date`对象拥有一个`toJSON()`方法，可以自动将 JavaScript`Date`对象转换为 ISO 8601 日期字符串（本质等同于对`Date`对象调用`ISOString()`）。

任何对象都可以添加`toJSON()`方法，例如：

```
var book = {
               "title": "Professional JavaScript",
                "authors": [
                    "Nicholas C. Zakas"
                ],
                edition: 3,
                year: 2011,
                toJSON: function(){
                    return this.title;
                }
           };

var jsonText = JSON.stringify(book);
```

### JSONStringifyExample05.htm

此代码在`book`对象上定义了一个`toJSON()`方法，该方法简单返回书籍标题。与`Date`对象类似，该对象被序列化为简单的字符串而不是对象。你可以从`toJSON()`返回任何序列化值，它将正常工作。返回`undefined`会导致当对象被嵌入另一个对象时，其值变为`null`；如果该对象是顶层的，则直接为`undefined`。

`toJSON()`方法除了过滤函数（filter function）之外还可以，因此理解序列化过程中各个部分执行的顺序非常重要。当一个对象传递给`JSON.stringify()`时，会执行以下步骤：

1. 如果可用，则调用`toJSON()`方法以获取实际值。否则，使用默认序列化方法。
2. 如果提供了第二个参数，则应用过滤器。传递给过滤函数的值将是第 1 步返回的值。
3. 对步骤 2 中的每个值都进行适当的序列化。
4. 如果提供了第三个参数，则进行适当的格式化。

在决定是创建一个`toJSON()`方法、使用过滤函数还是两者兼用时，理解这一顺序至关重要。

### 解析选项

`JSON.parse()`方法也接受一个额外的参数，该参数是一个在每个键值对上调用的函数。该函数被称为“还原函数”（reviver function），用以区别于`JSON.stringify()`接受的替换函数（replacer/filter function），尽管后者的格式完全相同：该函数接收两个参数，键（key）和值（value），并需要返回一个值。

如果还原函数返回`undefined`，则该键将从结果中移除；如果返回任何其他值，则该值将插入到结果中。还原函数的一个常见用途是将日期字符串转换为 Date 对象。例如：

```
var book = {
               "title": "Professional JavaScript",
                "authors": [
                    "Nicholas C. Zakas"
                ],
                edition: 3,
                year: 2011,
                releaseDate: new Date(2011, 11, 1)
           };

var jsonText = JSON.stringify(book);

var bookCopy = JSON.parse(jsonText, function(key, value){
    if (key == "releaseDate"){
        return new Date(value);
    } else {
        return value;
    }
});

alert(bookCopy.releaseDate.getFullYear());
```

`JSONParseExample02.htm`

这段代码从向`book`对象中添加一个`releaseDate`属性开始，该属性是一个`Date`。该对象被序列化以获得一个有效的 JSON 字符串，然后解析回对象`bookCopy`。还原函数寻找`"releaseDate"`键，并在找到时根据该字符串创建一个新的`Date`对象。生成的`bookCopy.releaseDate`属性随后是一个`Date`对象，因此可以调用`getFullYear()`方法。

## 总结

JSON 是一种轻量级数据格式，旨在轻松表示复杂的数据结构。该格式使用 JavaScript 法的子集来表示对象、数组、字符串、数字、`Booleans`和`null`。尽管 XML 可以处理相同的工作，但 JSON 更加简洁，且在 JavaScript 中有更好的支持。

ECMAScript 5 定义了一个原生`JSON`对象，用于将对象序列化为 JSON 格式以及将 JSON 数据解析为 JavaScript 对象。`JSON.stringify()`和`JSON.parse()`方法分别用于这两项操作。这两个方法都有许多选项，允许你更改默认行为以过滤或修改过程。

原生`JSON`对象在浏览器中得到了良好支持，包括 Internet Explorer 8+、Firefox 3.5+、Safari 4+、Opera 10.5 和 Chrome。

# 第 21 章：Ajax 和 Comet

### 本章内容

* 使用`XMLHttpRequest`对象
* 处理`XMLHttpRequest`事件
* 跨域 Ajax 限制

2005 年，Jesse James Garrett 编写了一篇名为《Ajax：Web 应用的新方法》的在线文章（[www.adaptivepath.com/ideas/essays/archives/000385.php](http://www.adaptivepath.com/ideas/essays/archives/000385.php)）。这篇文章概述了他称为 Ajax 的技术，它是 Asynchronous JavaScript+XML 的缩写。该技术包括在不卸载网页的情况下向服务器请求额外数据，从而提供更好的用户体验。Garrett 解释了如何使用这种技术来改变 Web 自诞生以来一直陷入的传统点击并等待范式。

推动 Ajax 发展的关键技术是`XMLHttpRequest`(XHR) 对象，它由微软发明，后被其他浏览器厂商复制。在引入`XHR`之前，Ajax 风格的通信必须通过许多黑科技来实现，主要使用隐藏的帧或`iframes`。`XHR`引入了一个用于创建服务器请求和评估响应的精简接口。这允许从服务器异步获取额外信息，意味着用户点击不需要刷新页面即可获取更多数据。相反，可以使用`XHR`对象获取数据，然后使用`DOM`将数据插入页面中。尽管名称中提到了 XML，但 Ajax 通信是格式无关的；该技术关于在不刷新页面的情况下从服务器获取数据，而不一定关于 XML。

Garrett 所指的 Ajax 技术实际上已经存在一段时间了。在 Garrett 文章之前，它通常被称为远程脚本（remote scripting），自 1998 年以来，通过不同的技术就可以实现这种浏览器-服务器通信。早期，可以通过 JavaScript 通过中间件（如 Java applet 或 Flash 电影）发送服务器请求。`XHR`对象为开发者带来了原生的浏览器通信能力，减少了实现结果所需的工作量。

更名为 Ajax 后，浏览器-服务器通信的流行在 2005 年底和 2006 年初爆发式增长。对 JavaScript 以及整个 Web 的重新关注带来了使用这些能力的新技术和模式。因此，`XHR`对象现在是每个 Web 开发者必备的工具。

### XMLHttpRequest 对象

Internet Explorer 5 是第一个引入 XHR 对象的浏览器。它是通过使用作为`MSXML`库一部分的`ActiveX`对象实现的。因此，浏览器中可以使用三个版本的 XHR 对象：`MSXML2.XMLHttp`、`MSXML2.XMLHttp.3.0`和`MSXML2.XMLHttp.6.0`。使用`MSXML`库使用 XHR 对象需要类似于第 18 章中创建文档的函数，如下：

```
//适用于 IE7 以前版本的函数
function createXHR(){
    if (typeof arguments.callee.activeXString != "string"){
        var versions = ["MSXML2.XMLHttp.6.0", "MSXML2.XMLHttp.3.0",
                        "MSXML2.XMLHttp"],
            i, len;
        for (i=0,len=versions.length; i < len; i++){
            try {
                new ActiveXObject(versions[i]);
                arguments.callee.activeXString = versions[i];
                break;
            } catch (ex){
                //skip
            }
        }
    }
    return new ActiveXObject(arguments.callee.activeXString);
}
```

此函数尝试创建 Internet Explorer 上可用的最新版本的 XHR 对象。

Internet Explorer 7+、Firefox、Opera、Chrome 和 Safari 都支持使用`XMLHttpRequest`构造函数创建原生 XHR 对象，如下：

```
var xhr = new XMLHttpRequest();
```

如果你只需要支持 Internet Explorer 7 及更高版本，可以放弃之前的函数，转而使用原生的 XHR 实现。相反，如果你必须扩展支持到更早版本的 Internet Explorer，则可以增强`createXHR()`函数以检查原生 XHR 对象，所示：

```
function createXHR(){
    if (typeof XMLHttpRequest != "undefined"){
        return new XMLHttpRequest();
    } else if (typeof ActiveXObject != "undefined"){
        if (typeof arguments.callee.activeXString != "string"){
            var versions = ["MSXML2.XMLHttp.6.0", "MSXML2.XMLHttp.3.0",
                            "MSXML2.XMLHttp"],
                i, len;
            for (i=0,len=versions.length; i < len; i++){
                try {
                    new ActiveXObject(versions[i]);
                    arguments.callee.activeXString = versions[i];
                    break;
                } catch (ex){
                    //skip
                }
            }
        }
        return new ActiveXObject(arguments.callee.activeXString);
    } else {
        throw new Error("No XHR object available.");
    }
}
```

`XHRExample01.htm`

该函数中的新代码首先检查原生的`XHR`对象，如果找到了则返回一个新实例。如果没有找到原生对象，则检查是否支持 ActiveX。如果这两种选项都不可用，则会抛出错误。你可以使用以下代码在所有浏览器中创建一个`XHR`对象：

```
var xhr = createXHR();
```

由于每个浏览器中的`XHR`实现都与原始的 Internet Explorer 版本兼容，你可以在所有浏览器中使用相同的方式使用创建的`xhr`对象。

# XHR 使用

要开始使用`XHR`对象，你首先需要调用`open()`方法，该方法接受三个参数：要发送的请求类型（"get"、"post" 等）、请求的`URL`以及一个指示请求是否应异步发送的布尔值。这里有一个示例：

```
xhr.open("get", "example.php", false);
```

这一行代码对`example.php`开启了一个同步 GET 请求。关于这段代码有几点需要注意。首先，`URL`相对于调用代码的页面路径，尽管也可以提供绝对路径。其次，`open()`的调用并没有真正发送请求；它只是准备好一个要发送的请求。

你只能访问存在同源上的 URL，这意味着相同的域名、相同的端口以及相同的协议。如果`URL`指定的任何一个项与发送请求的页面不同，则会抛出安全错误。

要发送指定的请求，你必须如下调用`send()`方法：

```
xhr.open("get", "example.txt", false);
xhr.send(null);
```

`XHRExample01.htm`

`send()`方法接受一个参数，即作为请求体发送的数据。如果不需要发送体数据，你必须传递`null`，因为某些浏览器要求必须传递此参数。一旦调用了`send()`，请求就会被发往服务器。

由于此请求是同步的，JavaScript 代码将等待响应返回后继续执行。当收到响应时，`XHR`对象的属性将被填充数据。相关属性如下：

* `responseText` — 作为响应体返回的文本。
* `responseXML` — 如果响应的内容为 "text/xml" 或 "application/xml"，则包含一个带有响应数据的 XML DOM 文档。
* `status` — 响应的 HTTP 状态。
* `statusText` — HTTP 状态的描述。

当接收到响应时，第一步是检查`status`属性以确保响应成功返回。通常情况下，200 的 HTTP 状态码被认为是成功的，如果内容类型正确，`responseText`中以及可能在`responseXML`中将会有可用内容。此外，状态码 304 表示资源未被修改并正在从浏览器缓存中提供，这也意味着响应是可用的。为了确保接收到正确的响应，你应该检查所有这些状态，如下所示：

```
xhr.open("get", "example.txt", false);
xhr.send(null);

if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
    alert(xhr.responseText);
} else {
    alert("Request was unsuccessful: " + xhr.status);
}
```



`XHRExample01.htm`

这段代码根据返回的状态码显示从服务器返回的内容或错误消息。建议始终检查`status`属性以确定最佳行动方案，并避免为此目的使用`statusText`，因为后者在不同浏览器中已证明是不可靠的。无论内容类型如何，`responseText`属性始终会被填充响应体，而对于非 XML 数据，`responseXML`将为`null`。

![image](img/pen.gif)

某些浏览器错误地报告了 204 状态码。Internet Explorer 中 ActiveX 版本的`XHR`在获取 204 时会将`status`设置为 1223，而 Internet Explorer 中的原生`XHR`对象会将 204 化为 200。Opera 在获取 204 时报告状态为 0。

虽然可以像这样进行同步请求，但大多数情况下最好使用异步请求，允许 JavaScript 代码继续执行而不等待响应。`XHR`对象有一个`readyState`属性，指示当前处于请求周期的阶段。可能的`readyState`值为：

* 0 — 未初始化。尚未调用`open()`方法。
* 1 — 已打开。已调用`open()`方法但尚未调用`send()`。
* 2 — 已发送。已调用`send()`方法但尚未收到响应。
* 3 — 接收中。已部分响应数据。
* 4 — 完成。响应数据均可用。

每当`readyState`从一个值变为另一个值时，就会触发`readystatechange`事件。你可以利用此机会检查`readyState`。通常情况下，感兴趣的唯一`readyState`是 4，表示数据已就绪。为了跨浏览器兼容，应在调用`open()`之前分配`onreadystatechange`处理器。考虑以下示例：

![image](img/logo1.gif)

```
var xhr = createXHR();

xhr.onreadystatechange = function(){

    if (xhr.readyState == 4){

        if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){

            alert(xhr.responseText);

        } else {

            alert("Request was unsuccessful: " + xhr.status);

        }

    }

};

xhr.open("get", "example.txt", true);

xhr.send(null);
```

`XAsyncExample01.htm`

# HTTP 头部

每个 HTTP 请求和响应都会带有一组头部信息，这些信息可能对开发者感兴趣。`XHR`对象通过多种方法暴露这两类头部信息——请求头部和响应头部。

默认情况下，当发送`XHR`请求时会发送以下头部：

- `Accept`: 浏览器可以处理的内容类型。
- `Accept-Charset`: 浏览器可以显示的字符集。
- `Accept-Encoding`: 浏览器处理的压缩编码。
- `Accept-Language`: 浏览器运行的语言。
- `Connection`: 浏览器与服务器建立的连接类型。
- `Cookie`: 页面上设置的任何 cookie。
- `Host`: 发起请求的页面域名。
- `Referer`: 发起请求的页面 URI。注意，该头部在 HTTP 规范中的拼写是错误的，为了兼容性，必须保持这种错误的拼写。（该词的正确拼写是“referrer”。）
- `User-Agent`: 浏览器的用户代理字符串。

虽然不同浏览器发送的精确请求头有所不同，但这些是通常会发送的头部。你可以通过`setRequestHeader()`方法设置额外的请求头。该方法接受两个参数：标头的名称和标头的值。为了发送请求头，必须在调用`open()`之后但`send()`之前调用`setRequestHeader()`，如下例所示：

![image](img/logo1.gif)

```
var xhr = createXHR();        

xhr.onreadystatechange = function(){

    if (xhr.readyState == 4){

        if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){

            alert(xhr.responseText);

        } else {

            alert("Request was unsuccessful: " + xhr.status);

        }

    }

};

xhr.open("get", "example.php", true);

xhr.setRequestHeader("MyHeader", "MyValue");

xhr.send(null);
```

`XHRRequestHeadersExample01.htm`

服务器可以读取这些自定义请求头以决定适当的操作。建议始终使用自定义头部名称，而不是浏览器通常发送的默认名称，因为使用默认头部可能会影响服务器的响应。某些浏览器允许覆盖默认头部，但另一些不允许。

你可以使用`getResponseHeader()`方法并传入要获取的头部名称，从`XHR`对象中获取响应头部。也可以使用`getAllResponseHeaders()`方法将所有头部作为一个长字符串获取。以下是这两种方法的示例：

```
var myHeader = xhr.getResponseHeader("MyHeader");

var allHeaders  xhr.getAllResponseHeaders();
```

头部可以用于从服务器向浏览器传递额外的结构化数据。`getAllResponseHeaders()`方法通常返回如下内容：

```
Date: Sun, 14 Nov 2004 18:04:03 GMT

Server: Apache/1.3.29 (Unix)

Vary: Accept

X-Powered-By: PHP/4.3.8

Connection: close

Content-Type: text/html; charset=iso-8859-1
```

此输出允许你解析响应头部以找到所有发送的头部名称，而不是逐个检查每个头部是否存在。

## GET 请求

最常见的请求类型是 GET，它通常在向服务器查询某些信息时发出。如有必要，可以将查询字符串（query-string）参数添加到 URL 的末尾以将信息传递给服务器。对于`XHR`，此查询字符串必须在传入`open()`方法的 URL 中存在并正确编码。

GET 请求中最常见的错误之一是查询字符串格式不正确。每个查询字符串的名称和值在附加到 URL 之前都必须使用`encodeURIComponent()`进行编码，并且所有的键值对必须用 ampersand（&）分隔，如下例所示：

```
xhr.open("get", "example.php?name1=value1&name2=value2", true);
```

以下函数帮助向现有 URL 的末尾添加查询字符串参数：

```
function addURLParam(url, name, value) {

    url += (url.indexOf("?") == -1 ? "?" : "&");

    url += encodeURIComponent(name) + "=" + encodeURIComponent(value);

    return url;   

}
```

`addURLParam()`函数接受三个参数：要添加参数的 URL、参数名称和参数值。首先，函数检查 URL 是否已经包含问号（以判断是否已存在其他参数）。如果没有，函数将添加一个问号；否则，添加一个 ampersand。接下来，对名称和值进行编码并附加到 URL 的末尾。最后一步是返回更新后的 URL。

此函数可以用于构建请求的 URL，如下例所示：

```
var url = "example.php";

//添加参数

url = addURLParam(url, "name", "Nicholas");

url = addURLParam(url, "book", "Professional JavaScript");

//发起请求

xhr.open("get", url, false);
```

在此处使用`addURLParam()`函数可以确保查询字符串格式正确，以便与`XHR`对象配合。

## POST 请求

第二常见的请求类型是 POST，它通常用于向服务器发送应该保存的数据。每个 POST 请求都预期以请求体的形式提交数据，而 GET 请求传统上不包含。POST 请求的主体可以包含大量数据，且这些数据可以是任何格式。你可以通过将`open()`方法的第一个参数指定为 post 来发起 POST 请求。例如：

```
xhr.open("post", "example.php", true);
```

第二部分是向`send()`方法传递某些数据。由于`XHR`最初设计主要用于处理 XML，你可以传入任何序列化并发送到服务器的字符串。默认情况下，POST 请求在服务器看来与表单提交相同。但你可以使用`XHR`模拟表单提交。如果页面上的表单需要序列化，请使用第 14 章的`serialize()`函数，如下所示：

![image](img/logo1.gif)

```
function submitData(){

    var xhr = createXHR();        

    xhr.onreadystatechange = function(){

        if (xhr.readyState == 4){

            if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){

                alert(xhr.responseText);

            } else {

                alert("Request was unsuccessful: " + xhr.status);

            }

        }

    };

    xhr.open("post", "postexample.php", true);

    xhr.setRequestHeader("Content-Type", "application/x-form-urlencoded");

    var form = document.getElementById("user-info");            

    xhr.send(serialize(form));

}
```

`XHRPostExample01.htm`

在此函数中，来自 ID 为 "user-info" 的表单数据被序列化并发送到服务器。PHP 文件`postexample.php`然后可以通过`$_POST`获取提交的数据。考虑此示例：

```php
<?php

    header("Content-Type: text/plain");   

    echo <<<EOF

Name: {$_POST['user-name']}

Email: {$_POST['user-email']}

EOF;

?>
```

`postexample.php`

如果不包含`Content-Type`头部，数据将不会出现在`$_POST`全局变量中——你需要使用`$HTTP_RAW_POST_DATA`来访问它。

![image](img/pen.gif)

POST 请求比 GET 请求有更多的开销。在性能方面，GET 请求发送相同数据的速度可以比 POST 请求快一倍。

## XMLHttpRequest LEVEL 2

`XHR`对象作为一种事实标准的流行，导致了 W3C 制定了官方规范来规范其行为。`XMLHttpRequest` Level 1 仅仅是定义了`XHR`对象已有的实现细节。`XMLHttpRequest` Level 2 则进一步演化了`XHR`对象。并不是所有浏览器都实现了 Level 2 规范的所有部分，但所有浏览器都实现了其中的部分功能。

### FormData 类型

现代 Web 应用中经常需要对表单进行序列化，因此`XMLHttpRequest` Level 2 规范引入了`FormData`类型。`FormData`类型可以轻松地对现有表单进行序列化，并创建与表单格式相同的数据，以便通过`XHR`传输。以下代码创建了一个`FormData`对象并填充了某些数据：

```
var data = new FormData();

data.append("name", "Nicholas");
```

`append()`方法接受两个参数：键（key）和值（value），本质上是表单字段的以及该字段包含的值。你可以根据需要添加任意数量的键值对。通过将表单元素传递给`FormData`构造函数，可以使用表单元素中存在的数据预填充键值对：

```
var data = new FormData(document.forms[0]);
```

一旦你有了`FormData`实例，就可以将其传递到`XHR`的`send()`方法中，例如所示：

![image](img/logo1.gif)

```
var xhr = createXHR();        

xhr.onreadystatechange = function(){

    if (xhr.readyState == 4){

        if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){

            alert(xhr.responseText);

        } else {

            alert("Request was unsuccessful: " + xhr.status);

        }

    }

};

xhr.open("post", "postexample.php", true);

var form = document.getElementById("user-info");            

xhr.send(new FormData(form));
```

`XHRFormDataExample01.htm`

`FormData`类型的便利之处之一是，你不需要显式地在`XHR`对象上设置任何请求头。`XHR`对象会识别传入的数据类型为`FormData`实例，并相应地配置请求头。

`FormData`类型在 Firefox 4+、Safari 5+、Chrome 以及 Android 3+ Web 中支持。

### 超时

在 Internet Explorer 8 中，`XHR`对象被扩展以包含一个`timeout`属性，该属性表示请求在中止前应等待响应的毫秒数。当`timeout`属性被设置为一个数字，且在指定的毫秒数内没有收到响应时，将触发一个超时事件并调用`ontimeout`事件处理程序。此功能后来被添加到`XMLHttpRequest` Level 2 规范中。这里有一个示例：

![image](img/logo1.gif)

```
var xhr = createXHR();

xhr.onreadystatechange = function(){

    if (xhr.readyState == 4){

        try {

            if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){

                alert(xhr.responseText);

            } else {

                alert("Request was unsuccessful: " + xhr.status);

            }

        } catch (ex){

            //假设已由 ontimeout 处理

        }

    }

};

xhr.open("get", "timeout.php", true);

xhr.timeout = 1000;  //设置 1 秒超时（仅限 IE 8+）

xhr.ontimeout = function(){

    alert("Request did not return in a second.");

};

xhr.send(null);
```



# XHRTimeoutExample01.htm

此示例说明了`timeout`属性的使用。将其设置为 1000 毫秒意味着如果请求在 1 秒或内没有返回，请求将被中止。当发生这种情况时，会调用`ontimeout`事件处理程序。`readyState`仍然变为 4，这意味着会调用`onreadystatechange`事件处理程序。但是如果你在超时发生后尝试访问`status`属性将会发生错误。为了防止这种情况，请将检查`status`属性的代码封装在`try-catch`语句中。

截至本文写作，Internet Explorer 8+ 仍然支持超时的浏览器。

## overrideMimeType() 方法

Firefox 首次引入`overrideMimeType()`作为覆盖`XHR`响应 MIME 类型的方法。这后来被添加到`XMLHttpRequest` Level 2 中。由于响应返回的 MIME 类型决定了`XHR`对象如何处理响应，因此拥有一种覆盖服务器返回类型的方法是非常用的补充。

考虑这种情况：服务器发送了`text/plain`的 MIME 类型，但实际上包含 XML。这会导致`responseXML`属性为`null`，尽管数据实际上是 XML。通过调用`overrideMimeType()`，你可以确保响应被视为 XML 而不是纯文本：

```
var xhr = createXHR();

xhr.open("get", "text.php", true);

xhr.overrideMimeType("text/xml");

xhr.send(null);
```

此示例强制`XHR`对象将响应处理为 XML 而不是纯文本。调用`overrideMimeType()`必须在调用`send()`之前发生，以便正确覆盖响应的 MIME 类型。`overrideMimeType()`必须在调用`send()`之前发生，由于响应返回的 MIME 类型决定了`XHR`对象如何处理响应。`overrideMimeType()`方法在 Firefox、Safari 4+ 以及 Chrome 中支持。

## 进度事件 (PROGRESS EVENTS)

进度事件规范是定义客户端与服务器通信的事件。这些事件最初针对 XHR，但现在已进入类似的 API。这里有六种进度事件：

- `loadstart` —— 在接收到响应的首字节时触发。
- `progress` —— 在正在接收响应时反复触发。
- `error` —— 在尝试请求时发生错误时触发。
- `abort` —— 在调用`abort()`终止连接时触发。
- `load` —— 在响应完全接收时触发。
- `loadend` —— 在触发`error`、`abort`或`load`后通信完成后触发。

每个请求都从`loadstart`事件开始；随后是一个或多个`progress`事件；然后是`error`、`abort`或`load`；最后以`loadend`结束。前五个事件在 Firefox 3.5+、Safari 4+、Chrome、iOS Safari 以及 Android WebKit 中支持。Opera 11 仅支持`load`。目前没有浏览器支持`loadend`事件。

大多数这些事件都是直观的，但有两个需要注意的细微之处。

### load 事件

当 Firefox 首次实现 XHR 的版本时，它试图简化交互模型。为此，引入了`load`事件作为`readystatechange`事件的替代。`load`事件在响应完全接收时立即触发，消除了检查`readyState`属性的需求。`onload`事件处理程序接收事件对象，其`target`属性设置为`XHR`实例，并且从内部可以使用所有的`XHR`对象属性和方法。然而，并不是所有浏览器都正确实现了该事件的事件对象，因此需要使用`XHR`对象变量本身，如下例所示：

![image](img/logo1.gif)

```
var xhr = createXHR();

xhr.onload = function(){

    if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){

        alert(xhr.responseText);

    } else {

        alert("Request was unsuccessful: " + xhr.status);

    }

};

xhr.open("get", "altevents.php", true);

xhr.send(null);
```

XHRProgressEventExample01.htm

只要从服务器收到响应，无论状态如何，`load`事件都会触发。这意味着你必须检查`status`属性以确定是否有可用数据。`load`事件在 Firefox、Opera、Chrome 和 Safari 中支持。

Mozilla 的另一项 XHR 创新是进度事件（progress event），它会在浏览器接收新数据时定期触发。`onprogress`事件监听器会接收一个事件对象，其`target`是`XHR`对象，并包含三个额外的属性：`lengthComputable`，指示进度信息是否可用布尔值；`position`，表示已接收的字节数；以及`totalSize`，由`Content-Length`响应头定义的预期字节总数。通过这些信息，你可以为用户提供进度指示器。以下代码包含了如何实现此点的示例：

```
var xhr = createXHR();        

xhr.onload = function(event){

    if ((xhr.status >= 200 && xhr.status < 300) || 

            xhr.status == 304){

        alert(xhr.responseText);

    } else {

        alert("Request was unsuccessful: " + xhr.status);

    }

};

xhr.onprogress = function(event){

    var divStatus = document.getElementById("status");

    if (event.lengthComputable){

        divStatus.innerHTML = "Received " + event.position + " of " + 

            event.totalSize +

" bytes";

    }

};

xhr.open("get", "altevents.php", true);

xhr.send(null);
```

`XHRProgressEventExample01.htm`

为了正确执行，必须在调用`open()`之前附加`onprogress`事件处理器。在前面的示例中，每当进度事件触发时，HTML 元素都会填充状态信息。假设响应具有`Content-Length`头部，你还可以使用此信息来计算已接收响应的百分比。

# 跨源资源共享 (CORS)

通过`XHR`进行 Ajax 通信的主要局限之一是跨源安全策略。默认情况下，`XHR`对象只能访问包含该网页的源域上的资源。这一安全特性防止了某些恶意行为。然而，对合法的跨源访问的需求非常大，使得解决方案开始在浏览器中出现。

跨源资源共享（CORS）是一项 W3C 工作草案，它定义了浏览器和服务器在访问跨源资源时必须如何通信。CORS 的基本思想是使用自定义 HTTP 头部，让浏览器和服务器都能了解足够的对方信息，以判断请求或响应应该成功还是失败。

对于简单的请求（即使用`GET`或`POST`且没有自定义头部且主体为`text/plain`的请求），发送时会带上一个名为`Origin`的额外头部。`Origin`头部包含请求页的源（协议、域名和端口），以便服务器可以轻松地判断是否应该提供响应。一个`Origin`头部示例可能如下：

```
Origin: http://www.nczonline.net
```

如果服务器决定允许该请求，它会发送`Access-Control-Allow-Origin`头部，回显发送的相同源，或者如果是公共资源则回显`"*"`。例如：

```
Access-Control-Allow-Origin: http://www.nczonline.net
```

如果缺少此头部，或者源不匹配，浏览器将不允许该请求。如果一切正常，浏览器将处理该请求。注意，请求和响应都不包含 cookie 信息。

## Internet Explorer 中的 CORS

微软在 Internet Explorer 8 中引入了`XDomainRequest` (`XDR`) 类型。该对象的工作方式与`XHR`类似，但对于跨域通信来说是安全且可靠的。`XDR`对象实现了 CORS 规范的一部分。以下是`XDR`不同于`XHR`的一些方式：

- Cookie 既不随请求发送，也不随响应接收。
- 除了`Content-Type`之外，无法访问并设置请求头部。
- 无法访问响应头部。
- 仅支持`GET`和`POST`请求。

这些更改缓解了与跨站请求伪造（CSRF）和跨站脚本（XSS）攻击相关的问题。请求的资源可以根据其认为适当的任何数据（用户代理、引荐页等）动态决定是否设置`Access-Control-Allow-Origin`头部。作为请求的一部分，会发送一个值指示请求源域的`Origin`头部，允许远程资源显式地识别`XDR`请求。

`XDR`对象的使用与`XHR`对象的使用非常相似。你创建一个`XDomainRequest`的新实例，调用`open()`方法，然后调用`send()`方法。与`XHR`对象上的`open()`方法不同，`XDR`对象上的方法只接受两个参数：请求类型和 URL。

所有`XDR`请求都是异步执行的，没有办法创建同步请求。当请求返回时，会触发`load`事件，`responseText`属性将填充响应内容，如下：

![image](img/logo1.gif)

```
var xdr = new XDomainRequest();

xdr.onload = function(){

    alert(xdr.responseText);

};

xdr.open("get", "http://www.somewhere-else.com/page/");

xdr.send(null);
```

`XDomainRequestExample01.htm`

当接收响应时，你只能访问响应的原始文本；无法确定响应的状态码。对于所有有效响应都会触发`load`事件，对于所有失败都会触发`error`事件。由于缺少`Access-Control-Allow-Origin`头部，你无法获得额外的错误信息，因此知道请求失败就足够了。为了检测错误，你应该分配一个`onerror`事件处理器，如下：

```
var xdr = new XDomainRequest();

xdr.onload = function(){

    alert(xdr.responseText);

};

xdr.onerror = function(){

    alert("An error occurred.");

};

xdr.open("get", "http://www.somewhere-else.com/page/");

xdr.send(null);
```

![image](img/pen.gif)

你可以在请求返回之前通过调用`abort()`来停止请求：

```
xdr.abort(); //停止请求
```

类似于`XHR`，`XDR`对象支持`timeout`属性和`ontimeout`事件处理器。示例如下：

```
var xdr = new XDomainRequest();

xdr.onload = function(){

    alert(xdr.responseText);

};

xdr.onerror = function(){

    alert("An error occurred.");

};

xdr.timeout = 1000;

xdr.ontimeout = function(){

    alert("Request took too long.");

};

xdr.open("get", "http://www.somewhere-else.com/page/");

xdr.send(null);
```

此示例在一秒后超时，此时调用`ontimeout`事件处理器。

为了允许`POST`请求，`XDR`对象暴露了`contentType`属性，可用于指示发布数据的格式，示例所示：

```
var xdr = new XDomainRequest();

xdr.onload = function(){

    alert(xdr.responseText);

};

xdr.onerror = function(){

    alert("An error occurred.");

};

xdr.open("post", "http://www.somewhere-else.com/page/");

xdr.contentType = "application/x-www-form-urlencoded";

xdr.send("name1=value1&name2=value2");
```

该属性是通过`XDR`对象访问头部信息的唯一方式。

## 其他浏览器中的 CORS

Firefox 3.5+、Safari 4+、Chrome、iOS 版 Safari 和 Android 版 WebKit 均通过`XMLHttpRequest`对象原生支持 CORS。当尝试打开不同源的资源时，这种行为会自动触发，无需任何额外代码。要向另一个域的资源发送请求，可以使用标准的`XHR`对象并在`open()`中指定绝对 URL，如下：

```javascript
var xhr = createXHR();

xhr.onreadystatechange = function(){

    if (xhr.readyState == 4){

        if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){

            alert(xhr.responseText);

        } else {

            alert("Request was unsuccessful: " + xhr.status);

        }

    }

};

xhr.open("get", "http://www.somewhere-else.com/page/", true);

xhr.send(null);
```

与 Internet Explorer 中的`XDR`对象不同，跨域`XHR`对象允许访问`status`和`statusText`属性，并允许同步请求。出于安全考虑，跨域`XHR`对象还有一些必要的额外限制。具体如下：

- 无法使用`setRequestHeader()`设置自定义请求头。
- Cookies 既不发送也不接收。
- `getAllResponseHeaders()`方法始终返回空字符串。

由于同域和跨域请求都使用相同的接口，因此在访问本地资源时最好始终使用相对 URL，在访问远程资源时使用绝对 URL。这可以区分用例，并防止诸如限制本地资源的标头和/或 cookie 信息访问等问题。

### 预检请求

CORS 允许通过一种透明的服务器验证机制（称为预检请求）使用自定义请求头、`GET`或`POST`以外的方法以及不同的主体内容类型。当你尝试使用这些高级选项之一发送请求时，会向服务器发送一个“预检”请求。该请求使用`OPTIONS`方法并发送以下请求头：

- `Origin` — 与简单请求相同。
- `Access-Control-Request-Method` — 请求想要使用的方法。
- `Access-Control-Request-Headers` — （可选）所使用的自定义请求头的逗号分隔列表。

这里有一个带有名为`NCZ`的自定义请求头的`POST`请求的示例：

```
Origin: http://www.nczonline.net

Access-Control-Request-Method: POST

Access-Control-Request-Headers: NCZ
```

在请求请求期间，服务器可以确定是否允许此类类型的请求。服务器通过在响应中发送以下响应头来通知浏览器：

- `Access-Control-Allow-Origin` — 与简单请求相同。
- `Access-Control-Allow-Methods` — 允许方法的逗号分隔列表。
- `Access-Control-Allow-Headers` — 服务器允许的请求头的逗号分隔列表。
- `Access-Control-Max-Age` — 该预检请求的缓存时间（秒）。

例如：

```
Access-Control-Allow-Origin: http://www.nczonline.net

Access-Control-Allow-Methods: POST, GET

Access-Control-Allow-Headers: NCZ

Access-Control-Max-Age: 1728000
```



一旦发送了预检请求，结果将在响应中指定的时间内缓存；你只有在第一次发送此类类型的请求时，才会产生额外 HTTP我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。请求的成本。

Firefox 3.5+、Safari 4+ 和 Chrome 都支持预检请求；版本 10 及以下的 Internet Explorer 不。

## 凭据请求

默认情况下，跨源请求不提供凭据（cookies、HTTP 身份验证和客户端 SSL 证书）。你可以通过将`withCredentials`属性设置为`true`来指定请求应发送凭据。如果服务器允许凭据请求，则它会响应以下 HTTP 头部：

```
Access-Control-Allow-Credentials: true
```

如果发送了凭据请求且此标头没有作为响应的一部分发送，则浏览器不会将响应传递给 JavaScript（`responseText`为空字符串，`status`为 0，并且会调用`onerror()`）。请注意，服务器也可以将此 HTTP 头部作为预检响应的一部分发送，以指示源允许发送凭据请求。

Firefox 3.5+、Safari 4+ 和 Chrome 都支持`withCredentials`属性。版本 10 及以下的 Internet Explorer 仍然不支持。

## 跨浏览器 CORS

尽管并非所有浏览器都原生支持相同级别的 CORS，但所有支持 CORS 的浏览器都支持简单（非预检、非凭据）请求，因此拥有一个跨浏览器解决方案是有意义的。判断`XHR`对象是否支持 CORS 的简单方法是检查`withCredentials`属性是否存在。然后你可以结合`XDomainRequest`对象的是否存在来覆盖所有浏览器：

![image](img/logo1.gif)

```javascript
function createCORSRequest(method, url){

    var xhr = new XMLHttpRequest();

    if ("withCredentials" in xhr){

        xhr.open(method, url, true);

    } else if (typeof XDomainRequest != "undefined"){

        xhr = new XDomainRequest();

        xhr.open(method, url);

    } else {

        xhr = null;

    }

    return xhr;

}

var request = createCORSRequest("get", "http://www.somewhere-else.com/page/");

if (request){

    request.onload = function(){

        //do something with request.responseText

    };

    request.send();

}
```

CrossBrowserCORSRequestExample01.htm

Firefox、Safari 和 Chrome 中的`XMLHttpRequest`对象在接口上与 Internet Explorer 的`XDomainRequest`对象相似，这种模式非常有效。常用的属性/方法有：

- `abort()` — 用于停止正在进行的请求。
- `onerror` — 代替`readyState`检测错误。
- `onload` — 代替`readyState`检测成功。
- `responseText` — 用于获取内容。
- `send()` — 用于发送请求。

这些都可以用于`createCORSRequest()`返回的对象，并适用于每个浏览器。

## 替代跨域技术

在 CORS 出现之前，实现跨域通信要困难得多。开发者不得不依赖 DOM 的部分在不使用 XHR 对象的情况下执行跨域请求。

### 图像像素 (Image Pings)

跨域通信的早期技术之一是通过使用`<img>`标签。图像可以跨域而不担心限制。这是在线广告跟踪展示的主要方式。正如第 13 章所述，你也可以动态创建图像并使用它们的`onload`和`onerror`事件处理程序来告知何时收到响应。

动态创建图像通常用于图像像素。图像像素是服务器之间简单的跨域单向通信。数据通过查询字符串参数发送，响应可以是任何内容，通常是像素图像或 204 响应。浏览器无法从图像像素中获取任何数据，但可以通过监听`load`和`error`事件来判断响应已接收。这里有一个简单的示例：

![image](img/logo1.gif)

```javascript
var img = new Image();

img.onload = img.onerror = function(){

    alert("Done!");

};

img.src = "http://www.example.com/test?name=Nicholas";
```

ImagePingExample01.htm

此示例创建了一个新的`Image`实例，然后将`onload`和`onerror`事件处理程序分配给同一个函数。这确保了无论响应如何，都会在请求完成时收到通知。请求在设置`src`属性时开始，此示例传递了一个 name 参数。

图像像素经常用于跟踪页面点击和动态广告展示。图像像素的两个主要缺点是你只能发送`GET`请求，并且无法访问服务器的响应文本。这就是为什么图像像素最适用于浏览器与服务器之间的单向通信。

## JSONP

JSONP 是 “JSON with padding”（填充 JSON）的缩写，它是 JSON 的一种变体，在 Web 服务中非常流行。JSONP 看起来和 JSON 一一样，只是数据被包裹在一个类似于函数调用的结构。例如：

```
callback({ "name": "Nicholas" });
```

JSONP 格式由两部分组成：回调（callback）和数据。回调是在接收到响应后在页面上调用的函数。通常，回调名称是作为请求的一部分指定的。数据则是要传递给函数的 JSON 数据。一个典型的 JSONP 请求如下：

```
http://freegeoip.net/json/?callback=handleResponse
```

该 URL 指向一个 JSONP 地理位置服务。在 JSONP 服务中，将回调参数作为查询字符串参数指定是非常常见的，在这种情况下，我将回调函数名指定为`handleResponse()`。

JSONP 通过动态`<script>`元素使用（详情请见第 13 章），将`src`属性赋值为跨域 URL。`<script>`元素类似于`<img>`，能够不受限制地从其他域加载资源。由于 JSONP 是有效的 JavaScript，JSONP 响应在完成后会被拉入页面并立即执行。这是一个示例：

![image](img/logo1.gif)

```
function handleResponse(response){

    alert("You're at IP address " + response.ip + ", which is in " + 

          response.city + ", " + response.region_name);

}

var script = document.createElement("script");

script.src = "http://freegeoip.net/json/?callback=handleResponse";

document.body.insertBefore(script, document.body.firstChild);
```

JSONPExample01.htm

此示例显示了来自地理位置服务的 IP 地址和位置信息。

JSONP 在 Web 开发人员中非常受欢迎，因为它简单易用。它相对于图片像素（image pings）的优势在于你可以直接访问响应文本，允许浏览器和服务器之间的双向通信。然而，使用 JSONP 也有缺点。

首先，你从另一个域向页面中引入了可执行的代码。如果该域不可信，它很容易将响应替换为更具恶性的内容，除了完全移除 JSONP 调用外，你将无计可施。在使用你不运营的 Web 服务时，请确保它来自可信源。

第二个缺点是没有简单的方法来判断 JSONP 请求是否失败。尽管 HTML5 为`<script>`元素指定了`onerror`事件处理器，但尚未没有任何浏览器实现它。开发者经常使用计时器来查看在规定时间内是否收到了响应，但即使是这样也很棘手，因为并不是每个用户的连接速度和带宽都是相同的。

## Comet

Comet 是 Alex Russell 提出的一个术语，用于描述一种更高级的 Ajax 技术，有时被称为服务器推送（server push）。Ajax 被描述为页面向服务器请求数据，而 Comet 被描述为服务器将数据推送到页面。这种方法允许信息以接近实时的方式进入页面，使其成为体育比分或股票价格等信息的理想选择。

Comet 有两种流行的方法：长轮询（long polling）和流式（streaming）。长轮询是传统轮询（也称为短轮询）的新变体，浏览器定期向服务器发送请求，以检查是否有任何数据。图 21-1 显示了短轮询的工作时间线。

FIGURE 21-1

![image](img/f721-01.jpg)

长轮询反转了短轮询。页面向服务器发起请求，服务器保持该连接开启直到有数据要发送。一旦发送了数据，浏览器会关闭连接，并立即向服务器开启新连接。只要页面在浏览器中打开，这个过程就会持续下去。图 21-2 显示了长轮询的工作时间线。

FIGURE 21-2

![image](img/f722-01.jpg)

在短轮询长轮询中，浏览器都需要在接收数据之前发起与服务器的连接。巨大的区别在于服务器如何处理返回数据的发送。短轮询无论数据是否可用都会立即发送响应，而长轮询则等待发送响应。轮询技术的优势是所有浏览器都通过`XHR`对象和使用`setTimeout()`支持这一点。你只需要管理何时发送请求。

Comet 的第二种流行方法是 HTTP 流（HTTP streaming）。流与任何轮询技术都不同，因为它在页面的整个生命周期内使用单个 HTTP 连接。浏览器向服务器发送请求，服务器保持该连接开启，通过连接定期向服务器发送数据。例如，一个 PHP 服务器可能会有这样的脚本：

```php
<?php

    $i = 0;

    while(true){

        //输出一些数据并立即刷新输出缓冲区

        echo "Number is $i";

        flush();

        //等待几秒

        sleep(10);

        $i++;

    }
```

所有服务器端语言都支持打印到输出缓冲区然后进行刷新（将输出缓冲区的内容发送到客户端）的概念。这是 HTTP 流的核心。

在 Firefox、Safari、Opera 和 Chrome 中，可以使用`XHR`对象通过监听`readyStatechange`事件并关注`readyState` 3 来实现 HTTP 流。在所有这些浏览器中，当数据正在接收时，`readyState`为 3 会周期性地触发。此时，`responseText`属性包含了所有数据，这意味着你需要通过跟踪已发送的内容来切片获取最新的部分。使用`XHR`实现的 HTTP 流如下：

![image](img/logo1.gif)

```javascript
function createStreamingClient(url, progress, finished){        

    var xhr = new XMLHttpRequest(),

        received = 0;

    xhr.open("get", url, true);

    xhr.onreadystatechange = function(){

        var result;

        if (xhr.readyState == 3){

            //仅获取新数据并调整计数

            result = xhr.responseText.substring(received);

            received += result.length;

            //调用进度回调

            progress(result);

        } else if (xhr.readyState == 4){

            finished(xhr.responseText);

        }

    };

    xhr.send(null);

    return xhr;

}

var client = createStreamingClient("streaming.php", function(data){

                alert("Received: " + data);

             }, function(data){

                alert("Done!");

             });
```

HTTPStreamingExample01.htm

`createStreamingClient()`函数接受三个参数：要连接的 URL、接收到更多数据时调用的函数，以及连接关闭时调用的函数。你可能可能或不想在连接关闭后重新连接，因此跟踪这一点是好的。

尽管这个示例相对简单并且可以在大多数浏览器中运行（Internet Explorer 除外），但 Comet 模式的连接管理很容易出错，并且需要时间来完善。浏览器社区认为 Comet 是 Web 未来的一个重要部分，因此创建了两个新接口来让 Comet 变得更加简单。

### 服务器发送事件 (Server-Sent Events)

服务器发送事件 (SSE) 是一种用于只读 Comet 交互的 API 和模式。`SSE` API 创建了一个从客户端到服务器的单向 HTTP 连接，服务器可以通过该连接传输其所需的尽可能或尽可能少的信息。服务器响应的 MIME 类型必须为`text/event-stream`，并以特定格式输出信息，浏览器 API 会消费这些信息并通过 JavaScript 提供。`SSE`支持短轮询、长轮询和 HTTP 流式传输，因此在连接断开时，它会自动决定何时重新连接到服务器。结果是一个极其简单且实用的 API，让 Comet 变得简单。

Firefox 6+、Safari 5+、Opera 11+、Chrome 以及 iOS Safari 4+ 均支持服务器发送事件。

#### API

`SSE`的 JavaScript API 与其他最近的 JavaScript 消息 API 类似。要订阅新的事件流，你首先创建一个新的`EventSource`对象并传入入口点：

```
var source = new EventSource("myevents.php");
```

注意，引用的 URL 必须与创建该对象的页面处于同源（方案、域名和端口）。`EventSource`实例有一个`readyState`属性，其设置为`0`表示正在连接到服务器，设置为`1`表示连接已打开，设置为`2`表示连接已关闭。

还有三个事件：

- `open`：在连接建立时触发
- `message`：在从服务器接收到新事件时时触发
- `error`：在无法建立连接时触发

在常规用法中，`onmessage`事件处理器可能是你使用最频繁的：

```
source.onmessage = function(event){

    var data = event.data;

    //对数据进行某些操作

};
```

从服务器传回的信息通过`event.data`以字符串形式返回。

默认情况下，`EventSource`对象将尝试保持与服务器的连接活跃状态。如果连接关闭，将会尝试重新连接。这意味着服务器发送事件可以与长轮询和 HTTP 流式传输配合工作。你可以通过调用`close()`方法强制对象立即断并停止尝试重新连接：

```
source.close();
```

#### 事件流

服务器事件通过 MIME 类型为`text/event-stream`的持久 HTTP 响应发送。响应的格式为纯文本，在最简单的形式下，由前缀`data:`组成，后跟文本，例如：

```
data: foo

data: bar

data: foo

data: bar
```

此流的第一部分会触发一个`event.data`设置为“foo”的消息事件；第二部分会触发一个`event.data`设置为“bar”的消息事件；第三部分触发一个`event.data`设置为“foo\nbar”的消息事件（注意中间的换行符）。当有两行或更多行连续以`data:`开头的行时，它被解释为多行数据，值将用换行符连接在一起。在遇到包含`data:`的行之后遇到空行之前，消息事件永远不会触发，因此在服务器上生成事件流时，请务必包含那个额外的换行符。

你还可以通过在`data:`行之前或之后包含`id:`行来为特定事件关联 ID：

```
data: foo

id: 1
```



通过设置 ID，`EventSource` 对象会跟踪最后一个触发的事件。如果连接掉落，将随请求一起发送一个名为 `Last-Event-ID` 的特殊 HTTP 请求头，以便服务器可以确定下一个触发哪个事件是合适的。这对于在多个连接上保持顺序数据的正确顺序至关重要。

## Web Sockets

Web Sockets 是最受关注的新浏览器 API 之一。Web Sockets 的目标是通过单个持久连接与服务器提供全双工、双向的通信。当在 JavaScript 中创建 Web Socket 时，会向服务器发送一个 HTTP 请求以初始化连接。当服务器响应时，该连接使用 HTTP 升级协议从 HTTP 切换到 Web Socket 协议。这意味着 Web Sockets 无法通过标准的 HTTP 服务器实现，必须使用支持该协议的专用服务器才能正常工作。

由于 Web Sockets 使用自定义协议，URL 方案略有不同。它不使用 `http://` 或 `https://` 方案，而是用于不安全连接的 `ws://` 和用于安全连接的 `wss://`。在指定 Web Socket URL 时，你必须包含方案，因为未来可能支持其他方案。

与 HTTP 相比，使用自定义协议的优势可以在客户端和服务器之间传输极少量的数据，且不受 HTTP 字节开销的限制。使用较小的数据包使得 Web Sockets 成为带宽和延迟成为问题的移动应用的理想选择。使用自定义协议的缺点是协议的定义比 JavaScript API 花了更长时间。由于人们在协议的一性和安全性方面都发现了问题，Web Sockets 曾被多次停滞。Firefox 4 和 Opera 11 都都默认启用了 Web Sockets，但由于安全考虑，在发布前夕又禁用了它。现在 Firefox 6+、Safari 5+、Chrome 以及 iOS Safari 4+ 均支持 Web Sockets。

### API

要创建一个 Web Socket，请实例化 `WebSocket` 对象并传入提供连接的 URL：

```
var socket = new WebSocket("ws://example.com/server.php");
```

注意你必须向 `WebSocket` 构造函数传递绝对 URL。同源策略不适用于 Web Sockets，因此你可以与任何站点建立连接。是否与来自特定源的页面通信完全取决于服务器。（可以使用握手信息确定请求的来源。）

一旦实例化 `WebSocket` 对象，浏览器就会尝试创建连接。与 XHR 类似，`WebSocket` 有一个 `readyState` 属性来指示当前状态。然而，其值与 XHR 不同，如下：

* `WebSocket.OPENING` (0)：正在建立连接
* `WebSocket.OPEN` (1)：连接已建立
* `WebSocket.CLOSING` (2)：连接正在关闭
* `WebSocket.CLOSE` (3)：连接已关闭

`WebSocket` 没有 `readyStatechange` 事件；但是有其他对应各种状态的事件。`readyState` 始终从 `0` 开始。

你可以使用 `close()` 方法随时关闭 Web Socket 连接：

```
socket.close();
```

调用 `close()` 后，`readyState` 立即变为 `2` (正在关闭)，并在完成后切换到 `3`。

### 发送/接收数据

一旦 Web Socket 打开，你就可以通过连接发送数据并从连接接收数据。要向服务器发送数据，请使用 `send()` 方法并传入任何字符串，例如：

```
var socket = new WebSocket("ws://example.com/server.php");
socket.send("Hello world!");
```

由于 Web Sockets 只能通过连接发送纯文本，因此在发送之前，你需要对更复杂的数据结构进行序列化。以下代码将数据序列化为 JSON 字符串，然后将字符串发送到服务器：

```
var message = {
    time: new Date(),
    text: "Hello world!",
    clientId: "asdfp8734rew"
};
socket.send(JSON.stringify(message));
```

服务器随后需要解析返回的 JSON 以访问数据。

当服务器向客户端发送消息时，`WebSocket` 对象上会触发一个消息事件（message event）。消息事件的工作方式与其他消息协议类似，可以通过 `event.data` 属性获取有效负载：

```javascript
socket.onmessage = function(event){
    var data = event.data;
    //do something with data
};
```

与通过 `send()` 发送到服务器的数据一样，`event.data` 返回的始终是一个字符串。如果你期望的是其他数据格式，则必须手动解析这些数据。

### 其他事件

`WebSocket` 对象在连接的生命周期内还有三个事件会触发：

* `open` — 当连接成功建立时触发。
* `error` — 当发生错误时触发。连接无法持续维持。
* `close` — 当连接关闭时触发。

`WebSocket` 对象不支持 DOM Level 2 事件监听器，因此你需要为每个事件使用 DOM Level 0 风格的事件处理器：

```javascript
var socket = new WebSocket("ws://www.example.com/server.php");
socket.onopen = function(){
    alert("Connection established."); own};
socket.onerror = function(){
    alert("Connection error.");
};
socket.onclose = function(){
    alert("Connection closed.");
};
```

在这三个事件中，只有 `close` 事件在事件对象上包含额外信息。事件对象上有三个额外的属性：`wasClean`，一个布尔值，表示连接是否是正常关闭的；`code`，一个从服务器发送的数字状态码；以及 `reason`，一个包含服务器发送的消息的字符串。你可能希望使用这些信息来显示给用户或记录以进行分析：

```javascript
socket.onclose = function(event){
    console.log("Was clean? " + event.wasClean + " Code=" + event.code + " Reason=" 
                + event.reason);
};
```

### SSE 与 Web Sockets

在决定针对特定用例使用 `SSE` 还是 `Web Sockets` 时，你可以考虑几个因素。首先，你是否有灵活性设置 `Web Socket` 服务器？由于 `WebSocket` 协议不是 HTTP，你现有的 Web 服务器可能无法进行 `WebSocket` 通信。`SSE` 运行在普通 HTTP 之，因此你可能可以使用现有的 Web 服务器来执行此类通信。

第二个要问的问题是你是否需要双向通信。如果该用例只需要对服务器数据进行只读访问（例如体育比分），那么 `SSE` 可能更容易实现。如果该用例需要全双向支持（例如聊天室），那么 `Web Sockets` 可能是更好的选择。请记住，如果 `Web Sockets` 对你来说不可行，你仍然可以通过 `XHR` 和 `SSE` 的组合来实现双向通信。

### 安全

关于 `Ajax` 和 `Comet` 安全已经有很多报道；事实上，有专门的书籍讨论这个主题。大规模 Ajax 应用的安全考量是海量的，但对于通用的 Ajax 安全，有一些基础知识是需要的。

首先，任何可以通过 `XHR` 访问的 URL 也可以被浏览器或服务器访问。例如，考虑以下 URL：

```
/getuserinfo.php?id=23
```

如果对此 URL 发起请求，它预计会返回关于 ID 为 23 的用户的数据。没有什么可以阻止有人将 URL 修改为另一个用户 ID。

JavaScript 是一种极其灵活的语言，可以使用多种风格编写。通常情况下，JavaScript 以过程化的方式或面向对象的方式使用。然而，由于其动态性质，该语言能够实现许多更复杂且有趣的模式。这些技术利用了 ECMAScript 语言特性、BOM 扩展和 DOM 功能来实现强大的效果。

# 高级函数

函数是 JavaScript 最有趣的部分之一。它们在本质上可以非常简单且过程化，也可以非常复杂且动态。通过使用闭包可以实现额外的功能。此外，函数指针非常容易使用，因为所有函数都是对象。这一切使得 JavaScript 函数既既有趣又强大。接下来的章节概述了 JavaScript 中使用函数的一些高级方法。

## 安全的类型检测

JavaScript 内置的类型检测机制并非万无一失，事实上，它们有时会产生误报或漏报。例如，`typeof` 运算符有几个怪癖，这可能导致它在检测某些类型的数据时变得不可靠。由于 Safari（在 4 版本之前）将 `typeof` 应用于正则表达式时会返回 `"function"`，因此很难确定判断一个值是否为函数。

`instanceof` 运算符也存在问题，当存在多个全局作用域时（例如存在多个帧/frames），它很难使用。正如第 5 章提到的，该问题的经典示例是尝试使用以下代码将对象识别为数组：

```
var isArray = value instanceof Array;
```

只有当 `value` 是数组且在与 `Array` 构造函数相同的全局作用域中创建时，此代码才会返回 `true`。（记住，`Array` 是 `window` 的一个属性。）如果 `value` 是来自另一个帧的数组，此代码将返回 `false`。

类型检测的另一个问题是尝试确定一个对象是原生实现还是开发者定义的。当浏览器开始原生实现 `JSON` 对象时，这个问题浮现出水面。由于许多人已经在使用 Douglas Crockford 的 `JSON` 库（该库定义了一个全局 `JSON` 对象），开发者很难判断页面上存在的是哪一个对象。

所有这些问题的解决方案是相同的。可以对任何值调用 `Object` 的原生 `toString()` 方法，返回格式为 `"[object NativeConstructorName]"` 的字符串。每个对象都有一个内部 `[[Class]]` 属性，它指定了作为该字符串一部分返回的构造函数名称。例如：

```
alert(Object.prototype.toString.call(value));   //"[object Array]"
```

由于数组的原生构造函数名称无论其在哪个全局上下文中创建都是相同的，使用 `toString()` 可以返回一个一致的值。这允许你创建一个这样的函数：

```javascript
function isArray(value){
    return Object.prototype.toString.call(value) == "[object Array]";
}
```

同样的方法可以用于判断一个值是原生函数还是正则表达式：

```javascript
function isFunction(value){
    return Object.prototype.toString.call(value) == "[object Function]";
}

function isRegExp(value){
    return Object.prototype.toString.call(value) == "[object RegExp]";
}
```

注意，在 Internet Explorer 中，对于任何实现为 COM 对象而非原生 JavaScript 函数的函数，`isFunction()` 将返回 `false`（见第 10 章）。

该技术也被广泛用于识别原生 `JSON` 对象。`Object` 的 `toString()` 方法无法确定非原生构造函数的构造函数名称，因此任何开发者定义构造函数的实例对象都会返回 `"[object Object]"`。一些 JavaScript 库包含类似以下的代码：

![image](img/logo1.gif)

```
var isNativeJSON = window.JSON && Object.prototype.toString.call(JSON) == 
"[object JSON]";
```

在 Web 开发中，能够区分原生和非原生 JavaScript 对象非常重要，这可以确保你了解对象的可用能力。这种技术可以用于任何对象以明确做出此判断。

![image](img/cross.gif)

请记住，可以将 `Object.prototype.toString()` 赋值给不同的值。本节讨论的技术假设 `Object.prototype.toString()` 是原生版本且没有被开发者覆盖。

## 作用安全的构造函数

第 6 章涵盖了用于定义自定义对象的构造函数的定义用法。你会记得，构造函数仅仅是一个使用 `new` 运算符调用的函数。当这样使用时，构造函数内部使用的 `this` 对象指向新创建的对象实例，如下例所示：

![image](img/logo1.gif)

```javascript
function Person(name, age, job){
    this.name = name;
    this.age = age;
    this.job = job;
}

var person = new Person("Nicholas", 29, "Software Engineer");
```

ScopeSafeConstructorsExample01.htm

在这个示例中，`Person` 构造函数使用 `this` 对象分配三个属性：`name`、`age` 和 `job`。当配合 `new` 运算符使用时，会创建一个新的 `Person` 对象并将属性分配到上面。问题发生在在没有使用 `new` 运算符调用构造函数时。由于 `this` 对象在运行时绑定，直接调用 `Person()` 会将其映射到全局对象（`window`），导致意外增强了错误的对象。例如：

```javascript
var person = Person("Nicholas", 29, "Software Engineer");
alert(window.name);     //"Nicholas"
alert(window.age);      //undefined
alert(window.job);      //undefined
```

ScopeSafeConstructorsExample01.htm

在这里，`window` 对象被赋予了本属于 `Person` 实例的三个属性，因为构造函数是作为普通函数调用的。这个问题由于 `this` 对象的后期绑定导致。由于 `window` 的 `name` 属性被用于识别目标和帧，这种对属性的意外覆盖会导致页面上的其他错误。解决方案是创建一个作用安全的构造函数。

ScopeSafeConstructorsExample01.htm

安全的构造函数首先检查 `this` 对象是否是正确类型的实例，然后再应用任何更改。如果不是，则创建并返回一个新的实例。考虑这个示例：

![image](img/logo1.gif)

```javascript
function Person(name, age, job){
    if (this instanceof Person){
        this.name = name;
        this.age = age;
        this.job = job;
    } else {
        return new Person(name, age, job);
    }
}

var person1 = Person("Nicholas", 29, "Software Engineer");
alert(window.name);   ""
alert(person1.name);  //"Nicholas"

var person2 = new Person("Shelby", 34, "Ergonomist");
alert(person2.name);  //"Shelby"
```

ScopeSafeConstructorsExample02.htm

代码中的 `Person` 构造函数增加了一个 `if` 语句来确保 `this` 对象是 `Person` 的实例，这表明使用了 `new` 运算符或在现有的 `Person` 实例上下文中调用了构造函数。在任何情况下，对象初始化都会照常进行。如果不是 `Person` 的实例，则使用 `new` 运算符再次调用构造函数并返回该值。结果是无论带带 `new` 调用 `Person` 构造函数都会返回一个新的 `Person` 实例，避免了在全局对象上意外设置属性。

作用安全的构造函数有一个注意事项。通过实现这种模式，你锁定了构造函数可以调用的上下文。如果你在使用构造函数窃取模式进行继承而没有同时使用原型链，那么你的继承可能会破坏。这是一个示例：

```javascript
function Polygon(sides){
    if (this instanceof Polygon) {
        this.sides = sides;
        this.getArea = function(){
            return 0;
        };
    } else {



## 作用安全的构造函数

```javascript
function Polygon(sides){
    if (this instanceof Polygon) {
        this.sides = sides;
        this.getArea = function(){
            return 0;
        };
    } else {
        return new Polygon(sides);
    }
}

function Rectangle(width, height){
    Polygon.call(this, 2);
    this.width = width;
    this.height = height;
    this.getArea = function(){
        return this.width * this.height;
    };
}

var rect = new Rectangle(5, 10);
alert(rect.sides);   //undefined
```

### ScopeSafeConstructorsExample03.htm

在这段代码中，`Polygon` 构造函数是作用安全的（scope-safe），而 `Rectangle` 构造函数不是。当创建一个新的 `Rectangle` 实例时，它应该通过 `Polygon.call()` 从 `Polygon` 继承 `sides` 属性。然而，由于 `Polygon` 构造函数是作用安全的，`this` 对象并不是 `Polygon` 的实例，因此会创建并返回一个新的 `Polygon` 对象。

`Rectangle` 构造函数中的 `this` 对象没有被扩展，且 `Polygon.call()` 返回的值没有被使用，因此 `Rectangle` 实例上没有 `sides` 属性。

如果在构造函数窃取（constructor stealing）中使用原型链或寄生组合（parasitic combination），这个问题就会解决。请考虑以下示例：

![image](img/logo1.gif)

```javascript
function Polygon(sides){
    if (this instanceof Polygon) {
        this.sides = sides;
        this.getArea = function(){
            return 0;
        };
    } else {
        return new Polygon(sides);
    }
}

function Rectangle(width, height){
    Polygon.call(this, 2);
    this.width = width;
    this.height = height;
    this.getArea = function(){
        return this.width * this.height;
    };
}

Rectangle.prototype = new Polygon();

var rect = new Rectangle(5, 10);
alert(rect.sides);   //2
```

### ScopeSafeConstructorsExample04.htm

在重写后的代码中，`Rectangle` 的实例也是 `Polygon` 的实例，因此 `Polygon.call()` 按照预期工作，最终为 `Rectangle` 实例添加了 `sides` 属性。

作用安全的构造函数在多个开发者编写 JavaScript 代码并运行在同一页面上的环境中非常有帮助。在这种情况下，对全局对象的意外更改可能会导致往往难以追踪的错误。除非你正在实现的是纯粹基于构造函数窃取的继承，否则建议将作用安全的构造函数作为一种最佳实践。

## 懒加载函数 (Lazy Loading Functions)

由于浏览器行为的差异，大多数 JavaScript 代码包含大量的 `if` 语句，用于将执行流分向那些应该成功的代码。考虑上一章中的以下 `createXHR()` 函数：

```javascript
function createXHR(){
    if (typeof XMLHttpRequest != "undefined"){
        return new XMLHttpRequest();
    } else if (typeof ActiveXObject != "undefined"){
        if (typeof arguments.callee.activeXString != "string"){
            var versions = ["MSXML2.XMLHttp.6.0", "MSXML2.XMLHttp.3.0",
                            "MSXML2.XMLHttp"], 
                i, len;
            for (i=0,len=versions.length; i < len; i++){
                try {
                    new ActiveXObject(versions[i]);
                    arguments.callee.activeXString = versions[i];
                    break;
                } catch (ex){
                    //skip
                }
            }
        }
        return new ActiveXObject(arguments.callee.activeXString);
    } else {
        throw new Error("No XHR object available.");
    }
}
```

每当调用 `createXHR()` 时，它都会遍历并检查浏览器支持哪些能力。首先它检查是否存在原生的 `XHR`，然后测试基于 `ActiveX` 的 `XHR`，如果两者都未找到，最后抛出错误。这在每次调用函数时都会发生，尽管这种分支的结果在调用之间不会改变：如果浏览器支持原生 `XHR`，它将永远支持原生 `XHR`，因此这种测试是不必要的。即使只通过一个 `if` 语句的代码也比没有 `if` 语句的代码慢，所以如果不需要都通过 `if` 语句，代码运行速度可能会更快。这种解决方案被称为懒加载（lazy loading）。

懒加载意味着函数的分支只发生一次。实现懒加载有两种方法，第一种是在第一次调用时对函数进行操作。在第一次调用期间，函数会被另一个函数覆盖，使得后续的调用不需要经过执行分支。例如，`createXHR()` 函数可以重写为如下这种懒加载方式：

![image](img/logo1.gif)

```javascript
function createXHR(){
    if (typeof XMLHttpRequest != "undefined"){
        createXHR = function(){
            return new XMLHttpRequest();
        };
    } else if (typeof ActiveXObject != "undefined"){
        createXHR = function(){
            if (typeof arguments.callee.activeXString != "string"){
                var versions = ["MSXML2.XMLHttp.6.0", "MSXML2.XMLHttp.3.0",
                                "MSXML2.XMLHttp"], 
                    i, len;
                for (i=0,len=versions.length; i < len; i++){
                    try {
                        new ActiveXObject(versions[i]);
                        arguments.callee.activeXString = versions[i];
                        break;
                    } catch (ex){
                        //skip
                    }
                }
            }
            return new ActiveXObject(arguments.callee.activeXString);
        };
    } else {
        createXHR = function(){
            throw new Error("No XHR object available.");
        };
    }
    return createXHR();
}
```

### LazyLoadingExample1.htm

在 `createXHR()` 的懒加载版本中，`if` 语句的每个分支都会为 `createXHR` 变量分配不同的函数，从而覆盖原始函数。最后一步是调用新分配的函数。下次调用 `createXHR()` 时，它将调用已赋值的函数，因此不再重新评估 `if` 语句。

另一种懒加载模式是在函数声明时立即分配适当的函数。因此，不是在第一次调用函数时产生性能损失，而是在代码加载时产生性能损失。这里是使用此模式编写的之前的示例：

![image](img/logo1.gif)

```javascript
var createXHR = (function(){
    if (typeof XMLHttpRequest != "undefined"){
        return function(){
            return new XMLHttpRequest();
        };
    } else if (typeof ActiveXObject != "undefined"){
        return function(){
            if (typeof arguments.callee.activeXString != "string"){
                var versions = ["MSXML2.XMLHttp.6.0", "MSXML2.XMLHttp.3.0",
                                "MSXML2.XMLHttp"],
                    i, len;
                for (i=0,len=versions.length; i < len; i++){
                    try {
                        new ActiveXObject(versions[i]);
                        arguments.callee.activeXString = versions[i];
                        break;
                    } catch (ex){
                        //skip
                    }
                }
            }
            return new ActiveXObject(arguments.callee.activeXString);
        };
    } else {
        return function(){
            throw new Error("No XHR object available.");
        };
    }
})();
```

### LazyLoadingExample02.htm

本示例中使用的方法是创建一个匿名的自执行函数，用以确定应该使用哪种不同的函数实现。请注意，逻辑是完全相同的。唯一变化的是第一行（使用 `var` 定义函数）、增加了自执行匿名函数，以及每个分支现在都返回正确的函数定义，以便将其立即赋值给 `createXHR()`。

懒加载函数的优势在于，你只需要在分叉代码时支付一次性能开销。哪种模式适合你取决于你的独特需求，但两种模式都具有确保不始终执行不必要的代码的优势。

## 函数绑定 (Function Binding)

一种已变得日益流行的高级技术是函数绑定。函数绑定涉及创建一个函数，该函数以特定的 `this` 值和特定的参数调用另一个函数。这种技术通常与回调函数和事件处理器结合使用，在将函数作为变量传递的同时保留代码的执行上下文。考虑以下示例：

```javascript
var handler = {
    message: "Event handled",
    handleClick: function(event){
        alert(this.message);
    }
};

var btn = document.getElementById("my-btn");
EventUtil.addHandler(btn, "click", handler.handleClick);
```

在这个示例中，创建了一个名为 `handler` 的对象。`handler.handleClick()` 方法被赋值为一个 DOM 按钮的事件处理器。当按钮被点击时，该函数被调用并显示警框。尽管看起来警框应该显示 "Event handled"，但实际上显示的是 "undefined"。问题在于 `handler.handleClick()` 的上下文没有被保存，因此在大多数浏览器中，`this` 对象最终指向 DOM 按钮而不是 `handler`。（在 Internet Explorer 8 及其之前的版本中，它指向 `window`。）你可以使用闭包来解决这个问题，如后续示例所示：

```javascript
var handler = {
    message: "Event handled",
    handleClick: function(event){
        alert(this.message);
    }
};

var btn = document.getElementById("my-btn");
EventUtil.addHandler(btn, "click", function(event){
    handler.handleClick(event);
});
```

该解决方案使用闭包在 `onclick` 事件处理器内部直接调用了 `handler.handleClick()`。当然，这是针对这部分特定代码的非常具体的解决方案。创建多个闭包会导致代码难以理解和调试。因此，许多 JavaScript 库都实现了一个可以将函数绑定到特定上下文的函数。通常，这个函数被称为 `bind()`。

简单的 `bind()` 函数接收一个函数和一个上下文，返回一个函数，该函数会在给定的上下文中调用给函数并保持所有参数完整。语法如下：

![image](img/logo1.gif)

```javascript
function bind(fn, context){
    return function(){
        return fn.apply(context, arguments);
    };
}
```

FunctionBindingExample01.htm

这个函数看起来简单得欺骗，但实际上非常强大。`bind()` 内部创建了一个闭包，通过使用 `apply()` 并传入上下文对象和参数来调用传入的函数。注意，这里使用的 `arguments` 对象是用于内部函数的，而不是 `bind()` 的。当返回的函数被调用时，它会在给定的上下文中执行传入的函数并传递所有参数。`bind()` 函数的用法如下：

```javascript
var handler = {
    message: "Event handled",
    handleClick: function(event){
        alert(this.message);
    }
};

var btn = document.getElementById("my-btn");
EventUtil.addHandler(btn, "click", bind(handler.handleClick, handler));
```

FunctionBindingExample01.htm

在这个示例中，使用 `bind()` 函数创建了一个可以传递给 `EventUtil.addHandler()` 的函数，同时保持了上下文。事件对象也被传递给了函数，如下：

![image](img/logo1.gif)

```javascript
var handler = {
    message: "Event handled",
    handleClick: function(event){
        alert(this.message + ":" + event.type);
    }
};

var btn = document.getElementById("my-btn");
EventUtil.addHandler(btn, "click", bind(handler.handleClick, handler));
```



## FunctionBindingExample01.htm

`handler.handleClick()` 方法像常一样接收了事件对象，因为所有参数都通过绑定函数直接传递给了它。

ECMAScript 5 在所有函数上引入了原生的 `bind()` 方法，使这个过程变得更加简单。你不需要定义自己的 `bind()` 函数，可以直接在函数本身上调用该方法。例如：

```javascript
var handler = {
    message: "Event handled",
    handleClick: function(event){
        alert(this.message + ":" + event.type);
    }
};

var btn = document.getElementById("my-btn");
EventUtil.addHandler(btn, "click", handler.handleClick.bind(handler));
```

## FunctionBindingExample02.htm

原生的 `bind()` 方法工作原理与之前描述的类似，即传入应该作为 `this` 值的对象。原生 `bind()` 方法在 Internet Explorer 9+、Firefox 4+ 和 Chrome 中可用。

当函数指针必须作为值传递且该函数需要在特定上下执行时，绑定函数非常有用。它们最常用于事件处理器，以及 `setTimeout()` 和 `setInterval()`。然而，绑定函数的开销比普通函数大——它们需要更多内存，并且因为多次函数调用而速度稍慢——因此最好只在必要时使用它们。

## 函数柯化 (Function Currying)

与函数绑定密切相关的话题是函数柯化，它创建一个具有一个或多个设置参数函数（也称为部分应用）。基本方法与函数绑定相同：使用闭包返回一个新函数。与柯化的区别在于，这个新函数在函数被调用时还设置了某些要传入的参数。考虑以下示例：

```javascript
function add(num1, num2){
    return num1 + num2;
}

function curriedAdd(num2){
    return add(5, num2);
}

alert(add(2, 3));      //5
alert(curriedAdd(3));  //8
```

这段代码定义了两个函数：`add()` 和 `curriedAdd()`。后者本质上是 `add()` 的版本，它在所有情况下将第一个参数设置为 5。尽管 `curriedAdd()` 在技术上并不是柯化函数，但它很好地演示了这一概念。

柯化函数通常通过调用另一个函数并传入要柯化的函数以及要提供的参数来动态创建。以下函数是创建柯化函数的通用方法：

![image](img/logo1.gif)

```javascript
function curry(fn){
    var args = Array.prototype.slice.call(arguments, 1);
    return function(){
        var innerArgs = Array.prototype.slice.call(arguments),
            finalArgs = args.concat(innerArgs);
        return fn.apply(null, finalArgs);
    };
}
```

## FunctionCurryingExample01.htm

`curry()` 函数的主要工作是按适当的顺序排列返回函数的参数。`curry()` 的第一个参数是需要被柯化的函数；所有其他参数都是要传入的值。为了获取从第一个参数之后的所有参数，在 `arguments` 对象上调用了 `slice()` 方法，并传入参数 `1`，这表示返回数组的第一个项应该是第二个参数。随后，`args` 数组包含了来自外部函数的参数。对于内部函数，创建了 `innerArgs` 数组来包含所有传入的参数（再次使用了 `slice()`）。在将外部函数和内部函数的参数都存储在数组中后，你可以使用 `concat()` 方法将它们合并为 `finalArgs`，然后使用 `apply()` 将结果传递给函数。注意，此函数没有考虑上下文（context），因此 `apply()` 的调用将 `null` 传递给第一个参数传入。可以按如下方式使用 `curry()` 函数：

![image](img/logo1.gif)

```javascript
function add(num1, num2){
    return num1 + num2;
}

var curriedAdd = curry(add, 5);
alert(curriedAdd(3));   //8
```

## FunctionCurryingExample01.htm

在这个示例中，创建了 `add()` 的柯化版本，其第一个参数绑定为 `5`。当调用 `curriedAdd()` 并传入 `3` 时，`3` 变成了 `add()` 的第二个参数，而第一个参数仍然是 `5`，结果和为 `8`。你也可以提供所有的函数参数，如示例所示：

```javascript
function add(num1, num2){
    return num1 + num2;
}

var curriedAdd = curry(add, 5, 12);
alert(curriedAdd());   //17
```

## FunctionCurryingExample01.htm

在这里，柯化的 `add()` 函数提供了两个参数，因此以后不需要传入。

函数柯化通常作为函数绑定的一部分，创建了一个更复杂的 `bind()` 函数。例如：

```javascript
function bind(fn, context){
    var args = Array.prototype.slice.call(arguments, 2);
    return function(){
        var innerArgs = Array.prototype.slice.call(arguments),
            finalArgs = args.concat(innerArgs);
        return fn.apply(context, finalArgs);
    };
}
```

## FunctionCurryingExample02.htm

`curry()` 函数的主要变化在于传入函数的参数数量以及它如何影响代码的结果。`curry()` 仅仅接受一个函数进行包装，而 `bind()` 接受一个函数和一个上下文对象。这意味着绑定函数的参数参数从第三个参数开始，而不是第二个参数，这改变了第一次对 `slice()` 的调用。另一个变化是在倒数第三行向 `apply()` 传入了上下文对象。当使用 `bind()` 时，它返回一个绑定到给定上下文的函数，并且可能已经设置了它的某些参数。当你想要向事件处理器传递事件对象之外的额外参数时，这非常有用，例如所示：

![image](img/logo1.gif)

```javascript
var handler = {
    message: "Event handled",
    handleClick: function(name, event){
        alert(this.message + ":" + name + ":" + event.type);
    }
};

var btn = document.getElementById("my-btn");
EventUtil.addHandler(btn, "click", bind(handler.handleClick, handler, "my-btn"));
```

## FunctionCurryingExample02.htm

在这个更新后的示例中，`handler.handleClick()` 方法接受两个参数：你正在操作的元素的名称和事件对象。名称作为第三个参数传入 `bind()` 函数，然后传递给 `handler.handleClick()`，该方法也接收了事件对象。

ECMAScript 5 的 `bind()` 方法也实现了函数柯化。只需在该对应值之后传入额外的参数即可：

```javascript
var handler = {
    message: "Event handled",
    handleClick: function(name, event){
        alert(this.message + ":" + name + ":" + event.type);
    }
};

var btn = document.getElementById("my-btn");
EventUtil.addHandler(btn, "click", handler.handleClick.bind(handler, "my-btn"));
```

## FunctionCurryingExample03.htm

柯化和绑定的函数为 JavaScript 提供了强大的动态函数创建能力。使用 `bind()` 还是 `curry()` 取决于对上下文对象的需求或缺失。它们都可以用于创建复杂的算法和功能，尽管两者都不应过度使用，因为每个函数都会产生额外的开销。

## 防篡对象 (TAMPER-PROOF OBJECTS)

JavaScript 一个广为人诟的缺点是它的共享性质：每个对象都可以被运行相同上下文中的任何代码修改。这可能导致开发者意外覆盖彼此的代码，更糟糕的是用不兼容的更改覆盖原生对象。ECMAScript 5 通过允许创建不可变的对象来解决这个问题。之前讨论了对象的本质，ECMAScript 5 通过引入 `Configurable`、`Writable`、`Enumerable`、`Value`、`Get` 和 `Set` 属性来改变属性的行为。

一个需要注意的是：一旦对象被设置为防篡，该操作就无法撤销。

### 不可扩展对象 (Nonensible Objects)

默认情况下，JavaScript 中的所有对象都是可扩展的，这意味着你可以随时添加属性和方法。例如，我可以定义一个对象然后决定添加另一个属性：

```javascript
var person = { name: "Nicholas" };
person.age = 29;
```

尽管第一行定义了 `person` 对象，`Object.preventExtensions()` 方法改变了这种行为，使得无法添加新属性。例如：

```javascript
var person = { name: "Nicholas" };
Object.preventExtensions(person);
person.age = 29;
alert(person.age);   //undefined
```

在调用 `Object.preventExtensions()` 之后，`person` 对象无法再添加属性。在非严格模式下，添加对象成员的尝试会被忽略，因此 `person.age` 的结果是 `undefined`。在严格模式下，尝试添加对象成员会导致错误。

尽管对象无法添加新成员，所有现有成员不受影响。你仍然可以修改和删除现有成员。还可以通过 `Object.isExtensible()` 方法确定对象是否可以扩展：

![image](img/logo1.gif)

```javascript
var person = { name: "Nicholas" };
alert(Object.isExtensible(person));   //true
Object.preventExtensions(person);
alert(Object.isExtensible(person));   //false
```

### 密封对象 (Sealed Objects)

ECMAScript 5 对对象的下一级保护是密封对象。密封对象是不可扩展，且现有对象成员的 `Configurable` 属性被设置为 `false`。这意味着属性和方法无法删除，因为数据属性无法通过 `Object.defineProperty()` 变为访问器属性，反之亦然。属性值仍然可以更改。

你可以通过 `Object.seal()` 方法来密封对象：

![image](img/logo1.gif)

```javascript
var person = { name: "Nicholas" };
Object.seal(person);
person.age = 29;
alert(person.age);      //undefined
delete person.name;
alert(person.name);     //"Nicholas"
```

在这个示例中，添加 `age` 属性的尝试被忽略。删除 `name` 属性的尝试同样被忽略，因此值保持完整。这是非严格模式下的行为。在严格模式下，尝试添加或删除对象成员会抛出错误。

你可以使用 `Object.isSealed()` 来判断一个对象是否是密封的。由于被密封的对象也是不可扩展的，因此密封对象在调用 `Object.isExtensible()` 时也会返回 `false`：

```javascript
var person = { name: "Nicholas" };
alert(Object.isExtensible(person));   //true
alert(Object.isSealed(person));       //false
Object.seal(person);
alert(Object.isExtensible(person));   //false
alert(Object.isSealed(person));       //true
```

## SealedObjectsExample02.htm

# 冻结对象

最严格的防篡对象类型是冻结对象（Frozen objects）。冻结对象不可扩展且密封的，而且其数据属性的 `Writable` 属性被设置为 `false`。访问器属性可能仍然被写入，但前提是定义了 `Set` 函数。ECMAScript 5 定义了 `Object.freeze()` 来允许冻结对象：

```javascript
var person = { name: "Nicholas" };
Object.freeze(person);
person.age = 29;
alert(person.age);      //undefined
delete person.name;
alert(person.name);     //"Nicholas"
person.name = "Greg";
alert(person.name);     //"Nicholas"
```

## FrozenObjectsExample01.htm

与防止扩展和密封一样，在冻结对象上执行禁止的操作尝试在非严格模式下会被忽略，而在严格模式下会抛出错误。

还有一个 `Object.isFrozen()` 方法用于检测冻结对象。由于冻结对象既是密封的不可扩展的，它们在调用 `Object.isExtensible()` 时返回 `false`，在调用 `Object.isSealed()` 时返回 `true`：

![image](img/logo1.gif)

```javascript
var person = { name: "Nicholas" };
alert(Object.isExtensible(person));   //true
alert(Object.isSealed(person));       //false
alert(Object.isFrozen(person));       //false
Object.freeze(person);
alert(Object.isExtensible(person));   //false
alert(Object.isSealed(person));       //true
alert(Object.isFrozen(person));       //true
```



`FrozenObjectsExample02.htm`

冻结对象对库作者特别有用。JavaScript 库的一个非常常见的问题是人们无意中（或故意）更改了主库对象。冻结主库对象（或密封）可以帮助防止此类错误。

# 高级定时器

使用 `setTimeout()` 或 `setInterval()` 创建的定时器可以实现有趣且实用的功能。尽管人们误认为 JavaScript 中的定时器实际上是线程，但 JavaScript 在单线程环境中运行。因此，定时器仅仅是安排代码在未来的某个点执行。执行的时机是不保证的，因为其他代码可能会在生命周期的不同时间控制 JavaScript 进程。页面下载时运行的代码、事件处理程序和 Ajax 回调都必须使用同一个线程执行。在页面生命周期的某个时间点哪些代码具有优先级是浏览器的任务。

将 JavaScript 想象成运行在时间轴上是有帮助的。当页面加载时，第一个执行的代码是任何通过 `<script>` 包含的代码。这通常只是为了以后在页面生命周期期间使用的函数和变量声明，但有时也可以包含初始数据处理。从那之后，JavaScript 进程会等待更多代码执行。当进程空闲时，将要触发的下一个代码会立即执行。例如，当点击按钮时，`onclick` 事件处理程序会立即执行，只要 JavaScript 进程没有执行任何其他代码。此类页面的时间轴可能看起来如图 22-1](#Chapter22.html_figure22-1)。

## 图 22-1

![image](img/f746-01.jpg)

除了主 JavaScript 执行进程外，还有一个代码队列，在进程下次空闲时应该执行代码。随着页面经历其生命周期，代码按照其应该执行的顺序被添加到队列中。例如，当点击按钮时，其事件处理程序代码被添加到队列中，并在下一个可能的时刻执行。当接收到 Ajax 响应时，回调函数代码被添加到队列中。JavaScript 中没有代码是立即执行的；它会在进程空闲立即执行。

定时器通过在经过特定时间后插入代码与此队列工作。注意，将代码添加到队列并不意味着它会立即执行；它仅仅意味着它将尽快执行。设置在 150 毫秒后执行的定时器并不意味着代码将在 150 毫秒后执行；它意味着代码将在 150 毫秒后被添加到队列中。如果在那个点队列中没有其他代码，定时器代码将执行，给出代码恰好在指定时间执行的假象。在其他时间，代码可能需要更长的时间执行。

考虑以下代码：

```javascript
var btn = document.getElementById("my-btn");

btn.onclick = function(){

    setTimeout(function(){

        document.getElementById("message").style.visibility = "visible";

    }, 250);

    //other code

};
```

在这里，为按钮设置了事件处理程序。该事件处理程序设置了一个 250 毫秒后调用的定时器。当点击按钮时，`onclick` 事件处理程序首先被添加到队列。当它执行时，设置了定时器，250 毫秒后，指定的代码被添加到队列中。

关于定时器最重要的一点是，指定的时间间隔是指代码何时被添加到队列，而不是它何时被执行。如果上例中的事件处理程序执行了 300 毫秒，那么定时器代码最早将在设置 300 毫秒后执行。队列中的所有代码都必须等待 JavaScript 进程空闲才能执行（见图 22-2](#Chapter22.html_figure22-2)）。

![image](img/f747-01.jpg)

从图 22-2](#Chapter22.html_figure22-2)中可以看出，尽管定时器代码在 250 毫秒处被添加，但它在当时无法执行，因为事件处理程序仍在运行。定时器代码首次执行的机会是在 300 毫秒处，此时事件处理程序已经完成。

Firefox 对定时器的实现实际上允许你确定定时器延迟了多少。它通过传入执行时间与指定间隔之间的差值来实现这一点。这里有一个示例：

```javascript
// 仅适用于 Firefox

setTimeout(function(diff){

    if (diff > 0) {

        // 调用延迟了

    } else if (diff < 0){

        // 调用提前了

    } else {

        // 准时调用

    }

}, 250);
```

当一组代码执行完成后，JavaScript 进程会短暂让位，以便页面上的其他进程可以执行。由于 JavaScript 进程会阻塞其他页面进程，这些短暂的休息是必要的，防止用户界面锁定（这在长时间运行期间可能会发生）。设置定时器确保在执行定时器代码之前至少一次进程中断。

# 重复定时器

使用 `setInterval()` 创建的定时器可以定期向队列注入定时器代码。这种方法的问题是，定时器代码在再次添加到队列之前可能尚未完成执行。结果是定时器代码连续运行多次，之间没有任何间隔。幸运的是，JavaScript 引擎足够聪明可以避免这个问题。使用 `setInterval()` 时，只有当队列中没有其他相同的定时器代码时，才会将其添加到队列中。这确保了定时器代码添加到队列之间的时间至少是指定的间隔。

这种对重复定时器的调节有两个负面影响：(1) 间隔可能会被跳过，(2) 在多次定时器-代码执行之间，间隔可能会比预期短。假设有这样一种情况：`onclick` 事件处理器使用 `setInterval()` 设置了一个每隔 200 毫秒执行一次的重复定时器。如果事件处理程序的完成需要略超过 300 毫秒，而定时器代码执行也需要相当的时间，你最终将面临间隔被跳过以及定时器代码连续运行的情况（参见图 22-3）。

## 图 22-3

![image](img/f749-01.jpg)

此示例中的第一个定时器在 205 毫秒时被添加到队列，但直到 300 毫秒之后才能执行。在定时器代码执行期间，另一个副本在 405 毫秒时被添加到队列。在下一个间隔 605 毫秒处，第一个定时器代码仍在执行，且队列中已经有一个定时器代码实例。结果是，此时定时器代码不会被添加到队列。在 405 毫秒时添加的定时器代码将在 5 毫秒时添加的定时器代码之后立即执行。

为了避免使用 `setInterval()` 重复定时器的两个缺陷，你可以按照以下模式使用链式 `setTimeout()` 调用：

```javascript
setTimeout(function(){

    //处理逻辑

    setTimeout(arguments.callee, interval);

}, interval);
```

这种模式将 `setTimeout()` 调用链联起来，在每次执行函数时都会创建一个新的定时器。第二次 `setTimeout()` 调用使用 `arguments.callee` 获取当前执行函数的引用，并为它设置另一个定时器。其优势处是，在上一个定时器代码执行之前，新的定时器代码不会被插入队列，从而确保不会有任何间隔丢失。此外，你还可以保证下一次执行定时器代码时，其间隔时间至少为指定的间隔，从而避免了连续运行。这种模式最用于重复定时器，如下例所示：

![image](img/logo1.gif)

```javascript
setTimeout(function(){

    var div = document.getElementById("myDiv"),
        left = parseInt(div.style.left) + 5;

    div.style.left = left + "px";

    if (left < 200){

        setTimeout(arguments.callee, 50);

    }

}, 50);
```

`RepeatingTimersExample.htm`

这段代码在每次定时器代码执行时将 `<div>` 元素向右移动，当左坐标达到 200 像素时停止。这种模式在 JavaScript 动画中非常常见。

![image](img/pen.gif)

每个浏览器窗口、标签页或帧都有自己的代码执行队列。这意味着跨帧或跨窗口的 JavaScript 调用的计时在代码同步执行时可能会导致竞态条件。每当需要这种通信时，在接收端的帧或窗口上创建一个定时器来执行代码是一个好主意。

## 产出进程（Yielding Processes）

在浏览器中运行的 JavaScript 拥有的资源是有限的。与桌面应用程序通常对内存和处理器时间有自由控制权不同，JavaScript 受到严格限制，以确保恶意的 Web 程序员不会导致用户的计算机崩溃。限制之一是长时间运行脚本限制，它防止代码运行时间超过特定时长或执行语句数量。如果你达到了该限制，用户将看到一个浏览器错误对话框，指示脚本执行时间过长，并询问用户是否允许其继续处理或停止。所有 JavaScript 开发者的目标都是确保用户永远不会看到来自浏览器的这种困惑信息。定时器是规避这一限制的一种方法。

长时间运行脚本的问题通常源于两个问题之一：长时间、深嵌套的函数调用，或者正在大量处理的循环。在这两个问题中，后者更容易解决。长时间运行的循环通常遵循这种模式：

```javascript
for (var i=0, len=data.length; i < len; i++){

    process(data[i]);

}
```

这种模式的问题是，在运行时之前不知道要处理的项数。如果 `process()` 完成需要 100 毫秒，那么一个包含两个元素的数组可能不需要担心，但一个包含十个元素的数组会导致脚本运行一秒钟完成。完全执行此循环所需的时间与数组中的项目数量直接相关。由于 JavaScript 执行是阻塞操作，脚本运行时间越长，用户无法与页面进行交互的时间就越长。

在拆解循环之前，你需要回答这两个重要问题：

1. 处理必须同步完成吗？如果对这些数据的处理阻塞了其他任务的完成，那么你可能不想触碰它。然而，如果你对这个问题能给出肯定的“否”，那么它就是将部分处理推迟到以后的良好候选对象。
2. 数据必须按顺序处理吗？通常情况下，值数组只是分组和迭代项的一种方便方式，无论顺序如何。如果项的顺序没有意义，那么你可能可以将某些处理推迟到以后。

当你发现一个循环完成需要大量时间，并且你对上述两个问题中的任一个可以回答“否”时，你可以使用以下技术将控制权交回浏览器：

```javascript
setTimeout(function(){

    //获取下一项并处理它

    var item = array.shift();

    process(item);

    //如果还有更多项，设置另一个定时器

    if(array.length > 0){

        setTimeout(arguments.callee, 100);

    }

}, 100);
```

在数组分片模式中，`array` 变量本质上是一个待处理项的“待事项列表”。使用 `shift()` 方法，你从队列中获取下一个要处理的项并将其传递给函数。如果队列中仍有项，则设置另一个定时器，通过 `arguments.callee` 调用同一个函数。你可以使用以下函数轻松实现数组分片：

![image](img/logo1.gif)

```javascript
function chunk(array, process, context){

    setTimeout(function(){

        var item = array.shift();

        process.call(context, item);

        if (array.length > 0){

            setTimeout(arguments.callee, 100);

        }

    }, 100);

}
```

`ArrayChunkingExample.htm`

`chunk()` 方法接受三个参数：要处理的项数组、用于处理项的函数、以及运行该函数的可选上下文。函数内部是之前描述的基本模式的复制，通过 `call()` 调用 `process()` 函数以便在需要时设置正确的上下文。定时器的间隔设置为 100 毫秒，这为 JavaScript 进程在处理事件之间留出了空闲时间。此间隔可以根据你的需求更改，尽管 100 毫秒在大多数情况下效果良好。该函数的用法如下：

![image](img/logo1.gif)

```javascript
var data = [12,123,1234,453,436,23,23,5,4123,45,346,5634,2234,345,342];

function printValue(item){

    var div = document.getElementById("myDiv");

    div.innerHTML += item + "<br>";

}

chunk(data, printValue);
```

`ArrayChunkingExample.htm`

此示例通过 `printValue()` 函数将 `data` 数组中的每个值输出到 `<div>` 元素中。由于函数存在于全局作用域，因此向 `chunk()` 传递上下文对象。

需要注意的是，传递给 `chunk()` 的数组被用作队列，因此随着数据的进行，数组中的项会发生变化。如果你想保持原始数组完整，应该将数组的克隆传递给 `chunk()`，例如例所示：

```javascript
chunk(data.concat(), printValue);
```

当对不带任何参数的数组调用 `concat()` 方法时，它会返回一个与原始数组项相同的数组。通过这种方式，你可以确保原始数组不会被函数修改。

数组分片（chunking）的重要性在于它将多个项目的处理拆分为执行队列上的独立代码。在处理完每个项目后，其他浏览器进程将有机会运行，从而避免由于长时间运行脚本导致的错误。

![image](img/pen.gif)

每当你有一个完成时间超过 50 毫秒的函数时，最好检查是否可以将该任务分成若干个较小的、可以使用定时器的任务。

## 函数节流（Function Throttling）

在浏览器中，某些计算和处理比其他更消耗资源。例如，DOM 操作比非 DOM 交互需要更多的内存和 CPU 时间。尝试连续执行过多的 DOM 相关操作可能会导致浏览器挂起，有时甚至会崩溃。这在 Internet Explorer 中使用 `onresize` 事件处理器时经常发生，因为当浏览器调整大小时，该事件会反复触发。在 `onresize` 事件处理器内部尝试进行 DOM 操作可能会因为计算频率过高而导致浏览器崩溃。为了解决这个问题，你可以使用定时器对函数调用进行节流。

函数节流的背后原理是，某些代码不应该在没有间隔的情况下重复执行。当函数第一次被调用时，会创建一个定时器，在指定的间隔后运行代码。当函数第二次被调用时，它会清除上一个定时器并设置另一个。如果之前的定时器已经执行，则没有影响。然而，如果之前的定时器还没有执行，它本质上会被一个较新的定时器取代。其目标是在执行该函数的请求停止一段时间后才执行该函数。以下是该模式的基本表示形式：

```javascript
var processor = {

    timeoutId: null,

    // 实际执行处理的方法

    performProcessing: function(){

        // 实际处理代码

    },

    // 调用此方法以启动处理

    process: function(){

        clearTimeout(this.timeoutId);

        var that = this;

        this.timeoutId = setTimeout(function(){

            that.performProcessing();

        }, 100);

    }

};

// 尝试开始处理

processor.process();
```

在此段代码中，创建了一个名为 `processor` 的对象。该对象有两个方法：`process()` 和 `performProcessing()`。前者是应该被调用以启动任何处理的方法，而后者实际执行应该完成的处理。当调用 `process()` 时，第一步是清除存储的 `timeoutId` 以防止任何之前的调用被执行。然后，创建一个新的定时器来调用 `performProcessing()`。由于 `setTimeout()` 中使用的函数上下文始终是 `window`，因此有必要存储它的引用以便稍后使用。

间隔被设置为 100 毫秒，这意味着在最后一次调用 `process()` 之后至少 100 毫秒后，才会被调用 `performProcessing()`。因此，如果在这 100 毫秒内调用了 20 次 `process()`，`performProcessing()` 仍然只会被一次。

可以通过使用 `throttle()` 函数来简化这种模式，该函数可以自动设置定时器的设置/清除功能，如下例所示：

![image](img/logo1.gif)

```javascript
function throttle(method, context) {

    clearTimeout(method.tId);

    method.tId = setTimeout(function(){

        method.call(context);

    }, 100);

}
```




### ThrottlingExample.htm

`throttle()` 函数接受两个参数：要执行的函数和执行它的作用域。该函数首先清除之前设置的任何定时器。定时器 ID 存储在方法的 `tId` 属性上，在第一次将方法传递 `throttle()` 时，该属性可能不存在。接下来，创建一个新的定时器并将其 ID 存储在方法的 `tId` 属性中。如果这是第一次使用该方法调用 `throttle()`，则代码会创建该属性。定时器代码使用 `call()` 来确保在适当的上下文中执行方法。如果没有提供第二个参数，则方法将在全局作用范围内执行。

如之前所述，节流最常用于 `resize` 事件期间。如果你根据此事件更改页面布局，最好对处理进行节流，以确保浏览器不会在短时间内进行过多的计算。例如，考虑有一个 `<div>` 元素，其高度应该更改为始终与其宽度相等。实现此更改的 JavaScript 代码可能如下：

```javascript
window.onresize = function(){

    var div = document.getElementById("myDiv");

    div.style.height = div.offsetWidth + "px";

};
```

这个非常简单的示例展示了可能会减慢浏览器的点。首先，正在计算 `offsetWidth` 属性，当元素和页面其余部分应用了足够的 CSS 样式时，可能是一个复杂的计算。其次，设置元素的高度需要页面重流（reflow）以考虑这些变化。再次，如果页面有许多元素和适量的 CSS，这可能需要多次计算。`throttle()` 函数可以帮助，如示例所示：

![image](img/logo1.gif)

```javascript
function resizeDiv(){

    var div = document.getElementById("myDiv");

    div.style.height = div.offsetWidth + "px";

}

window.onresize = function(){

    throttle(resizeDiv);

};
```

## 自定义事件

在本书之前，你学习了事件是 JavaScript 与浏览器交互的主要方式。事件是一种称为观察者模式（observer pattern）的设计模式，这是一种创建松耦合代码的技术。其核心思想是对象可以发布事件，指示对象生命周期中发生的有趣的时刻。其他对象可以观察该对象，等待这些有趣时刻的发生并通过运行代码做出响应。

观察者模式由两种类型的对象组成：主体（subject）和观察者（observer）。主体负责发布事件，而观察者只需通过订阅这些事件来观察主体。该模式的关键概念是主体对观察者一无所知，这意味着即使观察者不存在，也可以正常运行。相反，观察者知道主体，并为主体的事件注册回调函数（事件处理器）。

事件是与 `DOM` 交互的一种常见方式，但也可以通过实现自定义事件在非 `DOM` 代码中使用。自定义事件背后的思想是创建一个管理事件的对象，允许其他部分监听这些事件。实现此功能的基本类型可以定义如下：

![image](img/logo1.gif)

```javascript
function EventTarget(){

    this.handlers = {};    

}

EventTarget.prototype = {

    constructor: EventTarget,

    addHandler: function(type, handler){

        if (typeof this.handlers[type] == "undefined"){

            this.handlers[type] = [];

        }

        this.handlers[type].push(handler);

    },

    fire: function(event){

        if (!event.target){

            event.target = this;

        }

        if (this.handlers[event.type] instanceof Array){

            var handlers = this.handlers[event.type];

            for (var i=0, len=handlers.length; i < len; i++){

                handlersi;

            }

        }            

    },

    removeHandler: function(type, handler){

        if (this.handlers[type] instanceof Array){

            var handlers = this.handlers[type];

            for (var i=0, len=handlers.length; i < len; i++){

                if (handlers[i] === handler){

                    break;

                }

            }

            handlers.splice(i, 1);

        }            

    }

};
```

### EventTarget.js

`EventTarget` 类型有一个属性 `handlers`，用于存储事件处理器。它还有三个方法：`addHandler()`，用于为特定类型的事件注册事件处理器；`fire()`，用于触发事件；以及 `removeHandler()`，用于取消某个事件类型事件处理器的注册。

`addHandler()` 方法接受两个参数：事件类型和用于处理事件的函数。当调用此方法时，程序会检查 `handlers` 属性上是否已存在该事件类型的数组。如果不存在，则创建一个。然后使用 `push()` 将处理器添加到数组末尾。

当必须触发事件时，会调用 `fire()` 方法。该方法接受一个参数，即一个包含至少一个 `type` 属性的对象。`fire()` 方法首先在事件对象上设置 `target` 属性（如果尚未指定）。然后它简单地查找该事件类型的处理器数组，并调用每个函数，传入事件对象。由于这些是自定义事件，事件对象上还应该包含哪些额外信息由你来决定。

`removeHandler()` 方法是 `addHandler()` 的伴侣方法，接受相同的参数：事件类型和事件处理器。该方法遍历事件处理器数组以找到要删除的处理器的位置。找到后，使用 `break` 运算符退出 `for` 循环。然后使用 `splice()` 方法从数组中仅删除该项。

使用 `EventTarget` 类型的自定义事件可以如下所示所示：

![image](img/logo1.gif)

```javascript
function handleMessage(event){

    alert("Message received: " + event.message);

}

// 创建一个新对象

var target = new EventTarget();

// 添加事件处理器

target.addHandler("message", handleMessage);

// 触发事件

target.fire({ type: "message", message: "Hello world!"});

// 移除处理器

target.removeHandler("message", handleMessage);

// 再次尝试 - 不应该有处理器了

target.fire({ type: "message", message: "Hello world!"});
```

### EventTargetExample01.htm

在此代码中，定义了 `handleMessage()` 函数来处理消息事件。它接受事件对象并输出 `message` 属性。调用了 `target` 对象的 `addHandler()` 方法，传入 `"message"` 和 `handleMessage` 函数。在下一行，调用 `fire()` 并传入一个包含两个属性（`type` 和 `message`）的字面量对象。这会调用消息事件的事件处理器，从而显示警框（来自 `handleMessage()`）。随后移除了事件处理器，因此当再次触发事件时，不会显示警框。

由于此功能被封装在一个自定义类型中，其他对象可以通过继承 `EventTarget` 来获得这种行为，例如例所示：

![image](img/logo1.gif)

```javascript
function Person(name, age){

    EventTarget.call(this);

    this.name = name;

    this.age = age;

}

inheritPrototype(Person,EventTarget);

Person.prototype.say = function(message){

    this.fire({type: "message", message: message});

};
```

### EventTargetExample02.htm

`Person` 类型使用寄生组合继承（见第 6 章）继承自 `EventTarget`。每当调用 `say()` 方法时，都会触发一个带有消息详情的事件。在类型的其他方法中调用 `fire()` 方法很常见，但在公开方法调用它非常罕见。此代码可以如下所示使用：

```javascript
function handleMessage(event){

    alert(event.target.name + " says: " + event.message);

}

// 创建新人物

var person = new Person("Nicholas", 29);

// 添加事件处理器

person.addHandler("message", handleMessage);

// 调用对象的方法，触发消息事件

person.say("Hi there.");
```

EventTargetExample02.htm

此示例中的 `handleMessage()` 函数显示一个警框，其中包含姓名（通过 `event.target.name` 获取）和消息文本。当带消息调用 `say()` 方法时，会触发事件。这反过来又调用了 `handleMessage()` 函数并显示警框。

### 拖放与放置

计算机上最流行的用户界面模式之一是拖放。其思想非常简单：在项目上点击并按住鼠标键，将鼠标移动到另一个区域，释放鼠标键将项目“放置”在该处。拖放界面的流行扩展到了 Web 端，它已成为传统配置界面的流行替代方案。

拖放的基本思想非常简单：创建一个可以随鼠标移动的绝对定位元素。这种技术源于一种名为“光标轨迹”的经典网页技巧。光标轨迹是跟随指针移动的图像或多幅图像。单项目光标轨迹的基本代码涉及在文档上设置 `mousemove` 事件处理器，始终将给定元素移动到光标位置，如例所示：

```javascript
EventUtil.addHandler(document, "mousemove", function(event){

    var myDiv = document.getElementById("myDiv");

    myDiv.style.left = event.clientX + "px";

    myDiv.style.top = event.clientY + "px";

});
```

```javascript
var DragDrop = function(){

    var dragging = null;

    function handleEvent(event){

        //get event and target

        event = EventUtil.getEvent(event);

        var target = EventUtil.getTarget(event);            

        //determine the type of event

        switch(event.type){

            case "mousedown":

                if (target.className.indexOf("draggable") > -1){

                    dragging = target;

                }                     

                break;

            case "mousemove":

                if (dragging !== null){

                    //assign location

                    dragging.style.left = event.clientX + "px";

                    dragging.style.top = event.clientY + "px";                    

                }                    

                break;

            case "mouseup":

                dragging = null;

                break;

        }

    };

    //public interface

    return {            

        enable: function(){

            EventUtil.addHandler(document, "mousedown", handleEvent);

            EventUtil.addHandler(document, "mousemove", handleEvent);

            EventUtil.addHandler(document, "mouseup", handleEvent);

        },

        disable: function(){

            EventUtil.removeHandler(document, "mousedown", handleEvent);

            EventUtil.removeHandler(document, "mousemove", handleEvent);

            EventUtil.removeHandler(document, "mouseup", handleEvent);

        }

    }

}();
```

### DragAndDropExample02.htm

`DragDrop` 对象封装了所有的基础拖放功能。它是一个单例对象，使用模块模式来隐藏其部分实现细节。`dragging` 变量初始为 `null`，之后会被正在被拖拽的元素填充，因此当该变量不为 `null` 时，你就知道有元素正在被拖动。

`handleEvent()` 函数处理拖放功能所需的所有三个鼠标事件。它首先获取事件对象和事件目标的引用。随后，通过 `switch` 语句判断触发了哪种事件类型。当发生 `mousedown` 事件时，会检查 `target` 的类名，以确定其是否包含 `"draggable"` 类，如果是，则将 `target` 赋值给 `dragging`。这种技术允许通过标记语言而不是 JavaScript 轻松地指示可拖拽元素。

`handleEvent()` 的 `mousemove` 分支与之前的代码相同，区别在于会检查 `dragging` 是否为 `null`。当它不为 `null` 时，已知 `dragging` 是正在被拖拽的元素，因此对其进行相应的定位。`mouseup` 分支简单是将 `dragging` 重置为 `null`，这有效地抵消了 `mousemove` 事件。

`DragDrop` 有两个公共方法：`enable()` 和 `disable()`，它们分别绑定和解绑所有事件处理程序。这些方法为拖放功能提供了额外的控制手段。

要使用 `DragDrop` 对象，只需将其包含在页面中并调用 `enable()`。所有类包含 `"draggable"` 的元素都将自动启用拖放功能，例如所示：

```html
<div class="draggable" style="position:absolute; background:red"></</div>
```




注意，为了让元素支持拖放功能，它必须是绝对定位的。

### 自定义拖拽功能

当你尝试这个示例时，你会发现元素的左上角总是对齐光标。这种结果对用户来说有些突兀，因为当鼠标开始移动时，元素似乎会发生跳动。理想情况下，动作看起来应该像元素被光标“捡起”一样，这意味着用户点击的点应该是元素在拖拽期间光标停留的位置（参见图 22-4）。

图 22-4

![image](img/f760-01.jpg)

为了达到所需的效果，需要额外的计算。为此，你需要计算元素左上角与光标位置之间的差异。该差异需要在`mousedown`事件发生时确定，并一直持续到`mouseup`事件发生。通过比较`event`的`clientX`和`clientY`属性与元素的`offsetLeft`和`offsetTop`属性，你可以算出在水平和垂直方向上还需要多大的空间（参见图 22-5）。

图 22-5

![image](img/f760-02.jpg)

为了存储`x`和`y`轴的差异，你还需要几个变量。这些变量`diffX`和`diffY`需要在`onmousemove`事件处理程序中使用，以正确定位元素，如下例所示：

![image](img/logo1.gif)

```javascript
var DragDrop = function(){

    var dragging = null,

        diffX = 0,

        diffY = 0;

    function handleEvent(event){

        //get event and target

        event = EventUtil.getEvent(event);

        var target = EventUtil.getTarget(event);            

        //determine the type of event

        switch(event.type){

            case "mousedown":

                if (target.className.indexOf("draggable") > -1){

                    dragging = target;

                    diffX = event.clientX - target.offsetLeft;

                    diffY = event.clientY - target.offsetTop;

                }                     

                break;

            case "mousemove":

                if (dragging !== null){

                    //assign location

                    dragging.style.left = (event.clientX - diffX) + "px";

                    dragging.style.top = (event.clientY - diffY) + "px";                    

                }                    

                break;

            case "mouseup":

                dragging = null;

                break;

        }

    };

    //public interface

    return {            

        enable: function(){

            EventUtil.addHandler(document, "mousedown", handleEvent);

            EventUtil.addHandler(document, "mousemove", handleEvent);

            EventUtil.addHandler(document, "mouseup", handleEvent);

        },

        disable: function(){

            EventUtil.removeHandler(document, "mousedown", handleEvent);

            EventUtil.removeHandler(document, "mousemove", handleEvent);

            EventUtil.removeHandler(document, "mouseup", handleEvent);

        }

    }

}();
```

### DragAndDropExample03.htm

`diffX`和`diffY`变量是私有的，因为它们仅供`handleEvent()`函数使用。当`mousedown`事件发生时，它们通过从`target`的`clientX`减去`offsetLeft`以及从`clientY`减去`offsetTop`来计算。这些值提供了在`mousemove`事件触发时在每个维度上需要减去的量。结果是更平滑的拖拽体验，其行为更符合用户的预期。

### 添加自定义事件

除非你知道拖拽发生的时间，否则拖放功能无法真正在应用程序中使用。到目前为止，代码没有提供任何指示拖拽已开始、进行中或结束的方法。可以使用自定义事件来指示这些情况的发生，从而允许应用程序的其他部分与拖放功能进行交互。

由于`DragDrop`对象是使用模块模式的单例，为了使用`EventTarget`类型需要进行一些更改。首先，创建一个新的`EventTarget`对象，然后添加`enable()`和`disable()`方法，最后返回该对象。考虑以下内容：

![image](img/logo1.gif)

```javascript
var DragDrop = function(){

    var dragdrop = new EventTarget(),

        dragging = null,

        diffX = 0,

        diffY = 0;

    function handleEvent(event){

        //get event and target

        event = EventUtil.getEvent(event);

        var target = EventUtil.getTarget(event);            

        //determine the type of event

        switch(event.type){

            case "mousedown":

                if (target.className.indexOf("draggable") > -1){

                    dragging = target;

                    diffX = event.clientX - target.offsetLeft;

                    diffY = event.clientY - target.offsetTop;

                    dragdrop.fire({type:"dragstart", target: dragging, 

                                   x: event.clientX, y: event.clientY});

                }                    

                break;

            case "mousemove":

                if (dragging !== null){

                    //assign location

                    dragging.style.left = (event.clientX - diffX) + "px";

                    dragging.style.top = (event.clientY - diffY) + "px";   

                    //fire custom event

                    dragdrop.fire({type:"drag", target: dragging, 

                                   x: event.clientX, y: event.clientY});

                }                    

                break;

            case "mouseup":

                dragdrop.fire({type:"dragend", target: dragging, 

                               x: event.clientX, y: event.clientY});

                dragging = null;

                break;

        }

    };

    //public interface

    dragdrop.enable = function(){

        EventUtil.addHandler(document, "mousedown", handleEvent);

        EventUtil.addHandler(document, "mousemove", handleEvent);

        EventUtil.addHandler(document, "mouseup", handleEvent);

    };

    dragdrop.disable = function(){

        EventUtil.removeHandler(document, "mousedown", handleEvent);

        EventUtil.removeHandler(document, "mousemove", handleEvent);

        EventUtil.removeHandler(document, "mouseup", handleEvent);

    };

    return dragdrop;

}();
```

`DragAndDropExample04.htm`

这段代码定义了三个事件：`dragstart`、`drag`和`dragend`。这些事件中的每一个都会拖拽元素设置为目标，并提供`x`和`y`属性来指示其当前位置。这些事件在`dragdrop`对象上触发，该对象在返回之前被了`enable()`和`disable()`方法。这种模块模式的细微变化允许`DragDrop`对象支持如下事件：

![image](img/logo1.gif)

```javascript
DragDrop.addHandler("dragstart", function(event){

    var status = document.getElementById("status");

    status.innerHTML = "Started dragging " + event.target.id;

});

DragDrop.addHandler("drag", function(event){

    var status = document.getElementById("status");

    status.innerHTML += "<br>Dragged " + event.target.id + " to (" + event.x + 

                        "," + event.y + ")";

});

DragDrop.addHandler("dragend", function(event){

    var status = document.getElementById("status");

    status.innerHTML += "<br>Dropped " + event.target.id + " at (" + event.x + 

                        "," + event.y + ")";

});
```

`DragAndDropExample04.htm`

在这里，为`DragDrop`对象的每个事件添加了事件处理程序。使用一个元素来显示拖拽元素的当前状态和位置。一旦元素被释放，你将获得它从最初被拖拽以来所的所有中间步骤的列表。

为`DragDrop`添加自定义事件使其成为更健壮的对象，可以用于管理 Web 应用程序中复杂的拖放功能。

## 总结

JavaScript 中的函数非常强大，因为它们是一等对象。通过闭包和函数上下文切换，你可以以多种强大的方式使用函数。例如：

*   可以创建范围安全的构造函数，确保在没有使用`new`运算符的情况下调用的构造函数不会改变错误的上下文对象。
*   你可以使用延迟加载函数，通过延迟任何代码分支直到该函数第一次被调用。
*   函数绑定（Function binding）允许你创建始终在特定上下文中运行的函数，而函数柯里化（Function currying）允许你创建某些参数已经填充好的函数。
*   结合绑定和柯里化可以为你提供一种在任何上下文、以任何参数执行任何函数的方法。

ECMAScript 5 允许你通过多种不同的方式创建防篡改对象：

*   不可扩展对象（Nonextensible objects）不允许向对象添加新的属性或方法。
*   密封对象（Sealed objects）是不可扩展的，且不允许删除现有的属性和方法。
*   冻结对象（Frozen objects）是密封的，并且不允许覆盖对象的成员。

在 JavaScript 中可以使用`setTimeout()`或`setInterval()`创建定时器，如下：

*   定时器代码被放置在一个等待区域，直到达到间隔时间，此时代码会被添加到 JavaScript 执行队列中，以便下一次 JavaScript 进程空闲时执行。
*   每当一段代码完全执行完毕，都会有短暂的空闲时间允许其他浏览器进程完成。
*   这种行为意味着可以使用定时器将长时间运行的脚本拆分成较小的块，并在稍后执行。这样做有助于 Web 应用程序对用户交互做出更响应。

观察者模式以事件的形式经常在 JavaScript 中使用。虽然事件经常用于 DOM，但你也可以通过实现自定义事件在自己的代码中使用它们。使用自定义事件有助于代码部分之间的解耦，便于维护并减少引入错误。

## 第 23 章 离线应用程序与客户端存储

### 本章内容

*   设置离线检测
*   使用离线缓存
*   在浏览器中存储数据

HTML5 的关注领域之一是启用离线应用程序。离线 Web 应用程序在设备没有 Internet 连接的情况下仍然工作。这种关注基于 Web 开发者希望更好地竞争只要设备有电即可使用的传统客户端应用程序。

对于 Web 应用程序，创建离线体验需要几个步骤。第一步是确保应用程序知道 Internet 是否可用以便执行正确的操作。然后，应用程序仍然需要访问资源（图像、JavaScript、CSS 等）以便继续正常工作。最后一部分是本地数据存储区域，无论 Internet 是否可用都可以进行读写。HTML5 以及相关的 JavaScript API 使离线应用程序成为现实。

## 离线检测

由于离线应用程序的第一步是知道设备是否离线，HTML5 定义了`navigator.onLine`，当 Internet 连接可用时为真，不可用时为假。其理念是浏览器应该感知网络是否可用并返回相应的指示。在实践中，`navigator.onLine`在不同浏览器中表现有些异：

*   Internet Explorer 6+ 和 Safari 5+ 能够正确检测到网络连接已丢失并将`navigator.onLine`切换为 false。
*   `Firefox 3+`和`Opera 10.6+`支持`navigator.onLine`，但你必须通过“文件 ⇒ 离工作”菜单项手动将浏览器设置为离线模式。
*   `Chrome`直到版本 11 都将`navigator.onLine`永久设置为`true`。目前有一个待修复的 bug 来解决此问题。

由于这些兼容性问题，`navigator.onLine`不能作为网络连接的唯一判断标准。尽管如此，在请求过程中发生错误时，它仍然有用。你可以按照以下方式检查状态：

![image](img/logo1.gif)

```javascript
if (navigator.onLine){

    //照常工作

} else {

    //执行离线行为

}
```

OnlineExample01.htm

除了`navigator.onLine`，HTML5 还定义了两个事件以更好地跟踪网络是否可用：`online`和`offline`。当网络状态从`online`变为`offline`或反之时，这两个事件会被分别触发。这些事件在`window`对象上触发：



`EventUtil.addHandler(window, "online", function(){`

```
    alert("Online");
});
```

`EventUtil.addHandler(window, "offline", function(){`

```
    alert("Offline");
});
```

`OnlineEventsExample01.htm`

要判断应用程序是否处于离线状态，最好先开始查看`navigator.onLine`以获取页面加载时的初始状态。之后，最好使用事件来确定网络连接的变化。`navigator.onLine`属性也会随着事件的触发而改变，但你需要手动轮询该属性的变化来检测网络变化。

`Internet Explorer 6+`（仅支持`navigator.onLine`）、`Firefox 3`、`Safari 4`、`Opera 10.6`、`Chrome`、`Safari for iOS 3.2`以及`WebKit for Android`都支持离线检测。

## 应用缓存

HTML5 应用缓存，简称`appcache`，专门设计用于离线 Web 应用程序使用。`appcache`是一个独立于普通浏览器缓存的缓存区域。你通过提供一个列出需要下载和缓存的资源的清单文件（manifest file）来指定应该存储在页面的`appcache`中。这是一个简单的清单文件：

```
CACHE MANIFEST
#Comment
file.js
file.css
```

在最简单的形式下，清单文件列出了需要下载的资源，以便在离线时可用。

![image](img/pen.gif)

设置此文件有很多选项，这些内容超出了本书的范围。请参[`html5doctor.com/go-offline-with-application-cache/`](http://html5doctor.com/go-offline-with-application-cache/)获取选项的完整说明。

通过在`<html>`标签的`manifest`属性中指定路径，可以将清单文件与页面关联，例如：

```
<html manifest="/offline.manifest">
```

这段代码表示`/offline.manifest`包含了清单文件。该必须必须`text/cache-manifest`内容类型提供才能使用。

虽然`appcache`主要用于指定资源缓存供离线使用，但它确实有一个 JavaScript API 允许你确定`appcache`正在做什么。用于此的主要对象是`applicationCache`。该对象有一个属性`status`，它用以下常量之一指示`appcache`的当前状态：

* `0`表示未缓存，意味着没有与页面关联的`appcache`。
* `1`表示空闲，意味着`appcache`未更新。
* `2`表示正在检查，意味着正在下载`appcache`清单文件并检查是否有更新。
* `3`表示正在下载，意味着`appcache`正在下载清单文件中指定的资源。
* `4`表示更新就绪，意味着`appcache`已用新资源更新，且所有资源已下载，可以通过`swapCache()`使用。
* `5`表示过时，意味着`appcache`清单文件已失效，因此`appcache`对该页面不再有效。

还有许多与`appcache`相关的事件，用于指示其状态何时发生。这些事件是：

* `checking` — 当浏览器开始寻找`appcache`的更新时触发。
* `error` — 如果在检查或下载序列的任何一点发生错误则触发。
* `noupdate` — 在检查发现`appcache`清单文件未变化后触发。
* `downloading` — 当`appcache`资源开始下载时触发。
* `progress` — 当文件正在下载到`appcache`时反复触发。
* `updateready` — 当页面的新版本`appcache`已下载并准备好通过`swapCache()`使用时触发。
* `cached` — 当`appcache`完成并准备好使用时触发。

这些事件在页面加载时通常按以下顺序触发。你也可以通过调用`update()`触发`appcache`再次经历此更新检查序列：

```
applicationCache.update();
```

一旦调用了`update()`，`appcache`将检查清单文件是否已更新（触发`checking`），然后像页面刚刚加载一样继续。如果触发了`cached`事件，意味着新的`appcache`已可用。如果`updateready`事件触发，意味着新的`appcache`已就绪，可以通过`swapCache()`使用：

```
EventUtil.addHandler(applicationCache, "updateready", function(){
    applicationCache.swapCache();
});
```

## 数据存储

随着 Web 应用程序的出现，对在客户端存储数据的需求。逻辑上是：特定用户的信息应该存储在该用户的机器上。无论是登录信息、偏好设置还是其他数据，Web 应用提供者一直在寻找在客户端存储数据的方法。问题的第一个解决方案是以 Cookie 的形式出现的，它由 Netscape Communications 公司创建并在名为《持久客户端状态：HTTP Cookie》（仍可在 http://curl.haxx.se/cookie_spec.html 查看）的规范中描述。如今，Cookie 只是在客户端存储数据的一种可用方案。

## Cookie

HTTP Cookie（通常称为 Cookie）最初旨在在客户端存储会话信息。规范要求服务器在任何响应中发送包含会话信息的`Set-Cookie`HTTP 头部。例如，服务器响应的头部可能如下：

```
HTTP/1.1 200 OK
Content-type: text/html
Set-Cookie: name=value
Other-header: other-header-value
```

此 HTTP 响应设置了一个名为`name`值`value`的 Cookie。名称和值在发送时都会进行 URL 编码。浏览器存储此类会话信息，并在后的每个请求中通过`Cookie`HTTP 头部传回服务器：

```
GET /index.html HTTP/1.1
Cookie: name=value
Other-header: other-header-value
```

传回服务器的额外信息可用于唯一标识发送请求的客户端。

## 限制

Cookie 本质上绑定到特定域名。当设置 Cookie 时，它会随着向其创建域名的请求一起发送。这一限制确保存储在 Cookie 中的信息仅对批准的接收者可用，无法被其他域名访问。

由于 Cookie 存储在客户端计算机上，已经实施了一些限制以确保 Cookie 不被恶意使用并且不会占用过多磁盘空间。每个域名的 Cookie 总数是有限制的，尽管不同浏览器有所不同。例如：

* Internet Explorer 6 及低版本限制每个域名最多为 20 个 Cookie。
* `Internet Explorer 7`及更高版本限制每个域名最多存储 50 个 cookie。`Internet Explorer 7`最初出厂时每个域名最多支持 20 个 cookie，但后来通过微软的补丁进行了更新。
* `Firefox`每个域名的 cookie 限制为 50 个。
* `Opera`每个域名的 cookie 限制为 30 个。
* `Safari`和`Chrome`对每个域名的 cookie 没有硬性限制。

当设置的 cookie 超过每个域名限制时，浏览器将开始删除之前设置的 cookie。`Internet Explorer`和`Opera`从删除最久未使用（`LRU`）的 cookie 开始，为新设置的 cookie 留空间。`Firefox`似乎随机决定删除哪些 cookie，因此注意 cookie 限制以避免意外之外的后果非常重要。

浏览器对 cookie 的大小也有限制。大多数浏览器的字节数限制在 4096 字节左右（正负 1 字节）。为了获得最佳的跨浏览器兼容性，最好将所有 cookie 总大小保持在 4095 字节或以下。该大小限制适用于某个域名的所有 cookie，而不是每个单独 cookie。

如果你尝试创建一个超过最大 cookie 大小的 cookie，该 cookie 将被静默丢弃。注意，一个字符通常占用一个字节，除非你使用的是多字节字符。

### Cookie 部分

Cookie 由浏览器存储的以下信息组成：

* `Name` — 用于识别 cookie 的唯一名称。Cookie 名称不区分大小写，因此`myCookie`和`MyCookie`被视为相同。但在实践中，最好始终将 cookie 名称视为区分大小写的，因为某些服务器软件可能会将它们视为区分大小写的 cookie。cookie 名称必须经过 URL 编码。
* `Value` — 存储在 cookie 中的字符串值。此值也必须经过 URL 编码。
* `Domain` — cookie 有效的域名。从该域名资源发送的所有请求都将包含 cookie 信息。此值可以包含子域名（例如 [www.wrox.com](http://www.wrox.com)），也可以排除子域名（例如 `.wrox.com`，它对 [wrox.com](http://wrox.com) 的所有子域名有效）。如果没有显式设置，则假设域名为设置 cookie 的域名。
* `Path` — 在指定域名内，cookie 应该发送到服务器的路径。例如，你可以指定 cookie 仅从`http://www.wrox.com/books/`访问，这样位于[`www.wrox.com`](http://www.wrox.com)的页面将不会发送 cookie 信息，即使请求来自同一个域名。
* `Expiration` — 指示 cookie 何时应被删除的时间戳（即它何时停止发送到服务器）。默认情况下，所有 cookie 都在浏览器会话结束时被删除；但也可以设置另一个删除时间。此值以 GMT 格式的日期（`Wdy, DD-Mon-YYYY HH:MM:SS GMT`）设置，并指定 cookie 删除的精确时间。由于此原因，即使浏览器关闭后，cookie 可能会留在用户的机器上。可以通过设置一个已经过去的过期日期来立即删除 cookie。
* `Secure flag` — 如果指定，只有在使用 SSL 连接时，cookie 信息才会被发送到服务器。例如，对`https://www.wrox.com`的请求应该发送 cookie 信息，而对[`www.wrox.com`](http://www.wrox.com)的请求则不应发送。

每项信息都作为`Set-Cookie`头部的一部分指定，使用分号加空格的组合来分隔每个部分，如下例所示：

```
HTTP/1.1 200 OK
Content-type: text/html
Set-Cookie: name=value; expires=Mon, 22-Jan-07 07:10:24 GMT; domain=.wrox.com
Other-header: other-header-value
```

此头部指定了一个名为`"name"`的 cookie，它于 GMT 2007 年 1 月 22 日周一 07:10:24 过期，并对 [www.wrox.com](http://www.wrox.com) 以及 [wrox.com](http://wrox.com) 的任何其他子域名（如 [p2p.wrox.com](http://p2p.wrox.com)）有效。

`secure`标志是 cookie 中唯一键值对的部分；只需包含`"secure"`单词。考虑以下示例：

```
HTTP/1.1 200 OK
Content-type: text/html
Set-Cookie: name=value; domain=.wrox.com; path=/; secure
Other-header: other-header-value
```

在这里，创建的 cookie 对 [wrox.com](http://wrox.com) 的所有子域名该域名上的所有页面（由`path`参数指定）有效。由于包含了`secure`标志，此 cookie 只能通过 SSL 连接传输。

需要注意的是，`domain`、`path`、`expiration date`和`secure`是对浏览器的指示，说明在何时应随请求发送 cookie。这些参数实际上不会作为 cookie 信息的一部分发送到服务器；只有键值对会被发送。

### JavaScript 中的 Cookies

由于界面非常糟糕，在 JavaScript 中处理 cookie 稍微有点复杂，这涉及到 BOM 的`document`对象。

```javascript
var CookieUtil = {
    get: function (name){
        var cookieName = encodeURIComponent(name) + "=",
            cookieStart = document.cookie.indexOf(cookieName),
            cookieValue = null;
        if (cookieStart > -1){
            var cookieEnd = document.cookie.indexOf(";", cookieStart);
            if (cookieEnd == -1){
                cookieEnd = document.cookie.length;
            }
            cookieValue = decodeURIComponent(document.cookie.substring(cookieStart 
                          + cookieName.length, cookieEnd));
        } 
        return cookieValue;
    },
    set: function (name, value, expires, path, domain, secure) {
        var cookieText = encodeURIComponent(name) + "=" + 
                         encodeURIComponent(value);
        if (expires instanceof Date) {
            cookieText += "; expires=" + expires.toGMTString();
        }
        if (path) {
            cookieText += "; path=" + path;
        }
        if (domain) {
            cookieText += "; domain=" + domain;
        }
        if (secure) {
            cookieText += "; secure";
        }
        document.cookie = cookieText;
    },
    unset: function (name, path, domain, secure){
        this.set(name, "", new Date(0), path, domain, secure);
    }
};
```



`CookieUtil.js`

`CookieUtil.get()` 方法根据指定的名称检索 cookie 的值。为了实现这一点，它会在 `document.cookie` 中查找 cookie 名称后跟等号的出现位置。如果找到了该模式，则使用 `indexOf()` 找到该位置之后的下一个分号（这表示 cookie 的结束）。如果没有找到分号，则意味着该 cookie 是字符串中的最后一个 cookie，因此字符串的剩余部分都应该被视为 cookie 的值。该值将使用 `decodeURIComponent()` 进行解码并返回。在未找到 cookie 的情况下，将返回 `null`。

`CookieUtil.set()` 方法在页面上设置 cookie，并接受多个参数：cookie 的名称、cookie 的值、一个指示何时应删除 cookie 的可选 `Date` 对象、一个 cookie 的可选 URL 路径、一个 cookie 的可选域名，以及一个指示是否应添加安全标志的可选 `Boolean` 值。这些参数按照使用频率高低排序，只有前两个是必须的。在方法内部，名称和值使用 `encodeURIComponent()` 进行 URL 编码，然后检查其他选项。如果 `expires` 参数是一个 `Date` 对象，则将使用 `Date` 对象的 `toGMTString()` 方法添加 `expires` 选项，以正确格式化日期。方法的其余部分只是构建 cookie 字符串并将其设置为 `document.cookie`。

没有直接删除现有 cookie 的方法。相反，你需要再次设置 cookie——使用相同的 `path`、`domain` 和 `secure` 选项——并将其过期日期设置为过去的某个时间。`CookieUtil.unset()` 方法处理了这种情况。它接受四个参数：要删除的 cookie 名称、一个可选的 `path` 参数、一个可选的 `domain` 参数和一个可选的 `secure` 参数。

这些参数被传递给 `CookieUtil.set()`，其中值设为空字符串，过期日期设置为 1970 年 1 月 1 日（初始化为 `0` 毫秒的 `Date` 的值的值）。这样做可以确保 cookie 被移除。

这些方法可以如下所示使用：

```javascript
//set cookies
CookieUtil.set("name", "Nicholas");
CookieUtil.set("book", "Professional JavaScript");

//read the values
alert(CookieUtil.get("name"));  //"Nicholas"
alert(CookieUtil.get("book"));  //"Professional JavaScript"

//remove the cookies
CookieUtil.unset("name");
CookieUtil.unset("book");

//set a cookie with path, domain, and expiration date
CookieUtil.set("name", "Nicholas", "/books/projs/", "www.wrox.com",
               new Date("January 1, 2010"));

//delete that same cookie
CookieUtil.unset("name", "/books/projs/", "www.wrox.com");

//set a secure cookie
CookieUtil.set("name", "Nicholas", null, null, null, true);
```

`CookieExample01.htm`

这些方法通过处理解析和 cookie 字符串构建任务，使得使用 cookie 在客户端存储数据变得更加简单。

## 子 cookie (Subcookies)

为了绕过浏览器实施的每个域名 cookie 限制，一些开发者使用了一种称为子 cookie（subcookies）的概念。子 cookie 是存储在单个 cookie 内部的较小数据。其想法是使用 cookie 的值在单个 cookie 中存储多个键值对。子 cookie 最常见的格式如下：

```
name=name1=value1&name2=value2&name3=value3&name4=value4&name5=value5
```

子 cookie 倾向于采用查询字符串格式。这些值随后可以使用单个 cookie 进行存储和访问，而不是为每个键值对使用不同的 cookie。结果是网站或 Web 应用可以存储更多结构化数据，而不会达到每个域名的 cookie 限制。

要处理子 cookie，你需要一组新的方法。由于预期的子 cookie 用，子 cookie 的解析和序列化略有不同且更为复杂。例如，要获取子 cookie，你需要按照相同的步骤获取 cookie，但在解码值之前，你需要找到子 cookie 信息，如下所示：

![image](img/logo.gif)

```javascript
var SubCookieUtil = {
    get: function (name, subName){
        var subCookies = this.getAll(name);
        if (subCookies){
            return subCookies[subName];
        } else {
            return null;
        }
    },
    getAll: function(name){
        var cookieName = encodeURIComponent(name) + "=",
            cookieStart = document.cookie.indexOf(cookieName),
            cookieValue = null,
            cookieEnd,
            subcookies,
            i,
            parts,
            result = {};
        if (cookieStart > -1){
            cookieEnd = document.cookie.indexOf(";", cookieStart);
            if (cookieEnd == -1){
                cookieEnd = document.cookie.length;
            }
            cookieValue = document.cookie.substring(cookieStart 
                          + cookieName.length, cookieEnd);
            if (cookieValue.length > 0){
                subcookies = cookieValue.split("&");
                for (i=0, len=subcookies.length; i < len; i++){
                    parts = subcookies[i].split("=");
                    result[decodeURIComponent(parts[0])] = 
                         decodeURIComponent(parts[1]);
                }
                return result;
            }  
        } 
        return null;
    },
    //more code here
};
```

`SubCookieUtil.js`

有两个方法可以检索子 cookie：`get()` 和 `getAll()`。虽然 `get()` 获取单个子 cookie 值，但 `getAll()` 获取所有子 cookie 并将其封装在一个对象中，其属性等于子 cookie 名称，值等于子 cookie 值。`get()` 方法接受两个参数：cookie 的名称和子 cookie 的名称。它简单调用 `getAll()` 获取所有子 cookie，然后返回感兴趣的（如果 cookie 不存在，则返回 `null`）。

`SubCookieUtil.getAll()` 方法在解析 cookie 方面与 `CookieUtil.get()` 非常相似。不同在于 cookie 值没有立即解码。相反，它使用符号 `&` 进行分割，将所有子 cookie 放入数组。然后，每个子 cookie 使用等号进行分割，以便使部分数组中的第一个项是子 cookie 名称，第二个是子 cookie 值。这两个项都使用 `decodeURIComponent()` 进行解码并赋值给结果对象，结果对象作为方法的值返回。如果 cookie 不存在，则返回 `null`。

```javascript
//假设 document.cookie=data=name=Nicholas&book=Professional%20JavaScript
//获取所有子 cookie
var data = SubCookieUtil.getAll("data");
alert(data.name);  //"Nicholas"
alert(data.book);  //"Professional JavaScript"

//逐个获取子 cookie
alert(SubCookieUtil.get("data", "name"));  //"Nicholas"
alert(SubCookieUtil.get("data", "book"));  //"Professional JavaScript"
```

### SubCookiesExample01.htm

写入子 cookie 时，你可以使用两种方法：`set()` 和 `setAll()`。以下代码展示了它们的结构：

```javascript
var SubCookieUtil = {
    set: function (name, subName, value, expires, path, domain, secure) {
        var subcookies = this.getAll(name) || {};
        subcookies[subName] = value;
        this.setAll(name, subcookies, expires, path, domain, secure);
    },
    setAll: function(name, subcookies, expires, path, domain, secure){
        var cookieText = encodeURIComponent(name) + "=",
            subcookieParts = new Array(),
            subName;
        for (subName in subcookies){
            if (subName.length > 0 && subcookies.hasOwnProperty(subName)){
                subcookieParts.push(encodeURIComponent(subName) + "=" + 
                    encodeURIComponent(subcookies[subName]));
            }
        }
        if (cookieParts.length > 0){
            cookieText += subcookieParts.join("&");
            if (expires instanceof Date) {
                cookieText += "; expires=" + expires.toGMTString();
            }
            if (path) {
                cookieText += "; path=" + path;
            }
            if (domain) {
                cookieText += "; domain=" + domain;
            }
            if (secure) {
                cookieText += "; secure";
            }
        } else {
            cookieText += "; expires=" + (new Date(0)).toGMTString();
        }
        document.cookie = cookieText;        
    },
    //更多代码在此
};
```

### SubCookieUtil.js

`set()` 方法接受七个参数：cookie 名称、子 cookie 名称、子 cookie 值、一个用于设置 cookie 过期日期的可选 `Date` 对象、一个可选的 cookie 路径、一个可选的 cookie 域名以及一个可选的 `Boolean` 安全标志。所有可选参数都指向 cookie 本身，而不是子 cookie。为了在同一个 cookie 中存储多个子 cookie，`path`、`domain` 和 `secure` 标志必须相同；过期日期指的是整个 cookie，并且可以在写入任何单个子 cookie 时进行设置。在方法内部，第一步是根据指定的 cookie 名称检索所有子 cookie。如果 `getAll()` 返回 `null`，则使用逻辑或位操作符将子 cookie 设置为一个新对象。之后，将子 cookie 值设置在 `subcookies` 对象上，然后传递给 `setAll()`。

`setAll()` 方法接受六个参数：cookie 名称、一个包含所有子 cookie 的对象，以及在 `set()` 中使用的其余可选参数。该方法使用 `for-in` 循环遍历第二个参数的属性。为了确保保存了适当的数据，请使用 `hasOwnProperty()` 方法来确保只有实例属性被序列化为子 cookie。由于属性名可能为空字符串，在将其添加到结果之前还会检查属性名的长度。每个子 cookie 键值对都会添加到 `subcookieParts` 数组中，以便以后可以使用 `join()` 方法使用 `&` 符号连接。该方法的其余部分与 `CookieUtil.set()` 相同。

这些方法可以如下方式使用：

![image](img/logo1.gif)

```javascript
//假设 document.cookie=data=name=Nicholas&book=Professional%20JavaScript
//设置两个子 cookie
SubCookieUtil.set("data", "name", "Nicholas");
SubCookieUtil.set("data", "book", "Professional JavaScript");

//带有过期日期设置所有子 cookie
SubCookieUtil.setAll("data", { name: "Nicholas", book: "Professional JavaScript" },
    new Date("January 1, 2010"));

//更改 name 值并更改 cookie 的过期日期
SubCookieUtil.set("data", "name", "Michael", new Date("February 1, 2010"));
```

### SubCookiesExample01.htm

最后一组子 cookie 方法与删除子 cookie 相关。普通 cookie 通过将过期日期设置为过去的某个时间来删除，但子 cookie 并不能那么容易删除。为了删除一个子 cookie，你需要检索 cookie 中包含的所有子 cookie，仅删除要移除的那一个，然后用剩余的子 cookie 值将 cookie 设置回去。考虑以下内容：

```javascript
var SubCookieUtil = {
    //更多代码在此
    unset: function (name, subName, path, domain, secure){
        var subcookies = this.getAll(name);
        if (subcookies){
            delete subcookies[subName];
            this.setAll(name, subcookies, null, path, domain, secure);
        }
    },
    unsetAll: function(name, path, domain, secure){
        this.setAll(name, null, new Date(0), path, domain, secure);
    }
};
```



### CookieUtil.js

这里定义的两个方法有不同的用途。`unset()` 方法用于从 cookie 中删除单个子 cookie 并保留其他部分；而 `unsetAll()` 方法相当于`CookieUtil.unset()`，它会移除整个 cookie。与`set()`和`setAll()`一样，`path`、`domain`和`secure`标志必须与创建 cookie 的选项匹配。这些方法可以如下使用：

```javascript
//仅删除 "name" 子 cookie
SubCookieUtil.unset("data", "name");

//移除整个 cookie
SubCookieUtil.unsetAll("data");
```

如果你担心达到每个域名的 cookie 限制，子 cookie 是一个吸引人的替代方案。

还有一种类型的 cookie 称为 HttpOnly。HttpOnly cookie 可以从浏览器或服务器设置，但只能从服务器读取，因为 JavaScript 无法获取 HttpOnly cookie 的值。

由于所有 cookie 都通过请求头从浏览器发送，在 cookie 中存储大量信息会影响浏览性能。cookie 信息越大，完成请求所需的时间越长。

强烈建议避免在 cookie 中存储重要或敏感数据。Cookie 数据未存储在安全环境中，因此其中包含任何数据可能被他人访问。你应该避免在 cookie 中存储信用卡号或个人地址等数据。

在 Internet Explorer 5 中，微软通过自定义行为引入了持久化用户数据的概念。用户数据允许每个文档存储高达 128KB 数据，每个域名存储高达 1MB 数据。要使用持久化用户数据，你首先必须如此处 CSS 所示在元素上指定 userData 行为：

```html
<div style="behavior:url(#default#userData)" id="dataStore"></div>
```

一旦元素使用了 userData 行为，你就可以使用`setAttribute()`方法向其保存数据。为了将数据提交到浏览器缓存，你必须调用`save()`并传入要保存的数据存储的名称。数据存储名称是完全任意的，用于区分不同的数据集。考虑以下示例：

```javascript
var dataStore = document.getElementById("dataStore");
dataStore.setAttribute("name", "Nicholas");
dataStore.setAttribute("book", "Professional JavaScript");
dataStore.save("BookInfo");
```

`UserDataExample01.htm`

在此代码中，有两条信息被存储在`<div>`元素上。在使用`setAttribute()`存储数据后，调用了数据存储名称为`"BookInfo"`的`save()`方法。当下次加载页面时，你可以使用数据存储名称调用`load()`方法来检索数据，如下：

```javascript
dataStore.load("BookInfo");
alert(dataStore.getAttribute("name"));    //"Nicholas"
alert(dataStore.getAttribute("book"));    //"Professional JavaScript"
```

`UserDataExample01.htm`

`load()`的调用会从`"BookInfo"`数据存储中检索所有信息并使其元素上可用；在显式加载之前，这些信息是不可用的。如果为`getAttribute()`调用一个不存在或未加载的名称，则将返回`null`。

你可以通过`removeAttribute()`方法并传递属性名来显式地从元素中移除数据。移除后，必须再次调用`save()`来提交更改，如下所示：

```javascript
dataStore.removeAttribute("name");
dataStore.removeAttribute("book");
dataStore.save("BookInfo");
```

`UserDataExample01.htm`

此代码删除了两个数据属性，然后将这些更改保存到缓存中。

Internet Explorer 用户数据的访问性限制与 cookies 类似。为了访问数据存储，运行脚本的页面必须来自同一域、同一目录路径，并使用与保存数据到存储器的脚本相同的协议。与 cookies 不同的是，你无法将用户数据的访问性限制扩大到更广泛的范围。此外，与 cookies 不同，用户数据默认跨会话持久且不会过期；需要使用`removeAttribute()`显式移除数据以释放空间。

![image](img/pen.gif)

与 cookies 一样，Internet Explorer 用户数据是不安全的，不应用于存储敏感信息。

# Web Storage

Web Storage 最初在 Web 超超文本应用程序技术工作组 (WHAT-WG) 的 Web Applications 1.0 规范中描述。该规范的初始工作最终成为了 HTML5 的一部分，然后被拆分为自己的规范。它的意图是解决当数据严格在客户端需要、而不需要持续向服务器发送数据时，由 cookies 带来的某些局限性。Web Storage 的两个主要目标是：

* 为在 cookies 之外提供一种存储会话数据的方法。
* 提供一种存储跨会话持久的大量数据的机制。

原始的 Web Storage 规范包含了两个对象的定义：`localStorage`和`globalStorage`。这些对象作为`window`的属性存在于 Internet Explorer 8+、Firefox 3.5+、Safari 3.1+、Chrome 4+ 以及 Opera 10.5+ 中。

![image](img/pen.gif)

Firefox 2 和 3 对 Web Storage 有部分实现，这些实现基于早期的工作，当时实现的是一个名为`globalStorage`的对象 own `localStorage`。

# 存储类型 (Storage Type)

Storage 类型用于存储最大 own（由浏览器决定）的键值对。`Storage`实例像任何其他对象一样，并具有以下额外方法：

* `clear()` — 移除所有值；在 Firefox 中未实现。
* `getItem(name)` — 获取给定名称的值。
* `key(index)` — 获取给定数字位置的名称。
* `removeItem(name)` — 移除由名称标识的键值对。
* `setItem(name, value)` — 设置给定名称的值。

`getItem()`、`removeItem()`和`setItem()`方法可以直接或间接地地通过操作`Storage`对象来调用。由于每个项目都作为属性存储在对象上，你可以简单地通过点符号语法或中括号语法访问属性来读取值，通过相同的操作设置值，或使用`delete`操作符将其移除。尽管如此，通常建议使用这些方法而不是属性访问，以确保你不会用一个键覆盖掉已存在的对象成员。

你可以通过使用`length`属性来确定`Storage`对象中有多少个键值对。无法确定对象中所有数据的大小，尽管 Internet Explorer 8 提供了一个`remainingSpace`属性，用于获取仍可存储的空间量（以字节为单位）。

![image](img/pen.gif)

Storage 类型仅能存储字符串。非字符串数据在存储之前会被转换为字符串。

# sessionStorage 对象

`sessionStorage`对象仅为当前会话存储数据，这意味着数据一直存储到浏览器关闭。这等同于在浏览器关闭时消失的会话 cookie。存储在`sessionStorage`上的数据在页面刷新时持久存在，取决于浏览器供应商，浏览器崩溃并重启后可能可用。（Firefox 和 WebKit 支持此，但 Internet Explorer 不支持。）

由于`sessionStorage`对象与服务器会话绑定，因此在本地运行文件运行时不可用的。存储在`sessionStorage`上的数据仅从最初将数据放置于对象的页面访问，这使其对于多页应用程序的作用有限。

由于`sessionStorage`对象是`Storage`的实例，你可以通过`setItem()`或直接分配新属性来向其分配数据。以下是每种方法的示例：

![image](img/pen.gif)

```javascript
// 使用方法存储数据
sessionStorage.setItem("name", "Nicholas");

// 使用属性存储数据
sessionStorage.book = "Professional JavaScript";
```

`UserDataExample01.htm`

写入存储在不同浏览器之间存在差异。Firefox 和 WebKit 同步实现存储，因此添加到存储的数据立即提交。Internet Explorer 的实现是异步的，因此数据赋值与写入磁盘之间可能存在延迟。对于少量数据，这种差异可以忽略不计。对于大量数据，你会发现 Internet Explorer 中的 JavaScript 恢复速度更快，因为它将实际写入过程卸载了。

你可以在分配任何新数据之前使用`begin()`方法并在所有赋值完成后使用`commit()`方法，在 Internet Explorer 中强制执行写入。考虑以下示例：

```javascript
// 仅限 IE8
sessionStorage.begin();
sessionStorage.name = "Nicholas";
sessionStorage.book = "Professional JavaScript";
sessionStorage.commit();
```

此代码确保一旦调用`commit()`，`"name"`和`"book"`的值就会写入。调用`begin()`确保在代码执行期间不会发生磁盘写入。对于少量数据，这种过程并不是必要的；但对于文档等大量数据，你可能希望考虑这种事务方法。

数据可以使用`getItem()`或直接访问属性名称来获取。以下是每种方法的示例：

```javascript
// 使用方法获取数据
var name = sessionStorage.getItem("name");

// 使用属性获取数据
var book = sessionStorage.book;
```

`UserDataExample01.htm`

你可以结合`length`属性和`key()`方法来遍历`sessionStorage`中的值，如下所示：

```javascript
for (var i=0, len = sessionStorage.length; i < len; i++){
    var key = sessionStorage.key(i);
    var value = sessionStorage.getItem(key);
    alert(key + "=" + value);
}
```

`sessionStorage`中的键值对可以通过以下顺序访问：首先通过`key()`获取指定位置的数据名称，然后使用该名称通过`getItem()`获取值。

也可以使用`for-in`循环来遍历`sessionStorage`中的值：

```javascript
for (var key in sessionStorage){
    var value = sessionStorage.getItem(key);
    alert(key + "=" + value);
}
```

每次循环时，`key`都会被填充`sessionStorage`中的另一个名称；不会返回任何内置方法或`length`属性。

要从`sessionStorage`中删除数据，可以使用针对对象属性的`delete`标识符，也可以使用`removeItem()`方法。以下是这两种方法的示例：

```javascript
//use delete 移除一个值 - 在 WebKit 中不起作用
delete sessionStorage.name;

//使用方法移除一个值
sessionStorage.removeItem("book");
```

SessionStorageExample01.htm

值得注意的是，截至本文编写时，`delete`运算符不会移除 WebKit 中的数据，而`removeItem()`在所有支持的浏览器中都能正常工作。

`sessionStorage`对象应主要用于存储仅在会话中有效的小段数据。如果你需要跨会话持久化数据，那么`globalStorage`或`localStorage`更为合适。

### globalStorage 对象

`globalStorage`对象在 Firefox 2 中实现。作为原始 Web Storage 规范的一部分，它的目的是跨会话持久化数据，并带有特定的访问限制。为了使用`globalStorage`，你需要指定数据可用的域名。这是通过使用括号表示法访问属性来实现的，如下例：

![image](img/logo1.gif)

```javascript
//save value
globalStorage["wrox.com"].name = "Nicholas";

//get value
var name = globalStorage["wrox.com"].name;
```

GlobalStorageExample01.htm

在这里，访问了域 [wrox.com](http://wrox.com) 的存储区域。虽然`globalStorage`对象本身不是`Storage`的实例，但`globalStorage["wrox.com"]`规范下的对象是实例，并可以相应使用。该存储区域可以从 [wrox.com](http://wrox.com) 以及所有子域名访问。你可以通过如下方式指定子域名来限制它：

```javascript
//save value
globalStorage["www.wrox.com"].name = "Nicholas";

//get value
var name = globalStorage["www.wrox.com"].name;
```

GlobalStorageExample01.htm

此处指定的存储区域仅可从 [www.wrox.com](http://www.wrox.com) 上的页面访问，排除其他子域名。

某些浏览器允许更通用的访问限制，例如仅限于顶级域名（TLDs）或允许全局访问，如下例所示：

```javascript
//store data 存储所有人可访问的数据 - 避免使用！
globalStorage[""].name = "Nicholas";

//store data 仅对 .net 结尾的域名可用 - 避免使用！
globalStorage["net"].name = "Nicholas";
```

尽管这些功能被支持，但建议避免使用通用访问的数据存储，以防止可能的安全问题。由于安全考虑，这种能力在未来可能会被移除或受到严重限制，因此应用程序不应依赖此类功能。在使用`globalStorage`时，请务必指定域名。

对`globalStorage`区域的访问受请求页面的域名、协议和端口的限制。例如，如果在使用 HTTPS 协议时为 [wrox.com](http://wrox.com) 存储数据，通过 HTTP 访问的 [wrox.com](http://wrox.com) 页面无法访问该信息。同样，通过端口 80 访问的页面无法与相同域名、相同协议但在端口 8080 访问的页面共享数据。这类似于 Ajax 请求的同源策略。

`globalStorage`的每个属性都是`Storage`的实例。因此，可以像示例所示使用：

![image](img/logo1.gif)

```javascript
globalStorage["www.wrox.com"].name = "Nicholas";
globalStorage["www.wrox.com"].book = "Professional JavaScript";
globalStorage["www.wrox.com"].removeItem("name");
var book = globalStorage["www.wrox.com"].getItem("book");
```

GlobalStorageExample01.htm

如果你事先不确定要使用的域名，使用`location.host`作为属性名可能更安全。例如：

```javascript
globalStorage[location.host].name = "Nicholas";
var book = globalStorage[location.host].getItem("book");
```

GlobalStorageExample01.htm

存储在`globalStorage`属性中的数据留在磁盘上，直到通过`removeItem()`或`delete`移除，或者用户清除浏览器缓存。这使得`globalStorage`成为存储客户端文档或持久化用户设置的理想选择。

### localStorage 对象

在修订后的 HTML5 规范中，`localStorage`对象取代了`globalStorage`作为存储持久客户端数据的方法。与`globalStorage`不同，你无法在`localStorage`上指定任何访问规则；规则已经设定。为了访问同一个`localStorage`对象，页面必须来自相同的域名（子域名无效）、使用相同的协议并在相同的端口。这实际上等同于`globalStorage`。

由于`localStorage`是`Storage`的实例，可以像下面所示使用。这里是一些示例：

```javascript
//使用方法存储数据
```



`localStorage.setItem("name", "Nicholas");`

```javascript
//使用属性存储数据
localStorage.book = "Professional JavaScript";

//使用方法获取数据
var name = localStorage.getItem("name");

//使用属性获取数据
var book = localStorage.book;
```

`LocalStorageExample01.htm`

存储在`localStorage`中的数据遵循与`globalStorage`相同的规则，直到它被特定移除或用户清除浏览器缓存。

为了均衡仅支持`globalStorage`的浏览器，可以使用以下函数：

![image](img/logo1.gif)

```javascript
function getLocalStorage(){
    if (typeof localStorage == "object"){
        return localStorage;
    } else if (typeof globalStorage == "object"){
        return globalStorage[location.host];
    } else {
        throw new Error("Local storage not available.");
    }
}
```

`GlobalLocalStorageExample01.htm`

然后，对函数的初始调用即可识别数据的正确位置：

```javascript
var storage = getLocalStorage();
```

`GlobalLocalStorageExample01.htm`

确定使用哪种`Storage`对象后，可以在所有支持 Web Storage 的浏览器中轻松地存储和检索数据。

### storage 事件

当`Storage`对象发生变化时，会在文档上触发存储事件。这发生在每次使用属性或`setItem()`设置值时、每次使用`delete`或`removeItem()`移除值时以及每次调用`clear()`时。事件对象具有以下四个属性：

* `domain` — 存储发生更改的域名。
* `key` — 被设置或移除的键。
* `newValue` — 键被设置的值，如果键被移除则为 null。
* `oldValue` — 键更改之前的值。

在这些四个属性中，Internet Explorer 8 和 Firefox 仅实现了`domain`属性。截至本文编写日期，WebKit 不支持存储事件。

你可以使用以下代码监听存储事件：

```javascript
EventUtil.addHandler(document, "storage", function(event){
    alert("Storage changed for " + event.domain);
});
```

`StorageEventExample01.htm`

存储事件会在`sessionStorage`和`localStorage`的所有更改时均触发，但不会区分它们。

与其他客户端端数据存储解决方案一样，Web Storage 也有局限性。这些局限性是特定浏览器的。通常情况下，客户端数据的大小限制是基于每个源（协议、域名和端口）设置的，因此每个源都有固定大小的空间来存储其数据。通过分析存储数据的页面源来强制执行这一限制。

大多数桌面浏览器对`localStorage`有每个源 5MB 的限制。Chrome 和 Safari 的每个源限制为 2.5MB。iOS 版 Safari 和 Android 版的 WebKit 同样有 2.5MB 的限制。

`sessionStorage`的限制在不同浏览器之间有所不同。许多浏览器对`sessionStorage`数据没有限制，而 Chrome、Safari、iOS 版 Safari 以及 Android 版的 WebKit 限制为 2.5MB。Internet Explorer 8+ 和 Opera 的`sessionStorage`限制为 5MB。

有关关于 Web Storage 限制的更多信息，请参阅 Web Storage 支持性测试：[`dev-test.nemikor.com/web-storage/support-test/`](http://dev-test.nemikor.com/web-storage/support-test/)。

## IndexedDB

Indexed Database API，简称为`IndexedDB`，是浏览器中的一种结构化数据存储。IndexedDB 的出现是现在已废弃的 Web SQL Database API 的替代方案（由于其已废弃，本书未涵盖该内容）。IndexedDB 的背后的理念是创建一个 API，能够方便地存储和检索 JavaScript 对象，同时允许进行查询和搜索。

IndexedDB 设计为几乎完全异步的。因此，大多数操作都是以请求的形式执行，这些请求将稍后执行并产生成功的结果或错误。几乎每个 IndexedDB 操作都需要你挂载`onerror`和`onsuccess`事件处理器来确定结果。

一旦获得完全支持，将有一个全局的`indexedDB`对象作为 API 宿主。由于 API 仍在变动中，浏览器正在使用厂商前缀，因此 Internet Explorer 10 中的该对象被称为`msIndexedDB`，在 Firefox 4 中被称为`mozIndexedDB`，在 Chrome 中被称为`webkitIndexedDB`。为了清晰起见，本节示例使用了`indexedDB`，因此你可能需要在每个示例之前包含以下代码：

```javascript
var indexedDB = window.indexedDB || window.msIndexedDB || window.mozIndexedDB || window.webkitIndexedDB;
```

`IndexedDBExample01.htm`

### 数据库 (Databases)

IndexedDB 是一个类似于你可能用过的数据库（如 MySQL 或 Web SQL Database）。巨大的区别在于，IndexedDB 使用对象存储（object stores）而不是表来跟踪数据。IndexedDB 数据库简单来说分组在共同名称下的对象存储集合。

使用数据库的第一步是使用`indexedDB.open()`打开它，并传递要打开的数据库名称。如果已存在名为名的数据库，则会发出请求打开它；如果数据库不存在，则会发出请求创建并打开它。对`indexDB.open()`的调用返回一个`IDBRequest`，你可以在上面挂载`onerror`和`onsuccess`事件处理器。这是一个示例：

![image](img/logo1.gif)

```javascript
var request, database;

request = indexedDB.open("admin");

request.onerror = function(event){
    alert("尝试打开时发生了错误：" + 
          event.target.errorCode);
};

request.onsuccess = function(event){
    database = event.target.result;
};
```

`IndexedDBExample01.htm`

在两个事件处理器中，`event.target`都指向`request`，因此它们可以互换。如果调用了`onsuccess`事件处理器，则数据库实例对象 (`IDBDatabase`) 可通过`event.target.result`获取并存储在变量`database`中。从现在开始，所有对数据库的操作都通过`database`对象本身进行。如果发生错误，存储在`event.target.errorCode`中的错误代码将指示问题的性质，如下所示（这些错误代码适用于所有操作）：

* `IDBDatabaseException.UNKNOWN_ERR (1)` — 错误是意外的，不属于任何可用类别。
* `IDBDatabaseException.NON_TRANSIENT_ERR (2)` — 不允许该操作。
* `IDBDatabaseException.NOT_FOUND_ERR (3)` — 未找到执行操作的数据库。
* `IDBDatabaseException.CONSTRAINT_ERR (4)` — 违反了数据库约束。
* `IDBDatabaseException.DATA_ERR (5)` — 为事务提供的数据不满足要求。
* `IDBDatabaseException.NOT_ALLOWED_ERR (6)` — 不允许该操作。
* `IDBDatabaseException.TRANSACTION_INACTIVE_ERR (7)` — 尝试重用已完成的事务。
* `IDBDatabaseException.ABORT_ERR (8)` — 请求已取消且未成功。
* `IDBDatabaseException.READ_ONLY_ERR (9)` — 在只读模式下尝试写入或以此方式更改数据。
* `IDBDatabaseException.TIMEOUT_ERR (10)` — 操作未在可用时间内完成。
* `IDBDatabaseException.QUOTA_ERR (11)` — 剩余磁盘空间不足。

默认情况下，数据库没有关联的版本号，因此在开始时设置初始版本是一个好主意。要这样做，请调用`setVersion()`方法并传入字符串格式的版本。再次，这会创建一个请求对象，你需要在其上分配事件处理器：

![image](img/logo1.gif)

```javascript
if (database.version != "1.0"){
    request = database.setVersion("1.0");
    request.onerror = function(event){
        alert("尝试设置版本时发生了错误：" + 
              event.target.errorCode);
    };
    request.onsuccess = function(event){
        alert("初始化完成。数据库名称：" + database.name);
    };
} else {
    alert("数据库已初始化。" + database.version);
}
```

`IndexedDBExample01.htm`

### 对象存储 (Object Stores)

一旦建立了与数据库的连接，下一步是与对象存储进行交互。如果数据库版本与你预期的不符，你可能需要创建一个对象存储。然而，在创建对象存储之前，考虑你想存储的数据类型很重要。

假设你想存储包含用户名、密码等的用户记录。持有单个记录的对象可能如下：

```javascript
var user = {
    username: "007",
    firstName: "James",
    lastName: "Bond",
    password: "foo"
};
```

观察这个对象，你可以很容易看到该对象存储的合适键是`username`属性。用户名必须是全局唯一的，而且这可能是你大多数时候访问数据的方式。这很重要，因为在创建对象存储时必须指定键。以下是为这些用户创建对象存储的方法：

```javascript
var store = db.createObjectStore("users", { keyPath: "username" });
```

`IndexedDBExample02.htm`

`keyPath`属性的第二个参数指示明了应用作键的存储对象的属性名称。

由于你现在已经有了对象存储（object store）的引用，可以使用`add()`或`put()`向其填充数据。这两种方法都接受一个参数，即要存储的对象，并将该对象保存到对象存储中。这两个方法之间的区别仅出现在对象存储中已经存在具有相同键的对象时。在这种情况下，`add()`会导致错误，而`put()`则直接覆盖该对象。简单来说，可以将`add()`用于用于插入新值，而将`put()`用于更新值。因此，首次初始化对象存储时，你可能想要执行类似如下的操作：

![image](img/logo1.gif)

```javascript
//where users 是一个新用户数组
var i=0,
    len = users.length;
while(i < len){
    store.add(users[i++]);
}
```

`IndexedDBExample02.htm`

每次调用`add()`或`put()`都会为对象存储创建一个新的更新请求。如果你想验证请求是否成功完成，可以将请求对象存储在变量中，并分配`onerror`和`onsuccess`事件处理器：

```javascript
//这里 users 是一个新用户数组
var i=0,
    request,
    requests = [],
    len = users.length;
while(i < len){
    request = store.add(users[i++]);
    request.onerror = function(){
        //处理错误
    };
    request.onsuccess = function(){
        //处理成功
    };
    requests.push(request);
}
```

一旦创建了对象存储并填充了数据，就可以开始查询了。

## 事务 (Transactions)

创建对象存储之后，所有的后续操作都通过事务完成。事务使用数据库对象上的`transaction()`方法创建。每你想读取或更改数据时，都会使用事务将所有更改组合在一起。在最简单的形式中，你如下创建一个新事务：

```javascript
var transaction = db.transaction();
```

在不指定参数的情况下，你对数据库中的所有对象存储具有只读访问权限。为了优化，你可以指定一个或多个想要访问的对象存储名称：

```javascript
var transaction = db.transaction("users");
```

这确保了在事务期间，只有用户对象存储的信息被加载并可用。如果你想访问多个对象存储，第一个参数也可以是字符串数组：

```javascript
var transaction = db.transaction(["users", "anotherStore"]);
```

如之前所述，这些事务中的每一个都以只读方式访问数据。要更改这一点，你必须传递第二个参数来指示访问模式。这些常量可以在`IDBTransaction`上访问：`READ_ONLY` (0)、`READ_WRITE` (1) 和`VERSION_CHANGE` (2)。虽然 Internet Explorer 10+ 和 Firefox 4+ 实现了`IDBTransaction`，但 Chrome 通过`webkitIDBTransaction`支持它，因此需要以下代码来规范化接口：

![image](img/logo1.gif)

```javascript
var IDBTransaction = window.IDBTransaction || window.webkitIDBTransaction;
```

`IndexedDBExample03.htm`

有了这种设置，你可以为`transaction()`指定第二个参数：

```javascript
var transaction = db.transaction("users", IDBTransaction.READ_WRITE);
```

`IndexedDBExample03.htm`

此此事务能够对用户对象存储同时进行读取和写入。

一旦你有了事务的引用，可以使用`objectStore()`方法并传入你想要操作的存储名称来访问特定的对象存储。然后你可以像以前一样使用`add()`和`put()`，以及使用`get()`获取值、使用`delete()`对象以及使用`clear()`所有对象。`get()`和`delete()`方法各接受一个对象键作为其参数，并且这五个方法每一个都会创建一个新的请求对象。例如：

![image](img/logo1.gif)

```javascript
var request = db.transaction("users").objectStore("users").get("007");

request.onerror = function(event){
    alert("未获取到对象!");
};

request.onsuccess = function(event){
    var result = event.target.result;
    alert(result.firstName);    //"James"
};
```

`IndexedDBExample02.htm`

由于任意数量的请求都可以作为单个事务的一部分完成，事务对象本身也拥有事件处理器：`onerror`和`oncomplete`。这些被用于提供事务级状态信息：

```javascript
transaction.onerror = function(event){
    //整个事务被取消
};

transaction.oncomplete = function(event){
    //整个事务成功完成
};
```



请记住，`oncomplete` 的事件对象并让你访问 `get()` 请求返回的任何数据，因此你仍然需要为这些类型的请求一个 `onsuccess` 事件处理器。

## 使用游标查询 (Querying with Cursors)

事务可以直接检索已知键的单个项目。当你想要检索多个项目时，需要在事务内部创建一个游标。游标是结果结果集的指针。与传统的数据库查询不同，游标不会预先收集整个结果集。相反，游标指向第一个结果，在接到指令之前它不会尝试寻找下一个。

游标是通过对象存储上的 `openCursor()` 方法创建的。与 IndexedDB 的其他操作一样，`openCursor()` 的返回值是一个请求，因此你必须分配 `onsuccess` 和 `onerror` 事件处理器。例如：

```javascript
var store = db.transaction("users").objectStore("users"),
    request = store.openCursor();

request.onsuccess = function(event){
    //处理成功
};

request.onfailure = function(event){
    //处理失败
};
```

IndexedDBExample04.htm

当 `onsuccess` 事件被调用时，如果存在下一个项目，则 `event.target.result` 持有一个 `IDBCursor`，如果没有项目则为 `null`。`IDBCursor` 实例具有多个属性：

- `direction`: 指示游标移动方向的数值。默认是 `IDBCursor.NEXT` (0) 表示下一个。其他值包括 `IDBCursor.NEXT_NO_DUPLICATE` (1) 表示不重复的下一个、`IDBCursor.PREV` (2) 表示上一个以及 `IDBCursor.PREV_NO_DUPLICATE` (3) 表示不重复的上一个。
- `key`: 键。
- `value`: 实际对象。
- `primaryKey`: 游标使用的键。可以是对象键或索引键（稍后讨论）。

可以使用代码获取单个结果的信息：

```javascript
request.onsuccess = function(event){
    var cursor = event.target.result;
    if (cursor){//始终检查
        console.log("Key: " + cursor.key + ", Value: " + 
                    JSON.stringify(cursor.value));
    }
};
```

请记住，此示例中的 `cursor.value` 是一个对象，这就是为什么在显示之前对其进行了 JSON 编码。

游标可用于更新单个记录。`update()` 方法用指定的对象更新当前游标值。与其他此类操作一样，调用 `update()` 会创建一个新的请求，如果你想知道结果，就需要分配 `onsuccess` 和 `onerror`：

```javascript
request.onsuccess = function(event){
    var cursor = event.target.result,
        value,
        updateRequest;

    if (cursor){   //始终检查
        if (cursor.key == "foo"){
            value = cursor.value;                   //获取当前值
            value.password = "magic!";              //更新密码
            updateRequest = cursor.update(value);   //请求保存
            updateRequest.onsuccess = function(){
                //处理成功;
            };
            updateRequest.onfailure = function(){
                //处理失败
            };
        }
    }
};
```

你还可以通过调用 `delete()` 删除该位置的项目。与 `update()` 一样，这也会创建一个请求：

```javascript
request.onsuccess = function(event){
    var cursor = event.target.result,
        value,
        deleteRequest;

    if (cursor){   //始终检查
        if (cursor.key == "foo"){
            deleteRequest = cursor.delete();       //请求删除该值
            deleteRequest.onsuccess = function(){
                //处理成功;
            };
            deleteRequest.onfailure = function(){
                //处理失败
            };
        }
    }
};
```

如果事务没有修改对象存储库的权限，`update()` 和 `delete()` 都会抛出错误。

默认情况下，每个游标只发送一次请求。若要发送另一个请求，你必须调用以下方法之一：

* `continue(key)` — 移动到结果集中的下一个项目。参数 `key` 是可选的。如果不指定，游标将仅移动到下一个项目；如果提供，游标将移动到指定的 `key`。
* `advance(count)` — 游标向前移动 `count` 个项目。

这些方法中的每一个都会导致游标复用同一个请求，因此 `onsuccess` 和 `onfailure` 事件处理器会被一直复用，直到不再需要为止。例如，以下代码遍历了对象存储中的所有项目：

```javascript
request.onsuccess = function(event){
    var cursor = event.target.result;
    if (cursor){  //始终检查
        console.log("Key: " + cursor.key + ", Value: " + 
                    JSON.stringify(cursor.value));
        cursor.continue();   //前往下一个
    } else {
        console.log("Done!");
    }
};
```

调用 `continue()` 会触发另一个请求，并再次调用 `onsuccess`。当没有更多项目可以遍历的项时，`onsuccess` 会最后被调用一次，此时 `event.target.result` 等于 `null`。

## 键范围 (Key Ranges)

使用游标似乎不是最优的，因为你检索数据的方式受到了限制。键范围（Key ranges）被用于让游标的操作变得更易管理。一个键范围由 `IDBKeyRange` 实例表示。标准版本是 `IDBKeyRange`，它在 Internet Explorer 10+ 和 Firefox 4+ 中支持，而 Chrome 通过 `webkitIDBKeyRange` 支持这种类型。与 IndexedDB 相关的其他类型一样，你首先需要创建一个本地副本，考虑到这些差异：

```javascript
var IDBKeyRange = window.IDBKeyRange || window.webkitIDBKeyRange;
```

指定键范围有四种不同的方法。第一种是使用 `only()` 方法并传入你想检索的键：

```javascript
var onlyRange  = IDBKeyRange.only("007");
```

此范围确保了只有键为 "007" 的值会被检索。使用此范围创建的游标与直接访问对象存储并调用 `get("007")` 类似。

第二种类型的范围为结果集定义了一个下界。下界指示了游标应该从哪个项目开始。例如，以下键范围确保游标从键 "007" 开始并一直持续到末尾：

```javascript
//从项目 "007" 开始，到末尾
var lowerRange  = IDBKeyRange.lowerBound("007");
```

如果你想从紧随 "007" 之后的值开始，则可以传入第二个参数 `true`：

```javascript
//从 "007" 之后的项目开始，到末尾
var lowerRange  = IDBKeyRange.lowerBound("007", true);
```

第三种类型的范围是上界，通过使用 `upperBound()` 方法指示你不想越过的键。以下键范围确保游标从开始开始，并在到达键为 "ace" 的值时停止：

```javascript
//从开始开始，到 "ace"
var upperRange  = IDBKeyRange.upperBound("ace");
```

如果你不想包含给定的键，则在第二个参数中传入 `true`：

```javascript
//从开始开始，到 "ace" 之前的项目
var upperRange  = IDBKeyRange.upperBound("ace", true);
```

若要同时指定下界和上界，请使用 `bound()` 方法。该方法接受四个参数：下界键、上界键、一个指示跳过下界的可选布尔值，以及一个指示跳过上界的可选布尔值。以下是一些示例：

```javascript
//从 "007" 开始，到 "ace"
var boundRange  = IDBKeyRange.bound("007", "ace");

//从 "007" 之后的项目开始，到 "ace"
var boundRange  = IDBKeyRange.bound("007", "ace", true);

//从 "007" 之后的项目开始，到 "ace" 之前的项目
var boundRange  = IDBKeyRange.bound("007", "ace", true, true);

//从 "007" 开始，到 "ace" 之前的项目
var boundRange  = IDBKeyRange.bound("007", "ace", false, true);
```

一旦定义了范围，将其传入 `openCursor()` 方法，你就会创建一个处于约束范围内的游标：

```javascript
var store = db.transaction("users").objectStore("users"),
    range = IDBKeyRange.bound("007", "ace");
request = store.openCursor(range);

request.onsuccess = function(event){
    var cursor = event.target.result;
    if (cursor){  //始终检查
        console.log("Key: " + cursor.key + ", Value: " + 
                    JSON.stringify(cursor.value));
        cursor.continue();   //前往下一个
    } else {
        console.log("Done!");
    }
};
```

此示例输出了 "007" 到 "ace" 之间的值，这比之前的示例要少。

## 设置游标方向 (Setting Cursor Direction)

`openCursor()` 实际上有两个参数。第一个参数是 `IDBKeyRange` 实例，第二个是指示方向的数值。这些常量定义在 `IDBCursor` 上，正如查询部分所示。Firefox 4+ 和 Chrome 有不同的实现，因此第一步是本地处理差异：

```javascript
var IDBCursor = window.IDBCursor || window.webkitIDBCursor;
```

通常游标从对象存储中的第一个项目开始，每次调用 `continue()` 或 `advance()` 都向前移动。这些游标默认的方向值为 `IDBCursor.NEXT`。如果对象存储中有重复项，你可能想要一个跳过重复项的游标。你可以通过将 `IDBCursor.NEXT_NO_DUPLICATE` 传入 `openCursor()` 的第二个参数来实现：

```javascript
var store = db.transaction("users").objectStore("users"),
    request = store.openCursor(null, IDBCursor.NEXT_NO_DUPLICATE);
```

注意 `openCursor()` 的第一个参数是 `null`，这表示使用所有值的默认键范围。此游标将从第一个项目开始遍历对象存储中的项目，并跳过任何重复项。

你还可以创建一个反向遍历对象存储的游标，从最后一个项目移动到第一个项目，只需传入 `IDBCursor.PREV` 或 `IDBCursor.PREV_NO_DUPLICATE`（当然，后者是为了避免重复项）。例如：

```javascript
var store = db.transaction("users").objectStore("users"),
    request = store.openCursor(null, IDBCursor.PREV);
```

当使用使用 `IDBCursor.PREV` 或 `IDBCursor.PREV_NO_DUPLICATE` 打开游标时，每次调用 `continue()` 或 `advance()` 都会让游标在对象存储中向后移动，而不是向前移动。

## 索引 (Indexes)

对于某些数据集，你可能希望为对象存储指定多个键。例如，如果你同时通过用户 ID 和用户名来跟踪用户，你可能希望使用这些数据中的任何一个来访问记录。为了实现这一点，可能会将用户 ID 视为主键并对用户名创建索引。

要创建新索引，首先获取对象存储的引用，然后调用 `createIndex()`，如下例所示：

```javascript
var store = db.transaction("users").objectStore("users"),
    index = store.createIndex("username", "username", { unique: true });
```

`createIndex()` 的第一个参数是索引名称，第二个参数是要索引的属性名称，第三个是一个包含 `unique` 键的选项对象。应该始终指定此选项，以指示该键在所有记录中是否是唯一的。由于 `username` 可能重复，因此此索引不是唯一的。

`createIndex()` 的返回值是 `IDBIndex` 实例。你也可以通过对象存储上的 `index()` 方法获取相同的实例。例如，要使用一个已存在的名为 `"username"` 的索引，代码如下：

```javascript
var store = db.transaction("users").objectStore("users"),
    index = store.index("username");
```

索引的作用非常类似于对象存储。你可以使用 `openCursor()` 方法在索引上创建新的游标，这与在对象存储上使用 `openCursor()` 的原理完全相同，不同之处`result.key` 属性填充的是索引键而不是主键。这里是一个示例：

```javascript
var store = db.transaction("users").objectStore("users"),
    index = store.index("username"),
    request = index.openCursor();

request.onsuccess = function(event){
    //处理成功回调
};
```

索引还可以使用 `openKeyCursor()` 方法创建一个特殊的游标，它仅返回每条记录的主键，该方法接受的参数与 `openCursor()` 相同。主要的区别在于 `event.result.key` 是索引键，而 `event.result.value` 是主键而不是整个记录。

```javascript
var store = db.transaction("users").objectStore("users"),
    index = store.index("username"),
    request = index.openKeyCursor();

request.onsuccess = function(event){
    //处理成功回调
    //event.result.key 是索引键，event.result.value 是主键
};
```

你还可以通过使用 `get()` 并传递索引键从索引中检索单个值，这将创建一个新的请求：

```javascript
var store = db.transaction("users").objectStore("users"),
```



`index = store.index("username")`,

`request = index.get("007")`;

`request.onsuccess = function(event){`

    //处理成功回调

`};`

`request.onfailure = function(event){`

    //处理失败回调

`};`

要仅检索给定索引键的主键，请使用`getKey()`方法。这也会创建一个新的请求，但`result.value`等于主键值而不是整个记录：

```javascript
var store = db.transaction("users").objectStore("users"),

    index = store.index("username"),

    request = index.getKey("007");

request.onsuccess = function(event){

    //处理成功回调

    //event.result.key 是索引键，event.result.value 是主键

};
```

在例例的`onsuccess`事件处理器中，`event.result.value`将是用户 ID。

在任何时刻，你都可以通过`IDBIndex`对象上的属性获取有关索引的信息：

*   `name` — 索引的名称。
*   `keyPath` — 传递`createIndex()`的属性路径。
*   `objectStore` — 该索引所作用的对象存储。
*   `unique` — 一个布尔值，指示索引键是否唯一。

对象存储本身还通过`indexNames`属性按名称跟踪索引。这使得可以使用以下代码轻松判断对象上已经存在哪些索引：

```javascript
var store = db.transaction("users").objectStore("users"),

    indexNames = store.indexNames,

    index,

    i = 0,

    len = indexNames.length;

while(i < len){

    index = store.index(indexNames[i++]);

    console.log("Index name: " + index.name + ", KeyPath: " + index.keyPath + 

        ", Unique: " + index.unique);

}
```

此代码遍历每个索引并将其信息输出到控制台。

可以通过调用对象存储上的`deleteIndex()`方法并传递索引名称来删除索引：

```javascript
var store = db.transaction("users").objectStore("users");

store.deleteIndex("username");
```

由于删除索引不会触及对象存储中的数据，因此该操作在没有任何回调的情况下完成。

### 并发问题

虽然 IndexedDB 是页面内部的异步 API，但仍然存在并发问题。如果同一个网页同时在两个浏览器标签页中打开，可能会其中一个标签页在另一个准备好之前尝试升级数据库。产生问题的操作是将数据库设置为新版本，因此`setVersion()`的调用只有当浏览器中只有一个标签页在使用该数据库时才能完成。

当你第一次打开数据库时，分配`onversionchange`事件处理器是关重要的。当同源的另一个标签页调用`setVersion()`时，会执行此回调。对此事件的最佳响应是立即关闭数据库，以便完成版本升级。例如：

```javascript
var request, database;

request = indexedDB.open("admin");

request.onsuccess = function(event){

    database = event.target.result;

    database.onversionchange = function(){

        database.close();

    };

};
```

你应该在每次成功打开数据库后分配`onversionchange`。

当调用`setVersion()`时，还需要为请求分配一个`onblocked`事件处理器。当另一个标签页打开数据库时，会触发此事件。在这种情况下，你可能希望用户关闭所有标签页后再重试。例如：

```javascript
var request = database.setVersion("2.0");

request.onblocked = function(){

    alert("请关闭所有标签页。");

};

request.onsuccess = function(event){

    //处理成功回调

};
```

记住，`onversionchange`也会在其他标签页中调用。通过始终分配这些事件处理器，你将确保 Web 能够处理并发问题。

### 限制与约束

IndexedDB 的许多限制与 Web Storage 完全相同。首先，IndexedDB 数据库绑定到源（协议、域名和端口），因此信息无法跨域共享。这意味着`www.wrox.com`和`p2p.wrox.com`有完全独立的数据存储。

其次，每个源存储的数据量存在限制。Firefox 4+ 的限制是每个源 50MB，而 Chrome 的限制为 5MB。移动版 Firefox 的限制为 5MB，如果超过配额将请求用户存储更多。

Firefox 实施了一个额外的限制，即本地文件无法访问 IndexedDB 数据库。Chrome 没有此限制。在本地运行书中的示例时，请确保使用 Chrome。

## 总结

离线 Web 应用和客户端数据存储是 Web 未来的重要部分。浏览器现在能够检测用户何时离线并触发 JavaScript 事件，以便应用程序做出响应。应用程序缓存允许你指定哪些文件在离线时可用。可以使用 JavaScript API 确定应用程序缓存的状态以及可能发生的变化。

本章还涵盖了客户端存储的以下方面：

*   传统上，这种存储局限于使用 Cookie，Cookie 是可以从客户端或服务器设置并随每次请求传输的小型信息。
*   JavaScript 通过`document.cookie`访问 Cookie。
*   Cookie 的限制使其适用于存储少量数据，但在存储大量数据时效率较低。

Internet Explorer 提供了一种名为用户数据的行为，可以如下所示应用于页面上的元素：

*   应用后，元素可以从命名的数据存储中加载数据，并通过`getAttribute()`、`setAttribute()`和`removeAttribute()`方法访问这些信息。

*   数据必须使用`save()`方法显式保存到命名的数据存储中，才能在会话之间持久化。

Web Storage 定义了两个保存数据的对象：`sessionStorage`和`localStorage`。前者专门用于在浏览器会话内保存数据，因为一旦关闭浏览器，数据就会被移除。后者用于在会话之间持久化数据，并基于跨域安全策略。

IndexedDB 是一种结构化数据存储机制，类似于 SQL 数据库。它不是将存储在表中，而是存储在对象存储（object stores）中。对象存储通过定义键并添加数据来创建。使用游标（Cursors）来查询对象存储中的特定数据，并可以为特定属性创建索引以便快速查找。

有了所有这些选项，可以使用 JavaScript 在客户端机器上存储大量数据。你应该谨慎操作，不要存储敏感信息，因为数据缓存是不加密的。

# 第 24 章：最佳实践

## 本章包含什么？

*   编写可维护的代码
*   确保代码性能
*   将代码部署到生产环境

自 2000 年以来，Web 开发领域已以惊人的速度增长。曾经几乎任何方法都可以接受的虚拟“西部西部”，已经演变成一个拥有研究和既定最佳实践的完整学科。随着简单的网站变成更复杂的 Web 应用，以及 Web 爱好者成为有职人士，Web 开发世界充满了关于最新技术和开发方法的信息。特别是 JavaScript，它是许多研究和推测的受益者。JavaScript 的最佳实践分为几类，并在开发过程的不同阶段进行相应的处理。

## 可维护性

在早期的网站中，JavaScript 主要用于小型效果或表单验证。今天的 Web 应用充斥着数千行的 JavaScript，执行着各种复杂的进程。这种演变要求开发者考虑可维护性。就像更传统学科的软件工程师一样，雇佣 JavaScript 开发者是为了为公司创造价值，他们不仅通过按时交付产品来实现，还通过开发在很久之后仍持续增加价值的知识产权来实现。

编写可维护的代码是非常重要的，因为大多数开发者花费大量时间维护他人的代码。从零开始开发新代码是非常罕见的情况；通常你必须在他人工作的基础上进行构建。确保你的代码具有可维护性可以确保其他开发者能够尽可能地完成工作。

![image](img/pen.gif)

注意，可维护代码的概念并不是 JavaScript 特有的。这些概念中的一些广泛适用于任何编程语言，尽管也存在一些 JavaScript 特有的概念。

### 什么是可维护的代码？

可维护的代码具有几个特征。通常情况下，如果代码满足以下所有条件，则认为它是可维护的：

*   **易于理解** —— 其他人可以拿起代码，并在没有原开发者进行讲解的情况下，弄清楚其目的和通用方法。
*   **直观性** —— 代码中的事情似乎都很合理，无论操作有多复杂。
*   **可适应性** —— 代码的编写方式使得数据的变化不需要完全重写。
*   **可扩展性** —— 代码架构经过了留心，允许未来对核心功能进行扩展。
*   **可调试性** —— 当出现问题时，代码为你提供了足够的信息，以便尽可能直接地识别问题。

能够编写可维护的 JavaScript 代码是专业人士的一项重要技能。这是在周末拼凑出一个网站的爱好者与真正精通技艺的专业开发者之间的区别。

### 代码规范

编写可维护代码的最简单方法之一是为你编写的 JavaScript 制定代码规范。大多数编程语言都开发了代码规范，互联网上快速搜索可能会找到数千份文档。专业机构长期以来一直开发者制定代码规范，试图使代码对所有人来说更具维护性。运行最好的开源项目都有严格的代码规范要求，允许社区中的每个人都能轻松理解代码是如何组织的。

代码规范对 JavaScript 来说很重要，因为该语言具有适应性。与大多数面向对象的语言不同， JavaScript 不会强制开发者将一切都定义为对象。该语言可以支持许多编程风格，从传统的面向对象方法到声明式方法再到函数式方法。快速查看几个开源 JavaScript 库就可以轻松获得创建对象、定义方法和管理环境的多种。

接下来的章节将讨论如何开发代码规范的通用性。这些主题需要被解决，尽管根据你的个人需求，处理方式可能会有所不同。

#### 可读性

为了使代码具有维护性，它首先必须是可读的。可读性与代码作为文本文件的格式化有关。可读性的很大一部分与代码的缩进有关。当大家都使用相同的缩进方案时，整个项目的代码将变得更容易阅读。缩进通常通过使用空格数量而不是制表键来实现，因为不同的文本编辑器对制表键的显示不同。良好的通用缩进大小是四个空格，尽管你可能决定使用更少或更多。

可读性的另一部分是注释。在大多数编程语言中，为每个方法编写注释是一种被接受的做法。由于 JavaScript 可以在代码的任何一点创建函数，这往往被忽视了。正因如此，在 JavaScript 中记录每个函数的文档可能更为重要。总的来说，你的代码中应该进行注释的地方如下：

*   **函数和方法** —— 每个函数或方法都应该包含一条注释，描述其目的以及可能用于完成任务的算法。说明所做的的假设、参数代表什么，以及函数是否返回值（因为这从函数定义中无法看出）也是重要的。
*   **大段代码** —— 所有用于完成单一任务的多行代码之前，应该有一个描述该任务的注释。
*   **复杂算法** —— 如果你使用独特的方法来解决问题，请作为注释解释你是如何做的。这不仅能帮助查看你代码的人，也能帮助你下次查看它。
*   **黑科技（Hacks）** —— 因为浏览器差异，JavaScript 代码通常包含一些黑科技。不要假设查看代码的其他人会理解此类黑科技正在解决的浏览器问题。如果你因为某个浏览器无法使用正常方法而需要采取不同的方式，请将其写在注释中。这减少了某人出现、看到你的黑科技并试图“修复”它从而无意中引入你已经解决过的 bug 的概率。

缩进和注释创建了更具读性的代码，使未来更容易维护。

### 变量和函数命名

代码中变量和函数的正确命名对于使其具有可读性和可维护性至关重要。由于许多 JavaScript 开发者最初是业爱好者，他们往往倾向于使用如 "foo" 和 "bar" 这样无意义的变量名，以及使用如 "doSomething" 这样的函数名。专业的 JavaScript 开发者必须克服这些旧习惯，以创建出可维护的代码。命名的通用规则如下：

*   变量名应当是名词，例如`car`或`person`。
*   函数名应当以动词开头，例如`getName()`。返回布尔值的函数通常以`is`开头，例如`isEnabled()`。
*   对变量和函数都应使用逻辑化的名称，而不必担心长度。长度可以通过后处理和压缩（在本章稍后的部分进行讨论）来缓解。

避免使用无法指示其包含数据类型的无用变量名是至关重要的。通过合理的命名，代码读起来就像是对正在发生的事情的叙述，使其更容易理解。

### 变量类型透明度

由于 JavaScript 中的变量是弱类型的，很容易丢失变量应该包含的数据类型。合理的命名在某种程度上可以缓解这一点，但在所有情况下可能都不够。指示变量数据类型有三种方法。

第一种方法是通过初始化。当定义变量时，它应该被初始化为一个指示其未来如何被使用的值。例如，存储布尔值的变量应该初始化为`true`或`false`，而存储数字的变量应该初始化为一个数字，如下例所示：

```javascript
//通过初始化指示变量类型

var found = false;              //Boolean

var count  = -1;                //number     

var name = "";                  //string

var person = null;              //object
```

初始化为特定的数据类型是变量类型的良好指示。但初始化的缺点是，它无法在函数声明的函数参数中使用。

指示变量类型的第二种方法是使用匈牙利命名（Hungarian notation）。匈牙利命名在变量开头添加一个或多个字符来指示数据类型。这种记法在脚本语言中非常流行，在很长一段时间内，它 JavaScript 的首选格式。JavaScript 最传统的匈牙利命名法为基本数据类型前加单个字符：对象用 "o"，字符串用 "s"，整数用 "i"，浮点数用 "f"，布尔值用 "b"。这里有一个例子：

```javascript
//使用匈牙利命名指示数据类型

var bFound;      //Boolean

var iCount;      //integer

var sName;       //string

var oPerson;     //object
```

JavaScript 匈牙利命法的优势在于它可以同样很好地用于函数参数。匈牙利命名的缺点是它会让代码的可读性稍微降低，中断了不使用它时就能实现的直观、如句子般的代码特性。由于这个原因，匈牙利命名在某些开发者中已开始不受宠。

指示变量类型的最后一种是使用类型注释（type comments）。类型注释放在变量名之后、任何初始化之前。其核心思想是在变量旁放置一个指示数据类型的注释，如下例所示：

```javascript
//使用类型注释指示类型

var found  /*:Boolean*/ = false;

var count  /*:int*/     = 10;

var name   /*:String*/  = "Nicholas";

var person /*:Object*/  = null;
```

类型注释在注入类型信息的同时保持了代码整体的可读性。类型注释的缺点是，你无法使用多行注释注释掉大块代码，因为类型注释本身也是多行注释，会产生干扰，正如此示例所示：

```javascript
//以下代码无法正常工作

/*

var found  /*:Boolean*/ = false;

var count  /*:int*/     = 10;

var name   /*:String*/  = "Nicholas";

var person /*:Object*/  = null;

*/
```



在这里，意图是使用多行注释注释掉所有变量。类型注释干扰了这一点，因为第一个`/*`（第二行）与第一个`*/`（第三行）相匹配，这将导致语法错误。如果你想使用类型注释注释掉代码行，最好在每行上都使用单行注释（许多编辑器会自动为你完成）。

这些是指示变量数据类型的三种常见方法。在决定使用哪一种之前，你需要对每种方法的优缺点进行评估。重要的是决定哪种方法最适合你的项目，并保持一致使用。

## 松耦合

每当应用程序的各个部分相互依赖过于紧密时，代码就会变得过于紧耦合且难以维护。典型问题出现在对象以直接相互引用的方式，导致其中一个的变化总是需要另一个发生改变。紧耦合的软件难以维护，并且不可避免地必须频繁重写。

由于涉及的技术，Web 应用程序有几种方式可能会变得过于紧耦合。意识到这一点并尽可能维护松耦合的代码是非常重要的。

### 解耦 HTML/JavaScript

最常见的耦合类型之一是 HTML/JavaScript 耦合。在 Web 上，HTML 和 JavaScript 分别代表解决方案的不同层级：HTML 是数据，而 JavaScript 是行为。因为它们旨在交互，所以有许多不同的方法将这两种技术结合在一起。不幸的是，某些方法会让 HTML 和 JavaScript 耦合得过于紧密。

内联在 HTML 中的 JavaScript（无论是使用带有内联代码的`<script>`元素还是使用 HTML 属性分配事件处理程序）都是紧耦合的。考虑以下代码示例：

```html
<!--使用 <script> 的紧耦合 HTML/JavaScript -->
<script type="text/javascript">
  document.write("Hello world!");
</script>

<!--使用事件处理属性的紧耦合 HTML/JavaScript -->
<input type="button" value="Click Me" onclick="doSomething()" />
```

尽管这些在技术上都是正确的，但在实践中它们将代表数据的 HTML 与定义行为的 JavaScript 紧密耦合。理想情况下，HTML 和 JavaScript 应该完全分离，通过外部文件引入 JavaScript 并使用 DOM 绑定行为。

当 HTML 和 JavaScript 过于紧耦合时，JavaScript 错误意味着首先要确定错误发生在解决方案的 HTML 部分还是 JavaScript 文件中。它还引入了与代码可用性相关的新类型错误。在示例中，可能在`doSomething()`函数可用之前被点击，导致 JavaScript 错误。这会影响可维护性，因为对按钮行为的任何更改都需要触及 HTML 和 JavaScript，而本该只需要后者。

当情况反过来时，HTML 和 JavaScript 也可能是过度紧耦合的：HTML 被包含在 JavaScript 内部。这通常发生在使用`innerHTML`向页面插入块 HTML 文本时，如下例所示：

```javascript
//HTML 到 JavaScript 的紧耦合
function insertMessage(msg){
    var container = document.getElementById("container");
    container.innerHTML = "<div class=\"msg\"><p class=\"post\">" + msg + "</p>" +
        "<p><em>Latest message above.</em></p></div>";
}
```

通常情况下，你应该避免在`JavaScript`中创建大量的 HTML。这再次与保持分层分离以及能够轻松识别错误根源有关。当使用此示例代码时，页面布局问题可能与格式不当的动态创建 HTML 有关。然而，定位错误可能会困难，因为你通常会查看页面源代码来寻找问题的 HTML，但你会在那里找不到它，因为它是动态生成的。对数据或布局的更改也需要修改`JavaScript`，这表明这两个层之间的耦合过于紧密。

HTML 渲染应该尽可能与`JavaScript`保持分离。当使用`JavaScript`插入数据时，只要可能，它应该在插入时不包含任何标记（markup）。通常，可以在渲染整个页面时包含并隐藏标记，这样之后可以使用`JavaScript`来显示这些标记，而不是由它来生成标记。另一种方法是发送 Ajax 请求来获取要显示的额外 HTML；这种方法允许由同一个渲染层（`PHP`、`JSP`、`Ruby`等）输出标记，而不是将其嵌入`JavaScript`中。

将 HTML 和`JavaScript`解耦可以在调试期间节省时间，因为这使得更容易识别错误根源，同时也增强了可维护性：行为的更改只发生在`JavaScript`文件中，而标记的更改只发生在渲染文件中。

### 解耦 CSS/JavaScript

Web 分层架构的另一层是`CSS`，它主要负责页面的显示。`JavaScript`和`CSS`之间关系密切：它们都是`HTML`之上的层，因此经常一起使用。然而，与`HTML`和`JavaScript`一样，`CSS`和`JavaScript`也可能耦合得太紧。最常见的紧耦合示例是使用`JavaScript`来更改单个样式，如下：

```javascript
//CSS 与 JavaScript 的紧耦合
element.style.color = "red";
element.style.backgroundColor = "blue";
```

由于`CSS`负责页面的显示，任何显示问题都应该通过查看`CSS`文件来解决。然而，当使用`JavaScript`更改颜色等单个样式时，它增加了一个必须检查并可能需要修改的第二个。结果是`JavaScript`在某种程度上负责页面显示，并与`CSS`存在紧密耦合。如果未来需要更改样式，`CSS`和`JavaScript`文件可能都需要修改。这为开发者创造了维护噩梦。层与层之间需要更清晰的隔离。

现代 Web 应用频繁使用`JavaScript`更改样式，因此无法完全解耦`CSS`和`JavaScript`，但可以让耦合变得更松。这是通过动态更改类（classes）而不是单个样式来实现的，如下所示：

```javascript
//CSS 与 JavaScript 的松耦合
element.className = "edit";
```

通过仅更改元素的`CSS`类，你允许大部分样式信息严格保留在`CSS`中。可以使用`JavaScript`来更改类，但它没有直接影响元素的样式。只要应用了正确的类，那么任何显示问题都可以直接追溯到`CSS`而不是`JavaScript`。

第二种紧耦合仅在 Internet Explorer 中有效（但在标准模式下运行的 Internet Explorer 8+ 中无效），在 IE 中，可以通过表达式（expressions）在`CSS`中嵌入`JavaScript`，如下例所示：

```css
/* JavaScript 与 CSS 的紧耦合 */
div {
    width: expression(document.body.offsetWidth - 10 + "px");
}
```

通常会避免使用表达式，因为它们不具备跨浏览器兼容性。它们还应该被避免，因为它们引入了`JavaScript`和`CSS`之间的紧耦合。当你使用表达式时，可能会在`CSS`中发生`JavaScript`错误。尝试由于`CSS`表达式追踪`JavaScript`错误的开发者可以告诉你，他们在甚至考虑查看`CSS`寻找错误根源之前花费了多久。

再次，保持良好的分层分离至关重要。显示问题的唯一源头应该是`CSS`，而行为问题的唯一源头应该是`JavaScript`。保持这些层之间的松散耦合会让你的整个应用程序更具可维护性。

### 解耦应用逻辑/事件处理器

每个 Web 应用通常充斥着许多监听众多不同事件的事件处理器。然而，很少有处理器刻意将应用程序逻辑与事件处理器隔离开。考虑以下示例：

```javascript
function handleKeyPress(event){
    event = EventUtil.getEvent(event);
    if (event.keyCode == 13){
        var target = EventUtil.getTarget(event);
        var value = 5 * parseInt(target.value);
        if (value > 10){
            document.getElementById("error-msg").style.display = "block";
        }
    }
}
```

这个事件处理器在处理事件的同时，还包含了应用程序逻辑。这种方法的问题有两点：首先，除了通过事件之外，没有方法可以触发应用程序逻辑，这使得调试变得困难。如果预期的结果没有发生呢？这意味着事件处理器没有被调用，还是应用程序逻辑失败了？其次，如果随后的事件导致了相同的应用程序逻辑发生，你需要重复该功能，或者将其提取到单独的函数中。无论哪种方式，所需的更改都比实际需要的更多。

更好的方法是将应用程序逻辑与事件处理器分离，使每个者只处理它们应该负责的内容。事件处理器应该从事件对象中获取相关信息，然后由专门的方法来处理。例如，之前的代码可以重写为：

```javascript
function validateValue(value){
    value = 5 * parseInt(value);
    if (value > 10){
        document.getElementById("error-msg").style.display = "block";
    }
}

function handleKeyPress(event){
    event = EventUtil.getEvent(event);
    if (event.keyCode == 13){
        var target = EventUtil.getTarget(event);
        validateValue(target.value);
    }
}
```

更新后的代码正确地将应用程序逻辑与事件处理器分离。`handleKeyPress()`函数检查是否按了回车键（`event.keyCode`为 13），然后获取事件目标并将值传递给包含应用程序逻辑的`validateValue()`函数。注意，`validateValue()`中没有依赖于任何事件处理器逻辑；它只接收一个值并根据该值执行所有其他操作。

将应用程序逻辑与事件处理器分离有许多好处。首先，它允许你以最小的工作量更改触发某些过程的事件。如果最初是用鼠标点击触发处理，但现在应该是按键触发，这种更改非常简单。其次，你可以在不附加事件的情况下测试代码，这使得创建单元测试或自动化应用程序流变得更容易。

在应用逻辑与业务逻辑松耦合方面，请记住以下规则：

*   不要将事件对象传递给其他方法；只传递事件对象中你需要的数据。
*   应用程序中可能的任何操作都应该可以在不执行事件处理器的情况下实现。
*   事件处理器应该处理事件，然后将处理交给应用程序逻辑。

在任何代码库中，记住这种方法对于维护来说都是巨大的胜利，为测试和进一步开发开启了无数可能性。

## 编写可维护的 JavaScript

编写可维护的`JavaScript`不仅仅关乎代码的格式，还关乎代码的功能。在企业环境中创建的 Web 应用程序通常由许多人同时开发。在这些情况下，目标是确保每个人工作的浏览器环境具有一致且不变的规则。为了实现这一点，开发者应该遵循某些编程实践。

### 尊重对象所有权

`JavaScript`的动态特性意味着几乎任何内容在任何时间都可以被修改。人们说`JavaScript`中没有什么是神圣不可侵的，因为你无法将某些内容标记为最终或常量。随着`ECMAScript 5`引入了防篡对象（在第 22 节中讨论），情况发生了一些变化，但默认情况下，所有对象都是可以修改的。在其他语言中，当你没有实际源代码时，对象和类是不可变的。`JavaScript`允许你在任何时间修改任何对象，这使得以意想不到的方式覆盖默认行为成为可能。由于语言本身没有施加限制，因此开发者进行限制是非常重要且必要的。

在企业环境中，最重要的编程实践可能就是尊重对象所有权，这意味着不要修改不属于你的对象。简单来说：如果你不负责某个对象、其构造函数或其方法的创建或维护，你就不应该对其进行更改。更具体地说：

*   不要在实例或原型上添加属性。
*   不要在实例或原型上添加方法。
*   不要重新定义现有方法。

问题在于，开发者假设浏览器环境是按照某种方式运行的。对被多人使用的对象进行更改意味着错误将会发生。如果有人期望调用`stopEvent()`函数来取消事件的默认行为，而你修改了它使其既执行了该操作又附加了其他事件处理器，那么问题将随之而来。其他开发者假设该函数只是执行它最初执行的功能，因此他们的用法将是错误的且可能是有害的，因为他们不知道副作用。

这些规则不仅适用于自定义类型和对象，还适用于原生类型和对象，例如`Object`、`String`、`document`、`window`等。这里的潜在问题更加危险，因为浏览器厂商可能会以不经通知且意料之外的方式更改这些对象。这种情况的一个例子出现在流行的 Prototype JavaScript 库中，它在`document`对象上实现了`getElementsByClassName()`方法，返回一个`Array`实例，而该实例还被扩展以包含一个名为`each()`的方法。John Resig 在博客上概述了导致该问题的事件序列。在他的文章（[`ejohn.org/blog/getelementsbyclassname-pre-prototype-16/`](http://ejohn.org/blog/getelementsbyclassname-pre-prototype-16/)）中，他提到当浏览器开始原生实现`getElementsByClassName()`时问题发生了，该方法返回的不是`Array`而一个没有`each()`方法的`NodeList`。使用 Prototype 库的开发者习惯了编写这样的代码：

```
document.getElementsByClassName("selected").each(Element.hide);
```

尽管这段代码在没有原生实现`getElementsByClassName()`的浏览器中运行良好，但由于返回值差异，它在实现了浏览器中导致了错误。你无法预测浏览器厂商未来将如何更改原生对象，因此以任何方式修改它们都可能导致当你的实现与他们的冲突时出现问题。

因此，最好的方法是永远不要修改你不拥有的对象。只有当你自己创建对象时（例如自定义类型或对象字面量），你才拥有该对象。你不拥有`Array`、`document`等，因为它们在你代码执行之前就已经那里了。你仍然可以通过以下方式为对象创建新功能：

*   创建一个具有所需功能的新对象，并让它与目标对象交互。
*   创建一个继承自你想要修改的类型的自定义类型。然后你可以用额外的功能修改自定义类型。

许多`JavaScript`库现在都遵循这种开发理论，允许它们在浏览器不断变化的情况下成长和适应。

### 避免全局变量

与尊重对象所有权密切相关的是尽可能避免全局变量和函数。再次，这与创建一个执行脚本的一致且可维护的环境有关。最多应该创建一个单一全局变量，其他对象和函数存在于其。考虑以下内容：

```javascript
//两个全局变量 - 避免！！！
var name = "Nicholas";
function sayName(){
    alert(name);
}
```

这段代码包含两个全局变量：变量`name`和函数`sayName()`。它们很容易在包含两者的对象上创建，如示例所示：

```javascript
//一个全局变量 - 优先
var MyApplication = {
    name: "Nicholas",
    sayName: function(){
        alert(this.name);
    }
};
```

这段重写后的代码引入了单一全局对象`MyApplication`，`name`和`sayName()`都被附加在其上。这样做消除了之前代码中几个问题。首先，变量`name`覆盖了`window.name`属性，这可能会干扰其他功能。其次，它有助于消除对功能所在位置的困惑。调用`MyApplication.sayName()`是一个逻辑提示，代码中的任何问题都可以通过查看定义`MyApplication`的代码来识别。

单一全局方法的扩展是命名空间（namespacing）概念，该概念由 Yahoo! User Interface (YUI) 库普及。命名空间涉及创建一个对象来持有功能。在 YUI 的 2.x 版本中，有多个挂载了功能的命名空间。以下是一些示例：

*   `YAHOO.util.Dom` — 用于操作 DOM 的方法。
*   `YAHOO.util.Event` — 与事件交互的方法。
*   `YAHOO.lang` — 帮助处理底层语言特征的方法。

对于 YUI，单一全局对象`YAHOO`作为一个容器，其他对象定义在其上面。每当对象被简单地以这种方式分组功能时，它们被称为命名空间。整个 YUI 库都构建在这一概念之上，允许它与任何 JavaScript 库在同一个页面上共存。

命名空间的重要部分是决定一个大家都同意使用的全局对象名称，并且该名称足够独特，使得其他人不太可能也使用。在大多数情况下，这可以是你正在开发代码的公司名称，例如`YAHOO`或`Wrox`。然后你可以开始创建命名空间来对你的功能分组，如下所示：

```javascript
var Wrox = {};

Wrox.ProJS = {};

Wrox.ProJS.EventUtil = {
    // 事件处理相关方法
};

Wrox.ProJS.DomUtil = {
    // DOM 操作相关方法
};
```



// 创建全局对象
var Wrox = {};

// 为 Professional JavaScript 创建命名空间
Wrox.ProJS = {};

// 附加书籍中使用的其他对象
Wrox.ProJS.EventUtil = { ... };
Wrox.ProJS.CookieUtil = { ... };
```

在这个示例中，`Wrox` 是创建命名空间的全局对象。如果书中的所有代码都放在 `Wrox.ProJS` 命名空间下，就留给了其他作者在 `Wrox` 对象上添加他们的代码。只要大家都遵循这种模式，就不必担心别人也会编写一个名为 `EventUtil` 或 `CookieUtil` 的对象，因为它存在于不同的命名空间中。考虑这个示例：

```javascript
// 为 Professional Ajax 创建命名空间
Wrox.ProAjax = {};

// 附加书籍中使用的其他对象
Wrox.ProAjax.EventUtil = { ... };
Wrox.ProAjax.CookieUtil = { ... };

// 你仍然可以访问 ProJS 的
Wrox.ProJS.EventUtil.addHandler( ... );

// 单独访问 ProAjax 的
Wrox.ProAjax.EventUtil.addHandler( ... );
```

虽然命名空间需要更多的代码，但为了可维护性的考虑，这种权衡是值得的。命名空间有助于确保你的代码能够非破坏地与页面上的其他代码共同工作。

## 避免 `null` 比较

由于 JavaScript 不进行任何自动类型检查，这变成了开发者的责任。因此，JavaScript 代码中实际执行的类型检查很少。最常见的类型检查是检查一个值是否为 `null`。遗憾的是，对 `null` 的检查被过度使用，并且经常由于类型检查不足而导致错误。考虑以下内容：

```javascript
function sortArray(values) {
    if (values != null) { // 避免！！

        values.sort(comparator);
    }
}
```

该函数的作用是根据指定的比较器对数组进行排序。`values` 参数必须是一个数组函数才能正确执行，但 `if` 语句简单地检查 `values` 是否为 `null`。有多个值可以通过这个 `if` 语句，包括任何字符串或任何数字，这会导致函数抛出错误。

现实中，`null` 比较很少好到足够。应该根据值预期的类型进行检查，而不是根据它们不预期的类型进行检查。例如，在之前的代码中，`values` 参数预期是一个数组，因此你应该检查它是否为数组，而不是检查它是否不是 `null`。该函数可以更合适地重写如下：

```javascript
function sortArray(values) {
    if (values instanceof Array) { // 推荐

        values.sort(comparator);
    }
}
```

此版本的函数可以防止所有无效值，并且完全不需要使用 `null`。

![image](img/pen.gif)

这种识别数组的技术在多框架 Web 中无法正常工作，因为每个框架都有自己的全局对象，因此也有它们自己的 `Array` 构造函数。如果你正在将数组从一个框架传递到另一个框架，你可能希望测试 `sort()` 方法是否存在。

如果你在代码中看到 `null` 比较，尝试使用以下技术之一进行替换：

* 如果该值应该是引用类型，请使用 `instanceof` 运算符来检查其构造函数。
* 如果该值应该是原始类型，请使用 `typeof` 运算符来检查其类型。
* 如果你期望一个具有特定方法名的对象，请使用 `typeof` 运算符确保对象上存在给定名称的方法。

代码中的 `null` 比较越少，越容易确定代码的目的并消除不必要的错误。

## 使用常量

尽管 JavaScript 没有正式的常量概念，但它们仍然很有用。其思想是将数据与应用程序逻辑隔离开来，这样在更改数据时就不会有引入引入的风险。考虑以下内容：

```javascript
function validate(value) {
    if (!value) {
        alert("Invalid value!");
        location.href = "/errors/invalid.php";
    }
}
```

该函数中有两个数据：显示给用户的消息和 URL。显示在用户界面上的字符串应该始终被提取，以便进行国际化。URL 也应该被提取，因为它们随着应用程序的增长而倾向于改变。基本上，这些每项都可能由于某种原因发生变化，而变化意味着进入函数并更改那里的代码。每当你更改应用程序逻辑代码时，你就打开了创建错误的可能性。通过将数据提取到单独定义的常量中，你可以保护应用程序逻辑不受数据变化。考虑以下示例：

```javascript
var Constants = {
    INVALID_VALUE_MSG: "Invalid value!",
    INVALID_VALUE_URL: "/errors/invalid.php"
};

function validate(value) {
    if (!value) {
        alert(Constants.INVALID_VALUE_MSG);
        location.href = Constants.INVALID_VALUE_URL;
    }
}
```

在这个重写的代码版本中，消息和 URL 都定义在 `Constants` 对象上；函数然后引用这些值。这种设置允许数据发生变化，而你永远不需要碰它的函数。`Constants` 对象甚至可以定义在完全不同的文件中，该文件可以通过某些根据国际化设置包含正确值的进程生成。

关键是将数据与使用它的逻辑分离。需要查找的值的类型如下：

* 重复值 — 任何在多个地方使用的值都应该提取为常量。这限制了当一个值改变而其他值未改变时的错误概率。这包括 CSS 类名。
* 用户界面字符串 — 任何要显示给用户的字符串都应该提取出来以便更容易国际化。
* URL — 资源位置在 Web 应用中往往经常变化，因此建议在一个共同的地方存储所有 URL。
* 任何可能变化的值 — 每当你使用代码中使用字面量值时，问问自己这个值在未来可能会改变。如果答案是肯定的，那么该值应该提取为常量。

使用常量是企业级 JavaScript 开发的一种重要技术，因为它使代码更具可维护性，并使其不受数据变化的影响。

## 性能

自该语言首次引入以来，每个页面编写的 JavaScript 代码量已大幅增加。随着这种增长，人们对 JavaScript 代码的运行时执行产生了担忧。JavaScript 最初是一种解释语言，因此执行速度明显慢于编译型语言。Chrome 是第一个引入优化引擎将 JavaScript 编译为原生代码的浏览器。从那时起，所有其他浏览器浏览器效效并实现了 JavaScript 编译。

即使转向编译后的 JavaScript，仍然可能编写慢代码。然而，有一些基本模式，遵循这些模式可以确保代码以快的速度执行。

### 注意作用域

第 4 章讨论了 JavaScript 中的作用域概念以及作用链如何工作。随着作用链中作用域数量增加，访问当前作用域之外变量的时间也越随增加。访问全局变量总是比访问局部变量慢，因为必须遍历作用链。你任何可以减少遍历作用链花费时间的操作都会提高脚本的整体性能。

### 避免全局查找

为了提高脚本性能你可以做的最重要的事情可能是警惕全局查找。全局变量和函数的运行成本总是比局部的高，因为它们涉及作用链查找。考虑以下函数：

```javascript
function updateUI() {
    var imgs = document.getElementsByTagName("img");

    for (var i = 0, len = imgs.length; i < len; i++) {
        imgs[i].title = document.title + " image " + i;
    }

    var msg = document.getElementById("msg");
    msg.innerHTML = "Update complete.";
}
```

这个函数看起来完全没问题，但它对全局 `document` 对象有三次引用。如果页面上有多个图片，`for` 循环中的 `document` 引用可能会执行几十次或数百次，每次都需要作用链查找。通过创建一个指向 `document` 对象的局部变量，你可以通过将全局查找限制为仅一次来提高此函数的性能。

```javascript
function updateUI() {
    var doc = document;
    var imgs = doc.getElementsByTagName("img");

    for (var i = 0, len = imgs.length; i < len; i++) {
        imgs[i].title = doc.title + " image " + i;
    }

    var msg = doc.getElementById("msg");
    msg.innerHTML = "Update complete.";
}
```

在这里，`document` 对象首先被存储在局部变量 `doc` 中。在代码的其余部分，使用 `doc` 变量来代替 `document`。与之前的版本相比，此函数中只有一次全局查找，这确保了它的运行速度更快。

一个实用的规则是：将函数中使用的超过一次的任何全局对象存储在局部变量中。

## 避免使用 `with` 语句

在性能要求重要的地方，应该避免使用 `with` 语句。与函数类似，`with` 语句会创建自己的作用域，从而增加了在其内部执行的代码的作用域链长度。由于在作用域链查找中存在额外的步骤，在 `with` 语句内执行的代码运行速度保证比在外部执行的代码慢。

很少需要使用 `with` 语句，因为它大部分用于消除多余的字符。在大多数情况下，可以使用局部变量来完成相同的工作，而不会引入新的作用域。这里有一个示例：

```javascript
function updateBody() {
    with (document.body) {
        alert(tagName);
        innerHTML = "Hello world!";
    }
}
```

这段代码中的 `with` 语句让你更方便地使用 `document.body`。通过使用局部变量也可以相同的效果，如下：

```javascript
function updateBody() {
    var body = document.body;

    alert(body.tagName);
    body.innerHTML = "Hello world!";
}
```

虽然这段代码稍微长一点，但它的可读性比 `with` 语句更好，确保了你清楚 `tagName` 和 `innerHTML` 属于哪个对象。这段代码通过将 `document.body` 存储在局部变量中也节省了全局查找。

## 选择正确的方法

与其他语言一样，性能方程的一部分与解决问题所使用的算法或方法有关。熟练的开发者根据经验知道哪些方法可能获得更好的性能结果。在其他编程语言中通常使用的许多技术和方法也可以在 JavaScript 中使用。

### 避免不必要的属性查找

在计算机科学中，算法的复杂度使用 `O` 符号表示。最简单、最快的算法是常量值或 `O(1)`。在此之后，算法变得越来越复杂，执行时间也越长。下表列出了 JavaScript 中常见的算法类型。

| 符号 | 名称 | 描述 |
| --- | --- | --- |
| `O(1)` | 常数级 | 无论值的数量是多少，执行所需的时间都保持恒定。表示简单值的值和存储在变量中的值。 |
| `O(log n)` | 对数级 | 执行时间与值的数量有关，但算法完成时并不需要检索每个值。例如：二分查找。 |
| `O(n)` | 线性级 | 执行时间与值的数量直接相关。例如：遍历数组中的所有项。 |
| `O(n2)` | 平方级 | 执行时间与值的数量有关，使得每个值必须被检索至少 `n` 次。例如：插入排序。 |

常量值或 `O(1)` 既指字面量，也指存储在变量中的值。`O(1)` 符号表示检索常量值所需的时间与值的数量无关，保持相同。检索常量值是一个极其高效的过程，因此也非常快。考虑以下内容：

```javascript
var value = 5;
var sum = 10 + value;

alert(sum);
```

这段代码执行了四次常量值查找：数字 `5`、变量 `value`、数字 `10` 以及变量 `sum`。这段代码的整体复杂度被认为是 `O(1)`。

访问数组项在 JavaScript 中也是一个 `O(1)` 操作，其性能与简单的变量查找一样。因此，以下代码的效率与之前的示例一样：

```javascript
var values = [5, 10];
var sum = values[0] + values[1];

alert(sum);
```

使用变量和数组比访问对象上的属性更高效，属性访问是 `O(n)` 操作。对象上的每次属性查找耗时都比访问变量或数组长，因为必须在原型链上搜索具有该名称的属性。简单来说，属性查找越多，执行时间就越慢。考虑以下内容：

```javascript
var values = { first: 5, second: 10 };
var sum = values.first + values.second;

alert(sum);
```

这段代码使用两次属性查找来计算 `sum` 的值。执行一次或两次属性查找可能不会导致严重的性能问题，但执行数百或数千次无疑会减慢执行。

要警惕为了获取单个值而进行的多次属性查找。例如，考虑以下：

```javascript
var query = window.location.href.substring(window.location.href.indexOf("?"));
```

在这段代码中，有六次属性查找：三次用于 `window.location.href.substring()`，三次用于 `window.location.href.indexOf()`。你可以通过数代码中中点的数量来轻松识别属性查找。这段代码特别低效，因为 `window.location.href` 值被使用了两次，导致了两次查找。

每当对象属性被使用多次时，请将其存储在局部变量中。例如，之前的代码可以重写为：

```javascript
var url = window.location.href;
var query = url.substring(url.indexOf("?"));
```

这个版本只有四次属性查找，比原来的减少了 33%。在大脚本中进行这种优化很可能带来更大的收益。

通常情况下，只要你能降低算法的复杂度，就应该这样做。尽可能使用局部变量替换许多属性查找。此外，如果你可以选择使用数字位置或命名属性（例如对于 `NodeList` 对象），请使用数字位置。

## 优化循环

循环是编程中最常见的结构之一。循环的基本优化步骤如下：

1. **递减迭代器**：大多数循环的迭代器从 `0` 开始并递增到某个值。在许多情况下，从最大值开始每次循环递减更高效。
2. **简化终止条件**：由于终止条件每次循环都会被评估，因此它应该尽可能快。这意味着要避免属性查找或其他 `O(n)` 操作。
3. **简化循环体**：循环体执行频率最高，因此请确保它尽可能优化。确保没有执行可以轻松移动到循环之外的密集计算。
4. **使用后测试循环**：最常用的循环是 `for` 和 `while`，它们都是预测试循环。后测试循环（如 `do-while`）避免了对终止条件的初始评估，通常运行更快。

这些变化通过一个示例说明最为合适。以下是一个基础的 `for` 循环：

```javascript
for (var i = 0; i < values.length; i++) {
    process(values[i]);
}
```

这段代码将变量 `i` 从 `0` 增加到 `values` 数组中的元素总数。假设 `values` 的处理顺序无关紧要，可以将循环改为递减 `i`，如下所示：

```javascript
for (var i = values.length - 1; i >= 0; i--) {
    process(values[i]);
}
```

在这里，变量 `i` 在每次循环时都会递减 1。在此过程中，通过移除对 `values.length` 的 `O(n)` 调用并替换为对 `0` 的 `O(1)` 调用，优化了终止条件。由于循环体只有一条语句，因此无法进一步优化。然而，循环本身可以更改如下所示后测试循环（posttest loop）：

```javascript
var i = values.length - 1;

if (i > -1) {
    do {
        process(values[i]);
    } while (--i >= 0);
}
```

这里的优化是将终止条件和递减运算符合并到一个语句中。此时，任何进一步的优化都必须对 `process()` 函数本身进行，因为循环已经完全优化了。

请记住，只有当你确定始终至少有一个值需要处理时，后测试循环才有效。空数组会导致不必要的循环遍历，而预测试循环（pre-test loop）则可以避免这种情况。

### 循环展开（Unrolling Loops）

当循环的次数是有限的，通常完全消除循环并将其替换为多次函数调用会更快。考虑上一个示例中的循环。如果数组的长度始终相同，那么直接对每个元素调用 `process()` 可能会更优，如下代码所示：

```javascript
// 消除了循环
process(values[0]);
process(values[1]);
process(values[2]);
```



此示例假设`values`数组中只有三个元素，并简单地直接对每个元素调用`process()`。以这种方式展开循环可以消除建立设置循环和处理终止条件的开销，使代码运行得更快。

如果无法预判断循环的迭代次数，你可能想要考虑使用一种名为 Duff's device（Duff 技巧）的技术。该技术以其创建者 Tom Duff 的名字命名，他首次在 C 编程语言中使用了它。Jeff Greenberg 被认为在 JavaScript 中实现了 Duff's device。Duff's device 的基本思想通过计算迭代次数作为`8`的倍数，将循环展开为一系列语句。考虑以下代码示例：

```
//感谢：Jeff Greenberg 在 JS 中实现 Duff's Device
//假设 values.length > 0

var iterations = Math.ceil(values.length / 8);
var startAt = values.length % 8;
var i = 0;

do {
    switch(startAt){
        case 0: process(values[i++]);
        case 7: process(values[i++]);
        case 6: process(values[i++]);
        case 5: process(values[i++]);
        case 4: process(values[i++]);
        case 3: process(values[i++]);
        case 2: process(values[i++]);
        case 1: process(values[i++]);
    }
    startAt = 0;
} while (--iterations > 0);
```

这种 Duff's device 的实现通过将`values`数组中的元素总数除以`8`来计算循环需要多少次迭代。然后使用向上取整函数（ceiling function）确保结果是一个整数。`startAt`变量保存了如果仅基于除以`8`的迭代将无法被处理的元素数量。当循环第一次执行时，会检查`startAt`变量以确定应该进行多少额外调用。例如，如果数组中有 10 个值，`startAt`将等于`2`，因此`process()`在第一次循环时只会被调用两次。在循环底部，`startAt`被重置为`0`，因此后续每次循环都会产生八次`process()`调用。这种展开加速了大型数据集的处理。

Andrew B. King 写的书籍 *Speed Up Your Site*（New Riders, 2003）提出了一种更快的 Duff's device 技术，它将`do-while`循环分成了两个独立的循环。这里是一个示例：

```
//感谢：Speed Up Your Site (New Riders, 2003)

var iterations = Math.floor(values.length / 8);
var leftover = values.length % 8;
var i = 0;

if (leftover > 0){
    do {
        process(values[i++]);
    } while (--leftover > 0);
}

do {
    process(values[i++]);
    process(values[i++]);
    process(values[i++]);
    process(values[i++]);
    process(values[i++]);
    process(values[i++]);
    process(values[i++]);
    process(values[i++]);
} while (--iterations > 0);
```

在此实现中，当简单除以`8`时无法在循环中处理的`leftover`计数在初始循环中被处理。一旦这些额外元素被处理，执行将在主循环中继续，主循环会调用八次`process()`。这种方法几乎比原始的 Duff's device 快得多。

### 避免双重解释 (Avoid Double Interpretation)

简单除以`8`时无法在循环中处理的计数会被初始循环处理。双重解释惩罚出现在使用`eval()`函数、`Function`构造函数或使用字符串`setTimeout()`时。以下是一些示例：

```javascript
//评估某些代码 - 避免
eval("Hello world!");

// 创建新函数 - 避免
var sayHi = new Function("Hello world!");

// 设置超时 - 避免
setTimeout("Hello world!", 500);
```

在这些情况下，包含 JavaScript 代码的字符串需要被解释。这在解析阶段无法完成，因为代码位于字符串中，这意味着在运行代码时需要启动一个新的解析器。实例化新的解析器会有巨大的开销，因此运行速度较慢。

这些实例都有解决方法。在这种情况下，代码可以直接内联。

```
// 修复
alert('Hello world!');

// 创建新函数 - 修复
var sayHi = function(){
    alert('Hello world!');
};

// 设置超时 - 修复
setTimeout(function(){
    alert('Hello world!');
}, 500);
```

- **位运算符速度快** —— 在执行数学运算时，位运算始终总是比任何布尔或数值算术运算快。选择性地将算术运算替换为位运算，可以极大提高复杂计算的性能。取模、逻辑与（AND）和逻辑或（OR）等操作是替换为位运算的理想选择。

## 减少语句数量

JavaScript 代码中的语句数量会影响操作执行的速度。单个语句完成多个操作的速度通常比每个语句执行单个操作的多个语句要快。因此，任务是寻找可以组合的语句，以缩短整个脚本的执行时间。为了这一点，你可以寻找以下几种模式。

### 多变量声明

开发者往往倾向于创建过多语句的一个领域是声明多个变量。在代码中看到多个`var`语句声明多个变量的情况非常常见，例如：

```javascript
//四条语句 - 浪费
var count = 5;
var color = "blue";
var values = [1,2,3];
var now = new Date();
```

在强类型语言中，不同数据类型的变量必须在单独的语句中声明。但在 JavaScript 中，所有变量都可以使用单个`var`语句声明。前面的代码可以重写为：

```javascript
//一条语句
var count = 5,
    color = "blue",
    values = [1,2,3],
    now = new Date();
```

在这里，变量声明使用单个`var`语句并用逗号分隔。这是在大多数情况下易于实现的优化，而且执行速度比单独声明每个变量要快得多。

### 插入迭代值

每当你使用迭代值（即在不同位置不断增加或减少小的值）时，请尽可能合并语句。考虑以下代码片段：

```javascript
var name = values[i];
i++;
```

上述两个语句中的每一个都有一个单一目的：第一个从`values`中检索一个值并将其存储在`name`中；第二个增加变量`i`。通过将迭代值插入到第一条语句中，可以将它们合并为一条语句，如下：

```javascript
var name = values[i++];
```

这条语句完成了与之前两个语句相同的工作。由于递增运算符是后置的，在语句其余部分执行之前，`i`的值不会增加。每当你遇到类似的情况时，尝试将迭代值插入到使用它的最后一条语句中。

### 使用数组和对象字面量

在本书中，你看到了创建数组和对象的两种方法：使用构造函数或使用字面量（literal）。使用构造函数总是会导致比插入项目或定义属性所需的语句更多的语句，而字面量则在单条语句中完成所有操作。考虑以下示例：

```javascript
//四条语句来创建并初始化数组 - 浪费
var values = new Array();
values[0] = 123;
values[1] = 456;
values[2] = 789;

//四条语句来创建并初始化对象 - 浪费
var person = new Object();
person.name = "Nicholas";
person.age = 29;
person.sayName = function(){
    alert(this.name);
};
```

在这段代码中，创建并初始化了一个数组和一个对象。每个都需要四条语句：一条调用构造函数，三条用于分配数据。这些可以很容易地转换为使用字面量，如下：

```javascript
//一条语句创建并初始化数组
var values = [123, 456, 789];

//一条语句创建并初始化对象
var person = {
    name : "Nicholas",
    age : 29,
    sayName : function(){
        alert(this.name);
    }
};
```

重写后的代码仅包含两条语句：一条用于创建并初始化数组，另一条用于创建并初始化对象。以前需要八条语句，现在只需要两条。

当`innerHTML`被赋值为一个值时，后台会创建一个 HTML 解析器，并使用原生 DOM 调用而非基于 JavaScript 的 DOM 调用来创建 DOM 结构。原生方法的执行速度快得多，因为它们是经过编译的而不是解释执行的。之前的示例可以重写为使用`innerHTML`，如下：

```
var list = document.getElementById("myList"),
    html = "",
    i;

for (i=0; i < 10; i++) {
    html += "<li>Item " + i + "</li>";
}

list.innerHTML = html;
```

这段代码构建了一个 HTML 字符串并将其赋值给`list.innerHTML`，从而创建相应的 DOM 结构。虽然字符串拼接总会有细微的性能损耗，但这种技术的执行速度仍然比多次进行 DOM 操作要快。

使用`innerHTML`的关键（与其他 DOM 操作一样）在于尽可能减少调用它的次数。例如，以下代码在执行此操作时过度使用了`innerHTML`：

```
var list = document.getElementById("myList"),
    i;

for (i=0; i < 10; i++) {
    list.innerHTML += "<li>Item " + i + "</li>";     // 避免！！！
}
```

这段代码的问题在于，每次循环都会调用`innerHTML`，这是极其低效的。事实上，对`innerHTML`的调用是一个实时更新，应该被视为此类操作。构建一个字符串并调用一次`innerHTML`比比多次调用`innerHTML`要快得多。

## 使用事件委托

大多数 Web 应用程序广泛使用事件处理程序进行用户交互。页面上的事件处理程序数量与页面响应用户交互的速度之间存在直接关系。为了减轻这些影响，你应该尽可能使用事件委托。

正如第 13 章所讨论的，事件委托利用了事件冒泡机制。任何可以冒泡的事件不仅可以在事件目标处处理，也可以在目标的任何祖先节点处处理。利用这一知识，你可以在高层附加事件处理程序，负责处理多个目标的事件。尽可能在`document`级别上附加一个事件处理程序，用以处理整个页面的事件。

## 注意 HTMLCollections

书中一直讨论了`HTMLCollection`对象的陷阱，因为它们是 Web 应用程序的性能杀手。请记住，每当你访问`HTMLCollection`（无论是通过属性还是方法）时，你都在对文档进行查询，而这种查询是非常昂贵的。减少访问`HTMLCollection`的次数可以极大提高脚本的性能。

优化`HTMLCollection`访问最重要的领域可能过于循环中。之前讨论过将`length`计算移动到`for`循环的初始化部分。现在考虑这个示例：

```
var images = document.getElementsByTagName("img"),
    i, len;

for (i=0, len=images.length; i < len; i++){
    //处理
}
```

这里的关键在于长度被存储在`len`变量中，而不是不断访问`HTMLCollection`的`length`属性。在循环中使用`HTMLCollection`时，你的下一步应该是获取你将要使用的项的引用，如下所示，以避免在循环体内多次调用`HTMLCollection`：

```
var images = document.getElementsByTagName("img"),
    image,
    i, len;

for (i=0, len=images.length; i < len; i++){
    image = images[i];
    //处理
}
```

这段代码增加了`image`变量，用于存储当前图像。一旦完成，循环内部就不应该理由再次访问`images` `HTMLCollection`了。

在编写 JavaScript 时，意识到何时返回了`HTMLCollection`对象很重要，这样你就可以减少它们的访问。当发生以下情况时，会返回`HTMLCollection`对象：

*   调用了`getElementsByTagName()`。
*   获取了元素的`childNodes`属性。
*   获取了元素的`attributes`属性。
*   访问了特殊集合，例如`document.forms`、`document.images`等。

理解何时使用`HTMLCollection`对象并确保恰当当使用它们，可以大大加快代码的执行速度。

## 部署

任何 JavaScript 解决方案最重要的部分可能是最终部署到生产环境的网站或 Web 应用程序。在此之前，你已经做了大量工作，为通用消费设计并优化了解决方案。现在是时候离开开发环境进入 Web 世界了，真实用户可以在那里与之交互。但在在此之前，有许多问题需要解决。

### 构建过程

为了让 JavaScript 代码准备好部署，你可以做的最重要的事情之一是在其周围开发某种构建过程。软件开发的典型模式是`编写-编译-测试`，即你编写代码、编译它，然后运行以确保其工作正常。由于 JavaScript 不是编译型语言，这种模式已变为`编写-测试`，你编写的代码与你在浏览器中测试的代码是同一份。这种方法的问题在于它并不是最优的；由于以下原因，你编写的代码不应该原封不动地传递给浏览器：

*   知识产权问题 —— 如果你将带有详尽注释的源码发布到网上，其他人将更容易发现你在做什么、复用它，并可能发现安全漏洞。
*   文件大小 —— 你以易读的方式编写代码，这对于维护是有益的，但对性能不利。浏览器并不会从空格、缩进或冗长的函数名中受益。
*   代码组织 —— 你为了维护而组织的代码方式未必是交付的最佳方式。

由于这些原因，最好为你的 JavaScript 文件定义构建过程。

构建过程从定义在版本控制中存储文件的逻辑结构开始。最好避免使用包含所有 JavaScript 的单个文件。相反，遵循面向对象语言的做法：将每个对象或自定义类型分离到文件中。这样做可以确保每个文件包含最少的代码，从而更容易更改而不引入错误。此外，在那些并发版本控制系统（如`CVS`或`Subversion`）的环境中，这减少了合并操作时的冲突风险。

请记住，将代码拆分为多个文件是为了维护，而不是为了部署。对于部署，你希望将源代码合并成一个或多个合并文件（rollup files）。建议 Web 应用程序尽可能少使用 JavaScript 文件，因为 HTTP 请求是 Web 上主要的性能瓶颈之一。记住，通过`<script>`标签引入 JavaScript 文件是一个阻塞操作，在代码下载和执行期间会停止所有其他下载。因此，请在逻辑上将 JavaScript 代码分组到部署文件中。

一旦你组织了文件和目录结构，并确定了部署文件中应该包含的内容，你将想要创建一个构建系统。`Ant`构建工具（[`ant.apache.org`](http://ant.apache.org)）最初是为了自动化 Java 构建过程而创建的，但由于其易用性以及软件工程师的覆盖，在 Web 开发者中广受欢迎，例如 Julien Lecomte 等工程师编写了关于如何使用 Ant 进行 JavaScript 和 CSS 构建自动化的教程（Lecomte 的文章可以在`[www.julienlecomte.net/blog/2007/09/16/](http://www.julienlecomte.net/blog/2007/09/16/)`找到）。

Ant 是非常理想的 JavaScript 构建系统，因为它具有简单的文件处理能力。例如，你可以轻松地获取目录中所有文件的列表，然后将它们合并成单个文件，如下所示：

![image](img/logo1.gif)

```xml
<project name="JavaScript Project" default="js.concatenate">
    <!-- 输出目录 -->
    <property name="build.dir" value="./js" />



<!-- 源文件所在目录 -->

<property name="src.dir" value="./dev/src" />

<!-- 合并所有 JS 文件的目标 -->

<!-- Credit: Julien Lecomte, http://www.julienlecomte.net/blog/2007/09/16/ -->

<target name="js.concatenate">

    <concat destfile="${build.dir}/output.js">

        <filelist dir="${src.dir}/js" files="a.js, b.js"/>

        <fileset dir="${src.dir}/js" includes="*.js" excludes="a.js, b.js"/>

    </concat>

</target>

</project>

### SampleAntDir/build.xml

此`build.xml`文件定义了两个属性：最终文件输出的构建目录，以及存放 JavaScript 源文件的源目录。目标`js.concatenate`使用`<concat>`元素来指定需要合并的文件列表以及生成文件的输出位置。`<filelist>`元素用于指定`a.js`和`b.js`文件应该排在合并后文件的前面，而`<fileset>`元素表示目录中的所有其他文件（排除`a.js`和`b.js`）都应随之添加。生成的文件将输出到`/js/output.js`。

安装好 Ant 后，你可以进入此`build.xml`文件所在的目录，并运行以下代码段：

```bash
ant
```

构建过程随之启动，并生成合并后的文件。如果文件中还有其他目标，你可以使用以下代码执行`js.concatenate`目标：

```bash
ant js.concatenate
```

根据你的需求，可以更改构建过程以包含更多或更少的步骤。在开发周期中引入构建步骤，可以为你提供一个位置，让你在部署之前对 JavaScript 文件进行更多额外的处理。

### 验证

尽管理解并支持 JavaScript 的 IDE 已经开始出现，但大多数开发者仍然通过在浏览器中运行代码来检查语法。这种方法存在两个问题：首先，这种验证无法容易地自动化或在系统之间迁移。其次，除了语法错误外，问题只有在代码执行时才会被发现，这导致错误可能会发生。有许多工具可以帮助识别 JavaScript 代码中的潜在问题，最流行的是 Douglas Crockford 的 JSLint（[www.jslint.com](http://www.jslint.com)）。

JSLint 会查找 JavaScript 代码中的语法错误和常见的编码错误。它列出的一些潜在问题如下：

* 使用`eval()`
* 使用了未声明的变量
* 缺少分号
* 不当的换行
* 错误的逗号用法
* 语句周围缺少大括号
* switch 分支中缺少`break`
* 变量重复声明
* 使用`with`
* 错误地使用等号（而不是双等号`==`或三等号`===`）
* 不的代码

提供了在线版本方便访问，但也可以使用基于 Java 的 Rhino JavaScript 引擎（[www.mozilla.org/rhino/](http://www.mozilla.org/rhino/)）在命令行运行。要在命令行上运行`JSLint`，必须先下载 Rhino，然后从`www.jslint.com/rhino/`下载 Rhino 版本的 JSLint。安装完成后，你可以使用以下语法在命令行运行`JSLint`：

```bash
java -jar rhino-1.6R7.jar jslint.js [input files]
```

这里是一个示例：

```bash
java -jar rhino-1.6R7.jar jslint.js a.js b.js c.js
```

如果给定文件中存在任何语法问题或潜在错误，将输出包含错误和警告的报告。如果没有问题，代码将完成执行而不显示任何消息。

你可以通过 Ant 的如下目标，作为构建过程的一部分来运行`JSLint`：

![image](img/logo1.gif)

```xml
<target name="js.verify">

    <apply executable="java" parallel="false">

        <fileset dir="${build.dir}" includes="output.js"/>

        <arg line="-jar"/>

        <arg path="${rhino.jar}"/>

        <arg path="${jslint.js}" />

        <srcfile/>

    </apply>

</target>
```

### SampleAntDir/build.xml

此目标假设 Rhino jar 文件的位置通过属性`rhino.jar`指定，且 JSLint Rhino 文件的位置通过属性`jslint.js`指定。`output.js`文件将传递给`JSLint`进行验证，并将输出它发现的任何问题。

在开发周期中添加代码验证有助于避免以后出现错误。建议开发者在构建过程中添加某种类型的代码验证，作为在问题变成错误之前识别潜在问题的方法。

![image](img/pen.gif)

JavaScript 代码验证列表可见附录 D。

### 压缩

当讨论 JavaScript 压缩时，你实际上是在讨论两个概念：代码大小和传输权重（wire weight）。代码大小指的是浏览器解析所需的字节数，而传输权重指的是实际传输到客户端的字节数。在网页开发的早期，这两个数字几乎是相同的，因为源代码是被原封不动传输到客户端的。但在今天，两者很少相等。不过，你可以使用压缩器来减小文件大小。

压缩器通常会执行以下部分或全部步骤：

* 移除额外的空格（包括换行）
* 移除注释
* 压缩变量名

有很多 JavaScript 压缩器（完整列表见附录 D），但最好的可能是 YUI Compressor，访问[`developer.yahoo.com/compressor/`](http://developer.yahoo.com/compressor/)。YUI Compressor 使用 Rhino JavaScript 解析器对代码进行分词处理。该标记流可以用于创建一个无空格的最佳版本。

YUI Compressor 以名为`yuicompress-x.y.z.jar`的 Java jar 文件提供，其中`x.y.z`是版本号。在写作期间，`2.4.6`是最新版本。你可以使用以下命令行格式执行 YUI Compressor：

```bash
java -jar yuicompress-x.y.z.jar [options] [input file]
```

YUI Compressor 的选项如下表所示。

| 选项 | 描述 |
| --- | --- |
| -h | 显示帮助信息。 |
| -o outputFile | 指定输出文件的名称。如果不包含，输出文件名将在输入文件名后加上 "-min"。例如，输入文件`input.js`将产生`input-min.js`。 |
| --line-break column | 指定在列数后包含换行符。默认情况下，压缩后的文件在一行输出，这在某些源码控制系统中可能会问题。 |
| -v, --verbose | 详细模式。输出有助于压缩的提示和警告。 |
| --charset charset | 指定输入文件所在的字符集。输出文件将使用相同的字符集。 |
| --nomunge | 关闭本地变量名替换。 |
| --disable-optimizations | 关闭 YUI Compressor 的微优化。 |
| --preserve-semi | 保留本会被移除的非必要分号。 |

例如，可以使用以下命令将`CookieUtil.js`文件压缩为仅名为`cookie.js`的文件：

```bash
java -jar yuicompressor-2.3.5.jar -o cookie.js CookieUtil.js
```

你也可以通过直接调用`java`可执行文件来从 Ant 中使用 YUI Compressor，例所示：

![image](img/logo1.gif)

```xml
<!-- Credit: Julien Lecomte, http://www.julienlecomte.net/blog/2007/09/16/ -->

<target name="js.compress">

    <apply executable="java" parallel="false">

        <fileset dir="${build.dir}" includes="output.js"/>

        <arg line="-jar"/>

        <arg path="${yuicompressor.jar}"/>

        <arg line="-o ${build.dir}/output-min.js"/>

        <srcfile/>

    </apply>

</target>
```

`SampleAntDir/build.xml`

此目标包含单个文件，即构建过程中创建的`output.js`文件，并将其传递给 YUI Compressor。输出文件指定为同一目录下的`output-min.js`。这假设了属性`yuicompressor.jar`包含了 YUI Compressor jar 文件的位置。你可以使用以下命令运行此目标：

```bash
ant js.compress
```

在将代码部署到生产环境之前，所有的 JavaScript 文件都应该使用 YUI Compressor 或类似的工具进行压缩。在你的构建过程中添加一个压缩 JavaScript 文件的步骤是确保这一操作始终发生的简单方法。

## HTTP 压缩

传输权重（Wire weight）指的是从服务器发送到浏览器的实际字节数。由于服务器和浏览器都具有压缩能力，字节数并不一定与代码大小相同。所有五大主流浏览器——Internet Explorer、Firefox、Safari、Chrome 和 Opera 均都支持对接收到的资源进行客户端解压缩。因此，服务器能够根据服务器的能力来压缩 JavaScript 文件。作为服务器响应的一部分，会包含一个标头，指示该文件已使用特定的格式进行了压缩。浏览器随后查看标头以确定文件已压缩，然后使用相应的格式进行解压缩。结果是，网络上传输的字节数远少于原始代码大小。

对于 Apache Web 服务器，有两个模块可以让 HTTP 压缩变得简单：`mod_gzip`（用于 Apache 1.3.x）和`mod_deflate`（用于 Apache 2.0.x）。对于`mod_gzip`，你可以通过向`httpd.conf`文件或`.htaccess`文件添加以下行来启用 JavaScript 文件的自动压缩：

```apache
#告诉 mod_gzip 包含任何以 .js 结尾的文件
mod_gzip_item_include         file       \.js$
```

此行告诉`mod_gzip`压缩从浏览器请求的任何以`.js`结尾的文件。假设你所有的 JavaScript 文件都以`.js`结尾，这将压缩每个请求并应用相应的标头以指示内容已压缩。有关关于`mod_gzip`的更多信息，请访问项目网站`www.sourceforge.net/projects/mod-gzip/`。

对于`mod_deflate`，你同样可以包含单行来确保 JavaScript 文件在发送之前被压缩。将以下行放入你的`httpd.conf`文件或`.htaccess`文件中：

```apache
#告诉 mod_deflate 包含所有 JavaScript 文件
AddOutputFilterByType DEFLATE application/x-javascript
```

注意，此行使用响应的 MIME 类型来决定是否对其进行压缩。记住，尽管`<script>`标签的`type`属性使用的是`text/javascript`，但 JavaScript 文件通常以`application/x-javascript`的 MIME 类型提供。有关关于`mod_deflate`的更多信息，请访问`http://httpd.apache.org/docs/2.0/mod/mod_deflate.html`。

`mod_gzip`和`mod_deflate`都能节省 JavaScript 文件原始大小约 70% 的空间。这很大程度上是因为 JavaScript 文件是纯文本，因此可以非常高效地压缩。减少文件的传输权重可以缩短传输到浏览器的时间。请记住，这存在微小的权衡，因为服务器必须在每个请求时花费时间压缩文件，而浏览器在文件到达后需要一些时间来解压缩文件。但总的来说，这种权衡是完全值得的。

![image](img/pen.gif)

大多数 Web 服务器（无论是开源还是商业）都具有某些 HTTP 压缩能力。请咨询你服务器的文档以确定如何正确配置压缩。

## 总结

随着 JavaScript 开发的成熟，最佳实践也应运而生。曾经被视为业好的领域现在已是一项正规的职业，因此，它已经经历了针对可维护性、性能和部署的研究，而这些研究通常是针对其他编程语言的。

JavaScript 的可维护性部分与以下代码规范有关：

* 可以使用其他语言的代码规范来决定何时注释以及如何缩进，但 JavaScript 需要一些特殊规范来弥补该语言弱类型的的特性。
* 由于 JavaScript 需要与 HTML 和 CSS 共存，同样重要的是让每个完全定义其职责：JavaScript 应该定义行为，HTML 定义内容，CSS 定义外观。
* 任何这些职责的混合会导致难以调试的错误。

随着 JavaScript 在 Web 应用中数量增加，性能变得越来越重要。因此，请记住以下几点：

* JavaScript 执行所需直接影响网页的整体性能，因此其重要性不容忽视。
* 许多针对 C 语言的性能建议也适用于 JavaScript，关于循环性能以及使用 switch 语句代替 if。
* 另一个需要记住的重要点是 DOM 操作是昂贵的，所以你应该限制 DOM 操作次数。

流程的最后一步是部署。以下是本章讨论的几个关键点：

* 为了辅助部署，你应该建立一个构建过程，将 JavaScript 文件合并为少数几个文件（理想情况下只有一个）。
* 拥有构建过程还让你有机会对源代码运行额外的处理过程和过滤器。例如，你可以运行一个 JavaScript 验证器以确保代码没有语法错误或潜在问题。
* 还建议在部署之前使用压缩器使文件尽可能小。

# 第 25 章：新兴 API

### 本章包含内容？

* 创建平滑动画
* 文件操作
* 使用 Web Workers 进行后台 JavaScript

HTML5 的引入也促进了面向 Web 应用的 JavaScript API 的巨大增长。这些 API 并不是 HTML5 规范的一部分，而是存在于自己的规范中，这些规范通常被归类为“HTML5 相关 API”。本章中的所有 API 仍在经历大量的开发，并且尚未完全稳定。

尽管如此，浏览器已经开始实现各种 API，Web 应用程序开发者也开始使用它们了。你会注意到，这些许多`APIs`在前面都有特定于浏览器的前缀，例如代表微软的“ms”或代表 Chrome 和 Safari 的“webkit”。这些前缀允许浏览器在`APIs`仍在开发期间对其进行实验，因为它们知道最终的、不带前缀的版本将与其他浏览器保持一致。

`requestAnimationFrame()`

长期以来，定时器和间隔一直是基于 JavaScript 动画的最先进技术。虽然 CSS 过渡和动画让 Web 开发者制作某些动画变得简单，但多年来，基于 JavaScript 动画的世界并没有发生太大变化。Firefox 4 是第一个包含名为`mozRequestAnimationFrame()`的 JavaScript 动画新 API 的浏览器。该方法告诉浏览器正在进行动画，以便浏览器反过来决定调度重绘的最佳方式。

## 早期动画循环

在 JavaScript 中创建动画的典型方法是使用`setInterval()`来管理所有动画。使用`setInterval()`的基础动画循环看起来如下：

```javascript
(function(){

    function updateAnimations(){

        doAnimation1();

        doAnimation2();

        //etc.

    }

    setInterval(updateAnimations, 100);

})();
```



为了构建一个小型动画库，`updateAnimations()` 方法会循环遍历运行中的动画，并对每个动画进行适当的更改（例如，新闻跑灯和进度条同时运行）。如果没有需要更新的动画，该方法可以在什么都不做的情况下退出，甚至可以停止动画循环，直到更多动画准备好更新。

这种动画循环棘手之处在于知道延迟应该是多少。间隔必须短到能够流畅地处理各种不同类型的动画，又要足够长以便产生浏览器实际上可以渲染的更改。大多数计算机显示器的刷新率为 60 Hz，这基本上意味着每秒重绘 60 次。大多数浏览器都限制了重绘次数，不会尝试进行高于该频率的重绘，因为它们知道最终用户的体验不会得到任何提升。

因此，最平滑动画的最佳间隔是 `1000ms / 60`，大约是 `17ms`。你在这个速率下看到最平滑的动画，因为你更精确地镜像了浏览器的能力。在使用间隔为 `17ms` 的动画循环循环时，多个动画可能需要节流，以防完成得太快。

尽管基于 `setInterval()` 的动画循环比使用多组基于 `setTimeout()` 的循环更高效，但仍然存在问题。`setInterval()` 和 `setTimeout()` 并不是为了精确而设计的。你作为第二个参数指定的延迟仅是代码被添加到浏览器 UI 线程队列中等待可能执行的指示。如果队列中前面还有其他任务，那么该代码将等待执行。简而言之：毫秒延迟并不是代码何时执行的指示，而只是任务何时进入队列的指示。如果 UI 线程正在忙碌（例如正在处理用户操作），那么该代码将不会立即执行。

## 间隔的问题

理解下一帧何时被绘制是实现平滑动画的关键，直到最近，还没有方法可以保证浏览器中下一帧何时会被被绘制。随着 `<canvas>` 变得流行以及新的基于浏览器的游戏出现，开发者们对 `setInterval()` 和 `setTimeout()` 的不准确性感到越来越沮丧。

加剧这些问题的是浏览器的定时器分辨率。定时器的精度并没毫秒级。以下是一些常见的定时器分辨率：

*   Internet Explorer 8 及更早版本的定时器分辨率为 `15.625ms`。
*   Internet Explorer 9 及更高版本的定时器分辨率为 `4ms`。
*   Firefox 和 Safari 的定时器分辨率为 `~10ms`。
*   Chrome 的定时器分辨率为 `4ms`。

第 9 版之前的 Internet Explorer 定时器分辨率为 `15.625ms`，因此 `0` 到 `15` 之间的任何值可能是 `0` 也可能是 `15`，而不是其他值。Internet Explorer 9 将定时器分辨率提高到 `4ms`，但对于动画来说这仍然不够精确。Chrome 的定时器分辨率为 `4ms`，而 Firefox 和 Safari 为 `10ms`。情况更复杂的是，浏览器开始对后台或非活动标签页的定时器进行限制。因此，即使你设置了最佳显示间隔，你仍然接近你想要的时间。

## mozRequestAnimationFrame

Mozilla 的 Robert O’Callahan 思考了这个问题并提出了一个独特的解决方案。他指出，CSS 过渡和动画受益于浏览器知道某些动画正在发生，因此计算出了刷新 UI 的正确间隔。而对于 JavaScript 动画，浏览器并不知道正在进行动画。他的解决方案是创建一个名为 `mozRequestAnimationFrame()` 的新方法，该方法告诉浏览器某些 JavaScript 代码正在执行动画。这允许浏览器在运行某些代码后进行适当优化。

`mozRequestAnimationFrame()` 方法接受一个参数，该参数是在重绘屏幕之前调用的函数。在该函数中，你对 DOM 样式进行适当更改，这些更改将在下一次重绘中反映。为了创建一个动画循环，你可以像以前使用 `setTimeout()` 那样，将多次调用 `mozRequestAnimationFrame()` 链在一起。例如：

```
function updateProgress(){

    var div = document.getElementById("status");

    div.style.width = (parseInt(div.style.width, 10) + 5) + "%";

    if (div.style.left != "100%"){

        mozRequestAnimationFrame(updateProgress);

    }

}

mozRequestAnimationFrame(updateProgress);
```

由于 `mozRequestAnimationFrame()` 只运行一次指定的函数，下次需要更改时你需要手动再次调用它。你还需要同样的方式管理何时停止动画。结果是非常平滑的动画。

到目前为止，`mozRequestAnimationFrame()` 解决了浏览器不知道动画何时发生以及不知道最佳间隔的问题，但代码代码何时实际执行的问题呢？这通过同一个解决方案解决了。

你传递给 `mozRequestAnimationFrame()` 的函数实际上接收一个参数，该参数是下次重绘何时发生的时间代码（自 1970 年 1 月 1 日起的毫秒）。这是一个非常重要的点：`mozRequestAnimationFrame()` 实际上调度了未来某个已知点的重绘，并可以告诉你何时。你就可以判断如何最佳调整你的动画。

为了确定自上一次重绘以来过了多久，你可以查询 `mozAnimationStartTime`，它包含了上一次重绘的时间代码。从传入回调的时间减去此值，可以算出在下一组更改绘制到屏幕之前精确经过了多久。使用这些值的典型模式如下：

```
function draw(timestamp){

    // 计算自上一次重绘的差值

    var diff = timestamp - startTime;

    // 使用 diff 确定正确的下一步

    // 重置 startTime 为本次重绘

    startTime = timestamp;

    // 再次绘制

    mozRequestAnimationFrame(draw);

}

var startTime = mozAnimationStartTime;

mozRequestAnimationFrame(draw);
```

关键是在传递 `mozRequestAnimationFrame()` 的回调函数之外第一次调用 `mozAnimationStartTime`。如果你在回调内部调用 `mozAnimationStartTime`，它将等于作为参数传递的时间代码。

## webkitRequestAnimationFrame 和 msRequestAnimationFrame

Chrome 和 Internet Explorer 10+ 也分别创建了它们自己的 `mozRequestAnimationFrame()` 实现版本，分别为 `webkitRequestAnimationFrame()` 和 `msRequestAnimationFrame()`。这些版本与 Firefox 的版本在两个方面略有不同。首先，回调函数中没有传递时间代码，因此你不知道下一次重绘将何时发生。其次，Chrome 增加了第二个可选参数，即发生发生改变的 DOM 元素。因此，如果你知道重绘只会发生在页面上的某一个特定元素内部，你就可以将重绘限制在那个区域。

没有与 `mozAnimationStartTime` 对应的等效方法这并不令人意外，因为在没有下一次重绘时间的情况下，该信息并不可用。不过，Chrome 有一个特定的方法称为 `webkitCancelAnimationFrame()`，它可以取消之前已调度计划的重绘。

如果你不需要精确的时间差，可以使用以下模式为 Firefox 4+、Internet Explorer 10+ 和 Chrome 创建动画循环：

```
(function(){

    function draw(timestamp){

        //计算自上一次重绘以来的差值

        var drawStart = (timestamp || Date.now()),

            diff = drawStart - startTime;

        //使用 diff 确定正确的后续步骤

        //将 startTime 重置为本次重绘

        startTime = drawStart;

        //再次绘制

        requestAnimationFrame(draw);

    }

    var requestAnimationFrame = window.requestAnimationFrame || 

                                window.mozRequestAnimationFrame || 

                                window.webkitRequestAnimationFrame || 

                                window.msRequestAnimationFrame,

        startTime = window.mozAnimationStartTime || Date.now();

    requestAnimationFrame(draw);

})();
```

该模式利用可用特性创建了一个动画循环，并对流逝的时间有一个大致的概念。在 Firefox 中，这使用了可用的时间代码信息，而 Chrome 和 Internet Explorer 则默认使用不那么准确的 `Date` 对象。使用此模式时，你可以通过时间差获得关于流逝时间的大致概念，但它显然无法告诉你 Chrome 或 Internet Explorer 中下一次重绘何时发生。尽管如此，对流逝的时间有一个大致的了解总比完全不知道要好。

通过先检查标准函数名，然后检查浏览器特定的名称，此动画循环在未来将继续工作。

`requestAnimationFrame()` API 现在正在由 W3C 草拟定为一项新建议，并由 Mozilla 和 Google 作为 Web 性能组的一部分共同开发。

## 页面可见性 API (PAGE VISIBILITY API)

Web 开发者的一个痛点是不知道用户何时与页面交互。如果页面被最小化或隐藏在另一个标签页后面，继续执行如轮询服务器更新或执行动画等功能可能没有意义。Page Visibility API 旨在为开发者提供页面是否对用户可见的信息。

API 本身非常简单，由三部分组成：

*   `document.hidden` — 一个布尔值，指示页面是否隐藏。这可能意味着页面处于后台标签页中，或者浏览器被最小化。
*   `document.visibilityState` — 一个表示四种状态之一的值：
    * 页面处于后台标签页或浏览器被最小化。
    * 页面在前台标签页中。
    * 实际页面隐藏，但可以看到页面预览（例如在 Windows 7 中，将鼠标悬停在任务栏图标上会显示预览）。
    * 页面正在屏幕外进行预渲染。
*   `visibilitychange` 事件 — 当文档从隐藏变为可见或反之时，会触发此事件。

在写本文时，只有 Internet Explorer 10 和 Chrome 实现了 Page Visibility API。Internet Explorer 为所有内容加上了“ms”前缀，而 Chrome 则为所有内容加上了“webkit”前缀。因此 `document.hidden` 在 Internet Explorer 中实现为 `document.msHidden`，在 Chrome 中实现为 `document.webkitHidden`。检查支持的最佳方法是使用以下代码：

```
function isHiddenSupported(){

    return typeof (document.hidden || document.msHidden || 

                   document.webkitHidden) != "undefined";

}
```

PageVisibilityAPIExample01.htm

同样，可以使用相同的结构检查页面是否隐藏：

```
if (document.hidden || document.msHidden || document.webKitHidden){

    //页面已隐藏

} else {

    //页面未隐藏

}
```

PageVisibilityAPIExample01.htm

注意，此代码将在不支持的浏览器中指示页面未隐藏，这是 API 为了向后兼容的有意行为。

为了在页面从可见变为隐藏或从隐藏变为可见时收到通知，你可以监听 `visibilitychange` 事件。在 Internet Explorer 中，此事件被称为 `msvisibilitychange`，在 Chrome 中被称为 `webkitvisibilitychange`。为了让此事件在两个浏览器中都能工作，你需要为每个事件分配相同的事件处理器，如示例所示：

```
function handleVisibilityChange(){

    var output = document.getElementById("output"),

        msg;

    if (document.hidden || document.msHidden || document.webkitHidden){

        msg = "页面现在隐藏了。" + (new Date()) + "<br>";

    } else {

        msg = "页面现在可见了。" + (new Date()) + "<br>";

    }

    output.innerHTML += msg;

}

//需要添加到两个地方

EventUtil.addHandler(document, "msvisibilitychange", handleVisibilityChange);

EventUtil.addHandler(document, "webkitvisibilitychange", handleVisibilityChange);
```

PageVisibilityExample01.htm

此代码在 Internet Explorer 和 Chrome 中运行良好。此外，该 API 的这部分相对稳定的，因此使用它是安全的。

实现之间最大的差异在于 `document.visibilityState`。Internet Explorer 10 PR 2 的 `document.msVisibilityState` 是一个表示四个常量之一的数值：

1. `document.MS_PAGE_HIDDEN (0)`
2. `document.MS_PAGE_VISIBLE (1)`
3. `document.MS_PAGE_PREVIEW (2)`
4. `document.MS_PAGE_PRENDER (3)`

在 Chrome 中，`document.webkitVisibilityState` 是三个可能的字符串值之一：

1. “hidden”
2. “visible”
3. “prender”

Chrome 没有提供对应的常量，尽管最终实现可能会包含它们。

由于这些差异，建议不要依赖带有厂商前缀的 `document.visibilityState`，而是坚持使用 `document.hidden`。

## geolocation API

有趣且支持良好的新 API 之一是 geolocation。 允许 JavaScript 访问用户的位置。当然，这只有在用户明确允许将信息共享给页面时才能进行。当页面尝试访问地理位置信息时，浏览器会显示一个对话框请求共享这些信息。图 25-1 显示了 Chrome 中的对话框。

Geolocation API 实现为 `navigator.geolocation`，并具有三个方法。第一个方法是 `getCurrentPosition()`，它会触发确认对话框以允许访问地理位置信息。该方法接受三个参数：成功回调函数、一个可选的失败回调函数和一个可选的选项对象。

成功回调接收一个 `Position` 对象作为其唯一参数，该对象有两个属性：`coords` 和 `timestamp`。`coords` 对象必须包含关于位置的以下信息：

*   `latitude` — 以度为单位的纬度。
*   `longitude` — 以度为单位的经度。
*   `accuracy` — 以米为单位的坐标准确度。数值越大，精度越低。

浏览器还可能可选包含以下属性：

*   `altitude` — 位置的高度，以米为单位；如果不可用则为 `null`。
*   `altitudeAccuracy` — 高度的精度，以米为单位。数值越大，精度越低。
*   `heading` — 以度为单位的罗盘方向，0 度为正北。如果无法确定方向，则值为 `NaN`。
*   `speed` — 每秒米为单位的速度；如果无法确定信息则为 `null`。

在实践中，大多数 Web 应用倾向于更频繁地使用经纬度而不是其他属性。例如，一个常见的用法是在地图上绘制用户的位置：

```
navigator.geolocation.getCurrentPosition(function(position){

    drawMapCenteredAt(position.coords.latitude, positions.coords.longitude);

});
```



失败回调函数在调用时也会接收一个参数。该参数是一个包含两个属性的对象：`message` 和 `code`。`message` 属性是人类可读的错误信息，解释了错误发生；而 `code` 属性是一个指示错误类型的数值：用户拒绝权限（1）、位置不可用（2）或超时（3）。在实践中，大多数 Web 应用仅仅是记录此类错误，但不一定会因此改变用户界面。例如：

```javascript
navigator.geolocation.getCurrentPosition(function(position){

    drawMapCenteredAt(position.coords.latitude, positions.coords.longitude);

}, function(error){

    console.log("Error code: " + error.code);

    console.log("Error message: " + error.message);

});
```

`getCurrentPosition()` 的第三个参数是一个用于指定信息类型的选项对象。有三个可以设置的选项：`enableHighAccuracy`，一个布尔值，表示请求尽可能的位置；`timeout`，等待确定位置所需的毫秒数；以及 `maximumAge`，在确定新位置之前可以使用上一次坐标的最长时间（毫秒数）。例如：

```javascript
navigator.geolocation.getCurrentPosition(function(position){

    drawMapCenteredAt(position.coords.latitude, positions.coords.longitude);

}, function(error){

    console.log("Error code: " + error.code);

    console.log("Error message: " + error.message);

}, {

    enableHighAccuracy: true,

    timeout: 5000,

    maximumAge: 25000

});
```

所有三个选项都是可选的，可以单独提供也可以与其他选项结合使用。除非你真的需要非常精确的信息，否则建议将 `enableHighAccuracy` 设置为 `false`（默认值）。启用此选项可能需要更多时间，在移动设备上可能需要更多电量。同样，如果你没有主动跟踪用户的位置，可以将 `maximumAge` 设置为 `Infinity` 以始终使用上一次坐标。

如果你想跟踪用户的位置，可以使用另一个名为 `watchPosition()` 的方法。该方法接受与 `getCurrentPosition()` 完全相同的参数。在实践中，`watchPosition()` 等同于定期调用 `getCurrentPosition()`。在第一次调用该方法时，会获取当前位置并执行成功或错误回调。之后，`watchPosition()` 会等待系统发送位置已更改的信号（它不会轮询位置）。

调用 `watchPosition()` 返回一个数值标识符，用于跟踪监听操作。可以通过将此值传递给 `clearWatch()` 方法来取消监听（类似于使用 `setTimeout()` 和 `clearTimeout()`）。例如：

```javascript
var watchId = navigator.geolocation.watchPosition(function(position){

    drawMapCenteredAt(position.coords.latitude, positions.coords.longitude);

}, function(error){

    console.log("Error code: " + error.code);

    console.log("Error message: " + error.message);

});

clearWatch(watchId);
```

此示例调用了 `watchPosition()` 并将返回的标识符存储在 `watchId` 中。随后，将 `watchId` 传递给 `clearWatch()` 以取消监听操作。

Internet Explorer 9+、Firefox 3.5+、Opera 10.6+、Safari 5+、Chrome、iOS Safari 和 Android WebKit 支持地理定位。有关良好的地理定位示例，请参阅 [`html5demos.com/geo`](http://html5demos.com/geo)。

# File API

Web 应用的一个主要痛点一直是无法与用户计算机上的文件进行交互。在 2000 年以前，处理文件的唯一方法是在表单中放置 `<input type="file">` 并仅限于此。File API 的设计旨在让 Web 开发人员以安全的方式访问客户端计算机上的文件，从而与这些文件进行更好的交互。File API 支持 Internet Explorer 10+、Firefox 4+、Safari 5.0.5+、Opera 11.1+ 和 Chrome。

File API 仍然基于表单中的文件输入字段，但增加了直接访问文件信息的能力。HTML5 为文件输入元素向 DOM 添加了 `files` 集合。当在字段中选择一个或多个文件时，`files` 集合包含一组代表每个文件的 `File` 对象。每个 `File` 对象都有几个只读属性，包括：

- `name` — 本地系统上的文件文件名。
- `size` — 以字节为单位的文件大小。
- `type` — 文件的 MIME 类型字符串。
- `lastModified` — 代表文件最后修改时间的字符串。该属性仅在 Chrome 中实现。

例如，你可以通过监听变化事件获取每个文件的信息：

![image](img/logo1.gif)

```javascript
var filesList = document.getElementById("files-list");

EventUtil.addHandler(filesList, "change", function(event){

    var files = EventUtil.getTarget(event).files,

        i = 0,

        len = files.length;

    while (i < len){

        console.log(files[i].name + " (" + files[i].type + ", " + files[i].size + " bytes)");

        i++;

    }

});
```

`FileAPI01.htm`

此示例简单向控制台输出每个文件的信息。这种能力本身是 Web 应用的一大进步，但 File API 通过 `FileReader` 类型允许实际读取文件数据。

## FileReader 类型

`FileReader` 类型代表一种异步文件读取机制。你可以将 `FileReader` 认为类似于 `XMLHttpRequest`，只不过它是从文件系统读取文件，而不是从服务器读取数据。`FileReader` 类型提供了多种读取文件数据的方法：

- `readAsText(file, encoding)` — 将文件作为文本读取并将文本存储在 `result` 属性中。第二个参数编码类型是可选的。
- `readAsDataURL(file)` — 读取文件并将代表文件的数据 URI 存储在 `result` 属性中。
- `readAsBinaryString(file)` — 读取文件并将每个字符代表一个字节的字符串存储在 `result` 属性中。
- `readAsArrayBuffer(file)` — 读取文件并将包含文件内容的 `ArrayBuffer` 存储在 `result` 属性中。

这些不同的读取文件方式为处理文件数据提供了最大的灵活性。例如，你可能希望将图像读取为数据 URI 以显示给用户，或者你可能希望将文件读取为文本以便解析。

由于读取是异步进行的，每个 `FileReader` 发布多个事件。三个最有用的事件是 `progress`、`error` 和 `load`，分别表示更多数据可用、发生了错误以及文件已完全读取。

`progress` 事件大约每 50ms 触发一次，提供的信息与 XHR 进度事件相同：`lengthComputable`、`loaded` 和 `total`。此外，在进度事件期间，`FileReader` 的 `result` 属性是可以读取的，尽管它可能尚未包含所有数据。

如果由于某些原因无法读取文件，会触发 `error` 事件。当 `error` 事件触发时，`FileReader` 的 `error` 属性会被填充。该对象有一个属性 `code`，其错误代码为 `1`（未找到文件）、`2`（安全错误）、`3`（读取已中止）、`4`（文件不可读）或 `5`（编码错误）。

`load` 事件在文件成功加载时触发；如果已经触发了 `error` 事件，则它将不会触发。这是一个使用所有三个事件的示例：

![image](img/logo1.gif)

```javascript
var filesList = document.getElementById("files-list");

EventUtil.addHandler(filesList, "change", function(event){

    var info = "",

        output = document.getElementById("output"),

        progress = document.getElementById("progress"),

        files = EventUtil.getTarget(event).files,

        type = "default",

        reader = new FileReader();

    if (/image/.test(files[0].type)){

        reader.readAsDataURL(files[0]);

        type = "image";

    } else {

        reader.readAsText(files[0]);

        type = "text";

    }

    reader.onerror = function(){

        output.innerHTML = "Could not read file, error code is " + 

                           reader.error.code;

    };

    reader.onprogress = function(event){

        if (event.lengthComputable){

            progress.innerHTML = event.loaded + "/" + event.total;

        }

    };

    reader.onload = function(){

        var html = "";

        switch(type){

            case "image":

                html = "<img src=\"" + reader.result + "\">";

                break;

            case "text":

                html = reader.result;

                break;

        }

        output.innerHTML = html;

    };

});
```

`FileAPIExample02.htm`

此代码从表单字段中读取文件并显示在页面上。如果文件的 MIME 类型指示它是图像，则会请求一个数据 URI，并在加载后将此数据 URI 作为图像插入到页面中。如果文件不是图像，则它被读取为字符串并原样输出到页面中。`progress` 事件用于跟踪和显示正在读取的字节数据，而 `error` 事件则监控任何错误。

你可以通过调用 `abort()` 方法来停止正在进行的读取，在这种情况下会触发一个 `abort` 事件。在触发 `load`、`error` 或 `abort` 之后，会触发一个名为 `loadend` 的事件。`loadend` 事件表示由于上述三个原因之一，所有读取工作都已完成。

`readAsText()` 和 `readAsDataURL()` 方法在所有实现的浏览器中都受支持。Internet Explorer 10 PR2 没有实现 `readAsBinaryString()` 或 `readAsArrayBuffer()`。

### 部分读取

在某些情况下，你可能只想读取文件的部分内容而不是整个文件。为此，`File` 对象有一个名为 `slice()` 的方法，它在 Firefox 中实现为 `mozSlice()`，在 Chrome 中实现为 `webkitSlice()`；Safari 从 5.1 版本起没有实现此方法。`slice()` 方法接受两个参数：起始字节和要读取的字节数。该方法返回一个 `Blob` 实例，`Blob` 实际上是 `File` 的超类型。以下函数在不同的实现之间统一了 `slice()` 的行为：

![image](img/logo1.gif)

```javascript
function blobSlice(blob, startByte, length){

    if (blob.slice){

        return blob.slice(startByte, length);

    } else if (blob.webkitSlice){

        return blob.webkitSlice(startByte, length);

    } else if (blob.mozSlice){

        return blob.mozSlice(startByte, length);

    } else {

        return null;

    }

}
```

`FileAPIExample03.htm`

`Blob` 也有 `size` 和 `type` 属性，以及用于进一步切割数据的 `slice()` 方法。你也可以使用 `FileReader` 从 `Blob` 中读取。此示例仅从文件中读取前 32 字节：

![image](img/logo1.gif)

```javascript
var filesList = document.getElementById("files-list");

EventUtil.addHandler(filesList, "change", function(event){

    var info = "",

        output = document.getElementById("output"),

        progress = document.getElementById("progress"),

        files = EventUtil.getTarget(event).files,

        reader = new FileReader(),

        blob = blobSlice(files[0], 0, 32);

    if (blob){

        reader.readAsText(blob);

        reader.onerror = function(){

            output.innerHTML = "Could not read file, error code is " + 

                               reader.error.code;

        };

        reader.onload = function(){

            output.innerHTML = reader.result;

        };

    } else {

        alert("Your browser doesn't support slice().");

    }

});
```

读取文件的部分内容可以节省时间，尤其是当你只需要查看文件的头部时。

### 对象 URL

对象 URL（有时称为 blob URL）是引用内存中数据的 URL。对象 URL 的优势在于你不需要将文件内容读取到 JavaScript 中即可使用它们。为了创建对象 URL，使用 `URL.createObjectURL()` 方法并传入 `File` 或 `Blob` 对象。Chrome 将其实现为 `webkitObjectURL()`，因此以下函数可以统一这种行为：

```javascript
function createObjectURL(blob){

    if (window.URL){

        return window.URL.createObjectURL(blob);

    } else if (window.webkitURL){

        return window.webkitObjectURL(blob);

    } else {

        return null;

    }

}
```

该函数的返回值指向内存地址的字符串。由于该字符串是一个 URL，它可以在 DOM 中使用。例如，以下代码显示了一个图像：

![image](img/logo1.gif)



`var filesList = document.getElementById("files-list");`

`EventUtil.addHandler(filesList, "change", function(event){`

```
    var info = "",

        output = document.getElementById("output"),

        progress = document.getElementById("progress"),

        files = EventUtil.getTarget(event).files,

        reader = new FileReader(),

        url = createObjectURL(files[0]);

    if (url){

        if (/image/.test(files[0].type)){

            output.innerHTML = "<img src=\"" + url + "\">";

        } else {

            output.innerHTML = "Not an image.";

        }

    } else {

        output.innerHTML = "Your browser doesn't support object URLs.";

    }

});
```

`FileAPIExample04.htm`

一旦数据不再需要，最好释放与之相关的内存。只要对象 URL 仍在在使用，内存就无法释放。你可以通过将其传递给 `window.URL.revokeObjectURL()`（Chrome 中为 `window.webkitURL.revokeObjectURL()`）来指示该 URL 不再需要。为了处理两种实现，使用此函数：

```javascript
function revokeObjectURL(url){

    if (window.URL){

        window.URL.revokeObjectURL(url);

    } else if (window.webkitURL){

        window.webkitURL.revokeObjectURL(url);

    }

}
```

所有对象 URL 都会页面卸载时自动从内存中释放。尽管如此，最好在不再需要时释放每个对象 URL，以确保页面的内存占用尽可能低。

对象 URL 支持 Internet Explorer 10+、Firefox 4+ 和 Chrome。

## 拖拽读取文件

将 HTML5 拖放 API 与 File API 结合，允许为读取文件信息创建有趣的界面。在页面上创建一个自定义投放目标后，你可以从桌面拖放文件并将其释放到投放目标上。这会触发 `drop` 事件，就像拖放图像或链接一样。被拖放的文件可以通过 `event.dataTransfer.files` 获取，这是一个 `File` 对象的列表，与文件输入字段中提供的对象相同。

以下示例打印了释放到页面上自定义投放目标上的文件信息：

![image](img/logo1.gif)

```
var droptarget = document.getElementById("droptarget");

function handleEvent(event){

    var info = "",

        output = document.getElementById("output"),

        files, i, len;            

    EventUtil.preventDefault(event);

    if (event.type == "drop"){

        files = event.dataTransfer.files;

        i = 0;

        len = files.length;

        while (i < len){

            info += files[i].name + " (" + files[i].type + ", " + files[i].size + 

                    " bytes)<br>";

            i++;

        }

        output.innerHTML = info;

    }

}

EventUtil.addHandler(droptarget, "dragenter", handleEvent);

EventUtil.addHandler(droptarget, "dragover", handleEvent);

EventUtil.addHandler(droptarget, "drop", handleEvent); 
```

`FileAPIExample05.htm`

与早期的拖放示例一样，你必须取消 `dragenter`、`dragover` 和 `drop` 的默认行为。在 `drop` 事件期间，文件将通过 `event.dataTransfer.files` 可用，你此时可以读取它们的信息。利用此功能最流行的方法之一是在使用 `XMLHttpRequest` 的拖放文件上传系统中。

## 使用 XHR 进行文件上传

由于 File API 允许你访问文件内容，可以推导出你可以使用 `XHR` 直接将文件上传到服务器。当然，你可以通过将数据传递给 `send()` 方法并使用 `POST` 请求来轻松地上传文件内容。但是，这样你传递的是文件的内容，你需要在服务器上获取这些内容并将其保存到另一个文件中。理想情况下，你希望像表单提交一样上传文件。

使用第 21 章首次引入的 `FormData` 类型可以非常容易地实现。创建一个新的 `FormData` 对象，并将任何 `File` 对象作为值传递给 `append()` 方法。然后，将 `FormData` 对象传递给 `XHR send()` 方法，你就成功地模拟了使用表单上传文件：

![image](img/logo1.gif)

```
var droptarget = document.getElementById("droptarget");

function handleEvent(event){

    var info = "",

        output = document.getElementById("output"),

        data, xhr,

        files, i, len;            

    EventUtil.preventDefault(event);

    if (event.type == "drop"){

        data = new FormData();

        files = event.dataTransfer.files;

        i = 0;

        len = files.length;

        while (i < len){

            data.append("file" + i, files[i]);

            i++;

        }

        xhr = new XMLHttpRequest();

        xhr.open("post", "FileAPIExample06Upload.php", true);

        xhr.onreadystatechange = function(){

            if (xhr.readyState == 4){

                alert(xhr.responseText);

            }

        };

        xhr.send(data);

    }

}

EventUtil.addHandler(droptarget, "dragenter", handleEvent);

EventUtil.addHandler(droptarget, "dragover", handleEvent);

EventUtil.addHandler(droptarget, "drop", handleEvent); 
```

`FileAPIExample06.htm`

此示例创建了一个带有每个文件键的 `FormData` 对象，例如 `file0`、`file1`、`file2`。注意，指定文件作为表单值不需要额外的处理。不需要使用 `FileReader`，只需传递 `File` 对象本身。

使用 `FormData` 上传文件可以确保服务器上的处理方式就像处理普通表单一样。这意味着像 PHP `$_FILES` 数组这样的实用方法在服务器上仍然可用用于上传文件。Firefox 4+、Safari 5+ 和 Chrome 都支持 `FormData` 以及这种文件上传方式。

## 计时（WEB TIMING）

页面性能一直是 Web 开发者关注的领域。直到最近，测量页面性能特性的唯一方法是通过日益复杂且巧妙地使用 JavaScript `Date` 对象。Web Timing API 通过 JavaScript API 暴露浏览器内部指标改变了这一点，允许开发者直接访问这些信息并随心所欲地使用。与本章中的其他 API 不同，Web Timing 实际上已经是 W3C 推荐，尽管浏览器对其采纳速度较慢。

Web Timing 的核心是 `window.performance` 对象。与页面相关的所有指标（包括已定义的和未来的）都存在此对象上。Web Timing 规范从定义 `performance` 的两个属性开始。

`performance.navigation` 属性是一个包含多个与页面导航相关的属性的对象。属性有：

*   `redirectCount` — 页面加载之前的重定向次数。
*   `type` — 刚刚发生的导航类型的数字常量：
    *   `performance.navigation.TYPE_NAVIGATE` (0) — 页面首次加载。
    *   `performance.navigation.TYPE_RELOAD` (1) — 页面重新加载。
    *   `performance.navigation.TYPE_BACK_FORWARD` (2) — 使用后退或前进按钮导航到页面。

另一方面，`performance.timing` 属性提供了许多仅仅是时间戳（自 epoch 以来来的毫秒数）的属性，表示各种事件发生的时间。属性有：

*   `navigationStart` — 开始导航到页面的时间。
*   `unloadEventStart` — 上一个页面卸载事件开始的时间。只有当上一个页面同源时才会填充；否则为 0。
*   `unloadEventEnd` — 上一个页面卸载事件完成的时间。只有当上一个页面同源时才会填充；否则为 0。
*   `redirectStart` — 当前页面开始重定向的时间，但仅当重定向发生在源内时。否则此值为 0。
*   `redirectEnd` — 当前页面重定向结束的时间，但仅当重定向发生在源内时。否则此值为 0。
*   `fetchStart` — 通过 HTTP 获取页面。
*   `domainLookupStart` — 页面 DNS 查询开始。
*   `domainLookupEnd` — 页面 DNS 查询结束。
*   `connectStart` — 浏览器尝试连接服务器。
*   `connectEnd` — 浏览器成功连接到服务器。
*   `secureConnectionStart` — 从浏览器尝试 SSL 连接。当未使用 SSL 时，此值为 0。
*   `requestStart` — 浏览器请求页面。
*   `responseStart` — 浏览器接收到页面第一个字节。
*   `responseEnd` — 浏览器接收到整个页面。
*   `domLoading` — `document.readyState` 变为“loading”。
*   `domInteractive` — `document.readyState` 变为“interactive”。
*   `domContentLoadedEventStart` — `DOMContentLoaded` 事件即将触发。
*   `domContentLoadedEventEnd` — `DOMContentLoaded` 事件已触发并执行所有事件处理程序。
*   `domComplete` — `document.readyState` 变为“complete”。
*   `loadEventStart` — `load` 事件即将触发。
*   `loadEventEnd` — `load` 事件已触发并执行所有事件处理程序。

使用各种时间之间的差值可以让你很好了解页面是如何加载到浏览器的，以及潜在的瓶颈隐藏在哪里。关于 Web Timing API 的优秀示例，请访问 [`webtimingdemo.appspot.com/`](http://webtimingdemo.appspot.com/)。

Web Timing API 在 Internet Explorer 10+ 和 Chrome 中受支持。

# WEB WORKERS

随着 Web 应用程序的复杂性不断增加，对复杂计算的需求也随之增长。长时间运行的 JavaScript 进程会导致浏览器结用户界面，用户可能会体验到屏幕“卡死”。Web Workers 通过在后台执行 JavaScript 解决了这个问题。浏览器可以选择以多种方式实现 Web Workers，包括线程、后台进程以及在其他处理器核心上运行的进程。实际的实现细节并不如在负面影响用户界面的情况下运行 JavaScript 的自由那样重要。

Web Workers 目前支持 Internet Explorer 10+、Firefox 3.5+、Safari 4+、Opera 10.6+、Chrome 以及 iOS 版 Safari 5。

## 使用 Worker

你可以通过实例化一个 `Worker` 对象并传递包含 worker 应执行的 JavaScript 的文件名来创建一个新的 Web Worker。例如：

```
var worker = new Worker("stufftodo.js");
```

这行代码会导致浏览器下载 `stufftodo.js`，但在 worker 接收到消息之前它实际上不会启动。你使用 `postMessage()` 方法向 worker 传递消息（类似于 XDM）：

```
worker.postMessage("start!");
```

消息可以是任何可序列化的值，尽管与 XDM 不同，所有支持的浏览器都接受 `postMessage()` 的对象参数（Safari 4 是最后一个支持 Web Workers 的浏览器，且仅支持字符串消息）。因此，你可以自由地以任何类型的对象形式传递数据，如下例所示：

```
worker.postMessage({

    type: "command",

    message: "start!"

});
```

通常情况下，任何可以序列化为 JSON 结构的数值都可以通过 `postMessage()` 传递。这意味着与 XDM 一样，值被复制到 workers 中，而不是直接传递。

worker 通过两个事件与页面进行通信：`message` 和 `error`。`message` 事件的行为与 XDM 相同，来自 worker 的数据通过 `event.data` 到达。此数据也可以是任何类型的可序列化值：

```
worker.onmessage = function(event){

    var data = event.data;

    //对数据进行某些操作

}
```

`error` 事件是 worker 表明无法完成给定任务的方式。当 worker 内部执行 JavaScript 发生错误时，就会触发该事件。`error` 事件的 `event` 对象有三个属性：`filename`，错误发生的文件名；`lineno`，该文件中错误所在的行号；以及 `message`，完整的错误信息。

```
worker.onerror = function(event){

    console.log("ERROR: " + event.filename + " (" + event.lineno + "): " + 

                event.message);

};
```

始终为 Web Workers 提供一个 `onerror` 事件处理器是一个好习惯，即使它除了记录错误外什么都不做。否则，当发生错误时，workers 将静默失败。

你可以在任何时间通过调用 `terminate()` 方法完全停止 worker。这意味着 worker 将立即停止，不会完成任何剩余的处理（不会触发错误和消息事件）。

```
worker.terminate();   //立即停止 worker
```



## Worker 全局作用域（Worker Global Scope）

理解 Web Worker 最重要的一点是，它的 JavaScript 是在与网页代码完全不同的作用域中执行的。Web Worker 内部有不同的全局对象以及不同的对象和方法。在 Web Worker 内部，无法访问 DOM，实际上无法以任何方式影响页面的外观。

Web Worker 内部的全局对象是 worker 对象本身。这意味着在全局作用域中访问 `this` 或 `self` 将导致访问工作对象。worker 内部还有一个极简的环境来允许其处理数据：

- 一个极简的 `navigator` 对象，包含 `onLine`、`appName`、`appVersion`、`userAgent` 和 `platform` 属性。
- 一个只读的 `location` 对象。
- `setTimeout()`、`setInterval()`、`clearTimeout()` 和 `clearInterval()`。
- `XMLHttpRequest` 构造函数。

可以看出，与页面环境相比，worker 的环境是非常有限的。

当页面对 worker 调用 `postMessage()` 时，该数据将异步传输到 worker，并导致 worker 内部触发 `message` 事件。因此，为了响应从页面发送的数据，你必须创建一个 `onmessage` 事件处理器：

```javascript
// worker 内部代码

self.onmessage = function(event) {
    var data = event.data;

    // 对数据进行某些操作
};
```

请记住，此示例中的 `self` 实际上是 worker 全局作用域内 worker 的引用（与页面内部的 `Worker` 实例是不同的对象）。一旦 worker 完成处理，也可以通过调用 `postMessage()` 将数据传回页面。例如，以下假设传入了一个数字数组并需要对其排序。然后将排序后的数组传回页面：

![image](img/logo1.gif)

```javascript
// worker 内部代码

self.onmessage = function(event) {
    var data = event.data;

    // 记住，默认情况下 sort() 执行的是字符串比较

    data.sort(function(a, b) {
        return a - b;
    });

    self.postMessage(data);
};
```

### WebWorkerExample01.js

数据的往来消息传递是页面与 worker 通信的方式。在 worker 内部调用 `postMessage()` 会在 `Worker` 实例上触发异步消息事件。如果页面想使用此 worker，其方式如下：

```javascript
// 页面中

var data = [23, 4, 7, 9, 2, 14, 6, 65, 87, 41],
    worker = new Worker("WebWorkerExample01.js");

worker.onmessage = function(event) {
    var data = event.data;

    // 对数组进行某些操作
};

// 将数组发送到 worker 进行排序

worker.postMessage(data);
```

### WebWorkerExample01.htm

排序正是有用卸载到 worker 中的耗时操作，以免阻塞用户界面。其他示例还有图像处理（例如将图像转换为灰度）以及加密操作。

worker 也可以通过调用 `close()` 方法随时完全停止自身。这与从页面调用的 `terminate()` 方法类似，区别在于不再触发后续事件：

```javascript
// worker 内部代码

self.close();
```

## 引入其他脚本

由于无法动态创建 `<script>` 元素，似乎无法向 worker 添加新脚本。幸运的是，worker 全局作用域考虑到了这一点并提供了一个 `importScripts()` 方法。该方法接受一个或多个加载 JavaScript 的 URL。所有加载都是同步进行的，因此在 `importScripts()` 之后的代码直到所有脚本都已加载并执行。例如：

```javascript
// worker 内部代码

importScripts("file1.js", "file2.js");
```

即使 `file2.js` 可能比 `file1.js` 先完成下载，它们也将按照指定的顺序执行。脚本在 worker 全局作用域中执行，因此如果它们使用了页面特定的 JavaScript，那么它们可能无法在 worker 中运行。通常，worker 代码是高度专门化的代码，而不是与页面共享的内容。

## Web Workers 的未来

Web Workers 规范仍有大量工作在进行。本节讨论的 worker 现在被称为“专用 worker”（dedicated workers），因为它们专门用于特定页面且不能共享。规范引入了“共享 worker”（shared workers）的概念，单个 worker 可以被浏览器中多个标签页中打开的相同页面共享。虽然 Safari 5、Chrome 和 Opera 10.6 支持共享 worker，但规范尚未最终定稿，可能会或不会发生变化。

关于 workers 内部应该和不应该访问内容的争论仍在继续。有些人认为，workers 应该能够访问页面所在的所有数据存储，这意味着 workers 不仅应该访问 `XHR`，还可以访问 `localStorage`、`sessionStorage`、`Indexed DB`、`Web Sockets`、`Server-Sent Events` 等。这一方向似乎得到了大量的支持，因此可能会进行一些更改以允许在 worker 全局作用范围内使用更多内容。

## 总结

除了 HTML5 外，还有一组 JavaScript API，虽然这些 API 在技术上并不属于规范的一部分，但通常被归类为 HTML5 JavaScript API。其中许多 API 仍处于定义中，但它们已经获得了跨浏览器支持，因此现在就值得讨论了。

- `requestAnimationFrame()` 试图通过信号通知动画何时运行来优化基于 JavaScript 的动画。这允许浏览器优化屏幕重绘。
- `Page Visibility API` 让你能够了解用户何时查看页面以及页面何时从视图中隐藏。
- `Geolocation API` 是一种在获得许可的情况下确定用户位置的方法。此功能在移动 Web 应用中非常流行。
- `File API` 允许 JavaScript 从文件中读取数据，以显示、处理或上传这些文件。结合 HTML5 的拖放功能，你可以轻松创建拖放文件上传。
- `Web Timing` 为你提供了有关页面加载和渲染时间的宝贵性能洞察。
- `Web Workers` 允许你运行不会阻塞用户界面的异步 JavaScript。这对于复杂的计算和数据处理非常有用，否则这些操作将占用大量时间并干扰用户使用页面的能力。

# ECMAScript Harmony

随着 2004 年以来人们对 Web 开发兴趣的增加，浏览器厂商和其他利益相关方开始关于 JavaScript 应该如何演变的讨论。`ECMA-262` 第四版的工作主要基于两个竞争性的提案开始：一个针对 Netscape 的 `JavaScript 2.0`，另一个针对微软的 `JScript.NET`。各方并没有在浏览器领域竞争，而是汇回到 `ECMA` 以敲定一个基于 JavaScript 的新语言提案。最初，工作是针对名为 `ECMAScript 4` 的提案开始的，在很长一段时间内，这似乎是 JavaScript 的下一个进化步骤。当后来引入一个名为 `ECMAScript 3.1` 的反向提案时，JavaScript 的未来变得扑朔不定。经过大量讨论后，确定 `ECMAScript 3.1` 将是 JavaScript 的下一步，并将进行一项代号为 `Harmony` 的进一步努力，将 `ECMAScript 4` 的某些特性整合到 `ECMAScript 3.1` 中。

`ECMAScript 3.1` 最终被重命名为 `ECMAScript 5` 并迅速标准化。`ECMAScript 5` 的细节已贯穿本书。一旦 `ECMAScript 5` 确定，`Harmony` 的工作立即开始。`Harmony` 试图保持 `ECMAScript 5` 的精神，进行更多增量式的更改而不是激进的语言变更。虽然到 2011 年 `Harmony`（即 `ECMAScript 6`）的细节仍在开发中，但规范的几个部分已经完成。本附录涵盖了 `Harmony` 中肯定会进入最终规范的部分，但请注意，最终实现的细节可能与此处呈现的内容不同。

## 通用更改

`Harmony` 为 `ECMAScript` 引入了若干项基础更改。这些不是语言的重大变化，而是填补了某些功能上一些奇特的遗留漏洞。

### 常量

JavaScript 的一个明显弱点是缺乏正式的常量。为了纠正这一点，开发者作为 `Harmony` 的一部分通过 `const` 关键字添加了常量。`const` 声明的使用方式类似于 `var`，它允许你定义一个一旦初始化就无法更改其值的变量。以下是用法示例：

```javascript
const MAX_SIZE = 25;
```

常量可以定义在任何可以定义变量的地方。常量名不能与同一作用域内声明的变量或函数名相同，因此以下会导致错误：

```javascript
const FLAG = true;

var FLAG = false; // error!
```

除了具有不可变的值外，常量可以像任何其他变量一样使用。任何更改值的尝试都会被直接忽略，所示：

```javascript
const FLAG = true;

FLAG = false;

alert(FLAG); // true
```

Firefox、Safari 3+、Opera 9+ 和 Chrome 均支持常量。在 Safari 和 Opera 中，`const` 的作用就像 `var` 一样，值仍然可以更改。

### 块级作用域和其他作用域

书中不断提醒的一点之一是，JavaScript 没有块级作用域的概念。这意味着定义在语句块内部的变量表现就像定义在包含它的函数中一样。`Harmony` 通过引入 `let` 关键字引入了块级作用域的概念。

与 `const` 和 `var` 类似，`let` 声明可以在任何点定义变量并初始化其值。区别在于，一旦 `let` 定义的变量执行移动到其定义块之外，它就会消失。例如，使用以下结构是非常常见的：

```javascript
for (var i = 0; i < 10; i++) {
    // 做一些事情
}

alert(i); // 10
```

当代码中声明变量 `i` 时，它被声明为代码所在函数的局部变量。这意味着该变量在代码所在的函数结束之前都是有效的。而使用 `let` 定义的变量，一旦执行移动到定义其所在的块之外，它就会消失。如果使用 `let` 替换 `var`，考虑以下：

```javascript
for (let i = 0; i < 10; i++) {
    // 做一些事情
}

alert(i); // i 是未定义的错误
```

```javascript
for (let i = 0; i < 10; i++) {
    // 做一些事情
}

alert(i); // 10
```

`let` 还有其他使用方式。你可以创建一个 `let` 语句，专门定义要在后续代码块使用的变量，如下所示：

```javascript
var num = 5;

let (num = 10, multiplier = 2) {
    alert(num * multiplier); // 20
}

alert(num); // 5
```

在此代码中，`let` 语句定义了一个区域，在该区域内 `num` 变量等于 10，`multiplier` 变量等于 2。这种对 `num` 的定义覆盖了之前使用 `var` 定义的值，因此在 `let` 语句内部，乘以乘数的结果是 20。在 `let` 语句之外，`num` 的值保持为 5。由于每个 `let` 语句都会创建自己的作用域，内部的变量值对外部没有影响。

你还可以使用类似的语法创建一个 `let` 表达式，其中变量值仅针对单个表达式设置。示例所示：

```javascript
var result = let (num = 10, multiplier = 2) num * multiplier;

alert(result); // 20
```

在这里，使用 `let` 表达式通过两个变量计算一个值。然后该值存储在 `result` 变量中。此之后，变量 `num` 和 `multiplier` 不再存在。

在 JavaScript 中使用块级作用域可以让你更有效地控制变量在代码执行过程中的何时存在。

## 函数

大部分代码都是函数中编写的，因此 `Harmony` 专注于改进函数并使其更易于使用。与 `Harmony` 的其他部分一样，这些更改关注于开发者和实现者的痛点。

### 剩余参数与展开参数

在 Harmony 中，`arguments` 对象已不再存在；你完全无法在其中访问未声明的参数。然而，有一种方法通过使用剩余参数（rest arguments）来指示你期望传入数量的参数。剩余参数用三个点后跟一个标识符来表示。这允许你定义已知将传入的参数，然后将剩余部分收集到一个数组中。这是一个示例：

```javascript
function sum(num1, num2, ...nums) {
    var result = num1 + num2;

    for (let i = 0, len = nums.length; i < len; i++) {
        result += nums[i];
    }

    return result;
}

var result = sum(1, 2, 3, 4, 5, 6);
```

这段代码定义了一个至少接受两个参数的 `sum()` 方法。它可以接受额外的参数，并且所有剩余参数都存储在 `nums` 数组中。与 `arguments` 对象不同，剩余参数存储在 `Array` 的实例中，因此可以使用所有的数组方法。即使没有向函数传递剩余参数，剩余参数对象始终是 `Array` 的实例。

与剩余参数密切相关的是展开参数（spread arguments）。展开参数允许你传入一个数组，并将每个项目映射到函数中的某个特定参数。展开参数的表示法与剩余参数相同，在值前面加上三个点。唯一的区别是，展开参数发生在函数被调用时，而剩余参数是在函数定义时使用的。例如，与其向 `sum()` 方法传递单个数字，你也可以像这里这样使用展开参数：

```javascript
var result = sum(...[1, 2, 3, 4, 5, 6]);
```

在这段代码中，参数数组作为展开参数传递给 `sum()`。这个示例在功能上等于以下代码：

```javascript
var result = sum.apply(this, [1, 2, 3, 4, 5, 6]);
```

### 默认参数值

ECMAScript 函数中的所有参数都被认为是可选的，因为程序没有对传入的参数数量进行任何检查。然而，你不需要手动检查提供了哪些参数，而是可以为参数指定默认值。如果没有正式传递参数，它们将获得给定的值。

要为参数指定默认值，只需在参数定义后添加等号和默认值，如下例所示：

```javascript
function sum(num1, num2 = 0) {
    return num1 + num2;
}

var result1 = sum(5);
var result2 = sum(5, 5);
```

`sum()` 函数接受两个参数，但第二个参数是可选的，并获得默认值 `0`。可选参数的优点在于，它让你无需再检查是否传递了值以及使用特殊值；所有这些都由系统为你完成。

### 生成器（Generators）

生成器是一个逐个生成值序列的对象。在 Harmony 中，你可以通过定义一个使用 `yield` 操作符返回特定值的函数来创建一个生成器。当调用使用 `yield` 的函数时，会创建并返回一个新的 `Generator` 实例。然后可以调用 `next()` 方法来获取生成器的第一个值。当发生时，原始函数将执行，并在遇到 `yield` 时停止执行，返回指定的值。通过这种方式，`yield` 的工作方式类似于 `return`。如果再次调用 `next()`，代码执行将从 `yield` 之后的下一个语句继续，然后一直运行直到再次遇到 `yield`，此时会返回一个新值。这是一个示例：

```javascript
function myNumbers() {
    for (var i = 0; i < 10; i++) {
        yield i * 2;
    }
}

var generator = myNumbers();

try {
    while (true) {
        document.write(generator.next() + "<br />");
    }
} catch (ex) {
    // 刻意留空
} finally {
    generator.close();
}
```



当调用函数`myNumbers()`时，会返回一个生成器。`myNumbers()`函数本身非常简单，包含一个`for`循环，每次循环都会`yield`一个值。每次调用`next()`都会导致`for`循环循环并返回下一个值。第一个值是`0`，第二个是`2`，第三个是`4`，依此类推。当`myNumbers()`在没有调用`yield`的情况下完成（最后一次循环之后），调用`next()`会抛出`StopIteration`错误。因此，为了输出生成器中的所有数字，将`while`循环封装在`try-catch`语句中，以防止错误停止代码执行。

如果不再需要生成器，最好调用`close()`方法。这样做可以确保原始函数的其余部分被执行，包括与`try-catch`语句相关的任何`finally`块。

当需要产生值序列且每个后续值都与前一个值有某种关联时，生成器是非常有用的。

### 数组及其他结构

Harmony 的另一个关注领域是数组。数组是 JavaScript 中最常用的数据结构之一，创建更直观、更强大的处理数组的方法是该语言的优先事项。

#### 迭代器（Iterators）

迭代器是一个遍历值序列并逐个返回它们的对象。当你使用`for`循环时，你通常是在遍历值并逐个处理它们。迭代器提供了在不使用循环的情况下实现此功能的能力。Harmony 支持所有类型的迭代器。

为对象创建迭代器，使用`Iterator`构造函数并传入该对象。`next()`方法用于检索序列中的下一个值。默认情况下，此方法返回一个数组，其第一个项目是索引（对于数组）或属性名（对于对象），当没有更多可用值时，`next()`会抛出`StopIteration`错误。这是一个示例：

```javascript
var person = {
    name: "Nicholas",
    age: 29
};
var iterator = new Iterator(person);

try {
    while(true){
        let value = iterator.next();
        document.write(value.join(":") + "<br />");
    }
} catch(ex){
```

这段代码为`person`对象创建迭代器。第一次调用`next()`时，返回数组`["name", "Nicholas"]`，第二次调用返回`["age", 29]`。这段代码的输出是：

```text
name:Nicholas
age:29
```

为数组创建的迭代器以类似的方式运行，遍历数组中的每个位置，如下：

```javascript
var colors = ["red", "green", "blue"];
var iterator = new Iterator(colors);

try {
    while(true){
        let value = iterator.next();
        document.write(value.join(":") + "<br />");
    }
} catch(ex){

}
```

这段代码的输出是：

```text
0:red
1:green
2:blue
```

通过在向`Iterator`构造函数传递第二个参数`true`，可以强制`next()`只返回属性名或索引，而不是包含索引和值的数组，如下：

```javascript
var iterator = new Iterator(colors, true);
```

传递第二个参数后，每次调用`next()`将只返回值的索引，而不是一个包含索引和值的数组。

![image](img/pen.gif)

通过定义特殊方法`__iterator__()`可以为自定义类型创建自己的迭代器，该方法必须返回一个具有`next()`方法的对象。当自定义类型的实例作为参数传递给`Iterator`构造函数时，将调用此方法。

#### 数组推导（Array Comprehensions）

数组推导是一种根据特定标准初始化数组的方法，这一特性在 Harmony 中引入，是 Python 中流行的语言结构。JavaScript 中数组推导的基本形式如下：

```javascript
array = [ value for each (variable in values) condition ];
```

`value`是要包含在最终数组中的实际值。该值基于`values`数组中的所有值。`for each`结构会遍历`values`中的每个值并将该值存储在`variable`中。如果满足可选的`condition`，则将`value`添加到结果数组。以下是一个示例：

```javascript
//original array
var numbers = [0,1,2,3,4,5,6,7,8,9,10];

//将所有项复制到新数组中
var duplicate = [i for each (i in numbers)];

// 仅获取偶数
var evens = [i for each (i in numbers) if (i % 2 == 0)];

// 将每个值乘以 2
var doubled = [i*2 for each (i in numbers)];

// 将每个奇数乘以 3
var tripledOdds = [i*3 for each (i in numbers) if (i % 2 > 0)];
```

此代码中的所有数组推导式都使用`i`作为遍历`numbers`中所有值的变量。其中一些使用条件来过滤数组结果。本质上，如果`condition`求值为`true`，则将`value`添加到数组。这种语法与传统的 JavaScript 语法略有不同，但比编写`for`循环来完成相同任务要简洁得多。Firefox（2 及更高版本）是唯一实现此功能的浏览器，它要求将`<script>`元素的`type`属性设置为`"application/javascript;version=1.7"`才能启用它。

![image](img/pen.gif)

数组推导式中的`values`部分也可以是一个生成器（generator）或迭代器（iterator）。

### 解构赋值

从一组值中提取一个或多个值到单独的变量中是非常常见的操作。考虑从迭代器的`next()`方法返回的值，它是一个包含属性名和值的数组。为了将每个值存储在它们自己的变量中，需要两条语句，如下例所示：

```javascript
var nextValue = ["color", "red"];
var name = nextValue[0];
var value = nextValue[1];
```

解构赋值允许你使用单个语句（如所示）将两个数组项都分配给变量：

```javascript
var [name, value] = ["color", "red"];
alert(name);     //"color"
alert(value);    //"red"
```

在传统的 JavaScript 语法中，数组字面量不能位于赋值的左侧。解构赋值引入了这种语法，表示等号左侧数组中的变量应该被赋值等号右侧数组包含的值。结果是`name`被填充为`"color"`，`value`被填充为`"red"`。

如果你不需要所有的值，可以只为你需要的值提供变量，如下例：

```javascript
var [, value] = ["color", "red"];
alert(value);    //"red"
```

在这里，只有变量`value`被分配了值，它接收了值`"red"`。

你可以以创新的方式使用解构赋值，例如交换两个变量的值。在 ECMAScript 3 中，交换两个变量的值通常如下：

```javascript
var value1 = 5;
var value2 = 10;

var temp = value1;
value1 = value2;
value2 = temp;
```

你可以通过使用解构数组赋值来消除对`temp`变量的需求，如下例：

```javascript
var value1 = 5;
var value2 = 10;

[value2, value1] = [value1, value2];
```

解构赋值也可以通过对象完成，如下：

```javascript
var person = {
    name: "Nicholas",
    age: 29
};

var { name: personName, age: personAge } = person;

alert(personName);   //"Nicholas"
alert(personAge);    //29
```

与数组字面量一样，当对象字面量出现在等号左侧时，它被认为是一个解构赋值。该语句实际上定义了两个变量`personName`和`personAge`，它们被填充了来自变量`person`的匹配信息。与数组一样，你可以选择要检索的值，如下所示：

```javascript
var { age: personAge } = person;
alert(personAge);    //29
```

这段修改后的代码仅从`person`对象中检索了`age`属性。

## 新对象类型

Harmony 为语言引入了几种新的对象类型。这些对象类型侧重于提供以前仅 JavaScript 引擎可用的功能。

#### 代理对象（Proxy Objects）

Harmony 为 JavaScript 引入了代理（proxy）的概念。代理是一个呈现接口的对象，该接口并不一定作用于代理本身。例如，在代理对象上设置属性实际上可能会调用另一个对象上的函数。代理是一种有效的抽象机制，可以通过 API 暴露部分信息，同时对数据源保持完全控制。

使用`Proxy.create()`方法并传入一个处理器对象（handler object）和一个可选的原型对象来创建代理对象：

```javascript
var proxy = Proxy.create(handler);

// 创建一个具有 myObject 原型的代理
var proxy = Proxy.create(handler, myObject);
```

`handler`对象由定义陷阱的属性组成。陷阱（traps）是用于处理原生功能的函数，以便可以用另一种方式处理。有七个基本陷阱是重要的，以确保代理对象按预期工作：

- `getOwnPropertyDescriptor`：调用`Object.getOwnPropertyDescriptor()`时调用的函数。它接收属性名作为参数。如果属性不存在，则返回属性描述符。

- `getPropertyDescriptor`：调用`Object.getPropertyDescriptor()`时调用的函数。（这是 Harmony 中引入的新方法。）它接收属性名作为参数。如果属性不存在，则返回属性描述符。

- `getOwnPropertyNames`：调用`Object.getOwnPropertyNames()`时调用的函数。它接收属性名作为参数。返回字符串数组。

- `getPropertyNames`：调用`Object.getPropertyNames()`时调用的函数。（这是 Harmony 中引入的新方法。）它接收属性名作为参数。返回字符串数组。

- `defineProperty`：调用`Object.defineProperty()`时调用的函数。它接收属性名和属性描述符作为参数。

- `delete`：在对象的属性上使用`delete`运算符时调用的函数。属性名作为参数传入。返回`true`表示删除成功，否则返回`false`。

- `fix`：调用`Object.freeze()`、`Object.seal()`或`Object.preventExtensions()`时调用的函数。返回`undefined`以在代理上调用这些方法时抛出错误。

除了基本陷阱，还有六个派生陷阱（derived traps）。与基本陷阱不同，未定义一个或多个派生陷阱不会导致错误。每个派生陷阱都会覆盖默认的 JavaScript 行为：

- `has`：当在对象中使用`in`运算符时调用的函数，例如`"name" in object`。属性名作为参数传入。返回`true`表示属性包含在对象中，否则返回`false`。

- `hasOwn`：当在代理上调用`hasOwnProperty()`方法时调用的函数。属性名作为参数传入。返回`true`表示属性包含该属性，否则返回`false`。

- `get`：当读取属性时调用的函数。它接收两个参数：被读取的对象引用和属性名。该对象引用可以是代理本身，也可以是继承自代理的对象。

- `set`：定义一个在向属性写入时调用的函数。该函数接收三个参数：被写入的对象引用、属性名和属性值。与`get`类似，该对象引用可以是代理本身，也可以是继承自代理的实例。

- `enumerate`：定义一个在代理被放入`for-in`循环中时调用的函数。该函数必须返回一个字符串数组，其中包含在`for-in`循环中使用的相应属性名。

- `keys`：定义一个在代理上调用`Object.keys()`时调用的函数。与`enumerate`类似，此函数必须返回一个字符串数组。

代理（Proxies）主要用于在你需要暴露 API 的同时防止某些底层数据被直接操作的情况。例如，假设你想实现一个传统的栈（stack）数据类型。虽然数组可以当作栈使用，但你想确保人们只使用`push()`、`pop()`和`length`。在这种情况下，你可以创建一个作用于数组的代理，但只暴露这三个对象成员：

```javascript
/*
 * 另一个 ES6 Proxy 实验。这个实验创建了一个底层
 * 实现为数组的栈。代理被用于过滤掉接口中
 * "push"、pop" 和 "length" 以外的所有内容，使其成为一个
 * 栈，你无法操作其内容。
 */

var Stack = (function(){

    var stack = [],
        allowed = [ "push", "pop", "length" ];

    return Proxy.create({
        get: function(receiver, name){
            if (allowed.indexOf(name) > -1){
                if(typeof stack[name] == "function"){
                    return stack[name].bind(stack);
                } else {
                    return stack[name];
                }
            } else {
                return undefined;
            }
        }

    });

});

var mystack = new Stack();

mystack.push("hi");
mystack.push("goodbye");

console.log(mystack.length);    //1

console.log(mystack[0]);        //undefined
console.log(mystack.pop());     //"goodbye"
```

这段代码创建了一个名为`Stack`的构造函数。`Stack`构造函数并不是直接在数组上工作，而是返回一个作用于数组的代理对象。`get`陷阱是唯一定义的陷阱，它在返回值之前简单地检查允许属性数组。所有未允许的属性在被引用时最终都会返回`undefined`，而`push()`、`pop()`和`length`则按预期工作。这段代码的关键部分是`get`陷阱的声明，它根据允许的成员来过滤对象的成员检索。如果该成员是函数，则会返回该函数的绑定版本，以便它作用于底层数组对象而不是代理对象本身。

### 代理函数（Proxy Functions）

除了创建代理对象外，你还可以在 Harmony 中创建代理函数。代理函数与代理对象相同，区别在于它是可执行的。代理函数通过使用`Proxy.createFunction()`方法并传入一个处理器对象、一个调用陷阱函数和一个可选的构造函数陷阱函数来创建。例如：

```javascript
var proxy = Proxy.createFunction(handler, function(){}, function(){});
```

`handler`对象拥有与代理对象相同的可用陷阱。调用陷阱函数是在执行代理函数（例如`proxy()`）时执行的代码。构造函数陷阱是在使用`new`运算符调用代理函数（例如`new proxy()`）时执行的代码。如果未定义构造函数陷阱，则调用陷阱也将用于构造函数陷阱。

### Map 和 Set

`Map`类型（也称为简单映射，map-as-simple map）有一个单一的目的：存储键值对列表。开发者通常使用通用对象来实现此目的，但这是有代价的，因为键很容易与原生属性混淆。简单映射将键和值与对象的属性分开，为这些信息提供更安全的存储。一些示例用法：

```javascript
var map = new Map();

map.set("name", "Nicholas");
map.set("book", "Professional JavaScript");

console.log(map.has("name"));   //true
console.log(map.get("name"));   //"Nicholas"

map.delete("name");
```



简单映射的基础 API 由`get()`、`set()`、`has()`和`delete()`组成，每个方法的作用都与其名称完全一致。键可以是原始值，也可以是引用值。

与简单映射相关的是`Set`类型。集合仅仅是一个没有重复项的项集合。与简单映射不同，`Set`只有键，没有与之关联的值。基础 API 有`add()`用于添加项，`has()`用于检查项是否存在以及`delete()`用于移除项。一些示例用法：

```
var set = new Set();
set.add("name");

console.log(set.has("name"));   //true
set.delete("name");

console.log(set.has("name"));   //false
```

截至 2011 年 10 月，`Map`和`Set`的规范尚完整，因此在 JavaScript 引擎开始实现它们之前，这里的细节可能会发生。

### WeakMap

`WeakMap`类型有趣之处在于，它是第一个允许你了解对象何时被完全解除引用的 ECMAScript 特性。`WeakMap`的工作方式类似于简单映射，你可以在其中存储键值对。`WeakMap`的巨大区别是键必须是一个对象，并且当该对象不再存在时，关联的键值对会被移除。例如：

```
var key = {},
    map = new WeakMap();

map.set(key, "Hello!");

// 解除引用，键值被移除
key = null;
```

`WeakMap`的用例尚不明确，但这种构造也出现在 Java 中。

### 结构体 (StructType)

JavaScript 的一个已知缺点是使用单一类型来表示所有数字。WebGL 引入了类型数组来帮助这个问题，而 ECMAScript 6 引入了更多数据类型。结构体类似于 C 语言中的结构。实现定义了若干块类型：

*   `uint8` — 8 位无符号整数
*   `int8` — 8 位符号整数
*   `uint16` — 16 位无符号整数
*   `int16` — 16 位符号整数
*   `uint32` — 32 位无符号整数
*   `int32` — 32 位符号整数
*   `float32` — 32 位浮点
*   `float64` — 64 位浮点

块类型包含单个值，预计未来会增加这八种以外的。结构体通过以对象字面量形式的属性定义实例化`StructType`来创建。例如：

```javascript
var Size = new StructType({ width: uint32, height: uint32 });
```

这段代码创建了一个名为`Size`的新结构体类型，具有两个属性：`width`和`height`。每个属性包含一个 32 位无符号整数。变量`Size`实际上是一个可以像对象构造函数一样使用的构造函数。通过向构造函数传入属性的对象字面量来初始化结构体实例：

```javascript
var boxSize = new Size({ width: 80, height: 60 });
console.log(boxSize.width);   //80
console.log(boxSize.height);  //60
```

在这里，创建了一个宽度为 80、高度为 60 的`Size`新实例。这些属性可读写但必须包含 32 位整数。

通过将每个属性定义为另一个结构体类型，可以创建更复杂的结构体类型。例如：

```javascript
var Location = new StructType({ x: int32, y: int32 });
var Box = new StructType({ size: Size, location: Location });

var boxInfo = new Box({ size: { width:80, height:60 }, location: { x: 0, y: 0 }});
console.log(boxInfo.size.width);   //80
```

此示例创建了一个名为`Location`的简单结构类型和一个名为`Box`的复杂结构类型，后者的属性被定义为结构类型。`Box`构造函数仍然接受一个对象字面量来定义每个属性的值，并会进行类型检查以确保值是正确的数据类型。

### ArrayType

与结构类型紧密相关的是数组类型。数组类型允许创建一个其值限制在特定类型的数组，这与 WebGL 的类型数组非常相似。要创建一个新的数组类型，调用`ArrayType`构造函数并传入它应该持有的数据类型以及数组中将包含多少项。例如：

```
var SizeArray = new ArrayType(Size, 2);
var boxes = new BoxArray([ { width: 80, height: 60 }, { width: 50, height: 50 } ]);
```

这段代码创建了一个名为`SizeArray`的新数组类型，初始化为持有`Size`实例，并在数组中分配了两个空间。数组类型通过传递一个包含需要转换的数据数组来初始化，允许传递字面量并将其强制转换为正确的数据类型（与结构类型相同）。

### 类 (CLASSES)

开发者长期以来渴望在 JavaScript 中有一种简单的方法来定义类似 Java 的类，ECMAScript 6 终于将此功能引入了语言。类是覆盖在当前基于构造函数和原型的类型方法上的语法糖。考虑以下类型定义：

```
function Person(name, age){
    this.name = name;
    this.age = age;
}

Person.prototype.sayName = function(){
    alert(this.name);
};

Person.prototype.getOlder = function(years){
    this.age += years;
};
```

使用新类语法的等效写法是：

```
class Person {

    constructor(name, age){
        public name = name;
        public age = age;
    }

    sayName(){
        alert(this.name);
    }

    getOlder(years){
        this.age += years;
    }

}
```

新的类语法以关键字`class`开始，后面跟着类型名称。大括号内部用于创建属性和方法。方法不再需要`function`关键字；只需使用方法名后跟括号。如果方法名为`constructor`，则它将作为类的构造函数（与之前代码中的`Person`函数相同）。在类大括号内定义的所有其他方法和属性都会应用于原型，因此在这种情况下，`sayName()`和`getOlder()`最终都位于`Person.prototype`上。

在构造函数内部，由关键字`public`或`private`前缀的变量将创建创建为对象的实例属性。在此示例中，`name`和`age`都被定义为公共属性。

#### 私有成员 (Private Members)

类提议默认支持私有成员，包括实例上和原型上的成员。`private`关键字表示该成员是私有的，无法从类方法的外部访问。为了访问私有成员，使用了一种特殊的语法，在`this`上调用`private()`函数，然后访问该属性。例如，以下代码将`Person`类更改为具有私有`age`属性。

```
class Person {

    constructor(name, age){
        public name = name;
        private age = age;
    }

    sayName(){
        alert(this.name);
    }

    getOlder(years){
        private(this).age += years;
    }

}
```

访问私有属性的语法仍在讨论中，并且可能在未来发生变化。

#### 获取器/设置器 (Getters/Setters)

新的类语法允许你直接为属性定义 getter 和 setter，避免了调用`Object.defineProperty()`的额外步骤。该语法与方法相同，但前面有一个`get`或`set`关键字。例如：

```
class Person {

    constructor(name, age){
        public name = name;
        public age = age;
        private innerTitle = "";

        get title(){
            return innerTitle;
        }

        set title(value){
            innerTitle = value;
        }
    }

    sayName(){
        alert(this.name);
    }

    getOlder(years){
        this.age += years;
    }

}
```

此版本的`Person`类为`title`属性定义了一个 getter 和 setter。每个函数都操作在构造函数中定义的`innerTitle`变量。通过在构造函数外部使用相同的语法，也可以为原型属性定义 getter 和 setter。

#### 继承 (Inheritance)

使用类而非传统的 JavaScript 语法的关键优势是实现实现的简单性。不需要担心构造函数劫持（constructor stealing）和原型链，而是使用一种与其他语言共享的简单语法：`extends`关键字。例如：

```
class Employee extends Person {
    constructor(name, age){
        super(name,age);
    }
}
```

这段代码创建了一个作为`Person`子类的新的`Employee`类。原型链在后台发生，现在通过使用`super()`函数正式支持了构造函数劫持。先前的代码与以下代码逻辑上等效：

```
function Employee(name, age){
    Person.call(this, name, age);
}

Employee.prototype = new Person();
```

除了这种继承样式外，类还可以使用`prototype`关键字代替`extends`来直接指定一个对象作为其原型：

```
var basePerson = {
    sayName: function(){
        alert(this.name);
    },

    getOlder: function(years){
        this.age += years;
    }
};

class Employee basePerson {
    constructor(name, age){
        public name = name;
        public age = age;
    }
}
```

在此示例中，`Employee.prototype`被赋值为`basePerson`。

### 模块 (MODULES)

模块（或命名空间或包）是组织 JavaScript 应用的一种流行概念。每个模块包含特定的、自包含且与其他分离的功能。尽管 JavaScript 中出现了几种临时的模块格式，但 ECMAScript 6 试图规范模块的创建和管理。

模块在自己的顶级执行上下运行，因此不会污染导入所在的执行上下文。默认情况下，模块内声明的所有变量、函数、类等对于该模块都是私有的。通过在成员前面使用`export`关键字指示该成员应暴露给外部世界。例如：

```
module MyModule {
    //导出这些内容
    export let myobject = {};
    export function hello(){ alert("hello"); };

    //隐藏这些内容
    function goodbye(){
        //...
    }
}
```

此模块导出了名为`myobject`的对象和一个名为`hello()`的函数。该模块在其他地方或其他模块中使用，但导入了其中一个或两个成员。导入通过`import`命令完成：

```
// 仅导入 myobject
import myobject from MyModule;
console.log(myobject);

// 导入所有
import * from MyModule;
console.log(myobject);
console.log(hello);

// 显式命名导入
import {myobject, hello} from MyModule;
console.log(myobject);
console.log(hello);

// 不导入 - 直接使用模块
console.log(MyModule.myobject);
console.log(MyModule.hello);
```

如果执行上下文可以访问模块，则可以直接访问模块以获取它导出的成员。导入的过程是将单个成员带入当前执行上下文，以便无需直接引用模块即可进行访问。

#### 外部模块 (External Modules)

可以通过提供加载模块的 URL 来动态包含模块。要这样做，只需在模块声明后添加 URL 即可：

```
module MyModule from "mymodule.js";
import myobject from MyModule;
```

此声明指示 JavaScript 引擎下载`mymodule.js`并从其加载名为`MyModule`的模块。请注意此调用是阻塞的——在 URL 被下载并评估之前，JavaScript 引擎将不会继续处理代码。

如果你想包含模块导出的内容但不想引入整个模块，可以使用`import`指令来指定该内容：

```
import myobject from "mymodule.js";
```

总的来说，模块只是将相关功能分组在一起并保护全局作用免受污染的一种方法。

# 严格模式 (Strict Mode)

ECMAScript`5`首次引入了严格模式的概念。严格模式允许你在全局范围内或单个函数内部局部对 JavaScript 错误情况选择开启更严格的检查。严格模式的优势在于，你可以更早地发现错误，因此某些导致编程错误的 ECMAScript 异点（quirks）会被立即捕获。

理解严格模式的规则非常重要，因为下一版本的 ECMAScript 将以严格模式为基础。严格模式支持 Internet Explorer 10+、Firefox 4+、Safari 5.1+ 以及 Chrome。

## 开启严格模式 (OPTING-IN)

要开启严格模式，请使用严格模式预言（pragma），它仅仅是一个没有赋值给任何变量的字符串：

```
"use strict";
```

使用这种语法（它即使在 ECMAScript`3`中也是有效的），可以允许不支持严格模式的 JavaScript 引擎进行无缝回退。支持严格模式的引擎将启用它，而不支持严格模式的引擎将仅仅把该预言视为未赋值的字符串字面量并忽略。

当预言应用于全局（即函数外部）时，整个脚本将启用严格模式。这意味着，将预言添加到与其他脚本合并成单个文件的单个脚本中，将使该文件中的所有 JavaScript 代码都进入严格模式。

你也可以仅在函数内部开启严格模式，例如：

```javascript
function doSomething(){
    "use strict";

    //其他处理
}
```

如果你对页面上的所有脚本没有完全控制权，那么建议仅在经过测试的特定函数内部启用严格模式。

## 变量 (VARIABLES)

在严格模式下，变量的创建方式和时机是不同的。第一个变化是不允许意外创建全局变量。在非严格模式下，以下代码会创建一个全局变量：

```
//变量未被声明
// 非严格模式：创建一个全局变量
// 严格模式：抛出 ReferenceError

message = "Hello world!";
```

尽管`message`前面没有`var`关键字，且没有被显式定义为全局对象的属性，但它仍会被自动创建为全局变量。在严格模式下，执行代码时对未声明的变量进行赋值将抛出`ReferenceError`。

另一个相关的变化是无法对变量调用`delete`操作。非严格模式允许这种操作并可能静默失败（返回`false`）。在严格模式下，尝试删除变量会导致错误：

```javascript
// 删除变量
// 非严格模式：静默失败
// 严格模式：抛出 ReferenceError

var color = "red";
delete color;
```

严格模式还对变量名实施了限制。具体来说，它不允许名为`implements`、`interface`、`let`、`package`、`private`、`protected`、`public`、`static`和`yield`的变量。这些现在是保留字，用于未来的 ECMAScript 版本。在严格模式下，任何尝试将这些作为变量名的行为都会导致语法错误。

## 对象 (OBJECTS)

在严格模式下，对象操作比非严格模式下更容易抛出错误。严格模式倾向于在非严格模式静默失败的情况下抛出错误，增加了在开发早期捕获错误的几率。

首先，有几种情况在尝试操作对象时比非严格模式更可能抛出错误。严格模式倾向于在非严格模式静默失败的情况下抛出错误，增加了在开发早期发现错误的概率。



向只读属性赋值会抛出错误。

在不可配置属性上使用`delete`会抛出错误。

在不可扩展对象上添加属性会抛出错误。

另一个限制是无法通过索引访问可删除的`arguments`。非严格模式允许这种操作并可能静默失败（返回`false`）。在严格模式下，尝试删除属性会导致错误：

```javascript我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。// 尝试删除对象的属性
// 非严格模式：静默失败
// 严格模式：抛出 TypeError

var person = {
    name: "Nicholas"
};
delete person.name;
```

严格模式下，对象的赋值可能会抛出错误。例如：

```javascript
// 尝试修改只读属性
// 非严格模式：允许
// 严格模式：抛出 TypeError

var person = {
    name: "Nicholas"
};
person.name = "Greg";
```

严格模式下，没有设置器（setter）的属性赋值会抛出错误：

```javascript
// 访问没有 setter 的属性
// 非严格模式：允许
// 严格模式：抛出 TypeError

var person = {
    get name() {
        return "Nicholas";
    }
};
person.name = "Greg";
```

严格模式下，在不可扩展对象上添加属性会抛出错误：

```javascript
// 在不可扩展对象上添加属性
// 非严格模式：允许
// 严格模式：抛出 TypeError

var person = {
    name: "Nicholas"
};
Object.freeze(person);
person.age = 25;
```

## 函数 (FUNCTIONS)

首先，严格模式要求函数的参数名是唯一的。考虑以下情况：

```javascript
// 重复的参数名
// 非严格模式：允许（以最后一个参数为准）
// 严格模式：抛出 SyntaxError

function sum(a, a) {
    return a + a;
}
```

其次，严格模式禁止在函数内部创建未声明的变量。在非严格模式下，这会创建一个全局变量：

```javascript
// 使用未声明的变量
// 非严格模式：允许
// 严格模式：抛出 ReferenceError

function showValue() {
    value = "Hi";
}
```

此外，严格模式还改变了函数中`this`值的行为。在非严格模式下，`this`可能会指向全局对象，而在严格模式下，如果不是作为方法调用，它将是`undefined`：

```javascript
// 在没有对象的情况下调用函数
// 非严格模式：指向全局对象
// 严格模式：为 undefined

function show() {
    console.log(this);
}
show(); 
```

另一个变化是消除了`arguments.callee`和`arguments.caller`。在非严格模式下，它们分别引用函数自身和调用者函数。在严格模式下，访问任何一个属性都会抛出`TypeError`。例如：

```javascript
// 访问 arguments.callee
// 非严格模式：正常工作
// 严格模式：抛出 TypeError

function factorial(num) {
    if (num <= 1) {
        return 1;
    } else {
        return num * arguments.callee(num - 1);
    }
}

var result = factorial(5);
```

最后，严格模式禁止函数声明，除非它们位于脚本或函数的顶层。这意味着，例如在`if`语句中声明的函数现在会产生语法错误：

```javascript
// 在 if 语句中的函数声明
// 非严格模式：函数被提升到 if 外部
// 严格模式：抛出语法错误

if (true) {
    function doSomething() {
        //...
    }
}
```

## EVAL()

长期以来备受争议的`eval()`函数在严格模式下得到了改进。`eval()`最大的变化是它不再包含的上下文中创建变量或函数。例如：

```javascript
// eval() 用来创建变量
// 非严格模式：alert 显示 10
// 严格模式：调用 alert(x) 时抛出 ReferenceError

function doSomething() {
    eval("var x=10");
    alert(x);
}
```

当在非严格模式下运行时，这段代码会在函数`doSomething()`中创建一个局部变量`x`，然后使用`alert()`显示该值。在严格模式下，对`eval()`的调用不会在`doSomething()`内部创建变量`x`，因此调用`alert()`会抛出`ReferenceError`，因为`x`未定义。

可以在`eval()`声明变量和函数，但它们仍然在一个特殊的作用域内，该作用域在代码执行时使用并在完成后销毁。因此，以下代码可以无错误运行：

```
"use strict";
var result = eval("var x=10, y=11;  x+y");
alert(result);    //21
```

变量`x`和`y`在`eval()`内部声明，并在返回值之前相加。变量`result`随后包含了 21（即`x`和`y`相加的结果），尽管在调用`alert()`时`x`和`y`已经不存在了。

# EVAL 与参数

严格模式现在明确禁止将`eval`和`arguments`作为标识符并操作它们的值。例如：

```
// 将 eval 和 arguments 重定义为变量
// 非严格模式：可以，无错误
// 严格模式：抛出语法错误

var eval = 10;
var arguments = "Hello world!";
```

在非严格模式下，你可以重写`eval`并为`arguments`赋值一个值。在严格模式下，这会导致语法错误。你不能将其中任何一个作为标识符，这意味着以下所有用例都会抛出语法错误：

* 使用`var`声明

* 赋值给另一个值

* 尝试更改包含的值（例如使用`++`）

* 用于函数名

* 用作命名函数参数

* 在`try-catch`语句中异常名称

# THIS 的强制类型转换

JavaScript 最大的安全问题之一，实际上也是最令人困惑的方面之一，是`this`值在某些情况下是如何被强制转换的。当使用函数的`apply()`或`call()`方法时，在非严格模式下，`null`或`undefined`值会被强制转换为全局对象。在严格模式下，函数的`this`值将始终按照指定使用，无论其值为何。例如：

```
// 访问属性
// 非严格模式：访问全局属性
// 严格模式：抛出错误因为 this 为 null

var color = "red";

function displayColor(){
    alert(this.color);
}

displayColor.call(null);
```

这段代码将`null`传递给`displayColor.call()`，在非严格模式下这意味着函数的`this`值是全局对象。结果是弹出一个显示“red”的警告。在严格模式下，函数的`this`值为`null`，因此在尝试访问`null`对象的属性时抛出错误。

## 其他变化

严格模式还有其他几个你需要注意的变化。第一个是消除了`with`语句。`with`语句改变了标识符的解析方式，为了简化，已从严格模式中移除。在严格模式下尝试使用`with`会导致语法错误。

```
// 使用 with 语句
// 非严格模式：允许
// 严格模式：抛出语法错误

with(location){
    alert(href);
}
```

严格模式还消除了 JavaScript 中的八进制字面量。八进制字面量以零开头，传统上它是许多错误的根源。在严格模式下，八进制字面量被视为无效语法。

```
// 使用八进制字面量
// 非严格模式：值 own 8。
// 严格模式：抛出语法错误。

var value = 010;
```

正如书中提到的，ECMAScript 5 还更改了非严格模式下的`parseInt()`，在该模式下，八进制字面量被视为带有前零的十进制字面量。例如：

```
// 在 parseInt() 中使用八进制字面量
// 非严格模式：值为 8
// 严格模式：值为 10

var value = parseInt("010");
```

# C

# JavaScript 库

JavaScript 库有助于弥补浏览器之间的差异，并提供更易访问复杂浏览器功能的方法。库有两种形式：通用型和专用型。通用 JavaScript 库提供对常用浏览器功能的访问，可以作为网站或 Web 应用程序的基础。专用库只执行特定任务，用于网站或 Web 应用程序的一部分。本附录提供了这些库及其部分功能的概述，以及你可以作为额外资源使用的网站。

## 通用库

通用 JavaScript 库提供了跨越主题的功能。所有通用库都试图通过新 API 封装常用功能，平衡浏览器接口和实现上的差异。某些 API 看起来与原生功能相似，而另一些则完全不同。通用库通常提供与 DOM 的交互、对 Ajax 的支持以及辅助常用任务的实用方法。

### Yahoo! 用户界面库 (YUI)

Yahoo! 用户界面库 (YUI) 是一个开源 JavaScript 和 CSS 库，按需方式设计。该库并非只有一个文件；而是提供了多种配置的多个文件，确保你只加载需要的内容。YUI 涵盖了 JavaScript 的各个方面，从基础工具和辅助函数到完整的组件。Yahoo! 有有一支专门的软件工程师团队提供出色的文档和支持。

* **许可证**：BSD 许可证

* **网站**：[www.yuilibrary.com](http://www.yuilibrary.com)

### Prototype

Prototype 是一个开源库，为常见的 任务提供简单的 API。它最初为 Ruby on Rails 开发，是类驱动的，旨在 JavaScript 提供类定义和继承。为了实现这一目标，Prototype 可以轻松地丢到任何页面中。它由 Sam Stephenson 编写并维护。

* **许可证**：MIT 许可证和知识共享署名 3.0 无演绎

* **网站**：[www.prototypejs.org](http://www.prototypejs.org/)

### Dojo Toolkit

Dojo Toolkit 是一个基于包系统的开源库，功能组组织在包中并按需加载。Dojo 提供了广泛的选项和配置，涵盖了你想用 JavaScript 做的任何事情。Dojo 由 Alex Russell 创建并在员工和志愿者维护。

* **许可证**：“New”BSD 许可证或学术自由许可证 2.1

* **网站**：[www.doolotkit.org](http://www.doolotkit.org/)

### MooTools

MooTools 是一个紧凑且优化的开源库，为原生 JavaScript 对象添加方法以提供熟悉界面的新功能。其小体积和简单的 API 使 MooTools 受到 Web 开发者的喜爱。

* **许可证**：MIT 许可证

* **网站**：[www.mootools.net](http://www.mootools.net/)

### jQuery

jQuery 是一个提供函数式编程界面的开源库。它是一个完整的库，核心围绕使用 CSS 选择器与 DOM 元素构建。通过链式，jQuery 代码看起来更像是对应该发生的事情的描述而非 JavaScript 代码。这种代码风格在设计师和原型师中变得流行。jQuery 由 John Resig 编写并维护。

* **许可证**：MIT 许可证或通用公共许可 (GPL)

* **网站**：[`jquery.com`](http://jquery.com/)

### MochiKit

MochiKit 是一个由几个较小工具组成的开源库，MochiKit 以文档完备和测试充分自豪，拥有大量的 API 和示例文档以及数百项测试以确保质量。MochiKit 由 Bob Ippolito 编写并维护。

* **许可证**：MIT 许可证或学术自由许可证 2.1

* **网站**：[www.mochikit.com](http://www.mochikit.com/)

### Underscore.js

虽然`Underscore.js`并不一个一个通用库，但它为 JavaScript 的函数式编程提供了一些额外功能。文档将`Underscore.js`称为`jQuery`的补充，为处理对象、数组、函数和其他 JavaScript 数据类型提供了额外的低级功能。`Underscore.js`由 DocumentCloud 的 Jeremy Ashkenas 维护。

许可证：MIT 许可证

网站：[`documentcloud.github.com/underscore/`](http://documentcloud.github.com/underscore/)

# 互联网应用程序

互联网应用程序库的设计旨在简化整个 Web 应用程序的开发。它们不是为应用程序拼图提供细小的碎片，而是为快速应用开发提供了整个概念框架。尽管这些库可能包含一些低级功能，但它们的目标是帮助你快速开发 Web 应用程序。

## Backbone.js

`Backbone.js`是一个构建在`Underscore.js`之上的极简模型-视图-控制器 (`MVC`) 开源库，针对单页应用进行了优化，允许你在应用程序状态更改时轻松更新页面的部分。`Backbone.js`由 DocumentCloud 的 Jeremy Ashkenas 维护。

许可证：MIT 许可证

网站：[`documentcloud.github.com/backbone/`](http://documentcloud.github.com/backbone/)

## Rico

`Rico`是一个旨在让丰富的互联网应用程序开发变得简单的开源库，它为`Ajax`、动画以及样式和小部件提供了工具。该库由一个小型志愿者团队维护，截至 2008 年开发工作已显著放缓。

许可证：Apache License 2.0 版本

网站：[`openrico.org/`](http://openrico.org/)

## qooxdoo

`qooxdoo`是一个旨在帮助整个 Web 应用程序开发周期的开源库。`qooxdoo`实现了了自己的类和接口版本，以创建一个类似于传统面向对象 (`OO`)语言的编程模型。该库包含完整的`GUI`工具包和用于简化前端构建过程的编译器。`qooxdoo`最初是 1&1 Web 托管公司（[www.1and1.com](http://www.1and1.com)）的内部库，后来根据开源许可证发布。1&1 雇用了几名全职开发者来维护和开发该库。

许可证：GNU 许可通用许可证 (LGPL) 或 Eclipse 公共许可证 (EPL)

网站：[www.qooxdoo.org/](http://www.qooxdoo.org/)

## 动画与特效

动画和其他视觉效果已成为 Web 开发的重要部分。在网页上获得流畅的动画是一项非凡的任务，几个库开发者已经站出来提供易用且流畅的动画和特效。之前提到的许多通用 JavaScript 库也具有动画功能。

## script.aculo.us

`script.aculo.us`是`Prototype`的伴侣，它仅需`CSS`和`DOM`即可轻松访问酷炫动画。在使用 [script.aculo.us](http://script.aculo.us) 之前必须加载`Prototype`。[script.aculo.us](http://script.aculo.us) 是最流行的特效库之一，被全球各大网站和 Web 应用程序使用。作者 Thomas Fuchs 积极维护`script.aculo.us`。

许可证：MIT 许可证

网站：[`script.aculo.us/`](http://script.aculo.us/)

## moo.fx

[moo.fx](http://moo.fx) 开源动画库设计运行在`Prototype`或`MooTools`之上。它的目标是尽可能小（最新版本为 3KB），并允许开发者在编写尽可能少代码的同时创建动画。[moo.fx](http://moo.fx) 默认包含在`MooTools`中；也可以单独下载以供`Prototype`使用。

许可证：MIT 许可证

网站：[`moofx.mad4milk.net/`](http://moofx.mad4milk.net/)

## Lightbox

`Lightbox`是一个用于在任何页面上创建简单图像叠加层的 JavaScript 库，它同时需要`Prototype`和 [script.aculo.us](http://script.aculo.us) 来创建视觉特效。基本思想是允许用户在不离开当前页面的情况下在叠加层中查看图像或一系列图像。“lightbox”叠加层外观和过渡上都是可自定义的。`Lightbox`由 Lokesh Dhakar 开发和维护。

许可证：知识共享署名许可协议 2.5 许可证

网站：[www.huddletogether.com/projects/lightbox2/](http://www.huddletogether.com/projects/lightbox2/)

## 加密



随着`Ajax`应用程序变得越来越流行，浏览器端加密以保护通信的需求日益增加。幸运的是，几个人已经在`JavaScript`中实现了常见的安全算法。这些库中的大多数没有得到作者的官方支持，但仍被广泛使用。

## JavaScript MD5

`JavaScript MD5`是一个实现了`MD4`、`MD5`和`SHA-1`安全哈希函数的开源库。作者`Paul Johnston`和其他几个贡献者编写了这个功能丰富的库，每个算法一个文件，用于`Web`应用程序。首页提供了哈希函数的概述，并对漏洞和适当用途简要讨论。

许可证：BSD许可证

网站：[`pajhome.org.uk/crypt/md5/`](http://pajhome.org.uk/crypt/md5/)

## JavaScrypt

`JavaScrypt`是一个实现了`MD5`和`AES`(256位)加密的库。`JavaScrypt`网站提供了关于加密历史及其在计算机中使用的大量信息。尽管缺乏如何将库集成到`Web`应用程序的基础文档，但`JavaScrypt`的源码充满了数学运算和计算。

许可证：公有领域

网站：[www.fourmilab.ch/javas/](http://www.fourmilab.ch/javas/)

# 工具

编写`JavaScript`就像编写其他语言一样，有旨在简化开发的工具。适用于`JavaScript`的工具不断增加，使得定位问题、优化和部署变得更加容易。某些工具设计为从`JavaScript`使用，而另一些可以在浏览器之外运行。本附录提供了这些工具的概述，以及更多信息的资源。

## 验证器

`JavaScript`调试的问题之一是许多`IDE`在输入时不会显示错误。大多数开发者编写代码并加载到浏览器中查找错误。在部署之前验证`JavaScript`代码可以显著减少此类错误的发生。验证器检查基本的语法和样式。

### JSLint

`JSLint`是由`Douglas Crockford`编写的`JavaScript`验证器。它在核心层面检查语法错误，兼容最低标准。（它遵循最严格的规则以确保代码在任何地方运行）。你可以启用关于代码风格的警告，包括代码格式、未定义的全局变量等。尽管`JSLint`用`JavaScript`编写的，但可以通过基于`Java`的`Rhino`解释器在命令行运行，也可以通过`WScript`和其他`JavaScript`解释器运行。该网站为每个命令行解释器提供了自定义版本。

许可证：免费

### JSHint

`JSHint`是`JSLint`的分支，在应用规则方面提供了更多的可定制性。像`JSLint`一样，它首先检查语法错误，然后查找问题的代码模式。每个`JSLint`检查也存在于`JSHint`中，但开发者对应用哪些规则有更好的控制。同样与`JSLint`类似，`JSHint`也可以使用`Rhino`在命令行运行。

许可证：免费

`JavaScript Lint`与`JSLint`完全无关，它是由`Matthias Miller`编写的基于`C`的`JavaScript`验证器。它使用`Firefox`使用的`JavaScript`解释器`SpiderMonkey`来解析代码并查找语法错误。该工具拥有大量的选项，可以对编码风格、未声明的变量和不可达的代码提供额外的警告。`JavaScript Lint`适用于`Windows`和`Macintosh`系统，并提供源代码。

价格：免费

网站：[www.javascriptlint.com/](http://www.javascriptlint.com/)

# 极简化工具 (MINIFIERS)

`JavaScript`构建过程的一个重要部分是对输出进行压缩以移除多余字符。这样做可以确保传输到浏览器进行解析的字节最少，从而最终提高用户体验。有多种此类压缩工具可用，压缩率各不相同。

### JSMin

`JSMin`是由`Douglas Crockford`编写的基于`C`的压缩工具，执行基本的`JavaScript`压缩。它主要移除空格和注释，以确保生成的代码仍然无问题地执行。`JSMin`提供`Windows`可执行文件版本，并提供`C`以及许多其他语言的源码。

价格：免费

网站：[www.crockford.com/javascript/jsmin.html](http://www.crockford.com/javascript/jsmin.html)

### Dojo ShrinkSafe

负责`Dojo Toolkit`的同一团队开发了一个名为`ShrinkSafe`的工具，它使用`Rhino` `JavaScript`解释器将`JavaScript`代码解析为标记流，然后利用它安全地压缩代码。与`JSMin`类似，`ShrinkSafe`会移除额外的空格（但不包括换行符）和注释，但它更进一步，将局部变量名替换为两个字符的变量名。结果是输出比`JSMin`更小，且没有任何引入语法错误的风险。

价格：免费

网站：[`shrinksafe.dojotoolkit.org/`](http://shrinksafe.dojotoolkit.org/)

### YUI Compressor

`YUI`团队拥有一个名为`YUI Compressor`的压缩工具。与`ShrinkSafe`类似，`YUI Compressor`使用`Rhino`将`JavaScript`代码解析为标记流，然后移除注释和空格并替换变量名。与`ShrinkSafe`不同，`YUI Compressor`还会移除换行并执行若干其他微优化以节省字节。通常，由`YUI Compressor`处理的文件比用`JSMin`或`ShrinkSafe`处理的文件更小。

价格：免费

网站：[`yuilibrary.com/projects/yuicompressor`](http://yuilibrary.com/projects/yuicompressor)

# 单元测试 (UNIT TESTING)

测试驱动开发 (TDD) 是一种围绕单元测试软件开发过程。直到最近，`JavaScript`还没有许多单元测试工具。现在，大多数`JavaScript`库都会对其代码进行某种形式的单元测试，有些发布单元测试框架供他人使用。

### JsUnit

原始`JavaScript`单元测试库不限于任何特定的`JavaScript`库。`JsUnit`是流行的`Java` `JUnit`测试框架的移植。测试在页面中运行，并可以设置为自动测试并将结果提交到服务器。该网站包含示例和基础文档。

价格：免费

网站：[www.jsunit.net/](http://www.jsunit.net/)

### YUI Test

`YUI Test`是`Yahoo!`用户界面库 (YUI) 的一部分，不仅可以测试使用`YUI`的代码，还可以测试你网站或应用程序上的任何`JavaScript`。`YUI Test`包含了简单和复杂的断言，以及模拟简单鼠标和键盘事件的方法。该框架在`Yahoo!`开发者网络上有完整的文档，包括示例、API文档等。测试在浏览器中运行，结果输出在页面上。`YUI`使用`YUI Test`来测试整个库。

价格：免费

网站：[`yuilibrary.com/projects/yuitest/`](http://yuilibrary.com/projects/yuitest/)

### Dojo Object Harness (DOH)

`Dojo Object Harness (DOH)`最初是`Dojo`的内部单元测试工具，后来向所有人开放。与其他框架一样，单元测试在浏览器内部运行的。

价格：免费

网站：[www.dojotoolkit.org/](http://www.dojotoolkit.org/)

### qUnit

`qUnit`是专为`jQuery`设计的单元测试框架。事实上，`jQuery`本身所有的测试都使用`qUnit`。尽管如此，`qUnit`并不依赖于`jQuery`，可以测试任何`JavaScript`代码。`qUnit`以其是一个非常简单的单元测试框架而自豪，让人们能够轻松上手。

价格：免费

网站：[`github.com/jquery/qunit`](https://github.com/jquery/qunit)

# 文档生成器 (DOCUMENTATION GENERATORS)

大多数`IDE`都包含主要语言的文档生成器。由于`JavaScript`没有官方`IDE`，传统上文档通过手工编写或通过重用其他语言的文档生成器完成。然而，现在有了专门针对`JavaScript`的文档生成器。

### JsDoc Toolkit

`JsDoc Toolkit`是最早的`JavaScript`文档生成器之一。它要求你在源代码中输入类似`Javadoc`的注释，这些注释会被处理并输出为`HTML`文件。你可以使用预建的`JsDoc`模板之一自定义`HTML`格式，也可以创建自己的。`JsDoc Toolkit`以`Java`包的形式提供。

价格：免费

网站：[`code.google.com/p/jsdoc-toolkit/`](http://code.google.com/p/jsdoc-toolkit/)

### YUI Doc

`YUI Doc`是`YUI`的文档生成器。该生成器用`Python`编写，因此需要安装`Python`运行时环境。`YUI Doc`输出的`HTML`文件集成了属性和方法搜索，这些功能是通过`YUI Autocomplete`组件实现的。与`JsDoc`类似，`YUI Doc`要求在源代码中插入类似`Javadoc`的注释。默认`HTML`可以通过修改默认`HTML`文件和关联样式表进行更改。

价格：免费

网站：[www.yuilibrary.com/projects/yuidoc/](http://www.yuilibrary.com/projects/yuidoc/)

### AjaxDoc

`AjaxDoc`的目标与之前的生成器略有不同。它不是为`JavaScript`文档创建`HTML`文件，而是创建与`.NET`语言（如`C#`和`Visual Basic .NET`）格式相同的`XML`文件。这样做允许标准的`.NET`文档生成器创建`HTML`格式的文档。`AjaxDoc`要求注释格式类似于所有`.NET`语言的文档注释。`AjaxDoc`是为`ASP.NET` `Ajax`解决方案创建，但也适用于独立项目。

价格：免费

网站：[www.codeplex.com/ajaxdoc/](http://www.codeplex.com/ajaxdoc/)

# 安全执行环境 (SECURE EXECUTION ENVIRONMENTS)

随着杂烩应用 (mashups) 的流行，越来越需要允许第三方`JavaScript`在同一页面上存在并运行。这引发了关于访问受限功能的若干安全问题。以下工具旨在创建安全执行环境，让不同来源的`JavaScript`可以在其中存在且互不干扰。

### ADsafe

由`Douglas Crockford`创建的`ADsafe`是被认为对第三方脚本安全的`JavaScript`子集。为了让代码在`ADsafe`中运行，页面必须包含`ADsafe` `JavaScript`库并以`ADsafe`小部件格式进行标记。因此，该代码在任何页面上执行都是安全的。

价格：免费

网站：[www.adsafe.org/](http://www.adsafe.org/)

### Caja

`Caja`采用了一种独特的方法来确保`JavaScript`执行的安全。与`ADsafe`，`Caja`定义了一个可以以安全方式使用的`JavaScript`子集。`Caja`然后可以对这些`JavaScript`代码进行清理，并验证它们仅执行了应该执行的操作。作为该项目的一部分，提供了一种名为`Cajita`的语言，它是`JavaScript`功能的一个更小的子集。`Caja`仍处于初期阶段，但在允许多个脚本在同一页面上运行而无恶意活动可能方面展现了巨大的潜力。

价格：免费

网站：[`code.google.com/p/google-caja/`](http://code.google.com/p/google-caja/)

![image](img/title.jpg)

# Web 开发人员的专业 JavaScript®，第三版

出版商：

John Wiley & Sons, Inc.

10475 Crosspoint Boulevard

Indianapolis, IN 46256

[www.wiley.com](http://www.wiley.com)

版权所有 © 2012 John Wiley & Sons, Inc., Indianapolis, Indiana

在加拿大同步出版

ISBN: 978-1-118-02669-4

ISBN: 978-1-118-22219-5 (ebk)

ISBN: 978-1-118-23309-2 (ebk)

ISBN: 978-1-118-26080-7 (ebk)

本出版物的任何部分均不得复制、存储在检索系统中或以任何形式或通过任何方式（电子、机械、复印、录制、扫描或其他）传输，除非 1976 年《美国版权法》第 107 节或 108 节允许，否则未经出版商的事先书面许可，或通过向版权许可中心支付适当的副本费用获得授权（222 Rosewood Drive, Danvers, MA 01923, (978) 750-8400，传真 (978) 646-8600）。向出版商请求许可应请致至：Permissions Department, John Wiley & Sons, Inc., 111 River Street, Hoboken, NJ 07030, (201) 748-6011,传真 (201) 748-6008，或在线访问 [`www.wiley.com/go/permissions`](http://www.wiley.com/go/permissions)。

## 责任限制/免责声明

出版商和作者对本作品内容的准确性或完整性不作任何陈述或保证，并特别放弃所有保证，包括但不限于对特定用途适用性的保证。销售或促销材料不得创建或扩大任何保证。书中包含的建议和策略可能不适用于所有情况。本书的销售是基于以下理解：即出版商并未从事法律、会计或其他专业服务。如果需要专业帮助，应寻求能力胜的专业人士的服务。出版商和作者对由此产生的损害概不承担责任。书中提到的某个组织或网站作为引用和/或进一步信息的潜在来源，并不意味着作者或出版商认可该组织或网站可能提供的信息或其可能做出的建议。此外，读者应注意，书中列出的`Internet`网站在本书编写与阅读期间之间可能已经发生了变化或消失。

有关我们其他产品的通用信息，请联系美国境内的客户服务部门 (877) 762-2974，美国境外请拨 (317) 572-3993 或传真至 (317) 572-4002。

`Wiley`以多种印刷和电子格式出版，并按需打印。本书标准纸质版本中包含的部分材料可能未包含在电子书或按需打印中。如果本书提到的媒体（如`CD`或`DVD`）未包含在您购买的版本中中，您可以在 [`booksupport.wiley.com`](http://booksupport.wiley.com) 下载这些材料。有关`Wiley`产品的更多信息，请访问 [www.wiley.com](http://www.wiley.com)。

美国国会图书馆控制号：2011943911

## 商标

`Wiley`、`Wiley`标志、`Wrox`、`Wrox`标志、`Wrox Programmer to Programmer`以及相关的商业装扮均为`John Wiley & Sons, Inc.`及其/或其关联公司在美国和其他国家的商标或注册商标，未经书面许可不得使用。`JavaScript`是`Oracle America, Inc.`的注册商标。所有其他商标均为其各自所有者的财产。`John Wiley & Sons, Inc.`与书中提到的任何产品或供应商均无关联。

致我的父母，他们从未停止支持和激励我。

# 关于作者

![image](img/fix-01.jpg)

`NICHOLAS C. ZAKAS`从事`Web`领域已十多年。在此，他既参与过全球大型公司使用的企业内网应用程序开发，也参与过如`My Yahoo!`和`Yahoo!`首页等大型消费者网站。作为`Yahoo!`的演示架构师，`Nicholas`指导了全球访问量最大的网站的前端开发和标准。`Nicholas`是一位な演讲者，经常在公司、会议和聚会上就前端最佳实践和新技术进行演讲。

## 关于编辑

`NICHOLAS C. ZAKAS`是一位拥有十年经验的前端工程师。`John`在加州大学伯克利分校获得数学学士学位，目前是一家健康初创公司的首席开发人员。在编辑本书之前，`John`编辑过几本书。当他不编程时，通常发现自己正浸于数学和哲学中。

## 制作名单

执行编辑

`Carol Long`

资深项目编辑

`Kevin Kent`

技术编辑

`John Peloquin`

制作编辑

`Kathleen Wisor`

校对编辑

`Katherine Burt`

编辑经理

`Mary Beth Wakefield`

自由职业编辑经理

`Rosemarie Graham`

营销总监

`David Mayhew`

营销经理

`Ashley Zurcher`

业务经理

`Amy Knies`

制作经理

`Tim Tate`

执行集团出版总裁

`Richard Swadley`

执行出版商

`Neil Edde`

副出版商

`Jim Minatel`

项目协调（封面）

`Katie Crocker`

校对

`Nicole Hirschman`

索引

`Robert Swanson`

封面设计

`Leandra Young`

封面图片

© iStock/Andrew Rich

# 致谢

尽管作者的名字印在书封上，但没有书并不是一个人的成果，我想感谢参与本书的几位人士。



首先，感谢 John Wiley & Sons我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。继续为我提供写作机会。他们在《Professional JavaScript for Web Developers》第一版时愿意为一个无名作者承担风险，对此我将永存感激。

感谢 John Wiley & Sons 的员工，特别是 Kevin Kent 和 John Peloquin，他们在确保我诚实以及处理我在写作过程中对书籍的频繁更改方面表现出色。

还要感谢所有对书稿草章节提供反馈的人：Rob Friesel, Sergey Ilinsky, Dan Kielp, Peter-Paul Koch, Jeremy McPeak, Alex Petrescu, Dmitry Soshnikov 和 Juriy “Kangax” Zaytsev。你们的反馈使这本书成为了我非常自豪的作品。

特别感谢 Brendan Eich 对第一章中包含的 JavaScript 历史进行的修正。

最后但同样重要的是，感谢 Rey Bango 为本书撰写序言。在在线交流多年后，我在 2010 年第一次见到 Rey。他是业内内真正友善的人之一，我很荣幸他抽出时间支持这本书。

回首我的职业生涯（现在已有 20 多年了），在意识到我的白发真的冒出来出来的空隙，我反思了那些对我的职业生活和决策产生巨大影响的技术和人物。如果我非要选择一种对我产生过最大积极影响的技术，那将是`JavaScript`。请注意，我并不总是`JavaScript`的信徒。像许多人一样，我曾将其视为一种玩具级语言，仅限于制作旋转轮播图和在页面上点缀一些有趣的特效。我当时是一个服务器端开发者，该死，我们可不玩玩具语言的！但随后发生了一些事情：`Ajax`。

我永远不会忘记听到到处都在讨论`Ajax`这个热词，并认为它是某种非常酷炫、新颖且创新的技术。我必须去查查它，当我阅读关于它的内容时，我震惊了，因为我发现那个被我轻易贬之的玩具语言，现在竟然是每一位专业 Web 开发者口口讨论的技术。突然间，我的认知改变了。当我继续探索`Ajax`的本质时，我意识到`JavaScript`是极其强大的，我想要拥有它所提供的所有美好。因此，我全心地拥抱了它，努力理解这门语言，加入`jQuery`项目团队，并专注于客户端开发。生活很美好。

我参与`JavaScript`越越深，遇到的开发者就越多，其中一些人直到今天我仍将他们视为巨星和导师。`Nicholas Zakas`就是这些开发者之一。我记得读过这本书的第二版，当时觉得尽管我投入了多年钻研，但从中中学到了非常多的东西。这本书感觉非常真诚且深思熟虑，仿佛`Nicholas`明白读者的经验水平是各异的，他需要据此调整语调。这在技术类书籍中非常引人注目。大多数作者试图通过深入探讨那些晦涩难懂的技术术语来给人留深刻印象。而这本书不同，它立即成为了我的案头好书，也是我推荐给任何想要实实理解`JavaScript`的开发者的书籍。我希望每个人都能产生我的感受，并意识到这是一份多么宝贵的资源。

随后，在一次`jQuery`大会议上，我有极大的幸运竟然亲面见到了`Nicholas`。这位世界顶尖的`JavaScript`开发者之一正在负责世界上最重要的 Web 属性网站之一（Yahoo!），而他是我见过最友善的人之一。我承认；见到他时我有点崇星了。而最棒的是，他是一个极其接地气的人，只想帮助开发者变得优秀。因此，不仅是他的书改变了我对`JavaScript`的看法，`Nicholas`本人也是一个我想继续合作并深入了解的人。

当`Nicholas`邀请我写这篇序言时，我无法形容我是多么受宠若惊。我竟然为大师做开场。这证明了他是一个多么酷的人。但重要的是，这给了我一个机会与你们分享为什么我觉得这本书如此重要。我读过很多`JavaScript`书，那里确实有很多优秀的作品。但我看来，这本书提供了全方位的保障，让你成为一名极其精通且能的`JavaScript`开发者。从`表达式`和`变量声明`等入门主题到`闭包`和`面向对象开发`等高级主题的流畅且周全的过渡，使它与其它书籍区别开来——那些书籍要么过于入门，要么预设你已经在用`JavaScript`构建导弹制导系统了。这是一本“普通人”的书，将帮助你写出令你自豪的代码，并构建令人们兴奋和喜悦的网站。

—Rey Bango

微软公司高级技术推广工程师

`jQuery`项目团队

# 引言

有人声称`JAVASCRIPT`现在是世界上最流行的编程语言，运行着无数世界赖以进行业务处理、购物、流程管理等活动的复杂 Web 应用。

`JavaScript`的基础非常松地类似于`Java`，`Java`是一种面向对象的编程语言，通过嵌入式应用程序（applets）在 Web 上流行起来。尽管`JavaScript`具有类似的语法和编程方法，但它并不是`Java`的“轻量级”版本。相反，`JavaScript`是它自己的动态语言，在世界各地的浏览器中找到了家园，并增强了网站和 Web 应用的用户交互。

在本书书中，`JavaScript`涵盖了从最早`Netscape`浏览器的初级一直到如今完全支持`DOM`和`Ajax`的形态。你将学习如何扩展这种语言以适应特定需求，以及如何在没有`Java`或隐藏帧等媒介的情况下，创建无缝的客户端-服务器通信。简而言之，你将学习如何将`JavaScript`解决方案应用于全球 Web 开发者面临的业务问题。

## 本书适合谁看

本书针对三类读者：

* 熟悉面向对象编程的经验丰富的开发者，他们希望学习`JavaScript`与传统 OO 语言（如`Java`和`C++`）的关系。

* 试图提高其网站和 Web 应用可用性的 Web 开发者。

* 旨在更好地理解这门语言的初级`JavaScript`开发者。

此外，熟悉以下相关技术是这本书适合你的一个强有力指标：

* `Java`

* `PHP`

* `ASP.NET`

* `HTML`

* `CSS`

* `XML`

本书并不针对缺乏基础计算机科学背景的初学者，或那些只想为网站添加简单用户交互的读者。这些读者应该参阅 Wrox 的《Beginning JavaScript》，第 4 版（Wiley, 2009）。

## 本书涵盖内容

《Professional JavaScript for Web Developers, 3rd Edition》提供了开发者级别的介绍，以及`JavaScript`更高级且实用的功能。

从基础开始，本书探讨了`JavaScript`如何起源并演变成现在的样子。随后对构成`JavaScript`实现的组件进行了详细讨论，特别关注`ECMAScript`和文档对象模型 (`DOM`) 等标准。同时也讨论了不同浏览器中`JavaScript`实现的差异。

在这些基础上，本书继续涵盖`JavaScript`的核心概念，包括面向对象编程、继承以及在`HTML`中的应用。在深入检查事件和事件处理之后，探讨了浏览器检测技术。书中最后一部分关注高级主题，包括性能/内存优化、最佳实践以及`JavaScript`的未来。

## 结构

本书由以下章节组成：

1. 什么是 JavaScript? —— 解释了`JavaScript`的起源：它的来源、如何演变以及现在是什么。介绍的概念包括`JavaScript`与`ECMAScript`的关系、文档对象模型 (`DOM`) 以及浏览器对象模型 (`BOM`)。还包含了对欧洲计算机标准协会 (`ECMA`) 和世界维网联盟 (`W3C`) 相关标准的讨论。

2. HTML 中的 JavaScript —— 研究了如何结合`HTML`使用`JavaScript`创建动态网页。介绍了将`JavaScript`嵌入页面的各种方式，包括对`JavaScript`内容类型与其`<script>`元素关系的讨论。

3. 语言基础 —— 介绍了基础语言概念，包括语法和流程控制语句。解释了`JavaScript`与其他 C 类语言的语法相似性并指出了差异。引入了类型转换及其与内置运算符相关的内容。

## 4. 变量、作用域与内存

探讨了`JavaScript`在其弱类型特性下是如何处理变量的。书中包含了关于原始值和引用值区别的讨论，以及与变量相关的执行上下文信息。此外，通过对`JavaScript`垃圾回收的讨论解释了当变量超出作用域时内存是如何被回收的。

## 5. 引用类型

涵盖了`JavaScript`内置引用类型的所有细节，如`Object`和`Array`。书中对`ECMA-262`中描述的每种引用类型都从理论以及它们与浏览器实现的关系两个方面进行了讨论。

## 6. 面向对象编程

解释了如何在`JavaScript`中面向对象编程。由于`JavaScript`没有类概念，书中探索了若干用于对象创建和继承的流行技术。本章还涵盖了函数原型概念以及它如何与整体面向对象（OO）方法相关。

## 7. 函数表达式

探讨了`JavaScript`最强大的特性之一：函数表达式。主题包括闭包、`this`对象的工作原理、模块模式以及创建私有对象成员。

## 8. 浏览器对象模型

介绍了浏览器对象模型 (BOM)，该模型负责允许与浏览器本身交互的对象。书中涵盖了每个 BOM 对象，包括`window`、`document`、`location`、`navigator`和`screen`。

## 9. 客户端检测

解释了检测客户端及其能力的各种方法。不同的技术包括能力检测和用户代理（user-agent）字符串检测。书中讨论了每种方法的优缺点以及场景适用性。

## 10. 文档对象模型

介绍了在`DOM Level 1`中定义的`JavaScript`可用文档对象模型 (DOM) 对象。对 XML 及其与 DOM 关系的简要介绍，随后是对整个 DOM 以及其如何允许开发者操作页面的深度探索。

## 11. DOM 扩展

解释了其他 API 以及浏览器本身如何扩展 DOM 的更多功能。主题包括`Selectors API`、`Element Traversal API`以及 HTML5 扩展。

## 12. DOM Level 2 和 3

在前两章的基础上，解释了 DOM Level 2 和 Level 3 如何通过额外的属性、方法和对象增强 DOM。讨论了 Internet Explorer 与其他浏览器之间的兼容性问题。

## 13. 事件

解释了`JavaScript`中事件的本质、它们的起源、遗留支持以及 DOM 如何重新定义事件应该的工作方式。涵盖了包括 Wii 和 iPhone 在内的各种设备。

## 14. 脚本表单

探讨了使用`JavaScript`增强表单交互并绕过浏览器限制的方法。讨论集中在单个表单元素（如文本框和选择框）以及数据验证与处理。

## 15. 使用 Canvas 图形

讨论了`<canvas>`标签以及如何使用它创建即时图形。涵盖了 2D 上下文和 WebGL (3D) 上下文，为你创建动画和游戏提供了良好的起点。

## 16. HTML5 脚本

介绍了 HTML5 中定义的`JavaScript` API 变化。主题包括跨文档消息传递、拖放 API、`<audio>`和`<video>`元素的脚本化，以及历史状态管理。

## 17. 错误处理与调试

讨论了浏览器如何处理`JavaScript`代码中的错误，并提供了几种处理错误的方法。书中还讨论了每个浏览器的调试工具和技术，包括关于简化调试过程的建议。

## 18. JavaScript 中的 XML

介绍了用于读取和操作可扩展标记语言 (XML) 数据的`JavaScript`特性。解释了各种 Web 浏览器在支持和对象方面的差异，并为更容易跨浏览器编码提供了建议。本章还涵盖了使用可扩展样式表语言转换 (XSLT) 在客户端转换 XML 数据。

## 19. 用于 XML 的 ECMAScript

讨论了`JavaScript`的扩展 ECMAScript for XML (E4X)，它旨在简化 XML 操作。解释了 E4X 相比于使用 DOM 进行 XML 操作的优势。

## 20. JSON

介绍了 JSON 数据格式作为 XML 的替代方案。讨论了浏览器原生的 JSON 解析和序列化，以及使用 JSON 时的安全性考量。

## 21. Ajax 和 Comet

探讨了常见的 Ajax 技术，包括使用`XMLHttpRequest`对象和用于跨域 Ajax 的跨源资源共享 (CORS)。解释了不同浏览器在实现和支持上的差异，并提供了使用建议。

## 22. 高级技术

深入研究了一些较为复杂的`JavaScript`模式，包括函数柯里、部分函数应用和动态函数。还涵盖了创建自定义事件框架以为自定义对象启用事件支持，以及使用 ECMAScript 5 创建防篡对象。

## 23. 离线应用程序与客户端存储

讨论了如何检测应用程序离线状态，并提供了在客户端机器存储数据的各种技术。从最常支持的特性 cookies 开始，然后讨论了如 Web Storage 和`IndexedDB`等较新功能。

## 24. 最佳实践

探讨了在企业环境中使用`JavaScript`的方法。讨论了更具可维护性的技术，包括编码技巧、格式化和通用编程实践。讨论了执行性能，并引入了几种速度优化技术。最后讨论了部署问题，包括如何创建构建流程。

## 25. 兴起 API

介绍了正在为增强浏览器中的`JavaScript`而创建的 API。尽管这些 API 尚未完成或完全实现，但它们已指在眉睫，浏览器已经开始部分实现其功能。包括对 Web Timing、地理定位和 File API 的讨论。

## 使用本书需要的条件

要运行书中的示例，你需要：

* Windows XP、Windows 7 或 Mac OS X

* Internet Explorer 6 或更高、Firefox 2 或更高、Opera 9 或更高、Chrome 或 Safari 2 或更高

书中的示例源代码可以通过 [www.wrox.com](http://www.wrox.com) 下载。

## 约定

为了帮助你充分利用书中内容并跟踪进度，我们在书中使用了一些约定。

![image](img/cross.gif)

带有警告图标的框包含了与周围文本直接相关的、不容忽视的信息。

![image](img/pen.gif)

铅笔图标表示注释、提示、技巧以及对当前讨论的旁注。

关于文本中的样式：

* 我们在引入新术语和重要词汇时对其加粗。

* 我们这样显示按键组合：`Ctrl+A`。

* 我们在文中这样显示文件名、URL 和代码：`persistence.properties`。

* 我们以两种方式展示代码：

```
大多数代码示例使用无高亮的等宽字体。
我们使用粗体来强调在当前范围内特别重要的代码。
```

列表在标题中包含了文件名。如果只是代码片段，您将在代码注释中找到文件名，如下所示：

```
Code snippet file name
```

![image](img/pen.gif)

由于许多书籍的标题相似，您可能会发现通过 ISBN 搜索是最方便的；这本书的 ISBN 是`978-1-118-02669-4`。

一旦下载了代码，只需使用您喜喜欢的压缩工具将其解压即可。或者，您也可以前往 [www.wrox.com/dynamic/books/download.aspx](http://www.wrox.com/dynamic/books/download.aspx) Wrox 代码下载主页，查看本书以及所有其他 Wrox 书籍的代码。

# 勘误 (ERRATA)

我们尽力确保文本或代码中没有错误。然而，没有人是完美的，错误在所难免。如果您在我们的某本书中发现错误（例如拼写错误或代码故障），我们将非常感谢您的反馈。通过提交勘误，您可能会为其他读者节省数小时的困扰，同时也能帮助我们提供更高质量的信息。

要找到本书的勘误页面，请访问 [www.wrox.com](http://www.wrox.com) 并使用搜索框或标题列表之一找到书名。然后在书籍详情页上，点击`Book Errata`链接。在该页面上，您可以查看所有提交给本书并由 Wrox 编辑器发布的勘误。在 [www.wrox.com/misc-pages/booklist.shtml](http://www.wrox.com/misc-pages/booklist.shtml) 也可以包含每本书勘误链接的完整书籍列表。

如果您在`Book Errata`页面上没有发现“您的”错误，请访问 [www.wrox.com/contact/techsupport.shtml](http://www.wrox.com/contact/techsupport.shtml) 并填写那上的表格向我们发送您发现的错误。我们将检查这些信息，并在适当的情况下向书籍的勘误页面发布消息，并在书籍的后续版本中修复问题。

# P2P.WROX.COM

如需与作者和同行讨论，请加入 [p2p.wrox.com](http://p2p.wrox.com) 的 P2P 论坛。论坛是一个基于 Web 的系统，您可以在其中发布与 Wrox 书籍及相关技术的消息，并与其他读者和技术用户互动。论坛提供了订阅功能，当论坛发布新贴文时，可以通过电子邮件向您发送您感兴趣的主题。Wrox 的作者、编辑、其他行业专家以及您的读者都活跃在论坛中。

在 [p2p.wrox.com](http://p2p.wrox.com) 您将发现许多不同的论坛，这些论坛不仅在您阅读本书时对您有帮助，在您开发自己的应用程序也有帮助。要加入论坛，请遵循以下步骤：

1. 访问 [p2p.wrox.com](http://p2p.wrox.com) 并点击`Register`链接。

2. 阅读使用条款并点击`Agree`。

3. 完成加入所需的信息，以及您希望提供的任何可选信息，并点击`Submit`。

4. 您将收到一封电子邮件，其中说明了如何验证您的账户并完成加入过程。

![image](img/pen.gif)

您可以在不加入 P2P 的情况下阅读论坛消息，但为了发布您自己的消息，您必须加入。



一旦加入，您就可以发布新消息并回复其他用户发布的消息。您可以随时在 Web 上阅读消息。如果您希望将特定论坛的新消息通过电子邮件发送给您，请点击论坛列表中论坛名称旁边的`Subscribe to this Forum`图标。

欲了解有关如何使用 Wrox P2P 的更多信息，请务必阅读`P2P FAQs`以获取有关论坛软件如何工作的问题的解答，以及许多针对 P2P 和 Wrox 书籍的常见问题。要阅读 FAQ，请点击任何 P2P 页面上的`FAQ`链接。

![advert](img/f920-01.jpg)

访问 [www.safaribooksonline.com/wrox1](http://www.safaribooksonline.com/wrox1) 开始

![advert](img/back01.jpg)

# 相关 Wrox 书籍

| ![image](img/back02_01.jpg) | 《使用 HTML 和 JavaScript 开始 iOS 应用程序开发》 ISBN: 978-1-1181-5900-2。希望将现有的 HTML/CSS/JavaScript 技能应用于 iPhone/iPad OS 应用程序开发的初级到中级开发者会喜欢这本书。这本书让熟悉这些核心技术的开发者能够利用他们已有的知识并快速上手。它介绍了使用 Web 技术进行 iOS 开发，解释了如何为 iPhone 和 iPad 启用并优化网站，探索了用户界面设计，然后进入动画、特效、使用 Web 框架进行构建等内容。 |

| ![image](img/back02_02.jpg) | 《入门 PhoneGap》 ISBN: 978-1-1181-5665-0。PhoneGap 是一个开源解决方案，对于想要构建跨平台移动应用而无需学习新语言的 Web 开发者来说是理想的。使用 HTML、CSS 和 JavaScript，让您进入移动世界并为 iPhone、Android 和 BlackBerry 开发应用。 |

| ![image](img/back02_03.jpg) | 《在云端构建移动应用开发》 ISBN: 978-1-1180-3469-9 应用程序市场不断扩大，增加了盈利的潜力。通过本指南，您将学习如何构建由 Amazon Web Services 等云服务支持的跨平台移动应用程序。云应用简介介绍了如何使用 HTML5 创建跨平台移动应用，然后使用云服务增强这些应用。您将学习如何使用 HTML5 构建您的第一个应用并将其部署在云端，同时发现如何利用 jQuery。 |

| ![image](img/back02_04.jpg) | 《使用 JavaScript 和 jQuery 进行专业 XMPP 编程》 ISBN: 978-0-470-54071-8。XMPP 是一种健壮的协议，适用于广泛，包括即时消息、多人聊天、语音和视频会议、协作空间、实时游戏、数据同步和搜索。这本书将教您如何在自己的应用程序中充分利用 XMPP 的力量，并为您提供使用 XMPP 构建下一代应用程序或为您当前的应用程序添加新功能所需的所有工具。书中贯穿了 JavaScript 语言并利用了 jQuery 库，包含了几个复杂度递增的 XMPP 应用，可作为理想的学习工具。 |
