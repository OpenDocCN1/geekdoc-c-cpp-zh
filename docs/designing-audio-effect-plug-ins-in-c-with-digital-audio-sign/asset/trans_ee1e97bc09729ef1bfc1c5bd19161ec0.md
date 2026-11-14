


![](img/b54974d0a4317ec82d7ae02126d10a6f_478_0.png)

### Figure A.1: VST兼容开关揭示了GUI的三个选项。

- Use RackAFX custom GUI: 如果你拥有适当版本的RackAFX，此按钮将被启用。选择此选项将允许你使用GUI设计器（附录B）创建的GUI被VST客户端使用。它的外观和工作方式将与你在RackAFX中创建的完全相同。你不需要为此选项提供任何额外代码。

- I will write my own GUI: 如果你具备相应技能，则可以勾选此框并编写自己的GUI。客户端将调用你插件上的一个方法来启动你的GUI。GUI的所有细节均由你负责，你必须提供代码并拥有必要的资源编辑器。

对于最后一个选项，首先在PlugIn.h文件中查找你需要重写的标志和三个方法。

```
// set this to TRUE if you have your own GUI to use; not for RackAFX GUIs
bool m_bUserCustomGUI;
```

首先，在构造函数中将m_bUserCustomGUI标志设置为"true"。这将告知客户端你拥有自己的GUI。接下来，重写以下三个方法：

```
// for user (NOT RackAFX) generated resources/GUIs
virtual void __stdcall showGUI(HWND hParentWnd);
virtual void __stdcall hideGUI(HWND hParentWnd);
virtual void __stdcall refreshGUI(HWND hParentWnd);
```

- 客户端调用showGUI()来显示它。
- 客户端调用hideGUI()来隐藏它。
- 客户端调用refreshGUI()来更新它。有关更新的更多信息，请参见附录B。

在三个方法中，参数是客户端的窗口句柄。你需要使用客户端的句柄作为父窗口来创建子窗口。如果你不明白这是什么意思，那么可能不应该使用此选项。

## A.2 封装你的RackAFX插件

你的RackAFX插件将在Windows（Visual Studio）或Mac（Xcode）上编译，因为它是纯C++，并添加了一些#define语句来分离Windows和Mac特定的组件。音频信号处理和GUI组件对象均使用C++完成，因此你的插件对象可以用一个外部C++对象进行封装，该对象将VST或AU客户端的函数调用转换为RackAFX函数调用。当你选择“Make VST Compatible”选项时，就会发生这种情况；当客户端请求VST对象时，它会接收到一个将你的插件作为成员对象嵌入其中的对象。包装对象随后将调用转发给你的插件，并将信息或音频数据返回给客户端，如图A.2所示。你的插件暴露一个公共方法接口（灰色框）。包装对象暴露其API特定方法（白色框），客户端调用这些方法。转换通常涉及一个简单的转发方法调用。有时，多个包装方法连接到单个插件方法。其他时候，包装方法只需要返回成功代码或特殊字符串，因此无需调用插件对象上的任何内容。

如果你想编写包装对象，这相当简单，如你将在A.3节中看到，我们将比较不同的API函数调用。然而，你需要多了解我们的GUI对象设计方式，以便你可以使用在RackAFX中设置的GUI控件。或者，你可以实现自己的方案。当你在RackAFX中设置一个控件时，你实际上是在创建一个新的C++对象，并将其添加到链表中。该链表是你CPlugIn类的一个成员，名为“m_UIControlList”。它包含一系列C++ CUICtrl对象。CUICtrl对象可以表示以下之一：

![](img/b54974d0a4317ec82d7ae02126d10a6f_479_0.png)

### Figure A.2: 包装对象暴露客户端特定接口，并路由插件之间的调用。

- 滑块
- 单选按钮组
- 计量表

解释的最简单方式是通过示例。查看任何插件的initUI()方法，你将看到GUI对象的实例化和初始化。以下是第一个项目中音量滑块代码的第一部分。高亮部分为粗体。请记住，绝不要手动编辑此代码。

