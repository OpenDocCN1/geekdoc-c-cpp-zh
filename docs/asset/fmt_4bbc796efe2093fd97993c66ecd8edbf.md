
```cpp
bool doControlUpdate(ProcessData& data);

// 用于 MIDI 音符开启/关闭

bool doProcessEvent(Event& vEvent);

// 一次更新所有声音

void update();

};
```

现在在构造函数 `VSTProcessor` 中初始化它。在 `synthfunctions.h` 中有一个枚举，可以容纳 16 个通道加上全模式：

```cpp
// -- 我们的接收通道
UINT m_uMidiRxChannel;
```

```cpp
enum midiChannels(
    MIDI_CH_1 = 0, MIDI_CH_2, MIDI_CH_3, MIDI_CH_4, MIDI_CH_5,
    MIDI_CH_6, MIDI_CH_7, MIDI_CH_8, MIDI_CH_9, MIDI_CH_10,
    MIDI_CH_11, MIDI_CH_12, MIDI_CH_13, MIDI_CH_14, MIDI_CH_15, MIDI_CH_16,
    MIDI_CH_ALL);
```

```cpp
## Processor::Processor() {
    // -- 我们是一个 Processor
    setControllerClass(Controller::);
    // -- 我们的初始化
    // 在所有通道上接收
    m_uMidiRxChannel = MIDI_CH_ALL;
}
```

```cpp
#define LOG_MIDI 1
```

当 MIDI 音符开启时，我们希望记录该事件、音符编号和速度，显示方式所示：

```
-- Note On: Ch: 1 Note:60
Vel:96
```

这表示在 MIDI 通道 1 上的音符开启事件，MIDI 音符编号为 60（中音），速度为 96。你可以按照喜欢的方式格式化字符串，但上述方法简单明了。找到 `doProcessEvents()` 函数，找到音符开启、音符关闭、多声道压力的 `case` 语句。用 `FDebugPrint` 语句填充它们。注意 `doProcessEvent()` 在处理了事件后返回 `true`。现在你可以安全地忽略音符开启和关闭选项涉及 `noteID` 的第一行。你在这些函数中执行的第一件事是测试 MIDI 通道，以确保你能够在其上接收消息。这些代码在所有函数中几乎是相同的。`FDebugPrint` 宏仅在项目的调试版本中可用，这就是为什么你在 `#if` 语句中看到了额外的 `_DEBUG` 术：

```cpp
#if(LOG_MIDI && _DEBUG)
#endif
// 测试通道/忽略
if(m_uMidiRxChannel != MIDI_CH_ALL && uChannel != m_uMidiRxChannel)
    return false;
```

