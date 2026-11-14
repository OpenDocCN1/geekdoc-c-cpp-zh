

| 下限 | 0.02 | 下限 | 0 |
|---|---|---|---|
| 上限 | 25 | 上限 | 100 |
| 初始值 | 5 | 初始值 | 50 |

| 按钮属性 | 值 |
|---|---|
| 控件名称 | LFO |
| 单位 | |
| 变量类型 | enum |
| 变量名 | m_uLFO_Waveform |
| 枚举字符串 | sine, saw, tri, square |

| 按钮属性 | 值 |
|---|---|
| 控件名称 | 模式 |
| 单位 | |
| 变量类型 | enum |
| 变量名 | m_uMode |
| 枚举字符串 | Tremolo, Panner |

## TremoloPanner.cpp 文件

颤音增益计算将：

- 将 LFO 样本乘以 depth/100.0。
- 将值 1.0-depth/100.0 加到结果中。

这提供了我们需要的效果映射。

```
float CTremoloPanner::calculateGainFactor(float fLFOSample)
{
    // first multiply the value by depth/100
    // fOutput = fLFOSample*(m_fModDepth/100.0);
    fOutput = fLFOSample*(m_fModDepth/100.0);

    // then add the value (1 - m_fModDepth/100.0)
    fOutput += 1 - m_fModDepth/100.0;

    return fOutput;
}

void CTremoloPanner::calculatePannerGainFactor(float fLFOSample,
    float* pLeftVolume, float* pRightVolume)
{
    // calc sin/cos quadrant location
    float fPan = ((m_fModDepth/100.0)*fLFOSample + 1)*pi/4.0;

    // equal power calculation
    *pLeftVolume = cos(fPan);
    *pRightVolume = sin(fPan);
}
```

### prepareForPlay()

- 初始化 LFO。
- 将 prepareForPlay() 方法转发给 LFO。

```
bool __stdcall CTremoloPanner::prepareForPlay()
{
    // Add your code here:
    m_LFO.m_fFrequency_Hz = m_fModRate;
    m_LFO.m_uPolarity = m_uMode == Panner ? 0 : 1; // 0 - bipolar, 1 - unipolar
    m_LFO.m_uTableMode = 0; // normal, no band limiting
    m_LFO.m_uOscType = m_uLFO_Waveform;
    m_LFO.setSampleRate(m_nSampleRate); // really important!

    // the LFO prepareForPlay() calls reset() and cookFrequency()
    m_LFO.prepareForPlay();

    return true;
}
```

### userInterfaceChange()

- 解码控件索引，并根据需要更新变量。
- 注意：确保检查 nControlIndex 值以匹配您的 GUI。

```
bool __stdcall CTremoloPanner::userInterfaceChange(int nControlIndex)
{
    // decode the control index, or delete the switch and use brute force calls
    // switchInControlIndex
    {
    case 0:
    {
        m_LFO.m_fFrequency_Hz = m_fModRate;
        m_LFO.cookFrequency();
        break;
    }

    // 41: LFO Waveform change
    case 41:
    {
        m_LFO.m_uOscType = m_uLFO_Waveform;
        break;
    }

    case 42:
    {
        if(m_uMode == Panner)
        m_LFO.m_uPolarity = 0; // 0 - bipolar, 1 - unipolar
        else // is tremolo
        m_LFO.m_uPolarity = 1; // 0 - bipolar, 1 - unipolar
        break;
    }
    }
}
```

### processAudioFrame()

- 生成 LFO 值。
- 根据模式计算通道增益值。

在 processAudioFrame() 中，我们需要生成一个新的 LFO 值，计算新的增益因子，然后实现增益函数。

```
bool __stdcall CTremoloPanner::processAudioFrame(float* pInputBuffer,
						float* pOutputBuffer,
						UINT uNumInputChannels,
						UINT uNumOutputChannels)
{
	// Do LEFT (MONO) Channel; there is always at least one input/one output
	float fYn = 0; // normal output
	float fYqn = 0; // quad phase output

	// call the LFO function; we only need first output
	m_LFO.doOscillate(&fYn, &fYqn);

	// setup necessary variables
	float fGnL = 1.0;
	float fGnR = 1.0;
	float fMonoIn = 0.0;

	// branch
	if(m_uMode == Tremolo)
		fGnL = calculateTremoloGainFactor(fYn);
	else // panner sums inputs
	{
		if(uNumInputChannels == 1)
			fMonoIn = pInputBuffer[0];
		else
			fMonoIn = 0.5*(pInputBuffer[0] + pInputBuffer[1]);

		calculatePannerGainFactor(fYn, &fGnL, &fGnR);
	}

	// do MONO (Left) channel
	pOutputBuffer[0] = pInputBuffer[0]*fGnL;

	// Mono-In, Stereo-Out (AUX Effect)
	if(uNumInputChannels == 1 && uNumOutputChannels == 2)
		pOutputBuffer[1] = pOutputBuffer[0]; // just copy

	// Stereo-In, Stereo-Out (INSERT Effect)
	if(uNumInputChannels == 2 && uNumOutputChannels == 2)
	{
		// branch
		if(m_uMode == Tremolo)
		{
			// do right channel, use same gain as left
			pOutputBuffer[1] = pInputBuffer[1]*fGnL;
		}
		else
		{
			// do right channel, its value
			pOutputBuffer[1] = pInputBuffer[1]*fGnR;
		}
	}

	return true;
}
```

