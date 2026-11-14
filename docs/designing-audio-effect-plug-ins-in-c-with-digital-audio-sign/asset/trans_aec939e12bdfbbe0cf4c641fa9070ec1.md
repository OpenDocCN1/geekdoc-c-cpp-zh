

```
// ADDED BY RACKAFX -- DO NOT EDIT THIS CODE!!! ......... //
// **--0x07DFD--** //

float m_fDelay_ms;
float m_fFeedback_pct;
float m_fWetLevel_pct;

// **--0x1a7F--** ......... //
```

## 7.6.4 StereoDelay.cpp 文件

编写 setDelayVariables() 函数。布尔标志允许您可选地对成员调用烹饪函数：

```
void CStereoDelay::setDelayVariables(bool bCook)
{
    // forward our variables over to the member objects
    m_DDL_Left.m_fDelay_ms = m_fDelay_ms;
    m_DDL_Right.m_fDelay_ms = m_fDelay_ms;

    m_DDL_Left.m_fFeedback_pct = m_fFeedback_pct;
    m_DDL_Right.m_fFeedback_pct = m_fFeedback_pct;

    m_DDL_Left.m_fWetLevel_pct = m_fWetLevel_pct;
    m_DDL_Right.m_fWetLevel_pct = m_fWetLevel_pct;

    // cook, if desired
    if(bCook)
    {
        m_DDL_Left.cookVariables();
        m_DDL_Right.cookVariables();
    }
}
```

### 构造函数

- 初始化延迟变量并对其进行烹饪；此版本不使用外部反馈选项，因此相应地设置布尔值。

```
CStereoDelay::CStereoDelay()
{
    <SNIP SNIP SNIP>

    // Finish initializations here
    m_DDL_Left.m_bUseExternalFeedback = false;
    m_DDL_Right.m_bUseExternalFeedback = false;

    // set and (true) cook the delays
    setDelayVariables(true);
}
```

### prepareForPlay()

- 设置延迟变量。
- 将对成员对象的 prepareForPlay() 调用转发过去，它们将对其进行烹饪。

DDL 模块将处理刷新缓冲区等等。

```
bool __stdcall CStereoDelay::prepareForPlay()
{
    setDelayVariables(false);

    m_DDL_Left.prepareForPlay();
    m_DDL_Right.prepareForPlay();

    return true;
}
```

### userInterfaceChange()

- 当我们的任何控件更改时，设置延迟变量并对其进行烹饪。这可以简化以提高效率。

```
bool __stdcall CStereoDelay::userInterfaceChange(int nControlIndex)
{
    // set and cook the variables
    setDelayVariables(true);

    return true;
}
```

### processAudioFrame()

- 将 processAudioFrame() 调用转发给成员对象。
- 请记住，我们需要一次只发送一个通道，并确保是正确的通道。
- 注意“取地址”运算符 (&) 以指向我们传递给它的单个内存位置。

```
bool __stdcall CStereoDelay::processAudioFrame(float* pInputBuffer, float* pOutputBuffer, UINT uNumInputChannels, UINT uNumOutputChannels)
{
    // Do LEFT (MONO) Channel; there is always at least one input/one output
    // forward call to sub-object: pinput, poutput, 1 input ch, 1 output ch
    m_DDL_Left.processAudioFrame(&pInputBuffer[0], &pOutputBuffer[0], 1, 1);

    // Mono-In, Stereo-Out (AUX Effect)
    if((uNumInputChannels == 1 && uNumOutputChannels == 2))
        pOutputBuffer[1] = pOutputBuffer[0]; // just copy

    // Stereo-In, Stereo-Out (INSERT Effect)
    if((uNumInputChannels == 2 && uNumOutputChannels == 2))
        // forward call to sub-object: pinput, poutput, 1 input ch, 1 output ch
        m_DDL_Right.processAudioFrame(&pInputBuffer[1], &pOutputBuffer[1], 1, 1);

    return true;
}
```

重新生成并测试项目，您现在就有了之前项目的立体声版本。希望您对创建可组合的模块有多么强大有了更好的认识，尽管在模块上需要做一些额外工作，因为您需要提前思考并实现独立（简单）插件操作不需要的函数或变量。接下来，我们将通过将此插件转换为交叉反馈延迟来练习该模块。我们将以特定方式进行此操作，以便以后可以使用枚举变量在正常和交叉反馈操作之间切换。

## 7.7 设计立体声交叉反馈延迟插件

交叉反馈延迟是通过交叉两条延迟线的反馈路径实现的。我们将此功能添加到现有的 StereoDelay 项目中。这就是我们将使用构建到模块中的外部反馈选项的地方。在图 7.31 中，您可以追踪反馈路径，看看它们是如何交叉到相反的延迟线中的。您会惊讶于将延迟转换为交叉反馈延迟是多么容易：

- 使用布尔标志启用外部反馈功能。
- 使用 getCurrentFeedbackOutput() 和 setCurrentFeedbackInput() 函数“交叉反馈路径的光束”。

![](img/b54974d0a4317ec82d7ae02126d10a6f_236_0.png)

图 7.31：交叉反馈延迟的框图。

## 7.8 枚举滑块变量

