
```objc
- (void)dealloc
{
    [self removeListeners];
    [backImage release];
    [backgroundColor release];
    [controlArray dealloc];
    [knobImages dealloc];
    [super dealloc];
}

- (void)drawRect:(NSRect)rect
```

```objc
// --- 使用 UIColor 创建平铺背景图案
NSColor *backgroundPattern = [NSColor colorWithPatternImage:backImage];

// --- 填充背景

[backgroundPattern setFill];
NSRectFill(rect);

// --- 分组框背景图
float x, y, w, h;
float y0Offset = -7;

// --- 第 1 列
//
// --- 底部旋钮
NSRect knob3Rect = [wpRotaryKnob_3 frame];
x = NSMinX(knob3Rect);
w = NSWidth(knob3Rect);

// --- 顶部旋钮
NSRect knob0Rect = [wpRotaryKnob_0 frame];
y = NSMinY(knob0Rect);

// --- 列高
h = y + NSHeight(knob0Rect) + 50;

// --- 分组框
NSRect rect1 = [NSMakeRect(x, y0Offset, w, h)];

// --- 获取图片
NSString* path = [[[NSBundle bundleForClass:[MiniSynthView class]] pathForResource:@"groupframe" ofType:@"png"] autorelease];

NSImage* image = [[NSImage alloc] initWithContentsOfURL:[NSUrl fileURLWithPath:path]];

float alpha = 1.0;

// --- 绘制
if(image) {
    [image drawInRect:groupRect1 fromRect:NSZeroRect
    operation:NSCompositesSourceover fraction:alpha];

    // --- 第 2 列
    etc...

    // --- 在填充背景后，调用 super 绘制所有其他控件
    // 背景
    [super drawRect:rect];
}
```

# 第 3 章：MIDI

在本章中，我们将开始一个名为 `NanoSynth` 的合成器项目。这是一个非常重要的项目，因为我们将用它来构建合成器架构，该架构将用于后续所有的项目。此外，当你在第 4 章设计将成为合成器核心的 C++ 对象时，你将在 `NanoSynth` 中对其进行测试。我们在 `NanoSynth` 中设置的 MIDI 消息解码将贯穿本书。为了节省空间，它不会在每个项目中重复出现；即使你了解 MIDI，理解 `NanoSynth` 的工作原理仍然很重要。

## 3.1 MIDI 消息

MIDI 是一种消息系统。每条消息都有一个发送者和一个接收者。这些消息的设计是为了在尽可能短的消息中编码尽可能的信息。消息还需要传达截然不同的信息类型。某些消息需要额外数据来完整传输信息。MIDI 的发明者首先拆分了合成器需要发送和接收的消息类型。他们实现了一个系统，用来处理未来随着时间推移可能发明的后续消息和数据。图 3.1 显示了规范中不同类型的 MIDI 消息。语音消息（Voice Message）是你将在书中花费时间最多的地方。通道消息（Channel Messages）在设备上有一个特定的目标，而系统消息（System Messages）是全局性的，并广播到所有设备。其余消息如下：

**通道（Channel）：**
- 语音（Voice）：性能信息和音符事件
- 通道模式（Channel Mode）：配置更改

**系统（System）：**
- 系统通用（System Common）：针对所有设备的信息
- 系统实时（System Real Time）：定时（时钟）
- 系统专用（System Exclusive）：任何及一切（开放式）

书中的合成器项目只处理通道消息，这是最常见且无疑重要的。这些不仅包括音符消息，还包括旋钮和滑块的所有连续消息（CCs）。MIDI 消息通过字节串行传输。图 3.2 显示了 MIDI 字节的结构。MIDI 字节编码了两种信息类型：状态（status）——正在发送的消息类型以及数据（data）——关于消息的信息。状态/数据位是有效位（MSB），即 MIDI 字节最左侧的位。状态字节被分为四个半字节（nibbles）。低位半字节编码 0–15 通道。高位半字节是消息内容，其高位始终为 1。对于数据字节，低 7 位编码数据。这提供了从 0 到 127 的 128 个不同的值。一个 MIDI 消息包含至少一个状态字节和零或多个数据字节。状态字节始终是消息的第一位。它决定了随其后的数据字节数量。通过这种方式，

## 3.2 通道消息

通道消息包含最重要的信息。这些在表 3.1 中。

### 08n—音符关闭（Note Off）

音符关闭消息编码音符编号和释放键时的速度。键盘以相同的方式解释这些消息。

### 09n—音符开启（Note On）

音符开启消息编码音符编号和击击时的速度。MIDI 控制器通常提供这种功能。

### 0An—压力（Aftertouch）

某些键盘可以感应按键按下并触底后的压力。你按下键并在声音产生后向下按。传感器组件将压力转换为电压，然后转换为压力值。如果键盘可以对单个音符这样做——即感应已按下按键的不同压力——那么它支持压力（也称为键盘压力、多音压力）。

### 0Bn—控制变化（Control Change）

大多数 MIDI 控制器具有大量的可用控制器旋钮、滑块、带和开关，此外还有音高控制（操杆或轮）和调制控制（通常是标记为 Mod 或 Modulation 的轮或滑块）。所有这些控制（包括延音踏板）都是连续控制器。共有 128 个连续控制器，索引从 0 到 127。MIDI 规范实现了其中一部分；许多被标记为“未定义”。我们所有的合成器都响应一组核心 CC。这些在表 3.2 中。

