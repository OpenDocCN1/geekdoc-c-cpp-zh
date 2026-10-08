
因此，在这种两个锯波振荡器硬同步（hard syncing）的情况下，我们产生了多个不连续点。

result PLUGIN_API Controller::initialize(FUnknown* context)

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

## 参考文献

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

Välämki, Vesa and Huovilainen, Antti. 2005. "Oscillator and Filter Algorithms for Virtual Audio." Computer Music Journal, vol. 30, no. 2, pp. 19–31. Cambridge: MIT Press.

Välämki, Vesa. 2015. "Discrete-Time Synthesis of the Sawtooth Waveform With Reduced Aliasing." IEEE Signal Letters, vol. 12, no. 3.

Välämki, Vesa; Nam, Juhan; Abel, Jonathan; and Smith, Julius O. 2010. "Alias-Suppressed Oscillators on Differential Polynomial Waveforms." IEEE Transactions on Audio, Speech and Language Processing, vol. 18, no. 4.