您可以从图 7.31 中看到，GUI 中有一个新的滑块控件，用于在正常和交叉反馈操作之间选择。您可以利用 RackAFX 的枚举 UINT 变量来制作一个在多个枚举值之间选择的滑块，就像多位开关一样。在我们的情况中，目前只有两个位置：正常和交叉。

右键单击滑块以打开属性对话框，并添加一个新的滑块/变量组合，如图 7.32 所示。为数据类型选择“enum”，并创建一个名为 m_uDelayType 的变量——该变量将是无符号整数类型（UINT）。低、高和初始值单元格将不再可编辑；RackAFX 将根据您在枚举变量框中键入的内容自行确定它们。您用逗号分隔键入值。第一个值将是默认值。

在底部的框中，键入将在滑块控件中显示的字符串（保持简短）；您可以拥有任意数量的枚举变量，但在此情况下，我们只需要 NORM 和 CROSS。转到插件的 .h 文件以查看新变量：

![](img/b54974d0a4317ec82d7ae02126d10a6f_237_0.png)

### 图 7.32：枚举 UINT 数据类型。

```
// ADDED BY RACKAFX -- DO NOT EDIT THIS CODE!!!
// *** -0x07FD- ***

float m_fDelay_ms;
float m_fFeedback_pct;
float m_fWetLevel_pct;
UINT m_uDelayType;
enum (NORM,CROSS);
// *** -0x1A7F- ***
```

对于枚举变量，列表中的第一个将是默认值，滑块在底部。当您向上移动滑块时，其他字符串将按顺序出现。UINT 将自动更新。我们可以将其用作直接控制变量，因此在 userInterfaceChange() 中无需添加任何内容。进行下面讨论的编辑。

### 7.8.1 构造函数

- 将延迟类型初始化为 NORM。

```
CStereoDelay::CStereoDelay()
{
	<SNIP SNIP SNIP>

	// Finish initializations here
	m_DDL_Left.m_bUseExternalFeedback = false;
	m_DDL_Right.m_bUseExternalFeedback = false;

	// set and (true) cook the delays
	setDelayVariables(true);

	// init the delay type
	m_uDelayType = NORM;
}
```

### 7.8.2 PrepareForPlay()

无需操作；我们不关心处于什么模式，也不希望每次用户播放音频时都重置模式。

### 7.8.3 UserInterfaceChange()

无需操作；我们将其用作直接控制变量。

### 7.8.4 ProcessAudioFrame()

- 在 switch/case 语句中使用枚举变量按需修改反馈。对于 CROSS 操作：
  - 将外部反馈标志设置为 true。
  - 获取左反馈输出并将其写入右反馈输入。
  - 获取右反馈输出并将其写入左反馈输入。
- 在 DDL 模块上调用 processAudioFrame() 函数。

```
bool __stdcall CStereoDelay::processAudioFrame(float* pInputBuffer, float* pOutputBuffer, UINT uNumInputChannels, UINT uNumOutputChannels)
{

	switch(m_uDelayType)
	{
	case CROSS:
		// CROSS FB DELAY --- NOTE: MUST HAVE STEREO FILE! ----------- //
		m_DDL_Left.m_bUseExternalFeedback = true;
		m_DDL_Right.m_bUseExternalFeedback = true;

		// cross the Feedbacks
		m_DDL_Left.setCurrentFeedbackInput(m_DDL_Right.getCurrentFeedbackOutput());
		m_DDL_Right.setCurrentFeedbackInput(m_DDL_Left.getCurrentFeedbackOutput());
		break;

	case NORM: // clear the flags
		m_DDL_Left.m_bUseExternalFeedback = false;
		m_DDL_Right.m_bUseExternalFeedback = false;
		break;

	default: // default is NORM operation; clear the flags
		m_DDL_Left.m_bUseExternalFeedback = false;
		m_DDL_Right.m_bUseExternalFeedback = false;
		break;
	}

	// SHARED CODE ------------------------------------------ //
	// Do LEFT (MONO) Channel; there is always at least one input/one output
	// forward call to sub-object: pinput, poutput, 1 input ch, 1 output ch
	m_DDL_Left.processAudioFrame(&pInputBuffer[0], &pOutputBuffer[0], 1, 1);

	// Mono-In, Stereo-Out (AUX Effect)
	if(uNumInputChannels == 1 && uNumOutputChannels == 2)
		pOutputBuffer[1] = pOutputBuffer[0]; // just copy

	// Stereo-In, Stereo-Out (INSERT Effect)
	if(uNumInputChannels == 2 && uNumOutputChannels == 2)
		// forward call to sub-object pinput, poutput, 1 input ch, 1 output ch
		m_DDL_Right.processAudioFrame(&pInputBuffer[1], &pOutputBuffer[1], 1, 1);

	return true;
}
```

重新生成并测试插件；也要练习新的延迟类型控件。

回顾您学到的一些内容：

- 将延迟线声明为循环缓冲区、刷新和操作。
- 使用插值实现分数延迟时间。
- 将插件用作父插件的子模块。
- 如何添加枚举 UINT 变量用于类型选择，或将滑块用作多极开关。

## 7.9 更多延迟算法

以下是一些更复杂的 DDL 模块和其他延迟插件的想法。

