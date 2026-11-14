

```cpp
bool __stdcall CRingModulator::processAudioFrame(float* pInputBuffer, float* pOutputBuffer,
uint uNumInputChannels, uint uNumOutputChannels)
{
    // Do LEFT (MONO) Channel; there is always at least one input/one output
    // generate carrier
    float yn;
    m_Oscillator.doOscillate(&yn, &yn);
    // multiply
    pOutputBuffer[0] = pInputBuffer[0]*yn*(m_fModDepth/100.0);
    // Mono-In, Stereo-Out (AUX Effect)
    if(uNumInputChannels == 1 && uNumOutputChannels == 2)
        pOutputBuffer[1] = pOutputBuffer[0];
    // Stereo-In, Stereo-Out (INSERT Effect)
    if(uNumInputChannels == 2 && uNumOutputChannels == 2)
        pOutputBuffer[1] = pInputBuffer[1]*yn*(m_fModDepth/100.0);
    return true;
}
```

构建并测试插件。你可能会发现它是一个非常出色的效果，或者你可能觉得它听起来很糟糕。你可以对这个项目进行的一些修改包括：

- 使用多个载波频率。
- 使用串联或并联的多重调制。
- 使用 LFO 调制载波频率。

## 14.3 设计波形整形插件

波形整形是一种非线性处理方法，其结果是向输入信号添加谐波。它用于合成器和失真算法中。由于向信号添加了谐波，波形整形器会像环形调制器一样遭受混叠问题。波形整形的过程很简单，因为不需要存储元件。你将输入信号 x 视为函数的自变量。该函数通常是三角函数或多项式函数。一个有趣的可用函数是反正切函数。它属于一组称为 Sigmoid 函数的函数家族。Sigmoid 函数产生 S 形曲线。电子管的幅度传递函数通常类似于 Sigmoid 曲线，因此可以使用此函数来尝试模拟电子管声音。图 14.3 显示了反正切函数 atan(kx)，其中 k 控制输入值的幅度，从而控制应用的非线性处理量。精确方程如公式 14.2 所示，其中添加了一个归一化系数以将输出限制在 -1 到 +1 的范围内。你可以在图 14.3 中看到，当 k = 1 时，输入/输出关系几乎是线性的。随着 k 的增加，S 形曲线出现并增加增益。例如，当 k = 5 且 x(n) = 0.25 时，y(n) 约为 0.6。

```
y(n) = \frac{1}{\arctan(k)} \arctan(kx(n)) (14.2)
```

非对称失真可以通过使用两个不同的 k 值来轻松实现，一个用于正输入样本，另一个用于负输入样本。这种非对称失真存在于 Class-A 电子管电路中。级联多个阶段将导致更多的谐波失真。在某些放大器中，许多阶段串联级联。Class A 电子管电路还会反相信号。这意味着在每个阶段之间，非对称失真曲线也会反相。所产生的声音与仅仅级联模块而不反相有很大不同。我们将设计一个插件，实现反正切波形整形，并允许用户调整以下内容；

![](img/b54974d0a4317ec82d7ae02126d10a6f_474_0.png)

Figure 14.3: 方程 14.1 在 k = 1 和 k = 5 时的输入/输出关系。

- 输入信号正半周期和负半周期的 k 值
- 串联的阶数，最多 10 个
- 级联时是否对每隔一个阶段进行反相

### 14.3.1 项目：WaveShaper

创建一个项目并将其命名为“WaveShaper”。没有其他对象或选项需要添加。

### 14.3.2 WaveShaper: GUI

将表 14.3 中的控件添加到 WaveShaper 项目所需的 GUI 中。

### WaveShaper.h 文件

.h 文件中无需任何操作，因为我们不需要额外的变量、内存存储空间、方法或对象！

### WaveShaper.cpp 文件

唯一需要修改的方法是 processAudioFrame()。

Table 14.3: WaveShaper 插件 GUI 控件。

| 滑块属性 | 值 | 滑块属性 | 值 |
|---|---|---|---|
| 控件名称 | +Atan 指数 | 控件名称 | -Atan 指数 |
| 单位 | | 单位 | |
| 变量类型 | float | 变量类型 | float |
| 变量名 | m_fArcTanKPos | 变量名 | m_fArcTanKNeg |
| 下限 | 0.10 | 下限 | 0.10 |
| 上限 | 20 | 上限 | 20 |
| 初始值 | 1 | 初始值 | 1 |
| 控件名称 | 阶数 | 控件名称 | 反相阶数 |
| 单位 | | 单位 | |
| 变量类型 | float | 变量类型 | enum |
| 变量名 | m_nStages | 变量名 | m_uInvertStages |
| 下限 | 1 | | |
| 上限 | 10 | | |
| 初始值 | 1 | 枚举字符串 | 关, 开 |

