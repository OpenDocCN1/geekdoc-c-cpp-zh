
```cpp
    }

    // --- 获取单位频率

    double dUnityFrequency = m_bSingleCycleSample ?

    (m_SampleRate / pSample->uNumChannels) :

    m_SampleRate / pSample->m_MIDINote;

    // 等效长度

    double dLength = m_SampleRate / dUnityFrequency;

    // 计算增量

    // inc = fs

    m_dInc *= dLength;

}
```

## `reset()`

该函数简单的清除输出变量并将读取索引重置为0（缓冲区顶部）。

```cpp
void CSampleOscillator::reset()
{
    // --- 首先调用基类
    CSampleOscillator::reset();
    // --- 清除输出
    m_dLeftOutputSample = 0.0;
    m_dRightOutputSample = 0.0;
    // --- 重置索引到缓冲区顶部（地址 0）
    m_dReadIndex = 0.0;
    // 更新
    update();
}
```

## `startOscillator()` 和 `stopOscillator()`

与所有振荡器相同——只需设置/清除标记并在需要时调用 `reset()`。

## `addWaveSample()`

这是一个简化文件遍历的辅助函数；它只需使用提供的文件路径创建对象并将指针添加到数组中。如果 `nMIDINoteNumber` 为 -1，则没有 MIDI 符号信息。

```cpp
bool CSampleOscillator::addWaveSample(char* pSamplePath, int nMIDINoteNumber)
{
    // --- 创建新对象
    WaveData* pSample = new WaveData(pSamplePath);
    // --- 有 MIDI 符号吗？
    if(pSample && nMIDINoteNumber < 0)
        nMIDINoteNumber = pSample->m_MIDINote;
    // --- 添加到波表
    m_WaveSamplePtrArray[nMIDINoteNumber] = pSample;
    return true;
}
```

## `getNumChannels()` 和 `getMIDINote()` 以及 `samplesLoaded()`

这些是自言自明的；新的 `SynthVoice` 对象将使用它们进行查询。

## `initWithFilePath`

此函数使用新创建的 `WaveData` 对象初始化 `m_pWaveSample` 指针。它还清除共享数据标记。

```cpp
bool CSampleOscillator::initWithFilePath(char* pSamplePath)
{
    // --- 如果已则销毁
    if(m_pWaveSample)
      delete m_pWaveSample;
    // -- 创建新对象
    m_pWaveSample = new WaveData(pSamplePath);
    // --- 我们找到样本了吗？
    if(!m_pWaveSample->m_bWaveLoaded)
      delete m_pWaveSample;
      m_pWaveSample = NULL;
      return false;
    // -- 如果我们刚刚创建它
    m_bWaveSample = false;
    return true;
}
```

## `initWithFolderPath`

此函数使用整个文件夹的 `.wav` 文件初始化波形数据数组，并实现设置数组的过程。定位文件的细节是特定于系统的，此处已移除以便阅读。注意我们将数组指针存储在另一个想要共享的对象中。

```cpp
bool CSampleOscillator::initWithFolderPath(char* pSampleFolderPath)
{
    // 清除掉
    if(!m_bSharedSampleArray)
      WaveData* pSample = NULL;
      WaveData* pDeletedSample = NULL;
for(int i=0; i<127; i++)
    {
        if(m_WaveSamplePtrArray[i]) {
            pSample = m_WaveSamplePtrArray[i];
            if(pSample != pDeletedSample)
            {
                pDeletedSample = pSample;
                delete pSample;
            }
            m_WaveSamplePtrArray[i] = NULL;
        }
    }
    // --- 现在遍历文件夹中的 .wav 文件
for(). {
    // 调用子函数添加文件
    if(success) addWaveSample(path);
    // 删除路径
    delete [] path;
}
}
```

```cpp
bool CSampleOscillator::setWaveDataPtr(CWaveData* pWaveData)
{
  // --- 是否有样本？
  if(!pWaveData)
    return false;
  // --- 仅拷贝指针
  m_pWaveSample = pWaveData;
  // --- 我们正在共享，所以设置标志位
  m_bSharedWaveSample = true;
  return true;
}
```

## `setWaveSamplePtrArray()`

