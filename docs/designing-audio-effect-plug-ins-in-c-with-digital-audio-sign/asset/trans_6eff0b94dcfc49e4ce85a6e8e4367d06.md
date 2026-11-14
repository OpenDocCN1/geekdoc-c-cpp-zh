

- 计算一个新的 $f_c$ LFO 值。
- 使用 LFO 值计算一个新的 $f_c$ 值。
- 计算一个新的 Q LFO 值。
- 使用 LFO 值计算一个新的 Q 值。
- 使用 $f_c$ 和 Q 值计算新的滤波器系数。
- 对输入样本执行 bi-quad 运算。

```
bool __stdcall CModFilter::processAudioFrame(float* pInputBuffer, float* pOutputBuffer,
    UINT uNumInputChannels, UINT uNumOutputChannels)
{
    //
    // output = input -- change this for meaningful processing
    //

    float fYn = 0; // normal output
    float fYqn = 0; // quad phase output

    // call the fc LFO function; we only need first output
    m_fc_LFO.doOscillate(&fYn, &fYqn);

    // calculate fc
    float fc = calculateCutoffFreq(fYn);

    // call the Q LFO function
    m_Q_LFO.doOscillate(&fYn, &fYqn);

    // calculate the new Q
    float fQ = calculateQ(fYn);

    // use to calculate the LPF
    calculateLPFCoeffs(fc, fQ, &m_LeftLPF);
    calculateLPFCoeffs(fc, fQ, &m_RightLPF);

    // do the BiQuads
    pOutputBuffer[0] = m_LeftLPF.doBiQuad(pInputBuffer[0]);

    // Mono-In, Stereo-Out (AUX Effect)
    if(uNumInputChannels == 1 && uNumOutputChannels == 2)
        pOutputBuffer[1] = pOutputBuffer[0]; // just copy

    // Stereo-In, Stereo-Out (INSERT Effect)
    if(uNumInputChannels == 2 && uNumOutputChannels == 2)
        pOutputBuffer[1] = m_RightLPF.doBiQuad(pInputBuffer[1]);

    return true;
}
```

你会发现，只需添加几行代码就能让第二个调制源正常工作。构建并测试插件。你将听到两个 LFO 对 $f_c$ 和 Q 进行调制；调整 LFO 速率和深度控制，也可以尝试更改 LFO 波形类型。Q 调制听起来可能更微妙，但如果你使用 RackAFX 的振荡器并将白噪声通过它，调制效果会变得清晰可闻。我们将通过再做一次修改来完成插件：能够将左右 LPF 调制源置于正交相位。

## 12.3 设计调制滤波器插件：第三部分，正交相位 LFO

在第三次设计迭代中，我们将修改当前插件以支持正交相位 LFO。框图如图 12.7 所示。

参数如下：

- $f_c$ 调制速率（0.2 至 10 Hz）
- $f_c$ 调制深度（0 至 100%）
- Q 调制速率（0.2 至 10 Hz）
- Q 调制深度（0 至 100%）
- LFO 类型（正弦、三角、锯齿、方波）
- LFO 相位（普通、正交）
- $f_c$ 调制范围：100 Hz 至 5 kHz
- Q 调制范围：0.577 至 10
- LPF 固定为二阶双二阶（bi-quad）

要将 LFO 切换到正交相位，我们只需添加一个单选按钮控件，并对 processAudioFrame() 函数做轻微修改。

### 12.3.1 ModFilter 图形用户界面

在表 12.4 中添加单选按钮控件。注意：这是一个直接控制变量——无需在 userInterfaceChange() 或 prepareForPlay() 中添加任何额外内容，因为我们仅在 processAudioFrame() 函数中使用它。

![](img/b54974d0a4317ec82d7ae02126d10a6f_404_0.png)

图 12.7：带有正交相位 LFO 的调制滤波器。

### 12.3.2 ModFilter.cpp 文件

```
processAudioFrame()
```

- 检查枚举变量并使用相应的 LFO 输出样本。

```
bool __stdcall CModFilter::processAudioFrame(float* pInputBuffer, float* pOutputBuffer,
UINT uNumInputChannels, UINT uNumOutputChannels)
{
  //
  // output = input -- change this for meaningful processing
  //
  float fYn = 0; // normal output
  float fYqn = 0; // quad phase output
  // call the LFO function; we only need first output
  m_fc_LFO.doOscillate(&fYn, &fYqn);
  // calculate both fc values (can be streamlined!)
  float fc = calculateCutoffFreq(fYn);
  float fcq = calculateCutoffFreq(fYqn);
  // get the Q LFO output
  m_Q_LFO.doOscillate(&fYn, &fYqn);
  // calculate both Q values
  float fQ = calculateQ(fYn);
  float fQq = calculateQ(fYqn);
  // use the fc and Q to calculate the Left LPF coeffs
  calculateLPFCoeffs(fc, fQ, &m_LeftLPF);
  calculateLPFCoeffs(fc, fQ, &m_RightLPF);
  // test the Phase variable; if not NORM, use the
  // quad phase values on the Right channel
  if(m_uLFO_Phase == NORM)
    calculateLPFCoeffs(fc, fQ, &m_RightLPF);
  else
    calculateLPFCoeffs(fcq, fQq, &m_RightLPF);
  // do the BiQuads
  pOutputBuffer[0] = m_LeftLPF.doBiQuad(pInputBuffer[0]);
  // Mono-In, Stereo-Out (AUX Effect)
  //(uNumInputChannels == 1 && uNumOutputChannels == 2)
  if(uNumInputChannels == 1 && uNumOutputChannels == 2)
    pOutputBuffer[1] = pOutputBuffer[0]; // just copy
  // Stereo-In, Stereo-Out (INSERT Effect)
  //(uNumInputChannels == 2 && uNumOutputChannels == 2)
  pOutputBuffer[1] = m_RightLPF.doBiQuad(pInputBuffer[1]);
  return true;
}
```

