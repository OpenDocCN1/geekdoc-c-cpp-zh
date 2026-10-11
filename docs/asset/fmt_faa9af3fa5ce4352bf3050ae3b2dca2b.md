
`bool __stdcall CNanoSynth::midiNoteOff(UINT uChannel, UINT uMIDiNote, UINT uVelocity, bool bAllNotesOff)` {

  // test channel/ignore

  if(m_uMidiRxChannel != MIDI_CH_ALL && uChannel != m_uMidiRxChannel)

    return false;

#ifdef LOG_MIDI

  if(bAllNotesOff)

    TRACE("-- All Notes Off Ch:%d \n", uChannel);

  else

    TRACE("-- Note Off Ch:%d Note:%d Vel:%d \n", uChannel, uMIDiNote, uVelocity);

#endif

  return true;

}
```

```cpp
bool __stdcall CNanoSynth::midiModWheel(UINT uChannel, UINT uModValue)
{
  // test channel/ignore
  if(m_uMidiRxChannel != MIDI_CH_ALL && uChannel != m_uMidiRxChannel)
    return false;
#ifdef LOG_MIDI
  TRACE("-- Mod Wheel Ch:%d Value:%d \n", uChannel, uModValue);
#endif
  return true;
}
```

构建 MIDI 日志以确保你已正确捕获消息。现在为音弯消息（Pitch Bend Message）添加代码。RackAFX 会自动从 14 位拼接字中计算音弯值，并将其交付两种形式：实际值是一个双极整数，而归一化值是一个浮点数。此消息将以以下格式记录：

`+ Pitch Bend Ch:1 int:2048 float:0.2500`

其中第一项是双极值 (`+2048`)，第二项是归一化版本 (`0.25`)。再次构建并测试你的插件，注意当你移动音弯控制控件时，状态窗口中会流过音弯值。

```cpp
// nActualPitchBendValue             = -8192 -> +8191, 0 at center
// fNormalizedPitchBendValue      = -1.0 -> +1.0, 0 at center
bool __stdcall CNanoSynth::midiPitchBendValue(UINT uChannel, int nActualPitchBendValue, float fNormalizedPitchBendValue)
{
  // test channel/ignore
  if (m_uMidiRxChannel != MIDI_CH_ALL && uChannel != m_uMidiRxChannel)
    return false;
#ifdef LOG_MIDI
  TRACE("-- Pitch Bend Ch:%d int:%d float:%f \n", uChannel, nActualPitchBendValue, fNormalizedPitchBendValue);
#endif
  return true;
}
```

所有剩余消息都将在全捕获函数 `finish()` 中处理，但它默认是不启用的。要启用它，你需要在构造函数中设置一个标志（你会在所有合成器中都这样做），让 RackAFX 知道你将处理所有消息。返回构造函数，在指定区域添加以下行代码。

现在我们需要解码剩余的消息（总共十种）：

`CNanoSynth::CNanoSynth()`

音色消息：

- 触后（Aftertouch）
- 控制变化（Control Change）
    - 声相控制 Pan CC10
    - 表达控制 Expression CC11
    - 延延板 Sustain Pedal CC64
- 程序更改（Program Change）
- 通道压力（Channel Pressure）

```cpp
// Added by RackAFX - DO NOT REMOVE
//
// initUI() for GUI controls
```

< SNIP SNIP SNIP>

```cpp
// Finish initializations here
// receive on all channels
m_uMidiRxChannel = MIDI_CH_ALL;
// set flag for all MIDI
m_bWantAllMIDIMessages = true;
```

你可以使用 `synthfunctions.file` 中的常量定义来提高代码的可读性。在 `CNanoSynth.cpp` 文件找到 `midiMessage()` 函数。注意参数是字节（unsigned char - byte）。然后，如果是 CC，首先解码 `cStatus` 字节。然后，如果控制编号是第一个数字的 `cData1`。这些都是通过 `switch/case` 语句完成的。CC 逻辑中的 `default` 处理任何未被你的支持列表捕获到的内容。MIDI 通道测试代码略有不同，因为通道必须转换为 `UINT`。此外注意延延板的逻辑，

```cpp
bool __stdcall CNanoSynth::midiMessage(unsigned char cChannel, unsigned char cStatus, unsigned char cData, unsigned char cData2)
{
  // test channel/ignore
  if(m_uMidiRxChannel != MIDI_CH_ALL && (UINT)cChannel != m_uMidiRxChannel)
    return false;
  switch(cStatus) {
    case POLY_PRESSURE:
      #ifdef LOG_MIDI
      TRACE("-- Poly Pressure Ch:%d Value:%d \n", (UINT)cChannel, (UINT)cData1, (UINT)cData2);
      #endif
      break;
    case CONTROL_CHANGE:
      switch(cData) {
        case VOLUME_CC07:
          #ifdef LOG_MIDI
          TRACE("-- Volume Ch:%d Value:%d \n", (UINT)cChannel, (UINT)cData2);
          #endif
          break;
        case PAN_CC10:
          #ifdef LOG_MIDI
          TRACE("-- Pan Ch:%d Value:%d \n", (UINT)cChannel, (UINT)cData2);
          #endif
          break;
        case EXPRESSION_CC11:
          #ifdef LOG_MIDI
          TRACE("-- Expression Ch:%d Value:%d \n", (UINT)cChannel, (UINT)cData2);
          #endif
          break;
        case SUSTAIN_PEDAL:
          // -- 64 or greater = ON for switch messages
          bool sus = (UINT)cData2 > 63 ? true : false;
          #ifdef LOG_MIDI
          if(sus)
            TRACE("-- Sustain Pedal ON");
          else
            TRACE("-- Sustain Pedal OFF");
          #endif
          break;
        case ALL_NOTES_OFF:
          // // handled in midiNoteOff() for RackAFX
          break;
        case MOD_WHEEL:
          // // handled separately
          break;
        // all other controllers
        default:
          #ifdef LOG_MIDI
          if((UINT)cData1 != RESET_ALL_CONTROLLERS)
            TRACE("-- CC Ch:%d Num:%d Value:%d \n", (UINT)cChannel, (UINT)cData1, (UINT)cData2);
          #endif
          break;
      }
      break;
    case PROGRAM_CHANGE:
      #ifdef LOG_MIDI
      TRACE("-- Program Change Ch:%d Value:%d \n", (UINT)cChannel, (UINT)cData);
      #endif
      break;
    case CHANNEL_PRESSURE:
      #ifdef LOG_MIDI
      TRACE("-- Channel Pressure Ch:%d Value:%d \n", (UINT)cChannel, (UINT)cData);
      #endif
      break;
  }
  return true;
}
```

```cpp
bool __stdcall CNanoSynth::midiNoteOn(UINT uChannel,
                               UINT uMIDINote,
                               UINT uVelocity)
{
    // 测试通道/忽略
    if (m_uMidiRxChannel != MIDI_CH_ALL && uChannel != m_uMidiRxChannel)
        return false;
    // --- 将 NOTE 转换为 char*
    char* note = uintToString(uMIDINote);
    // -- 添加空格
    char* note_ = addStrings(note, " ");
    // -- 将 VEL 转换为 char*
    char* vel = uintToString(uVelocity);
    // -- 创建子字符串
    char* noteVel = addStrings(note_, vel);
    // -- 最终消息
    char* message = addStrings("MIDI Note On: ", noteVel);
    // -- 记录它！
    sendStatusWndText(message);
    // -- 清理
    delete [] note;
    delete [] note_;
    delete [] vel;
    delete [] noteVel;
    delete [] message;
    return true;
}
```

第一步是使用 `uintToString()` 将音符转换为字符串（还有 `floatToString()`、`doubleToString()` 和 `intToString()` 函数）。然后，使用 `addStrings()` 插入分隔音符和速度的空格。同样，将速度转换为字符串，并在另一个 `addStrings()` 调用中将其与音符拼接。最终消息通过将字符串字面量 `"MIDI Note On: "` 添加到音符/速度组合来创建。调用状态日志消息，然后删除所有的 `char*`。这样做的原因是，所有数字到字符串的转换函数以及 `addStrings()` 都会从内存中分配返回的字符串。由调用者在完成后后删除这些字符串。我们在 RackAFX 中选择使用 `char*` 是为了尽可能地增加与 macOS 以及我们之前支持的任何 C++ 编译器的兼容性。

编译插件并将其加载到 RackAFX 中，打开状态窗口并在你的控制器上弹几个音符。你可以看到窗口顶部记录了几个事件——这是因为 RackAFX 使用状态窗口向用户提供信息。你可以区分出来，来自插件的消息是缩进的。如果你想使用状态窗口，请先确保这第一条消息日志正常工作，然后再实现剩下的 MIDI 日志。

## 3.6 NanoSynth: VST3

以 `TemplateSynth` 或带有 MIDI 项目的 `TemplateSynth` 为基础，并按照附录 A 中的指令将其改为 NanoSynth。它预装了所需的头文件以及你的第一个名为 `VSynthParamLimits.h` 的文件，你将为每个合成器修改该文件。如果你想通过编写本章的 MIDI 日志器来练习，请使用 `TemplateSynth`；另一个带有 MIDI 的 `TemplateSynth` 包含了本章的 MIDI 日志代码，但没有其他内容。

VST3 处理 MIDI 的方式非常特殊且令人困惑。从一开始开始，VST3 就不支持语音程序更改（0xn 其中 n = 通道），因此我们将在我们的 VST3 版本中省略它。处理连续控制器消息（Continuous Controller Messages）的机制非常有限；为了通过直接将 MIDI 控制器映射到你的控件来让你的生活更轻松，创建一个调制矩阵变得更加困难，因为控制器可能有多个目标并且需要动态配置。某些事件（如音符开启和关闭）以典型方式处理，但其他则不是。VST3 还提供了一种名为 Note Expression（音符表达式）的 MIDI 控制器，但我们不会在书中的任何项目中使用。

## 3.7 VST3 中的 MIDI 事件

VST3 将消息分为两个部分：事件（events）和控制变化（control changes）。事件包括音符开启、音符关闭、多声道压力（触后）、独占以及两种音乐类型：和（chord）和音阶（scale）。不同的事件以结构的形式传递——每个事件都有不同的结构。所有的和和音阶事件都包含标准的 MIDI 信息，如通道、音符编号、速度等。

事件封装在 VST3 Event 结构中，它包含一个事件类型索引以及一组作为联合（union）封装的成员结构。事件类型索引命名为 `type`。我们将捕获以下事件类型：

```
kNoteEvent
kNoteOffEvent
kPolyPressureEvent
```

每个类型对应于 union 中的一个：

```
NoteOnEvent
noteOn
NoteOffEvent noteOff
PolyPressureEvent polyPressure
```

将结构体放在 union 中可以方便访问各种事件属性。传递到 `doProcessEvent()` 的 Event 被命名为 `vstEvent`。对于音符开启和音符关闭，你像普通的 MIDI 范围（0–127）中这样获取通道、音符和速度：

音符开启：

```cpp
UINT uMIDiChannel = (UINT) vstEvent.noteOn.channel;
UINT uMIDINote = (UINT) vstEvent.noteOn.pitch;
UINT uMIDIVelocity = (UINT)(127.0*vEvent.noteOn.velocity);
```

音符关闭：
```cpp
UINT uMIDIChannel = (UINT)vEvent.noteOff.channel;
UINT uMIDIDoteNote = (UINT)vEvent.noteOff.pitch;
UINT uMIDIVelocity = (UINT)(127.0*vEvent.noteOff.velocity);
```

对于多声道压力，你这样获取音符和压力：

```cpp
UINT uMIDIDoteNote = (UINT)vEvent.polyPressure.pitch;
float pressure = vEvent.polyPressure.pressure;
```

我们将只跟踪这三个事件。所有工作都将通过一个名为 `doProcessEvent()` 的特殊函数完成，用于处理第 2 章所述的消息。它在 `process()` 函数中被调用，该函数在它的输入参数中接收事件。在 `TemplateSynth` 中，`doProcessEvents()` 部分空白的，因此你需要填充代码来记录 MIDI 消息。

接下来，找到或声明跟踪 MIDI 通道的变量。你希望能够识别 MIDI 通道，特别是对于多音色项目。在我们的合成器中，我们默认在所有通道上接收。当你的项目变得更高级，并且你想允许用户控制 MIDI 接收通道时，你可以之后更改这一点。在 `.h` 文件附近添加以下 `UINT` 变量：

```cpp
class Processor : public AudioEffect
{
    <SNIP SNIP SNIP>
protected:
    // --- 减少 process 大小的函数
