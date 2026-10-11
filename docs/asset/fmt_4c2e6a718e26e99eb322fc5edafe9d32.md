
启动并处于激活状态后，你可以开始添加控件了。让我们从第一个名为 `Volume`（音量）卷开始。设置这种连续控制，在滑块控制的边界框内点击右键。边界框是每个滑块周围的细灰色框，如图 2.2 所示。重新启动 `Slider Designer`（滑块设计师），使用它的一种简单方法是通过填充内容来创建控件。例如，右键点击左角的第一个滑块。它会生成你在图 2.9 中所示的表单。

你需要在 `Slider Properties`（滑块属性）中填写正确的值。你会注意到此滑块的 `uControlID` 为 `0`。这是将滑块链接到变量的 ID。你无法编辑此单元格。从 `Control Name`（控件名称）开始输入“`Volume`”（不带引号）。按进到下一个单元格，然后将 `Units`（单位）设置为“`dB`”。下一个单元格是最重要的之一——它是将链接的变量的数据类型；可以从下拉列表中选择。你可以用鼠标选择数据类型，也可以在框被高亮时直接输入第一个字母（例如，对于 `double` 输入 "`d`”）。将此图与表 2.6 的第一行进行比较，你就可以看到如何将表格行转换为控件配置。你现在可以忽略 MIDI 相关内容——请查看我的网站了解如何将 MIDI 控制器连接到任何 GUI 组件以使用此选项。然而，在左侧有一组重要的设置：

- `Linear Slider`（线性滑块）
- `Log Slider`（对数滑块）
- `One/octave Slider`（单八度滑块）

线性对数（算术）滑块随这些偏移移动，如果需要，可以使用对数控制音量。然而，对于某些合成器频率控制（如滤波器的截止频率），你需要选择 `volt/octave`（伏/八度）选项。这将使控件以 2N 方式（即以八度为单位）工作，这是合成器使用这种比例的工作方式（注意：在 VST3/AU 中，这种 volt/octave 被称为 "`arithmic Scale`”）。如果你发现错误或漏掉了某些，只需在滑块框内点击右键修复问题。你也可以通过点击属性窗口上的按钮删除滑块，并通过 `Copy Existing Slider Control`（复制现有滑块控件）下拉列表复制另一个滑块的设置。

当你从主 UI 添加、编辑或删除控件时，你会注意到 `RackAFX` 会闪烁编译器并为你编写代码。你可以将此闪烁作为代码更新已同步的信号。如果你不喜欢，最小化编译器，闪烁就不会发生。在 `View->Preferences`（视图->设置）中有一个特殊的复选框可以启动编译器（仅限 Visual Studio 2008；Microsoft 后来删除了此功能）。

你的插件代码将使用索引值 `0`（属性对话框中的 `uControlID`）将 UI 上名为 `Volume` 的滑块映射到 `m_dB` 变量。设置好 `Volume` 控制后，切换到 Visual Studio 编译器（提示：使用 `File -> C++` 提示来保存 `.sln` 文件，始终选 YES，并查看我的网站获取如何消除大部分弹出窗口的信息）并打开你的项目 `.h` 文件。在底部附近你会看到 `RackAFX` 为你编写的新变量声明：

```cpp
class CThrowAway : public CPlugin
{
public:

  <SNIP SNIP SNIP>

  // ADDED BY RACKAFX -- DO NOT EDIT THIS CODE!!! ---
  // **-0xD7FD-**

  double m_dVolume_dB;

  // **-0x1A7F-**
  //
```

| Volume | UI Item | Property |
|---|---|---|
| 0.00 dB | `uControlType` | Slider |
| | `uControlID` | 0 |
| | `Control Name` | Volume |
| | `Units` | db |
| | `DataType` | double |
| | `Variable Name` | m_dVolume_dB |
| | `Control Limit` | -96 |
| | `Control High Limit` | 24 |
| | `Initial Value` | 0.00 |
| Learn MIDI | MIDI Controller | false |
| Channel -n/- | MIDI Controller Type | Continuous Controller |
| Type -n/- | MIDI Controller | 3 Continuous Controller #3 |
| Control Method | | |

图 2.9：`Slider Designer` 使定义你的代码并将其链接到底层变量变得简单。

