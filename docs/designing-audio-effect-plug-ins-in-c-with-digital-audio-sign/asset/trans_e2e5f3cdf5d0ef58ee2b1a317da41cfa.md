

混叠，是故意的。然后，我们将探讨一种合成常见信号而不产生混叠的方法。唯一不会混叠的有意义信号是正弦波，所以我们可以从这里开始。

## 9.5 设计波表振荡器插件

要编写波表振荡器，你需要创建一个数据表并在构造函数中对其进行初始化。inc 使用浮点索引值，并将跟踪当前读取位置。将使用线性插值从表中提取样本。只要振荡器处于激活状态，循环缓冲区就会运行。因此，我们需要从与直接形式振荡器相似的插件设计开始。我们可以使用可分配按钮来触发振荡器以模拟 MIDI 记音开和记音关消息，并可以提供一个滑块用于频率控制。

### 9.5.1 项目：WTOscillator

创建一个新的 RackAFX 项目，并确保勾选合成器插件框（如果忘记了，以后随时可以更改）。

### 9.5.2 WTOscillator GUI

最终 GUI 将具有频率控制以及用于波形、模式和极性的多个单选按钮控件。最终，它将具有图 9.10 所示的控件。

![](img/b54974d0a4317ec82d7ae02126d10a6f_290_0.png)

**图 9.10：** 最终的 WTOscillator GUI。

**表 9.2：** 波表振荡器插件的 GUI 控件。

| 滑块属性 | 值 |
|---|---|
| 控件名称 | 频率 |
| 单位 | Hz |
| 变量类型 | float |
| 变量名 | m_fFrequency_Hz |
| 下限 | 25 |
| 上限 | 4200 |
| 初始值 | 440 |

首先，向 UI 添加一个频率滑块，并将其连接到名为 m_fFrequency_Hz 的变量，限制为 25 Hz 到 4.2 kHz，初始设置为 440 Hz（表 9.2）。选择这些限制是因为它们接近标准（88 键）钢琴或合成器上音符的低和高基频。接下来，设置可分配按钮以创建启动和停止功能，就像你为 DirectOscillator 插件所做的那样。

### 9.5.3 WTOscillator.h 文件

声明实现振荡器所需的变量：

```
// Add your code here:
// --------------------------------------------------------------- //
// Array for the Table
float m_SinArray[1024]; // 1024 Point Sinusoid

// current read location
float m_fReadIndex; // NOTE its a FLOAT!

// reset the read index
void reset()
{
    m_fReadIndex = 0.0;
}

// our inc value
float m_f_inc;

// our cooking function
void cookFrequency();

// our note on/off message
bool m_bNoteOn;

// END OF USER CODE --------------------------------------------------------------- //
```

可以看出，我们添加了必要的元素（数组、读取索引、inc、记音开/关），以及两个函数：

- cookFrequency() 用于在频率变化时更新 inc 值。
- reset()，它只是将读取索引重新定位到缓冲区顶部。

### 9.5.4 WTOscillator.cpp 文件

### 构造函数

- 通过设置在 .h 文件中声明的标志来关闭振荡器。

```
CWTOscillator::CWTOscillator()
{
    <SNIP SNIP SNIP>
    // Finish initializations here
    // setup array
    for(int i = 0; i < 1024; i++)
    {
        // sample the sinusoid, 1024 points
        // sin(wt) = sin(2pi*t/1024)
        m_SinArray[i] = sin( (float)i/1024.0)*(2*pi) );
    }

    // clear variables
    m_fReadIndex = 0.0;
    m_f_inc = 0.0;

    // silent
    m_bNoteOn = false;

    // initialize inc
    cookFrequency();
}
```

在构造函数中，你设置标志并通过对 1024 个点进行采样来设置波表。此版本设置为生成我们想要的一个周期减一个样本的波形。编写烹饪函数：

```
void CWTOscillator::cookFrequency()
{
    // inc = L*fd/fs
    m_f_inc = 1024.0*m_fFrequency_Hz/(float)m_nSampleRate;
}
```

### prepareForPlay()

- 重置振荡器。
- 更新变量。

```
bool __stdcall CWTOscillator::prepareForPlay()
{
    // Add your code here:
    // reset the index
    reset();

    // cook current frequency
    cookFrequency();

    return true;
}
```

### userInterfaceChange()

- 处理滑块控件以更新变量。
- 处理启动/停止按钮以打开/关闭标志，并在打开时更新变量。
- 确保你的 nControlIndex 变量与 GUI 控件匹配。

```
bool __stdcall CWTOscillator::userInterfaceChange(int nControlIndex)
{
    // add your code here
    switch(nControlIndex)
    {
    case 0:
        cookFrequency();
        break;

    // note on
    case 50:
        reset();
        cookFrequency();
        m_bNoteOn = true;
        break;

    // note off
    case 51:
        m_bNoteOn = false;
        break;

    default:
        break;
    }
    return true;
}
```

