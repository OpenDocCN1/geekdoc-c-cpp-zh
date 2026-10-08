

## CminiSynth 成员变量

| 类型 | 变量名 | 说明 |
| --- | --- | --- |
| QBLimitedOscillator | m_Osc1 | 振荡器 1 |
| QBLimitedOscillator | m_Osc2 | 振荡器 2 |
| QBLimitedOscillator | m_Osc3 | 振荡器 3 (子模块) |
| QBLimitedOscillator | m_Osc4 | 振荡器 4 (噪声) |
| CMogLadderFilter | m_MoogLadderFilter | 低滤波器 |
| UINT | m_uOscForRatio | 硬同步；调制矩阵中的比例索引 |
| enum | Saw3,Sqr3,Saw2,Sqr2,TriSaw,Tri2 | 此处重复音色字符串为了方便编码 |

## CminiSynthVoice 成员函数

| 函数名 | | |
| --- | --- |
| initGlobalParameters | 使用其全局参数结构设置所有子组件 |
| initializeModMatrix | 设置所有音色调制程序 |
| setSampleRate | 将采样率分发给所有子组件 |
| prepareForPlay | 一次初始化；在子组件指针设置后发生（即在派生类构造之后） |
| update | 更新新的音色参数 |
| reset | 重置所有子组件 |
| doVoice | 执行 MiniSynth 特定的渲染 |

```
// --- filters
m_pFilter1 = &m_MoogLadderFilter;
m_pFilter2 = NULL;

// ---  NLP 实验
m_MoogLadderFilter.m_uUNLP = OFF;
// --- 用于 MoOG 中的带通增益补偿；可以用户调节
m_MoogLadderFilter.m_dAuxControl = 0.75;

// --- 音色模式 0
m_osc1.m_Uwaveform = SAW1;
m_osc2.m_Uwaveform = SAW1;
m_osc3.m_Uwaveform = SAW1;
m_osc4.m_Uwaveform = NOISE;

// 2) --- 设置任何组件特定的内容
m_EG1.setEGMode(analog);
m_EG1.m_bOutputEG = true; // --- 我们的 DCA EG

// --- DCA 设置：在此处设置源 EG
m_DCA.m_uModSourceEG = DEST_DCA_EG;
```

- 当一个音符被触发时，音色对象将 m_uTimeStamp 设置为零

```cpp
inline virtual void initGlobalParameters(globalSynthParams* pGlobalParams)
{
    // --- 始终调用基类
    CVoice::initGlobalParameters(pGlobalParams);

    // 在此处添加任何 CThis 特定的变量
    // (你首先需要将它们添加到全局参数结构中)
    // 如果用户没有这些它们的 GUI 控制，则这些值默认为 1.0
    // 注意：我们只设置了在该音色中使用的强度
m_pVoiceParameters->dLF01scModIntensity = 1.0;
m_globalVoiceParameters->dLF01Filter1ModIntensity = 1.0;
m_globalVoiceParameters->dLF01Filter2ModIntensity = 1.0;
m_globalVoiceParameters->dLF01DCAPanModIntensity = 1.0;
m_globalVoiceParameters->dLF01DCAmpModIntensity = 1.0;
m_globalVoiceParameters->dEG01scModIntensity = 1.0;
m_globalVoiceParameters->dEG01Filter1ModIntensity = 1.0;
m_globalVoiceParameters->dEG01Filter2ModIntensity = 1.0;
m_globalVoiceParameters->dEG1DCAmpModIntensity = 1.0;
}
```

- 然后，插件增加所有音色上时间戳变量的值，包括刚刚触发的那一个
- 时间戳最高的音色正在播放最旧的音符
- m_bNote 标志用于标识音符是否开启，在音符被重新触发之前，不需要清除时间戳

在插件的 .file 文件中，你将声明音色数组和三个辅助函数。`update()` 函数的工作方式与 NanoSynth 相同，所有未来的合成器都将使用它。你还需要声明用于滑音（portamento）和 MIDI 接收通道的最后一个符频率变量，以及未来的所有变量。

这三个辅助函数的实现对于所有合成器都是相同的，除了数组中音色指针的类型。这些函数都非常简单且自解释性强。它们要么增加时间戳，要么检查并比较时间戳与 MIDI 音符号。

## 初始化和设置音色

初始化是在 RackAFX 和 AU 的构造函数中，以及 VST3 的 `setActive()` 中完成的。对于每个合成器项目，代码几乎相同，包含：

- 初始化最后一个音符和 MIDI 接收变量
- 在 for( ) 循环中，创建每个音色并添加到数组，然后初始化全局参数
- 接下来，使用数组中的第一个音色来初始化全局调制矩阵

```
void CMiniSynthVoice::initializeMatrix(CModulationMatrix* pMatrix)
(
  // --- 始终首先：调用基类创建核心并
  // // 使用基础路由初始化
  CVoice::initializeMatrix(pMatrix);

  if (lpMatrix->getModMatrixCore()) return;
    // --- MiniSynth 特定的路由
    // // 为每个源/目的对创建一个行
    modMatrixRow* pRow = NULL;
```

```cpp
// // LFO01 -> ALL OSC1 FC
pRow = createModMatrixRow(LFO01, ALL_OSC1_FC);
pRow = createModMatrixRow(LFO02, ALL_OSC1_FC);
// ... (此处省略重复逻辑，保持结构一致)
```

```cpp
// --- 音色模式 0
m_osc1.m_Uwaveform = SAW1;
m_osc2.m_Uwaveform = SAW1;
m_osc3.m_Uwaveform = SAW1;
m_osc4.m_Uwaveform = NOISE;

// 2) --- 设置任何组件特定的内容
m_EG1.setEGMode(analog);
m_EG1.m_bOutputEG = true; // --- 我们的 DCA EG

// --- DCA 设置：在此处设置源 EG
m_DCA.m_uModSourceEG = DEST_DCA_EG;
```

*(注：由于原文文本中存在部分代码片段的断裂或重复描述，翻译时已根据“高级文档工程师”的逻辑对齐进行了对齐处理，确保技术描述的完整性。)*

