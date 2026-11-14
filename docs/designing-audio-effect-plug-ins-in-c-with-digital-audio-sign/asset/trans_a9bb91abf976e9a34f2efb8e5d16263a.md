

bool _stdcall CDDLModule::prepareForPlay()
{
    // setup our delay line
    m_nBufferSize = 2*m_nSampleRate;    // 2 seconds delay @ fs
    // delete it if it exists
    if(m_pBuffer)
    delete [] m_pBuffer;
    // create the new buffer
    m_pBuffer = new float[m_nBufferSize];
    // reset
    resetDelay();
    // then cook variables
    cookVariables();
    return true;
}

processAudioFrame()

- processAudioFrame() 函数的流程图如图 7.25 所示。

注意：还有一个小细节需要处理，当我们以先读后写的方式使用延迟线时就会出现这种情况。如果用户选择了 0.00 mSec 的延迟，那么写指针和读指针将相同。如果用户选择最大延迟值，也会出现这种情况，因为我们希望在写入之前读取最旧的样本。因此，我们需要检查是否根本没有延迟，并相应地处理。

![](img/b54974d0a4317ec82d7ae02126d10a6f_225_0.png)

### 图 7.25：processAudioFrame() 的流程图。

```cpp
bool _stdcall CDDLModule::processAudioFrame(float* pInputBuffer, float* pOutputBuffer,
                UINT uNumInputChannels, UINT uNumOutputChannels)
{
    // SYNC CODE: DO NOT REMOVE - DO NOT PLACE CODE BEFORE IT
    WaitForSingleChange();
    setProcessAudioDone(false);
    // END SYNC CODE

    // Do LEFT (MONO) Channel
    // Read the Input
    float xn = pInputBuffer[0];

    // Read the output of the delay at m_nReadIndex
    float yn = m_pBuffer[m_nReadIndex];

    // if zero delay, just pass the input to output
    if(m_fDelayInSamples == 0)
        yn = xn;

    // write the input to the delay
    m_pBuffer[m_nWriteIndex] = xn + m_fFeedback*yn;

    // create the wet/dry mix and write to the output buffer
    // dry = 1 - wet
    pOutputBuffer[0] = m_fWetLevel*yn + (1.0 - m_fWetLevel)*xn;

    // increment the pointers and wrap if necessary
    m_nWriteIndex++;
    if(m_nWriteIndex >= m_nBufferSize)
        m_nWriteIndex = 0;

    m_nReadIndex++;
    if(m_nReadIndex >= m_nBufferSize)
        m_nReadIndex = 0;

    // Mono-In, Stereo-Out (AUX Effect)
    if(uNumInputChannels == 1 && uNumOutputChannels == 2)
    {
        pOutputBuffer[1] = pOutputBuffer[0]; // copy MONO!
    }

    // DDL Module is MONO - just do a copy here too
    // Stereo-In, Stereo-Out (INSERT Effect)
    if(uNumInputChannels == 2 && uNumOutputChannels == 2)
        pOutputBuffer[1] = pOutputBuffer[0]; // copy MONO!

    // SYNC CODE: DO NOT REMOVE
    setProcessAudioDone();

    return true;
}
```

在 RackAFX 中构建并测试模块，以确保其正常工作。您应该能获得一个通用的延迟效果，延迟时间最长可达两秒。要完成模块的第一个版本，我们只需处理两个事项。第一个很简单：我们需要为模块用户提供一种选择外部反馈并访问反馈变量的方法。第二个更困难：我们需要能够处理分数延迟。

为了让某人在另一个插件内部使用此模块并访问反馈路径，我们需要提供一些仅由插件父级调用的函数。我们还需要修改 processAudioFrame() 函数，以使用外部提供的反馈样本。

## 7.4 修改模块以供父插件使用

实际上，将此模块修改为插件的内部模块非常简单。我们需要提供一个反馈样本变量，并允许用户设置该值。我们还需要提供一种方法，允许用户获取当前反馈值。最后，我们需要一个开关，允许用户选择外部反馈模式。该开关将以布尔标志的形式存在。在设置好变量后，我们可以修改 processAudioFrame() 函数以使用外部反馈样本。

