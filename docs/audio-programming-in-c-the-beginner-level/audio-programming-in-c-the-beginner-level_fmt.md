
# C++ 音频编程入门指南

![](img/a70fd31fb441a0a03339261d9cdc8e0f_1_0.png)

献给我周围所有的朋友。你们知道自己是谁。

# 引言

欢迎阅读音频编程初级书籍。在本书中，我们将学习不同的合成类型（至少是常见的类型），并通过示例代码进行学习。所有的示例代码都使用 `C++20` 编写，并使用 `Clang` 作为编译器和链接器。你可以在附录 A 中找到所有的代码以及如何编译和链接。编译完成后，可以通过在程序名前加上 `./`（点斜）来运行程序。

虽然这本书是关于 `C++20` 音频编程的，但我们建议购买硬件或构建模块以更好地理解软件方面。特别是虚拟模拟合成，即在硬件单元中仿真组件。模块化合成器是我推荐的，我知道它可以扩展来构建自己的。使用 `VCV Rack` 等软件而不是自己制作也是一种选择，尽管主要针对声音，对硬件帮助不大。

# 为什么选择 C++20?

嗯，你可能可以使用 `C++17` 编译并运行示例。但由于 `C++20` 是最新标准，因此应该使用它。当 `C++23` 发布时，本书将会更新以支持该标准（如果需要）。

# 那么合成的定义是什么？

这个词仅在两个主要语境中使用：化学化合物的创造和电子声音的产生。

有许多类型的合成。例如纹理合成器、视频合成器、色彩合成器和语音合成器。这些在书中都不会讨论。

剑桥词典对“合成”的定义是：“将不同的想法或事物结合，形成一个与单独考虑这些项目时不同且新的整体”。

# 引言

在本书中，“合成”（Synthesis）指的是声音合成，即产生声音的过程。我们既可以通过产生现有的声音来复用这些声音，也可以通过电子或机械方式产生声音。声音合成可以使用数学、物理学甚至生物学；它将音乐技巧与技术专家相结合，把艺术与科学融合在了一起。

# 第一台合成器是什么？

1896年，特尔哈莫琴（Telharmonium）问世，并于1897年获得专利。特尔哈莫琴也被称为动力响琴（Dynamophone），它使用音轮通过加法合成（Additive synthesis）将音乐声产生为电信号。

特尔哈莫琴的发明者是塞德斯·卡希尔（Thaddeus Cahill），他是提摩西·卡希尔博士（Dr. Timothy Cahill）和艾伦·卡希尔（Ellen Harrington Cahill）的长子，两人都是爱尔兰的移民。塞德斯于1867年6月18日出生于美国爱荷华州。他在俄亥俄州奥伯林的奥伯林音乐学院学习了音乐物理学。他毕业于哥伦比亚法学院。在贝尔公司拒绝让他使用电话仪器进行实验后，塞德斯在13或14岁时就开始发明东西。

18岁时，他发明并专利化了一种用于打字机的机器。1893年，26岁的他产生了一个新想法。这个想法是利用电动力学来构建清晰的音色作为乐器。这样的发明将取代钢琴、管风琴和小提琴，成为首选乐器。钢琴无法保持调。此外，单音或和弦的音量会丢失。管风琴在这些方面更好，但表现能力有限。小提琴没有这些问题，但它的和弦能力很小。卡希尔的想法将发现并甚至有力量将音乐传输到任何可以传输的地方。通过电话网络，卡希尔可以从中心站将音乐传输到成千上万个地方。

卡希尔希望特尔哈莫琴的音乐可以通过电话线广播到酒店、餐厅、剧院甚至家庭。

他制作了三个版本：第一个版本重7吨。第二个和第三个版本重210吨。每一个版本相对于其前代的功能都有重大的进步。特尔哈莫琴的价格昂贵，达20万美元（约合今天的551.4万美元）。

特尔哈莫琴的表演在第39街和百老汇交叉口的“特尔哈莫大厅”举行。马克·吐温（Mark Twain）是他观众的欣赏者。

特尔哈莫琴在许多方面预示了现代电子音乐。例如，它的声音输出形式是将普通的电话接收器连接到大型纸锥上——这是扬声器的原始形式。卡希尔闻著名，他认为电磁振膜是输出其独特声音最可能的手段。遗憾的是，目前没有发现用特尔哈莫琴制作的音乐录音。

电话音被描述为“清晰而纯净”——指的是它能够产生的电子正弦波音。然而，它并不限于此类简单的声音。乐器的每个音色对应一个音符，为了扩大它的可能性，卡希尔增加了几个额外的音轮来为每个音符增加泛音。这结合类似于管风琴的音栓、多个键盘以及许多脚踏，意味着每个声音都可以被雕塑和重塑 —— 该乐器以其复制普通管响乐木管乐器（如笛子、巴松管、单簧管）以及大提琴声音而闻名。特尔哈莫琴。

卡希尔先生的特尔哈莫琴公司于1914年破产。

塞德斯·卡希尔于66岁去世（1934年4月12日于美国纽约市）。最后被报废的特尔哈莫琴是1962年的7吨版本。

# 什么是声音？

声音是空气分子连续且规律的振动，当它们到达人的耳朵时会被听到。

空气分子是组成空气的分子，包括氧气和氮气颗粒。空气是物质，尽管它是不可见的，但它不断影响着我们周围的世界。

音频可以通过扬声器和耳机制作。声音以压力波移动。当空气分子被足够压缩和稀薄时，我们就听到声音。我们听到的声音“频率”越高越高。当扬声器前后移动时，它推动空气改变空气压力并产生声波。

扬声器的工作原理是将电能转换为机械能（运动）。机械能压缩空气并将运动动为声能或声压级（SPL）。

这使得音圈连接并前后移动。这种往复运动在空气中产生压力波，我们将其感知为声音。

频率响应是指扬声器输出在不同频率下的响度。频率响应的典型测试是发送从低音到中频，再到高频范围的频率扫描，以查看扬声器的声音在所有区域是否相同。扬声器的理想频率响应是非常平坦的。这意味着扬声器在低频时的水平与在中频或高频时相同。

将计算机连接到数字设备非常简单。然而，当涉及模拟设备（扬声器、耳机或麦克风）时，接口变得复杂得多。需要的是电子地将模拟信号转换为数字（二进制）量子，反之亦然。

对于模拟信号的输入，使用模拟数字转换器（`ADC`）。对于扬声器或耳机（如果不是内置的），则使用数字模拟转换器（`DAC`）。

# 引言

`ADC`将模拟电信号（电压或电流）输入并输出二进制数。

另一方面，`DAC`输入二进制数并输出模拟电压或电流信号。

# 什么是音色？

音色（Timbre），也称为 timber，是由声波产生的听觉质量。

音色取决于声音的波形。该乐器的每个音色对应一个音符，为了扩大它的可能性，卡希尔增加了几个额外的音轮来为每个音符增加泛音。这结合类似于管风琴的音栓、多个键盘以及许多脚踏，意味着每个声音都可以被雕塑和重塑 —— 该乐器以其复制普通管响乐器木管乐器（如笛子、巴松管、单簧管）以及大提琴声音而闻名。特尔哈莫琴。

卡希尔先生的特尔哈莫琴公司于1914年宣布破产。

音色是由声波产生的听觉感受。

音色取决于声音的波形。

音色取决于其泛音。音色是清晰且纯净的，因为存在不同的泛音。

音色取决于乐器的形状、频率范围，并取决于声音的包络。

# 书中的合成章节

这是一本面向初学者的书籍，旨在正如生活中的许多事情——我们需要学习如何

- 加法合成
- 减法合成
- 泛音合成
- 颗粒合成
- FM频率调制合成
- 扫描合成
- 矢量合成
- 虚拟模拟合成
- 物理建模

`ADC`将模拟电信号（电压或电流）输入并输出二进制数。

另一方面，`DAC`输入二进制数并输出模拟电压或电流信号。

## 乐器的物理学

乐器以各种方式进行分类，其中某些相互重叠。中国人将它们分为三大类：气鸣、弦乐和打击乐。这种分类在中世纪被保留，并持续了几个世纪：增加了电子乐器。

### 弦乐

毕达哥对拨动不同长度弦产生的音进行了实验。他发现某些弦比例产生了悦耳的组合（和声），而另一些不是。通过他的仔细观察，毕达哥确定了形成今天使用的主要泛音系统的频率和音符之间的距离。

泛的数学结构从单个自然产生的开始，它包含了一系列额外的频率（“泛音”），我们在意识层面并察觉不到。在这个泛或泛音序列中，频率之间存在数学关系——它们是彼此的倍数。例如，如果最低频率（“基音”）是 `100 Hz`，那么泛音就是 `2 x 100 (200 Hz)`、`3 x 100 (300 Hz)`以此类推。

毕达哥观察到的最显著音程凸显了他的发现的普遍性。`2:1`的比例是另一个速率的两倍，第一个音认为比第二个音高一个八度，但有趣的是这些音通常被感知为几乎相同。例如，女性的声音可能在 `220赫兹` 左右，而男声大约是 `110赫兹`。然而，如果他们一起唱歌，听起来就像他们在同声齐唱同一个旋律，尽管它们实际上相差一个八度。这个八度。

### 弦、管和打击乐器的物理学

尽管世界各地的音乐文化多样，但它是所有记录在案的音乐系统的基础。

### 管

管乐器是管内振动的空气柱。如上所述，弦乐被拉伸在两点之间，并倾向于以特定的频率振动，这些频率被称为泛波（Harmonics）。我们注意到，二谐波的振荡频率是基频的两倍，而三谐波是基频的三倍。在理论上，完美的拉伸弦可以产生从 1 到无穷的完整泛波序列，但在现实中并非如此。

每根振动弦的振幅将决定产生的音频波形形状。如果任何泛波 `n` 的振幅是基频的 `1/n`，我们就得到锯齿波。或者，如果任何奇数泛波 `n` 的振幅是基频的 `1/n`，但缺少所有偶数泛波，我们就得到方波。

没有悬浮在真空中的开口管内部有一个空气柱。看起来空气可以在没有任何任何特殊处理的情况下进入和离开。但是，如果你向这种管子的顶部吹气，它将产生一个悦耳的音符。你可以假设其内部的空气以产生泛波序列的方式进行振荡。

通过向管子的一端吹气，你在一端产生了一个高压脉冲。高压脉冲穿过管子直到远端，此时大部分能量被反射回管内。它从一个无形的墙上反弹。这种来回的弹弹将一直持续到所有能量耗尽为止。

管子产生泛波序列的原因与弦的原因相似。弦必须固定在两端才能发生泛波运动，这被称为边界条件。管子具有类似的条件。管子外的大气压力必须与内部相同。因此，通过正确的吹气方式——管内的最大正压将出现在中心，而那里是反射脉冲的最大负压处。这些就是驻波发生的条件。管乐器的基频波长是管子长度的两倍（它必须来回复地运动）。

所以，如果管子的长度为 `0.34 米`，考虑到声速为每秒 `340 米`，管子内的脉冲将在千分之一秒内（`1 毫秒`）走完整个管子。然后脉冲将返回，这也需要几千分之一。因此，周期为 `2 毫秒`，基频频率为 `500 Hz`。

向空气柱提供能量并维持管内驻波的方法是通过吹嘴。通过吹嘴形成了一股压力脉冲流。吹嘴周围的唇部像阀一样工作，产生高压空气的短脉冲。如果这些脉冲的时机与管子的长度（波长）匹配，就会产生音符。时机由唇部张力的变化和口中气压的调节调节。

内导流笛器（如竖笛）产生更多锯齿波或三角波，而带有单簧哨口的木管乐器（如单簧）则更像方波（“空灵”的声音）。

管子和弦的相似之处还在于，两者都可以形成锯齿波和方波。

### 打击乐

弦和管乐器更多是一维振荡器（弦拉伸在两点之间，管乐器是带有振动空气柱的管子）。

鼓皮有两个维度，因为它是一个圆形膜，在所有点上以相同的张力拉伸，并在圆周周围的所有点上固定。鼓是与弦和管乐器不同类型的振荡器。描述振动膜的方程相当复杂，比弦和管乐器更难合成。

振动圆形膜的基频是通过恰好击中鼓皮中心激发的（这被称为膜的 `w01` 模式）。

如果你在中心之外击打鼓皮，膜将以完全不同的方式振动，让事情变得更加复杂。

要得到第二谐波、第三谐波等，你不能像弦那样得到正好是基频频率倍数的泛波。通过使用贝塞尔函数（Bessel function），我们可以相对于基频计算 `w02` 和 `w03`，从而得到第二三谐波。

其他因素是膜表面的张力。所有这一切使得鼓真的很难很好合成，这就是为什么使用鼓的采样或真实鼓的录音。

### 加法合成

在加法合成中，你从零开始，通过组合不同电平和、频率的正弦波来构建声音。随着更多正弦波的组合，它们开始产生额外的泛波。在大多数加法合成器中，每组正弦波被视为和使用类似于振荡器一样。

取决于你所使用的加法合成器的复杂程度，你将对每个正弦波的电平和和音进行单独包络控制，或者你将限于对一组正弦波进行包络控制。

在实践中，与一组相关的泛波一起工作是处理它们之间数学关系以及在批量调整时这种调整对整体音色影响的最佳方法，而不是逐个调整。

加法合成应被视为减法合成的反向方法。

真正的合成器将允许我们单独操纵 `32`、`64`、`128` 甚至 `256` 个泛波的振幅，这是任何预设的模拟合成器都无法做到的。这就是为什么……

### 使用 KAWAI K5 进行加法合成

KAWAI K5 合成器 1987 - 音色预设演示（无旁白，仅演奏）80 年代复古合成器

> https://www.youtube.com/watch?v=jXJQBL3iPdo

### 减法合成

减法合成基于这样一个核心理念：真实的乐器可以分为三个主要部分：声源、调制器（处理声源的输出）以及一些控制器（作为表演者与乐器之间的界面）。这在许多乐器中表现得最为明显，其各个部分可以被单独观察。

合成方法之间存在许多差异，但大多数遵循从根本上相似的架构和信号流，这是基于减法合成原理的。

根据传说，米开朗基罗被问及是如何从一块石料中雕刻出大卫像的，他回答：“我只是切掉了所有看起来不像大卫的部分。”

从本质上，这就是减法合成的工作原理。你过滤掉或切掉你不想听的声音部分。换句话说，你减去了频谱中的部分频率，这些频率由基音和相关的泛波组成。

减法合成假设可以用一个简单的振荡器来模拟声乐器，该器可以产生具有不同频谱的波形。信号从振荡器发送到滤波器，滤波器代表了乐器内部随频率变化的损耗和共鸣。经过过滤（或未过滤）的信号通过合成器的放大部分随时间进行塑造。

理论上，通过以类似于你试图模仿的乐器的自然行为组合这些组件，可以重建真实乐器独特的音色、音准和音量特征。

事实上，减法合成器在模拟真实世界乐器方面并不完美。没有任何一种合成单簧会被误认为是真实的单簧。减法合成真正的强大在于，它本身就能提供一种独特的音色组合。

滤波器的种类不多，但大多数依赖于两种关键滤波器——低通滤波器（`LPF`）和高通滤波器（`HPF`）。

低通滤波器允许低频通过，切断高频并产生低音。高通滤波器则相反。转动 `CUTOFF`（截止频率）旋钮会移动滤波器开始作用于声音的点。

滤波器并不是突然停止声音，而是从原始音量开始倾斜下降。斜率的单位是每倍频分贝（`dB`），这就是为什么你会在合成器上看到 `-12dB` 或 `-24dB` 滤波器。数字越高，滤波器的陡度和强度越强。

除了 `Cutoff` 外，滤波器的另一个关键部分是共鸣（Resonance）。大多数滤波器都有共鸣或 `Q` 控制。当与截止频率相同范围的声音被路由回滤波器时，就会产生共鸣。在极高水平下，这种反馈会引起滤波器自振荡并产生正弦波。增加共鸣会导致截止频率周围的音色更亮、更刺耳，并可用于多种技术，包括让合成器“尖叫”或创建经典的波形效果。

虽然较少常见，但你有时也会遇到带通滤波器（Bandpass）和带阻滤波器（或陷波滤波器 Notch）。带通滤波器是高通和低通的结合，只留下音频的中间部分不经滤波。带阻滤波器相反，留下高频和低频不经滤波。

减法合成使用不同类型的振荡器，有些比较“轻”，有些比较“暗”。主要的振荡器类型有：正弦波、锯齿波、方波和三角波。

正弦波是最基本的波形之一。它的边缘平滑，像池塘里的涟漪一样，没有剧烈的变化。这产生平滑、柔和的声音。正弦波常用于重建管乐声音，如笛子或管风琴，或平滑的铺垫音（pads）。

锯齿波因其看起来像锯齿而命名。锯齿波具有非常尖锐的顶点和突然的变化，创造出强烈的“嗡嗡”声。因为这个原因，锯齿波形具有规律间隔的泛波频率，这些频率逐渐减小。正是这些泛波频率让锯齿波听起来丰富且饱满，非常适合强大的合成贝斯和主奏音（leads）。

方波的声音含有丰富的泛波，不像锯齿波那样“嗡嗡”，但也没有正弦波那样平滑。它们拥有与锯齿波一样泛波频率，每两个周期重复一次。方波是一种特殊的脉冲波。正如名称所示，信号在开启和关闭之间切换。脉冲波常用于脉宽调制（`PWM`），这在早期合成器中用于模拟两个振荡器之间的相互作用。方波通常被描述为听起来“空灵”或有“鼻音”。这意味着它们非常适合创建风乐器，如单簧管。

三角波位于方波和正弦波之间。类似于方波，它们包含原始频率的奇次泛波。然而，这些泛波的值下降得更快。这使得波形看起来和听起来都更接近正弦波，但仍然保留了方波的一些“嗡嗡”特质。

在加法合成部分，我们提到过 `Envelope.hpp` 使用了 `ADSR` 包络。`ADSR` 代表攻击（Attack）、衰减（Decay）、持续（Sustain）和释放（Release）。包络是决定你想创造什么声音的关键。例如，考虑一下鼓声和小提琴声的区别。

鼓声的音量有尖锐、突然的增加（Attack），几乎没有持续（Sustain），且释放（Release）时间很短。小提琴有较长、缓慢的攻击，逐渐达到最大音量，有很长的持续（Sustain），且声音缓慢减弱。

包络不仅适用于放大器，许多合成器在滤波器或音高上也有包络。如果你使用模块化合成器，可以为喜欢的几乎任何参数设置包络。例如，在滤波器包络上，放大器的工作类似于你随时间转动截止频率旋钮，逐渐调大再调小。

为了让声音动起来，会使用 `LFO`。`LFO`（低频振荡器）顾如其名。它是另一个振荡器，波形与我们在本文之前提到的波形相似。然而，它的频率非常低，以至于你听不到。

与其使用 `LFO` 来产生音调，你可以使用它来操纵其他参数。把它想象成自动旋转旋钮。`LFO` 有一个速率（Rate）控制来改变其振荡速度，以及对合成器上每个影响参数的深度（Depth）控制。这些控制允许你设置 `LFO` 以变变化的幅度和正反方向来切换所选的参数。

许多合成器包含控制按钮，可以将 `LFO` 设置为音高（产生颤音 Vibrato）、音量（产生颤音 Tremolo）或滤波器截止频率。

### 使用 Sequential Circuits 设备进行减法合成

Prophet 5

Sequential Circuits Prophet 5 Sounds³

https://www.youtube.com/watch?v=YHNRR01xK68

### 共振峰合成 (Formant Synthesis)

共振峰是声学中最难理解的概念之一。它们是由你的声道、喉咙和嘴部形状所放大的频率范围，这些形状赋予了你声音独特的特征，并负责产生元音（A, E, I, O, U）。

从理论上讲，人声会产生无限数量的共峰。只有四个或五个共峰与我们的听觉有关。更高的频率超出了人类听力范围。重要的是前两个共峰，即最低的两个。这两个是负责元音音的共峰，而第三个及以上的共峰则负责音色或你声音的色彩。

即使在低语时，你声音中的共峰频率也是相同的。通过吹气噪声通过声带（vocal folds）发出声音时，最低的两个共峰频率是相同的。

声码器（Vocoder）的工作原理是从你的声音中提取共峰，并将其添加到合成器的声音中。共振峰合成通过使用共振峰滤波器，向合成声音添加最低的四五个元音峰值，使其能够说话。



我们都通过空气流过声带来产生具有确定基频和多个泛波的音高信号。我们都可以收紧和放松这些声带来改变信号的音高。此外，我们都能产生语音噪声。音高产生在声喉深处，因此它们必须通过我们的喉咙、嘴巴和鼻孔。和其他任何空腔一样，这个“声道”表现出共振模式，增强某些频率的同时抑制其他频率。换句话说，人类语音系统由一个频率控制振荡器、一个噪声生成器一组带通滤波器组成。声道的共振及其产生的频谱峰值被称为“共峰”（formants），这个词源于拉丁语“formare”，意为“形状”。

测量和声学理论已经证明，这些共峰的中心与解剖属性有关，例如构成声道的空气管的长度和截面积。由于较长的管基频比较短的管低，因此可以合理地假设成年男性的声音比成年女性或儿童更深沉。

基于共振峰合成的合成器示例是 `Yamaha FS1R`。

## 在 C++ 中实现共振峰合成

`03-formant.cpp` 代码示例非常直观。它将根据 `generate formant` 函数中的 Formant 1 和 2 表格生成元音声音。

## 使用 Yamaha FS1R 实现共振峰合成

Yamaha FS1R | 隐藏的宝藏！¹⁴

> *https://www.youtube.com/watch?v=UI-V48lpbQ

## 颗粒合成 (Granular Synthesis)

颗粒合成的基本原理是声音可以被分解为微小的粒子，称为“颗粒”（grains）。在许多方面，颗粒合成与波表合成相似，但它的工作尺度精细得多。这种方法非常适合不断演变的声音和独特的音色。

使用这种方法可以进行许多有趣的操作。

- 时间拉伸（Time-stretching）。颗粒的发送速度可以比原始样本中的对应颗粒更快或更慢，从而实现更快或更慢的播放——而不会产生传统样本播放中的音高变化。你甚至可以通过从单点提取多个颗粒来“冻结”样本的某个位置。关于这一点，例如你可以在时间拉伸的循环中多次重复一个鼓击的“颗粒”，以创建一个不同的鼓点模式。

- 音高偏移（Pitch-shifting）。对每个颗粒音高的修改允许你在不影响计时的情况下改变样本的音高。通过调制每个颗粒的音高或位置，你还可以创建空间和“模糊”效果。

- 你还可以打乱颗粒播放的顺序，以产生从轻微模糊到极端混乱的效果。

希腊作曲家雅尼斯·泽森塔基斯（Iannis Xenakis）被称为颗粒合成技术的发明者。

加拿大作曲家巴里·特拉克（Barry Truax）是最早实现这种合成技术实时版本的人之一。

## C++ 中实现颗粒合成

在 `04-granular.cpp` 代码示例中，我们加载了之前合成技术生成的声音，扩展了加载样本的长度，并将从加载样本中随机添加颗粒到扩展版本中。

## 使用 Output 的 Portal 实现颗粒合成

Portal by Output - 颗粒特效插件 - 初次外观预览⁵

> *https://www.youtube.com/watch?v=DScdfZcR2QE

## 频率调制 (FM) 合成

FM 合成使用一个调制振荡器和一个正弦载波振荡器。调制振荡器在音频范围内调制载波振荡器生成的波形频率，产生新的泛波。这些泛波被称为侧带。

当载波和调制波形之间存在数学关系时，产生的声音是谐波的。当调制器是载波形的非整数倍时，会产生非谐波侧带，导致非谐波声音。

通常，FM 合成器不包含滤波器。你可以生成一些减法合成器的风格，但很难用这种方法重现共振减法合成滤波器的声音。然而，FM 合成非常出色，能够创建出减法合成器难以实现的声音——例如铃声、金属音色和电钢琴的钢条音。FM 合成的另一个优势是强有力的低音和合成铜器声。

FM 合成于 20 世纪 60 年在加利福尼亚斯坦福大学由约翰·乔宁（John Chowning）开发，他试图创建出与模拟合成不同的声音。他的算法在 1973 年许可给日本雅马哈（Yamaha）。

雅马哈的工程师开始调整乔宁的算法，用于数字合成器。

## C++ 中实现频率调制 (FM) 合成

在 `05-fm.cpp` 示例中，频率调制有一个载波和一个调制器。通过添加更多的载波和调制器，我们可以生成更复杂的声音。

## 使用 Yamaha DX7 实现频率调制 (FM) 合成

1983 年的声音 | Yamaha DX7 演示 6

> *https://www.youtube.com/watch?v=13bWvQa

## 线性算术合成 (Linear Arithmetic Synthesis)

线性算术合成，或 LA 合成，是 Roland 在 1987 年发布 D50 合成器时发明的一种合成方法。LA 合成将减法合成与基于 PCM 的样本相结合。线性算术合成术是指在时间线上组合声音的合成。通常由 PCM 瞬态开始音符，然后由减法合成继续。

当时，采样器非常昂贵，因此 Roland 致力于制造一种易编程、声音真实且听起来像合成器的机器。

## C++ 中实现线性算术合成

在 `06-1a.cpp` 示例中，我们加载了一个样本用于包络的起始（Attack）部分，其余部分使用减法合成生成。

## 使用 Roland D-50 实现线性算术合成

Roland D-50 | 王者回归！

> *https://www.youtube.com/watch?v=zfMkRjHAWo

## 相位失真合成 (Phase Distortion Synthesis)

相位失真（PD）合成是 Casio 在 1984 年在其 CZ 系列合成器中引入的一种合成方法。概要，它与雅马哈公司推崇的相位调制合成相似，意义在于这两种方法都是在时域内通过另一个波形（调制器）的影响来动态改变载波波形的谐内容。然而，两种方法的应用和结果非常不同。这项技术由 Casio 在 1984 年在其 CZ 系列合成器中引入。

## C++ 中实现相位失真合成

`07-pd.cpp` 是相位失真合成的一个示例。`generatephasedistortionwave` 函数包含了该合成方法的所有逻辑。

## 扫描合成 (Scanned Synthesis)

扫描合成涉及一种振动频率在 15 Hz 以下的低速动态系统。人耳听不到这种动态系统的低频信号。因此，为了产生可听的频率，会沿着闭合路径周期地扫描动态系统的“形状”。该“形状”被转换为声波，其音高由扫描函数的速度决定。音高控制与动态系统控制完全分离。因此，音色和音高是独立的。该系统可以看作是一个动态波表。该模型可以比作缓慢振动的弦，或者一个遵循波方程的二维表面。

## C++ 中的扫描合成

`08-scanned.cpp` 中的 `generatesannedwave` 函数包含一个扫描合成的示例。

## 使用 Qu-Bit 扫描的合成

Qu-Bit Scanned，一种扫描合成 Eurorack 荡器*

> *https://www.youtube.com/watch?v=p_AboqfHAAE

## 矢量合成 (Vector Synthesis)

矢量合成是 Sequential Circuits 在 1986 年在 Prophet VS 合成器中引入的一种音频合成技术。

矢量合成通过在四个声源之间提供动态交叉淡，为声音提供运动感。四个声源在概念上排列为 X 轴和 Y 轴的顶点，并标记为 A、B、C 和 D。四个声源的给定混合可以用此“矢量平面”中的单个点表示。点的移动提供了声音的趣味性，这也是这种技术的魅力所在。混合通常使用摇杆完成，尽管也可以使用包络发生器或 LFO 控制该点。

该术语简单指的是通过摇杆在 4 种音色之间进行交叉淡的能力。

## C++ 中的矢量合成

在 `09-vectorsynth.cpp` 示例中，我们加载了 4 个采样并在它们之间进行交叉淡。

## 使用 Sequential Circuits Prophet VS 的矢量合成

Sequential Circuits Prophet VS 复古矢量合成器¹¹⁰

> ¹¹⁰https://www.youtube.com/watch?v=H4gSZ7_AWOK

## 虚拟模拟 (VA) 合成

使用数字信号处理器（DSP）作为其自身的 ASIC 或在 FPGA 中实现，可以帮助仿真/模拟产生合成声音的模拟硬件组件（电阻、电容器……）。

这种合成类型也被称为模拟建模合成。模拟建模合成器比真实的模拟对应品更可靠，因为振荡器音高最终由数字时钟维持，而且数字硬件通常不受温度变化的影响较小。

虽然模拟合成器的每个复声通道都需要一个振荡器电路，但模拟建模合成器并不面临这个问题。这意味着其中许多合成器（尤其是更现代的型号）可以产生与其运行的 CPU 处理能力相当的复声数量。

建模合成器还提供了大多数真实仪器不存在的 Patch 存储功能和 MIDI 支持。完全在主机计算机操作系统运行的模拟建模合成器通常被称为模拟软件合成器。

这个术语直到 1990 年 Nord Lead 出世才被使用。

最流行且为人知的 VA 合成器是 Access Virus TI。

## C++ 中的虚拟模拟 (VA) 合成

（未包含示例，因为这种合成方法对于初学者来说太复杂，因此超出了范围。）

## 使用 Access Virus TI 的虚拟模拟 (VA) 合成

Access Virus TI - Patches¹¹¹

> ¹¹¹https://www.youtube.com/watch?v=-S_zWBsxMzA

## 波表合成 (Wavetable Synthesis)

波表合成从根本上基于对任意单周期波形的周期性复制。在波表合成中，采用某种方法来改变或调制波表中的选定波形。波表中的位置选择了单周期波形。相邻波形之间的数字插值允许产生声音的音色发生动态且平滑的变化。向任一方向扫描波表可以通过多种方式控制，例如使用 LFO、包络、压力或速度。

波表合成也被称为“查找表合成”。

波表合成也被称为“查找表合成”。PPG 在 1970 年代对波表合成进行了大量研究，`wavetable` 这种方法。

## C++ 中的波表合成

`11-wavetable.cpp` 中的 `generate` 函数包含一个波表合成的示例。

## 物理建模的合成

物理建模 (Physical Modeling)

也被称为组件建模，这种合成方法使用数学模型来模拟乐器。为了建模声音，需要考虑以下方面：乐器的材质、尺寸、密度以及它所处环境。同样重要的是乐器的敲击方式——通过击子敲击、通过拉奏、拨弦或弹奏。

为了建模鼓，需要考虑鼓皮（或膜）的材质、刚度、密度以及它与鼓壳的连接。鼓本身的材质、尺寸、共振和阻尼特性。为了建模小提琴，需要考虑到弦的材质、弦的张力以及声音通过琴桥的传递。

## C++ 中的物理建模

`12-physicalmodeling_strong.cpp` 示例基于 Karplus-Strong 合成。

Alexander Strong 发明了该算法，Kevin Karplus 对其工作原理进行了首次分析。

## 使用 Anyma Phi 的物理建模

Phi 物理建模合成器 - 预设与声音调色¹³

> ¹³https://www.youtube.com/watch?v=oe6GMKSNO

## 回顾 (Rearview Mirror)

正如引言所述，这是一本面向初学者的书籍。正如生活中的许多事情一样——我们需要先学会站立才能学会走路，学会走路才能学会跑步，以此类推。

那么我们学到了什么？我们学到了不同的合成方法在工作原理上确实不同，在声音效果上也不同。

显而易见，某些合成方法比其他方法更有用。减法合成（无论是虚拟模拟）、FM 和波表合成是最常用的合成方法。而且，如今 DSP 的性能价格极低，这使得物理建模成为音乐制作中一种越来越可行的方法。

附录 C 比你想象的要重要。你应该学习术语，以便更精通地掌握音频工程师的工作内容和方式。作为音频程序员，你是为音频工程师制作工具，而不是反过来。

`00-signalgenerators.cpp` - 36691 bytes.

```cpp
// 信号生成器
// /
// 编译: clang++ -std=c++20 -lpng 00-signalgenerators.cpp -o 00-signalgenerators
// // 如果缺少 #include <png.hpp>
// // brew install png++
// png++ 用于将音频渲染为图像以可视化波形。
// 在 macOS 上使用 homebrew 或使用其他包管理器安装。
// https://savannah.nongnu.org/projects/pngpp/
//
// 使用 Adam Stark 的 AudioFile（仅头文件）来写入 AIFF 文件。
// 查看下方 github 链接中的代码。
// https://github.com/adamstark/AudioFile
//
// 使用 p-ravnav Indicators
// // git clone https://github.com/p-ravnav/indicators
// // mkdir build && && cd build
// // cmake -DINDICATORS_SAMPLES=ON -DINDICATORS_DEMO=ON ..
// // make
// python3 utils/amalgamate/amalgamate.py -c single_include.json -s
//
// 如果缺少 clang++:
// 来自 Xcode 的 clang++:
// // xcode-select --install
// // xcode-select -p
//
// 来自 homebrew llvm 的 clang++
// 如果需要 clang++，请通过 macOS homebrew 安装...
// // https://clang.llvm.org/get_started.html

#define USE_MATH_DEFINES
#include <cmath>
#include <vector>
```



```cpp
#include <random>
#include <filesystem>
#include "indicators.hpp"
#include <png++/png.hpp>
#include "AudioFile/AudioFile.h"

namespace Render {
    void fillbackground(png::image<png::rgb_pixel>&& image);
    void drawpx(png::image<png::rgb_pixel>&& image, int x, int y);
    void drawline(png::image<png::rgb_pixel>&& image, int x1, int y1, int x2, int y2);
    void drawwave(png::image<png::rgb_pixel>&& image, std::vector<uint32_t>& signalY);
}

namespace SignalGenerators {
    void generatesnewewaveaff();
    void rendersnewewavepng();
    void generatessumoffirsteightpartialaff();
    void renderssumoffirsteightpartialpng();
    void generatesawtoothwaveaff();
    void rendersawtoothwavepng();
    void generatesquaresquarewaveaff();
    void rendersquaresquarewavepng();
    void generateetrianglewaveaff();
    void rendertrianglewavepng();
    void generateetwentypepulsewaveaff();
    void rendertwentypepulseweeppng();
    void generateconvecurveaff();
    void renderconvecurvepng();
    void generateconcavecurveaff();
    void renderconcavecurvepng();
    void generatefrequencymodulationaff();
    void rendersfrequencymodulationpng();
    void generatephasemodulationaff();
    void rendersphasemodulationpng();
    void generateamplitudetedmodulationaff();
    void renderamplitudetedmodulationpng();
    void generateeringmodulationaff();
    void renderringmodulationpng();
    void generateatenoiseaff();
    void rendernooisepng();
    void generatepulsewaveaff();
    void renderpulsewavepng();
}

int main() {
    namespace fs = std::filesystem;
    fs::create_directory("signalgenerators");

    using namespace indicators;
    // 隐藏光标
    show_cursor(false);

    // 设置进度条
    ProgressBar bar{
        option::BarWidth(50),
        option::Start("{"),
        option::Fill("0"),
        option::Lead("0"),
        option::Remainder("-"),
        option::End("]"),
        option::PostfixText("正在生成正弦波 2/28"),
        option::ForegroundColor(Color::cyan),
        option::FontStyles(std::vector<FontStyle>{FontStyle::bold})
    };

    // 更新进度
    bar.set_progress(13);

    SignalGenerators::generinesewaveaff();

    // 更新进度
    bar.set_progress(19);
    bar.set_option(option::PostfixText("正在渲染正弦波 2/28"));

    SignalGenerators::rendinesewavepng();

    // 更新进度
    bar.set_progress(22);
    bar.set_option(option::PostfixText("正在生成前八部分泛波和 3/28"));

    SignalGenerators::generatesumofirsteightpartialsaff();

    // 更新进度
    bar.set_progress(25);
    bar.set_option(option::PostfixText("正在渲染前八部分泛波和 4/28"));

    SignalGenerators::rendumsoffirstightpartialspng();

    // 更新进度
    bar.set_progress(28);
    bar.set_option(option::PostfixText("正在生成锯齿波 5/28"));

    SignalGenerators::generatesothwaveaff();

    // 更新进度
    bar.set_progress(31);
    bar.set_option(option::PostfixText("正在渲染锯齿波 6/28"));

    SignalGenerators::rendersawtothwavepng();

    // 更新进度
    bar.set_progress(34);
    bar.set_option(option::PostfixText("正在生成方波 7/28"));

    SignalGenerators::generatesquarewaveaff();

    // 更新进度
    bar.set_progress(37);
    bar.set_option(option::PostfixText("正在渲染方波 8/28"));

    SignalGenerators::rendersquarewavepng();

    // 更新进度
    bar.set_progress(40);
    bar.set_option(option::PostfixText("正在生成三角波 9/28"));

    SignalGenerators::generatetrianglewaveaff();

    // 更新进度
    bar.set_progress(43);
    bar.set_option(option::PostfixText("正在渲染三角波 10/28"));

    SignalGenerators::rendertrianglewavepng();

    // 更新进度
    bar.set_progress(46);
    bar.set_option(option::PostfixText("正在生成25% 脉冲波 11/28"));

    SignalGenerators::generateetwentypepulsewaveaff();

    // 更新进度
    bar.set_progress(49);
    bar.set_option(option::PostfixText("正在渲染25% 脉冲波 12/28"));

    SignalGenerators::rendertwentypepulseweeppng();

    // 更新进度
    bar.set_progress(52);
    bar.set_option(option::PostfixText("正在生成凸曲线 13/28"));

    SignalGenerators::generateconvecurveaff();

    // 更新进度
    bar.set_progress(55);
    bar.set_option(option::PostfixText("正在渲染凸曲线 14/28"));

    SignalGenerators::renderconvecurvepng();

    // 更新进度
    bar.set_progress(58);
    bar.set_option(option::PostfixText("正在生成凹形曲线 15/28"));

    SignalGenerators::generateconcavecurveaff();

    // 更新进度
    bar.set_progress(61);
    bar.set_option(option::PostfixText("正在渲染凹形曲线 16/28"));

    SignalGenerators::renderconcavecurvepng();

    // 更新进度
    bar.set_progress(64);
    bar.set_option(option::PostfixText("正在生成频率调制 17/28"));

    SignalGenerators::generatefrequencymodulationaff();

    // 更新进度
    bar.set_progress(67);
    bar.set_option(option::PostfixText("正在渲染频率调制 18/28"));

    SignalGenerators::rendersfrequencymodulationpng();

    // 更新进度
    bar.set_progress(70);
    bar.set_option(option::PostfixText("正在生成相位调制 19/28"));

    SignalGenerators::generatephasemodulationaff();

    // 更新进度
    bar.set_progress(73);
    bar.set_option(option::PostfixText("正在渲染相位调制 20/28"));

    SignalGenerators::rendersphasemodulationpng();

    // 更新进度
    bar.set_progress(76);
    bar.set_option(option::PostfixText("正在生成幅度调制 21/28"));

    SignalGenerators::generateamplitudetedmodulationaff();

    // 更新进度
    bar.set_progress(79);
    bar.set_option(option::PostfixText("正在渲染幅度调制 22/28"));

    SignalGenerators::renderamplitudetedmodulationpng();

    // 更新进度
    bar.set_progress(82);
    bar.set_option(option::PostfixText("正在生成环形调制 23/28"));

    SignalGenerators::generateeringmodulationaff();

    // 更新进度
    bar.set_progress(85);
    bar.set_option(option::PostfixText("正在渲染环形调制 24/28"));

    SignalGenerators::renderringmodulationpng();

    // 更新进度
    bar.set_progress(88);
    bar.set_option(option::PostfixText("正在生成噪声 25/28"));

    SignalGenerators::generateatenoiseaff();

    // 更新进度
    bar.set_progress(91);
    bar.set_option(option::PostfixText("正在渲染噪声 26/28"));

    SignalGenerators::rendernooisepng();

    // 更新进度
    bar.set_progress(94);
    bar.set_option(option::PostfixText("正在生成脉冲波 27/28"));

    SignalGenerators::generatepulsewaveaff();

    // 更新进度
    bar.set_progress(100);
    bar.set_option(option::PostfixText("正在渲染脉冲波 28/28"));

    SignalGenerators::renderpulsewavepng();

    // 更新进度
    bar.set_option(option::PostfixText("完成 28/28"));
}
```

```cpp
295    a.setNumSamplesPerChannel(44100);
296    // 生成正弦波
297    for (int i=0;i<a.getNumSamplesPerChannel();++i)
298    {
299        for (int channel=0;channel<a.getNumChannels();++channel)
300            a.sample[channel][i]=sin((static_cast<double>(i) / sampleRate) * 
301
302* 2.0 * M_PI);
303        }
304    }
305    a.save(sineName,AudioFileFormat::Aiff);
306    }
307    void renderswavepng()
308    {
309        const std::string sineName="signalgenerators/02-sine-wave.png";
310        const double sampleRate=44100.0;
311        double frequencyInHz=440.0;
312        std::vector<uint32_t> signalY;
313        signalY.resize(44100);
314
315        for (int i=0;i<sampleRate;++i)
316        {
317            double value=sin((static_cast<double>(i) / sampleRate) * frequencyInHz * 2
318            PI);
319            if (value >= 0.0) {
320                signalY[i]=300-(300*value);
321            } else if (value < 0.0) {
322                signalY[i]=300+(300*fabs(value));
323            }
324        }
326        png::image::pixel image(44100,600);
327        Render::fillbackground(image);
328        Render::drawwave(image,signalY);
329        image.write(sineName);
330    }
331    void generatesumoffirstightpartialsaiff()
332    {
338    const std::string sineName="signalgenerators/03-sine-wave-first-eight-partials.aif";
339    const double sampleRate=44100.0;
340    const double frequencyInHz=440.0;
341
342    // 设置音频文件
343    AudioFile<float> a;
344    a.setNumChannels(1);
345    a.setBitDepth(24);
346    a.setNumSamplesPerChannel(44100);
347
348    double s1=0.0,s2=0.0,s3=0.0,s4=0.0,s5=0.0,s6=0.0,s7=0.0,s8=0.0,ss=0.0;
349
350    // 生成正弦波
351    for (int i=0;i<a.getNumSamplesPerChannel();++i) {
```



# 信号生成器代码示例

## 正弦波生成

```cpp
for (int channel = 0; channel < a.getNumChannels(); ++channel) {
    s1 = (static_cast<double>(i) / frequencyInHz * 1);
    s2 = (static_cast<double>(i) / frequencyInHz * 2);
    s3 = (static_cast<double>(i) / frequencyInHz * 3);
    s4 = (static_cast<double>(i) / frequencyInHz * 4);
    s5 = (static_cast<double>(i) / frequencyInHz * 5);
    s6 = (static_cast<double>(i) / frequencyInHz * 6);
    s7 = (static_cast<double>(i) / frequencyInHz * 7);
    s8 = (static_cast<double>(i) / frequencyInHz * 8);
    ss = (s1 + s2 + s3 + s4 + s5 + s6 + s7 + s8) / 8;
    a.samples[channel] = ss;
}
```

```cpp
// 371
a.save(sineName, AudioFormat::Aiff);

// 373
void renderumsoffirstightpartials() {
    // 374
    const std::string sineName = "signalgenerators/04-sine-wave-first-eight-partials.aif";
}
```

```cpp
// 生成正弦波
for (int i = 0; i < sampleRate; ++i) {
    s1 = sin((static_cast<double>(i) / sampleRate) * (frequencyHz * 1) * 2.0 * M_PI);
    s2 = sin((static_cast<double>(i) / sampleRate) * (frequencyHz * 2) * M_PI);
    s3 = sin((static_cast<double>(i) / sampleRate) * (frequencyHz * 3) * M_PI);
    s4 = sin((static_cast<double>(i) / sampleRate) * (frequencyHz * 4) * M_PI);
    s5 = sin((static_cast<double>(i) / sampleRate) * (frequencyHz * 5) * M_PI);
    s6 = sin((static_cast<double>(i) / sampleRate) * (frequencyHz * 6) * M_PI);
    s7 = sin((static_cast<double>(i) / sampleRate) * (frequencyHz * 7) * M_PI);
    s8 = sin((static_cast<double>(i) / sampleRate) * (frequencyHz * 8) * M_PI);
    ss = (s1 + s2 + s3 + s4 + s5 + s6 + s7 + s8) / 8;

    if (ss > 0.0) {
        signalY[i] = 300 - (300 * ss);
    } else if (ss < 0.0) {
        signalY[i] = 300 + (300 * fabs(ss));
    }
}
```

```cpp
png::image::pixel image(44100, 600);
Render::fillbackground(image);
Render::drawwave(image, signalY);
image.write(sineName);
```

## 锯齿波生成

```cpp
void generatessawtoothwave() {
    const std::string sineName = "signalgenerators/05-tooth-wave.aiff";
    const double sampleRate = 44100.0;
    const double frequencyInHz = 440.0;
    double ss;

    // 设置音频文件
    AudioFile<float> a;
    a.setNumChannels(1);
    a.setBitDepth(24);
    a.setNumSamplesPerChannel(44100);

    for (int i = 0; i < a.getNumSamplesPerChannel(); ++i) {
        for (int channel = 0; channel < a.getNumChannels(); ++channel) {
            ss = -2 / M_PI * tan(frequencyInHz * M_PI * i / sampleRate);
            a.samples[channel] = ss;
        }
    }
    a.save(sineName, AudioFormat::Aiff);
}
```

```cpp
void renderstoothpng() {
    const std::string sineName = "signalgenerators/06-saw-wave.png";
    const double sampleRate = 44100.0;
    const double frequencyInHz = 440.0;
    double ss;
    std::vector<uint32_t> signalY;
    signalY.resize(44100);

    for (int i = 0; i < sampleRate; ++i) {
        ss = -2 / M_PI * tan(frequencyInHz * M_PI * i / sampleRate);
        if (ss >= 0.0) {
            signalY[i] = 300 - (300 * ss);
        } else if (ss < 0.0) {
            signalY[i] = 300 + (300 * fabs(ss));
        }
    }

    png::image<png::rgb_pixel> image(44100, 600);
    Render::fillbackground(image);
    Render::drawwave(image, signalY);
    image.write(sineName);
}
```

## 方波生成

```cpp
void generatesquarewave() {
    const std::string sineName = "signalgenerators/07-square-wave.aiff";
    const double sampleRate = 44100.0;
    const double frequencyInHz = 440.0;
    double period = sampleRate / frequencyInHz;
    double dutyCycle = period * 0.5;
    double ss;

    // 设置音频文件
    AudioFile<float> a;
    a.setNumChannels(1);
    a.setBitDepth(24);
    a.setNumSamplesPerChannel(44100);

    for (int i = 0; i < a.getNumSamplesPerChannel(); ++i) {
        for (int channel = 0; channel < a.getNumChannels(); ++channel) {
            if ((int(period)) >= 0 && (i % int(period)) < int(dutyCycle)) {
                ss = 0.7;
            } else {
                ss = -0.7;
            }
            a.samples[channel] = ss;
        }
    }
    a.save(sineName, AudioFormat::Aiff);
}
```

```cpp
void rendersquarepng() {
    const std::string sineName = "signalgenerators/08-square-wave.png";
    const double sampleRate = 44100.0;
    const double frequencyInHz = 440.0;
    double period = sampleRate / frequencyInHz;
    double dutyCycle = period * 0.5;
    std::vector<uint32_t> signalY;
    signalY.resize(44100);

    for (int i = 0; i < 44100; ++i) {
        if ((int(period)) >= 0 && (i % int(period)) < int(dutyCycle)) {
            signalY[i] = 300;
        } else {
            signalY[i] = 600;
        }
    }

    png::image<png::rgb_pixel> image(44100, 600);
    Render::fillbackground(image);
    Render::drawwave(image, signalY);
    image.write(sineName);
}
```

## 三角波生成

```cpp
void generetrianglewaveaiff() {
    const std::string sineName = "signalgenerators/09-triangle-wave.aiff";
    const double sampleRate = 44100.0;
    const double frequencyHz = 440.0;
    double ss;

    // 设置音频文件
    AudioFile<float> a;
    a.setNumChannels(1);
    a.setBitDepth(24);
    a.setNumSamplesPerChannel(44100);

    for (int i = 0; i < a.getNumSamplesPerChannel(); ++i) {
        for (int channel = 0; channel < a.getNumChannels(); ++channel) {
            ss = M_PI * asin(frequencyHz * 2 * M_PI * i / sampleRate);
            a.samples[channel] = ss;
        }
    }
    a.save(sineName, AudioFormat::Aiff);
}
```

```cpp
void rendertrianglewavepng() {
    const std::string sineName = "signalgenerators/10-triangle-wave.png";
    const double sampleRate = 44100.0;
    const double frequencyHz = 440.0;
    double ss;
    std::vector<uint32_t> signalY;
    signalY.resize(44100);

    for (int i = 0; i < sampleRate; ++i) {
        ss = M_PI * asin(sin(frequencyHz * 2 * M_PI * i / sampleRate));
        if (ss >= 0.0) {
            signalY[i] = 300 - (300 * ss);
        } else if (ss < 0.0) {
            signalY[i] = 300 + (300 * fabs(ss));
        }
    }

    png::image<png::rgb_pixel> image(44100, 600);
    Render::fillbackground(image);
    Render::drawwave(image, signalY);
    image.write(sineName);
}
```

## 25% 脉冲波生成

```cpp
void generatenetfivepulsewaveaiff() {
    const std::string sineName = "signalgenerators/11-twenty-five-pulse-wave.aiff";
    const double sampleRate = 44100.0;
    const double frequencyInHz = 440.0;
    double period = sampleRate / frequencyInHz;
    double dutyCycle = period + 0.25;
    double ss;

    // 设置音频文件
    AudioFile<float> a;
    a.setNumChannels(1);
    a.setBitDepth(24);
    a.setNumSamplesPerChannel(44100);

    for (int i = 0; i < a.getNumSamplesPerChannel(); ++i) {
        for (int channel = 0; channel < a.getNumChannels(); ++channel) {
            if ((int(period)) >= 0 && (i % int(period)) < int(dutyCycle)) {
                ss = 0.7;
            } else {
                ss = -0.7;
            }
            a.samples[channel] = ss;
        }
    }
    a.save(sineName, AudioFormat::Aiff);
}
```

## 附录 A：C++20 代码



# C++ 信号生成与渲染示例

## `rendertentwentyfivepulsewavepng()`

```cpp
void rendertentwentyfivepulsewavepng() {
    const std::string sineName = "signalgenerators/12-twenty-five-pulse-wave";
    const double sampleRate = 44100.0;
    const double frequencyInHz = 440.0;
    double period = sampleRate / frequencyInHz;
    double dutyCycle = period * 0.25;
    std::vector<uint32_t> signalY;
    signalY.resize(44100);

    for (int i = 0; i < 44100; i++) {
        if ((int(period)) >= 0 && (int(period)) < (int(dutyCycle))) {
            signalY[i] = 0;
        } else {
            signalY[i] = 600;
        }
    }

    signalY[0] = 300;
    signalY[44099] = 300;

    png::image<png::rgb_pixel> image(44100, 600);
    Render::fillbackground(image);
    Render::drawwave(image, signalY);
    image.write(sineName);
}
```

## `generateconvexcurveaiff()`

```cpp
void generateconvexcurveaiff() {
    const std::string sineName = "signalgenerators/13-convex-curve.aiff";
    const double sampleRate = 44100.0;
    const double frequencyInHz = 440.0;
    double period = sampleRate / frequencyInHz;
    uint32_t maxValue = 0, temp = 0;
    double ss, sss;

    // Setup the audio file
    AudioFile<float> a;
    a.setNumChannels(1);
    a.setBitDepth(24);
    a.setNumSamplesPerChannel(44100);

    for (int i = 0; i < 44100; ++i) {
        temp = pow(abs((i % int(period))) - (int(period) / 2), 2.0);
        if (temp > maxValue) {
            maxValue = temp;
        }
    }
    for (int i = 0; i < a.getNumSamplesPerChannel(); ++i) {
        for (int channel = 0; channel < a.getNumChannels(); ++channel) {
            temp = pow(abs((i % int(period))) - (int(period) / 2), 2.0);
            ss = double(temp) / double(maxValue);
            sss = sss(-0.5) * 1.5;
            a.samples[channel][i] = sss;
        }
        a.save(sineName, AudioFileFormat::Aiff);
    }
}
```

## `renderconvexcurvepngng()`

```cpp
void renderconvexcurvepngng() {
    const std::string sineName = "signalgenerators/14-convex-curve.png";
    const double sampleRate = 44100.0;
    const double frequencyInHz = 440.0;
    double period = sampleRate / frequencyInHz;
    double ss;
    uint32_t maxValue = 0, temp = 0;
    std::vector<uint32_t> signalY;
    signalY.resize(44100);
    for (int i = 0; i < 44100; ++i) {
        temp = pow(abs((i % int(period))) - (int(period) / 2), 2.0);
        if (temp > maxValue) {
            maxValue = temp;
        }
    }
    for (int i = 0; i < 44100; ++i) {
        temp = pow(abs((i % int(period))) - (int(period) / 2), 2.0);
        ss = double(temp) / double(maxValue);
        signalY[i] = 600 - (ss);
    }

    png::image<png::rgb_pixel> image(44100, 600);
    Render::fillbackground(image);
    Render::drawwave(image, signalY);
    image.write(sineName);
}
```

## `generateconcavecurveaiff()`

```cpp
void generateconcavecurveaiff() {
    const std::string sineName = "signalgenerators/15-concave-curve.a";
    const double sampleRate = 44100.0;
    const double frequencyInHz = 440.0;
    double period = sampleRate / frequencyInHz;
    uint32_t maxValue = 0;
    double ss, sss, temp;

    // Setup the audio file
    AudioFile<float> a;
    a.setNumChannels(1);
    a.setDepth(24);
    a.setSamplesPerChannel(44100);

    for (int i = 0; i < 44100; ++i) {
        temp = pow(abs((i % int(period))) - (int(period) / 2), 2.0);
        if (temp > maxValue)
            maxValue = temp;
    }
    for (int channel = 0; i < a.getNumSamplesPerChannel(); ++i) {
        temp = pow(abs((i % int(period))) - (int(period) / 2), 2.0);
        ss = temp / double(maxValue);
        sss = sss(-0.5) * 1.5;
        a.samples[channel][i] = sss;
    }
    a.save(sineName, AudioFileFormat::Aiff);
}
```

## `renderconcavecurvepng()`

```cpp
void renderconcavecurvepng() {
    const std::string sineName = "signalgenerators/16-concave-curve.png";
    const double sampleRate = 44100.0;
    const double frequencyInHz = 440.0;
    double period = sampleRate / frequencyInHz;
    double ss;
    uint32_t maxValue = 0, temp = 0;
    std::vector<uint32_t> signalY;
    signalY.resize(44100);
    for (int i = 0; i < 44100; ++i) {
        temp = pow(abs((i % int(period))) - (int(period) / 2), 2.0);
        if (temp > maxValue) {
            maxValue = temp;
        }
    }
    for (int i = 0; i < 44100; ++i) {
        temp = pow(abs((i % int(period))) - (int(period) / 2), 2.0);
        ss = double(temp) / double(maxValue);
        signalY[i] = 600 - (ss);
    }

    png::image<png::rgb_pixel> image(44100, 600);
    Render::fillbackground(image);
    Render::drawwave(image, signalY);
    image.write(sineName);
}
```

## `generatefreymulationaiff()`

```cpp
void generatefreymulationaiff() {
    const std::string sineName = "signalgenerators/17-frequency-modulation.aiff";
    const double sampleRate = 44100.0;
    const double frequencyInHz = 440.0;
    double period = sampleRate / frequencyInHz;
    uint32_t maxValue = 0, temp = 0;
    double ss, sss;

    // Setup the audio file
    AudioFile<float> a;
    a.setNumChannels(1);
    a.setBitDepth(24);
    a.setNumSamplesPerChannel(44100);

    for (int i = 0; i < 44100; ++i) {
        temp = pow(abs((i % int(period))) - (int(period) / 2), 2.0);
        if (temp > maxValue) {
            maxValue = temp;
        }
    }
    for (int i = 0; i < a.getNumSamplesPerChannel(); ++i) {
        for (int channel = 0; channel < a.getNumChannels(); ++channel) {
            temp = pow(abs((i % int(period))) - (int(period) / 2), 2.0);
            ss = double(temp) / double(maxValue);
            sss = sss(-0.5) * 1.5;
            a.samples[channel][i] = sss;
        }
        a.save(sineName, AudioFileFormat::Aiff);
    }
}
```

## `renderfreymulationpng()`

```cpp
void renderfreymulationpng() {
    const std::string sineName = "signalgenerators/18-frequency-modulation.png";
    const double sampleRate = 44100.0;
    const double frequencyInHz = 440.0;
    double period = sampleRate / frequencyInHz;
    double ss;
    uint32_t maxValue = 0, temp = 0;
    std::vector<uint32_t> signalY;
    signalY.resize(44100);
    for (int i = 0; i < 44100; ++i) {
        temp = pow(abs((i % int(period))) - (int(period) / 2), 2.0);
        if (temp > maxValue) {
            maxValue = temp;
        }
    }
    for (int i = 0; i < 44100; ++i) {
        temp = pow(abs((i % int(period))) - (int(period) / 2), 2.0);
        ss = double(temp) / double(maxValue);
        signalY[i] = 600 - (ss);
    }

    png::image<png::rgb_pixel> image(44100, 600);
    Render::fillbackground(image);
    Render::drawwave(image, signalY);
    image.write(sineName);
}
```

## `generatephasymulationaiff()`

```cpp
void generatephasymulationaiff() {
    const std::string sineName = "signalgenerators/19-phase-modulation.aiff";
    const double sampleRate = 44100.0;
    const double frequencyInHz = 440.0;
    double period = sampleRate / frequencyInHz;
    uint32_t maxValue = 0;
    double ss, sss, temp;

    // Setup the audio file
    AudioFile<float> a;
    a.setNumChannels(1);
    a.setDepth(24);
    a.setSamplesPerChannel(44100);

    for (int i = 0; i < 44100; ++i) {
        temp = pow(abs((i % int(period))) - (int(period) / 2), 2.0);
        if (temp > maxValue)
            maxValue = temp;
    }
    for (int channel = 0; i < a.getNumSamplesPerChannel(); ++i) {
        temp = pow(abs((i % int(period))) - (int(period) / 2), 2.0);
        ss = temp / double(maxValue);
        sss = sss(-0.5) * 1.5;
        a.samples[channel][i] = sss;
    }
    a.save(sineName, AudioFileFormat::Aiff);
}
```

## 附录 A：C++20 代码



## 附录 A：C++20 代码

### 示例 1：相位调制音频生成

```cpp
const double sampleRate = 44100.0;
const double frequencyHz = 440.0;
const double frequencyRadius = twoPI / sampleRate;
double modifierFrequency = frequencyHz * 3;
double carrierIncrement = frequencyRadius * frequencyHz;
double modifierAmplitude = frequencyRadius * (2 * modifierFrequency);
double modifierValue = 0;
double carrierPhase = 0;
double modifierPhase = 0;
double modifierIncrement = frequencyRadius * modifierFrequency;

// Setup the audio file
AudioFile<float> a;
a.setNumChannels(1);
a.setBitDepth(24);
a.setSamplesPerChannel(44100);

for (int i = 0; i < a.getNumSamplesPerChannel(); ++i) {
    for (int channel = 0; channel < a.getNumChannels(); ++channel) {
        a.samples[channel][i] = sinf(carrierPhase);
        modifierValue = modifierAmplitude * sinf(modifierPhase);
        carrierPhase = carrierPhase + carrierIncrement + modifierValue;
        modifierPhase = modifierPhase + modifierIncrement;
        if (carrierPhase >= twoPI) {
            carrierPhase -= twoPI;
        } else if (carrierPhase < 0) {
            carrierPhase += twoPI;
        }
        if (modifierPhase >= twoPI) {
            modifierPhase -= twoPI;
        }
    }
}
a.save(sineName, AudioFileFormat::Aiff);
```

```cpp
void renderphasemodulationpng() {
    const std::string sineName = "signalgenerators/20-phase-modulation.png";
    const double twoPI = 2 * M_PI;
}
```

### 示例 2：相位调制波形渲染

```cpp
const double sampleRate = 44100.0;
const double frequencyInHz = 440.0;
const double frequencyRadius = twoPI / sampleRate;
double modifierFrequency = frequencyHz * 3;
double carrierIncrement = frequencyRadius * frequencyHz;
double modifierAmplitude = frequencyRadius * (2 * modifierFrequency);
double modifierValue = 0;
double carrierPhase = 0;
double modifierPhase = 0;
double modifierIncrement = frequencyRadius * modifierFrequency;
double doubleValue = 0;
std::vector<uint32_t> signalY;
signalY.resize(44100);

for (uint32_t i = 0; i < sampleRate; ++i) {
    double value = sin(carrierPhase);
    if (value >= 0.0) {
        signalY[i] = 300 - (300 * value);
    } else if (value < 0.0) {
        signalY[i] = 300 + (300 * abs(value));
    }
    modifierValue = modifierAmplitude * sin(carrierPhase);
    carrierPhase = carrierPhase + carrierIncrement + modifierValue;
    modifierPhase = modifierPhase + modifierIncrement;
    if (carrierPhase >= twoPI) {
        carrierPhase -= twoPI;
    } else if (carrierPhase < 0) {
        carrierPhase += twoPI;
    }
    if (modifierPhase >= twoPI) {
        modifierPhase -= twoPI;
    }
    png::image<png::rgb_pixel> image(44100, 600);
    Render::fillbackground(image);
    Render::drawwave(image, signalY);
    image.write(sineName);
}

void generateamplitudemodulationaiff();
```

### 示例 3：幅度调制音频生成

```cpp
const std::string sineName = "signalgenerators/21-amplified-modulation.aiff";
const double twoPI = 2 * M_PI;
const double sampleRate = 44100.0;
const double frequencyHz = 440.0;
const double frequencyRadian = twoPI / sampleRate;
double modifierFrequency = frequencyHz * 2.5;
double modifierIncrement = frequencyRadian * modifierFrequency;
double modifierAmplitude = 1.0;
double carrierPhase = 0;
double modifierPhase = 0;
double modifierScale = 1 / (1 + modifierAmplitude);
double modifierValue = 0;
double carrierIncrement = frequencyRadian * frequencyHz;

// Setup the audio file
AudioFile<float> a;
a.setNumChannels(1);
a.setBitDepth(24);
a.setSamplesPerChannel(44100);

for (int i = 0; i < a.getNumSamplesPerChannel(); ++i) {
    for (int channel = 0; channel < a.getNumChannels(); ++channel) {
        double modifierValue = 1.0 + (modifierAmplitude * sin(modifierPhase));
        a.samples[channel][i] = (sin(carrierPhase) * modifierValue) * modifierScale;
        carrierPhase += carrierIncrement;
        if (carrierPhase >= twoPI) {
            carrierPhase -= twoPI;
        }
        modifierPhase += modifierIncrement;
        if (modifierPhase >= twoPI) {
            modifierPhase -= twoPI;
        }
    }
}
a.save(sineName, AudioFileFormat::Aiff);
```

```cpp
void renderamplifiedmodulationpng() {
    const std::string sineName = "signalgenerators/22-amplified-modulation.png";
}
```

### 示例 4：幅度调制波形渲染（变量定义）

```cpp
const double twoPI = 2 * M_PI;
const double sampleRate = 44100.0;
const double frequencyInHz = 440.0;
double frequencyRadian = twoPI / sampleRate;
double modifierFrequency = frequencyInHz * 2.5;
double modifierIncrement = frequencyRadian * modifierFrequency;
double modifierAmplitude = 1.0;
double carrierPhase = 0;
double modifierScale = 1 / (1 + modifierAmplitude);
double modifierValue = 0;
double carrierIncrement = frequencyRadian * frequencyHz;
double value = 0;
std::vector<uint32_t> signalY;
signalY.resize(44100);

for (uint32_t i = 0; i < sampleRate; i++) {
    modifierValue = 1.0 + (modifierAmplitude * sin(modifierPhase));
    value = (sin(carrierPhase) * modifierValue) * modifierScale;
    if (value < 0.0) {
        signalY[i] = 300 + (300 * value);
    } else {
        signalY[i] = 300 - (300 * value);
    }
    carrierPhase += carrierIncrement;
    if (carrierPhase >= twoPI) {
        carrierPhase -= twoPI;
    }
    modifierPhase += modifierIncrement;
    if (modifierPhase >= twoPI) {
        modifierPhase -= twoPI;
    }
    png::image<png::rgb_pixel> image(44100, 600);
    Render::fillbackground(image);
    Render::drawwave(image, signalY);
    image.write(sineName);
}

void generateringmodulationaiff();
```

### 示例 5：环形调制音频生成

```cpp
const std::string sineName = "signalgenerators/23-ring-modulation.aiff";
const double twoPI = 2 * M_PI;
const double sampleRate = 44100.0;
const double frequencyInHz = 440.0;
const double frequencyRadius = twoPI / sampleRate;
double modifierAmplitude = 1.0;
double modifierFrequency = frequencyInHz * 2.5;
double modifierPhase = 0;
double modifierIncrement = frequencyRadius * modifierFrequency;
double carrierPhase = 0;
double carrierIncrement = frequencyRadius * frequencyHz;

// Set the audio file
AudioFile<float> a;
a.setNumChannels(1);
a.setBitDepth(24);
a.setSamplesPerChannel(44100);

for (int i = 0; i < a.getNumSamplesPerChannel(); ++i) {
    for (int channel = 0; channel < a.getNumChannels(); ++channel) {
        a.samples[channel][i] = sin(carrierPhase) * sin(modifierPhase) * modifierAmplitude;
        carrierPhase += carrierIncrement;
        if (carrierPhase >= twoPI) {
            carrierPhase -= twoPI;
        }
        modifierPhase += modifierIncrement;
        if (modifierPhase >= twoPI) {
            modifierPhase -= twoPI;
        }
    }
}
a.save(sineName, AudioFileFormat::Aiff);
```

```cpp
void renderringmodulationpng() {
    const std::string sineName = "signalgenerators/24-ring-modulation.png";
    const double twoPI = 2 * M_PI;
    const double sampleRate = 44100.0;
    const double frequencyInHz = 440.0;
}
```



## 附录 A：C++20 代码

```cpp
const double frequencyRadian = twoPI / sampleRate;
double modifieramplitude = 1.0;
double modifierFrequency = frequencyInHz * 2.5;
double modifierPhase = 0;
double modifierIncrement = frequencyRadian * modifierFrequency;
double carrierPhase = 0;
double carrierIncrement = frequencyRadian * frequencyHz;
double value = 0;
std::vector<uint32_t> signalY;
signalY.resize(44100);

for (uint32_t i = 0; i < sampleRate; ++i) {
  value = (sinf(carrierPhase) * modifieramplitude * Sinf(modifierPhase));
  if (value > 0.0) {
    signalY[i] = 300 - (300 * value);
  } else if (value < 0.0) {
    signalY[i] = 300 + (300 * fabs(value));
  }
  carrierPhase += carrierIncrement;
  if (carrierPhase >= twoPI) {
    carrierPhase -= twoPI;
  }
  modifierPhase += modifierIncrement;
  if (modifierPhase >= twoPI) {
    modifierPhase -= twoPI;
  }
}
png::image<png::rgb_pixel> image(44100, 600);
Render::fillbackground(image);
Render::drawwave(image, signalY);
image.write(sineName);
}

void generatenoiseaiff() {
    const std::string signalName = "signalgenerators/25-white-white-noise.aiff";
    std::random_device rd;
    std::mt19937 gen(rd());
    std::uniform_real_distribution<double> dis(-1.0, 1.0);


// Setup the audio file
```

## 附录 A：C++20 代码

```cpp
AudioFile<float> a;
a.setNumChannels(1);
a.setBitDepth(24);
a.setSamplesPerChannel(44100);
for (int i = 0; i < a.getNumSamplesPerChannel(); ++i) {
    for (int channel = 0; channel < a.getNumChannels(); ++channel) {
        a.samples[channel][i] = dis(gen);
    }
    a.save(sineName, AudioFileFormat::Aiff);
}

void rendernoisepng() {
    const std::string sineName = "signalgenerators/26-white-noise.png";
    const double sampleRate = 44100.0;
    std::random_device rd;
    std::mt19937 gen(rd);
    std::uniform_real_distribution<> dis(-1.0, 1.0);
    double value = 0;
    std::vector<uint32_t> signalY;
    signalY.resize(44100);
    for (uint32_t i = 0; i < sampleRate; ++i) {
        value = dis(gen);
        if (value >= 0.0) {
            signalY[i] = 300 - (300 * value);
        } else if (value < 0.0) {
            signalY[i] = 300 + (300 * fabs(value));
        }
    }
    ng::png::rgb_pixel> image(44100, 600);
    Render::fillbackground(image);
    Render::drawwave(image, signalY);
    image.write(sineName);
}

void generatepulsewaveiff() {
    const std::string sineName = "signalgenerators/27-pulse-wave.aiff";
    const double twoPI = 2 * M_PI;
    const double sampleRate = 44100.0;
    const double frequencyInHz = 440.0;
    const double frequencyRadian = twoPI / sampleRate;
    double maxNumber = floor(sampleRate / (2.0 * frequencyInHz)) - 1;
    double phaseIncrementDenominator = (M_PI / sampleRate) * frequencyInHz;
    double phaseIncrementNumerator = phaseIncrementDenominator * ((2.0 * maxNumber) + 1);
    double phaseDenominator = 0.0;
    double phaseNumerator = 0.0;
    double amplitudeScale = 1.0 / (2.0 * maxNumber);
    // 设置音频文件
    AudioFile a;
    a.setNumChannels(1);
    a.setBitDepth(24);
    a.setNumSamplesPerChannel(44100);

    for (int i = 0; i < a.getNumSamplesPerChannel(); ++i) {
        for (int channel = 0; channel < a.getNumChannels(); ++channel) {
            double Denominator = sin(phaseDenominator);
            if (Denominator == 0.0) {
                value = 1.0;
            } else {
                value = amplitudeScale * ((sin(phaseNumerator) / Denominator);
            }
            a.samples[channel][i] = value;
            phaseDenominator += phaseIncrementDenominator;
            if (phaseDenominator >= twoPI) {
                phaseDenominator -= twoPI;
            }
            phaseNumerator += phaseIncrementNumerator;
            if (phaseNumerator >= twoPI) {
                phaseNumerator -= twoPI;
            }
        }
    }
    a.save(sineName, AudioFormat::Aiff);
}

void renderpulsewavepng() {
    const std::string sineName = "signalgenerators/28-pulse-wave.png";
    const double twoPI = 2 * M_PI;
    const double sampleRate = 44100.0;
    const double frequencyHz = 440.0;
    const double frequencyRadian = twoPI / sampleRate;
    double maxNumber = floor(phaseDenominator / (2.0 * frequencyHz) - 0.5 - 1;
    double phaseIncrementDenominator = (M_PI / sampleRate) * frequencyHz;
    double phaseIncrementNumerator = phaseIncrementDenominator * ((2.0 * maxNumber) + 1);
    double phaseDenominator = 0.0;
    double phaseNumerator = 0.0;
    double amplitudeScale = 1.0 / (2.0 * maxNumber);
    double value = 0;
    std::vector<uint32_t> signalY;
    signalY.resize(44100);
    for (uint32_t i = 0; i < sampleRate; i++) {
        double Denominator = sin(phaseDenominator);
        if (Denominator == 0.0) {
            value = 1.0;
        } else {
            value = amplitudeScale * ((sin(phaseNumerator) / Denominator) - 1);
        }
        if (value >= 0.0) {
            signalY[i] = 300 - (300 * value);
        } else if (value < 0.0) {
            signalY[i] = 300 + (300 * fabs(value));
        }
        phaseDenominator += phaseIncrementDenominator;
        if (phaseDenominator >= twoPI) {
            phaseDenominator -= twoPI;
        }
        phaseNumerator += phaseIncrementNumerator;
        if (phaseNumerator >= twoPI) {
            phaseNumerator -= twoPI;
        }
    }
    png::image<rgb_pixel> image(44100, 600);
    Render::fillbackground(image);
    Render::drawwave(image, signalY);
    image.write(sineName);
}

namespace Render {
    void fillbackground(png::image<rgb_pixel>& image) {
        png::rgb_pixel px(0x04, 0x13, 0x31);
        for (uint32_t y = 0; y < image.height(); ++y) {
            for (uint32_t x = 0; x < image.get_width(); ++x) {
                image.set_pixel(x, y, px);
            }
        }
    }
    void drawpx(png::image<rgb_pixel>& image, int x, int y) {
        if ((x >= 0) && (x < image.get_width()) && (y >= 0) && (y < image.get_height())) {
            png::rgb_pixel px(0x7a, 0xb1, 0xe3);
            image.set_pixel(x, y, px);
        }
    }
    void drawline(png::image<rgb_pixel>& image, int x1, int y1, int x2, int y2) {
        int x, y, dx, dy, dx1, px, xe, yi;
        dx = x2 - x1; dy = y2 - y1;
        if (dx == 0) {
            if (y2 < y1) std::swap(y1, y2);
            for (y = y1; y <= y2; ++y) {
                drawpx(image, x1, y);
                return;
            }
        }
        if (dy == 0) {
            if (x2 < x1) std::swap(x1, x2);
            for (x = x1; x <= x2; ++x) {
                drawpx(image, x, y1);
                return;
            }
        }
    }
}
```

## 附录 A：C++20 代码

```cpp
sampleLength = sampleRate * duration;
A_1 = 0.2; A_r = 0.9; D_1 = 0.1; D_r = 0.7; S_1 = 0.4; S_r = D_r; R_1 = 0.3; R_r = 0.0;

~Envelope() {}
void generateenvelope(std::vector<float>& env) {
    env.resize(sampleLength);
    uint32_t height = 600;
    coords[0] = 0; // x1
    coords[1] = height; // y1
    coords[2] = sampleLength * A_1; // y2
    coords[3] = height - height * A_1; // y2
    coords[4] = sampleLength * (A_1 + D_1); // x3
    coords[5] = height - D_r; // y3
    coords[6] = sampleLength * (A_1 + D_1 + S_1); // x4
    coords[7] = height - S_r; // y4
    coords[8] = sampleLength; // x5
    coords[9] = height; // y5
    bridge(env, coords[0], coords[1], coords[2], coords[3]);
    bridge(env, coords[2], coords[3], coords[4], coords[5]);
    bridge(env, coords[4], coords[5], coords[6], coords[7], coords[8], coords[9]);
}
void generate2(std::vector<float>& env) {
    env.resize(sampleLength);
    uint32_t height = 600;
    coords[0] = 0; // x1
    coords[1] = height; // y1
    coords[2] = sampleLength; // x5
    coords[3] = 0; // y5
    bridge(env, coords[0], coords[1], coords[2], coords[3]);
}
void generate3(std::vector<float>& env) {
    env.resize(sampleLength);
    uint32_t height = 600;
    coords[0] = 0; // x1
    coords[1] = 0; // y1
    coords[2] = sampleLength; // x5
    coords[3] = height; // y5
    bridge(env, coords[0], coords[1], coords[2], coords[3]);
}
```



## 代码片段 1

```cpp
void applylyenvelope(std::vector<float>& v, std::vector<float>& env) {
    for (uint32_t i = 0; i < env.size(); ++i) {
        v[i] = v[i] * env[i];
    }
}

private:
    void setpt(std::vector<float>& env, uint32_t x, uint32_t y) {
        if ((x > 0) && (x < sampleLength) && ((y >= 0) && (y < 600))) {
            env[x] = ((600.0 - float(y)) / 600.0);
        }
    }

    void bridge(std::vector<float>& env, uint32_t x1, uint32_t y1, uint32_t x2, uint32_t y2) {
        int x, y, dx, dy, dx1, dy1, px, py, xe, i;
        dx = x2 - x1;
        dy = y2 - y1;
        if (dx == 0) {
            if (y2 < y1) std::swap(y1, y2);
            for (y = y1; y <= y2; y++)
                setpt(env, x1, y);
            return;
        }
        if (dy == 0) {
            if (x2 < x1) std::swap(x1, x2);
            for (x = x1; x <= x2; x++)
                setpt(env, x, y1);
            return;
        }
        dx1 = std::abs(dx);
        dy1 = std::abs(dy);
        px = 2 * dy1 - dx1;
        py = 2 * dx1 - dy1;
        if (dy1 <= dx1) {
            if (dx >= 0) {
                x = x1;
                y = y1;
                xe = x2;
            } else {
                x = x2;
                y = y2;
                xe = x1;
            }
            setpt(env, x, y);
            for (i = 0; x < xe; i++) {
                x = x + 1;
                if (px < 0)
                    px = px + 2 * dy1;
                else {
                    if ((dx < 0) || (dx > 0))
                        y = y + 1;
                    px = px + 2 * (dy1 - dx1);
                }
                setpt(env, x, y);
            }
        } else {
            if (dy >= 0) {
                x = x1;
                y = y1;
                xe = y2;
            } else {
                x = x2;
                y = y2;
                xe = y1;
            }
            setpt(env, x, y);
            for (i = 0; y < xe; i++) {
                y = y + 1;
                if (py <= 0)
                    py = py + 2 * dx1;
                else {
                    if ((dy < 0) || (dy > 0))
                        x = x + 1;
                    py = py + 2 * (dx1 - dy1);
                }
                setpt(env, x, y);
            }
        }
    }
```

## 代码片段 2

```cpp
float A_l;
float A_r;
float D_l;
float D_r;
float S_l;
float S_r;
float R_l;
float R_r;

protected:
    uint32_t sampleLength;
    uint32_t coords[10];
};
```

## MoogFilter.hpp - 1628 字节

```cpp
#ifndef MOOG_H
#define MOOG_H
```

```cpp
#define MOOG_PI 3.1415926535897238462648327528
#include <vector>
```

```cpp
namespace Moog
{
    class MoogFilter
    {
    public:
        MoogFilter(float sampleRate) : sampleRate(sampleRate)
        {
            memset(stage, 0, sizeof(stage));
            memset(delay, 0, sizeof(delay));
            SetCutoff(1000.0f);
            SetResonance(0.1f);
        }
        ~MoogFilter() {}

        void Process(std::vector<float>& samples, uint32_t n)
        {
            for (int s = 0; s < n; ++s)
            {
                float x = samples[s] - resonance * stage[3];
                
                // 四极点滤波器（双线性变换）
                stage[0] = x * p - k * stage[0];
                stage[1] = stage[0] * p - k * stage[1];
                stage[2] = stage[1] * p - k * stage[2];
                stage[3] = stage[2] * p - k * stage[3];

                // 削波带限 sigmoid
                stage[3] = (stage[3] * stage[3]) / 6.0;

                delay[0] = x;
                delay[1] = stage[0];
                delay[2] = stage[1];
                delay[3] = stage[2];
            }
        }

        void SetResonance(float r) {
            resonance = r * (t2 + 6.0 * t1) / (t2 - 6.0 * t1);
        }

        void SetCutoff(float c) {
            cutoff = 2.0 * c / sampleRate;
            p = cutoff * (1.8 - cutoff);
            k = 2.0 * sin(cutoff * MOOG_PI) - 1.0;
            t1 = (1.0 - p) * 1.386249;
            t2 = 12.0 + t1 * t1;
            SetResonance(resonance);
        }

        float GetResonance() { return resonance; }
        float GetCutoff() { return cutoff; }

    private:
        double stage[4];
        double delay[4];
        double p;
        double k;
        double t1;
        double t2;

    protected:
        float cutoff;
        float resonance;
        float sampleRate;
    };
}
#endif
```

## 01-additive.cpp - 21478 字节

```cpp
// 编译: clang++ -std=c++20 01-additive.cpp -o 01-additive
#define USE_MATH_DEFINES
#include <cmath>
#include <vector>
#include <random>
#include <filesystem>
#include <indicators/indicators.hpp>
#include <png.hpp>
#include "AudioFile.h"

namespace Renderer
{
    void fill(image<rgb_pixel>& image, int x, int y);
    void draw(image<rgb_pixel>& image, int x1, int y1, int x2, int y2);
    void line(image<rgb_pixel>& image, int x1, int y1, int x2, int y2);
    void rect(image<rgb_pixel>& image, int x1, int y1, int x2, int y2);
    void circle(image<rgb_pixel>& image, int x, int y, int radius);
    void text(image<rgb_pixel>& image, int x, int y, const std::string& text);
}

namespace SignalGenerators
{
    void gain(std::vector<float>& v, float amount);
    void normalize(std::vector<float>& v);
    void generatesinewave(std::vector<float>& v, float duration, float frequency);
    void generatenoise(std::vector<float>& v, float duration, float amplitude);
    void saveaudiofile(std::vector<float>& v, const std::string& filename);
}

int main() {
    namespace fs = std::filesystem;
    if (!fs::exists("output")) {
        fs::create_directory("output");
    }

    const int duration = 5;
    const double sampleRate = 44100.0;
    std::vector<float> buffer;

    ProgressBar bar{
        option::BarWidth{50},
        option::Empty{},
        option::ForegroundColor(Color::cyan),
        option::FontStyles(std::vector<FontStyle>{FontStyle::bold}),
    };

    for (int i = 0; i < 10; i++) {
        buffer.clear();
        SignalGenerators::generatesinewave(buffer, duration, 110.0 * pow(2, i));
        SignalGenerators::gain(buffer, 0.5);
        SignalGenerators::normalize(buffer);
        SignalGenerators::saveaudiofile(buffer, "output/osc_" + std::to_string(i) + ".aiff");

        bar.update((i + 1) / 10.0, "Setting: Sine Oscillator" + std::to_string(i + 1) + " @ " + std::to_string((int)(110.0 * pow(2, i))) + " Hz (" + std::to_string(i + 1) + "/10");
    }

    return 0;
}
```

## 附录 A：C++20 代码

```cpp
// 更新进度
bar_progress(6);
bar_set_option(option::PostfixText("Setting: Sine Oscillator3 @ 165 Hz 3/35"));

SignalGenerators::generatesinwave(osc3, duration, 165);
SignalGenerators::gain(osc3, 0.7);
SignalGenerators::saveaudiofile(osc3, "05-osc3.aiff");
Render::saveimagefile(osc3, "06-osc3.png");
```

```cpp
// 更新进度
bar_progress(8);
bar_set_option(option::PostfixText("Setting: Sine Oscillator4 @ 220 Hz 4/35"));

SignalGenerators::generatesinwave(osc4, duration, 220);
SignalGenerators::gain(osc4, 0.8);
SignalGenerators::saveaudiofile(osc4, "07-osc4.aiff");
Render::saveimagefile(osc4, "08-osc4.png");
```

```cpp
// 更新进度
bar_progress(11);
bar_set_option(option::PostfixText("Setting: Sine Oscillator5 @ 275 Hz 5/35"));

SignalGenerators::generatesinwave(osc5, duration, 275);
SignalGenerators::gain(osc5, 0.4);
SignalGenerators::saveaudiofile(osc5, "09-osc5.aiff");
Render::saveimagefile(osc5, "10-osc5.png");
```

```cpp
// 更新进度
bar_progress(14);
bar_set_option(option::PostfixText("Setting: Sine Oscillator6 @ 330 Hz 6/35"));

SignalGenerators::generatesinwave(osc6, duration, 330);
SignalGenerators::gain(osc6, 0.7);
SignalGenerators::saveaudiofile(osc6, "11-osc6.aiff");
Render::saveimagefile(osc6, "12-osc6.png");
```

```cpp
// 更新进度
bar_progress(17);
bar_set_option(option::PostfixText("Setting: Sine Oscillator7 @ 385 Hz 7/35"));

SignalGenerators::generatesinwave(osc7, duration, 385);
SignalGenerators::gain(osc7, 0.3);
SignalGenerators::saveaudiofile(osc7, "13-osc7.aiff");
Render::saveimagefile(osc7, "14-osc7.png");
```

```cpp
// 更新进度
bar.set_progress(20);
bar.set_option(option::PostfixText("Setting: Sine Oscillator8 @ 440 Hz 8/35"));

SignalGenerators::generatesinwave(osc8, duration, 440);
SignalGenerators::gain(osc8, 0.9);
SignalGenerators::saveaudiofile(osc8, "15-osc8.aiff");
Render::saveimagefile(osc8, "16-osc8.png");
```

```cpp
// 更新进度
bar.set_progress(23);
bar.set_option(option::PostfixText("Setting: Sine Oscillator9 @ 495 Hz 9/35"));

SignalGenerators::generatesinwave(osc9, duration, 490);
SignalGenerators::gain(osc9, 0.5);
SignalGenerators::saveaudiofile(osc9, "17-osc8.aiff");
Render::saveimagefile(osc9, "18-osc8.png");
```

```cpp
// 更新进度
bar.set_progress(26);
bar.set_option(option::PostfixText("Setting: Sine Oscillator10 @ 550 Hz 10/35"));

SignalGenerators::generatesinwave(osc10, duration, 550);
SignalGenerators::gain(osc10, 0.5);
SignalGenerators::saveaudiofile(osc10, "19-osc8.aiff");
Render::saveimagefile(osc10, "20-osc8.png");
```



```cpp
// 更新进度
bar.set_progress(29);
bar.set_option(option::PostfixText("Setting: Sine Oscillator11 @ 605 Hz 11/35"));

SignalGenerators::generatesinwave(osc11, duration, 605);
SignalGenerators::gain(osc11, 0.5);
SignalGenerators::saveaudiofile(osc11, "21-osc8.aiff");
Render::saveimagefile(osc11, "22-osc8.png");
```

```cpp
SignalGenerators::gain(osc12, 0.5);
SignalGenerators::saveaudiofile(osc12, "23-osc8.aiff");
Render::saveimagefile(osc12, "24-osc8.png");
// 更新进度
bar.set_progress(34);
bar.set_option(option::PostfixText("Setting: Sine Oscillator13 @ 715 Hz 13/35"));

SignalGenerators::generatesinwave(osc13, duration, 715);
SignalGenerators::saveaudiofile(osc13, "25-osc8.aiff");
Render::saveimagefile(osc13, "26-osc8.png");
```

```cpp
// 更新进度
bar.set_progress(37);
bar.set_option(option::PostfixText("Setting: Sine Oscillator14 @ 770 Hz 14/35"));

SignalGenerators::generatesinwave(osc14, duration, 770);
SignalGenerators::gain(osc14, 0.7);
SignalGenerators::saveaudiofile(osc14, "27-osc8.aiff");
Render::saveimagefile(osc14, "28-osc8.png");
```

```cpp
// 更新进度
bar.set_progress(40);
bar.set_option(option::PostfixText("Setting: Sine Oscillator15 @ 825 Hz 15/35"));

SignalGenerators::generatesinwave(osc15, duration, 825);
SignalGenerators::gain(osc15, 0.9);
SignalGenerators::saveaudiofile(osc15, "29-osc8.aiff");
Render::saveimagefile(osc15, "30-osc8.png");
```

```cpp
// 更新进度
bar.set_progress(43);
bar.set_option(option::PostfixText("Setting: Sine Oscillator16 @ 880 Hz 16/35"));

SignalGenerators::generatesinwave(osc16, duration, 880);
SignalGenerators::gain(osc16, 0.9);
SignalGenerators::saveaudiofile(osc16, "31-osc8.aiff");
Render::saveimagefile(osc16, "32-osc8.png");
```

```cpp
// 更新进度
bar.set_progress(46);
bar.set_option(option::PostfixText("Setting: Sine Oscillator17 @ 935 Hz 17/35"));

SignalGenerators::generatesinwave(osc17, duration, 935);
SignalGenerators::gain(osc17, 0.8);
SignalGenerators::saveaudiofile(osc17, "33-osc8.aiff");
Render::saveimagefile(osc17, "34-osc8.png");
```

```cpp
// 更新进度
bar.set_progress(49);
bar.set_option(option::PostfixText("Setting: Sine Oscillator18 @ 990 Hz 18/35"));

SignalGenerators::generatesinwave(osc18, duration, 990);
SignalGenerators::gain(osc18, 0.8);
SignalGenerators::saveaudiofile(osc18, "35-osc8.aiff");
Render::saveimagefile(osc18, "36-osc8.png");
```

```cpp
// 更新进度
bar.set_progress(51);
bar.set_option(option::PostfixText("Setting: Sine Oscillator19 @ 1045 Hz 19/35"));

SignalGenerators::generatesinwave(osc19, duration, 1045);
SignalGenerators::gain(osc19, 0.7);
SignalGenerators::saveaudiofile(osc19, "37-osc8.aiff");
Render::saveimagefile(osc19, "38-osc8.png");
```

```cpp
// 更新进度
bar.set_progress(54);
bar.set_option(option::PostfixText("Setting: Sine Oscillator20 @ 1100 Hz 20/35"));

SignalGenerators::generatesinwave(osc20, duration, 1100);
SignalGenerators::gain(osc20, 0.7);
SignalGenerators::saveaudiofile(osc20, "39-osc8.aiff");
Render::saveimagefile(osc20, "40-osc8.png");
```

```cpp
// 更新进度
bar.set_progress(57);
bar.set_option(option::PostfixText("Setting: Sine Oscillator21 @ 1155 Hz 21/35"));

SignalGenerators::generatesinwave(osc21, duration, 1155);
SignalGenerators::gain(osc21, 0.6);
SignalGenerators::saveaudiofile(osc21, "41-osc8.aiff");
Render::saveimagefile(osc21, "42-osc8.png");
```

```cpp
// 更新进度
bar.set_progress(60);
bar.set_option(option::PostfixPostfix("Setting: Sine Oscillator22 @ 1210 Hz 22/35"));

SignalGenerators::generatesinwave(osc22, duration, 1210);
SignalGenerators::gain(osc22, 0.6);
SignalGenerators::saveaudiofile(osc22, "43-osc8.aiff");
Render::saveimagefile(osc22, "44-osc8.png");
```

```cpp
// 更新进度
bar.set_progress(63);
bar.set_option(option::PostfixText("Setting: Sine Oscillator23 @ 1265 Hz 23/35"));

SignalGenerators::generatesinwave(osc23, duration, 1265);
SignalGenerators::gain(osc23, 0.5);
SignalGenerators::saveaudiofile(osc23, "45-osc8.aiff");
Render::saveimagefile(osc23, "46-osc8.png");
```

```cpp
// 更新进度
bar.set_progress(71);
bar.set_option(option::PostfixText("Setting: Sine Oscillator25 @ 1375 Hz 25/35"));

SignalGenerators::generatesinwave(osc25, duration, 1375);
SignalGenerators::gain(osc25, 0.4);
SignalGenerators::saveaudiofile(osc25, "49-osc8.aiff");
Render::saveimagefile(osc25, "50-osc8.png");
```

```cpp
// 更新进度
bar.set_progress(71);
bar.set_option(option::PostfixText("Setting: Sine Oscillator26 @ 1400 Hz 26/35"));

SignalGenerators::generatesinwave(osc26, duration, 1430);
SignalGenerators::gain(osc26, 0.4);
SignalGenerators::saveaudiofile(osc26, "51-osc8.aiff");
Render::saveimagefile(osc26, "52-osc8.png");
```

## 附录 A：C++20 代码



```cpp
332  // 更新进度
333  bar.set_progress(74);
334  bar.set_option(option::PostText("设置：正弦振荡器27 @ 1485 Hz 27/35"));

336  SignalGenerators::generatesinewave(osc27, duration, 1485);
337  SignalGenerators::gain(osc27, 0.3);
338  SignalGenerators::saveaudiofile(osc27, "53-oscc8.aiff");
339  Render::saveimagefile(osc27, "54-oscc8.png");

341  // 更新进度
342  bar.set_progress(77);
343  bar.set_option(option::PostText("设置：正弦振荡器28 @ 1540 Hz 28/35"));

345  SignalGenerators::generatesinewave(osc28, duration, 1540);
346  SignalGenerators::gain(osc28, 0.3);
347  SignalGenerators::saveaudiofile(osc28, "55-oscc8.aiff");
348  Render::saveimagefile(osc28, "56-oscc8.png");

350  // 更新进度
351  bar.set_progress(80);
352  bar.set_option(option::PostText("设置：正弦振荡器29 @ 1595 Hz 29/35"));

354  SignalGenerators::generatesinewave(osc29, duration, 1595);
355  SignalGenerators::gain(osc29, 0.3);
356  SignalGenerators::saveaudiofile(osc29, "57-oscc8.aiff");
357  Render::saveimagefile(osc29, "58-oscc8.png");

359  // 更新进度
360  bar.set_progress(83);
361  bar.set_option(option::PostText("设置：正弦振荡器30 @ 1650 Hz 30/35"));

363  SignalGenerators::generatesinewave(osc30, duration, 1650);
364  SignalGenerators::gain(osc30, 0.3);
365  SignalGenerators::saveaudiofile(osc30, "59-oscc8.aiff");
366  Render::saveimagefile(osc30, "60-oscc8.png");

368  // 更新进度
369  bar.set_progress(86);
370  bar.set_option(option::PostText("设置：正弦振荡器31 @ 1705 Hz 31/35"));

372  SignalGenerators::generatesinewave(osc31, duration, 1705);
373  SignalGenerators::gain(osc31, 0.3);
375  SignalGenerators::saveaudiofile(osc31, "61-osc8.aiff");
376  Render::saveimagefile(osc31, "62-osc8.png");

378  // 更新进度
379  bar.set_progress(89);
380  bar.set_option(option::PostText("设置：正弦振荡器32 @ 1760 Hz 32/35"));

382  SignalGenerators::generatesinewave(osc32, duration, 1760);
383  SignalGenerators::gain(osc32, 0.3);
384  SignalGenerators::saveaudiofile(osc32, "63-osc8.aiff");
385  Render::saveimagefile(osc32, "64-osc8.png");

387  // 更新进度
388  bar.set_progress(91);
389  bar.set_option(option::PostText("设置：噪声振荡器33 33/35"));

391  SignalGenerators::generatenoise(osc33, duration);
392  SignalGenerators::gain(osc33, 0.1);
393  SignalGenerators::saveaudiofile(osc33, "65-osc9.aiff");
394  Render::saveimagefile(osc33, "66-osc9.png");

396  // 更新进度
397  bar.set_progress(94);
398  bar.set_option(option::PostText("混合所有 33 个振荡器 34/35"));

400  mixer.resize(duration * sampleRate);
401  SignalGenerators::addwaves(osc1, osc2, mixer);
402  SignalGenerators::addwaves(mixer, osc3, mixer);
403  SignalGenerators::addwaves(mixer, osc4, mixer);
404  SignalGenerators::addwaves(mixer, osc5, mixer);
405  SignalGenerators::addwaves(mixer, osc6, mixer);
406  SignalGenerators::addwaves(mixer, osc7, mixer);
407  SignalGenerators::addwaves(mixer, osc8, mixer);
408  SignalGenerators::addwaves(mixer, osc9, mixer);
409  SignalGenerators::addwaves(mixer, osc10, mixer);
410  SignalGenerators::addwaves(mixer, osc11, mixer);
411  SignalGenerators::addwaves(mixer, osc12, mixer);
412  SignalGenerators::addwaves(mixer, osc13, mixer);
413  SignalGenerators::addwaves(mixer, osc14, mixer);
414  SignalGenerators::addwaves(mixer, osc15, mixer);
415  SignalGenerators::addwaves(mixer, osc16, mixer);
416  SignalGenerators::addwaves(mixer, osc17, mixer);
417  SignalGenerators::addwaves(mixer, osc18, mixer);
418  SignalGenerators::addwaves(mixer, osc19, mixer);
419  SignalGenerators::addwaves(mixer, osc20, mixer);
420  SignalGenerators::addwaves(mixer, osc21, mixer);
421  SignalGenerators::addwaves(mixer, osc22, mixer);
422  SignalGenerators::addwaves(mixer, osc23, mixer);
423  SignalGenerators::addwaves(mixer, osc24, mixer);
424  SignalGenerators::addwaves(mixer, osc25, mixer);
425  SignalGenerators::addwaves(mixer, osc26, mixer);
426  SignalGenerators::addwaves(mixer, osc27, mixer);
427  SignalGenerators::addwaves(mixer, osc28, mixer);
428  SignalGenerators::addwaves(mixer, osc29, mixer);
429  SignalGenerators::addwaves(mixer, osc30, mixer);
430  SignalGenerators::addwaves(mixer, osc31, mixer);
431  SignalGenerators::addwaves(mixer, osc32, mixer);
432  SignalGenerators::addwaves(mixer, osc33, mixer);
433  SignalGenerators::normalize(mixer);
434  SignalGenerators::saveaudiofile(mixer, "67-mixed.aiff");
435  Render::saveimagefile(mixer, "68-mixed.png");

436  // 更新进度
437  bar.set_progress(97);
438  bar.set_option(option::PostText("添加 ADSR 包络器 35/35"));

439  ADSR Envelope(sampleRate, duration);
440  en.generate(envelope);
441  en.applyenvelope(mixer);
442  SignalGenerators::normalize(mixer);
443  Render::saveimagefile(mixer, "69-envelope.png");
444  SignalGenerators::saveaudiofile(mixer, "70-mixedenveloped.aiff");
445  Render::saveimagefile(mixer, "71-mixedenveloped.png");

446  // 更新进度
447  bar.set_progress(100);
448  bar.set_option(option::PostText("完成 35/35"));

449  // 显示光标
450  show_console_cursor(true);
451  return 0;
```

## `SignalGenerators` 命名空间实现

```cpp
namespace SignalGenerators
{
  void gain(std::vector<float>& v, double gain) {
    for (uint32_t i = 0; i < v.size(); ++i) {
      v[i] = v[i] * gain;
    }
  }

  void normalize(std::vector<float>& v) {
    float max = 0.0, value = 0.0;
    for (uint32_t i = 0; i < v.size(); ++i) {
        value = v[i];
        if (value > max) max = value;
    }
    for (uint32_t i = 0; i < v.size(); ++i) {
        v[i] = (v[i] / max) * 0.707;
    }
  }

  void addwaves(std::vector<float>& v1, std::vector<float>& v2, std::vector<float>& v3) {
    for (uint32_t i = 0; i < v1.size(); ++i) {
        v3[i] = v1[i] + v2[i];
    }
  }

  void generatesinwave(std::vector<float>& v, int duration, float frequencyInHz) {
    const double sampleRate = 44100.0;
    for (uint32_t i = 0; i < sampleRate * duration; ++i) {
        v.push_back(sin((static_cast<double>(i) / sampleRate) * frequencyInHz));
    }
  }

  void generenoise(std::vector<float>& v, int duration) {
    const double sampleRate = 44100.0;
    std::random_device rd;
    std::mt19937 gen(rd);
    std::uniform_real_distribution<> dis(-1.0, 1.0);
    for (uint32_t i = 0; i < sampleRate * duration; ++i) {
        v.push_back(dis(gen));
    }
  }
}
```

# 附录：C++20 代码

```cpp
590    if ((dx < 0 && dy < 0)) || ((dx > 0 && dy > 0)) y = y + 1; else y = y
591    px = px + 2 * (dy - dx1);
592  }
593    drawpx(image, x, y);
594  }
595    else
596    {
597
598
        if (dy >= 0)
599        {
600            x = x1; y = y1; else y = y2;
601        }
602        else
603        {
604            x = x2; y = y2; else y = y1;
605        }
606        drawpx(image, x, y);
607        for (i = 0; i < y; i++)
608        {
609            y = y + 1;
610            if (py <= 0)
611                py = py + 2 * dx1;
612            else
613                {
614                    if ((dx < 0 && dy < 0)) || ((dx > 0 && dy > 0)) x = x + 1; else x = x
615                    py = py + 2 * (dx1 - dy1);
616                }
617            }
618        }
619  }
620    drawpx(image, x, y);

void drawwave(png::image<png::rgb_pixel>& image, std::vector<uint32_t>& signalY)
622  {
623    uint32_t y = 0, ox, oy = 0;
624    for (uint32_t x = 0; x < image.get_width(); ++x)
625        {
626            y = signalY[x];
627            if (x == 0) {ox = x; oy = y};
628            drawline(image, x, y, ox, oy);
629            ox = x; oy = y;
630        }
631  }
```



## C++ 代码示例

### 渲染与保存图像函数

```cpp
void normalizedtoimg(png::image<png::rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2) {
    uint32_t halfHeight = image.get_height() / 2;
    double value = 0.0;
    if (v2.size() == 0 || v2.size() > v1.size()) {
        v2.resize(v1.size());
    }

    for (uint32_t i = 0; i < v1.size(); ++i) {
        value = v1[i];
        if (value >= 0.0) {
            v2[i] = halfHeight - (halfHeight * value);
        } else if (value < 0.0) {
            v2[i] = halfHeight + (halfHeight * abs(value));
        }
    }
}

void renderimage(png::image<png::rgb_pixel>& image, std::vector<uint32_t>& v) {
    fillbackground(image);
    drawwave(image, v);
}

void saveimagefile(std::vector<uint32_t>& v, std::string filename) {
    const std::string path = "additive/";
    png::image<png::rgb_pixel> image(441000, 600);
    renderimage(image, v);
    image.write(path + filename);
}

void saveimagefile(std::vector<float>& v2, std::string filename) {
    const std::string path = "additive/";
    png::image<png::rgb_pixel> image(441000, 600);
    std::vector<uint32_t> v;
    normalizedtoimg(image, v2, v);
    renderimage(image, v);
    image.write(path + filename);
}

void normalizedenetoimg(png::image<png::rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2) {
    uint32_t height = image.get_height();
    if (v2.size() == 0 || v2.size() > v1.size()) {
        v2.resize(v1.size());
    }
    for (uint32_t i = 0; i < v1.size(); ++i) {
        v2[i] = height - (height * v1[i]);
    }
}

void saveenvelopeimage(std::vector<uint32_t>& v, std::string filename) {
    const std::string path = "additive/";
    png::image<png::rgb_pixel> image(441000, 600);
    renderimage(image, v);
    image.write(path + filename);
}

void saveenvelopeimage(std::vector<float>& v2, std::string filename) {
    const std::string path = "additive/";
    png::image<png::rgb_pixel> image(441000, 600);
    std::vector<uint32_t> v;
    normalizedtoimg(image, v2, v);
    renderimage(image, v);
    image.write(path + filename);
}
```

### 主流程代码

```cpp
SignalGenerators::normalize(mixer);
SignalGenerators::addwaves(mixer, osc3, mixer);
SignalGenerators::normalize(mixer);
Render::saveimagefile(mixer, "01-mixerpreosc4.png");
SignalGenerators::saveaudiofile(mixer, "02-mixerpreosc4.aiff");
SignalGenerators::addwaves(mixer, osc4, mixer);
SignalGenerators::normalize(mixer);
Render::saveimagefile(mixer, "03-mixerpostosc4.png");
SignalGenerators::saveaudiofile(mixer, "04-mixerpostosc4.aiff");
// 更新过程
bar.set_progress(62);
bar.set_option(option::PostText("混合荡器 1 到 4 混合 6/8"));
Render::saveimagefile(mixer, "05-prefilter.png");
SignalGenerators::saveaudiofile(mixer, "06-prefilter.aiff");
mf.Process(mixer, mixer.size());
SignalGenerators::normalize(mixer);
Render::saveimagefile(mixer, "07-postfilter.png");
SignalGenerators::saveaudiofile(mixer, "08-postfilter.aiff");
// 更新进度
bar.set_progress(75);
bar.set_option(option::PostText("向混合信号中添加 MoogFilter 7/8"));
ADSR::Envelope env(sampleRate, duration);
env.generateenvelope(env);
Render::saveimagefile(env, "09-envelope.png");
// 更新进度
bar.set_progress(87);
bar.set_option(option::PostText("向混合信号中添加 ADSR 包络 8/8"));
env.applyenvelope(mixer, env);
Render::saveimagefile(mixer, "10-envelopedmix.png");
SignalGenerators::saveaudiofile(mixer, "11-envelopedmix.aiff");
// 更新进度
bar.set_progress(100);
bar.set_option(option::PostText("完成 8/8"));
```

### 显示光标

```cpp
show_console_cursor(true);
return 0;
}
```

### `SignalGenerators` 命名空间

```cpp
namespace SignalGenerators {
```

### 信号处理函数

#### `gain()`

```cpp
void gain(std::vector<float>& v, double gain) {
    for (uint32_t i = 0; i < v.size(); ++i) {
        v[i] = v[i] * gain;
    }
}
```

#### `normalize()`

```cpp
void normalize(std::vector<float>& v) {
    float max = 0.0, value = 0.0;
    for (uint32_t i = 0; i < v.size(); ++i) {
        value = v[i];
        if (value > max) max = value;
    }
    // scale std::ceil(max);
    for (uint32_t i = 0; i < v.size(); ++i) {
        v[i] = (v[i] / max) + 0.707;
    }
}
```

#### `addwaves()`

```cpp
void addwaves(std::vector<float>& v1, std::vector<float>& v2, std::vector<float>& v3) {
    for (uint32_t i = 0; i < v1.size(); ++i) {
        v3[i] = v1[i] + v2[i];
    }
}
```

#### `generatetrianglewave()`

```cpp
void generatetrianglewave(std::vector<float>& v, int duration, double frequencyInHz) {
    const double sampleRate = 44100.0;
    for (uint32_t i = 0; i < sampleRate * duration; ++i) {
        v.push_back(M_2_PI * asin(sin(frequencyInHz * 2 * M_PI * i / sampleRate)));
    }
}
```

#### `generatesawtoothwave()`

```cpp
void generatesawtoothwave(std::vector<float>& v, int duration, double frequencyInHz) {
    const double sampleRate = 44100.0;
    double period = sampleRate / frequencyInHz;
    std::vector<float> temp;
    for (uint32_t i = 0; i < duration; ++i) {
        temp.push_back(-2 / M_PI * atan(1 / tan(frequencyInHz * M_PI * i / sampleRate)));
        v.push_back(temp[temp.size() - (i % temp.size())]);
    }
}
```

#### `generatesquarewave()`

```cpp
void generatesquarewave(std::vector<float>& v, int duration, double frequencyInHz) {
    const double sampleRate = 44100.0;
    double period = period * frequencyInHz;
    double dutyCycle = period * 0.5;
    double ss = 0.0;
    for (uint32_t i = 0; i < sampleRate * duration; ++i) {
        v.push_back(-2 / M_PI * atan(1 / tan(frequencyInHz * M_PI * i / sampleRate)));
        if ((i % period) >= 0 && (i % period) < dutyCycle) {
            ss = 0.7;
        } else {
            ss = -0.7;
        }
    }
    v[0] = 0;
    v[v.size() - 1] = 0;
}
```

#### `generatethirtiesfquarewave()`

```cpp
void generatethirtiesfquarewave(std::vector<float>& v, int duration, double frequencyInHz) {
    const double sampleRate = 44100.0;
    double period = sampleRate / frequencyInHz;
    double dutyCycle = period * 0.35;
    double ss = 0.0;
    for (uint32_t i = 0; i < sampleRate * duration; ++i) {
        v.push_back(-2 / M_PI * atan(1 / tan(frequencyInHz * M_PI * i / sampleRate)));
        if ((i % period) >= 0 && (i % period) < dutyCycle) {
            ss = 0.7;
        } else {
            ss = -0.7;
        }
    }
}
```

#### `generatetwentyfquarewave()`

```cpp
void generatetwentyfquarewave(std::vector<float>& v, int duration, double frequencyInHz) {
    const double sampleRate = 44100.0;
    double period = sampleRate / frequencyInHz;
    double dutyCycle = period * 0.25;
    double ss = 0.0;
    for (uint32_t i = 0; i < sampleRate * duration; ++i) {
        v.push_back(-2 / M_PI * atan(1 / tan(frequencyInHz * M_PI * i / sampleRate)));
        if ((i % period) >= 0 && (i % period) < dutyCycle) {
            ss = 0.7;
        } else {
            ss = -0.7;
        }
    }
}
```

#### `generatenoise()`

```cpp
void generatenoise(std::vector<float>& v, int duration) {
    const double sampleRate = 44100.0;
    std::random_device rd;
    std::mt19937 gen(rd);
    std::uniform_real_distribution<> dis(-1.0, 1.0);
    for (uint32_t i = 0; i < sampleRate * duration; ++i) {
        v.push_back(dis(gen));
    }
}
```

#### `generateInHz()`

```cpp
void generateInHz(std::vector<float>& v, int osc, int duration, double frequencyInHz) {
    if (frequencyInHz > 0.0 && frequencyInHz <= 20.0) {
        switch (osc) {
            case 0: generatetrianglewave(v, duration, frequencyInHz); break;
            case 1: generateinversesawtooth(v, duration, frequencyInHz); break;
            case 2: generatesawtoothwave(v, duration, frequencyInHz); break;
            case 3: generatesquarewave(v, duration, frequencyInHz); break;
            case 4: generatethirtiesfquarewave(v, duration, frequencyInHz); break;
            case 5: generatetwentyfquarewave(v, duration, frequencyInHz); break;
        }
    }
}
```

#### `generateoscillator()`

```cpp
void generateoscillator(std::vector<float>& v, int osc, int duration, double frequencyInHz) {
    if (frequencyInHz >= 20.0 && frequencyInHz <= 20000.0) {
        switch (osc) {
            case 0: generatetrianglewave(v, duration, frequencyInHz); break;
            case 1: generateinversesawtooth(v, duration, frequencyInHz); break;
            case 2: generatesawtoothwave(v, duration, frequencyInHz); break;
            case 3: generatesquarewave(v, duration, frequencyInHz); break;
        }
    }
}
```



## 附录 A：C++20 代码

```cpp
void saveaudiofile(std::vector<float>& v, std::string filename)
{
    std::string path = "subtractive";
    AudioFile<float> a;
    a.setSampleRate(44100);
    a.setBitDepth(24);
    a.setChannels(1);
    for (uint32_t i = 0; i < v.size(); ++i) {
        a.samples[i] = v[i];
    }
    a.save(path + filename);
}
```

```cpp
void fillbackground(std::image<rgb_pixel>& image)
{
    rgb_pixel px(0x04, 0x13, 0x31);
    for (uint32_t y = 0; y < image.height(); ++y)
        for (uint32_t x = 0; x < image.width(); ++x)
            image.set_pixel(x, y, px);
}
```

```cpp
void drawpx(std::image<rgb_pixel>& image, int x, int y)
{
    if ((x >= 0) && (x < image.width()) && ((y >= 0) && (y < image.height()))) {
        rgb_pixel px(0x7a, 0xb1, 0xe3);
        image.set_pixel(x, y, px);
    }
}
```

```cpp
void drawline(std::image<rgb_pixel>& image, int x1, int y1, int x2, int y2)
{
    int x, y, dx, dy1, dy, px, py, xe, i;

    dx = x2 - x1;
    dy = y2 - y1;

    if (dx == 0) {
        if (y2 < y1) std::swap(y1, y2);
        for (y = y1; y <= y2; y++)
            drawpx(image, x1, y);
        return;
    }

    if (dy == 0) {
        if (x2 < x1) std::swap(x1, x2);
        for (x = x1; x <= x2; x++)
            drawpx(image, x, y1);
        return;
    }

    dx1 = abs(dx);
    dy1 = abs(dy);

    px = 2 * dy1 - dx1;
    py = 2 * dx1 - dy1;

    if (dy1 >= dx1) {
        x = x1;
        y = y1;
        xe = x2;
    } else {
        x = x2;
        y = y2;
        xe = x1;
    }

    drawpx(image, x, y);

    for (i = 0; i < xe; i++) {
        x = x + 1;

        if (px < 0)
            px = px + 2 * dy1;
        else {
            if ((dx < 0 && dy < 0) || (dx > 0 && dy > 0))
                y = y + 1;
            else
                y = y;
            px = px + 2 * (dy1 - dx1);
        }
        drawpx(image, x, y);
    }
}
```

```cpp
void drawwave(png::image<rgb_pixel>& image, std::vector<uint32_t>& signalY)
{
    uint32_t y = 0, ox = 0, oy = 0;

    for (uint32_t x = 0; x < image.get_width(); ++x) {
        y = signalY[x];

        if (x == 0) {
            ox = x;
            oy = y;
        }
        drawline(image, x, y, ox, oy);

        ox = x;
        oy = y;
    }
}
```

```cpp
void normalizedtoimg(png::image<png::rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2)
{
    uint32_t halfHeight = image.get_height() / 2;
    double value = 0.0;

    if (v2.size() == 0 || v2.size() > v1.size()) {
        v2.resize(v1.size());
    }

    for (uint32_t i = 0; i < v1.size(); ++i) {
        value = v1[i];

        if (value >= 0.0) {
            v2[i] = halfHeight - (halfHeight * value);
        } else if (value < 0.0) {
            v2[i] = halfHeight + (halfHeight * fabs(value));
        }
    }
}
```

```cpp
void renderimage(png::image<png::rgb_pixel>& image, std::vector<uint32_t>& v)
{
    fillbackground(image);
    drawwave(image, v);
}
```

```cpp
void saveimage(std::vector<uint32_t>& v, std::string filename)
{
    const std::string path = "subtractive/";
    png::image<png::rgb_pixel> image(44100, 600);
    renderimage(image, v);
    image.write(path + filename);
}
```

```cpp
void saveimage(std::vector<float>& v2, std::string filename)
{
    const std::string path = "subtractive/";
    png::image<png::rgb_pixel> image(44100, 600);
    std::vector<uint32_t> v;
    normalizedtoimg(image, v2, v);
    renderimage(image, v);
    image.write(path + filename);
}
```

```cpp
void normalizeddenvelopetoimg(png::image<png::rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2)
{
    uint32_t height = image.get_height();

    if (v2.size() == 0 || v2.size() != v1.size())
        v2.resize(v1.size());

    for (uint32_t i = 0; i < v1.size(); ++i) {
        v2[i] = height * v1[i];
    }
}
```

```cpp
void saveenvelopimage(std::vector<uint32_t>& v, std::string filename)
{
    const std::string path = "subtractive/";
    png::image<png::rgb_pixel> image(44100, 600);
    renderimage(image, v);
    image.write(path + filename);
}
```

```cpp
void saveenvelopimage(std::vector<float>& v2, std::string filename)
{
    const std::string path = "subtractive/";
    png::image<png::rgb_pixel> image(44100, 600);
    std::vector<uint32_t> v;
    normalizeddenvelopetoimg(image, v2, v);
    renderimage(image, v);
    image.write(path + filename);
}
```

编译命令：`clang++ -std=c++20 -lpng subtractive.cpp -o subtractive`

```cpp
#define USE_MATH_DEFINES
#include <cmath>
#include <vector>
#include <random>
#include <filesystem>
#include "indicators.hpp"
#include <png.hpp>
#include "AudioFile.h"
#include "Envelope.hpp"

namespace Render {
    void fillbackground(png::image<rgb_pixel>& image, int x, int y);
    void drawpx(png::image<rgb_pixel>& image, int x, int y);
    void drawline(png::image<rgb_pixel>& image, int x1, int y1, int x2, int y2);
    void drawwave(png::image<rgb_pixel>& image, std::vector<uint32_t>& signal);
    void normalizedtoimg(png::image<rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2);
    void render(std::vector<uint32_t>& v, std::string filename);
    void saveimagefile(std::vector<float>& v, std::string filename);
    void normalvelopopimg(png::image<rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t> v2);
    void saveenvelopimage(std::vector<uint32_t>& v, std::string filename);
    void saveenvelopimage(std::vector<float>& v2, std::string filename);
}

namespace SignalGenerators {
    void gain(std::vector<float>& v, double);
    void normalize(std::vector<float>& v);
    void addwaves(std::vector<float>& v1, std::vector<uint32_t>& v2);
    void wave(std::vector<float>& v);
    void generateformat(std::vector<float>& v, int, int duration);
    void generatenoise(std::vector<float>& v, int, float frequencyHz);
    void saveaudiofile(std::vector<float>& v, std::string filename);
}

int main()
{
    namespace fs = std::filesystem;
    fs::create_directory("format");

    const int duration = 1;
    const double sampleRate = 44100.0;

    std::vector<float> format0;
    std::vector<float> format1;
    std::vector<float> format2;
    std::vector<float> format3;
    std::vector<float> format4;
    std::vector<float> format5;
    std::vector<float> envelope;

    // Hide cursor
    indicators::hide_cursor(false);
    // Setup ProgressBar
    indicators::ProgressBar bar{50, "{", "}"};
    bar.Start();
    bar.Fill(" ");
    bar.Lead(" ");
    bar.Remainder(" ");
    bar.PostText("Generate Formant/23");
    bar.ForegroundColor(indicators::Color::cyan);
    bar.FontStyle(indicators::FontStyle::bold);

    // Update progress
    SignalGenerators::generateformat(format0, 0, duration);
    SignalGenerators::saveaudiofile(format0, "01-formatant0-vowel.png");

    // Update progress
    SignalGenerators::generateformat(format1, 1, duration);
    SignalGenerators::saveaudiofile(format1, "02-formatant1-vowel.png");

    // Update progress
    SignalGenerators::generateformat(format2, 2, duration);
    SignalGenerators::saveaudiofile(format2, "03-formatant2-vowel.png");

    // Update progress
    SignalGenerators::generateformat(format3, 3, duration);
    SignalGenerators::saveaudiofile(format3, "04-formatant3-vowel.png");

    // Update progress
    SignalGenerators::generateformat(format4, 4, duration);
    SignalGenerators::saveaudiofile(format4, "05-formatant4-vowel-#.png");

    // Update progress
    SignalGenerators::generateformat(format5, 5, duration);
    SignalGenerators::saveaudiofile(format5, "11-formatant5-vowel-0.png");
}
```



## 代码片段：主流程

```cpp
129 Render::saveimage(format0, "12-formant5-vowel-0.png");
```

```cpp
130 // 更新进度
```

```cpp
131 bar.set_progress(26);
```

```cpp
132 bar.set_option(option::PostText("生成共振 6 7/23"));
```

```cpp
135 // 元音 [0]
```

```cpp
136 SignalGenerators::generateformat(formant6, 6, duration);
```

```cpp
137 SignalGenerators::saveaudiofile(formant6, "13-formant6-vowel-0.aiff");
```

```cpp
138 Render::saveimage(format0, "14-formant6-vowel-0.png");
```

```cpp
140 // 更新进度
```

```cpp
141 bar.set_progress(30);
```

```cpp
142 bar.set_option(option::PostText("生成共振 7 8/23"));
```

```cpp
144 // 元音 [0]
```

```cpp
145 SignalGenerators::generateformat(formant7, 7, duration);
```

```cpp
146 SignalGenerators::saveaudiofile(formant7, "15-formant7-vowel-0.aiff");
```

```cpp
147 Render::saveimage(format0, "16-formant7-vowel-0.png");
```

```cpp
149 // 更新进度
```

```cpp
150 bar.set_progress(35);
```

```cpp
151 bar.set_option(option::PostText("生成共振 8 9/23"));
```

```cpp
153 // 元音 [0]
```

```cpp
154 SignalGenerators::generateformat(formant8, 8, duration);
```

```cpp
155 SignalGenerators::saveaudiofile(formant8, "17-formant8-vowel-0.aiff");
```

```cpp
156 Render::saveimage(format0, "18-formant8-vowel-0.png");
```

```cpp
158 // 更新进度
```

```cpp
159 bar.set_progress(39);
```

```cpp
160 bar.set_option(option::PostText("生成共振 9 10/23"));
```

```cpp
162 // 元音 [u]
```

```cpp
163 SignalGenerators::generateformat(formant9, 9, duration);
```

```cpp
164 SignalGenerators::saveaudiofile(formant9, "19-formant9-vowel-u.aiff");
```

```cpp
165 Render::saveimage(format0, "20-formant9-vowel-u.png");
```

```cpp
167 // 更新进度
```

```cpp
168 bar.set_progress(43);
```

```cpp
169 bar.set_option(option::PostText("生成共振 10 11/23"));
```

```cpp
171 // 元音 [0]
```

```cpp
172 SignalGenerators::generateformat(formant10, duration);
```

```cpp
173 SignalGenerators::saveaudiofile(formant10, "21-formant10-vowel-0.aiff");
```

```cpp
174 Render::saveimagefile(formant0, "22-formant10-vowel-0.png");
```

```cpp
176 // 更新进度
```

```cpp
177 bar.set_progress(48);
```

```cpp
178 bar.set_option(option::PostText("生成包络 12/23"));
```

```cpp
180 ADSR::Envelope env(sampleRate, duration);
```

```cpp
181 env.generateenvelope(envelope);
```

```cpp
182 Render::saveimagefile(envelope, "23-envelope.png");
```

```cpp
184 // 更新进度
```

```cpp
185 bar.set_progress(52);
```

```cpp
186 bar.set_option(option::PostText("将包络应用到共振 13/23"));
```

```cpp
188 env.generateenvelope(formant0, envelope);
```

```cpp
189 SignalGenerators::normalize(formant0);
```

```cpp
190 SignalGenerators::saveaudiofile(formant0, "24-formant0-vowel-i.aiff");
```

```cpp
191 Render::saveimagefile(formant0, "25-formant0-vowel-i.png");
```

```cpp
193 // 更新进度
```

```cpp
194 bar.set_progress(57);
```

```cpp
195 bar.set_option(option::PostText("将包络应用到共振 14/23"));
```

```cpp
197 env.generateenvelope(formant1, envelope);
```

```cpp
198 SignalGenerators::normalize(formant1);
```

```cpp
199 SignalGenerators::saveaudiofile(formant1, "26-formant1-vowel-0.aiff");
```

```cpp
200 Render::saveimagefile(formant1, "27-formant1-vowel-0.png");
```

```cpp
202 // 更新进度
```

```cpp
203 bar.set_progress(61);
```

```cpp
204 bar.set_option(option::PostText("将包络应用到共振 15/23"));
```

```cpp
206 env.generateenvelope(formant2, envelope);
```

```cpp
207 SignalGenerators::normalize(formant2);
```

```cpp
208 SignalGenerators::saveaudiofile(formant2, "28-formant2-vowel-e.aiff");
```

```cpp
209 Render::saveimagefile(formant2, "29-formant2-vowel-e.png");
```

```cpp
211 // 更新进度
```

```cpp
212 bar.set_progress(65);
```

```cpp
213 bar.set_option(option::PostText("将包络应用到共振 16/23"));
```

```cpp
env.applyenvelope(format3,
```

```cpp
// 更新进度
bar.set_progress(70);
bar.set_option(option::PostText("将包络应用到共振 17/23"));
```

```cpp
env.applyenvelope(format4,
```

```cpp
// 更新进度
bar.set_progress(74);
bar.set_option(option::PostText("将包络应用到共振 18/23"));
```

```cpp
env.applyenvelope(format5,
```

```cpp
// 更新进度
bar.set_progress(78);
bar.set_option(option::PostText("将包络应用到共振 19/23"));
```

```cpp
env.applyenvelope(format6,
```

```cpp
// 更新进度
bar.set_progress(83);
bar.set_option(option::PostText("将包络应用到共振 20/23"));
```

```cpp
env.applyenvelope(format7,
```

```cpp
// 更新进度
bar.set_progress(87);
258 bar.set_option(option::PostText("将包络应用到共振 21/23"));
```

```cpp
259 env.applyenvelope(formant8, envelope);
```

```cpp
260 SignalGenerators::normalize(formant8);
```

```cpp
263 // 更新进度
```

```cpp
264 bar.set_progress(91);
```

```cpp
265 bar.set_option(option::PostText("将包络应用到共振 22/23"));
```

```cpp
266 env.applyenvelope(formant9, envelope);
```

```cpp
267 SignalGenerators::normalize(formant9);
```

```cpp
270 // 更新进度
```

```cpp
271 bar.set_progress(96);
```

```cpp
272 bar.set_option(option::PostfixText("将包络应用到共振 10 23/23"));
```

```cpp
273 env.applyenvelope(formant10, envelope);
```

```cpp
274 SignalGenerators::normalize(formant10);
```

```cpp
277 // 更新进度
```

```cpp
278 bar.set_progress(100);
```

```cpp
279 bar.set_option(option::PostfixText("完成 23/23"));
```

```cpp
280 // 显示光标
281 show_console_cursor(true);
282 return 0;
283 }
```

## 附录 A：C++20 代码

### `SignalGenerators` 命名空间

```cpp
namespace SignalGenerators
{
    void gain(std::vector<float>& v, double gain)
    {
        for (uint32_t i = 0; i < v.size(); ++i) {
            v[i] = v[i] * gain;
        }
    }
}
```

### 全局函数

```cpp
void normalize(std::vector<float>& v)
{
    float max = 0.0, value = 0.0;
    for (uint32_t i = 0; i < v.size(); ++i) {
        value = v[i];
        if (value > max) { max = value; }
    }
    // max = std::ceil(max);
    for (uint32_t i = 0; i < v.size(); ++i) {
        v[i] = (v[i] / max) * 0.707;
    }
}
```

```cpp
void addwaves(std::vector<float>& v1, std::vector<float>& v2, std::vector<float>& v3)
{
    for (uint32_t i = 0; i < v1.size(); ++i) {
        v3[i] = v1[i] + v2[i];
    }
}
```

```cpp
void generateswave(std::vector<float>& v, int duration, float frequencyHz)
{
    const double sampleRate = 44100;
    for (uint32_t i = 0; i < v.size(); ++i) {
        v[i] = sin(2.0 * M_PI * frequencyHz * i / sampleRate);
    }
}
```

```cpp
void generatenoise(std::vector<float>& v, int duration)
{
    const double sampleRate = 44100;
    std::random_device rd;
    std::mt19937 gen(rd());
    std::uniform_real_distribution<double> dis(-1.0, 1.0);
    for (uint32_t i = 0; i < v.size(); ++i) {
        v[i] = dis(gen);
    }
}
```



```cpp
430  if (dx >= 0)
431  {
432          x = x1; y = y1; xe = x2;
433  }
434  else
435  {
436          x = x2; y = y2; xe = x1;
437  }
438  drawpx(image, x, y);
439  for (i = 0; x < xe; i++)
440  {
441      x = x + 1;
442      if (px > 0)
443          px = px + 2 * dy1;
444      else
445      {
446          if ((dx < 0 && dy < 0) || (dx > 0 && dy > 0)) y = y + 1; else y = y;
447          px = px + 2 * (dy1 - dx1);
448      }
449      drawpx(image, x, y);
450  }
451  else
452  {
453      if (dy >= 0)
454      {
455          x = x1; y = y1; ye = y2;
456      }
457      else
458      {
459          x = x2; y = y2; ye = y1;
460      }
461      drawpx(image, x, y);
462      for (i = 0; y < ye; i++)
463      {
464          y = y + 1;
465          if (py <= 0)
466              py = py + 2 * dx1;
467          else
468          {
469              if ((dx < 0 && dy < 0) || (dx > 0 && dy > 0)) x = x + 1; else x = x;
470              py = py + 2 * (dx1 - dy1);
471          }
472      }
473      drawwpx(image, x, y);
474  }
475}
```

```cpp
{
void drawwave(image::png::rgb_pixel& image, std::vector<uint32_t>& signalY)
{
    uint32_t y = 0, x = 0, oy = 0;
    for (uint32_t x = 0; x < image.get_width(); ++x)
    {
        y = signalY[x];
        if (x == 0) { ox = x; oy = y; }
        drawline(image, x, y, ox, oy);
        ox = x; oy = y;
    }
}

void normalizedToImg(image::png::rgb_pixel& image, std::vector<float>& v1, std::vector<uint32_t>& v2)
{
    uint32_t halfHeight = image.get_height() / 2;
    double value = 0.0;
    if (v2.size() == 0 || v2.size() > v1.size()) {
        v2.resize(v1.size());
    }

    for (uint32_t i = 0; i < v1.size(); ++i)
    {
        value = v1[i];
        if (value >= 0.0) {
            v2[i] = halfHeight - (halfHeight * value);
        } else if (value < 0.0) {
            v2[i] = halfHeight + (halfHeight * fabs(value));
        }
    }
}

void renderimage(image::png::rgb_pixel& image, std::vector<uint32_t>& v)
{
    fillbackground(image);
    drawwave(image, v);
}

void saveimage(std::vector<uint32_t>& v, std::string filename)
{
    const std::string path = "format";
    png::image<rgb_pixel> image(410, 600);
    renderimage(image, v);
    image.write(path + filename);
}

void saveimage(std::vector<float>& v2, std::string filename)
{
    const std::string path = "format";
    png::image<rgb_pixel> image(410, 600);
    std::vector<uint32_t> v;
    normalizedtoimg(image, v2, v);
    renderimage(image, v);
    image.write(path + filename);
}

void normalizedtoimg(image::png::rgb_pixel& image, std::vector<float>& v1, std::vector<uint32_t>& v2)
{
    uint32_t height = image.get_height();
    if (v2.size() == 0 || v2.size() > v1.size()) {
        v2.resize(v1.size());
    }
    for (uint32_t i = 0; i < v1.size(); ++i) {
        v2[i] = height * v1[i];
    }
}

void saveenvelopeimage(std::vector<uint32_t>& v, std::string filename)
{
    const std::string path = "format";
    png::image<rgb_pixel> image(410, 600);
    renderimage(image, v);
    image.write(path + filename);
}

void saveenvelopeimage(std::vector<float>& v2, std::string filename)
{
    const std::string path = "format";
    png::image<rgb_pixel> image(410, 600);
    std::vector<uint32_t> v;
    normalizedvelopetoimg(image, v2);
    render(image, v);
    image.write(path + filename);
}
}
```

### 04-granular.cpp - 96 bytes

```cpp
// 编译命令: clang++ -std=c++20 -lpng 04-granular.cpp -o 04-granular

#define _MATH_DEFINES

#include <cmath>
#include <vector>
#include <random>
#include <filesystem>
#include "indicators.hpp"
#include <png++/png.hpp>
#include "Audio/AudioFile.h"
#include "Envelope.hpp"

namespace Renderer
{
    void fillbackground(png::image<rgb_pixel>& image, int x, int y);
    void drawx(png::image<rgb_pixel>& image, int x1, int y1, int x2, int y2);
    void drawline(png::image<rgb_pixel>& image, int x1, int y1, int x2, int y2);
    void drawwave(png::image<rgb_pixel>& image, std::vector<uint32_t>& signalY);
    void normalizedtoimg(png::image<rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2);
    void renderimage(png::image<rgb_pixel>& image, std::vector<uint32_t>& v);
    void saveimage(std::vector<uint32_t>& v, std::string filename);
    void saveimage(std::vector<float>& v2, png::image<rgb_pixel>& image, std::vector<float>);
    void normalizedenvelopetoimg(png::image<rgb_pixel>& image, std::vector<float>);
    void saveenvelopeimage(std::vector<uint32_t>& v, std::string filename);
    void saveenvelopeimage(std::vector<float>& v2, std::string filename);
}

namespace SignalGenerators
{
    void gain(std::vector<float>& v, double gain);
    void normalize(std::vector<float>& v);
}
```

## 附录 C C++20 代码

```cpp
void addwaves(std::vector<float>& v1, std::vector<float>& v2, std::vector<float>& v3);
void generatesample(std::vector<float>& v, int duration);
void extendsample(std::vector<float>& v1, std::vector<float>& v2, int n);
void saveaudiofile(std::vector<float>& v, std::string filename, int duration);
void loadaudiofile(std::vector<float>& v, std::string filename);

int main() {
    namespace fs = std::filesystem;
    using namespace indicators;
    show_cursor(false);

    // 设置进度条
    ProgressBar{
        BarWidth{50},
        Start(""),
        Fill("0"),
        End(""),
        ForegroundColor(Color::cyan),
        FontStyle{bold}
    };
}
```

## 附录 A：C++20 代码

```cpp
SignalGenerators::extendsample(sample, sample_extended, 4);
```

```cpp
SignalGenerators::saveaudiofile(sample_extended, "01-generatedsample.aiff");
```

```cpp
SignalGenerators::saveaudiofile(sample, "02-generatedsample.png");
```

```cpp
// 从采样中获取颗粒
SignalGenerators::saveaudiofile(sample_extended, "03-extendedsample.aiff");
```

```cpp
float grains[100][44];
uint32_t ptr1 = 0, ptr2 = 0;
std::random_device rd;
std::mt19937 gen(rd());
std::uniform_int_distribution<> distria(1, 990);
std::uniform_int_distribution<> distrib(1, 4000);
std::uniform_int_distribution<> distric(0, 99);

for (uint32_t i = 0; i < 100; i++) {
    ptr1 = distria(gen) * 44;
    for (uint32_t j = 0; j < 44; j++) {
        grains[i][j] = sample[ptr1];
    }
}
```

```cpp
for (uint32_t i = 0; i < 100; i++) {
    ptr1 = distric(gen);
    ptr2 = distrib(gen) * 44;
    for (uint32_t j = 0; j < 44; j++) {
        sample_extended[ptr2++] = grains[ptr1][j];
    }
}
```

```cpp
SignalGenerators::normalize(sample_extended);
SignalGenerators::saveaudiofile(sample_extended, "04-finalgranular.aiff");
```

```cpp
// 更新进度
bar_set_progress(option::PostfixText("Done 5/5"));

// 显示光标
show_console_cursor(true);
return 0;
}

namespace SignalGenerators
{
    void gain(std::vector<float>& v, double gain)
    {
        for (uint32_t i = 0; i < v.size(); ++i)
            v[i] = v[i] * gain;
    }

    void normalize(std::vector<float>& v)
    {
        float max = 0.0, value = 0.0;
        for (uint32_t i = 0; i < v.size(); ++i) {
            value = v[i];
            if (value > max) max = value;
        }
        // max = ceil(max);
        for (uint32_t i = 0; i < v.size(); ++i)
            v[i] = (v[i] / max) * 0.707;
    }

    void addwaves(std::vector<float>& v1, std::vector<float>& v2, std::vector<float>& v3)
    {
        for (uint32_t i = 0; i < v1.size(); ++i)
        {
            v3[i] = v1[i] + v2[i];
        }
    }

    void generatesample(std::vector<float>& v, int duration)
    {
        const double sampleRate = 44100.0;
        std::vector<float> envelope1;
        std::vector<float> envelope2;
        std::vector<float> sample1;
        std::vector<float> sample2;
        ADSR::Envelope env(sampleRate, duration);
        env.generateenvelope2(envelope1);
        env.generateenvelope3(envelope2);
        loadaudiofile(sample1, "additive/67-mixed.aiff");
        loadaudiofile(sample2, "subtractive/08-postfilter.aiff");
        env.applyenvelope(sample1, envelope2);
        v.resize(duration * sampleRate);
        addwaves(sample1, sample2, v);
        normalize(v);
    }
}
```



## C++ 代码示例

### 音频处理函数

```cpp
void extendsample(std::vector<float>& v1, std::vector<float>& v2, int n) {
    for (uint32_t i = 0; i < v1.size(); ++i) {
        for (uint32_t j = 0; j < n; ++j) {
            v2.push_back(v1[i]);
        }
    }
}
```

```cpp
void saveaudiofile(std::vector<float>& v, std::string filename, int duration) {
    const std::string path = "granular/";

    // 设置音频文件
    AudioFile a;
    a.setNumChannels(1);
    a.setBitDepth(24);
    a.setNumSamplesPerChannel(44100 * duration);

    for (int i = 0; i < a.getNumSamplesPerChannel(); ++i) {
        for (int channel = 0; channel < a.getNumChannels(); ++channel) {
            a.samples[channel][i] = v[i];
        }
    }
    a.save(path + filename, AudioFormat::Aiff);
}
```

```cpp
void loadaudiofile(std::vector<float> v, std::string filename) {
    AudioFile<float> a;
    bool loadedOK = a.load(filename);

    if (loadedOK) {
        for (int i = 0; i < a.getNumSamplesPerChannel(); ++i) {
            for (int channel = 0; channel < 1; ++channel) {
                v.push_back(a.samples[channel][i]);
            }
        }
    }
}
```

### Render 命名空间

```cpp
namespace Render {
    void fillbackground(png::image<rgb_pixel>& image) {
        png::rgb_pixel px(0, 0, 0);
        for (uint32_t y = 0; y < image.height(); ++y) {
            for (uint32_t x = 0; x < image.width(); ++x) {
                image.set_pixel(x, y);
            }
        }
    }

    void drawpx(png::image<rgb_pixel>& image, int x, int y) {
        if ((x >= 0) && (x < image.width()) && (y >= 0) && (y < image.height())) {
            png::rgb_pixel px(255, 255, 255);
            image.set_pixel(x, y);
        }
    }

    void drawline(png::image<rgb_pixel>& image, int x1, int y1, int x2, int y2) {
        int x, y, dx, dy, dx1, dy1, px, py, xe;
        dx = x2 - x1;
        dy = y2 - y1;

        if (dx == 0) {
            if (y2 < y1) std::swap(y1, y2);
            for (y = y1; y <= y2; y++) {
                drawpx(image, x, y);
            }
        }

        if (dy == 0) {
            if (x2 < x1) std::swap(x1, x2);
            for (x = x1; x <= x2; x++) {
                drawpx(image, x, y1);
            }
        }

        dx1 = abs(dx);
        dy1 = abs(dy);
        px = 2 * dx - dx1;
        py = 2 * dy1 - dy1;

        if (dy1 <= dx1) {
            if (dx >= 0) {
                x = x1;
                y = y1;
                xe = x2;
            } else {
                x = x2;
                y = y2;
                xe = x1;
            }
            drawpx(image, x, y);
            for (int i = 0; i < xe; i++) {
                x = x + i;
                if (px < 0) {
                    px = px + 2 * dy1;
                } else {
                    if ((dx < 0 && dy < 0) || (dx > 0 && dy > 0))
                        y = y + 1;
                    else
                        y = y - 1;
                    px = px + 2 - (dy1 - dx1);
                }
                drawpx(image, x, y);
            }
        } else {
            if (dy >= 0) {
                x = x1;
                y = y1;
                ye = y2;
            } else {
                x = x2;
                y = y2;
                ye = y1;
            }
            drawpx(image, x, y);
            for (int i = 0; y < ye; i++) {
                y = y + 1;
                if (py <= 0) {
                    py = py + 2 * dx1;
                } else {
                    if ((dx > 0 && dy < 0) || (dx > 0 && dy > 0))
                        x = x + 1;
                    else
                        x = x;
                    py = py + 2 * (dx1 - dy1);
                }
                drawpx(image, x, y);
            }
        }
    }

    void drawwave(png::image<rgb_pixel>& image, std::vector<uint32_t>& signalY) {
        uint32_t y = 0;
        for (uint32_t x = 0; x < image.width(); ++x) {
            y = signalY[x];
            drawline(image, 0, 0, x, y);
        }
    }
}
```

## 附录 A：C++20 代码

### Render 命名空间声明

```cpp
namespace Render {
    void fillbackground(png::image<png::rgb_pixel>& image, int x, int y);
    void drawline(png::image<png::rgb_pixel>& image, int x1, int y1, int x2, int y2);
    void drawwave(png::image<png::rgb_pixel>& image, std::vector<uint32_t>& signal);
    void normalized(png::image<png::rgb_pixel>& image, std::vector<uint32_t>&, std::vector<uint32_t>&);
    void renderimage(png::image<png::rgb_pixel>& image, std::vector<uint32_t>& v);
    void saveimage(std::vector<float>& v, std::string filename);
    void normalizedvelopimage(png::image<png::rgb_pixel>& image, std::vector<float>& v);
    void saveenvelopeimage(std::vector<uint32_t>& v, std::string filename);
    void saveenvelopeimage(std::vector<float>& v, std::string filename);
}
```

### SignalGenerators 命名空间声明

```cpp
namespace SignalGenerators {
    void gain(std::vector<float>& std, double gain);
    void normalize(std::vector<float>& v);
    void addwaves(std::vector<float>& v1, std::vector<float>& v2, std::vector<float>& v3);
    void generatefrequencymodulation(std::vector<float>& v, int duration, float frequencyInHz);
    void saveaudiofile(std::vector<float>& v, std::string filename);
}
```

### 主函数与实现

```cpp
int main() {
    namespace fs = std::filesystem;
    fs::create_directory("fm");

    const int duration = 1;
    const double sampleRate = 44100.0;
    std::vector<float> fm;
    std::vector<float> envelope;

    using namespace indicators;

    // 隐藏光标
    show_console_cursor(false);

    // 设置进度条
    ProgressBar bar{
        option::BarWidth(50)
    };
}
```

```cpp
struct {
    void gain(std::vector<float>& v, double gain) {
        for (uint32_t i = 0; i < v.size(); ++i) {
            v[i] = v[i] * gain;
        }
    }

    void normalize(std::vector<float>& v) {
        float max = 0.0, value = 0.0;
        for (uint32_t i = 0; i < v.size(); ++i) {
            value = v[i];
            if (value > max) { max = value; }
        }
        // max = std::ceil(max);
        for (uint32_t i = 0; i < v.size(); ++i) {
            v[i] = (v[i] / max) * 0.707;
        }
    }

    void addwaves(std::vector<float>& v1, std::vector<float>& v2, std::vector<float>& v3) {
        for (uint32_t i = 0; i < v1.size(); ++i) {
            v3[i] = v1[i] + v2[i];
        }
    }

    void generatefrequencymodulation(std::vector<float>& v, int duration, float frequencyInHz) {
        const double twoPI = 2 * M_PI;
        const double sampleRate = 44100.0;
        const double frequencyRadius = twoPI / sampleRate;
        double modulatorFrequency = frequencyInHz;
        double modulatorIncrement = frequencyRadius;
        double modulatorPhase = 0;
        double carrierIncrement = 0;
        double carrierPhase = 0;
        double amplitude = 2;
        double modulatorValue = 0;

        for (uint32_t i = 0; i < sampleRate * duration; ++i) {
            v.push_back(sin(carrierPhase));
            modulatorValue = amplitude * sin(modulatorPhase);
            carrierIncrement = frequencyInHz * modulatorValue;
            carrierPhase = carrierPhase + carrierIncrement;
            modulatorPhase = modulatorPhase + carrierIncrement;

            if (carrierPhase >= twoPI) {
                carrierPhase -= twoPI;
            } else if (carrierPhase < 0) {
                carrierPhase += twoPI;
            }

            if (modulatorPhase >= twoPI) {
                modulatorPhase -= twoPI;
            }
        }
    }
};
```

```cpp
void saveaudiofile(std::vector<float>& v, std::string filename) {
    const std::string path = filename;

    // 设置音频文件
    AudioFile<float> a;
    a.setChannels(1);
    a.setDepth(24);
    a.setSamplesPerChannel(44100);

    for (int i = 0; i < a.getNumSamplesPerChannel(); ++i) {
        for (int channel = 0; channel < a.getNumChannels(); ++channel) {
            a.samples[channel][i] = v[i];
        }
    }
    a.save(path, AudioFormat::AIFF);
}
```

### Render 命名空间实现（续）

```cpp
namespace Render {
    void fillbackground(png::image<png::rgb_pixel>& image) {
        png::rgb_pixel px(0x04, 0x13, 0x31);
        for (uint32_t y = 0; y < image.height(); ++y) {
            for (uint32_t x = 0; x < image.width(); ++x) {
                image.set_pixel(x, y);
            }
        }
    }

    void drawpx(png::image<png::rgb_pixel>& image, int x, int y) {
        if ((x > 0 && x < image.width()) && (y > 0 && y < image.height())) {
            png::rgb_pixel px(0x7a, 0xb1, 0x33);
            image.set_pixel(x, y);
        }
    }
}
```



## 附录 A：C++20 代码

### 124

```cpp
const std::string path = "fm";
png::image<png::rgb_pixel> image(44100, 600);
renderimage(image, v);
image.write(path + filename);
```

```cpp
void saveimagefile(std::vector<float>& v2, std::string filename)
{
    const std::string path = "fm";
    png::image<png::rgb_pixel> image(44100, 600);
    std::vector<uint32_t> v;
    normalizedimg(image, v2);
    image.write(path + filename);
}
```

```cpp
void normalizedvelopetoimg(png::image<png::rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2)
{
    uint32_t height = image.get_height();
    if (v2.size() == 0 || v2.size() != v1.size()) {
        v2.resize(v1.size());
    }
    for (uint32_t i = 0; i < v1.size(); ++i) {
        v2[i] = height - v1[i];
    }
}
```

```cpp
void saveenvelopeimage(std::vector<uint32_t>& v, std::string filename)
{
    const std::string path = "fm";
    png::image<png::rgb_pixel> image(44100, 600);
    renderimage(image, v);
    image.write(path + filename);
}
```

```cpp
void saveenvelopeimage(std::vector<float>& v2, std::string filename)
{
    const std::string path = "fm";
    png::image<png::rgb_pixel> image(44100, 600);
    std::vector<uint32_t> v;
    normalizedvelopetoimg(image, v2);
    renderimage(image, v);
    image.write(path + filename);
}
```

### 06-la.cpp

```cpp
// compile clang++ -std=c++20 -lpng 06-la.cpp -o 06-la
#define _USE_MATH_DEFINES
#include <cmath>
#include <vector>
#include <random>
#include <filesystem>
#include "indicators.hpp"
#include <png++/png.hpp>
#include "AudioFile/AudioFile.h"
#include "Envelope.hpp"

namespace Renderer {
    void fillbackground(png::image<png::rgb_pixel>& image, int x, int y);
    void drawline(png::image<png::rgb_pixel>& image, int x1, int y1, int x2, int y2);
    void drawwave(png::image<png::rgb_pixel>& image, std::vector<uint32_t>& signalY);
    void normalizedtoimg(png::image<png::rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2);
    void renderimage(png::image<png::rgb_pixel>& image, std::vector<uint32_t>& v);
    void saveimage(std::vector<uint32_t>& v, std::string filename);
    void normalizedenvelopetoimg(png::image<png::rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2);
    void saveenvelopetoimage(std::vector<uint32_t>& v, std::string filename);
    void saveenvelopetoimage(std::vector<float>& v2, std::string filename);
}

namespace SignalGenerators {
    void gain(std::vector<float>& v, double gain);
    void normalize(std::vector<float>& v);
    void addwaves(std::vector<float>& v1, std::vector<float>& v2, std::vector<float>& v3);
    void generatesubractive(std::vector<float>& v);
    void generatesample(std::vector<float>& v);
    void saveaudiooffile(std::vector<float>& v, std::string filename);
}

int main()
{
    namespace fs = std::filesystem;
    fs::create_directory("la");

    const int duration = 1;
    const double sampleRate = 44100.0;
    std::vector<float> sample;
    std::vector<float> subtractive;
    std::vector<float> envelope1;
    std::vector<float> envelope2;
    std::vector<float> envelope;
    std::vector<float> lineararithmetic;

    using namespace indicators;
    // 隐藏光标
    show_console_cursor(false);

    // 设置进度条
    ProgressBar bar(
        option::BarWidth(50),
        option::Start("{"),
        option::Fill("0"),
        option::Lead("0"),
        option::Remainder("-"),
        option::End("]"),
        option::PostText("设置线性算术 1/2"),
        option::ForegroundColor(Color::cyan),
        option::FontStyles(std::vector<FontStyle>(FontStyle::bold))
    );

    // 更新进度
    bar.set_progress(0);

    SignalGenerators::generamples(sample);
    SignalGenerators::normalize(sample);

    SignalGenerators::generatesubractive(subtractive);
    SignalGenerators::normalize(subtractive);
    envelope(sample);
    lineararithmetic.resize(sample.size());
    SignalGenerators::addwaves(sample, subtractive, lineararithmetic);
    SignalGenerators::saveaudiofile(lineararithmetic, "01-arithmetic.wav");

    // 更新进度
    bar.set_progress(50);
    bar.option(PostText("正在线性算术 1/2"));

    envelope(lineararithmetic);
    SignalGenerators::normalize(lineararithmetic);
    SignalGenerators::saveaudiofile(lineararithmetic, "02-arithmetic.wav");

    // 更新进度
    bar.set_progress(100);
    bar.option(PostText("完成 2/2"));

    // 显示光标
    show_console_cursor(true);
    return 0;
}
```

### 131

```cpp
if ((dx < 0 && dy < 0) || (dx > 0 && dy > 0)) y = y + 1; else y = y;
px = px + 2 * (dy1 - dx1);
}
drawpx(image, x, y);
}
else
{
    if (dy >= 0)
    {
        x = x1; y = y1; ye = y2;
    }
    else
    {
        x = x2; y = y2; ye = y1;
    }
    drawpx(image, x, y);
    for (i = 0; y < ye; i++)
    {
        y = y + 1;
        if (py <= 0)
            py = py + 2 * dx1;
        else
        {
            if ((dx < 0 && dy < 0) || (dx > 0 && dy > 0)) x = x + 1; else x = x;
            py = py + 2 * (dx1 - dy1);
        }
    }
}
drawpx(image, x, y);
}

void drawwave(png::image<png::rgb_pixel>& image, std::vector<uint32_t>& signalY)
{
    uint32_t y = 0, ox = 0, oy = 0;
    for (uint32_t x = 0; x < image.get_width(); ++x)
    {
        y = signalY[x];
        if (x == 0) { ox = x; oy = y; }
        drawline(image, x, y, ox, oy);
        ox = x; oy = y;
    }
}
```

### 132

```cpp
void normalizedimg(png::image<png::rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2)
{
    uint32_t halfHeight = image.get_height();
    double value = 0.0;
    if (v2.size() == 0 || v2.size() > v1.size()) {
        v2.resize(v1.size());
    }
    for (uint32_t i = 0; i < v1.size(); ++i) {
        value = v1[i];
        if (value >= 0.0) {
            v2[i] = halfHeight - halfHeight * value;
        } else if (value < 0.0) {
            v2[i] = halfHeight + halfHeight * abs(value);
        }
    }
}
```



### C++ 代码片段

```cpp
}

}

}

}

void renderimage(png::image<png::rgb_pixel>& image, std::vector<uint32_t>& v) {

    fillbackground(image);
    drawwave(image, v);
}

void saveimagefile(std::vector<uint32_t>& v, std::string filename) {

    const std::string path = "la/";
    png::image<png::rgb_pixel> image(44100, 600);
    renderimage(image, v);
    image.write(path + filename);
}

void saveimagefile(std::vector<float>& v2, std::string filename) {

    const std::string path = "la/";
    png::image<png::rgb_pixel> image(44100, 600);
    std::vector<uint32_t> v;
    normalizedimg(image, v2, v);
    renderimage(image, v);
    image.write(path + filename);
}

void normalizedvelopetoimg(png::image<png::rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2) {

    uint32_t height = image.get_height();

    if (v2.size() == 0 || v2.size() > v1.size()) {
        v2.resize(v1.size());
    }

    for (uint32_t i = 0; i < v1.size(); ++i) {
        v2[i] = height - v1[i];
    }
}

void saveenvelopimage(std::vector<uint32_t>& v, std::string filename) {

    const std::string path = "la/";
    png::image<png::rgb_pixel> image(44100, 600);
    renderimage(image, v);
    image.write(path + filename);
}

void saveenvelopimage(std::vector<float>& v2, std::string filename) {

    const std::string path = "la/";
    png::image<png::rgb_pixel> image(44100, 600);
    std::vector<uint32_t> v;
    normalizedvelopetoimg(image, v2, v);
    renderimage(image, v);
    image.write(path + filename);
}
```

### 133

```cpp
// compile: clang++ -std=c++20 -lpng 07-pd.cpp -o 07-pd.cpp

#define _USE_MATH

#include <cmath>
#include <vector>
#include <random>
#include <filesystem>
#include "indicators.hpp"
#include <png.hpp>
#include "AudioFile.h"
#include "Envelope.hpp"

namespace Render {

    void fillbackground(png::image<png::rgb_pixel>& image);
    void drawpx(png::image<png::rgb_pixel>& image, int x, int y);
    void drawline(png::image<png::rgb_pixel>& image, int x1, int y1, int x2, int y2);
    void drawwave(png::image<png::rgb_pixel>& image, std::vector<uint32_t>& signalY);
    void normalizedimg(png::image<png::rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2);
    void renderimage(png::image<png::rgb_pixel>& image, std::vector<uint32_t>& v);
    void saveimagefile(std::vector<uint32_t>& v, std::string filename);
    void saveimagefile(std::vector<float>& v2, std::string filename);
    void normalizedvelopetoimg(png::image<png::rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2);
    void saveenvelopimage(std::vector<uint32_t>& v, std::string filename);
    void saveenvelopimage(std::vector<float>& v2, std::string filename);
}

namespace SignalGenerators {

    void gain(std::vector<float>& v, double gain);
    void normalize(std::vector<float>& v);
    void addwaves(std::vector<float>& v1, std::vector<float>& v2, std::vector<float>& v3);
    void generatephasedistortionwave(std::vector<float>& v, int duration, float frequencyInHz, float x1, float y1, float x2, bool isCosine);
    void saveaudiofile(std::vector<float>& v, std::string filename);
}

int main() {

    namespace fs = std::filesystem;
    fs::create_directory("pd");

    const int duration = 1;
    const double sampleRate = 44100.0;
    std::vector<float> pd;
    std::vector<float> envelope;

    using namespace indicators;

    // 隐藏光标
    show_console_cursor(false);

    // 设置进度条
    ProgressBar bar{
        option::BarWidth(50)
    };

    // 更新进度
    bar.set_progress(100);
    bar.set_option(option::PostfixText("Done 2/2"));

    // 显示光标
    show_console_cursor(true);

    return 0;
}

namespace SignalGenerators {

    void gain(std::vector<float>& v, double gain) {
        for (uint32_t i = 0; i < v.size(); ++i) {
            v[i] = v[i] * gain;
        }
    }

    void normalize(std::vector<float>& v) {
        float max = 0.0, value = 0.0;
        for (uint32_t i = 0; i < v.size(); ++i) {
            value = v[i];
            if (value > max) max = value;
        }
        max = std::ceil(max);
        for (uint32_t i = 0; i < v.size(); ++i) {
            v[i] = v[i] / max;
        }
    }

    void addwaves(std::vector<float>& v1, std::vector<float>& v2, std::vector<float>& v3) {
        for (uint32_t i = 0; i < v1.size(); ++i) {
            v3[i] = v1[i] + v2[i];
        }
    }

    void generatephasedistortionwave(std::vector<float>& v, int duration, float frequencyInHz, float x1, float y1, float x2, bool isCosine) {
        // 实现细节...
    }

    void saveaudiofile(std::vector<float>& v, std::string filename) {
        // 实现细节...
    }
}
```

## 附录 A：C++20 代码

```cpp
if (x2 < x1) std::swap(x1, x2);

for (x = x1; x <= x2; x++)
    drawpx(image, x, y1);

dx1 = abs(dx);
dy1 = abs(dy);
px = 2 * dy1 - dx1;
py = 2 * dx1 - dy1;

if (dy1 <= dx1) {
    if (dx >= 0) {
        x = x1; y = y1; xe = x2;
    } else {
        x = x2; y = y2; xe = x1;
    }
    drawpx(image, x, y);
    for (i = 0; x < xe; i++) {
        x = x + 1;
        if (px < 0)
            px = px + 2 * dy1;
        else {
            if ((dx < 0 && dy < 0) || (dx > 0 && dy > 0)) y = y + 1; else y = y - 1;
            px = px + 2 * (dy1 - dx1);
        }
        drawpx(image, x, y);
    }
} else {
    if (dy >= 0) {
        x = x1; y = y1; ye = y2;
    } else {
        x = x2; y = y2; ye = y1;
    }
    drawpx(image, x, y);
    for (i = 0; y < ye; i++) {
        y = y + 1;
        if (py <= 0)
            py = py + 2 * dx1;
        else {
            if ((dx < 0 && dy > 0) || (dx > 0 && dy > 0)) x = x + 1; else x = x;
            py = py + 2 * (dx1 - dy1);
        }
        drawpx(image, x, y);
    }
}
```

```cpp
void drawwave(png::image<png::rgb_pixel>& image, std::vector<uint32_t>& signalY) {
    uint32_t y = 0, ox = 0, oy = 0;
    for (uint32_t x = 0; x < image.get_width(); ++x) {
        y = signalY[x];
        if (x == 0) { ox = x; oy = y; }
        drawline(image, x, y, ox, oy);
        ox = x; oy = y;
    }
}

void normalizedtoimg(png::image<png::rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2) {
    uint32_t halfHeight = image.get_height() / 2;
    double value = 0.0;
    if (v2.size() == 0 || v2.size() > v1.size())
        v2.resize(v1.size());
    for (uint32_t i = 0; i < v1.size(); ++i) {
        value = v1[i];
        if (value >= 0.0) {
            v2[i] = halfHeight - (halfHeight * value);
        } else if (value < 0.0) {
            v2[i] = halfHeight + (halfHeight * fabs(value));
        }
    }
}

void renderimage(png::image<png::rgb_pixel>& image, std::vector<uint32_t>& v) {
    fillbackground(image);
    drawwave(image, v);
}

void saveimage(std::vector<uint32_t>& v, std::string filename) {
    const std::string path = "pd";
    png::image<png::rgb_pixel> image(44100, 600);
    renderimage(image, v);
    image.write(path + filename);
}

void saveimage(std::vector<float>& v2, std::string filename) {
    const std::string path = "pd";
    png::image<png::rgb_pixel> image(44100, 600);
    std::vector<uint32_t> v;
    normalizedtoimg(image, v2, v);
    renderimage(image, v);
    image.write(path + filename);
}

void normalizedenopetoimage(png::image<png::rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2) {
    uint32_t height = image.get_height();
    if (v2.size() == 0 || v2.size() > v1.size()) {
        v2.resize(v1.size());
    }
    for (uint32_t i = 0; i < v1.size(); ++i) {
        v2[i] = height - (height * v1[i]);
    }
}

void saveenopetoimage(std::vector<uint32_t>& v, std::string filename) {
    const std::string path = "/pd";
    png::image<png::rgb_pixel> image(44100, 600);
    renderimage(image, v);
}
```



# C++ 代码示例

## 图像保存函数

```cpp
image.write(path + filename);
}

void saveenvelopeimage(std::vector<float>& v2, std::string filename)
{
    const std::string path = "/pd";
    png::image<png::rgb_pixel> image(44100, 600);
    std::vector<uint32_t> v;
    normalizedetoimage(image, v2, v);
    image.write(path + filename);
}
```

## 编译命令

```cpp
// 编译命令: clang++ -std=c++20 -lpng 08-scanned
```

## 头文件与命名空间声明

```cpp
#define USE_MATH_DEFINES

#include <cmath>
#include <vector>
#include <random>
#include <filesystem>
#include "indicators.hpp"
#include <png++/hpp>
#include "AudioFile.h"
#include "Envelope.hpp"
#include <iostream>

namespace Render {
    void fillbackground(png::image<png::rgb_pixel>& image, int x, int y);
    void drawpx(png::image<png::rgb_pixel>& image, int x, int y1, int x2, int y2);
    void drawline(png::image<png::rgb_pixel>& image, int x1, int y1);
    void drawwave(png::image<png::rgb_pixel>& image, std::vector<uint32_t>& signalY);
    void normalizedtoimage(png::image<png::rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2);
}
```

## 函数前向声明

```cpp
void renderimage(png::image<png::rgb_pixel>& image, std::vector<uint32_t>& v);
void saveimage(std::vector<uint32_t>& v, std::string filename);
void saveimage(std::vector<float>& v, std::string filename);
void normalizedetoimage(png::image<png::rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2);
void saveenopetoimage(std::vector<uint32_t>& v, std::string filename);
void saveenvelopeimage(std::vector<float>& v2, std::string filename);
void gain(std::vector<float>& v, double gain);
void normalize(std::vector<float>& v);
void addwaves(std::vector<float>& v1, std::vector<float>& v2, std::vector<float>& v3);
void generatescwave(std::vector<float>& v, int duration, float frequency);
void saveaudiofile(std::vector<float>& v, std::string filename);
```

## 主函数

```cpp
int main()
{
    namespace fs = std::filesystem;
    fs::create_directory("scanned");

    const int duration = 1;
    const double sampleRate = 44100.0;
    std::vector<float> scanned;
    std::vector<float> envelope;

    using namespace indicators;

    // 隐藏光标
    show_console_cursor(false);

    // 设置进度条
    ProgressBar bar{
        option::BarWidth{50},
        option::Start(""),
        option::Fill("0"),
        option::Lead("0"),
        option::Remainder("-"),
        option::End(" "),
        option::Postfix("生成扫描波 1/2"),
        option::ForegroundColor(Color::cyan,
        option::FontStyles(std::vector<FontStyle>{FontStyle::bold})
    };

    // 更新进度
    bar.set_progress(0);
    SignalGenerators::generatescwave(scanned, duration, 440);
    SignalGenerators::saveaudiofile(scanned, "01-scanned.wav");
    Render::saveimagefile(scanned, "02-scanned.png");

    bar.set_progress(50);
    bar.set_option(option::Postfix("完成最终扫描 2/2"));

    ADSR::Envelope env(sampleRate, duration);
    env.generateenvelope(envelope);
    env.applyenvelope(scanned, envelope);
    SignalGenerators::normalize(scanned);
    SignalGenerators::saveaudiofile(scanned, "03-final-scanned.wav");
    Render::saveimagefile(scanned, "04-final-scanned.png");

    // 更新进度
    bar.set_progress(100);
    bar.set_option(option::Postfix("完成 2/2"));

    // 显示光标
    show_console_cursor(true);

    return 0;
}
```

## SignalGenerators 命名空间实现

```cpp
namespace SignalGenerators
{
    void gain(std::vector<float>& v, double gain)
    {
        for (uint32_t i = 0; i < v.size(); ++i) {
            v[i] = v[i] * gain;
        }
    }

    void normalize(std::vector<float>& v)
    {
        float max = 0.0, value = 0.0;
        for (uint32_t i = 0; i < v.size(); ++i) {
            value = v[i];
            if (value > max) max = value;
        }
        // std::ceil(max);
        for (uint32_t i = 0; i < v.size(); ++i) {
            v[i] = v[i] / max;
            v[i] = (v[i] / max) + 0.707;
        }
    }

    void addwaves(std::vector<float>& v1, std::vector<float>& v2, std::vector<float>& v3)
    {
        for (uint32_t i = 0; i < v1.size(); ++i) {
            v3[i] = v1[i] + v2[i];
        }
    }

    void generatescwave(std::vector<float>& v, int duration, float frequency)
    {
        // implementation
    }

    void saveaudiofile(std::vector<float>& v, std::string filename)
    {
        // implementation
    }
}
```

# 附录 A：C++20 代码

## 扫描合成核心循环

```cpp
for (int j = 0; j < state->size; j++) {
    auto prevIndex = j > 0 ? j - 1 : state->size - 1;
    auto nextIndex = j < state->size - 1 ? j + 1 : 0;
    previousPosition[j] = state->position[j];
    previousPosition[nextIndex] = state->position[nextIndex];
}
```

## 力计算

```cpp
float prev = previousPosition[prevIndex];
float next = previousPosition[nextIndex];
float deltaX = (prev + next + 0) / 3 - state->position[j];
float force = system->k * deltaX - system->b;
```

## 状态更新

```cpp
state->velocity[j] += force * system->updateSize;
state->position[j] += state->velocity[j] * system->updateSize;
```

```cpp
}
elapsed += system->updateSize;
}
```

## 内存清理

```cpp
delete[] previousPosition;
```

## 波形生成函数

```cpp
void generateersancannwave(std::vector<float>& v, int duration, float frequencyInHz) {
```

## 系统初始化

```cpp
const double sampleRate = 44100.0;
SystemDesc system = {.8, .01, .016, .01};
ScanState state;
state.size = 128;
state.position = new float[state.size];
state.velocity = new float[state.size];
std::random_device rd;
std::mt19937 gen(rd());
std::uniform_real_distribution<double> dis(0.0, 1.0);
```

## 状态初始化循环

```cpp
for (int i = 0; i < state.size; i++) {
    float randOffset = dis(gen);
    float amplitude = 0.1 + 0.5 * ((1 + 1) % 2);
    state.position[i] = sin(2 * M_PI * i / state.size / 4) * amplitude + randOffset;
    state.velocity[i] = dis(gen);
}
```

## 扫描与清理

```cpp
scan(v, &state, &system, frequencyInHz, duration);
delete[] state.position;
delete[] state.velocity;
}
```

## 音频文件保存

```cpp
void saveaudiofile(std::vector<float>& v, std::string filename)
{
    const std::string path = "scanned/";
    // 设置音频文件
    AudioFile<float> a;
    a.setNumChannels(1);
    a.setBitDepth(24);
    a.setNumSamplesPerChannel(44100);

    {
        a.samples[channel][i] = v[i];
    }
    a.save(path + filename, AudioFormat::Aiff);
}
```

## Render 命名空间实现

### 背景填充

```cpp
namespace Render
{
void fillbackground(png::image<png::rgb_pixel>& image) {
    png::rgb_pixel px(0x04, 0x13, 0x31);
    for (uint32_t y = 0; y < image.get_height(); ++y) {
        for (uint32_t x = 0; x < image.get_width(); ++x) {
            image.set_pixel(x, y, px);
        }
    }
}
```

### 像素绘制

```cpp
void drawpx(png::image<png::rgb_pixel>& image, int x, int y) {
}
```

### 直线绘制 (Bresenham 算法)

```cpp
void drawline(png::image<png::rgb_pixel>& image, int x1, int y1, int x2, int y2)
{
    int x, y, dx, dy, dx1, dy1, px, py, xe, i;
    dx = x2 - x1; dy = y2 - y1;
    if (dx == 0) {
        if (y1 < y2) std::swap(y1, y2);
        for (y = y1; y <= y2; y++)
            drawpx(image, x1);
        return;
    }
    if (dy == 0) {
        if (x1 < x2) std::swap(x1, x2);
        for (x = x1; x <= x2; x++)
            drawpx(image, x, y1);
        return;
    }
    dx1 = abs(dx); dy1 = abs(dy);
    px = 2 * dx1 - dy1; py = 2 * dy1 - dx1;
    if (dy1 >= dx1) {
        x = x1; y = y1; xe = x2;
    } else {
        x = x2; y = y2; xe = x1;
    }
    drawpx(image, x, y);
    for (i = 0; i < xe; i++) {
        x++;
        if (px < 0) else {
            if ((dx < 0) || (dy > 0)) y = y + 1; else y = y - 1;
            px = 1;
        }
        drawpx(image, x, y);
    }
    if (dy >= 0) {
        x = x1; y = y1; xe = y2;
    } else {
        x = x2; y = y2; xe = x1;
    }
    drawpx(image, x, y);
    for (i = 0; i < xe; i++) {
        y++;
        if (py <= 0) else {
            if ((dx <= 0) || (dy > 0)) x = x + 1; else x = x - 1;
            py = 1;
        }
        drawpx(image, x, y);
    }
}
```

### 波形绘制

```cpp
void drawwave(png::image<png::rgb_pixel>& image, std::vector<uint32_t>& signalY)
{
    uint32_t y = 0, ox = 0, oy = 0;
    for (uint32_t x = 0; x < image.get_width(); ++x) {
        y = signalY[x];
```



```cpp
if (x == 0) ox=x,oy=y;

drawline(image,x,y,ox,oy);

ox=x;oy=y;

}
}
```

```cpp
void normalizedToimg(png::image<png::rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2) {

    uint32_t halfHeight=image.get_height()/2;

    double value=0.0;

    if (v2.size() == 0 || v2.size() > v1.size()) {

        v2.resize(v1.size());

    }

}
```

```cpp
for (uint32_t i=0;i<v1.size();++i) {

    value=v1[i];

    if (value >= 0.0) {

        v2[i]=halfHeight-halfHeight*value;

    } else if (value < 0.0) {

        v2[i]=halfHeight+halfHeight*value;

    }

}
```

```cpp
void renderimage(png::image<png::rgb_pixel>& image, std::vector<uint32_t>& v) {

    fillbackground(image);

    drawwave(image, v);

}
```

```cpp
void saveimagefile(std::vector<uint32_t>& v, std::string filename) {

    const std::string path="scanned/";

    png::image<png::rgb_pixel> image(44100,600);

    renderimage(image,v);

    image.write(path+filename);

}
```

```cpp
void saveimagefile(std::vector<float>& v2, std::string filename) {

    const std::string path="scanned/";

    png::image<png::rgb_pixel> image(44100,600);

    std::vector<uint32_t> v;

    normalizedToimg(image,v2,v);

    renderimage(image,v);

    image.write(path+filename);

}
```

```cpp
void normalizedToimg(png::image<png::rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2) {

    uint32_t height=image.get_height();

    if (v2.size() == 0 || v2.size() > v1.size()) {

        v2.resize(v1.size());

    }

    for (uint32_t i=0;i<v1.size();++i) {

        v2[i]=height-height*v1[i];

    }

}
```

## 附录 A：C++20 代码

```cpp
43 const int duration=4;
44 const double sampleRate=44100.0;
45 std::vector<float> vectorsynth;
46 std::vector<float> envelope;
47
48
49 using namespace indicators;
50 // 隐藏光标
51 show_console_cursor(false);
52
53 // 设置进度条
ProgressBar({
55 option::BarWidth{50},
56 option::Start("{",
57 option::Fill("0"),
58 option::Lead("0"),
59 option::Remainder("-"),
60 option::End(" "),
61 option::PostfixText("Setup Vector Synth 1/2",
62 option::ForegroundColor(Color::cyan),
63 option::FontStyles(std::vector<FontStyle>{FontStyle::bold})
64});
65
66
67 // 更新进度
68 bar.set_progress(0);
69 SignalGenerators::generatevectorsynth(vectorsynth,duration,440);
70 SignalGenerators::saveaudiofile(vectorsynth,"01-vectorsynth.aiff");
71 Render::saveimagefile(vectorsynth,"02-vectorsynth.png");
72
73 // 更新进度
74 bar.set_progress(50);
75 bar.set_option(option::PostfixText("Generating: Vector Synth 2/2"));
76
77 ADSR::Env(sampleRate, duration);
78 env::generateenvelope(envelope);
79 env::applyenvelope(vectorsynth,envelope);
80 SignalGenerators::saveaudiofile(vectorsynth,"03-final_vectorsynth.aiff");
81 Render::saveimagefile(vectorsynth,"04-final_vectorsynth.png");
82
83 // 更新进度
84 bar.set_progress(100);
85 bar.set_option(option::PostfixText("Done 2/2"));
```



## C++ 信号生成与渲染代码

### 核心功能函数

```cpp
// 显示光标
show_console_cursor(true);
return 0;
```

### `SignalGenerators` 命名空间

```cpp
namespace SignalGenerators
{
    void gain(std::vector<float>& v, double gain)
    {
        for (uint32_t i = 0; i < v.size(); ++i)
            v[i] = v[i] * gain;
    }
}
```

### 信号处理函数

#### `normalize`
```cpp
void normalize(std::vector<float>& v)
{
    float max = 0.0, value = 0.0;
    for (uint32_t i = 0; i < v.size(); ++i) {
        value = v[i];
        if (value > max) { max = value; }
    }
    // max = std::ceil(max);
    for (uint32_t i = 0; i < v.size(); ++i)
        v[i] = (v[i] / max) + 0.707;
}
```

#### `addwaves`
```cpp
void addwaves(std::vector<float>& v1, std::vector<float>& v2, std::vector<float>& v3)
{
    for (uint32_t i = 0; i < v1.size(); ++i)
        v3[i] = v1[i] + v2[i];
}
```

#### `generetrianglewave`
```cpp
void generetrianglewave(std::vector<float>& v, int duration, double frequencyInHz)
{
    const double sampleRate = 44100.0;
    for (uint32_t i = 0; i < sampleRate * duration; ++i)
        v.push_back(M_2_PI * asin(sin(frequencyInHz * 2 * M_PI * i / sampleRate)));
}
```

#### `generateinversesawtoothwave`
```cpp
void generateinversesawtoothwave(std::vector<float>& v, int duration, double frequencyInHz)
{
    const double sampleRate = 44100.0;
    double period = sampleRate / frequencyHz;
    std::vector<float> temp;

    for (uint32_t i = 0; i < period; ++i) {
        temp.push_back(-2 / M_PI * atan(1 / tan(frequencyHz * M_PI * i / sampleRate)));
    }
    for (uint32_t i = 0; i < sampleRate * duration; ++i) {
        v.push_back(temp[temp.size() - (i % temp.size())]);
    }
}
```

#### `generatesawtoothwave`
```cpp
void generatesawtoothwave(std::vector<float>& v, int duration, double frequencyInHz)
{
    const double sampleRate = 44100.0;
    for (uint32_t i = 0; i < sampleRate * duration; ++i) {
        v.push_back(-2 / M_PI * atan(1 / tan(frequencyHz * M_PI * i / sampleRate)));
    }
}
```

#### `generatesquarewave`
```cpp
void generatesquarewave(std::vector<float>& v, int duration, double frequencyInHz)
{
    const double sampleRate = 44100.0;
    double period = sampleRate / frequencyHz;
    double dutyCycle = period * 0.5;
    for (uint32_t i = 0; i < sampleRate * duration; ++i) {
        if ((int(i % period)) >= 0 && (int(i % period)) < dutyCycle) {
            ss = 0.7;
        } else {
            ss = -0.7;
        }
        v.push_back(ss);
    }
    v[0] = 0.0;
    v[v.size() - 1] = 0.0;
}
```

#### `generatevectorsynth`
```cpp
void generatevectorsynth(std::vector<float>& v, int duration, double frequencyInHz)
{
    float transition[4][4] = {{1.0, 0.5, 0.5, 0.0}, {0.5, 0.0, 0.0, 0.5}, {0.25, 0.0, 0.0, 1.0}, {0.5}, {0.25, 0.0, 0.0}};
    const double sampleRate = 44100.0;
    std::vector<float> sample1;
    std::vector<float> sample2;
    std::vector<float> sample3;
    std::vector<float> sample4;

    generetrianglewave(sample1, duration, frequencyInHz);
    generateinversesawtoothwave(sample2, duration, frequencyInHz);
    generatesawtoothwave(sample3, duration, frequencyInHz);
    generatesquarewave(sample4, duration, frequencyInHz);

    int ptr = 0;
    for (int i = 0; i < 4; ++i) {
        for (int j = 0; j < 5; ++j) {
            sample1[ptr] = sample1[i][0];
            sample2[ptr] = sample2[i][1];
            sample3[ptr] = sample3[i][2];
            sample4[ptr] = sample4[i][3];
            ptr++;
        }
    }
    v.resize(sample1.size());
    addwaves(sample1, sample2, v);
    addwaves(v, sample3, v);
    addwaves(v, sample4, v);
    normalize(v);
}
```

### 音频文件保存

#### `saveaudiofile`
```cpp
void saveaudiofile(std::vector<float>& v, std::string filename)
{
    const std::string path = "vectorsynth";
    // 设置音频文件
    AudioFile<float> a;
    a.setNumChannels(1);
    a.setDepth(24);
    a.setSamplesPerChannel(44100);

    for (int i = 0; i < a.getNumSamplesPerChannel(); ++i) {
        for (int channel = 0; channel < a.getNumChannels(); ++channel) {
            a.samples[channel][i] = v[i];
        }
    }
    a.save(path + filename, AudioFileFormat::Aff);
}
```

### `Render` 命名空间

#### `fill`
```cpp
namespace Render
{
    void fill(image<rgb_pixel>& image)
    {
        rgb_pixel px(0x4, 0xb1, 0x3);
        for (uint32_t y = 0; y < image.height(); ++y) {
            for (uint32_t x = 0; x < image.width(); ++x) {
                image(x, y) = px;
            }
        }
    }
```

#### `drawpx`
```cpp
    void drawpx(image<rgb_pixel>& image, int x, int y)
    {
        if ((x >= 0) && (x < image.width()) && (y >= 0) && (y < image.height())) {
            rgb_pixel px(0x7a, 0xb, 0xe3);
            image(x, y) = px;
        }
    }
```

#### `drawline`
```cpp
    void drawline(image<rgb_pixel>& image, int x1, int y1, int x2, int y2)
    {
        int x, y, dx, dy, dx1, dy1, px, py, xe, ye;
        dx = x2 - x1; dy = y2 - y1;
        if (dx == 0) {
            if (y2 < y1) std::swap(y1, y2);
            for (y = y1; y <= y2; y++) drawpx(image, x1, y);
            return;
        }
        if (dy == 0) {
            if (x2 < x1) std::swap(x1, x2);
            for (x = x1; x <= x2; x++) drawpx(image, x, y1);
            return;
        }
        dx1 = abs(dx); dy1 = abs(dy);
        px = 2 * dy - dx1;      py = 2 * dx1 - dy1;
        if (dy1 <= 0) {
            if (dx >= 0) { x = x1; y = y1; xe = x2; }
            else { x = x2; y = y2; xe = x1; }
            drawpx(image, x, y);
            for (i = 0; i < xe; i++) {
                x = x + 1;
                if (px < 0) px = px + 2 * dy1;
                else {
                    if ((dx < 0 && dy < 0) || (dx > 0 && dy > 0)) y = y + 1; else y = y - 1;
                    px = px + 2 * (dy1 - dx1);
                }
            }
            drawpx(image, x, y);
        } else {
            if (dy >= 0) { x = x1; y = y1; ye = y2; }
            else { x = x2; y = y2; ye = y1; }
            // ... logic continues in original source
        }
    }
}
```

---

## 附录 A：C++20 代码片段

### `drawline` 续篇
```cpp
{
    x = x2; y = y2; ye = y1;
}
drawpx(image, x, y);
for (i = 0; y < ye; i++) {
    y = y + 1;
    if (py <= 0)
        py = py + 2 * dx1;
    else {
        if ((dx < 0 && dy < 0) || (dx > 0 && dy > 0)) x = x + 1; else x = x - (dx - dy1);
    }
}
drawpx(image, x, y);
};
```

### `drawwave`
```cpp
void drawwave(png::image<rgb_pixel>& image, std::vector<uint32_t>& signalY) {
    uint32_t y = 0, ox = 0, oy = 0;
    for (uint32_t x = 0; x < image.get_width(); ++x) {
        y = signalY[x];
        if (x == 0) ox = x; oy = y;
        drawline(image, x, y, ox, oy);
        ox = x; oy = y;
    }
}
```

### `normalizedtoimg`
```cpp
void normalizedtoimg(png::image<rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2) {
    uint32_t halfHeight = image.get_height() / 2;
    double value = 0.0;
    if (v2.size() == 0 || v2.size() > v1.size()) {
        v2.resize(v1.size());
    }
    for (uint32_t i = 0; i < v1.size(); ++i) {
        value = v1[i];

        if (value >= 0.0) {
            v2[i] = halfHeight - (halfHeight * value);
        } else if (value < 0.0) {
            v2[i] = halfHeight + (halfHeight * fabs(value));
        }
    }
}
```

### `render`
```cpp
void render(png::image<png::rgb_pixel>& image, std::vector<uint32_t>& v) {
    fillbackground(image);
    drawwave(image, v);
}
```

### `saveimage` 重载版本 1
```cpp
void saveimage(std::vector<uint32_t>& v, std::string filename) {
    const std::string path = "vectors/";
    png::image<png::rgb_pixel> image(44100, 600);
    render(image, v);
    image.write(path + filename);
}
```

### `saveimage` 重载版本 2
```cpp
void saveimage(std::vector<float>& v2, std::string filename) {
    const std::string path = "vectors/";
    png::image<png::rgb_pixel> image(44100, 600);
    std::vector<uint32_t> v;
    normalizedto(image, v2, v);
    render(image, v);
    image.write(path + filename);
}
```

### `normalizedopetoimage`
```cpp
void normalizedopetoimage(png::image<png::rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2) {
    uint32_t height = image.get_height();
    if (v2.size() == 0 || v2.size() > v1.size()) {
        v2.resize(v1.size());
    }
    for (uint32_t i = 0; i < v1.size(); ++i) {
        v2[i] = height - (height * v1[i]);
    }
}
```

### `saveenvelopeimage`
```cpp
void saveenvelopeimage(std::vector<uint32_t>& v, std::string filename)
{
    const std::string path = "vectorsynth/";
    png::image<png::rgb_pixel> image(44100, 600);
    renderimage(image, v);
    image.write(path + filename);
}
```



# 代码文件列表

## 10-virtualanalog.cpp - 1351 字节

```cpp
// compile: clang++ -std=c++20 10-virtualanalog.cpp -o 10-virtualanalog
#include <iostream>

int main() 
{
    std::cout << "An synthesizer is a synthesizer that uses DSP components and software that generates the behavior of original electronic circuitry to digitally recreate their tone.";
    std::cout << "This method of synthesis is also referred to Virtual Analog or VA. Analog modeling synthesizers can be more reliable than their true counterpart, hardware is typically less susceptible to temperature changes.";
    std::cout << "While analog synthesizers need an oscillator for each voice, analog modeling synthesizers don't face this problem. This means that especially more modern models, can produce more polyphonic voice on which they can handle.";
    std::cout << "Modeling synthesis also provide storage and MIDI capabilities found on true analog. Analog modeling synthesizers that run entirely within host system are referred to as software synthesizers.";
    return 0;
}
```

## 11-wavetable.cpp - 1067 字节

```cpp
// compile: clang++ -std=c++20 -lpng 11-wavetable.cpp -o 11-wavetable
#define _MATH_DEFINES
#include <cmath>
#include <vector>
#include <random>
#include <filesystem>
#include "indicators.hpp"
#include <png.h>
#include "AudioFile.h"
#include "Envelope.hpp"

namespace Renderer {
    void fillbackground(image::image<png::rgb_pixel>& image, int x, int y);
    void drawpx(image::image<png::rgb_pixel>& image, int x1, int y1, int x2, int y2);
    void drawline(image::image<png::rgb_pixel>& image, std::vector<uint32_t>& signalY);
    void drawwavetoimg(image::image<png::rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2);
    void renderimage(image::image<png::rgb_pixel>& image, std::vector<uint32_t>& v);
    void savefileimage(std::vector<uint32_t>& v, std::string filename);
    void normalizedenvelopopimg(image::image<png::rgb_pixel>& image, std::vector<float>& v1, std::vector<uint32_t>& v2);
    void saveenvelopepage(std::vector<uint32_t>& v, std::string filename);
}

namespace SignalGenerators {
    void gain(std::vector<float>& v, double gain);
    void normalize(std::vector<float>& v);
    void addwaves(std::vector<float>& v1, std::vector<float>& v2, std::vector<float>& v3);
    void generatewavetable(std::vector<float>& v, int duration);
    void saveaudiofile(std::vector<float>& v, std::string filename);
}

int main() {
    namespace fs = std::filesystem;
    fs::create_directory("wavetable");

    const double sampleRate = 44100.0;
    const int duration = 1;
    std::vector<float> wavetable;
    std::vector<float> envelope;

    using namespace indicators;
    // 隐藏光标
    show_cursor(false);

    // 设置进度条
    ProgressBar bar(
        option::BarWidth{50},
        option::Start("["),
        option::Fill("0"),
        option::Lead("0"),
        option::Remainder("-"),
        option::End("]"),
        option::PostfixText("Setting up: wavetable 1/2"),
        option::ForegroundColor(Color::cyan),
        option::FontStyles(std::vector<FontStyle>{FontStyle::bold})
    );

    // 更新进度
    bar.set_progress(0);

    SignalGenerators::generatewavetable(wavetable, duration);
    SignalGenerators::normalize(wavetable);
    SignalGenerators::saveaudiofile(wavetable, "01-wavetable.aiff");
    Render::savefile(wavetable, "02-wavetable.png");

    // 更新进度
    bar.set_progress(50);
    bar.set_option(option::PostfixText("Generating wavetable 2/2"));

    ADSR::Envelope env(sampleRate, duration);
    env.generateenvelope(envelope);
    env.applyenvelope(wavetablewave, envelope);
    SignalGenerators::saveaudiofile(wavetablewave, "03-final_wavetable.aiff");
    Render::saveimage(wavetablewave, "04-final_wavetable.png");

    // 更新进度
    bar.set_progress(100);
    bar.set_option(option::PostfixText("Done 2/2"));

    // 显示控制台
    show_cursor(true);
    return 0;
}
```

## 附录 A：C++20 代码片段

### 全局变量与初始化函数

```cpp
int lfo[2048];
float wavetable[2048][2048];

void setuplfo() {
    for (int i = 0; i < 2048; i++) {
        lfo[i] = int(2047 - 1023 * sin((static_cast<double>(i)) / 2048 * 2.0));
    }
}

void setupwavetable() {
    for (int i = 0; i < 2048; i++) {
        wavetable[0][i] = M_2_PI * asin(sin(440 * 2 * M_PI / 2048));
        wavetable[511][i] = -2 / M_PI * atan(1 / tan(440 * M_PI / 2048));
        wavetable[1023][i] = sin((static_cast<double>(i)) / 2048 * 440 * 2.0 * M_PI);
        wavetable[1535][i] = M_2_PI * asin(sin(440 * 2 * M_PI / 2048));
        wavetable[2047][i] = -2 / M_PI * atan(1 / tan(440 * M_PI / 2048));
    }
}
```

### 波表插值生成逻辑

```cpp
} else if (wavetable[0][i] > wavetable[511][i]) {
    wavetable[j][i] = wavetable[0][i] - (step * j);
} else if (wavetable[0][i] == wavetable[511][i]) {
    wavetable[j][i] = wavetable[0][i];
}

for (int i = 0; i < 2048; ++i) {
    diff = std::fabs(wavetable[511][i] - wavetable[1023][i]);
    step = diff / 511;
    for (int j = 511; j < 1024; ++j) {
        if (wavetable[511][i] < wavetable[1023][i]) {
            wavetable[j][i] = wavetable[511][i] + (step * j);
        } else if (wavetable[511][i] > wavetable[1023][i]) {
            wavetable[j][i] = wavetable[511][i] - (step * j);
        } else if (wavetable[511][i] == wavetable[1023][i]) {
            wavetable[j][i] = wavetable[511][i];
        }
    }
}

for (int i = 0; i < 2048; ++i) {
    diff = std::fabs(wavetable[1023][i] - wavetable[1535][i]);
    step = diff / 511;
    for (int j = 1023; j < 1536; ++j) {
        if (wavetable[1023][i] < wavetable[1535][i]) {
            wavetable[j][i] = wavetable[1023][i] + (step * j);
        } else if (wavetable[1023][i] > wavetable[1535][i]) {
            wavetable[j][i] = wavetable[1023][i] - (step * j);
        } else if (wavetable[1023][i] == wavetable[1535][i]) {
            wavetable[j][i] = wavetable[1535][i];
        }
    }
}

for (int i = 0; i < 2048; ++i) {
    diff = std::fabs(wavetable[1535][i] - wavetable[2047][i]);
    step = diff / 511;
    for (int j = 1535; j < 2048; ++j) {
        if (wavetable[1535][i] < wavetable[2047][i]) {
            wavetable[j][i] = wavetable[1535][i] + (step * j);
        } else if (wavetable[1535][i] > wavetable[2047][i]) {
            wavetable[j][i] = wavetable[1535][i] - (step * j);
        } else if (wavetable[1535][i] == wavetable[2047][i]) {
            wavetable[j][i] = wavetable[1535][i];
        }
    }
}
```

### 核心功能函数

```cpp
void generatewavetable(std::vector<float>& v, int duration) {
    const double sampleRate = 44100.0;
    setupfo();
    setupwavetable();
    for (int i = 0; i < sampleRate * duration; ++i) {
        v.push_back(wavetable[lfo][i % 2048]);
    }
}

void saveaudiofile(std::vector<float>& v, std::string filename) {
    const std::string path = "wavetable";
    // Setup the audio file
    AudioFile<float> a;
    a.setNumChannels(1);
    a.setDepth(24);
    a.setNumSamplesPerChannel(44100);
    for (int i = 0; i < a.getNumSamplesPerChannel(); ++i) {
        for (int channel = 0; channel < a.getNumChannels(); ++channel) {
            a.samples[channel][i] = v[i];
        }
    }
    a.save(path + filename, AudioFileFormat::Aiff);
}

namespace Render {
    void fillbackground(png::image<png::rgb_pixel>& image) {
        png::rgb_pixel px(0x04, 0x13, 0x31);
        for (uint32_t y = 0; y < image.height(); ++y) {
            for (uint32_t x = 0; x < image.width(); ++x) {
                image.set_pixel(x, y, px);
            }
        }
    }

    void drawpx(png::image<png::rgb_pixel>& image, int x, int y) {
        if ((x > 0 && (x < image.width()) && (y >= 0 && (y < image.height()))) {
            png::rgb_pixel px(0x7a, 0xb1, 0xe3);
            image.set_pixel(x, y, px);
        }
    }
}
```



# 附录 A：C++20 代码

## 文件：12-physicalmodelling_karplus_strong.cpp

### 编译命令

```bash
clang -std=c++20 -lpng 12-physicalmodelling_karplus_strong.cpp -o 12-physicalmodelling_karplus_strong
```

### 源代码

```cpp
#define _USE_MATH_DEFINES
#include <cmath>
#include <vector>
#include <random>
#include <filesystem>
#include <indicators.hpp>
#include <png++/png.hpp>
#include "AudioFile/Audio.h"
#include "Envelope.hpp"

namespace Render
{
    void fillbackground(png::image<png::rgb_pixel>&& image, int x, int y);
    void drawpix(png::image<png::rgb_pixel>&& image, int x1, int y1, int x2, int y2);
    void drawline(png::image<png::rgb_pixel>&& image, std::vector<uint32_t>& signal);
    void drawwave(png::image<png::rgb_pixel>&& image, std::vector<uint32_t>& signal, std::vector<float>& v1, std::vector<uint32_t>& v2);
    void normalizedtoimage(png::image<png::rgb_pixel>&& image, std::vector<float>& v1, std::vector<uint32_t>& v2);
    void renderimage(png::image<png::rgb_pixel>&& image, std::vector<uint32_t>& v2);
    void saveimage(std::vector<uint32_t>& v, std::string filename);
    void saveimage(std::vector<float>& v, std::string filename);
    void normalizedvelopetoimage(png::image<png::rgb_pixel>&& image, v1, std::vector<uint32_t>& v2);
    void saveenvelopetoimage(std::vector<uint32_t>& v, std::string filename);
    void saveenvelopetoimage(std::vector<float>& v, std::string filename);
}

namespace SignalGenerators
{
    void gain(std::vector<float>& v, double gain);
    void normalize(std::vector<float>& v);
    void addwaves(std::vector<float>& v1, std::vector<float>& v2, std::vector<float>& v3);
    void generatekarplusstrong(std::vector<float>& v, int duration, double frequencyInHz, double feedback);
    void saveaudiofile(std::vector<float>& v, std::string filename);
}

int main()
{
    namespace fs = std::filesystem;
    const int duration = 1;
    const double sampleRate = 44100.0;
    const double feedback = 0.2;
    std::vector<float> karplusstrong;
    int octave = 3;

    using namespace indicators;
    // 隐藏光标
    show_console_cursor(false);
    // 设置进度条
    ProgressBar bar(
        option::BarWidth({50}),
        option::Start("{"),
        option::Fill("0"),
        option::Lead("0"),
        option::Remainder("--"),
        option::End("}"),
        option::PostFixText("Generate Physical Modeling 1/1"),
        option::ForegroundColor(Color::cyan),
        option::FontStyles(std::vector<FontStyle>({FontStyle::bold}))
    );

    // 更新进度
    bar.set_progress(0);
    SignalGenerators::generatekarplusstrong(karplusstrong, duration, frequencyInHz, 0.996);
    SignalGenerators::normalize(karplusstrong);
    SignalGenerators::saveaudiofile(karplusstrong, "01-karplusstrong.wav");
    Render::saveimage(karplusstrong, "02-karplusstrong.png");

    // 更新进度
    bar.set_progress(100);
    bar.set_option(option::PostfixText("Done 1/1"));
    // 显示光标
    show_console_cursor(true);
    return 0;
}

namespace SignalGenerators
{
    class KSString
    {
    public:
        KSString(float frequencyHz, float sampleRate, float feedback)
        {
            std::random_device rd;
            std::mt19937 gen(rd);
            std::uniform_real_distribution<double> dis(-1.0, 1.0);
            m_buffer.resize(uint32_t(sampleRate / frequencyHz));
            for (size_t i = 0; i < m_buffer.size(); ++i) {
                m_buffer[i] = dis(gen);
            }
            m_index = 0;
            m_feedback = feedback;
        }

        float GenerateSample()
        {
            // 获取并返回采样
            float ret = m_buffer[m_index];
            // 对某些样本进行低通滤波（平均）
            float value = (m_buffer[m_index] + m_buffer[(m_index + 1) % m_buffer.size()]) * 0.5f + m_feedback;
            m_buffer[m_index] = value;
            // 移动到下一个样本
            m_index = (m_index + 1) % m_buffer.size();
            // 返回缓冲区中的采样
            return ret;
        }

    private:
        std::vector<float> m_buffer;
        size_t m_index;
        float m_feedback;
    };

    void gain(std::vector<float>& v, double gain)
    {
        for (uint32_t i = 0; i < v.size(); ++i) {
            v[i] = v[i] * gain;
        }
    }

    void normalize(std::vector<float>& v)
    {
        float max = 0.0, value = 0.0;
        for (uint32_t i = 0; i < v.size(); ++i) {
            value = v[i];
            if (value > max) {
                max = value;
            }
        }
        // max=std::ceil(max);
        for (uint32_t i = 0; i < v.size(); ++i) {
            // v[i]=v[i]/max;
            v[i] = (v[i] / max) * 0.707;
        }
    }

    void addwaves(std::vector<float>& v1, std::vector<float>& v2, std::vector<float>& v3)
    {
        for (uint32_t i = 0; i < v1.size(); ++i) {
            v3[i] = v1[i] + v2[i];
        }
    }

    void generatekarplusstrong(std::vector<float>& v, int duration, double frequencyInHz, double feedback)
    {
        const double sampleRate = 44100.0;
        KSString pluck(frequencyHz, sampleRate, 0.996f);
        v.resize(uint32_t(sampleRate * duration));
        for (uint32_t i = 0; i < v.size(); ++i) {
            v[i] = pluck.GenerateSample();
        }
    }
}
```

## 文件：quiz.cpp (片段)

### 代码片段 1

```cpp
294        ox=x;oy=y;
295    }
296    }
297    void normalizedtoimg(png::image<png::rgb_pixel>& image, std::vector<float>& v1,std::
299:vector<uint32_t>& v2)
300    {
301        uint32_t halfHeight=image.get_height()/2;
302        double value=0.0;
303        if (v2.size() == 0 || v2.size() > v1.size()) {
304            v2.resize(v1.size());
305        }
306        for (uint32_t i=0;i<v1.size();++i) {
308        {
309            value=v1[i];
310            if (value >= 0.0) {
311                v2[i]=halfHeight-halfHeight*value);
312            } else if (value < 0.0) {
313            {
314                v2[i]=halfHeight+halfHeight*abs(value);
315            }
316        }
317    }
318    
319 void renderimage(png::image<png::rgb_pixel>& image, std::vector<uint32_t>& v)
321    {
322        fillbackground(image);
323        drawwave(image,v);
325    }
326    void saveimagefile(std::vector<uint32_t>& v, std::string filename)
328    {
330        const std::string path="physicalmodelling";
331        png::image<png::rgb_pixel> image(44100,600);
332        renderimage(image,v);
333        image.write(path+filename);
334    }
336 void saveimagefile(std::vector<float>& v2, std::string filename)
338    {
339        const std::string path="physicalmodelling";
340        png::image<png::rgb_pixel> image(44100,600);
std::vector<uint32_t> v;
normalizedtoimg(image,v2,v);
renderimage(image,v);
image.write(path+filename);
}
```

### 代码片段 2

```cpp
void normalizedenvelopetoimg(png::image<png::rgb_pixel>&image, std::vector<float>&
v1,std::vector<uint32_t>& v) {

    uint32_t height=image.get_height();
    if (v2.size() == 0 || v2.size() > v1.size()) {
     v2.resize(v1.size());
    }
    for (uint32_t i=0;i<v1.size(); i++) {
    v2[i]=height*v1[i];
    }
}
```

### 代码片段 3

```cpp
void saveenvelopeimage(std::vector<uint32_t>& v, std::string filename) {

    const std::string path="physicalmodelling";
    png::image<png::rgb_pixel> image(44100,600);
    renderimage(image,v);
    image.write(path+filename);
}
```

### 代码片段 4

```cpp
void saveenvelopeimage(std::vector<float>& v2, std::string filename) {

    const std::string path="physicalmodelling";
    png::image<png::rgb_pixel> image(44100,600);
    std::vector<uint32_t> v;
    normalizedenvelopetoimg(image,v2,v);
    renderimage(image,v);
    image.write(path+filename);
}
```



```cpp
// compile: clang -std=c++20 quiz.cpp -o quiz
#include <iostream>
#include <fstream>
#include <vector>
#include <algorithm>
#include <random>

namespace quiz
{
    class Quiz
    {
    public:
        Quiz(const std::string &q, const std::string &a) : _a=a,_q=q; {}
        virtual ~Quiz() {}
        std::string getQ() { return _q; }
        std::string getA() { return _a; }
    private:
        std::string _q;
        std::string _a;
    };
}
std::vector<quiz::Quiz> game;
```

## Quiz 数据

`Quiz("0-5v", "表示 0 到 5 伏的范围，这在模块化合成器的门信号（gates）、触发信号（triggers）和调制控制电压中很常见。门信号和触发信号将事件视为新音符 - 通常从 0v 上升到 5v（0v 到 10v 也很常见，大约是起始事件的中间）。门信号保持在 5v（或 10v）时被视为高电平，返回 0v 时视为低电平。");`

`Quiz("1 pole", "这种数字和缩写格式（dB/octave = 每八度分贝）用于描述滤波的斜率。");`

`Quiz("pp", "通常指脉冲宽度。");`

`Quiz("ve", "通常代表电压。");`

`Quiz("2 pole", "这种数字和缩写格式（dB/octave = 每八度分贝）常用于描述滤波的斜率。滤波器通常有一个截止频率，它通过该频率来调整信号。这种滤波器在信号频率高于截止频率时，每八度衰减 12 分贝。12db/octave 滤波器通常被称为“二极滤波器”（因为每个极点的设计会产生 6 分贝的衰减）。这种滤波器在 vintage Korg 和 Oberheim 合成器中非常常见，能产生更明亮的声音。");`

`Quiz("a common clock division", "一种用于 MIDI、同步以及其他电子音乐系统的常见时钟划分。这意味着在内部，24 个时间细分可以被细分以产生十六分音符。这种快速内部时钟可以进一步细分以产生十六分音符（+6）、八分音符等。");`

`Quiz("3.5 mm", "用于安装 Eurorack 模块的标准螺丝纹。。，这种尺寸略大于 1/8\"");");`

`Quiz("24 db/oct", "这种数字和缩写格式（dB/octave = 每八度分贝）常用于描述滤波的斜率。滤波器通常有一个截止频率，它通过该频率来调整信号。这种滤波器在信号频率高于截止频率时，每八度衰减 24 分贝。24db/oct 滤波器在 vintage Moog 和 Roland 合成器中非常常见。四极滤波器通常与主观的“更圆润”的二极滤波器在一起 - 这种泛化的说法总是是危险的。");`

`Quiz("3 Pole", "这种数字和缩写格式（dB/octave = 每八度分贝）常用于描述滤波的斜率。滤波器通常有一个截止频率，它通过该频率来调整信号。这种滤波器在信号频率高于截止频率时，每八度衰减 12 分贝。12db/octave 滤波器通常被称为“二极滤波器”（因为每个极点的设计会产生 6 分贝的衰减）。它经常被用作一种代码简写，用于在不提及乐器名称的情况下指代 TB-303 的 A 型低音线条。");`

`Quiz("2.5 mm", "用于安装 Eurorack 模块的常用螺丝纹。这种尺寸通常用于已经预钻孔的模块轨上。");`

## 附录 A: C++20 代码

131 低音效果。303 的许多特性归功于它的滤波器设计。

132 `quiz::Quiz("32", "有时在振荡器的八度选择开关上看到。它指的是风琴管的长度。管子越长，音调越低；32' 是你所看到的最低设置，已经进入地震级的水平了。管子或设置为长度的一半（'16'）则高一个八度；长度为倍（'8'）则高两个八度，以此等等。")`

137 `quiz::Quiz("3U", "指高度为3 机架单元（U）的模块——这是 Eurorack 最年轻的格式。")`

141 通常指滤波器的频率响应。滤波器通常有一个被调优的截止频率或角频率。然后它根据距离截止频率每远一个八度，将通过它的信号频率谱减少（每24分贝的倍数）。这种设计用于 Moog 和 Roland 合成器。4 极滤波器通常被认为与主观感受相关，比 2 极滤波器具有更“圆润”的声音——但泛泛概括是危险的。）

149 例如，这种尺寸被 Pittsburgh Module 用于外壳。

150 `quiz::Quiz("4U", "指高度为 4 机架单元（U）的模块——即，Buchla 和Serge 倾向于采用更具实验性的合成和音乐方法，因此一些用户将 '4U' 视为一种荣誉标志，代表他们不随大流且很酷（他们确实如此）。")`

155 `quiz::Quiz("4S", "有时在振荡器的八度选择开关上看到。它指的是风琴管的长度。管子越短，音调越高；4' 是你在所有振荡器上看到的最高八度设置。管子或设置为长度的两倍（'8'）则高一个八度；长度的两倍（'16'）则高两个八度，以此等等。")`

160 `quiz::Quiz("5U", "指高度为 5 机架单元（U）或 8.75''（22.2 厘米）的模块，这与复古 Moog 标准最为相关。我们有时会将它与 Moog Units 混用，后者指的是比 Mi 宽 2.125''（5.4 厘米）的标准宽度。这种设计既是历史的也是传统的。一些用户将 '5U' 视为一种荣誉标志，代表他们很传统且酷（他们确实如此）。还有一种来自 MOTM 的流行 5U 格式，使用了不同的宽度和电源连接。它已经被淘汰，但今天仍有少量的 MOTM 格式在使用。")`

170 通常指滤波器的频率响应行为。滤波器通常有一个被调优的截止频率或角频率。然后它将通过它的信号频率谱根据其距离截止频率每远一个八度减少（每6分贝的倍数），直到音量。6dB/八度的滤波器通常被称为“单极”滤波器（因为滤波器设计中的每个极都会导致 6dB 的衰减，并且对信号抽样的影响较小）。低通滤波器（LPG）通常——并非总是——使用 1 极通过滤波器，将其截止频率上方每一个八度的谐波强度减少 6 分贝。")

`Quiz:"888","Roland TR-888 节奏作曲器使用模拟电路创建了它的所有声音。它刚出来时并不受欢迎，因为模拟声音听起来并不真实。但后来，House 和 Hip-Hop 等音乐风格接受了它的合成声音。它创建的“808 鼓”是他们试图模仿的乐器。复制最多的是 808 踢鼓声，它倾向于低音调、长衰减的正弦波形，并带有清脆的攻击音。"`

`Quiz:"8","有时在振荡器的八度开关上看到。它指的是风琴的长度。管子越短，音调越高；8' 通常与中 C 相关。管子或设置为长度的（'4'）则高一个八度；管子或设置为长度的两倍（'16'）则低一个八度。"`

`Quiz:"909","TR-909 节奏作曲器是 Roland 从未推出的 TR-808 的续作。它将用于闭��和镲的数字样本与 808 的模拟声音相结合，并也变得流行。当一个模块说 909 时，指的就是它。"`

`Quiz:"A-440","这是中 C 的频率（频率，每秒循环次数）。它通常被用作调音参考。"`

`Quiz:"A/B Technique","一种麦克风放置技术，将两个心形或全指向性麦克风放置在某处之间...")`

## 附录 C：C20 代码

`Quiz::("AD", "两阶段攻击/衰减（Attack/Decay）包络的缩写。这种简单的包络形状从 0 升到其最大水平（通常为 5、8 或可能是 10 伏），速度由其 Attack 参数定义，然后立即以其 Decay 参数定义的速率回落到 0。此结构的一个变体是 AHD 包络：在完成攻击阶段后，它会在最大水平保持特定时间（与 AR 包络相比，后者在音符门保持为高电平期间会一直保持在最大水平），然后衰减回零。我听过有些例子是 AHD 和 AR 的混合体，其在固定时间内或在输入门信号保持为高电平期间都保持在最大水平。")`

`Quiz::("加法合成", "使声音独有的特性之一是泛波的混合——即构建声音的纯净成分。加法合成是一种让你直接控制每个分量泛波的技术，允许你直接拨出你想要的混合比例。由于加法合成听起来是非常真实的（或在屏幕上），要制作出正确的混合比例来创造另一种声音确实需要大量工作，尤其是每个泛波的强度随时间变化。加法振荡器在模块化合成中相对稀少；示例包括 Verbos 振荡器和 Noise Name 的 ELHARMONIC")`

`Quiz::("AES", "音频工程学会（Audio Engineering Society）。")`

`Quiz::("AES3", "有时被称为 AES/ESU）由音频工程学会和欧洲广播联盟开发的数字音频传输标准，用于携带双通道音频数据标准。AES 是 XLR 电缆以及 RCA 和 SPDIF 电缆背后的协议。")`

`Quiz::("AFG", "音频频率发生器（Audio Frequency Generator）是 Electronics 公司的一款功能非常齐全的模拟振荡器。它已经停产，但翻新的的 B 类库存每隔一段时间都会上架出售。据我所知，扩展模块从未发布过（至少没有广泛发布过）。")`

`Quiz::("触后", "也称为‘压力灵敏度’）。某些键盘会测量你按键的力度，并将其转换为来自 MIDI 的电压（或其他控制）信号，该信号可以转换为你使用的电压（或控制电压），以为音符增加表现，例如颤音或滤波器脉冲。单音触后对整个键盘使用一个压力值，无论你按了哪个键；多音触后则为每个键产生一个信号。重要的小知识：触控键盘实际上测量的是接触皮肤的表面积，而不是压力或力——因此你可以通过在指尖和指节之间滚动来增加或减少触后量。")`

## 附录 A：C++20 代码

`quiz:Quiz("ADHDSR", "攻击（Attack）、衰减（Decay）、维持（Sustain）和释放（Release）。这是一种稍微不同的 ADSR 包络，在攻击上升且开始下降之前，通常会将值保持在其最大值处指定一段时间。")`

`quiz:Quiz("混叠 (Aliasing)")`

`quiz:Quiz("交流电或 AC", "录音室使用的电流类型是通过音频通道运行的信号。在交流电中，方向会‘交替’，在电路中往回流动。")`

`quiz:Quiz("Amp", "幅度调制（AM）是指使用第二个称为调制器的信号来改变称为载波的（通常是音频信号，在 0 伏以上和以下切换）的信号幅度或调制的技术。在典型的幅度调制（AM）场景中，一个带有正电压的低频振荡器（例如在 0 到 5v 之间，或者更小的 1v 到 2v 之间）被馈入电压控制放大器的输入，通过它为音频信号增加颤音。这被称为双象限调制器，调制信号中的任何负向波动都会被忽略；当将其添加到你的 LFO 时，可以确保声音不会在 LFO 波形的下部偏离处中断。")`

`quiz:Quiz("环境场", "远离源的区域，那里的混响比直接声源大。")`

`quiz:Quiz("环境混合", "这指的是将麦克风放在环境场中录制声音的环境混响。录音引擎在对乐器进行直接混合的同时执行此操作，以在录中创建直接声和混响声的混合。")`

`quiz:Quiz("Amp", "根据语境，是‘放大器’、‘幅度’或‘安培’的缩写。")`

`quiz: Quiz("安培", "电流的单位，缩写为 Amp。")`

`quiz: Quiz("放大器", "一种增加电信号电平或幅度的设备")`

`quiz: Quiz("校准", "使产生的声音变大。")`

`quiz: Quiz("幅度", "波形的高度。在音频中，它意味着信号强度或声音的响度。")`

`quiz: Quiz("模拟录音", "音频波形连续变化的录制。录音室中最常见的模拟录音示例是制在磁带上。")`

`quiz: Quiz("模拟数字转换器 (A/D, 或 ADC)", "一种将不断变化的信号（模拟）转换为离散数字（数字）的设备，与没有数字（晶体管、二极管、电容器）的电路设计相比。")`

`quiz: Quiz("AR", "两阶段攻击/释放包络从 0 伏范围到其最大水平（通常为 5、8 或可能是 10 伏），速率由其 Attack 参数设置，然后在门信号保持为高电平期间保持在该值处。当门信号回到 0 时，包络以其 Release 参数设置的速率回落到 0。（有一类型的包络被称为 AHD - 攻击/衰减 - 在其中你可以指定一个固定时间让其保持在最大水平。）")`

`quiz:Quiz("琶音器", "在音乐理论中，琶音器是一种在键盘上逐个播放音符而不是一次性的类型。琶音器通常内置在键盘或声音模块中——它让你更方便地演奏复杂的和弦。好的琶音器有不同的模式（向上、来回，等），甚至可以具有锁存（latch）功能，可以在你释放按键后仍保持音符。")`

`quiz:Quiz("ASR", "模拟移位寄存器（ASR）是采样与桶形寄存器的交叉。当最初触发时，它采样输入电压并输出到第一个输出。在第二个输出处，再次采样输入电压。AS 有三个阶段。")`

`quiz:Quiz("攻击/衰减/维持", "具有四个阶段的包络器：攻击、衰减、维持和释放。当此包络器接收门信号时，它从 0 伏开始（连接到电压控制放大器相当于静音，连接到电压控制滤波器或振荡器相当于最低电压），并上升到它可以输出的最大电压——通常取决于系统为 5 到 10 伏；通过衰减控制立即下降，直到达到维持控制设置的电压。如果输入仍然活跃，它将保持，直到门回到 0 伏（通常是因为你释放了控制按键等）。此时，电压以释放控制设置的速率回落到 0 伏。")`

`quiz::("攻击/衰减", "两阶段攻击/衰减（Attack/Decay）包络的缩写。这种简单的包络形状从 0 升到其最大水平（通常为 5、8 或 10 伏），速度由其 Attack 参数定义，然后立即以其 Decay 参数定义的速率回落到 0。AHD 是它的变体：在完成攻击阶段后，它会在最大水平保持特定时间（与 AR 包络相比，后者在音符门保持为高电平期间会一直保持在最大水平），然后衰减回零。我听过有些例子是 AHD 和 AR 的混合体，其在固定时间内或在输入门信号保持为高电平期间都保持在最大水平")`

`quiz:Quiz("AND 函数", "最常见的布尔或逻辑函数之一，AND 只有在所有输入都为‘高’时才输出门信号（即如果输入 1 和 2 都低则为低）。NAND 函数具有反向输出：如果两个输入都是高，输出为低，否则为高-")`

## 附录 A：C20 代码

- `quiz("攻击/衰减/维持/释放 (ADSR)","这是一种稍微复杂一点的的 ADSR 包络，它在攻击上升之后、衰减开始下降之前，会将电压在指定时间内保持在其最大值。")`

- `quiz("攻击/释放 (Attack/Release)","两阶段攻击/释放包络按照其攻击参数设置的速率从 0 伏上升到最大值（通常为 5、8 甚至 10 伏），只要包络发生器中的门限信号保持高电平，它就会保持在该值。当门限信号恢复为零时，包络的输出也按照其释放参数设置的速率降回零。（另一种不同类型的包络被称为 AHD - 攻击/衰减 - 它在衰减达到最大值时有一个设定的特定固定时间，而不是取决于门限信号。")`

- `quiz("攻击 (Attack)","这通常指包络的第一阶段，发生从 0 伏开始处（当静音功能是一个放大器模块时）到通常的响度值。打击乐和拨弦乐器的攻击速度非常快；缓慢、悠闲的风管或弦乐器可能有缓慢的攻击。")`

- `quiz("衰减 (Attenuation)","电或声学强度的降低。音频以分贝（DB）测量，通常是指音量的减小。声波在空气中传播时自然衰减。工程师故意在录音室链路图或插件中衰减信号以防止过载。")`

- `quiz("衰减器 (Attenuator)","控制单元可以减少通过它的信号或电压强度。")`

- `quiz("反相器 (Attenuverter)","衰减器的特殊版本，可以反转通过它的信号或电压的相位。大多数衰减器在中心位置时为直通无信号；当你顺时针旋转时，你增加了信号的正相；当你逆时针旋转时，你增加了信号的反相版本。某些衰减器是带有极性开关的普通衰减器。")`

- `quiz("音频频率发生器 (Audio Frequency Generator)","AFG（音频频率发生器）是 Livewire Electronics 发布的一种功能非常强大的振荡器。据我所知，它曾在许多扩展模块中出现过，从未发布过（或未广泛发布）。")`

- `quiz("音频 (Audio)","广义上讲，音频是人类用耳朵听到的频率范围。在技术意义上，音频是指声音的传输、录制或复制，无论是数字的、电气还是声学的。")`

- `quiz("自动对白同步 (ADR)","电影拍摄后在受控环境中重新录制对话的过程，目的是替换录音质量较的对话。")`

- `quiz("自动增益控制 (Automatic Gain Control)","具有长释放时间的压缩器，用于保持音频音量处于一致水平。")`

- `quiz("自动化 (Automation)","编程在录音和播放期间自动发生某些更改。在录音室，工程师在调音台和电脑上使用自动化，以便各种参数在多轨道录音和播放期间的不同时间自动更改。这种预处理功能使得更容易创建更改，而无需在实时手动执行这些更改。")`

- `quiz("辅助设备 (Auxiliary Equipment)","与调音台一起工作修改信号的外部信号处理设备。")`

- `quiz("返回 (Return)","简称 Aux Return 或 Return。调音台或 DAW 上的输入将发送回通道混音的带效果信号。")`

- `quiz("辅助发送 (Auxiliary Send)","简称 Aux Send 或 Send。控制调节从调音台或 DAW 的输入通道通过该总线发送到辅助设备或插件的信号。这用于创建一个效果环路，处理信号的一部分，然后通过辅助返回到混音中。")`

- `quiz("轴 (Axis)","设备运行的虚构线。例如，在：[麦克风开启]状态下，轴是一条从麦克风正面朝振膜方向伸出的虚线，它界定了麦克风拾取声音的最佳位置。导致麦克风“离轴”的声音将无法清晰地拾取。")`



- quiz("背景噪声 (Background Noise)","指此处 (1) 房间内与录制的乐器或人声无关的环境噪声；(2) 与录制信号无关的系统噪声。（所有电子设备都会发出某种程度的噪声）。")

- quiz("隔声板 (Baffles)","用于防止声波进入或离开空间的吸声面板。")

- quiz("平衡 (Balance)","混音中两个乐器之间的相对电平，或立体声录制通道中音频信号的相对电平。")

- quiz("音频偏置 (Audio Bias)","有一种系统使用三根线传输音频信号：一根是地（0 伏参考），第二根线携带随 0v 上下变化的音频信号，第三根是音频信号的反相拷贝，将负值变为正值。平衡（Balanced）意味着 +4dB 的参考信号（高于线路电平；低于大多数模块化合成器），尽管麦克风信号——比比较的对象弱得多且更容易受到噪声影响——始终是平衡的。模块化合成器在其内部信号中使用不平衡音频。如果你有平衡输出（或输入），你需要在平衡和不平衡音频之间使用一个特殊的模式转换器，加上任何必要的电平匹配。")

- quiz("平衡线 (Balanced Cable)","由三个（信号和地）连接器组成的电缆。两根线携带极性相反的相同信号，提供防止系统噪声的保护。平衡线的示例包括尖-环-套 (TRS) 和 XLR 电缆。")

- quiz("平衡混音器 (Balanced Mixer)","产生输入信号之和与差的电路或设备。")

- quiz("平衡调制器 (Balanced Modulator)","平衡或环形调制是一种特殊的幅度调制，一个双极性（在 0 伏上下摆动）信号调制器的频率与载波频率相加相减；产生的谐波加强原始信号。")

- quiz("香蕉头 (Banana)","另一种连接器类型（https://en.wikipedia.org/wiki/Banana_connector），用于 Buchla（控制电压）和 Serge（音频）。它们只有一根线，优点是通常可以“堆叠”的，这意味着可以将一个插孔插入另一个的背面，提供被动多路。")

- quiz("带通滤波器 (Band Pass Filter)","设备，电路，允许窄范围的频率通过电路，或衰减高于或低于指定范围的频率。")

- quiz("带阻滤波器 (Band Stop Filter)","设备，电路，衰减信号中窄范围的频率，允许频带之外的频率通过。这与带通滤波器完全相反。")

- quiz("频带轨道 (Band Track)","（某些情况下简称 Track）去掉了主人声和乐器/背景人声的歌曲混音。换句话说，包含歌曲部分的混音轨道。")

- quiz("频带 (Band)","I 频率范围，由范围的中心频率确定。2) 一群在一起演奏的音乐家。")

- quiz("带通滤波器 (Bandpass Filter)","带通滤波器 (BPF) 保持中心或截止频率周围的谐波不变，并衰减中心频率上方和下方的部分。距离中心越远，衰减越严重，基于滤波器中极点的数量，每个极点每隔一个八度产生 6dB 的衰减。")

- quiz("带宽 (Band)","在信号处理中，带宽指的是信道的可用频率，通过设备最高和最低可用频率之间的差来测量。")

- quiz("组 (Bank)","I 合成器生成器和调制器内存中的音色、序列数据和/或操作参数集合。2) 模块的一组。")

- quiz("小节 (Bar)","在音乐记法中，bar 是节的另一个术语，指包含特定拍数的特定时期，并在两侧由小节线标记。")

- quiz("Bark 标度 (Bark Scale)","人类听觉（听力）系统可以被认为是由一系列带通滤波器组成。有趣的是，滤波器的间隔并不严格遵循线性频率刻度或对数音乐刻度。频率标度（Bank Scale）试图确定这些“听觉滤波器”（称为关键频带）的中心频率和带宽是多少。")

## 附录 A：C++20 代码

测试题：“屏障反射（Barrier Mirroring）”，一种将麦克风放置在反射面附近的录音技术。如果操作正确，屏障反射可以确保直声和反射声同时到达麦克风，防止两者之间的相位抵消。

测试题：“基础配音（Basic Session）”，为基础轨道进行的首次音频录音，这些轨道承担了歌曲的功能（例如鼓和贝斯）。

测试题：“低音反射（Bass Reflex）”，一种扬声器箱体设计，箱体的一部分（开口）会增强频率。其原理是箱体内部扬声器振膜背面产生的声音从箱体前面排出，与来自低音器单元前面的声音混合。改变尺寸和位置将极大地改变低频的特性。

测试题：“低音（Bass）”，大约 250 Hz 以下的音频频率低范围。一个参考值。

测试题：“BBD（桶形延迟）”，一种音频效果的简单设计，其中输入音频是一个模拟值，并保持片刻。然后在下一个高于音频采样率的点的时钟脉冲处，该电压将通过电路中的下一个样本点（桶），并在那里采样出一个新的电平。桶形传输延迟（BOBs）通常具有两个级数的阶段或桶（256, 512, 1024, 2048 等）；延迟长度由级数数量乘以样本之间的时间间隔决定。

测试题：“束射（Beaming）”，一种在扬声器中发现的现象，而不是随着扬声器投影出的其他高频一起扩散。当你站在扬声器正前轴时，听起来好像它只产生高频，而不是低频或中频。这种现象可以通过通过扬声器内的号声喇叭传输高频来缓解。

测试题：“节拍映射（Beat Mapping）”，调整音乐作品中速度变化以设置项目速度的过程。在数字音频工作站（DAW）中，这是使用时间结构工具并将瞬态同步到适当的速度标记的过程。这种技术经常用于，例如，解决漂移或在没有节拍器的情况下录制的贝斯表演。

测试题：“节拍（Beat）”，1) 音乐中稳定、均匀的脉冲。两个频率略有不同的音频信号相互干扰导致音量周期性增加和减少，耳朵听起来为“拍音”。

测试题：“拍频（Beating）”，当两个振荡器的频率调得非常接近但并不完全相等时，它们之间的差异会导致被称为“拍频”的干扰模式。当频率差低于音频速率时，这听起来就像对组合声音的亮度使用了颤音。

测试题：“BPM”，每分钟 120 拍的速度意味着每秒有一个节拍（120 拍/分钟 x 1/60 = 2）。每分钟内发生的均匀脉冲的数量（定义了歌曲的性质）。

Tangerine Dream 和 Klaus Schulze 的浮动和弦和从独奏中弹出的无人音。从 Node 和 Reich Shift 中可以听到更多柏林学派（Berlin School）音乐。

或扬声器系统由两个独立的放大器驱动。

其中每个数字只能有两个值：0 或关闭；或者像门和分频时钟这样的二进制信号的低或高。

到双极性。模块合成器内部的一些调制信号，如颤音（var）（使振荡器的频率高于或低于它应该所在的音符（播放）- 它们本质上是双极性的）。

测试题：“比特（Bit）”，代表“0”的数字信息的最小单位。

测试题：“比特率或位深（Bitrate or Bit Depth）”，数字录制中描述每个样本的计算机比特数。比特率越高，采样声音的动态范围越大。音频样本的质量和分辨率描述为采样率和比特率的结合。（参见“采样率”）。

测试题：“混合（Blending）”，将多个声音或通道混合以形成一个。

测试题：“蓝噪声（Blue Noise）”，技术上，一种功率密度（频谱响度）随频率增加每倍八度增加 3 dB 的噪声。它具有非常明显的“嘶嘶”特征（缺乏低音）。

测试题：“布尔（Boolean）”，布尔逻辑可以有两个状态：高或低；1 或 0。

测试题：“吊架（Boom Stand）”，一种带有伸缩式支撑臂的麦克风架，用于固定麦克风。

测试题：“吊杆（Boom）”，连接在麦克风架上的伸缩式支撑臂，用于固定麦克风。

测试题：“增益（Boost）”，使用均衡器增加特定频率的增益。

测试题：“跳混（Bouncing）”（也称为“乒乓混音”或“Ponging”），通过调音台播放或数字方式将多个轨道混合到一个或两个轨道上的技术。以前经常用于在轨道无限的数字工作站中释放轨道，现在这种做法基本上已经过时了。

测试题：“边界麦克风（Boundary Microphone）”，一种设计为放在平面表面（或边界）上的全向麦克风，可以有效消除反射声引起的相位问题。压力麦克风（PZM）。

测试题：“BPF（带通滤波器）”，带通滤波器（BPF）保持中心频率周围的谐波不变，并衰减中心外的信号。距离中心越远，衰减越严重，取决于滤波器极点的数量，每个极相当于距离中心每倍八度产生 6 分贝的衰减。

测试题：“BPM”，BPM（每分钟拍数）是说明每分钟应该计算多少拍（通常是四分音符）最常用的方法。每分钟 120 拍意味着每秒有一个节拍（120 拍/分钟 x 1/60 分是 2）。

测试题：“呼吸（Breathing）”，拍频和呼吸 - 在录音室混响中，压缩器快速压缩和释放声音产生的效果，在信号电平中产生可见水平。“拍频”通常指压缩发生后的可见效应，“呼吸”是指人声中类似的效应，在声唱者吸气时提高音量。

测试题：“砖墙滤波器（Brickwall Filter）”，一种具有陡峭截止斜率类似于“砖墙”的特殊低通滤波器。虽然这些滤波器出现在 A/D 转换器中以防止混叠，但其陡峭的截止会对音频信号引入不必要的副作用，一种将单输入到放大器的两个通道，然后将其合并为一个通道的技术，从而使放大器提供的信号功率翻倍。

测试题：“布朗噪声（Brownian Noise）”，也称为棕噪声，技术上它是一种功率密度（频谱响度）随频率增加每倍八度减少 6 dB 的噪声。它具有沉重的低音感，类似于远处的海浪声。它也可以用于缓慢变化的随机电压或调制信号。

## 附录 A：C++20 代码

...的（而不是音频源）。

quiz: Quiz("Buchla Bongos","这是一个经典的连接，其中一个复杂的声源——例如一个振荡器频率调制另一个振荡器——发送到低通门（Low Pass Gate）；只需通过触发信号来“击打”内部的振荡器，或者通过瞬时的跟踪/包络衰减来产生悦耳的打击声。低通滤波在音量减小的同时减少高频谐波，这有助于抑制复杂声源的谐波，并产生类似被击打打击乐器的衰减）。")

quiz: Quiz("Bucket Brigade Delay","桶式延迟是一种期的回声或延迟设计，其中输入音频被采样为模拟电压并在短时间内保持。然后在下一个高于当前采样率的时钟脉冲处，该电压将传递到电路中的下一个采样并保持（桶）中，同时采样一个新的电平。桶式延迟（BDS）通常具有 2 的幂方的级数或桶（256, 512, 1024, 2048...）；延迟长度由级数数量乘以采样点之间的时间间隔决定。")

quiz: Quiz("Bucking","两个相同频率信号之间的相位抵消，具有相同幅度但极性相反的信号会相互抵消，最常用于乐器频率语文中。例如：使用此原理的“（反相）信号。")

quiz: Quiz("Buffered Multiple","你通常需要拆分或复制信号以查看多个目标地。这在多路输出器（multiple）中很常见，你接入一个源，然后接入额外的连接去往多个目标。有源或带缓冲的多路输出器在输入和输出之间包含一个缓冲电路，确保信号不会因为多次复制而丢失强度或完整性，并且其中一个输出端口上的任何操作都不会影响其他任何连接。某些模块具有良好的输出缓冲，可以无问题地驱动多个输出。如果你尝试使用无源源多路输出器连接三个振荡器，并发现跟踪效果并不理想（当你沿着音阶向上或向下时，它们会迅速跑调），那么你需要一个缓冲多路输出器。")

quiz: Quiz("Bulk Dump","用于系统独占批量传输（System Exclusive Bulk Dump），一种在 MIDI 设备之间传输内部参数的方法。")

quiz: Quiz("Burst Generator","当你发送模块触发器时，它会响应输出一串或“脉冲”（burst）触发。你通常可以控制触发的数量、它们之间的间距，通常还有单个触发输出发送或跳过的概率（用于随机模式）。在最温和的情况下，它可以用于在普通音符中创建“双脉冲”触发；在最极端的情况下，它被用于触发高能量、混沌的鼓点流，这些鼓点可能不符合音乐节奏。")

# 附录 C：+20 代码

quiz:Quiz("Bus","一种将一个或多个信号（通常来自不同的源）路由到指定位置的音频路径。由于总线连接到信号流，它们在音频应用中具有广泛的用途。2) 指通过总线路由的信号本身的术语（另参见“子分组”）。")

quiz:Quiz("Byte","一组八个位中的信息（数据）位。一个字节 = 八个位。")

quiz:Quiz("Cable Assembly","准备好在特定应用中安装的电缆，通常带有连接器端头。")

quiz: Quiz("Cable Harness","用于互连电子系统的电缆或电线束。")

quiz: Quiz("Cable Sheath","应用在电缆上的导电保护层。")

quiz: Quiz("Cable","一组位于包护套内的一个或多个绝缘导体、音频光纤或两者的组合，通常传输不同类型的电信号。")

quiz: Quiz("Capacitor","由两个极板和中间绝缘体制成的电子器件，用于存储静电能。例如，电容器是电容麦克风中的关键组件。")

quiz: Quiz("Capstan","磁带录音机的机械部分，用于控制磁带穿过磁头时的速度。")

quiz: Quiz("Capsule","在声学定义中，这是麦克风中包含振膜和有源元件部分的名称，即将声波转换为电流的机械结构。")

quiz: Quiz("Carbon Microphone","一种使用碳颗粒将声波转换为电流的麦克风，碳颗粒在极板之间产生电阻，从而影响电信号。")

quiz: Quiz("Cardioid Pattern","一种心形拾音模式，对来自振膜前方的声音最敏感，对侧面和后方的声音最不敏感。命名是因为其拾音形状呈心形（cardio）。")

quiz: Quiz("Carrier","有几种不同的技术使用一个信号的变化调制另一个信号。例如，在频率调制中，第二个信号（称为调制器）的变化调制频率幅（幅度调制）。")

quiz: Quiz("Cascade","连接或“串联”两个调音器，使总线的立体混声首先馈到第二个调音器中。")

quiz: Quiz("CCW","逆时针，通常用于控制旋钮的移动语境。")

quiz: Quiz("CD","紧凑光盘的缩写，或一种录有数字音频的小型光盘。")

quiz: Quiz("Cent","在调音器时，一个半音被分为 100 个单位，相对于另一个音的偏差。")

quiz: Quiz("Center Frequency","音频信号最有效的频率——这是频率钟形曲线的顶端或底部（“峰值”）。")

quiz: Quiz("Channel Path","从源到录音机的完整信号路径。例如，音频信号从麦克风传输到前放大器，进入调音台的通道条，然后通过输出进入录音机。这与监听路径不同，后者将混合信号馈到监听扬声箱或耳机中，而不影响录制的内容。（参见“监听路径”。")

quiz: Quiz("Channel","1 在磁带的宽度部分上录制的音频，或在数字工作站内隔离，通常用于合并其他通道。音频信号传输到输出端口的单一路径。")

quiz: Quiz("Chaotic","信不信由，对数学家来说，混沌并不意味着完全随机。混沌理论处理在边界内是随机的系统，例如摇晃轮子的路径或滴水水龙头的频率。虽然它们没有失控，但每个都是完全可预测的。它们以一种松散或重复的、非模式的方式出现。它也可以指不符合音乐节拍的触发脉冲。")

quiz: Quiz("Chord Chart","一种音乐谱的简写形式，提供歌曲的基础弦和基本的节奏信息。最常用于录音室乐手、节奏组或爵士乐队，以提供歌曲的骨架结构，同时允许演奏者创建自己的路径和即兴——线谱通常关注旋律线和弦结构，而和谱显示主和和节奏。（另参见“线谱”。")

quiz: Quiz("Chord","同时播放三个或多个音乐音符。2) 一个由许多歌手组成的音乐合唱团。3) 一种通过添加多个带有中等反馈的延迟来模拟人声合唱的延迟。")

quiz: Quiz("Circuit","一个完整的电路路径。2) 与定义 1 相似，但包含了所有音频信号路径和组件以完成特定的功能。")

quiz: Quiz("Class Compliant","指一种“即插即用”的设备——它可以直接插入计算机或其他主机并立即被识别")

# 附录 A：C++ 代码 20

无需安装额外的驱动程序。这在带有 USB 的 MIDI 转 CV/Gate 接口模块化单词中会出现：如果你的转换器是 USB 主机，并且向其插入一个标准的 USB 设备（如控制器键盘或推子面板），转换器将识别它。

821: 测验("节拍", "一种输入到耳机监听器的节拍器节拍声，目的是让音乐家能够与歌曲保持同步演奏。")

823: 测验("削波 (Clip)", "所有电子电路对通过其的信号强度都有限制。这些限制通常与正、负电源电平有关。如果信号试图超过这些限制，它们会在该时刻被切断或削掉。例如，+12 伏的输入电压可以在不经改变的情况下通过，但输入处的 +13 伏输出时将变为 12 伏。这种削波会导致波形产生失真，增加高次谐波（如刺耳的嗡嗡声）。以不同方式进入的不同电路在达到该阈值之前可能会有些圆滑处理；这被称为软削波（soft clipping），通常是理想的，因为可以不那么刺耳。削波之所以这样命名是因为产生的波形看起来就像波形的边缘被屏蔽了。")

834: 测验("时钟信号", "由电路中的设备发送的信号，产生脉冲或代码，以与其他设备同步工作。音乐中的例子是通过 MIDI 进行序列化。序列器发送时钟信号，以便连接的设备能够同步播放。")

837: 测验("时钟", "通常指系统中除节奏脉冲以外的任何东西。脉冲比任何可能驱动的东西都要快得多，0 就是这种情况。常见的时钟速率是 24 ppqn（每四分音符脉冲数），MIDI 时钟和 DIN Sync 正如此。然而，一个驱动序列器每次前进一个音符的触发器在系统中也可以称为“时钟”。事实上，某些模块会对主时钟进行分频和倍频以产生与主时钟有关的新时钟信号。")

846: 测验("顺时针", "顺时针，如向右旋转时钟——与时针移动的方向相同。")

847: 测验("近距离麦克风", "一种放置技术，将麦克风放置在声音源附近以拾取直接声音并拒绝环境声。")

849: 测验("同轴", "(缩写为 'Coax') 一种由屏蔽层包围单个导体的双导导体电缆。")

852: 测验("共置麦克风", "一种立体声技术，将两个麦克风的头部尽可能地靠在一起。这防止了混音中的相位抵消问题，因为另一个麦克风的声音是相同的。")



# 术语表

## 测验

### 压缩器
一种结合了压缩器和扩展器的信号处理器，广泛用于模拟系统中的降噪。在录制前对音频信号进行压缩，然后在播放阶段进行扩展。

### 比较器
一种比较一个电压电平与第二个电压电平的电子设备。第二个电压可以是比较器合成模块上的第二个输入，也可以通过旋钮或内部参考电压设置。大多数情况下，比较器输出一个门控信号，当第一个信号高于第二个信号（或反之）时，信号变为高电平；当第一个信号低于第二个信号时，信号变为低电平。在音频速率下，它将输入波形转换为方波或脉冲波，第二个信号在新的波形电压变为高或低时设置。

### 叠辑 (Comping)
可能是世界上最著名的控制电压处理器；你也会发现一些名称中专门带有 CVP 的模块。无论如何，在系统中拥有一个或多个此类类型的模块是有益的，可以帮助调节电压达到你想要的效果（或教它们新花样）。

### 控制器
从广义上说，控制器是任何用于控制另一个设备的设备。最常见于 MIDI 控制器，它们发送 MIDI 信号来控制连接的 MIDI 乐器和设备。录音室中的其他控制器示例包括监听控制器、DAW 控制器和 DJ 控制器。

### 截止频率
滤波器的截止或频率是其开始过滤的点。例如，如果一个低通滤波器的截止频率为 500 Hz（每秒循环），则 500 Hz 以下的所有谐波或其他声音成分都被允许通过，而 500 Hz 以上的所有谐波将被过滤并降低音量——即你使用的 500Hz 以上部分。

### 反时针
反时针，通常在旋转控制旋钮的背景下（在时钟指针移动的反向方向）。

### CPU
中央处理器的缩写，计算机中的主“大脑”芯片（也称为处理器）。

### 关键距离
从声源到声音和反射声量相等的距离。关键距离根据环境而变化；在有吸音墙的房间里，距离会更近；在有反射的房间里，距离会更远。

### 交叉淡
一种音频编辑技术，其中一个轨道淡出而另一个轨道淡入，以创建无缝过渡。例如，DJ 使用这种方法。

### 分频
一种根据频率将信号分成两个或多个频段的音频滤波器（也称为分频网络）。

### 串扰
通道之间音频信号的意外泄漏——例如调音台上的重叠通道。

### 截止斜率
截止频率之外频率减少的速率。斜率描述为每八度减少的分贝数。

### CV/Gate
这是用于音高和门控信号的控制电压的缩写。越来越多的控制器键盘除了常用的 MIDI 外使用了 CV/Gate 输出，使得它们更容易连接到模块合成器，因为不需要额外的 MIDI 转 CV 接口。

### CV
控制电压 (CV)的概念是模块合成器的核心。基本思想是使用模拟电压电平控制模块的参数。例如，一个控制电压可以决定振荡器的音高；第二个控制电压可以决定信号通过电压控制放大器后的音量。CV 是控制电压最常用的简写——当合成器具有通过 CV 控制滤波器谐振（反馈）的功能时，而不仅仅是前面面板上的自定义旋钮。

### CVP
CVP 是允许对通过它的电压进行处理的模块缩写——例如放大或偏移、向正或负方向方向偏移、引入（电压变化的平滑），以及其他属性，如通过比较器从输入电压中导出门控信号。Make Noise 的 Maths 可能是最著名的控制电压处理器；你也会发现一些名称中专门带有 CVP 的模块。无论如何，在系统中拥有一个或多个此类类型的模块是有益的，可以帮助调节电压达到你想要的效果（或教它们新花样）。

### CW
顺时针，如向右旋转时钟——与时针移动的方向相同。

## 附录 C：C++20 代码

### 周期
如时钟指针的运动，从特定点开始的波形的完整表达式，从零线进展到最高和最低点。一次完整的振动或声波。

### D-Sub 接口
“D-submissive（D型）”的缩写，一种 D-Sub 多针接口，最常用于连接计算机和 VGA 显示器，但也偶尔用于录音室的数字音频应用。

### D/A
数字转模拟（Digital to Analog）的缩写，将数字数据数字（数字音频）转换为离散电压电平。A/D 的逆过程。也称为 DAC。

### ADSR
这是标准 ADSR 包络发生器的一个更高级的版本，它在攻击阶段（从 0 升到峰值水平）之前引入了初始延迟。有一种补丁是将这种类型的包络路由到低通滤波器截止频率，这样当音符开始时，声音是静音且经过滤波的，在暂停后它开始增强为更明亮、更饱满的声音。

### 链链
三个或更多设备的串联连接，其中音频信号通过一个设备到达第二个设备，然后从第二个设备到达第三个设备，以此此类推。

### 阻尼
描述当音频声音停止时，限制扬声器振膜反推力（反电动势）的能力。

### 阻尼
振动系统中能量的减少，摩擦。可以指电信号中振幅的减少，或者乐器受抑制的振動（例如原声钢琴上的延音板）。

### DAW
数字音频工作站（Digital Audio Workstation）的缩写，一种用于数字录制和混合音频的设备或软件程序。

### db
分贝（decibel）的缩写，一种比较信号强度（通常是音频电平）的测量比例。

### DBX
一系列降噪系统，以开发它们的公司命名。DBX 降噪比为人知的 Dolby 系统商业成功程度较低，但在录音室偶尔仍可见。

### DC 耦合
当模块说输入是 DC 耦合时，意味着它接受 DC 电压（恒定或缓慢变化的电压）并不加修改地传递它们。这很重要，例如，如果你想用 VCA 控制通过的包络的幅度：你需要一个 AC 耦合来移除信号的 DC 分量（如其持续电平）并将其返回 0v。

### DC
芯片运行在 DC 上，通常由电池电源、USB 电源或插入墙壁的 AC 适配器提供。在模块术语中，DC 指倾向于保持一段时间稳定水平的电压，例如门输出在音符关闭时切换到 0v，音符开启时切换到 5 或 10v。它也可以指缓慢变化的电压，以及 10v。

### DCO
DCO（数字控制振荡器）是一种振荡器的混合设计——它不使用电压电平来确定振荡器的频率，而是使用数字设备作为计数来确定每个波形周期的长度，从而确定频率。优点是调谐非常稳定，与全模拟设计不同。缺点是，每个音色使用多个振荡器时，没有任何不完美会导致细微的调偏（从而产生对“厚实感”的感知）。

### 去涩
一种音频压缩器，用于减少静音声音和频率的量，特别是发字母 's' 时产生的。

### 衰减
通常，衰减是指电压或整体水平从高点下降，例如包络发生器的衰减。现实世界的情况是，如果你敲击鼓或拨动弦，它就会衰减。音量也可以从初始响度逐渐衰减，直到完全安静。它可以指混响或回声的尾迹，其中声音随时间衰减。

### Deca Tree
一种涉及三个麦克风（全向性）呈“T”型排列的立体麦克风技术。通常用于混音、管弦乐和其他大型组合，但 Deca tree 技术的变体也用于声音场合。

### 分贝
(缩写为 DB) 根据比例尺对两个水平进行测量，特定百分比的变化为一个单位。最用于描述音频电平。

### 消磁
物体去磁化的过程。在音频语境下，基本上是擦除磁带上的录音。

### 延迟/攻击/衰减/维持/释放
这是标准 ADSR 包络上的一个轻微闪烁，它在初始攻击（从 0 升到峰值水平）之前引入了时间延迟。每个补丁延迟是将这种类型的包络路由到低通滤波器截止频率，这样当音符开始时，声音是多边缘处理的，在暂停后它开始增强为更明亮、更饱满的声音。

### 延迟
在正常世界中，你只知道延迟的意思；它以不同的形式出现在模块系统中。例如，它可以指回声中重复部分的间距；一种被称为“延迟”效果的音频设备。它也可以指你延迟信号的可编程时间，例如门、触发或包络的初始阶段，使其开始时间比实际播放时间晚。此外，1 一种将音频信号录制介质或设备的过程，在延迟后播放，与原始非延迟信号混合，以创建各种效果，如更饱满的声音、回声、合唱、法兰等。2 一种产生延迟效果的信号处理器。

## 附录 A：C++20 代码

### 演示
一种初步录制，旨在让听众了解歌曲听起来是什么样的。Demo 通常涉及最小化和制作，类似于录音的“草稿”。

### 调偏
如果你有两个振荡器调谐到完全相同的频率——我的意思是完全相同的频率——那么使用多一个振荡器就没有意义。然而，当你稍微改变其中一个的调谐——也就是说，让它调偏——你将看到它们之间有趣的相互作用，通常被称为合唱或拍频。结果会更强烈且更自然，因为两个歌手或乐器很少处于同一个音。故意让乐器或信号跑调（通常是微小的）。这种效果在室内有多种用途，常用于“双轨”，混合调偏的乐器/轨道将产生更饱满的声音。

### DI
通过拾音器或直接盒将音频信号从乐器直接到调音台的过程，而不是使用麦克风。

### 振膜
麦克风中响应声波而移动的部分，将其转换为电信号。

### 差异
一种高级方式，通过从一个控制频率减去另一个频率来产生音频或泛波。

### 数字音频工作站
一种用于数字录制和混合音频并创建数字音频文件的设备或软件。DAW 可以是独立的或集成组件，但它们通常是运行在计算机上的“箱内”软件。录音室最常用的 DAW 是 Pro Tools；其他常用程序包括 Logic、Reason 和 Ableton。

### 数字表表
一种测试电流、电阻的小型设备。万用表用于录音室校准电气系统和排除故障。

### 数字录制
将音频信号转换为数字并存储为数据的过程。

### 数字转模拟器
(缩写为 D/A) 一种将数字音频转换为原始模拟音频电压水平的设备。

### 数字
曾经数字（指基于二进制逻辑、计算机和等，与传统的晶体管、运放大器、电容器和其他构成模拟电路的元件相比）是一种更糟糕的合成技术。当时的假设是数字技术产生的声音更加冷酷、脆弱且具有攻击性，不那么“真实”。电路被应用于合成器中，包括模块化系统。虽然模拟信号在我们心中始终占据着特殊地位，但实现良好的数字电路听起来可以和模拟电路一样好，而数字信号处理和编程可以创造比某些模拟电路更广泛的声音。

### 数字控制振荡器
A DCO（数字控制振荡器）是一种模拟振荡器的混合设计 - 它不再是使用电压电平来确定振荡器的音高，而是使用数字设备（如计数器）来确定每个波形周期的长度，从而确定音高。优点是调音比某些全模拟设计非常稳定。缺点是音高上的不完美会导致细微的离调（因此在在使用更多振荡器或声部时会产生‘厚实感’的感觉）。

### DIN 立声
一种立体麦克风放置技术，将两个电容放置在约 200cm 处并以 90 度角分离，以创建声场。特别适用于近距离立体声混音。（另参见“非相干混合”。）

### DIN 同步
一种用于控制序列器、效果器和鼓机节奏的信号，它使用带有 DIN 风格连接器的分布式电缆（是的，就像旧式的 MIDI 连接器，但 DIN Sync 一直流行）。Roland 将其作为标准，又名为 Sync24。Korg 使用了这种技术的变体，每四分音运行 4 次脉冲，也称为 Sync48。DIN Sync 是向模块化合成器发送时钟信号的流行方法，特别是在与其他合成器、序列器和鼓机接口时。

### 二极管滤波器
这种滤波器设计与 Roland TB-303 贝斯线最为相关，它以橡胶性的声音和激进的共鸣而闻名。

### 二极管
一种允许电流向一个方向流动但不能反向流动的电子元件。在录音室中，这些元件常用于电吉器和放大器的真空管中。

### 直弹盒
一种小型设备，将不平衡的高阻抗扬声器或乐器级输出转换为平衡的低阻抗麦克风电级输出。经常用于将电元件‘直接’连接到调音台的信号路径中，而不是使用麦克风采集。也称为直弹盒或 DI 盒。

### 直流
在现代术语中，DC 指在一段时间内保持在一个稳定水平的电压，例如门控输出，在音符关闭时为 0 伏，开启时为 5 伏。它也可以指缓慢变化的电压，如包络。（缩写为 'DC'）。沿单方向流动的电流，相对于交替方向流动的交流电 (AC)。许多电子设备由直流，通常由电池、USB 端口或插入插座的 AC 适配器提供。

### 直弹
(缩写为 'DI'）通过电拾声器或直弹盒将电信号从乐器发送到调音台的过程（而不是使用麦克风）。这种功能通常用于将‘干’声发送到监听或录音设备。2. 在扬声器中，它是扩散区域（即扬声器声音覆盖听音区域的区域）。

### 远拾音
将麦克风放置远离声源的技巧，以便采集直接声和反射声的波形。

### 多样性
(无描述)

### Double
1) 录制与第一次表演非常匹配的第二次表演，目的是混合两条轨道。2) 使用带有中等延迟的线。

### Driver
1) 扬声器中将电信号转换为声压波的换能器。2) 控制连接设备或硬件的计算机程序。

### 中断
磁带上音频信号的短暂丢失，数字音频文件中数据的短暂丢失，可能导致音频出现不预期的下降、碎裂声或啪嗒声。

### 鼓机
一种包含音乐中合成和采样鼓声的电子设备，并带有一个内部序列器，该序列器可以编程播放模式或循环。

### 鼓点句型
由鼓手演奏或输入鼓机并在歌曲中使用特定的鼓声序列。

### 干声（干声）
没有效果的声音被称为‘干声’；混合了效果（如混响）的声音被称为‘湿声’。效果器或调音台通常有干/湿混合比调节，用于设置原始未处理声音与完全效果化声音之间的比例。

### DSP
在模拟音频信号转换为数字音频后进行的任何信号处理。

### 双录（或叠录）
1) 复制录音。2) 实时录制另一段录音，意图是混合这两个录音（也称为 Overdub/Overdubbing）。‘3’是 dubstep（电子音乐的一种分支或风格）的缩写。

### 避让（Ducking）
一种基于压缩的音频效果，音频信号根据另一个音频信号的存在按比例降低，有时通过与信号处理器的‘侧链’连接来实现。一个著名的例子是位于音乐轨道上录制的口白旁白轨道，当说话者说话时，音乐音量会下降。

### 双声
双声意味着两个‘声音’。大多数早期仪器（包括模块系统）是单声的，这意味着它们一次只能演奏一个声音。有些系统通过振荡器、包络和放大器来实现双声，以便从键盘控制多个声音。

### 持续时间
长度的另一种表达方式。在时间内保持高电平的时钟脉冲或门，例如，持续时间为 100 毫秒。你保持音符的时间或序列的长度也称为持续时间。

### 动态麦克风
(也称为线圈麦克风) 一种磁场内感应线圈将声波转换为电信号的麦克风，其过程通常与扬声器相反。动态麦克风没有电容麦克风敏感，但在处理较大的声音时有效。

### 动态处理/动态信号处理
通过改变电平（或增益）来改变最响和最软声音关系的过程。动态处理器包括压缩器、限幅器、扩展器和门。

### 东岸合成
这种概括被应用于 Moog、ARP 和 EML 等东岸公司常见的合成器配置：一个或多个振荡器产生带有谐波波形（如锯齿波或方波），进入滤波器以消除大部分这些谐波，然后通过放大器塑造声音的响度。这种方法也被称为减法灵敏，因为滤波器减少了来自振荡器的谐波。今天东岸和西岸的方法在系统中都很常见。

### 回声室
一个设计有反射性非平行面的封闭房间，旨在产生声学回声（混响）。

### 回声
初始声音的清晰留存，由声波在表面反射引起。当距离足够远，我们可以检测到声源和反射之间的差异时，就能识别回声。本质上，混响是两者之间的延迟。对于发生过快而无法单独听出的每个回声。在录音室中，回声可以通过声学方式或数字处理器复制。

### 效果回路
有时你可能将信号发送到模块外部，通过外部设备进行处理，然后将其带回你的模块进行处理。这种出去/返回的过程被称为效果回路。具有内部电平倾向的多个合成器的技巧在于通常比外部效果设备使用的高得多（模块化效果器通常带有电平匹配电路）。

### 效果处理器
（也称为吉他处理器）一种向直路音频信号中添加各种效果的设备，如混响、合唱、闪延、延迟、过载、放大器模拟等。效果处理器可以以单个效果盒或多效果踏板板（参见“脚式踏板”）的形式存在，添加在吉他和音箱之间的信号路径中。它们也可以以吉他放大器中预设的形式，或 DAW 内部数字插件的形式存在。

### 效果轨道
1) 在电影制作中，指所有音效的混音录制，准备好与对话和音乐混合。2) 在音乐录制中，指一个带有要添加到另一条乐器录制中的效果录制的轨道。

### 效果
2) 通过向声音中添加某些东西来修改各种音频信号。术语 Sound Effects（音效）的缩写（指添加到电影或视频中的除对话、旁白或音乐之外的声音，如门点击声等）。

### 电极麦克风
电容麦克风的一种变体，使用电极代替电容器。（也称为“电极电容麦克风”）。由于它是永久极化的，因此电极麦克风不需要外部电源（而标准的电容麦克风设备需要）。

### 电极式麦克风
(无描述)

### 电磁场
(缩写为 EMF) 由于电流通过导体而产生的磁能场。

### 电磁干扰 (EMI)
“音频专业人士的噩梦。EMI 是一种由附近的电磁活动引起的干扰，这种干扰会被音频电缆和设备拾到，导致音频系统中产生不必要的噪声、嗡嗡声或蜂鸣。音频系统中 EMI 的常见原因可能包括高电流电源线、荧光灯、调光开关、计算机、视频显示器和无线发射器。

## 附录 A：C++20 代码



# 附录 C：C20 代码

- 1419 直接拾取麦克风正前方后方的声音（有效抑制来自侧面的声音）。

- 1421 测验：`Quiz("滤波器", "一种减少或消除通过的声音中的某些频率和谐波的模块。在合成器中，最典型的滤波器类型是低通（允许所有截止频率或拐角频率以下的谐波完整通过，然后降低截止频率以上谐波的电平）、高通（允许所有截止频率以上的谐波完整通过）以及带通（截止频率周围的谐波完整通过，然后减小——距离截止频率越远或低于截止频率减得越越多），且截止频率附近的谐波被减小或完全截止；以上的部分则允许通过。")`

- 1430 测验：`Quiz("法器", "一种被识别为产生‘喷气式飞机起飞’嗖声的信号处理器。面板背后的原理是输入的复制被延迟了非常小的量（比合唱效果长，短于‘梳滤波器’效果），并与原始信号混合。当延迟恒定时，，结果是一个“梳滤波器”，某些谐波在相位重叠混合时被抵消。当延迟随时间变化时，你就会得到嗖声和扫描声。这种效果最初是通过同时播放两台录带机的同一首歌曲，让它们同步启动，然后用手指按住磁带法兰边缘来删除它产生的。")`

- 1439 测验：`Quiz("法圈", "一种通过将信号与其略微延迟的复制混合，并修改延迟的复制而产生的‘旋涡声’的音频效果——这最初是在模拟磁带记录中通过同时播放原始磁带和两台录带机的复制来实现，物理上按下其中一台机器的法兰边缘来更改复制轨道。如今，法圈通过删除盒或数字插件完成。")`

- 1444 测验：`Quiz("平直", "用于描述设备或扬声器频率均匀的术语，意味着该设备/扬声器不需要均衡即可处理所有频率。当图形化显示时，频率显示为没有峰值或波谷的直线。在音乐中，描述一个不准的音符或音高，听起来比实际频率略低（3）。在音乐记法中，一种指示演奏者/歌手将该音符降低半音的‘变音符号’。")`

- 1451 测验：`Quiz("弗莱彻-蒙森曲线", "也称为‘等响曲线’，一组绘制的图形曲线，用于说明人耳在不同音量下不同频率的响应。以首次绘制这些曲线的两个研究人员命名（另见‘等响曲线’）。")`

- 1455 测验：`Quiz("触发器", "二进制逻辑，触发器在每当接收到输入触发时会在高电平和低电平之间切换（即第一次触发设置输出，第二次触发再次设置为低电平，以此此类推）。在时钟音频术语中，它将输入时钟或方波的速度除以2）。")`

- 1459 测验：`Quiz("浮不平衡线", "一种连接‘变通’，通过修改线路中的连接使其类似于平衡线，将不平衡输出连接到平衡输入，从而减轻不需要的嗡嗡声或滋声")`

- 1467 测验：`Quiz("带总线", "通常使用带有沿长度多个连接器的排线来引出电源并将其分配到各个模块中。模块之间的共享。")`

- 1472 测验：`Quiz("低频振荡器", "振荡器的频率被另一个振荡器非常快速的变化（调制）——在音频速率/秒。结果是几个谐波，它们可能与主振荡器的基频非常和谐，也可能非常刺耳（‘不准’）。")`

- 1477 测验：`Quiz("调音器", "表演的现场音频连接并混合的地方）。英国国家称为监听器或楔形音箱（‘折返扬声器’）的扬声器提供音频信号混合，供表演者听到并演奏。这与音频扬声器从反馈中分离到主系统的 FOH（现场）混合完全不同。这种监控经常作为舞台监听音箱的替代方案，以控制噪声并减少反馈风险）。")`

- 1492 测验：`Quiz("VCA", "执行各种功能。")`

- 1493 测验：`Quiz("电阻", "通常以圆形焊盘的形式出现，你按下它来改变参数。它充当电阻，在你按下时减小阻值。")`

- 1497 测验：`Quiz("共峰", "语音轨道——具有某些喜欢振动或‘共振’的频率。风（或其某些谐波）以匹配这些共振频率。这些共振频率中的每一个被称为该乐器的共峰。合成人声的常用方法是将振荡器通过滤波器或均衡器，这是声音或乐器声音中在不同音高下不改变频率的元素。共峰本质上是‘固定’频率，共振是由于声源物理结构产生的结果。这些频率创造了音色，即创造吉他、长笛、男声或女声等特定声音的声音元素）。")`

- 1504 测验：`Quiz("格式", "绑定格式，如黑胶唱片和压缩光盘；绝对格式；数字格式，如。1) 用于存储和播放音频的许多不同介质之一。2) 格式也可以描述轨道数、宽度和间距。3) 格式化是为使用准备硬盘或内存卡。")`

- 1508 测验：`Quiz("四象限乘法器", "声音合成方法，由一个振荡器（载波）产生的频率由一个或多个振荡器（算子）的输出改变，以产生多种谐波丰富的声音。四象限乘法器也称为幅度调制（AM）。调制频率既从载波频率中加上又减去；结果是 60Hz 的正弦波，调制器是 100Hz 的正弦波。")`

- 1512 测验：`Quiz("分数机架", "由 Pia 和 Blacet 提出的一种不常见的模块化合成器格式。分数机架的研究；一个单元为 1.5 英寸（3.8 厘米宽，30 或 5.25 厘米高）。注：此条目在 OCR 中重复出现）`

- 1517 测验：`Quiz("频率响应", "音频系统组件能够充分处理、传输或接收的高低频率之间的范围。")`

- 1519 测验：`Quiz("频率灵活型", "在无线麦克风系统中，频率灵活描述系统在特定带宽内的可选 RF 频率上工作。频率灵活系统优于在无线信号密集的地区（如大城市）巡演，因为设备的 RF 频率可以更改以避免干扰。")`

- 1524 测验：`Quiz("函数发生器", "函数发生器在合成世界中有两种含义。一种是产生波形（如正弦波）的测试实验，或创建上升下降以触发发生器。")`

- 1528 测验：`Quiz("全规范化", "描述跳线批内的配置，插座形成一个连接路径，直到插入补丁，仅当电线插入输入时更改路径。‘非规范化’或‘开放’在那里输出。")`

# 附录 A：C2 代码

- `quiz:Quiz("增益衰", "压缩器或限幅器调节音频信号幅的动作。")`

- `quiz:Quiz("增益结构", "描述音频信号中多个时刻之间相互连接，以及在某点发生的增加量或减少的的术语。良好的结构配置意味着组件正在正常工作，以最小的失真或噪声提供最佳增益。")`

- `quiz:Quiz("增益", "音频信号强度的增加量，通常以 DB 为单位表示。")`

- `quiz:Quiz("门限检测器", "这是模块化合成器中传输的主要类型之一。当有新的输入脉冲启动时，它会跳转到高电平（通常为 5 伏），例如当你按下键盘控制器上的键时，或者序列器跳转到下一个“阶段”或音符时。门限在整个音符期间保持高电平（即按住按键期间），并在音符结束（即释放按键时）突然下降或变为“低”静止水平——通常为 0 伏，或其他数值。在实践中，门限信号被发送到典型的包络生成器，门限的开始（变为高电平时）告诉包络通过其攻击（Attack）和衰减（Decay）阶段；当门限持续时，包络保持在其持续水平，并且")`

- `quiz:Quiz("拷贝损", "录音频编码时音频噪声和失真导致的清晰度损失。")`

- `quiz:Quiz("拷贝", "用于描述音频信号复制次数的术语。")`

- `quiz:Quiz("滑音", "指音符在可见范围内从一个音高变为另一个音高。这种效果的音乐术语是滑音（portamento），即音符之间的揉连。在合成器中，这种效果是通过改变音符的控制电压音高，使其从上一个音符的音高滑动而不是离散跳转来实现。创建这种效果的模块被称为慢生成器、滑生成器、斜率生成器或滞后器。有些人将滑音（glissando）和滑音（portamento）互换使用，但如果你想分割音阶，滑音（gliss）是一种不同的效果，其中中间音符更加清晰，例如快速顺序播放——而不是通过揉连通过。")`

- `quiz:Quiz("黄金分割", "也称为黄金比例）高度与宽度或长度的比例，宽度是高度的 1.6 倍，长度约为高度的 2.6 倍。由古希腊人首次计算，这种在数学上被称为“phi”的比例是许多应用中的最佳比例，包括房间尺寸和工作室设计（以实现房间内的“最佳声学”）以及某些声学乐器的设计。")`

- `quiz:Quiz("颗粒合成", "颗粒合成可以被认为是声音的粒子理论。这个概念是将声音分解为非常小的“颗粒”——通常在 100 毫秒内有 1-50 个，或者通过改变单个颗粒的速度、音高、音、播放顺序和方向来创建新声音。你可以在这些修改过的颗粒之间进行交叉淡出，或在上方叠加更多颗粒。结果范围从音频处理技巧（如在不改变音高的情况下改变速度，反之亦然）到创造幻幻的“云”（事实上，有一个名为 Clouds 的流行模块）。")`

- `quiz:"Quiz("图形均衡器," "一种使用分配给特定频率的滑块来调整输入信号频率的均衡器。（另请参见“均衡器”）。"`

- `quiz:"Quiz("地抬起插头," "一种允许三芯线插入两芯插座的适配器。一些工程师使用它来中断地连接并防止蜂嗡声，但不通过任何方式对设备接地就使用此插头断开地是一种**非常**不安全的做法。）"`

- `quiz:"Quiz("地抬开关," "一种断开一个电路接地与另一个电路接地之间连接的开关，用于消除由地路引起的引起的声或蜂嗡声。")`

- `quiz:"Quiz("地," "一个或多个电子设备连接到同一个地的情况。设备在不同地电位的不同点运行，这会在地线上产生电压，导致低频嗡嗡声，这种声音在最好情况下也是恼人的，并且会损坏设备。地路的最佳解决方法是使用中央电源将所有设备接地在同一点。另一种解决方案是断开回路的地抬开关或插头，但当这被认为是不安全的电力约定同时应应避免。")`

- `quiz:"Quiz("组（或分组）," "控制台上的若干输入通道，在组合信号到主输出之前可以作为一个整体进行控制和调整。有时也称为“子混（Submix）”、“总线（Bus）”或简单的“组（Group）”。")`

- `quiz:"Quiz("延迟," "在音频中，组延迟是一种现象，所有电子音频设备（例如扬声器、放大器）中的信号中不同频率的延迟导致了组延迟，其中某些频率的延迟略高于其他频率。在所有系统中，组延迟是为了保持原始声音尽可能小。创建这种效果的模块被称为一个a。")`

- `quiz:"Quiz("吉他控制器," "一种为吉他声音添加效果的电子设备，如混响、合唱、法兰、过载。这些也可以作为踏板或放大器内的插件被找到。")`

# 附录 A：C++ 代码

- `quiz:Quiz("哈斯效应", "也称为先验效应（Precedence Effect）。简单来说，人类听觉中的一个因素，我们通过时间而不是电平来感知声源。在研究中，赫尔穆特·哈斯（Helmut Haas）确定，到达我们耳朵的第一声波有助于确定声音的位置，除非它比原始声音大至少10dB，或者延迟超过30毫秒（在此时我们将其感知为回声），否则不会影响我们对方向的感知。")`

- `quiz:Quiz("半音", "音高的变化，相当于钢琴上相邻的键。也称为“半音（Semitone）”。")`

- `quiz:Quiz("半归一", "描述跳线板内的连接，当跳线板是“全归一（full-normalized）”时，通过向输入或输出插入线来改变连接；当它是“半归一（half-normalized）”时，只有当线插入输入时路径才会改变。“非归一”或“开放”则没有内部连接，每个输入都通过其输出发送信号。")`

- `quiz:Quiz("半波整流", "半波整流仅通过正电压，并将任何负电压替换。换句话说，任何“零以下”的内容都会被削掉。")`

- `quiz:Quiz("音乐厅程序", "模拟音乐厅的延迟/混响效果设置。音乐厅程序的特征是25毫秒的预延迟。")`

- `quiz:Quiz("硬拐", "在压缩中，指声音电平超过阈值时信号的更剧烈的压缩。另请参见“拐（Knee）”。")`

- `quiz:Quiz("硬同步", "这是最常见的振荡器类型，振荡器每当接收到同步就会重置波形。如果没有指定同步类型，那么它可能是硬同步。")`

- `quiz:Quiz("谐波失真", "设备输出信号中存在的谐波，而这些波在输入信号中不存在，通常是为了改变乐器的音色。")`

- `quiz:Quiz("谐波", "单个谐波是最纯净的声音：除了音高和音量之外，它包含泛音或其他识别特征。它的振动形状——无论是通过空气让我们听，还是通过引起电压上升和下降的电振动——都是正弦波。随着时间的推移，泛音之间具有非常特定的音高关系。第一个或最低的谐波被称为“基音（fundamental）”，是声音的音高，就像和弦的最低音是它的“根”。其他谐波是，a`

## 附录 C：C++ 代码

基础频率的等距整数倍数：其频率的两倍、三次、四倍，依此类推。第一阶泛波恰好具有良好的音乐间距：一个八度；一个八度五度；两个八度。（但频率越高，它们听起来可能越不音乐化）。

- `Quiz("裕量量 (Headroom)","放大器或音频设备中正常工作电平与裁剪电平之间的分贝（db）差异。也描述录制峰值与信号失真点之间的分贝差异。（也称为 Margin）。")`

- `Quiz("赫兹 (Hertz)")`

- `Quiz("高阻 (Hi-Z)","High impedance 的缩写。描述为几千欧姆的阻抗或电阻。在麦克风中，Hi-Z 通常指定为 10,000 欧姆或更多。（参见“阻抗”。）")`

- `Quiz("门 (Gate)","当门信号处于电压水平（通常为 5 伏，尽管也可以）时，表示处于“开启”状态——例如当键盘控制器开始触发音符时——称为门信号为高电平。")`

- `Quiz("阻抗 (Impedance)")`

- `Quiz("高通滤波器 (High Pass Filter)","一种音频滤波器，它可以衰减特定频率（截止频率）以下的信号，并通过频率较高的信号。")`

- `quiz("高端 (High-End)","High 或 Hi-End -“高频”的缩写，泛指 4000 Hz 以上的频率。通常在音频信号的“高、中、低音”语境中使用。")`

- `quiz::Quiz("高通滤波器"),"高通滤波器 (HPF) 设计原封不动地通过截止或拐角频率以上的泛波，并根据截止频率的高低降低低阶泛波的水平。在 12dB/oct（分贝/八度）的高通滤波器中，截止频率低一个八度（换说，频率的一半）的泛波电平降低 12 dB；截止频率低两个八度（频率的三分之一）的泛波降低 24dB，依此类推。高通滤波器通常用于创建明亮的声音，其中高阶泛波比基频和低阶泛波强得多——例如古大琴（harshichord）。")`



# 术语表

## H

### 水平音高 (Horizontal Pitch)
**HP = Horizontal Pitch**。在 Eurorack 合成器模块格式中，模块的宽度定义为 `hp`（水平音高）的数量。每个 `hp` 为 0.2 英寸（0.5 cm）。大多数是 `hp` 的偶数倍宽，有些是奇数。此外，模块的宽度通常略小于 0.2 英寸的精确整数倍，以确保你不会遇到过宽导致重叠的问题。

### 号叭 (Horn)
1. 一种扬声器或扬声器箱，波形通过锥形驱动器发送到一个狭窄开口，然后向外扩散到更大的开口。
2. 铜管乐器中的几种类型之一。

### 同步信号 (House Sync)
用于 SMPTE 类型代码的参考信号（用于保持房间内设备同步）。

### HP
**HP = Horizontal Pitch**。在 Eurorack 合成器模块格式中，模块的宽度定义为 `hp`（水平）单位的数量。每个 `hp` 是 0.2 英寸（0.5 cm）。大多数是 `hp` 的偶数倍宽，尽管有些是奇数。此外，模块的宽度通常略小于 0.2 英寸的精确整数倍，以确保你不会遇到过宽导致重叠的问题。

### HPF (高通滤波器)
高通滤波器 (`HPF`) 设计原封不动地通过其截止或拐角频率以上的泛波，并根据低于截止频率的远程度降低泛波水平。在 12dB/oct（分贝/八度）的高通滤波器中，截止频率低一个八度（换句话说，截止频率的一半）的泛波电平降低 12 dB；截止频率低两个八度（频率的四分之一）的泛波降低 24dB，依此类推。高通滤波器通常用于创建明亮的声音，其中高阶泛波比基频和低阶泛波强得多——例如古钢琴。

### 交流电声 (Hum)
1. 当电源线意外感应或馈入电子设备时产生的低频音高。这种嗡声反映了电流的基频（美国为 60 Hz，许多欧洲国家为 50 Hz）。
2. 在不开口的情况下唱出一个音高。

### 混合电源 (Hybrid Power Supply)
混合电源使用重量较轻、效率更高的开关电源来执行大部分电压降——例如从 12 AC 转换为 DC——然后使用线性电源处理剩余的较小电压降，例如从 15v 到 12v。这些正成为许多模块化合成器的首选设计。电源的缺点是——噪声太大，或没有。

### 超心形 (Hypercardioid)
心形图型的一种变体，其最佳拾音区域的形状更高且更具指向性的心形。超心形麦克风对麦克风正前方最敏感，并根据其物理特性开始拒绝轴外 90-150 度范围内的声音。

### Hz/V
一个输入端变化 1 v 的系统会导致音高的变化。

### Hz
赫兹，是频率的单位（每秒循环）。

## A

### ADSR
**ADSR**（起始、衰减、维持、释放）是一种包络发生器。`ADSR` 包络发生器允许它在初始水平开始——而不是 0 伏。在 Prophet 模块中，它具有这种能力。

### IC (集成电路)
集成电路（缩写为 `IC`）——由许多组件组成的微型电路。在术语中称为芯片。

### Impedance (阻抗)
阻抗是指对流的阻碍。

### In Line (线路)
线路（在混音台上，用于录制和监听功能）。

### In Phase (相位)
相位，是指两个或多个信号处于相同的极性状态，使得波不会相互抵消。

### In Port (在端口)
在端口（进入 DAW）的信号。

### Input (输入)
接收信号的插孔或物理位置。它指的是输入信号本身。

### Insert (插入)
在信号链中（通常在混音台或虚拟 DAW 中），一个设备、信号处理器或插件被“插入”到当前的放大级和通道或总线中。通常用于为组添加混响、压缩或 EQ 处理。

### Instrument Amplifier (乐器放大器)
一种通过放大器输出乐器的设备（乐器放大器）。

### Instrument Direct (乐器直出)
乐器直出（在音频设备中输出乐器）。

### Insulator (绝缘体)
如玻璃、空气、塑料等绝缘体（将不会导电）。

### Integrated Circuit (集成电路)
集成电路（缩写为 `IC`）——由许多组件组成的微型电路。在电子设备中称为“芯片”。

### Integrator (积分器)
积分器，用于平滑输入信号的。

### Inductor (电感器)
一种线圈，当电流通过它时会产生或存储电荷（电压）。通常用于各种音频应用，如吉他拾音器和扬声器。来自前面的波在理论上不会到达背面，防止声波相互抵消。“无限”术语源于将扬声器放置在墙尽头的想法。当然，这在物理上是不可能的，因此无限屏障旨在尽可能模拟这种效果。无限屏障的示例是在房间墙上，或者建造足够大的密封箱体以防止锥体背面的声音。

### Attack/Decay/Sustain/Release
**ADSR**（起始、衰减、维持、释放）包络发生器允许它在初始水平开始——而不是 0 伏。在 Prophet 模块中，它具有这种能力。

### Input/Output (输入/输出)
输入/输出在音频中是指任何涉及传输音频信号或数据的设备或系统。

### Impedance (阻抗)
第一电路对流的阻碍。

### Monitoring (监控)
许多 DAW 的设置允许你监控进入 DAW 的实时信号（作为录制信号）。

### Input (输入)
接收信号的插孔或物理位置。它指的是输入信号本身。

## 附录 A：C++20 代码

电压的变化。“积分器”（`Integrator`）是该数学函数的学术名称；你更有可能看到此模块被称为更精简的限制器（我将在那里详细介绍它的用途），或者较少地被称为延迟生成器或处理器。

测试：“接口（`Interface`）”，任何允许一个单元与另一个单元工作、驱动或通信，或允许人类与计算机或其他电子设备交互的设备或连接点。在专业音频环境中有很多接口示例，包括 `MIDI`（乐器接口）；音频接口将音频输入连接到你的电脑；甚至是你的 `DAW` 程序，它显示了一个允许你分配乐器、调整设置、录音、混合播放的屏幕。调音台也是一种接口，连接了控制室的各个元素。

测试：“互调失真（`IM Distortion`）”，由两个或多个不同频率的音频信号相互作用引起的失真。产生的频率之和与差值（通常是不需要的频率）在任何原始频率中都不存在。

测试：“反平方定律（`Inverse Square Law`）”，描述数量与另一个数量平方之间反比关系的数学规则。用通俗的话说，如果一个数字每次减少一定量，另一个数字也会相应变化。在音频声学中，反平方定律说，在没有建筑物的开放区域，声源距离每增加一倍，声压就会下降一半（6dB）。这个方程对于在户外环境工作的音频工程师非常有用，例如。

测试：“反相器（`Inverter`）”，反相器将输入的控制电压乘以 -1。在门或逻辑反相器的情况下，它反转高低状态（即 0v 变为 5v，5v 变为 0v）。这有时被称为极化器，因为它改变了信号的极性（正与负）。控制反相器通常与偏移电压相结合，将输出电压调整到所需的范围。例如，如果你有一个输出范围为 0 到 +8 伏的包络生成器，而你对其进行了反相，结果将是 0 到 -8 伏。由于控制放大器模块通常只接受正电压，你需要加上 8 伏来使其恢复倒置（反相后的平均值仍为 0 到 +8v）。

测试：“反相混合（`Inverse Mixing`）”，大多数调音器努力让信号在通过调音器时保持相同的极性。然而，某些调音器可能会反转信号的极性或“相位”（因为设计更简单）；其他调音器可能允许你故意反转信号，以便你可以尝试一些技巧（例如添加来自同一振荡器或滤波器的另一个信号的反相波形或滤波器模式）。

测试：“隔离（`Isolation`）”，将声音限制在特定区域内的过程，使其不与其他声音发生作用。例如，声学处理过的隔离间通常用于录音室录制人声或乐器，以防止外部噪音泄露到麦克风中，或者在现场录音期间防止人声或其他声音干扰乐器麦克风。

测试：“IV 线（`IV Cable`）”，你需要将信号发送到多个目的地。实现此点的选项包括使用专用的分线器。

测试：“插座（`Jack`）”，“你将跳线线插入合成器模块的那个孔”）这叫法。插座的大小和类型——3.5mm、香蕉头或 1/4 英——通常是不同同步模块的定义特征之一：3U/Eurack 和 SU/mult。不，插头不叫 Jill。实际上，情况是反的。插头有时被称为公头（`male connector`），插座被称为母头（`female connector`）。

测试：“詹姆斯同步（`James Sync`）”，时钟或同步设备上可用的一种过程，它读取外部时间并重建（或“詹姆斯”）一个与原始外部代码相同的新时间码，用于设备同步。此功能主要用于替换已退化的代码。

测试：“卡普斯强（`Karpus Strong`）”，这是一种物理建模合成设计，用于复制拨动、振动弦的声音——尽管它也被证明对打击乐声也有用。一个短样本——最初是噪声，尽管也可以是高频合唱或其他声音——发送到输出端并进入延迟线。延迟的输出连接到滤波器——最初是一个单极滤波器；改变滤波器对声音的特性有巨大影响，然后回到主输出和延迟线的输入端。静音，连接你自己并尝试结果。

测试：“键（`Key`）”
1. 在音乐中，调中的音阶，或“C 大调”。2 被通过音阶的第一个音（主音）识别，作为通过侧链信号使用外部音频信号进行动态处理的一种控制方式。
2. 解锁设备或软件使用的数字或数据代码。例如：Pro Tools 通过物理 USB 密钥的 `ILK ID` 授权。

测试：“键盘控制器（`Keyboard Controller`）”，一种钢琴风格的键盘，发送 `MIDI` 信号以控制其他 `MIDI` 设备。大多数键盘乐器都配备了 `MIDI` 输入/输出 数据。

测试：“键盘跟踪（`Keyboard Tracking`）”，大多数模块合成器遵循频率与音高之间的严格关系，即每八度 1 伏；任何偏差都会导致调音错误。由于这种敏感性，`1v/oct` 及其类似的信号和连接有时会被专门区分为键盘跟踪，而不仅仅是“CV”（控制电压，以明确它们不会被模块上的功能控制而衰减或修改。）

测试：“吉他（`Keytar`）”，一种背式的、轻量级的便携式键盘，让吉他手获得与脚踏板相同的自由。

测试：“千赫兹（`kHz`）”，`kHz` - 1000 Hz 的缩写，2000 Hz = 2 kHz。常用于描述频率范围。

测试：“膝（`Knee`）”，压缩器上的一个功能，决定一旦音量超过阈值，压缩开始的剧烈或缓慢程度。曲线线上所谓的“弯曲”让人联想到膝部。“硬膝”（`Hard knee`）指的是压缩器的突然启动，而“软膝”（`soft`）指的是渐进的。

测试：“克里补丁（`Krell Patch`）”，基于 1959 年电影《禁地星球》，其中一段他们演奏了古代克里人的音乐。在一般术语中，不是插件、包络和时长。

测试：“延迟生成器（`Lag Generator`）”，此功能平滑输入信号，使其电平变化不超过每秒特定的电压数。这导致结果后于输入的变化。它被称为斜率限制器或技术上称为积分器。

测试：“层叠（`Layering`）”，指在组合到一个通道或分配给一个控制器后，对类似的多个部分或声音进行的任何混合。在音频录制中，层叠通常涉及录制相同的乐器或人声（或带有轻微延迟或合唱效果的复制），以产生比单独人声/乐器更丰富、更饱的声音。在声音设计中，也指混合多个样本（例如两个或多个声音）以创建更丰富的声音。

测试：“LFO”，该模块产生周期性的循环波，频率范围从频谱低端到每周期几秒甚至几分钟不等。它们用于产生诸如颤音（控制信号音量）、颤音（控制信号音高）、重复振荡器等效果。

测试：“限制器（`Limiter`）”，一种剧烈减少（限制）增益的压缩器。

## 附录 A：C++20 代码

音频水平达到特定阈值，通常用于防止过载和信号峰值。当压缩器的压缩比达到 10:1 或更高时，它实际上变成了一个限制器。（另参见“压缩器”）。- 一个用于接收线路电平信号的输入。

quiz: "线路输出 (Line Out)", "任何发送线路电平信号的输出，例如馈给读取器的控制台输出。",

quiz: "调制 (`modulating`) 振荡器，因为当您改变调制器时，结果会保持音准。",

quiz: "线性电源 (Linear Power)", "线性电源设计产生较高的电压，并使用变压器等元件将其降低到较低电压。通常情况下，它们倾向于在输出功率中引入噪声，代价是增加热量和重量（它们的效率并不高）。许多人转向使用结合开关和简单线性电源的爱好电源，以兼顾两者的优点。",

quiz: "线性 VCA (Linear VCA)", "线性电压控制放大器 (`VCA`) 在控制输入和信号电平输出之间使用简单的比率关系 - 例如，输出信号中 50% 的标称控制值对应于，然而，我们耳朵感知的响度必须放大 10 倍才能被感知为响亮。线性 `VCA` 用于缩放控制电压，但可能较少用于音频电路电路。如果您将一个具有指数输出的包络发生器连接到线性 `VCA`，您将得到想要的结果。困吗？当包络发生器或 `VCA` 具有线性和指数响应之间的开关或控制变量时，它是很棒的。线性混音器类似于线性 `VCA`：“如果输入电平控制了足够的输入电压，则输入就是一半。再次，这是为了改变控制电压，而不是为了混合音频信号；在这种情况下，您需要一个具有指数特性的混音器。",

quiz: "线性 VCO (Linear VCO)", "线性电压控制振荡器 (`VCO`) 遵循赫兹 (`v/Hz`) 标准；更常见的是指数伏特/八八度 (`v/oct`) 标准。例外是频率调制 (`FM`)，其中线性控制输入通常用于重建经典风格的 `FM`（因为它不会改变载波振荡器的基本音高）。",

# 附录 C：++20 代码

quiz:Quiz("现场录音 (Live Recording)", "所有音乐家同时演奏且没有叠加录制的录音环节。"),

quiz:Quiz("录音室 (Live Room)", "录音室的大主增益区域，大多数乐器和歌手在此处表演。所以，不仅是因为那里有现场表演的空间，而且因为房间经过了声学处理，以产生悦耳的现场回响。"),

quiz:Quiz("现场 (Live)", "1) 一个描述具有回响和反射声音的“空间”，声波是活跃的或“现场”的。2) 实时发生（与之前录音的相反）。"),

quiz:Quiz("本地开启/关闭 (Local On/Off)", "本地开启/关闭 - 连接合成器或 `MIDI` 控制器内部声音的 `MIDI` 消息。“Local On”在按下按键时触发内部模块；“Local Off”则断开连接。需要“Local Off”是为了防止消息的意外循环，或者当通过另一个控制器录制内部介质时。"),

quiz:Quiz("逻辑函数 (Logic Functions)", "在模块合成器中，控制电压通常是模拟的，而门限和触发信号是二制的：开启或高；低。`T` 相当于数字电路中的逻辑信号。因此，制作了数字逻辑模块。一种常见的逻辑函数是：如果信号 A 或信号 B 任为高电，则输出高门（开启）；否则输出低门（关闭）。另一个是与门 (`AND`)：如果信号 A 和信号 B 同时为高电，则输出高门（开启）；否则输出低门（关闭）。这些是处理来自不同时钟源触发信号的绝佳函数。"),

quiz:Quiz("逻辑 (Logic)", "二进制或布尔逻辑是组合信号（开启或关闭电压）以创建新输出的方法。或门是最常见的。或门 (`OR`) 函数表示如果任何输入端有门限（开启或“高”）信号（即输入 1 或输入 2 或输入 3 等），则输出开启门信号。与门 (`AND`) 函数仅在所有输入都看到“高”信号时才输出开启信号（即输入 1 和输入 2 等都具有门限信号）。在函数名称前加“N”表示“该函数的反转”，非门 (`NOT`) 函数只有当所有输入都不为高时才输出高信号（而不是输入 1 或 2 为高电）。"),

quiz:Quiz("循环 (Looping)", "有时，拥有一个循环或重复其功能是很有用的。例如，一个可以通过循环磁带设置为循环的包络发生器。今天，循环被用于样本以保持采样音符足够长时间，直到触发器被触发，而鼓点循环和其他循环在音乐制作中很常见。2) 波节 (`antinode`) 的另一个术语，指拉伸琴弦或声波中位移瞬间的点。（参见“驻波”）。"),

quiz:Quiz("循环 (Looping)", "一个可以设置为循环的低频振荡器包络发生器：当它攻击到最大值并衰减回零时，它再次开始攻击阶段。通常您使用音符序列进行循环：当它到达序列中的最后一个音符时，如果它能循环回到"),

# 附录 C：+20 代码

quiz("响度 (Loudness)", "一个指人类耳朵感知强度的术语。这个术语似乎自言自懂，但它具有误骗性。我们通常认为响度与音量有关，但这是一种间接关系"),

quiz::("低门限 (Low (gate))", "通常，这是门限或信号处于“关闭”状态（通常为 0 伏）或“开启”（+5 伏）的缩写。"),

quiz("低频振荡器 (Low Frequency Oscillator)", "一种引入低于人类听力范围的电子波形的电路（20 Hz 或以下）。这种低频波形创建一个节奏脉冲，通过音频信号中的参数（如音高或音量）进行调制。`LFO` 经常用于样本、合成器和信号处理器以创建此类颤音、颤音和相位偏移效果。"),

（低阻抗 `Lo-Z`）描述为 500 欧姆或以下。（另参见“阻抗”）。

quiz("低通滤波器 (Low Pass Filter)", "一种衰减高于特定频率（截止频率）的信号并通过低于截止频率的信号的音频滤波器或设备。在 12dB/(分贝/八八度）低通滤波器中，截止频率下方八八度的泛波（换句话说，频率翻倍）减少 12 dB；截止频率上方两个八八度的泛波（频率四倍）减少 24dB，以此此类推。quiz("低通门 (Low Pass Gate)", "根据严格定义，低通门 (`LPG`) 是一种低通滤波器，当其控制电压变为 0 伏时，截止频率进入声波范围，导致输入信号几乎被过滤为沉默。可以通过模块中的一个低通滤波器和一个电压控制放大器来复制，两者都使用相同的控制电压。当输入从高电平下降到 0 伏时，在过程中（高泛波被过滤），输出产生非常自然的声音的方式。这模仿了"),

quiz::("低通滤波器 (low-pass-filter)", "一种衰减高于特定频率（截止频率）的信号并通过低于截止频率的信号的音频滤波器或设备。").

# 附录 A: C++20



# Quiz 术语表

## L

**Quiz("Lows or Low-End")**  
低频的缩写，泛指 250 Hz 以下的低频信号。通常指音频信号中的“高音、中音和低音”。

## M

**Quiz("LPF")**  
**Quiz("LPG")**  
**Quiz("M2")**  
一种用于安装 Eurorack 模块的常用螺纹。当使用沿模块固定的导轨滑动的松散螺母系统时，这种尺寸最常见。

**Quiz("M3")**  
一种用于安装 Eurorack 模块的常用螺纹。当使用已钻孔的安装导轨时，这种尺寸最常见。

**Quiz("Magnetic Tape")**  
一种由涂有磁性材料的塑料带组成的录音带，材料为细磨的氧化铁（铁锈）颗粒。常用于模拟录音。

**Quiz("Magnetism")**  
铁基材料对其他铁基材料的自然吸引力能量。

**Quiz("Marf")**  
稀有的 Buchla 2024 MarF（多功能算术发生器，或是序列器与包络发生器的交叉体，两者在此处都有描述），通常包含 16 或 32 个阶段（有时被称为“段”）和一个用于插值这些阶段的速率控制。这意味着可以创建非常复杂的字母表和其他控制电压变化。后来，Buchla 在 Buchla 400 等乐器中使用 MARF 指多步包络。

**Quiz("Margin")**  
参见“Headroom”。

**Quiz("Masking")**  
听力的一种特征，大声音会导致耳朵无法听见频率相似的较小声音。也指较大的声音对较小声音的遮蔽。

**Quiz("Master")**  
1) 控制台或 DAW 的输出，设置混合信号离开控制台时的电平。也称为“主推子”。  
2) 用于制作复制的原始录音母带。

**Quiz("Mastering")**  
对歌曲或歌曲集进行精细调优和“美化”的最终过程，并在此过程中创建母带带。

**Quiz("Measure")**  
音乐中若干节拍的组合。（参见“Bar”。）

**Quiz("Meg")**  
前缀 Mega- 的俚语缩写，意为 1,000,000。常作为兆赫（1,000,000 Hertz, Hz）或兆字节（1,000,000 bytes）的简写。

**Quiz("Meter")**  
1) 一种测量并显示音频数字元件信号电平的设备。电表通常测量峰值或 RMS 值。（参见“Peak Value”、“RMS Value”。）  
2) 音乐的节奏结构，通常描述一个小节中的节拍数。

**Quiz("Mic / Line Switch")**  
Mic, Mike - microphone 的缩写。

**Quiz("Microphone Input")**  
为麦克风信号设计的控制台或其他设备的输入。

**Quiz("Mic Level")**  
音乐引入的极低音频电压水平。信号在进入控制台之前必须通过放大器增加电平。（参见“Line Level”、“Preamplifier”。）

**Quiz("Mic Pad")**  
麦克风或前放大器上的设置，独立的适配器/连接器，在麦克风信号进入前放大器之前降低其电平以防止过载。

**Quiz("Microphone")**  
一种将声波转换为电信号的换能器。

**Quiz("MIDI Clock")**  
MIDI 传输的时钟信号，用于连接的序列器和音乐设备之间保持同步。不要与 MIDI 时间码 (MTC) 混淆，MIDI 时钟与每分钟拍数 (BPM) 步进绑定。

**Quiz("MIDI Controller")**  
可以指 MIDI 的两个元素，取决于上下文。一个向连接设备发送 MIDI 数据的设备或软件，通过预编程序列或通过音乐家的实时表演来实现。MIDI 设备上用于控制声音和表演特定参数的任何小型控制器。

**Quiz("MIDI Interface")**  
一种将 MIDI 信号转换为计算机数字格式的设备，以便存储和使用 MIDI 信号。

**Quiz("MIDI over Bluetooth")**  
蓝牙低功耗 (BLE) 是大多数移动设备支持的无线连接规范。BLE（也称为蓝牙 SMART）可以为使用非持续传输数据配件（如 MIDI 键盘和控制器）的移动设备延长电池寿命。

## 附录 A：C++20 代码

```cpp
// 此处为示例代码结构，原文重复内容已省略
Bluetooth Low Energy (BLE) 是大多数移动设备支持的无线连接规范。
BLE（也称为蓝牙 SMART）可以为使用非持续传输数据配件（如 MIDI 键盘和控制器）的移动设备延长电池寿命。
```

## 附录

### 中文术语

**Quiz("监听混音器部分")**  
监听部分/监听混音器部分 - 调音台上用于创建工程师丰富的混音的部分，工程师可以通过此听到正在录制的内容，而不会影响输送至多轨道录音机或 DAW 的电平。

**Quiz("监听路径")**  
一条与通道路径分离的信号路径，允许工程师听到正在录制的内容，而不会影响输送至多轨道录音机或 DAW 的信号。（也称为“通道路径”。）

**Quiz("监听")**  
单声道 Mono  
1) 为了检查质量或避免峰值而听音乐。  
2) 录音室内的扬声器（通常是两个中的），用于监听音频信号。这包括控制室内用于听混音的监听音箱，以及录音间或现场室内的耳机，供表演者在表演时听到音轨的混音。

**Quiz("单声")**  
缩写为 Mono  
1) 单源或单通道传输（与立体声相反）。  
2) 一次只播放一个音符的旋律。  
3) 描述乐器或合成器设置只播放一个音高（或一次一个“声音” Voice。（也称为“声音”。）

**Quiz("变幻")**  
在模块化合成器的语境下，变幻指的是一个可以或多程度上改变其输出波形形状的振荡器——因此，随着你的演奏产生声音。这通常是数字振荡器的默认设置，它们在内部从一个到另一个交叉淡入（在某些情况下切换），尽管它有时也应用于可以实时控制波形的振荡器。

**Quiz("Mother-32")**  
Moog 的一款非常流行的半模块合成器。自带外壳，也可以安装在 Eurorack 格式的机箱中。它带有 VCO（锯齿波和方波）、一个 LFO（三角波和方波）、可以作为低通或高通的 Moog 风格阶梯滤波器，以及一个 ADSR 或 AR 包络发生器。它还有一个半模块跳线板，允许合成器声音的内部布线提供备选输出，并在讨论如何使用基础模块化系统时，使其像典型的半模块或“入门级”合成器一样进行连接。我们将在明年春天推出关于 Mother-32 的在线入门课程，并将有一个每周系列介绍如何向这个入门系统添加不同的模块。

**Quiz("动圈麦克风")**  
一种通过磁场过程中的感应线移动将声波转换为电音频信号的麦克风，通常被比作反向工作的扬声器。动态麦克风的灵敏度低于电容麦克风，但对于混响更大的声源或近麦应用非常有效。

**Quiz("MU")**  
指的是与 Moog 合成器标准最相关的模块以及追随他们的人，包括 Synthesizers.Dotcom 和 Moon Modular。你有时会听到这与 Moog Units 互换使用，这也指的是每个 MU 2.125 英寸（5.4 厘米）的标准宽度。鉴于这种标准具有历史性且物理巨大，一些人将“SU”作为一种荣誉桥，称他们激进且酷（它们确实如此）。MOTM 还有一种双声道 50 格式，使用一个带有电源和连接的设备。它已经停产，但今天仍有很多活跃的 MAR form 用户。

**Quiz("多点延迟")**  
延迟的工作原理是将编辑好的音频放入管道的一端，并在它从另一端出来时将其抓取。多点延迟说：“等一下，直到音频快照完全穿过管道。让我们在它是你想要的部分时抓取它。那些之前被抓取的点被称为“采样点” taps——就像在长管道上添加的水龙头一样。

**Quiz("万用表")**  
一种测试电电压、电流和电阻的小设备，用于录音室控制电气系统和排除故障问题。

**Quiz("多功能算术函数发生器")**  
稀有的 Buchla Model 248 MARF（多功能算术函数发生器）是一种位于序列器和包络发生器（两者在本词表中均有描述）之间的类别，它通常包含 16 或 32 个阶段。这意味着可以创建非常复杂的包络和其他控制电压序列。之后，Buchla 使用 MARF 一词来描述使用 Buchla 400 的乐器中的多步包络。

**Quiz("多路")**  
你通常需要分分或复制信号以发送到多个目的地。这在分路器（简称“mult”）中很常见，你输入一个源，然后使用跳线通道去往多个标记。

**Quiz("复用器")**  
复用是一种描述信号路由的技术方法，其中多个信号可能被路由到一个目的地。在合成器模块中，这最终扩展到包括一个输入在多个输出之间切换的可能性。开关器是复用器的一种，因为它在多个输入中进行选择以决定将哪一个发送到输出（反之亦然）。有些模块正是这样做，使用振荡器在其它波形的变体之间切换，以创建复杂的、切割的混合物。

**Quiz("多音")**  
指合成器或模块的音频同时播放几种不同的声音、补丁或“音色” timbres。

**Quiz("多轨道录制")**  
也称为轨道记录或多轨道录制。录音室的心脏，多轨道录制是将一系列声音录制到独立轨道上的过程，每个轨道都有自己的音频通道，并将轨道组合以同时播放。录制可以一次录制一个轨道或乐器（稍后组合），或者在表演者一起演奏时录制到独立轨道。这些信号最初录制在多轨道磁带上，但现在也可以作为数字文件录入数字工作站（DAW）。

**Quiz("多轨道磁带")**  
一种可以与其他同步录制的离散信号的磁带。

**Quiz("MIDI")**  
乐器数字接口 MIDI 的缩写。MIDI 是一种连接一个合成器到另一个的常用语言。它是一种数字语言，可以购买 MIDI/Gate（控制电压和门）转换器来驱动序列器和合成器。最要注意连接的类型：传统的 5 针 DIN 或 USB 连接。

**Quiz("静音开关")**  
调音台或音频设备上的开关关闭输出，或者是 DAW 虚拟控制上的匹配按钮。

**Quiz("静音")**  
有时我们需要静音或断开信号。允许执行此操作的电路被称为静音。

## 附录 A：C++20 代码（续）

- 测验：“降噪” — 从信号、设备或系统中去除噪声的若干种过程之一。
- 测验：“噪声” — 描述音频信号中令人不悦、反感或无意识的音频频率。所有电子设备都会产生某种类型的噪声，可以被描述为在安静或无声段落中产生的嘶嘶声或嗡嗡（也称为“底噪”）。连接不良、无线电接口接地不当等问题也可能导致信号贯穿出现噪声。工程师还可能为了测试目的特意让噪声信号通过系统。
- 测验：“非破坏性编辑” — 录音系统（最常见于数字音频工作站，简称 DAW）中的一种功能，在执行编辑时，原始信号或内容保持完整，允许编辑人员随时恢复到原始版本。（有时也称为“非线性编辑”。）
- 测验：“归一化” — 应用固定量的音频，使最高峰值设置为最高可接受的录音水平。



# 测验术语集

## 核心概念

### 已归一化的
模块化合成器的优势在于，你可以通过系统将信号连接到你喜欢的方式。当你只是尝试连接一个“典型”信号流时，这也可以是一个望远镜数字。因此，某些制造商创建了“半模块化”合成器，它们将所有典型连接都预先布好了线，其重要特性是这些布线可以通过在正确的插槽中插入跳线线来覆盖。这些预布的连接通常被称为“直连”。对于一个通常连接到许多通道之一且差异很明显的内部噪声，如果你将跳线线插入标记为外部输入的插槽，它的“直连”状态就会被打破，并被你的连接所取代。

### 陷波滤波器
这是一种特殊的滤波器模式，可以移除转角或截止频率附近的音频频率或谐波，而不是从整个频谱中将其“切除”。它是带通滤波器的相反，带通滤波器只通过截止频率附近的谐波。陷波滤波器往往对声音产生细微的影响；（调制）截止频率可能会导致声音产生微弱的相位。陷波滤波器通常用于系统中消除问题频率，例如地线干扰、房间共鸣或声音谐波频谱中的另一个峰值。想象一下使用陷波滤波器进行跳线来帮助某种声音，在谐波频谱中留下空间让其他声音以较少的竞争存在，或者创造一种更容易吸引耳朵的声音，因为是某种预期而不是缺失。

## 术语定义

### 陷波
窄的音频频率带。

### 八度
调音高一个八度。

### 离轴
偏离麦克风接收器正前方的虚线（轴线）。以角度测量。

### 偏移时间
在时间上。

### 偏移
术语上，偏移模块通常增加或减去电压。

### 欧姆
用于测量信号或设备中电流流阻力（阻抗）大小的单位。（参见“阻抗”）。

### 全
一个表示“所有”的前缀。

### 运算放大器
简称“Op Amp”，用于大多数音频和电子设备的放大电路。

### 运算跨导电放大器
OTA（运算跨导电放大器）是一种将输入电压转换为输出电流的器件。这是一种流行的放大器设计，因为它较不容易发生失真（或裁剪），具有良好的带宽，并且以“暖”的音色闻名。在这里，你可以在 `VCA`（电压控制放大器）中找到它。电流可以被视为电阻的反面，你在 `OTA` 电路中拥有的是电压电阻器件，使得向滤波器等电路添加电压控制成为可能。通常情况下，当有人告诉他们有一个 `OTA` 滤波器时，通常意味着它具有“暖”的音色……除非它是 `MS-20` 滤波克隆版，那种情况下它会更薄、更尖锐。实际上，`OTA` 更多关于设计的便利性，而不是创造特定的声音。

### 或
最常见的布尔或二进制逻辑函数之一，或如果任何输入端有开启（或“高”电平）信号（即输入 1 或输入 2 或输入 3）。每米磁带纳米数实际上描述了在音频信号或 36 Hz 测试频率下录制的信号。也称为亚八度或亚低音函数。

### 振荡器
在其核心处，振荡意味着以重复的模式往复变化。这种模式重复的快慢被称为频率（如方波）。模块化系统中的主要发生器是在高低电压之间上下波动（振荡）的发生器。这种模式被称为波形（如方波、三角波或正弦波）。这是一种显示 `LFO` 或包络或快速变化电压的设备。示波器用于构建设备的峰值，但现在你可以使用 `USB` 接口将其显示到你的电脑上。

### OTA
一个运算跨导电放大器，是一种将输入电压转换为输出电流的器件。这是一种流行的放大器设计，因为它较不容易发生失真（或裁剪），具有良好的带宽，并且以“暖”的音色闻名。在这里，你可以在 `VCA`（电压控制放大器）中找到它。电流可以被视为电阻的反面，你在 `OTA` 电路中拥有的是电压电阻器件，使得向滤波器等电路添加电压控制成为可能。通常情况下，当有人告诉他们有一个 `OTA` 滤波器时，通常意味着它具有“暖”的音色……除非它是 `MS-20` 滤波克隆版，那种情况下它会更薄、更尖锐。实际上，`OTA` 更多关于设计的便利性，而不是创造特定的声音。

### 异或
最常见的布尔或二进制逻辑函数之一。异或（Exclusive OR）仅在仅一个高电平时输出高电平，但如果两个均为高电平则不输出。最后，异否（XNOR）仅在所有输入均为低电平时输出高电平。

## 附录 A：C++20 代码相关术语

### 衰减器
一种衰减输入信号的设备或电路，通常用于防止沿路径放大声音的放大器过载。（也称为衰减器负载。）

### 触发板
一种表面可以被鼓棒击打的设备；其平移产生输出信号（`MIDI` 命令），导致鼓机或合成器产生持续的或氛围感的声音。

### 全景声
一种合成器补丁，用于在立体声场中创建声音。这是通过控制来自全景左和右位置的信号平衡来实现的，耳朵从左侧和右侧听到声音。这种声空间有时被称为平移。平移发生在控制条上的 360 度平移钮上，它控制音频信号发送到由某些通道产生的每个声器或（环绕声器）的量，对应其他插座的相应连接，同时通过不同的平移来实现。

### 参数
你尝试更改的合成器模块的参数。例如，振荡器的参数通常包括它的音高和脉冲波宽度。一个滤波器（反馈），以及可能的作为不同输出增强或切除之间的混合和其他控制，以及带宽。

### 单滤波器架构
通过单个滤波器 (`VCF`) 和放大器 (`VCA`)。这是早期多音合成器的一种流行选择，这些合成器使用分离器（或类似于滤波器的频率分频器，在“弦乐合成器”和去同步器的情况下），并（被）用于每个音符。可以独立地控制其振荡器的音高，同时仍然经过单个滤波器。这对于大和弦非常有效；但在按住其他音符时弹奏新音符并不总是那么有效，因为所有音符都会一起重新触发。

### 泛音
泛音的另一种说法。构成复杂声音的正弦波之一，有助于定义音色。这个概念是合成器中创建声音的关键部分：在加法合成中，使用多个泛音来创建特定的音调。

### 通带
滤波器将“通过”的信号频率范围，而不是被减小。

### 被动元件
一个不产生或控制电能的组件（与“有源元件”相反）。在音频应用中，通常指一种不包含放大器或其设计部分的设备。例如，有源扬声器是自供电的，被动扬声器需要放大器来产生声音。

### 被动式
意味着没有涉及活动（连接到电源）的电子设备，例如通过电位器控制发送信号，而不是使用放大器和其他电子设备在其周围创建一个混合器电路。被动式很容易，且不会给信号增加噪声。被动电子元件无法从一个信号放大另一个信号（指的是以不可理想的方式），并且不能放大、偏移或反转信号。

### 跳线盘
`Patch Bay` 或 `Patchback`、`Patch Field`、`Patch Panel` - 一个包含一系列插座的面板或组件，具有连接控制台和工作室组件的大部分输入输出的连接，用于组织、管理和调节信号流。

### 跳线线
用于连接模块合成器中不同输入和输出的电缆，携带电控制电压和音频。该术语源于旧电话接线板，操作员必须使用电缆物理地连接两个呼叫者。由于不同的模块格式经常使用不同的连接器标准，你需要确保跳线线末端的连接是你所需的尺寸（`Eurorack` 为 3.5mm，`Moog` 单元为 1/4"，或 `Serge` 或 `Buchla` 控制为香蕉头）。

### 跳线线或跳线线
一种末端带有插头的绝缘电缆，用于路由音频信号。跳线线通常被认为是用于跳线盘（其名称）中制作连接的短线；然而，跳线线方便设备之间几乎任何类型的音频连接，有多种长度，并可以包含多种不同的连接器。

### 跳线区域
一个包含一系列插座的面板或组件，具有连接控制台和工作室组件的大部分输入输出的连接，用于组织、管理和调节信号流。

### 补丁库管理器
一个允许通过 `MIDI` 存储合成器声音补丁的计算机程序。

### 跳线面板
一个包含一系列插座的面板或组件，具有连接控制台和工作室组件的大部分输入输出的连接，用于组织、管理和调节信号流。

### 补丁
指代一系列模块如何互连以创建声音的简写术语，源于跳线线用于：1) 通过使用插入插座的短线在音频系统（如控制台）中路由信号。2) 在合成器上设置程序。

### 路径
信号路径（`Signal Path`）的缩写，电流通过电路或设备的方式。

### PCM
脉冲编码调制 - 将模拟信号转换为数字代码的过程。这是通过定期间隔对模拟信号进行采样，然后转换为二进制数字作为数字制作的。`PCM` 是数字线路中最常见的 `A/D` 转换形式。

### 峰值
也称为峰值电平 - 测量波形在任何时刻最大正值或负值（幅度）的量。在音频中，这在视觉上描绘为波形在零上方或下方的最远点。

### 踏单板
一个带有几个踏板并相互连接的板，以便吉他手可以方便地激活许多不同的效果。

### 相位抵消
相位叠加的反面，是当两个波形反相时发生的能量减少（当波形完全反相（偏移180度）时，理论上会导致信号完全静音）。

### 相位失真合成
相位失真合成在 80 年代被 `Casio` 用于合成器。它与 `FM`（频率调制）有关，具有足够的差异来避免数字合成器的问题。有趣的是，它很好地模拟了滤波器的效果。

### 相位失真
由于信号的相位偏移引起的声音变化。有时在合成器中作为改变波形或泛音的方法。

### 相位锁定
任何通过纠正相位差来同步设备的程序之一。例如，在模拟磁带机中，相位锁定通过感应两台机器播放音调的相位差异并调整速度来消除差异。其波形相位控制一个振荡器使其与另一个同相位。相位锁定环 (`PLL`) 是电子设备时钟功能的参考信号。

### 相位锁定环
相位锁定环本质上是一个尝试匹配频率——更重要的是频率的分数或倍数——另一个信号的振荡器。它最用于创建一个产生 2、4 或 8 倍或更多输入频率频率的输出时钟 - 以驱动特殊电路，如开关电容滤波器。

### 相位调制
有人认为这是频率调制 (`FM`) 的严谨术语，因为导致载波振荡器播放得更快、更慢（快速改变其频率使其更高、更低）的行为等于波形正常行为的位置提前和延迟（相位）。但在创建 `FM` 补丁时不要被术语困住；只需将一个振荡器的输出连接到另一个的音高输入即可。

### 相位反转
电路中将波形偏移 180 度的变化。

### 相位偏移
引入音频信号的延迟，以度为单位。

### 相位移动器
这种效果将信号分为两个副本。其中一个副本通过“全通滤波器”处理，该滤波器不会像低通滤波器那样衰减任何原始泛波，但它确实改变了滤波器的相位，导致泛波相对于原始信号产生不同程度的相位偏移。将这两个副本重新混合，原始声音的泛波分量会相互抵消（参见“相位抵消”），从而产生陷波滤波器效果。相位移动器的每个“阶段”——全通滤波器部分都会产生一个陷波。更多的阶段产生更多的陷波，以及更深的效果。

## 附录 C：C++20 代码相关术语

### 锁相环
`PLL` - 一种通过纠正相位差来帮助同步信号或设备的进程方法。例如，在模拟录带机中，相位锁定通过感应两台机器之间导频信号差异中的相位并调整速度来消除相位差，从而帮助多台机器保持同步。在合成器中，相位锁定控制一个音色发生器，使其与另一个发生器的信号同相位开始。锁相环（`PLL`）是电子设备控制功能中的参考信号。

### 相位
`Phase` 是两个相似波形之间时间差的测量（以度为单位）。波形的一个周期被认为有 360 度，就像圆一样。你沿着圆周（或穿过波形）移动的距离定义为相位。例如，如果你处于一个波形周期的四分之一处，你的相位就是 90 度。

### 相位变化
`Phasing` - 通过改变音频信号的相位移并将其与直接信号混合产生的效果。

### 响度单位
`Phon`，响度的单位，数值上等于 1000 Hz 音调播放时的分贝数。例如，如果一个声音被感知为 1000 Hz 播放的 60db 音调，则它就是 60 ph。

### 声插
`Phon Plug` - 直径 1/4 英寸、长度 1/4 英寸的插头（或匹配插座），用于音频连接。

### 圈插
`Phono Plug` - 大多数立体声系统中常见的音频连接器，中心针脚为一个连接，外壳为第二个连接。

### 物理建模
一种（通常用于合成）方法，通过重构音频乐器的元件 - 例如振动体体或管子，或作为吉他或鼓外壳的共鸣体 -并将声音串联。许多模块执行这种建模来创建声音。

### 拾音模式
麦克风前方或周围采集声音的区域形状。此术语与“极性图”通用，但极性图提供了更多关于麦克风灵敏度的信息。（另见“拾音模式”。）

### 拾音
（待补充内容）

### 压带轮
录带机上的橡胶（或塑料）轮子，将带带夹在压带轮和卷轴之间，由卷轴拉动带带。

### 跳录
将轨道混合并跳录到一个或两条轨道（单声道或立体声）的技术。这可以通过通过控制台播放轨道并录制到独立轨道以实时或模拟方式完成，也可以通过数字工作站以数字方式完成。工程师曾经常使用跳录来释放出额外的轨道用于录音，但在数字工作站中轨道几乎是无限的，这种做法基本上已经过时了。今天，工程师通常通过跳录轨道来创建歌曲的初步或最终混音。

### 粉色噪声
一种与白噪声类似的噪声信号，包含所有音频频率，每个倍频的能量相等，而不是所有频带相等。工程师使用粉色噪声作为调优和校准音频设备的工具。（另见“白噪声”。）噪声是一种随机的无音高音频信号，听起来像嘶嘶声或风声。粉色噪声每个倍频具有相同的能量（水平），因为每个高倍频的频率都是下方一个倍频的两倍，这在更宽的频率范围内读取能量，粉色噪声往往具有更自然的电子声，低音更多而高音更少，特特别是与白噪声相比，白噪声每个赫兹（频率）的能量相等，听起来非常明亮。

### 变音
合成器、键盘或控制器上的机制，可以改变音符的音调使其向上或向下移动少量。

### 频率电压转换
一种检测音频波形频率并将其控制电压的设备，电压反馈入振荡器以产生相同频率的音调。

### 音调转 MIDI 转换器
一种检测音频信号中音调并将其转换为 `MIDI` 信息的设备。（也称为“音频转 `MIDI` 转换器”。）

### 音调
耳朵对混响的感知（音乐的高音或低音调）。在录带传输设备上，微调速度或改变音乐的音调和时间。

### 板式混响
一种通过类似于驱动器的换能器将振动传输到金属板产生人工混响的设备。今天的物理板混响被认为是一种复古的人工混响；现在由插件或混响单元模拟。

### 播放头
一种将磁通量转换为音频信号以播放的设备。

### 播放模式
控制台上的配置，允许播放录在带上或通过 `DAW` 监听混音器的原始信号。

### 播放
通过扬声器重放音乐，以便表演者/音乐家配合摄像机表演。

### 播放列表
查看“带（Take）”。由用户定义的歌曲选择；一种可用功能。

### PLL
锁相环本质上是一个锁定在输入频率倍数的振荡器。

### 插头
常见的音频连接器，通常与插座匹配。

### 极性图
麦克风前方或周围采集声音的区域形状。与“拾音”类似，但极性图提供了更多关于麦克风色散的信息。

### 极性
电流的方向。在逻辑门的情况下，它反转高、低状态。例如，如果你使用一个输出范围为 0 到 +8 的包络发生器并直接插入它，结果将是 0 到 -8v。

### 极化器
反相器将输入电压乘以 -1。在逻辑门的情况下，它反转高、低状态。例如，如果你使用一个输出范围为 0 到 +8 的包络发生器并直接插入它，结果将是 0 到 -8v。



# 附录 A：C++20 代码

释放额外录音轨道的引擎，在轨道几乎无限的数字音频工作站中，这种做法基本上已经过时了。今天，工程师通常通过渲染轨道（`bounce tracks`）来创建歌曲的初步或最终混音。

- `Quiz("防喷罩", "放置在麦克风上或麦克风与歌手之间的设备，用于防止歌手对着麦克风吹气产生的响亮“噗噗”声。")`
- `Quiz("端口 (Port)", "计算机或电子设备中用于传输和接收数字数据的连接，类似于插孔接收和传输音频信号。（等待，用于传输和接收数字数据，类似于插孔接收和传输音频信号。2 扬声箱壳内的开口，与扬声箱内的空气运动产生共鸣，在倒反射式低音单元中增强低频）。")`
- `Quiz("滑音 (Portamento)", "音高从一个音平滑滑动到另一个音的变化。也指允许或引起这种变化的合成器模式或 MIDI 命令。")`
- `Quiz("后期制作 (Post Production)", "指在主要录音完成后，对轨道进行编辑、处理和其他精调的工作。录音中的后期制作包括音频叠加、编辑、混音和母带处理。电影中的后期制作包括广泛的音频和视觉效果。我们在此处提到电影是因为电影制作包含大量的音频工作（例如。")`
- `Quiz("后卷带 (Post Roll)", "运行到录音结束的空白磁带（或 DAW 上的轨道）段。（另见“重录 (Re-Roll)”。)")`
- `Quiz("推子后置 (Post-Fader)")`
- `Quiz("后置 (Post)")`
- `Quiz("电位器 (Pot)", "通常被认为是“旋钮 (knob)”的雅说法，电位器基本上是任何通过改变变化量来控制输入或输出的机制（例如，左右平移、音量控制，或发送到辅助发送器或总线的信号量。电位器可以是旋钮或推子，这意味着调音台上几乎每个不是按钮或开关的控制装置都是电位器。然而，我的工程师通常将推子称为“faders”，将旋钮称为“pots（电位器）”。)")`
- `Quiz("电位器 (Potentiometer)", "缩写为 'Pot'") 通常被认为是“旋钮 (knob)”的雅说法，电位器是任何通过改变变化量来控制输入输出电压的机制（例如，左右平移、音量控制，或发送到辅助或总线的信号量。电位器可以是旋钮或推子，这意味着调音台上几乎每个不是按钮或开关的控制装置都是电位器。)`
- `Quiz("功率放大器 (Power Amplifier)", "缩写为 'Power Amp'") 一种放大电级信号以驱动扬声器或一组扬声器的设备。（另见“线路电平 (Line Level)”。)`
- `Quiz("配电板 (Power Distribution Board", "这个简单的电路板将你的模块化系统的输出并创建多个副本，路由到连接各个各个模块的连接器。")`
- `Quiz("PPQN", "当在模块化系统周围使用时信号（通常是门信号或其他脉冲）来让序列器移动其步骤等时，了解时钟如何脉冲很有帮助。这通常以每四分符的脉冲数表示 PPQ 或 PON。如果循环每四分之一发生一次，则时钟速度为 PPQN；在 DIN Sync（早期 Roland 合成器的一种正式标准，DIN 是 MIDI 代码下的电气连接器类型）的情况下，标准为 24 PPQN。这意味着主脉冲可以定义每个八分音符的三连音符（8 x 3）。")`
- `Quiz("前置/后置开关 (Pre / Post Switch)", "输入模块上的开关，决定发送控制在信号中是在主通道推子之前还是之后")`
- `Quiz("预强调 (Pre Emphasis", "在录音过程中对高频进行增强，以使可听信号处于噪底之上。")`
- `Quiz("前置 (Pre)", "指发送位置或设置，将发送放置在路径内的通道推子之前。发送推子意味着推子不影响发送信号的电平，正如推子前置建议的那样。")`
- `Quiz("预延迟 (Pre-Delay)", "混响单元或插件上的参数，决定了原始干声与回响早期反射之间的时间（延迟）。此功能通常用于模拟房间的声学特性，但也可以用于创建不自然的效果。")`
- `Quiz("预回声 (Pre-Echo", "前向回声") 音频中出现的一种压缩伪真，其中可以听到声音本身（或声音的部分）的“回声”，通常由于某些压缩数字格式中的数据不一致引起。录制最终产品中也会出现类型的预回声，由于磁带上的低电平泄漏产生，在黑胶唱片中由于相位差和变形产生，这是一个完全不想要的问题，需要额外的信号处理来解决——在某些情况下它也可以作为音效（不要与“反向回声”混淆）。)`
- `Quiz("推子前监听 (Pre-Fade Listen (PFL)", "调音台或 DAW 通道上的功能允许在淡出之前听到并通常电表显示信号")`
- `Quiz("前放大器 (Preamplifier Preamp)", "一种低噪声放大器，旨在将低电平信号（例如来自麦克风的信号）提高到正常电平并发送到调音台上")`
- `Quiz("精密加法器 (Precision Adder,", "合成器对频率控制电压的意外变化非常敏感——任何误差都可能导致振荡器跑调。因此，当你在模块化合成器中添加音高控制电压时，你应该使用精密加法器，它可以精确地衰减或放大通过它的声音。")`
- `Quiz("预混音 (Premix)", "1) 通过路由到辅助通道来混合一组轨道的的过程。通过渲染轨道（bouncing）来合并轨道是预混音的形式，不一定是预录的。（另见“渲染 (Bouncing)”。）2) 电影制作中的重要部分，在混合对话、拟音、音效和音乐片段时，可以在与其他部分合并之前进行混合。")`
- `Quiz("频率存在感 (Frequency Presence", "4 kHz 之间的音频频率范围，当被增强时，可以增加存在感，特别是对于人声。")`
- `Quiz("预设 (Preset)", "合成器、信号处理器、插件或电子设备上的出厂编程参数集。")`
- `Quiz("压力麦克风 (Pressure Microphone)", "也称为“压力式麦克风”） - 麦克风的振膜随着入射声波工作，因为它对抗受控空气压力增加了麦克风外壳。这种设计使振膜无论方向如何都对压力敏感，从而具有全指向的拾音模式。（另见“全指向模式 (Omnidirectional Pattern)”。")`
- `Quiz("压力敏感度 (Aftertouch)", "某些键盘乐的一种功能，在按下键之后释放之前施加额外压力，将激活一个由玩家设置的控制命令。")`
- `Quiz("压力区域麦克风（边界麦克风) (Pressure Zone Microphone)", "一种设计放置在平面表面（或边界）上的全指向麦克风，有效地创建了“半全指向拾音模式”，同时消除了反射声引起的相位问题风险。一种流行的边界麦克风是 Crown Audio 的")`
- `Quiz("压力梯度麦克风 (Pressure-Gradient Microphone,也称为“速度麦克风”） 麦克风振膜从前后都暴露，振膜运动由前后之间的差异引起。这创建了双向或“8字形”拾音模式（另见“双向模式 (Bi-Directional Pattern)”。")`
- `Quiz("某些键盘测量你按下键的力度，并将其转换为电压或其他控制信号，如 MIDI，然后可以转换为控制电压），你可以用它表达音符，例如颤音或扩大滤波器。单声道后触测量整个键盘的单一值，无论你按下哪个键；多声道后触实际上测量接触皮肤的面积。")`
- `Quiz("串扰 (Print Through)", "模拟磁带上磁通量到另一层的意外传输。")`
- `Quiz("Pro Tools", "软件对其数字音频工作站 (DAW) 的命名，它在专业录音室中是行业标准。")`
- `Quiz("制作人 (Producer)", "音乐中，制作人是音频录制项目的导演，负责根据预算获得所需的最终产品的人。")`
- `Quiz("制作 (Production)", "I) 制作音乐的集体行动。2) 描述录音质量——录制和混合过程中制作决策的最终结果。")`
- `Quiz("程序更改 (Program Change)", "告诉接收设备更改预设的 MIDI 消息。")`
- `Quiz("可编程 (Programmable)", "允许用户更改参数，特别是计算机设备。")`
- `Quiz("提示 (Prompt)", "显示在计算机屏幕上供用户遵循的指令。")`

# 附录 A：C20 代码

- `quiz: Quiz("协议 (Protocol)", "在信息和技术中，指一组用于以标准格式结构化和传输数据的规则，以便所有相关设备都能正确解释这些数据。")`
- `quiz: Quiz("近场效应 (Proximity Effect)", "麦克风的频率更靠近声源。")`
- `quiz: Quiz("心理声学 (Psychooustics)", "研究人类如何感知和响应声音的科学，不仅考虑物理声波的背景，还考虑了心理和情感因素。这一科学分支有助于音频引擎理解大脑如何解释各种声音和频率。")`
- `quiz: Quiz("转子 (Puck)", "任何由金属、纤维、橡胶等制成的圆形部件，它通过旋转动力源驱动机构。录音室中常见的例子是旋转 Leslie 扬声器中的转子。")`
- `quiz: Quiz("脉冲编码调制 (PCM)", "将模拟波转换为数字代码的过程。这是通过以快速的时间间隔对模拟波的幅度进行采样，并将其转换为二进制数作为原始信号的数字表示来实现的。采样率越高，数字复制效果越好。PCM 是数字音频中最常见的 A/D 转换形式。")`
- `quiz: Quiz("每四分音符脉冲 (Pulse Per Quarter)", "当你发送信号（通常是门或其他电脉冲）通过模块系统以改变序列器的步骤时，最好知道该时钟脉冲的速度有多快。这定义为每个四分音符有多少个脉冲——简称为 PPQ 或 PPQN。如果时钟每四分音符发生一次，则时钟速度为 1 PPN；在 DIN Sync（早期 Roland 设备常用的一种流行的电子连接标准）或 MIDI 时钟的情况下，标准是 24 PPQN。这种主控脉冲可以为每个八分音符提供一个三连音节（8 x 3）。")`
- `quiz: Quiz("脉冲宽度调制 (Pulse Width Modulation)", "大多数输出方波的振荡器还有一个额外的控制电压输入，用于设置‘方波’顶部部分的宽度（显然，使顶部部分变宽会导致底部部分变窄，反之亦然）。通过改变产生脉冲的宽度，我们创建了一种类似多尔比移位器；通过低频振荡器调制脉冲宽度来来回变化，会产生一种唱效果，听起来像失调的振荡器脉冲。其结果被称为脉冲宽度调制。使用控制电压来改变脉冲波宽度的过程本质上是在波和脉冲波之间切换。这具有产生更丰富音色、使声音听起来更厚实、感觉更华丽或赋予数字声音模拟属性的效果。")`
- `quiz: Quiz("脉冲 (Pulse)", "脉冲在模块系统中几种不同的含义。当你改变方波的形状，使一部分比另一部分窄时，它被称为脉冲波（见下文的脉冲宽度调制）。此外，窄门或作为序列器等设备的时钟信号触发的脉冲通常被称为脉冲。1) 基于其主题的稳定节拍，无论是听觉到的还是感知的。2) 一种由合成器通常创建和处理的声波，其波形特征是幅度的剧烈上升和下降（如方波），但其峰值比谷值短，使波形具有脉冲感，也称为‘抽吸波’ (Pumping Wave)”。")`
- `quiz: Quiz("抽吸与呼吸 (Pumping and Breathing)", "在录音室术语中，当压缩器快速处理和释放声音时产生的一种效应，导致信号电平产生可见的变化。“抽吸” (Pumping) 通常指压缩后声音电平的可听增加。“呼吸” (breathing) 指类似的效果，即歌手吸气时信号量增大。抽吸和呼吸是廉价或过度压缩的标志，通常是不需要的，尽管某些工程师和音乐家偶尔使用它来创建特定的效果。")`
- `quiz: Quiz("入/出录制 (In / Punch Out Recording)", "在表演者伴奏/伴唱片段期间，在磁带或 DAW 上激活和/或取消录制功能的过程。这可以作为回到起点的方法。这可以作为回到起点的方法。这可以作为回到起点的方法。这可以作为回到起点的方法。这可以作为回到起点的方法。这可以作为回到起点的方法。（注：OCR 文本重复）")`
- `quiz: Quiz("PWM (脉冲宽度调制 (Pulse Width Modulation))", "大多数输出方波的振荡器还有一个额外的控制电压输入，用于设置‘方波’顶部部分的宽度（显然，使顶部部分变宽会导致底部部分变窄，反之亦然）。通过改变产生脉冲的宽度，我们创建了一种类似多尔比移位器；通过低频振荡器调制脉冲宽度来来回变化，会产生一种唱效果，听起来像失调的振荡器脉冲。其结果被称为脉冲宽度调制。使用控制电压来改变脉冲波宽度的过程本质上是在波和脉冲波之间切换。这具有产生更丰富音色、使声音听起来更厚实、感觉更华丽或赋予数字声音模拟属性的效果。")`
- `quiz: Quiz("Q", "品质因数 (Quality Factor) 的缩写。在滤波器中，共振越高，带宽越窄。")`
- `quiz: Quiz("四声道环绕 (Quadraphonic)", "一种很少使用的四声道声音系统，其中通道被指定为左前、左后、右前、右后。")`
- `quiz: Quiz("正交 (Quadrature)", "你可以将一个完整周期定义为 360 度，类似于圆。沿着这个圆移动四分之一，或者移动到处于周期四分之一的点，是 90°。正弦波和余弦波偏移了 90 度或四分之一周期的相位；这通常被称为正交。")`
- `quiz: Quiz("量化失真 (Quantization Distortion)", "模拟信号与其数字部分转换之间的误差，由于大量模拟值舍入到最近的数字数量引起的。")`
- `quiz: Quiz("量化噪声 (Quantization Noise)", "由量化误差产生的信号噪声。")`
- `quiz: Quiz("量化器 (Quantizer)", "数字音乐中通过将音符移动到时间轴上的精确位置来调整表演的过程，有效地将发生‘舍入’到最近定义的网格点。")`
- `quiz: Quiz("机架耳朵 (Rack Ears)", "可以连接以便安装在设备架中的支架。")`
- `quiz: Quiz("架式 (Rack Mounted)", "描述可以安装在环境中的外挂设备。")`
- `quiz("Rack Rash", "当你将模块安装到机箱时，用于安装模块的螺丝头部会划伤模块面板。")`
- `quiz: Quiz("机架单元 (Rack Unit)", "架式设备遵循一组标准尺寸，包括宽度 19 英寸（48.3 厘米），以及每个机架单元（或 U）高度等于 1.75 英寸（4.4 厘米）。")`

## 附录 C：C++20 代码

Eurack 使用13 cm，Buchla 和 Serge 使用 4U，经典的 Moogs 使用 5U（有时称为 MU，即 Moog Unit）。

`Quiz: Quiz("辐射模式,", "对扬声器覆盖范围的图形化描述。这与麦克风的极性方向相似，不同之处在于极性方向描述声音在麦克风处扩散的区域，而辐射模式描述声音如何从扬声器扩散。")`

`Quiz: Quiz("辐射,", "扬声器覆盖的角度和模式。")`

`Quiz: Quiz("随机访问存储器 (RAM,)", "计算机中与处理器配合执行即时任务的短期内存（与保存和调取项目的硬盘存储内存相反）。在录音室中，计算机的 RAM 越大，一次性处理大量数据的能力就越强（例如，多轨道录音或使用虚拟 MIDI 乐器）。")`

`Quiz: Quiz("随机音符生成器,", "一种以固定速率生成补丁的设备，用于合成器。")`

`Quiz: Quiz("随机,", "模块合成器内部的大部分运动变化都是非常有目的性的：音频速率振荡器或低频振荡器的重复波形；包络生成器的上升、下降和波谷。然而，具有随机游动的电压是非常有用的，可以创造从音高抖动到剧烈变化的音量或滤波的一切。噪声是音频随机信号的一个示例。")`

`Quiz: Quiz("说唱,", "对音乐或打击乐表演进行节奏节拍表演。")`

`Quiz: Quiz("稀疏,", "声波波谷期间空气颗粒密度的降低；在“压缩与稀疏”的语境下，它是压缩的反立面。（参见“压缩”）。")`

`Quiz: Quiz("棘轮,", "这是一种用于序列器的一种技巧，其中序列中的一个阶段可能会被触发多次，而不仅仅是在移动到该阶段时触发一次。例如，结果可能是一个四分音符序列，其中一个或多个阶段会出现连串十六分音符。")`

`Quiz: Quiz("速率,", "这个词有时指低频振荡器或重复函数的速度或频率，即序列器的节拍时。")`

`Quiz: Quiz("负载阻抗,", "输入阻抗，或者为设备设备设计的输入端对流经电流的阻碍。")`

`Quiz: Quiz("RCA 插头,", "也称为唱片插头。立体声系统上常见的音频连接器（中心针为一个连接，外壳为第二个连接）。")`

## 附录 A：C++20 代码

`Quiz: Quiz("只读存储器 (ROM,)", "一种用户无法擦除或重新编程的数据存储类型。今天最常见的音频/视频设置形式是光电存储介质（如 CD、DVD、CD-ROM 和 DVD-ROM）。")`

`Quiz: Quiz("读取,", "从存储设备中检索信息位；在数字音频中，指数字信号的再现。")`

`Quiz: Quiz("Reason,", "来自 Propeller Software 的流行音乐软件。它提供了硬件合成器、采样器、信号处理序列器和混音器的数字等效设备。Reason 作为一个虚拟音乐室工作，或者作为一组可以与其他序列软件播放或使用的虚拟音乐乐器。")`

`Quiz: Quiz("更换电容,", "电容器电子元件——电解和钽电容，通常位于电源部分——最容易随时间老化；电解电容的最大安全寿命为 25 年。因此，一些老设备所有者会进行“更换电容”（替换其旧设备中对年龄敏感的电容）。")`

`Quiz: Quiz("磁头,", "模拟磁带机上的设备，将电流转换为磁能；磁性的变化将音频信号的波形形状转换到磁头上。")`



# 附录 C：C++ 代码

- Quiz: Quiz("录音电平", "机器上的控制按钮，决定录制在磁带上的磁通量，或决定数字录制到声音文件电平的 DAW 控制。")
- Quiz: Quiz("录音监听", "在某些磁带机上，一个开关位置允许电表和磁带机电路的声音输出来监控磁带机的输入信号。")
- Quiz: Quiz("录音就绪", "多轨道磁带录音机的控制状态，当录音机录音功能被激活时，指定的轨道将进行录音。")
- Quiz: Quiz("录音总线", "将调音台通道的混合信号发送到多轨道录音机或 DAW 的总线。（参见“总线”）")
- Quiz: Quiz("录音课程", "在录音室录制音乐的时间段。")
- Quiz: Quiz("整流器", "确保电压仅保持正或负的电路。在电源器中，它用于消除交流电压的负成分，或防止你反向插拔模块电源。作为一个模块，半波整流器只通过正电压并将任何负电压替换为零；全波整流器获取负电压并将其反转为正电压。这实际上双倍了许多波形的频率（例如三角波和正弦波）。")
- Quiz: Quiz("红噪声", "也称为棕噪声，技术上这是一种噪声功率密度（频谱响度）随频率增加每八音阶减少 6 dB 的噪声。它具有重低音，听起来像远处的海浪声。它可以作为缓慢变化的随机控制电压或调制信号，而不是作为音频源。")

- Quiz: Quiz("卷盘", "1) 绕在模拟磁带上的轴和法兰；录音和播放将磁带从一个卷盘释放到另一个。2) 有时也称为“演示带”，一种展示能力的音频或视频汇编。与旨在播放一或多首歌曲的设备不同，演示带是专门用于推广专业能力的演示，而不是产品本身。术语本身源于这种促销材料通过卷带递交的时代。")
- Quiz: Quiz("参考电平", "1) 标准基准音量，用于测量以分贝（db）或高于基准的电平。2) “工作电平”。")
- Quiz: Quiz("参考音", "单频音调（通常为 1000 Hz），用于校准音频设备；设置电平的音调。（参见“测试音”）")
- Quiz: Quiz("反射", "声波在平表面上的反射，与吸收相反。反射对我们感知声音的方式有很大影响；远处的反射声被感知为回声，而混响是由成千上万次反射引起的。（参见“吸收”）")
- Quiz: Quiz("再生", "再生在合成器中有几种不同的含义，指反馈。回声单元可以将其输出的一部分馈回到输出中，导致延迟信号再次重复；这有时被称为再生。也偶尔会在滤波器中听到共鸣，被称为再生。")
- Quiz: Quiz("稳压电源", "一种为电子设备供电的设备，当更多设备开启或线路电压变化时，其输出电压不会波动。稳压电源旨在保护敏感元件免受破坏性电压冲击。")
- Quiz: Quiz("继电器", "一种电磁开关，在应用控制电压时连接或断开两个终端。")
- Quiz: Quiz("释放时间", "在动态信号处理中，当信号越过设计阈值时，输出信号返回原始电平所需的时间。")
- Quiz: Quiz("释放", "这指的是包络的最后一个阶段，通常回落到零伏，导致静音。它通常用于讨论攻击/释放（AR）包络或攻击/衰减/维持/释放（ADSR）包络的语境。")
- Quiz: Quiz("远程", "1) 一种远程控制其他设备功能的设备。2) 现场录制")
- Quiz: Quiz("重置", "模块上的重置输入接受触发或门控信号，告诉模块回到它正在执行的操作的开头。对于在除法中计数的时钟分器（完整定义中会有更多详细说明）。对于触发器，回到攻击阶段的起点。对于门限延迟，回到延迟的计时器。")

# 附录 C：C++20 代码

- quiz: Quiz("剩余磁性", "磁力移除后留在磁性材料中的磁性。剩余磁性随时间推移会在磁带机中积累，部分擦除磁带。")
- quiz: Quiz("剩余噪声", "擦除。")
- quiz: Quiz("电阻", "以欧姆为单位的电阻，对电电流，在电路中用于调节电流流量。")
- quiz: Quiz("共振", "在某些频率下产生更多能量。共振原理是一个关键元素，增加了滤波器截止频率或截止频率周围谐波的增益。听上的效果类似于在一个具有永久回响的房间里播放声音，导致声源停止后声音仍持续。参考，共振一术语通常指滤波器的反馈量。")
- quiz: Quiz("混响时间", "rb 时间是在声源停止点和回响电平下降 60 dB 的峰值之间测量的。")
- quiz: Quiz("房间模式", "在一个房间里，你可以听到原始声音从墙壁反射的倍数，可能导致刺耳的声音。只有极少数模块允许通过电压控制其 s（ErbeVerb 是最多的）；许多仅使用外部回响效果。")
- quiz: Quiz("回声室", "一种模拟房间反射的设备。")
- quiz: Quiz("射频干扰 (RFI)", "ts 和/或系统通过 RF 信号功率。系统中的干扰会产生诚实的嗡嗡声、滋滋声、静电声甚至无线电传输的复制。")
- quiz: Quiz("射频 (RF)", "携带无线无线和电视信号的电磁波。频率高于 100 kHz 的大多数 RF 信号。")
- quiz: Quiz("节奏组", "负责演奏节奏部分而非旋律部分。在当代的打击乐、钢琴/键盘和/或吉他音乐中。")
- quiz: Quiz("缩短音", "确定音高。较短的版本有时作为合成器上的替代控制器出现，例如雅马 CS-80。")
- quiz: Quiz("带式麦克风", "通过设置在磁极之间的薄丝带传输电流。带式麦克风对丝带两侧的声音始终有反应，创建出双向或 8 字形图案。")
- quiz: Quiz("人声行间", "在人声行之间。")
- quiz: Quiz("环形调制", "载波。调制器的频率同时从载波频率中加上和减去；产生的谐波取代了原始的载波和调制器。")
- quiz::Quiz("房间反馈消除", "识别并补偿房间内缺陷的过程，旨在优化该房间内的现场音频（将麦克风增加到反馈点，并使用 EQ 剔除违规频率）。")
- quiz::Quiz("上升时间", "音频波形突然增加到较高幅值的速率。")
- quiz::Quiz("均方根 (RMS)", "e，RMS 电平，以及交流电波形的有效平均值，而非其峰值电平。（参见“均方根”、“峰值表”。)")
- quiz::Quiz("滚衰", "当信号的频率从截止频率移动时信号电平的减少。")
- quiz::Quiz("房间均衡化", "在现场音频中，插入监听系统中的均衡器，其尝试补偿由房间声学引起的频率变化。")
- quiz::Quiz("房间音色", "房间的自然环境，包括回声和背景噪声。")
- quiz::Quiz("房间底噪", "在没有音乐或人说话的房间内发生的背景噪声。在为电影和电视录制音频时，rs 捕捉一段房间底噪，作为整体电平的测量，而非仅仅是去峰去-peaks。（参见“均方根”、“峰值表”。)")
- quiz::Quiz("旋转头", "一个带有两个头的圆形头，其旋转方向相对于运动方向有一个微小角度。")
- quiz::Quiz("隆隆声", "一种低频噪声，通常由驱动中的地板或不平整表面引起。")
- quiz::Quiz("节奏轨道", "制作中的节奏录制。")
- quiz::Quiz("S-tri", "某些系统 - 使用一个 s-tri，它就像开关一样简单。")
- quiz::Quiz("采样保持 (S/H)", "采样保持 (S/H) 有两个输入：一个正在采样的信号，和一个在何时对第一个进行采样的触发。当接收到触发时，第一个输入处的当前电压被采样（测量）并保持（存储），然后在输出处呈现。这个稳定电压保持到接收到新触发为止。采样保持与随机电压关联最多。要做到这一点，每当接收到触发时，就会向主输入馈噪声，该输入处的电压是某个值，然后忠实地发送到输出。")
- quiz: Quiz("SPDIF", "“Sony/Philips Digital Interface”的缩写，一种使用通用连接器发送和接收数字信号的协议。")
- quiz: Quiz("安全备份 (ST)", "在质量已之后捕捉的额外音频备份。")
- quiz: Quiz("Sallen-Key", "Sallen-Key 拓扑创建低通、高通、带通滤波器并具有高 Q 值。这是 Korg 或其他设备使用的设计。")
- quiz: Quiz("采样保持", "采样保持 (S/H) 有两个输入：一个正在采样的信号，和一个在何时对第一个进行采样的触发。当接收到触发时，第一个输入处的当前电压被采样（测量）并保持（存储），然后在输出处呈现。这个稳定电压保持到接收到新触发为止。采样保持与随机电压关联最多。要做到这一点，每当接收到触发时，就会向主输入馈噪声，该输入处的电压是某个值，然后忠实地发送到输出。")
- quiz: Quiz("采样数据标准 (SDS)", "参见 MIDI 采样标准。")
- quiz: Quiz("采样率转换", "将数字音频从一种率转换为另一种率，而不将采样转换为模拟。")
- quiz: Quiz("采样率", "这是数字音频的一个规格：录制或播放单个测量（采样）的速度。音频文件的带宽（对应于可以复制的最高频率），每秒采样的样本数。采样率越高，声音的数字再现越真实，可以复制的高频越高。在数字音频中，质量和分辨率是位率的组合。")
- quiz: Quiz("采样", "在数字录制中，瞬时波形的数值水平。数字音乐通过快速连续的许多样本产生。为了通过数字方式复制和处理声音而录制的短音频段。")
- quiz: Quiz("采样器", "一种录制和播放样本的设备，通常具有编辑、处理和存储样本的功能。")
- quiz: Quiz("饱和", "简单来说，饱和是裁剪的一个术语：一旦输入电压超过了电路能够处理的范围（或低于该范围），它将会被限制在该限制处。然而，饱和通常意味着对这种裁剪限制有更圆润、更有形状的方法，从而产生更愉悦（或至少不烦")

# 附录 A：C++ 代码

- 测试题：“锯齿波”，一种每个周期从零值跳变到峰值，并立即掉回零值的波形。（有时被称为‘R波’）
- 测试题：“锯齿波”，合成器中最常见的波形之一。这种斜坡波包含偶次和奇次谐波，分布在基频（即正在播放的频率）处，并在高频处逐渐减小。结果是浑厚的、“类铜管”音色。
- 测试题：“施密特触发器”，这是一种门限检测器，位于变化的输入并输出“高”（通常为 10 伏甚至 15 伏）信号或“低”（通常为 0）输出。当输入低于一个参考阈值 4 伏时，输出变为低电。当输入回到另一个不同的阈值——例如 1 伏时，输出恢复为低电。
- 测试题：“临时轨道 (Scratch)”，一个描述性术语，意思是‘临时的’。2) 在录音期间进行的临时人声，以帮助音乐家演奏或对齐。稍后会覆盖最终的人声轨道。3) 音乐唱片的动作，在唱片机上来回移动唱片，以重现针头的运动，创造出具有节奏感的声音模式。
- 测试题：“倒带 (Scrubbing)”，在监控时对录制的音频进行来回移动的动作，以定位记录中的某一点。在早期，倒带是通过卷带录机手动转动卷轴完成的，今天则通过在 DAW 中沿波形来回拖动光标来完成。
- 测试题：“助理工程师”，一名助理录音师。
- 测试题：“SEM”，Oberheim SEM（合成器仿真模块）是最早的产品之一。它是一个完整的合成器音色——包含两个振荡器、简单的包络器、VCA 以及一个非常流行的二极状态滤波器设计，带有一个旋钮可以在低通、带阻和高通输出之间交叉，一个独立的带通设置——位于立方体形的外壳中。今天大多数时候，当模块制造商使用 SEM 这个魔术字母时，他们指的是旨在模拟原始 Oberheim 合成器的滤波器。
- 测试题：“半模块化”，半模块化合成器的组件——如振荡器、滤波器和放大器——在前面板后面是预先连线的，制造商认为这是一种典型的逻辑方式。然而，它们也提供了跳线点，可以访问其某些功能（如振荡器的波形输出）以切换到其他模块，或者覆盖这些预先连线。许多初次接触模块化合成器的人会通过购买一个半模块化合成器并用额外模块对其进行扩展来尝试。
- 测试题：“半音 (Semitone)”，也称为半音或软音，这是大多数西方音乐中最小的音高划分——例如 C 音和 C# 音之间的差异。使用等平均律（西方音阶最常见的调音方法），这种音高划分是八八度的 1/12。
- 测试题：“发送电平 (Send Level)”，决定发送到总线的信号的控制。
- 测试题：“灵敏度 (Sensitivity)”，在音频设置中，描述该麦克风相对于标准声平产生的输出，与相同声平下其他麦克风的输出相比。2) 在音乐中，泛指艺术人格。
- 测试题：“序列 (Sequence)”，一组预设的音乐事件（如音高、样本音色），由设备顺序播放。也指编程设备播放这组音乐事件的操作。2) 宽泛地指音乐中的某段序列。
- 测试题：“序列器 (Sequencer)”，你在模块化合成器中常见的序列器类型包含一排旋钮（也称为阶段），每个旋钮可以被设置为输出不同的电压。序列器一次通过一个步骤。这通常被用于创建重复的音乐线条，其中每个音符都有持续时间，这在迷幻（trance）类音乐以及经典的柏林学派风格（70 年代的 Tangerine Dream 和 Klaus Schulze；Red Shift Node）中非常流行。
- 测试题：“顺序切换器 (Sequential Switch)”，该模块有几种不同类型；在最常见的情况下，几个输入被路由到一个输出（尽管它们通常是对称的——一个输入可以在多个输出之间切换）。脉冲或门控输入一次步进一个输入，从而切换哪一个作为输出。更复杂的开关允许你设置阶段数量，划分输入时钟以便以比主时钟慢的速度进行切换，或者可能直接将一系列输入路由到相应的输出（同时带有一个求和输出）。
- 测试题：“串行数据 (Serial Data)”，一种数字数据流，其中单个位通过单个连接一个接一个传输（与并行数据相反），在后者中可以同时发送多个位。录音室的大多数连接传输串行数据——例如
- 测试题：“设置 (Set Up)”
- 测试题：“架式滤波 (Shelf Filtering)”，……中电路的名称
- 测试题：“架式 (Shelf)”，均衡中对频率以上部分的频率响应增益。低频架式对频率以下的部分执行相同的操作。
- 测试题：“屏蔽 (Shield)”，包裹在内部导线周围或用于屏蔽目的的导体。
- 测试题：“屏蔽线 (Shielded Cable)”，在内部周围带有屏蔽层的电缆。
- 测试题：“防震架 (Shock Mount)”，麦克风上的弹性支架，用于承受冲击。
- 测试题：“短路 (Short Circuit)”，两点之间的直接连接不应存在。
- 测试题：“短延迟 (Short Delay)”，20 毫秒以下的的延迟时间。
- 测试题：“最短路径 (Shortest Path)”，通过最少数量路由信号的技术。
- 测试题：“长枪麦克风 (Shotgun Microphone)”，一种具有长线条的麦克风，可以在声学上消除侧面声音，使麦克风更好地捕捉某个方向。长枪麦是超心形指向型。长枪麦克风常用于拍摄现场，通常挂在吊杆上。
- 测试题：“齿音 (Sibilance)”，中心在 7 kHz 附近的声音能量，源自“s”、“sh”或“ch”音。
- 测试题：“侧链 (Sidechain)”
- 测试题：“信号流 (Signal Flow)”，泛义而言，音频从源到系统输出的传输路径。（例如，从人声进入麦克风，通过电缆，进入功率放大器，进入调音台，通过所有插件，最后输出到 DAW。）
- 测试题：“信号波 (Signal Wave)”，泛义而言，音频信号从源到系统输出的路径。（例如，从人声进入麦克风，通过电缆，功率放大器输出进入调音台，通过所有插件，最后输出到 DAW 录音。）
- 测试题：“正弦波 (Sine)”，是最纯净的波形。它只包含基频而不含谐波。结果是它是创建底鼓或其他鼓音的次低音的极佳方法；它也是使用频率调制 (FM)、幅度调制 (AM) 或被称为“apback”的波形技术的良好源波。
- 测试题：“滑动回声 (Slip Echo，也称为 Slapback)”，单个、清晰的回声可以由于高频从非吸收墙的反射而自然产生，也可以通过信号处理单元或插件人工复制。滑动回声是一种类似于你在体育馆内听到的“现场”效果。
- 测试题：“从限制器 (Slave Limiter)”，此功能平滑输入信号，使得电压水平的变化每秒不能超过特定的伏特数。结果是它有时被称为延迟发生器或处理器，或者在技术上称为-

# 附录 A：C++20 代码

- quiz("导轨", "这是一种将模块安装到箱内的常用系统，模块连接到这些通道的导轨，这些通道可以滑动到任何位置——它需要适应你模块的安装孔空间。在 Eurorack 机箱中，导轨通常具有 2.5mm 或 3mm 的孔以及相应的螺纹。")
- quiz("斜率发生器", "斜率发生器产生上升或下降的电压。它本质上是一个门信号发生器和一个在同一个模块中接线更紧密的慢速限制器（上所示）。斜率发生器的常见例子是攻击/衰减（AD）或攻击/释放（AR）包络发生器。然而，由于它可以用于通用的控制电压函数，即使是平滑或三角波振荡器，Buchla 和 Serge 等公司也会生成斜率电压。")
- quiz("斜率", "大多数滤波器都有其调优的截止频率或角频率。它通过该频率减少信号的频谱，距离截止频率越远，频率衰减得越厉害。这种效果的强度被称为斜率。智能波定义为每距离截止频率一个八度增加 6 分贝（dB）。例如，斜率为 24 dB/八度的低通滤波器（LPF）会衰减高于其截止频率的谐波 24 分贝。")
- quiz("智能 FSK 频率键", "智能 FSK - 频率键键（FSK）的更新形式使 MIDI 设备能够与音频带或其他录设备同步。带有 MIDI 歌曲位置指针（SPP）数据的数字信号被编码到空轨道上，用于识别录音中任意点的 MIDI 序列器/设备的精确小节、拍和拍。这使得设备能够在完全正确的位置开始，无论你从哪里开始磁带。（参见‘频率键’）")
- quiz("SMPTE 时间", "简写 SMPTE。由电影电视工程师学会创建的标准计时和同步协议，用于音频用于视频/电影，可用于录音环境中的音频同步。音频专业人士个人将这种时间代码称为‘SMPTE’。")
- quiz("SMPTE", "1) 电影电视工程师学会的缩写。2) ‘SMPTE 时间代码’。")
- quiz("小军鼓", "2) ‘小军鼓（snare drum）’的缩写。横跨小军鼓底部鼓面的金属丝，有助于在击打小军鼓时产生‘啪啪’声。")
- quiz("踩镲片", "‘踏镲（hi-hat）’的一个极少使用的替代术语，留自踩镲被放置在‘脚踝高度’的时代。（参见‘踏镲’）")
- quiz("软拐点", "在压缩中，当声音电平超过阈值时，对信号引入的通用压缩。（参见‘拐点’）")
- quiz("单独开关", "一种用于激活控制台或一个或多个选定通道的单独功能的开关，使其被听到或到达输出，而其他通道则自动静音。2. 在音乐中，歌曲中歌唱者或乐器优于其他乐器的片段。")



# 术语表

- quiz("歌曲位置指针 (SPP)", "一种用于连接 MIDI 设备以定位歌曲中给定点的 MIDI 消息。结合 MIDI 时钟，作为同步设备或告诉连接设备何时开始播放的方法。")

- quiz("声学毯", "厚毯子可以铺在地板上或挂起来，为房间增加吸音，并帮助防止声反射。")

- quiz("音效 (SFX)", "电影/视频背景下添加到音频中的除对话、旁白或音乐之外的其他内容。")

- quiz("音频文件", "可以存储在计算机或数字存储介质（如硬盘）上的数字音频记录。")

- quiz("声音建模", "一种在不直接修改物理设备的情况下重建声音的技术。它是加法合成，使用噪声波组合来创建声音。")

- quiz("声音模块", "一种电子乐器（音调发生器、合成器或采样播放单元），它没有可操作接口，而是对输入的 MIDI 消息做出响应。声音模块通常被创建为流行合成器的‘大脑’，即该产品的廉价版本，可以添加到现有配置中。声音模块也可以作为在计算机上加速的软件版本或插件。")

- quiz("声压级", "科学/技术术语中，声波引起空气压力变化的测量，单位为 dB。我们通过声音的振幅、音量或响度来听到和感知 SPL。")

- quiz("声源", "声音的起源，其振动产生声波。")

- quiz("声波", "(也称为‘声压波’) 由振动引起的波，导致空气压发生微小变化，我们听到声音。")

- quiz("声带", "(1) 广而言之，指随视觉媒体的任何音频，无论是音乐还是对话。2) 在常用术语中指与电视或视频游戏同步的音乐谱。")

- quiz("统一源", "这是原始模板中用于随机控制的 Buchla 255 和 266 模块名称。")

- quiz("等距对", "(也称为‘A/B 技术’) 一种立体技术，将两个心形或全指向性麦克风放置在相距 3-10 英尺的地方（取决于声源的大小），以创建左/右像。")

- quiz("声速", "通常情况下，声波通过介质所需的时间。声音在固体、液体和气体中的传播速度不同，我们通常认为声音在空气中的传播速度。在空气中，声速定义为 340 m/s（在 70 摄氏度下），大气条件下 770 m/s。")

- quiz("剪辑", "历史上，音频或电影片段的连接或缩短行为。")

- quiz("分配器", "定义是指可以将信号分成多个副本的东西，分配器电缆连接到一个输入。")

- quiz("扩散", "几个振荡器可以同时产生音调。对这些音调进行微调会产生悦耳的合唱声。取决于模块，音程、和弦。")

- quiz("弹簧混响", "一种通过在弹簧上产生振动来模拟混响的设备，另一端的传感器将这些振动转换为电信号并与原始音频混合。虽然物理存在，大多数模块使用插件或硬件模拟混响。")

- quiz("方波", "这是由振荡器产生的常见波形；它在高、低电压之间迭代（音频振荡器 +/- 5 或 8 伏）；它具有有趣的谐波：具有强大的基频、奇次谐波：频率的三倍、五倍、等等。其结果是空洞的声音。一种电压与电平相关的波形，在该电平处，立即变为另一个电平，最终回到原始电平以完成波周期。")

- quiz("堆叠电缆", "许多香蕉头风格的电缆制成，每个插头都有一个接口，允许你直接在原始插头顶部插入另一个。这些用于 Buchla 和 Serge 系统。TipTop 使用 3.5mm 插头和接口制造类似的电缆，供 Eurorack 用户称为堆叠线。")

- quiz("舞台监听器", "舞台上的扬声器，让表演者听到自己并听到舞台上其他音乐手的演奏声。")

- quiz("阶段", "2. 在混响效果中，混响时间之后的回声将来自中心舞台。在最常见的情况下，阶段是系列变化中的下一个阶段。在 8 序列中，它产生的每个音符都是有序的。在包络发生器的 ADSR（攻击/衰减/维持/释放）中，每个阶段——例如攻击，包络从 0 伏产生它可以输出的最大电压。你可能还会听到描述 BDD 的阶段数量。")

- quiz("标准工作电平", "正常运行时不应超过的参考电平或平均电平。")

- quiz("驻波", "通常当波在房间内两个反射平行表面之间反射时产生的意外波形，反射波与来自源的初始波发生干涉，其中呈现影响频率的复合波长实际上是房间的长度。这创造了波保持静止的听觉幻觉，频率在房间的某些部分被放大到不需要的水平，而在其他地方几乎消失。驻波最常见于具有平行平面的正方形或矩形房间中（声学设计师试图通过吸收材料或引入其他物品来抵消平行表面以防止这些波）。")

## 附录 A：C++20 代码

- quiz("步进模式（Step Mode）", "序列器或数字音频工作站（DAW）中的一种设置，其中手动输入音符，一次一个音符或一个步骤。")

- quiz("步进序列器（Step Sequencer）", "这通常指一种序列器，你在一个阶段上步进并暂停，通过回车（以及可能可能的持续时间）让该阶段移动到下一个步骤，依此类推。")

- quiz("步（Step）", "通常与阶段（stage）互换使用（见上文），特别是在谈论序列器时。")

- quiz("立体声录音（Stereo Micing）", "放置两个或多个麦克风，使它们的输出组合形成立体声像。")

- quiz("击打（Strike）", "这似乎出现在 Make Noise 模块上，尽管已进入通用领域。某些滤波器和低通门（LGs）使用模拟人声（放置在发光二极管如 LED 旁的光敏电阻，允许将电压转换为电阻以控制参数）可能具有一个击打输入。当你向传感器闪烁 LED 时，电阻不会瞬间改变并保持在那里——相反，在它滑向所需的电阻值的过程中，它会发生变化。当你关闭 LED 时，电阻可能不会瞬间恢复到满值；它可能需要短暂的时间来衰减。这些特性对于创建打击性声音和攻击（attacks）非常有用——允许你在 LED 否则仍然开启的情况下进行再次攻击。为了输出并消除杂质并清理录制会话音频，用于控制和播放之目的。")

- quiz("子组（Subgroup）", "通道上的若干组信息，可以在将组合信号发送到主输出之前作为一个整体进行控制或调整。有时也称为‘子混（Submix）’、『总线（Bus）’或简单的‘组（Group）’。")

- quiz("子主控器（Submaster / Sub Master）", "在混音或录制期间控制几个通道声音电平的推子。")

- quiz("子混（Submix）", "见‘子组’。")

- quiz("次低八度（Suboctave）", "一个创建一个比基础泛波低两个八度的新音色或频率的模块——进入它的声音的‘音高’，以强调低音。（次谐波在术语表的其他地方有讨论。）这种音色通常是方波，尽管某些巧妙的模块可能会创建更像正弦波的或类似于原始波形的波形。")

- quiz("减法合成（Subtractive Synthesis）", "最常用的合成技术：你从一个或多个振荡器输出具有大量谐波的波形开始，并将此混合通过通过滤波器移除某些谐波以创建所需的声音或音色。这种修改后的音色被发送到放大器，通过改变其亮度为音色增加包络。一种老派合成方法，通过产生谐波丰富的波形来设计和创建声音，并在所需处过滤掉不需要的谐波。")

- quiz("和（Sum）", "求和是指将两个（或更多）事物放在一起；结果本身就是它。它用于叠加控制电压的上下文中，即从一个减去另一个。一个等电平且相位相同的双声通道混合的信号。")

- quiz("求和（Summing）", "将两个或多个信号混合成一个混音的过程——。在音频中，每个连续通道都会为总信号增加音量，因此通道必须按顺序混合以防止组合信号过载。")

- quiz("超心形指向图型（Super-Cardioid Pattern）", "一种非常窄的心形麦克风指向图型，轴线敏感度高，轴外敏感度最低约为 150 度。")

- quiz("环绕声（Surround Sound）", "一种录制和播放技术，听者可以从前、后以及两侧听到声音的各个方面——一个全度的音频像，与立体声的左右像相反。环绕声出现在具有多个扬声器的各种格式中。今天环绕声最常用于电影和电视制作。")

- quiz("持续（Sustain）", "这是包络发生器的常见阶段，当音符仍被按住时电压通常被发送到电平。音符被按住的知识通常由门信号（gate）提供，只要音符被按住它就会保持，尽管某些包络发生器可能有一个专门的时间控制来决定持续阶段的持续时间。包络包含持续阶段包括 ADSR（攻击/衰减/持续/释放）和 AR（攻击/释放，通常包含一个持续阶段）。")

- quiz("SVF", "一个状态变量滤波器（SVF）是这种设计的常用设计，这种设计本身倾向于同时允许低通、高通和带通。另一个副作用是它们在高频率（共振）设置下不会发生振荡，尽管某些设计已经想出如何实现这一点。Oberheim SEM（合成器扩展器模块）滤波器是最著名的状态变量设计，它可以像一根蛇形线一样简单。")

- quiz("开关（Switch）", "一种制造和/或中断连接的设备。")

- quiz("合成器（Synthesizer）", "一种使用电气振荡器产生声音的乐器，以模拟乐器的声音或创建乐器无法产生的声音。")

- quiz("系统专用（System Exclusive）", "SysEx – 一种 MIDI 消息，只有特定制造商识别。")

- quiz("转速计（Tach/Tometer）", "在模拟磁带录制中，录音机上的一个设备通过发射脉冲来测量和调节速度，磁带穿过磁头。")

- quiz("带尾在外（Tails Out）", "一种音频磁带卷绕方法，即最后记录选择的末端位于带卷外部。")

- quiz("带（Take）", "在一次磁带开始和停止之间完成的记录，或在带有注释的轨道日志上。这种记录过去/现在在数字磁带录制中完成，但在大多数录音室中，此功能现在通过 DAW 完成。")

- quiz("口吞（Talk Box）", "一种效果装置，使音乐家能够通过放入嘴里的软管调制其乐器的声音。从历史上看，口吞一直用作吉他的效果，但它们也可以用于修改其他。")

- quiz("对讲（Talkback）", "控制室内的麦克风，位于与录制通道的独立电路上，允许工程师通过监控系统与现场乐室或隔音室内的音乐家通信。")

- quiz("磁带延迟（Tape Delay）", "一种通过模拟磁带机操纵时间延迟来创建人工延迟或回声的信号处理技术。这种技术从将信号路由到录音机并将延迟响应混合回信号中开始，然后演变为使用专用机器通过调整距离来调整延迟长度。今天，录音室中的大多数磁带效果都是通过 DAW 中的插件数字模拟。")

- quiz("导带器（Tape Guide）", "任何固定或旋转设备，用于引导磁带穿过磁带机的磁头，或从一个带卷移动到另一个带卷。")

## 附录 C：C++20 代码

- quiz("磁带噪声", "由于制造磁带的磁颗粒在模拟磁带上产生的自然高频噪声。磁带噪声形成了模拟录音中大部分噪声底，可以通过使用由更细磁颗粒制成的磁带来减少（参见“噪声底”）。")

- quiz("磁带环", "一段末端接合在一起的磁带，使录音能够连续播放。")

- quiz("磁带录音均衡", "在机器电子设备中增加信号幅度，并保持高频，以使录制的高频信号保持在磁带噪声之上。")

- quiz("电话滤波器", "一种过滤器，通过滤除 300 Hz 以下和 3500 Hz 以上的频率信号来模拟通过接收器听到的音频。")

- quiz("速度映射", "对序列器或数字音频工作站（DAW）进行编程使其遵循的时间变化。与磁带匹配（tape matching）或拍频（beating）不同，两者都有效地将录音调整到设定的速度，而速度映射是调整项目的速度（特别是 MIDI 器器）以适应录制材料的自然细微差别（参见“拍频”、“节拍匹配”）。")

- quiz("速度", "音乐移动的速率，以每分钟拍数（BPM）衡量。")

- quiz("终端", "1) 两根线之间的连接，包括电缆末端的引脚和设备上的插座。2) 指电脑的键盘和显示器，使用户可以输入信息并访问数据。")

- quiz("测试振荡器", "一种产生各种频率音频波以用于测试的设备。")

- quiz("测试压片", "从第一个母版压制出的少数黑胶唱片副本之一，数量有限并经过目视检查，以在压制更多副本之前检查质量。")

- quiz("测试音", "1) 磁参考电平的磁带录音，用于录制节目。2) 人造生成的音用于校准音频系统。")

- quiz("单薄的声音", "一个模糊的术语，描述缺乏某些频率（尤其是低频）的音频信号。例如，使用均衡器（EQ）过度滤波可能会产生单薄的声音。")

- quiz("螺纹嵌件", "一种常用的通过滑轨或螺母将模块安装到外箱的系统。许多螺母被插入这些通道中，可以通过滑动它们来适应模块的安装间距。某些人不喜欢这种系统，他们用插入通道的金属条代替螺母，金属条已预钻了标准的 Eurorack 安装孔间距。它们可能是为 2.5 或 3 mm 的螺丝钻的；购买带有预安装轨道或外箱时请注意。")

使用多个麦克风时，麦克风之间的距离应至少是每个麦克风与其感应源距离的三倍。使用三一原则（tree-to-one rule）是为了防止音频信号之间的相位问题。

- quiz("三音扬声器", "具有重现低音、中音和高音扬声器系统。")

- quiz("听力阈值", "描述为人们在50%时间内听到的声压。")

- quiz("阈值", "阈值通常是指模块采取动作之前信号需要越过的电压水平。例如，当包络跟踪器（一种产生与音频信号当前水平对应的电压的模块）的输出高于阈值电平时，它的门信号将变为高电，表示音符开始。当包络跟踪器的输出下降到阈值（可能与开启阈值相同或不同）之前，门信号低电，表示声音应结束。动态单元开始对输入信号增益的水平。")

- quiz("过零频率调制", "TZFM 是过零调制（Through-Zero Modulation）的缩写。想象从一个振荡器（调制器）到第二个振荡器（载波）频率电压控制输入的声音距离。当调制器的波形输出高于零时，它对应载波正常的音调控制电压，载波音调升高。当调制器的波形输出低于零时，它从正常的音调控制电压中减去，但结果是什么？从正常中减去调制器")

- quiz("喉部", "")

- quiz("行程", "1) 在扬声器中，它描述振膜可以产生的移动量。在麦克风中，它影响敏感度；在扬声器中，它影响方向性。2) 在扬声器中，“行程”也可能描述距离。在低音扬声器中，它是短行程。3) 制作人或工程师对线路可能的操作，它有长行程。")

- quiz("跳线", "两端都有连接器的电缆，通常穿过墙壁。跳线提供了路由信号的极佳方法。")

- quiz("音色", "这个词经常用于描述你创建的声音的独特特征，从音高或响度。当你更改参数时，音色会改变。例如，小号的音色使它听起来像小号而不是笛子。")

- quiz("时间码", "一种标准的计时信号，用于帮助设备同步，或将音频与视频同步。工作室中常用的时间码是 MIDI 时间码 (MTC) 和 SMPTE 时间。")

- quiz("时间压缩/扩展", "也称为“时间拉伸”（Time Stretching）或“时间偏移”（Time shifting）。在不改变声音的情况下加速或减慢音频录制的过程。")

- quiz("时间常数", "复杂的数学概念，基本上描述了当电压应用于电路并响应的时间延迟。")

- quiz("MiniJack", "这是 Switchcraft 设计的一种特殊插座，被许多用于传输音频信号。它们的直径为 3.5 mm，但与常见的 3.5 mm 插座略有不同。1/8 英插头插入 Mini-Jack 会松动；Mini-Jack 插头可能无法放入。")

- quiz("通鼓", "安装在支架上的小鼓（直径小至10英寸），以及鼓组中的底鼓和大鼓。")

- quiz("音调发生器", "一种产生频繁测试音以对准磁带机或其他测试目的的设备。合成器中的电路产生音频信号以模拟另一种乐器。")

- quiz("音调", "任何单频信号或声音。相对于不同频率处所的能量的声音质量。")

- quiz("吐音法", "用舌头控制低音木管乐器声音的技术。")

- quiz("总谐波失真 (THD)", "衡量放大器输出级与输入级之间谐波频率电平的差异，是以百分比表示的比例。这是一个许多人耳朵难以察觉的精细调整规格，但 THD 越低，放大器/扬声器还原声音就越准确。")

- quiz("触摸敏感", "参见“速度敏感”。")

- quiz("保持", "这是采样保持（Sample & Hold）的一种变体。两者都有入 uts - 门信号，以及电压信号 - 电压输出。当采样并保持器（Sample & Hold）接收到门信号时，它会冻结并输出进入参考输入的参考电压。该电压将保持直到出现新的门高电平信号；低电平信号会被忽略。在跟踪并保持器（Track & Hold）中，当门信号为高平时，参考输入被传递到电压输出（这是“跟踪”阶段）；当门信号变为低电平时，此时的电压输入被冻结并保持电压输出，直到接收到新的门信号。")

- quiz("轨道日志/轨道分配表（Track Log / Track Assignment Sheet）", "轨道日志/轨道分配表 - 一带有多轨道磁带的纸，记录了每个轨道录制了什么乐器。")

- quiz("轨道（Track）", "1) 录制在多轨道磁带某部分的音频，或在 DAW 中创建的数字表示。2) 序列器或 DAW 中的一个控制命令之一，用于通过 MIDI 通道控制一个乐器。3) 参见“乐队轨道（Band Track）”。")



## 测验术语表

- **跟踪**  
  通常指振荡器如何跟随设定的音高控制（CV）。随着电压升高，振荡器“跟踪”它并产生更高的音高。大多数（但并非所有！）合成器遵循每八度 1 伏特的规则，音高输入处上升 1.00 伏特会产生恰好一个八度；如果振荡器出现偏差，则振荡器存在跟踪误差，或跟踪性能不佳。有时你会发现电压控制滤波器有一个针对 CV 输入的“跟踪”开关，在该开关下，滤波器截止频率的音高仅上升为相应低音的 1/3、1/2 或 2/3，听起来太沉闷。有时你会发现电压控制滤波器有一个针对 CV 输入的“跟踪”开关，在该开关下，滤波器截止频率的变化仅为音高输入变化的 1/3、1/2 或 2/3。录制多轨道录音中单个音道的行为。

- **换能器**  
  一种将能量从一种介质转换为另一种介质的设备。换能器广泛存在录音设备中。波形开始时的初始高能峰值，由拨片或锤子击弦的打击动作，或击击鼓引起。

- **晶体管阶梯滤波器**  
  这个术语通常用于描述 Moog 低通滤波器的设计，它仍然被视为低通滤波器声音的金标准。Moog 实际上对这种设计获得过专利（现已过期）；他们的许多竞争对手复制了它，或者为了模仿它这样做。

- **传输控制**  
  1) 磁带机的功能，用于将磁带从供带卷移动到卷带卷。  
  2) 在 DAW 或序列器上找到的控制组，用于跟踪、停止、暂停、快进和回放，模拟磁带传输控制的功能。

- **移调**  
  简单来说，是将音符的音高进行平移，使其升高或降低固定数量的半音或八度。这有时被称为“半音移调”。一种更复杂的变体是“音阶移调”，其中每个音符移动固定数量的音阶步；这与半音移调不同，因为不同音阶之间的半音数量可能不同。将一组音乐音符移动固定间距。这可以通过许多方式处理——例如：1) 用新调性重写整首音乐；2) 改变乐器的调音，使其以比弹奏音符更低或更高的音高（通过电子键盘人为实现，或者通过移调乐器的自然调音），例如；3) 实时移调，在记谱上方或下方固定水平演奏（也称为视唱）。

- **陷阱**  
  1) 设计用于拒绝频率音频信号的滤波器；  
  2) 用声学材料制成的物体，放置在墙内以减少房间内的低频反射（也称为“低音陷阱/bass trap”）；  
  3) 另一个用于鼓组（如“set trap”）。

- **颤音**  
  这是改变音符振幅（响度）的效果。在模块合成器上创建这种效果的方法是将低频振荡器（LFO）连接到放大器的一个控制输入上。颤音与音高颤动不同；后者是音高的抖动而不是下降。一种通过快速重复音符（如小提琴颤音）或通过快速振幅变化产生的波动或“摇晃”的音乐效果。

- **三角波**  
  一种谐波丰富的波形，在图上显示为三角形，这是由于奇谐波的存在和快速衰减的结合。

- **触发信号**  
  触发信号是一个非常短的电脉冲信号，从 0 伏升到 5 或 10 伏的标准水平，持续几毫秒后落回 0 伏。它通常用于“触发”循环声音的播放，启动包发生器。它们也可以用于在连接的合成器模块之间传递时钟信号，告知音符何时开始。触发信号通常有固定持续，也会从 0 伏升到高电压回到零，但保持“高”电平的时间长度取决于发送信号以控制音符开始的操作。

- **截断**  
  1) 通过切掉末尾来缩短音频信号。  
  2) 降低数据分辨率（例如从 24 位到 16 位），除非应用抖动，否则会导致数字失真。

- **调音**  
  调整合成器音高的行为。

- **调音叉**  
  在被击中时以相同频率振动的金属叉子。

- **唱片机**  
  一个用于旋转唱片的设备。

- **高音器**  
  一个还原高频的扬声器。

- **二象限乘器**  
  一种简单的幅度调制（AM）场景，第二个载波改变音频信号的幅度。电压仅在 0 伏到最大正电压之间波动；这是单极电压。某些信号的负向波动会被忽略；在幅度调制（AM）中，作为包发生器的输出（称为二象限乘器）。

- **U**  
  机架设备的标准尺寸包括 19 英寸（48.3 厘米）宽，以及 3U（5.25 英寸）高；4U（7 英寸）用于 Eurorack，以及 Serge；5U（8.75 英寸）用于经典 Moog（有时称为 MU for Moog）。

- **不平衡音频**  
  大多数音频信号通过两条线（一个信号线和一个地线）传输（这种布线通常被称为不平衡音频）。

- **不平衡电缆**  
  具有两个导体（信号线和地线）且两端带有连接器的电缆。不平衡电缆经常受到电磁干扰和噪声的影响。不平衡电缆的示例是吉他/乐器线（TS 线）和 RCA 线。

- **指向性模式**  
  麦克风采集模式比任何其他方向都敏感。电压在正负电压之间波动。这是双极电压。某些包发生器的输出仅在 0 伏到最大正电压之间；这是单极性的。

- **同音**  
  同时以相同音高的多个表演者、乐器或声音。

- **单位增益**  
  输出信号相对于输入信号没有增加或减少的情况（通常描述为 0 db）。

- **通常**  
  在“单位增益”短语中通常这意味着信号从输入到输出处于相同水平。

- **真空管**  
  一种抽真空的玻璃管，允许电流通过。真空管用于放大器、振荡器和模拟设备。

- **重复与淡出**  
  一种结束歌曲录制的方法，其中音乐重复部分且工程师减小音量直到音乐淡出。

- **重复**  
  歌曲或和弦进行的重复部分，通常在歌曲结束时，通常是副歌或副歌的一部分。

- **变速**  
  机器上改变播放速度的控制。

- **变D**  
  ElectroVoice 在其麦克风上的专利技术，位于麦克风体上的孔，每个孔对高频的敏感度降低，它们距离麦克风膜。

- **VCA 自动化**  
  某些调音台中的混合自动化系统，通过使用电压控制放大器来改变高音量或其他功能。

- **VCA 组**  
  多个 VCA 推子接收来自组主滑块的控制电压。高端调音台的一项功能允许工程师通过单个推子控制一组独立信号，使用 VCA 调整 th

## 附录 A：C++20 代码

```cpp
4343 发送到每个通道的电压
```

- `quiz:Quiz("速度消息 (Velocity Message)", "在合成器和键盘控制器中，MIDI 消息用于传输关于击键力度的数据。速度消息可用于传输音量信息，还可以触发多采样乐器补丁上的不同样本。")`

- `quiz:Quiz("速度敏感麦克风 (Velocity Microphone)", "参阅‘压力梯度麦克风’。")`

- `quiz:Quiz("速度敏感（也称为‘触控敏感’）MIDI 乐器（如键盘）的一种功能，它根据击键的力度来翻译 MIDI 速度消息。")`

- `quiz:Quiz("颤音 (Vibrato)", "音高相对于标准音乐音的平滑且重复的上下变化，通常由歌手完成或由弦乐和管乐演奏者表现。")`

- `quiz:Quiz("虚拟乐器（也称为软件乐器） 许多软件基合成器、采样器或声音样本的类型之一，它们由计算机存储和访问，并通过外部 MIDI 控制器执行，而不是在标准的合成器或模块中执行。由于这些乐器的多功能性，越来越多的作曲家和电子音乐人在使用可以存储在硬盘中的虚拟乐器，而不是购买键盘和模块。")`

- `quiz:Quiz("人声室 (Vocal Booth)", "用于隔离录制人声的录音室。这种做法防止其他乐器的声音渗入人声麦克风，并减少人声录音中的自然环境音和混响。")`

- `quiz:Quiz("声码器 (Vocoder)", "一种音频处理设备效果或插件，分析音频信号的特征并利用这些特征影响任何合成信号。主要开发目的是从人类语音产生合成效果，声码器可以创建特征性的机器人声音或‘人类合成器’效果，使其听起来像合成器在说话和唱歌。")`

- `quiz:Quiz("旁白 (Voice Over)", "视频、电影或广告中录制的代替音乐的人声公告或旁白。在合成器中，“声”指的是同时播放的许多声音/音高之一。“单声部”意味着一次只有一个声音，“多声部”意味着可以同时发出多个声音。（也称为‘多变声部’）2）。在合成器（如雅马哈）中，“声”也可能指合成器上可用的特定声音补丁。")`

- `quiz:Quiz("易失内存 (Volatile Memory)", "计算机关闭时，内存数据将丢失。RAM（随机存取存储）是最常见的内存形式。")`

- `quiz:Quiz("电压控制放大器 (VCA)", "一种增益水平受发送它的外部电压影响的放大器。VCA 常用于合成器、信号处理器以及某些调音台的自动化手段。")`

## 附录 A：C++20 代码

- `quiz:Quiz("电压控制振荡器 (VCO)", "频率由电压输入的振荡器。最常见于合成器。")`

- `quiz:Quiz("电压 (Voltage)", "两个物体之间电力或压力（‘电位’）的差异，导致它们之间产生电流。")`

- `quiz:Quiz("响单位 (VU)", "音频感知响度的度量。该单位基本上是根据 VU 表测量的平均电平的分贝水平。（另参阅‘VU 表’）")`

- `quiz:Quiz("音量 (Volume)", "一个常见的非技术术语，指声压（当我们听起来是响度时）或音频电压电平。")`

- `quiz:Quiz("声 (Vox)", "一个拉丁词，意为‘声音’，常用作录音室音轨的缩写。")`

- `quiz:Quiz("VU 表 (VU Meter)", "一种读取设备进输出音频电压电平的表，设计用于匹配耳朵对电平突然变化的响应。")`

- `quiz:Quiz("瓦特 (Watt)", "这是振荡器输出的振动模式——电压的上升和波动。不同的模式产生声音。使用比较器和其他电路。通过它们查看波形是否高于（或低于）阈值。当它这样做时，而不是裁剪掉顶部和底部。")`

- `quiz:Quiz("波形 (Waveform)", "振荡器输出的振动模式——电压的上升和波动。不同的模式产生声音。使用比较器和其他电路。通过它们查看波形是否高于（或低于）波值的视觉表示。")`

- `quiz:Quiz("波长 (Wavelength)", "波的物理长度，以英尺、英寸测量。波的长度；较短的波长频率越高。")`

- `quiz:Quiz("波形器 (Waveshaper)", "显而易见地是指一个改变通过它的波形形状的电路，但其峰值和瞬态。许多波形器的目标是以有趣的方式合并（或向波形添加谐波），产生更多或更亮的声音。")`

- `quiz:Quiz("波形表 (Wavetable)", "每个表称为‘波’，将一组波称为波形表")`

## 附录 A：C++20 代码

- `e:etable`

- `quiz:Quiz("加权 (Weighting)", "用于音频测试的均衡曲线补偿了各种电平下的莱曼森。（另参阅‘莱曼-森曲线’）")`

- `quiz:Quiz("西海岸合成 (West Coast Synthesis)", "所谓的西海岸合成方法通常基于向简单波形添加谐波，而不是过滤它们。这通过使用一对振荡器来实现。你可能会发现两级发生器（通常称为发生器）而不是四级 ADSR，并强调控制电压的操作。一个常见特征是内置低通滤波器的电压控制放大器，创建被称为低通门 (LPG)。西海岸方法还采用非传统的控制器，如触控板，并且在同一个系统中混合东海岸和西海岸的方法。")`

- `quiz:Quiz("湿声 (Wet)", "带有效果（如混响）的声音被称为‘湿声’，没有效果的声音被称为‘干声’。效果或调音台的湿干量设置了原始未处理声音与完全影响声音的比例。全部效果（如混响）添加到信号的参考，相对于干声，后者指的是未处理的声音。优选的声音在湿干信号的混合中。（另参阅‘干声’）")`

- `quiz:Quiz("白噪声 (White Noise)", "噪声是一种没有明显音高的随机信号，例如嘶嘶声、呼吸声或风声或浪声。噪声通常根据不同的‘颜色’描述为白色、粉色、红色或蓝色，它们具有不同的频率。单位频率内的功率相等（例如 1000 赫兹），产生更大的嘶嘶声。噪声信号在所有频率频率内的能量相等。与粉红噪声一样，初学者会将白噪声信号通过音频设备用于调优和校准，或在现场 EQ。（另参阅‘粉红噪声’）")`

- `quiz:Quiz("全音 (Whole Step)", "相当于两个半音的音高变化（或两个钢琴键之间的差异）。")`

- `quiz:Quiz("野生声 (Wild Sound)", "在电影和视频中，独立于画面录制的音频`

## 附录 C：C++20 代码

```cpp
4473 用图片初始化（）。
4476 板载控制器（）。
4478 由风吹入麦克风产生的噪声。通常用于在
4479 户外地点录音（）。
4481 频率偏移到接收机，而不是通过音频线传输。
4484 录音机控制通道增益，录音机会随
4485 时间变化。
4488 lo “XLR 接头”。
4491 两个心形麦克风的头部相对，成 90 度
4492 角，并尽可能靠近（参见“同轴录音”）。
4495 事件（）。
4498 在垂直于磁带传输的方向上（）。
```

```cpp
int main() {
    std::random_device rd;
    std::mt19937 gen(rd());
    std::uniform_int_distribution<int> distria(1, 4);
    std::uniform_int_distribution<int> distrib(0, game.size()-1);
    std::shuffle(std::begin(game), std::end(game), std::default_random_engine());
    std::vector<std::string> answers;
    std::string string;
    uint32_t n;
    uint8_t correct;
}
```

## 附录 A：C++20 代码

```cpp
uint32_t score=0;
uint32_t tqs=0;

for (uint32_t ctr=0;ctr<game.size();++ctr) {
    answers.clear();
    correct=distrib(gen);
    for (uint8_t i=1;i<=4;i++) {
        if (i == correct) {
            answers.push_back(game[ctr].getQ());
            question=game[ctr].getA();
        } else {
            answers.push_back(distrib(gen).getQ());
        }
    }
    std::cout << "\33c\e[3J]";
    if (tqs == 0) {
        std::cout << "QUESTIONS: " << tqs << " / " << game.size() << " SCORE: " << "\n\n";
        std::cout << "Question " << tqs+1 << ": " << question << "\n\n";
        std::cout << "Answer #1" << answers[0] << "\n\n";
        std::cout << "Answer #2" << answers[1] << "\n\n";
        std::cout << "Answer #3" << answers[2] << "\n\n";
        std::cout << "Answer #4" << answers[3] << "\n\n";
        std::cout << "What answer is correct (q=quit)? " << "\n\n";
        cin >> n;
        if (n == 0) {
            break;
        } else if (n == correct) {
            score++;
        }
        tqs++;
        std::cout << "\n " << n << " is the answer you gave. And the correct answer is: " << correct << "\n";
    }
}
std::cout << "\33c\e[3J]";
if (tqs != 0) {
    std::cout << "[QUESTIONS: " << tqs << " / " << game.size() << "] SCORE: " << score << "\n\n";
    std::cout << "[" << (double(score)/double(tqs))*100.0 << "] % correct answers.]\n";
}
}
```

## 附录 A：C++20 代码

```cpp
return 0;
}
```

`quiz2.cpp` - 33868 字节。



```cpp
1 // 编译：clang++ -std=c++20 quiz2.cpp -o quiz2
2 #include <iostream>
3 #include <fstream>
4 #include <vector>
5 #include <algorithm>
6 #include <random>
7
8 namespace quiz
9 {
10    class Quiz
11    {
12        public:
13            Quiz(const std::string &q, const std::string &a):_a=a,_q=q;
14            virtual ~Quiz() {}
15            std::string getQ() {return _q;}
16            std::string getA() {return _a;}
17
18        private:
19            std::string _q;
20            std::string _a;
21    };
22};
```

```cpp
23 std::vector<Quiz> quiz::game{
24 Quiz("0-5v","表示 0 到 5 伏特的范围，常用于模块化合成器中的门、三角波-
25 器以及调制控制。门（Gates）和触发器 -
26 作为新音符启动事件——通常从 0v 到 5v（0v 到 10v 也是
27），），在该范围的中间启动事件。门在保持在 5v（或 10v）时为高电平，
28 回到 0v 时变为低电平。）
29 Quiz("1-6pole","这种数字和缩写格式（dB/octave = 每八度分贝）常用于描述滤波器的频率响应。滤波-
31 通常有一个调谐的截止频率或角频率。它随后减少（滤波）
32 通过该信号的频率频谱，使其亮度在距离截止
33 频率每远一个八度减弱 6 分贝的倍数。
34 6dB/octave 滤波器会导致 6dB 的衰减），这被称为“单极性”（因为滤波器的每个
35 极对通过其的信号产生相对较弱的-
36 影响。低通门（LPGs）通常是- 但不是低-
37 通滤波器，它们通过在其截止频率上方每八度减少 6 分贝的
38 强度来降低高次谐波的强度。）
```

## 附录 A：C++20 代码

```cpp
39 quiz:Quiz("24ppqn","最常见的序列器时钟向前移动一步（每四分之一分音符一个脉冲）。这是模块化系统中传输的核心同步，通过倍频或除频来创建音乐节奏划分
41 1 v/oct","模块化合成器中控制音高最常用的标准。在该系统-
42 合成器下，增加进入 VCO（电压控制-
43 振荡器）的电压，在 0v 到 5v 之间（10v 也是）增加音高
47 quiz:Quiz("1.2 v/oct","在模块化合成器中控制音高最常用的标准。在该系统-
48 合成器下，增加进入 VCO（电压控制-
49 振荡器）的电压，在 0v 到 5v 之间（0v 到 10v 也是
50），在该范围的中间启动事件。门在保持在 5v（或 10v）时为高电平，然后
51 回到 0v 时变为低电平。）
52 quiz:Quiz("1/4","用于吉他的最常见连接尺寸（TS/声道）。")
54 quiz:Quiz("1/8","通常用于 Eurack 的连接尺寸。3.5mm 的插头（如 TS-
55 3.5mm 的插头）。3.5mm 的插头（如 3.5mm 的插头 3.5mm 的插头 3.5mm 的插头。）
61 quiz:Quiz("10 vpp","一种峰峰值的缩写。在模块化合成器中，0v 到 5v 之间（0v 到 10v 也是
62），在该范围的中间启动事件。截止频率每八度减弱 63 分贝的倍数。
68 quiz:Quiz("12 db/octave","这种数字和缩写格式（dB/octave = 每八度分贝）常用于描述滤波器的频率响应。滤波-
69 通常有一个调谐的截止频率或角频率。它随后减少（滤波）
70 通过该信号的频率频谱，使其亮度在距离截止
71 频率每远一个八度减弱 6 分贝的倍数。
72 滤波器被称为“单极性”（因为滤波器的每个
73 极对通过其的信号产生相对较弱的-
74 影响。低通门（LPGs）通常是- 但不是低-
75 通滤波器，通过在其截止频率上方每八度减少 6 分贝的
76 强度来降低高次谐波的强度。）
77 quiz:Quiz("16","有时出现在振荡器的音阶选择器上。它指的是风管的长度。较长的风管 = 较低的音高；16 在中
78 范围内。风管或设置为 (8) 再高一个八度；风管再次设置为 (4) 再高两个八度，等。）
81 quiz:Quiz("18 db/oct","这种数字和缩写格式（dB/octave = 每八度分贝）常
```

## 附录 C：C++20 代码

频率。它通常作为缩写（当人们想要提到 TB-303 的类型低音线条而不提及乐器名称时）。

Quiz("3.5 mm", "Euroack 格式模块合成器中插孔和电缆使用的标准连接器尺寸。注意这比 1/8"略大。")

Quiz("303", "Roland 制制的 TB-303 Bass Line 因其磁性的、银色的合成器低音音色，在 Acid House 和其他风格的 EDM（电子舞曲）中备受喜爱。许多人将 303 的声音归功于它的滤波器设计")

Quiz("32", "有时出现在振荡器的八度选择器开关上。它指的是风琴管的长度。风管越长，音调越低；32 是你将看到的最低设置，已经进入了地震级范围。长度为一半的管设置（16'）则高一个八度；再长一倍的管（8）则高两个八度；以此类推")

Quiz("3U", "指高度为 3 个单位（U）的模块——Euroack 标准，这是目前最常见的模块化格式，尽管它是最年轻的格式之一")

Quiz("4 Pole", "这种数字和缩写格式（db/oct = 每八度分贝）通常用于描述滤波器的频率响应。滤波器有一个被调优的截止频率或角频率。它会衰减（过滤通过滤波器的信号的频谱，使其其响度每距离截止设计越远一个八度，就乘以 24 分贝的幂次），这种衰减设计常用于复古 Moog 系统。4 极滤波器与 2 极滤波器相比，通常在主观上认为更肥满、更“圆润”——但这种概括是危险的")

Quiz("4-", "Eurorack 模块偶尔使用的螺丝纹尺寸。Pittsburgh Modular 使用这种尺寸来制作外壳，例如")

Quiz("4U", "指高度为 4U（机架单元）的模块——即 Buchla 和 Serge 系统，以及这些模块的 DIY 仿制品。Buchla 和 Serge 都导向了更具实验性的合成和音乐方法，一些用户将“4U”视为一种不随大流且酷的荣誉标志。（它们确实如此）")

Quiz("4", "有时出现在振荡器的八度选择器开关上。它指的是风琴管的长度。管越长，音调越高；4 是你在所有振荡器上看到的最高八度设置。长度长一倍的管（8）则低一个八度；长两倍的管（16'）则低两个八度，以此类推")

Quiz("5U", "指高度为 5U（机架单元）或 8.75（22.2 cm）的模块，这通常与复古 Moog 标准以及那些追随其脚步、使用 Synthesizers.com 和 Moog Modular 的人相关联。你有时会听到他们与 Mu for Modules 交替使用，后者也指每个 MU 2.125"（5.4 cm）的标准化宽度。鉴于这种支架既有历史意义又物理尺寸巨大，一些人将“5U”作为他们传统且酷的荣誉标志。（确实也有）。此外还有来自 MOTM 的一个短暂的 5U 格式，使用了不同的宽度和电源连接。它后来已停产，但今天仍有忠实的 MOTM 格式用户）。")

Quiz("6 dB/oct", "这种数字和缩写格式（db/oct = 每八度分贝）通常用于描述滤波器的频率行为。滤波器通常有一个被调优的截止频率或角频率。它随后衰减（过滤通过它的信号的频谱，使其响度每距离截止频率越远一个八度，就乘以 6 分贝。6dB/oct 滤波器通常被称为“单极”滤波器（因为对通过它的信号的每个效果都有影响。低通滤波器（LGP）通常——但不总是在其截止频率之上的每个八度衰减分贝，")

Quiz("sound,", "风琴管的长度。管越短音调越高；通常与中 C 相关联。长度为一半的管或设置（4）则高一个八度；管或设置到（16）则低一个八度。")

Quiz("ed-808.", "它将镲和钲的数字声音与 808 声音相结合，中 C。它通常被用作调音参考。")

Quiz("d or omnidirectional microphones are placed somewhere between 3-10 feet apart from each other（取决于声源的声音）以创建左右立体声像。也作为空间间距空气（Spaced Air）。")

Quiz("quantity", "将连续变化的量（如电信号）转换为近似这些变化的数字（即计算机数据）。")

Quiz("final signal", "最终信号（通过麦克风）和再的的信号（通过扬声器）。当施加在麦克风的正压力转换为施加在扬声器的正压力时，两者处于“绝对相位”。")

Quiz("as", "声能量在反射后被吸收。（参见“反射”"))")

Quiz("AC Coupled", "交流耦合输入尝试移除任何通过它的直流电压老化。如果你有一个交流信号（例如振荡器的输出，其本质上是交流的），并且你想移除任何可能渗入其中的直流偏置，这将很有用。这种耦合可能会导致组件在开始和结束处削波。")

Quiz("AC", "交流电 - 音频线中的电流类型。通常，AC 指的是在正值和负值之间交替变化的电压")

Quiz("Additive Synthesis", "使其具有独性的主要属性之一是泛波的混合——构建它的纯组件。加法合成是一种允许对每个泛波直接控制的技术，允许你直接调配混合以重建另一种声音，特别是每个泛波的厚度随模块变化；加法振荡器在现代模块中相对稀少")

Quiz("ADSR", "用于四个阶段的包络发生器：攻击、衰减、维持、释放。当这个包络发生器接收到门输入时，它通常从 0 伏开始（连接到电压控制放大器时相当于静音，连接到电压控制振荡器时相当于最低频率），并通过攻击控制上升到它可以输出的最大水平（通常为 5 到 10 伏，取决于系统；通常可以使用输出电平进行设置）。一旦达到，输出会以衰减控制的速度立即下降，或者如果门信号仍然激活，则保持维持，直到门信号回到 0 伏（通常是你松开控制键盘上的按键，等）。此时，电压开始按照释放控制定义的速率降回 0 伏）。")

Quiz("AES", "音频工程协会）。")

Quiz("AES", "有时被称为 AES/BU) 一种由音频工程协会和欧洲广播联盟开发的数字音频标准，用于在设备之间传输双通道数字音频数据。AES 是使用 XLR 线缆的协议，以及 RCA 和 S/PDIF 线缆)")

Quiz("AFG", "AFG（音频频率发生器）是 Livewire Electronics 发布的一款全功能模拟振荡器。它后来已停产，但经常会有 B 级库存出售，但据我所知，扩展模块从未发布（至少没有在范围内发布）。")

## 附录 C：C++20 代码

quiz: Quiz("触后 (Aftertouch","也称为“压力敏感度”。某些键盘会测量你按下按键的力度，并将其转换为电压（或 MIDI 的其他控制信号，可以转换为控制电压），用于表达压力，例如添加颤音或更宽地打开滤波器。单声道触后（Monophonic aftertouch）测量整个键盘的值，无论你按了哪个键；多声道触后（polyphonic aftertouch）则为每个单独的键产生信号。一个重要的冷知识：触摸踏板实际上测量的是接触它们的皮肤表面积，而不是压力或力——因此你可以通过在指尖和手指长度之间滚动来增加或减少触后。")

Quiz: Quiz("AMHDSR",","攻击、保持、衰减、维持和释放。这是一种略有不同的 ADSR 包络，它在攻击（上升沿且在衰减开始之前）之后将电压保持在其最大值一段指定时间。")

Quiz("混叠 (Aliasing)",","当采样器中的输入信号频率超过该单元的奈奎斯特频率时，会发生一种数字信号失真。采样器以错误的频率（或“混叠”）重现它，导致声音产生伪影。如果你播放一个数字音频文件，其中一半采样是可听的音高，你还将听到声音谐波内容在半采样率枢点处重启的镜像内容（除非进行了某些过滤。参见“奈奎斯特频率”）。")

Quiz("交流电或 AC",","在直接电方向和音频录音室中通过音频线传输的电流类型。在交流电中，电流“交替”，在电路中往回流动。")

Quiz: Quiz("AM","幅度调制（AM）是指使用称为调制器的第二个信号（通常是音频信号，在 0 伏上下波动）来改变称为载波的信号幅度或响度的技术。在典型的幅度调制（AM）场景中，具有正电压的低频振荡器（例如，0 到 5v 之间，通过在 1v 和 2v 之间进行一些较小的变化）馈入电压控制放大器的输入，为通过的音频信号添加颤音。从技术上讲，这是一个象限乘法器或调制器，因为调制信号中的任何负向波动都会被忽略；在连接颤音（tremolo）时，你需要确保为 LFO 添加了偏置电压，以确保声音在 LFO 波形的低端行程处不会中断。")

Quiz: Quiz("环境 (Ambient)",","在这种情况下，它指的是一个地方（如餐厅）的“氛围”。很多情况下，它指的是来自周围环境的声音部分，而不是直接来自声源。例如，从天花板播放或从后墙反射进入耳朵声波就是环境音。")

Quiz: Quiz("环境场 (Ambient Field)",","远离声源且混响响大于直声的区域。")

Quiz: Quiz("环境录音 (Ambient Miking)",","利用房间空间来录制录中的混响。录音引擎通常会在对乐器直接拾音的同时这样做，以在录音中创建直声和混响的混合。"),

quiz: Quiz("Amp","根据上下文，它是 Amplifier（放大器）、Amplitude（幅度）和 Ampere（培）的缩写。")

quiz: Quiz("Ampere","电流的单位，缩写为 Amp。")

quiz: Quiz("Amplifier","放大器，一种增加电信号电平或幅度的设备，使产生的声音更大。")

quiz: Quiz("Amplifier Modulation","幅度调制（AM）是指使用称为调制器的第二个信号（通常是音频信号，在 0 伏上下切换）来改变作为载波的信号幅度或响度的技术。在典型的幅度调制（AM）场景中，一个具有正电压的低频振荡器（在 0 到 5 之间）可能会遇到类似 1v 和 2v 的值，并馈入电压控制幅的控制，为通过它的音频信号添加颤音。从技术上讲，这被称为双象限乘法器或调制器，因为调制信号中的任何负向波动都会被忽略；在连接颤音（tremolo）时，你可能需要为 LFO 添加一个偏置电压，以确保声音在 LFO 波形的低端行程处不会中断。")

quiz: Quiz("幅度 (Amplitude)","波形在零线以上或以下的高度。在音频中，这通常转化为信号强度或电压的音量。")

quiz: Quiz("模拟录音 (Analog Recording)","对音频波连续变化的录制。音乐制作中最常见的模拟录音示例是在卷带机上录音。")

quiz: Quiz("模拟移位寄存器 (Analog Shift Register)","模拟移位寄存器（ASR）是采样保持（Sample & Hold）和桶形延迟（Bucket Brigade Delay）之间的交叉体（假设你已经知道它们是如何工作的）。在初始触发时，它触发输入电压并将其作为第一个输出。在第二次触发时，输入电压再次采样，并使用第一个输出产生的新电压进行采样，同时原始电压被移动到第二个输出。这种“传声筒”游戏按照 ASR 拥有的阶段传递（传统上为三个或四个阶段）。")

quiz: Quiz("模拟数字转换器 (A/D, 或 ADC),","一种将不断变化的信号（模拟）转换为近似这些变化的数值值（数字）的设备。在音频录制中，这指的是将声音从关键值转换为计算机数据。")

quiz: Quiz("模拟 (Analog)","该术意味着信号是连续可变的，与信号转换为离散数字的情况相比。在模块化合成器领域，模拟指的是没有数字（或至少没有基于计算机的）组件的电路设计——相反，它使用晶体管、二极管和电容器完成所有的处理。")

quiz: Quiz("AND 门函数","最常见的逻辑函数之一，AND 门输出仅当两个输入均为高时为高。NAND 门是反 AND。")

quiz: Quiz("OR 门函数","当至少一个输入为高时输出高（逻辑门）。NOR 门是反 OR。")

quiz: Quiz("XOR 门函数","仅当输入不同时输出高。")

quiz: Quiz("AR","攻击/释放（Attack/Release）包络的缩写。这种简单的包络从 0 伏上升到其最大值（通常为 5、8 或 10 伏），速度由攻击参数定义，然后按照释放参数定义的速率立即返回 0 伏。这种变体是")

quiz: Quiz("琶音器 (Arpeggiator)","一种“破碎和弦”类型，按顺序播放而不是一次性播放所有音。琶音器（通常内置键盘或声音模块中，让你更容易演奏琶音：来往复、随机等）。良好的琶音器有不同的模式（保持键）。")

quiz: Quiz("ASR","是采样保持和桶形延迟之间的交叉体（假设你已经知道它们是如何工作的）。在初始触发时，它触发输入电压并将其作为第一个输出。在第二次触发时，输入电压再次采样，并使用第一个输出产生的新电压进行采样，同时原始电压被移动到第二个输出。这种“传声筒”游戏按照 ASR 拥有的阶段传递（传统上为三个或四个阶段）。")

quiz: Quiz("攻击/衰减/维持/释放","具有四个阶段的包络发生器：攻击、衰减、维持和释放。当此包络发生器接收门输入时，它从 0 伏开始（连接电压放大器时的信号电平，或连接电压控制时的最低频率，通常为 5 到 10 伏下降系统）；然后通过攻击控制设置的速率设置输出控制。一旦达到该电平，输出电压立即开始按照衰减控制下降，直到输入门保持有效，它达到维持控制设置的电压。如果输入门仍然有效（通常是你松开了控制键盘的键等）。此时，输出电压落回")

quiz: Quiz("攻击/衰减","攻击/衰减阶段包络的缩写。这种简单的包络从 0 伏上升到其最大值（通常为 5、8 或 10 伏），速度由攻击参数定义，然后按照衰减参数定义的速率立即返回 0 伏。这种变体是")



# 附录 A：C20 代码

指定的时间（与 AR 包络不同，AR 在门控信号为高电平期间一直保持在最大值），然后衰减回零。我这里有一些包络是 AHD 和 AR 的混合体，它们会在定义的保持时间（Hold time）内或在信号保持高电平期间保持最大水平。

`quiz:Quiz("Attack/Hold/Decay/Release","这是一种稍微复杂的 ADSR 包络，它在攻击上升之后、衰减开始下降之前，通常将电压保持在其最大值处持续指定的时间。")`

`quiz:Quiz("Attack/Release","两阶段的攻击/释放以其攻击参数的速率从 0 伏上升到最大值（通常为 5 伏，甚至可能是 10 伏），只要包络发生器中的门控信号保持高电平，它就会在该数值。当门控信号回到零时，包络输出也以其释放参数设置的速率回到零。）`

（有另一种类型的包络称为 AHD - 攻击/保持/衰减，其中你指定一个门控保持在最大值的固定时间，而不是关注门控信号。）

`quiz:Quiz("Attack","这通常指音符开始时的包络特性，它从 0 伏（如果控制放大器模块则为静音）上升到典型的响度值。打击乐和拨弦乐的攻击非常快；长管乐器或弦乐乐句可能有很长的攻击。）`

`quiz:Quiz("Attenuator","电气或声学信号强度的降低。衰减以分贝（dB）测量，通常听为声音减小。声波在空气中传播时会自然衰减。工程师在录音室内通过增益控制或衰减器故意衰减防止过载。）`

`quiz:Quiz("Attenuver","衰减器的特殊版本，可以反转通过它的信号或电压的极性。大多数衰减器在中心位置使用正常信号；当你顺时针旋转时，你增加了信号的标准版本；当你逆时针旋转时，它们增加了信号的反相版本。一些衰减器是增加了极性开关的普通衰减器。）`

`quiz:Quiz("Audio Frequency Generator","AFG（音频频率发生器）是 Livewire Electronics 的一款功能非常齐全模拟振荡器。它已经停产，现在偶尔会有翻新的 B8 模块单元出售。据我们所知，扩展模块已经发布（至少没有广泛发布）。")`

`quiz:Quiz("Audio","在广义上，音频是指我们人类用耳朵听到的频率范围。在技术意义上，音频指的是声音的传输、录制或复制，以数字、电子或声学方式”）`

# 附录 A：C20 代码

469 `quiz: Quiz("Automatic Dialogue Replacement (ADR)","在电影拍摄后，在受控环境中重新录制对话的过程，用于替换录制不好的对话。）`

`quiz: Quiz("Automatic Gain Control","一种具有长释放时间的压缩器，用于保持音频音量在一致的水平。")`

`quiz:Quiz("Automation","编程在编码和/或播放期间自动发生某些变化。在录音室内，工程师在调音台或计算机上使用自动化，以便各种参数在多轨道录制和播放期间的不同时间自动更改。这种预编程使得创建变化比尝试在实时手动执行它们要容易得多。）`

`quiz: Quiz("Auxiliary Return","与混音台协同工作的外部信号处理设备，用于修改信号。）`

`quiz: Quiz("Auxiliary Return","缩写为 Aux Return 或 Return。调音台或 DAW 上的输入，通过辅助发送（auxiliary send）发送的效果返回到通道混音。）`

`quiz: Quiz("Auxiliary Send","缩写为 Aux Send 或 Send。用于调整从调音台或 DAW 输入通道发送到辅助发送或来自辅助总线插件的信号电平的控制。这通常用于创建效果循环，处理信号的一部分并将其返回到辅助返回。）`

`quiz: Quiz("Axis","设备运行围绕的虚拟轴线。例如：在麦克风开启时，轴线是从麦克风前方的一条虚拟线，划定了麦克风拾取声音的位置。发生在麦克风“轴外”的声音将无法被清晰地拾。）`

`quiz: Quiz("Background Noise","指 1) 与所录制的乐器或人声无关的房间环境噪声；2) 与录制信号相关的系统噪声。（所有电子设备都有某种程度的噪声。）`

`quiz: Quiz("Balance","混音中两个或多个乐器的相对水平，或者立体声录音通道中音频信号的相对水平。2) 调整立体声录音通道中音频信号的相对水平。）`

`quiz: Quiz("Balanced","指的是一个使用三根线的系统：一根是地，第二根传输信号，第三根传输信号的反相版本。平衡系统比非平衡系统更不容易受到干扰。如果你需要平衡输出（或输入），你需要一根平衡电缆来进行电平匹配。）`

# 附录 A：C20 代码

299),

`quiz:Quiz("Balanced Cable","由三根线组成的电缆（两根信号线一根地线）。两根信号线携带相同的信号，提供对干扰和噪声的保护。平衡电线的示例包括尖-环-套 (TRS) 和 XLR 电缆。）`

`quiz:Quiz("Balanced Mixer","产生两个输入之和与差的电路或设备”）`

`quiz:Quiz("Balanced Modulator","平衡调制或环形调制是一种特殊的幅度调制，其中一个双极信号（在 0 伏以上和以下之间摆动）被用来改变双极信号的幅度；调制器的频率同时加上并减去载波频率；产生的谐波取代了原始载波和调制器。）`

`quiz:Quiz("Banana","另一种类型的连接器（https://en.wikipedia.org/wiki/Banana_connector），被许多系统使用，如 Buchla（控制电压）和 Serge（音频）。这些连接器只有一根线，因此它们在模块面板和机路上携带信号以提供地参考。香蕉连接器的优势是它们通常是“可堆叠的”，你可以将一个插头插入另一个，提供被动多路。）`

`quiz:Quiz("Band Stop Filter","一种抑制信号中窄频带的设备、电路或插件，允许带外的频率通过。带通滤波器的反面。）`

`quiz:Quiz("Band Track","有时称为减轨道和/或人声的混音。换句话说，包含歌曲所有乐器部分的混音轨道。）`

`quiz:Quiz("Band","频率范围，通常由该范围的中心频率识别。一组音乐家演奏。）`

`quiz:Quiz("Bandpass Filter","带通滤波器（BPF）允许中心或截止频率附近的谐波通过，并衰减中心频率以上和以下的。距离中心越远，衰减越严重，取决于滤波器极的数量，每偏中心一个八度。）`

`quiz:Quiz("Bandwidth","在信号处理中，带宽是指通信通道的可用范围，通过设备最高和最低可用频率之差来测量。）`

`quiz:Quiz("Bank","合成器内存中声音音色、序列器数据和/或生成器和调制器参数的集合。2) 不作为一个单元使用的声音组。）`

## 附录 C：C++20 代码

- `quiz::Quiz("Bar", "在音乐记法中，bar（小节）是measure 的另一种说法；指包含特定数量拍子的时期，并在乐谱两侧用小节线标记。")`

- `quiz::Quiz("Bark Scale", "人体解剖（听觉）系统可以被视为一系列带通滤波器。有趣的是，这些滤波器的间距并不严格遵循线性比例或对数比例。Bark Scale（贝克标）试图确定这些“听觉滤波器”（称为临界带）的中心频率和带宽。")`

- `quiz::Quiz("Barrier Mixing", "一种将麦克风放置在反射面附近的放置技术。如果操作正确，屏障混合可以确保直声和反射声同时到达麦克风，防止两者之间的相位抵消。")`

- `quiz::Quiz("Basic Session", "首次录制基础轨道的音频记录，这些轨道作为歌曲的基础（例如鼓组和贝斯）。")`

- `quiz::Quiz("Bass Reflex", "一种扬声器箱体设计，通过箱体内的端口（开口处）来增强低频。其原理是箱体内部背面产生的低压通过端口排出，并与来自正面低音单元的声音混合。改变尺寸和位置通常会改变低频的特性。")`

- `quiz::Quiz("Bass", "频率最高约为 250 Hz 的音频低频范围。")`

- `quiz::Quiz("BBD", "一种早期的回声或延迟效果设计，输入音频会在短时间内被采样为模拟电压。然后在电路中高于采样率时钟的下一个保持（桶/bucket）上，会使用一个新的电平。桶队延迟（BBDs）通常具有若干个为 256、512、1024、2048 幂的级数或桶；延迟由级数数量乘以采样之间的时间间隔决定。")`

- `quiz::Quiz("Beaming", "扬声器中发现的一种现象，高频会射出扬声器，而不是与低频一起扩散。当你站在扬声器轴线上时，听起来似乎只在播放高频，而不是中频或低频。这种现象可以通过通过扬声器内的喇叭调节高频来缓解。")`

- `quiz::Quiz("Bass Mapping", "调整录制音乐中的速度变化以设置项目速度的过程。在 DAW 中，这是使用时间工具和切割将瞬态同步到适当标记处完成的。这种技术经常用于，例如协调在没有节节拍器（click track）的情况下录制的鼓点或贝斯表演。")`

- `quiz::Quiz("Beat", "1) 音乐中稳定、均匀的脉冲。2) 两个频率略有不同的声音相互干扰，导致音量周期性增加和减少，耳朵听到的现象称为“拍”。")`

## 附录 C：C++20 代码

- `quiz::Quiz("Beating", "当两个振荡器被调到非常接近但并不完全相同的频率时，它们之间的差异会导致被称为“拍频”的干涉图案。当频率差低于音频速率时，这听起来像是组合声音响度的颤音（tremolo）。")`

- `quiz::Quiz("Beatmatching", "一种由 DJ 开发的技术，用于同步两条录制轨道的速度，通常通过使用时间拉伸和音调偏移工具，以创建从一首歌到另一首歌的无缝过渡。")`

- `quiz::Quiz("Beats Per Minute (B.P.M.)", "BPM（每分钟拍数）是表示速度最常见的方式：每分钟应该数几几拍（通常是四分音符）。每分钟 120 拍的速度意味着每秒两拍（120 拍/分钟 x 60 秒 = 2）。音乐中一分钟内稳定均匀脉冲的数量定义了歌曲的速度。")`

- `quiz::Quiz("Berlin School", "一种由 Tangerine Dream 和 Klaus Schulze 等乐团推广的电子音乐风格，基于模拟合成器，强调重复的序列以及在歌曲中播放的浮动和弦或无人音（drones）。更多版本的柏林学派音乐可以在 Note 和 Red Shift 中听到。")`

- `quiz::Quiz("Bi-amplification", "一种由两个放大器驱动扬声器系统中的频和低频的技术。")`

- `quiz::Quiz("Directional Pattern", "一种麦克风拾音模式，最能捕捉麦克风正前方和后方的声音，有效拒绝来自侧面的声音。也称为“字形图案”（figure-pattern）。")`

- `quiz::Quiz("Binary", "数字系统的基石是二进制计数法，每个数字只有两个不同的值：0；关或开；低或高；信号只能有这两个状态之一。因此，模块合成器中的门或触发器——如果是由模拟电路生成的——可以被称为二进制信号。参见“Binary”条目以了解使用二进制门和分频时钟可以做的事。")`

- `quiz::Quiz("Bipolar", "既高于零也可以低于零的电压被称为双极性（bipolar）。模块合成器内部的一些调制信号——例如颤音（LFO）是双极性的。")`

- `quiz::Quiz("Bit", "代表 0 或 1 的数字信息的最小单位。")`

- `quiz::Quiz("Bit (Bit Depth)", "在数字录音中，使用的位数决定了动态范围。比特率越高，质量越高。")`

- `quiz::Quiz("Blending", "将多个通道混合为一个通道的过程。")`

- `quiz::Quiz("Blue Noise", "技术上，一种功率密度随频率增加而增加的噪声。具有嘶声的特征。")`

- `quiz::Quiz("Boolean", "布尔逻辑有两个状态：0 或 1。")`

- `quiz::Quiz("Boost", "使用均衡器增加特定频率的增益。")`

- `quiz::Quiz("Bouncing", "过去经常使用的将多个轨道混合到一个或两个（单声道或立体声）轨道的技术。")`

- `quiz::Quiz("Boundary Microphone", "一种全向麦克风，设计为平放在平坦表面（或边界）上，创建“半全向”模式。边界麦克风是 Crown Audio 的商标。")`

- `quiz::Quiz("BPF", "带通滤波器（BPF）保留中心频率周围的谐波不变，并衰减中心上方和下方的。距离中心越远，衰减越严重，取决于滤波器中极点的数量，每个极在每个八度内对应 6 分贝的衰减。")`

- `quiz::Quiz("Boom Stand", "一种带有伸缩臂的麦克风支架。")`

- `quiz::Quiz("Brickwall Filter", "一种特定的低通滤波器，表现出陡峭的截止斜，类似于“砖墙”。虽然这些滤波器通常用于 A/D 转换器以防止混叠，但它们陡峭的截止可能会对音频信号引入意外的副作用，即相位偏移。")`

- `quiz::Quiz("Bridging", "一种将单个输入送到放大器两个通道的技术，将它们合并为一个，从而有效地倍增了放大器提供给信号的功率。")`

## 附录 C：C20 代码

- `quiz:Quiz("Brownian Noise", "也称为棕色噪声，从技术上说，它是噪声功率密度（频谱响度）在产生频率时每八度下降 6 分贝的噪声。它具有丰富的低音音色，类似于远处的波浪声。它也可以用于缓慢变化的控制电压或调制信号，而不是作为音频源。")`

- `quiz:Quiz("Buchla Bongos", "这是一个经典的接线模式，将复杂的源（例如一个振荡器频率调制另一个振荡器）发送通过低通门（Low Pass Gate），仅发送触发信号来“击打”虚拟内部，或者使用瞬时攻击/快速衰减来产生打击乐器声。最后一次通过门限时在减少音量的同时也减少了高谐波，这一事实有助于消除复杂源中的谐波，并创造出类似于击打乐器的衰减。")`

- `quiz:Quiz("Bucket Brigade Delay", "回声或延迟效果的早期设计，其中输入音频被采样为模拟电压，在短暂的瞬间，下一个高于采样采样率的时钟脉冲会将该电压传递到电路中的下一个采样并保持（桶），同时采样一个新的电平。桶式延迟（BDBs）的桶数量通常是 2 的幂（256, 512, 1024, 2048 等）；其长度由级数乘以采样之间的时间间隔决定。")`

- `quiz:Quiz("Bucket", "两个相同信号或频率之间的相位抵消阶段，具有相同的振幅、相反的极性，会相互抵消。最常用于乐器频率背景。例如：带有嗡嗡声的吉他拾音器设计初衷是利用这一原理从信号中返回或“抵消（buck）”频率。")`

- `quiz:Quiz("Multiple", "你通常需要分割或复制信号以发送到一个目的地。这在分路器（multiple）中很常见，你插入源，然后插上跳线线去往多个目的地。有源或缓冲的分路器在输入和输出之间包含一个缓冲电路，确保信号不会因为被拆分多次而失去强度或完整性，并且一个输出上的任何操作都不会影响任何其他连接。某些模块在其输出中内置了缓冲，并可以使用驱动多个模块。但如果你想使用无源分路器连接（例如）三个振荡器，而你发现轨道并不理想（随着你向下移动比例，它们会很快不同步），那么你需要缓冲分路器实例。")`

- `quiz:Quiz("Bulk Dump", "系统独占批量传输（System Exclusive Bulk Dump）的缩写，在 MIDI 设备之间传输此类内部参数的方法。")`

- `quiz:Quiz("Burst Generator", "当你发送此模块时，它会响应输出一个触发流或“爆发（burst）”。通常你可以控制触发的数量、它们之间的间距，通常还有单个触发输出被发送或跳过的概率（随机模式）。在最温和的情况下，它可以用于响应普通音符创建“双脉冲”触发；在最极端的情况下，它被用于触发可能与音乐不同步的混沌触发。")`

## 附录 A：C20 代码

- `quiz:Quiz("Capsule", "撇开空间追踪定义不，这是麦克风中包含振膜和活性元件部分的名称，即将声波转换为到电流和电脉冲的机械结构。碳元件位于两块板之间；当声波击中碳元件时，它会产生板之间电阻的变化，从而影响电信号。")`

- `quiz:Quiz("Carrier", "有几种合成技术，其中一个普通的音频速率信号改变另一个音频信号。例如，在频率调制中，第二个信号（称为调制器）改变主信号（称为载器）的频率（音高）。更多细节请见频率调制和幅度调制的条目。")`

- `quiz:Quiz("Cascade", "连接或“链式连接”两个混音器，使第一个混音器的立体声混合到第二个混音器的立体声总线中。")`

- `quiz:Quiz("CCW", "逆时针，通常用于控制旋向左旋转（时钟指针相反的方向）。")`

- `quiz:Quiz("CD", "光盘的缩写，一种带有数字音频的小型光学磁盘。")`

- `quiz:Quiz("Cent", "在调音器时，一个半音被分为 100 个称为“分”（cents）的单位；每八度 100 分。当一个振荡器相对于另一个失调时，它们的频率差有时用分来测量。")`

- `quiz:Quiz("Center Frequency", "受均衡器影响最大的音频信号频率，无论是增强还是衰减该频率。在图上绘制，这是钟形曲线的顶部或底部（峰值）。")`

- `quiz:Quiz("Channel Path", "从声源到多轨道录音机（或 DAW）的完整信号。例如，从麦克风传输到前放大器的音频信号，在混音器上有一个通道条，然后通过输出发送到录音机。这与监听不同，监听将信号馈入耳机而不触碰（不影响录制）。")`

- `quiz:Quiz("Channel", "多轨道磁带某部分的音频录制，通常用于与其他通道合并，一个可以从输入传输到输出的单一路径。")`

- `quiz:Quiz("Chaotic", "信你不信，混沌并不意味着完全随机。混沌理论处理在边界范围内是随机的系统。它们既不是失控的，也无法预测。混沌系统通常指一个类似于低频振荡器的调制器，它在另一个松散或偶尔重复的模式中具有不可预测的抖动或故障。它也可以指不符合音乐节奏划分的触发爆发。")`

- `quiz:Quiz("Chase", "自动调整记录器（或序列器）的速度。")`



## 术语表

- `quiz:Quiz("Chord Chart", "一种提供节奏信息的音乐简记形式，常用于节奏组或爵士乐队。在同步中，和弦图通常关注旋律和和弦（详见‘线谱（Lead Sheet）’）。")`
- `quiz:Quiz("Circuit", "电路内部的一条完整信号路径。")`
- `quiz:Quiz("Class Compliant", "指即插即用的设备——它可以直接插入 USB 而无需安装额外的驱动程序。这在模块世界中通过 USB 同步非常常见：如果你将经典的 USB 设备如推子插入它，转换器将识别它。")`
- `quiz:Quiz("Click Track", "馈入耳机的节拍器“点击”，其目的是帮助音乐家与歌曲同步。")`
- `quiz:Quiz("Clip", "所有活动电路对通过它们的信号强度都有限制。这些限制通常与正负电源电平有关。如果信号尝试超出这些限制，它们会在那里变平（或被裁剪）。例如，12 伏输入可能没有变化，但 13 伏输入将输出 12 伏。裁剪会导致波形失真，增加高谐波。之所以命名裁剪是因为生成的图形波形看起来像波形的边缘被“裁剪”了。")`
- `quiz:Quiz("Clock Signal", "电路内设备通过产生稳定脉冲以保持其他设备同步的信号。音乐中的一个例子是同步 MIDI。序列器发送时钟信号，使连接的设备同步。")`
- `quiz:Quiz("Clock", "通常指同步中的主节奏脉冲。通常，时钟脉冲比它可能驱动的快得多，例如序列器或 LF。常见的时钟速率是 24 ppqn（每四分音符脉冲），DIN 同步也是如此。驱动序列器向前移动音符的触发在系统中也称为“时钟”。在这里，时钟模式对主时钟进行分频和倍频以产生与主时钟相关的时钟信号。")`
- `quiz:Quiz("Clock Moving", "一种麦克风放置技术，将麦克风靠近光源以捕捉直接声并抑制环境声。")`
- `quiz:Quiz("Coaxial Cable", "同轴电缆（缩写为 Coax）由由周围屏蔽的导体组成的双导体电缆。")`
- `quiz:Quiz("Coincident Mixing", "一种立体声混音技术，将两个麦克风的头部尽可能靠近。由于声源到另一个麦克风的距离相同，这防止了混音中的相位抵消问题。")`
- `quiz:Quiz("Compander", "一种作为压缩器和扩展器组合的信号处理器")`

## 附录 A：C++20 代码

（是杜比降噪系统背后的原理）。

`quiz:Quiz("比较器", "一种比较一个电压电平与第二个电压电平的电子设备。这第二个电压可以是比较器开关模块上的第二个输入，也可以通过旋钮或内部参考值进行设置。大多数情况下，比较器输出一个门控信号，当第一个信号高于第二个信号时，信号变为高电（反之亦然），当第一个信号低于第二个信号时，信号变为低电。")`

`quiz:Quiz("混音", "在数字音频工作站 (DAWs) 中，混合多条录音的过程需要时间来创建一个“混音”（参见轨道、播放列表。） 2) 在爵士乐表演中，“伴奏”（accompanying）的缩写。")`

`quiz:Quiz("压缩器驱动程序", "一个显示压力波进入扬声器的 AD 图形。")`

`quiz:Quiz("比率", "它定义了压缩器对输入信号的衰减程度，以分贝为单位。例如，4:1 的压缩比意味着对于信号超过阈值的每 4 dB 增加，压缩器仅允许信号增加 1 dB。")`

`quiz:Quiz("压缩器", "在信号处理中，压缩器执行的操作也称为“压缩”（Compressor）。 2) 在声学中，由声波压力峰值引起的空气压力增加，用于“压缩与稀疏”（compression and rarefaction，也称为“稀疏”）。")`

`quiz:Quiz("压缩器", "一种信号处理器或插件，通过放大音频的较小部分并衰减其较大部分来控制音频的动态范围。")`

`quiz:Quiz("电容麦克风", "一种通过电容器的变化将声音转换为电流的麦克风。（声波移动振膜，改变电容的变化，然后这些变化被转换为电电压）。")`

`quiz:Quiz("接触式麦克风", "一种旨在拾取固体振动（而非空气中的振动）的麦克风。也被“压电式”，通常用作声吉他拾音器来捕捉琴板的振动，或用于使用各种物体创作“噪音音乐”的实验音乐家。")`

`quiz:Quiz("控制电压处理器", "CVP 是处理通过它的电压的所有底层处理模块的缩写 - 例如通过通过比较器来放大或衰减输入电压。Make Noise 的 Maths 也许是世界上最著名的电压处理器；你还会在系统中发现更多此类模块，帮助调节电压以实现你的需求（或教它们新花样）。")`

`quiz:Quiz("控制电压", "控制电压 (CV) 的概念是合成器的根基。基本思想是使用模拟电压电平通过振荡器来确定音高；第二个控制电压可能决定该信号在通过电压控制放大器后的响量。CV 是用于控制共振（反馈）量的控制电压输入 - 不仅仅是前面板上的自定义旋钮。））用于控制另一个设备。最常用在控制其他 乐器和设备的 MIDI 控制器语境中，MIDI 控制器发送 MIDI 信号来控制其他 MIDI 乐器和设备。录音室中控制器的其他用途还包括监听控制，控制左侧（与时针反方向移动）。一个计算机（也简单地称为“处理器”）让声音和混响声音量相等。临界距离随距离而变化。")`

`rd 轨道合并到复合录音中。夜店 DJ 还使用交叉淡入淡出从一个过渡到下一个而无需停止。”将信号发送到一个扬声器并发送到另一个。`

`quiz:Quiz("分频器")`

`quiz:Quiz("串扰", "两个音频通道之间音频信号的意外泄漏，例如调音台上的信号叠加，或者两条轨道之间的重叠。")`

`quiz:Quiz("截止频率", "滤波器的截止或频率是信号开始过滤的电位。例如，低通滤波器的转角频率为 500 Hz（每秒循环），所有 500 Hz 以下的谐波将不受影响，而所有 500 Hz 以上的谐波将被“过滤掉强度 - 越超过 500Hz，过滤越越多”。")`

`quiz:Quiz("截止斜率", "滤波器通过范围之外频率的衰减率。斜率是滤波器的特性。")`

`quiz:Quiz("CV/Gate", "这是标准 ADSR 包络的一个稍微高级一点，它引入了一个初始攻击阶段（从峰值上升）。每个补丁都是将某种类型的包络路由到低通截止，因此音符开始时最初有一个静音的、经过过滤的声音。")`

`quiz:Quiz("CV", "控制电压 (CV) 的概念是合成器的根基。基本思想是使用模拟电压电平通过振荡器来确定音高；第二个控制电压可能决定该信号在通过电压控制放大器后的响量。CV 是用于控制共振（反馈）量的控制电压输入 - 不仅仅是前面板上的自定义旋钮。")`

`quiz:Quiz("CVP", "CVP 是处理通过它的电压的所有底层处理模块的缩写 - 例如通过比较器来放大或衰减输入电压。Make Noise 的 Maths 也许是世界上最著名的电压处理器；你还会在系统中发现更多此类模块，帮助调节电压以实现你的需求（或教它们新花样）。")`

`quiz:Quiz("周期", "波形的一个完整表达式，从某点开始并返回相同的值。")`

`quiz:Quiz("链式连接", "三个或更多设备的连接，其中音频信号通过第一个设备到达第二个，再通过第二个设备到达第三个。")`

`quiz:Quiz("阻尼系数", "描述了放大器在音频信号峰值时抑制扬声器振盆推回运动（刹车）的能力。")`

`quiz:Quiz("阻尼", "振动系统能量的减少，摩擦可以指电信号中幅的减小，或者乐器的受控振动（例如声学钢琴上的延音踏板）。")`

`quiz:Quiz("DAW", "数字音频工作站缩写，用于数字录音和混制的设备或软件程序。")`

`quiz:Quiz("dB", "分贝的缩写，一种比较信号（音频电平）的测量比例。")`

`quiz:Quiz("DBX", "一系列降噪系统，由开发它们的公司。DBX 降噪没有为人知的杜比系统那样成功，但偶尔出现在录音室中。")`

`quiz:Quiz("直流耦合", "当模块保持其输入为直流耦合时，意味着它可以接受直流电压（恒或不断变化的电压）并不加改变地传递。这很重要，例如，如果你想使用 VCA 控制通过它的包络的振幅。你需要一个直流耦合的，a")`

## 附录 A：C20 代码

交流耦合允许你减少信号的直流分量（例如它

维持电平）并将其返回到 @").

交流电（AC），以交替的方向流动。许多电子设备运行在直流电上，直流通常由电池电源、USB 电源或插入墙插座的 AC 适配器提供。在模块化术语中

在一个稳定的电平上保持一段时间，就像门控输出在音符关闭时切换到 \@ 在音符开启时切换到 5 或 10。它也可以指一个缓慢变化的

速度

模拟振荡器 - 不使用电压电平来确定振荡器的频率，

振荡器使用数字设备作为计数器来确定每个

波形的长度，从而确定频率。优点是调音非常稳定，

不像某些全模拟设计。缺点是，没有不完美性，而这些

冲拍会导致细微的调偏（从而产生对“厚实感”的感知），当

使用多个振荡器速度时。",

`Quiz("去齿器", "一种音频压缩器，旨在减少��齿声和频率的音量，特别是发音字母“s”时产生的声音。")`

`Quiz("衰减", "通常，衰减是指电压或整体电平从高点下降 - 如包络发生器的衰减阶段。在真实 世界中，当你敲击鼓或拨动弦时，它会衰减 - 从音量逐渐减小，直到完全静音。它也可以")`

`Quiz("迪卡树", "一种立体声麦克风放置技术，涉及三只麦克风 （通常是指向性的），以“T”字型排列。常用于混音 - 合唱团、交响团和其他更大的合唱团，但迪卡技术的 变体今天也被用于环绕声场合）。")`

`Quiz("分贝", "缩写为“dB”。两个相应量之间的比例测量，根据一个比例，其中某个百分比代表一个单位。最用于 描述音频电平。")`

`usdy, 去磁消除录音带上的残留 -`

`Quiz("这是标准的 ADSR 包络发生器，在延迟攻击之前引入一个初始延迟 初始攻击阶段（从 0 到峰值电平的上升）。一种方法是将 这种类型的包络路由到低通滤波器截止频率，这样当音符开始时， 最初是静音的，在暂停后它开始膨胀成 更明亮、完整的声音。")`

`Quiz("延迟", "你们都知道 delay 这个词在正常世界中的含义；它 在模块合成器中以不同的形式出现。例如，它可以指回 声中重复部分之间的间距；那是一个回声设备被称为 \-delay 效果。它也可以指你延迟信号的可编程时间， 例如门控、触发器或包络的初始阶段，使音符在实际播放 后才开始。还有")`

`Quiz("演示版", "一种初步录音，旨在让听众对最终制作中的声音可能有多好有一个直观感受。Demo 利用了最少的跟踪 制作，几乎就像录音的“粗草稿”。")`

`Quiz("调谐", "如果你有两个振荡器的频率调到完全相同 – 我我的意思是，完全相同的频率，那么使用超过一个 振荡器就没意义。当你非常细微地改变一个振荡器的调谐， 换句话说，对其进行调谐，你将开始听到两个振荡器 之间有趣的相互作用，通常被称为合唱或拍频。结果往往 更有趣且“丰满”，并更自然一些，因为两个歌手或乐器很难 达到完全相同的频率。这种目的是可以使用乐器或 故意跑调（通常是轻微的）。这种效果可以用于录室中的 多种用途，也可以用于“双轨录音”，将调谐偏差的乐器/轨道与 混合以创造出更丰满的声音。")`

`Quiz("直连", "使用电学拾声器或直连盒将电音频信号 直接从乐器发送到控制音台的过程，而不是使用麦克风。")`

`Quiz("对话", "在电影/视频声音、广告和 教学录制中记录的词。")`

`Quiz("振膜", "麦克风中响应声波而移动的部分，将其转换为 电信号。")`

`Quiz("数字音频工作站", "缩写为 DAW。一种设备或计算机软件 以数字方式记录和混音音频，或一组集成程序，但它们最常见 是独立的单元或“机内”软件程序。录音室中最常用的 DAW 程序是 Pro Tools；其他常用的程序包括 Line, Reason, Ableton 和 Logic。")`

`Quiz("数字万用表", "一种测试电电压、电流、电阻的小型设备。万用表用于录音室校准电 系统和排除故障。")`

`Quiz("数字录音", "将音频信号转换为代表波形的数字的过程，将这些数字存储为数据")`

`Quiz("数字信号处理", "缩写为“DSP”。任何信号处理 过程，其中音频信号已转换为数字")`

`Quiz("数字转模拟器", "缩写为 D/A。一种将数字 数据转换为模拟量的设备。")`

`Quiz("数字", "曾有一段时间，基于数字的 ar ")`

## 附录 A：C++20 代码

方向。许多电子设备

设备运行在直流电上，直流通常由电池 电源、USB 电源或插入墙插座的 AC 适配器提供）。

`Quiz("直接输入", "缩写为“DI”。使用电学 拾声器或直连盒将电音频 信号直接从乐器发送到控制音台的过程， 而不是使用麦克风。")`

`Quiz("直接输出", "某些控制台上的可用输出，直接馈送到 通道和推子。此功能用于发送一个")`

`Quiz("直射声", "直接到达麦克风或听者耳朵的声音，没有 经过任何障碍物的反射")`

`Quiz("指向性模式", "I) 在麦克风中，一个术语，意思与 采样模式相同，在扩散模式中，即")`

`Quiz("扩散", "扬声器声音有效覆盖的区域；具体来说是扬声器两侧的虚拟边界，那里的声音比正面前低 6 dB。每个扬声器都有水平和垂直角度。")`

`Quiz("远场拾音", "将麦克风放置远离声源的技巧，以捕捉 直接声和反射声的组合")`

`Quiz("失真", "指设备输出处的波形与输入相比 发生了变形，通常是由于过载，导致产生失真或“脏 信号。虽然电气或音频失真通常是不受欢迎且被规避 的，但在音频的受控情况下经常被用来创造理想的 效果，特别是对于电吉他和放大器。")`

`Quiz("多样性", "I 在音频设置中：在无线接收 系统中使用两个或多个天线来防止无线麦克风的音频中断。 2 在其他设置中：拥抱每个个体的独特性）。")`

`Quiz("杜比", "一家制造降噪系统和其他音频系统的制造商的品牌名称，用于提高音频录制、回放和传输的性能和保真度")`

`Quiz("多普勒效应", "人类耳朵在声音运动时感知到声音频率（音调）变化的现象。当声源靠近，声波到达耳朵的距离变短，增加了频率和声音的音调；当声源远离时，声波必须走得越远越，导致频率降低。这种效应的一个例子是接近的紧急车辆，警报声在靠近时较高，驶过后变低。多普勒效应可以 应用于音频设置中，例如在 Leslie 扬声器中，电机 带动旋转箱体内的扬声器，不断改变之间的")`

## 附录 C：C++ 代码 20

在声源与听者（麦克风）之间，并创建其独特的摇摆颤音效果）。

`Quiz("Double", "1) 录制第二次与第一次表演非常匹配的表演，目的是为了混合两条轨道。2) 使用延迟线 m-")`

`Quiz("Driver", "1) 扬声器中的换能器，它将电信号转换为声压。2) 控制连接的设备（一个硬件部件）的计算机程序。")`

`Quiz("Dropout", "在数字文件中（通常是由于采样丢失），这可能导致音频出现意外的下降、破裂声或啪嗒声”。")`

`Quiz("Drum Machine", "一种电子设备，其内存中合成和/或采样声音，并带有一个可以编程播放鼓点模式或循环的内部序列器。")`

`Quiz("Pattern", "一段特定的由鼓手演奏的特定鼓声序列，或在鼓机中进行解序的序列以供歌曲使用）。")`

`Quiz("Dry", "没有任何效果的声音被称为“干声”（dry），带有效果（如混响）的声音经过混合后被称为“湿声”（wet）。效果器或调音台具有干湿混合比例（该比例调节了原始未处理声音与完全添加效果声音之间的比例）。")`

`Quiz("DSP", "在音频信号转换为数字音频后的任何数字信号处理）。")`

`Quiz("Dub (or Dubbing", "1) 复制录音。2) 实时录制并意图是混合两条录音（另见叠加录音 Overdubbing）。3 “Dub”是“双步舞”（dubstep）的缩写，电子音乐的一种风格或子派）。")`

`Quiz("Ducking", "一种基于压缩的音频效果，由于另一个音频信号的存在，音频信号被不成比例地减小，这通常通过人声轨道在录制的音乐轨道上使用带有信号处理器的“侧链”来实现。一个显著例子是当演讲者再次说话时的音量变化。更微妙的例子是音频引擎声音为轨道中的其他声音留出空间；例如，当贝斯吉他信号触发鼓或吉他电平轻微降低。（参见“侧链 Sidechain”。）")`

`Quiz("Duphonic", "Duphonic 意味着两个“声音”。大多数早期合成器（包括模块化系统）是单声的（monophonic），这意味着它们一次只能播放一个音；某些乐器具有振荡器、滤波器、包络和放大器，它们可以将两个独立的音符作为一个整体播放。某些 MIDI 接口允许来自你的——和多声的（polyphonic）， 门限信号在一定时间内保持“高”电平 - 100 msec 被认为持续了 100 msec。你按住音符的时间")`

## 附录 A：C++ 代码 20

`Quiz("Dynamic Microphone", "（也称为动线圈麦克风）一种声波中的麦克风，通过磁场内移动的感应线圈将压力转换为电信号——这一过程通常被比作扬声器的反向工作。动态麦克风的灵敏度低于电容麦克风，但对于产生更大的声源或近麦应用可能非常有效。")`

`Quiz("Processing/Dynamic Signal Processing", "自动改变电平（或）以改变最响和最软音频之间电平关系的过程。动态处理器包括压缩器、限制器、门限器。")`

`Quiz("Dynamic Range", "声音或录音的峰值与最软电平之间的比例（单位为 dB）。设备或系统在不失真的情况下能提供的最软与最响电平之间的比例（单位为 dB）。")`

`Quiz("Early Reflections", "在房间内传播的第一批波，通常在经过表面反射后被听者的耳朵听到，在初始声音后立即被听到。混响的第一阶段。")`

`Quiz("East Synthesis", "此预置应用于 East 合成器生产的最常见合成器配置，如 Moo、ARP 和 East（以及“远东”的合成器，如 Roland 和 Karg），其中一个或多个产生具有谐波波形（如锯齿波或方波）的振荡器被输入滤波器，滤波器移除了一些谐波，然后通过放大器调整到音符的响度。这也被称为减法合成，因为滤波器减少了")`

`Quiz("Echo Chamber", "一个具有非平行表面的封闭房间，用于创建声学回声。")`

`Quiz("Echo", "初始声音的清晰反射，在表面反弹后被我们识别为回声，许多回声发生得太快，以无法单独听清。")`

`Quiz("Edit", "在播放后更改录音声音的多个参数；现在几乎所有的编辑都是通过数字完成的。")`



# 术语词汇表

## 效果与信号处理

### Effect Loop (效果环路)
有时你可能想将信号发送到系统之外，通过外部设备处理并将其带回。效果环路的技巧在于，它们的电平往往比外部设备使用的要高得多。

### Effects Processor (效果处理器/吉他效果器)
一种向直接信号路径添加混响、合唱、移相等效果的设备。它们也可以作为单体踏板或数字插件被找到。

### Effects Track (效果轨道)
1. 在电影制作中，准备好与另一个声音混合的录音。
2. 在音乐中，有一段要添加效果的录音。

### Effects (效果)
1. 通过某些事物修改音频信号以改变声音的各种方法。
2. 除了旁白或音乐之外的音效等添加到电影中的短音。

### EG (Envelope Generator, 包络发生器)
包络发生器用于连接到 VCA（电压控制放大器）时处理音符的响度或动态，并在连接到 VCF（电压控制滤波器）时处理其频率或音色随时间的变化。为了做到这一点，包络发生器创建一个电压，通常从零上升到某些最大电平，然后返回。你控制这需要多久，通常分为几个阶段：从零到最大值的起始阶段（Attack），从最大值回落到零的衰减阶段（Decay，在 AD 或 Attack/Decay 包络的情况下）或称为持续的中间电平（Sustain），以及（通常在键释放后，相应的门限从持续电平回到零，其持续时间被称为释放时间 Release）。

### Electphone (驻极体麦克风)
电容麦克风的一种变体，在电容器内部有一个电极（也称为“驻极体麦克风”）。由于元件是完全极化的，驻极体麦克风不需要像标准电容麦克风那样的外部电源。

### Electret (驻极体)
电介质板被设计为具有永久性，使其功能类似于磁铁（“Electret”一词来自电力和磁铁两个词）。用于某些技术。

### Electromagnetic Field (EMF, 电磁场)
由通过导体的电流产生的电磁场。

### Electromagnetic Interference (EMI, 电磁干扰)
世界各地音频专业人士的噩梦，EMI 是由附近的电磁活动引起的干扰类型，这种干扰会被音频线和设备拾取，导致音频系统中产生不必要的噪声、嗡嗡声或滋滋声。音频系统中电磁干扰（EMI）的常见原因可能包括大电源线、荧光灯、调光开关、计算机、视频显示器和无线电发射器。

## 电子学基础

### Electron (电子)
围绕原子核旋转的带负电的粒子。电流是由电子沿导体（如金属线）移动产生的。

### Emphasis (强调/重点)
这个词有两个含义。在普通的音频语境下，它通常是指某种形式的高频增强，强调高谐波可以为音色增添色彩并帮助将其与其他声音区分开。在合成器中，强调是指滤波器上的 Q 值或共振设置，增加此设置会增强截止频率或中心频率的谐波。

### Envelope Follower (包络跟踪器)
该模块跟随声音的响度，输出与响度变化相应的电压。然后对该信号进行一些平滑处理，使其在本质上不会过于敏感或抖动。包络跟踪器还有一个门限输出，当输入信号的响度超过特定电平时输出高电平，当其低于该水平时输出低电平。

### Envelope Generator (包络发生器)
包络发生器（EG）模块用于塑造连接到 VCA（电压控制放大器）的音符响度或动态，并在必要时通过 VCF（电压控制滤波器）改变其频率或音色。为了做到这一点，包络会创建一个通常从零伏上升到某些最大值然后再次下降的电压。你控制这些变化，通常分为若干个阶段：起始阶段（Attack）从零到最大，衰减阶段（Decay）从最大回到起始水平（如果是 AD 包络）或作为持续（Sustain）的中间水平，然后（通常在按键释放且相应的门信号回到零后）从持续水平在持续时间内回到零，这称为释放阶段（Release）。

### Envelope (包络)
声音寿命的四个要素的统称：起始（Attack）、衰减（Decay）、持续（Sustain）和释放（Release）（简称 ADSR）。声音包络描述了声音或音频信号强度随时间变化的程度。

### Equalness Contours (等响度曲线/菲莱彻-曼森曲线)
一张显示几条曲线的图，展示了不同频率的音调必须以多大的响度才能让人们认为它们的响度相等。

### Equalizer (均衡器)
一种使用一个或多个滤波器来增强或减少声音中某些频率的幅度（音量）的音频处理器。其基本原理是平衡或“均衡”音频系统的频率响应，或者在声空间内的多个信号之间建立平衡。然而，音频工程师以许多不同的方式使用均衡器来“染色”声音。

## 模块化合成与制式

### Eurorack (欧莱克)
Eurorack 可能是最流行的模块化合成器格式，拥有 100 多家制造商和 1000 多个模块。它由 Doepfer Musikelektronik 在 1995 年创建，其尺寸基于 Eurorack 格式设备标准。有些用户会试图告诉你 Eurorack 的声音“听起来”没有其他格式好，但那只是基于少数不标准的制造商或模块；该标准本身没有任何导致最终声音产生巨大差异的固有因素（不；12 伏和 15 伏电源之间的差异不足以导致大多数差异）。

### Expander (扩展器)
一种信号处理器（或插件），其执行的功能与压缩器相反，是扩展音频信号的动态范围而非压缩。这是通过进一步减小低于设定阈值的信号幅度来实现的。

### Expansion Ratio (扩展比)
扩展器在每秒内衰减的速率，以分贝为单位。例如，2:1 的扩展比意味着信号每低于阈值 2dB，扩展器就将信号衰减 2dB。如果信号低于阈值 3dB，扩展器将将其衰减 6dB，依此类推。

### Exponential (指数/指数型)
通常来说，这是一种从平坦到陡峭上升的数学曲线。在合成中，它指的是一个起始相对平坦并按八度增加的电压，与线性系统形成对比。它会导致每秒的衰减或增加。

### Fader (推子)
一种调整信号电平或衰减的控制。

### Field (声场)
声音的一个区域。在扬声器周围，随着距离的变化而发生变化。音频工程师在混调时经常使用近场和远场监控。另参见“Near Field（近场）”。

### Feed (馈送)
将音频或控制信号发送到...

### Feedback (反馈)
反馈线上的反馈量。

### Feedback (反馈/啸叫)
通过均衡器进行频率响应。

### Fidelity (保真度)
描述声音再现准确性的术语。

### Figure-8 (八字型/双向型)
拾音模式，对正反方向最敏感，有效过滤掉侧面的声音。

### Filter (滤波器)
减少或移除通过它的频率的模块。在合成器中，典型类型有低通（通过截止频率以下的谐波，并减少更高频率的谐波）、高通（通过截止频率以上的谐波，并减少截止频率以下的谐波）、带通（截止频率附近的谐波被减少或完全切除）；陷波（截止频率附近的谐波被减少或实时）。

### Flanger (移相器/法兰杰)
一种将信号与其带有微小延迟的副本混合（延迟长于合唱效果；短于另一种效果）并与原始信号混合而产生的音频效果。当延迟是恒定时，结果是“梳状滤波器”，其中谐波由于相位相反在自身点上重叠而被抵消。当延迟随时间变化时，你会得到一种扫过的声音。这种效果最初是通过同时播放两个磁带循环，让它们同步，并用手指按法兰来改变副本来实现的。现在，大多数移相通过效果盒或数字插件完成。

### Flanging (移相/法兰效果)
一种将信号与其带有微小时间延迟的副本混合产生的音频效果，通过修改延迟副本产生“旋转”声音。这最初是通过模拟磁带录制中同时播放两台磁带机，让它们同步，并按下机器法兰来改变副本实现的。

### Flat (平坦/降号)
1. 描述设备或扬声器频率响应的术语，当设备不需要均衡即可处理所有频率时。在图形显示时，频率响应是没有峰值或谷值的“平坦”。
2. 在音乐中描述一个音准偏差的音符或音高，频率比预期略低。
3. 在乐谱中，一种“变音”标记，指示演奏者或演唱将音符降低半音。

### Flip-Flop (触发器)
在二进制逻辑术语中，触发器在高低电平之间切换，每当接收到输入触发时变为低电平（即：第一个触发将输出置为高电平，第二个触发再次将其置为低电平，以此类推）。在时钟或音频术语中，它分频输入时钟或方波的速度（除以 2）。

### Floating Balanced Line (浮动平衡线)
一种连接“变通方案”，通过修改线路中的连接使其类似于平衡线，从而将不平衡输出连接到平衡输入，以消除不需要的嗡嗡声或蜂鸣声。

### Fly-in (飞入/插入)
向混音或录制中添加没有同步的音频。

### Flying Bus (飞行总线/飞入总线)
这是一种简单的电源分配或总线板类型，通常使用沿整个长度带有多个连接器的带状线来接入电源的输出并将其分配给各个设备。这种类型易于创建和安装，但在某些情况下，可能是模块共享噪声的情况。

### FM (Frequency Modulation, 频率调制)
指一种合成技术，其中振荡器的频率非常快地（以音频速率）由另一个振荡器进行变化（调制）。结果是谐波复合，这些谐波可能与主振荡器的基频调一致，也可能显得刺耳且“不和谐”。

### FOH (Front of House, 音控/前场)
在现场音频中，场馆内位于舞台对面的位置，在此处控制和混音表演的现场音频。

### Foldback (回送/返听/舞台监听)
现场音频中使用的一种监控系统。一组扬声器或监听箱（英国称为“foldback 扬声器”）提供音频信号混合，供舞台表演者听到并演奏。这与观众听到的 FOH（音控）混音完全不同，有时由第二个工程师通过独立于主音响系统的放大器和扬声器进行控制。这种类型的舞台监控经常受到麦克风反馈的影响，在某些场所可能会导致输出混响。由于原因，现场音频系统使用入耳机监听作为舞台监听箱的替代品，以控制舞台噪音并降低反馈风险。

### FSR (Force Sensitive Resistor, 力敏电阻)
在模块化系统中，FSR（力敏电阻）通常表现为一个圆形焊垫，你通过按它来改变参数。它充当电阻，你越用力，电阻就越小。

### Formant (共振峰)
许多在振动管上制造的仪器（包括我们的声道）都有某些它们喜欢的振动或“共振”频率。当你将声音送入这些管子时，它们会强调声音频率（或其某些谐波）以匹配这些共振频率。这些每一个共振频率被称为该仪器的共振峰。合成类人声的一种常用方法是让振荡器通过一个具有多个共振峰的均衡器，这些共振峰间距相等，以模拟某些元音。共振峰是人声或乐器声音中的一种元素，不会随着不同音高的发出而改变频率。共振峰本质上是由于声源的物理结构产生的“固定”频率或共振。这些频率创造了音色，声音中产生吉他、长笛、男声或女声等特定声音的元素。

### Format (格式)
1. 用于在录音室或收听时存储和制作音频的许多媒体之一。示例包括日益使用的物理格式，如黑胶唱片和唱片；过时的格式，如卡带、8 轨道和 DAT；模拟磁带和数据带，如卷带多轨磁带；以及许多数字音频格式，如 mp3、WAV、MAG、AIFF 等。
2. 格式也可以描述录制到模拟磁带时的特定参数，如轨道数、使用间距和顺序。
3. 为了使用对硬盘或载体进行格式化，通常是擦除其中的所有现有数据。

### Four Quadrant (四象限/四象限乘法器)
四象限混音器是幅度调制（AM）的一种特殊情况。它也被称为环调制或平衡调制。一个信号改变第二个信号的电平。结果是频率的复合波。

### Fractional (分式/分数)
合成器中的一个振荡器以频率变化...

### Full Normalled (全常态/全规范化)
描述跳线板中的一种配置，插座形成一个连接路径，直到插入插头改变切换。见“Half Normalled（半常态）”。

### Frequency Modulation (FM) Synthesis (频率调制合成)
一种方法，其中振荡器（载波）被改变...

### Frequency Range (频率范围)
1. 电子设备可以工作的频率范围。
2. 声音源的频率范围。

### Frequency Response (频率响应)
系统能够有效处理的高低频率的范围。

### FSK (Frequency Shift Keying, 频移键控)
一种已过时的协议，在磁带上录制以同步。见“Smart FSK”。

### Frequency (频率)
特定事件在时间内发生的次数。在音频和声学中，频率指的是振动或波形的完整循环次数，单位为每秒循环（Hz）。频率决定了我们听到的音高。频率越高，音高越高；频率越低，音高越低。

### Front of House (FOH, 音控/前场)
在现场音频设置中，场馆内位于舞台对面的位置，在此处控制和混音表演的音频。

### Full Normalled (全常态化/全规范化)
描述跳线板中的一种配置，在没有插入插头的情况下，插座形成一个连接路径。

### Full Wave Rectification (全波整流)
全波整流器将任何负电压反转使其变为正电压。这实际上双倍了许多简单波形的频率。

### Function Generator (函数发生器)
发生器一词有两种含义。一种产生正弦波、方波等波形的测试设备通常被称为“函数发生器”。包络发生器有时被称为“发生器”。在这两种情况下，“函数”都意味着执行某种方程，如产生周期性波形或响应触发信号产生上升下降。

### Fundamental (基频)
（也称为基频频率或第一谐波）乐器或人声发声时的最低频率。

## 增益与动态控制

### Gain Control (增益控制)
改变放大器或电路增益的设备，通常是一个可以旋转的旋钮（电位器）。在调音台上，每个通道通常都有自己的控制单元，用于调节输入调音台信号的增益（不要与通道“Fader（推子）”混淆，推子用于调节已放大信号的输出）。

### Gain Reduction (增益衰减)
压缩器或限制器在调节音频信号振幅时的动作。

### Gain Structure (增益结构)
一个描述音频系统中多个组件之间互连方式的术语，以及在每个点发生的增益增加或减少的量。具有良好增益结构的配置意味着组件正在协同工作，以最小的失真或噪声提供最佳的增益。

### Gain (增益)
音频信号强度的增加量，通常以分贝（dB）表示。

### Gate (门限/门控信号)
这是模块化合成器内部主要的信号类型之一。当新的音符被建议开始时（例如你在键盘控制上按下琴键，或序列器跳到下一个“阶段”或一个音符时），门限会跳到高电平——通常为 5 伏。门限通常持续整个音符期间（只要琴键一直被按住），并在音符结束时（即松开琴键时）突然下降或回到其静止电平——通常为 0 伏，但某些情况下为 5 伏或其他数字。

### Generation Loss (代损/世代损失)
音频被录制时，由于额外的噪声和失真导致的清晰度减少量。

### Generation (代/世代)
用于描述录制的音频信号被复制的次数的术语。

### Glide (滑音/滑移)
指音符在仍可听的情况下从一个音高滑动到另一个音高。这种效果的术语称为 Portamento（滑音），即音符之间的连奏。在合成器中，这种效果通过使音符的音高控制电压从上一个音符的音高滑动而不是跳变来实现。创建这种效果的模块有时被称为 Slew Generator（斜率发生器）、Slew Limiter（斜率限制器）、Lag Processor（延迟处理器）或 Lag（延迟器）。有些人将 Glide、Glissando 等术语通用使用，但如果你非常钻牛角尖，Glissando（滑奏）是一种不同的效果，当中间音符更加清晰时——例如快速连续弹奏而不是平滑滑过。

### Golden Ratio (黄金分割/黄金比例)
也称为黄金比例。宽度与长度的比例，其中宽度大约是高度的 1.6 倍，长度大约是高度的 2.6 倍。这种比例由古希腊人首次计算，在数学上被称为“phi”，用于许多应用，包括房间尺寸和录音室设计（为了实现房间内的“最佳声学效果”），以及某些声学仪器的设计。

### Graphic Equalizer (图形均衡器)
一种均衡器，可以使用分配给特定频率频带的推子来调整输入信号的各种频率。（参见“Equalizer（均衡器）”）。

### Ground Lift (地线提升/接地举升)
一种能让三脚插头插入两脚插座的适配器。有些劣质产品使用这种插头来中断接地并防止嗡嗡声，但在未通过其他方式接地设备的情况下，使用不接地的插头来保护地线连接是非常不安全的。

### Ground Lift Switch (地线提升开关)
一种断开接地与机箱地之间连接的开关，用于消除地环路引起的嗡嗡声或滋声。

### Ground Loop (地环路)
一个或多个电子设备在不同点连接到同一个地的情况。设备在不同的地电位下运行，这会在地线上产生电压，导致（低频）嗡嗡声，这种声音可能令人厌烦，最坏的情况下会损坏设备。解决地环路的最佳方法是在同一点对所有设备接地。

### Group (编组/分组)
调音台上的一组输入通道，可以在之前进行调整并合并到总输出。也称为“Bus（总线）”或简单的“组”。

### Group Delay (群延迟)
在音频中，群延迟是所有音频设备（如扬声器、放大器）内部的一种现象，简单来说，较低频率传输得较慢。在所有设备中，输入和输出之间都有固有的延迟，但群延迟专门处理声音中特定频率之间的延迟。配置的目标是将群延迟尽可能小；在极端情况下，高低之间的延迟是可以听到的。

### Guitar Controller (吉他控制器)
一种电吉他（或像吉他一样弹奏的设备），可以传输 MIDI 数据以控制合成器和声音模块。

### Guitar Processor (吉他处理器)
一种为吉他信号添加音频效果的设备，如混响、合唱、延迟、过载等。效果处理器可以以单块或多功能踏板的形式（参见“Pedal（踏板）”）添加到信号路径中。

### Half Step (半音)
钢琴上相邻琴键之间的音高变化。也称为 Semitone（半音）。

### Half Normalled (半常态/半规范化)
描述跳线板中的连接路径，通过插入线缆形成一个连接路径。当 Patch 是“Full Normalled（全常态）”时，通过在输入或输出端插入线缆来更改；当它是“Half Normalled（半常态）”、“Non-Normalled（非常态）”或“Open（开启）”时，则没有内部连接，每个输入都通过其对应发送。

### Half Wave Rectifier (半波整流器)
半波整流器仅通过正电压，并将任何负电压替换为 0V。换句话说，任何“零以下”的内容都被剪切了。



# 附录 A：C++20

## 术语定义

- **quiz::Quiz("厅堂程序")**  
  使用模拟音乐厅的数字混响效果设置。厅堂程序的特点是具有高达 25 ms 的预延迟，在声音电平超过阈值后压缩。（参见“拐点”。）

- **quiz::Quiz("硬拐点")**  
  这是最常见的振荡器同步类型，同步振荡器每当收到同步脉冲时都会重置其波形。如果未指定同步类型，通常是硬同步。

- **quiz::Quiz("谐波失真")**  
  设备输出信号中存在谐波，而这些谐波在输入信号中不存在，通常是为了改变乐器的音色。

- **quiz::Quiz("谐波")**  
  单个谐波是最可能的纯净声音：除了音高和响度之外，它不包含任何识别特征。它的振动形状——无论它是在振动你能听到的空气，还是引起电压升起的电振动——正弦波。大多数时候，泛音之间具有非常特定的频率关系。第一个或最低的泛音——被称为“基频”——是声音的音高，就像和弦中最低的音符是它的“根音”一样。其他泛音更高，表现为基频的整数倍数：其频率的两倍、三倍、四倍，依此类推。前几个泛音恰好具有良好的音乐间距：一个八度；一个八度加纯五度；两个八度。但随着频率越高，它们听起来可能越不音乐化。

### 问答条目

- **问答("泛音 (Harmonics)")**  
  在声音过程中自然产生的基频的整数倍数。在数学上，如果基频为 $f$，则泛音为 $2f、3f、4f$ 等。例如，如果音符的基频为 440Hz（或 A-440），则泛音将为 880Hz、1320Hz、1760Hz 等。泛音的存在创造了乐器或人声的音色。

- **问答("余量 (Headroom)")**  
  放大器或音频设备中正常工作水平与削波水平之间的分贝（dB）差。也描述录制峰值电平与信号失真点之间的分贝差。（也）称为("裕量 (Margin)")。

- **问答("赫兹/伏特 (Hertz/Volt)")**  
  一种系统，其中输入端 1 伏特的变化会导致音高发生固定赫兹（每秒循环）的变化，而不是音乐音程。

- **问答("赫兹 (Hertz)")**  
  （缩写为 Hz）1) 频率的测量单位，具体指每秒内发生的完整波循环次数（每秒循环）Hz = 每秒一个完整波形。（一种在录制中运往录音室常用的租赁车（非典型））。

- **问答("踏镲 (Hi-Hat)")**  
  在鼓中，安装在支架上的双镲片，通常位置在军鼓旁边，可以通过脚踏板或用鼓棒击打上方镲片来演奏。

- **问答("门控 (gate)")**  
  当信号处于电压电平时（通常为 8 伏，它可以被保持，因为它表示它处于“开启”状态——例如键盘控制器上按住了一个音符——称为高电平门。

- **问答("高阻抗 (High Impedance)")**  
  （缩写为 Hi-Z）描述为几千欧姆的阻抗或电抗。在麦克风中，Hi-Z 通常指定为 10,000 欧姆以上。（参见“阻抗 (Impedance)”）。

- **问答("高通滤波器 (High Pass Filter)")**  
  一种音频滤波器，会衰减某些频率（截止频率）以下的信号，并通过频率较高的信号。

- **问答("高端 (High-End)")**  
  "Highs or High End" - “高频”的缩写，泛指 4000 Hz 以上的频率。通常用于音频信号的“高音、中音和低音”语境中。

- **问答("高通滤波器 (High-Pass Filter)")**  
  高通滤波器 (HPF) 设计允许截止或角频率以上的泛音不受影响地通过，并根据低于截止频率的远程度降低低泛音的水平。在 12dB/oct（分贝/八度）高通滤波器中，截止频率下方一个八度的泛音（换句话说，截止频率的一半）被降低 12 dB；截止频率下方两个八度（频率的四分之一）被降低 24dB，依此类推。高通滤波器通常用于产生明亮的声音，其中高泛音远强于基频和低泛音——例如，羽键琴的声音。

- **问答("水平音高 (Horizontal Pitch)")**  
  HP = Horizontal Pitch（水平音高）。在 Eurorack 合成器格式中，模块的宽度定义为 hp（水平音高）单位的数量。每个 hp 是 0.2 英寸（0.5 厘米）。大多数模块的宽度是 hp 的偶数，但有些是奇数。此外，模块的宽度往往略小于 0.2 英寸的精确倍数，以确保你不会遇到模块过宽导致重叠的问题。

- **问答("喇叭 (Horn)")**  
  扬声器或外壳，声音通过扬声器锥体或驱动器进入狭窄开口，该开口扩大到更大的开口。几种低音乐器之一。

- **问答("同步同步 (House Sync)")**  
  使用如 SMPTE 码之类的参考信号来保持房间内所有设备的同步。

- **问答("HPF")**  
  高通滤波器设计允许截止角频率以上的泛音通过，并根据低于截止频率的程度降低低泛音的水平。在 12dB/oct（分贝/八度）高通滤波器中，截止频率下方一个八度的泛音（换句话说，频率的一半）被降低 12 dB；截止频率下方两个八度（频率的四分之一）被降低 24dB，依此类推。高通滤波器通常用于产生明亮的声音，其中高泛音远强于基频和低泛音——例如，羽键琴的声音。

- **问答("嗡嗡声 (Hum)")**  
  1) 电线电流意外感应或馈入电子设备时产生的低频嗡嗡声。反映了基频频率（美国为 60 Hz，其他国家为 50 Hz）。

- **问答("混合电源 (Hybrid Supply)")**  
  混合电源使用线性电源和开关电源技术来处理电压升起和下降的情况。在音频设备中，混合电源通常比纯开关电源更安静且更高效。

- **问答("超心指向型 (Hypercardioid)")**  
  一种麦克风变体，其指向性更窄，能够拒绝来自正面以外的声音。

- **问答("输入端口 (Input Port)")**  
  设备接收信号的插座或物理位置。也指输入的信号本身。

- **问答("ADSR")**  
  这是一种攻击/衰减/维持/释放（ADSR）包络，允许你让攻击阶段处于初始水平——即“I”——而不是自定义。包络线具有这种能力。

- **问答("成像 (Imaging)")**  
  指在立体声场中定位声音的能力。在录制环境中，它欺骗听者认为声源来自特定区域。

- **问答("阻抗 (Impedance)")**  
  指电路对交流电流的电阻。设备之间的阻抗差异会影响其工作方式。阻抗用字母 Z 表示，以欧姆为单位。

- **问答("相位 (Phase)")**  
  当两个或多个设备（以及音频信号）处于相同极性的理想情况，波形不会产生冲突或抵消。

- **问答("无限声障板 (Infinite Baffle)")**  
  一种扬声器或箱，其设计使得来自前面的声波无法到达背面，防止声波相互抵消。“无限”一词源于认为安装扬声器时如果没有墙，将允许无限声波移动到其背后。这在物理上是不可能的，因此无限声障板通过将扬声器安装在墙上，或者建造一个封闭箱体来实现。

## 附录 C：C20 代码

### 测验条目

- **1888 测验：Quiz("集成电路")**  
  集成电路（缩写为“IC”）——一种设置在半导体材料上的由许多组件组成的微型电路，用于电子设备。“芯片”或“微芯片”的华丽说法。

- **1891 测验：Quiz("积分器")**  
  此函数可以平滑化我们改变数值的输入信号。‘积分器’（Integrator）是这种数学函数的学术名称；你更有可能看到此模块被称为慢速斜率（slew）（我会对我们的进行详细介绍）或作为发生器或处理器使用。

- **1895 测验：Quiz("接口")**  
  任何允许一个单元驱动或其他单元通信，或允许人类与计算机或其他电子设备交互的设备或连接点。在专业音频录制中有很多接口的例子，包括 MIDI（乐器数字接口）；音频接口将音频输入连接到你的计算机；你的 DAW 程序显示一个屏幕，允许你分配乐器、调整设置、录制和播放。调音台也是一种接口，连接着房间里的许多元素。

- **1903 测验：Quiz("调制 IM 失真")**  
  由两个或多个音频信号产生的频率（通常是意料之外的频率）之间产生的失真。产生的频率之和与差并不存在于任何原始频率中。

- **1907 测验：Quiz("反平方律")**  
  一种描述一个量与另一个量的平方之间反比关系的数学规则。用通俗的话说，如果一个数字按一定幅度变化，另一个数字也这样做。在音频和声学中，反平方律说，在没有障碍物的开放区域内，距离源每增加一倍，声压就会下降 (6dB)。（这个方程对于试图在户外环境中提供声音的音频工程师非常有用）。

- **1914 测验：Quiz("反相器")**  
  反相器将输入的控制电压乘以 -1。在逻辑反相器的情况下，它反转了高低状态，使得（例如）0 变成 5v，5 变成 0v。这被称为极化器，因为它改变了信号的极性（+ –）。控制反相器结合偏置电压，可以将输出电压调整到所需的范围。例如，如果你使用一个输出电压为 0v 到 +8v 的反相器，并且刚刚对其进行了反相，结果将是 0 到 -8v。由于某些模块作为电压控制放大器只放大正电压，你需要加上 8v 以获得一个整体范围为 0 到 +8v 的倒置（反相）输出。

- **1924 测验：Quiz("反相混合器")**  
  大多数混音器在信号通过混音器时产生相同极性的信号。然而，某些混合器可能会反转信号的极性或“相位”（因为这种设计更简单）；其他混合器可能允许你故意反转信号，以便你可以尝试一些技巧，例如将波形或滤波器模式输出与来自同一振荡器或滤波器的另一个输出反相。

- **1930 测验：Quiz("隔离")**  
  在特定区域内持续声音的过程，因此隔间经常用于在录音室录制人声或乐器，以防止外部声音进入。

- **1939 测验：Quiz("IV 线")**  
  IV 线由 Erthenar 制造，因为它在电缆中点有一个额外的 3.5mm 插头（松散地组装一个人声电缆 1/4 通常是不同合成器模块格式的定义特征之一：3U j 指母头连接器）。

- **1948 测验：Quiz("添加外部时间并创建（或 'Jam'）一个与原始通道相同的新时间码")**  
  用于设备同步。此功能主要用于替换已经退化的代码。

- **1952 测验：Quiz("以复制振动弦的声音")**  
  尽管它已被证明是延迟线。延迟线的输出连接到滤波器——最初是一个单极低通滤波器；改变滤波器对声音的特性有巨大影响，然后回到主输出和延迟线的输入。

- **1959 测验：Quiz("用于多声部并对延迟线的结果进行处理、播放")**  
  通过音阶的第一个音（主音）来识别，例如 C 大调。

- **1962 测验：Quiz("通过侧链由外部信号控制动态")**  
  一种解锁设备使用或...的 key 或代码。例如：Pro Tools 通过物理 USB 密钥授权。

- **1965 测验：Quiz("用于控制其他设备")**  
  大多数键盘乐器配备了 MIDI 跟踪，而不仅仅是“CV”（控制电压）来控制其他设备（以明确它们在模块上运行功能时不会被衰减或被修改）。

- **1977 测验：Quiz("ey")**  
  （没有提到吉他手使用踏板的摆拍机会）。

- **1981 测验：Quiz("每秒")**  
  例如：2000 Hz = 2 kHz。在录音室中最常用于频率范围或数字采样率。

- **1984 测验：Quiz("一旦电平超过阈值就会开始")**  
  所谓的“硬拐点”（Hard knee）是指变化水平不能超过每秒某些伏特数。

- **1986 测验：Quiz("双的，改变")**  
  “硬拐点”具有变化水平滞后。这使用结果在输入端中“滞后”。它有时被称为斜率（slew）或技术上称为“积分器”。

- **2000 测验：Quiz("乐器")**  
  （或带有轻微延迟或合唱效果的配音部分）以混合多个样本（例如：使用两个或多个鼓创建更丰满的声音）。

- **2003 测验：Quiz("产生更丰满的声音")**  
  显示每个音符或表情的基本元素。用音乐谱编写、并在下方带有歌词的领谱。（也称为“和弦图”。）

- **2006 测验：Quiz("旨在被麦克风拾到")**  
  （内容缺失）

- **2008 测验：Quiz("幅度范围")**  
  它们被用于产生如颤音（当控制振荡器时，以及更多）的效果。

- **2011 测验：Quiz("每周期")**  
  （内容缺失）

- **334 测验：Quiz("限制器")**  
  一种压缩器，当音频电平达到阈值时剧烈减少信号的增益，通常用于防止过载和信号峰值。当压缩器的压缩比为 10:1 时，压缩器就有效地变成了限制器。（另见“压缩器”）

- **335 测验：Quiz("线路")**  
  输入“Line In”（线路输入）——设计用于接收线路电平信号的输入。

- **336 测验：Quiz("线路电平")**  
  大多数消费级和低成本专业音频使用参考线路电平和 -10dB（分贝）。最常见的连接器是 RCA（莲花）和 3.5mm，尽管也使用 1/4；信号是“非平衡”的（它使用两根线：信号和地）。在线路标准中，波动 +/- 0.447 伏特的波认为是 -10dB。相比之下，模块合成器中的振荡器是 +/- 5 到 +8 伏特。结果是你需要衰减模块合成器的输出或混音器/录音机的输入来接入信号。同样，你需要大幅提升线路信号以达到模块合成器的标准以便进行处理。

- **337 测验：Quiz("线性 FM")**  
  这通常是频率调制（FM）振荡器的首选输入响应，因为当你改变调制器时结果保持音准。

- **338 测验：Quiz("线性电源")**  
  线性电源设计通过变压器降低较高的输入电压。一般而言，它们在输出功率中产生更少噪声，代价是增加了热量重量（它们并不高效）。我们正在转向混合电源，它将开关与小型线性电源或调节器相结合，以获得两者的优点。

- **最终测验：Quiz("线性 VCA")**  
  线性电压控制放大器（VCA）使用控制电压输入与信号电平输出之间的简单数学关系——对于 50% 的额定控制电压，输出信号为 50% 的输入信号。然而，这并不是我们感知响度的方式；声音必须放大 10 倍才能被感知为大一倍。这使得线性 VCA 在缩放控制电压方面是非常理想的，但对于缩放音频信号可能不那么理想。如果你将具有指数输出的包络发生器连接到线性 VCA，你将得到理想的结果。困惑吗？当包络发生器或 VCA 具有线性和指数响应之间的切换时，这就太棒了。线性混合器类似于线性 VCA：输入电平控制的“一半”等于输出具有相同的电压摆动。再次，这对于改变控制电压是可以的，但对于混合音频信号不是；在这种情况下你需要具有指数控制的混合器。

## 附录 C：C++20 代码

### Quiz 条目

- **quiz: Quiz("线性 VCO")**  
  线性电压控制振荡器（VCO）遵循伏特/赫兹标准；更常见的是指数伏特/八度（v/oct）标准。例外是频率调制（FM），在那种情况下，倾向于使用线性控制电压输入以重建经典的波形，因为它不会改变载波振荡器的基础音高。

- **quiz: Quiz("现场录制")**  
  一段所有音乐家同时演奏且不进行叠录（overdubbing）的录音环节。

- **quiz: Quiz("现场录音室")**  
  录音室的主房间，大多数乐器和歌手在此处表演。之所以被称为现场房间，不仅是因为那里有表演空间，还因为该房间经过了声学处理，能够产生悦耳的现场混响。

- **quiz: Quiz("现场（Live）")**  
  描述具有混响或反射声的空间的术语。在“现场”中，声波是活跃的或“活”的，即实时发生（与之前录音的不同）。

- **quiz: Quiz("本地开启/关闭")**  
  Local On/Off - 一种在播放时控制内部时钟的 MIDI 消息；“Local On”触发内部 MIDI。“Local Off”经常用于在某些配置下防止 MIDI 消息的意外循环，或者当通过另一个控制器注册内部媒体时使用。

- **quiz: Quiz("逻辑函数")**  
  在模块化合成器中，电压本质上是连续的，而门（gate）和触发信号是二元的：开启或关闭；高或低，这与数字电路中的逻辑信号相同。常见的逻辑函数是或门（OR）：如果信号 A 或信号 B 任一为高，则输出门信号（开启）；否则输出低门（关闭）。另一种是与门（AND）：仅当信号 A 和信号 B 都为高时，才输出高门（开启）；否则输出低门（关闭）。这些是组合不同源触发信号的绝佳函数。

- **quiz: Quiz("逻辑")**  
  二进制和布尔逻辑是组合门信号（开启或关闭电压）以创建新输出的方法。逻辑模块的每个部分通常包含 1 到 3 个输入，其中 2 个最常见。如果任何输入端有门信号或“高”信号（例如输入 1 或输入 2 或 3），则存在或门函数并输出门信号。只有当所有输入都看到“高”门信号时（例如输入 1 和输入 2 都有门），与门函数才会输出门信号。函数名称前的“N”字表示“非此函数”，换句话说，非或门（NOR）函数仅在所有输入均为低电平时才输出高信号（此处既不是输入 1 也不是 2）。

- **quiz: Quiz("循环")**  
  广义来说，任何无限重复的音乐或数据都是循环。在音频采样之前，循环是通过循环磁带创建的。今天，循环用于采样中，以便在音符被触发时对音符进行采样，而鼓点循环（drum loops）和其他音乐循环在现代音乐制作中非常常见。  
  A) 波腹（antinode）的另一个术语，指振动拉伸弦或声波中运动位移最大的点。（另请参阅“驻波”）。

- **quiz: Quiz("循环过程")**  
  有时让模块循环或重复其函数的攻击阶段是非常有用的。通常你会在等待音符序列器循环：当它到达序列中的最后一个音符时，如果它能回溯或返回第一个音符并重新开始，将非常有用。带有循环功能的音频录音器在现场表演中也很流行。

- **quiz: Quiz("门 (gate)")**  
  通常这是门或触发处于“关闭”状态的缩写（通常为 0 或 -5 伏，相比之下，“高”或“开启”信号为 +5 伏）。

- **quiz: Quiz("频率振荡器")**  
  此模块产生重复、循环的波形，范围从音频频谱的低端到每个周期几秒甚至几分钟。它们被用于产生效果，如颤音（通过控制信号的响度）、揉音（控制信号的音高）、重复的滤波器哇哇效果、改变振荡器中脉冲波形的脉冲调制等。

- **quiz: Quiz("阻抗")**  
  （缩写为 Z）如描述的 500 欧姆或以下的系统。（小于“高阻抗”）。



# 术语表

## L

### 低频振荡器 (LFO)
一种限制低频电子波形在人类听力范围以下（20 Hz 或以下）的电路。这种低频波形创建一个节奏脉冲，该脉冲由音频信号中的各种参数（如音高或音量）调制。LFO 经常用于采样、合成器和信号处理器，以创建揉音、颤音和相位偏移效果。

### 低通滤波器
一种音频滤波器或设备，它可以衰减特定频率（截止频率）以上的信号，并通过频率低于截止频率的信号。

### 低频 (Lows or Low)
“low frequencies”的缩写，泛指 250 Hz 以下的低频。通常指在音频信号语境下。

### LPF
低通滤波器（LPF）的设计通过其截止频率以下的谐波，并根据它们高于截止频率的程度降低低阶谐波的电平。换句话说，双倍截止频率（八度）意味着截止频率上方一个八度的谐波减少 12 db；截止频率上方两个八度的谐波减少 24dB，依此类推。这是最常用的类型，因为自然声音如音符会逐渐消失为沉默。

### LPG
根据定义，低通滤波器（LPG）是一种低通滤波器，当其控制电压变为零时，其截止频率进入声波范围，导致输入信号通过结合低通滤波器和电压控制放大器进行过滤，而相同的控制电压沿着轨道跟随谐波。

## M

### M2.5
用于安装模块的常见螺纹尺寸。

### M3
用于安装模块的常见螺纹尺寸。

### 磁带
由磁性颗粒涂层的塑料条带，用于录制。

### 磁性
铁对铁的自然吸引。

### MARF
Model 248（任意函数发生器）是用于这些阶段的 MIDI 信号，有时被称为 segments（分段信号）。

### 余量 (Margin)
参见 Headroom。

### 掩蔽 (Masking)
大声音阻碍耳朵听到相似频率的较小声音的特征。

### 主输出 (Master)
1) 控制台或 DAW 的主输出，设置离开控制台时的水平（也称为主推子）。2) 制作复制的原始录制。

### 母带处理
对歌曲或歌曲集进行精调和“润色”的最后步骤。

### 小节 (Measure)
音乐中节拍的组合。（另请参阅“节”）

### 兆
前缀“Mega-”的小缩写，用于兆赫（1,000,000 次，MHz）或兆字节（1,000,000 字节，MB）。

### 仪表
1) 测量并显示信号电平的设备（峰值）。2) 音乐的节奏结构。

### 麦线切换
Mic 的缩写。

### 麦克风输入
控制台或其他设备设计的输入。

### 麦克风电平
麦克风发出的非常低的音频电平。信号在进入控制台之前必须通过放大器增加到线路电平。（参见“线路”、“放大器”）

### 麦克风衰减
麦克风或放大器上的设置，独立的适配器，在进入放大器前降低麦克风信号电平以防止过载。

### 麦克风
将声波转换为电信号的换能器。

### 中侧混音 (M/S)
缩写 M/S) 一种立体并置麦克风放置技术，一个心形图案指向声音，另一个双向麦克风侧向并尽可能靠近第一个麦克风。

### MIDI 时钟
通过 MIDI 传输的时钟信号用于连接的序列器设备保持同步。不要与 MIDI 时间（MTC）混淆，MIDI 时钟与每分钟节拍（BPM）速度绑定，每个四分音符 24 步。

### MIDI 控制器
根据上下文可以指 MIDI 的两个不同元素。1) 通过预编程序列或音乐家的现场表演发送数据以连接设备或软件。2) MIDI 设备上任何较小的控件，分配用于控制声音或表演的特定参数。

### MIDI 接口
将 MIDI 信号转换为计算机数字格式以便存储和使用 MIDI 信号的设备。

### 蓝牙 MIDI
蓝牙低功耗（BLE）是大多数移动设备支持的无线连接规范。BLE（也称为蓝牙 SMART）可以使用不持续传输数据的加速度计（如 MIDI 键盘和控制器）来延长移动设备的电池寿命。

MMA 工作组评估了蓝牙 MIDI 性能（延迟和抖动），并决定了一项基于蓝牙的 MIDI 规范，使不同制造商的产品能够互操作。低功耗蓝牙（BLE）MIDI 规范基于 Apple 的实现，该实现植根于 iOS 和 OS 10.0，因此早期采用者的产品将与行业标准保持兼容。

### MIDI 样本下载 (SDS)
一种添加到 MIDI 中的子协议，用于在乐器、存储单元或声音之间传输数字录制的样本，而无需将其转换为模拟信号。

### MIDI 序列器
一种可以记录和播放 MIDI 数据的设备或软件，能够通过一系列步骤控制 MIDI 乐器的性能。MIDI 序列器可以以板载控制器、键盘或工作站、独立设备或计算机软件的形式存在。

### MIDI Thru 转继盒
一个具有输入端口和多个 MIDI 输出端口的单元，用于将 MIDI 信号中继到多个设备。MIDI 用户通常偏于此作为“链式连接”的替代方案，因为后者会导致 MIDI 信号延迟。

### MIDI Thru
一个输出与输入 MIDI 相同的 MIDI 信号的端口，有效地在不干扰或更改信号的情况下将其中继到另一个设备。（许多设备具有三个 MIDI 端口：In、Out 和 Thru。）

### MIDI 时间码 (MTC)
将 SMPTE 码中的信息翻译为 MIDI 数据，使 MIDI 序列器和连接的设备与 SMPTE 同步（通常与视频相关）。参见（“SMPTE 时间码”。）

### MIDI
音乐乐器数字接口的缩写。MIDI 是连接一个合成器与另一个合成器、以及合成器与计算机的常用语言。虽然它是一种数字语言，但很容易买到一个 MIDI 控制器模块，同时处理事件和 MIDI 时钟以驱动门控序列器。最需要注意的是需要种种连接：传统的 5 脚 DIN 接口，还是 USB 控制器风格的连接。

### 中频
“中频频率”的缩写，指从 250 Hz 到 6000 Hz 的音频频率。在音频信号的“高音、低音和中音”背景下。

### Mini Keys
一些控制器甚至键盘使用的键比典型的钢琴键更小。Mini Keys 是指代这种硬件的常用术语（有时源于此，尽管成本和空间上的节省可能非常显著）。

### 混音
混音或向下混音 - 在母带处理阶段之前，通过将多个音频轨道合并到单个轨道（或双声道立体声轨道）来创建最终混音的过程。这可以包括将模拟磁带的多个通道混合到双轨母带的传统方法，或者使用 DAW 创建数字混音的更现代的方法（通常被称为“渲染”）。

## 附录 A：C++20 代码

### 混合
4. 将音频信号混合成一个复合信号的过程。2. 也可以指将有效音频信号混合回直接信号。

### 混音器
此模块组合音频信号。你可以使用混音器组合音频信号，在这种情况下，你可能使用一个具有指数电平和平立体声控制的混音器，或者控制电压（在这种情况下你可能需要线性控制加上额外的功能来反转和偏移通过它的电压）。

### 模块化
模块化合成器将合成器的主要组件分解为发生器振荡器、音色调制滤波器、振幅塑造 VCA 以及创建包络、颤音等等调制源，这些都是你可以购买和安装的各个独立模块。在这个层面上，所有模块现在都允许你在构建自己的自定义合成器时进行混搭。

### 调制节点
噪声仅当音频信号是页面控制时才存在，我们说你正在调制该参数。例如，低频振荡器 (LFO) 改变滤波器的截止频率以产生波形效果，说 LFO 电压控制放大器 (VCA) 打开声音作为发生器，会导致包络突然出现，然后淡出到静音，就像将“调制”限制为重复动作。因此，我们称这些变化的来源为调制器。

### 调制 (FM)
我们在上面提到了调制的般概念。然而，通常当人们使用调制 (FM) 合成术语时，调制器（振荡器）改变载波（振荡器）的频率以产生丰富的谐波频谱。

### 模块
一个自包含的电路组。在录音室中，模块通常包含在机架中，可以包括放大器、均衡化器、效果、合成器。

### 监听混音
现场和录制信号的混合通常是主混音的独立路径，以便音乐家在表演时听到音乐，然而在录音室中。

### 监听部分
监听部分/监听部分 - 控制台的一个部分，允许工程师听到正在录制的内容而不影响的。

### 监听路径
来自通道的信号路径，允许工程师听正在录制的内容而不影响的。

### 单声道
1. 用于检查质量或避免峰值的目的。2. 录音室中的一个扬声器（通常是对中的一个）用于听音乐，表演时在隔音室或现场室中使用耳机。

### 单声道
1. 单一源或通道（与立体声相反）。2. 每次只播放一个音符的旋律线。3. 描述一次只播放一个音高（或声部）的乐器或合成器。

### 变形
在模块化合成器的语境下，变形是指振荡器可以合并或平地改变其输出波形 - 因此，产生的声音 - 你播放它。这通常是指允许对波形进行实时控制的数字合成器。

### Mother-32
Moog 出品的一种非常流行的模块化合成器。它带有自己的外壳，也可以安装在 Eurack 格式的箱体内。它带有一个锯齿波和脉冲波 VCO、一个 LFO（三角波和方波，Moog 风格）低通或高通滤波器，以及一个 AR 或环境发生器。它是一个可变步进序列器加上一个小八度键盘。什么是小型模块化的是跳线面板，它允许合成器语音进行内部布线的替代路由，并可以连接到外部模块。由于许多此类设备被使用，我使用它作为典型半模块化或“入门”合成器的代表，来讨论如何扩展基础模块化合成器。我有一个关于 Mother-32 的入门介绍即将推出，并将举办有关向此入门系统添加不同模块的每周课程。

### 动圈麦克风
一种通过在磁铁内移动感应线将声波转换为电信号的麦克风。

## 附录 A：C++ 代码 20

### 推子自动化
某些调音台中的一种功能，其中推子通道可以预先编程，在多轨道录制播放期间自动发生（排序）。

### Moog
指高度为 5U（机架单元）或 8.75 英寸（22.2 厘米）的模块，这通常与复古 Moog 标准以及追随其脚步的合成器厂商相关。(Moog.com) 和 Moon Modular。你有时会看到它与“Moog Units”交替使用，后者也指 Moog 标准的 2.125 英寸（5.4 厘米）宽度。由于该标准具有历史性且物理尺寸巨大，一些用户将“5U”作为一种荣誉的额外奖励，以证明他们传统且酷（事实确实如此）。MOTM 曾经短暂流行过一种 50 格式，使用了不同的宽度和连接方式。该格式已停产，但今天仍有很多 MOTM 用户青睐它。

### 多点延迟
延迟的工作原理是将音频放入管道的一端，并当它从另一端传出时将其捕获。多点延迟的意思是：为什么要等待呢？音频快照直接穿过整个管道。让我们在它只经过管道部分区域时就将其捕获。那些假设被捕获的孔被称为“抽头”（taps）——就像在长管上添加的额外水龙头。

### 万用表
一种测试电电压和电阻的小型设备。万用表用于录音室中校准电气系统和排除故障。

### 多路复用器
你经常需要分割或复制信号以发送到一个目的地。这通常通过多路复用器完成（mult”代表多个，你输入一个源，然后插入额外的跳线连接到多个目的地）。

### 多路复用器
多路复用是描述信号路由的技术术语，信号可能会被路由到一个目的地。在合成器模块中，这通常扩展到包括一个输入在多个输出之间切换的可能性。顺序选择器是多路复用器的一种，因为它在多个输入之间进行选择，以决定将哪一个发送到输出（或反之）。有些模块可以在音频速率下执行此操作，使用振荡器在另一种波形的变化之间切换通道，以创建这些波形的复杂混合物。

### 多音性
几个不同的声音、补丁或“音色”（同时）。

### 多轨道录制
也称为跟踪或多轨道录制）录音室的心脏，多轨道录制是将一组声源录制到单独的轨道上的过程，每个轨道都有自己的音频通道，然后组合这些轨道以同时播放。录制可以一次录制一个轨道-仪器（然后组合），也可以在表演者现场演奏时将其录制到单独的轨道上。信号录制在多轨道模拟磁带上，但今天它们作为独立的音频文件数字录制到数字音频工作站（DAW）中。

### 多轨道磁带
一卷磁带，可用于同步存储两个或多个离散信号。

### 乐器接口 (MIDI)
音乐数字接口接口的缩写。MIDI 是连接一个合成器与另一个、以及合成器与计算机的常用语言。它是一种数字语言，用于购买 MIDI CV/Gate（控制电压和门限）转换模块，它可以同时处理用于驱动序列器等设备的事件和 MIDI 时钟。关键在于需要什么类型的连接器：传统的 5 针 DIN 接口，还是 USB 计算机连接。

### 静音
调音台或其他音频设备上的开关，用于关闭输入或输出，或者通过 DAW 虚拟音频控制上的按钮来实现。调音台上的每个通道都有一个开关，可以中断该通道的信号。

### 静音
有时你需要安静或断开信号。静音功能允许你做到这一点。

### 每米纳纳伏特
测量磁带磁强度标准单位。由于每米纳纳伏特数值太大，因此使用它作为替代。

### 窄带噪声
（发生在有限频率范围内的随机能量。）

### 近场
扬声器之间的区域。

### 同轴混音
一种立体声技术，将两个麦克风放置彼此附近以创建立体声像。

### 负反馈
输出中反馈回放大器输入端的部分，它对输出具有阻尼作用。

### 噪底
录制前存在的噪声水平。通常情况下，噪底越低，录制质量越高。目标始终是让噪底保持尽可能低。

### 噪声门限
一种门限，通过在信号低于某些阈值时自动关闭音频通道来减少可听噪声。

### 降噪
任何消除信号中噪声的过程。

### 噪声
描述音频信号中不悦的、非预期的声音。所有电子设备都会产生某种噪声，在安静片段中可以听到嘶嘶声或嗡声。不良连接、接地不当、无线干扰等问题也可能导致信号噪声。工程师也会为了测试目的故意系统中运行噪声。

### 非破坏性编辑
录制系统（最常见于数字音频工作站 DAW）中的一种功能，在执行编辑时原始信号或内容保持完整，允许工程师随时恢复到原始版本。（有时被称为“非线性编辑”。）

### 全指向性
麦克风中，从所有方向拾音。

### 归一化
对音频应用固定增益，使峰值达到最高录制水平。

### 规范化
模块化合成器的力量，你可以让信号按照你喜欢的方式流过系统。当你只想尝试通过“典型”信号流时，这可能非常耗时。因此，一些制造商创建了“半模块化”声音，这些所有典型连接都是预连好的，只需将跳线插入正确的插孔。这些预连连接通常被称为规范化（normal）。例如：内部源可能连接到过滤器之前的调音台通道，如果你向标记为外部输入的插孔插入跳线，这种“规范”就会中断并被你的外部连接取代。

### 陷波滤波器
是一种特殊的滤波器模式，其中角或截止频率设置附近的音频频率或谐波从整个频谱中切除。它是带通滤波器的一种，后者仅允许截止频率附近的谐波。陷波滤波器对声音的影响非常微妙；移动（调制）截止频率会导致声音相位。陷波滤波器通常用于系统以消除不需要的频率。

## 附录 C：C++20 代码

移除有问题的频率，例如地线回路、房间共鸣或谐频谱中另一个烦人的峰值。想象在调音中使用陷波滤波器（notch filter）来挖空声音，为竞争较少的其他声音在谐频谱留留空间，或者仅仅是为了让声音更容易捕捉到某些预期缺失的内容。

### 陷波
窄的音频频率带。

### N/m
测量模拟磁带磁强的标准单位。韦伯（Weber）是磁强单位，但由于它太大，不适用于录音机中的磁性，因此使用纳米韦（nanobels）。每米磁带的纳米韦有效地描述了录制磁带的信号强度。

### 字节 (Nibble)
计算机数据的一半，即 4 位。

### 奈奎斯特频率
在数字录音中，能够正确记录和还原的最高频率，等于采样率的一半。（F）或者对于每秒 44,100 kHz 的常用采样率，奈奎斯特频率为 22,050 kHz，超过此阈值的频率（另见“混叠”）。

### 奈奎斯特率
能够使用和还原给定音频信号或声音的最低采样率，为 18,000 Hz。理论上，模拟信号中的信号至少需要每秒 36,000 Hz——否则信号将被认为采样不足并发生混叠。这本质上是奈奎斯特频率原理。（注意：每秒 44,100 Hz的标准率轻松覆盖了人类听力范围（超过 20,000 Hz）。）

### 八度分频器
创建一个相对于输入声音谐波（“音高”）的新一个或两个八度的模块，以强调低音。也称为次八度或低音功能。

### 八度
八度之间是相互分离的。要演奏一个音准为一个八度的音符，你需要将其音高翻倍；要演奏一个八度，你需要在前面板上带有增加或减少这些电压的开关（针对所有八度）。它们并非完全准确；在切换次八度或次谐波发生器将输入乘以 2 倍或 4 倍后，你通常需要重新调音。



# 术语表

## 离轴
偏离接收麦克风正方的虚线（轴线）。以角度度测量。（例如，直接从麦克风后方传来的声音是离轴 180 度。）

## 偏移时间
1. 触发 MIDI 序列器的 SMPTE 时间。
2. 为了让两卷磁带同步播放音乐的位置差。
3. 信号通过时的偏移 - 将 0v 信号位移至 +10v 信号，以替代信号或设备中的电电流。（另见“阻抗”）。

## 全向 (Omni)
一个表示“所有”的前缀，意味着在所有方向上的信号。

## 振荡器
在其“振荡器”中来回振荡，因为它的输出电压上下变化（振荡）形成重复的模式。这种模式被称为它的波形（例如方波，在高电压和低电压之间切换）；这种模式的重复次数就是它的频率或音高。振荡器的声学仪器是吉他上来回振动的弦，是上下振动的鼓膜。

## 示波器
这是一台显示电压波形的设备。“示波器”可以显示电压的重复模式。这种模式被称为它的波形（例如方波，在高电压和低电压之间切换）；这种模式的重复次数就是它的频率或音高。

## 附录 A：C++20 代码
独立控制其振荡器音高的附加说明，同时仍通过单个滤波器。这对于和弦有效；但当在保持其他音符的同时播放新音符时，效果并不总是那么理想（因为所有音符都会被重新发声）。

## Partial (泛音)
泛音的另一种工作方式。2 组成正弦波的数量之一——构成一个复杂的声音，有助于定义音色。这是合成器产生声音的关键部分：在加法合成中，将许多个泛音组合在一起以创建一个特定的音调。

## Pass Band (通带)
信号会被滤波器“通过”而非被衰减的频率范围。

## Passive Device (无源器件)
一种不产生或控制电学能量的组件（与“有源器件”相反）。在音频应用中，这通常指设计上不充当放大器的设备。例如，有源扬箱是自供电的，而被动扬箱则需要外部放大器来产生声音。（参见“有源器件”）。

## Passive (无源)
意味着不涉及有源（即未连接电源）电子设备——例如通过电位器发送信号，而不是使用放大器和其他电子设备构建一个混音器电路。这种方法既廉价又简单，且不会给信号增加噪声。被动电子设备无法放大来自另一个设备的信号（这意味着它们可能会以不可理想的方式相互作用），并且无法放大、偏移或反转信号。

## Patch Bay (跳线盘)
跳线盘（或称为 Patchback, Patch Field, Patch Panel）—— 一种包含一系列插孔的面板或组件，具有与控制台及工作室组件的大部分输入和输出的连接，用于组织、管理和调节信号流。

## Patch Cable (跳线)
用于连接模块化合成器中不同输入和输出的电缆，用于调节控制电压和音频。该术语源于旧的电话接线板，接线员必须使用电缆物理地连接两个呼叫者。由于模块化格式使用不同的连接器，需要确保跳线线末端的连接器是您所需的尺寸（Eurorack 使用 3.5mm，Su/Moog 单元使用 1/4 英寸，Buchla 控制使用香蕉头）。

## Patch Cord or Patch Cable (跳线)
一种带有插头的绝缘电缆，用于传输音频信号。跳线通常被认为是在跳线盘中建立连接的短电缆（尽管名称如此），然而，跳线可以方便设备之间任何种类的音频连接，长度范围广泛，并且可以包括多种不同类型的连接器。

## Patch Field (跳线区)
一种包含一系列插孔的面板或组件，具有工作室控制台大部分输入和输出的连接，用于组织、管理和调节信号流。

## Patch Librarian (补丁管理器)
一个允许通过 MIDI 在合成器外部存储声音补丁（patches）的计算机程序。

## Patch Panel (配线架)
一种包含一系列插孔的面板或组件，具有控制台及工作室组件的大部分输入和输出的连接，用于组织、管理和调节信号流。

## Patch (补丁)
补丁，是指一系列连接以创建声音的模块的简称为术语，源于使用跳线将模块连接在一起的事实。
1. 使用插入插孔的带插头短电缆在音频系统（如控制台）中路由或重新路由信号。
2. 合成器上的声音序列。

## Path (路径)
信号路径（Signal Path）的缩写，电流流动或可能穿越电路或通过设备的方式。

## PCM (脉冲编码调制)
脉冲编码调制——一种将模拟信号转换为数字代码的过程。这是通过以快速间隔对模拟信号进行采样，然后将其转换为二进制数字作为原始信号的数字表示来实现。速率越高，还原越好。PCM 是数字音频中最常见的 A/D 转换形式。

## PO (相位失真)
相位失真最初由卡西在 80 年代使用——一种合成器系列。它与 FM（频率调制）相关，但具有足够的差异，以避免与当时雅马哈合成器使用的专利产生冲突。巧妙地，它很好地模拟了许多“模拟”效果，包括共振滤波器的声音。

## Peak (峰值)
一种 EQ 滤波器，用于增强或切除音频信号中的中间（中心）频率，与高通或低通滤波器不同。（不要与模拟峰值混淆）。

## Meter (电表)
电表检测波形的绝对值——而不是 RMS（均方值）（参见“峰值”、“均方根”、“RMS 电表”）。

## Peak to Peak Value (峰峰值)
测量音频信号中正峰和负峰之间的总振幅。对于正弦波，等于峰值（参见“峰值”）。

## Peak Value (峰值电平)
每个值（也称为峰值电平）——波形在任何时刻的最大正或负值（振幅）的测量。在音频中，它在视觉上显示为波形上方或下方最远的点。

## Pedal Board (踏板板)
一个带有几个脚踏和效果器的板子，吉他手可以激活或取消它们。

## Phantom Power (幻象电源)
幻象电源，用于为电容麦克风提供直流电压并消除对外部电源的需求系统。

## Phase Addition (相位叠加)
当波形相位相似时发生的能量增加，导致音量增大。

## Phase Cancellation (相位抵消)
相位叠加的反面，这是当相似波形相反（偏移 180 度）时发生的能量减少，结果是完全静音。

## Phase Distortion Synthesis (相位失真合成)
相位失真合成最初在 80 年代产生——一种合成器系列。它与 FM（频率调制）相关，但具有足够的差异，以避免与当时雅马哈合成器使用的专利产生冲突。巧妙地，它很好地模拟了许多“模拟”效果，包括共振滤波器的声音。

## Phase Distortion (相位失真)
信号相位偏移引起的声音变化。

## Phase Lock (相位锁定)
任何通过纠正相位差来帮助同步信号的过程。例如，在模拟带机中，相位锁定通过检测播放中的相位差并调整速度来保持机器同步。

## Phase Locked Loop (锁相环)
相位环是一种试图匹配频率的振荡器——更重要的是，信号的分频或倍频。这主要用于创建一个是输入时钟 2、4、8 或更多倍的输出时钟。

## Phase Modulation (相位调制)
一些人认为这是严谨上正确的术语频率调制（FM），因为携带载波变快或变慢以改变其频率变高变低，等同于提前或延迟波形正常播放的位置（相位）。

## Phase Reversal (相位反转)
一种电路变化，以使波形偏移 180 度。

## Phase Shift (相位偏移)
引入音频信号的延迟，以度为单位。

## Phase Shifter (移相器)
这种效果将信号分成两个副本。一个副本通过“全通滤波器”，该滤波器不会像低通或高通滤波器那样衰减任何原始谐波，但会改变信号的相位，导致谐波根据频率相对于原始信号产生不同量的相位偏移。将这两个副本混合在一起。

## 附录 A：C++20 代码
原始声音中不同的谐波分量相互抵消（参见“相位”），导致陷波滤波器效应。移相器的每个“阶段”全通滤波器部分都会创建一个这样的陷波。阶段越多，陷波越密，效果也越深。

## PLL (锁相环)
PLL - 用于通过纠正相位差来帮助同步信号或设备的任何过程。例如，在模拟磁带机中，相位锁定通过感应相位差来消除相位差，从而帮助多台机器保持同步。在合成器中，相位锁定是一种音调发生器，使其根据另一个发生器的信号相位来创建自己的波形。锁相环（PLL）是电子设备 `c` 函数中使用的参考信号。

## Phase (相位)
两个相似波形之间时间差的测量（以度为单位）。波形的一个周期被认为是 360 度，就像圆一样。你在圆上移动（或穿过波形）的距离可以定义为相位。例如，如果你处于波形周期的四分之一，你的相位就是 90°。

## Phase Change (相位变化)
通过改变音频的相位移然后将其与直接信号混合而产生的效果。

## Unit (单元)
*待补充内容*

## Phone Plug (电话插头)
一种直径为 1/4 英寸、长度为 1/4 英寸的插头（或配套插座），用于连接音频。单/立体声系统上的常用音频连接器，中心销脚作为一个连接，外壳作为第二个连接。

## Physical Modeling (物理建模)
一种（通常是数字的）合成方法，重建声学元件的元素——例如振动弦或共鸣体（如吉他鼓体和弦），并将它们连接起来以产生声音。有许多可用模块可以创建它们的声音。

## Pickup Pattern (拾音模式)
麦克风前面或周围均匀拾音的区域形状。此术语可与“极性图”互换，但极性图提供了更多关于麦克风灵敏度的详细信息。（参见“极性图”）。

## Pickup (拾音器)
1. 电吉他或其他乐器上的设备，根据弦的运动产生音频信号。
2. 参见“接触式拾音器”。

## Pinch Roller (压带轮)
录音机上的橡胶（或塑料）部件，将磁带夹在它和转动轴之间，允许转动轴带动磁带。

## Ping-Pong Modulation (乒乓调制)
将多个轨道合并并混合到一条或两条轨道（单声道或立体声）上的技术。这可以在实时进行，也可以通过通道播放轨道并录制到单独的轨道上。

## 附录 C：C++20 代码
或通过数字工作站进行。混叠（Bouncing）以前经常用于释放相同的轨道进行录制，在轨道几乎无限制的数字工作站中，这种做法基本上已经过时了。今天通常混叠轨道是为了创建一个初步的或最终的-

### Pink Noise (粉红噪声)
一种类似于白噪声的噪声信号，包含所有可听频率，每个倍频内的能量相等，而不是所有频带。工程师使用粉红噪声作为校准音频设备的工具。（参见“白噪声”。）噪声是一种随机的无音高信号，以某些速率听起来像嘶嘶声或风声。粉红噪声每个倍频的能量（声级）相等。由于高倍频的频率是其覆盖倍频的两倍，在更宽的频率范围内，粉红噪声具有更多的电子感，质量更大且高频更少，尤其是与白噪声相比，白噪声每赫兹（频率）的能量相等，听起来非常明亮。

### Pitch Bend (音弯)
合成器、键盘或控制器上的机制，可以使音符的音高发生小幅上升或下降。

### Pitch-to-Voltage Converter (音高转电压转换器)
一种检测音频波形频率并转换为控制电压的设备，该电压反过来驱动振荡器产生相同频率的音高。

### Pitch-to-MIDI Converter (音高转 MIDI 转换器)
一种检测模拟音频信号中音高并将其转换为 MIDI 信息的设备。（也称为“音频转 MIDI 转换器”。）

### Pitch (音高)
1. 耳对频率的感知（较高或较低的音调）。
2. 磁带传输设备上的控制，可略微增加或降低速度，改变音乐的音高和时间。

### Plate Reverb (板混响)
一种通过变声器将振动通过金属板发送扬声器驱动器的执行人工混响设备。物理板混响现在被认为是一种复古的人工混响，现在大多数混响效果通过插件或混响单元进行模拟。

### Playback Head (播放头)
一种将记录在磁带上的磁通量转换为播放用音频信号的变声器。

### Playback Mode (播放模式)
控制台上的某种配置，允许播放之前记录在磁带上或通过监听调音器录制的信号。

### Playback (播放)
1. 录制音频的再现。
2. 在电影视频制作中，在表演者/音乐家上方播放录制的扬声器，可以随时间进行-

### Playlist (播放列表)
1. 大多数媒体播放器上用户定义的歌曲选择。

### PLL (锁相环)
锁相环本质上是一个试图匹配另一个信号频率的振荡器。

## 附录 A：C++20 代码
原始声音中不同的谐波分量相互抵消（参见“相位”），导致陷波滤波器效应。移相器的每个“阶段”全通滤波器部分都会创建一个这样的陷波。阶段越多，陷波越密，效果也越深。

## Potentiometer (电位器)
（简称 "Pot"）通常被认为是“旋钮”的雅俗，但电位器本质上是任何通过改变变化量来控制输入或输出电压的机制（例如，信号的左/右平移、音量控制或发送到辅助发送端或总线的信号量）。电位器可以是旋钮或推子，这意味着许多工程师将推子和旋钮统称为“pots”。

## Power Amplifier (功率放大器)
（简称 "Power Amp"）一种放大电平信号以驱动一个或多个扬声器的设备。（参见“线路电平”。）

## Power Distribution (电源分配)
“这块简单的电路板接收你的模块化系统的电源输出，创建多个副本，并将其路由到连接你各个模块的连接器上。”



- quiz：Quiz("PPQN", "当你将时钟信号（门控信号或其他电脉冲）沿模块化开关传输并按步骤序列时，了解时钟脉冲的速度是有好处的。这通常定义为每个四分音符有多少脉冲——简称为 PGO 或 PPQN。如果锁定在每个四分音符后发生，则时钟为 SPQN；在 SYN（一种基于 DIN 的流行电气连接标准）和 MIDI 档口的情况下，标准是 24 PPQN。这意味着主脉冲可以创建一个 8 分音符的三连音（8 x.）。")

- quiz：Quiz("前发送", "在输入模块上的一个开关，用于决定信号中的发送控制是在主信道推子之前还是之后（“推子前”、“推子后”）。")

- quiz：Quiz("预均衡", "在制作过程中对高频进行增强，以使音频信号保持在噪声底之上。")

- quiz：Quiz("预延迟", "指一种发送位置或设置，将发送推子置于信号路径中。推子前发送意味着推子不会影响原始干声（或延迟）与混响早期反射之间的时间量（延迟）。此功能也可用于创建不自然的效果。")

- 回声（Echo），一种压缩压缩（压缩）效果，该声音（或其部分）在声音本身之前被听到，通常由于数字格式的不一致导致。录制成品中也会出现类型的预回声，在黑胶唱片上也是由于低电平泄漏，以及由于纹槽的物理差异/或变形，产生了一个需要额外信号来解决的非预期问题。在某些情况下，它也可以用作特殊效果使用（不要与“反向回声”混淆）。

- quiz：Quiz("推子前监听 (PFL)", "调音台或 DAW 通道条上的一个功能，允许通道在通道衰减（通常在通道衰减之前）被听到。")

- quiz：Quiz("前置放大器 Preamp", "一种低噪声放大器，用于接收低电平信号（例如麦克风）并在发送到调音台之前将其提升到正常线路电平。")

- quiz：Quiz("优先效应 (哈斯效应)", "简单来说，这是人类听觉中的一个因素，我们通过时间而不是速度来感知声音的来源。在研究中，赫尔穆特·哈斯（Helmut Haas）确定，到达我们耳朵的第一声波帮助大脑判断来源在哪里，而不是来自另一个源的反射或复制。声音的反射必须比原始声音低 5db，或延迟超过 30ms（在此处我们就可以在不受附近表面的反射和混响融合的情况下区分原始声源。理解哈斯效应是指扬声器的时间延迟，以匹配来自源的初始声波。")

- quiz：Quiz("精密加法", "合成器对音高控制中的意外变化非常敏感，任何错误都可能导致振荡器跑调。因此，每当你在模块合成器中添加音高控制电压时，你都应该使用精密加法器，精确地加上音高电压而不引入误差。普通的调音台可能会产生误差。")

- quiz：Quiz("预混", "1) 在其他轨道的范围内，通过将轨道路由到辅助通道，将一组轨道作为混合组进行混合的过程。通过跳混（bounce）合并轨道是预混的一种形式，但不一定是预录制的。（参见“跳混”）2) 电影后期制作中的重要部分，其中将音频混合以与视频组合在一起的过程。")

- quiz：Quiz("存在频率", "4 khz 到 6 khz 之间的音频频率范围")

- quiz：Quiz("存在感", "1) 在放大中，对中高频的增强会导致声音或乐器突出，营造出源更有“存在感”的印象，仿佛就在听者旁边。参见 Room.")

- quiz：Quiz("预设", "合成器、信号或麦克风上的出厂编程参数集，麦克风的振膜在对抗麦克风壳内部正常或受控的气压时响应入射声波压力。这种设计使得振膜无论方向如何都会产生压力，使其具有全向拾音模式。（参见“全向模式”。")

- quiz：Quiz("压力灵敏度 (触后)", "某些键盘上的功能，在已按下的按键上增加压力可以激活如 MIDI 等控制信号，然后将其转换为你可以使用的控制电压来表达音符，例如添加颤音或打开滤波器宽度。单声道触后无论你按下哪个键，整个键盘只产生一个压力值；多声道触后为每个单独的键产生信号。")

- quiz：Quiz("压力区域麦克风 (边界麦克风)", "放置在平坦表面（或边界）上的全向麦克风，有效地创建一个半全向模式，同时消除了反射声带来的相位问题风险。一种流行的麦克风是 Crown Audio 的商标 Zone 麦克风 (PZM)。")

- quiz：Quiz("压力梯度麦克风", "(也称为“速度麦克风”）一种从正面和背面引入相位的麦克风，振膜运动是由正面的压力差引起的。这创建了双向或“数字8字”拾音（参见“双向模式”。")

- quiz：Quiz("Pro Tools", "Avid 的数字音频工作站 (DAW) 商标，在专业录音室是行业标准。")

- quiz：Quiz("制作人", "在音乐中，制作人是音频录制的导演；负责在预算范围内获得所需质量最终产品的人。")

- quiz：Quiz("制作室", "广义上，任何用于艺术、电影/视频/动画或后期制作的区域。在音频语境下，制作室实际上是一个专门为商业广告和广播节目将预录的风声和效果与新录制的对话进行组装和混合的录音室。")

- quiz：Quiz("制作", "1) 制作音乐的活动。2) 描述录制质量——录制和混合过程中制作决策的最终结果。")

- quiz：Quiz("程序更改", "一种告诉接收设备更改预设的 MIDI 消息。")

## 附录 C：+20 代码

3092 quiz：Quiz("可编程的", "“允许用户更改参数，特别是由计算机控制的设备”。")

3093 quiz：Quiz("提示词", "“一组供用户遵循的指令，显示在计算机屏幕上”。")

3095 quiz：Quiz("协议", "“在数字和信息技术中，一组规定以标准格式对数据进行结构化和传输的规则以便所有相关的设备都能正确地解释数据”。")

3099 quiz：Quiz("近接效应", "“当麦克风离声源越近时，麦克风对低频频率输出的自然增强”。")

3101 quiz：Quiz("心理声学", "“研究人类如何感知和响应声音，不仅是在解释物理声波的背景下，还考虑了心理和情感因素。研究人类如何感知和响应声音，不仅是在解释物理声波的背景下，还考虑了心理和情感因素。这一科学分支有助于音频工程师理解大脑如何解释声音和频率”。")

3106 quiz：Quiz("转子 (Puck)", "任何圆形的金属、纤维、橡胶等部件，通过动力源驱动物体。录音室中的常见例子是旋转 Leslie 扬声器内部。")

3109 quiz：Quiz("脉冲编码调制 (PCM)", "“一种将模拟信号转换为数字代码的过程。这是通过定期采样对模拟信号的幅度进行采样，将其转换为二进制数作为原始信号的数字表示。采样率越高，数字制作效果越好。PCM 是数字音频中最常见的 A/D 转换形式”。")

3115 quiz：Quiz("每四分之一脉冲")

3124 quiz：Quiz("脉宽调制 (PWM)", "绝大多数输出方波的振荡器都有额外的控制电压，用于设置“方”波顶部部分的宽度（显然，顶部部分越宽，底部部分就越窄，反之亦然）。改变产生的脉冲波宽度的行为会产生某种多普勒效应，通过低频振荡器改变脉冲宽度——例如，听起来可能像一对未调谐的振荡器。使用控制电压改变脉冲波形状的过程，本质上是在方波和脉冲波之间切换。这种效果可以产生更丰富的音色，使声音听起来更厚实、更有感，或者赋予数字声音更多的模拟特性”。")

## 附录 A：++20 代码

3135 quiz：Quiz("脉冲 (Pulse)", "在模块化合成器中有几种不同的含义。当我们改变方波的形状使其中一部分比另一部分窄时，它被称为脉冲波（见下文的脉冲波调制）。此外，用于序列器等的时钟信号的窄门或触发信号通常被称为脉冲。1) 音乐中基于节奏的稳定节拍，无论是可听的还是感知的。2) 一种通常由合成器创建和调制的声波，其特征是幅度具有像方波那样的剧剧上升和下降，但峰值比谷值短，使波具有脉冲感。也称为“脉冲波”。")

3144 quiz：Quiz("抽吸与呼吸 (Pumping and Breeding)", "“在工作室中，当压缩器快速压缩和释放声音时产生电平变化的效果。‘抽吸’是指压缩发生后声平的可听性增加；‘呼吸’是指人声的类似效果——在吸气时提高信号量。抽吸和呼吸是压缩或过度压缩的标志，通常是不受欢迎的，尽管一些工程师和音乐师偶尔会使用它来营造艺术效果”。")

3152 quiz：Quiz("点入点出记录 (Punch in/Punch Out Recording)", "“在磁带或 DAW 回放上激活和取消执行/演奏/演唱者的功能的过程。这可以作为一种快速叠加录音的方法，也可以作为回到特定段落而无需从音轨重新开始的方法”。")

3157 quiz：Quiz("纯音", "“仅由基频组成而没有泛音或谐波的频率，在图上表示为简单的波形”。")

3159 quiz：Quiz("PVC", "PVC 代表音高转换 (pitch conversion)。在尝试使用键盘以外的微型（触摸板）设备来演奏电压控制合成器时，有些人设计了模块或其他设备，尝试检测音频信号的音高——例如来自吉他、笛子或歌手的声音，并将音高转换为相应的电压，与信号结合驱动 VCO。")

3165 quiz：Quiz("PWM", "绝大多数输出方波形状的振荡器都有额外的电压输入，用于设置“方”波顶部部分的宽度（显然，顶部部分越宽，底部部分就越窄，反之亦然）。改变产生的脉冲波宽度的行为会产生某种多普勒效应，通过低频振荡器改变脉冲宽度——例如，听起来可能像一对未调谐的振荡器。使用控制电压改变脉冲波的过程，本质上是在方波和脉冲冲之间之间。这种这种可以产生更丰富的音色，使声音听起来更厚实、更有感，或者赋予数字声音更多的模拟特性”。")

3172 quiz：Quiz("PZM", "Crown 压力麦克风的缩写。（另见‘边界麦克风’）。")

3175 quiz：Quiz("Q -（也称为 Q Factor）", "代表“品质因”，定义了将被均衡器影响的频率带宽。在滤波器中，当你增加共振（反馈）时，滤波器截止频率周围会形成峰值。共振越高，这个峰值越窄。因此，过去曾使用音频术语来指共振量，尽管现在很少听到这个词了”。")

380 quiz：Quiz("四声道 (Quadrphonic)", "“一种很少使用的四声道系统，其通道被指定为左前、左后、右前、右后，以便从房间的角落传输声音。四声道是今天环绕声系统的前身。（你可以定义波形的一个完整周期为 360 度，类似于四分之一。这个圆周的四分之一移动到波形四分之一处的地点是 90°。一种正交关系”。")

quiz: Quiz：Quiz("量化失真 (Quantization Distortion)", "量化失真/量化误差：由于大量模拟波被舍入到最近的数字数量，导致模拟信号与其采样部分之间有效的‘翻译误差’。这通常会导致声音中产生额外的频率，通常被听为噪声。")

: Quiz：Quiz("量化噪声 (Quantization Noise)", "由于量化误差而在信号中产生的调制。")

: Quiz：Quiz("1) ", "1) 在数字音乐中，将节奏对齐时间线的过程，通过移动音符到精确位置来调整性能被称为‘舍入’音符到最近的定义频率。2) 在...中将模拟信号转换为较小阶梯集合（数字数量）。")

quiz: Quiz：Quiz("量化器 (Quantizer)", "量化器通过将输入电压自动纠正到最近的所需目标（即对应于半音或其他音符的电压），通常是独立的模块。")

quiz: Quiz：Quiz("机架耳朵 (Rack Ears)", "机架架/机架法通过螺栓固定安装模块的支架可能会划伤模块的前面板。这对于一个没有划痕的旧模块来说划得更严重。所以买一袋塑料垫圈并放在螺丝或螺栓头后面，以消除另一个让人不想买你旧模块的理由。")

# 附录 A: +20 代码

quiz: Quiz("单元 (Rack Unit)", "架式设备通常遵循一组标准尺寸，包括宽度 19 英寸（48.3厘米），以及“机单元”（或 U 或 unit 的缩写），每个 U 为 1.75 英寸（4.4厘米）。许多常见的模块合成器格式遵循机单元来标准化模块高度 - 例如 3U（3 x 1.75 = 5.25）或 13.3U。对于 Eurorack，Buchla 和 Serge 为 4U，常见的 Mo 为 5U（有时被称为 Mu Unit）。")

quiz: Quiz("辐射模式", "扬声器覆盖范围的图形描述。这与麦克风的模式相似，不同之处在于模式描述的是声音到达麦克风的区域，而模式描述的是声音如何从扬声器扩散出来）。")

quiz: Quiz("辐射", "扬声器覆盖的角度和模式。")

quiz: Quiz("斜坡 (Ramp)", "斜坡是指任何稳定上升或下降的电压；它在达到目标电压时通常会重置，并切换到锯齿振荡器波形有时被称为斜坡。有时，包络生成器的各个阶段也被斜坡；它从 0 上升到最大水平（例如攻击阶段为 5V），然后从此峰值下降到维持阶段的维持水平。")

quiz: Quiz("随机存储器 (RAM)")

quiz: Quiz("随机音符生成器", "一种以特定速率产生音高的设备，用于合成器中。")

quiz: Quiz("随机", "模块系统内部移动的大电压在变化上都是非常随机的：音频速率或低频振荡器的重复波形；包络生成器的上升和下降电压。然而，将这些随机漂变的电压应用于从稳定的频率变化到变化的音量或滤波器等一切也是很有用的。噪声是一种音频速率随机信号。")

quiz: Quiz("说唱 (Rap)", "在音乐或打击乐表演中执行节奏部分。")

quiz: Quiz("稀疏 (Rarefaction)", "通过声波波谷空气粒子密度降低；在“压缩与稀疏”的语下，它是压缩的反面。（参见“压缩”。")

quiz: Quiz("棘轮 (Ratchet)", "这是使用序列器时的一种技巧，序列中的一个阶段可能会被快速触发多次，而不仅仅是在进入该阶段时触发一次。例如，结果可能是出现十六个音符的缓冲（而不是是指一个或多个阶段的速度或频率）。")

quiz: Quiz("速率 (Rate)", "这个词有时用于指代低频振荡器或类似的重复函数的速度或频率（如序列器的时钟）。")

# 附录 C: C++20 代码

quiz: Quiz("额定负载阻抗", "输入阻抗，或设备输入对供电设备电流流的阻碍。")

quiz: Quiz("RCA 插头", "（也称为花朵插头 Phono Plug）一种在立体声系统中常见的音频连接器，具有中心针脚作为一个连接，外外壳作为第二个连接。")

quiz: Quiz("只读存储器 (ROM)", "一种无法被用户擦除或重新编程的数据存储类型。如今音视频系统中最常见的 ROM 形式是光存储介质（例如，CD、DVD、CD-ROM 和 DVD-ROM）。")

quiz: Quiz("读取 (Read)", "从存储设备中检索信息；在数字音频中，指数字信号的再现。")

quiz: Quiz("Reason (软件)", "来自 Propeller Software 的流行音乐软件。它提供了硬件合成器、信号处理器的数字设备；Reason 可以作为一个音乐工作室工作，或者作为一组可以现场或与其他序列软件播放的虚拟乐器。")

quiz: Quiz("更换电容 (Recapping)", "电子元件会老化。电容类型，特别是电解和钽电容，通常位于电源部分 - 最容易随时间退化；电解容器的最大安全寿命为 25 年。因此，复古合成器会按照顺序进行“更换电容”（更换年龄敏感型电容）。")

quiz: Quiz("录音头", "模拟录带机上的设备，将电流变化转换为磁能；磁场的变化将音频信号记录在磁头上。")

quiz: Quiz("录音电平 (Record Level)", "录带机上的控制按钮，决定记录在磁带上的磁通量，或 DAW 决定记录到声音文件中的数字信号电平。")

quiz: Quiz("录音监听 (Record Monitor)", "在某些磁带上，一个开关位置，允许 VU 表和录带机电路的声音输出来监控进入录带机的输入信号。")

quiz: Quiz("录音准备 (Record Ready)", "多轨道录带机的状态控制，当录带机录音功能激活时，指定的轨道将被记录。")

quiz: Quiz("录音总线 (Record Bus)", "一种将控制台通道的混合信号发送到多轨道录音机或 DAW 的总线。（参见“总线”。")

quiz: Quiz("录音课程 (Record Session)", "在工作室录制音乐的时间段。")

quiz: Quiz("整流器 (Rectifier)", "使电压保持正或负的电路。在电源中，它用于消除交流电压的负部分，或防止你反插模块的电源连接器。作为模块，半波整流器仅通过正电压并将任何负电压替换为正；这有效地使许多简单波形（如三角波和正弦波）的频率翻倍。")

quiz: Quiz("红噪声", "也称为棕噪声，技术上它是功率密度（频谱响度）随频率增加而每八度下降 6 dB 的噪声。它具有沉重的低音，类似于远处的海浪。它也可以用于变化的控制信号。")

quiz: Quiz("真实 (Real)", "1) 磁带卷绕在轴和边缘上；2) 有时称为“演示带”（demo reel），是展示音乐家、音频工程师或其他专业人士能力的音频视频编译。与用于单曲歌曲的 Demo 不同，演示带旨在推广产品。")

quiz: Quiz("参考电平 (Reference Level)", "1) 一个基准音量，用于测量高于或低于 db 分。")

quiz: Quiz("参考音 (Reference Tone)", "一种单频音（通常为 1000 Hz），用于设置参考电平。（参见“音频”。")

quiz: Quiz("反射声 (Reflected Sound)", "到达麦克风或周围表面的声音。")

quiz: Quiz("反射 (Reflection)", "在声学中，声波在平面的边界，与吸收相反。反射对我们的感知有很大影响；来自远处反射声被感知为回声，而成千上万的反射产生了混响。（参见“吸收”、“回声”、“混响”。")

quiz: Quiz("再生 (Regeneration)", "再生在合成器中有几种含义，都指反馈。音频单元可以从输出反馈回输入，导致延迟再次重复；这有时被称为再生。")

quiz: Quiz("稳压电源 (Regulated Power Supply)", "为电子设备供电的设备，当设备开启或电源线电压变化时输出电压不会波动。稳压电源旨在保护敏感电子设备免受破坏性浪涌。")

quiz: Quiz("继电器 (Relay)", "一种电磁开关，在应用控制电压时连接或断开终端。")

quiz: Quiz("释放时间 (Release Time)", "在动态信号处理器中，当输入信号超过设计的阈值时，输出返回原始水平的时间。")



# Quiz 术语表

## 释放
quiz: Quiz("释放 (Release)", "这指的是包络的最后一个阶段，通常下降到 0 伏，导致静音。它通常用于攻击/释放（AR）或攻击/衰减/维持/释放（ADSR）包络")

## 远程
quiz: Quiz("远程 Remote", "1) 一种无线控制另一个设备功能的设备。2) 描述现场录音，与在录音室录音相对。")

## 重置
quiz: Quiz("重置 Reset", "模块上的 Reset 输入接受触发或信号，并告诉模块回到其之前正在执行的状态。对于时钟而言，这意味着下一个时钟是你在分频中应该计数的第一个时钟（完整定义中更为如此）。对于序列器而言，这意味着回到到起始阶段（attack）的开始。对于门延迟而言，这意味着重置延迟计时器。")

## 剩磁
quiz: Quiz("剩磁 Residual Magnetization", "移除磁力后在磁性材料中留留的磁量。剩磁会在磁带中积累，部分擦除磁带。")

## 残余噪声
quiz: Quiz("残余噪声 Residual Noise", "消磁后录音磁带上的噪声水平。")

## 电阻
quiz: Quiz("电阻 Resistance", "电流相对于电流函数的基准位置，用于电路内调节电流流量。")

## 共振
在某些频率处更多。共振原理是声学乐器的关键元素；例如，吉他或小提琴的空腔设计为与弦的振产生共振。共振在空间的声学设计中起着作用，并在开发投影声音的人声技巧中发挥作用。滤波器的输出被反馈到其输入，导致截止频率或离频附近的谐波增强。可听到的结果类似于在具有共振的房间里播放声音——产生特定频率的共感、增强性回声或振动。因此，“共振”一词通常用于指反馈回路的反馈机制。

## 共振频率
quiz: Quiz("共振频率 Resonant Frequency", "物体自然产生共振的频率。")

## 共振
quiz: Quiz("共振 Resonate", "以共振频率振动。也指声源停止后导致声音持续的回响。这种持续的声音是由于附近物体的共感共振引起的。")

## 共振器
quiz: Quiz("共振器 Resonator", "许多乐器包含一个箱体或声腔，它会以共感的方式振动，或增强一个或多个频率。为了在模块系统中模拟这种效果，你可以获得专用滤波器或均衡频率，每个通常位于窄带内。这是合成真实世界空间或空间的秘密之一。")

## 混响
quiz: Quiz("混响 Reverb (Reverberation)", "1) Reverberation 的缩写。2) 一种为信号创建人工混响的信号处理器或插件。")

quiz: Quiz("混响 Reverb", "reverberation 的缩写。这是一种模拟在房间内效果的效果设备，在房间里你可以听到原始声音在墙壁上反射多次，在声音的洗涤中回荡，直到最终衰减为沉默。混响可以极大增强合成器的声音，为原本可能很单调的较少模块增加亮度和维度。甚至有允许你控制其参数的效果（其中混响是最著名的）；许多效果使用外部混响效果。")

## 混响场
quiz: Quiz("混响场 Reverb Field", "描述距离源足够远，以至于回响晚于直达声的空间。")

## 混响室
quiz: Quiz("混响室 Reverberation Chamber", "用于模拟房间反射和混响体积的设备；或者混响如何达到峰值水平及其衰减率。")

## 混响包络
quiz: Quiz("混响包络 Reverberation Envelope", "声源停止后空间的持续性，由于离散的回声到达耳朵的时间间隔如此紧密，导致耳朵无法区分它们。")

## 射频干扰
quiz: Quiz("射频干扰 RF Interference", "由于 RF 信号的存在而引入电子设备、电路和音频系统的意外噪声。系统中的 RF 干扰会导致嗡嗡声、滋滋声、静电或无线无线传输。")

## 射频信号
quiz: Quiz("射频信号 RF Signals", "RF Signals（或 RF）——无线电频率信号的缩写，携带无线无线和电视信号的电磁波。绝大多数 RF 信号的频率高于 100 kHz。")

## 节奏组
quiz: Quiz("节奏组 Rhythm Section", "乐队或合唱中的乐器负责演奏节奏型而非旋律。在当代音乐中，节奏系统由鼓和贝斯组成，还结合了打击乐、钢琴/键盘和吉他的某些组合。")

## 丝带控制器
quiz: Quiz("丝带控制器 Ribbon Controller", "这是一条长条，能够测量你使用的长度位置以及按下它时使用的压力。它可以作为替代控制器或音高弯音控制器，通过位置检测音高。较短的版本也作为合成器上的替代控制器出现，例如雅马哈 CS-80。")

## 丝带麦克风
quiz: Quiz("丝带麦克风 Ribbon Microphone", "一种通过磁极设置的导电丝带将声波转换为电信号的麦克风。丝带麦克风对丝带的两侧都有响应，形成双向或 8 字形图案。")

## 乐句
quiz: Quiz("乐句 Riff", "曲中反复播放的简短旋律，通常在歌词行之间有变化")

## 房间回声处理
quiz: Quiz("房间回声处理 Ringing Out a Room", "识别并补偿房间内问题频率以优化该现场音频的过程，这是通过向扬声器发送粉红噪声、增大麦克风量直到产生反馈，并使用 EQ 挖除干扰频率来实现。")

## 上升时间
quiz: Quiz("上升时间 Rise Time", "音频波形突然增加到较高幅值的速率。")

## RMS 表
quiz: Quiz("RMS 表 RMS Meter", "一种识别并响应有效平均 RMS 电平和以及 AC 波形平均值的表，而不是峰值电平。（参见‘均方根’、‘峰值表’）。")

## 衰减
quiz: Quiz("衰减 Roll Off", "当信号频率离开截止频率时信号电平降低，特别是当速率缓慢时。")

## 房间均衡
quiz: Quiz("房间均衡 Room Equalization", "在现场音频中，插入均衡器以补偿由房间声学引起的频率变化。")

## 房间声音
quiz: Quiz("房间声音 Room Sound", "房间的自然氛围，包括混响和背景噪声。")

## 房间色调
quiz: Quiz("房间色调 Room Tone", "房间内发生的背景噪声。在电影和电视录制中，用于保持连续性。")

## 均方根
quiz: Quiz("均方根 Root Mean Square", "AC 波形的有效平均值。")

## 旋转头
quiz: Quiz("旋转头 Rotating Head", "带有两个或多个间隙并以角度旋转的圆形头")

## 低频噪声
quiz: Quiz("低频噪声 Rumble", "通常由不规则表面引起的噪声")

## 节奏轨道
quiz: Quiz("节奏轨道 Rhythm Tracks", "音乐制作中的节奏录制。")

---

# 附录 A：C++20 代码

## 采样保持
quiz: Quiz("采样保持 Sample & Hold", "采样保持器（S/H）有两个输入：一个被采样的信号，和一个指示何时采样（存储）并输出第一个输入的触发输入。这种稳定电压将保持直到收到新的触发。采样保持通常与创建随机电压有关。为了这样做，噪声输入主输入，每当收到触发时，输入处的电压是某个随机值，然后发送到输出。")

## S/PDF
quiz: Quiz("S/PDF", "Sony/Philips 数字接口的缩写")

## 采样率转换
quiz: Quiz("采样率转换 Sample Rate Conversion", "将一种采样率录制的数字音频转换为另一种采样率，而不转换为模拟信号。")

## 采样率
quiz: Quiz("采样率 Sample Rate", "这是数字音频的规格。重建声音的测量值是如何记录或播放的。该音频文件的带宽（对应可产生的最高频率）小于采样速度的一半。在数字录制中，每秒采样次数。采样率越高，声音复制越真实，产生的频率越高。")

## 采样
quiz: Quiz("采样 Sample", "1 在数字录制中，给定时刻波形水平的数值测量。模拟音乐通过快速连续的样本数字化表示。2) 为了数字化复制和处理声音而捕捉的短音频片段。")

## 采样器
quiz: Quiz("采样器 Sampler", "一种录制和播放样本的设备，具有编辑、处理和存储样本的功能。")

## Sallen-Key Filter
quiz: Quiz("Sallen-Key Filter", "Sallen-Key 滤波器拓扑创建一个二阶低通、高通或带通滤波器，并具有高共振能力。")

---

# 附录 C：C20 代码

## 饱和
quiz:Quiz("饱和", "在浅层次上，饱和是削波（clipping）的一种高级说法：一旦输入电压高于（或低于）电路能够承受的范围，它会在每个周期内立即下降到零值，从而产生一种更悦耳（或至少不那么刺耳）的形式。电子管通常与这种软削波方法联系在一起。1) 磁带达到完全磁化以产生极端音量的点。这会产生一些失真，某些音频发烧友认为在特定情况下这种‘警音’是一种理想的品质。2) 通过电子管放大器或前置放大器过载信号产生的音频失真——再次在峰值后为声音产生色彩感和温暖感。3) 一种模拟磁带和电子管饱和的数字插件。")

## 方波
quiz:Quiz("方波", "合成器产生的常见波形之一。其基频（正在播放的音符）在高频处逐渐衰减。结果是非常明亮、响亮且具有‘铜管质感’。")

## 正弦波
quiz:Quiz("正弦波", "低电压（通常为0 伏）。当输入超过一个参考阈值 - y 伏时，输出恢复高电平。当输入低于 a 时，输出恢复低电平。")

## 示波器
quiz:Quiz("示波器", "示波器可以运行在宽范围内，显示变化的电压 LFO 或包络，或快速变化的电压。振荡器和示波器用于查看外部设备的脉冲，但你可以使用 USB 示波器将显示端口的工作交给你的电脑，或将示波器作为模块使用。")

## 人声音色
quiz:Quiz("人声音色", "录音期间的一种人色，以帮助音乐家表现得更好。在后期最终的人声音轨上进行叠加。3) 音乐家或唱片师在唱片机上快速往回移动唱片的动作，通过针头的运动创建声音的节奏模式。")

## 倒带
quiz:Quiz("倒带 (Scrubbing)", "编辑时对一段录制音频来回移动的操作或功能，通过倒带定位录音中的某一点。在早期，倒带是指使用带式模拟磁带，通过手动旋转卷轴使磁带穿过录音头。今天，倒带主要在 DAW 中通过拖动光标在波形上来回移动即时完成。")

## 副工程师
quiz:Quiz("副工程师", "助理录音工程师。")

---

# 附录 A：C++20 代码

## SEM
quiz:Quiz("SEM", "Oberheim SEM（合成器扩展模块）是最早的产品之一。它是一个完整的合成器音色——包含两个振荡器、两个简单包络、VCA 以及一个非常流行的双极状态变量滤波器设计，带有旋钮，可以在低通、带通和高通输出之间进行交叉切换，并有一个独立的带宽设置——外壳呈立方体形状。今天在大多数情况下，当模块化制造商使用‘SEM’这几个魔法字母时，他们指的是一种模拟原始 Oberheim 合成器的滤波器。")

## 半模块化
quiz:Quiz("半模块化", "半模块化合成器的组件——如振荡器、滤波器和放大器——在前面板上是预连接的，这是一种典型的逻辑方式。然而，它们也提供了跳线点来访问其部分功能（例如振荡器的波形输出），以设置模块顺序，或覆盖这些预设连线。许多模块化合成领域的新手会通过购买一个半模块化合成器并用额外模块对其扩展来尝试。")

## 半音
quiz:Quiz("半音", "也称为半阶（half step），这是西方音乐中最小的音高划分——例如 A 和 C# 之间的差异。在平均律（西方音阶最常见的调音方式）中，这种音高划分是一个八度的 1/12。")

## 发送电平
quiz:Quiz("发送电平", "决定发送到发送总线的信号的控制。")

## 灵敏度
quiz:Quiz("灵敏度", "在音频设置中，描述麦克风在标准声级下能产生的输出量，与另一只麦克风在相同声级下的输出进行比较。2) 在……中指泛指的艺术人格。")

## 序列
quiz:Quiz("序列", "一组预设的音乐事件，如音高、采样声音和休止符，由设备按顺序播放。也指编写设备以播放这组音乐事件的行为。2) 在")

## 序列器
quiz:Quiz("序列器", "最常见的序列器类型是包含步骤的模块化设备。你使用这些步骤来创建声音模式。这在音乐中通常用于创建节奏或旋律。序列器还被用作门信号。")

## 顺序开关
quiz:Quiz("顺序开关", "一种一个一个切换输入的开关。顺序开关在音乐中按顺序触发不同的声音或效果。这通常用于合成器。")

## 串行数据
quiz:Quiz("串行数据", "其中单个比特一个接一个传输的数据流。这与并行数据相反，并行数据可以同时看到多个比特。")

## 串联连接
quiz:Quiz("串联连接", "连接设备（特别是电路），使电信号从一个流向下一个一个。")

## 设置
quiz:Quiz("设置", "录音期间麦克风、乐器和设备的放置，以获得尽可能好的音质。")

## 架式滤波器
quiz:Quiz("架式滤波器", "一种在频率图中形成特定形状的均衡曲线。高频架式滤波器影响设定频率及以上的所有频率电平。低频架式滤波器对设定频率以下的所有频率具有同样的作用。")

## 屏蔽
quiz:Quiz("屏蔽", "电缆中内部导体或导线周围的外层包裹，目的是防止电缆拾取电磁干扰。")

## 屏蔽线
quiz:Quiz("屏蔽线", "在内部导体周围有屏蔽保护的电缆。")

## 防震架
quiz:Quiz("防震架", "麦克风上的弹性支架，用于承受可能影响录音的意外震动（例如脚步声）。")

## 短路
quiz:Quiz("短路", "电路中两点之间（通常）不应存在的直接连接。")

## 短延迟
quiz:Quiz("短延迟", "小于 20 毫秒的延迟时间。")

## 最短路径
quiz:Quiz("最短路径", "一种录音技术，让信号在录音过程中通过最少的活动设备。")

## 枪式麦克风
quiz:Quiz("枪式麦克风", "一种带有长纤维管的麦，风可以消除从侧面到达的声音，使麦克风对某个方向的拾音优于任何其他方向。这使得枪式麦克风具有紧凑的手持模式。枪式麦克风常用于拍摄现场对话，通常安装在带有防震架的吊杆上。")

## 齿音
quiz:Quiz("齿音", "集中在 7kHz 附近的声音能量，由发音 s、sh 或 ch 音节引起。")

## 侧链
quiz:Quiz("侧链", "信号处理器的辅助输入，允许由外部源触发处理控制。侧链的常见用法是压缩器中，特别是在闪避（ducking）效果中，其中特定音频信号的存在触发另一个音频信号的压缩。（另见‘闪避’）")

---

# 附录 C: +20 代码

## 信号流
3651 测验：Quiz("信号流", "从广义上讲，音频信号从声源到系统输出的传输路径。（例如，从歌手的声音进入麦克风，通过电缆进入预置放大器，从预置放大器输出调音台，通过所有插入和总线，最后输出到 DAW 进行记录。2) 信号流通常是指音频信号通过调音台从输入到输出的路由）.")

## 信号处理
3657 测验：Quiz("信号处理", "")

## 信号
3666 测验：Quiz("信号", "1) 在音频中，与声波匹配或最初获取自声压波的交流电（或电压）。2) 在音频中，频率为 20 Hz 到 20,000 Hz 的交流电（或电压）。3) 数字音频流。")

## 正弦波
3671 测验：Quiz("正弦波", "1) 从广义上讲，音频信号从声源到系统输出的传输路径。（例如，从歌手的声音进入麦克风，通过电缆进入预置放大器，从预置放大器输出调音台，通过所有插入和总线，最后输出到 DAW 进行记录。）")

## 状态
3676 测验：Quiz("状态", "这是纯波形。它只包含基波，不包含高阶谐波。因此，它是创建源波形贝斯（作为底鼓）或其他可供使用的纯净音色的极佳来源，可以采用等技术（如频率调制 (FM)、幅度调制 (AM) 或波形折叠或偏移谐波内容）。")

## 场板
3686 测验：Quiz("场板,（打板）", "1) 在视频中，在片段开头对场景进行标识，以便进行视频剪辑。这是通过在摄像机前的场板上写下场景/场次、口头报出场景，并用打板器标记以便与视频同步。2) 音频录制，类似的做法是在录制轨道开头通过可听的提示来识别场次，虽然现在一些工程师仍在使用这种方法，但在过去那个时代是必要的")

## 从设备
3691 测验：Quiz("从设备", "1) 在音频中，任何通过读取从主设备发射的时钟信息而切换到另一个设备。2) MIDI，任何通过另一个设备的 MIDI 信息进行远程操作的设备或乐器。")

---

# 附录 A: C++20 代码

## 斜率限制器
quiz: Quiz("斜率限制器", "此函数可以平滑输入信号，使电压水平的变化不会超过每秒特定的伏特数。因此，它有时被称为延迟发生器，或在更技术意义上称为积分器。")

## 斜率生成器
quiz: Quiz("斜率生成器", "斜率生成器产生上升沿：上升或下降的电压。它本质上是一个门限生成器和一个斜率限制器（见上文）位于同一个模块中的组件。斜率生成器的常见示例是起始/衰减（AD）或起始/释放（AR）包包络生成器。然而，由于它可以用于通用控制函数——创建锯齿波或三角波振荡器，像 Buchla 和 Serge 等公司将其功能描述为生成斜率电压。")

## 斜率
quiz: Quiz("斜率", "大多数滤波器通常都有与其调优的截止频率或转角频率。然后它会减少（过滤）通过它的信号频率，使其谐波随着远离截止频率而逐渐远离。这种效果进一步被称为其斜率。大多数滤波器的定义是距离截止频率每倍频程 6 分贝（dB）的倍数。斜率为 24dB/octave 的低滤波器（LPF）可以将其截止频率上方一个倍频程的谐波衰减 24 分贝。")

## 智能 FSK 密钥
quiz: Quiz("智能 FSK 密钥", "智能 FSK——频率密钥（FSK）的更新形式，使 MIDI 设备能够同步模拟录带和其他记录设备。带有 MIDI 音频定位器（SPP）的数字信号被编码到空轨道上，它可以识别 MIDI 序列器/解码器中任何一点的精确小节、拍和小节拍。这使得设备可以在完全正确的位置开始，无论你从何处开始磁带。")

## SMPTE 代码
quiz: Quiz("SMPTE 代码", "简称‘SMPTE’。由电影和电视工程师学会创建的标准计时和同步协议，用于同步音频/电影，也可用于所谓的音频录制环境。许多音频专业人士将此时间码称为‘SMPTE’。")

## SMPTE
quiz: Quiz("SMPTE", "电影和电视工程师的缩写。2) 参见‘SMPTE 时间码’。")

## 小军鼓
quiz: Quiz("小军鼓", "小军鼓的缩写。横跨小军鼓底膜的金属丝，有助于在击打小军鼓时产生刺耳的‘破碎声’。")

## 镲片
quiz: Quiz("镲片", "踩镲（hi-hat）的很少使用的替代术语")

---

# 附录 A: C++20 代码

3737 镲符号被放在“脚踝高度”的时代。（参见‘踩镲’），

## 软膝
3738 测验：Quiz("软膝", "在压缩中，指信号电平超过阈值后逐渐引入压缩。（参见‘膝度’）")

## 软件乐器（虚拟乐器）
3741 测验：Quiz("软件乐器（虚拟乐器）", "基于软件的合成器、采样器或声音之一，通过 MIDI 控制器存储和访问，而不是通过独立模块。由于这些乐器的多功能性，作曲家和电子音乐家正在软件中使用虚拟乐器。")

## 焊接
3748 测验：Quiz("焊接", "使用焊锡建立连接的，焊锡是一种用于连接两个表面的软金属。在音频设置中，焊接常用于构建、修改和维修设备的各种用途。")



# 测验术语集

## 核心术语

- **3753 测验**：`Quiz("固态", "在电子领域，指在电子设备中使用晶体管和半导体材料，相对于真空管。录音中，固态放大与管放大具有不同特性，各有优势。固态结构的近期应用是计算机设备，特别是固态硬盘（SSD），它们传输数据比传统硬盘更快且不易损坏。")`
- **3760 测验**：`Quiz("独占开关", "调音台或 DAW 上激活独占功能的开关。")`
- **3762 测验**：`Quiz("独占", "调音台中的电路，允许一个或多个选定通道被听到或输出，而其他通道静音。在音乐中，歌曲中人声或乐器作为主角的片段。")`
- **3766 测验**：`Quiz("音频位置指针 (SPP)", "一种允许 MIDI 设备定位歌曲位置的消息。使用 MIDI 时钟连接作为同步设备或告知连接设备何时开始。")`
- **3770 测验**：`Quiz("隔音毯", "可以铺在地板上或挂起来增加房间声吸收，有助于防止声反射。")`
- **3772 测验**：`Quiz("音效 (SFX)", "除对话、旁白或音乐之外的添加到音频中的声音，通常用于电影/视频。")`
- **3774 测验**：`Quiz("音频文件", "可以存储在计算机数字存储介质（如硬盘）上的数字音频录制。")`
- **3776 测验**：`Quiz("声音建模", "一种不直接模拟物理设备而重建声音的技术。例如加法合成，它使用正弦波和噪声的组合来重建声音。")`
- **3779 测验**：`Quiz("声音模块", "电子乐器（音色发生器、合成器或采样器）")`

## 附录 C：C++20 代码（播放单元）

它没有播放接口，而是响应挖掘的 MIDI 消息。音模块通常被创建为流行合成器或该产品廉价版本的“大脑”，可以被添加到现有的 MIDI 配置中。音模块也可以以软件版本或插件的形式出现在可在计算机上访问。

- 测验：`Quiz("声压级 (SPL)", "在科学/技术术语中，指声波引起空气压力变化的测量，单位为 dB。（我们通过声音的振幅、音量或响度来听和感知 SPL）")`
- 测验：`Quiz("声压级", "在科学/技术术语中，指声波引起空气压力变化的测量，单位为 dB。（我们通过声音的振幅、音量或响度来听和感知 spl）")`
- 测验：`Quiz("声波", "也称为“声压波”。振动引起的波会导致气压发生细微变化，我们将其听到的（即声音）。")`
- 测验：`Quiz("声带", "1) 广义来说，指伴随视觉媒介的任何音频，音乐、对话或授权的音效（SFX）。在常用的术语中，指与电影、电视节目或视频游戏同步的配乐和授权音乐。")`
- 测验：`Quiz("不确定性声音", "这是 Buchla 265 和 266 模块用于创建控制范围的名称。它的偏移源于遵循原始 Buchla 模板或受其启发的圆形音模块。")`
- 测验：`Quiz("双声道对", "也称为“A/B 技术”。一种立体声麦克风放置技术，将心形或全指向性麦克风彼此间隔 3-10 英尺（取决于声音的大小，以创建左/右立体声声像）。")`
- 测验：`Quiz("扬声器", "一种将电信号转换为声音的设备；从更技术角度上说，是一种将电音频信号转换为声压波的换能器。")`
- 测验：`Quiz("声速", "通常来说，声波通过介质传播所需的时间。声在固体、液体和气体中的传播速度不同，我们通常认为的是在空气中传播，温度、气压和湿度的差异也会影响声的快速传播。作为一个参考点，声速通常被航空天工程师定义为“马赫 1.0”，相当于每秒 340.2 米（约 761.1 英里/小时，或每秒 1116 英尺），这是声在海平面、15 摄氏度（59 华氏度）温度下通过空气传播的速度。相比之下，在大气条件下70 华氏度的速度约为 344 米/秒，或 770 英里/小时。")`
- 测验：`Quiz("剪辑", "历史上，通过使用特殊的胶带将之前切割的磁带或胶片片段在精确的位置连接，目的是缩短音频段或进行编辑。今天，剪辑通过编辑音频段变成了一个非常简单的过程。")`

## 附录 A：C++20 代码

- 测验：`Quiz("弹簧混响", "一种通过将金属弹簧连接到换能器并让音频信号通过它在其内部产生振动来模拟混响的设备。末端的拾器将振动转换为电。虽然物理混响仍然存在，大多数学生使用插件或硬件混响单元来模拟混响。")`
- 电压上升到某一水平的波。
- 测验：`Quiz("可叠加电缆", "香蕉插头电缆的构造方式是每个插头都内置了一个插座，允许你将电缆直接插在原始插头的顶部。这些用于 Buchla 和 Serge 兼容系统。TipTop 使用 3.5mm 插头和插座为 Eurformat 用户制作了类似的 Stackables 电缆。")`
- 测验：`Quiz("驻波", "一种不需要的声波模式，通常发生在房间内，反射波在两个反射的平行表面之间反弹，初始波来自源，干扰受影响频率的波长实际上是房间的长度。这产生了波是静止的听觉幻觉，因此频率在房间的某些部分被放大到不需要的水平，而在其他部分几乎不存在。驻波在具有平行表面的方形或矩形房间中最常见，声学设计师试图通过插入吸收材料或引入其他物品来抵消平行表面以防止这些波的产生。")`
- 测验：`Quiz("步模式", "序器或 DAW 中的一种设置，手动输入音符，一次一个音符。")`
- 测验：`Quiz("序器", "这通常指一种序器，你可以在步骤上步进并暂停（可能还有持续时间），移动到下一步，依此类推。")`
- 测验：`Quiz("步骤", "Step 经常与 stage（见上方）通用使用，特别是在谈论序器时。")`
- 测验：`Quiz("立体声声像", "对立体声的感知，不同的来源似乎来自左侧。")`
- 测验：`Quiz("立体声录音", "两个或多个麦克风的放置。")`
- 测验：`Quiz("立体声", "两个通道的录制或复制。")`
- 测验：`Quiz("打击", "这个词出现在……")`
- 测验：`Quiz("子码", "额外的位。")`
- 测验：`Quiz("子帧", "比帧小的。")`
- 测验：`Quiz("子组", "控制台上可以作为一个整体控制的通道。")`
- 测验：`Quiz("求和", "求和是指加两个（或多个）东西的方式；总和是结果。")`
- 测验：`Quiz("汇总", "将两个或多个信号混合为一个信号的过程。")`
- 测验：`Quiz("次谐波", "一种（次谐波在其他地方详细讨论")`
- 测验：`Quiz("次八度", "一种在低音下方两个八度创建新音的模块。")`
- 测验：`Quiz("超心形指向", "一种非常窄的心形麦克风模式，轴线灵敏，轴外灵敏度约为 150 度。")`
- 测验：`Quiz("环绕声", "一种录制和播放技术，从前到后和左右列出声音的各个方面——一个 360 度的图像，而不是标准的左右图像。环绕声以不同数量的扬声器阵的形式出现。")`
- 测验：`Quiz("持续", "这是包络发生器的一个常见阶段，电压通常发送到截止滤波器或放大器的电平——在音符仍被按住时保持稳定的水平。音符被按住的持续，尽管有些包络发生器有专门的时间控制器来决定持续阶段应该持续多长时间。包含 ADSR（攻击/衰减/持续/释放）和 AR（攻击/释放，通常假设有一个持续阶段）的包络。")`

## 附录 A：C++20 代码（续）

- 测验：`Quiz("SVF", "变量滤波器 (SVF) 是合成器滤波器的常用设计——这种设计允许低通、高通和带通滤波器同时成为可行的方案。另一个副作用是，它们在高反馈（共振）设置下不易发生振荡，尽管某些人已经想出了如何实现这一点。欧海姆 SEM（合成器扩展模块）滤波器可能是最著名的状态变量设计。")`
- 测验：`Quiz("Sweetening", "该术语指在录音的后期制作阶段对音频进行微调。实际上，对音频声音的任何细微‘修饰’都被视为润色（Sweetening）。")`
- 测验：`Quiz("Switch Trigger", "某些系统（例如原始的 Moog 模块）使用开关型触发（开启或关闭）而不是普通的门信号（gate），门信号是一个短路到 0 伏特地的线，就像连接到地的开关点击声一样。在不进行某种形式的转换的情况下，你无法连接这两个系统，这种转换可能仅仅是一根电缆。")`
- 测验：`Quiz("Switch", "一种接通或断开电气连接的设备。")`
- 测验：`Quiz("Switchable Pattern", "具有两种或两种拾音模式的麦克风，可以通过麦克风主体上的开关进行切换。")`
- 测验：`Quiz("Sync Power Supply", "通过直接将高压交流信号转换为低电压输出电源的开关电源。它们通过快速切换开关的开启和关闭来创建一个所需电压的恒定直流电源，然后进行平滑处理以产生所需的电压。开关电源通常更轻、更凉、更便宜，但代价是噪声较高——包括输出电压噪声和射频噪声（这就是为什么它们通过屏蔽罩布线）。许多开关电源被用于制作混合电源，将开关电源与小型线性电源或调节器结合，以兼顾两者的优点。")`
- 测验：`Quiz("Sync Pop", "在电影或音乐开始前持续恰好两秒的短调（频率为 1 kHz 的正弦波，长度为一个胶帧）。同步脉（Sync pop）用于确保相关的音视频轨道在后期制作的所有阶段中保持同步。")`
- 测验：`Quiz("Sync24", "Sync24 是 Roland 标准 DIN 同步的另一种名称，它在当前使用的速率为每四分音符 24 个脉冲的时钟信号。Korg 设备使用了这种方法的变体，运行速率为每四分音符 48 个脉冲，被称为 Sync48。")`
- 测验：`Quiz("Sync", "同步有两种不同的含义，取决于我们讨论的是否支持振荡器模式（在接收到另一个振荡器的信号时将其波形重置为起始）。如果两个振荡器之间没有精确的八度关系，结果将是跟随第二个振荡器频率的提前重置的修改波形。你可以通过调制从振荡器的频率创建一些酷炫的‘撕裂’声；一个简单的 AD 包络效果就很好。在时序背景下，当你同步序列器或鼓点模式时，通常会使用一个定时器或同步信号供所有相关模块遵循。这通常是一个门信号或触发信号。Synchronization（同步）的缩写。在音频/录音室环境中，同步是指两个或多个段音频或视频之间的关联。这可以包括同步两个根据 SMPTE 码同步信号定时的录音/播放设备、同步电影或电视中的音频，以及许多其他例子。为电影、电视或视频制作的同步音乐也被称为‘同步（syncing）’。")`
- 测验：`Quiz("Synthesizer Expander Module", "欧海姆 SEM（合成器扩展模块）是他们最早的产品之一。它是一个完整的合成器声音——两个振荡器、两个简单包络、VCA 以及一个非常流行的二极状态滤波器设计，带有一个旋钮可以在低通、陷波和高通输出之间切换，并带有一个旁路设置——采用立方体外壳。如今当模块化制造商使用‘SEM’这两个魔法字母时，他们指的是旨在从原始欧海姆中移除的内容。")`
- 测验：`Quiz("Synthesizer", "一种使用电气振荡器人工产生音色的乐器，用于模拟其他乐器的声音或创建")`
- 测验：`Quiz("System Exclusive", "系统专用 (SysEx) 一种乐器使用的 MIDI 消息")`
- 测验：`Quiz("Tachometer", "在磁带录音中，一种测量和调节速度的设备")`
- 测验：`Quiz("Tails Out", "磁带的末")`
- 测验：`Quiz("Take Notation", "记录下磁带上的素材（takes）")`
- 测验：`Quiz("Take", "磁带的录音")`
- 测验：`Quiz("Talk Box", "吉他用于调制声音的效果器")`
- 测验：`Quiz("Talkback", "控制音室中与音乐家通信的麦克风")`
- 测验：`Quiz("Tape Delay", "一种创建人工延迟的处理技术")`
- 测验：`Quiz("Tape Guide", "任何引导磁带从一端到另一端的固定或旋转设备。")`
- 测验：`Quiz("Tape Hiss", "由于制作磁带的磁颗粒产生的天然高频噪声。")`
- 测验：`Quiz("Tape Loop", "一段末端接合在一起的磁带")`
- 测验：`Quiz("Tape Recording Equalization", "磁带机电路中高频信号振幅的增加")`
- 测验：`Quiz("Telephone Filter", "用于模拟通过接收器听到的音频的滤波器")`
- 测验：`Quiz("Tape Mapping", "对序列器或 DAW 进行遵循录制表演的速度变化的行为。与调整记录以匹配固定磁带的节拍映射或节拍对齐不同，磁带映射是调整项目（尤其是 MIDI 乐器）以匹配录制素材的细微差别。")`
- 测验：`Quiz("Tempo", "音乐移动的速率，单位为每分钟拍数 (BPM)")`
- 测验：`Quiz("Test Oscillator", "一种用于测试目的产生各种频率音频波形的设备。")`
- 测验：`Quiz("Test Pressing", "从第一个母版压出的少量黑胶唱片副本之一，在压制更多之前会试听和视觉检查质量。")`
- 测验：`Quiz("Test Tones", "1) 磁带卷开头参考电平单频率录音，用于编程。2) 用于校准音频系统的人工产生音调。")`
- 测验：`Quiz("Thin Sound", "一种描述缺少某些频率（尤其是低频）的音频信号的模糊术语。")`
- 测验：`Quiz("Threaded Inserts", "一种在带有滑动轨或螺母的通道中安装模块的常用系统。许多螺母插入这些通道中，可以滑动到任何位置以适应模块的安装间距。有些人不喜欢这种系统，因此他们用金属条代替了螺母。")`

## 附录 C：C++20 代码（安装细节）

插入已为标准 Eurorack 安装间距预钻的槽中。这些槽可能为 2.5 mm 或 3 mm 的螺丝进行了钻孔（购买导轨或外壳时请注意它们是否已安装）。

- 问答：`Quiz("三一原则", "一种麦克风放置的原则，指出当同时使用多个麦克风时，麦克风之间的距离至少应该是每个麦克风与其响应声源之间距离的三倍。三一原则用于防止音频信号之间的相位问题。")`
- 问答：`Quiz("三音扬声器", "一种具有独立扬声器来再现低频、中频和高频频率的系统。")`
- 问答：`Quiz("听力阈", "被描述为耳朵在 50% 的时间内能够听到的声压级。")`
- 问答：`Quiz("阈值", "阈值是信号在模块采取动作之前需要跨越的通用电压。例如，当包络跟随器（一种产生与音频信号电流相应的电压的模块）的输出高于阈值时，它的门控信号将变为高电，表示音符已开始。当包络输出遵循阈值时（可能与音符阈值相同或不同），门控变为低，表示音符应停止显示。动态处理单元的阈值会改变输入信号的增益。")`
- 问答：`Quiz("喉", "在扬声器中，喇叭或驱动器的小开口，声波通过这里从驱动器进入喇叭。")`
- 问答：`Quiz("零频调制", "ZFM 是通过零频率调制的缩写。想象一个连接，你将一个振荡器的输出（调制器）输入另一个振荡器（载波）的频率控制输入。当调制波形上升到零以下时，它会被加到载波正常的频率控制电压上，载波的音高上升。当调制波形低于零以下时，它从正常的频率控制电压中减去。在明确实现零频调制的振荡器中，载波将开始反向播放——本质上是负频率。通常产生更悦耳的声音，是振荡器一个理想的特性。")`
- 问答：`Quiz("喉,1", "在扬声器和麦克风中，描述振膜可以移动的无限制运动输出。在麦克风中，这影响麦克风的灵敏度；在较小空间内具有“短喉”，设计用于远距离投影；为较小空间设计则影响声的投影距离。（扬声器具有“长投射”。2）在扬声器中，“投射”也可能用于描述扬声器的方向性输出，通常基于它发射的频率。例如，喇叭在有限的角度内发射高频，因此具有“长投射”，而低音炮则向所有方向发射低频，制片人、工程师或音乐家在极度沮丧的时刻可能会随手做任何任何事。")`

## 附录 A：C++20 代码（续）

- 问答：`Quiz("跳线接", "跳线接 - 两端带有连接器的电缆，通常穿过工作室的墙壁或地板，用于在不同房间之间传输信号。跳线接提供了一种很好的半永久方式，通过工作室的各个部分路由和配置信号路径，并让工程师跟踪信号流。")`
- 问答：`Quiz("音色", "这个词用于描述你所创建的声音独特的音调特征，独立于其音高或响度。根据定义，不同的声音具有不同的音色。当时间改变声音的特征时（例如改变滤波器截止频率、脉冲宽度、波形量等），你正在改变你的音色。音色通常在音符的生命周期内变化。让乐器在演奏相同音高时听起来与其他乐器不同的音质。例如，小号的音色让它听起来像小号而不是笛子。它是通过乐器演奏时泛波的存在、缺失和复杂性而塑造的。")`
- 问答：`Quiz("时间码", "一种标准的计时信号，帮助设备之间相互同步，或同步音视频。音频中使用的时间码有 MIDI 时间码 (MTC) 和 SMPTE 时间码。")`
- 问答：`Quiz("压缩/扩展", "(也称为“时间拉伸”和“时间处理”）在不改变声音音高的情况下加快或减慢音频录制的过程。")`
- 问答：`Quiz("时间常数", "一个复杂的数学概念，基本上描述了电电压应用于电路时以及电路对其响应的时间延迟。")`
- 问答：`Quiz("Ti-Jan", "这是由 Switchcraft 的一种特殊设计的接口，用于 Rocha（以及许多克隆产品）传输音频信号。它们的直径为 3.5mm，但在物理上与常见的 3.5 mm 插头略有不同。1/8 英寸插头插入 Ti-Jan 接口时会松动，Ti-Jan 插头甚至可能不适合 1/8 英寸直径。")`
- 问答：`Quiz("通鼓", "鼓组中安装在底鼓上方的小鼓（如通鼓）和大鼓。")`
- 问答：`Quiz("音发生器", "1) 一种在各种频率下输出测试以校准磁带机或其他目的的设备。2) 合成器中的电路由单元产生音频信号，通常用于消除乐器的声音。")`
- 问答：`Quiz("音", "1) 任何单频信号或声音。乐器声音的音质相对于不同频率处存在能量的量。")`
- 问答：`Quiz("吐舌法", "用舌头控制木管乐器音符开始的技巧。")`
- 问答：`Quiz("总谐波失真 (THD)", "衡量输出阶段谐波频率电平与输入阶段比较的差异，以百分比表示的比例。它对许多耳朵来说几乎无法察觉，但越低越好。")`
- 问答：`Quiz("轨道/分配", "当时间改变声音的特征时……一个记录的轨道。")`
- 问答：`Quiz("轨道", "一个记录的轨道。1. 使用序列器制作，直到门保持高。")`
- 问答：`Quiz("换能器", "一种将一种介质转换为另一种能量的设备。换能器在录音室随处可见。见“带带”。")`
- 问答：`Quiz("瞬态", "波形开始时的初始能量峰值，例如敲击琴弦造成的。")`
- 问答：`Quiz("晶体管梯形滤波器", "术语常用于描述深受喜爱的低通滤波器（它曾获得专利；后来许多竞争者都模仿了它。）")`
- 问答：`Quiz("传输", "向上或向下移动磁带的机器部分。这有时被称为半音转调，因为它以固定的音程平移整个音乐。这可以通过多种方式发生：1) 通过新调性重写整首音乐；2) 通过比音符更低或更高的区间调调（通过电子键盘或乐器的自然调律）；3) 设计的声学材料放置在房间内以减少频率反射（即“低音陷阱”）。3) 另一种鼓（如“陷阱组”）")`



- 问答("颤音"，"这是响度变化的效果。在模块化合成器上创建这种效果是将低频振荡器 (`LFO`) 连接到放大器的控制电压输入。颤音与揉音不同；后者是音高的波动而不是响度。一种通过快速触发音符产生的音乐效果。")

- 问答("三角波"，"三角形是一种常见的合成器波形。当被选为振荡器的输出时，它比标准的方锯波声音更柔和，谐波更少更弱。它是低频振荡器 (`LFO`) 的流行输出，因为它在其控制的范围内产生相对平滑且下降的变化，同时比母正弦波更容易创建。")

- 问答("三角波"，"富谐波的波形在图形显示时呈三角形形状，这是由于奇谐波的存在和衰减共同导致的。")

## 附录 A：C++20 代码

386

# 附录 C：C++20 代码

quiz: Quiz("U", "架式设备通常遵循一组标准尺寸，包括 19 英寸（48.3厘米）的宽度，以及“机架单元”（或简称 `U`），每个 `U` 高 1.75 英寸（4.4厘米）。许多常见的模块化合成器格式遵循机架系统来标准化模块高度——例如 3U（3 x 1.75 = 5.25）或13.3厘米的 Eurack，用于 Buchla 和 Serge 的 4U，以及用于经典 Moog 的 5U（有时被称为 Moog Unit）。")

quiz: Quiz("不平衡音频", "大多数音频信号在电缆上通过两根线配对：一根代表音频振动的电压线，另一根是地线。干扰通常被称为不平衡音频干扰。")

quiz: Quiz("不平衡音频", "具有两个导体（一个信号线和根地线）且两端连接的电缆。不平衡电缆容易受到电磁干扰和噪声的影响。不平衡电缆的示例包括吉他/乐器线（也称为 `TS` 线或 `RCA` 线）和 `RCA` 线。")

quiz: Quiz("单向性图形", "一种对某个方向声音的敏感度高于任何其他方向的麦克风拾音。")

quiz: Quiz("单极", "模块化合成器中的许多电压——包括音频振荡器的输出以及大多数低频振荡器——在正负值之间波动。这被称为双极电压。某些电压，如包络生成器的输出——仅在 0 伏和最大正值之间；这被称为单极。")

quiz: Quiz("同音", "多个同时发出相同音高的表演者、乐器或声源。")

quiz: Quiz("等量增益", "放大器或设备输出端的信号强度相对于输入端的信号强度没有增加或减少的情况（通常被描述为 0 dB）。")

quiz: Quiz("Unity", "通常用于短语“等量增益（`unity gain`）”中，这意味着从输入到输出发送的信号电平完全相同。")

quiz: Quiz("真空管", "一种抽除了气体的玻璃管状二极管，允许电流通过。音频管用于放大器、振荡器和其他设备中。")

quiz: Quiz("循环与淡出", "一种结束歌曲录制的方法，音乐有一个重复部分，工程师减小音量直到其淡出。")

quiz: Quiz("循环 (Vamp)", "歌曲或和弦进行中不断重复的部分，通常是歌曲的结尾，通常是副歌的副歌部分。")

quiz: Quiz("变速", "磁带机上用于改变播放速度的控制装置。")

quiz: Quiz("Variable-D", "`ElectroVoice` 在其麦克风设计中的一项商标、专利技术，用于改变其麦克风的近距离效应。`Variable-D` 在麦克风主体周围放置了气口，每个气口距离麦克风振膜越远，其对频率的灵敏度就越低。")

quiz: Quiz("VCA 自动化", "某些调音台中的混合操作系统，通过电压控制来改变声电水平或其他功能")

## 附录 A：C++20 代码

4339 edquiz: Quiz("VCA 分组"，"若干个 `VCA` 滑推接收来自组组主滑块的控制电压。高端调音台的一项功能，允许工程师通过单个滑推控制一组独立信号，使工程师能够调整发送到每个通道的电压。")

4345 传输关于击键力度的数据。速度消息（`Velocity messages`）可用于传输音量信息，还可以触发多采样乐器补丁上的补丁。")

4350 乐器作为一种键盘，根据击键的力度发送 `MIDI` 速度消息。")

4352 quiz: Quiz("颤音"，"音高从常规音乐音高向上和向下发生平滑且重复的变化，通常由歌手或管乐和和弦乐演奏者完成。")

3356 f 软件基于软件的合成器，或者由计算机和外部 `MIDI` 控制器存储并访问的采样声音，而不是存储在立式合成器或模块中。由于这些乐器具有多功能性，越来越多的作曲家和电子音乐家正在使用可以存储在硬盘中的虚拟乐器，而不是购买键盘和模块。")

4362 quiz: Quiz("声室"，"录音室内用于隔离开录制人声的房间。这种做法可以防止其他乐器的声音渗入人声麦克风，并减少人声区域的自然环境和混响。")

4366 quiz: Quiz("声码器"，"一种音频处理设备或插件，用于分析音频信号的特征并用于影响另一个合成信号。主要开发用于合成人声效果的-

7369 ts 人类，声码器创建出特征性的声音效果，使其听起来像在说话-

7372 quiz: Quiz("旁白"，"在视频、电影上录制的语音播报")

7374 quiz: Quiz("声 (1) 除了嘴部的明显定义外，在合成器中，声（`voice`）也可能指声音。“单声道”意味着一次只播放一个声音，而“多声道”意味着可以同时播放多个声音（见“多声道”）")

7379 可合成器的补丁。")

7380 quiz: Quiz("易失性内存"，"计算机关闭时数据会丢失的计算机内存。`RAM`（随机存内存）是最常见的形式-

## 附录 A：C++20 代码

389

内存。Quiz: Quiz("电压控制放大器"，"增益水平受发送电压影响的放大器。`VCA` 常用于调音台。")

quiz: Quiz("电压控制滤波器"，"截止频率随电压控制改变的滤波器（尤其是低通滤波器）。")

quiz: Quiz("电压控制振荡器"，"频率受输入影响的振荡器。最常见于合成器中。")

quiz: Quiz("电压"，"导致它们之间产生电流的电动力或压力（“势能”）。")

quiz: Quiz("音量单位"，"用于测量响度变化的单位。基本是分贝刻度（见“`VU 表`”）")

quiz: Quiz("音量 (Volume)"，"一个常用的非技术术语，指代我们听到的声音电平，或电压电平。")

quiz: Quiz("Vox"，"一个意思是“声音”的词，通常作为录音室轨道的缩写。")

quiz: Quiz("VU 表"，"一种读取设备输入或输出音频电平的仪表，设计目的是匹配耳朵对突然变化的响应。")

quiz: Quiz("波"，"这是振荡器输出的电压向上和向下的振动模式。不同的模式产生不同的声音）")

folder:波折叠器（`wavefolder`）是波形器的一种非常特殊的设计，它使用比较器和其他电路。它们的作用是查看波形是否超过特定阈值。当超过时，它们不是剪掉波形的顶部和底部，而是创建一个镜像并将波形的该部分反射回自身，在此过程中产生更多的谐波和有趣的（效果）。

quiz: Quiz("波形 (Waveform)"，"这是振荡器输出的电压向上和向下的振动模式。不同的模式产生不同的声音。波、音频信号或其他类型波的表示或图表，显示波形在零线以上的振荡。")

quiz: Quiz("波长"，"波的一个周期的物理长度，以英尺测量，波长越长，频率越低；波长越短，频率越高。")

quiz: Quiz("波形器 (Waveshaper)"，"说它是“一个改变通过它的形状的电路”可能有点显而易见，但这正是其点。波形器有特定的目标，例如将输入的三角形波转换为输出正弦波，或对波形的峰值和瞬态进行真空管式的软剪切。")

# 附录 A：C++20

用于创建新声音的...光谱。

测试：“波形表 (`Wavetable`)”，“这个术语有两个相关但略有不同的含义。数字振荡器通常通过顺序读取数字表来产生声音——即从一个数值描述的电平跳转到下一个。这组数字描述了一个波形的一个周期，通常被称为波形表。许多数字振荡器有多个排列齐的波形表，并且可以通过突然跳转（原始的 `PPG Wave` 合成器做法）或通过在它们之间交叉滤波（大多数数字波形表振荡器的做法）在这些表之间移动。有些人将每个表称为“波形”，将一组单独波形称为波形表。”

测试：“加权 (`Weighting`)”，“音频测试中使用的均衡曲线用于补偿弗莱彻-蒙森曲线（`Fletcher-Munson Curve`）。（参见“弗莱彻-蒙森曲线”）”

测试：“西岸系统 (`West Coast System`)”，“所谓的“西岸”合成方法传统上与 `Buchla` 和 `Serge` 等公司相关——通常基于谐波到简单波形，而不是移除（滤波）复杂的波形。这是通过使用一对有时被称为“复杂振荡器”的振荡器实现的，它调制频率（`FM`）或振幅（`AM`）；另一个西岸模型是波形或波形折叠器（`wavefolder`）。你也可能会发现两阶段生成器如 `AD` 或 `OR`，而不是四阶段的 `SDR`，并且强调控制电压管理。一个共同特征是具有内置低通滤波器的电压控制放大器，创建了所谓的低通门限（`LPG`）。西岸方法还拥抱了非传统的控制器，例如触控和脉冲。在今天，在同一个系统中混合使用东岸和西岸方法是很普遍的。”

测试：“湿润的音色 (`wet sound`)”，“有时人们会说一个滤波器的声音是“湿”的。这指的是一个少于 4 极的声音——通常是低通或窄带，且共振稍微调高，但未达到自激振荡的程度。这种声音在 `Audio House` 和其他 `Techno` 风格中很流行。”

测试：“湿声 (`Wet`)”，“带有效果（如混响）的声音被称为“湿声”，没有效果的声音被称为“干声（`dry`）”。许多调音器都有湿/干混合，可以设置原始未处理声音与完全受影响声音之间的比例。指的是应用了完整效果（如混响）的信号，被称为“干声”，指的是未受影响的声音。首选的混合方式是湿声和干声的混合。（参见“干声”）”

测试：“白噪声 (`White Noise`)”，“噪声是一种没有明显音高的随机信号，例如呼吸声、背景噪音或风声或海浪声。噪声由不同的“颜色”描述，如粉色、红色或蓝色，它们具有不同的频率。白噪声在每个频率单位具有相等功率（例如每 1000 赫兹），听起来更亮、频率更高。噪声信号包含跨越所有可听频率的相等能量。像噪声信号一样，工程师经常通过音频设备观察白噪声信号用于调优和校准，或者在对现场音频空间进行 `EQ` 处理时。（参见“粉红噪声”）”

# 附录 A：C++ 代码

```cpp
4468 ion
4470 ence in pitch.") 两个钢琴键之间的音高差异。）
4471 quiz:Quiz("异音 (Wild Sound)","在电影和视频中，与画面同步录制的音频是单独录制的。") 
4473 quiz:Quiz("风控制器 (Wind Controller)","一种像现场乐器一样演奏的设备，用于计算吹入麦克风产生的噪声。通常用于录制 
4478 频率偏移到接收器阶段，而不是通过音频电缆传输。）
4482 quiz::Quiz("低音喇器 (Woofer)","一种设计用于仅重低频的扬声器。")
4484 er 是增益通道的控制，计算机正在记录其变化 
4489 常用于麦克风电缆。）
4492 两个心形麦克风的头部相互对着，角度为 90 度
4499 处理处理由传统的数字模拟转换器 (DAC) 完成的。")
4501 );
4502 ;
4503 ;
4504 int main()
4505 {
4506 std::random_device rd;
4507 std::mt19937 gen(rd));
4508 std::uniform_int_distribution<> distria(1, 4);
4509 std::uniform_int_distribution<> distrib(0, game.size()-1);
4510 std::shuffle(std::begin(gen), std::end(gen), std::default_random_engine());
4511 std::vector<std::string> answers;
4512 std::string question;
4513 uint32_t n;
4514 uint8_t correct;
4515 uint32_t score=0;
4516 uint32_t tqs=0;
4517 for (uint32_t ctr=0;ctr<game.size();++ctr) {
4519 answers.clear();
4520 correct=distria(gen);
4521 for (uint8_t i=1;i<=4;i++) {
4522 if (i == correct)
4523 answers.push_back(game[ctr].getA());
4524 question=game[ctr].getQ();
4525 else {
4526 answers.push_back(distrib(gen)).getA());
4527 }
4528 std::cout << "\33c
4529 if (tqs != 0) {
4530 std::cout << "QUESTIONS: " << tqs << " / " << game.size() << " SCORE: " << score << "\n";
4555 std::cout << "[" << ((double(score)/double(tqs))*100.0) << " % correct.\n";
4556 }
4557 return 0;
}
```

# 附录 B：音频工程术语 (0 - 9, A - Z)

`0–5v` 表示 0 到 5 伏特的范围，常用于模块合成器中的门触发和触发电压。触发器通常在 5v 为高（10v）。

`1 pole` 这种数字和缩写格式（`dB/oct` = 每字节分贝）通常用于描述滤波器的频率响应。滤波器通常有一个截止频率或角频率。它通过通过滤波器的信号频谱，使其强度每离开截止频率一个倍频衰减 6 分贝。`6dB/oct` 滤波器通常被称为“一极”（因为滤波器设计的每个极都会导致 6dB 的衰减），对通过它的信号的影响较小。低通门限（`LPG`）通常但并非总是使用一极低通滤波器，使其高于截止频率的高波每倍频减少 6 分贝。

`1 ppqn` 最常见的序列时钟划分是每四分音一个步脉冲。这通常是模块系统中被除的核心脉冲，以产生其他音乐划分。

`1 v/oct` 模块合成器中控制音高最常用的标准。在西方音乐的一个八度内有 12 个半音的情况下，等律下每个半音音高变化正好是 0.1 伏。

`1.2 v/oct` `Buchla` 组件使用了 1.2 伏每倍频的系统，而不是更常见的 `1 v/oct`。

`1/4"` `5U`（`Moog`格式）模块合成器中最常用的连接尺寸。这些是 `TS`（尖/环）插座和插头，类似于吉他和和其他乐器电缆。

`1/8"` 常错误地描述为 `Eurorack` 模块中常用的连接尺寸，以及 `Buchla` 音频信号。事实上，`Eurorack` 模块使用 `3.5mm` 插座和插头（比 `1/8"` 略大）；`Buchla` 使用 `Switchcraft Tini-Jaj` 连接器。`Tini-Jax` 的直径为 `3.5mm`，但是

## 附录 B：音频工程术语 (0 - 9 - A - Z)

物理上与 `3.5 mm` 接口略有不同。`1/8` 英插头在这些插座中都会松动，因此在为这些格式订购零件或电缆时，请确保获取的是 `3.5mm` 连接器。

`10 vpp`

“10 峰值电压”（`10 volts peak to peak`）的缩写，指信号传输过程中最低电压和最高电压之间的差。这是模块合成器中音频和调制信号的常用电压范围。实际范围为 -5 到 +5 特。精确范围可能会根据效果的深度而变化，因此不要纠结于特定的电压范围。更多关注它们是在 0v 之上或某个值变化，还是在 0v 上下以大致相等的数量变化（如`10vpp` 降一个八度）。

`12 dB/oct`

这种数字和缩写格式（`dB/oct` = 每八度分贝）通常用于指滤波器的频率响应行为。滤波器通常有一个其调优的截止频率或角频率。它会减少（滤波）通过它的信号的频谱，使得每距离截止频率一个八度，其亮度就减弱 12 分贝的倍数。`12dB/oct` 通常被称为“二极”滤波器（因为滤波器设计中的每个极都会导致 6db 的衰减）。复古 `Arp`、`Korg` 和 `Oberheim` 乐器具有 2 极滤波器，与 4 极乐器相比，声音更明亮。

`16’`

有时出现在振荡器的八度选择开关上。它指的是风琴管的长度。管子越长音越低；它处于中频范围。长度减半（`8’`）的管子或设置高一个八度；长度再次减半（`4’`）高两个八度；以此此类推。

`18 dB/oct`

这种数字和缩写格式（`dB/oct` = 每八度分贝）通常用于指滤波器的频率响应行为。滤波器通常有一个其调优的截止频率或角频率。它会减少（滤波）通过它的信号的频谱，使得每距离截止频率一个八度，其亮度就减弱 18 分贝的倍数。它通常用作一种代码简写，当有人想要在不提及乐器名称的情况下，提到 `TB-303` 的酸性风格低音线条时使用。

## 二极

这种数字和缩写格式（`dB/oct` = 每八度分贝）通常用于指滤波器的频率响应行为。滤波器通常有一个其调优的截止频率或角频率。它会减少（滤波）通过它的信号的频谱，使得每距离截止频率一个八度，其亮度就减弱 12 分贝的倍数。`12dB/oct` 滤波器通常被称为“二极”滤波器（因为滤波器设计中的每个极都会导致 6db 的衰减）。复古 `Arp`、`Korg` 和 `Oberheim` 乐器具有 2 极滤波器，与 4 极乐器相比，声音更明亮。

`2.5 mm`

一种用于安装 `Eurack` 模块的常用螺纹尺寸。当使用沿模块附固的导轨滑动的松螺母系统时，这种尺寸最常见。

`24 dB/oct`

这种数字和缩写格式（`dB/oct` = 每八度分贝）通常用于指滤波器的频率行为。滤波器通常有一个其调优的截止频率或角频率。它会减少（滤波）通过它的信号的频谱，使得每距离截止频率一个八度，其亮度就减弱 24 分贝的倍数。这种设计常用于复古 `Moog` 和 `Roland` 合成器。4 极滤波器通常被主观认为具有比 2 极滤波器更厚实、更“圆润”的声音——这种概括总是危险的。

`24 ppqn`

`MIDI`、`DIN` 同步以及其他用于电子音乐和合成器系统中常用的主时钟划分。它意味着在内部，当前节拍下的每个四分音符都会计算 24 个时间细分。这个快速的内部时钟可以进一步分频以创建十六音符 (+6)、八分音符 (+12)、八三连音符 (+8) 等。

`2'`



# 附录 B：音频工程术语 (0 - 9 - A - Z)

## 2'

有时出现在振荡器的八度选择开关上。它指的是风琴管的长度。管子越短 = 音高越高；`2'` 在模块振荡器上很少见，因为它的音高很高——以中间 C 音为起点高两个八度。长度加倍（`4'`）的管子或设置低一个八度；长度再次加倍（`8'`）低两个八度；以此类推。

## 3 mm

一种用于安装 Eurorack 模块的常用螺纹尺寸。当使用预钻孔的模块轨道时，这种尺寸最常见。

## 三极

这种数字和缩写格式（`dB/oct` = 每八度分贝）通常用于指滤波器的频率行为。滤波器通常有一个其调优的截止频率或角频率。它会减少（滤波）通过它的信号的频谱，使得每距离截止频率一个八度，其亮度就减弱 `18` 分贝的倍数。它通常用作一种代码简写，当有人想要在不提及乐器名称的情况下，提到 `TB-303` 的酸性风格低音线条时使用。

## 3.5 mm

Eurorack 模块合成器中接口和电缆的标准尺寸。注意这比 `1/8"` 略大。

## 303

`TB-303` 是 Roland 生产的一种低音合成器。由于其独特的尖鸣（squelchy）滤波器，成为了酸性音乐派的支柱。

## 32'

有时出现在振荡器的八度选择开关上。它指的是风琴管的长度。管子越长音越低；它处于中频范围。长度减半（`16'`）的管子或设置高一个八度；长度减半（`8'`）高两个八度；以此类推。

## 3U

指高度为 `3` 单位的模块。这在许多模块系统中常见，尽管 Eurorack 通常是 `3.5` 单位。

## 四极

这种数字和缩写格式（`dB/oct` = 每八度分贝）通常用于指滤波器的频率行为。滤波器通常有一个其调优的截止频率或角频率。它会减少（滤波）通过它的信号的频谱，使得每距离截止频率一个八度，其亮度就减弱 `24` 分贝的倍数。这种设计常用于复古 Moog 和 Roland 合成器。`4` 极滤波器通常被主观认为具有比 `2` 极滤波器更厚实、更“圆润”的声音——这种概括总是危险的。

## 4-40

偶尔用于安装 Eurorack 模块的螺丝尺寸。例如 Pittsburgh Modular 使用这种尺寸。

## 4U

指 `4U` 高的模块——即 Buchla 和 Serge 系统，以及这些仿制品。Buchla 和 Serge 都倾向于更具实验性的合成和音乐方法，因此有些人将“`4U`”作为他们不随俗且酷的勋章。

## 4'

有时出现在振荡器的八度开关上。它指的是风琴管的长度。管子越短 = 音高越高；`4'` 是振荡器上能看到的最高八度。长度加倍（`8'`）的管子或设置低一个八度；长度再次加倍（`16'`）低两个八度；以此类推。

## 5U

指 `5U` 高的模块或 `8.75` 英寸（`22.2 cm`），这通常与复古 Moog 标准以及遵循其足迹的 Syntizers.com (Dotcom) 和 Moog Modular 相关。你有时听到这与 Moog Units 互换使用，后者指的是标准的 `2.125` 英寸（`5.4 cm`）宽。鉴于这种标准既具有历史意义又物理尺寸巨大，有些人将“`5U`”作为他们传统且酷的勋章。此前 MOTM 曾有一种流行的 `5u` 滤波器，使用不同的宽度和电源连接。它已经停产，但今天仍有忠实的 MOTM 设备。

## 6 dB/octave

这种数字和缩写格式（`dB/oct` = 每八度分贝）通常用于指滤波器的 频率响应行为。滤波器通常有一个其调优的截止频率或角频率。它会减少（滤波）通过它的信号的频谱，使得每距离截止频率一个八度，其亮度就减弱 `6` 分贝的倍数。`6dB/oct` 滤波器通常被称为“单极”滤波器（因为滤波器设计中的每个极都会导致 `6db` 的衰减），对通过它的信号的影响相对较弱。低通门限（LPGs）通常——并非总是——使用单极低通滤波器，在每个截止频率上方每一个八度减少 `6` 分贝的高波强度。

## 808

Roland 的 `TR-808` 节奏合成器使用模拟电路创建了所有的声音。它刚问世时并不为人知，因为模拟声音不够真实。但后来，House 和 Hip-Hop 等音乐采用了它那种浑大、沉闷的声音。当一个模块说它重现了“`808`”鼓时，这就是它们试图模仿的乐器。被复制最多的是 `808` 踢鼓声，它倾向于是一种低音、长衰减的正弦波形，且通常带有清脆的起始部（attack）。

## 8'

有时在振荡器的八度选择器上看到。它指的是风琴管的长度。管越短，音高越高；`8'` 通常与中音 C 相关。长度为半的管或设置（`4'`）高一个八度；长度为一倍的管或设置（`16'`）低一个八度。

## 909

`TR-909` 节奏合成器是 Roland 现在已停役的 `TR-808` 的后续产品。它将哈士鼓和踏镲的采样与 `808` 的模拟声音相结合，并变得流行。当一个模块说它产生类似 `909` 的声音时，这就是它所引用的乐器。

## A-440

这是高于中音 C 的 A 音的赫兹频率（每秒循环）。它通常被用作调音参考。

## A/B 技术

一种双声麦克风放置技术，将两个心形或全指向性麦克风彼此间隔 `3-10` 英尺（取决于声源的大小），以创建左/右双声声像。也称为间距相位（Spaced Phase）。

## A/D

模拟数字转换（Analog-to-Digital Conversion）的缩写，将具有连续变化的量（如电信号）转换为近似这些变化的数字（即计算机数据）。

## 绝对相位

该术语描述原始信号（进入麦克风）与重现声音（通过扬声器）之间的完美极性。当施加在麦克风上的正压力被翻译为扬声器的正压力时，两者处于“绝对相位”中。

## 吸收

在声学中，吸收是指声波被表面吸收的现象，而不是从表面反弹（反射）。例如，控制室中的吸收性材料倾向于“消减”房间的声音，因为声能被吸收了而不是被反射。（另另阅“反射”。）

## AC 耦合

`AC` 耦合输入尝试移除任何通过它的恒定直流电压。如果你有一个本质上是交流的音频信号（例如振荡器的输出），并且你想移除任何可能渗入其中的电直流偏移，那么它是很有用的。这些偏移会导致交流波形的一半过早削波（clip），或者在静音的开始和结束处产生咔哒声。然而，这种耦合会使通过它的波形产生轻微失真，本质上，`AC` 耦合是一个试图移除极低频率分量的高通滤波器。

## AC

交流电（Alternating Current）——标准插座和通过音频线传输的工作室信号中存在的电流类型。在 `AC` 中，电流方向“交替”，在电路中来回流动。在模块术语中，`AC` 指在正值和负值之间交变的电压——例如振荡器的输出。

## 加速度计

一种测量其承受的加速度并创建与之匹配电信号的设备。在音乐和音频中，加速度计用于麦克风和吉他拾音器等设备。

## 橡果管

因形状像橡果而命名，橡果管是一种用于超高频（UHF）电子设备（如真空管放大器）的小真空管。

## 声放大

乐器中响应乐器初始振动的部分，导致周围的空气更有效地移动并使声音更大。例如：声学吉他的琴身、喇号的喇、鼓壳以及钢琴的木制共鸣板。

## 声学回室

一个设计有硬非平行表面的房间，以产生混响。在录音室中，它们被用于为干信号添加自然混响。

## 声学

声音的科学——更具体地说，是声波属性和行为的科学。深入理解声学对于音频工程和录音室设计至关重要。

## 有源设备

一种具有控制电电流能力的组件（与“被动设备”相反）。在录音室中，有源设备通常是指包含放大器的组件。（见“被动设备”。）

## 有源多路器

你通常需要分配或复制信号以发送到多个目的地。这通常通过多路器完成，你插入一个源，然后插入跳线线连接到多个目的地。有源缓冲多路器在输入和输出之间包含一个缓冲电路，使得信号不会因为被拆分多次而失去强度或完整性，并且其中一个输出端的任何异常情况都不会影响任何其他连接。某些模块在其输出中内置了良好的缓冲，可以无问题地驱动多个模块。但如果你尝试使用被动多路器连接到例如三个振荡器，并发现跟调效果不好，那么你需要一个缓冲多路器。

## 执行器

开关中引起连接变化的部分（例如拨动开关、翘开关）。

## AD

两阶段攻击/衰减包络的缩写。这种简单的包络形状从 `0` 伏上升到其最大值，然后根据衰减控制下降。

## ADSR

具有四个阶段的包络：攻击、衰减、持续和释放。当此包络接收门输入时，它通常从 `0` 伏开始（连接到电压控制放大器时相当于静音，连接到电压控制滤波器或振荡器时相当于最低频率）上升到它可以输出的最大电压（取决于系统通常为 `5` 到 `10` 伏）；它通常可以通过攻击控制的时间设置输出电平。一旦达到电平，输出电压立即开始按照衰减控制的速度下降，直到达到由持续控制设置的电压。如果输入门仍然有效，则保持该电平，直到门回到 `0` 伏（通常是因为你松开了控制键盘的键等）。此时，输出电压开始按照释放控制设置的速率回到 `0` 伏。

## AES

音频工程协会。

## AES3

（称为 AES/EBU）一种由音频工程协会和欧洲广播联盟开发的数字音频传输标准，用于在设备之间传输双通道数字音频数据。`AES3` 是 XLR 线缆以及 RCA 和 S/PDIF 线缆的协议。

## AFG

`AFG`（音频频率发生器）是 Livewire 发布的一种功能非常强大的模拟振荡器电子设备。该设备此已停产，目前偶尔会有翻新的 B 级库存机出售。据我所知，这些扩展模块从未发布过（至少没有过广泛发行）。

## 触后

（也称为“压力灵敏”）某些键盘会测量你按下按键的力度，并将其转换为音高电压（或控制信号如 MIDI，随后可以转换为控制电压），你可以利用它来为音符增加表现力，例如添加颤音或加宽滤波器的范围。单音触后无论你按下哪个键，都为整个键盘测量一个值；复音触后则为每个单独的按键产生信号。重要冷知识：触控板键盘实际上测量的是接触皮肤的表面积，而不是压力或力——因此你可以通过转动指尖和手指来增加或减少触后量。

## ADSR (AHDSR)

起始、保持、衰减、持续和释放。这是一种稍微复杂的 `ADSR` 包络，它在起始上升完成后、衰减开始之前，会将电压保持在其最大值一段特定时间内。

## 混叠

一种在采样器中发生的数字失真，当输入信号频率超过了该设备的奈奎斯特频率时发生。采样器以错误的频率（或“别名频率”）重现它，导致声音中产生失真或伪影。如果你播放一个数字音频文件，其中采样率的一半是一个可听的音高，那么你还将听到声音的谐波内容在该半采样率转折点重现的镜像内容（除非经过良好的滤波）。（参见“奈奎斯特频率”）。

## 交流电

在标准电源插座和音频线传输的工作室信号中常见的电流类型。在交流电中，电流方向会“交替”，在电路中往复流动。

## 调幅

幅度调制（AM）是指使用称为“调制器”的信号来改变已知信号（载波，通常是音频信号，在 `0` 伏上下波动）的响度变化技术。在典型的调制（AM）场景下，一个具有正电压的低频振荡器（例如在 `0v` 到 `5v` 之间，或者 `1v` 到 `2v` 之间更小的值）被馈入电压控制放大器的输入端，为通过它的音频信号添加颤音。从技术上讲，这被称为二象乘法器或调制器，因为调制信号中的任何负波动都会被忽略；在连接颤音时，你可能需要确保为 LFO 添加了偏置电压，以确保声音在 LFO 波形的序列上不会出现断音。

## 环境音

在大多数情况下，这指的是某个地方（如餐厅）的“氛围”。但在录音中，它指的是来自环境而非直接来自声源的声音部分。例如，从弹奏的大提琴发出的进入你耳朵的声波直接来自声源，但同一把大提琴的声音经过后墙反射后传给你的声音就是环境音。

## 环境场

远离声源且混响响大于直声的区域。

## 环境拾音

指的是将麦克风放置在房间的环境场中以录制声音的环境混响。录音工程师通常会在对乐器进行直接拾音的同时也这样做，以便在录音中创建直声与混响声的混合。

## Amp

根据语境，是“Amplifier（放大器）”、“Amplitude（幅度）或“Ampere（安培）”的缩写。

## 安培

电流的单位缩写。

## 放大器

一种增加电信号电平或幅的设备，使产生的声音更大。

## 幅度调制

幅度调制（AM）是指使用称为“调制器”的第二个信号来改变作为载波的信号（通常是音频信号，在 `0` 伏上下波动）的幅度或响度。在幅度调制（AM）场景，一个具有正电压的低频振荡器（例如在 `0v` 到 `5v` 之间，或者 `1v` 到 `2v` 之间更小的值）被馈入电压控制放大器的控制输入，为通过它的音频信号添加颤音。从技术上讲，这被称为二象乘法器或调制器，因为调制信号中的任何负波动都会被忽略；在连接颤音时，你可能需要确保为 LFO 添加了偏置电压，以确保声音在 LFO 波形的低端行程上不会断音。

## 幅

波形在零线以上或以下的高度。在音频中，这通常意味着声音的强度或音量。

## 模拟录音

对音频波形连续变化的录制。录音室中最常见的模拟录音例子是卷带磁带。

## 模拟移位寄存器

模拟移位寄存器（ASR）是采样保持模块与桶延迟的混合体（假设你已经知道它们是如何工作的）。在最初被触发时，它采样输入电压并在第一个输出端呈现。在第二次触发时，采样输入电压并将此新电压从第一个输出呈现，同时移动到第二个输出。这种“传声筒”游戏会一直持续，传统的 ASR 有三个或四个阶段。

## 模拟数字转换器

一种将连续变化的信号（模拟）转换为近似这些变化的数值（数字）的设备。在音频录音中，这指的是将录制的声音从电电压转换为计算机数据。

## 模拟

模拟术语意味着信号是连续变化的，与信号已转换为离散数字的数字相比。在模块合成器领域，模拟指的是不包含数字（或至少不是基于计算机）组件的设计设计——相反，它使用晶体管、二极管、电容器等进行处理，而不是 CPU 和 DSP。

## AND 功能

常见的布尔或二进制逻辑功能之一，AND 表示只有当所有输入为“高”（例如输入 1 和输入 2 等开启）时才输出门信号。NAND 功能具有反相输出：当两个输入都高时输出为低，否则为高。

## AR

两阶段的起始/释放包络按照起始参数的速率从 `0` 伏范围到其最大值（通常为 `5`、`8` 伏甚至是 `10` 伏），并在馈入包络发生器的门信号持续期间保持该值。当门信号变为零时，包络按照释放参数的速率回到零。（另一种类型的包络被称为 ASD - 起始/保持/衰减，你指定衰减保持在最大值的固定时间，而不是关注门信号）。

## 琶音器

稍微谈谈音乐理论，琶音器是一种每个音符单独播放而非一次性播放所有音的“分解弦”。琶音器——通常内置在键盘中，或插入键盘与声音模块之间的设备——让你更轻松地演奏琶音：你只需按住和弦的音，它就会自动一个接一个循环播放这些，就像一个可以即时编程的步序器。琶音器有各种模式选择（向下、向上、往复等），甚至有一个锁定或保持功能，即使在你松开键后它也能继续。

## Attack/Decay

两阶段起始/衰减包络的缩写。这种简单的包络形状按照其 Attack 参数定义的速率从 `0` 伏上升到最大电平（通常为 `5`、`8` 或可能是 `10` 伏），然后按照其 Decay 参数定义的速率立即回到 `0` 伏。其变体是 AHD：在完成 Attack 阶段后，它会在最大电平保持指定时间（与 AR 包络相反，AR 在门信号高电期间一直保持最大电平），然后衰减回零。我听说有些包络是 AHD 和 AR 的混合体，它们可以在 Hold 时间或输入门高期间保持最大电平。

## Attack/Hold/Decay/Release

这是一个稍微复杂的 `ADSR` 包络，在起始完成后、衰减开始下降之前，它通常会将衰减保持在其最大值持续指定时间。

## Attack/Release

两阶段起始/衰减包络按照 Attack 参数设置的速率从 `0` 伏上升到最大电平（通常为 `5`、`8` 甚至 `10` 伏），然后只要输入包络发生器的门信号保持高电平，它就保持在该数值上。当门信号回到零时，包络输出也按照 Release 参数设置的速率回到零。（还有一种名为 AHD – 起始/保持/衰减 – 的独立包络类型，其中你指定电平保持在最大水平的固定时间，而不是关注门信号。）

## Attack

这通常指包络的第一阶段，发生在音符开始时，它从 `0` 伏（控制放大器模块时为静音）上升到响度值。打击声和拨弦声具有非常快的起始；缓慢、悠闲的风声或弦乐乐句具有很长的起始。

## Attenuation

电信号或声信号强度的降低。在音频中，衰减以分贝 (`dB`) 计算，通常听为音量减小。声波在空气中远离声源传播时会衰减。工程师在录音室内通过增益控制故意衰减信号以防止过载。

## Attenuator

可以减少通过它的信号或电压强度的控制装置。

## Attenuverter



衰减器的特殊版本，还可以反转通过它的信号或电压的极性。大多数反相器在中心位置不通过信号；当你顺时针旋转时，你会增加正常版本的信号；当你逆时针旋转时，你会增加反相版本的信号。某些反相器是开启了极性的普通衰减器。

# Audio Frequency Generator（音频频率发生器）

AFG（音频频率发生器）是 Livewire Electronics 发布的一款功能非常齐全的模拟振荡器。此后已停产，偶尔会有翻新的 B 品设备出售。据我所知，扩展模块从未发布过（至少没有广泛发布过）。

# Audio（音频）

在广义上，音频是指我们人类用耳朵能听到的频率范围。在技术上，音频是指声音的传输、录制或复制，无论是数字、电子还是声学的。

# Automatic Dialogue Replacement (ADR)（自动对话替换）

电影拍摄完成后，在受控环境中重新录制对话的过程，用于替换录制较差对话。

# Automatic Gain Control（自动增益控制）

具有长释放时间的压缩器，用于保持音频音量在一致水平。

# Automation（自动化）

编程在录制和/或播放期间自动发生。在录音室内，工程师在调音台或计算机上使用自动化，以便各种参数在多轨道录制和播放的不同时间自动更改。这种预编程功能使得创建这些变化比尝试在实时手动执行所有变化要容易得多。

# Auxiliary Equipment（辅助设备）

与调音台配合工作修改信号的外部信号处理设备。

# Auxiliary Return（辅助返回）

（缩写为 Aux Return 或 Return）调音台或 DAW 输入，将通过辅助发送发送的处理过的信号返回到通道混中。

# Auxiliary Send（辅助发送）

（缩写为 Aux Send 或 Send）用于调整从调音台或 DAW 的输入通道通过辅助总线发送到辅助设备或插件的信号电平的控制。这通常用于创建一个效果回路，处理信号的一部分，然后通过辅助返回回到混音。

# Axis（轴线）

设备运行周围的一条虚拟线。例如：在麦克风使用中，轴线是从麦克风正面朝向振膜运动方向延伸出的一条虚拟线，界定了麦克风拾取声音的最佳位置。发生在麦克风“轴外”的声音拾取得不会那么清晰。

# Background Noise（背景噪声）

+ 指：

1. 房间内与所录制的乐器或人声无关的环境噪声；或
2. 系统噪声。（所有电子设备都会发出某种水平的噪声。）

# Baffles（声学屏）

用于防止声波进入或离开空间的吸声板。

# Balance（平衡）

+ 1. 麦克风中两个或多个乐器之间的相对电平，或者立体声录制通道间音频信号的相对电平。
2. 平衡立体声录制通道间的音频信号。

# Balanced Audio（平衡音频）

这指的是使用三根线传输音频信号的系统：一根是地（0 伏参考），第二根在 0 伏上下变化的音频信号，第三根是音频信号的反相。平衡音频通常意味着 +dB 的参考信号水平（高于线路电平；但低于大多数合成器），尽管麦克风信号相比之下更好，因此更容易受到外部噪声影响——模块合成器倾向于内部使用非平衡音频。如果你需要平衡输出（或输入），你需要一个转换平衡与非平衡音频的特殊模块，以及必要的水平匹配。

# Balanced Cable（平衡线）

由三根线（两根信号线一根地线）和两个连接器组成的电缆。两根信号线以相反极性传输相同信号，为平衡系统提供了干扰和噪声的保护。平衡线的示例包括 TRS 立体线和 XLR 线。

# Mixer（混音器）

产生两个输入信号的和与差频率的电路或设备。

# Balanced Modulator（平衡调制器）

平衡或环形调制是一种特殊的幅度调制，其中一个双极性（在 0 伏上下摆动）信号——调制器——用于改变双极性信号（称为载波）的幅度。调制器的频率同时加上并减去载波的频率；产生的谐波取代了原始的载波和调制器。

# Banana（香蕉头）

4U 系统使用的另一种连接器类型（https://en.wikipedia.org/wiki/Banana_connector）

## 附录 B：音频工程术语 (0 - 9 - A - Z)

例如 Buchla（控制电压）和 Serge（同时包含控制和音频）。这些电缆只有一根导线，因此它们只传输信号，依靠系统的模块面板和底座提供地参考。香蕉插头的优势在于它们是“可堆叠的”，这意味着你可以将一个插头插入另一个插头的背面，从而提供被动多路输出（passive multiple）。

## 带通滤波器

一种设备、电路或插件，它允许窄频带频率通过电路，同时拒绝或衰减高于或低于指定的频率。

## 带阻滤波器

一种设备、电路或插件，它会衰减信号中的窄频带，并允许频带之外的频率通过。这与带通滤波器完全相反。

## 乐带轨道 (Band Track)

（有时缩写为 "Track"）指歌曲去除了主人声和/或背景和声后的混音。换句话说，是一个仅包含歌曲乐器部分的混音轨道。

## 乐队 (Band)

- 1. 频率范围，通常由该范围的中心频率确定。
- 2. 一群一起演奏的音乐人。

## 带通滤波器

带通滤波器 (BPF) 保留中心频率、角频率或截止频率附近的谐波，并衰减中心频率以上和以下的频率。根据滤波器中极点（poles）的数量，距离中心越远，衰减越严重；每个极每偏中心一个八度就相当于衰减 6 分贝。

## 带宽

在信号处理中，带宽是指通信通道的可用频率范围，通过设备最高和最低可用频率之间的差值来测量。

## 组 (Bank)

- 1. 内存中声音补丁、序列器数据和/或合成器发生器及调制器参数的集合。
- 2. 作为单元的一组声音模块。

## 小节 (Bar)

在音乐记谱中，bar 是节拍（measure）的另一种术语，指包含特定数量节拍的特定时间段，并用谱两侧的线进行标记。

## 巴克刻度 (Bark Scale)

听觉系统可以被认为是由一系列带通滤波器组成的。有趣的是，这些滤波器的间隔并不严格遵循线性频率刻度或对数音乐刻度。巴克刻度试图确定这些“听觉滤波器”（被称为关键频带）的中心频率和带宽。

## 屏障法 (Barrier Miking)

一种麦克风放置技术，将麦克风放置在反射表面附近。如果操作正确，屏障法可以确保直声和反射声同时到达麦克风，防止两者之间的相位抵消。

## 贝斯节录 (Bass Session)

用于录制作为歌曲基础的贝斯轨道（例如鼓和贝斯）首次音频录音。

## 低音反射 (BassReflex)

一种扬声箱设计，通过箱体内的端口（开口）增强低频频率。其原理是箱体内部扬声器盆背面产生的声压从箱体正面排出，与来自低音单元前面的声音混合。改变端口的大小和位置将极大改变低频的特性。

## 低音 (Bass)

音频频率的较低范围，低至约 250 Hz。一个参考值。

## BBD (桶形延迟)

一种回声或延迟效果的早期设计，输入音频会被采样为模拟电压且持续很短。随后在下一个高于音频采样率的时钟脉冲处，电压将传递到电路中的下一个采样保持单元（bucket）中，并在那里采样一个新水平。桶形延迟 (BBDs) 通常具有 2 的幂级级或桶（256, 512, 1024, 2048 等）；延迟长度由级数乘以样本之间的时间间隔决定。

## 射流效应 (Beaming)

扬声器中的一种现象，高频直接从扬声器射出，而不是与低频一起色散。当你站在扬声器正轴前方时，听起来似乎只播放高频，而不是中频或低频。这种现象通过通过扬声器内的号叭传输高频来得到缓解。

## 节拍映射 (Beat Mapping)

调整录制音乐作品中的节奏变化以适应项目设定节拍的过程。在 DAW 中，这是使用拉伸工具并将瞬态（transients）同步到相应的节拍图中完成的。这种技术通常用于调正在没有节拍器的情况下录制的鼓点或贝斯表演。

## 节拍 (Beat)

- 1. 稳定的、均匀的脉冲。
- 2. 两个频率略不同的声音或音频信号相互干扰，导致音量周期性增加和减少，听起来像“拍频”。

## 拍频现象 (Beating)

当两个振荡器的频率调到非常接近但并不完全相同的频率时，它们之间的差异会导致被称为“拍频”的干扰图案。当频率差低于音频速率时，这听起来像是对组合声音的响度应用颤音（tremolo）。

## 合拍 (Beatmatching)

一种主要由 DJ 使用的技术，用于同步两个录制轨目的节奏，通常通过使用时间拉伸和变调工具，创建从一首歌到另一首歌的无缝过渡。

## 每分钟节拍数 (B.P.M.)

BPM（beats per minute）是表示节奏最常用的方法：每分钟应该数几节拍（通常是四分音符）。每分钟 120 节拍的节奏意味着每秒有两个节拍（120 节拍/分钟 ÷ 1 分钟/60 秒 = 2）。

## 合拍技术

一种 DJ 主要使用的技术，用于同步两个录制轨目的节奏，通常通过使用时间拉伸和变调工具，创建从一首歌到另一首歌的无缝过渡。

# 附录 B：音频工程术语 (0 - 9 - A - Z)

呼吸感（breathing）是廉价压缩或过度压缩的迹象，通常是不受欢迎的，尽管某些工程师和音乐家偶尔会使用它来营造特定的效果。

## 砖墙滤波器 (Brickwall Filter)

一种具有陡峭截止斜率的低通滤波器，其形状类似于“砖墙”。虽然这些滤波器通常出现在 A/D 转换器中以防止混叠，但其陡峭的截止可能会给音频信号引入意外的副作用，例如相位偏移。

## 桥接 (Bridging)

一种将单个输入馈送到放大器两个通道的技术，将其合并为一路，从而有效地使供给信号的放大功率翻倍。

## 布朗噪声 (Brownian Noise)

也称为棕噪声，从技术上讲，它是一种功率密度（频谱亮度）随频率增加而每八八度下降 6 dB 的噪声。它的低音很重，类似于远处的海浪声。它也可以作为缓慢变化的随机控制电压或调制信号，而不是音频源。

## Buchla 邦鼓 (Buchla Bongos)

这是一个经典的接线组合，将一个复杂源（例如一个振荡器调制另一个振荡器）通过通过门（Pass Gate），并带有触发信号来“击打”人声，或者使用一个瞬时攻击/衰减包络来创建一个好听的“噗”声。通过门随着音量同步达到高谐波的特性，有助于抑制来自复杂源的谐波，并使其产生类似于打击脉冲的衰减。

## 桶形传输延迟 (Bucket Brigade Delay)

一种回声或延迟效果的早期设计，其中音频被采样为模拟电压并保持片刻。然后在下一个高于音频采样率的的时钟脉冲处，电压将传递到电路中的下一个采样并保持单元（桶），同时对新的电平进行采样。桶形传输延迟（BBD）通常具有 2 的幂次桶级（256, 512, 1024, 2048 等）；其长度由级数乘以采样之间的时间决定。

## 磁性消除 (Bucking)

一种抵消方式，两个幅度相同但极性相反相同信号或频率相互抵消。最常用于乐器频率。例如，“双降”（Humbucker）吉他拾声器设计旨在利用这种方法消除或“消除”信号中的频率。

## 缓冲多路输出 (Buffered Multiple)

你通常需要将信号分发或复制到多个目标。这通常通过多路输出（multiple）完成，你接入一个源，然后插上跳线线连接到多个目标。有源或缓冲的多路输出在输入和输出之间包含一个缓冲电路，确保信号不会因为分分过多而丢失强度或完整性，并且其中一个输出端发生的异常情况不会影响任何其他连接。某些模块的输出内置了良好的缓冲功能，可以无问题地驱动多个模块。但如果你尝试使用无源多路输出来连接例如三个振荡器，并发现跟踪（tracking）效果不好（当你在音阶上上下移动时，它们会很快跑调），那么你需要一个缓冲多路输出器。

## 批量传输 (Bulk Dump)

系统独占批量传输（System Exclusive Bulk Dump）的缩写，一种在 MIDI 设备之间传输内部参数等数据的方法。

## 脉冲发生器 (Burst Generator)

当你向此模块发送触发信号时，它会响应输出一串或一个“脉冲”触发信号。你通常可以控制触发的数量、它们之间的间距，并且通常可以单个触发输出发送或跳过的概率（用于随机图案）。在最温和的情况下，它可以用于创建响应于普通触发的“双拨弦”触发；在最极端的情况下，它被用于触发一个高能量、混沌的鼓点流，这些鼓点可能与音乐对拍。

## 总线板 (Bus Board)

这种简单的电路板接收你的模块化系统电源的输出，并创建其多个副本，路由到你的各个模块。

## 总线 (Bus)

一种音频路径，将来自不同源的一个或多个信号路由到指定位置。由于总线与信号流紧密相关，它们在音频应用中具有广泛用途。2 通过总线路由的信号本身的简写术语（参见“子组”）。

## 字节 (Byte)

八位一组的信息（数据）位。一个字节 = 八个位。

## 电缆组件 (Cable Assembly)

准备好在特定应用中安装的电缆，通常带有连接器终端。

## 电缆束 (Cable Harness)

用于互连电子系统的电缆或电线组。

## 电缆护鞘 (Cable Sheath)

应用于电缆的导电保护外层。

## 电缆 (Cable)

位于包护护套内的一个或多个绝缘导体、光纤或两者的组合，通常用于传输不同类型的电信号。

## 电容器 (Capacitor)

一种由绝缘体隔开的两个板组成的电子器件，用于储存静能。例如，电容器是电容麦克风中的关键组件。

## 卷轴 (Capstan)

磁带录音机的机械部件，用于控制磁带通过磁带头时的速度。

## 胶囊 (Capsule)

撇开太空旅行的定义不，，麦克风中包含振膜和活性元件部分的名称，即将声波转换为电流的机械结构。

## 碳粒麦克风 (Carbon Microphone)

一种使用碳颗粒将声波转换为电脉冲的麦克风。两个板之间是碳元件；当声波撞击碳颗粒时，它会产生板之间的电阻变化，从而影响电信号。

## 心形指向模式 (Cardioid Pattern)

对正面最敏感的麦克风拾音模式。

## 载波 (Carrier)

携带信息或另一个信号的信号。在调制中，载波是被另一个信号修改的信号。

## 级联 (Cascade)

将一个设备的输出连接或“串联”到下一个设备的输入端。

## 逆时针 (CCW)

Counter-clockwise。

## CD

紧凑性（Compact Disc）的缩写，一种小型光盘。

## 分 (Cent)

音高的的测量单位，半音的 1/100。

## 中心频率 (Center Frequency)

滤波器或均衡器最有效的频率。

## 通道路径 (Channel Path)

音频信号从输入到输出的完整路径。

## 混沌 (Chaotic)

不要相信，混沌并不意味着完全随机。混沌理论处理在特定边界内随机的系统。

## 追踪 (Chase)

自动调整录音机或序列器的速度以保持同步。

## 和弦图 (Chord Chart)

一种提供歌曲基本和弦和关键节奏信息的简写记谱形式。

## 和弦 (Chord)

同时弹出的三个或多个音符。

## 副歌 (Chorus)

1. 歌曲中每次重复时都具有相同音乐和歌词的部分。
2. 一种延迟效果，通过添加带有轻微反馈和中等深度多个延迟来模拟人声合。

## 电路 (Circuit)

1. 电流的一个完整路径。
2. 与定义 1 类似，但包含了用于实现特定音频功能的所有音频信号路径和组件。

## 类兼容 (Class Compliant)

这指的是“即插即用”的设备——它可以直接插入计算机或其他主机，并能立即被识别，无需安装额外的驱动程序。

## 附录：音频工程术语 (0 - 9 - A - Z)

# 节拍 (Click Track)

一种输入耳机监听器的节拍器“滴”声，旨在帮助音乐家在歌曲中保持节奏同步。

# 切波 (Clip)

所有活跃的电子电路对通过的信号强度都有限制。这些限制通常与正、负电源的电平水平有关。如果信号尝试超过这些限制，它们就会在该限制处被削波或切断。例如，+12 伏的输入电压可以无经改变地通过，但输入的 +13 伏输出时将变为 12 伏。这种削波会导致波形失真，通常会增加高次谐（例如刺耳的嗡嗡声）。不同的电路以不同的方式削波——某些在达到平直阈值之前可能会有一定的圆滑处理；这被称为软削波（soft clipping），通常是理想的，因为它听起来不那么刺耳。之所以被称为削波，是因为生成的图形波形看起来就像波形的边缘被“剪切”了。

# 时钟信号 (Clock Signal)

由电路中的设备产生的信号，通过产生稳定的脉冲或代码来使其他设备保持同步。音乐世界中的例子是 MIDI 排序。序列器向连接的设备发送时钟信号，这些设备随之同步节奏播放。

# 时钟 (Clock)

通常指系统中的节奏脉冲。时钟脉冲通常远快于它驱动的任何设备，例如序列器或 LFO（低频振荡器）。常见的时钟速率是 24 ppqn（每个音符），MIDI 时钟和 DIN Sync也是如此。然而，驱动序列器每次前进一个音符的触发信号也可以称为系统中的“时钟”。事实上，某些模块可以对主时钟进行分频和倍频，产生与主时钟关联的新时钟信号。

# 顺时针 (Clockwise)

顺时针，即向右旋转——方向与时钟指针的移动相同。

# 近距离拾音 (Close Miking)

一种麦克风放置技术，将麦克风放置靠近声源的位置以捕捉声音并抑制环境噪音。

# 同轴电缆 (Coaxial Cable)

（缩写 "Coax"）一种双导导体电缆，由一个被屏蔽层包围的导体组成。

# 邻接拾音 (Coincident Miking)

一种双声道拾音技术，将两个麦克风的头部尽可能地靠在一起。这防止了混音中的相位抵消问题，因为声音到每个麦克风的距离是相同的。

# 增压器 (Compander)

一种信号处理器，作为压缩器和扩展器的结合，主要用于模拟系统的降噪目的。音频信号在录制前被压缩，然后在重放阶段被扩展。增压技术（Companding）是降噪系统的原理。

# 比较器 (Comparator)

一种比较一个电压电平与第二个电压电平的电气设备。第二个电压可以是比较器合成器模块上的第二个输入，也可以通过旋钮或内部参考电压设置。大多数情况下，比较器输出一个门控信号，当第一个信号高于第二个信号（或反之）时，信号变为高电平；当第一个信号低于第二个信号时，信号变为低电平。在音频频率下，它将输入波形转换为方波或脉冲波，由第二个信号决定新波形电压变高或变低的时刻。

# 倒辑 (Comping)

# 复合振荡器 (Complex Oscillator)



这通常在一个面板后有一对振荡器，它们是预先接线的：一个振荡器调制频率（称为频率调制或 FM 合成器）；某些模块允许你快速切换它们，使第一个调制第二个的振幅，或其他变体。它们可能内置了波形整形器。它们基于 Buchla 创建的一款流行模块，该模块是合成器“西海岸”设计方法的标准。

# 压缩驱动器 (Compression Driver)

由一个振膜将声波馈入号角形扬声器。

# 压缩比 (Compression Ratio)

压缩器衰减输入信号的速率，以分贝（dB）测量。例如，4:1 的压缩比意味着信号每超过阈值增加 4 dB，压缩器就仅允许信号增加 1 dB。

# 压缩 (Compression)

1) 在信号处理中，由压缩器执行的操作（另参见“压缩器” Compressor）。

2) 在声学中，指由声压波峰值引起的空气压力增加，用于“压缩与稀疏”（compression and rarefaction）的语境（另参见“稀疏” Rarefaction）。

# 比较器 (Comparator)

一种信号处理器或插件，通过放大音频信号安静的部分并衰减较大的部分来缩小音频信号的动态范围。

# 电容麦克风 (Condenser Microphone)

一种通过电容的变化将声音转换为电流的麦克风。声压波移动振膜，改变电容的变化，然后这些变化随后被转换为电电压。

# 接触式麦克风 (Contact Microphone)

一种设计用于捕捉固体物体振动（而非空气中的振动）的麦克风。也称为“拾音器”或“压电元件”，这种麦克风常用作原声吉他拾音器来捕捉面板板的振动，或用于使用各种物体创作“噪音音乐”的实验音乐家。

# 控制电压处理器 (Control Voltage Processor)

CVP 是模块的缩写，允许处理通过它的电压——例如放大或衰减、向正向或负方向偏移、引入斜率（电压变化的平滑处理），以及可能通过比较器从输入电压提取门控信号等其他功能。Noise's Maths 是目前最著名的控制电压处理器；你也会发现名称中专门带有 CVP 字样的模块。无论如何，在系统中拥有一个或多个此类模块是有益的，可以帮助电压实现你的目标（或教它们新花样）。

# 控制电压 (Control Voltage)

控制电压 (CV) 的概念是模块化合成的核心。通用想法是模拟电压电平是模块的控制函数和参数。例如，控制电压可以由振荡器决定音高；如果信号通过电压控制放大器，第二个控制电压可以决定信号的大小。

# 控制器 (Controller)

在最广泛的意义上，控制器是任何用于控制其他设备的设备。最用于 MIDI 控制器，它们发送 MIDI 信号来控制连接的仪器。录音室中的其他控制器示例包括监听控制器、DAW 控制器和 DJ 控制器。

# 角频率 (Corner Frequency)

滤波器的截止或角频率是开始滤波的点。例如，如果一个低滤波器的角频率为 500 Hz（每秒循环），所有 500 Hz 以下的谐波或其他声音成分将不受影响地通过，而 500 Hz 以上的所有谐波将随着距离 500Hz 的增加而被“过滤”——音量减小。

# 逆时针 (Counter Clockwise)

逆时针，通常指控制旋钮向左旋转——与时钟指针的移动方向相反。

# CPU

中央处理器的缩写，计算机中的主“大脑”芯片（也称为“处理器” Processor）。

# 临界距离 (Critical Distance)

声源到直达声与混响声量相同的距离。临界距离随空间变化；在具有吸收墙的房间里，临界距离离声源更远；在混响房间里，距离则更近。

# 交叉淡化 (Crossfade)

一种音频编辑技术，在一种声音逐渐淡出的同时另一个声音逐渐淡入，以在两者之间创建无缝过渡。音频工程师使用交叉淡化，例如融合两个

# 附录 B：音频工程术语 (0 - 9 - A - Z)

将两个或多个“轨道素材”（takes）合并到一个复合轨道中。俱乐部 DJ 还使用交叉淡（crossfading）在不间断的情况下切换歌曲。

# 分频频率 (Crossover Frequency)

分频器停止向一个扬声器发送信号并开始向另一个发送信号的频率。

# 分频 (Crossover)

一种音频滤波器组件，将音频信号分成两个或多个频段或信号，通常根据频率范围输入音箱系统的不同部分。（也称为“分频网络”。）

# 串扰 (Crosstalk)

两个音频通道之间意外的信号泄漏——例如调音台上通道之间的信号重叠，或磁带轨道之间的轨道重叠。

# 提示 (Cue)

广义来说，cue 是一段音乐或一个乐段的起点。根据上下文，“cue”一词可能描述：

- 1) 音乐家或歌手应该开始演奏或演唱的时间点；
- 2) 通过耳机传输给音乐家的音频，以便他们确定何时开始演奏/演唱；
- 3) DAW 中或磁带上音乐时间线上的特定位置点；或
- 4) 设置磁带或歌曲中的某个起始点（“对位”磁带）。一个 cue 可以指用于视频制作的任何音乐部分。

# 截止频率 (Cutoff Frequency)

滤波器的截止频率是其开始过滤的点。例如，如果一个低通滤波器的角频率为 500 Hz，那么所有 500 Hz 以下的谐波或其他声音成分将允许不受损地通过，而所有 500 Hz 以上的谐波将被“过滤”——越高于 500Hz，音量衰减得越厉害。

# 截止斜率 (Cutoff Slope)

滤波器通带之外频率的衰减速率。斜率描述为在超过截止频率后，每八度滤波器减少信号的分贝（dB）数。

# CV/Gate

这是电压的缩写，表示合成器可以通过电压（通常用于控制音高）和门控信号（gate signals）来指示音符何时“开启”。越来越多的控制键盘包含了标准的 MIDI（乐器数字接口）CV/Gate 输出，这使得它们更容易连接到模块化合成器，因为不需要额外的 MIDI 转 CV 接口。

# CV (电压控制)

电压控制（CV）的概念是模块化合成器的核心。基本思想是使用模拟电压电平来控制模块的功能和参数。例如，一个控制电压可以决定振荡器播放的音高；第二个控制电压可以决定该信号在通过电压控制放大器后的音量。CV 是控制电压最常见的缩写——例如，当一个合成器模块说它具有“通过滤波器共振的 CV”时，意味着有一个控制电压输入来控制共振（反馈）的量，而不仅仅是前面板上常见的旋钮。

# CVP (电压处理器)

CVP 是模块的缩写，该模块允许对通过它的电压进行处理——如放大或衰减、在正或负方向上进行偏移、引入滑变（电压变化的平滑），以及可能的其他功能，例如通过比较器从传入的电压中导出门控信号。Make Noise 的 Maths 也许是最著名的控制电压处理器；你也会发现名称中专门带有 CVP 的模块。无论如何，在系统中拥有一个或多个此类模块是有好处的，可以帮助调控电压以获得想要的结果（或教它们一些新花招）。

# CW

顺时针（Clockwise），如向右旋转控制旋钮——与时针移动的方向相同。

# 周期 (Cycle)

波形从某一点开始的一个完整表达式，通过零线到达波形的最高点和最低点，并返回起始点的值。一次完整的振动或声波。

# D-Sub 连接器

“D型连接器”（D-subminiature connector）的缩写，D-sub 多针连接器，通常用于将计算机连接到 VGA 显示器，但也偶尔用于录音室的数字音频应用。

# D/A (数字转模拟)

数字转模拟转换的缩写，将数字数据（数字音频信号）转换为离散的电压电平。A/D 的相反过程。也称为 DAC。

# DADSR

这是对 ADSR 包络发生器的略微复杂的改进，在初始攻击阶段（从 0 升到峰值水平）之前引入了初始延迟。一种连接思路是将此类包络路由到低通滤波器的截止频率，这样当音符开始时，声音是静音且经过滤波的，在暂停之后，它开始逐渐变成更亮、更饱满的声音。

# 链链 (Daisy Chain)

三个或更多设备的串联连接，其中音频信号通过一个设备到达第二个设备，再通过第二个设备到达第三个设备。

# 阻尼系数 (Damping Factor)

描述放大器在音频信号停止时抑制扬声器振动锥推回运动（反向电动势）的能力。

# 阻尼 (Damping)

通过摩擦减少振动系统中的能量。可以指电信号中振幅的减小，或乐器受抑制的波动（例如声钢琴上的消音踏）。

# DAW

数字音频工作站（Digital Audio Workstation）的缩写，一种用于数字录制和混合音频的设备或软件程序。

# dB

分贝（decibel）缩写，比较信号强度（通常为音频电平）的测量比例。

# DBX

该公司开发的系列噪声系统。

# 直流耦合 (DC Coupled)

当一个模块说它是耦合的时，意味着有一个控制电压输入来控制信号的量——而不仅仅是前面板上常见的旋钮。

# DC (直流)

沿一个方向流动的电流，与交流电（AC）相反。在音频术语中，DC 指直流电压。

# 直流偏移 (DC Offset)

在音频术语中，直流偏移是添加到信号中的恒定电压，使其偏离零。

# DCO (数字控制振荡器)

数字控制振荡器，使用数字信号控制振荡器以确保调性的混合设计。

# 去齿 (De-esser)

一种用于减少齿音（尤其是“s”音）的音频压缩器。

# 衰减 (Decay)

广义来说，decay是指声音随时间消失。它也可以指混响或包络发生器的尾迹。

# 卡树 (Decca Tree)

一种麦克风放置技术，涉及三个以T型型排列的全指向麦克风。通常用于合唱团、交响团和大型乐队。

# 去磁 (Degussing)

使物体去磁的过程。在音频领域，去磁本质上是擦除磁带。

# 延迟 (Delay)

你知道延迟在通常世界的含义；它在模块化合成器内部以不同形式出现。例如，它可以指回声之间的间距；延迟设备被称为“延迟”效果。它也可以指你延迟信号的可编程时间，例如门控、触发或包络的初始阶段，使其比播放时间推迟。

- 1) 一种将音频信号录制到介质或设备并在之后复制，然后与原始非延迟信号混合以产生各种效果，如饱满的声音、回声、颤音调制等。
- 2) 信号处理器产生延迟。

# 演示 (Demo)

一种录制品，旨在让听众了解歌曲在最终制作中的可能效果。演示涉及极少数的跟踪，几乎是录音的“草案”。

# 离调 (Detune)

故意使用乐器或跑调演奏（显然是轻微的）。这种效果在录音室可以用于多种目的，但通常用于“双轨”，将离调的乐器/轨道与原始轨道混合以创建更饱满的声音。

# 附录 B：音频工程术语 (0 - 9 - A - Z)

通过使用电拾音器或直接传输盒将电音频信号直接从乐器发送到调音台的过程，而不是使用麦克风。

# 对白 (Dialogue)

录在电影/视频声音、广告和教学录音中的口语内容。

# 振膜 (Diaphragm)

麦克风中随声波移动的部分，将其转换为电信号。

# 差值 (Difference)

一种从另一种控制电压中减去电压的说法。它也可以应用于音频或谐波。

# 数字音频工作站 (Digital Audio Workstation)

（简称 DAW）一种以数字方式混合音频并创建数字音频文件的设备或计算机软件。DAW 可以是独立单元，也可以是集成组件，但今天它们最常见的形式是来自计算机的“箱内”软件程序。录音室中最常见的 DAW 程序是 Pro Tools；其他常用程序包括 Reason、Ableton 和 Logic。

# 数字万用表 (Digital Multimeter)

一种测试电电压、电流和电阻的小型设备。万用表在录音室中用于校准电气系统和排除故障。

# 数字录音 (Digital Recording)

将音频信号转换为代表波形的数字的过程，并将这些数字存储为数据。

# 数字信号处理 (Digital Signal Processing)

（简称“DSP”）在模拟音频信号转换为数字音频后进行的任何信号处理。

# 数字模拟转换器 (Digital to Analog Converter)

（简称 D/A）一种将数字音频的数字数据转换为接近原始模拟音频电压水平的设备。

# 数字 (Digital)

曾有段时间，“数字”（指的是基于二进制逻辑、计算机，以及与构成模拟电路的老式晶体管、运放大器、电容器和其他元件相比的）在同义词中是一个贬义词。人们假设数字产生的声音更加冷冰冰、脆弱且具有刺性——而不仅仅是“不真实”。今天，数字电路在模块化系统中被广泛采用。尽管模拟在我们心中始终占有特殊地位，但实施良好的数字电路听起来可以和模拟一样好，而数字信号处理和编程可以产生比大多数模拟电路更广泛的声音。

# 数字控制振荡器 (Digitally Controlled Oscillator)

DCO（数字控制振荡器）是一种模拟振荡器的混合设计——它不再使用电压水平来确定振荡器的频率，而是使用计数器等数字设备来确定每个波形的长度，从而确定频率。其优点是，调音非常稳定，不像某些全模拟设计。缺点是，当使用多个振荡器声部时，频率上没有缺陷，导致产生细微的调偏（从而产生对声音“厚实感”的感知）。

# DIN 立体 (DIN Stereo)

一种立体麦克风放置技术，将两个心心形麦克风间隔约 20 厘米，并向外呈 90 度角以创建声场。特别适用于近距离立体拾音。（参见“近场拾音”。）

# DIN 同步 (DIN Sync)

一种用于控制序列器、分解器和鼓机节奏的时钟信号，使用带有 DIN 风格连接器的电缆进行传输（就像老式的 MIDI 连接器一样，DIN Sync 甚至更老）。Roland 开创了这一标准，该标准包括每四分符发送 24 个脉冲 (PPQN)，产生了替代的 Sync24。Korg 设备使用了此标准的变体，以每四分符 48 个脉冲运行，也称为 Sync8。DIN Sync 仍然是向模块合成器发送时钟信号的流行方式，特别是在与其他复古合成器、序列器和鼓机连接时。

# 二极管阶梯滤波器 (Diode Ladder Filter)

这种滤波器设计通常与 Roland TB-303 Bass Line 相关，该设备以具有深层共鸣的橡胶声闻名。

# 二极管 (Diode)

一种允许电流向一个方向流动而在另一个方向不流动的电子元件。在录音室中，这些通常出现在电子管放大器的真空管中。

# 直接传输盒 (Direct Box)

一种将非平衡、高阻抗的扬声器或乐器级输出转换为平衡、低阻抗麦克风级输出的小型设备。经常用于将乐器“直接”连接到调音台的信号路径，而不是通过声学方式拾音。也称为“直接注入盒”或“DI Box”。

# 直流 (Direct Current)

在模块术语中，DC 指倾向于在一个稳定水平保持一段时间的电压，例如门控输出在音符关闭时切换到 0v，音符开启时切换到 5v 或 10v。它也可以上升为缓慢变化的电压，如包络（“DC”）。以单方向流动的电流，与交替流动的交流电（AC）相反。许多电子设备由直流运行，通常由电池、USB 电源或插入墙座的 AC 适配器提供。

# 直接注入 (Direct Injection)

（简称“DI”）通过使用电拾音器或直接传输盒将电音频信号直接从乐器发送到调音台的过程，而不是使用麦克风。

# 直接输出 (Direct Out)

某些调音台上的可用输出，它直接从输入的前级放大级馈送，跳过了通道条和推子。此功能通常用于将“干”信号发送到监听混音或录制设备。

# 直接声 (Direct Sound)

在不碰撞或反射任何障碍物到达麦克风或听者耳朵的声音（与反射声或环境声相反）。

# 方向性模式 (Directional Pattern)

- 1) 在麦克风中，一个术语，意思是“拾音模式”，描述麦克风对声音最敏感的区域。
- 2) 在扬声器中，它是扩散模式，即扬声器声音在听音区域均匀覆盖的区域。

# 扩散 (Dispersion，也称为扩散角)

扬声器发出的声音有效覆盖的区域；具体来说，在声音两侧的虚拟边界，该处的声压比你直接站在扬声器前要低 6 dB。每个扬声器都有水平和垂直扩散角。

# 远麦克风 (Distant Microphone)

将麦克风放置在声源远处的技术，以便捕捉直接声和反射声的结合。

# 失真 (Distortion)

指与输入相比，设备输出波形的变形，通常由于过载、失真或“脏”信号引起。虽然电气或音频失真通常是不受欢迎且需要避免的，但在受控的情况下经常被用于产生某些理想的效果，特别是在电吉他和扩放大器上。

# 多样性 (Diversity)

- 1) 在音频设置中：在无线接收系统中使用两个天线以防止无线接收音频中断。
- 2) 在其他设置中：对个人独特性的尊重。

# 杜比 (Dolby)

一家降噪系统和其他音频系统制造商的品牌，用于提高音频录制、回放和传输的性能和保真度。

# 多普勒效应 (Doppler Effect)

人耳感知移动声音频率（音调）变化的现象。当声源靠近时，声波到达耳朵的距离变短，增加了波频和音调；当声源远离时，声波必须传播更远，导致频率降低。这种效应的一个常见例子是紧急车辆的警报声在靠近时声音较高，经过后变低。多普勒效应可以利用在音频设置中，例如在 Leslie 扬声器中，电动机带动箱内的扬声器旋转，不断改变声源与听者（或麦克风）之间的距离，产生其独特的颤音效果。

# 附录 B：音频工程术语 (0 - 9 - A - Z)

## Double (双轨)

- 1) 录制一段与第一次表演高度匹配的第二次表演，目的是混合这两个轨道。
- 2) 使用具有中等延迟的延迟线来模拟双轨录音。

## Driver (驱动单元)

- 1) 扬声器中的换能器，将电信号转换为声压波。
- 2) 控制连接设备或硬件的计算机程序。

## Dropout (信号丢包/断断声)

磁带上音频信号的短暂丢失，或数字音频文件中数据的短暂丢失（通常由于采样丢失引起），这会导致音频出现不希望的凹陷、断裂声或啪啪声。

## Drum Machine (鼓机)

一种电子设备，内存中包含合成和采样的鼓声，并配有一个内部序列器，该序列器可以编程播放鼓点模式或循环。

## Drum Pattern (鼓点模式)

由鼓手演奏或在鼓机中序列化生成的、用于歌曲的特定鼓声序列。

## Dry (干声)

没有任何效果的声音被称为“干声”；带有效果（如混响）的声音以“湿声”的形式混合。单元或调音器具有湿/干比调节，用于设置原始未处理声音与完全效果化声音之间的比例。

## DSP (数字信号处理)

## Dub (or Dubbing) (混录/叠录)

- 1) 复制录音。
- 2) 实时录制，并意图同时混合这两段录音，也称为“Overdub/Overdubbing”。



- 3) “Dub”是“dubstep”（低步滚）的缩写，电子音乐的一种风格或子类型。

## Ducking (压限)

一种基于压缩的音频效果，其中音频信号根据另一个音频信号的存在按比例降低，有时通过与信号处理器的“侧链”（`sidechain`）连接来实现。一个著名的例子是在音乐轨道上录制的旁人语音轨道，当演讲者说话时，音乐音量会下降。更微妙的例子是音频工程师“压低”某个轨道以为轨道中的其他部分留出空间；例如，当贝斯吉他信号触发鼓或吉他电平的轻微降低。（另见“Sidechain”）

## Duophonic (双声)

Duophonic 的意思是“声音”。早期合成器（包括模块化系统）是单声的，这意味着它们一次只能弹一个音；乐器拥有足够的振荡器、滤波器、包络和放大器，可以同时播放两个独立的音符。模块化合成器的 MIDI 接口包含双声模式，让你可以从键盘接线并控制两个独立的声音。某些用户会混用 `duophonic`（双声）、`monophonic`（单声）和 `polyphonic`（多声）等术语。

## Duration (时长)

时长是长度的另一种表达方式。在一定时间内（例如 100 秒）保持高电的时钟脉冲或门信号被称为持续了 100 msec。你按下音符的时间或序列中一个步骤的长度也被称为其时长。

## Dynamic Microphone (动态麦克风)

（也称为动圈麦克风）通过在磁场中移动的感应线将声压波转换为电音频信号的麦克风——这一过程通常被比作扬声器的反向工作。动态麦克风灵敏度低于电容麦克风，但在处理大声源或近距离拾音应用时非常有效。

## Dynamic Processing/Dynamic Signal Processing (动态处理/动态信号处理)

自动改变电平（或增益）以改变最强音频与最弱音频之间水平关系的过程。动态处理器包括压缩器、限制器、扩展器和门限。

## Dynamic Range (动态范围)

- 1) 歌曲或录音中最强峰值与最弱电平之间的比例（dB）。
- 2) 设备或系统在不失真的情况下能提供的最低与最高电平之间的比例（dB）。

## Early Reflections (早期反射)

声波在房间表面反射后到达听者耳朵的第一批声波，通常在初始声音后几乎立即听到。混响的第一阶段。

## East Coast Synthesis (东岸合成)

这是一个统称，适用于由 Moog、Arp 和 EML 等位于东岸的公司（以及 Roland 和 Korg 等“远东”公司）开创的大多数合成器配置。其中，一个或多个产生丰富谐波波形（如锯齿波或方波）的振荡器输入滤波器，移除其中一些谐波，然后进入放大器以塑造音符的响度。这种方法也被称为减法合成，因为滤波器减少（减去）了来自振荡器的谐波。东岸合成器还具有风琴风格的黑白键，以及四级 ADSR 类型包络。如今的趋势是在同一个系统中混合使用东岸和西岸的方法。

## Echo Chamber (回声室)

一个封闭的房间，设计有反射性的非平行表面，用于创建声学回声（混响）。

## Echo (回声)

声波在表面反射引起的初始声音明显重复。当源与反射点之间的距离足够远，我们可以检测到它们之间的时间延迟时，我们将声音识别为回声。本质上，混响是许多回声快速组合的结果，无法单独听到每一个。在录音室内，回声可以通过声学方式复制，也可以通过数字处理器模拟。

## Edit (编辑)

完成后更改录制声音的一个或多个参数。这可以有多种形式，包括“挖补”重录一段音乐以替换原始版本；改变波形的形状/大小。在现代，这是在数字音频工作站（`DAW`）中完成的。

## Effect Loop (效果环路)

有时效果环路允许信号发送到外部效果处理器，然后返回信号路径。这通常通过侧链连接实现。

## Effects Processor (效果处理器)

自动改变电平（或增益）以改变最强音频与最弱音频之间水平关系的过程。动态处理器包括压缩器、限制器、扩展器和门限。

## Effects Track (效果轨道)

- 1) 歌曲或录音中最强峰值与最弱电平之间的比例（dB）。
- 2) 设备或系统在不失真的情况下能提供的最低与最高电平之间的比例（dB）。

## Effects (效果)

- 1) 完成后更改录制声音的一个或多个参数。
- 2) 完成后更改录制声音的一个或多个参数。

## EG (包络发生器)

包络发生器模块用于在连接 `VCA`（电压控制放大器）时塑造音符的响度，或在连接 `VCF`（电压控制滤波器）时塑造其频率内容或音色。为了实现这一点，包络发生器产生一个通常从 0 伏上升到最大值的电压，然后下降。你控制这种变化，通常分为四个阶段：起始阶段从 0 到最大值，衰减阶段从最大值下降（此处后续取决于具体设置）。

## Envelope Follower (包络跟随)

该模块跟随声音的响度轮廓，并输出与响度变化相应的电压。它们倾向于对信号进行平滑处理，使其不会过于敏感或跳跃。包络跟随器还有一个门输出，在输入信号响度较高时变为高电平，在低于该电平时变为低电平。

## Envelope Generator (包络发生器)

包络发生器模块用于在连接 `VCA`（电压控制放大器）时塑造音符的响度，或在连接 `VCF`（电压控制滤波器）时塑造其频率内容或音色。为了实现这一点，包络发生器产生一个通常从 0 伏上升到最大值的电压，然后下降。你控制这种变化，通常分为四个阶段：起始阶段从 0 到最大值，衰减阶段从最大值下降（此处后续取决于具体设置）。

## Electret Microphone (电极麦克风)

一种使用电极代替电容器的电容麦克风变体。也称为电极麦克风。由于电极是永久极化的，因此电极麦克风不需要外部电源。

## Electret (电极材料)

电介质板被设计具有永久极性，使其功能类似于磁铁。（“Electret”源于“electricity”和“magnet”两个词。）

## Electromagnetic Field (电磁场)

（缩写为 `EMF`）由于电流通过导体产生的磁能场。

## Electromagnetic Interference (EMI) (电磁干扰)

全球音频专业人士的噩梦，`EMI` 是由电磁活动引起的干扰类型，会被音频电缆和设备吸收，引起不需要的噪声、嗡嗡声或干扰声。音频系统的 `EMI` 原因包括大电流线、荧光灯、调光开关、计算机和无线发射器。

## Electrons (电子)

原子周围运行的带负电粒子。电流是由电子沿金属导线移动产生的。

## Emphasis (强调)

这个词有两个含义。在正常的音频语境下，它通常是指高频增强，强调高谐波增加音色的清晰度并有助于与其他区分。在合成器中，强调通常指滤波器上的 `Q` 或共振设置，因为增加这些设置会增强（强调）截止频率或频率范围内的谐波。

# 附录 B：音频工程术语 (0 - 9 - A - Z)

`AD`，攻击/衰减（`Attack/Decay`）包络，或称为持续（`sustain`）的中间水平，然后（通常在按键释放且相应信号回到零后）从持续电平回到零，持续时间被称为释放（`release`）。

## 包络跟踪 (Envelope Tracking)

这描述了包络跟随器的主要动作：模块或模块的某个部分，它跟随信号的响度并输出一个与轨迹（即输入信号）对应的电压。

## 包络 (Envelope)

声音的四个元素的统称：攻击（`Attack`）、衰减（`Decay`）、持续（`Sustain`）和释放（`Release`），简称 `AS`。声音的包络描述了声音或音频信号的强度随时间变化的情况。

## 等响响度曲线 (Equal Loudness Contours)

由几条曲线组成的图，显示了不同频率的音调必须达到多大的响，人们才能认为它们具有相等的响度。（参见“费莱彻尔-蒙森曲线”）

## 均衡器 (Equalizer)

音频信号处理器使用一个或多个滤波器来增强或削减声音中某些频率的振幅（音量）。其原理是平衡或“均衡”音频系统的频率响应，或者在声学空间中的多个信号之间建立平衡。然而，音频工程师可以使用均衡器以许多方式改变或“染色”声音。

## Eurorack

`Eurorack` 也许被认为是最流行的模块化合成器格式，有 100 多家制造商和 1000 多个模块可用。它由 `Doepfer Musikelektron` 于 1995 年创建，其尺寸基于 `Eurorack` 实验室设备格式。有些用户会告诉你 `Eurorack` 的“音色”听起来没有其他格式好，但那仅仅基于少数标准制造商的模块；标准格式本身并没有任何让最终声音产生巨大差异的地方（不；12 伏和 15 伏电源之间的差异对大多数耳朵来说并不足够大）。

## 扩展器 (Expander)

一种信号处理器（或插件），它执行类似于压缩器的功能，但是扩展音频信号的动态范围而不是压缩它。它通过进一步降低低于设定阈值的信号的振幅来实现这一点。

## 扩展比例 (Expansion Ratio)

扩展器衰减输入信号的速率，以分贝为单位测量。例如，`2:1` 的扩展比例意味着信号每低于阈值 1dB，扩展器就会将信号减少 2dB。如果信号低于阈值 3dB，扩展器会将其衰减 6dB，依此类推。

## 指数 (Exponential)

通俗上讲，这是一种数学曲线，起始相对平坦，然后弯曲陡峭上升。在合成器术语中，它通常指控制电压方案，其中 1 伏的变化对应于音高的增加一个，即每秒循环（振动）次数翻倍。这与线性系统形成对比，在线性系统中，1 伏的增加始终会导致每秒循环数的相同增加。

## 淡出 (Fade)

逐渐降低音频信号电平，或从一个预设电平到另一个电平的逐渐变化。

## 推子 (Fader)

一种用于调整进入调音台通道或通道组的输入信号电平（增益或衰减）的控制。

## 远场 (Far Field)

远离扬声器的区域，在该区域内声音随距离增加一倍下降 6dB，直到达到临界距离。远场的开始取决于扬声器的大小，但在大多数情况下，远场从声源约 3 英尺处开始。音频工程师在精调混合时经常同时使用近场和远场监听。（参见“临界距离”、“近场”）

## 馈送 (Feed)

向发送音频或控制信号。

## 反馈控制 (Feedback Control)

延迟线或延迟效果上的控制，用于控制进入系统的反馈量。

## 反馈 (Feedback)

将输出信号的一部分返回到系统的输入。这可以通过反馈电路以受控的方式进行，以改变乐器的声音（最常见电吉他或模拟合成器）。它也可以描述当开启的麦克风拾取附近扬声器的声音时产生的意外反馈环，产生巨大的震荡频率，其强度不断增加，直到通过关闭麦克风或使用均衡器衰减该频率打破反馈环。

## 保真度 (Fidelity)

描述声音从原始源再现准确程度的术语。

## 八字形模式 (Figure-8 Pattern)

一种麦克风拾音模式，对拾取麦克风正前方的声音最敏感，有效抑制来自侧面的声音。

## 滤波器 (Filter)

一种减少或消除通过它的声音中的某些频率和谐波的模块。在合成器中，最典型的滤波器类型是低通（允许所有截止频率或角频率以下的谐波不受影响，然后随着超过该截止频率进一步减少高阶谐波的电平）、高通（允许所有截止频率以上的谐波不受影响，并减少截止频率逐渐越来越低的谐波的电平）、带通（截止频率附近的谐波完整通过，且越偏高于或低于截止频率衰减得越多）以及陷波（截止截止频率附近的谐波被减少或完全切除；其它的谐波则允许保留）。

## 飞行器 (Flanger)

一种通常被识别为产生“喷气式飞机起飞”嗖嗖声的信号处理器。面板后面发生的是一个被延迟了极小幅量的信号副本（比合唱效果长；比回声效果短），并将其混合到原始信号中。当延迟恒定时，结果是“梳状滤波器”，某些谐波在以反相位叠加混合时被抵消。当延迟随时间变化时，它会产生扫描效果。这种效果最初是在模拟磁带录制中产生的，通过播放两段相同的歌曲磁带，让它们同步开始，然后用手指在其中一个磁带的法兰边缘滑动以产生延迟。在这些类型中，飞行效果是通过延迟总线或数字脉冲实现的。

## 飞行效果 (Flanging)

一种通过将信号与其略微延迟的副本混合，并修改延迟副本产生的音频效果，产生“旋转”声。

## 平直 (Flat)

- 用于描述设备或扬声器频率响应均匀的术语，意味着设备/扬声器不需要均衡即可处理所有频率。在图形显示时，频率响应显示为没有峰或谷的直线。
- 在音乐中，描述音准错误的音符，听起来比实际频率略低。
- 在音乐记谱中，一种符号标记，指示演奏者将音符降低一个半音。

## 费莱彻尔-蒙森曲线 (Fletcher-Munson Curves)

也称为“等响度曲线”，一组图表，用于说明人类耳朵在不同音量水平对不同频率的响应。在两个研究人员首次绘制这些曲线之后。（参见*等响度曲线*。）

## 触发器 (Flip-Flop)

在二进制逻辑中，触发器在接收到输入触发时会在高低电平之间切换（例如，第一次触发将输出置为高，第二次触发将其置为低，依此类推）。在时钟或音频术语中，它将输入时钟或方波的速度减半。

## 浮空平衡线 (Floating Balanced Line)

一种连接“变通方案”，通过修改线路中的连接以类似于平衡线路，将非平衡输出连接到平衡输入，从而消除不需要的嗡嗡声或滋声。

## 飞入 (Fly In)

向混合或录制中加入没有同步的声音。

## 附 B：音频工程术语 (0 - 9 - A - Z)

### Flying Bus（飞行总线）

这是一个非常简单的电源分配或总线板，通常使用一种沿长度带有多个连接器的带状电缆，将电源的输出分配到各个模块中。它们价格低廉且易于安装，但在某些情况下可能会导致模块之间产生噪声共享。

### FM

频率调制（`Frequency modulation`，简称 `FM`）是指一种合成技术，其中一个振荡器的频率以极快的速度（音频速率）被另一个振荡器改变（调制）。结果是一组复杂的谐波侧带，这些谐波可能非常和谐，也可能非常刺耳且与主振荡器的基频“不和谐”。

### FOH（调音台控制区）

在现场音频环境中，指场馆内舞台对面的位置，用于控制和调音表演的现场音频。

### Foldback（监听/返送）

一种用于现场音频的舞台监控系统。一组被称为监听器或楔形音箱（在英国国家称为“foldback speakers”）的舞台音箱，是一组特殊的音频信号混合，供舞台表演者听音并演奏。这种混合通常与观众听到的 `FOH`（调音台）混合不同，有时由独立于主系统的第二个放大器和音箱控制。这种类型的舞台监控经常受到麦克风反馈的影响，并且在某些场馆中可能会引起不希望的反射噪声，导致 `FOH` 工程师难以为观众创造良好的混音效果。由于由于原因，许多现场音频系统使用耳机式监听（`in-ear monitoring`）作为舞台音箱的替代方案，以控制舞台噪声并降低反馈风险。

### Foot Pedal（脚踏）

由音乐人用脚控制的特效设备。

### Foot Switch（脚开关）

放置在地面上由音乐人按下执行各种功能的开关。

### Force-Sensing Resistor（力敏电阻）

在模块化系统中，`FSR`（`Force-Sensing or -Sensitive Resistor`）通常呈圆垫状，你通过按它来改变参数。它像一个电阻，按得越用力，电阻就越小。

### Formant（共振峰）

许多乐器具有振动道——包括你自己的声道——当你发送这些音调时，它们会有某些喜欢振动或“共振”的频率，它们会增强声音（或其某些谐波）的频率以匹配这些共振频率。这些每一个共振频率被称为该乐器的共振峰。合成类人声音的一种常用方法是将振荡器通过一个具有多个共振峰的滤波器或均衡器，这些峰之间的间距模拟了某些元音。

共振峰（`Formant`）是声音或乐器声音中不随音高变化而改变频率的元素。共振峰本质上是由于声源的物理结构产生的“固定”频率或共振。这些频率创造了音色，这种声音元素创造了吉他、笛、男声或女声等的特定声音。

### Format（格式）

- 1) 用于存储和播放音频的多种不同媒介之一，无论是在录音室还是出于听目的。示例包括目前使用的物理格式，如黑胶唱片和光盘；过时的格式，如磁带、8 轨道磁带和 `DAT`；模拟录制存储如开盘多轨道磁带；以及许多不同的数字音频文件，如 `mp3`、`WAV`、`WMA`、`AIFF` 等。
- 2) 格式也可以描述录制到模拟磁带时的特定参数，如轨道数、宽度、间距和顺序。
- 3) 为使用准备准备硬盘或内存卡，通常在此过程中擦除所有现有数据。

### Four Quadrant Multiplier（四象限乘法器）

四象限乘法器幅度调制（`AM`）的一种特殊情况。它也被称为环调制或平衡调制。一个信号改变“倍数”电平——第二个信号的电平。典型用法是两个以音频速率运行的 `VCO` 输入到调制器（四象限乘法器）。输出是一组复杂的分量音，这些音并不遵循谐波通常遵循的基于基频八度的“音乐”间隔。也就是说，调制频率既被加上又从载波频率去；产生的谐波取代了原始载波和调制器。假设载波是 600Hz 的正弦波（存在的基谐波），调制器是 100Hz 的正弦波。结果是一个频率分量为 500 和 700Hz 的音。

### FracRack（分级框架）

一种由 `PAIA` 和 `Blacet Research` 提出的不常见的模块化合成器格式。它代表 `Fractional Rack`；一个单元宽为 1.5 英寸（3.8 厘米），高为 3U（或 5.25 英寸/13.3 厘米）。

### Fractional Rack（分级框架）

一种由 `PAIA` 和 `Blacet Research` 提出的不常见的模块化合成器格式。它代表 `Fractional Rack`；一个单元宽为 1.5 英寸（3.8 厘米），高为 3U（或 5.25 英寸/13.3 厘米）。

### Frequency Modulation (FM) Synthesis（频率调制合成）

一种声音合成方法，其中一个振荡器（载波）产生的频率由一个或多个额外振荡器（运算）的输出改变，以创建丰富的谐波声音。

### Frequency Range（频率范围）

- 1) 电子设备输出有用信号的频率范围（见“带宽”）。
- 2) 对于声源可以实质性传输或接收的频率范围。每种乐器都有其可以演奏的频率范围；耳朵也可以在特定的频率范围内听到。

### Frequency Response（频率响应）

音频系统组件能够充分处理、传输或接收的高低频之间的范围。

### Frequency-Agile（频率跳变的）

在无线系统中，频率跳变描述系统在特定带宽内选择频率上运行的能力。频率跳变系统优于现场巡演和无线信号密集的区域（如大城市）。

### Frequency-Shift Key (FSK)（频移键）

### Frequency（频率）

在特定时间内特定事件发生的次数。在音频和声学中，频率特指每秒完成循环的次数，以赫兹（`Hz`）为单位。在声音中，频率决定了我们听到的音高。波长越长，每秒循环越少，音高越低。



## Front-of-House（现场控制）

（简称 `FOH`）在现场音频环境中，指场馆内舞台对面的位置，用于控制和调音表演的现场音频。

## FSR（力敏电阻）

在模块化系统中，`FSR`（`Force-Sensing -Sensitive Resistor`）通常呈圆垫状，你通过按它来改变参数。它像一个电阻，按得越用力，电阻就越小。

## Full-Normalled（全矩阵）

描述跳线板内的配置，其中插孔形成一条连接路径，直到插入跳线线来改变连接。当跳线板为“全矩阵”时，通过在输入或输出端插入线来改变连接；当为“半矩阵”时，只有在输入端插入线时路径才会改变。“非矩阵”或“开路”意味着没有内部连接，每个输入都向相应的输出发送信号。

## Full-Wave Rectifier（全波整流器）

全波整流器将任何负电压反转为正电压。这实际上使许多波形（如三角波和正弦波）的频率增加。

## Function Generator（函数发生器）

函数发生器在合成领域有两种含义。一种，产生正弦波或方波等波形的测试设备被称为“函数发生器”。二，包络发生器有时被称为“函数发生器”。在这两种情况下，“函数”都意味着执行某种操作，例如创建周期性波形或响应触发产生上升和下降。

## Fundamental（基频）

（也称为基频或第一谐波）发声中存在的最低频率

# 附录 B：音频工程术语 (0 - 9 - A - Z)

通过乐器或人声产生的音。

# 增益控制 (Gain Control)

一种改变放大器或电路增益的设备，通常是一个可以旋转的旋钮（电位器）。在调音台上，每个通道通常都有自己的增益控制，用于调节进入调音台的信号增益——不要与通道“推子”（`fader`）混淆，推子用于调节已经放大信号的输出。

# 增益衰减 (Gain Reduction)

压缩器或限制器调节音频信号幅的行为。

# 增益结构 (Gain Structure)

一个描述音频系统中多个组件互连关系，以及在每个点发生的增益增加或减少量的的术语。良好的增益结构意味着组件正在正常协同工作，以最小的失真或噪声提供最佳增益。

# 增益 (Gain)

音频信号强度的增加量，通常用 `dB` 表示。

# 门检测器 (Gate Detector)

这是模块化合成器内部传输的主要信号类型之一。当一个新的音符应该开始时（例如当你按下键盘控制器上的键时），或者当序列器跳转到下一个“阶段”或音符时，它会跳到高电平——通常为 `5 伏特`。门信号持续整个音符期间（即门被按期间），并在音符结束时（即释放门时）突然下降或“变低”到其静止电平——通常为 `0 伏特`或其他数字。在实践中，当门信号进入典型的包络发生器时，门的开始（变高时）告诉包络器通过其攻击（`Attack`）和衰减（`Decay`）阶段；当门保持高电平时，包络保持在维持（`Sustain`）电平，当门再次变低时，包络进入其释放（`Release`）阶段。

# 代际损失 (Generation Loss)

录音音频复制时清晰度的减少，由于增加了噪声和失真引起。

# 代际 (Generation)

用于描述录音音频复制次数的术语。

# 滑音 (Glide)

指从一个音平滑移动到另一个仍然可听的音符。这种效果的音乐术语是滑音（`portamento`），即音符之间的连奏。在合成器中，这种效果是通过使音符音高的控制电压从上一个音符音高滑动而不是离散跳转来实现的。创建这种效果的模块有时被称为斜率发生器（`slew generator`）、斜率限制器（`slew limiter`）、斜坡发生器（`slope generator`）或延迟（`lag`）。可以使用 `glide`、`glissando` 和 `portamento` 术语，但如果你想计较细节，`glissando`（`gliss`）是一种不同的效果，其中中间音符更加清晰——例如按顺序快速播放——而不是连奏。

# 黄金分割 (Golden Section)

（也称为黄金比例）高度、宽度与长度的比例，其中宽度约为高度的 `1.6` 倍，长度约为高度的 `2.6` 倍。这种比例由古希腊人首次计算，在数学上称为“`phi`”，用于许多应用中的最佳比例，包括房间尺寸和录音室设计（以实现房间内的“最佳声学”），甚至是某些声学乐器的设计。

### 颗粒合成 (Granular Synthesis)

颗粒合成可以被认为是应用于声音的粒子理论。“颗粒”——持续时间为 `1-50` 或 `100 毫秒`。这些微小的片段随后被播放以重现声音，或通过改变单个颗粒的速度、音高、音量、播放顺序和方向来创建新声音。你可以在这些修改过的颗粒之间进行交叉淡入淡出，或者叠加更多颗粒。结果涵盖了音频处理技巧，例如在不改变音高的情况下改变速度以及反之亦然，创建幻幻的声音“云”（这里有一个名为 `Clouds` 的流行模块）。

# 图形均衡器 (Graphic Equalizer)

一种均衡器，可以使用分配给特定频段的推子调整输入信号的各种频率。（另见“均衡器”）。

# 地线提升插头 (Ground Lift Plug)

一种将三脚电源线适配为双脚插座的适配器。某些工程师错误地使用这种插头来中断接地连接以防止嗡嗡声，但不通过其他方式对设备接地的情况下断开接地是非常不安全的做法。

# 地线提升开关 (Ground Lift Switch)

一种中断一个电路接地点与另一个接地接地之间之间的开关，用于消除由地环引起的嗡嗡声或噪音。

# 地环 (Ground Loop)

当一个或多个电子设备在不同点连接到同一个地时产生的情况。设备在不同的地电位下运行，在地线上产生电压，导致低频嗡嗡声，这可能令人烦恼，最坏的情况下会导致损坏。地环的最好解决方法是使用中央电源在同一点连接所有设备。另一种解决方案是通过地线提升开关或插头打破环路，但如果这属于电子设备的不安全管理，应尽量避免。

# 分组 (Group 或 Grouping)

调音台上的若干输入通道，可以在将组合信号发送到主输出之前作为一个整体进行控制和调整。有时被称为**副混音”（`Submix`）、“总线”（`Bus`）或直接称为“组”。

# 组延迟 (Group Delay)

在音频中，组延迟是所有电子音频设备（如扬声器、放大器）中的一种现象，信号中不同频率的输出之间略有延迟。简单来说，低频率的传输比高频率稍慢。在所有设备中，信号的输入和输出之间都有固有的延迟，但组延迟专门处理频率之间的延迟。任何配置的目标都是将组延迟保持尽可能小；在配置极差的情况下，高低音之间的延迟是可以听得的。

# 吉他控制器 (Guitar Controller)

一种可以传输 `MIDI` 数据以控制合成器的电吉他（或类似吉他的设备）。

# 吉他处理器 (Guitar Processor)

一种为直接信号添加音频效果的设备，如混响、合唱、法兰、延迟、过载、放大器模拟等。效果处理器以独立效果箱或多踏板（另见“踏板”、“踏板开关”）的形式出现在吉他和调音台之间的信号路径中。也可以作为吉他放大器中的预设或 `DAW` 中的数字插件使用。

# 哈斯效应 (Haas Effect)

（也称为偏效应）简单来说，人类听觉中的一种因素，我们根据时间而不是声级来感知声音源。在研究中，赫尔穆特·哈斯确定首先到达耳朵的波有助于确定声音的位置，而不是其反射。声音的反射必须比原始声至少大 `10dB`，或者延迟超过 `30 毫秒`（我们可以将其感知为回声），才会影响我们对方向的感知。这有助于我们区分原始源，而不被周围表面的反射和混响所干扰。哈斯效应在现场音频环境中特别有用，尤其是在大型场馆，扬声器经过时间延迟以匹配来自源的初始声波。

# 半音 (Half Step)

相当于钢琴上相邻键的音高变化。也称为“半音”。

# 半归一化 (Half-Normalized)

描述配线板内部布线的配置，其中插孔形成一个连接路径，直到插入跳线以改变路径。当配线板为“全归一化”时，插入输入或输出端的跳线都会改变连接；当为“半归一化”时，只有插入输入端时路径才会改变。“非归一化”或“开放”意味着没有内部连接，每个输入向相应的输出发送信号。

# 半波整流器 (Half-Wave Rectifier)

半波整流器只通过正电压，并将任何负电压替换为 `0v`。换句话说，任何“零以下的部分都会被削掉。

# 附录 B：音频工程术语 (0 - 9 - A - Z)

# 大厅模式 (Hall)

一种数字延迟/混响效果设置，模拟音乐厅。大厅模式的特点是高达 `25 ms` 的预延迟。

# 硬拐点 (Hard Knee)

在压缩中，指声音电平一旦超过阈值，压缩的引入更加突兀。（参见“拐点”）

# 硬同步 (Hard Sync)

这是最常见的振荡器类型，从振荡器每次收到同步脉冲都会重置其波形。如果没有指定同步类型，通常可能是硬同步。

# 谐波失真 (Harmonic Distortion)

设备输出信号中存在输入信号中不存在的谐波，通常用于改变乐器的音色。

# 泛波 (Harmonic)

单个泛波是最纯净的声音：它不包含任何泛音或其他音量之外的识别特征。它的振动形状——无论是振动空气让你听到，还是引起电压升降的产生电振动——都是正弦波。大多数情况下，泛音之间具有非常特定的音高关系。第一个或最低的泛波——称为“基波”——是声音的音高，就像和弦的最低音是它的“根”。泛波更高，且按基波的整数倍间隔：其频率的两倍、三倍、四倍等此类推。前几个泛波恰好具有良好的音乐间距：一个八度、一个八度五；两个八度。越高，看起来可能越不音乐化。

# 泛波 (Harmonics)

在发声过程中自然产生的基频的整数倍。在数学上，如果基频为 `x`，则泛波将为 `2x`、`3x`、`4x` 等。例如，如果音符的基频为 `440Hz`（或 `A-440`），泛波将为 `880Hz`、`1320Hz`、`1760Hz` 等。音中泛波的存在形成了乐器或人声的音色。

# 磁头 (Head)

在磁带录制中，一种影响经过它的磁带的电磁换能器。录音/播放头将音频信号从电能转换为磁能，反之亦然，用于录音和播放。消磁头产生强大的电磁场，用于消除磁带上之前的信号。

# 裕量 (Headroom)

放大器或音频设备中正常工作电平与削波电平之间的分贝（`dB`）差。也描述录制峰值电平与信号失真点之间的分贝差。（也称为“边缘”）

# 赫兹/伏特 (Hertz/Volt)

一种系统，输入端 `1 伏特` 的变化会导致固定数量的赫兹变化（每秒循环），而不是固定的音程。

# 赫兹 (Hertz)

(缩写为 `Hz`)

1) 频率的单位，特别是每秒内发生的完整波周期数（每秒循环）。`1 Hz` = 每秒一个完整波。

2) 一家流行的租车公司（通常不用于录音，除非运往录音室）。

# 高音镲 (Hi-Hat)

在鼓组中，支架上的双对镲，通常位于军鼓旁边，可以用脚踏踩，也可以用棒子击上方镲。

# 高阻抗 (Hi-Z)

(缩写为 `Hi-Z`) 描述为几千欧姆的阻抗或电阻。在麦克风中，`Hi-Z` 通常指定为 `10,000 欧姆` 或更多。（参见“阻抗”。）

# 高电平 (High gate)

当门信号处于电压水平（通常为 `5 伏`，尽管可以更高）表示其“开启”时——例如当键盘控制器上按住音符时——称为门高电平。

# 高阻抗 (High Impedance)

(缩写为 `Hi-Z`) 描述为几千欧姆的阻抗或电阻。在麦克风中，`Hi-Z` 通常指定为 `10,000 欧姆` 或更多。（参见“阻抗”。）

# 高通滤波器 (High Pass Filter)

一种音频滤波器，衰减低于某些频率（截止频率）的信号，并通过频率更高的信号。

# 高端 (High-End)

`Highs` 或 `Hi-End` – “高频”的缩写，泛指 `4000 Hz` 以上的频率。通常用于“高频”的语境下。

# 高通滤波器 (HPF)

一种音频滤波器，衰减低于某些频率（截止频率）的信号，并通过频率更高的信号。

# 喇叭 (Horn)

# 附录 B：音频工程术语 (0 - 9 - A - Z)

1) 用于放大和引导声音的喇叭状开口。

2) 不同类型乐器之一。

# 房屋同步 (House Sync)

用于保持设备同步的参考信号，如 `SMPTE` 码。

# HP

`HP` = 水平频率。在 `Eurack` 格式中，模块的宽度定义为高频单位的数量。

# 高通滤波器 (HPF)

一种音频滤波器，衰减低于某些频率（截止频率）的信号，并通过频率更高的信号。

# 交流声 (Hum)

1) 当电源电流意外感应或进入电子设备时产生的低频音。交流声反映了电流的基础频率（美国为 `60 Hz`，许多欧洲国家为 `50 Hz`）。

2) 在不开口的情况下发出音高。

# 混合电源 (Hybrid Power Supply)

混合电源使用较轻、更高效的开关电源执行大部分电压降——例如从 `120 AC` 到 `15 DC`——然后使用线性电源处理剩余较小的电压降——例如从 `15V` 到 `12V`。这在许多合成器中正成为主流设计。

# 超心形 (Hypercardioid)

心形麦克风的一种变体，其最佳拾音区域的形状更紧凑、更具方向性。超心形麦克风在麦克风正轴方向上最敏感，并在离轴 `90-150 度` 之间开始拒绝声音，取决于图形的紧密程度。

## 附录 B：音频工程术语 (0 - 9 - A - Z) 445

### ADSR

这是一个攻击/衰减/维持/释放（`ADSR`）包络发生器，它允许你从初始电平——即“I”开始攻击阶段，而不是常用的 `0 伏`。`Prophet VS` 中的包络器以及 `Ladik` 的模块都具有这一功能。

### IC

集成电路 – 一种半导体材料上由许多组件组成的微型电路，用于电子设备。是“芯片”或“微芯片”的正式说法。

### 成像 (Imaging)

指在声空间内定位特定的声音。在录音环境中，它是将乐器“放置”在立体声或环绕场中，以便当通过声器播放声音时，能够欺骗我们的耳朵，让我们认为声源来自某个特定的点而不是声器。在现场音频和声学增强系统中，成像原理相同，目标是让观众感知到声音来自舞台上的表演者，而不是声器。

### 阻抗 (Impedance)

指电路或设备对交流的的阻，在数学上可以描述为电压与电流的比值。录音室设备之间的阻抗差异会影响它们的协同工作。阻抗缩写为字母 `Z`，单位是欧姆（`Ω`）。

### 线路调音台 (In Line Console)

一种音频调音台，其设计和配置使得每个通道条在多轨道录音期间都可以同时用于录音和监控功能。这种配置与标准调音台不同，后者需要在面板上有单独的通道用于录音和监控功能。

### 同相 (In Phase)

两个或多个设备（及其相应的音频信号）处于极性光谱的同一侧，产生的波形互不冲突或不互相抵消的理想状态。

### 端口 (In Port)

`MIDI` 设备或计算机上接受输入数据信号的插孔。

### 电感 (Inductance)

电导体的一种特性，由于对电流变化的自然阻力，以磁性方式产生或储存电荷（电压）。电感是一种电磁原理，可以辅助音频应用（如扬声器），或导致阻力（例如使用的扬声器线线规格过低）。

### 电感器 (Inductor)

一种设备（通常是线圈），当电流通过它时，将电能转换为储存的磁能。常见于各种音频应用中，如吉他拾音器和扬声器。

## 无限反射板 (Infinite Baffle)

一种扬声器支架或外壳，其设计使得从前面的声波理论上无法到达背面，防止声波互相抵消。“无限”一词源于这样一个想法：没有尽点的墙上的扬声器不会让声波迁移到它后面。当然，这在物理上是不可能的，因此无限反射板旨在尽可能模拟这种效果。无限反射板的示例是将扬声器安装在封闭房间的墙上，或在足够大的密封柜内部建造以防止声音影响背面。

## 初始/攻击/衰减/维持/释放 (Initial/Attack/Decay/Sustain/Release)

这是一个攻击/衰减/维持/释放（`ADSR`）发生器，它允许你从初始电平——即“I”开始攻击阶段，而不是常用的 `0 伏`。`Prophet VS` 中的包络器以及 `Ladik` 的模块都具有这一功能。

## 输入/输出 (I/O)

`I/O` 是“`Input/Output`”的缩写。在音频领域，指的是任何涉及电/音频信号或数据传输的设备、程序或系统。

## 输入阻抗 (Input Impedance)

设备前端电路对电流流的阻碍。

## 输入监控 (Input Monitoring)

许多 `DAW` 上的一个设置，允许你监控进入 `DAW` 的实时输入信号（与录制信号相反）。

## 输入 (Input)

设备接收信号的插孔或物理位置。也指输入信号本身。

## 插入 (Insert)

信号链中的接入点（通常在调音台中或虚拟地位于 `DAW` 内部），设备、信号处理器或数字插件可以“插入”到前放大与通道或总输出之间的电路中。通常用于为通道或组通道添加混响、压缩或均衡等处理。

## 乐器放大器 (Instrument Amplifier)

一种带有功率放大器和扬声器的设备，用于还原电乐器输出的信号。



## 直接乐器输出 (Instrument Out Direct)

将电乐器（如电吉他）的输出直接连接到录音台或磁带机，而不是使用放大器麦克风。

## 绝缘体 (Insulator)

一种如玻璃、空气、塑料等（在所有实际用途中）不导电的物质。

## 集成电路 (Integrated Circuit)

集成电路（缩写为“IC”）– 一种半导体材料上由许多组件组成的微型电路，用于电子设备。是“芯片”或“微芯片”的正式说法。

### 积分器 (Integrator)

该功能可以平滑输入信号，使电压平发生变化。“积分器”是该数学函数的名称；你更有可能看到此模块被称为斜率限制器（我们将对此进行详细介绍），或较少地称为延迟发生器或处理器。

### 接口 (Interface)

任何允许一个单元工作、驱动或与另一个单元连接的设备或连接点，或者允许人类与计算机或其他电子设备交互的设备。专业音频领域有很多接口示例，包括 `MIDI`（乐器数字接口）；将音频输入连接到计算机的音频接口；甚至是你的 `DAW`，它显示了一个允许你进行分配的屏幕。

## 互调失真 (IM)

由两个或多个频率相互作用引起的失真。

## 反平方定律 (Inverse Square Law)

一种描述声音强度随距离源距离增加而减弱的数学规则。在声学中，距离每增加一倍，声压减半。

## 反相器 (Inverter)

一种翻转信号相位的电路。这通常用于逻辑电路以翻转高低状态，但在音频中，它可以将波形翻转 180 度。

## 反相调音器 (Inverting Mixer)

大多数调音台都可以翻转信号相位。这通常用于在使用多个麦克风时修正相位问题。

## 隔离 (Isolation)

将声音限制在特定区域内使其与其他声音相互作用的过程。例如，使用声学处理间的来录制人声或乐器。

## IV 线 (IV Cable)

你通常需要将一个信号发送到多个目的地。方案包括使用分线器或连接在一起的专用线。

## 插孔 (Jack)

你将跳线线插入合成器面板的孔。插孔的尺寸和类型（`3.5mm`、`香蕉头`、`1/4英寸`）通常是不同格式定义的特征之一。

## 同步 (Jam Sync)

某些时钟或同步设备上的过程，读取外部时间码并产生（或同步）与原始外部码相同的时间码，用于设备同步。

## Karplus Strong

这种物理建模合成算法，旨在模拟拨击振动弦的声音。一个短的样本（最初是噪声）被发送到输出和延迟线。延迟线的输出连接到滤波器，然后回到主输出和延迟线的输入。

## 调性 (Key)

1. 在音乐中，指编写或演奏音乐作品的音阶，由音阶的第一个音（主音）确定。
2. 通过侧链使用外部音频信号对动态处理设备进行控制。
3. 用于解锁设备或软件使用的数字或数据代码。

# 附录 B：音频工程术语 (0 - 9 - A - Z)

## 键盘控制器 (Keyboard Controller)

一种钢琴式键盘，通过发送 `MIDI` 信号来控制其他 `MIDI` 设备。大多数键盘乐器都带有 `MIDI` 控制功能，但专用的 `MIDI` 键盘控制器产生音频信号，只输出 `MIDI` 数据。

## 键盘跟踪 (Keyboard Tracking)

大多数模块合成器遵循电压与音高之间的严格关系，例如每八度 `1 伏`；任何偏差都会导致调音。由于这种敏感性，`1/oct` 和类似的信号与连接有时被专门区分为键盘跟踪，而非仅仅是“CV（控制电压）”，以确保在控制模块上的功能时它们不会被衰减或修改。

## 键盘 (Keyboard)

任何通过按键控制的乐器或计算机。

## 肩吉他 (Keytar)

一种轻便、便携的键盘，旨在让键盘手获得与吉他手同样的自由（更不用说摆造型的机会）。

## 大底鼓 (Kick Drum)

架子鼓组中的底鼓，之所以这样命名是因为它是通过踏板的。

## 千赫兹 (kHz)

`kHz` 是千赫兹的缩写（`1000 Hz`，或每秒 `1000` 次循环）。例如：`2000 Hz = 2 kHz`。在工作室中最用于描述音频频率范围或数字采样率。

## 膝部 (Knee)

压缩器上的一个功能，决定当音量超过阈值时，压缩开始得剧烈或缓慢。响应曲线中所谓的“弯曲”让人联想到膝盖。“硬拐”（`Hard knee`）指的是压缩器的突然激活，而“软拐”（`soft knee`）指的是更平缓的变化。

## Krell 补丁电路 (Krell Patch)

重建这个补丁是许多模块化音乐人想要尝试的挑战。它基于 1959 年的电影《星球大战》，其中一段据他们在演奏古代克雷尔（`Krell`）种族的音乐。通常情况下，每个音都有随机的音高、包络和时长。

## 延迟生成器 (Lag Generator)

此功能平滑输入信号，使得电压水平的变化每秒不超过特定的伏数。这导致结果“滞后”于输入的变化。有时被称为斜率限制器（`slew limiter`）或在技术上称为积分器。

## 叠层 (Layering)

指的是几乎任何多个音乐部分或声音的同步混合，通常组合在一个通道上或分配给一个控制器。在音频录制中，叠层通常涉及同一乐器或人声的相似录音（或带有轻微延迟或合唱效果的部分复制），以创建比人声/乐器本身更完整、丰富的声音。在声音设计中，它也指混合多个样本（例如：两个或多个鼓声）以创建更丰富的声音。

## 领谱 (Lead Sheet)

一种音乐记法的简写形式（类似于和弦图），显示某些歌曲的基本元素，以便音乐家可以遵循，而无需每个音符或表情的完整记法。领谱通常包含记谱上的旋律线，五谱上方有和弦变化，下方是歌词。（参见“和弦图”）

## 漏音 (Leakage)

来自其他乐器和声源且非麦克风采集的声音。

## 电平 (Level)

信号强度的大小；振幅，特别是平均振幅。

## 低频振荡器 (LFO)

该模块产生重复的、循环的波形，频率范围从音频频谱的低端一直慢到每个周期几秒或几分钟。它们被用于产生各种效果，如颤音（控制信号的响度）、揉音（控制信号的音高）、重复的滤波器哇哇（`wah-wah`）效果、对振荡器中脉冲波形的脉冲宽度调制等。

## 限幅器 (Limiter)

一种压缩器，当音频电平达到特定阈值时剧烈地减少（限制）信号的增益，通常用于防止过载和信号峰值。当压缩器的压缩比为 `10:1` 或更高时，压缩器实际上变成了限幅器。（参见“压缩器”）

## 线路输入 (Line Input)

线路输入（`Line In`）——一种旨在接收线路电平信号的输入。

## 线路电平 (Line Level)

大多数消费级和低成本专业音频设备使用被称为 `+/-10dB`（分贝伏）的信号电平。最常见的连接器是 `RCA`（插口）或 `3.5mm`，尽管也使用 `1/4 英寸`；信号是“不平衡的”（它使用两根线：信号线和地线）。在线路电平标准中，变化 `+/-0.447 伏`的正弦波被认为是 `+/-10dB`。相比之下，模块化合成器中的双极振荡器是 `+/-5` 到 `+/-8 伏`。因此，你需要在模块化合成器中使用输出模块，或者在调音台或录音机上一个输入衰减器，以便将合成器连接到设备。同样，你需要大幅放大线路信号以达到模块化标准，以便在你的模块化合成器中处理。

## 线路输出 (Line Output)

线路输出（`Line Out`）——任何发送线路电平信号的输出，例如连接录音机的控制台输出。

## 线性 FM (Linear FM)

这是频率调制（`FM`）振荡器的优选输入响应，因为当你改变调制器时，结果会保持音准。

## 线性电源 (Linear Power Supply)

线性电源设计使用变压器等组件将较高的输入电压降低到较低电压。广泛来说，它们倾向于向输出功率信号中引入更少的噪声，代价是增加热量和重量（效率不高）。许多人正转向混合电源，将开关电源与小型线性电源或调节器结合，以获得两者的优点。

## 电压控制放大器 (VCA)

线性电压控制放大器（`VCA`）使用控制输入与信号电平之间的简单数学关系——例如，`50%` 的标称控制会导致输出变为输入的 `50%`。然而，这不是我们耳朵感知响度的方式；声音必须放大 `10` 倍才能被感知为响一倍。这使得 `VCA` 在扩展控制方面非常理想，但对于扩展音频信号可能没那么理想。如果你将具有指数输出的包络生成器连接到线性 `VCA`，你将得到想要的结果。困惑吗？这就是为什么当包络生成器或 `VCA` 有一个在线性和指数响应之间切换的开关是非常棒。线性调音器类似于线性 `VCA`，线路上的“一半”等于输入电压的一半。再次，这对于改变控制是可以的，但对于混合音频信号不是；以你使用指数控制的调音器。

## 线性 VCO

线性电压控制振荡器（`VCO`）遵循伏/赫兹（`v/Hz`）标准；更常见的是伏/八度（`v/oct`）标准。例外是频率调制（`FM`），其中通常优选线性控制电压输入，以创造经典的 `FM`，因为它不会改变载波振荡器的基本音高。

## 现场录制 (Live Recording)

所有音乐家同时演奏且不叠加录制的录音课程。

## 现场室 (Live Room)

录音室的大型房间，大多数乐器和/或歌手在此表演。之所以这样命名，不仅是因为有供现场表演的空间，而且是因为房间经过声学处理，产生了悦耳的现场混响。

## 现场 (Live)

1. 描述具有回响或反射空间的术语。在“现场”空间内，声波是活跃的。
2. 实时发生的，与预录录的相反。

## 本地开启关闭 (Local On/Off)

本地开启关闭 – 一种控制合成器或 `MIDI` 控制器内部模块的 `MIDI` 消息。“本地开启”在按下键盘时触发内部模块；“本地关闭”将其断开。“本地关闭”经常用于防止在配置中 `MIDI` 消息的意外循环，或者当通过另一个控制器控制内部模块时使用。

# 逻辑函数

在模块化合成器中，控制电压通常是连续的，而门信号（`gate`）和触发信号（`trigger`）是二进制的：开启或关闭；高或低。这与数字电路相同。因此，可以制作数字逻辑模块。常见的逻辑函数是 `OR`（或）：如果信号 `A` 或信号 `B` 之一为高（开启），则输出高电门（开启）；否则输出低电门（关闭）。另一种是 `AND`（与）：当且仅当信号 `A` 和信号 `B` 同时为高时，输出高电门（开启）；否则输出低电门（关闭）。这些是组合来自不同源节拍触发的绝佳函数。

# 逻辑

二进制或布尔逻辑是一种组合门信号（开启或关闭电压）以创建新输出的方法。逻辑模块的每个部分通常包含 `1` 到 `3` 个输入，其中 `2` 个最常见。`OR` 函数表示，如果任何输入端有门开启（“高电”）信号（即输入 `1` 或输入 `2` 或输入 `3` 等），则输出门信号。`AND` 函数表示，只有当所有输入都检测到“高电”时，才输出门开启信号。函数名称前的前缀表示“非此函数”——换句话说，`NOR`（非或）函数只有在所有输入均为低电时（输入 `1` 和输入 `2` 都不高）才会输出高信号。

# 循环 (Loop)

1. 实际上，任何无限重复的音乐或数据。在数字音频和采样之前，循环是通过磁带循环创建的。今天，循环被用于采样中以保持采样音符在触发期间持续，而鼓点循环和其他音乐循环在现代制作中非常常见。
2. 波节（`antinode`）的另一种术语，指振动弦或波位移最大的点。（参见“驻波”。）

# 循环操作

有时拥有一个循环模块或其重复功能是有用的。例如，一个可以设置为循环低频振荡器的包络生成器：当它攻击到最大值并衰减回零时，它会再次开始该攻击阶段。通常你希望音符序列器循环：当它到达序列中的最后一个音符时，如果它可以回溯或返回第一个音符并重新开始将非常有用。具有循环功能的音频录音机在现场表演中也很流行。

# 亮度 (Loudness)

一个指的是人耳感知传入声波的术语。这个词自俗其明，但我们通常认为响度与声音的音量有关，尽管这是一种间接关系。在声学术语中，音量更多关于声波的幅度，而响度描述的是我们的耳朵如何听到这些波的强度。

# 低（门）

通常，这是门信号或触发信号处于“关闭”状态的缩写（通常为 `0 – 5 伏`，与之相对的是 `+5 伏`的“高”或“开启”信号）。

# 低频振荡器

该模块产生重复的、循环波形，频率范围从音频频谱的低端到每周期几秒甚至几分钟不等。

# 附录 B：音频工程术语 (0 - 9 - A - Z)

例如颤音（`tremolo`，用于控制信号响度时）、揉音（`vibrato`，用于控制信号音高时）、重复性滤波器哇哇哇效果、用于改变振荡器中脉冲波形的脉冲宽度调制等。

# 低阻抗

（缩写为 `Lo-Z`）描述为 `500 欧`或以下的阻抗。（参见“阻抗”。）

# 低通滤波器

低通滤波器（`LPF`）设计通过通过低于截止频率或角频率的谐波，并根据它们高于截止频率的远程度来降低较低谐波的电平。在 `12dB/oct`（分贝/倍频）低通滤波器在高于截止频率一个倍频（换说，截止频率的两倍）的谐波电平降低 `12 dB`；高于截止频率两个倍频（频率的四倍）的谐波降低 `24dB`，依此类推。这是常用的滤波器类型，因为大多数自然声音具有较强的谐波和较弱的高谐波——尤其是当音符衰减至消失时。

# 低通门

根据严格定义，低通门（`LPG`）是一种低通滤波器，当控制电压趋于 `0 伏`时，其截止频率进入次声范围，导致输入信号被过滤为静。有些通过将低通滤波器和电压控制放大器在同一个模块中来实现这一点，两者都遵循相同的控制电压。在任何情况下，当输入包络从高电平流向 `0 伏`时，输出会变得暗淡（高谐波被过滤更多），但没有完全消失。这模仿了自然声音的工作方式。

# 低频振荡器 (LFO)

一种发射低于人类听力范围范围（`20 Hz` 或以下）的低频电子波形的电路。这种低频波形产生节奏脉冲，以调制音频信号中的各种参数，例如音高或音量。`LFO` 经常用于采样器、合成器和信号处理器，以创建如揉音、颤音和相位等效果。

# 低通滤波器

一种音频滤波器或设备，衰减某些频率（截止频率）以上的信号，并通过低于截止频率的频率信号。

# 低音或低频端

“low frequencies”的缩写，指 `250 Hz` 以下的低频信号。通常用于音频信号中“高、中、低”的语境下。

# LPF

低通滤波器（`LPF`）设计通过通过低于截止频率或角频率的谐波，并根据它们高于截止频率的远程度来降低较低谐波的电平。在 `12dB/oct`（分贝/倍频）低通滤波器在高于截止频率一个倍频（换说，截止频率的两倍）的谐波电平降低 `12 dB`；高于截止频率两个倍频（频率的四倍）的谐波降低 `24dB`，依此类推。这是常用的滤波器类型，因为大多数自然声音具有较强的谐波和较弱的高谐波——尤其是当音符衰减至消失时。

# 附录 B：音频工程术语 (0 - 9 - A - Z)

# LPG

根据严格定义，低通门（`LPG`）是一种低通滤波器，当控制电压趋于 `0 伏`时，其截止频率进入次声范围，导致输入信号被过滤为静。有些通过将低通滤波器和电压控制放大器在同一个模块中来实现这一点，两者都遵循相同的控制电压。在任何情况下，当输入包络从高电平流向 `0 伏`时，输出会变得暗淡（高谐波被过滤更多），但没有完全消失。这模仿了自然声音的工作方式。

# M2.5

`Eurorack` 模块的常用螺纹。当使用沿轨上滑动的方螺母系统时，这种尺寸最常见。

# M3

`Eurorack` 模块的常用螺纹。当使用预钻孔的模块安装轨时，这种尺寸最常见。

# 磁带

一种由涂有磁性材料细粒氧化铁颗粒的塑料带组成的录带。通常用于模拟录音。

# 磁性

铁基材料对铁基材料的自然吸引力。

# MARF

`Buchla 248 MARF`（多功能函数生成器）是序列器和包络生成器（均在词表其他地方描述）的交叉体，因为它通常包含 `16` 或 `32` 个阶段（有时称为“段”），以及一个在这些阶段之间插值的速率控制。这意味着创建复杂的包络形状和其他控制电压序列。之后，`Buchla` 使用 `MARF` 术语描述 `400` 等仪器的多步包络。

# 余裕

参见“Headroom”。

# 掩蔽

听觉的一种特性，大声会耳朵听不到相似频率的弱声。也指大声对弱声的遮蔽。

# Master

1. 控制台或 `DAW` 的主输出控制，设置混合信号离开控制台时的电平。（也称为“主推子”。）
2. 用于制作复制的最终混合原始记录。

# 母带处理

对歌曲或歌曲集的混合进行精细调优和“润色”的最终过程，并将在此创建母带。

## 附录 B：音频工程术语 (0 - 9 - A - Z)

### Measure（小节）

音乐中节拍数的分组。（参见“Bar”。）

### Meg（兆/百万）

基于前缀 "Mega-" 的俚语缩写，表示 `1,000,000`。通常用作兆赫（`1,000,000 Hz`，`MHz`）或兆字节（`1,000,000 字节`，`MB`）的简写。

### Meter（电表）

1. 一种用于测量和显示音频或数字设备信号电的设备。电表通常测量峰值或 `RMS`（均方根）值。（参见“Peak Value”、“RMS Value”。）
2. 音乐的节奏结构，通常描述小节中的节拍数。

### Mic / Line Switch（麦克风/线路开关）

`Mic`、`Mike` – “microphone”（`microphone`）的缩写。

### Microphone (Mic) Input（麦路输入）

调音台或其他设备专为麦克风信号设计的输入。

### Microphone (Mic) Level（麦路电平）

录室麦克风发出的极低电压电平。信号在进入调音台之前必须通过前放大器增加到线路电平。（参见“Line Level”、“Amplifier”。）

### Microphone (Mic) Pad（麦路衰减）

麦克风前放大器上的设置，或独立的适配器/连接器，在麦克风信号进入前放大器之前降低其电平以防止过载。

### Microphone（麦克风）

一种将声压转换为电信号的换能器。

### Mid-Side Mixing (M/S)（中侧混音）

（缩写 `M/S`）一种立体声同步麦克风放置技术，其中一个心形指向麦克风直接对光源，另一个双指向麦克风侧放并尽可能地靠近第一个麦克风。

### MIDI Clock（MIDI 时钟）

由 `MIDI` 传输的时钟，用于节序器和音乐设备之间保持同步。不要与 `MIDI` 时间码（`MTC`）混淆，`MIDI` 时钟与每分钟拍数（`BPM`）速度绑定，每个四分音前进 `24` 步。

### MIDI Controller（MIDI 控制器）

根据上下文，可以指 `MIDI` 的两个不同元素。

1. 一种向连接设备发送 `MIDI` 数据的设备或软件，通过预编程序列或音乐师的现场表演来发送。
2. `MIDI` 设备上若干较小控制器中的任何一个，被分配控制声音或性能的特定参数。

### MIDI Interface（MIDI 接口）

一种将 `MIDI` 信号转换为计算机数字格式的设备，以便能够存储和使用 `MIDI` 信号。

## MIDI over Bluetooth（蓝牙 MIDI）



# 蓝牙低功耗（BLE）

蓝牙低功耗（BLE）是大多数移动计算设备支持的无线连接规范。BLE（也称为蓝牙 SMART）可以为使用不持续传输数据的连接配件（如 MIDI 键盘和控制器）的移动设备延长电池寿命。

MMA 工作评估了 LE MIDI 性能（延迟和抖动），并发现了一项蓝牙 MIDI 规范，使不同制造商的产品能够运行。蓝牙低功耗 MIDI 规范（BLE-MIDI）基于 Apple 在 iOS 和 OS 10.10 中实现的方案，以便早期采用者的产品保持与行业标准的兼容。

## MIDI Sample Standard (SDS)（MIDI 采样标准）

添加到 MIDI 中的一种子协议，允许在仪器、存储单元或节点之间传输数字录制的样本，无需转换为模拟信号。

## MIDI Sequencer（MIDI 节序器）

一种可以记录和回放 MIDI 数据的设备或软件，通过一系列定时步骤控制乐器或设备的性能。MIDI 节序器可以存在于 MIDI 控制器、键盘或工作站板上、作为独立设备或计算机软件存在。

## MIDI Thru Box（MIDI 跳线盒）

具有一个 MIDI In 和多个 MIDI Thru 端口的单元，用于将 MIDI 信号中继到多个设备。MIDI 用户通常于将此作为“串联”设备的替代方案，因为后者会导致 MIDI 信号出现轻微延迟。

## MIDI Thru（MIDI 跳线）

输出与输入 MIDI 信号相同的端口，有效地在不更改或修改信号的情况下将信号中继到另一个设备。（许多 MIDI 设备有三个 MIDI 端口：In、Out 和 Thru。）

## MIDI Time Code (MTC)（MIDI 时间码）

将 SMPTE 时间码中的信息转换为 MIDI 数据，使 MIDI 节序器和连接设备能够与 SMPTE 代码同步（通常与视频相关）（另参见“SMPTE Time Code”）

## MIDI

Musical Instrument Digital Interface（乐器数字接口）的缩写。MIDI 是连接合成器与其他合成器以及合成器与计算机的常用语言。尽管它是一种数字语言，但很容易买到 MIDI 转 CV/Gate（控制电压和门信号）转换模块，它可以同时处理驱动节序器和合成器的音符事件和 MIDI 时钟。最值得注意的是需要何种类型的连接器：传统的 5 脚 DIN 还是 USB 式连接。

## Mid-range frequencies（中频）

“中频”的缩写，指约 250 Hz 到 6000 Hz 的音频频率。在音频信号的“高、中、低”语境中使用。

## Mini Keys（小键）

一些键盘控制器甚至键盘合成器使用的键位尺寸比典型的钢琴键小得多。Mini keys 是这种硬件选择的常用术语（有时带有贬义，尽管空间和成本的节省非常显著）。

## Mix（混音/过程）

Mixdown 或 Mix Down – 在母带阶段之前，通过将多个音频轨道合并为单个轨道（或双声道立体声轨道）来创建最终混音的过程。这可以包括将模拟磁带的多通道混合成双轨母带的传统方法，也可以使用 DAW 创建数字混音的更现代方法（通常被称为“渲染”）。

## Mix（混音）

1) 将音频信号混合在一起。

2) 也可以指将部分处理过的信号混合回直接信号中。

## Mixer（混音台）

该模块组合信号。你可以使用混音台来组合音频信号，以防你需要指数电平控制以及可能的声相，或者反转电压，以防你需要额外的功能。

## Modular（模块化）

模块合成器将合成器的主要组件——产生声音的振荡器、修改声音的滤波器、塑造幅的 VCA 以及创建包络、颤音等的调制源——分解为可以购买和安装的单个模块。在最基础的层，这允许你在构建自己的合成器时进行混合组合。

## Modulation Noise（调制噪声）

当音频信号存在时存在的噪声。

## Modulation（调制）

当你使用电压控制改变合成器模块的参数时，被称为你正在调制该参数。例如，当低频振荡器（LFO）改变滤波器的截止频率以产生哇哇效果时，被称为 LFO 正在调制截止频率。当包络导致电压控制放大器（VCA）打开让声音突然变大，然后淡减回静音时，你也可以说包络正在调制放大器（尽管有些人将“调制”限制为重复动作）。因此，我们将这些变化的称为调制。

## Modulator（调制器）

我们在上面的定义中接触了调制和调制器的通用主题。然而，通常当有人使用调制器一术语时，他们是在讨论一种合成技术，其中一个音频信号“调制”（改变）另一个音频信号。例如，在频率调制（FM）中，调制器（调制振荡器）改变主信号发生器（振荡器）的频率（音高）。在环形、平衡或幅度调制中，调制器改变载波信号的亮度。

## 附录 B：音频工程术语 (0 - 9 - A - Z)

## 模块 (Module)

一组自包含电路和控制单元。在录音室中，模块通常包含在可更换的外壳中，以便安装在机架上，并包括放大器、均衡器、效果处理器和声音模块（由外部控制器激活的 MIDI 乐器）。在数字空间中，插件、软件小部件、采样器和插件也被描述为模块。

## 单声道 (Monaural / Mono)

（缩写为 "Mono"）描述通过单个通道传输的音频信号，与之对应的是双道的立体。（参见“单音 Monophonic”）

## 监听混音 (Monitor Mix)

发送给音乐人的现场和录音音频信号混合，让他们在表演时（无论舞台现场还是录音室）能够听到音乐。监听混音与主混音位于信号路径（通常由独立的较小调音台控制），并且不会影响 FOH 混音（现场音频）或进入多轨道录音机/DAW 的信号。在现场表演环境中，监听混音通常由运行独立调音台的独立音频工程师控制。

## 监听混音器部分 (Monitor Mixer Section)

监听区域/监听区 – 调音台上用于创建粗混的部分，以便工程师可以听到已录制的内容，而不影响馈到多轨道录音机或 DAW 的信号。

## 监听路径 (Monitor Path)

从通道路径引出的信号路径，允许工程师听听正在录制的内容，而不影响馈到多轨道录音机或 DAW 的信号。（参见“通道路径 Channel Path”）

## 监听 (Monitor)

- 1) 为了检查质量或避免峰值而听听音乐。

- 2) 录音室中的扬声器（通常是对中的一个），用于监听音频信号。这包括控制室里用于听混音的监听音箱，以及隔间或现场的耳机，供表演者在表演时听到音轨混音。

## 单音 (Monophonic)

- （缩写为 "Mono"）1) 单一声源或单通道传输（与立体声相反）。

- 2) 一次只播放一个音符的旋律线。

- 3) 描述乐器或合成器设置一次只播放一个音高（或“音色”）（参见“音色 Voice”）。

## 变形 (Morphing)

在模块化合成器的语境下，变形指的是振荡器在弹奏时可以更平滑地改变其输出波形的形状——从而改变产生的声音。这通常是数字振荡器的领域，它们在内部从一种波形交叉淡入（在某些情况下是切换）到另一种波形，尽管有时也应用于可以让你真实控制波形的模拟振荡器。

## Mother-32

Moog 出品的一种非常流行的半模块化合成器。它有自己的外壳，但也可以安装在 Eurorack 格式的机箱中。它配备一个 VCO（锯齿波和脉冲波形）、一个 LFO（三角波和正方波）、一个 Moog 风格的阶梯滤波器（可低通或高通）以及一个 AD 或 AR 包络发生器。它还有一个非常强大的步进序列器和一个微型八度键盘。它之所以是半模块化的，是因为有一个漂亮的跳线面板，允许为内部布线的合成器声音提供替代路由，并将其连接到外部模块。由于这些模块中许多被使用，在讨论如何扩展基础模块化系统时，它是典型的半模块化或“入门级”合成器声音的代表。今年春天将推出针对 Mother-32 的在线入门课程，并将推出关于为此入门系统添加不同模块的课程及每周系列。

## 动圈麦克风 (Moving Coil Microphone)

这种麦克风通过磁场中移动的感应线将声压波转换为电音频信号——这一过程通常被比作扬声器的反向工作。动态麦克风灵敏度低于电容麦克风，但对于产生较大的声源或近距离拾音应用非常有效。

## 移动推子自动控制 (Moving Fader Automaton)

某些调音台上的一个功能，推子可以预设在播放多轨道录制内容期间自动发生。

## MU

指高度为 5U（机架单元）或 8.75 英寸（22.2 厘米）的模块，这通常与经典的 Moog 标准以及追随其脚步的人有关，包括 Synthesizers.com (Dotcom) 和 Moon Modular。你会看到它与 MU（Moog Units）通用用，MU 也指每个单元标准宽度为 2.125 英寸（5.4 厘米）。鉴于该标准既具有历史意义物理尺寸巨大，某些用户将“5U”作为他们传统且酷的荣誉标志。（而且它们确实如此）。曾使用不同的宽度和电源连接。该标准现已停产，但今天仍在使用旧的 MOTM 格式。

## 多点延迟 (Multi-Tap Delay)

延迟的工作原理是将音频放入管道的一端，并在它从另一端传出时将其抓取。而多点延迟的意思是：“等音频快照完全穿过管子吗？让我们在它只通过一半管子时就抓取它。”这些被提前抓取的点就是“采样点（taps）”——就像长管子上的额外水龙头。

## 万用表 (Multimeter)

一种测试电压、电流和电阻的小装置。万用表在录音室中用于校准电气系统和排除故障。

## 多功能任意函数发生器 (Multiple Arbitrary Function Generator)

稀有的 Burch Model 248 MarF（多功能任意函数发生器）是序列器和包络发生器（在本词表其他处描述）的交叉体，它通常包含 16 或 32 个阶段在这些阶段之间进行插值。这意味着可以创建非常包络形状。

## 多路 (Multiple)

你经常需要分割或复制信号以发送到多个目的地。这通常通过多路（简写为 mult）实现，即你放入一个源，然后插入额外的跳线连接到多个目的地。

## 复用器 (Multiplexer)

复用是一种用于描述信号路由的技术方法，其中多个信号路由到一个目的地。在合成器模块中，这通常扩展为允许一个输入在多个输出之间切换。顺序开关是复用器的一种类型，因为它在进行选择。

## 多音色 (Multitimbral)

指合成器或模块一次播放几种不同声音（或“音色”）的能力。

## 多轨道录制 (Multitrack Recording)

也称为跟踪（tracking）或多轨道录制，是将一组声源录制到独立轨道的过程，每个轨道都有自己的音频通道，然后同时播放这些轨道。录制可以一次一个轨道或乐器（稍后合并），也可以在表演者一起演奏时将其录制到独立轨道上。这些信号最初录制在多轨道磁带上，但今天它们可以作为单独音频文件录入数字音频工作站（DAW）。

## 多轨道带 (Multitrack Tape)

一卷磁带可以用于存储两个或多个相互同步的离散信号。

## 乐器数字接口 (MIDI)

乐器数字接口的缩写。MIDI 是连接合成器与其他设备以及合成器与计算机的常用语言。尽管它是一种数字语言，但很容易买到 MIDI 转 CV/Gate（控制电压和门信号）转换器，它可以处理音符事件和驱动序列器及合成器的 MIDI 时钟。需要注意的是什么种类型的连接：5 针 DIN 还是 USB 风格连接。

## 静音开关 (Mute Switch)

调音台或其他音频设备上的关闭输入或输出开关，或者是 DAW 虚拟音频控制空间上的匹配按钮。调音台上的独立通道都有静音开关，可以中断该通道的信号。

## 静音 (Mute)

有时你需要静音或断开信号。允许你执行此操作的电路被称为

## 附录 B：音频工程术语 (0 - 9 - A - Z)

## 每米纳米韦 (NW/m)

测量模拟磁带磁力强度的标准单位。韦（Weber）是磁强度的单位，但由于该单位数值太大，不适用于磁带录音机中的磁性，因此使用了纳米韦。磁带的每米纳米韦实际上描述了正在录制到磁带上的信号强度。

## 窄带噪声

发生在有限频率范围内的噪声（随机能量）。

## 近场

距离声源 1-5 英尺以内的区域。录音室监听音箱通常被认为是“近场”扬声器，因为它们的设计是为了近距离聆听。（参见“远场”）

## 近共振混音

一种立体声混音技术，将两个麦克风以向外的角度相互放置，以创建声场（相对于“共振混音”，后者是将麦克风指向彼此）。近共振混音的版本包括 DIN 立声（90度角，间距 20厘米）、NOS 立声（90度角，间距 30厘米）和 ORTF（110度角，间距 17厘米）。

## 负反馈

将输出信号的一部分反馈回放大器的输入端，其相位与原始输出信号相反。这会对输出产生阻尼效果，有效地抵消掉部分音量。

## 噪声底

音频信号下方存在的噪声水平，以分贝（dB）测量。每个电子设备在没有音频通过时也会发出最小水平的噪声；这被称为其噪声底。通常，设备的噪声底越低，设备质量越高。噪声底也会反映在录制信号中；录制的噪声底是所有连接设备产生的噪声之和。目标始终尽可能保持噪声底最低。

## 噪声门

用于在信号不存在时自动关闭音频通道以减少可听噪声的门。

## 噪声消除

从信号、设备或系统中去除噪声的多种过程。

## 噪声

描述音频信号中存在的任何不愉快、令人反感或非预期的频率。所有电子设备都会产生某种类型的噪声，可以描述为在安静或其他无声段落中听到的嘶嘶声或嗡嗡声。（参见“噪声底”）。连接不良、接地不当、无线电干扰和其他问题也可能为信号引入噪声。工程师可能会为了测试目的特意让噪声信号通过声音系统。参见“白噪声”、“红噪声”。

## 非破坏性编辑

录音系统中的一项功能（最常见于数字音频工作站，即 DAW），在执行编辑时，原始信号或内容保持完好，允许工程师随时恢复到原始版本。（有时被称为“非线性编辑”。）

## 无指向性

在麦克风中，从所有方向均匀拾音。

## 归一化

对音频应用固定数量的增益，使最高峰值达到最高可接受的录制水平。

## 直连/正常连接 (Normalled)

模块化合成器的优势在于，你可以让信号按照你喜欢的方式在系统中流动。但当你尝试连接一个“典型”的信号流时，这可能是一个非常耗时的过程。因此，一些制造商创建了“半模块化”合成器，它们为你预接线了所有的典型连接，其重要特征是许多这些布线通过跨越跳线线连接到正确的插孔中。这些预接连接通常被称为“直连”。例如：一个内部噪声源通常连接到调音器的一个通道，该通道位于滤波器之前，但如果你向通常标记为外部输入的地方插入跳线线，这个“直连”连接就会中断，并被你的外部连接取代。

## 陷波滤波器

这是一种特殊的滤波器模式，其中角或截止频率附近的音频频率或谐波被移除，或从整个频谱中“切除”。它是带通滤波器的相反，带通滤波器只通过截止频率附近的谐波。陷波滤波器对声音的影响往往微妙；移动（调制）截止频率会导致声音产生微弱的相位变化。陷波滤波器通常用于系统中削弱或消除问题频率，例如地线嗡嗡声、房间共鸣或声音谐频谱中的其他烦人频率。想象一下在跳线中使用陷波来掏空声音，为谐频谱中的其他声音的存在留出空间，使其竞争较少，或者仅仅是为了创造一种更容易吸引耳朵的声音，因为预期的东西缺失了。

## 陷波

狭窄的音频频率带。

## NW/m

测量模拟磁带磁力强度的标准单位。韦（Weber）是磁强度的单位，但由于该单位数值太大，不适用于磁带录音机中的磁性，因此使用了纳米韦。磁带的每米纳米韦实际上描述了正在录制到磁带上的信号强度。

## 尼比特 (Nyble)

Nyble（或 Nibble）——计算机数据的一半字节，或 4 位。

## 奈奎斯特频率

## 奈奎斯特率

录制和播放给定音频信号的最低采样率，等于奈奎斯特频率的两倍。如果在模拟信号或声音中发现的频率是 18,000 Hz，理论上信号每秒必须以至少 36,000 Hz 进行采样——否则，信号被认为采样不足并将产生混叠。这本质上是奈奎斯特频率的相反原理。（注意：44,100 Hz/秒的采样率被认为是标准采样率，因为它很容易覆盖人类听力的高端范围，约为 20,000 Hz。）

## 八度分频器

创建一个比基频谐波低一或两个八度的新音的模块。

## 八度

八度是一个音程。例如，键盘上所有的 C 音之间相隔一个八度。当你想要获得高一个八度的音时，或者想要低一个八度的音时，频率增加或减小一半。在术语中，这通常意味着增加或减少一个八度；某些振荡器面板上有开关可以增加或减少这些电压。

## 低音

距离声源 1-5 英尺以内的区域。录音室监听音箱通常被认为是“近场”扬声器，因为它们的设计是为了近距离聆听。（参见“远场”）

## 离轴

偏离麦克风正前的虚线（轴线）。

## 在轴

位于麦克风振膜正前的位置。

## 开路

一个断开、中断或不完整的电路，阻止电流流动。

## 工作电平

（有时被称为“参考电平”）正常运行期间不应超过的水平。

## 运算放大器

（缩写为 Op Amp）用于大多数音频和电子设备的放大电路。

## 运算跨导放大器

OTA（运算跨导放大器）电路是将输入电压转换为输出电流的电路。这是一种流行的放大设计，因为它不容易进入饱和（削波），具有良好的带宽，并且以“温暖”的声音著称。你可能会在 V 中发现它。电流可以被认为是电阻的相反，所以 OTA 电路中一个电压电阻器件使得滤波器等电路添加电压控制成为可能。当人们调音时，他们使用的是基于 OTA 的滤波器，除非它具有 MS-20 滤波器电路，那样声音会更薄、更尖锐。实际上，使用 OTA 更多关于创建特定声音的设计。

## 操作器

在不同的合成技术中，通常音频信号对另一个音频信号进行处理。例如，在频率调制（FM）中，第二个信号（调制器）改变主信号（载波）的频率（音高）。这两个信号或振荡器通常被称为操作器，特别是在 FM 跳线中。在使用 Yamaha DX7 及其后代产品的专用 FM 合成器时，比使用模块系统更可能听到这个术语。

# 附录 B：音频工程术语 (0 - 9 - A - Z)

## OR function 或门逻辑

最常见的布尔或二进制逻辑函数之一，或逻辑表示如果任何输入端有开启（或“高电平”）信号（即输入 1 或输入 2 或输入 3 等），则输出开启信号。NOR（非或）函数具有反相输出：只有当所有输入均为低电平时（输入 1 和 2 均非高电平），输出才会开启。XOR（异或）仅在其中一个输入为高电平但两个输入不同为高电平时输出高电平信号。最后，XNOR 是 XOR 函数的反相。

## Oscillator 振荡器



核心上，振荡意味着在重复的模式中往复变化。模块系统中的主要声音发生器被称为振荡器，因为它的输出在重复的模式中上下变化（振荡）。这种模式被称为其波形（例如在高、低电压之间交替的方波）；这种模式重复的快称为频率或音高。振荡器的声学器等效物是吉他上往复振动的弦、鼓面上上下振动的鼓膜，或者木管乐器簧片的动。模块系统振荡器的振动是通过电流通过电线实现的，而不是物理物体在空气中振动。（最终这些电流会被路由到扬声器，由扬声器通过线路振动空气。）

## Oscilloscope 示波器

一种将电压波动显示为图形波形的测试设备。“示波器”可以在很宽范围内运行，显示缓慢变化的电压（如 `LFO` 低频振荡器）或快速变化的电压（如振荡器和噪声）。示波器曾是笨重的外部设备，但现在你可以获得输出电脑显示部分的 USB 示波器，或者作为模块的示波器。

## OTA 运算跨导放大器

`OTA`（运算跨导放大器）电路是将输入电压转换为输出电流的电路。这是一种流行的放大器设计，因为它不容易进入饱和（削波），具有良好的带宽，并以“温暖”的音色闻名。因此，你可能会在 `VCA`（控制放大器）中发现它。电流可以被视为电阻的倒数，所以 `OTA` 电路中的本质上是一个电压电阻器件，使得向滤波器等电路添加电压控制成为可能。通常当有人说他们有一个基于 `OTA` 的滤波器时，他们通常是指它具有“温暖”的音色……除非它是 `MS-20` 滤波器克隆，那种情况下它的声音会更薄、更尖锐。实际上，`OTA` 更多是关于创建特定声音的便利性。

### Out of Phase 反相

1. 在振幅、频率和波形上与其他信号相似，但在周期的部分偏移。
2. 具有相反的极性。

## Outboard Equipment 外置设备

与调音台配合但不是调音台一部分设备。

## Output Impedance 输出阻抗

放大器（或其他设备）输出电路对电流流的阻碍。

## Output Level 输出电平

设备输出端的信号水平。

## Output 输出

1. 设备发送信号的插孔或物理位置。
2. 设备输出的信号。

## Overdubbing 叠录

在现有记录（通常在其独立轨道上）之上录制额外表演的过程。随着多轨道录制的出现，叠录已成为常见的录音技术，最初是在多轨道模拟磁带上，最近通过计算机和数字音频工作站 (`DAW`)。

## Overtone 泛音

音中除基频之外的任何谐波。（也参见“分音”）

## Pad 衰减器

1. 一种衰减输入信号的设备或电路，通常用于防止信号路径后续放大器过载。（有时也称为“衰减垫”。）
2. 一个表面可以被鼓棒击中的设备；击中垫产生输出脉冲（或 `MIDI` 命令），导致鼓机或合成器发出鼓声。
3. 一种合成器音色/程序，用于创建持续的背景或氛围声。

## Pan (Panning) 声位

在立体声场内“放置”声音的过程。这是通过控制左右扬声器之间信号的平衡来实现的，使耳朵听到的声音像是来自左右之间声音空间中的特定点。这个声音空间有时被称为“立体声全景”，“panning”一词便源于此。在环绕声中，声位发生在 360° 声音空间内，而不仅仅是左右。

## Panpot 声位电位器

“Panoramic Potentiometer”的缩写，是通道条上的一个旋钮，通过控制发送到每个扬声器或通道的信号量，控制音频信号在立体（或环绕）空间中的声位。

## Parallel Jacks 并行插孔

多个插孔的连接方式使得每个连接都对应到相应的插孔。

## Parallel Port 并行端口

能够通过不同引脚同时传输和接收数字数据的连接器。

## Parameter 参数

参数是给合成器模块中你尝试更改的任何值、属性或控制的华丽名称。例如，振荡器的参数通常包括它的音高和脉冲波宽度。滤波器的参数将包括截止频率（音高）、共振量（反馈），以及可能作为不同输出之间混合的其他控制。参数曾是描述软件中可以更改的值的流行术语，一些硬件合成器也延续了这一概念。

## Parametric Equalization 参数均衡器

一种均衡器，其中所有的均衡参数均可调整为任意值，包括中心频率、提升或衰减的量。

## Paraphonic 半声部

半声部合成器是指所有弹奏的音符都通过单个滤波器 (`VCF`) 和放大器 (`VCA`)。这对于单声合成器来说，允许 2 到 4 个独立音符独立控制音高同时仍经过滤波器并不多见。这对于和弦非常有效；但当在按下其他音符时弹奏新音符效果并不好，因为所有音符都会一起重新触发。

## Partial 分音

1. 泛音的另一个词。
2. 构成复杂声音的任何正弦波，有助于定义音色。这一概念是合成器创建声音的关键部分：在加法合成中，多个部分组合以创建特定的音色。

## Pass Band 通带

滤波器将“通过”而非减少的信号频率范围。

## Passive Device 无源设备

不产生或控制电流的组件（与“有源设备”相反）。在音频应用中，这通常指设计中不包含放大器的设备。例如，有源扬声器自带电源，而无源扬声器需要外部放大器来还原声音。（参见“有源设备”）

## Passive 无源

意味着没有涉及（即未连接电源）电子设备——例如直接让信号通过电位器，而不是使用放大器和其他设备创建一个混合电路。无源廉价且简单，并且不会给信号增加噪声。但无源电子设备无法相互隔离（这意味着它们可能会以不可理想的方式相互作用），并且无法放大或反转信号。

## Patch Bay 跳线架

`Patch Bay` 是一个包含一系列插孔的面板或组件，连接调音台和录音室组件大部分输入输出，用于组织、管理和调节信号流。

## Patch Cable 跳线线

用于连接模块合成器中不同输入和输出的电缆，

## 附录 B：音频工程术语 (0 - 9 - A - Z)

用于传输电控制电压和音频。该术语源于旧式的电话接线盘，当时接线员必须使用电缆将两个呼叫者物理地连接在一起。由于不同的模块化格式通常使用不同的连接器标准，你需要确保跳线线末端的连接器尺寸是你所需的（`Eurack` 使用 3.5mm，`5U/Moog` 单元使用 1/4"，或 `Serge` 或 `Buchla` 电压使用香蕉头）。

### 跳线线 (Patch Cord / Patch Cable)

一种两端带有插头的绝缘电缆，用于路由音频信号。跳线线通常被认为是用于跳线槽（`patch bay`）中建立连接的短线（因此得名）；然而，跳线线可以方便设备之间的任何音频连接，长度多样，并可包含多种类型的连接器。

### 跳线区域 (Patch Field)

一种面板或组件，其中包含一系列插座，连接了调音台和工作室组件的大部分输入和输出，用于组织、管理和调节信号流。

### 跳线库管理器 (Patch Librarian)

一种计算机程序，允许通过 `MIDI` 在合成器之外存储音色补丁（sound patches）。

### 跳线面板 (Patch Panel)

一种面板或组件，其中包含一系列插座，连接了调音台和工作室组件的大部分输入和输出，用于组织、管理和调节信号流。

### 跳线 (Patch)

指代一组模块如何相互连接以产生声音的简称为 patch，源于使用跳线线将模块连接在一起的事实。

- 1) 通过使用插入插座的带头短线，对音频系统（如调音台）中的信号进行路由或重新路由。
- 2) 合成器上的音色设置或程序。

## 路径 (Path)

信号路径（`Signal Path`）的缩写，电流或数据在电路中或设备中传输的方式。

## PCM

脉冲编码调制（`Pulse Code Modulation`）——一种将模拟信号转换为数字代码的过程。这是通过规律快速间隔对模拟信号的幅度进行采样，将其转换为二进制数字作为原始信号的数字表示。速率越快，数字复制效果越好。`PCM` 是数字音频中最常见的 A/D 转换形式。

## PD

相位失真（`Phase Distortion`）合成曾被 `Casio` 在 80 年代表的 `CZ` 系列合成器中使用。它与 `FM`（频率调制）有关，但具有足够的差异，以避免当时雅马 `FM` 合成器所用专利的问题。有趣的是，它在模拟许多“模拟”效果方面表现出色，包括谐振滤波的声音。

## 峰值滤波器 (Peak Filter)

一种 `EQ` 电路/滤波器，用于增强或衰减音频信号中的中间部分（中心频率），而不是高通滤波器或低通滤波器。（不要与幅度峰值混淆）。

## 峰值表 (Peak Meter)

一种检测波形绝对峰值值的仪表，而不是 `RMS` 值。（另见“峰值”、“均方根”、“RMS 功率表”）。

## 峰值到峰值 (Peak to Peak Value)

音频信号中正峰和负峰之间的总幅度。对于正弦波，它等于峰值的两倍。（另见“峰值”）。

## 峰值 (Peak Value)

对波形在任何时刻的最大正或负值（幅度）的测量。在音频中，这在视觉上表现为波形在零轴上方或下方的最远点。

## 效果板 (Pedal Board)

一块带有多个连接好的吉他效果器的板，吉他手可以通过它方便地激活多种不同的效果。

## 幻象电源 (Phantom Power)

一种通过音频线为电容麦克风和其他组件提供直流电压的系统，消除了对外部电源的需求。

## 相位叠加 (Phase Addition)

波形处于相似相位关系时发生的音频能量增加，导致音量增加到应值的两倍。

## 相位抵消 (Phase Cancellation)

相位叠加的反面，当两个相似波形相位相反并开始相互抵消时发生的能量减少，会导致音量大幅降低或消除当两个相同的波形完全相反（180度）时，结果是信号完全静音或消除。

## 相位失真合成 (Phase Distortion Synthesis)

相位失真最初由 `Casio` 在 80 年代的 `CZ` 系列合成器合成。它与 `FM`（频率调制）相似，但具有足够的差异，以避免当时雅马 `FM` 合成器所用专利的问题。有趣的是，它在模拟“模拟”效果方面表现出色，包括谐振滤波的声音。

## 相位失真 (Phase Distortion)

由于信号中的相位移导致声音变化。有时在合成器中用作改变波形或为声音增加谐波的方法。

## 相位锁定 (Phase Lock)

任何通过修正相位差来帮助同步信号或设备的过程。例如，在模拟磁带机中，相位锁定通过感知两台机器播放导频时的相位差并调整速度以消除相位差，从而帮助多台机器保持同步。在合成器中，相位锁定控制一个频率发生器，使其波形与另一个频率发生器的信号同步开始。

锁环（`PLL`）是电子设备时钟功能中使用的参考信号。

## 锁环 (Phase Locked Loop)

锁环本质上是一种振荡器，试图匹配另一个信号的频率——或者更重要的是其频率的倍频或分频。它最常用于创建一个远高于输入参考信号的频率——例如定时模块，它可以创建一个产生输入时钟 2、4 或更多倍的输出时钟——可能用于驱动开关电容器滤波器。

## 相位调制 (Phase Modulation)

一些人认为这是频率调制（`FM`）的严谨正确术语，因为导致振荡器运行快或慢（快速改变频率）的行为与推进或延迟正常播放的位置（相位）是相同的。但在创建 `FM` 跳线时，不要纠结于术语；只需将一个振荡器的输出连接到另一个的频率输入即可。

## 相位反转 (Phase Reverse)

电路中一种使波形偏移180度的变化。

## 相位移 (Phase Shift)

以度为单位引入音频信号的延迟。

## 相位器 (Phase Shifter)

这种效果将信号拆分为两个副本。其中一个通过“全通滤波器”传输，该滤波器不会像高通或低通滤波器那样衰减原始信号，但它改变了信号的相位，导致这些谐波根据其频率相对于原始信号产生不同程度的相位移。将这两个副本重新混合，原始信号的不同谐波分量会相互抵消（参见“相位”），产生陷波滤波效果。相位器的每个“阶段”（全通滤波器部分）都会产生一个槽。阶段越多，槽越多，效果越深。

## 相位锁环 (Phase-Locked Loop)

`PLL` - 任何通过修正相位差来帮助同步信号或设备的过程。例如，在模拟磁带机中，相位锁定通过感知两台机器播放导频时的相位差并调整速度以消除相位差，从而帮助多台机器保持同步。

## 相位 (Phase)

以度为单位的两个相似波形之间时间差的测量。

波形的一个周期被认为有 360 度，就像圆一样。你在圆（或波形）上移动的距离可以通过相位来定义。例如，如果你处于波形周期的四分之一处，你的相位就是 90 度。

## 附录 B：音频工程术语 (0 - 9 - A - Z)

### 相移 (Phasing)

通过改变音频信号的相位移，然后将其与直接信号混合而产生的音效。

### 宽 (Phon)

表观响度的单位，数值上等于 1000 Hz 播放音调的相同 dB 值。例如，如果一个声音听起来与 60dB 的 1000Hz 音调一样大，则该声音为 60 宽。

### 插头 (Phone Plug)

直径为 1/4 英寸、长度为 1 1/4 英寸的插头（或对应的插座），用于音频连接。

### 唱片插头 (Phono Plug)

大多数立体声系统中常见的连接器，以中心针为一个连接，外壳为第二个连接。

### 物理建模 (Physical Modeling)

一种（通常是数字的）合成方法，通过重建实际乐器的组件——例如振动的弦或管子，或者作为吉他或鼓外壳的共鸣体——并将它们组合在一起来产生声音。有少数模块可以执行这种建模来创建它们的声音。

### 拾音模式 (Pickup Pattern)

麦克风前方或周围均匀采集声音的区域形状。许多人将此术与“极性模式”（`polar pattern`）交叉使用，但极性模式提供了关于麦克风敏感性的更多细节。（也称为“极性模式”。）

### 拾音器 (Pickup)

1. 电吉他或其他乐器上的设备，根据弦的运动输出音频信号。
2. 参见“接触式麦克风”。

### 压带轮 (Pinch Roller)

录音机上的橡胶（或塑料）轮，将磁带夹在它和卷轴之间，允许卷轴带动磁带。

### 乒乓/混缩 (Ping-Ponging / Bouncing)

将多个轨道合并并混合到一条或两个轨道（单声道或立体声）的技术。这可以在实时完成，也可以通过通过控制台播放轨道并录制到单独轨道中，或者通过数字音频工作站（`DAW`）数字化完成。工程师过去经常使用混缩来腾出额外的轨道进行录制，但在轨道几乎无限的数字工作站中，这种做法基本上过时了。如今，工程师通常通过混缩来创建歌曲的初步或最终混音。

### 粉红噪声 (Pink Noise)

一种类似于白噪声的噪声信号，包含所有可听频率，但每个音域的能量相等，而不是所有频带相等。工程师经常使用粉红噪声作为调优和校准音频设备的工具。（参见“白噪声”。）噪声是一种随机的、无音高的音频信号，听起来像嘶嘶声或风声。粉红噪声每个音域内具有相同的能量（声级）。由于每个高音域的频率都是下方音域的两倍，它将能量分散在更宽的范围内，因此粉红噪声往往具有更自然、非电子化的声音，低音更多高音更少——特别是与白噪声相比，白噪声每个赫兹（频率）能量相等，因此听起来往往比较明亮。

### 变音 (Pitch Bend)

合成器、键盘或控制器上的机制，可以使音符音高发生微小的上下移动。

### 音高转电压转换器 (Pitch to Voltage Converter)

一种检测音频波形频率并将其转换为控制电压的设备，反过来给振荡器以产生相同频率的音高。

### 音高转 MIDI 转换器 (Pitch-to-MIDI Converter)

一种检测模拟音频信号中音高并将其翻译 `MIDI` 信息的设备。也称为“音频转 `MIDI` 转换器”。

### 音高转电压转换器 (Pitch-to-Voltage Converter)

一种检测音频波形频率并将其转换为控制电压的设备，反过来给振荡器以产生相同频率的音高。

### 音高 (Pitch)

1. 耳朵对频率的感知（音乐中较高或较低的音调）。
2. 磁带传输设备上的控制，可略微增加或降低速度，从而改变音乐的音高和时间。

### 板混响 (Plate Reverb)

一种通过类似于扬声器驱动单元的换能器将振动传过金属板，从而产生人工混响的设备。物理板混响被认为是一种复古的人工混响；现在，大多数板混响效果通过插件或混响单元进行数字模拟。

### 播放头 (Playback Head)

一种将录制在磁带上的磁通量转换为用于播放的音频信号的换能器。

### 播放模式 (Playback Mode)

控制台上的某种配置，允许在监听混音器中快速播放之前录制在磁带上或通过 `DAW` 的信号。

### 播放 (Playback)

1. 录制音频的再生。
2. 在电影或视频制作中，通过扬声器播放音乐，以便表演者/音乐家能够配合音乐为摄像机表演。

### 播放列表 (Playlist)

1. 参见“片段”（Take）。
2. 用户定义的歌曲选择；大多数流媒体和数字媒体播放器都有此功能。

### 锁相环 (PLL)

锁相环本质上是一种振荡器，试图匹配另一个信号的频率——重要的是匹配其频率的分数或倍数。这通常用于创建一个比输入参考信号高得多的频率——例如，可以创建比输入时钟 2、4、8 或更多倍输出时钟的时序模块，或者锁定在输入音高倍数上的高频振荡器——也许用于驱动如开关电容滤波器等特殊电路。

### 插头 (Plug)

一种连接器，通常位于电缆上，与插座配合。

### 极性模式 (Polar Pattern)

1. 在麦克风中，麦克风周围对声波敏感区域的图形显示，详细说明了从不同方向到达声音的 dB 输出电平。
2. 在麦克风中，麦克风周围对声波敏感区域的图形显示，详细说明了从不同方向到达声音的 dB 输出电平。

### 极性 (Polarity)

声音的方向。

### 偏振器 (Polarizer)

在麦克风中，麦克风周围对声波敏感区域的图形显示，详细说明了从不同方向到达声音的 dB 输出电平。

### 极化电压 (Polarizing Voltage)

在麦克风中，麦克风周围对声波敏感区域的图形显示，详细说明了从不同方向到达声音的 dB 输出电平。

### 极片 (Pole Pieces)

指扬声器或播放头使用的材料。

### 极点 (Pole)

这是一个关于滤波器设计的术语，用于衰减截止频率之外的频率。

### 多音 (Polyphonic)

“多音”一词指的是可以同时播放多个音符或音声的合成器。

### 端口 (Port)

1. 插座或电子设备上的连接点，用于传输接收数字数据，类似于插座接收和传输音频信号。
2. 声箱上的一个开口或通风口，与声箱内的空气运动共振，用于倒相式声箱和低音扬声器增强低频。

### 滑音 (Portamento)



从一个音高滑向另一个音高的变化。也允许这种变化的合成器模式或 MIDI 命令。

## 后期制作 (Post Production)

指在录制或拍摄完成后添加轨道、编辑和其他精细调整的工作。录制的后期制作包括额外的配音、编辑、混音和母带。电影后期制作包括广泛的额外音频视觉效果。注意：我们在此提到电影是因为电影后期制作涉及大量的音频工作（例如旁白、音效、音频混音和编辑），以至于许多工程师全职从事电影后期制作。

## 后滚 (Post Roll)

录制结束后继续运行的空白磁带段（或 DAW 中的轨道静音）。参见“前滚”（Pre-Roll）。

## 后推子 (Post-Fader)

指辅助发送位置或设置，将发送放置在信号路径中通道推子之后。后推子发送会使推子本身影响发送信号的电平，与前推子相反。参见“前推子”（Pre-Fader）。

## 附录 B：音频工程术语 (0 - 9 - A - Z)

### Post（后发送）

指一种辅助位置或设置，将发送点放置在信号路径中通道推子之后。推后发送信号（post-fader）意味着推子本身会影响发送信号的电平，与推前（pre-fader）相反。（参见 Pre-Fader。）

### Pot（电位器）

Potentiometer（缩写 "Pot"）通常被认为是“旋钮”的雅说法，电位器本质上是任何通过改变变化来控制输入或输出电压的机制（例如：信号的左/右平衡、音量控制，或发送到辅助发送口或总线的信号量）。电位器可以是旋钮或推子，这意味着调音台上几乎每一个不是按钮或开关的控制部件都是电位器。然而，许多工程师习惯于将推子称为“faders”，将旋钮称为“pots”。

### Power Amplifier（功率放大器）

（缩写 "Power Amp"）一种用于连接线路信号以驱动扬声器或一组扬声器的设备。（参见 "Line Level."）

### Power Distribution Board（电源分配板）

这种简单的电路板获取模块化系统电源的输出并创建其副本，路由到连接各个独立模块的连接器。

### PPQN（每四分符脉冲数）

当你发送时钟信号（通常是门信号或其他电脉冲）环绕模块化合成器让序列器移动步骤等时，了解时钟脉冲的速度是非常重要的。这通常定义为每四分符有多少个脉冲——简称为 PPQ 或 PPQN。如果时钟只是每个四分符发生一次，标准是 1 PPQN；对于 DIN Sync（早期 Roland 合成器的一种流行标准，DIN 是使用的连接器类型），标准是 24 PPQN。这意味着主脉冲可以定义每个八分音符的三连音 (8 x 3)。

### Pre / Post Switch（推前/后开关）

输入模块上的开关决定了发送点位于信号路径中主通道推子的之前还是之后（参见 "Pre-Fader," "Post-Fader."）。

### Pre Emphasis（预强调）

在录制过程中对高频增强，以使可听信号保持在底噪之上。

### Pre Fader（推前）

指一种辅助位置或设置，将发送点放置在信号路径中通道推子之前。推前发送信号（pre-fader）意味着推子不会影响发送信号的电平，与推后（post-fader）相反。

### Pre-Delay（预延迟）

混响单元或插件上的一个参数，决定了原始干声（dry sound）与混响早期反射之间的持续时间（延迟）。此功能通常用于模拟房间的自然声学特性，但也可用于不自然的效果。

### Pre-Echo（预回声）

（也称为 "Forward Echo"）数字音频中常见的压缩伪真，即在声音（或声音的一部分）出现之前就能听到其“回声”，通常是由于压缩数字格式中的数据不一致引起的。预回声类型有时也会出现在录制成品中，如在磁带上由于串扰（print-through）引起的低电平泄漏，以及在黑胶唱片上由于静音与强瞬态波之间的物理差异和/或变形。在数字格式中，预回声通常是一个不需要的问题，需要额外的信号处理来解决——但在某些情况下，它也可以特意用于音效（不要与 "Reverse Echo" 混淆）。

### Pre-Fade Listen (PFL)（推前监听）

调音台或 DAW 通道条上的功能，允许通道信号通过推子通道听到并通常进行电平检测。

### Preamplifier (Preamp)（前放大器）

一种低噪声放大器，旨在接收低电平信号（例如来自麦克风），并在插入调音台之前将其提升到线路电平。

### Precedence Effect (Haas Effect)（先行效应/哈斯效应）

简单来说，这是人类听觉中的一种因素，我们通过声音的时间而不是声音电平来感知声源。在赫尔穆特·哈斯（Helmut Haas）的研究中，他确定第一声波到达耳朵的速度比大脑判断第一声声音来自反射或另一个源的再生要快。声音的反射必须比原始源至少大 10dB，或者延迟超过 30ms（此时我们将其感知为回声），才会影响我们对声音方向的感知。这有助于我们区分原始声音，而不至于被附近表面的反射和混响所困扰。理解哈斯效应在现场音频环境中特别有用，尤其是在大型场馆中，那里扬声器经过延迟处理以匹配来自源的初始声波。

### Precision Adder（精密加法器）

合成器对音高控制电压的意外变化非常敏感——任何误差都会导致振荡器跑调。因此，每当模块化系统内部添加音高控制电压时，都应该使用精密加法器，精确地叠加音高电压而不引入误差。普通的调音台会轻微衰减或放大通过它们的电压，这在大多数情况下会导致调音误差。

### Premix（预混音）

- 1) 将一组轨道作为一个整体进行混合，然后通过将其路由到辅助通道，在其他轨的上下文中管理混合后的组。通过渲染（bouncing）合并轨道是预混的一种，但预混并不一定是预录制的。（参见 "Bouncing."）

- 2) 电影后期制作的重要部分，即混合某部分音频以与其他部分结合的过程。对话、音效、SFX 和音乐在视频之前可能都要预混。

### Presence Frequencies（存在感频率）

4 kHz 到 6 kHz 之间的音频频率范围，增强时可以增加存在感，尤其是对于人声。

### Presence（存在感）

- 1) 在放大和混音中，增强中频以使声音或乐器突出，营造出声源更加“现场”、就在听者旁边的印象。

- 2) 参见 "Room Tone."（环境音）。

### Preset（预设）

合成器、信号处理器、插件或其他电子设备上的出厂编程参数集。

### Pressure Microphone（压力式麦克风）

（也称为“压力操作麦克风”）——一种振膜在与麦克风外壳内部正常或受控空气压力作用时，对入射声压做出响应。这种设计使振膜无论方向如何都对压力敏感，从而具有全指向性拾音模式。（参见 "Omnidirectional Pattern."）

### Pressure Sensitivity (Aftertouch)（压力感应）

某些键盘乐器的功能，在按下按键后施加额外压力可以激活额外的 MIDI 指令；合成器或键盘控制器的 Touch（指合成器在按下按键后、释放之前的控制或操作功能，将激活一个由玩家设置的命令）。

### Pressure Zone Microphone (Boundary Microphone)（压力区域麦克风/边界麦克风）

一种全指向性麦克风，设计为放置在平面（或边界）上，有效地创建一个“半全指向”拾音模式，同时消除反射声引起的相位问题风险。一种流行的边界麦克风是 Crown Audio 的专利压力区域麦克风 (PZM)。

### Pressure-Gradient Microphone（压力梯度麦克风）

（也称为“速度麦克风”）一种振膜正反暴露的麦克风，振膜运动由前后压力差引起。这创建了双向或“八字形”拾音模式（参见 “Bi-Directional Pattern.”）

### Pressure（压力）

某些键盘测量你按键的方式，并将其转换为电压或其他控制信号，如 MIDI，可用于表达表现力，例如增加颤音或打开滤波器宽度。单音压力感应无论按下哪个键，都为整个键盘测量一个压力值；多音压力感应为每个单独的键产生一个信号。重要冷知识：触摸板键盘实际上测量的是接触它们的皮肤表面积，而不是压力或力 (force) – 你可以通过在指尖和指节之间滑动来增加或减少触后（aftertouch）量。

### 串扰 (Print Through)

磁通从模拟磁带的一层到另一层的非预期的传输。

### Pro Tools

Avid 对其数字音频工作站 (DAW) 的商品名称，已成为专业录音室的行业标准。

### 制作人 (Producer)

在音乐中，制作人是音频录制项目的导演；是负责在预算内获得所需质量最终产品的人员。

### 制作棚 (Production Studio)

广义上，指任何艺术领域内专门用于制作的空间，例如电影/视频、动画或后期制作。在音频语境下，制作棚实际上是一个录音室，专门负责将预录的音乐、效果与新录制的对话进行组装和混音。

### 制作/后期制作 (Production)

1) 制作音乐时投入的集体活动。

2) 描述录音质量——即录制和混音过程中制作决策的最终结果。

### 程序更改 (Program Change)

一种告诉接收设备更改预设的 MIDI 消息。

### 可编程的 (Programmable)

能够让用户更改参数，特别是在计算机控制设备中。

### 提示 (Prompt)

显示在计算机屏幕上供用户遵循的一组指令。

### 协议 (Protocol)

在数字和信息技术中，一组规定以标准格式结构化和传输传输的规则，以便所有相关设备都能正确解释数据。

### 近接效应 (Proximity Effect)

当麦克风更靠近声源时，麦克风输出中低频频率的自然增强现象。

### 声心理学 (Psychoacoustics)

研究人类如何感知和响应声音的学科，不仅限于解释物理声波的层面，还考虑了心理和情感因素。这一科学分支有助于音频工程师理解大脑如何解释各种声音和频率。

### 滚子/轮 (Puck)

任何由金属、纤维、橡胶等制的圆形部件，通过旋转动力源驱动物体。

录音室中常见的例子是旋转 Leslie 扬声器中的滚子。

### 脉冲编码调制 (PCM)

将模拟信号转换为数字代码的过程。这是通过定期采样对模拟信号的幅度进行采样，并将其转换为二进制数字作为原始信号的数字表示来实现的。采样率越高，数字复制效果越好。PCM 是数字音频中最常见的 A/D 转换形式。

### 四分音符脉冲数 (Pulse Per Quarter Note)

当你向模块化合成器发送时钟信号（通常是门信号或其他电脉冲）以使序列器按其步骤移动时，了解时钟的脉冲速度很有帮助。这通常定义为每个四分音符有多少个波形——简称为 PPQ 或 PPQN。如果时钟每个四分音符脉冲一次，则时钟速度为 1 PPQN；在 DIN Sync（早期 Roland 常用标准，DIN 是一种电气连接器类型）或 MIDI 时钟的情况下，标准为 24 PPQN。这意味着主脉冲可以为每个八分音符定义三连音 (8 x 3)。

### 脉宽调制 (Pulse Width Modulation)

大多数方波波振荡器都有额外的控制电压输入，用于设置“方波”顶部部分的宽度（使顶部比底部更宽，反之亦然）。改变产生的脉冲波的行为创建了一种多普勒频移；来回改变宽度——例如，通过低频波振器调制宽度——会产生合唱效果，听起来像一对未调谐的振荡器。产生的效果被称为脉冲波调制。

使用控制信号来改变脉冲波宽度的过程，本质上是在方波和脉冲波之间切换。这种做法具有产生更丰富音色的效果，让声音听起来更厚实、更丰满，或赋予数字声音模拟的属性。

### 脉冲 (Pulse)

脉冲在模块化合成器中有几种不同的含义。当你改变方波的形状使其中一部分大于另一部分时，它被称为脉冲。

1) 制作音乐时的集体动作。

2) 描述录音质量——即录制和混音过程中制作决策的最终结果。

1) 音乐波的的，，定义为脉冲。

2) 描述序列器的的稳定，，通常被称为脉冲冲。

在录音室术语中，当压缩器快速压缩时会产生听觉上的变化，也被称为“脉冲波”。

### 抽吸与呼吸 (Pumping and Breathing)

在工作室术语中，当压缩器压缩并释放声音时产生的听觉变化。“抽吸”通常指压缩后的声音量增加；“呼吸”指的是人声的类似效果。有些工程师为了创造特定的效果而偶尔刻意使用它。

### 点入/点出录制 (Punch In / Punch Out Recording)

在播放磁带或 DAW 期间激活或取消录制功能的过程，通常在表演者演奏/演唱时进行。这可以作为快速录制的方法，或者无需从头开始轨道。

### 纯音 (Pure Tone)

仅包含基频而无泛音或谐波的音，在图上表示为简单的正弦波。

### PVC

PVC 代表音高到电压的转换。为了使用键盘以外的东西控制合成器（例如触摸板），某些模块或设备尝试检测音频信号的音高，将其转换为与原始声音同步的相应电压。

### PWM (脉宽调制)

大多数输出方波的波振荡器也有一个额外的控制电压输入，用于设置“方波”顶部部分的宽度（显然，使顶部比底部更宽，反之亦然）。改变脉冲波宽度的行为创建了一种多普勒频移；来回改变宽度——例如，通过低频波振器调制宽度——会产生合唱效果，听起来像一对未调谐的振荡器。产生的效果被称为脉冲波调制。

### PZM

Crown 压力区麦克风的缩写。（参见“边界麦克风”）。

### Q - (也称为“Q 因子”)

代表“品质因子”，定义了均衡器影响的频率带宽。Q 值越小，受影响的频率曲线越宽。

如果你来自专业音频领域，可能习惯于 Q 指峰值或带通滤波器的宽窄。在合成器滤波器中，当你增加共振（反馈）时，截止频率曲线或形状周围会形成一个峰值。共振越高，峰值越高越窄。因此，有些人曾使用 Q 术语指共振量。

### 四声道声 (Quadraphonic)

一种很少使用的四声道声音系统，通道被标记为左前、左后、右前、右后，旨在从房间的四个角传递声音。四声道声是今天环绕声系统的先驱。

### 正交 (Quadrature)

你可以将波形的完整周期定义为包含 360 度，类似于圆。四分之一沿着这个圆周的路径——或移动到周期性波四分之一处的位置——是 90°。正弦波和余弦波之间存在 90 度或四分之一周期的相位偏移（相位，phase）。由于这是一个周期的四分之一，因此通常被称为正交关系（quadrature relationship）。

## 量化失真

量化失真/量化误差 —— 由于将大量的模拟值四舍入到最接近的数字量，在模拟信号与其采样副本之间进行“转换”时产生的有效“误差”。这通常会导致声音中产生额外的随机频率，通常听为噪声。

## 量化噪声

由量化误差导致信号中的调制噪声。

## 量化

- 1) 在数字音乐中，通过将音符移动到时间线上的精确位置来调整音乐的节奏表演，实际上是将音符的发生“四舍入”到最近定义的增量上。

- 2) 在模拟转数字转换中，使用相同的数学量化原理将模拟信号转换为较小的阶梯集合（数字量）。

## 量化器

量化器将输入电压自动修正为最接近的理想目标，例如对应音阶中半音或其他音符的电压。这些有时被内置在序列发生器或振荡器等模块中，但通常情况下是独立模块。

## 机架耳朵 (Rack Ears)

机架耳朵/机架法 —— 可安装在设备上的支架，使其能够安装在标准机架中。

## 机架安装

描述可以放置在设备机架中的外置设备。

## 机架划痕 (Rack Rash)

当你将模块安装到箱体时，用于安装模块的螺钉或螺栓头可能会划伤模块的前面板。这些划痕被称为机架划痕。在安装模块时你几乎看不到它，划痕在螺钉或螺栓头后面，但尽管如此，为没有划痕的二手模块会支付更多费用。买一袋塑料垫圈并将它们放在螺钉或螺栓头后面，消除别人不想买你二手模块的理由。

## 机架单元 (Rack Unit)

机架式设备通常遵循一套标准尺寸，包括 19 英寸（48.3 厘米）的宽度，以及高度为“机架单元”（简称 U），每个 U 等于 1.75 英寸（4.4 厘米）。许多常见的模块化合成器格式遵循机架单元系统来标准化模块高度——例如 Eurorack 的 3U（3 x 1.75 = 5.25 英寸或 13.3 厘米），Buchla 和 Serge 的 4U，以及经典模块化 Moog 的 5U（有时称为 MU，Moog Unit）。

## 辐射图

扬声器覆盖范围的图形描述。这与麦克风的极性图相似，区别在于极性图描述声音到达麦克风的区域，而辐射图描述声音如何从扬声器扩散出来。

## 辐射

扬声器的覆盖角度和模式。

## 斜坡 (Ramp)

通常情况下，斜坡是指任何稳定上升或下降的电压；当达到目标电压时经常重置并重新开始。锯齿振荡器波形有时被称为斜坡。包络发生器的各个阶段也被称为斜坡，当它从 0 伏上升到最大水平（例如攻击阶段为 5v），然后从此峰值下降到维持电平（衰减阶段）。

## 随机存取存储 (RAM)

计算机中的“短期”内存，与处理器协同执行即时任务（与用于保存和调回项目的硬盘存储内存相反）。在录音室中，计算机的 RAM 越多，一次性处理大量数据的能力就越强（例如在多轨道录音或使用虚拟 MIDI 器器时）。

## 随机音符生成器

一种以速率生成随机补丁的设备，用于合成器。

## 随机

模块系统内部移动的大多数电压变化非常有用：音频速率振荡器或低频振荡器的重复波形；包络发生器的上升和下降电压。然而，随机漂动的电压也有用，可以创建从音高细微变化到音量或滤波剧烈变化的各种。噪声是音频速率信号的一个例子。

## Rap (节奏)

在音乐或打击乐表演中执行快速的节奏部分。

## 疏散 (Rarefaction)

声波谷期间空气粒子密度降低；在“压缩与疏散”的背景下，它是压缩的反面。（参见“压缩 Compression”。）

## 连触发 (Ratching)

这是序列发生器中使用的一种技巧，序列中的一个阶段可能会被快速触发多次，而不仅仅是在移动到该阶段时只触发一次。例如，结果可能是一系列四分音符，其中一个或多个阶段会出现四次十六六分音符的爆发。

## 速率 (Rate)

这个词有时用于指低频振荡器或类似的重复功能的速度或频率，例如序列发生器的节拍时。

## 额定负载阻抗

设备设计用于驱动的输入阻抗，或设备输入端对电流流的阻碍。

## RCA 插头

（也称为唱片插头）一种在大多数立体声系统中看到的常见的音频连接器，中心针脚作为一个连接，外壳作为第二个连接。

## 只读存储器 (ROM)

一种不能擦除的数据存储类型。

## 读取 (Read)



# 从存储中检索信息

## Reason

一种流行的软件，提供合成器、采样器、效果和序列发生器等许多功能。它还用于创建和混合音频。

## 读存储器 (Read-ROM)

用于光学介质（如 `CD-ROM`）上的数据存储类型。

## 只读 (Read Only)

一种不能擦除的数据存储类型。

## 只读 (Read-Only)

用于光学介质（如 `CD-ROM`）的数据存储类型。

## 只读存储器 (Read-Memory)

用于计算机的数据存储类型。

## 只读 (Read-Only)

一种不能擦除的数据存储类型。

## 录制

将音频、视频或数据录制到存储介质的过程。

## 录音课程

录制音乐的时间段。

## 录音头

磁带机上的制的设备。

## 录音电平

决定录制电平量的控制。

## 录音监听

在磁带机上，允许监听输入。

## 录制就绪

机器准备好录制的状态。

## 录音总线

发送信号到录制的总线。（参见“总线 Bus”。）

## 录音室

录制音频、视频或数据的地方。

## 整流器

确保电压保持正值的电路。在电源中，它用于移除交流电的负成分。半波整流仅通过正电压；全波整流器取任何电压并反转使其变为正值。这实际上使频率倍增。

## 红噪声 (Red Noise)

也称为棕噪声，其功率密度（频谱响度）随频率增加而每倍频减少 `6 dB`。它具有深低音感。

## 卷轴 (Reel)

- 1) 磁带绕在轴心和边缘上；录制和播放将磁带从一个卷轴释放到另一个。
- 2) 有些网站称为“演示带”（demo reel），展示音乐家、音频工程师、演员或其他视听专业能力的音频或视频合集。与旨在推销一或多首歌曲的 Demo 不同，演示带旨在推广人士的能力而非产品本身。该术语本身是这种促销材料通过卷轴交付的时代的遗留。

## 参考电平 (Reference Level)

- 1) 标准基准音量，用于测量高于或低于基准的分贝电平量。
- 2) “工作电平 Operating Level”。

## 参考音

一种单频音调（通常为 `1000 Hz`），用于校准音响设备的电平。（参见“测试音 Test Tones”。）

## 反射声 (Reflected Sound)

经过周围表面一次或多次反射到达麦克风或听者的声音。

## 反射 (Reflection)

在声学中，声波在平面表面上的反射，与吸收相反。反射对我们感知整体声音有很大影响；来自远处的反射感知为回声，而混响由成千上万的反射产生。（参见“吸收 Absorption”、“早期反射 Early Reflection”、“回声 Echo”、“混响 Reverberation”。）

## 再 (Regeneration)

在合成器内部可能有两种含义，都指反馈。回声单元可以将其输出反馈回输入，导致延迟信号重复

## 附录 B：音频工程术语 (0 - 9 - A - Z)

再次；这有时被称为再生（regeneration）。此外，极少情况下你会听到滤波器中的共鸣被称为再生。

### 稳压电源 (Regulated Power Supply)

一种为电子设备供电的设备，当设备开启或线路电压发生变化时，其输出电压不会波动。稳压电源旨在保护敏感电子设备免受破坏性电压浪涌的影响。

### 继电器 (Relay)

一种电磁驱动开关，在施加控制电压时连接或断开两个端子。

### 释放时间 (Release Time)

在动态信号处理器中，当输入信号超过指定阈值时，输出信号返回原始水平所需的时间。

### 释放 (Release)

这指的是包络的最后一个阶段，通常会跌回 `0 伏`，通常导致静音。它经常用于讨论攻击/释放（AR）或攻击/衰减/维持/释放（ADSR）包络生成器的语文中，但也可以指任何包络的最终阶段。

### 远程 (Remote)

1) 一种无线控制另一台设备功能的设备。
2) 描述现场录音，相对于录音室录音。

### 重置 (Reset)

模块上的 `Reset` 输入接受触发或门控信号，并告诉模块回到其正在执行的任务的开头。对于时钟分频器，这意味着假设下一个时钟是你在分频中应该数的数的时钟（在完整定义中会有更多介绍）。对于序列器，这意味着回到第一阶段。对于包络，这意味着回到攻击阶段（attack stage）的开始。对于门控延迟，这意味着重新启动延迟计时器。

### 剩磁 (Residual Magnetization)

在去除磁力后，磁性材料中留下的磁性量。剩磁会随着时间的推移在磁带机中积累，导致声音输出产生失真和噪声，或部分擦除磁带。

### 残留噪声 (Residual Noise)

录带在擦除后留在录带上的噪声水平。

### 电阻 (Resistance)

物质对电流流的阻碍，以欧姆为单位测量。

### 电阻 (Resistor)

一种具有特定电流电阻的电子元件，用于电路内调节电流流。

### 共鸣 (Resonance)

1) 物理物质在某些频率下以更多能量振动的自然倾向。共鸣原理是声学仪器设计的关键元素；例如，吉他或小提琴的空腔设计成与弦的振动产生共鸣。共鸣在空间的声学设计中也起着作用，甚至有助于开发良好的投影声音的歌唱技巧。

当滤波器的输出反馈到其输入时，结果是滤波器截止频率或角频率附近的谐波增强。听觉上的结果类似于在一个具有共鸣的房间里播放声音——在特定频率产生感应、增强性的回声或振动。因此，“共鸣”一词通常指滤波器的反馈量。

## 共振频率 (Resonant Frequency)

物理物体自然振动的频率。

## 共振 (Resonate)

以共振频率振动。也指声源停止后导致声音持续的残留回响。这种持续的声音由于附近物体的感共共引起。

## 共振器 (Resonator)

许多声学仪器包含一个主体或声腔，它们会“共振”——即以感应方式振动或增强——一个或多个频率。为了在模块合成器中模拟这种现象，你可以获得特殊的滤波器或均衡模块，它可以在三个或用户定义的频率（通常在窄频内）上增强声音。这是合成真实世界声音或空间的秘密之一。

## 回响 (Reverb / Reverberation)

1) "Reverberation" 的缩写。（参见 "Reverberation."）
2) 一种为信号创建人工回响的信号处理器或插件。

## 回响时间 (Reverb Time, RT)

声源直接声音后，回响或回声消失所需的时间。具体来说，回响时间是在声源停止的点与回响下降 `60 dB` 的点之间测量的。

## 回响 (Reverb)

Reverb 的缩写。这是一种模拟房间的效果设备，在房间里你可以听到原始声音多次从墙壁反射，在声音的洪流中弹跳，直到衰减为静音。回响可以极大增强合成器的声音，为原本可能单调的声音增加响亮度和维度。实现回响效果的模块相对较少，允许对其参数进行电压控制的更少（ErbeVerb 是最著名的）；直接使用外部回响效果即可。

## 回响场 (Reverant Field)

描述距离声源足够远，以至于回响比直接声音更大的空间。

## 回声室 (Reverberation Chamber)

一种用于模拟房间反射的设备。

## 回声包络 (Reverberation Envelope)

回响音量的攻击、衰减、维持和释放；或者回响达到峰值水平的速度及其衰减率。

## 回声 (Reverberation)

声源停止发射后声音的持续性，由于许多离散的回声到达耳朵的时间间隔非常紧密，以至于耳朵无法区分它们。

## RF 接口 (RF Interface)

由于 RF 信号的存在而引入电子设备、电路和音频系统的意外噪声。系统中的 RF 干扰可能导致嗡嗡声、滋滋、静电甚至播放广播传输。

## RF 信号 (RF Signals)

RF 信号（或 RF）——Radio Frequency Signals 的缩写，携带无线电频率的电磁波。

## 节奏部 (Rhythm Section)

乐队中的乐器，通常包括鼓和贝斯。

## 丝带控制器 (Ribbon Controller)

插入监听系统中的均衡器，试图补偿由房间声学引起的频率响应。

## 铝带麦克风 (Ribbon Microphone)

一种通过薄导电丝带将声波转换为电电流的麦克风。

## 乐句 (Riff)

一段重复播放的短旋律。

## 环形调制器 (Ring Modulator)

一种幅度调制，其中信号是双极性的（在 `0 伏` 上下波动），类似于一个开关。

## 房间调试 (Ringing Out a Room)

通过向扬声器发送粉噪声，识别并补偿房间内的问题频率的过程。

## 上升时间 (Rise Time)

音频波形突然增加的速率。

## RMS 表计 (RMS Meter)

一种识别并响应有效平均值、RMS 水平或交流波形有效值的仪表，而不是仅仅测量峰值。

## 滚降 (Roll Off)

信号电随频率离开截止频率而减少，特别是当截止率较缓时。

## 房间均衡 (Room Equalization)

在现场音频中，用于补偿房间声学引起的频率变化的均衡器。

## 房间声音 (Room Sound)

房间的自然氛围，包括回响和背景噪声。

## 环境音 (Room Tone)

房间在没有音乐或说话时发生的自然背景噪声。在为电影和电视录制音频时，现场录音师会捕捉一段环境音，以便在后期制作的剪辑之间提供连续性。

## 均方根 (Root Mean Square, RMS)

交流波形的有效值。用作声音整体电平的衡量，而不是仅仅通过峰值测量。

## 旋转头 (Rotating Head)

带有两个（或更多）头的圆形头，相对于磁带运动的方向以微小角度旋转。

## 低频干扰 (Rumble)

一种低频噪声，通常由地面/地板振动或录带机/播放单元驱动机构的不平表面引起。

## 节奏轨道 (Rhythm Tracks)

音乐制作中节奏乐器的录音。

## S-触发 (S-trig)

某些系统——例如原始的 Moog 模块——使用 s-触发（开关或短路触发）而不是普通的门控（后者短路到 `0 伏` 地）。在没有某种形式转换的情况下，你无法连接这两个系统。

## S/H (Sample and Hold)

采样并保持（S/H）模块有两个输入：一个正在被采样的信号和一个触发信号。

## 附录 B：音频工程术语 (0 - 9 - A - Z)

### 采样保持 (Sample & Hold)

表示何时对第一个输入进行采样。当接收到触发信号时，第一个输入的当前电压会被采样（测量）并保持（存储），然后输出输出。这个稳定的电压将一直保持，直到接收到新的触发信号。采样保持电路通常用于创建阶梯随机电压。要实现这一点，将噪声输入主输入；每当接收到触发信号时，输入的电压都是某个随机值，然后被忠实地发送到输出。

### S/PDIF

“Sony/Phillips Digital Interface”（索尼数字数字接口）的缩写，是一种使用常用 RCA 连接器发送和接收数字音频信号的协议。

### 安全备份 (Safety Take, ST)

在录制了质量合格的轨道后，为了保险起见而额外录制的音频。

### Sallen-Key (选频滤波器)

Sallen-Key 滤波器拓扑结构或设计创建一个“二阶”或双极低通、高通或带通滤波器，并具有高共振或高 Q 值。这种设计用于 KRS-20 滤波器及其克隆版本等。

### 采样保持 (Sample & Hold)

采样保持（S/H）模块有两个输入：一个正在被采样的信号，一个指示何时对第一个输入进行采样的触发输入。当接收到触发信号时，第一个输入的当前电压会被采样（测量）并保持（存储），然后输出。这个稳定的电压将一直保持，直到接收到新的触发信号。采样保持电路通常用于创建阶梯随机电压。要实现这一点，将噪声输入主输入；每当该输入的电压是某个随机值时，然后被忠实地发送到输出。

### 采样数据传输标准 (SDS)

采样数据传输标准 (SDS) – “MIDI 采样传输标准”。

### 采样率转换 (Sample Rate Conversion)

将在一个采样率录制的数字音频转换为另一种采样率，而不将信号转换为模拟信号。

### 采样率 (Sample Rate)

这是数字音频的一个规范：重建声音的单个测量值（采样）是如何记录或播放的。音频文件的带宽（对应于可以复制的最高频率）在实际上比采样率的一半少一点。在数字录音中，每秒采样的次数。采样率越高，声音的数字复制就越真实，可以复制的高频率也越高。在数字音频中，数字复制声音的质量和分辨率描述为采样率和比特率的结合。（参见“比特率”。）

### 采样 (Sample)

- 1) 在数字录音中，在给定时间时刻波形的数值测量值。模拟音乐通过许多连续的采样以数字形式表示。
- 2) 为了以数字方式复制和处理声音而录制的简短音频段。

### 采样器 (Sampler)

一种用于记录和播放采样的设备，通常具有编辑、处理和存储采样的功能。

### 饱和 (Saturation)

一种简单的电平概念，饱和是“削波”（clipping）的华丽说法：一旦输入电压高于（或低于）电路能够处理的范围，它将保持保持在那个限制上。然而，饱和通常意味着一种更圆润、更具形状的削波限制方法，从而产生更悦耳（至少是不那么烦人）的失真形式。电子管通常与这种软裁剪行为有关，尽管可以在其他电路或数字信号处理中进行模拟。人们可能会为了特定的音色而寻找不同的设备。

- 1) 磁带因音量过大而达到完全磁化的点。这产生了一些失真，音频发烧友描述为“模拟温暖感”，在某些情况下是一种理想的品质。
- 2) 通过通过电子管放大器或前置器过度驱动信号产生的失真——为声音增加了色彩和温暖，工程师通常认为这很有吸引力。
- 3) 模拟电子管或饱和的数字插件。

### 锯齿波 (Sawtooth Wave)

每个周期从零值跳变到峰值，然后立即掉回零值的波形。（有时被称为“斜坡波”。）

### 锯齿波 (Sawtooth)

合成器产生的最常见的波形之一。这种斜坡波包含偶次和奇次谐波，在基频（正在播放的音符）处最强，在高频处减小。结果是是非常响亮的、“带铜质感”的声音。

### 密特触发器 (Schmitt Trigger)

这是一种门检测器，观察变化的输入信号并输出“高电”（通常为 `0`、`10` 甚至 `15 伏`）或“低”信号（通常为 `0 伏`）。当输入高于一个阈值——例如 `4 伏`——时，输出变为高。当输入回到第二个不同的阈值——例如 `1 伏`——以下时，输出变回低。

### 示波器 (scope)

这是一种以图形波形显示波动的设备。示波器可以在宽的频率范围内运行，显示缓慢变化的电压（如 LFO 或振荡器）或快速变化的电压（如振荡器和噪声）。示波器曾是笨笨的外部设备，但现在你可以使用 USB 示波器将显示部分的工作交给电脑，或将示波器作为模块。

### 拨胶 (Scratch)

- 1) 一种描述性词，意思是“临时的”。
- 2) 粗带人声（scratch vocal）是在基础录音期间期间完成的人声，用于帮助音乐家熟悉自己的部分。稍后会录制最终的人声轨道。
- 3) 音乐家或 DJ 在转盘上快速前后唱片的动作，通过复制唱头的运动来创建声音节奏模式。

### 扫描 / 倒带搜索 (Scrubbing)

在监控的同时反复移动一段录制音频的操作或功能，通常用于定位录音中的某一点。在早期，扫描是通过手动转动卷带轴完成的。今天，扫描主要在 DAW 上通过拖动光标来实现。

### 二副工程师 (Second Engineer)

助理录音工程师。

### SEM

Oberheim SEM（合成器扩展模块）是他们最早的产品之一。它是一个早期合成器——两个振荡器、两个简单的包络、VCA 以及一个非常流行的变量滤波器，其旋钮可以在低通和高通输出之间切换一个带通设置——位于立方体外壳。通常当模块制造商使用魔法字母“SEM”时，他们指的是模拟原始合成器的滤波器。

### 半模块化 (Semi-modular)

半模块合成器的组件——振荡器、滤波器和放大器——在前面板后面以制造商认为的典型、逻辑的方式预接。然而，它们还提供了连接点，以便将其某些功能（例如振荡器的单个波形输出）发送到其他模块，或覆盖预接。许多接触模块合成的新学者通过获取一个半模块合成器来尝试，然后使用额外的模块对其进行扩展。

### 半音 (Semitone)

也称为半度或半音，这是大多数西方音乐中最小的音划分——例如 C 和 C# 之间的差异。在平均律（西方音阶常用的调音方式）中，这种音划分是八度的 `1/12`。

### 发送电平 (Send Level)

决定发送到总线的信号电平。

### 灵敏度 (Sensitivity)

- 1) 在音频设置中，麦克风在标准声音水平下产生的输出量，与其他麦克风在相同水平下的输出对比。
- 2) 在音乐中，描述一般的艺术人格。

### 序列 (Sequence)

- 1) 一组预编程的音乐事件，例如音高、采样播放和休符，由设备按顺序播放。也指编程设备播放这组音乐事件的操作。
- 2) 泛指广义意义上的音乐片段。

### 序列器 (Sequencer)

## 附录 B：音频工程术语 (0 - 9 - A - Z)

你在模块化合成器中最常见的类型序列器包含一排旋钮（也称为步骤或阶段），每个旋钮都可以设置为输出不同的电压。然后序列器会一个接一个地处理这些旋钮。这通常用于创建重复的音乐线条，其中每个音符的持续时间相同，这在迷幻类音乐以及经典的柏林学派（70年代的 Tangerine 和 Klaus Schulze；以及现在的 Red Shift 和 Node）中非常流行。可以被编程按阶梯式顺序播放音乐事件计算机设备或软件，包括音高的播放、采样滤波和休止。

### 顺序开关器 (Sequential Switch)

这种模块有几种不同的形式；在大多数情况下，几个输入路由到一个输出（尽管通常是对称的——一个输入可以在输出之间进行切换）。然后脉冲或门控输入会逐个切换输入，决定哪一个被路由到输出。更复杂的开关器允许你设置阶段数量，划分输入时钟以便以比主时钟更慢的速度进行切换，或直接将一系列输入路由到相应的输出（通常还有一个求和输出）。

### 串行数据 (Serial Data)

数字流，单个位通过单个连接一个接一个传输（与“并行数据”相反，后者可以同时设置多个位）。录音室中的大多数数据连接传输串行数据——例如 USB、Firewire 和 MIDI。

### 串联连接 (Series Connection)

连接设备（特别是电路元件），使电信号从一个物体流向下一个、下一个，等等。

### 设置 (Set Up)

在录音室内对麦克风、仪器、连接和监控定位，以及控制台、DAW 等上的控制和电平，为录音做准备。

### 高架滤波器 (Shelf Filter)

均衡器中用于获得高架效果的门的名称。

### 高架 (Shelf)



# 均衡电路的频率响应

均衡电路的频率响应，其中频率的提升或衰减在频率响应图中形成一个架。高频高架控制影响设定频率及以上所有频率的信号电平；低频高架对设定频率及以下的所有信号执行同样的操作。

## 屏蔽 (Shield)

电缆内部导线或导线周围的外部导电包裹，目的是防止电缆接收外部电磁干扰。

## 屏蔽电缆 (Shielded Cable)

在内部导体或内部导体周围带有屏蔽层的电缆。

## 避震架 (Shock Mount)

麦克风支架上的弹性支架，用于减少可能影响支架的意外震动的影响（例如，脚步引起的地面震动）。

## 短路 (Short Circuit)

电路中两个（通常）不应连接的点之间的直接连接。

## 短延迟 (Short Delay)

20 毫秒以下的延迟时间。

## 最短路径 (Shortest Path)

录音中的一种技术，使信号在录音期间通过最少数量的活动（放大）设备。

## 打枪式麦克风 (Shotgun Microphone)

带有长线滤波器的麦克风，这种管可以在声上抵消从侧面到达的声音，使麦克风对某一方向的选择优于任何其他方向。这使得打枪麦具有紧凑的超心形拾音模式。打枪式麦克风常用于电影拍摄中的对话录制，通常带有支架固定在吊杆上。

## 齿音 (Sibilance)

集中在 7 kHz 附近的语音能量，由发音“s”、“sh”或“ch”音引起。

## 侧链 (Sidechain)

信号处理器的辅助输入，允许由外部源触发处理控制。侧链的一种常见用途是压缩器中，特别是在凹陷效果中，特定音频信号的存在触发另一个音频信号的压缩。（另参见“闪避” [Ducking]）

## 信号流 (Signal Flow)

1. 广义上，音频信号从声源到系统输出的传输路径。（例如，从歌手的声进入麦克风，通过电缆、前放大器，从前放大器输出到控制台，通过所有插入点和总线，输出到 DAW 进行录音。）
2. 信号流通常特指音频信号通过控制台从输入到输出的路由情况。

## 信号处理 (Signal Processing)

通过各种设备或插件（如均衡器、压缩器、混响单元等）改变音频信号特征或声音的实践。

## 信噪比 (SNR)

信号电平强度与设备发射噪声数量的比较，以 dB 表示。

## 信号 (Signal)

1. 在音频中，与声压波匹配或最初从声压波获得的交流电（或电压）。
2. 在音频中，20 Hz 到 20,000 Hz 之间的交流电（或电压）。
3. 数字音频位比特流。

## 正弦波 (Sine Wave)

正弦波是完美的波形：它只包含基波，没有高阶谐波。结果，它是创建作为底鼓或其他鼓音色的低音波的极佳波形；在探索诸如频率调制 (FM)、幅度调制 (AM) 或增加或移动谐波内容的波形等技术时，它也是一个极佳的源波。

## 正弦 (Sine)

这是完美的波形：它只包含基波，没有高阶谐波。结果，它是创建作为底鼓或其他鼓音色的低音波的极佳波形；在探索诸如频率调制 (FM)、幅度调制 (AM) 或增加或移动谐波内容的波形等技术时，它也是一个极佳的源波。

## 拍击式回声 (Slap Echo) (也称为 拍后回声 [Slapback])

声音的单一、清晰的回声，可以自然地由高频从非吸收墙壁反射产生，也可以由信号处理单元或插件人工产生。拍击式回声创造了一种类似于你在竞技场内听到的“活”音效。

## 场板 (Slate)

1. 场板（Slating）——在视频中，在片段开头识别场景，以便进行视频编辑。这是通过在分镜脚本上以书面形式在镜头前展示场景/场次，口头标记场景/场次，然后用场板标记，以便将音频与视频同步。
2. 在音频录制中，类似的做法是在录制轨目的开始处通过听觉提示来识别素材带（take）。虽然一些工程师仍坚持这样做，但在模拟磁带录制时代这是非常有必要的，因为它能帮助编辑人员跟踪录音机上素材带的位置。今天，DAW 通过在屏幕上视觉化识别每个素材带使得跟踪变得更容易。

## 从设备 (Slave)

1. 在音频中，任何通过读取由主设备发射的时钟信息来与另一个设备同步的设备。
2. 在 MIDI 中，任何通过读取主设备发射的时钟信息来与另一个设备同步的设备。

## 速率限制器 (Slew Limiter)

此功能平滑输入信号，使变化不会超过某个数值。

## 滑动轨道 (Sliding Rails)

这是用于安装模块的常用系统。在 Eurorack 中，这些导轨可以滑动以适应任何位置。

## 斜率发生器 (Slope Generator)

斜率发生器产生上升或下降的电压。它本质上是一个门控发生器或速率限制器（见上文）。

## 斜率 (Slope)

大多数滤波器都有截止频率或角频率。它随后减少（滤波）进入信号的频谱，使得谐波越远离截止频率越安静。这种效果的强度被称为其斜率。例如，斜率为 24 dB/oct 的低通滤波器 (LPF) 会使其截止频率上方的一个倍频衰减 24 dB。

## 智能 FSK (Smart FSK) (频率移频)

同步的更新形式，使 MIDI 设备能够同步磁带录音机。数字歌曲位置指针 (SPP) 数据编码到空闲轨道中，识别 MIDI 序列器/设备的精确小节、小节和拍。这使得设备无论从磁带的何处开始都能在准确的位置启动。（另参见“频率移频” [Frequency-Shift Key]）

## SMPTE 码

SMPTE 一种由电影和电视工程师学会创建的标准计时信号协议，用于将音频与视频/电影同步，也可用于音频录制环境中的同步。许多音频专业人士简单将这种代码称为“SMPTE”。

## SMPTE

1. 电影和电视工程师学会的缩写。
2. 参见“SMPTE 码”。

## 小鼓 (Snare)

1. “军鼓”的缩写。
2. 跨越在军鼓底皮上的金属丝，有助于在击打军鼓时产生尖锐的爆裂声。

## 脚镲 (Sock Cymbal)

踩镲（hi-hat）的罕用术语，源自踩镲被放在“脚高度”的时代。（另参见“镲” [Hi-Hat]）

## 软膝 (Soft Knee)

在压缩中，指当声音电平超过阈值时，逐渐引入对信号的压缩。（另参见“膝度” [Knee]）

## 软件乐器 (Virtual Instrument)

基于软件的合成器、采样器或声音采样之一，通过计算机存储和访问并由任何外部 MIDI 控制器执行，而不是在独立的合成器或模块中。由于这些乐器提供的广泛功能性，许多作曲家和电子音乐人正在使用存储在硬盘中的虚拟乐器，而不是购买一堆键盘和模块。

## 焊接 (Soldering)

使用锡进行连接动作。锡是一种软金属合金，通过熔化来键合两个金属表面。在音频设置中，焊接用于构建、修改或修复设备等各种目的——最常见的是为了成本而维修或制作音频电缆，而不是购买新电缆或将其送去维修。

## 固态 (Solid State)

在电子学中，指在制造电子设备中使用晶体管和半导体（固体材料），而不是电子管。在录音室中，固态放大器的特性与电子管放大器不同，且两者各有优缺点。固态结构较新的应用是在于计算机设备，特别是固态硬盘 (SSD)，它们传输数据的速度比传统的机械旋转硬盘更快，且更不易损坏。

## 独奏开关 (Solo Switch)

在调音台或 DAW（数字音频工作站）上激活独奏功能的开关。

1. 调音台或 DAW 中的电路，允许一个或多个通道被听到或到达输出端，而其他通道自动静音。
2. 在音乐中，歌曲中的某段，其中歌手或乐器在其他乐器背景上突出。

## 声位指针 (Sound Position Pointer - SPP)

一种 MIDI 消息，允许 MIDI 设备定位歌曲中的给定点。与 MIDI 时钟配合使用，作为同步设备或告诉连接设备何时开始播放的方法。

## 声学毯 (Sound Blanket)

可以将厚毯子铺在地上或挂起来，以增加房间的吸声，并防止声反射。

## 音效 (SFX)

除对白、旁白或音乐外，添加到音频中的内容，通常出现在电影/视频背景中。

## 音频 (Sound File)

可以存储在计算机或数字存储介质（如硬盘）上的数字音频录制。

## 建模 (Sound Modeling)

一种在不直接模拟物理设备的情况下重建声音的技术。例如加法合成，它使用正弦波和噪声的组合来重建声音。

## 音模块 (Sound Module)

一种电子乐器（音色发生器、合成器或采样播放单元），它没有可演奏接口，而是对传入的 MIDI 消息做出响应。音模块通常被创建为流行合成器的“大脑”，即该产品的更廉价版本，可以添加到现有的 MIDI 配置中。今天，音模块也可以以软件版本或插件的形式在计算机上访问。

## 声压 (Sound Pressure Level - SPL)

在科学/技术术语中，声波引起的气压变化的测量，单位为分贝 (dB)。我们通过声音的幅度、音量或响度听到并感知 SPL。

## 声源 (Sound Source)

声音的起源，其振动产生声波。

## 声波 (Sound Wave)

（也称为压力波）振动引起的波，导致气压的微小变化，我们听到的声音。

## 声带 (Soundtrack)

1. 广义而言，指随视觉媒体的任何/所有音频，无论是音乐、对白还是音效。
2. 在更通俗的语中，指与电影、视频、电视节目或视频游戏同步的配乐和/授权音乐。

## 不确定性源 (Source of Uncertainty)

这是 Buchla 265 和 266 模块的，用于产生随机控制电压。它的名称常用于遵循或受原始 Buchla 模板启发的随机源模块。

## 间距 (Spaced Pair)

（也称为“A/B 技术”）一种立体声麦克风放置技术，将两个心型形或全指向形麦克风之间隔开 3-10 英尺（取决于声源的大小），以创建左/右立体声场。

## 扬声器 (Speaker)

一种将电信号转换为声音的设备；更技术地说，换能器将电学音频信号转换为压力波。

## 声速 (Speed of Sound)

通常来说，声波穿过介质所需的时间。声音在固体、液体和气体中的传播速度不同，我们认为声音在空气中传播，但温度、气压和湿度的差异也会影响声音的传播方式。作为一个起始参考基准，声速通常由航空航天工程师定义为“1 马赫”，相当于每秒 340 米（约每秒 1116 英尺）。相比之下，在 20 摄氏度的海平面，声速约为 344 米/秒，或 70 华氏度。

## 剪辑 (Splicing)

历史上，在精确位置连接之前切断的胶带或胶片的动作。今天，剪辑已通过 DAW 或软件数字地缩短音频或视频段变成一个非常简单的过程。

## 分路器 (Splitter)

定义是能够将信号分成两个或多个拷贝的东西，例如两个输出端连接到输入的分路器线。要进行深入讨论，请参见“扩散 (Spread)”条目。

## 扩散 (Spread)

某些模块可以同时产生多个音色。将这些音色之间略微调调或“扩散”，通常会创造出悦听的合唱效果。

## 弹簧混响 (Spring Reverb)

一种通过将金属弹簧连接到换能器并在其中发送音频产生振动来模拟混响的设备。虽然物理混响仍然存在，但大多数使用插件或硬件单元来模拟混响。

## 方波 (Square wave)

这是由合成器振荡器产生的常见波形，它在高电压和低电压之间切换（通常为 +/-5 伏或正电压）。除了形状简单外（特别是与锯波（斜坡波）相比，后者的电压瞬间上升到一个水平，在该水平保持一段时间，最后上升到另一个水平）。

## 堆叠电缆 (Stackable Cable)

许多香蕉头电缆的设计允许你直接插入另一个。Tip 制造了使用 3.5mm 插头的类似电缆，供 Eurack 用户使用。

## 舞台监听器 (Stage Monitor)

舞台上的扬声器，让表演者听到自己以及其他音乐人的声音。

## 舞台 (Stage)

1. 现场音乐表演的封闭或抬高的区域。
2. 在混响效果中，在混响之前添加的回声，以模拟回声。在最广泛的术语中，stage 是电压的变化。在 8 步序列器中，例如，每个音符都是一个 stage。在包络发生器中，如 ADSR（攻击 Attack/衰减 Decay/持续 Sustain/释放 Release）中，每个阶段——如包络发生器从 0 伏上升到最高电压——都是 stage。

## 标准工作水平 (Standard Operating Level)

正常操作中不应超过的参考电压水平或平均水平。

## 驻波 (Standing Wave)

当声波在房间内两个平行表面之间反射时，会产生不需要的波形，反射波与来自源的波干扰，受影响频率的长实际上是房间的长度。这产生了听上的错觉，即波在房间的某些部分被放大到不必要的水平，而在其他部分几乎不存在。这种波在正方形或矩形房间中最为常见，声设计师通过安装吸收材料或引入其他物品来防止这些波。

## 步模式 (Step Mode)

序列器或 DAW 中的一种设置，其中手动输入一个音符或一个步骤。

## 步序列器 (Step Sequencer)

这通常指一种序列器，你走到并停在某个 stage，输入音符（以及可能的时长），移动到下一步，依此类推。

## 步骤 (Step)

Step 通常与 stage（见上文）通用，特别是在讨论序列器时。

## 立体声场 (Stereo Image)

对立体声的感知，其中不同的声源似乎来自左侧、右侧或之间的任何地方。

## 立体声收音 (Stereo Micing)

放置两个或多个麦克风，使它们的输出组合成立体声场。

## 立体声 (Stereo)

至少两个通道的录制或再现，可以感知乐器声音的左右定位。

## 击打 (Strike)

这个术语出现在几个 Make Noise 模块中，尽管它已渗透进通用术语。某些滤波器、放大器和低通门（LPGs）使用或模拟 vactrol（放置在 LED 等光源旁的光敏电阻，允许将电压转换为电阻以控制参数），它们可能会有 strike 输入。当你用 LED 闪烁光敏电阻时，它不会瞬间改变电阻并保持在该状态——相反，在滑向到目标电阻值时存在延迟。当你关闭 LED 时，电阻可能不会瞬间恢复到最大；相反，它可能需要短时间来衰减。这些特性对于创建打击乐声音和起始音（attacks）非常有用。触发输入（strike input）的目的是通过一个极短的脉冲，或者在 LED 开启的情况下允许你重新触发（re-attack）。

## 子代码 (Subcode)

与数字音频一同记录的额外信息位，用于控制和播放目的。

## 子帧 (Subframe)

SMPTE 码中比一帧更小的单位。

## 子组 (Subgroup)

控制台上的若干输入通道，在将组合信号发送到主输出之前，可以作为一个整体进行控制和调整。有时也称为“子混”（Submix）、“总线”（Bus）或简单的“组”（Group）。

## 次泛波 (Subharmonic)

一种通过划分输入声音的基础谐波来产生更低频率（即次泛波）的电路。最常见的是八度分频器或次低音电路，它通过将基础频率除以 2 来产生次泛波（有些也可以通过除以 4 产生基础频率低两个八度的次泛波）。

## 子主母 / 副主母 (Submaster / Sub-Master)

推子控制混音和录音期间多个通道声音的组合电平。

## 子混 (Submix)

子混 – 参见“子组”。

## 次八度 (Suboctave)

一种能够产生比其输入声音的基础谐波（即“音高”）低一或两个八度的新音调的模块，用于增强低音。（泛泛在本词汇表的其他部分有详细讨论。）这种音调通常是方波，尽管一些巧妙的模块可能会产生更像正弦波或更接近原始波形的声音。

## 减法合成 (Subtractive Synthesis)

最常用的合成技术：你从一个或多个输出具有大量谐波波形的振荡器开始，然后将其通过滤波器，通过滤波器移除一些谐波来创建所需声音或音色。然后将这种修改后的音调发送到放大器，通过改变其响度为音符增加清晰度。

一种老派的声音合成方法，通过产生谐波丰富的波形来设计和创建声音，然后过滤掉不需要的谐波以获得所需的声音。

## 和 (Sum)

“求和”是表示你将两个（或多个）东西加在一起的雅说法；总和就是结果。通常用于控制电压的语境，尽管也可以用于音频甚至谐波的混合。相反的是“差值”（difference），即从一个输入中减去另一个。由两个声道以等量电平和同相位混合的信号。

## 混总 (Summing)

将两个或多个信号融合成一个混合信号的过程。在音频混总中，每个连续通道都会为整体信号增加量，因此必须按顺序混合以防止组合信号出现峰值。

## 超心形指向性 (Super-Cardioid Pattern)

一种紧凑的心形麦克风指向性，轴线敏感度最高，在离轴约 150 度处敏感度最低。

## 环绕声 (Surround Sound)

一种录制和播放技术，听者可以从前到后、从左到右听到声音的各个方面——一个 360 度的音频图像，相对于立体声的左右图像。环绕声可以多种格式出现，房间内布置了不同数量的扬声器。如今环绕声主要用于电影和电视制作。

## 持续 (Sustain)

这是包络发生的一个常见阶段，其中电压（通常发送到滤波截止频率或放大器电平）在音符仍按住时保持稳定电平。音符是否被按住的信息通常由门信号（gate signal）提供，只要按住键它就会保持高电平，尽管某些包络器可能有专门的时间控制来规定持续阶段应该持续多久。包含持续阶段的包络包括 ADSR（攻击/衰减/持续/释放）和 AR（攻击/释放，通常假设有一个持续阶段）。

## 可变滤波器 (SVF)

可变滤波器 (SVF) 是合成器滤波器的常用设计。这种设计允许低通、高通和带通滤波器同时可用。另一个副作用是它们不容易在高反馈（共振）设置下产生振荡，尽管已经有人研究出如何实现这一点。奥伯海姆 SEM（合成器扩展模块）滤波器可能是最著名的状态变量设计。

## 润色 (Sweetening)

一个模糊的术语，指录音后期阶段对音频的微调。实际上，任何让音频听起来更好的细微“调整”都被视为润色。

## 开关触发 (Switch Trigger)



系统——如原始的 Moog 模块——使用 s-触发（开关或切换触发）而不是普通的门信号（gate），门信号是一根短路到 0 伏地的导线，就像连接到地的开关关闭一样。如果没有某种形式的转换（可以是特殊的电缆），你无法连接这两个系统。

# 开关 (Switch)

一种制造和/或中断电气连接的设备。

# 可切换指向性麦克风 (Switchable Pattern Microphone)

具有两个或多个拾音模式的麦克风可以通过麦克风上的开关进行切换。

# 开关电源 (Switching Power Supply)

开关电源直接将输入的高电压交流信号转换为高电压直流信号。然后通过快速切换输出的开启和关闭来获得较低的输出电压。这种开关电压经过平滑处理以产生恒定的直流信号。开关电源通常更轻、更凉且更便宜，但代价是通常会有噪声——许多电源正转向混合电源，将开关器与线性稳压器相结合以兼两者之长。

# 同步声 (Sync Pop)

一个短音（使用 1 kHz 的正弦波，长度为一帧），精确地放置在电影开始之前。同步声用于确保所有相关的音频和视频轨道保持同步。这包括将视频/播放设备连接到类似 SMPTE 码的同步信号。

# 同步24 (Sync24)

Sync24 是罗兰创建的 DIN Sync 的另一种名称，它以每四分符 24 个脉冲的速度发送信号。Korg 设备使用了这种变体，每四分符 48 个脉冲，称为 Sync48。

# 同步 (Sync)

Sync 有两种含义，取决于我们讨论的是振荡器还是时钟信号。某些振荡器使用一种模式，在接收到另一个振荡器的信号时将其波形触发到起始。如果两个振荡器之间没有精确的八度关系，结果是过早重置的修改波形。通过调制从属振荡器的频率，可以创建非常酷的“撕裂”声音；使用简单的包络即可。在计时语境下，当你同步序列器或鼓点模式时，通常会在所有相关模块周围使用主计时或同步信号。这通常是一个门信号或触发信号。“同步”的缩写。在音频/录音室环境中，同步是指两个或多个音频或视频片段之间的关联。这包括将视频/播放设备连接到类似 SMPTE 码的同步信号，在电影或电视中同步音视频，以及许多其他示例。为电视或视频投放许可歌曲或音乐片段也被称为“同步”。

# 合成器扩展模块 (Synthesizer Expander Module)

奥伯海姆 SEM（合成器扩展模块）是他们最早的产品之一。它是一个完整的合成器单元——两个振荡器、两个简单的包络、VCA 以及非常流行的双极状态变量滤波器设计，旋钮可以在低通、陷波和高通输出之间进行交叉淡化，并带有独立的带通设置——如今大多数当模块化制造商使用魔术字母“SEM”时，他们指的是旨在模仿原始奥伯海姆合成器的滤波器。

## 附录 B：音频工程术语 (0 - 9 - A - Z)

### 合成器 (Synthesizer)

一种利用电子振荡器人工产生音乐器，用于模拟其他乐器的声音或创造其他乐器无法产生的声音。

### 系统专用 (System Exclusive)

专用 (SysEx) – 一仅会被特定制造商设备识别的 MIDI 消息。

### 转速计 (Tach/Tachometer)

在模拟磁带录音中，录音机上的一个设备，通过在带经过磁头时发射脉冲来测量和调节带速。

### 外带法 (Tails Out)

一种卷绕音频带的方法，使最后录制的片段位于卷轴的外侧。

### 带次标记 (Take Notation)

在磁带纸或轨道日志上记录录制的曲目带次并附带注释。模拟磁带录音建议使用带次标记，但在大多数工作室中，此功能现在通过 DAW（数字音频工作站）完成。

### 带次 (Take)

在磁带录音机或 DAW 的一次开始到停止之间录制的内容。

### 话盒 (Talk Box)

一种效果器，允许音乐人通过放入嘴里的软管来调制其乐器的声音。从历史上看，话盒一直被用作吉他的效果，也可以用于修改其他乐器。

### 话回 (Talkback)

控制室内的麦克风，与录制通道采用独立电路，允许工程师通过监控系统与活动室或隔音间内的音乐人进行交流。

### 磁带延迟 (Tape Delay)

一种用于创建人工延迟或通过模拟磁带机操控时间延迟的信号处理技术。这种技术最初通过将磁带路由到另一台独立的录音机并将延迟响应混合回系统来实现；随后演变为使用专用设备，通过调整录音头和播放头之间的距离来调整延迟长度。今天，工作室中的大多数磁带延迟效果都是通过 DAW 中的插件进行数字模拟的。

### 导带器 (Tape Guide)

任何固定或旋转的设备，引导磁带通过带机的磁头或从一个卷轴移动到另一个卷轴。

### 磁带底噪 (Tape Hiss)

### 磁带环 (Tape Loop)

一段末端拼接在一起的磁带，录音将持续播放。

### 磁带录音均衡 (Tape Recording Equalization)

在磁带机的电子设备中，在录制时增加高频信号的幅度，以保持高频信号高于磁带底噪。

### 电话滤波器 (Telephone Filter)

一种过滤器，通过移除 300 Hz 以下和 350 Hz 以上的信号，模拟通过电话听筒器听到的音频。

### 速度映射 (Tempo Mapping)

对序列器或 DAW 进行编程以遵循录制表演的速度变化的行为。与节拍映射（beat mapping）或节拍匹配（beatmatching）不同（两者都是有效地调整录音以适应固定速度），速度映射是调整项目的速度（特别是是 MIDI 乐器）以匹配录制材料的自然细微差别。（参见“节拍映射”、“节拍匹配”。）

### 速度 (Tempo)

音乐移动率，以每分钟拍数 (BPM) 测量。

### 终端 (Terminal)

- 1) 两线之间的连接点，包括电缆末端的插头和设备上的接口。
- 2) 指电脑的键盘和显示器，使用户能够输入信息并访问数据。

### 测试振荡器 (Test Oscillator)

一种为了测试目的而产生各种频率音频波形的设备。

### 测试压片 (Test Pressing)

由第一个压制模制作的少数初始乙胶唱片拷贝之一，在压制更多拷贝之前，对其进行听音和目视检查以批准质量。

### 测试音 (Test Tones)

- 1) 在磁带卷开头以磁参考电平录制的几个单频音调，用于录制节目。
- 2) 用于校准音频系统的人工产生音调。

### 单薄声 (Thin Sound)

一个描述音频信号缺乏某些频率（尤其是低端）的模糊术语。例如，用均衡器（EQ）过度滤波信号可能会产生单薄的声音。

### 螺纹插入件 (Threaded Inserts)

一种将模块安装到机箱中的常用系统称为滑轨或螺母。许多此类螺母被插入这些槽中，然后可以滑动到任何位置，以适应您的模块的安装孔间距。有些人不喜欢这种系统，他们用插入槽的金属条代替螺母，这些金属条已针对标准的 Eurorack 安装孔间距进行了预钻。它们可能是为 2.5 或 3 mm 的螺丝预钻的；在购买带有预安装滑轨或机箱时请留意。

### 三比一规则 (Three-To-One Rule)

一种麦克风放置原则，即当同时使用多个麦克风时，麦克风之间的距离至少应该是每个麦克风与其声源之间距离的三倍。三比一规则用于防止音频信号之间的相位问题。

### 三音音箱 (Three-Way Speaker)

一种具有独立扬声器来重现低音、中频和高频的音箱系统。

### 听阈 (Threshold of Hearing)

### 阈值 (Threshold)

描述为人们在 50% 的时间内能到的声压级。

阈值通常是指模块采取动作之前信号需要越过的电压电平。例如，当包络跟随器（产生与音频信号当前水平相应的电压的模块）的输出高于阈值时，其门限（gate）将变为高，表示音符已开始。当包络跟随器的输出在阈值之前（该阈值可能与音符开启阈值相同也不同）下降时，门限变为低，表示音符应结束。

动态[处理器]运行的电平。

### 喉口 (Throat)

声音通过的喇叭或扬声器的开口处。

### 穿零调制 (Through-Zero Modulation)

TZFM 是穿零调制的缩写。它是调制的一种，频率由通过零点的信号进行调制。

### 投射 (Throw)

- 1) 在扬声器中，“throw”也可用于描述方向性。为较小空间设计的音箱具有“短投射”，而为远距离设计的具有“长投射”。
- 2) 在麦克风中，“throw”描述振膜的移动幅度。
- 3) 制作人在感到沮丧时可能会做的事情。

### 跨接线 (Tie Lines)

两端都有连接器的电缆，通常穿过墙壁或地板在房间之间传输信号。跨接线提供了一种半永久的路由方式。

### 音色 (Timbre)

这个词经常用于描述声音独特的色彩特征，独立于其音高或亮度。根据定义，不同的声音具有不同的音色。当你改变声音色彩特征的参数时（例如改变滤波器截止频率、脉宽等），你正在改变它的音色。音色在音符的生命周期内经常变化。

区分不同乐器的声音质量，即使它们演奏相同的音符。例如，小号的音色是使其听起来像小号而不是笛子的原因。音色主要取决于乐器演奏时泛波的存在、缺失和复杂性。

### 时间代码 (Time Code)

工作室使用的标准定时信号，帮助设备相互同步或将音频同步视频。工作室常用的时间代码是 MIDI 时间代码 (MTC) 和 SMPTE 时间代码。

### 时间压缩/扩张 (Time Compression / Expansion)

也称为“时间拉伸”或“时间偏移”。在不改变声音音高的加速或减慢音频记录的过程。

### 时间常数 (Time Constant)

描述应用于电路电压到电路做出响应之间时间延迟的概念。

### TiniJax

这是由 Switchcraft 设计的一种特殊种的接口，用于 Buchla（及其许多克隆产品）传输音频信号。它们的直径为 3.5mm，但在物理上与常见的 3.5 mm 接口略有不同。1/8 英寸插头插入 Tini-Jax 接口时会松动；Tini-Jax 插头可能无法插入或损坏 1/8 英寸接口。

### 通鼓 (Toms)

安装在底鼓上方架子上的小鼓鼓（直径最小为 10 英寸）以及鼓组中的大鼓。

### 信号发生发生器 (Tone Generator)

1) 一种产生各种频率测试音调的设备，用于校准磁带机或其他测试用途。
- 2) 合成器中产生输出音频信号的电路，通常用于模拟其他乐器的声音。

### 音色 (Tone)

- 1) 任何单频信号或声音。
- 2) 乐器声音相对于不同频率下含能量量的音质。

### 舌法 (Tonguing)

用舌头控制铜管或木管乐器音符起始的技巧。

### 总谐波失真 (THD)

衡量放大器输出级与输入级谐波频率电平差异的指标，以百分比表示。这是一个许多耳朵几乎无法察觉的精细调整规格，但 THD 越低，放大器/扬声器还原声音就越准确。

### 触控 (Touch Sensitive)

触控敏感——参见“速度敏感 (Velocity Sensitive)”。

### 跟踪保持 (Track & Hold)

这是采样保持（Sample & Hold）的一种变体。两者都有两个输入——一个门控信号和一个电压参考信号——以及一个电压输出。当采样保持接收到高电平门信号时，它会将输出电压冻在参考输入中。该电压将保持直到收到新的高电平门信号；低电平门信号会被忽略。在跟踪保持中，当门为高电平时，参考输入将传递到电压输出（这是“跟踪”阶段）；当门变为低电平时，该瞬间的输入电压被冻结并保持在电压输出，直到接收到新的高电平门信号。

### 轨道日志/轨道分配表 (Track Log / Track Assignment Sheet)

轨道日志/轨道分配表——随多轨道磁带一起保存的纸张，说明每个轨道录制的是哪种乐器。

### 轨道 (Track)

- 1) 多轨道磁带某部分宽度上的任何音频录制，或使用 DAW 创建的数字表示形式。
- 2) 序列器或 DAW 中的一组控制命令，用于通过 MIDI 通道控制某件乐器。
- 3) 参见“乐队轨道 (Band Track)”。

### 跟踪 (Tracking)

跟踪通常是指振荡器如何随从发送给它的音高控制电压 (CV)。随着电压上升，“振荡器”会跟踪它并产生更高的音高。（但并非所有如此！）有些系统遵循每八度 1 伏系统，其中音高输入上升 1.00 伏应正好产生振荡器音高的翻倍（升高一个八度）。这确实是发生的情况，振荡器具有良好的跟踪性。如果振荡器跑调，则被视为跟踪错误或跟踪性差。有时你会发现电压控制滤波器有一个 CV 输入的“跟踪”开关，此时滤波器截止频率的音高仅为对应音高输入变化的 1/3、1/2 或 2/3。这可以防止音符听起来太亮，同时又不让低音听起来太沉闷。有时你会发现电压控制滤波器有一个 CV 输入的“跟踪”开关，滤波器截止频率的音高上升为对应音高输入变化的 1/3、1/2 或 2/3。

录制多轨道中单个轨道的行为。

# 换能器 (Transducer)

将能量从一种介质转换为另一种的设备。换能器遍布录音室的所有设备。

# 瞬态 (Transient)

波形开始处的高能量峰值，例如拨片或锤子击弦产生的，或击鼓产生的。

# 晶体阶梯滤波器 (Transistor Ladder Filter)

这通常用于描述深受喜爱的 Moog 低通滤波的设计，该设计仍被许多人视为低通滤波器声音的黄金标准。Moog 实际上为这种设计获得了专利（其竞争对手中要么复制了它，要么尽力估算出它）。

# 传输控制 (Transport)

- 1) 磁带机中将磁带从供带卷移动、经过磁头并移动到卷带卷的部分。
- 2) DAW 或序列器上找到的一组控件，用于磁带机传输控制的启动、停止、快进和回退、编辑功能。

# 移调 (Transpose)

简单来说，移调一条音乐旋律的音高是指将其按固定数量的半音或八度向上或向下移动。这有时被称为“半音”移调。更复杂的变体是“音阶”移调，其中每个节点移动固定的数量的音阶步数；这些与半音移调不同，因为不同音阶步长之间的半音数量可能有所不同。

按固定音程移动一组音符。这可以通过多种方式实现——例如：

1) 用新调重写一首音乐；2) 通过改变乐器的调音，使其以比弹奏音符更低或更高的音程演奏（可以是任意的，如电子键盘，也可以通过经过移调乐器的自然调音，如小号）；或 3) 瞬时移调，在谱面音符上方或下方按固定音程演奏（也称为视唱移调）。

# 陷阱/吸收 (Trap)

- 1) 一种旨在拒绝某些频率音频信号的滤波器。
- 2) 用声学材料制成的物体，放置在墙内以减少房间内的低频反射（也称为“低音陷阱 bass trap”）。
- 3) 鼓组的另一种说法（如“trap set”）。

# 颤调 (Tremolo)

这是改变音符振幅（响度）的效果。在模块化合成器上创建这种效果的方法是将低频振荡器 (LFO) 连接到放大器其中一个控制输入上。颤调比颤音 (vibrato) 更纤薄；后者是音高的抖动而非响度的抖动。通过音符的快速重复或振幅的快速变化产生的效应。

# 三角波 (Triangle)

三角波是一种常见的合成器波形。当选择作为振荡器的输出时，它的声音比方波或锯齿波更柔，谐波更少更弱。它也是低频振荡器 (LFO) 的流行输出，因为它在其控制的内容上产生平滑的波动，同时能够产生正弦波。

# 三角波 (Triangular Wave)

一种谐波丰富的波形，图中呈三角形，由于奇谐波的存在和快速衰减。

# 触发 (Trigger)

触发是一个非常短的电脉冲信号，从 0 伏上升到标准水平（如 5 或 10 伏），几毫秒后回到零。它通常用于启动或“触发”打击乐。触发通常具有固定的持续时间，而门信号也从 0 伏上升到较高的电压然后回到零，但其保持“高”的时间取决于音符长度。

控制事件的信号或行为。

# 微调 (Trim / Trim Control)

放大器中减少或增加信号强度的设备，通常在一个限制范围内。通常与增益 (gain) 通用，但通常是指微调信号强度，而非放大它。

# 截断 (Truncation)

- 1) 音频信号、采样或歌曲的加密，通常通过切掉结尾。
- 2) 当位深降低时（例如从 24 位降至 16 位）丢弃数据位，在应用抖动 (dither) 时会导致数字失真。

# 定调 (Tune)

调整合成器振荡器（主音高产生元件）的音高以匹配另一个振荡器、乐器或参考标准被称为调音。

# 音叉 (Tuning Fork)

带有两个齿的金属叉子，击击时会产生一个频率相当纯净的音。

# 转盘机 (Turntable)

在播放期间支撑并旋转唱片片的设备。

# 高音单元 (Tweeter)

设计用于仅重低低的扬声器。

# 二限乘法器 (Two Quadrant Multiplier)

二限乘法器执行的是简单的幅度调制 (AM)，它通过第二个称为调制器的信号（通常是音频信号，在 0 伏上下波动）来改变称为载波的信号的幅度或响度。在典型的幅度调制 (AM)场景下，一个具有正电压的低频振荡器（例如 0v 到 5v 之间，或更小的 1v 和 2v）被馈入电压控制放大器的控制端，以为通过的音频信号添加颤音（vibrato）。调制信号中的任何负向波动都会被忽略；在连接颤音（tremolo）时，你可能需要确保为 LFO 添加了偏置电压，以防止声音在 LFO 波形的低端偏置处发生断音。（调制器同时具有负向和正向偏置的情况称为四限乘法器）。

# 双音扬声器 (Two-Way Speaker)

一种具有独立扬声器的扬声器系统，分别用于重现低频（低音单元）和高频（高音单元）。

# TZFM

TZFM 是“过零频率调制”（Through-Zero Frequency Modulation）的缩写。想象这样一个跳线：你将一个振荡器的输出（调制器）馈入第二个振荡器（载波）的频率控制输入。当调制器的波形输出高于零时，它会被加到载波正常的音调控制电压上，载波的音调随之上升。当调制器的波形输出低于零时，它从正常的音调控制电压中减去，音调随之下降。如果音调控制减去调制器的结果低于零伏，会怎样？在一个明确表示实现过零频率调制的振荡器中，载波将开始反向播放——本质上是一个负频率。这通常会产生更悦耳的声音，是振荡器的一种理想特性。

# U



# 机架式设备标准尺寸

机架式设备通常遵循一组标准尺寸，包括宽度 19 英寸（48.3 厘米），以及每个“机架单元”（或简称 U）高度 1.75 英寸（4.4 厘米）。许多模块化合成器使用机架单元格式来标准化模块高度——例如 Eurorack 的 3U（3 x 1.75 = 5.25 英寸）或 13.3 厘米，Buchla 和 Serge 的 4U，以及经典模块化 Moog 的 5U（有时被称为 Mu，即 Moog Unit）。

# 不平衡传输音频 (Unbalanced Audio)

大多数音频信号通过两根导线传输：一根代表音频振动的电压线，另一根是地线。这种布局通常被称为不平衡音频。

# 不平衡电缆 (Unbalanced Cable)

一种具有两个导体（一个信号线和一地线）且两端都有连接器的电缆。不平衡电缆往往受到电磁干扰和噪声的影响。不平衡电缆的示例包括吉他/乐器线（也称为 TS 线）和 RCA 线。

# 单向性音型 (Unidirectional Pattern)

一种麦克风拾音模式，对从一个方向到达的声音比其他任何方向都敏感。

# 单极 (Unipolar)

模块化合成器中的许多电压——包括音频振荡器的输出以及大多数低频振荡器——都在正电压和负电压之间波动。这被称为双极电压。某些电压——例如包络生成器的输出——仅在 0 伏和某些最大正电压之间变化；这被称为单极。

# 同音 (Unison)

多个表演者、乐器或声源同时以相同的音色发声。

# 单位增益 (Unity Gain)

放大器或设备的输出信号强度与输入信号强度相比没有增加或减少的情况（通常描述为 0 dB）。

# Unity (Unity)

# 真空管 (Vacuum Tube)

一种抽除了气体的玻璃管，电流可以通过其中流动。在音频领域，真空管被用于放大器、振荡器和其他模拟设备。

# 循环淡出 (Vamp and Fade)

一种结束歌曲的方法，音乐有一个重复部分，工程师逐渐降低音量直到音乐淡出。

# 循环 (Vamp)

歌曲或和弦进行重复的部分，通常位于歌曲结束，通常是副歌或副歌的一部分。

# 变速 (Vari-Speed)

磁带机上用于改变播放速度的控制装置。

# 可变 D (Variable-D)

ElectroVoice 在其麦克风设计中的一项受商标保护的专利，用于改变麦克风的近距离效应。`Variable-D` 在麦克风身上放置了几个端口，每个端口距离麦克风振膜越远，其对高频的敏感度就越低。

# VCA 自动化 (VCA Automation)

某些调音台中的混音自动化系统，通过使用电压控制放大器来改变声压水平或其他功能。

# VCA 组 (VCA Group)

多个 VCA 推子接收来自一组主推子控制的控制电压。这是高档调音台的一项功能，允许工程师通过单个推子控制一组独立信号，该推子使用 VCA 发送到每个通道的电压。

# 速度消息 (Velocity Message)

在合成器和键盘控制器中，一种传输击键力度数据的 MIDI 消息。速度消息可用于传输音量信息，还可以触发多采样器音色补丁上的不同样本。

# 速度麦克风 / 压力梯度麦克风 (Velocity Microphone / Pressure-Gradient Microphone)

速度麦克风 – 参见“压力梯度麦克风”。

# 速度敏感 (Velocity Sensitive)

（也称为“触控敏感”）MIDI 器（如键盘）的一种功能，根据击键力度程度传输 MIDI 速度依赖数据。

# 颤音 (Vibrato)

音调的平滑变化。

# 虚拟乐器 (Virtual Instrument)

（也称为软件乐器）一种基于软件的乐器。

# 易失性内存 (Volatile Memory)

电脑关闭时数据将会丢失。RAM（随机存储器）是最常见的易失性内存形式。

# 电压控制放大器 (VCA)

一种增益水平受外部电压影响的放大器。VCA 常用于合成器、信号处理器以及某些调音台的自动化手段。

# 电压控制滤波器 (Voltage Controlled Filter)

一种根据输入的控制电压改变截止频率的滤波器（特别是低通滤波器）。

# 电压控制振荡器 (VCO)

一种频率通过电压修改的振荡器。最常见于合成器。

# 电压 (Voltage)

两个物体之间的电势或压力（电位），会导致电流在它们之间流动。

# VU 单位 (VU)

一种用于测量音频响度变化的单位。该单位基本上是 VU 表读数所示的分贝变化。

# 音量 (Volume)

一个常用的非技术术语，要么指声压级（我们听到的响度），要么指音频电平。

# Vox

一个拉丁词，意为“声音”，常作为录音室音轨日志的缩写。

# VU 表 (VU Meter)

一种读取设备输出电压水平的仪表，其设计符合耳朵对电平突然变化的反应。

# 瓦特 (Watt)

电功率单位。

# 波形 (Wave)

这是振荡器产生的电压上下波动模式。不同的模式产生不同的声音。

# 波折叠器 (Wavefolder)

波折叠器是一种使用比较器和其他电路的特殊波整形器设计。

# 声 (Voice)

1. 除了人类嘴发出的声音定义外——在合成器中，“声”指的是声音之一。“单声道”意味着一次播放一个声音，“多声道”意味着多个声音可以同时发声。
2. 在某些合成器中（如雅马哈），“声”也可以指特定的音色补丁。

# 旁白 (Voice Over)

在音乐背景上录制的人声公告或旁白。

# 语音间 (Vocal Booth)

录音室内用于录制人声的房间，防止其他乐器串入。

# 声码器 (Vocoder)

一种分析信号特征并利用这些特征来影响另一个信号的音频处理设备。

# 声码器

产生特征性的机器人声。

# 附录 B：音频工程术语 (0 - 9 - A - Z)

观察波形是否超过（或低于）特定阈值。当波超过时，它们不是削掉波形的顶部和底部，而是创建一个它的镜像，并将该部分波形反射回自身，在此过程中产生更多的谐波和有趣的频谱。

## 波形 (Waveform)

这是振荡器输出的振动模式——电压的上下起伏。不同的模式产生不同的声音。

声波、音频信号或其他类型波的视觉表示或图表，显示波形在零线以上的下的波动。

## 波长 (Wavelength)

波的一个周期的物理长度，以英尺、英寸等单位测量。波长越长声音越低；波长越短，频率越高。

## 波形整形器 (Waveshaper)

说是“改变通过的波形形状的电路”显而易见，但这正是本质。波形整形器有特定的目标，例如将输入的三角形波转换为输出的正弦波，或者对波峰和瞬态添加类电子管的软剪切。许多波形整形器旨在以有趣的方式扭曲（或为波形添加谐波），产生更嘈杂（或更复杂明亮）的谐波频谱以创建新的声音。

## 波表 (Wetable)

这个术语具有相关但略有不同的含义。数字振荡器通过顺序读取数字表来产生声音，从一个数字描述的电平跳转到下一个。这个数字表描述了波的一个周期，通常被称为波表。许多数字振荡器具有多个对齐的波形，并可以在这些表之间移动——要么突然跳转（原始的 PPG 合成器这样做），要么通过在它们之间进行交叉淡入（今天大多数波表振荡器的做法）。有些人将每个表称为一个“波”，将一组这样的表称为一个波表。

## 加权 (Weighting)

用于音频测试的均衡曲线，用于补偿不同电平下的弗莱彻-曼森曲线（Fletcher-Munson Curve）。（参见“弗莱彻-曼森曲线”。）

## 西岸合成 (West Coast Synthesis)

所谓的“西岸”合成方法——传统上与 Buchla 和 Serge 等公司相关——通常基于向简单的波形添加谐波，而不是从复杂的波形中移除（滤波）它们。这通常通过使用一对振荡器（有时称为“复杂振荡器”）实现，其中一个调制另一个的频率（FM）或幅度（AM）；另一种常见的西岸方法是波形整形器或波折叠器。你可能还会发现两阶段包络生成器作为 AD 或 R（通常称为斜率发生器），而不是四阶段 ADSR，更强调控制电压的操作，一个共同特征还是具有内置低通滤波器的电压控制放大器，创建了所谓的低通门（LPG）。西岸方法还拥抱了非传统的控制器，如补丁控制和触摸。现在的系统中通常混合了东岸和西岸的方法。

## 湿声 (wet sound)

有时人们会说滤波器的声音很“湿”。这通常指的是一个少于 4 极的滤波器声音——通常是开启了共鸣的低通或带通滤波器，但未达到自激荡的程度。这种声音在酸 House 和其他技曲风格中很流行。

## 湿 (Wet)

混合了效果（如混响）的声音被称为“湿”（wet）；没有效果的声音被称为“干”（dry）。效果单元或调音台具有湿干比，用于设置原始未处理声音与完全效果化声音之间的比例。指带有全量效果（如混响）的信号，相对于“干”（指未加效果的声音）。在很多时候，混音中的首选声音是湿信号和干信号的混合。（参见“干”。）

## 白噪声 (White Noise)

噪声是一种没有明显音高的随机声音，例如呼吸声、呼吸噪音或风声或海浪声。噪声通常用不同的“颜色”描述，如白色、粉色、红色或蓝色，它们具有不同的分布频率。白噪声每个单位频率的功率相等（例如每 1000 赫兹），导致能量在所有频率上均匀分布。像粉色噪声这种更亮、更多嘶声的声音，工程师经常通过音频设备使用白噪声信号进行调音和校准，或在现场音频空间进行均衡处理。（参见“粉色噪声”。）

## 全音 (Whole Step)

相当于于两个半的音高变化，或者两个钢琴键之间的音高差。

## 自动声 (Wild Sound)

在电影和视频中，与视觉画面分开录制的音频可以添加到音频轨道层，且不需要与画面同步。

## 风控控制器 (Wind Controller)

一种类似于风乐器的设备，使用 MIDI 信号控制合成器、模块或虚拟乐器，而不是键盘控制器。

## 防风罩 (Windscreen)

一种覆盖在麦克风上的罩，用于减少风吹入麦克风引起的过度噪声。通常用于户外场所录音。

## 无线麦克风 (Wireless Microphone)

通过 FM 频率传输信号到舞台外接收器的麦克风，而不是通过音频线传输。

## 低音器 (Woofer)

设计用于重现低频低音扬声器。

## 写入模式 (Write Mode)

自动化控制台的操作模式，工程师控制通道增益，计算机记录随时间变化的增益值。

## XLR 线缆

使用 XLR 连接头的平衡麦克风线。（参见“XLR 连接头”。）

## XLR 连接头 (XLR Connector)

使用由 3 个针脚 XLR 连接头的平衡线。

## XY 拾音 (XY Miking)

一种同步技术，将两个心形麦克风以 90 度角相互放置，尽可能靠近。

## Y 型线 (Y-Cord)

一个输入和两个输出的分分器。

## 顶点 (Zenith)

指带有全量效果（如混响）的信号，相对于“干”（指未加效果的声音）。

## 零阶保持 (Zero-Order Hold (ZOH))

DAC 处理的数学表达式。

# 附录 C：源代码

- `00-generators`
- `01-additive`
- `02-subtractive`
- `03-formant`
- `04-granular`
- `05-fm`
- `06-la`
- `07-pd`
- `08-scanned`
- `09-vectorsynth`
- `10-virtualanalog`
- `11-wavetable`
- `12-physicalmodelling_karplus_strong`
- `Envelope.hpp`
- `MoogFilter.hpp`
- `quiz.cpp`
- `quiz2.cpp`
