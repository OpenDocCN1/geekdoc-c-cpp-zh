
没有人负责主持协作会话，也没有人负责会话中被操作的代码。相反，每位参与者都是所讨论代码的平等作者和贡献者。如果在会话过程中出现争议，负责该任务的程序员是最终裁决者。

在会话中，所有人都盯着屏幕，所有人都在思考问题。可能有一两个人坐在键盘前，但这些座位在会话期间可能频繁更换。可以把这种会话同时看作现场编码练习和代码评审。

协作会话强度很高，需要大量脑力和情绪能量。在这种强度下，普通程序员大概最多能承受一两个小时，之后就需要抽身去做些消耗较少的事情。

你可能会担心，这样的协作是对人力的低效使用，独立工作的人能比一起工作的人完成更多事情。事实并非如此。对结对工作的程序员进行的研究⁵表明，结对会话中的生产率只下降约 15%，而不是人们担心的 50%。然而，在结对会话期间，结对者产生的缺陷约少 15%，而且（更重要的是）每个功能所需的代码约少 15%。

⁵. 两项此类研究分别是 Laurie Williams、Robert R. Kessler、Ward Cunningham 和 Ron Jeffries 的 “Strengthening the Case for Pair Programming”，*IEEE Software* 17, no. 4 (2000), 19–25；以及 J. T. Nosek 的 “The Case for Collaborative Programming”，*Communications of the ACM* 41, no. 3 (1998), 105–108。

最后两项统计数据意味着，所产出的代码结构显著优于程序员各自独立工作可能产出的代码。

我还没有看到关于群体编程（mobbing）的研究，但轶事证据⁶令人鼓舞。

⁶. 敏捷联盟，“Mob Programming: A Whole Team Approach，” AATC2017，https://www.agilealliance.org/resources/sessions/mob-programming-aatc2017/。

资深程序员可以与初级程序员协作。这样做时，资深程序员会在会话期间被初级程序员拖慢。另一方面，初级程序员在余生中都会因此加速——所以这是一个很好的权衡。

资深程序员也可以与资深程序员协作；只要确保房间里没有武器。

初级程序员也可以与初级程序员协作，不过资深程序员应仔细观察这类会话。初级程序员可能*更愿意*与其他初级程序员一起工作。如果这种情况发生得太频繁，资深程序员就应该介入。

有些人就是不喜欢参与这种协作。有些人在独自工作时表现更好。不应施加超出合理同伴压力的强迫，迫使他们参与协作会话。也不应因为他们的偏好而贬低他们。通常，他们在群体编程中会比在结对编程中更快乐。

协作是一项需要时间和耐心才能获得的技能。在练习很多个小时之前，不要指望自己擅长它。然而，这项技能对整个团队以及每一位参与其中的程序员都非常有益。

## 8 验收测试

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_268_0.png)

在整洁技艺的所有纪律中，验收测试是程序员控制力最弱的一项。要履行这项纪律，需要业务方的参与。不幸的是，迄今为止，许多企业已被证明不愿适当参与。

你如何知道一个系统何时可以部署？世界各地的组织经常通过让 QA 部门或团队“认可”部署来做出这一决定。通常，这意味着 QA 人员运行大量手动测试，遍历系统的各种行为，直到他们确信系统按规范运行。当这些测试“通过”时，系统就可以部署了。

这意味着系统的真正需求*就是那些测试*。需求文档说什么并不重要；只有测试才重要。如果 QA 在运行测试后签字确认，系统就会部署。因此，那些测试就是需求。

验收测试这项纪律认识到这个简单事实，并建议将所有需求*以测试的形式*规定下来。这些测试应由业务分析师（BA）和 QA 团队逐个功能编写，并在每个功能实现前不久完成。QA 不负责运行这些测试。相反，这项任务留给程序员；因此，程序员很可能会将这些测试自动化。

任何心智正常的程序员都不希望一遍又一遍地手动测试系统。程序员会让事情自动化。因此，如果程序员负责运行测试，程序员*就会*将这些测试自动化。

然而，由于测试由 BA 和 QA 编写，程序员必须能够向 BA 和 QA 证明，自动化确实执行了所编写的测试。因此，用于自动化测试的语言必须是 BA 和 QA 能理解的语言。实际上，BA 和 QA 应该能够用这种自动化语言*编写*测试。

