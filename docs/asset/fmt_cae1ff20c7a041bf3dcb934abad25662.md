
```
// --- RX 通道
UINT `m_uMidiRxChannel`;
```

```
// --- 调制矩阵
CModulationMatrix `m_GlobalModMatrix`;
```

```
// 调制矩阵需要这些变量
double `m_dDefaultModIntensity` // 1.0
double `m_dDefaultModRange` // 1.0
double `m_d0scFoModRange`;
double `m_dFilterModRange`;
```

```
// 用户代码结束
```

修改 `processAudioFrame()` 函数以使用新的调制矩阵：

在 `midiNoteOn()` 中添加一行代码，将新的音符编号写入调制矩阵的源数组中：

编译并测试合成器——它的声音和行为应该与之前完全相同，但现在使用的是调制矩阵。如果某些功能无法运行，请返回并仔细检查你的代码。

# 8.5 NanoSynth MM 第一部分：VST

将 `Modulation.h` 和 `.Matrix.cpp` 文件复制到你的项目文件夹中，并将它们添加到 Visual Studio 项目中。

## VSTSynthProcessor.h

打开 `VSTSynthProcessor.h` 文件并添加以下内容：

```
#include
"ModulationMatrix.h"
```

在变量声明中，添加矩阵及其强度、范围变量。

## VSTSynthProcessor.cpp

在构造函数中，添加调制范围的初始化。确保你理解如何根据表 8.1 设置矩阵行，这样你就可以随着项目轻松地添加更多调制路由。

在 `setActive()` 中，初始化对象，然后动态分配矩阵行，并在激活时使用源/目标索引值以及指向全局矩阵的调制矩阵指针来初始化组件，在取消激活时销毁全局矩阵。

在 `update()` 中添加代码来启用和禁用

```
CNanoSynth::CNanoSynth(
{
// RackAFX 添加 - 不要删除
//
initUI();

// END initUI()
)

<SNIP SNIP SNIP>

// 接收自所有通道
```

```
// -- 创建调制矩阵行
// 在此此处插入 ** 代码列表 8.1: 调制矩阵路由 ** >>
// -- 在组件上设置源和目标索引
// 在此此处插入 ** 代码列表 8.2: 调制矩阵连接 I ** >>
```

```
m_uMidiRxChannel = MIDI_CH_ALL;

// -- 初始化调制范围
m_DefaultModIntensity = 1.0;
m_DefaultModRange = 1.0;

// -- 初始化调制范围
m_0dScFoModRange = OSC_FO_MOD_RANGE;
m_dfFilterModRange = FILTER_FC_MOD_RANGE;
```

矩阵中的滤波器音键跟踪行。

在 `process()` 中移除旧的硬编码代码，并替换为使用调制矩阵的精简版本。

在 `doProcessEvent()` 中修改音符开启逻辑，将数字写入矩阵：

```
CNanoSynth::CNanoSynth(void)
{
// -- 仅主主删除
m_GlobalModMatrix.deleteModMatrix();
```

编译并测试合成器——它的声音和行为应该与之前完全相同，但现在使用的是调制矩阵。如果某些功能无法运行，请返回并仔细检查你的代码。

```
bool __stdcall cNanoSynth::processAudioFrame(float* pInputBuffer,
float* pOutputBuffer,
UINT uNumInputChannels,
UINT uNumOutputChannels;
```

```
double dOutL = 0.0;
double dOutR = 0.0;
```

```
if(m_Osc1.m_bNoteOn)
{
    << 插入 ** 代码列表 8.3: 调制矩阵渲染 I ** >>

// 现在检查音符关闭
if(m_EG1.getState() == 0) // 0 - 关闭
{
    m_Osc1.stoposcillator();
    m_Osc2.stoposcillator();
    m_LF01.stoposcillator();
    m_EG1.stopEG();
}
```

```
pOutputBuffer[0] = dOutL;
```

```
<SNIP SNIP SNIP>
```

```
return true;
}
```

```
bool __stdcall cNanoSynth::midiNoteOn(UINT uChannel, UINT uMIDINote,
UINT uVelocity)
```

# NanoSynth MM 第一部分：AU

将 `ModulationMatrix.h` 和 `.cpp` 文件添加到你的 Xcode 项目。然后修改 `AUSynth` 对象：

```
// 测试通道/忽略
if(m_uMidiRxChannel != MIDI_CH_ALL && uChannel != m_uMidiRxChannel)
    return false;
```

```
<SNIP SNIP SNIP>

// 如果未播放，重置并执行 update0Oscillator
if(!m_Oscl1.m_bNoteOn)
(
    m_osccl1.startOscillator(); // 这执行了 update0Oscillator()
    m_osccl2.startOscillator();
)
else // 如果音符正在播放，仅更改音高
(
    m_osccl1.updateOscillator();
    m_osccl2.updateOscillator();
)

// --- KT 路由
// 在调制矩阵中为滤波器音键跟踪设置音符
m_GlobalModMatrix.m_dSources[SOURCE_MIDI_NOTE_NUM] = uMIDiNote;

return true;
```

