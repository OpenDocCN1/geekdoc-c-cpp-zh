
Controller 暴露了 `IMIDIMapping` 接口，并且且仅实现纯抽象函数 `getMIDIControllerAssignment()`。在启动时，宿主机将查询插件，询问如何映射给控制器消息。共有 130 个控制器消息。它们在 Controllers 结构中枚举到 `vstmidcontrollers.h` 文件。我们所有的合成器都将响应一组基础控制更改消息，但我们鼓励你探索支持其他控制器的可能性，你应该查看该 `.h` 文件以获取其他可用控制器常量。我们的基础 MIDI 控制器集包括：

- 音高弯 (`pitch bend`)
- 调制轮 (`mod wheel`)
- 音量 (`volume`)
- 声相 (`pan`)
- 表达 (`expression`)
- 延音踏板 (`sustain pedal`)
- 通道压力（后触）(`channel pressure (aftertouch)`)
- 全音符关闭 (`all notes off`)

正如我们之前讨论的，计划是让这些每一个都映射到一个虚拟 `Parameter`。它们与上面第一步中的其他项一起枚举。在实现 `Processor` 的下一节中，你将看到如何使用这些索引值。

接下来，这组虚拟参数通过上述三个步骤被添加到容器中。这些参数中的每一个默认都会被归一化，其中 `MIN_UNIPOLAR` 和 `MAX_UNIPOLAR` 分别定义为 `0.0` 和 `1.0`。这里是前几个：

```cpp
enum {
    VOLUME_DB,      /* * 0 *
    OCTAVE,          /* * 1 *
    FILTER_CUTOFF,   /* * 2 *
    FILTER_TYPE,     /* * 3 *
}
```

在创建虚拟参数并放入容器后，我们现在可以实现 `getMIDIControllerAssignment()` 方法。这是一个解码 MIDI 控制码并将其映射到我们的某一个参数的简单案例。这是该 `IMIMapping` 接口的原型：

（注：由于原文包含大量重复段，已根据注意事项进行了去重翻译处理）

```cpp
tresult PLUGIN_API process(ProcessData& data);
```

- 音频渲染函数
- 同时处理 MIDI 事件和控制变化

```cpp
static FUnknown* createInstance(void*) { return (IAudioProcessor*)new Processor (); }
```

- COM 创建函数

```cpp
static FUID cid;
```

- 此对象的全局唯一标识符

除了这些方法外，我们还将为 GUI 上的每个控件声明变量，以改变合成器的输出。当我们处理变化控件时，我们会相应地更改这些变量的值，然后调用更新方法来设置合成器对象中的变量。如果你查看 `MiniSynth` 项目中的 `VSTSynth.h` 文件，你可以看到额外的声明。不要担心涉及多音数组的第一部分；我们将在第 8 章使用多音性时讨论该部分。在讨论 `process()` 函数时，我们会讨论 `doControlUpdate()` 和 `doProcessEvent()` 函数。

此部分的代码大部分是被称为合成器参数（`synth parameters`）的变量列表。这些是直接影响合成器运行的变量。

你需要在 `Controller` 的 `initialize()` 方法中为每个参数设置一个变量。每个合成器的 GUI 设计表中都命名并列出了这些变量。将这些变量添加到每个项目的 `Project` 对象的 `.h` 文件中。然后，仅添加与 `Controller` 的 `initialize()` 方法中设置的虚拟 MIDI 控件对应的变量。

之后，你将设置虚拟 MIDI 控制器变量。当我们在 `process()` 函数期间解码控制变化时，日志过滤器需要一些转换。为此，我们将创建一个特殊的辅助对象 `Parameter`，其方式与你在 `Controller` 中设置的过滤器参数相同。它命名为 `m_pFilterLogParam`。

## 其他函数和变量

以下函数用于辅助多音性。我们将在第 8 章详细讨论它们。它们用于实现动态器分配分配或器窃取（voice-stealing）。现在你可以跳过它们。

```cpp
void incrementVoiceTimestamps()
```

```cpp
CMiniSynthVoice* getOldestVoice()
```

```cpp
CMiniSynthVoice* getOldestVoiceWithNote(UINT MIDINote)
```

```cpp
bool doControlUpdate(ProcessData& data);
```

- 处理 GUI 控件变化的辅助函数

```cpp
bool doProcessEvent(Event& vstEvent);
```

- 处理 MIDI 音符和触后（aftertouch）事件的辅助函数

```cpp
void update();
```

- 更新合成器参数的函数

我们将在第 3 章和……详细讨论这些变量。

```cpp
// --- 滑音 (portamento)
double m_dLastNoteFrequency;

// --- 我们的接收通道（可选）
UINT m_uidiRxChannel;

// --- 用于转换日志过滤器控制值
Parameter* m_pFilterLogParam;
```