你将会在代码中频繁看到该注释，作为一种提醒，为了方便阅读可以将其删掉。除了第 2 章讨论的插件函数外，你还会看到更多注释代码区域。在第一部分，你可以像在 `.h` 文件中那样添加变量或函数定义。尝试将你的代码保持在指定区域。下面的区域写着：`// ADDED BY RACKAFX -- DO NOT EDIT THIS CODE!!!` 这非常重要——你会在该区域看到你的变量 `m_dVolume` 定义。这是 `RackAFX` 在你添加、编辑或删除控件时修改的 `.h` 文件部分。代码还有具有有趣的十六进制符号（`0x1A7F...`）的属性，不要编辑它们之间的代码。`RackAFX` 为你编写 C++ 代码。你必须小心不要以任何方式更改 `RackAFX` 的 C++ 代码。

现在练习设置 `Octave`（八度）控制——选择整数数据类型并进行填充表格。由于这是一个 C++ 枚举，你必须确保对字符串使用合法值；例如，你的子字符串不能以数字开头，不能包含保留字符 `*`。如果你编译并得到引用枚举的错误，请检查字符串名称的合法性。如果你需要更改枚举字符串，请在 `RackAFX` 中进行。在图 2.10 的左侧，你可以通过输入文本看到枚举字符串的模拟图。这就是你确保字符串不会超出控件的方法（提示：使用有意义的字符串）。你还可以看到它的索引为 41。

### 2.10 设置索引控件：单选按钮

继续查看表格，我们找到了两个枚举控件。让我们先练习设置单选按钮。在与第一个滑块位于同一行的第一个按钮组的任何位置点击右键，并使用类似的 `Radio Button Designer`。从数据类型列表中选择 `enum`（枚举）。对话框打开，显示字符串输入框和另一个填充了当前枚举字符串的列表。你可以通过双击下框框中的字符串，在控件之间共享这些列表，这会将字符串传输到“This enum list:”。图 2.11 显示了新的 `Slider Designer`。在 `enum` 模式下，高限、下限和默认值是不可编辑的。双击此行以填充枚举列表。

### 2.11 设置索引控件：滑块

继续查看表 2.6，我们找到了另一个名为 `FX Filter`（滤波器）的滤波器类型。该控件使用三个滑块作为第一种滤波器类型：`LPF`（低通）、`HPF`（高通）、`BPF`（带通）。你可以放置一个滑块控件作为枚举控件使用。右键点击另一个滑块组并选择 `enum`。

### 2.12 在 LCD 控件内部放置控件

![](img/b42d0dca53f4a889d8162d557c8c05d_49_0.png)图 2.10：配置单选按钮组像滑块控件一样简单。

`RackAFX` UI 的右上角有一个代表 alpha 轮、`LCD` 显示器视图和旋钮的控件。在项目设计期间，我注意到 `LCD` 用于向你提供项目和计算机状态的反馈。然而，它也可以像其他滑块一样作为 GUI 控件。`LCD` 允许内部存储多达 1024 个连续滑块。任何使用普通滑块设置的内容在嵌入 `LCD` 中也同样有效，`GUI Designer` 让你在自定义的 GUI 上选择一个。该控件有几种用途：

- 它是存储连续控件的一种方式
- 如果滑块用完了，你可以在 `LCD` 中放入更多的 1024 个
- 你可以使用枚举控件创建一组预设或其他全局函数/配置——我们将广泛用于合成器的全局参数，如音高范围，并通过使用小控件来精简 GUI

图 2.12 显示了嵌入了两个控件的 `LCD` 控件示例。alpha 轮用于选择 `Filter Fc` 或补丁（patches）。数值旋钮用于调整控件值。右侧显示你正在使用哪个控件。

让我们从表 2.6 添加 `Filter Fc` 控制。首先要设置 `LCD` 控件，请在开发模式下（未加载插件）点击右键。弹出的对话框如图 2.13。点击打开非常相似的 `Slider Properties` 对话框。使用表 2.6 填写表单，注意 `volt/octave` 比例为

![](img/b42d0dca53f4a889d8162d557c8c05d_50_0.png)限值和默认值不可编辑。双击此行以填充枚举列表。

图 2.11：你可以将滑块作为索引控件。

![](img/b42d0dca53f4a889d8162d55f7c8c05d_51_0.png)

