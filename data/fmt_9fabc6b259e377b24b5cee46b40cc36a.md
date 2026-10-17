
对于 AU，第一步是在 `SynthParamList.h` 中设置 GUI 索引。与 VST3 和 RackAFX 不同，你不需要为控件声明变量——它们将存储在你的参数计数器中。

# AU 控制步骤 2：初始化

声明索引参数的数量，然后在 `AUSynth` 构造函数中初始化这些参数。参数的数量与步骤 1 中的枚举匹配。

# AU 控制步骤 3：设置参数信息

GUI 参数的属性在 `GetParameterInfo()` 中设置。请使用：

```cpp
bool __stdcall CNanoSynth::prepareForPlay() {
```

```cpp
// sample rates
m_Osc1.setSampleRate((double)m_nSampleRate);
m_Osc2.setSampleRate((double)m_nSampleRate);
m_LFO1.setSampleRate((double)m_nSampleRate);
```

```cpp
// detune 2.5 cents
m_Osc2.m_nCents = 2.5;
```

```cpp
// update the synth
update();
```

```cpp
return true;
```

参考表 5.3 来设置此函数。辅助函数名为 `setAUParameter()`，最后两个参数是用于索引字符串的标志。将索引参数设置为 `type` 类型将其识别为枚举类型。接下来，对于任何你设置为索引字符串的参数，你需要查询字符串列表。你可以从表 5.3 中获取这些内容。现在 GUI 部分已完成，我们可以将注意力转向合成器本身。请记住，你需要实现这三步 GUI 编码来添加新控件。

# AUSynth.h

在 h 文件中，我们需要包含成员对象并声明它们。我们先从 `QBLimitedOscators` 开始。

# AUSynth.cpp

```cpp
void CNanoSynth::update() {
    // oscillators
    m_Osc1.m_Waveform = m_uWaveform;
    m_Osc2.m_Waveform = m_uWaveform;
    m_Osc1.update();
    m_Osc2.update();

    // --- LFO
    m_LFO1.m_Waveform = m_uWaveform;
    m_LFO1.m_Amplitude = m_dAmplitude;
    m_LFO1.m_Rate = m_dRate;
    m_LFO1.m_Mode = m_uMode;
    m_LFO1.update();
}
```

从文件顶部开始逐个处理函数：

```cpp
bool _stdcall CNanoSynth::processAudio(args...) {
    // render
    double dOut = 0.0;
    if(m_Osc1.m_bNoteOn) {
        // --- OSCILLATION BLOCK --
        // --- render LFO output
        double dLFOOut = m_LFO1.Oscillate();
    }
```

# 构造函数

你已经在那里设置了 GUI 控制。

## Initialize()

在 `Initialize()` 函数中执行上一节描述的一次性初始化。然后调用 `update()` 函数。

## update()

在 `update()` 函数中更新合成器变量。通过 `GetParameter()` 从容器中检索参数。始终调用子组件的 `update()` 函数以重新计算参数。

## Render()

按照之前的描述执行音频渲染。首先调用我们刚刚编写的 `update()` 函数。它设置了整个处理块的参数。与 VST3 一，你可能决定在块处理期间定期调用 `update` 以使参数的粒度更细。注意：RackAFX 以采样帧（单声道或立体声对）处理，因此控制变化在一个采样周期内生效。

# StartNote()

在 MIDI 日志之后添加来自 5.10 节的 Note On 事件代码。

```cpp
// --- apply modulation inputs
m_Osc1.setModExp(dLFOOut * OSC_MOD_RANGE);
m_Osc2.setModExp(dLFOOut * OSC_MOD_RANGE);

// -- update
m_Osc1.update();
m_Osc2.update();

// -- DIGITAL AUDIO ENGINE --
dOut = 0.5*m_Osc1.Oscillate() + 0.5*m_Osc2.Oscillate();
```

```cpp
pOutputBuffer[0] = dOut;

// Mono-In, Stereo-Out (AUX Effect)
if(uNumInputChannels == 1 && uNumOutputChannels == 2)
pOutputBuffer[1] = dOut;

// Stereo-In, Stereo-Out (INSERT Effect)
if(uNumInputChannels == 2 && uNumOutputChannels == 2)
pOutputBuffer[1] = dOut;
```

