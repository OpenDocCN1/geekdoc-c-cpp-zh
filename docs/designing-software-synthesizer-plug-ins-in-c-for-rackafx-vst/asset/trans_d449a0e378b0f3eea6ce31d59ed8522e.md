

计算线性关机值（1000 转换为毫秒关机时间）

-   进入关机状态

## startEG(), stopEG() 与 Legato 模式（连奏）

在单音合成器的 legato 模式下，如果你按住一个键然后按下另一个键，你将收到关机信号，因为合成器的音符已经用尽。在上面的 shutdown 函数中，我们简单地忽略了请求并返回而不关机。同样，我们忽略了启动消息并在不离开当前状态的情况下返回。关闭 EG 将其推入该状态（你可能需要对特殊的 EG 进行此修改）：

```
void EnvelopeGenerator::setEGMode(UINT u)
{
    // --- 保存它
    m_uEGMode = u;
    // --- 模拟 - 使用 e^-1.5x, e^-4.95x
    if (m_uEGMode == analog)
    {
        m_dAttackTCO = exp(-1.5); // 快速攻击
        m_dDecayTCO = exp(-4.95);
        m_dReleaseTCO = m_dDecayTCO;
    }
    else {
        // 数字是分贝线性的，所以使用
        m_dAttackTCO = 0.99999;
        m_dDecayTCO = m_dDecayTCO - exp(-11.05);
        m_dReleaseTCO = m_dDecayTCO;
    }
}
```

## isActive() & canNoteOff() 状态查询

我们需要回答拥有 EG 的外部对象的问题。我们将这些状态定义为：

-   active（激活）：如果我们不在 release（释放）或 off（关闭）状态
-   can note off（可以释放音符）：如果我们不在 release、shutdown（关机）或 off 状态，我们可以接受音符释放事件

## set ADSR 值

```
// --- 重新计算
calculateAttackTime();
calculateDecayTime();
calculateReleaseTime();
```

用户将使用一个（但并不一定）带有单位标记的接口。我们讨论过衰减（decay）和释放（release）段的时间与速率。此 EG 遵循相同的规则，并使用速率计算其参数。以下函数存储当前值并更新段变量。注意持续（sustain）电平影响衰减和释放。如果已经处于 release 状态，我们不会重新计算任何内容，以避免产生可能的抖动。

## 6.12 数字控制放大器 (DCA)

在本章中，我们还将研究并实现一个数字控制放大器或 DCA。DCA 将对每个合成器声部或补丁的最终输出应用所有增益控制。它还将实现声位（左/右平衡），并且该值可以被调制。图 6.29 显示了 DCA 的详细连接和简单框图。DCA 可以是单声道或立体声输入，但始终是立体声输出。

图 6.29：DCA 和声位控制组合在一个 DCA 对象中。你在 GUI 上看到的音量和声位控制按钮。幅度调制控制是单极性的，因此它只能衰减输出而不能放大输出。DCA 具有多个输入用于控制增益和声位：

```
void EnvelopeGenerator::reset()
{
    // -- 状态
    m_uState = off;

    // -- 重置
    setEGMode(m_uEGMode);

    // -- 可能在 noteOff() 中修改
    calculateReleaseTime();

    // -- 如果重置为零，让它保持冻结
    if(m_bResetToZero)
    {
        m_dEnvelopeOutput = 0.0;
    }
}
```

```cpp
void EnvelopeGenerator::calculateAttackTime()
{
    // -- 指数速率的采样
    double dSamples = m_dSampleRate*((m_dAttackTime_Sec)/1000.0);

    // -- 迭代指数计算的系数和基数
    m_dAttackCoeff = exp(-log((1.0 + m_dAttackTCO)/m_dAttackTCO)/dSamples);
    m_dAttackOffset = (1.0 + m_dAttackTCO)*(1.0 - m_dAttackCoeff);
}
```

```cpp
void EnvelopeGenerator::calculateDecayTime()
{
    // --- 指数速率的采样
    double dSamples = m_dSampleRate*(m_dDecayTime_Sec)/1000.0;

    // -- 迭代指数计算的系数和基数
    m_dDecayCoeff = exp(-log((1.0 + m_dDecayTCO)/m_dDecayTCO)/dSamples);
    m_dDecayOffset = (m_dSustainLevel - m_dDecayTCO)*(1.0 - m_dDecayCoeff);
}
```

```cpp
void EnvelopeGenerator::calculateReleaseTime()
{
    // --- 指数速率的采样
    double dSamples = m_dSampleRate*(m_dReleaseTime_Sec)/1000.0;

    // -- 迭代指数计算的系数和基数
    m_dReleaseCoeff = exp(-log((1.0 + m_dReleaseTCO)/m_dReleaseTCO)/dSamples);
    m_dReleaseOffset = -m_dReleaseTCO*(1.0 - m_dReleaseCoeff);
}
```

-   Amplitude（幅度）：用于音量的 GUI 控制
-   MIDI Velocity（MIDI 速度）：DCA 将 note on 事件的 MIDI 值转换为增益倍数
-   MIDI Volume（MIDI 音量）：MIDI 音量控制是连续控制器 CC7
-   MIDI Pan（MIDI 声位）：MIDI 声位控制是 CC10
-   Amplitude Modulation（幅度调制）：这连接到一个单极源用于幅度调制
-   Pan（声位）：用于声位的 GUI 控制
-   Amplitude Modulation（幅度调制）：连接到单极源用于幅度调制
-   Amp（幅度）：用于调制

```
void EnvelopeGenerator::noteOff()
{
    // 直接进入 release 状态
    if(m_dEnvelopeOutput > 0)
        m_uState = release;
    else // 持续电平为零
        m_uState = off;
}
```

DCA 在考虑输入后将计算最终增益值。它还将根据 GUI 计算声位值（这可能不是这样）。声位值基于正弦和余弦波的第一象限计算，因此没有真正的中心值——它是不对称的。声位的计算方法如下：

## 6.13 CDCA 对象

DCA 功能封装在 CDCA 对象中。该对象实现了增益和声位功能，并允许这些值进行调制。在第 8 章中，我们将修改它以接受来自 MIDI 连续控制器 7（音量）和 10（声位）的输入。表 6.2 列出了成员变量和方法。

```cpp
最简单的方法是 {
    if(m_uState != release && m_uState != off) {
        return true;
    }
}inline bool canNoteOff() {
    if(m_uState != release && m_uState != shutdown && m_uState != off) {
        return false;
    }
}
```

理解该对象的目的是遍历函数并讨论它们。打开 DCA.h 和 .cpp 文件并检查函数。

## 构造函数

-   初始化所有变量；注意此对象的许多变量默认值为 1.0，以避免 DCA 处于关闭状态——这些包括幅度控制、增益和 EG 调制变量
-   MIDI 速度也默认为最大值，以避免在未使用 MIDI 速度时出现静音

表 6.2：CDCA 成员变量和方法。

## 析构函数

-   这里不需要做什么，因为此对象中没有动态创建的变量

