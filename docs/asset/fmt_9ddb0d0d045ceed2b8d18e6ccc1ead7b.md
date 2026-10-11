
```cpp
for(Uint32 frame=0; frame<inNumberFrames; ++frame)
{
    // --- 清空累加器
    dOutL = 0.0;
    dOutR = 0.0;
    if(m_oscl1.bNoteOn)
    {
        << INSERT ** 代码列表 7.1：音频渲染 ** >>
    }
    // 写入缓冲区
    // --- 单声道
    left[frame] = dOutL;
}
etc...
}
```

## 第 8 章
参数化

NanoSynth 项目已初具规模，但仍有一些需要解决的问题以及需要增加的灵活性。首先，NanoSynth 是硬编码在特定的配置或补丁中的。例如，用户无法将 LFO 从振荡器重新路由到其他其他目标（例如滤波器截止频率）。此外，每当我们设计一个新的合成器架构时，都必须通过代码布线来手动连接组件。其次，它是单声的，而我们希望制作多声合成器（或至少理解它）。在本章中，我们将通过调制矩阵来解决第一个问题，该矩阵将补丁配置编程为矩阵中的一系列行。这将允许用户对调制路由有更多的控制权，并简化渲染函数的编码工作。接下来，我们将使用所有项目都将包含的标准 MIDI 控制器调制。然后，我们将为合成器添加另一个多声音符，并在双音符的 NanoSynth Poly 中实验音色抢取（voice-stealing）。最后，我们将使用全局参数化来简化合成器的更新过程。我们将尝试以尽可能易于理解的方式为 NanoSynth 添加这些新功能。然而，在下一章中，我们将处理出现的一些问题，并稍作修改范式——NanoSynth 是我们的“学习型合成器”，我们将利用经验来帮助塑造未来的项目。这是一个重要的章节——因为其余的项目将使用相同的核心 MIDI 功能、调制矩阵概念和全局参数化，这是我们最后一次打印合成器插件的详细细节。

强烈建议您获取《MIDI 制造商协会 DLS 二级规范》。它是一个在振荡器中使用音频样本的软件规范。更重要的是，它是本章基于的调制概念。它还包含了一套 GUI 以及对象的最小值、最大值和默认值，一种替代且有趣的滤波器设计，以及关于基于样本合成的大量信息。最后，这是一份供主要合成器制造商使用的实际规范。除非你在合成器公司工作，否则这将是你看到实际合成器规范的最接近。

## 8.1 调制路由

图 8.1 显示了目前 NanoSynth 的框图。调制路由为虚线。你可以观察到以下几点：

- EG1 到振荡器和 EG1 到 DCA 的路由具有强度控制，可以改变它们的调制量
- LFO 到振荡器和 EG1 到滤波器的路由没有这些控制
- LFO 强度通过其幅度变量进行全局控制
- EG 和 LFO 输出在应用到振荡器调制之前会求和
- EG1 和滤波器截止频率之间没有控制
- 没有可以重新路由调制输出的开关
- 没有可以启用/禁用路由的开关

在本章中，我们将学习如何设置带有和不带强度控制的调制矩阵，多个调制源可以以高度灵活的方式馈调制目标。对于你添加自己的自定义源和目标来说将非常容易。你还将学习如何在大矩阵中启用或禁用路由。图 8.1 显示了目前 NanoSynth 的详细连接图。虚线表示调制路由。

让我们通过追踪虚线连接，列出图 8.1 中的调制源和目标。

源：

- EG1 输出
- EG1 偏置输出
- LFO1 输出
- MIDI 音符编号（用于滤波器键跟踪调制）

![](img/b42d0dca53f4a889d8162d55f7c8c05d_457_0.png)

图 8.1：详细的 NanoSynth 框图。

目标：

- Osc1 $f_0$ 调制
- Osc2 $f_0$ 调制
- Filter $f_c$ 调制

### DCA EG 调制

还有更多可能的源和目标，在本章中添加其中几个。图 8.2 显示了 NanoSynth 当前版本中调制路由的概念图。源与右侧的目标对齐。我们看到了一个源馈给多个目标的情况，以及一个目标的强度是多个源之和的情况。我们希望描述一种具有这种灵活性且对路由数量没有限制的调制矩阵。