### USynth.h

打开 `VSTSynthProcessor.h` 文件并添加以下内容：

```
#include
"ModulationMatrix.h"
```

在变量声明中，添加矩阵及其强度、范围变量。

### USynth.cpp

在构造函数中，初始化对象和矩阵。确保你理解如何根据表 8.1 设置矩阵行，这样你就可以随着项目轻松地添加。

在 `update()` 中添加代码来启用/禁用滤波器音键跟踪。

在 `Render()` 中修改函数以使用新的调制矩阵。首先获取你声明的新变量的最新值，然后使用之前描述的代码渲染音频。

# Class Processor : public AudioEffect

public:

在 `StartNote()` 中修改音符逻辑，将数字写入矩阵：

```
<SNIP SNIP SNIP>
CMoogLadderFilter m_Filter;
// -- 调制矩阵
ModulationMatrix m_GlobalMatrix;
// 调制矩阵需要这些变量
double m_dDefaultModIntensity // 1.0
double m_dDefaultModRange // 1.0
double m_d0scFoRange;
double m_dFilterModRange;
```

编译并测试合成器——它的声音和行为应该与之前完全相同，但使用的是调制索引。如果某些功能无法运行，请返回并仔细检查你的代码。

# 8.7 更多 MIDI 调制路由

在本节中，我们将添加所有合成器将拥有的 MIDI 调制路由。这包括添加速度到 DCA 的路由，以便你的合成器具有速度敏感性。表 8.4 列出了新的调制路由。

前四行非常显而易见——我们希望将速度映射到 DCA 输入，将音程映射到振荡器音高，并将 MIDI 音量和全景控制（分别为 CC7 和 CC10）映射到 DCA 音量和全景输入。延音踏板发送低于 64（关闭）或大于 64（开启）的值。MIDI 开启/开关处理这种简单的技术。

这些并不是唯一的路由——你可以在这里变得非常聪明且富有表现力。例如，你可以添加一行让 MIDI 速度改变截止频率的路由，使截止频率随着速度的增加而上升。将 MIDI 音符作为调制源也非常流行。最后两个路由更高级，因为它们是层 0 调制。这些调制需要在包发生器写入其输出之前应用。

表 8.4：用于所有合成器的附加 MIDI 调制路由。

# Processor::Processor()

```
<SNIP SNIP SNIP>

m_dFilterKeyTrackIntensity = DEFAULT_FILTER_KEYTRACK_INTENSITY;
m_dDEGIoscIntensity = DEFAULT_BIPOLAR;

// --- 初始化强度
m_dDefaultModIntensity = 1.0;
m_dDefaultModRange = 1.0;
m_dOscFoModRange = OSC_FO_MOD_RANGE;
m_dFilterModRange = FILTER_FC_MOD_RANGE;

// VSTMIDID 特定
m_dDMIDIPitchBend = DEFAULT_MIDI_PITCHBEND; // -1 到 +1
```

etc...

```
tresult PLUGIN_API Processor::setActive(TBool state)
{
if(state)
{
  <SNIP SNIP SNIP>

  // 清空
m_dlastNoteFrequency = 0.0;

  // -- 创建调制矩阵行
  << 插入 ** 代码列表 8.1: Mod Matrix Routings I ** 此此处 >>
  // -- 在组件上设置源和目的索引
  << 插入 ** 代码列表 8.2: Mod Matrix Connections I ** 此此处 >>
}
```

etc...

# 持续延踏板 (Sustain Pedal)

MIDI 持续踏板直接影响 EG 对象；当按住持续踏板时，EG 将保持在持续（sustain）状态，即使音符已释放。这被称为持续踏板覆盖（sustain pedal override）。当发生持续踏板覆盖时，我们会设置一个指示此条件的标志。当在按住持续踏板的情况下释放音符时，我们将设置释放（release）标志，表示我们需要在释放持续踏板时移动到释放状态。

```
 // --- 执行关闭相关操作；删除上方分配的内存
if(m_pFilterLogParam)
    delete m_pFilterLogParam;

// --- 仅在主实例上删除
m_GlobalModMatrix.deleteModMatrix();

// --- 最后调用基类方法
return AudioEffect::setActive(state);

void Processor::update() {
    <SNIP SNIP SNIP>
    // --- DCA
    m_DCA.setPanControl(m_dPanControl);
    m_DCA.setAmplitude_dB(m_dVolume_dB);

    // -- 调制矩阵处理
    if(m_FilterKeyTrack == 1)
        m_GlobalModMatrix.enableMatrixRow(SOURCE_MIDI_NOTE_NUM, DEST_ALL_FILTER_KEYTRACK, true);
else
        m_GlobalModMatrix.enableMatrixRow(SOURCE_MIDI_NOTE_NUM, DEST_ALL_FILTER_KEYTRACK, false);
}
```

# 速度到攻击时间缩放 (Velocity to Attack Scaling)

