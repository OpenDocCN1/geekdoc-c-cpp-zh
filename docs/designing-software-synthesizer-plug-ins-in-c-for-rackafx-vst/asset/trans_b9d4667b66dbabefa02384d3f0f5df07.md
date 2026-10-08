
第 9 章是书中的转折点，因为所有的底层合成器 C++ 对象都在代码中设定，且将不再更改。在这里，你设计了 MiniSynth——一种模拟建模合成器。如果你愿意，可以偏离书籍，实现你自己的合成器语音对象和模型编码。在第 10 章中，你将学习如何使用音频文件导入 DigiSynth，这是一种立体声播放合成器。第 11 章矢量合成使用了 Vector 项目中基于样本的振荡器，并包含一个额外项目 AniSynth，它是对 Moog Anisynthhesizer Android 应用的解读。在第 12 章中，你设计了一个 Yamaha DX100 FM 合成器的克隆版本。第 13 章是音频效果章节，向你展示如何为 MiniSynth 添加延迟效果，从而极大地扩展你的合成器功能。简要附录向你展示如何将 VST 和 AU 模板转换为项目的基础代码（如果 RackAFX 为你创建了项目，则不需要这样做）。

有两个人对本书的早期产生了巨大影响——Bill Jenkins 和 Andy Lear，他们都是 K 研究开发部门的高级工程师，也是原始提案的评审员。Bill 的评论和建议塑造了 C++ 代码的呈现方式，并使其尽可能与描述性文本交织。事实上，他正是不同的 API 在单独章节中编码，而不是像提案中那样混合在一起的原因。英语中没有一个单词可以描述对 Andy 在理论章节（4–8 章）中投入的感激之情。他是这些章节中许多算法的专家，他的投入是无价的。Andy 还反复校对了了章节，提供了源源不断的灵感。模拟的 MiniSynth 对我来说听起来极棒，这很大程度上归功于 Andy 的投入。Bill 和 Andy——感谢你们！

我的教授和学生们也对这项工作充满热情，我得到了同事 Dean Shelby、Serona Elton、Rey Sanchez、Colby Leider、Joe Abbatti 和 Chris Bennett 的全力支持，包括在我在音乐工程论坛（Music Engineering Forum）课程糟糕的缺勤记录中给予宽限。尽管我从 20 世纪 90 年代就开始教授合成器课程，但直到四年前学生才开始使用 RackAFX。最后几代音乐工程专业的学生无论他们是否知晓，也塑造了书的内容和 RackAFX 软件。去年，Colin Franks 和 Mark Gill 改进了几个合成器组件的稳定性能。Rob Reinh 翻新了 GUI 元素。我还需要感谢学生在去年合成器课程中的投入和帮助（按字母顺序）：Daniel Avissar、Andy Ayers、Daniel Bennett、Garrett Claussen、Sammy Falcon、Michael Intenda、Connor McCullough、Tac Nicol、Crispin Odomn、Andrew O'Neil-Smith、Ross Penniman、Michael Tony 和 Francisco Valencia Otalvar。

你可以通过加入网站论坛 http://www.willpirkle.com/synth/ 与我保持联系，那里包含了书中未涵盖的信息和资源。像往常一样，我鼓励向我发送你的作品或在论坛发布链接。作为我的最后一本书，我迫不及待想听听你在插件开发中出了什么花样！

祝好，
Will Pirkle
2014年6月1日

# 前言

以下关于书籍项目和惯的一些说明。

# 技能

基础的 C++ 编程技能都是用 C++ 编写的。如果你上过该主题的一两门大学课程，应该没有问题。在 API 中，你需要完全精通 Visual Studio 编译器，并且需要知道如何向项目添加文件、使用过滤器重新排列源文件以及使用调试器。如果你想设计 GUI，你需要精通 AppKit 和 CoreAudio 等框架；同样，你需要了解 InterfaceBuilder 和 Xcode。

# 匈牙利命名（Hungarian Notation）

99% 的 RackAFX 和 VST 代码是使用匈牙利命名的。大部分 AU 代码也使用了它（部分来自 Apple 公司）。以下是微软对匈牙利命名的描述：很久在 DOS 早期，微软首席架构师 Charles Simonyi 引入了一种命名规范，在标识符名称前添加前缀以指示其功能类型。该系统在微软内部被广称为“匈牙利命名”，因为前缀让变量名看起来有点像是用非英语语言编写的。事实证明，匈牙利命名非常有用——它是许多技术中一种能帮助程序员编写出更好代码的技术。由于过去 15 年发布的大多数头文件和文档都使用匈牙利命名标识符，因此最重要的出版物是几乎每个 Windows 程序员读的第一本书（Simonyi, 1999）。

