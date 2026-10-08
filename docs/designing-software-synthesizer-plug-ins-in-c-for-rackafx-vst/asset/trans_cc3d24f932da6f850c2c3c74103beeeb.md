

清除调制变量

## update()

```cpp
// --- called during updates
inline void setAttackTime_mSec(double d)
{
    m_dAttackTime_mSec = d;
    calculateAttackTime();
}
```

- 重新计算增益变量
- 注意，它是所有调制输入和 MIDI 控制值的组合
- 使用 `synthfunctions.h` 中提供的 `midiToAtten()` 函数来使用凸变换，你可以自由将其更改为任何你需要的幅度曲线

```cpp
inline void setDecayTime_mSec(double d)
{
    m_dDecayTime_mSec = d;
    calculateDecayTime();
}
```

## DCA()

- 计算控制值和调制的和作为总声位值
- 将声位值限制在 [-1..+1] 之间，以防用户控制设置导致偏移
- 计算等功率声位（equal power pan）值
- 根据增益和声位值的组合形成左右输出
- 使用 pass-reference 传递输出值；始终以立体声模式运行，即使不存在右输入

```cpp
inline void setReleaseTime_mSec(double d)
{
    m_dReleaseTime_mSec = d;
    calculateReleaseTime();
}
```

```cpp
inline void setSustainLevel(double d)
{
    m_dSustainLevel = d;
    // --- 持留水平影响衰减
    calculateDecayTime();
}
```

## 6.14 NanoSynth: EG/DCA

```cpp
// --- and release, 如果不在 release 状态
if(m_uState != )
    calculateReleaseTime();
```

我们继续学习上一章中修改过的学习合成器。在本章中，我们将添加一个包络生成器（EG）和 DCA。图 6.30 显示了添加了 EG 和 DCA 的 NanoSynth 简化框图。在本章中，我们只使用 EG 作为 DCA 的输出。在随后的章节中，我们将使用它来调制振荡器和滤波器。

你可以使用 NanoSynth 来测试对象的功能，并通过挑战（Challenges）来扩展它们。表 6.3 显示了你需要添加到现有 NanoSynth 项目中的连续列表控制和枚举列表控制。你可能想先查看示例代码，然后尝试自己的实现。记住，在你选择的平台上设计、编写代码和管理 GUI 由你决定。请参阅 http://www.willinkle.com/synthbook/ 的第 2 章寻求帮助。

图 6.31 和 6.32 显示了在本章完成后在 RackAFX、VST3 和 AU 中的 NanoSynth GUI。在随后的章节中，我们将继续填充其余的控制。对于 RackAFX，几个控制已嵌入 LCD 中——这些将始终由全局参数组成，而不是单个控制。![](img/b42d0dca53f4a889d8162d55f7c8c.png)

图 6.33 显示了 NanoSynth 的详细连接图。它显示了表 6.3 中的控制如何连接到基础合成器对象。你也可以看到强度控制的添加。你现在应该熟悉项目进展的流程了。对于所有平台，第一件事是实现 GUI。如果需要帮助，请回看第 2 章。一旦你有了 GUI 控制代码，就可以开始为新模块添加代码。你需要添加四个新文件（或手动创建它们）：

- EnvelopeGenerator.h 和 .cpp
- DCA.h 和 .cpp

图 6.30：NanoSynth 项目增加了两个部分：EG 和 DCA。

表 6.3：NanoSynth GUI 新增的连续和枚举参数。

图 6.31：RackAFX 中的一个 NanoSynth GUI；注意几个控制被嵌入在 LCD 控制中。

图 6.32： VST3 和 AU 项目的 NanoSynth GUI。

## 6.15 NanoSynth: EG/DCA 音频渲染

对于所有平台，核心音频渲染是相同的。与上一章的代码进行比较（此处仅对新代码加粗）。

- EG 是数据块的一部分，因此我们需要在输出的同一块代码中渲染它
- EG 输出乘以强度变量

```cpp
$p = \frac{(control+1)}{4}$
$L_{out} = \cos(p)$
$R_{out} = \sin(p)$
```

```cpp$attenuation = \frac{-x}{20\log_{10}(x)}$
$x=0, \quad 0 < x \le 127$
```

```cpp
DCA::DCA() {
    // 初始化变量
    m_dAmplitudeControl = 1.0;
    m_dAmp_dB = 0.0;
    m_dGain = 1.0;
    m_dAmplitude_dB = 0.0;
    m_dEGMod = 1.0;
    m_dPanControl = 0.0;
    m_dPan = 0.0;
    m_uVelocity = 127;
}
```

## DCA 成员变量

| 类型 | 变量名 | 说明 |
|---|---|---|
| double | m_dGain | 期间的总增益值 |
| double | m_dAmplitude_dB | dB 单位的幅度 |
| double | m_dAmplitudeControl | 原始形式的幅度 |
| double | m_dPanControl | [-1..+1] 范围内的声位控制，-1 为左，1 为右 |
| double | m_dAmp_dB | dB 调制 |
| double | m_dEGMod | EG 输入 |
| double | m_dPanMod | 声位调制 |

 DCA 成员函数（虚函数）

