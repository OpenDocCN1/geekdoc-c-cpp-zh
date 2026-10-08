
EG 对象的框图如图 6.28 所示，绘图中使用了典型的线性线段。

虽然状态机的操作似乎有很多变量和方法，但你将学到 EG 的状态非常重要。它有助于判断音符事件（note events）是否结束，或者 EG 是否能够接收音符事件。还有很多重复的变量；每个状态都有一组用于计算的变量。还要注意成员变量 `m_bOutputEG`，这是一个标志位，如果 EG 连接到输出放大器，则会被被设置为 `true`。当连接到输出放大器的 EG 过期并进入关闭状态时，该信号表示一个音符事件已完全结束。在我们制作多音性合成器时，它将发挥重要作用。理解该对象最简单的方法是逐步执行函数并讨论它们。让我们从最重要的函数 `doEnvelope()` 开始。打开 `EnvelopeGenerator.h` 和 `.cpp` 文件并检查这些函数。

## doEnvelope()

一旦我们计算出指数系数和基数，EG 输出的计算就很简单了。虽然我们稍后会讨论包络生成器的代码，但查看这种直接且简单的实现是值得的。`doEnvelope()` 函数每个样本周期会被调用一次。返回值是当前 EG 的输出值。它还可以根据函数参数可选地返回偏置输出，该参数是一个指向接收信息的变量指针。花点时间研究流程并跟踪状态机操作。

表 6.1：EnvelopeGenerator 成员变量和方法。

![](img/b42d0dca53f4a889d8162d55f7c8c05d_359_0.png)

| 类型 | 变量名 | 说明 |
| --- | --- | --- |
| bool | m_bResetToZero | RTZ 模式标志 |
| bool | m_bLegacyMode | legato 模式标志 |
| bool | m_bOutputEG | 如果此 EG 连接到补丁的输出放大器，则为 true |
| UINT | m_uEGMode | 模式标志 |
| enum | analog_digital | 模式字符串 |

## EnvelopeGenerator 保护成员变量

| 类型 | 变量名 | 说明 |
| --- | --- | --- |
| double | m_DSampleRate | 采样率 |
| double | m_DEnvelopeOutput | 当前包络输出值 |
| double | m_dAttackCoef | 攻击系数 |
| double | m_dAttackOffset | 偏移量 x_ |
| double | m_dAttackTC | 时间常数过冲 |
| double | m_dDecayCoef | 衰减系数 |
| double | m_dDecayOffset | 衰减量 x_ |
| double | m_dDecayTC | 时间常数过冲 |
| double | m_dReleaseCoef | 释放系数 |
| double | m_dReleaseOffset | 释放偏移量 x_ |
| double | m_dReleaseTC | 释放时间常数过冲 |
| double | m_dAttackTime_mSec | 毫秒级攻击时间 |
| double | m_dDecayTime_mSec | 毫秒级衰减时间 |
| double | m_dReleaseTime_mSec | 毫秒级释放时间 |
| double | m_dShutdownTime_mSec | 毫秒级关闭时间 |
| double | m_dSustainLevel | 持续电平 [0..+1] |
| double | m_dIncShutdown | 关闭模式的增量值 |
| UINT | m_uState | 状态变量 |
| enum | off,attack,decay,sustain,release,shutdown | 可能的状态 |

## EnvelopeGenerator 成员函数（非虚）

| 函数名 | 说明 |
| --- | --- |
| getState | 返回当前状态变量 |
| isActive | 如果 EG 正在运行则为 true |
| canNoteOff | 如果 EG 可以接收 Note Off 消息则为 true |
| reset | 设置模式；模拟/analog |
| setEGAttackTime | 根据毫秒级攻击时间计算攻击变量 |
| calculateDecayTime | 根据毫秒级衰减时间计算衰减变量 |
| calculateReleaseTime | 根据毫秒级释放时间计算释放变量 |
| setAttackTime_mSec | 设置毫秒级攻击时间 |
| setDecayTime_mSec | 设置毫秒级衰减时间 |
| setReleaseTime_mSec | 设置毫秒级释放时间 |
| setSustainLevel | 设置持续电平 |
| setSampleRate | 设置采样率 |
| update | 更新变量（尚未使用） |
| startEG | 启动 EG 的有限状态机 |
| stopEG | 停止 EG 的有限状态机 |
| doEnvelope | 渲染包络输出值（正常和偏置） |