现在，考虑一下在渲染音频时代码是怎样的。对于 EG 到 振荡器的路由，其调制值是多个源的乘积：

```cpp
// （此处为代码）
```

对于 LFO 到路由器的路由，其调制值是多个源的乘积：

```cpp
// （此处为代码）
```

对于 EG 到 DCA 的路由，其调制值是多个源的乘积：

```cpp
// （此处为代码）
```

对于 EG 到滤波器的路由，其调制值是多个源的乘积：

```cpp
// （此处为代码）
```

对于 MIDI 到滤波器的路由，其调制值是多个源的乘积：

```cpp
// （此处为代码）
```

| 源 | 转换 | 强度 | 目标 |
| :--- | :--- | :--- | :--- |
| LFO1 输出 | 无 | 1.0 | Osc1 调制 |
| LFO1 输出 | 无 | 1.0 | Osc2 调制 |
| LFO1 输出 | 无 | 1.0 | Filter 调制 |
| EG1 输出 | 无 | 1.0 | Osc1 调制 |
| EG1 输出 | 无 | 1.0 | Osc2 调制 |
| EG1 输出 | 无 | 1.0 | Filter 调制 |
| EG1 偏置输出 | 无 | 1.0 | Osc1 调制 |
| EG1 偏置输出 | 无 | 1.0 | Osc2 调制 |
| EG1 偏置输出 | 无 | 1.0 | Filter 调制 |
| MIDI 音符编号 | 无 | 1.0 | Osc1 调制 |
| MIDI 音符编号 | 无 | 1.0 | Osc2 调制 |
| MIDI 音符编号 | 无 | 1.0 | Filter 调制 |

图 8.2：调制路由。

## 8.2 调制矩阵

调制矩阵背后的想法是：目前你必须编写代码来获取 LFO、EG 和 MIDI 音符编号的调制输出，并对其进行缩放。在本章中，我们将学习如何设置带有和不带强度控制的调制矩阵，多个调制源可以以高度灵活的方式馈调制目标。对于你添加自己的自定义源和目标来说将非常容易。你还将学习如何在大矩阵中启用或禁用路由。图 8.1 显示了目前 NanoSynth 的详细连接图。虚线表示调制路由。

| 源 | 转换 | 强度 | 目标 |
| :--- | :--- | :--- | :--- |
| LFO1 输出 | 无 | 1.0 | Osc1 调制 |
| LFO1 输出 | 无 | 1.0 | Osc2 调制 |
| LFO1 输出 | 无 | 1.0 | Filter 调制 |
| EG1 输出 | 无 | 1.0 | Osc1 调制 |
| EG1 输出 | 无 | 1.0 | Osc2 调制 |
| EG1 输出 | 无 | 1.0 | Filter 调制 |
| EG1 偏置输出 | 无 | 1.0 | Osc1 调制 |
| EG1 偏置输出 | 无 | 1.0 | Osc2 调制 |
| EG1 偏置输出 | 无 | 1.0 | Filter 调制 |
| MIDI 音符编号 | 无 | 1.0 | Osc1 调制 |
| MIDI 音符编号 | 无 | 1.0 | Osc2 调制 |
| MIDI 音符编号 | 无 | 1.0 | Filter 调制 |

图 8.2：调制路由。

每个单独路由都占据表格中的一行。

```cpp
// -- 调制衔接块 -- //
double dLF01Out = m_LF01.doOscillate();
double dBiasedEG = 0.0;
double dEGOut = m_EG1.Envelope(&dBiasedEG);
// -- 计算 EG->振荡器调制 (强度)(范围)(输出)
double dEGscMod = m_dEG10scIntensity*OSC_FO_MOD_RANGE*dBiasedEG;
// -- 将 EG 调制与 LFO 调制叠加 (强度)(1.0)(输出)
// 并应用到振荡器频率
m_0sc1.setFoModExp(dLF01Out*OSC_FO_MOD_RANGE + dEGscMod);
m_0sc2.setFoModExp(dLF01Out*OSC_FO_MOD_RANGE + dEGscMod);
m_0sc1.update();
m_0sc2.update();
// -- 检查键位跟踪 (keytrack)
if(m_uFilterKeyTrack == ON)
    // -- 设置为匹配经强度缩放的振荡器频率
    m_Filter1.m_dFcControl = m_0sc1.dOscFo*m_dFilterKeyTrackIntensity;
// -- 设置 EG->滤波器调制 (1.0)(范围)(输出)
m_Filter1.setFcMod(dEGOut*FILTER_FC_MOD_RANGE);
m_Filter1.update();
// -- 设置 EG->DCA 调制 (强度)(1.0)(输出)
m_DCA.setEGMod(dEGOut*m_dEG1DCAIntensity);
m_DCA.update();
```