# 合成器项目

在本书过程中，你将从任何 API 开发六个项目。代码被分为每个 API 的章节。章节遵循相同的思想呈现顺序，你可以先读理论部分，然后跳到包含你目标平台的章节。这些项目的设计允许你衍生出许多你自己的变体。以下是合成器项目及其包含的组件列表：

| 项目 | 振荡器 | 滤波器 | | | |
| :--- | :--- | :--- | :--- | :--- |
| NanoSynth | 模拟建模 (BLEP) | Moog Ladder | 通用 LFO | 组合 Amp-EG, Filter-EG, Pitch-EG |
| MiniSynth | 模拟建模 (BLEP) | Moog Ladder | 通用 LFO | 组合 Amp-EG, Filter-EG, Pitch-EG |
| DigiSynth | 样本播放 | Oberheim SEMF | 通用 LFO | 组合 Amp-EG, Filter-EG, Pitch-EG |
| VectorSynth | 样本播放 | Korg Lowpass | 通用 LFO | 组合 Amp-EG, Filter-EG, Pitch-EG |
| AniSynth | 样本播放 | Diode Ladder | 通用 LFO | 组合 Amp-EG, Filter-EG, Pitch-EG |
| DxSynth | 波形表 | 无 | 通用 LFO | FM EGs |

# 延迟效果 (Delay FX)

第 13 章中的延迟效果套作为示例添加到 MiniSynth 中，但也可以很容易地添加到任何合成器中，鼓励你在所有合成器中实现效果。

# 参考文献

Simonyi, Charles. 1999. "Hungarian Notation." 2014年8月访问。 http://msdn.microsoft.com/en-us/library/aa26976vs.aspx

# 第 1 章：合成器基础

合成器通常被模糊地定义为一种产生并控制声音的电子仪器。在与同事讨论此时，我们同意这个定义的密度可能具有限制性。为什么迪杰鲁（didgeridoo）或口琴不能被称为合成器呢？事实上，难道没有人声不是合成器吗？将美国发明家 Thaddeus Cahill 视为现代合成器的发明者。1897年，他为 Telharmonium 或 Dynaphone 申请了专利，这是一种使用蒸汽动力电机合成正弦波的仪器——它甚至是复声的（能够同时播放多个音符）。Leon Ther 在1919年发明了明琴（Theremin），它包含一个控制正弦波振幅和音高的无接触接口。与 Telharmonium 不同，明琴使用电子放大器重现声音而不是声学喇叭。然而，发明者创造了独特的仪器，如 Ondes Marten、Trautonium 和 Mixtartonium 等。合成器（synthesizer）一词的首次使用是在1929年的 Complexplex Synthesizer。RCA 标记了使用调音叉控制振荡的电子音乐合成器。1957年，Max Mathews 实验使用计算机渲染和控制音频信号，而 Robert Moog 普及了硬件，并被认为在1963年发明了第一台电压控制合成器。他的发明包括 Moog 阶梯滤波器，我们将在第7章中研究它。1967年，他销售了可以连接到系统中以产生各种声音的电子模块——他把这些称为合成器。这些合成器的驱动力不是电子音乐，而是20世纪的新古典音乐作曲家。关于作曲家与电子工程师之间关联的文章并不少见，例如 Moog 与作曲家 Herbert Deutsch 合作，Donald Buchla 与作曲家 Morton Subotnik 和 Ramon Sender 合作创作先锋派。Sergio Franco 和 Ken Pohlmann 在70年代与作曲家 Salvatore Martini 合作，开发了如图1.1所示的 SAL-MAR 结构。

Moog 的合成器由各种组件组成，每个组件都有自己的电路板、旋钮、灯和接口。振荡器产生原始波形——正弦波、锯齿波和方波。放大器使用电压控制放大器修改信号振幅。滤波器实现各种基本功能，如低通和高通类型。包络发生产生变化的输出值，用于控制其他模块的振幅或滤波。以各种方式组合模块产生最有趣的声音；结果在某种程度上大于部分。Moog 的每个模块都有自己的输出，控制插座使用音频跳线线连接在一起，这种做法在录音室被广泛采用。这就是 patch（跳线）一词的起源，我们经常使用它。一个 patch 是连接和设置每个模块参数以形成特定声音的配方。在合成器周围，你会经常听到 patch cord patch patch patch 这些词。