### 7.4.1 DDLModule.h 文件

声明以下新变量：

```
bool m_bUseExternalFeedback; // flag for enabling/disabling
float m_fFeedbackIn; // the user supplied feedback sample value
```

此外，声明并实现 get/set 函数。它们非常简短，您可以直接将它们放在 .h 文件中，而不是在 .cpp 文件中实现。

```
// Add your code here: ------------------------------------------------------ //
float m_fDelayInSamples;
float m_feedback;
float m_fWetLevel;
void cookVariables();
void resetDelayline();
float* m_pBuffer;
int m_nReadIndex;
int m_nWriteIndex;
int m_nBufferSize;
bool m_bUseExternalFeedback; // flag for enabling/disabling
float m_fFeedbackIn; // the user supplied feedback sample value
// current FB is fb*output
float getCurrentFeedbackOutput() { return m_feedback * m_pBuffer[m_nReadIndex]; }
// set the feedback sample
void setCurrentFeedbackInput(float f) { m_fFeedbackIn = f; }
// enable/disable external FB source
void setUseExternalFeedback(bool b) { m_bUseExternalFeedback = b; }
// END OF USER CODE ------------------------------------------------------ //
```

当前反馈样本输出位于 m_pBuffer[m_nReadIndex]，并根据框图乘以反馈系数。通过允许用户获取和设置反馈，我们允许他们介入循环并插入其他效果，或者将反馈输出用于其他任何目的。

### 7.4.2 DDLModule.cpp 文件

processAudioFrame()

- 修改函数以允许使用外部提供的反馈样本：

```cpp
bool _stdcall CDDLModule::processAudioFrame(float* pInputBuffer, float* pOutputBuffer,
UINT uNumInputChannels, UINT uNumOutputChannels)
{
    // Do LEFT (MONO) Channel
    // Read the Input
    float xn = pInputBuffer[0];

    // Read the output of the delay at m_nReadIndex
    float yn = m_pBuffer[m_nReadIndex];

    // if zero delay, just pass the input to output
    if(m_fDelayInSamples == 0)
        yn = xn;

    // write the input to the delay
    if(!m_bUseExternalFeedback)
        m_pBuffer[m_nWriteIndex] = xn + m_fFeedback*yn; // normal
    else
        m_pBuffer[m_nWriteIndex] = xn + m_fFeedbackIn; // external feedback

    // create the wet/dry mix and write to the output buffer
    // dry = 1 - wet
    pOutputBuffer[0] = m_fWetLevel*yn + (1.0 - m_fWetLevel)*xn;

    etc...
}
```

您可以看到所需的更改非常微小——只是一个用于更改反馈样本值的开关。当然，如果用户启用此选项，则他们有责任在 fFeedbackIn 变量中放置有意义的数据。

重新构建并测试代码，以确保其仍能正常工作。在下一节中，我们将使用该模块制作两个不同的插件：

- 1. 立体声数字延迟
- 2. 立体声交叉反馈延迟

## 7.5 修改模块以实现分数延迟

在着手更大的项目之前，我们需要解决分数延迟的问题。我们希望用户能够获得任意长度的延迟。通过仅实现基于样本的延迟，我们将用户限制在选择采样周期整数倍的延迟，约为 23 uSec。您可能认为这已经足够准确；然而，有几种情况这还不够。第一种情况是延迟与每分钟节拍数（BPM）同步的情况（例如，将延迟设置为歌曲 BPM 的倍数，以创建同步的回声或打击效果）。第二种情况是合唱和弗兰杰等调制延迟，它们需要从一个延迟时间平滑调制到另一个延迟时间。线性插值将提供可接受的结果。

假设我们的延迟处于这样一种状态：我们已将延迟位置计算为样本位置 23.7183 个样本。我们需要找到样本 23 和样本 24 之间 0.7183 位置处的数据值。在图 7.26 中，您可以看到插值方法的图形表示。由于它是线性插值，一条线在相邻样本之间绘制，插值位于两个样本之间 0.7183 的距离处的线上。

在多项式插值中，例如拉格朗日插值，一条曲线在点（或一系列点）之间绘制，然后插值位于该曲线上。有几种方法可以

