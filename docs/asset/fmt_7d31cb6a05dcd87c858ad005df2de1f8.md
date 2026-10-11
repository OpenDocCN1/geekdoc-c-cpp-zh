
- `nIndex`：基于 0 的步骤索引
- `fX` 和 `fY`：`(x,y)` 坐标
- `fTimeToStep_mSec`：到下一个步骤的时间
- `bJoystick`：如果使用摇杆坐标则为 true，否则为 false。

图 11.31：VectorSynth 详细连接图。

表 11.5：VectorSynth 的调制矩阵与 DigiSynth 几乎相同；新增部分显示了位于转子振荡器处的 LFO2。

表 11.6：VectorSynth GUI 控制列表。

图 11.32：RackAFX 中一种可能的 VectorSynth GUI；注意有几个控件被嵌入在 LCD 控制中。

![](img/b42d0dca53f4a889d8162d55f7c8c05d_757_0.png)

## 11.12 CVectorSynth 对象

`CVectorSynth` 对象派自 `CDiSynthVoice`，因此它继承了所有的振荡器加载功能。它为矢量摇杆添加了新变量以及一些简单的函数。它像之前的所有对象一样，重写了标准的 `CVoice` 函数。表 11.7 列出了成员变量，表 11.8 列出了成员函数。到目前，这些内容看起来应该很熟悉了。

### 音色全局参数

我们需要为新的 `CVectorSynthVoice` 对象使用更多的默认全局参数。这些包括以下内容（见 `synthfunctions.h` 中的 `struct GlobalParams`）。

```cpp
// --- vector_synth
double dOrbitXAmp;
double dOrbitYAmp;
double dAmplitude_A;
double dAmplitude_B;
double dAmplitude_C;
double dAmplitude_D;
double dAmplitude_ACmix;
double dAmplitude_BDmix;
UINT juVectorPathMode;
```

音色对象的成员变量是言自自明的，所以让我们关注成员函数，其中一些与上一章中的 `CMiniSynthVoice` 对象几乎相同。

### 构造函数

构造函数执行以下初始化，其中某些你可能会进行修改：

- 将振荡器连接到成员指针
- 将滤波器连接到成员指针
- 开启滤波器上的 NLP（可选）
- 将 EG 模式设为模拟（可选）
- 设置 EG1 输出标志
- 设置 EG1 的 DCA EG 调制源（重要——必须在派生类构造函数中始终完成）
- 初始化新的矢量合成器变量
- 初始化矢量路径生成器（注意 `#define _RAFXX`）

![](img/b42d0dca53f4a889d8162d55f7c8c05d_758_0.png)

**表 11.7：** `CVeterSynthVoice` 成员变量。

**表 11.8：** `CVeterSynthVoice` 成员变量。

构造函数还包含一个简单的矢量路径程序示例；对于 RackAFX 它是禁用的，因此你可以使用内置的摇杆程序，但可以通过设置 `m_bEnableVPG = true` 来重写此项并对该对象进行实验。

### VectorSynth 调制矩阵

| 源 | 目标/强度 | 变换/范围 | 启用 |
| --- | --- | --- | --- |
| `SOURCE_LFO1` | `DEST_ALL_OSC_FO` | `TRANSFORM_NONE` | TRUE |
| | `dLFO1OscModIntensity` | `dOscFoModRange` | | |
| `SOURCE_BIASED_EG1` | `DEST_ALL_FILTER_FC` | `TRANSFORM_NONE` | TRUE |
| | `dFilter1ModIntensity` | `dFilterModRange` | | |
| `SOURCE_EG1` | `DEST_CA_EG` | `TRANSFORM_NONE` | TRUE |
| | `dEG1CAAmpModIntensity` | `m_dDefaultModRange` | | |
| `SOURCE_BIASED_EG1` | `DEST_ALL_OSC_FO` | `TRANSFORM_NONE` | TRUE |
| | `dEG10OscModIntensity` | `dOscFoModRange` | | |
| `SOURCE_LFO1` | `DEST_ALL_FILTER_FC` | `TRANSFORM_NONE` | TRUE |
| | `dLFO1FilterMod` | `dFilterModRange` | | |
| `SOURCE_LFO1` | `DEST_CA_AMP` | `TRANSFORM_BIPOLAR_TO_UNIPOL` | TRUE |
| | `dLFO1CAAmpModIntensity` | `dAmpModRange` | | |
| `SOURCE_LFO1` | `DEST_CA_PAN` | `TRANSFORM_NONE` | TRUE |
| | `dLFO1DCanModIntensity` | `m_dDefaultModRange` | | |
| `SOURCE_LFO2` | `DEST_VS_AC_AX` | `TRANSFORM_NONE` | TRUE |
| | `m_dDefaultModRange` | `d_DefaultModRange` | | |
| `SOURCE_LFO2` | `DEST_VS_BD_AX` | `TRANSFORM_NONE` | TRUE |
| | `m_dDefaultModRange` | `d_DefaultModRange` | | |