表 3.2：所有合成器将支持的控制变化消息。

| 控制编号 | 控制消息 |
|---|---|
| 1 = 0x01 | 调制轮轮 |
| 7 = 0x07 | 通道音量 |
| 10 = 0x0A | 声位 |
| 11 = 0x0B | 表达式 |
| 64 = 0x40 | 延音踏 |
| 123 = 0x7B | 所有音符关闭 (恐慌/重置) |

### 0xC—程序更改 (Program Change)

程序更改消息传输介于 0 到 127 之间的单字节值，它用于选择合成器上数字为 1 到 128 的音色（patch）。我们将在合成器中拦截并识别此消息，但在你继续开发并构建自己的多程序合成器之前，我们不会使用它。

### 0xD—通道触后压力 (Channel Aftertouch)

通道触后压力与触后（Aftertouch）类似，但它不是为每个音符单独传输。相反，它是全局发送到特定通道上的所有音符。由于这是一个更廉价的方案，许多控制器实现了它，而不是多声道按键压力（Polyphonic Key Pressure）。

| 状态：弯调 (Pitch Bend) | 数据 1: LSB | 数据 2: MSB |
|---|---|---|
| 1 1 1 0 X X X X | 0 L L L L L L L | 0 M M M M M M M |
| | | M M M M M M L L L L L L |
| | | 14位值 |

图 3.3：弯调消息有两个数据字节，每个字节向 14 位字贡献 7 位数据。

### 0xE—音高弯调 (Pitch Bend)

由于解码方式的原因，音高弯调消息是一种特殊的语音消息（Voice Message）。它通常由操纵杆或轮产生。音高弯调解码使用两个数据字节来编码一个中心点为 0 的双极值（无弯调）。正的弯调值表示音高升高（升），而负值表示音高下降（降）。大多数合成器的音高弯调范围至少为一个八度到 +/- 4 个八度。如果只使用一个数据字节来传输值，你的耳朵将把弯调听为一系列离散的音高跳变，而不是平滑且连续的变化。平滑过渡是通过使用两个数据字节实现的，每个字节贡献 7 位形成一个 14 位值，产生 16,384 个值——这足以产生平滑的弯调。

MIDI 1.0 规定音高弯调为一个双极值范围，其如下：

- `0x00 00` = 最大负（降）音高弯调
- `0x00 64` = 中心 (0)
- `0x7F 7F` = 最大正（升）音高弯调

为了便于计算，将其转换为双极值更简单，这样 0 就不产生任何音高变化。这 16,384 个值随后分布在 -8192 到 +8191 或 -1.0 到 +0.999 的双极范围内。

## 3.4 项目：NanoSynth

`NanoSynth` 将成为后续每个其他合成器 MIDI 部分的基础，并作为你 C++ 对象的测试平台。你将在接下来的五章构建 `NanoSynth`。在本章中，你将学习你的平台如何处理 MIDI 消息并配置基础消息系统。没有需要处理的控制项，因为这是一个简单的项目，你应该能快速运行它。你需要一个 MIDI 控制器来提供 3.2 节中尽可能多的控制消息。你将拦截 MIDI 事件并将其记录到输出窗口，以创建一个基础 MIDI 监控器。在下一章中，你将使用音符开启/关闭事件来开启并测试振荡器。这个插件不会产生声音，但它将帮助你熟悉在所选择的平台上进行编码。查看上一章的表 3.3，它显示了每个 API MIDI 函数实现的差异。在这个项目中，我们将在这些函数中工作。

表 3.3：用于 RackAFX、VST3 和 AU 的 MIDI 函数。

| 函数 | RackAFX | VST3 | AU |
| --- | --- | --- | --- |
| MIDI 消息 | | | |
| 音符开启 (Note On) | `midiNoteOn()` | `process()` | `StartNote()` |
| 音符关闭 (Note Off) | `midiNoteOff()` | `process()` | `StopNote()` |
| 音高弯调 (Pitch Bend) | `midiPitchBend()` | `process()` | `HandlePitchWheel()` |
| 调制轮 (Mod Wheel) | `midiModWheel()` | `process()` | `HandleControl()` |
| 所有其他 MIDI 消息 | `midiMessage()` | `process()` | `HandleMouseEvent()` |

对于 VST3，你将创建一个子函数 `processEvents()` 来处理解码，但信息是在 `process()` 函数期间到达的；我们将从 `process()` 中调用 `processEvents()`。

### 通用文件

所有平台将使用一些相同并包含在每个合成器中的通用函数：

- `synthfunctions.h`——每个项目中广泛使用的常量、结构体和函数集合。
- `pluginconstants.h`——最初是一个 RackAFX 文件，它包含了更多常量、函数和对象，如 GUI 控制项。
- `pluginobjects.cpp`——用于对象的实现文件。
- `synthlimits.h`——用于定义参数限制的枚举文件。
- `synthconstants.h`——用于定义常量。
- 3参数的实现文件。
- `synthparameters.h`——用于定义参数值范围的枚举。