```cpp
bool Processor::doEvent(Event& v) {
    bool noteEvent = false;
    // --- 在此处处理 Note On 或 Note Off 消息
    switch(vstevent.type) {
        // --- NOTE ON (音开启)
        case Event::kNoteEvent:
        {
            // --- 获取通道/音符/力度
            UINT uMIDiChannel = (UINT)vstevent.noteon.channel;
            UINT uMIDiNote = (UINT)vstevent.noteon.pitch;
            UINT uMIDiVelocity = (UINT)((127.0) * vstevent.noteon.velocity);
            // --- 通道/忽略
            if(m_uMidiRxChannel != MIDI_CH_ALL && uMIDiChannel != m_uMidiRxChannel)
                return false;
            // --- 发生事件
            noteEvent = true;
            // --- 根据 SDK 修正 noteid
            if(vstevent.noteon.noteid == -1)
                vstevent.noteon.noteid = uMIDiNote;
            #if(LOG_MIDI && _DEBUG)
            DebugPrint("-- Note On Ch:%d Note:%d Vel:%d \n", uMIDiChannel, uMIDiNote, uMIDiVelocity);
            #endif
            break;
        }
        // --- NOTE OFF (音关闭)
        case Event::kNoteOffEvent:
        {
            // --- 获取通道/音符/力度
            UINT uMIDiChannel = (UINT)vEvent.noteoff.channel;
            UINT uMIDiNote = (UINT)vEvent.noteoff.pitch;
            UINT uMIDiVelocity = (UINT)(127.0 * vEvent.noteoff.velocity); // 未使用
            // --- 测试通道/忽略
            if(m_uMidiRxChannel != MIDI_CH_ALL && uMIDiChannel != m_uMidiRxChannel)
                return false;
            // --- 发生事件
            noteEvent = true;
            // --- 根据 SDK 修正 noteID
            if(vEvent.noteoff.noteID == -1)
                vEvent.noteoff.noteID = uMIDiNote;
            #if(LOG_MIDI && _DEBUG)
            FDebugPrint("-- Note Ch:%d Note:%d Vel:%d \n", uMIDiChannel, uMIDiNote, uMIDiVelocity);
            #endif
            break;
        }
        // --- 多声触 (polyphonic aftertouch)
        case Event::kPolyPressureEvent:
        {
            // --- 获取通道
            UINT uMIDIDChannel = (UINT)vEvent.polypeure.channel;
            UINT uMIDINote = (UINT)vEvent.polypeure.pitch;
            float fPressure = vEvent.polypeure.pressure;
            // --- 测试通道/忽略
            if (m_uMidiRxChannel != MIDI_CH_ALL && uMIDIDChannel != m_uMidiRxChannel)
                return false;
            //--- 音事件未发生
            noteEvent = false;
            #if(LOG_MIDI && _DEBUG)
            FDebugPrint("-- Poly Pressure Ch:%d Note:%d Value:%d\n", uMIDIDChannel, uMIDINote, fPressure);
            #endif
            break;
        }
    }
    // -- 是否发生了音事件？
    return noteEvent;
}
```

我们将在接下来的章节中添加额外的代码来启动和停止振荡器并控制合成器。在此期间，对于 MIDI 事件你只需要完成这些操作。

## 3.8 VST3 中的 MIDI 控制器

有趣的是（也令人困惑的是），VST 宿主不会直接将 MIDI 控制变化（control changes）传递给你的插件。Steinberg 试图通过这一点来解释：直接将 MIDI 数据传递到使用该数据更改其参数和 GUI 的插件中可能会干扰宿主的自动化。为了让事情变得更有趣，VST3 将通道压力（Channel Pressure）和音高偏移（Pitch Bend）消息与控制索引值分组在一起。这些是 MIDI 消息，而不是控制器索引！这产生了一个需要大于 127 的索引值的情况，这可能会让验证程序产生混乱。

如果你接收这些消息，VST3 需要使用 MIDI 映射（MIDI Map）。其思路是创建一个带有参数控制控件的 GUI，并将 CC——例如，表情（Expression）——映射到你的参数之一，例如滤波器截止频率（Filteroff Frequency）。默认情况下，调制轮（mod wheel）始终映射到 LFO。音量控制通常映射到输出电平。

一个简单的解决方案是为你想要接收的 MIDI 消息创建虚拟参数（dummy parameters）。你并不打算用户在最终的 GUI 上看到它们。然后，将这些控制器消息映射到你的虚拟参数上。在 `process()` 函数期间，这些参数被提取出来就像它们来自 GUI 一样。一个根本性的缺点是参数值（Parameter value）在 0 到 1 之间归一化。通道信息丢失了，因此你不知道原始的 CC 通道。一个名为 `doUIControl()` 的辅助函数处理参数变化。它在 `process()` 函数中被调用，该函数在其参数中接收事件。

### 定义参数索引值

对于所有 GUI 参数，这些虚拟参数通过一个索引值进行标识。我们使用相同的索引来初始化参数，并在稍后 `doUIControl()` 函数中解码时使用。对于所有 VST3 合成器，这些参数索引值是通过位于 `SynthParamLimits.h` 顶部的枚举实现的：

```cpp
enum {
    MIDI_PITCHBEND,
    MIDI_MODWHEEL,
    MIDI_VOLUME_CC7,
    MIDI_PAN_CC10,
    MIDI_EXPRESSION_CC11,
    MIDI_SUSTAIN_PEDAL,
    MIDI_CHANNEL_PRESSURE,
    MIDI_ALL_NOTES_OFF // 最后
```

### 初始化 MIDI 参数