此函数为多样本设置数组——它拷贝新的数据指针并将共享标志位设为 true。

```cpp
bool CSampleOscillator::setWaveSamplePtrArray(CWaveData** ppWaveSamplePtrArray)
{
  // --- 测试
  if(!ppWaveSamplePtrArray)
    return false;
  // --- 仅拷贝它
  m_pWaveSamplePtrArray = ppWaveSamplePtrArray;
  // --- 标志位防止我们删除
  m_bSharedWaveSamplePtrArray = true;
  return true;
}
```

## `readSampleBuffer()`

此函数从波形数据缓冲区读取并插值样本。它处理单声道和立体声缓冲区，并使用了你在 `CWaveTable` 对象中看到的相同技术。其核心操作上几乎完全相同。对于单声道，它将左通道写入右输出。你会发现此函数主要处理索引和计数工作，并将缓冲区视为波形查找表。

## `doOscillate()`

渲染函数使用了上述辅助函数，该函数处理了读取和插值音频数据的细节。`doOscillate()` 函数主要处理读取索引值的封装和循环。它在持续循环模式（sustain loop mode）下起始和结束循环值。对于单次（one-shot）模式，样本通过一次后，读取索引被设置为 -1；这是退出函数并返回我们清除的 0.0 样本的标志。在持续模式下，循环模式被处理为单次模式。

```cpp
void CSampleOscillator::readSampleBuffer(CWaveData* pWaveSample,
    double dReadIndex, double dinc,
    double dLeftSample,
    double dRightSample)
{
    // 波形表读取：从左通道开始
    int nReadIndex = (int)dReadIndex;
    // 获取分数部分
    float ffrac = dReadIndex - nReadIndex;
    // 单声道或立体声文件：目前仅支持这两种
    if(pWaveSample->m_NumChannels == 1) {
        // 设置用于插值的第二个索引；
        // 如果需要则循环缓冲区
        int nReadIndexNext = nReadIndex + 1;
        pWaveSample->m_sampleCount > 0 ? nReadIndex + 1 : 0;
        // 在两者之间进行插值
        dLeftSample = dInterp(0, 1, pWaveSample->m_pWaveBuffer[nReadIndex], pWaveSample->m_pWaveBuffer[nReadIndexNext], ffrac);
        dRightSample = dLeftSample;
        // 下次使用的增量
        dReadIndex += dinc;
    } else if(pWaveSample->m_NumChannels == 2) {
        // 跨交错缓冲区进行插值！
        int nReadIndexLeft = (int)dReadIndex * 2;
        // 设置用于插值的第二个索引；
        // 如果需要则循环缓冲区，我们知道最后一个样本是右通道
        // 所以重置为顶部（?? 之后的 0）
        int nReadIndexNextLeft = nReadIndexLeft + 2;
        pWaveSample->m_sampleCount > 0 ? nReadIndexLeft + 2 : 0;
        // 在两者之间进行插值
        dLeftSample = dInterp(0, 1, pWaveSample->m_pWaveBuffer[nReadIndexLeft], pWaveSample->m_pWaveBuffer[nReadIndexNextLeft], ffrac);
        // 处理右通道
        int nReadIndexRight = nReadIndexLeft + 1;
        // 找到下一个，跳过。
    }
}
```

在循环模式下，封装代码的工作与 `CWaveTable` 对象类似。在持续模式下，读取索引使用循环起始和结束点计算，当你移动到结束循环样本之外时会发生相位偏移，逻辑如下：

```cpp
// 注意封装跳转索引从 1 --> 1
int nReadIndexNextRight = nReadIndexRight + 2 > pWaveSample->m_sampleCount - 1 ? 1 : nReadIndexRight + 2;
// 在两者之间进行插值
dRightSample = dInterp(0, 1, pWaveSample->m_pWaveBuffer[nReadIndexRight], pWaveSample->m_pWaveBuffer[nReadIndexNextRight], ffrac);
// 下次使用的增量
dReadIndex += dinc;
if (dReadIndex > (double)(pSample->m_uLoopIndex)/dChannels)
```

## 10.7 音频文件位置