最后是你使用每个合成器章节自带 GUI 控件声明的合成器参数。

```cpp
// --- 合成器参数；在构造函数中初始化！
double m_dNoiseOsc_dB;
double m_dPulseWidth_Pct;
double m_dEGLOscIntensity;
double m_dFcControl;
```

等等，以及用于捕捉 MIDI 控制器变化的虚拟变量。

```cpp
// 这些是用于非音符 MIDI 消息的 VST3 特定变量！
double m_dMIDIPitchBend; // -1 到 +1
UINT m_uMIDIModWheel;
UINT m_uMIDIVolumeCC7;
```

`UINT m_uMIDIPanCC10;`

`UINT m_uMIDIEExpressionCC11;`

等等……

## 2.27 VST3 Processor 初始化

在 `VSTSynthProcessor.cpp` 文件中，你从构造函数开始处理插件的初始化。对于 VST3 插件，构造函数的第一行调用 `setControllerClass()` 方法，并传递 `Controller` 的 GUID 作为参数，声明与其配对的 `Controller`。这是底层 COM 组件的一部分，你不需要担心它，只需确保你的 `Processor` 组件始终在构造函数中调用它。以下是所有合成处理器的默认值，声明在 `SynthParamLimits.h` 文件中。打开 `MiniSynth` 的 `VSTController.cpp` 文件并对比 `initialize()` 中的参数声明。

（注：提供的输入包含大量重复，我提供的是唯一的内容流。）

此方法在不同的合成器上略有不同。宿主程序调用此方法来开启和关闭合成器。Steinberg 建议在激活时进行动态内存分配，在停用时销毁或释放资源。书中的每个合成器都会在此创建并销毁它的音器数组。基于采样的合成器项目将在此初始化动态创建采样数组。当宿主程序调用此方法时，项目的采样率已经设置（或更改）。我们所有的合成器在正常运行都需要采样率，因此我们在这里初始化它。细节将在后续章节中介绍。`Processor` 对象继承自基类 `AudioEffect`，该类声明了一个名为 `processSetup` 的成员变量：

`ProcessSetup` 是一个遵循以下定义的结构：

protected:

我们将使用 `sampleRate` 变量（类型为 `double`）在音器对象添加到栈中后为它们设置采样率：

`ProcessSetup processSetup;`

```cpp
int32 processMode;                //< ProcessModes
int32 symbolicSampleSize;        //< SymbolicSampleSizes
int32 maxSamplesPerBlock;       //< 每个音频块的最大采样数
SampleRate sampleRate;            //< 采样率
```

示例中，我们展示了 `MiniSynth` 的方法。如果 `state` 参数为 `true`，我们向数组中加载我们的音器对象，为音器对象设置采样率，调用 `update()` 方法初始化合成器参数并重置上一个音符频率变量。然后，我们创建日志参数对象。`prepareForPlay()` 方法将在第 8 章中讨论。在下面的代码中，功能被分为两个 `for()` 循环，它们可以很容易地合并为一个。保留两个循环的原因是为了与其他 API 进行比较，在那些 API 中这两个操作是分开的，不在同一个函数中。

如果 `setActive()` 的参数为 `false`，我们将卸载音器栈并删除指针。`MAX_VOICES` 定义了该合成器的最大复声数。最后，调用基类执行其设置工作。

```cpp
result PLUGIN_API Processor::setActive(TBool state)
{
  if(state)
  {
    // 加载音器
    for(int i=0; i<MAX_VOICES; i++)
    {
      CMiniSynthVoice* pVoice = new CMiniSynthVoice;
      if(!pVoice)
        return kInvalidArgument;

      m_pVoiceArray[i] = pVoice;
    }
    for(int i=0; i<MAX_VOICES; i++)
    {
      m_pVoiceArray[i]->setSampleRate((double)processSetup.sampleRate);
      pVoice->prepareForPlay();
    }

    // 批量更新
    update();

    // 清空
    m_dLastNoteFrequency = -1.0;

    // 辅助函数
  }
  else
  {
    // --- 删除音器
    for(int i=0; i<MAX_VOICES; i++)
    {
      delete m_pVoiceArray[i];
    }
    if(m_pFilterLogParam)
      delete m_pFilterLogParam;
  }
  return kSuccess;
}
```

# 2.28 VST3 序列化

序列化通过 `getState()` 和 `setState()` 方法处理。

## getState()

此方法在不同的合成器上略有不同。用户保存项目或预设时，宿主会调用此方法。宿主传递一个文件流指针，你可以用它写入合成器参数变量。`Controller` 的 `createComponent()`（通过读取文件设置 GUI）遵循我们在此方法中设置的顺序，必须非常仔细确保操作顺序完全一致。这里是 `MiniSynth` 方法的部分代码。与之前会话中的 `Controller` 示例一样，我们创建了一个 `IBStreamer` 接口并使用其方法写入我们的变量：

