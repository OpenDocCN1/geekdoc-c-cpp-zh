
```cpp
virtual bool __stdcall midiModWheel(UINT uchannel, UINT uModValue);
```
- 处理调制轮（常见于大多数合成器控制器）变化的函数

```cpp
virtual bool __stdcall midiPitchBend(UINT uchannel,
                                       int nActualPitchValue,
                                       float nNormalizedPitchBendValue);
```

- 针对音变轮/摇杆的专用函数

```cpp
<SNIP SNIP SNIP> -- 我们不会在书中的项目中实现 MIDI 时钟
virtual bool __stdcall midiMessage(unsigned char cchannel,
                                     unsigned char cStatus,
                                     unsigned char cData,
                                     unsigned char cData2);
```

- 所有其他 MIDI 消息，包括连续控制器

`MiniSynth.h` 文件的最后部分包含几个成员变量。对于 `MiniSynth`，这些变量是：

```cpp
CMiniSynth* m_pVoiceArray[MAX_VOICES];
void incrementVoiceTimestamps;
CMiniSynth* getOldVoice();
CMiniSynth* getOldVoiceWithNote(UINT uMIDINote);
```

```cpp
// --- 一性更新所有 voice
void update();
```

```cpp
// --- 用于滑音 (portamento)
double m_dLastNoteFrequency;
```

```cpp
// --- 我们的接收通道
UINT m_uMidiRxChannel;
```

合成器的多音性通过维护一个 voice 指针对象数组来实现。对于所有合成器，该数组命名为 `m_pVoiceArray`。区别在于它们所持有的指针类型；在这种情况下，数组持有 `Synth` 指针。其定义下方的三个函数用于处理 voice 的时间顺序。`update()` 函数用于一次性更新所有合成器变量。随着第 3-12 章的学习，我们将深入这些细节以及剩余的几个变量。

现在，让我们逐个查看每个函数的实现。从插件对象的角度来看，所有的合成器项目非常相似。区分合成器的大部分工作在我们设计的 `CVoice` 对象中完成。因此，一旦你理解了一个合成器，其他的就很容易掌握。打开 `MiniSynth.cpp` 文件，让我们从顶部开始向下研究实现。

## 构造函数

每个 RackAFX 插件中的构造函数执行以下操作：

- 分配动态内存
- 初始化变量
- 释放任何分配的内存
- 每次运行初始化函数
- 始终在子组件上设置采样率
- 始终更新合成器对象
- 渲染合成的音频输出
- 在用户移动 GUI 上的控件后调用；你可以选择在此处不进行处理：在所有情况下我们都会调用合成器更新函数

合成器的多音性通过维护一个 voice 指针对象数组来实现。对于所有合成器，该数组命名为 `m_pVoiceArray`。区别在于它们所持有的指针类型；在这种情况下，数组持有 `Synth` 指针。其定义下方的三个函数用于处理 voice 的时间顺序。`update()` 函数用于一次性更新所有合成器变量。随着第 3-12 章的学习，我们将深入这些细节以及剩余的几个变量。

```cpp
bool __stdcall cMiniSynth::processAudioFrame(float* pInputBuffer,
float* pOutputBuffer,
UINT uNumInputChannels,
UINT uNumOutputChannels)
{
  // Do LEFT (MONO) Channel
  double dLeftAccum = 0.0;
  double dRightAccum = 0.0;

  // --- 12dB headroom
  float fMix = 0.25;
  double dLeft = 0.0;
  double dRight = 0.0;

  // --- loop and accumulate voices
  for(int i=0; i<MAX_VOICES; i++)
  {
    // detailed in future chapters
  }
  pOutputBuffer[0] = dLeftAccum;

  // Mono-In, Stereo-Out (AUX Effect)
  if(uNumInputChannels == 1 && uNumOutputChannels == 2)
    pOutputBuffer[1] = dLeftAccum;

  // Stereo-In, Stereo-Out (INSERT Effect)
  if(uNumInputChannels == 2 && uNumOutputChannels == 2)
    pOutputBuffer[1] = dRightAccum;

  return true;
}
```

在 `userInterfaceChange()` 中，你通常首先解码控件的索引（通过 `nControlIndex` 参数传递），然后根据该索引调用相应的更新函数或计算。在我们的 RackAFX 合成器项目中（以及 VST3 和 AU 版本）中，如果其中一个变量发生了变化，我们将强制强制更新所有变量。这主要是为了极大简化代码。经过特性化测试，我们发现全量更新带来的额外销并没有显著影响 CPU 负载；与实际的音频合成相比，更新函数的开销非常小。然而，我们鼓励你在完成同步运行后改变这种范式，并单独解码每个控件。为了方便解码，RackAFX 在 `userInterfaceChange` 函数上方留了一个注释，提醒你索引映射。

```cpp
/* ADDED BY RACKAFX -- DO NOT EDIT THIS CODE!!! */
**--0x2983--**

Variable Name Index
m_uVoiceMode 0
m_dDetune_cents 1
m_dFcControl 2
m_dLF01Rate 3

etc...
**--0xFFDD--**
n// ... */
// Add your UI Handler code here
//
bool _stdcall CMiniSynth::userInterfaceChange(int nControlIndex)
{
    // --- just update all, ignoring the index value
    update();
    return true;
}
```