### VectorSynth 连续参数

| 控制名称 (单位) | 类型 | 变量名称 (VST, RAFX) | 低/高/默认 | VST/AU 索引 |
| --- | --- | --- | --- | --- |
| Osc EG Int | double | `m_dEG1Intensity` | -1 / 0 | EG1_TO_OSC |
| Filter fc (Hz/octave) | double | `m_dFcControl` | 80 / 18000 | FILTER_FC |
| Filter Q | double | `m_dQControl` | 1 / 10 | FILTER_Q |
| Filter EG Int | double | `m_dEG1Intensity` | -1 / 0 | EG1_TO_FILTER |
| Key Track Int | double | `m_dFilterTrack` | 0 / 10 | FILTER_KEYTRACK |
| Attack (ms) | double | `m_dAttackTime` | 0 / 5000 | EG1_ATTACK |
| Decay/Release (ms) | double | `m_dDecayTime` | 0 / 10000 | EG1_DECAY_RELEASE |
| Sustain | double | `m_dSustainLevel` | 0 / 1 / 0.7 | EG1_SUSTAIN_LEVEL |
| LFO Rate | double | `m_dLFO1Rate` | 0 / 2 / 0.5 | LFO_RATE |
| LFO Depth | double | `m_dLFO1Amplitude` | 0 / 1 | LFO1_TO_FILTER |
| LFO Pitch Int | double | `m_dLFO1OscIntensity` | -1 / 0 | LFO1_TO_OSC |
| LFO Amp Int | double | `m_dLFO1AmpIntensity` | 0 / 1 | |
| LFO Pan Int | double | `m_dLFO1PanIntensity` | 0 / 1 | LFO1_TO_PAN |
| Volume | double | `m_Volume` | -96 / 200 | OUTPUT_AMPLITUDE |
| DCA EG Int | double | `m_dEG1CA` | -1 / 1 | EG1_TO_DCA |
| Detune | double | `m_dDetune_cents` | -100 / 100 | DETUNE_CENTS |

### initParameters()

此函数与 `CDigSynthVoice` 大体相同——调用基类函数并初始化新的音色参数。

| Portamento (mS) | double | `m_dPortamento_mSec` | 0 / 5000 / 0 | PORTAMENTO_TIME_SEC |
| --- | --- | --- | --- | --- |
| A-Cut Output | double | `m_dOsc1Amplitude_dB` | -96 / 24 / 0 | OSC1_AMPLITUDE_DB |
| B-D Output | double | `m_dOsc2Amplitude_dB` | -96 / 24 / 0 | OSC2_AMPLITUDE_DB |
| Rotor Rate | double | `m_dRotorRate` | 0.01 / 2 / 0.5 | ROTOR_RATE |
| Orbit X | double | `m_dOrbitX` | 0 / 1 / 0 | ORBIT_X |
| Orbit Y | double | `m_dOrbitY` | 0 / 1 / 0 | ORBIT_Y |
| Octave | int | `m_Octave` | -4 / 4 / 0 | OCTAVE |
| PBandRange (semi) | int | `m_nPitchRange` | 0 / 12 / 1 | PITCHBAND_RANGE |
| Vector Joystick X | int | `m_dJoystickX` | 0 / 1 / 0 | VECTOR_JOYSTICK_X |
| Vector Joystick Y | int | `m_dJoystickY` | 0 / 1 / 0 | VECTOR_JOYSTICK_Y |

- 低值和高值定义在每个项目的 `SynthParamLimits.h` 中
- 仅适用于 VST 和 AU（客户端没有内置摇杆控制）

### VectorSynth 枚举字符串参数

| 控制名称 | 变量名称 | 枚举字符串 | VST3/AU 索引 |
| --- | --- | --- | --- |
| LFO Waveform | `m_uLFOWaveform` | sine,saw,tri,square,exp,rsq | LFO_WAVEFORM |
| Rotor Waveform | `m_uRotorWaveform` | sine,saw,tri,square,exp,rsq | | ROTOR_WAVEFORM |
| Voice Mode | `m_uVoiceMode` | manual,program | VOICE_MODE |
| Path Mode | `m_uVectorPathMode` | off,sustain,backfreq | PATH_MODE |
| Vel->Att Scale | `m_uVelocityToAtt` | OFF | VELOCITY_TO_ATTACK |
| Note->Dcy Scale | `m_uNumberToDecaying` | OFF | NOTE_NUM_TO_DECAY |
| Reset to Zero | `m_uResetToZero` | OFF | RESET_ZERO |
| Filter KeyTrack | `m_uFilterKeyTrack` | OFF | FILTER_KEYTRACK |
| Legato Mode | `m_uLegato` | OFF | LEGATO_MODE |