此方法在不同的合成器上略有不同。宿主程序调用此方法从预设文件设置合成器。这与你在 `Controller` 的 `setComponent()` 方法中看到的非常相似。区别在于，在该函数中，你直接从文件加载变量，而不需要将其转换为归一化值。读取操作的顺序必须与 `getState()` 方法中的完全匹配。这里是 `MiniSynth` 方法的部分，你可以看到在 `Controller` 示例中读取 `UINT` 和数据时所需的 `udata` 和 `data` 哑变量的用法。你还可以看到在产品发布和修订后添加额外参数时的版本控制。

```cpp
result PLUGIN_API Processor::getState(IBStream* fileStream)
{
  // 获取流接口
  IBStreamer s(fileStream, kLittleEndian);

  // --- MiniSynthVersion - 将此置于顶部以便在读取操作期间使用版本
  if(is.writeInt64u(MiniSynthVersion)) return kResultFalse;
  // --- 这些顺序与枚举的顺序一致
  if(is.writeDouble(m_dNoiseOsc_db)) return kResultFalse;
  if(is.writeDouble(m_dPulseWidth_Pct)) return kResultFalse;
  if(is.writeDouble(m_dEG10scIntensity)) return kResultFalse;
  // 等...
  return kResultTrue;
}
```

## update()

```cpp
tresult PLUGIN_API Processor::setState(IBStream* fileStream)
{
    IBStreamer s(fileStream, kLittleEndian);
    // 数据块
    uint64 version = 0;
    // 转换为 UINT
    uint32 udata = 0;
    int32 data = 0;

    // 读取版本
    if(is.read64u(version)) return kResultFalse;
    // 读取相同的顺序
    if(is.readDouble(m_dNoiseOsc_db)) return kResultFalse;
    if(is.readDouble(m_dPulseWidth_Pct)) return kResultFalse;
    if(is.readDouble(m_dEG10scIntensity)) return kResultFalse;
    // 等...

    if(version >= 1)
    {
        // // 在此处添加内容
    }
    return kSuccess;
}
```

（注：后续文本内容为上述内容的重复，已按要求要求未进行重复翻译。）

编码时，每个队列仅对最后一次更改的值进行处理。MIDI 事件的处理和音频渲染发生在 32 个采样点的子块中，这由我们在 `.cpp` 文件顶端定义的自定义 `SYNTH_PROC_BLOCKSIZE` 决定。可以自由更改此值以进行实验。我们现在可以将图 2.26 重新绘制为图 2.2，展示所有列表控制数据如何被忽略，以及 MIDI 和音频渲染如何被分解为子块。末尾有一个部分块，当音频缓冲区大小不是 `SYN_PROC_BLOCKSIZE` 的倍数时，它将在我们的处理循环中自动处理。

```cpp
process() {
```

```cpp
while processingSubblocks() {
```

图 2.2 显示了 `process()` 方法作为代码块的。阴影部分对所有合成器具有本质相同的代码。

## 访问控制队列

为了使 `process()` 函数更短，我们创建了两个辅助函数来处理控制队列和 MIDI 事件。控制队列处理程序是 `doControlEvents()`，它接受一个 `ProcessData` 引用，该引用被传递给 `process()` 函数。

```cpp
} // while loop
} // process
```

```cpp
bool Processor::doControlEvents(ProcessData& data)
```

我们从封装在 `processData` 结构中的 `IParameter` 接口获取计数，并遍历队列。如果用户没有更改任何控制，则没有需要处理的内容。使用 `IQueue` 接口访问每个队列调用 `getPoint()` 方法，并将 `value->getPoint()-1` 作为目标点的参数；这代表队列中的最后一点。情况下，消息每 10ms 更新一次。其他参数返回：一个 `sampleOffset` 值，为了简单我们忽略了它，因为我们只需要最后一个控制值以及在 [0..1] 范围内的归一化（原始）控制值。为了将此值转换为我们合成器有意义的信息，这是通过我们在 `synthfunctions` 中编写的辅助函数 `coolVSTGUIVariable()` 完成的；它根据参数返回基于 `float` 类型的数据。该值可以被转换为 `int`、`UINT` 或其他数据类型作为布尔。例如，你可以看到 `OCTAVE` 控制更改正在被处理。因此，这些控制 ID 值与你在控制器的 `initialize()` 方法中为每个控制设置的值完全相同，你编写了一个长的 `switch/case` 语句来解码并处理每个单独的控制，将其保存到我们的 `Processor` 控制变量中。在语句末尾，如果 `count` 大于零，你调用 `update()` 方法在我们的语音对象上设置新变量。这段代码是从 `doControlEvents()` 函数提取的。
