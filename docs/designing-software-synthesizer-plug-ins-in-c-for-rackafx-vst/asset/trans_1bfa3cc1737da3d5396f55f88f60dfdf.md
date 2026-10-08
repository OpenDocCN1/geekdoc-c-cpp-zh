
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

`LogScaleParameter` 类似于 `RangeParameter`，但控件按对数方式移动。我们将专门用于滤波器截止频率控件，希望以对数方式移动。

### Parameter Container

Controller 类声明了一个 `Container` 来持有所有的控件。这本质上是一个链表。你声明你的 `Parameters` 并它们添加到 Container 中，并在需要时评估控件的值。Container 的名为 `parameters`，在 `vstedcontainer.h` 中声明

`ParameterContainer parameters;`

### Normalized and Plain Parameters

VST 中的一个重要概念是 GUI 控件传输参数。在我书中（以及 VST 的早期版本）中，这些被称为“原始”（raw）值。有时参数的范围可能是 0.0 到 1.0，但大多数时候不是。例如，所有滤波器的截止频率控件范围为 80.0 Hz 到 18 kHz——在 UI 上你会看到这些值，但当用户移动控件时，GUI 传输归一化或原始值。编写代码确定映射值取决于你。VST3 将映射值称为“普通”（plain）值，而在 VST2 和 RackFX 中它被称为“编码”（coded）值，将归一化/原始值转换为普通/编码值的函数是“处理函数”（cooking function）。我们已经在 `synthfunctions.h` 中为你提供了处理和反处理你变量的函数；你提供最小、最大和原始/处理值。在我们的所有合成器项目中，Container 将负责在用户移动控件时让 UI 具有处理值。这是通过映射到归一化值（如果使用 `LogScaleParameter` 则为对数）来实现的。这在控件自动化的情况下产生了一个问题，用户想要随歌曲信息实时召回他的控件移动。如果你的控件不是线性或对数方式映射，你需要提供一些从普通到归一化的转换代码。在我们的项目中不需要这个，因为我们将提供所有函数并跟踪你自己的变量及其原始/处理映射。

为了实现你的 Controller 对象，请遵循以下步骤：

- 每个控件都有一个索引，因此在 `SynthParamLimits.h` 文件中以枚举的形式列出
- 决定 UI 并为每个控件建立最小、最大和默认值
- 在 `VSynthController.cpp` 文件中声明 UI 参数并将添加到 parameters container 中；这将设置默认 UI 所有
- 编写执行读取侧序列化的代码

- 实现 MIDI 控制器映射（控制器暴露 `IMIDapping`）

让我们从参数开始。假设我们正在 Controller 中实现上述四个控件。确保你理解稍后可以作为章节挑战的一部分添加你的控件和变量。

## 第一步：为控件索引枚举一些常量

你可以选择任何 way顺序。你将参数添加到控件列表的顺序将最终决定它们在默认 GUI 中的顺序，但在自定义 GUI 中你可以将它们放在任何地方。尽管这是一个任意分配，但不要重新排列这些是重要的，否则你可能需要更改自定义 GUI 中的某些连接。在每个合成器中，此枚举列在 `SynthParamLimits.h` 顶部：

```cpp
enum (
    VOLUME_DB,          /* 0 */
    OCTAVE,             /* 1 */
    FILTER_CUTOFF,      /* 2 */
    FILTER_TYPE,        /* 3 */

etc...

    NUMBER_OF_SYNTH_PARAMETERS); // 始终在最后，这里是 4
```

枚举会自动创建 UINT 值列表。列表中的最后一个值将始终是参数计数。当你添加或删除自己的控件时，你将修改此列表。

## 第二步：决定控件的最小、最大和默认值

这些都定义在每个合成器项目包含的 `SynthParamLimits.h` 文件中。请查看此文件获取定义。

## 第三步：在 Initialize() 方法中创建参数并添加到 Container

这是一个非常直观的过程，通过在 `VSynthController.cpp` 文件中的示例进行解释。我们将