### processAudioFrame()

- 实现表查找。
- 请注意，与延迟线一样，我们将插值点的参考框架移动到 n = 0 和 n = 1 之间，然后仅使用 frac 组件来查找样本之间的值。

```
bool __stdcall CWTOscillator::processAudioFrame(float* pInputBuffer, float* pOutputBuffer, UINT uNumInputChannels, UINT uNumOutputChannels)
{
    // Do LEFT (MONO) Channel
    // if not running, write 0s and bail
    if(!m_bNoteOn)
    {
        pOutputBuffer[0] = 0.0;

        // Mono-In, Stereo-Out (AUX Effect)
        if(uNumInputChannels == 1 && uNumOutputChannels == 2)
            pOutputBuffer[1] = 0.0;

        // Stereo-In, Stereo-Out (INSERT Effect)
        if(uNumInputChannels == 2 && uNumOutputChannels == 2)
            pOutputBuffer[1] = 0.0;

        return true;
    }

    // our output value for this cycle
    float fOutputSample = 0;

    // get INT part
    int nReadIndex = (int)m_fReadIndex;

    // get FRAC part
    float fFrac = m_fReadIndex - nReadIndex;

// setup second index for interpolation; wrap the buffer if needed
int nReadIndexNext = nReadIndex + 1 > 1023 ? 0 : nReadIndex + 1;
// interpolate that output (x1,x2,y1,y2,frac) - notice the way we set x1 and x2
// to 0 and 1, then only use the frac value while nReadIndex and nReadIndexNext
// acquire the values from the table
fOutputSample = dLinTerp(0, 1, m_SinArray[nReadIndex], m_SinArray[nReadIndexNext],
                      fFrac);
// add the increment for next time
m_fReadIndex += m_f_inc;
// check for wrap
if(m_fReadIndex > 1024)
    m_fReadIndex -= m_fReadIndex - 1024;
// write out
pOutputBuffer[0] = fOutputSample;
// Mono-In, Stereo-Out (AUX Effect)
if(uNumInputChannels == 1 && uNumOutputChannels == 2)
    pOutputBuffer[1] = fOutputSample;
// Stereo-In, Stereo-Out (INSERT Effect)
if(uNumInputChannels == 2 && uNumOutputChannels == 2)
    pOutputBuffer[1] = fOutputSample;
}
return true;
}
```

构建并运行振荡器，使用分析器窗口检查音调。使用滑块调整振荡频率。如果需要，可以添加一个音量控制滑块。

## 9.6 添加更多波表

正弦振荡器很有趣，但你可以实现任何想要的表类型。你会发现添加更多表实际上很容易，因为它们都使用相同的振荡频率方程。在本节中，我们将添加以下表类型：

- 锯齿波
- 三角波
- 方波

这三种波形在离散时间系统中数学上尽可能接近，但播放时会产生混叠。然而，我们仍然想要实现它们，因为我们可以将波表振荡器用作 LFO（低频振荡器）来用于即将到来的效果，如合唱和弗兰杰。要添加更多表，我们需要执行以下操作：

- 添加更多数组来存储表。
- 在构造函数中初始化数组。
- 为用户提供一种切换振荡器类型的方法。

### 9.6.1 WTOscillator.h 文件

从 .h 文件中的新数组开始：

```
// Add your code here: ----------------------------------------------------------------
// Array for the Table
float m_SinArray[1024]; // 1024 Point Sinusoid
float m_SawtoothArray[1024]; // saw
float m_TriangleArray[1024]; // tri
float m_SquareArray[1024]; // sqr

// current read location
float m_fReadIndex; // NOTE its a FLOAT!
```

### 9.6.2 WTOscillator.cpp 文件

### 构造函数

- 这三个新波表将像正弦表一样是双极的，并在 –1.0 到 +1.0 之间摆动，并且它们都将以第一个样本 = 0.0 开始。

```
CWTOscillator::CWTOscillator()
{
    m_PlugInName = "WTOscillator";

    // set our oscillator flag:
    this->m_bOutputOnlyPlugIn = true;

    // slope and y-intercept values for the
    // Triangle Wave
    // rising edge1:
    float mt1 = 1.0/256.0;
    float bt1 = 0.0;

    // rising edge2:
    float mt2 = 1.0/256.0;
    float bt2 = -1.0;

    // falling edge:
    float mtf2 = -2.0/512.0;
    float btf2 = +1.0;

    // Sawtooth
    // rising edge1:
    float ms1 = 1.0/512.0;
    float bs1 = 0.0;

    // rising edge2:
    float ms2 = 1.0/512.0;
    float bs2 = -1.0;
```