GUI 参数始终在 `Controller::initialize` 函数中创建并初始化。初始化参数对象涉及将它们与枚举索引关联，同时建立最大值和默认值。我们的参数值传递到 `Processor` 时已经是归一化值，因此简单的方法是将它们设置为单极性（unipolar）。`SynthParamLimits.h` 文件包含了所有合成器参数的最大值和默认值声明，并包含了双极性（bipolar）限制。打开 `SynthController.cpp` 文件并设置变量（如果需要，请参考第 2 章）、以及限制：

```cpp
PLUGIN_API Controller::initialize(FUnknown* context)
{
    // -- 基类处理其逻辑
    result = EditController::initialize(context);
    // -- 现在定义控件
    if(result == kResultTrue) {
        // 初始化
        Parameter* param;
        // MIDI 参数在自定义 GUI 中没有旋钮，但必须出现在默认中
        // 注意：仅限 V3！AU 或 RAF 不需要
        param = new RangeParameter(UString("PitchBend"), MIDI_PITCHBEND, UString(" MIN_UNIPOLAR, MAX_UNIPOLAR, DEFAULT_UNIPOLAR);
        param->setPrecision(1);
        parameters.addParameter(param);
        param = new RangeParameter(UString("MIDI Vol1"), MIDI_VOLUME_CC7, UString(" MIN_UNIPOLAR, MAX_UNIPOLAR, DEFAULT_UNIPOLAR);
        param->setPrecision(1);
        parameters.addParameter(param);
        param = new RangeParameter(UString("MIDI Pan"), MIDI_PAN_CC10, UString(" MIN_UNIPOLAR, MAX_UNIPOLAR, DEFAULT_UNIPOLAR);
        param->setPrecision(1);
        parameters.addParameter(param);
        param = new RangeParameter(UString("MIDI Mod Wheel"), MIDI_MODWHEEL, UString(" MIN_UNIPOLAR, MAX_UNIPOLAR, DEFAULT_UNIPOLAR);
        param->setPrecision(1);
        parameters.addParameter(param);
        param = new RangeParameter(UString("MIDI Expression"), MIDI_EXPRESSION_CC11, UString(" MIN_UNIPOLAR, MAX_UNIPOLAR, DEFAULT_UNIPOLAR);
        param->setPrecision(1);
        parameters.addParameter(param);
    }
}
```

```cpp
param->setPrecision(1);
parameters.addParameter(param);
param = new RangeParameter(USTRING("MIDI Sustain Pedal"),
MIDI_SUSTAIN_PEDAL, USTRING(""),
MIN_UNIPOLAR, MAX_UNIPOLAR,
DEFAULT_UNIPOLAR);
param->setPrecision(1);
parameters.addParameter(param);
param = new RangeParameter(USTRING("All Notes Off"),
MIDI_ALL_NOTES_OFF, USTRING(""),
MIN_UNIPOLAR, MAX_UNIPOLAR,
DEFAULT_UNIPOLAR);
param->setPrecision(1);
parameters.addParameter(param);
)
return kResultTrue;
```

下一步是重写并实现 `IMidiMapping` 接口函数 `getMidiControllerAssignment()`，并将 MIDI 控制映射到您的虚拟参数。这涉及到解码 `midiControlNumber` 并将参数 ID 值设置为您关联参数索引。

```cpp
tresult PLUGIN_API Controller::getMidiControllerAssignment(
int32 busIndex,
int16 channel,
CtrlNumber midiControllerNumber,
ParamID& id /*out*/ );
```

```cpp
// 注意：我们只有一个 EventBus(0)
// 但它上面有 16 个通道
if(busIndex == 0)
{
    id = -1;
    switch (midiControllerNumber)
    {
        // 处理逻辑请参见 Processor::process() 方法
        case kPitchBend:
            id = MIDI_PITCHBEND;
            break;
        case kCtrlModWheel:
            id = MIDI_MODWHEEL;
            break;
        case kCtrlVolume:
            id = MIDI_VOLUME_CC7;
            break;
        case kCtrlPan:
            id = MIDI_PAN_CC10;
            break;
case kCtrlExpression:
```
