
# DXSynthVoice 成员函数

| 函数名 | 描述 |
| --- | --- |
| initGlobalParameters | 初始化全局参数 |
| initializeModMatrix | 初始化调制矩阵 |
| setSampleRate | 设置子组件的采样率 |
| prepareForPlay | 在子组件上准备工作，初始化 |
| update | 更新变量 |
| reset | 重置变量 |
| setLFODestination | 将 LFO 目标设置为任何操作器的 Amp 或颤抖调制输入 |
| canNoteOff | 重写；当所有载波器都可以进入关闭状态时返回 true |
| isVoiceDone | 重写；当所有载波器过期时返回 true |
| setOutputEGs | 设置载波器的输出 EG 标记（延续、归零以及任何其他输出 EG 操作） |
| doVoice | 渲染音频 |

# setSamplerRate()

在此处你只需要调用基类。

# prepareForPlay()

在 `prepareForPlay()` 中你调用基类，然后像之前的合成器一样调用 `reset()`。

# reset()

在 `reset()` 中你首先调用基类，然后将 portamento（滑音）时间归零，类似于之前的合成器。

# update()

`update()` 函数在 DXSynthVoice 中非常简单——只需调用基类，然后进行任何 voice 特定的初始化；我们只需要在对象上设置四个新参数。

```
CDSynthVoice::CDSynthVoice(void) {
    // 你的振荡器和滤波器
    m_p0sc1 = &m_0p1;
    m_p0sc2 = &m_0p2;
    m_p0sc3 = &m_0p3;
    m_p0sc4 = &m_0p4;

    // 清除我们的变量
    m_dop1Feedback = 0.0;
    m_dop2Feedback = 0.0;
    m_dop3Feedback = 0.0;
    m_dop4Feedback = 0.0;
}

inline virtual void initGlobalParameters(globalSynthParams* pGlobalParams)
// --- 首先调用基类
CVoice::initGlobalParameters(pGlobalParams);

// --- 添加 voice 特定的变量
// 注意：我们在此处设置 VOICE 使用的强度
m_pGlobalVoiceParams->d01Feedback = m_dop1Feedback;
m_pGlobalVoiceParams->d02Feedback = m_dop2Feedback;
m_pGlobalVoiceParams->d03Feedback = m_dop3Feedback;
m_pGlobalVoiceParams->d04Feedback = m_dop4Feedback;

// --- 如果用户没有 GUI 控制，则设置为 1.0
m_pGlobalVoiceParams->dLFO1scModIntensity = 1.0;
```

# setLFODestination()

在 `setLFODestination` 中解码操作器的索引，然后操作其调制矩阵源。你在一个巨大的 switch/case 语句中将 `m_uSourceAmp` 和/或 `m_uSourceFo` 设置为相应的 LFO 输出目标。如果用户选择了 none（无），你将两者都设置为 `DEST_NONE`。这是对每个操作器独立进行的（DEST_OSC1_OUTPUT_AMP 和 DEST_OSC1_FO 对应操作器 1，而 DEST_OSC2_OUTPUT_AMP 和 DEST_OSC2_FO 对应操作器 2，依此类推）。

```
void DXSynthVoice::initializeMatrix(CModulationMatrix* pMatrix)
{
  // --- 始终首先调用基类来创建核心并初始化基础路由
  CVoice::initializeMatrix(pMatrix);

  if(!pMatrix->getModMatrixCore()) return;

  // DX 合成器特定的调制矩阵 - 与其他不同
  // 因为它对所有 LFO 路由使用单一 LFO 强度控制
  // -- 这些默认关闭，但你可以允许用户启用/禁用
  modMatrixRow* pRow = NULL;

  // LFO1 -> DEST_OSC1_OUTPUT_AMP (幅度调制)
  pRow = createModMatrixRow(SOURCE_LFO1,
      DEST_OSC1_OUTPUT_AMP,
      &m_GlobalVoiceParams->dLFO1scModIntensity,
      &m_dDefaultRange, // 此用于 AM

  TRANSFORM_BIPOLAR_TO_UNIPOLAR,
      false); /* 默认禁用 */

  pMatrix->addModMatrixRow(pRow);

  等等... 在此处添加后续行
```

# canNoteOff()

这是我们第一次需要重写此函数。通常，它将调用转发到默认输出 EG (EG1)。如果 EG 可以进入关闭状态，则返回，这意味着它不处于释放（release）、等待释放（releasePending）、关闭（shutdown）或偏移（offsets）状态。对于 DXVoice，当所有 EG 都连接到可以进入关闭状态的载波时，我们需要返回 true。这涉及检查算法和检查所有载波 EG。注意算法索引中的偏移；这只是匹配 DX 图形上的数字（AU 和 VST3 用户可用）。因此算法 1 实际上是模式 0。switch/case 语句根据载波振荡器的数量分为若干部分。

# isVoiceDone()

下一个 DX 特定的重写是 `VoiceDone()`，它以与 `canNoteOff()` 相同检查载波 EG。

# setOutputEGs()

`setOutputEGs()` 遵循之前相同的模式，两个函数——识别输出 EG（连接到载波的 EG）并在它们上设置标记。

```
void CDSynthVoice::update()
```

```
{
    // -- voice 特定的更新
    if(!m_pGlobalVoiceParams) return;
```

# doVoice()

`doVoice()` 中的音频渲染与与其他合成器略有不同，因为这里没有滤波器。这是唯一不使用调制矩阵将 EG 连接到振荡器的渲染函数。可以那样做，但那会让调制矩阵编程变得非常复杂，因为更改算法索引将重新布线调制器和信号流。相反，调制矩阵仅用于 LFO 调制路由以及 MIDI 速度到起始时间和音符到衰减的循环。算法块是按老办法连接在一起的。

```
// -- 始终调用基类
CVoice::update();
```

```
// --- 这里的代码
m_dop1Feedback = m_pGlobalVoiceParams->d01Feedback;
m_dop2Feedback = m_pGlobalVoiceParams->d02Feedback;
m_dop3Feedback = m_pGlobalVoiceParams->d03Feedback;
m_dop4Feedback = m_pGlobalVoiceParams->d04Feedback;
```