### initializeModMatrix()

此函数创建并设置调制矩阵；与 DigiSynth 相同，但增加了新的 LFO2 路由![](img/b42d0dca53f4a889d8162d55f7c8c05d_760_0.png)

### CVectorSynth 成员变量

| 类型 | 变量名称 | 说明 |
| --- | --- | --- |
| `CSampleillator` | `m_OscA, m_OscB, m_OscC, m_OscD` | 四个振荡器 |
| `CKFiveFilter` | `m_LeftK35Filter, m_RightK35Filter` | 左右通道滤波器 |
| double | `m_Amplitude_A, m_Amplitude_B, m_Amplitude_C, m_Amplitude_D, m_Amplitude_ACmix, m_Amplitude_BDmix` | 存储当前混合的变量；这些每个采样更新一次 |
| double | `m_CenterX, m_CenterY, m_OrbitXAmp, m_OrbitAmp` | 处理转子以及通过摇杆偏移路径中心的变量 |
| `JoystickProgram*` | `m_jsProgram` | RackAFX 摇杆程序 |
| `CVectorPathGenerator` | `m_VPG` | 所有的矢量路径对象 |
| bool | `m_EnableVPG` | 仅用于 RackAFX——允许选择程序或矢量生成器 |
| | | once, loop, sustain - 程序的路径模式 |
| enum | | 音色模式枚举 |

### CVectorSynth 成员函数

| 函数名称 | 说明 |
| --- | --- |
| `initGlobalParameters` | 初始化全局参数 |
| `initializeModMatrix` | 初始化调制矩阵 |
| `setSampleRate` | 在子组件上设置采样率 |
| `prepareForPlay` | 在子组件上准备播放，仅需执行一次——针对矢量路径生成器对象；它们需要采样率，因为它们随时间生成事件 |
| `update` | 更新音色变量 |
| `reset` | 重置音色变量 |
| `noteOn` | 重写基类方法；在音符开启期间启动摇杆程序（如果使用） |
| `noteOff` | 重写基类方法；在音符关闭期间（且处于持续模式时）恢复摇杆程序（如果使用） |
| `doVoice` | 渲染音频 |

```cpp
// --- voice stealing
m_EG1.m_bResetZero = true;

// --- experiment with NLP
m_LeftK35Filter.m_nULP = ON;
m_RightK35Filter.m_nULP = ON;

// m_EG1.setEG(analog);
m_EG1.m_bOutput = true;

// --- VS Specific
m_dAmplitude_A = 0.25;
m_dAmplitude_B = 0.25;
m_dAmplitude_C = 0.25;
m_dAmplitude_D = 0.25;
m_dAmplitude_ACmix = 0.5;
m_dAmplitude_BDmix = 0.5;
m_dCenterX = 0.0;
m_dCenterY = 0.0;
m_dOrbitXAmp = 0.0;
m_dOrbitYAmp = 0.0;

// --- plug-in must set this RAFX only!!
m_pProgram = NULL;
m_uVoice = manual;

// // example of programmatically creating a path
// without RAFX generator

// -- Setup path generator; this just moves around
// one apex to the next.

// start at 100% A morph to next step in 2 sec
// start at 100% B morph to next step in 2 sec
// start at 100% C morph to next step in 2 sec
// start at 100% D morph to BEGINNING in 2 sec (if LOOP)

#ifdef _RAFX
// the true argument means using Korg/RAFX
m_VPG.setStep(0, -1.0, 0.0, 2000);

first, then any voice specific
```

```cpp
m_vpg.setStep(1, 0.0, 1.0, 2000);

m_VPG.setStep(2, 1.0, 0.0, 2000);

m_VPG.setStep(3, 0.0, -1.0, 2000);
```

```cpp
// --- RAFX version, VPG is disabled so you can use the

// joystick in RAFX (hit the Program button)

m_bEnableVPG = false;

// m_bEnableVPG = true; <-- uncomment to use VPG instead of JS

#else

// -- the flag means you rotated

m_VPG.setStep(0, -1.0, 1.0, 2000);

m_VPG.setStep(1, 1.0, 1.0, 2000);

m_VPG.setStep(2, 1.0, -1.0, 2000);

m_VPG.setStep(3, -1.0, -1.0, 2000);

// --- for VST/AU, there is no built-in generator, do it by hand

m_bEnableVPG = true;

#endif
```
