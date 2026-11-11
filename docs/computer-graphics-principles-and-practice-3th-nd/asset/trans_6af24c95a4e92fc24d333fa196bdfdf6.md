
源自它，但许多章节还有额外材料，以及第2章和第6章的WPF交互实验。

## 致谢

这样一本书由作者写成，但其他人的贡献极大地提升了它。

来自Microsoft的支持和鼓励，尤其是Eric Rudder和S. Somasegar的支持和鼓励，帮助启动并完成了这个项目。

3D测试平台由Dan Leventhal编写的代码演变而来；我们也感谢kindohm.com的Mike Hodnick，他慷慨同意让我们将他的代码作为早期草稿的起点，并感谢Jordan Parker和Anthony Hodson协助处理WPF。

威廉姆斯学院的两名学生为支持本书付出了非常努力的工作：Guedis Cardenas负责参考文献，Michael Mara负责若干章中使用的G3D Innovation Engine；Electronic Arts的Corey Taylor也帮助了G3D。

CMU的Nancy Pollard和匹兹堡大学的Liz Marai都在各自的图形学课程中使用了若干章的早期草稿，并提供了极好的反馈。

Jim Arvo不仅是与渲染相关一切问题的权威，还帮助重新构建了第一作者对该领域的理解。

除了刚才提到的部分人之外，还有许多其他人阅读了章节草稿、准备了图像或插图、建议了主题或呈现方式，或以其他方式提供了帮助。按字母顺序，他们是John Anderson、Jim Arvo、Tom Banchoff、Pascal Barla、Connelly Barnes、Brian Barsky、Ronen Barzel、Melissa Byun、Marie-Paule Cani、Lauren Clarke、Elaine Cohen、Doug DeCarlo、Patrick Doran、Kayvon Fatahalian、Adam Finkelstein、Travis Fischer、Roger Fong、Mike Fredrickson、Yudi Fu、Andrew Glassner、Bernie Gordon、Don Greenberg、Pat Hanrahan、Ben Herila、Alex Hills、Ken Joy、Olga Karpenko、Donnie Kendall、Justin Kim、Philip Klein、Joe LaViola、Kefei Lei、Nong Li、Lisa Manekofsky、Bill Mark、John Montrym、Henry Moreton、Tomer Moscovich、Jacopo Pantaleoni、Jill Pipher、Charles Poynton、Rich Riesenfeld、Alyn Rockwood、Peter Schroeder、Francois Sillion、David Simons、Alvy Ray Smith、Stephen Spencer、Eric Sudderth、Joelle Tollet、Ken Torrance、Jim Van Dessel、Daniel Wigdor、Dan Wilk、Brian Wyvill，以及Silvia Zuffi。尽管我们尽了最大努力，可能还是遗漏了一些人，谨向他们致歉。

我们在写作过程中得到了竞争书籍作者的大量支持，这体现了这个领域普遍的善意。Eric Haines、Greg Humphreys、Steve Marschner、Matt Pharr和Pete Shirley都为把本书变得更好作出了贡献。能与这样的人共事于这个领域，真是太好了。

如果没有我们的编辑Peter Gordon的支持、宽容、包容和远见，我们绝不可能完成本书。我们也都感激家人在整个项目期间给予的巨大支持。

## 致学生

你的教授可能会选择本书的某种阅读路线，挑选彼此契合的主题，或许会遵循前面提到的某条建议路线。不要让它限制你。如果你想了解某个主题，就利用索引开始阅读。有时你会发现自己缺乏背景知识，无法理解所读内容。当这种情况发生时，就去阅读背景材料。这会比在其他时候读更容易，因为现在你有一个学习它的*理由*。如果你卡住了，就在网上搜索别人的实现，下载并运行它。当你注意到它看起来不太对劲时，就可以开始检查这个实现，并尝试逆向工程它。有时这是理解某个东西的绝佳方式。遵循实践—理论—实践的学习模式：先尝试某件事，看看能否让它运行起来；如果不行，就去阅读别人是怎么做的，然后再试一次。第一次尝试可能令人沮丧，但它能让你在接触理论时更好地理解理论。如果你无法让自己遵循实践—理论—实践模式，至少应该花时间完成所读章节中的内联练习。

图形学是一个年轻的领域，年轻到本科生经常成为SIGGRAPH论文的合著者。一年之内，你就能学到足够的知识，开始贡献新的想法。

图形学也使用大量数学。如果数学对你来说一直显得抽象而理论化，图形学可以真正有所帮助：数学在图形学中的用途是实际的，而且你常常可以在自己制作的图片中*看到*某个定理的后果。如果数学一直对你来说很容易，你可以尝试把我们提出的思想进一步扩展，从中获得一些乐趣。虽然本书包含大量数学内容，但它只触及现代研究论文中所用数学的表面。

最后，*怀疑一切*。我们已尽力在本书中讲述我们所理解的真理。我们认为自己做得相当不错，我们所说的绝大部分都是真的。在少数地方，我们在引入某个概念时故意只讲了部分真相，然后在后面讨论细节的章节中再加以补充。但除此之外，我们在其他地方肯定也有未能讲述真相之处。在某些情况下，我们只是犯了错误，比如漏掉一个负号，或在循环中犯了一个差一错误（off-by-one error）。在其他情况下，图形学界当前的理解还不够充分，我们相信了别人所说的话，之后将不得不调整我们的看法。这些错误对你来说是机会。Martin Gardner说过，科学发现真正的声音不是“啊哈！”，而是“嘿，*那可真奇怪*……”所以，如果偶尔有东西让你觉得奇怪，尽管去怀疑它。更仔细地研究它。如果它最终是真的，你就清除了一些理解上的蛛网；如果它是假的，那就是你推动这个领域前进的机会。

## 致教师

如果你和我们一样，你很可能读了“致学生”部分，尽管它不是为你写的。（你的学生可能也在读这一部分。）你知道，我们建议他们随意翻阅本书，并怀疑一切。

除了本前言其余部分的建议之外，我们向你推荐两件事。第一，鼓励甚至要求学生回答书中的内联练习。对于说“我要做的事太多了！我不能浪费时间停下来做练习”的学生，你只需说：“我们没时间停下来加油……我们已经迟到了。”第二，给学生布置既有固定目标又有开放式部分的项目或作业。踏实的学生会完成固定目标部分，并学会你想讲授的材料。其他人一旦有机会做有趣的事，可能会用开放式练习做出让你惊讶的东西。而在这样做时，他们会发现需要学习一些可能看似*刚好*超出能力范围的东西，直到突然掌握它们，并获得能力感。图形学是做到这一点的绝佳媒介：成功立即可见且令人有成就感，这就形成了一个促进进步的反馈循环。可见反馈与他们在计算机科学其他领域遇到的可扩展性思想相结合，可能会带来启发。

## 讨论与延伸阅读

本书大多数章节都包含像这一节这样的“讨论与延伸阅读”部分，指向背景参考文献或本章思想的高级应用。对于本前言而言，唯一合适的延伸阅读非常笼统：我们建议你立即开始浏览ACM SIGGRAPH会议以及其他图形学会议（如Eurographics和Computer Graphics International）的论文集，并根据你不断变化的兴趣，查看一些更专门的会议，如Eurographics Symposium on Rendering、I3D和Symposium on Computer Animation。虽然起初这些会议中的论文似乎依赖大量先验知识，但你会发现，你很快就能了解哪些事情是可能的（哪怕只是通过看图片），以及实现它们需要哪些技能。你还会迅速发现一些在你最感兴趣领域中反复出现的想法，这可以在你学习图形学的过程中帮助指导你的进一步阅读。