图 2.13：使用“New”（新建）、“Edit”（编辑）和“Remove”（删除）按钮向 `LCD` 添加控件；在这里我们正在设置使用伏特/八八aves为单位的 `Filter Fc` 控制。

你可以通过按钮添加、编辑或删除控件。你还可以使用“Move In List”（在列表中移动）微调按钮更改列表中控件的顺序。列表中的顺序就是控件在编译后的插件（即 `LCD` 控制）中出现的顺序。接下来，设置 `Patch`（补丁）控制，使用下划线（`_`）来分隔你列表中的字符串（你可以在枚举名称中使用空格）。你可以利用 `LCD` 控制的一项功能：当 `LCD` 使用这些名称时，它会将下划线替换为带空格的标题。当你输入一个枚举名称时，这比使用旋转旋钮或普通滑块提供了更大的灵活性。因此，请在 `Heavy_Lead`、`Lush_Pad` 和 `Space_Cad` 单词之间使用下划线。设置好此控件后，在 Visual Studio 或 `RackAFX` 中使用“Rebuild”（重新生成）重建项目。编译完成后，使用“Load”（加载）按钮加载 DLL。尝试不同的控件，注意带有 `Patch` 的 `LCD` 控制单词之间是否有如图 2.14 所示的空间。

如果你下载了示例项目，你会发现 `LCD` 控制内部嵌入了多个控件。

## 2.13 使用 RackAFX GUI 设计器

`RackAFX` 拥有一个强大的 GUI 设计器，可以让你在几分钟内布置出视觉良好的 GUI。GUI 设计器不断更新以包含更多功能，因此请务必在网站上查看最新添加。根据你拥有的版本，你的 GUI 设计器看起来与图 2.15 所示相似。操作流程如下：

- 在原型（prototype，即主 `RackAFX`）中，你组装你的插件。创建控件，为它们赋予最小值、最大值初始值，将它们连接到变量等。由于这是开发模式，你可能会更改某些控件、添加或删除它们等。此外，由于我们处于原型设计阶段，你可以设置一组你不希望用户在最终插件中调整的控件。
- 你的插件编译、调试并准备就绪后，使用 GUI 标签页显示图 2.15 所示的空白 GUI。
- 从左侧的调色板上拖放控件并将它们排列在表面。由于它们具有透明背景，因此可以相互重叠。
- 对于滑块、单选按钮和旋钮控件，你必须将它们连接到插件中受控制的变量。
- 矢量摇杆不需要任何额外设置。

图 2.14：通过在设计表单中插入下划线，枚举字符串可以包含空格。

![](img/b42d0dca53f4a889d8162d55f7c8c05d_52_0.png)

2.15：GUI 设计器主要由左侧的控件面板和右侧的大 GUI 设计区域组成。

使用“Background Pattern”（背景图案）框选择背景图像或颜色；在这里选择了白色。顶部的全局按钮允许你更改字体、清空设计区域中的所有控件并更新代码（稍后详细介绍）。当你拖动控件时，右键点击旋钮本身；对于单选按钮，点击任何一个按钮；对于滑块，点击滑块控件。如果你将其释放到设计区域，就可以对其进行移动和自定义。右键点击控件以调出变量链接和自定义框。

注意：当向设计区域添加控件时，始终从左上角开始排列，这样控件在最终的 GUI 中就能被正确裁剪。

原型中的任何滑块都可以使用左侧的调色板作为旋钮或滑块进行拖放。图 2.16 显示了在放置第一个旋钮后，并在右键点击已放置的旋钮进行设置后的 GUI 设计器。在 GUI 控件设置中，你可以：

- 通过下拉列表将旋钮连接到变量
- 更改旋钮和组合的外观
- 更改行为；隐藏它或更改其颜色
- 设置所有其他旋钮以匹配这一个

现在，执行相同的操作，但拖入一个滑块。它连接到 `Filter` 控制，因此在带有滑块自定义选项的下拉框中选择它。要移除滑块或旋钮，请从变量下拉列表中选择“none”（无）。拖入一个单选按钮组并同样通过右键点击进行设置。它会自动为你分配单选按钮，从第一个组开始向下处理。如果你尝试绘制单选按钮组但系统不允许，这意味着你已经用完了这些控件。最后，将 `LCD` 拖入设计区域并右键点击进行设置。你应该会得到与图 2.17 类似的结果。