function 是一个大的 switch/case 语句

在非 off 状态下，首先渲染输出，然后评估状态更改条件（对于 attack，这意味着这意味着超过了 1.0 等）

sustain（持续）段仅保持恒定的输出值

shutdown（关闭）状态实现了第 6.3 节中的重置零操作；如果没有启用，它将直接移动到 off 状态，并将当前的电容“电荷”作为 `m_dEnvelopeOutput` 中的最后一个输出值

off 状态仅在启用了重置零时才将包络设置为 0.0

偏置输出的计算很简单——只需减去持续电平

接下来，逐步其余部分：

```cpp
inline double dEnvelope(double* pBiasedOutput - NULL)

// --- 解码状态
switch(m_uState)
    case off:
        // --- 输出为关闭
        if(m_bResetToZero)
            m_dEnvelopeOutput = 0.0;
        break;
    case attack:
        // --- 渲染输出
        m_dEnvelopeOutput = m_dAttackOffset + m_dAttackCoef * m_dAttackTC;
        // 检查 状态


        if(m_dEnvelope >= >= 1.0 || m_dAttackTime_mSec <= 0.0) {
            m_dEnvelopeOutput = 1.0;
            m_uState = decay; // 进入下一个状态
        }
        break;
    case decay:
        // --- 渲染输出
        m_dEnvelopeOutput = m_dDecayOffset + m_dDecayCoef * m_dDecay;;
        // 检查状态状态
        if(m_dEnvelopeOutput <= m_dSustainLevel || m_dDecayTime_mSec <= 0.0) {
            m_dEnvelopeOutput = m_dSustainLevel;
            m_uState = sustain; // 进入下一个状态
        }
        break;
    case sustain:
        // --- 渲染输出
        m_dEnvelopeOutput = m_dSustainLevel;
        break;
    case release:
        // --- 渲染输出
        m_dEnvelopeOutput = m_dReleaseOffset + m_dReleaseCoef * m_dRelease;
        // 检查状态状态
        if(m_dEnvelopeOutput <= 0.0 || m_dReleaseTime_mSec <= 0.0) {
            m_dEnvelopeOutput = 0.0;
            m_uState = off; // 进入下一个状态
        }
        break;
    case shutdown:
        // --- 渲染输出
        m_dEnvelopeOutput -= m_dIncShutdown;
        if(m_dEnvelopeOutput <= 0.0) {
            m_dEnvelopeOutput = 0.0;
            m_uState = off;
        }
        break;
}

if(pBiasedOutput)
    *pBiasedOutput = m_dEnvelopeOutput - m_dSustainLevel;
// 如果存在，则设置偏置输出
return m_dEnvelopeOutput;
}

```

## 方法

## 构造函数

## 析构函数

## setEGMode()

## reset()

## 重新计算释放时间（解释）

## noteOff ()

## shutDown()

```cpp
CEnvelopeGenerator::CEnvelopeGenerator(void)
// 默认值
m_dSampleRate = 44100;
m_dAttackTime_mSec = EG_DEFAULT_STATE_TIME;
m_dDecayTime_mSec = EG_DEFAULT_STATE_TIME;
m_dReleaseTime_mSec = EG_DEFAULT_STATE_TIME;
m_dSustainLevel = 1.0;
m_dEnvelopeOutput = 0.0;
m_dIncShutdown = 0.0;

// -- 用户通常不允许设置时间
m_dShutdownTime_mSec = 10.0; // 毫秒
```

```cpp
// -- 状态和标志
m_uState = off;
m_bOutputEG = false;
m_uEGMode = analog;
setEGMode(m_uEGMode);
m_bResetToZero = false;
m_bLegatoMode = false;
```

```cpp
// 如果重置零已启用，//清除输出变量
```

```cpp
// reset()
- 将状态重置为 off
- 重置模式
```

```cpp
// 在 legato 模式下忽略；我们希望
EG 保持其状态
```
