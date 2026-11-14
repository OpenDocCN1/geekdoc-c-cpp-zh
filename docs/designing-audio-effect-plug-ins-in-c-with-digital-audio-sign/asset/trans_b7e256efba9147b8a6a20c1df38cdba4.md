

## prepareForPlay()

- 清除 LPF 中的延迟。
- 通过设置初始速率和 LFO 类型来设置 LFO（LFO 类型将与我们的 LFO_waveform 变量匹配）。

```cpp
bool __stdcall CModFilter::prepareForPlay()
{
    // Add your code here:
    //
    // Flush the LPFs
    m_LeftLPF.flushDelays();
    m_RightLPF.flushDelays();
    // now we do NOT need to init the cutoff and Q;
    // these are done in processAudioFrame()

    // setup LFO
    m_fc_LFO.m_Frequency_Hz = m_fModRate_fc;
    m_fc_LFO.m_uPolarity = 1; // 0 = bipolar, 1 = unipolar
    m_fc_LFO.m_uTableMode = 0; // normal, no band limiting
    m_fc_LFO.m_uOscType = m_uLFO_Waveform; // our own variable
    m_fc_LFO.setSampleRate(m_nSampleRate); // really important!

    // the LFO prepareForPlay() calls reset() and cookFrequency()
    m_fc_LFO.prepareForPlay();

    return true;
}
```

## userInterfaceChange()

- 如果用户移动速率滑块，我们需要更改 LFO 速率。
- 如果用户单击单选按钮，我们需要更改 LFO 波形类型。
- 目前，当任何控件移动时，只需重新计算所有内容即可；以后可以精简此过程。

```cpp
bool __stdcall CModFilter::userInterfaceChange(int nControlIndex)
{
    // brute force update all
    m_fc_LFO.m_Frequency_Hz = m_fModRate_fc;
    m_fc_LFO.m_uOscType = m_uLFO_Waveform;
    // cook to calculate
    m_fc_LFO.cookFrequency();

    return true;
}
```

## processAudioFrame()

- 计算新的 LFO 值。
- 使用 LFO 值计算新的 $f_c$ 值。
- 使用 $f_c$ 值计算新的滤波器系数。
- 对输入样本执行双四方运算。

```cpp
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

    // use the LFO value to calculate the updated fc value
    float fc = calculateCutoffFreq(fYn);

    // use the fc value and a preset Q = 2.0
    // to calculate the LPF coefficients for each channel
    calculateLPFCoeffs(fc, 2.0, &m_LeftLPF);
    calculateLPFCoeffs(fc, 2.0, &m_RightLPF);

    // do the BiQuad operation on the Left LPF
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

构建并测试插件。您将听到 LFO 调制的 $f_c$；调整 LFO 速率和深度控件，并尝试更改 LFO 波形类型；三角波和正弦波似乎是最常见的选择，而锯齿波会产生有趣的脉冲效果。

## 12.2 设计调制滤波器插件：第二部分，调制 $f_c$ Q

在第二种设计中，我们将修改当前插件以包含 LPF Q 值的调制。我们将使用第二个独立的 LFO 来调制 Q，但将与 fc LFO 共享相同的 LFO 波形类型。框图如图 12.6 所示。

参数如下：

- fc 调制速率 (0.2 到 10 Hz)
- fc 调制深度 (0 到 100%)
- Q 调制速率 (0.2 到 10 Hz)
- Q 调制深度 (0 到 100%)
- LFO 类型 (正弦, 三角, 锯齿, 方波)
- fc 调制范围：100 Hz 到 5 kHz
- Q 调制范围：0.5 到 10
- LPF 固定为二阶双四方

### 12.2.1 ModFilter GUI

根据表 12.3，为新的 LFO 向用户界面 (UI) 添加更多滑块。

| 滑块属性 | 值 |
|---|---|
| 控件名称 | 调制深度 Q |
| 单位 | % |
| 变量类型 | float |
| 变量名称 | m_fMod_Depth_Q |
| 下限 | 0 |
| 上限 | 100 |
| 初始值 | 50 |

| 滑块属性 | 值 |
|---|---|
| 控件名称 | 调制速率 Q |
| 单位 | Hz |
| 变量类型 | float |
| 变量名称 | m_fModRate_Q |
| 下限 | 0.2 |
| 上限 | 10 |
| 初始值 | 0.5 |

### 12.2.2 ModFilter.h 文件

我们需要添加以下新函数和变量，基本上只是复制 $f_c$ 调制的那些：

- 用于 Q 调制的 LFO 对象
- calculateQ() 用于从 LFO 样本值计算新的 Q 值
- 最小和最大 Q 值

```cpp
// Add your code here: ---------------------------------------------------------------- //
CBiQuad m_LeftLPF;
CBiQuad m_RightLPF;

