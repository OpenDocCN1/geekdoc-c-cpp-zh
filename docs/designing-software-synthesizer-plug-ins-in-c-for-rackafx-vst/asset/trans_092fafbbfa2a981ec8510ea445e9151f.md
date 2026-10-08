

```cpp
enum midiChannels{MIDI_CH_1 = 0, MIDI_CH_2, MIDI_CH_3, MIDI_CH_4, MIDI_CH_5,
MIDI_CH_6, MIDI_CH_7, MIDI_CH_8, MIDI_CH_9, MIDI_CH_10,
MIDI_CH_11, MIDI_CH_12, MIDI_CH_13, MIDI_CH_14, MIDI_CH_15,
MIDI_CH_16, MIDI_CH_ALL};
```

在构造函数中使用 `MIDI_CH_ALL` 初始化 MIDI 接收变量：
USynth::USynth(AudioUnit inComponentInstance)
:AUInstrumentBase(inComponentInstance, 0, 1)

```cpp
// 创建输入、输出端口、组和部分
CreateElements();

<SNIP SNIP SNIP>

// 在所有通道上接收
m_uMidiRxChannel - MIDI_CH_ALL;
```

你将成为使用 `printf` 宏将日志打印到 Xcode 控制台（输出）窗口。请确保你理解函数如何配合 `%d`、`%u` 等说明符工作。你还希望能够启用或禁用日志。定义一个 `#define` 来启用日志。在 `USynth.cpp` 顶部添加该 `#define`：

```cpp
#define LOG_MIDI
1
```

当 MIDI 音符开启（Note On）时，你想要记录该事件、音号数字和速度，使其显示如下所示：

```
-- Note On: Ch:1 Note:60
Vel:96
```

这表示在 MIDI 通道 1 上有一个 MIDI 音号为 60（中音 C）、速度为 96 的 Note On 消息。当然，你可以按照自己的方式格式化字符串，但上面的方法简短简单。MIDI 音号消息在 `StartNote()` 和 `StopNote()` 函数中处理。有趣的是，这两个函数的参数不同。

```cpp
OSStatus USynth::StartNote(MusicDeviceInstrumentID inInstrument,
MusicDeviceGroupID inGroupID,
NoteID *outNoteID,
Uint32 inOffsetSampleFrame,
const MusicDeviceNoteParams &inParams);
```

你可以安全地忽略这五个参数中的三个——你所有的信息都包含在 `MusicDeviceGroupID` 和 `MusicNoteParams` 参数中。`inGroupID` 是 MIDI 通道。音号和速度信息在 `inParams` 中。该结构体包含两个变量：

- * mPitch: 分数形式，例如 60.5 表示 MIDI 音号 60 带有 +50 音分的偏移，该偏移源于主调调整；在我们的项目中我们将忽略此偏移，但鼓励你对其对其进行调查。

在所有 MIDI 函数中，你做的第一件事是测试 MIDI 通道，以确保你有能力接收该通道的消息。这段代码对于所有函数基本上是相同的。

```cpp
// 测试通道/忽略
if(m_uUMidiRxChannel != MIDI_CH_ALL && uChannel != m_uUMidiRxChannel)
    return false;
```

在音符开启和关闭的处理程序中填充音符，并使用 `printf` 将信息记录到控制台。
// / -- Note On 事件处理程序

```cpp
OSStatus AUSynth::StartNote(MusicDeviceInstrumentID inInstrument,
                                        MusicDeviceGroupID inGroup,
                                        NoteID *outNoteInstanceID,
                                        UINT32 inOffsetsSampleFrame,
                                        const MusicDeviceNoteParams &inParams)
```

```cpp
{
    UINT uUMidiNote = (UINT)inParams.mPitch;
    UINT uVelocity = (UINT)inParams.mVelocity;
    UINT uChannel = (UINT)inGroup;

    // -- 测试通道/忽略; inGroup = MIDI 通道 0-15
    if(m_uUMidiRxChannel != MIDI_CH_ALL && uChannel != m_uUMidiRxChannel)
        return noErr;
```

```cpp
#ifdef LOG_MIDI
    printf("-- Note On Ch:%d Note:%d Vel:%d \n", uChannel, uMIDINote, uVelocity);
#endif
```

```cpp
    return noErr;
}
// / -- Note Off 处理程序
OSStatus AUSynth::StopNote(MusicDeviceGroupID inGroup,
                                           NoteID inNoteInstanceID,
                                           UINT32 inOffsetsSampleFrame)
```

```cpp
{
    UINT uUMidiNote = (UINT)inNoteInstanceID;
    UINT uChannel = (UINT)inGroup;

    // -- 测试通道/忽略; inGroup = MIDI 通道 0-15
    if(m_uUMidiRxChannel != MIDI_CH_ALL && uChannel != m_uUMidiRxChannel)
        return noErr;
```

```cpp
#ifdef LOG_MIDI
    // -- 注意：AU 不传输音符关闭的速度！
    printf("-- Note Off Ch:%d Note:%d \n", uChannel, uMIDINote);
#endif
```

```cpp
    return noErr;
}
```

接下来，实现音弯（pitch bend）处理程序，它有一组不同的参数：

- inChannel: MIDI 接收通道
- inPitch1 和 inPitch2: 音弯消息的低位字节（LSB）和高位字节（MSB）

首先将 LSB 和 MSB 转换为 14 位字并解码。

控制变化消息（Control Change Messages）在 `HandleControlChange()` 中处理，参数为：