构建并测试插件。尝试将 LFO 速率最大值从 20 Hz 提高到 200 或 2 kHz 左右；结果非常有趣。

## 14.2 设计环形调制器插件

环形调制是通过将输入信号与称为载波的正弦波相乘来实现的，如图 14.2 所示。从技术上讲，这是幅度调制或频率混频。结果信号包含信号中每个频率的和频与差频对。例如，如果载波为 250 Hz，输入信号为 1 kHz，则输出将包含两个频率：1 kHz – 250 Hz = 750 Hz 和 1 kHz + 250 Hz = 1.25 kHz。原来的 1 kHz 输入信号消失了。对于复杂音频信号，此过程会对信号包含的每个频率分量发生。结果输出可能与输入完全不同。鼓声会改变音调，全频谱信号会被摧毁。由于存在和频与差频对，当和频信号超出奈奎斯特频率时，会发生混叠。处理混叠的一种方法是像频谱压缩器一样对信号进行分频，仅处理较低频率。虽然这不是完美的解决方案，但至少可以缓解一些混叠问题。此处的环形调制器项目仅实现频率调制，而不解决混叠问题。

### 14.2.1 项目：RingModulator

创建一个项目并将其命名为“RingModulator”。没有其他对象或选项需要添加。

### 14.2.2 RingModulator：GUI

我们需要在表 14.2 中为载波振荡器添加频率和深度控制。深度控制将增加或减少调制量。

![](img/b54974d0a4317ec82d7ae02126d10a6f_471_0.png)

### 图 14.2：环形调制器框图。

### 表 14.2：RingModulator 插件 GUI 控件。

| 滑块属性 | 值 | 滑块属性 | 值 |
|---|---|---|---|
| 控件名称 | 调制频率 | 控件名称 | 调制深度 |
| 单位 | Hz | 单位 | % |
| 变量类型 | float | 变量类型 | float |
| 变量名 | m_fModFrequency | 变量名 | m_fModDepth |
| 下限 | 100 | 下限 | 0 |
| 上限 | 5000 | 上限 | 100 |
| 初始值 | 1000 | 初始值 | 50 |

### 14.2.3 RingModulator.h 文件

我们只需添加一个单波表对象来实现载波振荡器。

```
// Add your code here: ............................ //
// the Carrier Oscillator
CWaveTable m_Oscillator;
// END OF USER CODE ............................ //
```

### 14.2.4 RingModulator.cpp 文件

### prepareForPlay()

- 初始化振荡器。
- 将 prepareForPlay() 方法转发给振荡器。

```
bool __stdcall CRingModulator::prepareForPlay()
{
    // Add your code here:
    m_Oscillator.m_fFrequencyHz = m_fModFrequency;
    m_Oscillator.m_uPolarity = 0; // 0 = bipolar, 1 = unipolar
    m_Oscillator.m_uTableMode = 0; // normal, no band limiting
    m_Oscillator.m_uOscType = 0; // 0 = sin()
    m_Oscillator.setSampleRate(m_nSampleRate); // really important!
    // the prepareForPlay() calls reset() and cookFrequency()
    m_Oscillator.prepareForPlay();
    return true;
}
```

### userInterfaceChange()

- 如果频率滑块移动，更改振荡器频率并调用频率计算函数。
- 深度控制是直接控制变量，因此此处无需处理。

```
bool __stdcall CRingModulator::userInterfaceChange(int nControlIndex)
{
    // decode the control index, or delete the switch and use brute force calls
    switch(nControlIndex)
    {
        case 0:
        {
            m_Oscillator.m_fFrequencyHz -= m_fModFrequency;
            m_Oscillator.cookFrequency();
            break;
        }
        default:
            break;
    }
    return true;
}
```

### processAudioFrame()

- 生成新的载波振荡器值。
- 将输入信号与其相乘。

