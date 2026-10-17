
微软和 Steinberg 的 ID 都是 128 位的，所以你只需要格式化数字。例如，为了将上述 Microsoft GUID 作为此 Controller 的 VST FUID，你如下所示复制数字，删除横线并合并：

```
GUID({846EB93F-3247-4B8F-A901-10E8EDACC34})
```

变为：

```cpp
FUID Controller::cid(0x846EB93F, 0x32474B8F, 0xA90110E8, 0xED4ACC34)
```

## 2.18 VST3 插件架构

现在你已经了解 COM 的一些基础知识，让我们回顾 VST3 插件架构，特别关注你的插件。图 2.21 显示了更以 COM 为中心的 VST3 插件架构；Processor 和 Controllers 是具有接口的真实 COM 对象，由圆和线表示，这些是某种程度上偏移的控件。你可能会将 VST 客户端认为是一个多臂实体，手放在每个接口控件上，在接口之间来回跳跃。

在 Processor 上，`IAudioProcessor` 接口暴露了许多接口，我们将使用它们来接收 MIDI 事件、控制信息和音频 I/O，因此你的插件将是仅输出的。在 Controller 上，

`jTextField` 维护 GUI 参数，`IMIDIMapping` 负责处理 MIDI CC 到 GUI 参数的映射，而 `IVGroup` 用于实例化我们的 GUI。

Processor（处理器）的职责之一是声明插件的输入和输出能力。Processor 具有三种不同的 I/O 类型：音频、MIDI 事件和参数。图 2.22 显示了一个通用 Processor 的块图。音频和 MIDI 事件在总线（busses）中移动，总线是从 0 开始索引的，并命名为 `bus 0`、`bus 1` 等。插件可以拥有输入和输出总线的任意组合。在本文最通版本中，Processor 可以接收和传输 MIDI 事件和控制变化信息。

音频总线可以具有任意数量的通道，以防将总线（bus）与通道（channel）混淆。我们的合成器插件将实现一个名为 `bus 0` 的单音频输出总线，以及一个具有立体声通道的 `bus 3`。MIDI 事件总线包含我们决定的若干个 MIDI 通道。Processor 只有一个不需要声明的唯一参数总线。我们的合成器插件仅接受输入参数而不会传输任何参数，尽管模板代码在你想实验从插件外传递参数和 MIDI 信息时提供了支持。

图 2.23 所示的组件描述了 GUI 如何与其容器中的参数进行通信。在这种情况下，GUI 可能是默认版本也可能是自定义设计。MIDI CC 信息可以映射到 GUI 控制控件，作为一种外部控制机制。我们可能还会使用子控制器作为某些复杂 GUI 控制控件的助手；我们将在第 11 章中将其用于摇杆控制器。`Controller` 对象不需要声明任何总线，底层接口已经为你完成了大部分工作，因此你实际上只需要设置 Controller 以及可选的自定义 GUI。在一切都妥善设置后，它基本上会处理自己的操作。这是 VST3 的一个非常好的特性。

![](img/b42d0dca53f4a889d8162d55f7c8c05d_73_0.png)

图 2.21：VST3 插件架构的完整视图显示了它的 COM 组件和接口。

图 2.22：通用插件 Processor 组件包含了用于处理 I/O 的总线。

![](img/b42d0dca53f4a889d8162d55f7c8c05d_73_1.png)

图 2.24 显示了 VST3 合成器架构的完整图。MIDI 控制器向 Processor 发送事件，向 Controller 发送控制事件。Processor 只有一个输入总线（`bus 0`）和一个输出总线（立体声输出总线 `bus 0`）。尽管 Controller 维护着用户界面，但 Processor 也会接收控制变化信息。这张图非常有启发性。首先，MIDI 控制器消息如何绕远路通过参数容器，然后进入 Processor。虚线显示了 VST3 框架交付给 Processor 的参数，用于控制 GUI 变化和 MIDI 控制器事件。这是设计如此，因此我们可以动态重路由 MIDI 控制器。我们将在 2.25 节中讨论 MIDI 控制器的细节。接下来，你可能会想，为什么我们需要 VST3 框架来交付参数。当你需要访问 GUI 数据时，你不能像访问 AU 参数那样以类似的方式查询 `Controller` 对象。Controller 和 Processor 对象的分离是 VST3 设计的关键部分，并且花费了很大精力保持这些对象分离。虽然可以通过宿主机在对象之间建立通信路径，但你不能在实时使用该路径；它太慢了，会拖慢系统。详情请参阅 VST3 文档。编写 VST3 插件的工作涉及为每个 GUI 控件声明变量；如果 Processor 能直接访问 Controller 的参数，我们就不需要那样做了。在 AU 插件中就是如此。