# MIDI 消息函数与辅助函数

最后一个块全部涉及 MIDI 消息。很棒在于，除了数组持有的音色指针类型外，所有合成器项目的 MIDI 函数都是相同的，因此一旦你掌握了它们，就可以复制粘贴到其他地方。

# MIDI 音符时间戳函数

有三个函数有助于多声部。

```cpp
void CMiniSynth::incrementVoiceTimestamps()
CMiniSynthVoice* CMiniSynth::getOldestVoice()
CMiniSynthVoice* CMiniSynth::getOldestVoiceWithNote(UINT uMIDNote)
```

我们将在第 8 章详细讨论这些内容。它们用于实现动态音色分配或偷声（voice-stealing）。现在你可以跳过它们。

# MIDI 音符 On 和 Off

这是我们将处理的两个最重要的 MIDI 消息。我们将在第 8 章介绍这些方法的具体细节；然而，你需要了解 RackAFX 如何根据 MIDI 消息为你简化一些工作。对于音符开启（note on），RackAFX 将 MIDI 字节数据转换为可管理的 UINT 类型。这三个参数是：

- `UINT uChannel`: 0–15，总共 16 个通道
- `UINT uMIDINote`: 音符事件的 MIDI 音符编号 0->127
- `UINT uMIDIVelocity`: 音符事件的 note ON 速度 0->127

第一步是检查 `midiNote`，如果它不是我们正在播放或支持的通道，则退出。更多细节将在下一章我们仔细查看 MIDI 消息时显示。之后，我们执行必要的事件处理。

```cpp
bool __stdcall CMiniSynth::midiNoteOn(UINT uChannel, UINT uMIDINote, UINT uVelocity)
```

对于音符关闭（note off），RackAFX 将 MIDI 字节数据转换为更容易管理的 UINT 类型。这三个参数是：

- `UINT uChannel`: 0–15，总共 16 个通道
- `UINT uMIDINote`: 音符事件的 MIDI 音符编号 0->127
- `UINT uMIDIVelocity`: 音符事件的 note off 0->127（大多数 MIDI 键盘不传输此值）
- `bool bAllNotesOff`: 用于关闭所有音符的 MIDI 消息

```cpp
bool __stdcall CMiniSynth::midiNoteOff(UINT uChannel, UINT uMIDNote, UINT uVelocity, bool bAllNotesOff)
```

# MIDI 调制轮 (Mod Wheel)

调制轮（mod wheel）是大多数 MIDI 控制器上的标准。它通常与连续控制器（CC）消息分开管理，VST3 和 AU 除外。在处理音符 On 和 Off 时，RackAFX 将字节转换为易于管理的 UINT。调制轮值为 0 到 127。

- `UINT uChannel`: 0–15，总共 16 个通道
- `UINT uModValue`: 0 到 127 的调制轮位置

```cpp
bool __stdcall CMiniSynth::midiModWheel(UINT uChannel, UINT uModValue)
```

# MIDI 弯音 (Pitch Bend)

弯音是一种特殊的 MIDI 消息，因为它使用 14 位值来表示弯音量。对于此消息，RackAFX 发送两个版本的弯音以产生声音转换：一次是有符号整数（-8192 到 +8191），另是浮点值（-1.0 到 +1.0）。0 表示中心位置或无偏移。

```cpp
// nActualPitchBend = -8192 -> +8191, 0 为中心
// nNormalizedPitchBend = -1.0 -> +1.0, 0 为中心
bool _stdcall CMiniSynth::midiPitchBend(UINT uChannel, int nActualPitchValue, float fNormalizedPitchValue)
```

# 其他 MIDI 消息

要告诉主机所有 MIDI 消息，你在构造函数中将 `m_bWantMIDIMessages` 设置为 true。我们的所有合成器（在所有平台上）都支持以下消息：

- 音量 (volume CC7)
- 声 (pan CC10)
- 表现 (expression CC11)
- 延音踏 (sustain pedal)
- 程序更改 (program change)
- 多声部触 (polyphonic aftertouch)
- 通道触 (channel aftertouch)

我们将在下一章讨论 "CC 7" 的含义。现在重要的是理解此消息将字节作为参数（`unsigned char`）发送。在检查通道后，如果是控制更改消息（control change），我们会解码数据字节 1 并将其传递给音色对象。值编码在数据字节 2 中。

```cpp
bool _stdcall CMiniSynth::midiMessage(unsigned char channel, unsigned char status, unsigned char data1, unsigned char data2)
```

这结束了我们对 RackAFX 插件的基本讨论。在处理对象和 MIDI 消息的过程中，你将学习更多关于 RackAFX 的知识。第 3 章将要求你进行编程。当我们到达设计章节（第 9-13 章）时，你将变得精通且不需要任何指导——你可以从头开始自己的合成器项目。

## 2.15 编写 VST 插件