多年来，人们发明了多种工具来帮助解决这个问题：FitNesse、<sup>1</sup> JBehave、SpecFlow、Cucumber 等。但工具并不是真正的问题。软件行为的规定始终是规定输入数据、要执行的动作和预期输出数据的简单函数。这就是众所周知的 AAA 模式：Arrange/Act/Assert（准备/执行/断言）。<sup>2</sup>

- 1. fitnesse.org
- 2. 该模式归功于 Bill Wake，他在 2001 年识别出该模式（https://xp123.com/articles/3a-arrange-act-assert）。

所有测试都从准备测试的输入数据开始；然后测试会促使被测动作被执行。最后，测试断言该动作产生的输出数据与预期相符。

这三个要素可以通过多种不同方式规定，但最容易上手的是简单的表格格式。

例如，图 8.1 是 FitNesse 工具中一个验收测试的一部分。FitNesse 是一个 wiki，这个测试检查各种标记手势是否被正确转换为 HTML。要执行的动作是 `widget should render`，输入数据是 `wiki` 文本，输出是 `html` 文本。

**控件应渲染（widget should render）**

| wiki 文本 | html 文本 | |
|---|---|---|
| normal text | normal text | |
| this is ''italic'' text | this is &lt;i&gt;italic&lt;/i&gt; text | 斜体控件 |
| this is '''bold''' text | this is &lt;b&gt;bold&lt;/b&gt; text | 粗体控件 |
| !c This is centered text | &lt;center&gt;This is centered text&lt;/center&gt; | |
| !1 header | &lt;h1&gt;header&lt;/h1&gt; | |
| !2 header | &lt;h2&gt;header&lt;/h2&gt; | |
| !3 header | &lt;h3&gt;header&lt;/h3&gt; | |
| !4 header | &lt;h4&gt;header&lt;/h4&gt; | |
| !5 header | &lt;h5&gt;header&lt;/h5&gt; | |
| !6 header | &lt;h6&gt;header&lt;/h6&gt; | |
| http://files/x | &lt;a href=&quot;files/x&quot;&gt;http://files/x&lt;/a&gt; | 文件链接 |
| http://fitnesse.org | &lt;a href=&quot;http://fitnesse.org&quot;&gt;http://fitnesse.org&lt;/a&gt; | http 链接 |
| SomePage | SomePage&lt;a title=&quot;create page&quot; href=&quot;SomePage?edit&amp;nonExistent=true&quot;&gt;[?]&lt;/a&gt; | 缺失的 wiki 词 |

**图 8.1** FitNesse 工具中一个验收测试的部分结果

另一种常见格式是 Given-When-Then：

单击此处查看代码图像

```
Given a page with the wiki text: !1 header
When that page is rendered.
Then the page will contain: <h1>header</h1>
```

应该清楚的是，这些形式化表示——无论写在验收测试工具中，还是写在简单的电子表格或文本编辑器中——都相对容易自动化。

### 纪律

在这种纪律最严格的形式下，验收测试由 BA 和 QA 编写。BA 关注正常路径场景，而 QA 关注探索系统可能失败的各种方式。

这些测试与它们所测试的功能同时编写，或略早于功能开发。在划分为冲刺或迭代的敏捷项目中，测试在冲刺的头几天编写。到冲刺结束时，它们应该全部通过。

BA 和 QA 将这些测试提供给程序员，程序员以让 BA 和 QA 保持参与的方式将它们自动化。

这些测试成为*完成定义*。一个功能直到其所有验收测试通过才算完成。而当所有验收测试通过时，该功能就完成了。

当然，这给 BA 和 QA 带来了巨大的责任。他们编写的测试必须是被测功能的完整规范。验收测试套件*就是*整个系统的需求文档。通过编写这些测试，BA 和 QA 在确认：当这些测试通过时，指定的功能已经完成并可正常工作。

有些 BA 和 QA 团队可能不习惯编写如此正式而详细的文档。在这种情况下，程序员可能希望在 BA 和 QA 的指导下编写验收测试。中间目标是创建 BA 和 QA *能读懂*并认可的测试。最终目标是让 BA 和 QA 足够适应，从而自己编写测试。