```cpp
bool __stdcall CWaveShaper::processAudioFrame(float* pInputBuffer, float* pOutputBuffer,
    UINT uNumInputChannels,
    UINT uNumOutputChannels)
{
    // Do LEFT (MONO) Channel; there is always at least one input/one output
    // (INSERT Effect)
    float f_xn = pInputBuffer[0];

    // cascaded stages
    for(int i=0; i<m_nStages; i++)
    {
        if(f_xn > 0)
            f_xn = (1.0/atan(m_fArcTanKPos))*atan(m_fArcTanKPos*f_xn);
        else
            f_xn = (1.0/atan(m_fArcTanKNeg))*atan(m_fArcTanKNeg*f_xn);

        // invert every other stage
        if(m_uInvertStages == ON && i%2 == 0)
            f_xn *= -1.0;
    }

    pOutputBuffer[0] = f_xn;

    // Mono-In, Stereo-Out (AUX Effect)
    if(uNumInputChannels == 1 && uNumOutputChannels == 2)
        pOutputBuffer[1] = pOutputBuffer[0];

    // Stereo-In, Stereo-Out (INSERT Effect)
    if(uNumInputChannels == 2 && uNumOutputChannels == 2)
    {
        float f_xn = pInputBuffer[0];

        // cascaded stages
        for(int i=0; i<m_nStages; i++)
        {
            if(f_xn > 0)
                f_xn = (1.0/atan(m_fArcTanKPos))*atan(m_fArcTanKPos*f_xn);
            else
                f_xn = (1.0/atan(m_fArcTanKNeg))*atan(m_fArcTanKNeg*f_xn);

            // invert every other stage
            if(m_uInvertStages == ON && i%2 == 0)
                f_xn *= -1.0;
        }

        pOutputBuffer[1] = f_xn;
    }

    return true;
}
```

构建并测试插件。请注意，要完全复制电子管电路，你需要的远不止失真组件，因为电子管电路对幅度敏感且带宽受限。然而，这个插件是开始尝试非线性处理的一个好地方。

## 参考文献

- Black, H. S. 1953. 调制理论. New York: Van Nostrand-Reinhold.
- Dodge, C. 和 T. Jerse. 1997. 计算机音乐合成、作曲与表演，第 4 章. New York: Schirmer.
- Roads, C. 1996. 计算机音乐教程，第 2 章. Cambridge, MA: The MIT Press.
- U.S. Navy. 1973. 基础电子学，速成培训手册 NAVPES, 10087-C. New York: Dover Publications.

## VST® 和 AU® 插件 API

一旦你学会如何使用 RackAFX 设计插件，你会发现学习其他插件应用程序编程接口（API）相当简单。主要原因是大多数插件 API 与 RackAFX 共享非常相似的结构和函数调用。一个类比可能是学习飞行：一旦你内化了单飞的基础知识，学习驾驶不同类型的飞机就是了解每种飞机的特殊性问题。在掌握升力、阻力、俯仰和偏航原理后，你不需要再担心这些原理。当前流行的插件 API 包括 Steinberg 的虚拟工作室技术 (VST)、Apple Computer 的音频单元 (AU) 以及 Avid 的 Avid 音频扩展 (AAX)® 格式。如果你想为这些 API 编写代码，第一步是通过制造商的网站设置开发者账户。拥有账户后，你可以下载他们的 API 文档和 SDK（软件开发工具包），其中包括示例代码模板。VST 和 AU API 是公开文档化的，而 AAX 不是。像 RackAFX 一样，VST 插件使用纯 C++ 编写，不需要外部框架或基础类。AU 插件不是，并且需要良好的 Mac 编程知识才能开发。一旦你有了 RackAFX 插件，如何使其在其他插件 API 中工作？

### A.1 在 Windows 上编译为 VST 插件

在第三方客户端中使用 RackAFX 插件的最简单方法是利用这样一个事实：你可以将项目设置为编译为与 RackAFX 和 Windows 操作系统 (OS) 上的 VST 兼容的动态链接库 (DLL)。你可以在创建项目时或开发过程中稍后启用此功能。如果你已经有一个正在开发的项目，请使用 文件 → 编辑项目 或用户界面 (UI) 上的编辑按钮。在编辑项目对话框中，勾选“使 VST 兼容”复选框，如图 A.1 所示。生成的 DLL 将同时适用于 RackAFX 和任何 Windows VST 客户端。只需将 DLL 从你的 /PlugIns 文件夹复制到客户端的指定 VST 文件夹中。

GUI 选项如下：

- 使用 VST 客户端的 GUI：VST 客户端将为你提供一个 *默认界面*，其外观和手感由客户端制造商决定。这些界面从简单的滑块组到更复杂的 GUI 不等。客户端将查询你的插件以获取控件信息并在运行时构建 GUI。对于此选项，你不需要提供任何额外代码。