```
m_fVolume = 0.750000;
CUICtrl u10;
u10.uControlType = FILTER_CONTROL_CONTINUOUSLY_VARIABLE;
u10.uControlID = 0;
u10.fUserDisplayDataLoLimit = 0.000000;
u10.fUserDisplayDataHiLimit = 1.000000;
u10.uUserDataType = floatData;
u10.fInitUserIntValue = 0;
u10.fInitUserFloatValue = 0.750000;
u10.fInitUserDoubleValue = 0;
u10.fInitUserUINTValue = 0;
u10.m_pUserCookedIntData = NULL;
u10.m_pUserCookedFloatData = &m_fVolume;
u10.m_pUserCookedDoubleData = NULL;
u10.m_pUserCookedUINTData = NULL;
u10.cControlUnits = "";
u10.cVariableName = "m_fVolume";
u10.cEnumeratedList = "SEL1,SEL2,SEL3";
u10.dPresetData[0] = 0.000000;
u10.dPresetData[1] <SNIP SNIP SNIP>
u10.cControlName = "Volume";
```

第一行初始化底层变量m_fVolume，就像你在创建滑块时设置的那样。控件类型是FILTER_CONTROL_CONTINUOUSLY_VARIABLE，这意味着一个连续控制器。uControlID为0——这是在控件被操作时传递给userInterfaceChange()的值。这种用于标识控件的“唯一ID”范式在其他插件API中也是通用的。与变量本身的连接是通过指针实现的。由于这是一个浮点变量，m_pUserCookedFloatData被设置为底层变量的地址。RackAFX就是通过这种方式为你操作它。当你封装插件时，也可以使用此方式来控制该变量。当然，你始终可以使用其他方案。单位变量编码了多个项目，在使用前需要去除空白字符（不过，不要在对象中更改其长度）。因此，你可以看到每个变量的基本要素：ID、最小值、最大值和初始值，以及名称和单位。这些在其他插件API中也同样适用。

> RackAFX会自动按类型对GUI组件对象进行排序。滑块和单选按钮组受VST和AU格式的默认GUI支持，但计量表不受支持。m_UIControlList定义在pluginconstants.h中，并暴露了几个可供你使用的方法：

```
int count(); // returns the total number of GUI objects
int countLegalVST(); // returns the number of legal VST Default GUI objects
CUICtrl* getAt(int nIndex); // returns a pointer to a GUI object at a list index
```

CPlugIn对象还有一些可供你使用的辅助函数。一旦你知道控件的ID值，就可以使用以下CPlugIn方法来访问这些对象：

```
void setParameter (UINT index, float value); // set a parameter 0 -> 1
float getParameter (UINT index); // get a parameter 0 -> 1
```

这两个方法非常重要，因为它们模拟了VST客户端通过默认界面获取或设置值的方式。*索引值是链表中的索引，而不是ID值。* 最后，对于Windows插件，你通常需要知道DLL所在目录的名称，以便处理预设或加载/保存自定义信息。CPlugIn暴露了一个方法供你使用来获取该文件夹名称。

```
char* getMyDLLDirectory(); // return the DLL's owning directory
```

## A.3 对象/方法/GUI比较

RackAFX、VST和AU有许多相似之处。首先，它们都要求你将插件派生自制造商指定的基类（或类）。它们还实现了你一直在编写的同一组基本功能。基类如表A.1所示。方法比较如表A.2所示。

### Table A.1: 实现功能的函数和方法比较。

| API | 基类(们) |
| :--- | :--- |
| RackAFX | CPlugIn |
| VST | AudioEffect, AudioEffectX |
| AU | AUBase, AUEffectBase, AUKernelBase |

### Table A.2: 实现功能的函数和方法比较。

| 函数 | RackAFX | VST | AU |
| :--- | :--- | :--- | :--- |
| 实例化 | CPlugIn() | AudioEffectX() | AUEffectBase()\nAUKernelBase() |
| 销毁 | ~CPlugIn() | ~AudioEffectX() | ~AUEffectBase()\n~AUKernelBase() |
| 初始化 | prepareForPlay() | resume() | Initialize() |
| 准备播放 | prepareForPlay() | setSampleRate()\nupdateSampleRate()\nresume() | N/A |
| 处理音频 | processAudioFrame() | processReplacing() | Process()\nProcessBufferList() |
| 获取UI控件值 | getParameter()\n(optional) | getParameter() | GetParameter() |
| 设置UI控件值 | userInterfaceChange()\n(optional) | setParameter() | SetParameter() |
| 更新GUI (see | | | |