- inChannel: MIDI 通道
- inController: MIDI CC 索引
- inValue: CC 值 0 到 127

所有合成器都会响应一组默认的 CC：

- 调制轮（Mod Wheel）
- 音量 CC7
- 声全 CC10
- 表达（Expression）CC11
- 延音踏板（Sustain Pedal）CC64
- 所有音符关闭（All Notes Off）

你将在 `HandleControlChange()` 中拦截并记录这些消息，同时解码控制器索引。当 CC 值为 64 或更大时，延音踏板开启。CC 索引（例如 `MOD_WHEEL`）定义在 `synthfunctions.h` 中。

```cpp
OSStatus AUSynth::HandleControlChange(Uint8 inChannel,
	Uint8 inController,
	Uint8 inValue,
	Uint32 tStartFrame)
```

```cpp
UINT uChannel = (UINT)inChannel;
// 测试通道/忽略
if (m_uUMidiRxChannel != MIDI_CH_ALL && uChannel != m_uUMidiRxChannel)
	return noErr;

switch(inController)
{
	case MOD_WHEEL:
		#ifdef LOG_MIDI
		printf("-- Mod Wheel Ch:%d Value:%d \n", uChannel, inValue);
		#endif
		break;
	case VOLUME_CC7:
		// -- 自身拦截音量 ---
		#ifdef LOG_MIDI
		printf("-- Volume Ch:%d Value:%d \n", uChannel, inValue);
		#endif
		break;
	case PAN_CC10:
		// -- 自身拦截声全 ---
		#ifdef LOG_MIDI
		printf("-- Pan Ch:%d Value:%d \n", uChannel, inValue);
		#endif
		break;
	case EXPRESSION_CC11:
		#ifdef LOG_MIDI
		printf("-- Expression Ch:%d Value:%d \n", uChannel, inValue);
		#endif
		break;
	case SUSTAIN_PEDAL:
		// 64 或更大为开启
		bool m_bSustain = (UINT)inValue > 63 ? true : false;
		#ifdef LOG_MIDI
		if(m_bSustain)
			printf("-- Sustain Pedal ON");
		else
			printf("-- Sustain Pedal OFF");
		#endif
		break;
	case ALL_NOTES_OFF:
		#ifdef LOG_MIDI
		printf("-- All Notes Off!");
		#endif
		break;
	// --- 其他控制器
	default:
		#ifdef LOG_MIDI
		printf("-- CC Ch:%d Value:%d \n", uChannel, inValue);
		#endif
		break;
}

return true;
```

你在 `HandleEvent()` 中拦截剩余的 MIDI 消息，其参数为 MIDI 字节：

- status
- channel
- data1
- data2

你在此函数处理多音压力、程序更改和通道压力。

```cpp
OSStatus AUSynth::HandleMidiEvent(Uint8 status,
Uint8 channel,
Uint8 data1,
Uint8 data2,
Uint32 inStartFrame)
```

```cpp
UINT uChannel = (UINT)channel;
// 测试通道/忽略
if(m_uUMidiRxChannel != MIDI_CH_ALL && uChannel != m_uUMidiRxChannel)
	return false;

switch(status)
{
	case POLY_PRESSURE:
		#ifdef LOG_MIDI
		printf("-- Poly Pressure Ch:%d Note:%d Value:%d \n", uChannel, (UINT)data1, (UINT)data2);
		#endif
		break;
	case PROGRAM_CHANGE:
		#ifdef LOG_MIDI
		printf("-- Program Change Num Ch:%d Value:%d \n", uChannel, (UINT)data1);
		#endif
		break;
	case CHANNEL_PRESSURE:
		#ifdef LOG_MIDI
		printf("-- Channel Pressure Value:%d Value:%d \n", uChannel, (UINT)data1);
		#endif
		break;
	// --- 调用基类处理其逻辑 ---
	return AUMIDIBase::HandleMidiEvent(status, channel, data1, data2,
inStartFrame);
}
```

```
-- Mod Wheel Ch:0: Value:3
-- Mod Wheel Ch:0: Value:4
-- Mod Wheel Ch:0: Value:5
-- Mod Wheel Ch:0: Value:6
-- Mod Wheel Ch:0: Value:7
-- Pitch Bend Ch:0 int:08448 float:0.031250
-- Pitch Bend Ch:0 int:08576 float:0.046875
-- Pitch Bend Ch:0 int:08702 float:0.026200
-- Pitch Bend Ch:0 int:08192 float:0.000000
-- Expression Ch:0: Value:72
-- Expression Ch:0: Value:71
-- Note On Ch:0: Note:47 Vel:65
-- Note On Ch:0: Note:43 Vel:88
-- Note On Ch:0: Note:45 Vel:55
-- Note On Ch:0: Note:40 Vel:59
-- Note Off Ch:0: Note:47
-- Note Off Ch:0: Note:41
-- Note Off Ch:0: Note:45
-- Note Off Ch:0: Note:43
-- Note Off Ch:0: Note:41
-- Note Off Ch:0: Note:40
-- CC Ch:0: Num:17 Value:83
-- CC Ch:0: Num:17 Value:82
-- CC Ch:0: Num:5 Value:2
-- CC Ch:0: Num:5 Value:3
-- CC Ch:0: Num:5 Value:4
-- CC Ch:0: Num:5 Value:5
-- CC Ch:0: Num:5 Value:6
```

图 3.6：Xcode 控制台窗口显示了我们记录的 MIDI 事件。

