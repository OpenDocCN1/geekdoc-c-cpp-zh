

## CStereoDelayFX 成员变量

| 变量名称 | 说明 |
| --- | --- |
| CDelayLine | m_Delay, m_RightDelay | 左、右延迟线对象 |
| double | m_dDelayTime_mSec | 用户控制的延迟时间（单位：毫秒）
| double | m_dFeedback_Pct | 用户控制的反馈（单位：%） |
| double | m_dDelayRatio | 左右通道之间延迟时间的比例 |
| double | m_dWetMix | 0 到 100 的湿信号（延迟）混合量；0.5 = 50% 混合 |
| UINT | m_uMode | 运行模式（目前下方有三种） |
| enum | norm,tap1,tap2,pingpong | 运行模式的枚举 |

表 13.4：CStereoDelayFX 成员函数。

## CStereoDelayFX 成员函数

| 函数名称 | 说明 |
| --- | --- |
| setMode | 设置模式变量 |
| setDelayTime_mSec | 设置延迟时间变量 |
| setFeedback_Pct | 设置反馈变量 |
| setDelayRatio | 设置比例变量 |
| setWetMix | 设置湿混合初始化函数 |
| preparePlay | 一次性初始化函数 |
| reset | 清空并重置两条延迟线 |
| update | 解码模式变量并在两个延迟线对象上设置两个延迟时间 |
| processAudio | 执行效果 |

与 `CDelayLine` 对象一样，`CStereoDelayFX` 也是一个短且简单的对象。你可以向该对象添加运行模式、更多的延迟线，甚至是滤波器和其他处理组件。插件需要新的控件来配合该对象：延迟时间、反馈、延迟比例、干湿混合以及延迟模式。这些控件会调用你在表 13.4 中看到的五个 `set()` 函数。其他函数函数如下：

## 构造函数

初始化成员变量。

## reset()

`reset()` 函数简单地调用了两个成员对象的 `resetDelay()` 方法。

```
CStereoDelayFX::CStereoDelayFX(void)
{
    // -- 将所有内容置零
    m_dDelayTime_mSec = 0.0;
    m_dFeedback_Pct = 0.0;
    m_dDelayRatio = 0.0; // 1:1
    m_dWetMix = 0.5; // 50%
}
```

```
void CStereoDelayFX::reset() {
    // --- 清空缓冲区并重置索引值

    m_LeftDelay.resetDelay();
    m_RightDelay.resetDelay();
}
```

## prepareForPlay()

这是该对象的一次性初始化函数。插件在其自身的一次性初始化函数中调用它，并传递当前的采样率。该函数将采样率传递给成员对象，然后调用 `init()` 函数请求分配两秒长的缓冲区。

```
// --- 一次性初始化
void CStereoDelayFX::prepareForPlay(double sampleRate) {
    // --- 先设置采样率
    m_LeftDelay.setSampleRate((int)dSampleRate);
    m_RightDelay.setSampleRate((int)dSampleRate);

    // --- 初始化为2秒最大延迟
    m_LeftDelay.init(2.0*sampleRate);
    m_RightDelay.init(2.0*sampleRate);

    // --- 执行清空
    reset();
}
```

## update()

`update()` 函数接收延迟比例，并使用该节开头的逻辑计算左、右延迟线上的独立延迟时间。对于负比例，请注意取反操作，这等同于此处调用了绝对值函数。

```
void CStereoDelayFX::update()
{
    if(m_uMode == tap1 || m_uMode == tap2)
    {
        // 如果负向左偏移
        // 如果正向右偏移
        // 如果比例为 0.0 则为 1:1
        if(m_dDelayRatio < 0)
        {
            // 注意取反！
            m_dTap2LTime_mSec = -m_dDelayRatio*m_dDelayTime_mSec;
            m_dTap2RTime_mSec = (1.0 + m_dDelayRatio)*m_dDelayTime_mSec;
        } else if (m_dDelayRatio > 0)
        {
            m_dTap2LTime_mSec = (1.0 - m_dDelayRatio)*m_dDelayTime_mSec;
            m_dTap2RTime_mSec = m_dDelayRatio*m_dDelayTime_mSec;
        } else
        {
            m_dTap2LTime_mSec = 0.0;
            m_dTap2RTime_mSec = 0.0;
        }

        // 普通时间
        m_LeftDelay.setDelay(m_dDelayTime_mSec);
        m_RightDelay.setDelay(m_dDelayTime_mSec);

        return;
    } else // 否则
    m_dTap2LTime_mSec = 0.0;
    m_dTap2RTime_mSec = 0.0;

    // --- 根据控制设置延迟时间
    // 如果负向左偏移
    // 如果正向右偏移
    // 如果比例为 0.0 则为 1:1
    if(m_dDelayRatio < 0)
    {
        // --- 注意取反！
        m_LeftDelay.setDelay(-m_dDelayRatio*m_dDelayTime_mSec);
        m_RightDelay.setDelay(m_dDelayTime_mSec);
    } else if (m_dDelayRatio > 0)
    {
        m_LeftDelay.setDelay(m_dDelayTime_mSec);
        m_RightDelay.setDelay(m_dDelayRatio*m_dDelayTime_mSec);
    } else
    {
        m_LeftDelay.setDelay(m_dDelayTime_mSec);
        m_RightDelay.setDelay(m_dDelayTime_mSec);
    }
```

