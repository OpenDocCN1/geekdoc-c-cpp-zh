
## `update()`

该函数略有不同，因为删除了一些控件并添加了一些新的。此函数显示了加粗的新代码。对于 VST3 和 AU，你还需要从摇杆控制计算向量混合值（在 RackAFX 中，客户端为你完成此操作）。注意此函数使用引用传递，因此我们可以将值计算到全局参数中。

```
// --- 用于 note on/off/voice steal 的辅助函数
void incrementVoiceTimestamps();
CVectorsSynth* getgetOldestVoice();
CVectorsSynth* getOldestVoiceWithNote(UINT uMIDINote);
```

// --- 加载采样集

`bool loadSamples();`

```
// 一次更新所有声器
void update();
```

```
// 用于滑音
double m_dLastNoteFrequency;
```

```
// 我们的接收通道
UINT m_uMidiRxChannel;
```

新增：

## Osc A: Heaver

Osc B: OldFlatty

Osc C: Divider

Osc D: FuzzVibe

- 路径模式 (`path mode`)

- 轨道 X 和 Y 数量 (`orbit X and Y amounts`)

- 旋转速率 (`rotor rate`)

- 旋转波形 (`rotor waveform`)

- AC, BD 输出幅度 (`AC, BD Output Amplitude`)

- 循环模式 (`Loop Mode`)

<< 代码列表 11.2: 加载样本 >>

## `doControlUpdate()`