基于样本的合成器需要单个样本或文件夹，插件需要知道这些文件的所在位置。一些选项包括硬编码位置、使用安装程序将位置写入注册表，或使用其他方法让 DLL 知道文件位置。解决此问题的一种无需注册文件的简单方法是将文件放置在与 DLL（或组件）相同的目录中，或者放在该文件夹的子目录中。这种方法在 Windows 和 MacOS 中都适用，你可以查询操作系统获取应用程序的位置。所有基于样本的合成器将使用 DLL 或组件因子来存储样本。样本本身位于名为 `/Samples` 和 `/MultiSamples` 的子目录中。寻找 DLL/组件因子的方法是打开软件并使用文件夹放置：

- RackAFX;
- VST3;
- AU: `~Library/Audio/Plug-Ins/Components`

```cpp
CPlugin::getMyDLLDirectory(), 位于 Plugin.cpp
VSTSynth::getMyDLLDirectory(), 位于 VSTSynth.h
```

## AU;

`getMyComponentDirectory()` 在 `AUSynth` 顶部全局声明。

```cpp
double CSampleOscillator::dooscillate(double dOutput)
{
    // 清除样本
    m_dleftSample = 0.0;
    m_dRightSample = 0.0;
    if(pOutput) *pOutput = 0.0;
}
```

## 单样本示例

这是一个使用单声道 `Fuzz.wav` 初始化 `CSampleOscillator` 的示例。单声道位于 `Samples` 目录。

```cpp
// 获取指针
WaveData* pSample = m_pWaveSample;
if(m_pSamplePtrArray[m_uNumber]);
```

## RackAFX

注意 `addStrings()` 的使用；这是你在第 3 章中看到的单声道事件。你必须处理 `addStrings()` 返回的字符串。

```cpp
// 获取路径
char* pPath = addStrings(getMyDLLDirectory(), UString("\\Samples"));
```

## VST3

在 VST3 中，函数需要你传递插件名称，然后像 `RackAFX` 一样使用 `addStrings()`。

```cpp
// 获取路径
char* pPath = getMyDLLDirectory(UString("DigiSynth.vst"));
```

```cpp
if(dReadIndex > (double)(pSample->m_uLoopIndex)/dChannels)
    m_dReadIndex = dReadIndex - (double)(pSample->m_uLoopIndex)/dChannels + (double)(pSample->m_uStartIndex);
}
else if(m_loopMode == loop) // 使用结束-开始样本
{
    if(m_dReadIndex > (double)(pSample->m_sampleCount - dChannels - 1)/dChannels)
        m_dReadIndex = 0.0;
}
else if(m_loopMode == oneshot) // 读取索引 -1 标志
{
    if(m_dReadIndex > (double)(pSample->m_sampleCount - dChannels - 1)/dChannels)
        m_dReadIndex = -1;
}
}
// 无循环计数，将持续模式处理为单次
if(pSample->m_uLoopCount == 0)
{
    if(m_loopMode == oneshot || m_loopMode == sustain)
    {
        if(m_dReadIndex > (double)(pSample->m_sampleCount - dChannels - 1)/dChannels)
            m_dReadIndex = -1;
    }
else if(m_loopMode == loop)
    {
        if(m_dReadIndex > (double)(pSample->m_sampleCount - dChannels - 1)/dChannels)
            m_dReadIndex = 0.0;
    }
}
// 输出到输出
if(m_pModulationMatrix)
{
    // // 将我们的输出写入目标
    m_pModulationMatrix->m_dSources[m_uModDestOutput] = m_dleftSample*m_Amplitude*m_dAmp;
    // // CSampleOscillator 是立体声的
    m_pModulationMatrix->m_dSources[m_uModDestOutput] = m_dRightOutputSample*m_Amplitude*m_dAmp;
}
```

```cpp
// --- aux 是右输出
if(pAuxOutput)
    *pAuxOutput = m_dRightOutputSample*m_dAmplitude*m_dAmpMod;
// -- 独立模式使用
    return m_dLeftOutputSample*m_dAmplitude*m_dAmpMod;
```

```cpp
char* pPath =
addStrings(pDLLPath,\"Samples\FuzzVibeAl.wav");
```

# AU