#define stringPluginName "MiniSynth"

BEGIN_FACTORY_DEF ("Will Pirkle",

```
http://www.willpirkle.com/synthbook/,
mailto:will@willpirkle.com)
```

如果你将此作为模板使用，你需要将插件名称从 MiniSynth 更改为你的新插件的名称，当然还需要更改制造商（Will Pirkle）以及网站等。下面是两个以 `Processor` 开头的巨型声明：

```
DEF_CLASS2 (INLINE_UID_FROM_FUID(Steinberg::Vst::MiniSynth:
Processor::cid),
PClassInfo::kManyInstances,
kVstAudioEffectClass,
stringPluginName,
Vst::kDistributable,
Vst::PlugType::kInstrumentSynth,
FULL_VERSION_STR,
kVestVersionString,
Steinberg::Vst::MiniSynth::nProcessor::createInstance)
```

重要的变量已用**粗体**标识——顶部是唯一标识此组件的 `cid` 或 `FUID`。`PClassInfo::kManyInstances` 表示主机可以多次实例化同一个插件对象。除非你有非常充分的理由将插件限制为一个实例——例如它是一个演示版本——否则请忽略它。`kAudioEffectClass` 告诉客户端我们是一个音频效果，而 `kDistributable` 标识我们实现了两个独立的独立组件，这些组件可能运行在不同的处理器、处理器上下文或计算机上。`PlugType` 是一个合成器（`kInstrumentSynth`），最后一个参数是我们的创建函数。

`Controller` 的声明类似，包含一个 `FUID` (`cid`) 和其他标记。在 `Controller` 声明中不使用 `kDistributable` 和 `PlugType`，因此参数列表中是 0 和 `""`。

最终，你的每一个合成器插件项目都将包含以下文件。每当你开始一个新项目时，你主要将在这些文件中工作：

- factory.cpp

- VSTSynthProcessor.h

- VSTSynthProcessor.cpp

- VSTSynthController.cpp

回到 Visual Studio 中的 MiniSynth 项目，你可以看到解决方案（Solution）包含两个项目。一个命名为 `base_x`，其中 X 根据你的 Visual Studio 版本可能是 9 或 10。该项目首先被编译，并创建一个封装在 `.lib` 文件中的静态库。第二个项目包含几个文件：

- plugininterfaces

- public.sdk

- vstgui4

这前三组包含了大量的支持文件，用于从基类管理、接口到 GUI 控制的各个方面。你永远不需要修改这些文件中的任何一个。

`SynthCore` 组包含了你首先将开发的所有合成器 C++ 对象。这些文件随项目而异，但通常相似度达 90%。如果你在前面的章节中已经正确设计并调试了这些对象，那么在设计合成器时，你就不需要再次修改它们，除非你想添加原始项目中未包含的内容。

`Resources` 组包含了构建所需的旋钮图像、背景图像以及 `.uidesc` 文件。`Source` 过滤器是上一节中讨论的过滤器对象，包含 `logscale.h` 和 `version.h` 两个文件，你都不需要修改它们。

## 2.21 VST3 约定

在 VST3 中，你会看到一些需要注意的约定。

### 命名空间的使用

VST3 使用命名空间来避免命名冲突。`Processor`、`Controller` 和 `classfactory` 文件都用三个命名空间包裹内容。对于每个合成器，你需要将第三个命名空间更改为合成器的名称；

这里是 MiniSynth 的命名空间结构。

你会在类定义中使用 `factory .cpp` 文件时看到这些内容，例如：

```
namespace Steinberg (
namespace Vst (
namespace MiniSynth (
```

```
<--- 接口或实现 ---

))) // 命名空间
```

`INLINE_UID_FROM_FUID(Steinberg::Vst::MiniSynth::Processor::cid)`

and

`Steinberg::Vst::MiniSynth::Processor::createInstance`

你还可以看到不同命名空间作用域的使用方式（再次来自 factory.cpp）。

`Vst::kDistributable`

如果你需要更多关于命名空间的信息，请访问 www.cplusplus.com。

### 常量以 ‘k’ 开头

在 VST API 中，你会看到匈牙利命名法（Hungarian notation）。当 Steinberg 声明常量值时，他们会在常量开头添加匈牙利命名法提示 "k"，例如 `kResultTrue` 和 `kResultFalse`。也许这是因为德语中“常量”的单词是 *konstante*？

### 方法返回结果

几乎所有的 VST 方法（COM 除外）都返回类型为 `tresult` 的成功代码，它被定义为 32 位整数。`kResultTrue` 和 `kResultFalse` 是成功或失败的常用返回值。

### 方法声明为 PLUG_API

`PLUG_API` 简单定义为 `__stdcall`，这在 RackAX 章节中讨论过。

### 多字节字符与 UString

VST3 设计用于使用多字节字符（或宽字符串）。ASCII 字符使用 8 位字节编码，而多字节字符使用 16 位，允许更多的字符。Steinberg 提供了一个 `UString` 对象来处理这些字符串并在 ASCII 之间进行转换。在我们的项目中，真正需要它的唯一时刻是我们想将字符串字面量作为函数参数时。例如，对于 ASCII 字符串字面量，你可能会调用此方法：

```
setPluginName("Awesome Synth");
```

`ustring.h` 中有一个名为 `USTRING()` 的宏，允许我们：

```
setPluginName("Awesome Synth");

setPluginName(USTRING("Awesome Synth"));
```

### 类模板

使用类模板可以在处理参数时具有灵活性。使用类模板可以减少代码量。

### 数据类型的重声明

VST3 还重声明了数据类型为 `int32`、`uint32`、`int16`、`int64`。

## 2.22 实现 VST3 插件：Controller

`Controller` 实现创建、初始化、序列化、处理和 MIDI 事件。在 `VSTSynthController.h` 中你可以找到原型。注意基类：

- EditController：处理 GUI 和参数功能

- IMidiMapping：MIDI 映射

- VST3EditorDelegate：处理自定义创建和接口

当你实现合成器时，你会获得关于如何将各种代码块放入这些文件中的指令。这些

对于每个合成器，处理过程都是相同的，尽管变量名和某些代码会略有不同。

你可能需要回看这一章，因为它将解释插件内部正在发生什么，而不会深入到每个合成器的细节。当你添加、删除或更改任何用户 GUI 底层结构时，你正在修改 Controller。设置供使用的控件有一个简单的四步流程；只要你恰当地遵循这个顺序，你的 GUI 就能正常工作。

Controller 对象定义了你插件的 GUI 控件，我们的自定义 GUI 也依赖于此。称为 `Parameters` 的对象代表 GUI 控件，Controller 在 `Container` 内部存储一组此类 `Parameter` 对象。如果需要，你可以从其中访问中心和 `Parameters`。Controller 通过从零开始的索引从 GUI 发送和接收值。当用户移动控件时，GUI 会发送一个从 0.0 到 1.0 的归一化值（称为原始值），以及一个标识控件的索引或 ID（称为标签）。当 Controller 想要在启动或自动化期间更改控件的位置时，它会将索引化的归一化值发送到 GUI。因此，理解每个 `Parameter`（GUI 控制）都有一个索引是非常重要的。控件可能会为了一起移动而共享相同的索引，但我们不会有任何共享控件——我们的每个索引值必须是唯一的。

图 2.25：Controller 从控件发送和接收归一化值；一个名为 `parameters` 的容器存储了 `Parameter` 对象集。

![](img/b42d0dca53f4a889d8162d55f7c8c05d_83_0.png)

在 Processor 端，每个 GUI 将被用于控制底层变量。当用户移动控件时，该变量将改变，音频渲染也将随之修改。本书中的所有合成器项目都将使用这些类型的变量：

- double

- int

- enumerated UINT（即 enum）

连接到 `double` 变量的控件最终将生成连续的双精度浮点值。`int` 控件将生成基于整数的值。`enumerated UINT` 控件将生成无符号整数（UInts），这些值将映射到枚举列表中的字符串。在 VST3 中，你不需要像在 RackAFX 中那样实现枚举，你将负责知道哪些字符串映射到值。

## 2.23 VST Controller 初始化

Controller 的初始化涉及你 UI 的所有参数，无论你使用的是自定义版本还是内置版本。在每个合成器项目中，你将获得一个定义 GUI 控件的表格，类似于表 2.8。你需要将此表的每一行转换成你的控件。对于 VST3，你将在 Controller 和 Processor 实现中都使用此表。以下是该行中两个对象将使用的部分列表（两个组件在引用各种 `Parameters` 时使用相同的索引，此处未包含该索引；建立索引列表取决于你）：

Controller:

- 控件名称

- 单位

- 下限

- 上限

- 默认值

- 枚举字符串

- 变量类型（仅用于序列化）

Processor:

- 变量类型（用于序列化和控制合成器）

- 下限

- 上限

- 默认值

在下方的“Variable Name”（变量名）代表定义在你的 Processor 对象上的变量。Controller 对象将不会使用此变量名引用控件，这种分离是非常重要的。我们在讨论实现 Processor 对象时将再次访问此表。假设我们查看其中一个表中的四个特定控件：

表 2.8：某些 GUI 控件示例。

| 控件名称 (单位) | 类型 | 变量名 (VST3, RAFX) | 低/高/默认 | VST3/AU 索引 |

| --- | --- | --- | --- | --- |

| Volume (dB) | double | m_d_dB | -96 / 24 / 0.0 | OUTPUT_AMPLITUDE_DB |

| Octave | int | m_nOctave | -4 / 4 / 0 | OCTAVE |

| Fc (Hz)(volt/octave) | double | m_dFilterFc | 80 / 18000 / 10000 | FILTER_FC |

| 控件名称 | 变量名 | VST3/AU 索引 |

| --- | --- | --- |

| Filter Type | m_uFilterType | LPF,HPF,BPF |

基础变量类型是 float、int 和枚举 UINT。Octave 和 Octave 控件通常生成用户在 GUI 中使用的数值值，它们有最小限制（Lo Limit）、最大限制（Hi Limit）和默认值（Def）值。Fc（滤波器截止频率）控件具有“volt/octave”，这意味着该控件是逻辑性的。Filter 控件显示当前值的字符串。无符号整数（UINT）跟踪当前设置。Enum String 给你逗号分隔的值，将映射到 UINT。例如：

- LPF: 0

- HPF: 1

- BPF: 2

每个控件被称为“parameter”，并有一个 `Parameter` 对象来处理细节。控件通过索引引用。跟踪并维护此系统取决于你。如果你更改了索引值，你的控件可能无法正确映射。跟踪索引值的简单方法是使用枚举。VST3 限制、默认值和枚举都包含在 `SynthParamLimits.h` 文件中，每个合成器都不同。我们将使用 container 来持有它们。

### RangeParameter

`RangeParameter` 代表具有最小、最大和默认值的连续控件。一个简单的例子是音量控制，最小值为 -96，最大值为 +24，默认值为 0。控件在该范围内平滑移动。

### StringListParameter

`StringListParameter` 定义了一个由一组固定字符串定义的控件。示例可能是“Filter Type”控件，用户从 LPF、HPF 等字符串列表中选择。我们还将通过将字符串限制为 ON 和 OFF 来将其用于开关控件。

### LogScaleParameter