| 函数名 | 说明 |
|---|---|
| setmidiVelocity | 设置 MIDI 速度 |
| setPanControl | 设置 [-1..+1] 范围内的声位控制，-1 为左，1 为右 |
| reset | 重置 |
| setAmplitude_dB | 设置 dB 单位的幅度（音量） |
| setAmpMod_dB | dB 调制输入 |
| setEGMod | [0..1] 的 EG 输入 |
| setPanMod | [-1..+1] 的声位调制 |
| update | 更新增益和声位值 |
| doDCA | 渲染 DCA，单声道或立体声 |

```cpp
inline void setAmplitude_db(double d)
{
  m_dAmplitude_dB = d;
  m_dAmplitudeControl = pow((double)10.0, m_d/20.0);
}
```

- 渲染输出后，我们检查 EG 是否进入了关闭 状态，这表示音符事件结束，我们可以停止振荡器

```cpp
inline void reset()
{
  m_dEGMod = 0.0;
  m_dAmpMod = 0.0;
}
```

**图 6.33：** NanoSynth 连接图显示了来自表 6.3 的新控制；Pan 和音量控制在 DCA 块内部。

## 6.16 NanoSynth EG/DCA: RackAFX

使用表 6.3 将新控制添加到 GUI。打开 NanoSynth.h 和 .cpp 文件进行编辑。

### NanoSynth.h

为两个新对象添加新的 #include 语句并添加成员变量。

### NanoSynth.cpp

处理 .cpp 文件并在需要修改函数。我们主要添加新行，因为没有声明任何新函数。

 构造函数：inline void update()

- 不需要添加，因为成员构造函数会初始化对象

```cpp
{
 // 检查极性
if (m_dEGMod >= 0)
    m_dGain = m_dEGMod;
else
    m_dGain = m_dEGMod + 1.0;
}
```

## prepareForPlay()

- 在 EG 上设置采样率
- 将 EG 的 m_bOutputEG 标记为 true，因为此 EG 将连接到 DCA

```cpp
// --- 调制仅为衰减，dB 单位
m_dGain *= pow(10.0, m_dAmpDB/20.0);
// --- 使用 MIDI->Atten (凸) 变换
m_dGain *= midiToAtten(m_uVelocity);
```

## update()

- 使用 GUI 控制变量更新 EG 和 DCA

```cpp
inline void doDCA(double dLeftInput, double dRightInput,
double& dLeftOutput, double& dRightOutput)
{
 // 总声位值
dPanTotal = m_dPanControl + m_dPanMod;
 // 防止声位控制偏移的限制
dPanTotal = fmin(dPanTotal, 1.0);
dPanTotal = fmax(dPanTotal, -1.0);

double dLeft = 0.707;
double dRight = 0.707;

 // 等功率声位
calculatePanValues(dPanTotal, dLeft, dRight);

 // 形成左右输出
dLeftOutput = dLeft * m_dGain;
dRightOutput = dRight * m_dGain;
}
```

## processFrame()

- 修改音频渲染

## midiNoteOn()

- 我们需要修改此来启动 EG

![](img/b42d0dca53f4a889d8162d55f7c8c.374_0)

| 控制名称 (单位) | 类型 | 变量名 (VST3, RAFX) | 低/高/默认 | VST3/AU 索引 |
|---|---|---|---|---|
| Attack (mS) | double | m_AttackTime_MSec | 0.0 / 5000 / 100 | EG_ATTACK_MSEC |
| Decay (mS) | double | m_DecayTime_MSec | 0.0 / 5000 / 100 | EG_DECAY_MSEC |
| Sustain (mS) | double | m_SustainTime_MSec | 0.0 / 1.0 / 0.707 | EG_SUSTAIN_LEVEL |
| Release (mS) | double | m_ReleaseTime_MSec | 0.0 / 10000 / 2 | EG_RELEASE_MSEC |
| Pan | double | m_PanControl | -1.0 / 1.0 / 0.0 | OUTPUT_PAN |
| Volume (dB) | double | m_volume_DB | -96.0 / +24.0 / 0.0 | OUTPUT_AMPLITUDE_DB |
| EG DCA In | | m_EGDCAIntensity | -1.0 / 1.0 / 0.0 | EG_TO_DCA_INTENSITY |

| 控制名称 | 变量名 | 枚举字符串 | VST3/AU 索引 |
|---|---|---|---|
| Legato Mode | m_uLegatoMode | mono,legacy | LEGATO_MODE |
| Reset To Zero | m_uResetToZero | OFF | RESET_TO_ZERO |

同上

## midiNoteOff()

- （取消注释）停止振荡器的原始代码；这在 EG 衰减到相应阶段后才进行
- 只有当振荡器正在播放设计的 MIDI 音高时，才调用 EG 的 noteOff() 函数

![](img/b42d0dca53f4a889d8162d55f7c8c.374_1.png)

**图 6.33：** NanoSynth 连接图显示了来自表 6.3 的新控制；Pan 和音量控制在 DCA 块内部。