Steinberg 最初在 1996 年开发 VST 插件 API 以提供简单的跨平台解决方案。版本 1 和 2 的 API 与当时的 DirectX（一种竞争格式）相比非常基础，几乎每个录音软件包最终都遵循 VST 规范。VST2 代表了迄为止最成熟的版本，插件封装在具有 `.dll` 扩展名的动态库中。

![](img/b42d0ca53f4a889d8162d557c8c05d_65_0.png)

VST3 在 2008 年引入，不是更新而是完全的重做，因此它们不直接兼容。与 VST2 不同，插件封装在动态链接库中，扩展从 `.dll` 重名为 `.vist`。2013 年 9 月，Steinberg 正式停止了对 VST2 的支持并从网站删除了 VST 软件开发包（SDK）。Steinberg 的移除和废弃意味着只有主要的客户端将支持 VST3。由于存在大量的 VST2 插件，客户端仍仍支持 VST2。VST3 提供了一种封装机制，如果插件没有实现 GUI，VST 客户端会提供一个默认 GUI。也有自定义 GUI 的选项。我们将实现两者。我们需要先定义 GUI，然后将 GUI 连接到其参数。你可以在 VST 客户端中不同的 GUI 之间切换。

本书仅涵盖 VST3。如果你想从 VST2 开始，你需要 VST2 SDK（免费）和版本的 Microsoft Visual Studio（示例适用于 VS2008 和 VS2010）。你可以在 http://www.steinberg.net/en/company/developer.html 获取 SDK，当时的最新版本为 3.6.0。当你解压 SDK 时，你会发现一个子文件夹层次结构，包含所有基类文件、VSTGUIGUI 文件和示例代码。你可以将这组文件夹放在本地驱动器的任何位置，但建议将其放在根目录。文档位于主目录下的 HTML 格式，名为 `index.html`——你应该在浏览器中打开并书签；你会经常参考它。SDK 的一个根本问题在于文件夹的层次结构性质，这体现在各个文件夹文件的 `#include` 语句中。换句话说，文件设置为在特定的目录层次中相互引用。如果你修改了层次结构、尝试移动文件、合并或平铺目录，当你尝试 Steinberg 示例项目或书中的任何项目时，就会发生故障。

在任何情况下都不要更改 SDK 文件夹的层次结构。在某些情况下，你可能可以重命名文件夹，但通常你应该避免修改目录，除非如本章所示。

# 设置目录层次结构

在正确的文件夹层次结构中创建项目至关重要，否则编译器将无法找到文件并进行链接。当你安装 SDK 时，你需要找到包含 Windows 插件示例代码的文件夹；这里我们将使用项目名称 `name_expression_synth`，但任何示例代码文件夹都位于：

`win` 文件夹包含 Visual Studio 项目文件。需要注意的是，当项目文件夹在 `public.sdk` 内部深 4 层时，你有两个选择：将你所有的合成器项目放在 `vst` 文件夹中并在每个项目文件夹下声明子文件夹（如果你喜欢命名为 `win`，但实际名称并不重要），或者构建自己的模拟 `public.sdk` 四层结构的层次结构。这是

我们做了哪些工作，以便将我们的合成器项目保持在一个主文件夹中。我们创建了以下层次结构：

每个合成器文件夹都在 Windows 文件夹内，并且每个文件夹在 public.sdk 内部深达四层。确保你在开始时处理好这个问题，否则你的代码将无法编译。

- `<Root>`
- `VST3 SDK`
- `public.sdk`
- `MyProjects`
- `SynthProjects`
- `Windows`
- `Nanosynth`
- `MiniSynth`
- `DigiSynth`
- `VectorSynth`
- `AniSynth`
- `DXSynth`

# 开始新项目

从零开始一个一个新的 VST3 项目在最好的情况下也是艰辛的，在最坏的情况下是令人沮丧的。我们最强的建议是下载示例项目并将它们作为基础。我们提供了多个版本供你下载，每个合成器项目进行了设置：

- `empty`（空）——编写所有内容并设计 GUI——如果你已经是高级 VST3 程序员，这可能是一个不错的选择。
- `GUI`——代码和 UI 已经完成，因此你可以专注于合成器组件和处理；在每一章中，你都有机会进入并逐步修改 GUI，在完成几个项目之后，你可能需要考虑 GUI 设计：这是推荐的选项！
- `full`（完整）——项目包含了全部；我们不建议简单地编译别人的代码作为学习方法，然而，拥有完整代码允许你不仅不用检查自己的工作，还能在调试模式下单步执行代码，查看客户端是如何交互的——简而言之，完整项目对于帮助你理解正在进行的项目非常有帮助。

另一种方法是从示例项目之一开始，将项目文件夹复制并重命名为项目名称，然后按照附录 A 中的描述修改 Files 和 Visual。它逐步展示了如何修改项目以转换为 anis。这在利用 MiniSynth、DigiSynth、VectorSynth、AnySynth 的演进过程中特别有用，因为它们将相互构建。如果你真的想从零开始一个项目，你也可以从网站上获取这些信息，但请注意：这不适合意志不坚定的人。