调制矩阵替换了上述内容。伪代码如下：

```cpp
// --- 调制器渲染它们的输出
m_LFQ1.dooscillate();
m_EG1.doEnvelope();
```

```cpp
// --- 让调制矩阵处理连接和缩放
m_ModMatrix.doModulationMatrix();
```

```cpp
// --- 更新目标对象
m_Osc1.update();
m_Osc2.update();
m_Filter1.update();
m_DCA.update();
```

```cpp
// --- 现在进行数字音频渲染
etc...
```

注意杂乱的代码被消除了；不再有中间变量，也不再需要在对象之间传递变量。事实上，函数上不再有参数了！这变得非常简洁且高效。此外，由于补丁信息被编码在调制矩阵内部，相同的代码可以重复用于许多不同的补丁（patches）。我们的渲染函数不再需要知道或处理补丁路由的细节。

调制矩阵是以 C++ 对象的的形式实现的。该矩阵实际上由三个部分组成：

- 一个源（Source）寄存器数组
- 一个目标（Destination）寄存器数组
- 一个指向 `modMatrixRow` 结构体的指针数组，称为矩阵核心（matrix core）

源和目标寄存器是双精度浮点数（double），因此源和目标简单来说就是 `double` 数组。调制源将它们的输出写入源数组中预定义的位置。目标将从目标数组中预定义的位置读取其值。

调制核心的工作是从源数组中取值，可选地对其进行转换，根据其范围和强度变量进行缩放，然后将这些值累加到目标数组的位置中。

矩阵核心是定义每个调制路由的矩阵行指针数组。核心是动态创建的，并具有 get/set 函数，因此单个核心可以被多个矩阵共享。

图 8.3 显示了调制核心；它是一个填满了 `modMatrix` 指针和表示不存在某行的 `NULL` 指针的固定大小数组。矩阵核心的大小等于非 NULL 行的数量。

图 8.4–8.6 显示了通过调制矩阵进行调制的操作序列。这些操作可以分为三个阶段：

阶段 1：调制器将它们的输出写入 Sources 数组（MIDI 调制将通过 MIDI 到达）。

阶段 2：调制矩阵遍历其数组，从 Sources 数组提取值，进行转换、缩放，并将其累加到 Destinations 数组。

阶段 3：合成器组件从 Destinations 数组读取它们的调制值。

图 8.3：矩阵核心包含矩阵行指针或 NULL 指针；由于它有 8 个非 NULL 行，该矩阵的大小为 8。![](img/b42d0ca53f4a889d162d55f7c8c_0.png)

图 8.4：阶段 1：调制器将输出写入预定义位置的 Sources 数组。
```cpp
enum sources {
SOURCE_NONE = 0,
```
![](img/b42d0ca53f4a889d162d55f7c8c_462.png)

图 8.6：阶段 3：合成器从预定义位置的 Destinations 数组读取调制值。SOURCE_LF01,SOURCE_LF02,<SNIP SNIP_X,SOURCE_MIDI_JS,SOURCE_MIDI_Y,MAX_SOURCES, 
```cpp
enum destinations{
    DEST_NONE = 0,
    // --- 第 0 层
    // 见调制矩阵
    DEST_LF01,
    DEST_LF02,
    <SNIP SNIP_X,
    DEST_MIDI_JS,
    DEST_MIDI_Y,
    // --- 第 1 层
    // 见调制矩阵
    DEST_EG01,
    DEST_EG02,
    <SNIP SNIP_X,
    // --- 第 1 层结束
};
```

注意以下“通用”目标：

- DEST_OSC1
- DEST_OSC2
- DEST_FILTER1
- DEST_DCA