CWaveTable m_fc_LFO;
CWaveTable m_Q_LFO;

float m_fMinCutoffFreq;
float m_fMaxCutoffFreq;

float m_fMin0;
float m_fMax0;

// functions to calculate the fc or Q for a given LFO sample
float calculateCutoffFreq(float fLFOSample);
float calculateQ(float fLFOSample);

// calculate the coeffs for a given filter
void calculateLPFCoeffs(float fCutoffFreq, float fQ, CBiQuad* pFilter);

// END OF USER CODE ---------------------------------------------------------------- //
```

![](img/b54974d0a4317ec82d7ae02126d10a6f_401_0.png)

### 图 12.6: 带有第二个用于 Q 的 LFO 的调制滤波器。

### 12.2.3 ModFilter.cpp 文件

### 构造函数

- 初始化最小和最大 Q 值。

```cpp
CModFilter::CModFilter()
{
	m_PlugInName = "ModFilter";

	// Default to Stereo Operation:
	// Change this if you want to support more/less channels
	m_uMaxInputChannels = 2;
	m_uMaxOutputChannels = 2;

	// Finish initializations here
	// set our Min and Max Modulation points
	m_fMinCutoffFreq = 100.0;
	m_fMaxCutoffFreq = 5000.0;
	m_fMin0 = 0.577;
	m_fMax0 = 10;
}
```

编写 calculateQ() 函数，其行为与 calculateCutoffFreq() 相同；您只需更改调制深度源以及最小值和最大值：

```cpp
float CModFilter::calculateQ(float fLFOSample)
{
    return (m_fMod_Depth_Q/100.0)*(fLFOSample*(m_fMax0 - m_fMin0)) + m_fMin0;
}
```

### prepareForPlay()

- 通过设置初始速率和 LFO 类型来设置 Q LFO（LFO 类型将与我们的 m_uLFO_Waveform 变量匹配）。

```cpp
bool __stdcall CModFilter::prepareForPlay()
{
    // Add your code here:
    <SNIP SNIP SNIP>

    // the LFO prepareForPlay() calls reset() and cookFrequency()
    m_fc_LFO.prepareForPlay();

    // now do the Q LFO
    m_Q_LFO.m_fFrequency_Hz = m_fModRate_Q;
    m_Q_LFO.m_uPolarity = 1; // 0 = bipolar, 1 = unipolar
    m_Q_LFO.m_uTableMode = 0; // normal, no band limiting
    m_Q_LFO.m_uOscType = m_uLFO_Waveform;
    m_Q_LFO.setSampleRate(m_nSampleRate); // really important!

    // this calls reset() and cookFrequency()
    m_Q_LFO.prepareForPlay();

    return true;
}
```

### userInterfaceChange()

- 当用户更改此值时，更新 Q LFO。

```cpp
bool __stdcall CModFilter::userInterfaceChange(int nControlIndex)
{
    // add your code here:
    // brute force update all
    m_fc_LFO.m_fFrequency_Hz = m_fModRate_fc;
    m_fc_LFO.m_uOscType = m_uLFO_Waveform;

    m_Q_LFO.m_fFrequency_Hz = m_fModRate_Q;
    m_Q_LFO.m_uOscType = m_uLFO_Waveform;

    // cook to calculate
    m_fc_LFO.cookFrequency();
    m_Q_LFO.cookFrequency();

    etc...
}
```

### processAudioFrame()