```cpp
return true;
```

# StopNote()

在 MIDI 日志之后添加来自 5.10 节的 Note Off 事件代码。

`__stdcall CNanoSynth::userInterfaceChange(int nControlIndex)`

```cpp
// --- all at once
update();
```

```cpp
// --- done
return true;
```

使用 Interface Builder 和第 2 章描述的方法设计你的 GUI。在 Xcode 中拷贝项目时，记住扁平 Cocoa 命名空间的问题。

# 5.38 NanoSynth: Wavetables

在你的平台上构建并测试插件。如果你想确保振荡器正常工作，请比较它们的频谱。独立开启 LFO 和调频振荡器然后尝试调制。接下来，你可以独立将准带限振荡器替换为波表振荡器进行比较。这在所有平台上都是简单且一致的。在插件对象的 .h 文件中，将波表振荡器替换为准带限振荡器：

```cpp
bool _stdcall CNanoSynth::midiNoteOn(args...)
{
    // test channel/ignore
    if(m_uMidiRxChannel != MIDI_CH_ALL && uChannel != m_uMidiRxChannel)
        return false;

    #ifdef LOG_MIDI
    TRACE("-- Note On Ch:%d Note:%d Vel:%d \n", uChannel, uMIDINote, uVelocity);
    #endif

    // INSERT ** Code Listing 5.1: Note On ** HERE

    return true;
}
```

```cpp
bool _stdcall CNanoSynth::midiNoteOff(args...)
{
    // test channel/ignore
    if(m_uMidiRxChannel != MIDI_CH_ALL && uChannel != m_uMidiRxChannel)
        return false;

    #ifdef LOG_MIDI
    TRACE("-- Note Off Ch:%d Note:%d Vel:%d \n", uChannel, uMIDINote, uVelocity);
    #endif

    // INSERT ** Code Listing 5.2: Note Off ** HERE

    return true;
}
```

```cpp
// our two oscillators
CQBLimitedOscillator m_Osc1;
CQBLimitedOscillator m_Osc2;

// one LFO
CLFO m_LFO1;

// update function for synth
void update();

// MIDI receive channel
UINT m_uMidiRxChannel;
// END OF USER CODE
```

# AU GUI 控制步骤 1

```cpp
// Add your code here:
```

```cpp
// our two oscillators
CQBLimitedOscillator m_Osc1;
CQBLimitedOscillator m_Osc2;
```

```cpp
// one LFO
CLFO m_LFO1;
```

```cpp
// update function for synth
void update();
```

```cpp
// MIDI receive channel
UINT m_uMidiRxChannel;
// END OF USER CODE
```

因此，在这种两个锯波振荡器硬同步（hard syncing）的情况下，我们产生了多个不连续点。

`result PLUGIN_API Controller::initialize(FUnknown* context)`

```cpp
// -- base class does its thing
tresult result = EditController::initialize(context);

// -- define the controls
if (result == kResultTrue)
{
    // -- Init parameters
    Parameter* param;

StringListParameter* enumStringParam = new StringListParameter(USTR("Osc Waveform"),
OS_WAVEFORM);
// 现在按照 Synth 项目 中枚举中声明的相同顺序为列表添加字符串
enumStringParam->appendString(USTR("SINE"));
enumStringParam->appendString(USTR("SAW1"));
enumStringParam->appendString(USTR("SAW2"));
enumStringParam->appendString(USTR("SAW3"));

enumStringParam->appendString(USTR("TRI"));
enumStringParam->appendString(USTR("SQUARE"));
enumStringParam->appendString(USTR("NOISE"));
enumStringParam->appendString(USTR("PNOISE"));
parameters.addParameter(enumStringParam);

enumStringParam = new StringListParameter(USTR("LFO Waveform"), LFO1_WAVEFORM);
// 现在添加字符串
enumStringParam->appendString(USTR("sine"));
enumStringParam->appendString(USTR("usaw"));
enumStringParam->appendString(USTR("dsaw"));
enumStringParam->appendString(uSTR("tri"));
enumStringParam->appendString(USTR("square"));
enumStringParam->appendString(USTR("expo"));
enumStringParam->appendString(USTR("rsh"));
enumStringParam->appendString(USTR("qrsh"));
parameters.addParameter(enumStringParam);

param = new RangeParameter(USTR("LFO Rate"), LFO1_RATE,
USTRING(MZ), MIN_LFU_KITE,
MAX_LFO_RATE, DEFAULT_LFO_RATE);

param->setPrecision(2); // 小数有效数字
parameters.addParameter(param);

param = new RangeParameter(USTRING("LFO1 Amplitude"),
LFO1_AMPLITUDE, USTRING(""),
MIN_UNIPOLAR, MAX_UNIPOLAR,
DEFAULT_UNIPOLAR);

param->setPrecision(1); // 小数有效数字
parameters.addParameter(param);

enumStringParam = new StringParameter(USTRING("LFO1 Mode"),
LFO1_MODE);
```