在这种调制中，键力度控制攻击时间（attack time）；较高的速度会缩短攻击时间，而较低的速度则不会（或者相反地延长它）。在这种情况下，我们跨速度线性硬编码了缩放范围，但你可以更改此以创建各种奇特的攻击时间缩放调制路由。

# Note

```
tresult PLUGIN_API Processor::process(ProcessData& data)
{
    <SNIP SNIP SNIP 缩进已移除>

    // --- 输出累加器*
    double dOutL = 0.0;
    double dOutR = 0.0;

    for(int32 j=0; j<samplesToProcess; j++) {
        // --- 清空累加器
        dOutL = 0.0;
        dOutR = 0.0;

        if(m_0sc1.m_bNoteOn) << << 插入 ** 代码列表 8.3: Mod Matrix Render ** 此此处 >>

            // 现在检查音符释放
            if(m_EG1.getState() == 0) // 0 - 关闭 {
                m_0sc1.stoposcillator();
                m_0sc2.stoposcillator();
                m_LF01.stoposcillator();
                m_EG1.stopEG();
            }
        }
    }
    etc...
```

# 音号到衰减时间缩放 (Number to Decay Scaling)

在这种调制中，音号缩放包络的衰减时间（decay time）。通常，将其设置为较高的音号会缩短衰减时间，而较低的数字则不会（或者相反地延长它）。缩放可能仅应用于衰减时间，也可以同时应用于衰减和释放时间。

这两种调制都需要将 MIDI 值 [0..127] 归一化为 [0..] 然后反转 [1..]，这是因为调制的方向（注意：你也可以尝试相反的版本）。我们需要在 EG 对象中额外添加四个变量，用于处理持续踏板和两个新的调制路由。在 .h 文件中声明这些变量：

接下来，实现设置此覆盖值的函数。如果释放了持续键且我们有释放踏板，则调用 `noteOff()` 方法，将 EG 转移到释放状态。

最后，在 `doEnvelopeGenerator()` 函数中实现持续覆盖。只要按住踏板，EG 就会保持在释放状态。我们将在讨论这种调制路由时添加剩余的持续踏板代码。

修改函数中的释放状态部分，以便在发生持续覆盖时保持持续电平。

`bool Processor::doProcessEvent(Event&, vstEvent)`

在

.h

.cpp

文件中，首先

```
<SNIP SNIP SNIP>

// -- 关于音符开启的注意 (NOTE ON)
case Event::kNoteEvent:
(
    <SNIP SNIP SNIP>

m_LFQ1.startOscillator();
m_EG1.startEG();

// -- 调制矩阵中滤波器跟踪的音号
m_GlobalModMatrix.m_dSources[SOURCE_MIDI_NOTE_NUM] - uID;

    break;
```

etc...

在构造函数中添加这些变量。

class Synth：

| 控制名称 | 变量名 | 枚举类型 | VST3 索引 |
|---|---|---|---|

| 速度->攻击 | m_velocityToAttack | 关闭/开启 | VELOCITY_ATTACK |
| 音号->衰减 | m_numberToDecay | 关闭/开启 | NOTE_NUM_DECAY |

你还需要对 MIDI 消息处理进行一些修改，因为这些调制是平台特定的，我们将单独处理它们。在 8.5 表中添加新的 GUI 控制。

## 8.8 NanoSynth 第二部分: RackAFX

添加新的 GUI 控制，在项目的 .h 文件中使用一些范围变量：

```
AUSynth(AudioUnit inComponent)
  : AuInstrumentBase(inComponent, 0)
```

```
// 创建输入、输出端口、组和部分
CreateElements();
```

# NanoSynth.h

![](img/b42d0dca53f4a889d8162d5f7c8c05d_507_0.png)

添加变量声明：

# NanoSynth.cpp

在构造函数中：

```
// 接收所有通道
m_uidiRXChannel = MIDI_CH_ALL;
```

```
m_DEGI0scIntensity = 0.0;
m_DEGI1CAIntensity = 1.0;
m_dFilterKeyTrackIntensity = 1.0;
```

初始化范围变量：

```
// 初始化强度
m_dDefaultModIntensity = 1.0;
m_dDefaultModRange = 1.0;
```

```
// 初始化调制范围
m_d0OscModRange = OSC_FO_MOD_RANGE;
m_dFilterModRange = FILTER_FC_MOD_RANGE;
```

```
// --- 调制矩阵
CMulationMatrix m_GlobalModMatrix;
```

// --- 仅在 AU 中

m_DEGI0scIntensity = 0.0;

m_DEGI1CAIntensity = 1.0;

m_dFilterKeyTrackIntensity = 1.0;

// --- 更新所有声音

void update();

```

所以，我们需要设置一个默认值。这在 `prepareForPlay()` 中很容易实现，只需将值强制送入矩阵 `ASynth::update()` 中。

```cpp

<SNIP SNIP SNIP>

// / -- 矩阵相关操作
```
