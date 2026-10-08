
```cpp
inline virtual double oscillate(double* pQuadPhaseOutput = NULL)
{
  if(!m_bNoteOn)
  {
    if(pQuadPhaseOutput)
      *pQuadPhaseOutput = 0.0;
    return 0.0;
  }
  // 输出
  double dOut = 0.0;
  double dQOut = 0.0;
  <SNIP SNIP SNIP>
  // 现在可以增加模值
  incModulo();
  if(m_pModulationMatrix)
  {
    // 将我们的输出写入对应的目标
    m_pModulationMatrix->m_dSources[m_uModDestOutput1] = 
      dOut*m_dAmplitude*m_dAmpMod;
    // 添加四相位/立体声输出
    m_pModulationMatrix->m_dSources[m_uModDestOutput2] = 
      dQOut*m_dAmplitude*m_dAmpMod;
  }
  etc...
}
```

# QBLimitedOscillator.h

修改 `doOscillate()` 函数将输出写入矩阵的 `Sources` 数组。这是一个单声振荡器，因此你只需要将最终输出拷贝到数组中的左右插槽中。

```cpp
virtual inline double doOscillate(double* pAuxOutput = NULL)
{
    if(!m_bNoteOn)
        return 0.0;

    <SNIP SNIP SNIP>

    // 现在可以增加模值
    incModulo();
    if(m_uWaveform == TRI)
        incModulo();

    if(m_pModulationMatrix)
    {
        // 将我们的输出写入对应的目标
        m_pModulationMatrix->m_dS[m_uModDestOutput1] = dOut*m_dAmplitude*m_dAmpMod;

        // 添加四相位/立体声输出 (QBL 是单声的)
        m_pModulationMatrix->m_dS[m_uModDestOutput2] = dOut*m_dAmplitude*m_dAmpMod;
    }

    // m_dAmpMod 在 updateOscillator() 中设置
    if(pAuxOutput)
        *pAuxOutput = dOut*m_dAmplitude*m_dAmpMod;

    // m_dAmpMod 在 updateOscillator() 中设置
    return dOut*m_dAmplitude*m_dAmpMod;
}
```

# WTOcillator.cpp

修改 `doOscillate()` 函数将输出写入矩阵的 `Sources` 数组。这是一个单声振荡器，因此你只需要将最终输出拷贝到数组中的左右插槽中。

# Filter.h

在 `Filter.h` 文件中，你首先 #include `modulation matrix.h` 文件，然后对调制矩阵指针、源和目标进行声明。对于滤波器，我们有：

- 源：`double CWToscillator::dooscillate(double* pAuxOutput)`
- 滤波器 fc
- 滤波器控制（用于 Filter Key Track，其中 `fc` 控制值会被 MIDI Note音高覆盖）

```cpp
if(Im_bNoteOn) {
    if(pAuxOutput)
        *pAuxOutput = 0.0;
    return 0.0;
}

// SNIP SNIP SNIP

// 获取第一个输出
double dOutSample = doWaveTable(m_dReadIndex, m_dWT_inc);

if(m_pModulationMatrix) {
    // 将我们的输出写入对应的目标
    m_pModulationMatrix->m_dS[m_uModDestOutput1] = dOutSample*m_dAmplitude*m_dAmpMod;

    // 添加四相位/立体声输出 (QBL 是单声的)
    m_pModulationMatrix->m_dS[m_uModDestOutput2] = dOutSample*m_dAmplitude*m_dAmpMod;

    // 单声振荡器
    if(pAuxOutput)
        *pAuxOutput = dOutSample*m_dAmplitude*m_dAmpMod;

    return dOutSample*m_dAmplitude*m_dAmpMod;
}
```

目标：
- 无