`doControlUpdate()` 函数必须从 { 修改：

```cpp
bool CVectorsynth::loadSamples() //RAFX
_bool Processor::loadSamples() //VST3

bool ASynth::loadSamples() //AU

// -- 加载 4 组多采样
// -- 用于多采样处理 -- /

// RackAFX
char* pPath0 = addStrings(getMyDLLDirectory()) + "MultiSamples\\Heaver";
char* pPath1 = addStrings(getMyDLLDirectory()) + "MultiSamples\\OldFlatty";
char* pPath2 = addStrings(getMyDLLDirectory()) + "MultiSamples\\Divider";
char* pPath3 = addStrings(getMyDLLDirectory()) + "MultiSamples\\FuzzVibe";

// // --- VST3
char* pDLLPath = getMyDLLDirectory(USTRING("VectorSynth.vst3"));
char* pPath0 = addStrings(pDLLPath) + "MultiSamples\\Heaver";
char* pPath1 = addStrings(pDLLPath) + "MultiSamples\\OldFlatty";
char* pPath2 = addStrings(pDLLPath) + "MultiSamples\\Divider";
char* pPath3 = addStrings(pDLLPath) + "MultiSamples\\FuzzVibe";

// // --- AU
char* componentFolder = getMyComponentDirectory(
CFSTR("developer.audiounit.yourname.vectorsynth");
```
```cpp
char* pPath0 = addStrings(componentFolder, "/MultiSamples/Heaver");
char* pPath1 = addStrings(componentFolder, "/MultiSamples/OldFlatty");
char* pPath2 = addStrings(componentFolder, "/MultiSamples/Divider");
char* pPath3 = addStrings(componentFolder, "/MultiSamples/Fuzzibe");
//
```
```cpp
// 为了加速样本加载，初始化第一个声音，我们
init(false, false) = 不是单采样，不是无音高样本
if(im_pVoiceArray[0]->initOscWithFolderPath(0, pPath0, false, false))
    return false;
if(im_pVoiceArray[0]->initOscWithFolderPath(1, pPath1, false, false))
    return false;
if(im_pVoiceArray[0]->initOscWithFolderPath(2, pPath2, false, false))
    return false;
if(im_pVoiceArray[0]->initOscWithFolderPath(3, pPath3, false, false))
    return false;
// 然后使用其他函数拷贝样本指针
// 以共享指向相同数据缓冲指针
for(int i=1; i<MAX_VOICES; i++)
```

修改 DigiSynth 以匹配上述列出的新变量添加/删除。在 `switch/case` 语句中，删除已删除变量的 `case` 语句，并为新变量添加 `case` 语句（此处**加粗**所示）。这些与你在 `update()` 函数中实现的添加/删除相同。同样注意，你在此处获取了矢量摇杆的位置；它来自新的摇杆控制。

## 11.16 VectorSynth: AU

创建一个新项目 `VectorSynth`，并使用表 11.6 设置 GUI。如第 11.9 节所述，添加新的矢量摇杆控制。

## `AUSynth.h`

在文件顶部，添加对 `VectorVoice.h` 的 `#include` 语句，并设置声音数组和所有辅助成员函数。同样添加 `loadSamples()` 函数。

## `AUSynth.cpp`

以下函数与 DigiSynth 相同，但存储在数组中的声音指针类型除外。

- 析构函数

```cpp
// -- init false, false = 不是单采样
// 无音高样本
m_pVoiceArray[i]->initAllscWithiSynth(m_pVoiceArray[0],
    false, false);

// 总是 addStrings() 返回
delete [] p0;
delete [] p1;
delete [] p2;
delete [] p3;

// --- VST3
delete [] pDLLPath;

// --- AU
delete [] componentFolder;

<< 代码列表 11.2: 加载样本 >>

class CVectorSynth : public CPlugin
{
public:
    <省略内容>

    // 添加你的代码：--------------------

<< 代码列表 11.1: 声明 >>
etc...

- Initialize()

## `CVectorSynth::CVectorSynth()`

```cpp

{

  <省略内容>

  // 加载声音

  for(int i=0; i<MAX_VOICES; i++)

    // 创建声音

    m_pVoiceArray[i] = new Synth;

    // 全局参数（必须在设置矩阵之前完成）

    m_pVoiceArray[i]->initGlobal(&GlobalParams);

    // VectorSynth 添加

    // CJoystickProgram(m_pJSProgram, m_uPathMode)

    m_pJSProgram 指向 JS 数组

    （RAFX 中，无需代码）

    // m_uPathMode 初始路径模式

    m_pVoiceArray[i]->m_pJSProgram = new

      CJoystickProgram(m_pJSProgram, m_uPathMode);

}

etc...

```

- `Reset()`
- `Render()`
- `StartNote()`
- `StopNote()`
- `HandleWheel()`
- `HandleChange()`

`bool stdcall CVectorSynth::initialize()`

```cpp

{

  // --- 加载样本

  return loadSamples();

}

```

构造函数

初始化工厂预设（可选）以及表 11.6 中的所有 GUI 变量；其余与 MiniSynth 相同。

## `loadSamples()`

在 `.cpp` 文件中任何位置插入代码列表 11.2。

```cpp

void CVectorsSynth::update() // RAFX

{

    // --- 更新参数

    etc...

    // --- AC/BD 混合：

    double dscAmplitude = m_d01Amplitude_dB <= -96.0 ? 0.0 :

        pow(10.0, m_d01Amplitude_dB/20.0);

    m_GlobalSynthParams.osc1Params.Amplitude = dscAmplitude;

    m_GlobalSynthParams.osc2Params.Amplitude = dscAmplitude;

    dscAmplitude = m_d02Amplitude_dB <= -96.0 ? 0.0 :

        pow(10.0, m_d02Amplitude_dB/20.0);

    m_GlobalSynthParams.osc3Params.Amplitude = dscAmplitude;

    m_GlobalSynthParams.osc4Params.Amplitude = dscAmplitude;

    // -- VS 特有

    m_GlobalSynthParams.voiceParams.uVectorPathMode = m_uPathMode;

    m_GlobalSynthParams.voiceParams.dorXamp = dbitX;

    m_GlobalSynthParams.voiceParams.dorYamp = dbitY;

    // -- LFO2:

    m_GlobalSynthParams.lfo2Params.uWaveform = m_uRotorWaveform;

    m_GlobalSynthParams.lfo2Params.dsc = m_dRotorRate;

    etc...

}

class Processor : public AudioEffect

{

public:

    <省略内容>

    // 在处添加你的代码：--

    update()

```

## << 代码列表 11.1: 声明 >>

其他差异在于 `update()` 函数，它略有不同，因为一些控件被删除了，另一些被新增。此外，现在有两个过滤器需要处理。

```cpp

Processor::Processor () {

    // --- 我们是一个 Processor

    setControllerClass(Controller::cid);

    // --- 初始化

    m_dsc1Amplitude_dB = DEFAULT_OUTPUT_AMPLITUDE_DB;

    m_dsc2Amplitude_dB = DEFAULT_OUTPUT_AMPLITUDE_DB;

    // 矢量摇杆

    m_dJoystickX = DEFAULT_UNIPOLAR_HALF; // 注意这些是 0->1

    m_dJoystickY = DEFAULT_UNIPOLAR_HALF; // 同上

    m_uVectorPathMode = DEFAULT_PATH_MODE;

    m_OrbitX = DEFAULT_BIPOLAR;

    m_dOrbitY = DEFAULT_BIPOLAR;

    m_dRotorRate = DEFAULT_SLOW_LFO_RATE;

    m_uRotorWaveform = DEFAULT_LFO_WAVEFORM;

```

etc... 剩余函数显示了**加粗**的新添加代码。对于 VST3 和 AU，你还需要从摇杆控制计算矢量混合值（在 RackAFX 中，客户端会为你完成）。注意此函数使用引用传递，因此我们可以直接将值计算到全局参数中。

从 DigiSynth 中移除：

- 循环模式
- Osc1, Osc2 输出幅度

新增：

- 路径模式
- 轨道 X 和 Y 数量
- 旋转速率

```cpp

void Processor::update() 

{

    // --- 更新全局参数

    etc...

    // -- VS 特有

    m_GlobalSynthParams.voiceParams.uVectorPathMode = m_uPathMode;

    m_GlobalSynthParams.voiceParams.dbitX = dbitX;

    m_GlobalSynthParams.voiceParams.dbitYAmp = dbitY;

    // --- 仅 VST3/AU

    // 根据 x,y 位置计算矢量摇混合值

    // (x,y 为 0-1)

    calculateVectorJoystickValues(m_dJoystickX, m_dJoystickY, m_GlobalSynthParams.voiceParams.dAmplitude_A,

    m_GlobalSynthParams.voiceParams.dAmplitude_B, m_GlobalSynthParams.voiceParams.dAmplitude_C, m_GlobalSynthParams.voiceParams.dAmplitude_D, m_GlobalSynthParams.voiceParams.dAmplitude_ACmix, m_GlobalSynthParams.voiceParams.dAmplitude_BDmix);

    // -- LFO2:

    m_GlobalSynthParams.lfo2Params.uWaveform = m_uRotorWaveform;

    m_GlobalSynthParams.lfo2Params.dsc = m_dRotorRate;

}

```

似乎唯一的不同在于随着向量移动，混合过程中所经历的音色数量。

```cpp

Processor::doControlUpdate(ProcessData& data) mix {\<SNIP SNIP SNIP Indents Removed>

switch (pid) {

  // cookVSTGUIVable(min, max, currentValue) - 将原始数据处理为

  // 我们有用的信息
case VECTORJOYSTICK_X:
{
  m_dJoystickX = value;
  break;
}
case VECTORJOYSTICK_Y:
{
  m_dJoystick = value;
  break;
}
case PATH_MODE:
{
  m_uVectorPathMode = (UINT)cookVSTGUIVable(MIN_PATH_MODE, MAX_PATH_MODE, value);
  break;
}
case ORBIT_X:
{
  m_dOrbitX = value;
  break;
}
case ORBIT_Y:
{
  m_dOrbitY = value;
  break;
}
```

```cpp

}
case ROTOR_RATE:
(
  m_dRotorRate = cookVSTGUIVariable(MIN_SLOW_LFO_RATE,
    MAX_SLOW_LFO_RATE, value);
  break;
```

```cpp

case ROTOR_WAVEFORM:
(
  m_uRotorWaveform = (UINT)cookVSTGUIVariable(MIN_LFO_WAVEFORM,
    MAX_LFO_WAVEFORM,
    value);
  break;
```

```cpp

// --- MIDI messages
case MIDI_PITCHBEND: // 想要 -1 到 +1
```

等等……然而，我们可以对其运行提出一些假设。注意在这些要点中波形表、振荡器和音色的术语是不断变化的。

```cpp

class AUSynth : public AUInstrumentBase

{
```

public:

```cpp

// 在此处添加您的代码：