表 12.4：正交相位控件。

| 按钮属性 | 值 |
|---|---|
| 控件名称 | LFO |
| 单位 | |
| 变量类型 | enum |
| 变量名 | m_uLFO_Phase |
| 枚举字符串 | NORM, QUAD |

构建并测试新插件。当你将相位更改为正交时，你会轻松地听到两个调制在两个扬声器之间互相追逐。未来插件的想法包括：

- 更改滤波器类型（高通滤波器、带阻滤波器、带通滤波器）。
- 使用双调制器：用*另一个* LFO 调制一个 LFO，然后用它来控制一个参数。

## 12.4 设计包络跟随器插件

尽管普通的调制滤波器很有趣，但由于 LFO 调制，它具有一种机械感。这对合成器来说可能不是问题，但听起来不够音乐化。我们可以通过实现包络跟随器来将调制与音乐输入信号相关联，包络跟随器使用输入信号的幅度包络来控制滤波器参数。例如，我们可以编写代码，使得当输入信号幅度较高时，$f_c*会被调制*向上*到更高的值，当然，作为插件创建者，我们也可以进行相反的调制。
包络跟随器需要一个音频包络检测器，你可以使用 RackAFX 内置的一个。我们将使用与滤波器相同的二阶 LPF 来进行调制；然后你可以自行尝试不同的滤波器类型。首先，请看图 12.8 中的框图。

参数如下：

- 前置增益：0 至 +20 dB 的前置增益，用于驱动检测电路
- 阈值（信号必须超过的值才能激活检测器）
- 包络攻击时间（mSec）
- 包络释放时间（mSec）
- 上/下调制控制（决定正向幅度偏移是否导致正向或负向 $f_c$ 偏移）
- 数字/模拟检测模式：更改检测器时间常数
- 用户可调 Q
- LPF 固定为二阶双二阶（bi-quad）

![](img/b54974d0a4317ec82d7ae02126d10a6f_406_0.png)

图 12.8：包络检测器框图。

我们可以为 LFO 使用相同的 CBiquad 对象，但需要另一个对象来处理包络检测。该对象是内置的；接口在 pluginconstants.h 中，实现位于 pluginobjects.cpp 文件中。CEnvelopeDetector 具有表 12.5 所示的成员变量和函数。

这是一个功能相当丰富的插件，包含多个控件和交互。让我们先从检测器本身开始。CEnvelopeDetector 基于参考文献（musicdsp.org）中列出的一个简单检测器。该检测器将模拟峰值、均方和 RMS 检测器合二为一。要使用检测器，请执行以下步骤：

- 创建检测器的实例，例如 CEnvelopeDetector m_Detector。
- 使用 init() 函数一次性初始化所有参数，例如 m_Detector.init((float)m_nSampleRate, 10.0, 250.0, true, DETECT_MODE_RMS, false)。
- 这段代码使用以下参数初始化检测器：
  - 采样率 = 对象的 m_nSampleRate
  - 攻击时间 = 10 mSec
  - 释放时间 = 250 mSec
  - 模拟时间常数 = true
  - 检测 RMS 信号电平
  - 线性，而非对数检测
- 要随时更改任何参数，请使用各个函数：
  - m_Detector.setAttackTime()
  - m_Detector.setReleaseTime()
  - m_Detector.setDetectMode()
  - m_Detector.setTCModeAnalog()

攻击时间和释放时间只是调整这些常用参数。检测模式可以设置为峰值、均方或 RMS。由于 RackAFX 中的音频信号必须在 –1.0 到 +1.0 的范围内，这意味着 MS 和 RMS 模式的平方函数将产生小于瞬时值的值。在 RMS 模式下，均方值会开平方根，这使得生成的包络更小。因此，在使用 MS 和 RMS 模式时需要小心。在这个包络跟随器中，我们将使用 RMS 值来触发我们的动态滤波器。

时间常数决定检测器上升或下降到其最大值（1.0）和最小值（0.0）的速度。在模拟电路中，电阻-电容（RC）的上升和下降时间仅为边沿的 63.3%。在数字系统中，该值通常为 80% 到 99%。包络检测器有一个控件，允许你在非常快速（数字）版本或较慢（模拟）版本之间更改时间常数。我们将在包络跟随器插件中尝试这两种类型。

表 12.5：CEnvelopeDetector 对象定义。

| CEnvelopeDetector |
| --- |
| 功能：实现一个包络检测单元 |
| 成员变量 | 用途 |
| int m_nSample; | 检测器的 z⁻¹ 延迟元素 |
| float m_fAttackTime; float m_fReleaseTime; | 检测器的攻击时间和释放时间（mSec） |
| float m_fSampleRate; | 采样率，用于检测时序 |
| UINT m_uDetectMode; | 根据这些预编码的枚举值设置的检测模式：DETECT_MODE_PEAK = 0 |