在 `LCD` 设置中，你可以添加或删除控件并设置配色方案。你可以更改控件的顺序。GUI 与原型 UI 略有不同，任何连续控件都可以放在内部，而不只是你正在分配的那些。这意味着你可以拥有一个仅由 `LCD` 控制和单选按钮组成的 GUI。使用“Add”和“Remove”按钮添加和删除控件。你可以通过“Move In List”更改列表顺序。添加控件后，关闭设置。此时，在准备就绪之前还有最后一步——你需要返回并重新编译插件以将 GUI 嵌入其中。这与 VST GUI 设计器的工作方式相同。在 `RackAFX` 中，这意味着你需要更新代码。有两种方法可以：要么切换回 Prototype，要么使用左上角的“Update Code”按钮。如果不通过这种方式更新代码，设计将不会保存。切换回 Prototype 查看 GUI 并点击“Rebuild”重新生成项目。现在使用“Load”按钮加载 DLL。你会发现 Custom GUI 现在处于激活状态——它看起来像一个旋钮。点击此按钮，你会发现带有 `Patch` 的 `LCD` 控制单词之间有空格，如图 2.14 所示。

如果你下载了示例项目，你会发现 `LCD` 控制内部嵌入了多个控件。

在 Visual Studio 中，选择 `MiniSynth.h` 文件并滚动到底部，查看设置 GUI 时添加的所有变量。注意 `double`、`int`、`UINT` 和 `enum` 的组合。例如，`UINT m_uVoiceMode` 使用其正下方的枚举列表向用户显示可能的声色设置。

```cpp
class CMiniSynth : public CPlugin
{
public:
    // RackAFX plug-in API Member Methods:

<SNIP SNIP SNIP>

// ADDED BY RACKFX -- DO NOT EDIT THIS CODE!!!
// **--0x07FD--**

UINT m_uVoiceMode;
enum(Saw3,Sqr3, Saw2Sqr, Tri2Saw, Tri2Sqr);
double m_dDetune_cents;
double m_dFCcControl;
double m_dLF01Rate;
etc...

// **--0x1A7F--**
//
};
```

现在，关注文件顶部的成员函数。我们将为自己的合成器项目重写和或实现 `CPlugin` 函数：

## 标准插件函数：

Here 你看到构造函数和析构函数，我们使用它们来初始化变量和销毁对象。

```cpp
CMiniSynth():
  allocate dynamic memory
  initialize variables
```

```cpp
virtual ~CMiniSynth():
  deallocate any allocated memory
```

```cpp
virtual bool __stdcall prepareForPlay():
  每次运行初始化函数
  始终在子组件上设置采样率
  始终更新合成器对象
```

```cpp
virtual bool __stdcall processAudioFrame(float* pInputBuffer,
  float* pOutputBuffer,
  UINT uNumInputChannels,
  UINT uNumOutputChannels);
```

```cpp
virtual bool __stdcall userInterfaceChange(int nControlIndex):
  这里是渲染合成的音频输出的地方
  在用户移动 GUI 上的控件后调用；你可以选择在此处不进行处理：在所有情况下我们都会调用合成器更新函数
```

## MIDI 和摇杆控制函数

表 2.3 列出了我们将实现的 MIDI 函数，你可以在标记为“高级函数”的区域找到它们的原型。在 `VectorSynth` 和 `AniSynth` 中，我们将使用矢量摇杆，它会发出位置和混合信息。该方法也在组函数中：

```cpp
virtual bool __stdcall joystickControlChange(float fControlA,
  float fControlB,
  float fControlC,
  float fControlD,
  float fACMix,
  float fBDMMix);
```

- 表示用户移动了内置的矢量摇杆，我们在 `VectorSynth` 中使用了它
- AniSynth

```cpp
<SNIP SNIP SNIP> -- 你可以跳过函数 8 和 9
virtual bool __stdcall midiNoteOn(UINT uchannel,
                               UINT uMIDINote,
                               UINT velocity);
```

- 为每个 MIDI note 事件调用，传递通道、音符和速度

```cpp
virtual bool __stdcall midiNoteOff(UINT uchannel, UINT uMIDINote,
                                      UINT velocity, bool bAllNotesOff);
```

- 为每个 MIDI note off 事件调用
- 也在所有 notes off 紧急（panic）消息时调用