```cpp
// 现在添加字符串
enumStringParam->appendString(USTRING("sync"));
enumStringParam->appendString(USTRING("shot"));
enumStringParam->appendString(USTRING("free"));
parameters.addParameter(enumStringParam);
```

```cpp
// MIDI 参数 - 这些在 GUI 中没有旋钮，但必须
// 出现在默认列表中
// 注意：这仅适用于 VST3！AU 或 RAFX 不需要

etc...
```

我们的两个振荡器将使用某些耦合，我们需要知道在下一个采样周期内是否有待处理的重置（reset）操作，或者是否在采样周期内发生。如果没有待处理或正在发生的重置，我们仍然需要检查相对于普通锯波不连续点的位置。重置不连续点的高度是通过振荡频率比例的函数部分找到的。

图 5.51: 两个硬锯波波形的硬同步。

图 5.52: 两个硬锯波波形 (a) 和 (b) 的频谱，在 f (master) = 440 Hz 且 f (slope) = 600 Hz 时应用了双点 PolyBLEP。

BLEP/PolyBLEP 可用于平滑处理不连续点，但仍有一些主要问题需要解决。事实上，Brand 的专利并未披露任何实现细节或任何真实或模拟结果。在主从振荡器运行在较低频率的情况下，可以获得如图 5.52 所示的半离散结果，其中双点 PolyBLEP 已应用于不连续点。正如 Andrey 所指出的，当频率足够高且 BLEP 修正被应用于重叠脉冲时，或者当主从振荡器在同一采样间隔内重置时，就会出现问题（参见参考文献中的 Lear/Bright 专利）。这在主和/或振荡器频率变得非常高时尤为糟糕，此时会发生不可接受的混叠（aliasing）。产生图 5.52 的 PolyBLEP 振荡器受到此问题的影响，在较高的主从频率下或当同步率在高频下调制时，无法产生可接受的结果。

另开 Lear/Bright 专利，研究作者是如何处理硬同步情况的。使用提供的块来实现无混叠的硬同步振荡器部分。

```cpp
// -- 定义我们的控制器类 FUID
setControllerClass(Controller::cid);
```

# 参考文献

Brand, Eli. 2001. "Hard Sync Without Aliasing." Proceedings from the International Conference, Havana.

```cpp
// 初始化
m_uWaveform = DEFAULT_OSC;
m_LF1Waveform = DEFAULT_LFO;
m_dLF1Rate = DEFAULT_RATE;
m_dLF1Amplitude = DEFAULT_UNIPOLAR;
m_LF1Mode = DEFAULT_MODE;
```

Dattorno, Jon. 2003. "Effect Design Part 3." Journal of Audio Engineering, vol. 50, no. 3.

```cpp
// 所有通道
m_uChannel = DEFAULT_ALL;
```

imola, Jari and Välämki, 2012. "Reducing Aliasing from Synthetic Signals." IEEE Processing Letters, vol. 19, no. 2.

Leary, Andrew and Bright, Charles. 2009. "Alias-free Oscillators." IEEE Processing Letters.

```cpp
// 获取状态
m_uPitch = DEFAULT_BEND;
```

Pekonen, Jussi; Lazzarini, Victor; Timoney, Joseph; Kleimola, Jari; and Välämki, Vesa. 2011. "Discrete-Time Modeling of the Sawtooth Waveform." EURADISP Journal on Advances in Signal Processing.

Silston, Tim and Smith, Julius. 1996. "Digital Synthesis of Classic Waveforms." Proceedings from the 1996 International Music Conference.