```cpp
#include "ModulationMatrix.h"

// 46.8817993634 半音 = semitonesBetweenFrequencies(80, 18000.0)/2.0
#define FILTER_FC_MOD_RANGE 46.881799364656880
#define FILTER_FC_MIN 80                   // 80 Hz
#define FILTER_FC_MAX 18000              // 18 kHz

class CFilter{
public:
    CFilter(void);
    ~CFilter(void);

    // --- 调制矩阵 ---
    //
    // -- 共享调制矩阵
    CModulationMatrix* m_pModulationMatrix;

    // -- 我们从处读取的源
    //
    // m_pModulationMatrix->Sources[] 中的索引
    UINT m_uModSourceFc;

    UINT m_uSourceFcControl; // 直接控制 Fc，用于 Key跟踪模式

    // -- 用户截止频率控制位置
    double m_dfcControl;

    etc...
```

# Filter.cpp

与振荡器类似，你只需要在构造函数中初始化变量。调制矩阵指针为 NULL 且是的。默认连接为 `DEST_NONE`。

```cpp
CFilter::CFilter(void)
{
    // 默认值
    m_dSampleRate = 44100;
    m_dFc = 10000.0;
    m_dQ = 0.707;
    m_dcFControl = 10000.0;

    m_dcFMod = 0.0;
    m_dAuxControl = 0.5;
    m_uNLP = OFF;
    m_dSaturation = 1.0;

    // --- 调制矩阵初始化
    m_pModulationMatrix = NULL;

    // --- 除非使用调制矩阵，否则都是断开的
    m_uModSourceFc = DEST_NONE;
    m_uFcControl = DEST_NONE;
}
```

# EnvelopeGenerator.h

在 `EnvelopeGenerator.h` 文件中，你首先 #include 调制矩阵文件，然后对调制矩阵指针、源和目标进行声明。对于 EG（包络），我们有：

字体 源：
- EG Attack 缩放
- EG Decay 缩放

目标：
- 正常 EG 输出
- 偏置 EG 输出

我们将很快讨论 EG 的 Attack 和 Decay 缩放。目标仅仅是对象的两个输出。

# EnvelopeGenerator.cpp

与振荡器类似，你只需要在构造函数中初始化变量。调制矩阵指针为 NULL 且是可选的。默认连接为 `NONE`。

```cpp
#include "ModulationMatrix.h"

class CEnvelopeGenerator
{
public:
    CEnvelopeGenerator(void);
    ~CEnvelopeGenerator(void);

    // --- 调制矩阵
    // --- 共享调制矩阵
    CModulationMatrix* m_pModulationMatrix;

    // // 我们从处读取的源
    // m_pModulationMatrix->Sources[] 中的索引
    UINT m_uModSourceEGScaling;
    UINT m_uSourceEGDecayScaling;
};
```

编程主矩阵 (Programming the Master Matrix)

还有部分需要处理——调制强度和范围值位于 `modulationRow` 结构中。这样你就可以通过 GUI 参数直接控制这些值。我们需要声明一些变量来连接到它们。我们需要 1.0 的默认强度和范围值，并且还需要滤波器和振荡器的频率范围（我们在 NanoSynth 处理中使用的相同）。插件的 h 文件，你需要添加：

这些是在构造函数中初始化的。注意范围是用对象 .h 文件中定义的常量初始化的，但你也可以将其连接到 GUI 参数并使其变为变量或用户可编程。

表 8.1 如下：

| 源 | LFO1 |
| --- | --- |
| 目标: | 所有 OSC f0 |
| 强度: | m_dDefaultIntensity |
| 范围: | m_dOSfoRange |
|  | 无 |
| 默认启用 | 是 |

检查表 8.1，你可以看到 LFO1 输出调制振荡器的 f0 值。表 8.3 显示了调制矩阵中的此类信息。注意 `DEST_ALL_OSC_FO` 值的用法。我们尽可能使用这些值以减少矩阵行数并简化代码。

源：
- EG Mod
- 用于颤音的 Amp Mod (dB)
- 速度
- 平移

目标：
- 无