```cpp
enum sources {
    SOURCE_NONE = 0,
    // --- 第 0 层
    // 见调制矩阵
    SOURCE_OSC1,
    SOURCE_OSC2,
    SOURCE_LF01,
    SOURCE_LF02,
    <SNIP SNIP_X,
    SOURCE_MIDI_JS,
    SOURCE_MIDI_Y,
    // --- 第 1 层
    // 见调制矩阵
    SOURCE_EG01,
    SOURCE_EG02,
    <SNIP SNIP_X,
    MAX_SOURCES
};
```

```cpp
enum destinations {
    DEST_NONE = 0,
    // --- 第 0 层
    DEST_OSC1,
    DEST_OSC2,
    DEST_FILTER1,
    DEST_DCA1,
    <SNIP SNIP_X,
    // --- 第 1 层
    DEST_OSC3,
    DEST_OSC4,
    DEST_FILTER2,
    DEST_DCA2,
    <SNIP SNIP_X,
    MAX_DESTINATIONS
};
```

调制矩阵替换了上述内容。伪代码如下：

```cpp
// --- 调制器渲染它们的输出
m_LFQ1.dooscillate();
m_EG1.doEnvelope();
```

```cpp
// --- 让调制矩阵处理连接和缩放
m_ModMatrix.doModulationMatrix();
```

```cpp
// --- 更新目标对象
m_Osc1.update();
m_Osc2.update();
m_Filter1.update();
m_DCA.update();
```

```cpp
// --- 现在进行数字音频渲染
etc...
```

注意杂乱的代码被消除了；不再有中间变量，也不再需要在对象之间传递变量。事实上，函数上不再有参数了！这变得非常简洁且高效。此外，由于补丁信息被编码在调制矩阵内部，相同的代码可以重复用于许多不同的补丁。我们的渲染函数不再需要知道或处理补丁路由的细节。

调制矩阵是以 C++ 对象的的形式实现的。该矩阵实际上由三个部分组成：

- 一个源（Source）寄存器数组
- 一个目标（Destination）寄存器数组
- 一个指向 `modMatrixRow` 结构体的指针数组，称为矩阵核心（matrix core）

源和目标寄存器是双精度浮点数（double），因此源和目标简单来说就是 `double` 数组。调制源将它们的输出写入源数组中预定义的位置。目标将从目标数组中预定义的位置读取其值。

调制核心的工作是从源数组中取值，可选地对其进行转换，根据其范围和强度变量进行缩放，然后将这些值累加到目标数组的位置中。

矩阵核心是定义每个调制路由的矩阵行指针数组。核心是动态创建的，并具有 get/set 函数，因此单个核心可以被多个矩阵共享。

图 8.3 显示了调制核心；它是一个填满了 `modMatrix` 指针和表示不存在某行的 `NULL` 指针的固定大小数组。矩阵核心的大小等于非 NULL 行的数量。

图 8.4–8.6 显示了通过调制矩阵进行调制的操作序列。这些操作可以分为三个阶段：

阶段 1：调制器将它们的输出写入 Sources 数组（MIDI 调制将通过 MIDI 到达）。

阶段 2：调制矩阵遍历其数组，从 Sources 数组提取值，进行转换、缩放，并将其累加到 Destinations 数组。

阶段 3：合成器组件从 Destinations 数组读取它们的调制值。

图 8.3：矩阵核心包含矩阵行指针或 NULL 指针；由于它有 8 个非 NULL 行，该矩阵的大小为 8。![](img/b42d0ca53f4a889d162d55f7c8c_0.png)

图 8.4：阶段 1：调制器将输出写入预定义位置的 Sources 数组。
```cpp
enum sources {
SOURCE_NONE = 0,
```
![](img/b42d0ca53f4a889d162d55f7c8c_462.png)

图 8.6：阶段 3：合成器从预定义位置的 Destinations 数组读取调制值。SOURCE_LF01,SOURCE_LF02,<SNIP SNIP_X,SOURCE_MIDI_JS,SOURCE_MIDI_Y,MAX_SOURCES,
```cpp
enum destinations{
    DEST_NONE = 0,
    // --- 第 0 层
    // 见调制矩阵
    DEST_LF01,
    DEST_LF02,
    <SNIP SNIP_X,
```
