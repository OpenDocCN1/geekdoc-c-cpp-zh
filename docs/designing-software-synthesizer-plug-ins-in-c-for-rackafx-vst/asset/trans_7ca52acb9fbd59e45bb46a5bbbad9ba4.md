

```cpp
{
< 解码采样器索引 >

// --- 调用初始化函数
if(p0sc) {
    ((CSampleOscillator*)p0sc)->m_bSingleCycleSample = -bSingleCycleSample;

    ((CSampleOscillator*)p0sc)->m_bPitchlessSample = -bPitchlessSample;
    return ((CSampleOscillator*)p0sc)->initWithFolderPath(pPath);
}

return false;
}
```

以下内容与 MiniSynth（以及书中的其他项目）相同，区别在于声部数组中创建和存储的声部指针类型。

- 析构函数 destructor 
- Reset()
- Render()
- StartNote()
- StopNote()
- HandlePitchWheel()
- HandleControlChange()

## 构造函数 Constructor
初始化工厂预设（可选）以及表 10.6 中的所有变量；其余部分与 MiniSynth 相同。

## loadSamples()
在 .cpp 文件中任何你希望的地方插入代码。

## Initialize()
`Initialize()` 与 MiniSynth 的区别在于增加了对 `loadSamples()` 的调用。

## update()
另一个区别在于 `update()` 函数，它仅略有不同，因为删除了一些控件并添加了其他。此外，现在有两个滤波器需要处理。

```cpp
inline bool initSynthVoice(CDigiSynthVoice* pVoice, bool bSingleCycleSample, bool bPitchlessSample);
```

```cpp
if (pVoice->getWaveData(0))
    ((CSampleOscillator*)m_p0sc1)->setWaveData(pVoice->getWaveData(0));
if (pVoice->getWavePtrArray(0))
    ((CSampleOscillator*)m_p0sc1)->setWavePtrArray(0);
```
<SNIP - 采样器部分相同>

```cpp
if (m_p0sc1)
    ((CSampleOscillator*)m_p0sc1)->m_bSingleCycleSample = bSingleCycleSample;
    ((CSampleOscillator*)m_p0sc1)->m_bPitchlessSample = bPitchlessSample;
```
<SNIP - 采样器部分相同>

```cpp
return true;
```

```cpp
inline virtual bool doVoice(double& dLeftOutput, double& dRightOutput)
```

```cpp
// 此处执行基础的开关工作
if(!this::doVoice(dLeftOutput, dRightOutput))
    return false;
```

```cpp
// --- 调制块 //
// 层 0 调制器：速度->攻击，音符->衰减
m_ModulationMatrix.doModulationMatrix(0);
```

```cpp
// --- 更新层 1 调制器
m_EG1.update();
m_LF01.update();

// --- 执行层 1 调制器
m_EG1.update();
m_LF01.update();

// --- 调制矩阵 层 1
m_ModulationMatrix.doModulationMatrix(1);

// --- 更新声部、DCA 和滤波器
this->update();
m_DCA.update();
m_LeftSEMFilter.update();
m_RightSEMFilter.update();

// --- 更新采样器
m_Osc1.update();
m_Osc2.update();
```

```cpp
// --- 数字音频引擎 //
double dLeftAccum = 0.0;
double dRightAccum = 0.0;
double dLeft1 = 0.0;
double dRight1 = 0.0;
double dLeft2 = 0.0;
double dRight2 = 0.0;

// --- 检查速度和分离
if(m_pGlobalVoiceParams->uVoiceMode == Osc1)
    dLeftAccum = m_Osc1.oscillate(&dRightAccum);
else if(m_pGlobalVoiceParams->uVoiceMode == Osc2)
    dLeftAccum = m_Osc2.oscillate(&dRightAccum);
else if(m_pGlobalVoiceParams->uVoiceMode == split)
{
  bool osc0n = getWaveData(0);
  bool osc2n = inWaveData(1);

  dLeft1 = m_Osc1.oscillate(&dRight1);
  dLeft2 = m_Osc2.oscillate(&dRight2);

  ```cpp
    ((CSampleOscillator*)m_p0sc1)->m_bSingleCycleSample = bSingleCycleSample;
    ((CSampleOscillator*)m_p0sc1)->m_bPitchlessSample = bPitchlessSample;
  ```
  <SNIP - 采样器部分相同>
```*(注：此处根据原文逻辑翻译，内部代码块保持原样，仅翻译注释)*
}

```cpp
// --- 应用滤波器
dLeftOutput = m_LeftSEMFilter.doFilter(dLeftAccum);
dRightOutput = m_RightSEMFilter.doFilter(dRightAccum);

// --- 应用 DCA
m_DCA.doDCA(dLeftOutput, dRightOutput, dLeftOutput, dRightOutput, dRightOutput);

return true;
```

该函数仅**加粗**了新添加的代码。

从 MiniSynth 中移除了：
- 脉宽
- 对采样器 3 (sub osc) 和采样器 4 (noise) 的所有引用

新增：
- Osc1 输出 (dB)
- Osc2 输出 (dB)
- 循环模式 Loop

在你选择的平台上构建并测试 DigiSynth。你会发现合成器核心部分大部分与 MiniSynth 相同。尝试任何其他的采样集、循环和单采样文件。

## 10.14 挑战

| DCA.h | SEMFilter.h |
| DCA.cpp | SEMFilter.cpp |
| EnvelopeGenerator.h | Oscillator.h |
| EnvelopeGenerator.cpp | Oscillator.cpp |
| Filter.h | SampleOscillator.h |
| Filter.cpp | SampleOscillator.cpp |
| LFO.h | synth.h |
| LFO.cpp | VAOPoleFilter.h |
| DigiSynth.h | VAOPoleFilter.cpp |
| DigiSynth.cpp | Voice.h |
| ModulationMatrix.h | Voice.cpp |
| ModulationMatrix.cpp | Voice.cpp |