## processAudio()

这是实现立体延迟的主函数。它遵循以下逻辑：

- 获取左、右延迟输出
- 根据运行模式形成延迟输入
- 调用 `processAudio()` 函数处理延迟输入
- 根据用户控制将干信号输入与湿信号混合

```cpp
bool CStereoFX::processAudio(double* pInputL, double* pInputR, double* pOutputL, double* pOutputR)
{
    // --- 执行延迟
    // 通用组件：
    double dLeftOut = m_LeftDelay.readDelay();
    double dRightOut = m_RightDelay.readDelay();

    // --- 输入延迟：默认为 norm
    double dLeftIn = *pInputL + dLeftOut*(m_dFeedback_Pct/100.0);
    double dRightIn = *pInputR + dRightOut*(m_dFeedback_Pct/100.0);

    double dLeftTap2out = 0.0;
    double dRightTap2out = 0.0;

    // --- 执行其他模式：
    // 注意：如果输入是单声（两个信号相同），cross 模式与 ping-pong 相同
    case cross:
        dLeftTap2out = m_LeftDelay.readDelayAt(m_dTap2LTime_mSec);
        dRightTap2out = m_RightDelay.readDelayAt(m_dTap2RTime_mSec);
        break;

    // 左输入 -> 左延迟； 左反馈 -> 右延迟
    // 右输入 -> 右延迟; 右反馈 -> 左延迟
    case ping:
        dLeftTap2out = m_LeftDelay.readDelayAt(m_dTap2LTime_mSec);
        dRightTap2out = m_RightDelay.readDelayAt(m_dTap2RTime_mSec);
        dLeftIn = *pInputL + (0.5*dLeftOut + 0.5*dLeftTap2out)*(m_dFeedback_Pct/100.0);
        dRightIn = *pInputR + (0.5*dRightOut + 0.5*dRightTap2out)*(m_dFeedback_Pct/100.0);
        break;

    case pong:
        // 左输入 -> 右延迟; 左反馈 -> 右延迟
        // 右输入 -> 左延迟; 右反馈 -> 左延迟
        dLeftIn = *pInputR + dRightOut*(m_dFeedback_Pct/100.0);
        dRightIn = *pInputL + dLeftOut*(m_dFeedback_Pct/100.0);
        break;
}

    // --- 中间变量
    double dLeftOut = 0.0;
    double dRightOut = 0.0;

    // --- 执行延迟线
    m_LeftDelay.processAudio(&dLeftIn, &dLeftOut);
    m_RightDelay.processAudio(&dRightIn, &dRightOut);

    // --- 生成输出
    *pOutputL = *pInputL*(1.0 - m_dWetMix) + dLeftOut*m_dWetMix;
    *pOutputR = *pInputR*(1.0 - m_dWetMix) + dRightOut*m_dWetMix;

```
    // --- 返回全部
    return true;
```

# 13.5 在插件中使用 CStereoDelayFX 对象

![](img/b42d0dca53f4a889d162d55f7c8c05d_886_0.png)

图 13.11：在 DCA 之后添加延迟的新型 MiniSynth。

使用延迟对象是令人耳目的。当然，接口是如此，但之后只有几个函数需要调用。这个延迟对象不是声部的成员——作为主效果，它位于声部之外。为了方便实现，我们将延迟对象作为插件的成员。插件对象将形成当前采样输出，然后在写入输出位置之前通过延迟处理。请记住，这是按样本进行的，而不是按声部半径进行的。图 13.11 显示了在 DCA 之后添加延迟的 MiniSynth。我们没有添加调制例程，但如果需要可以作为一个章节挑战。记住插件与声部共享调制核心，并且接收 MIDI 控制输入，因此我们可以根据需要将其添加到 FX 部分。

使用延迟对象，你需要实现以下代码块：

## 声明

在插件的 h 文件中 #include 语句并添加延迟成员变量。

```
CStereDelayFX
m_DelayFX;
```

## 初始化

在已知采样率的一次性函数中初始化该对象。这是在主更新函数之前添加的一行代码。

