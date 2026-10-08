
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
```

<< 插入代码列表 11.1: 声明 **此处** >>

等……

- 创建一个包含 128 个振荡器和 128 个向量混合值的混合表面是困难且低效的；在任何时刻，对于远离混合点的样本，大多数混合值将是零或接近于零

- 在 iPad 上为每个笔记事件运行 128 个振荡器将非常繁琐，如果不是不可能的话

- 如果所有 128 个振荡器在混合点位于波形表之间时以非零比例进行混合，你将得到一大堆噪音

```cpp
AUSynth::AUSynth(AudioUnitInComponentInstance)
: AUInstrumentBase(inComponentInstance, 0, 1)
```

```cpp
{
  // --- 创建输入、输出端口、组和部分
  CreateElements();
```

```cpp
// --- 设置默认工厂预设（示例）
factoryPreset[OSC1_AMPLITUDE_DB] = 0.0;
factoryPreset[OSC2_AMPLITUDE_DB] = 0.0;
```

```cpp
<SNIP SNIP SNIP>
```

```cpp
// --- 定义参数（控件）的数量
Globals()->SetUseIndexedParameters(NUMBER_OF_SYNTH_PARAMETERS);
```

```cpp
// --- 在此处初始化控件！
// --- 这些定义在 SynthParamLimits.h 中
```

```cpp
<SNIP SNIP SNIP>
```

```cpp
// -- VS 特有
Globals()->SetParameter(VECTORJOYSTICK_X, DEFAULT_UNIPOLAR_HALF);
Globals()->SetParameter(VECTORJOYSTICK_Y, DEFAULT_UNIPOLAR_HALF);
Globals()->SetParameter(PATH_MODE, DEFAULT_PATH_MODE);
Globals()->SetParameter(ORBIT_X, DEFAULT_UNIPOLAR);
Globals()->SetParameter(ORBIT_Y, DEFAULT_UNIPOLAR);
```

- 当 Globals()->SetParameter(ROTOR_RATE, DEFAULT_SLOW_LFO_RATE);
Globals()->SetParameter(ROTOR_WAVEFORM, DEFAULT_LFO_WAVEFORM);

等……关于设备上的注释，你会听到靠近混合点的振荡器的混合，而听不到远处的音色

- - 声音平滑地相互变换，没有不连续性，除非转子速率和轨道幅度非常高，此时你可以听到波形表被跳过了

```cpp
void AuSynth::update()
{
    // --- 更新全局参数
    //
    等……

    // --- VS 特有
m_GlobalSynthParams.voiceParams.uvectorPathMode =
    Globals()->GetParameter(PATH_MODE);
m_GlobalSynthParams.voiceParams.dorbitXAmp =
    Globals()->GetParameter(ORBIT_X);
m_GlobalSynthParams.voiceParams.dorbitYAmp =
    Globals()->GetParameter(ORBIT_Y);

// --- 仅限 VST3/AU ---
// 根据 x,y 位置计算向量摇杆混合值
// (x,y 为 0到1)
calculateVectorJoystickValues(
    Globals()->GetParameter(VECTORJOYSTICK_X),
    Globals()->GetParameter(VECTORJOYSTICK_Y),
    m_GlobalSynthParams.voiceParams.dAmplitude_A,
    m_GlobalSynthParams.voiceParams.dAmplitude_B,
    m_GlobalSynthParams.voiceParams.dAmplitude_C,
    m_GlobalSynthParams.voiceParams.dAmplitude_D);
```

混合方程效果非常好且易于实现——为什么要发明轮子？AUSynth 将四个振荡器视为一个较小的混合表面。每个振荡器组构成一个混合表面。在任何时刻，合成器的输出是包含混合点的四个振荡器的组合。注意到任何相邻单元格都会共享两个波形表。为了简化计算并复用摇杆控件，AUSynth 使用正方形波形表而不是矩形。如果将摇杆控件修改为矩形，通过使用非摇杆坐标系更容易看到 AUSynth 如何工作，其中混合点呈正方形排列。

等…… -- LFO: m_GlobalSynthParams.lfoParams.uWaveform = Globals()->Get(ROTOR_WAVEFORM);
m_GlobalSynthParams.lfofo = Globals()->Get(ROTOR_RATE);

它不仅决定了波形表的数量，还作为计算的一部分。每边单元格的数量与总波形表数量：

图11.34：AUSynth 表面上的几个单元格。

图11.35：当 C=3 时，有 (a) 三行三列共九个单元格和 (b) 编号 0 到 15 的波形表。

num samples = (C + 1)^2

AUSynth 使用 C=5 波形表。我们将很快讨论这些表。为了显示 AUSynth 如何清晰地跨越混合表面，使用 C=3 或 16 的较小混合表面更简单。单元格结构和波形表如图11.35 所示。注意到每边单元格的数量也是行数。行索引值在稍后需要。在这种情况下，C=3 用于使图表复杂。

![](img/b42d0dca53f4a889d8162d5f7c8c05d_786_0)

# Wavetable Grid

当混合点位于单元格之外时，该单元格被激活，其顶点被视为 VS 表面的 A、B、C 和 D。随着路径/路由器的移动，活跃单元格进行切换。由于相邻单元格共享公共顶点，这只是将正确的波形表映射到语音对象的问题。AUSynth 对象与具有振荡器的 VectorSynth 对象类似，每个从采样文件读取。图11.36(a) 显示第一个单元格中的混合点正向单元格移动。注意到顶点已索引。在图11.36(b) 中，混合点触碰了 D-C 边界，其混合比例为 50% C、50% D 以及其他。

现在假设混合点跨越 D-C 边界进入下方单元格（单元格 3），如图11.37 所示。当发生时，语音对象必须为下一个单元格切换当前的波形表。然而，有两个是共享的——波表 4 和 5（D 和 C）变为下一个单元格的 A 和 B。在边界处，由于位置的原因，D 和 C 波形表被重命名为 A 和 B。注意到现在的混合比例为 50% A、50% B 以及其他，由于波形表共享共享，单元格切换没有故障或不连续。如果路径直接通过顶点，则混合值将为 100%，波形表将分布，混合继续到下一个单元格（100% 水平）。

![](img/b42d0dca53f4a88912df7c8c05d_787_0.png)

图11.36：(a) 单元格 0 中的混合点使用单元格顶点计算当前混合 (b) 混合点已移动到单元格顶点 D 和 C 的边缘。

![](img/b42d0dca53f4a88912df7c8c05d_787_1.png)

图11.37：(a) 混合点跨入下一个单元格，那里的振荡器名称被洗牌，但边缘波形表保持不变，因此当混合点进入新单元格时没有听到的点击声 (b) 混合点继续沿路径 3 移动。

![](img/b42d0dca53f4a88912df7c8c05d_787_2.png)
