

the volume does indeed change. Congrats on your first plug-in!

音量确实会发生变化。恭喜你完成了第一个插件！

What makes this plug-in so easy and quick to develop is that the slider volume control maps directly to a variable that is used in the processAudioFrame() function, as depicted in Figure 3.14. This means the data coming from the slider can be used directly in the algorithm. The data coming from the slider and controlling m_fVolume is said to be raw data. You use the raw value to affect the signal processing algorithm.

这个插件之所以如此容易和快速开发，是因为滑块音量控件直接映射到 processAudioFrame() 函数中使用的一个变量，如图 3.14 所示。这意味着来自滑块的数据可以直接在算法中使用。来自滑块并控制 m_fVolume 的数据被称为原始数据。你使用原始值来影响信号处理算法。

## 3.10 设计一个以分贝为单位的音量插件

This next example will show you how to cook your raw data to be used in the signal processing algorithm. The VolumedB plug-in will also be a volume control, but will operate in dB instead of using a raw multiplier. You may have noticed that your previous volume control didn't seem to do much in the upper half of the throw of the slider. This is because your ears hear logarithmically and so linear deflections of the slider do not correspond to linear changes in perceived loudness. To fix this, we'll design another plug-in that will operate in decibels (dB). The block diagram is identical to the first project, only the control range of values has changed.

下一个示例将向你展示如何处理原始数据以便在信号处理算法中使用。VolumedB 插件也将是一个音量控件，但将以分贝（dB）为单位运行，而不是使用原始乘数。你可能已经注意到，你之前的音量控件在滑块上半部分似乎没有太大作用。这是因为人耳是以对数方式听觉的，因此滑块的线性偏移并不对应于感知响度的线性变化。为了解决这个问题，我们将设计另一个以分贝（dB）为单位运行的插件。框图与第一个项目相同，只有控制值的范围发生了变化。

- a2 = -96 dB: Mute
- a2 = 0 dB: Max volume

- a2 = -96 dB：静音
- a2 = 0 dB：最大音量

Now, the volume control is specified in dB, so you need a formula to convert the dB value to a scalar multiplier for the algorithm. You should memorize the dB equations now if you haven't already, since they will reappear over and over in audio plug-ins. This is the cooking formula that will take the raw data from the slider –96 to 0 dB and cook it into a variable we can use in our scalar multiplication:

现在，音量控件以 dB 为单位指定，因此你需要一个公式将 dB 值转换为算法中的标量乘数。如果你还没有记住 dB 方程，现在应该记住，因为它们会在音频插件中反复出现。这是处理公式，它将滑块上的原始数据（–96 到 0 dB）转换为我们可以在标量乘法中使用的变量：

```
dB = 20log(x)
x = 10^(dB/20)
```

You set up the cooking formula by implementing the userInterfaceChange() function which is always called when the user changes anything on the control surface. When the user moves the slider, you cook the data. This is shown conceptually in Figure 3.15.

你通过实现 userInterfaceChange() 函数来设置处理公式，该函数在用户更改控制面板上的任何内容时始终会被调用。当用户移动滑块时，你处理数据。这在图 3.15 中以概念方式展示。

The cooking function simply converts the dB into a scalar multiplier. In this case, the cooking function is short enough to simply leave inside the userInterfaceChange() function; as the cooking functions become more complex, you will probably want to break them out into separate functions, which are called from userInterfaceChange(). Remember the two RackAFX rules you've learned so far:

处理函数只是将 dB 转换为标量乘数。在这种情况下，处理函数足够短，可以直接保留在 userInterfaceChange() 函数中；随着处理函数变得更加复杂，你可能希望将它们拆分为单独的函数，并从 userInterfaceChange() 调用它们。记住你迄今学到的两条 RackAFX 规则：

> Coefficients in a block diagram (or transfer function or algorithm) become float member variables in your plug-in code. Each slider or button control on the UI will map to and control a member variable in your plug-in.

> 框图（或传递函数或算法）中的系数将成为插件代码中的 float 成员变量。UI 上的每个滑块或按钮控件都将映射到并控制插件中的一个成员变量。

![](img/b54974d0a4317ec82d7ae02126d10a6f_67_0.png)

Figure 3.15: The volume-in-dB plug-in will have a single slider that generates values between –96 and 0.0 dB; you need to cook the raw dB values to use in your plug-in.

图 3.15：以分贝为单位的音量插件将有一个生成 –96 到 0.0 dB 之间值的单个滑块；你需要处理原始 dB 值以便在插件中使用。

In the first plug-in, the variable was shared between the slider and the algorithm. Now we need two variables, one for the raw slider data and the other for the cooked algorithm processing. We will name them as follows:

在第一个插件中，变量在滑块和算法之间共享。现在我们需要两个变量，一个用于原始滑块数据，另一个用于处理后的算法处理。我们将它们命名如下：

- m_fVolume_dB: The raw slider data
- m_fVolume: The cooked value used in the algorithm

- m_fVolume_dB：原始滑块数据
- m_fVolume：算法中使用的处理后的值

### 3.10.1 Project: VolumedB

### 3.10.1 项目：VolumedB

Using the same method as before, create a new project named “VolumedB.” As before, you don’t have to worry about the advanced options at the bottom of the new project window. Your compiler will automatically start.

使用与之前相同的方法，创建一个名为“VolumedB”的新项目。与之前一样，你不必担心新建项目窗口底部的高级选项。你的编译器将自动启动。

### 3.10.2 VolumedB GUI

### 3.10.2 VolumedB GUI

We only need a single slider control. It will be adjustable from –96 to 0 dB. Set up the GUI in RackAFX by choosing a slider and right-clicking inside the bounding box. Set the slider according to Table 3.1.

我们只需要一个单个滑块控件。它将可从 –96 调整到 0 dB。在 RackAFX 中通过选择滑块并在边界框内右键单击来设置 GUI。根据表 3.1 设置滑块。

### 3.10.3 VolumedB.h File

### 3.10.3 VolumedB.h 文件

RackAFX has written the code and declared the variable float m_fVolume_dB but we still need to declare our second variable named m_fVolume, which stores the cooked data. Open the VolumedB.h file and declare the variable in the user declarations area:

RackAFX 已编写代码并声明了变量 float m_fVolume_dB，但我们仍需要声明名为 m_fVolume 的第二个变量，用于存储处理后的数据。打开 VolumedB.h 文件并在用户声明区域声明该变量：

```
// abstract base class for DSP filters
class CVolumeDb : public CPlugIn
{
public: // plug-in API Functions

<SNIP SNIP SNIP>

// Add your code here: .................... //

// our Cooked Volume Multiplier
float m_fVolume;

// END OF USER CODE .................... //
```

Table 3.1: The slider properties for the VolumedB project.

表 3.1：VolumedB 项目的滑块属性。

| Slider Property | Value |
|---|---|
| Control name | Volume |
| Units | dB |
| Variable type | float |
| Variable name | m_fVolume_dB |
| Low limit | -96 |
| High limit | 0 |
| Initial value | -6 |

| 滑块属性 | 值 |
|---|---|
| 控件名称 | Volume |
| 单位 | dB |
| 变量类型 | float |
| 变量名 | m_fVolume_dB |
| 下限 | -96 |
| 上限 | 0 |
| 初始值 | -6 |

### 3.10.4 VolumedB.cpp File

### 3.10.4 VolumedB.cpp 文件

### Constructor

### 构造函数

- Cook and initialize the member variable.
- Use the pow() function.

- 处理并初始化成员变量。
- 使用 pow() 函数。

```
CVolumeDb::CVolumeDb()
{
    // Added by RackAFX - DO NOT REMOVE
    //
    // Setup the RackAFX UI Control List and Initialize Variables
    initUI();
    // END InitUI

    <SNIP SNIP SNIP>

    // Finish initializations here

    // Cook the raw data:
    m_fVolume = pow(10.0, m_fVolume_dB/20.0);
}
```

### prepareForPlay()

### prepareForPlay()

There is nothing to do here because the volume variable does not need to be reset on each play event.

这里无需做任何事情，因为音量变量不需要在每次播放事件时重置。

### userInterfaceChange()

### userInterfaceChange()

- Decode the control ID value.
- Cook the raw data using the formula.
- When the plug-ins get more complex, you can create separate cooking functions and then share the functions as needed.
- Make sure you check your control ID values from the comments so that they match properly.

- 解码控件 ID 值。
- 使用公式处理原始数据。
- 当插件变得更加复杂时，你可以创建单独的处理函数，然后根据需要共享这些函数。
- 确保你从注释中检查控件 ID 值，以便它们正确匹配。

```
bool __stdcall CVolumedB::userInterfaceChange(int nControlIndex)
{
    // decode the control index, or delete the switch and use brute force calls
    switch(nControlIndex)
    {
        case 0:
        {
            // Cook the raw data:
            m_fVolume = pow(10.0, m_fVolume_dB/20.0);
        }
        default:
            break;
    }

    return true;
}
```

### processAudioFrame()

### processAudioFrame()

- Implement the difference equation.

- 实现差分方程。

```
bool __stdcall CVolumedB::processAudioFrame(float* pInputBuffer, float* pOutputBuffer,
                                             UINT uNumInputChannels, UINT uNumOutputChannels)
{
    // output = input -- change this for meaningful processing
    //
    // Do LEFT (MONO) Channel; there is always at least one input/one output
    // (INSERT Effect)
    pOutputBuffer[0] = pInputBuffer[0]*m_fVolume;

    // Mono-In, Stereo-Out (AUX Effect)
    if(uNumInputChannels == 1 && uNumOutputChannels == 2)
        pOutputBuffer[1] = pInputBuffer[0]*m_fVolume;

    // Stereo-In, Stereo-Out (INSERT Effect)
    if(uNumInputChannels == 2 && uNumOutputChannels == 2)
        pOutputBuffer[1] = pInputBuffer[1]*m_fVolume;

    return true;
}
```

Build and test your plug-in. You should now hear a smooth volume transition as you move the slider. Depending on your sound system and volume levels, you might not hear much below –40 dB.

构建并测试你的插件。现在当你移动滑块时，应该能听到平滑的音量过渡。取决于你的音响系统和音量电平，你可能在 –40 dB 以下听不到太多声音。

## 3.11 设计一个高频音调控制插件

This example will show you how to implement the last of the digital signal processing (DSP) algorithm building blocks: the delay element (z^-N), where N is the number of samples of delay. In this example, N = 1, so we are dealing with a one-sample delay, a fundamental building block for many DSP algorithms. Although we won’t get to the theory of how this delay creates a tone control until the next chapter, it's worth it to go ahead and build a plug-in that uses it. After this exercise, you will be able to build almost any kind of DSP filter that uses one-sample-delay elements—and that's a lot of DSP filters. The later examples in the book will not be as detailed regarding the operation of RackAFX and your C++ compiler, so be sure you understand how to manipulate the software as needed to complete the project. Figure 3.16 shows the block diagram for the filter.

本示例将向你展示如何实现数字信号处理（DSP）算法构建块的最后一个：延迟元素（z^-N），其中 N 是延迟的样本数。在本示例中，N = 1，因此我们处理的是一个采样延迟，这是许多 DSP 算法的基本构建块。尽管我们要等到下一章才会了解这种延迟如何创建音调控制的理论，但现在先构建一个使用它的插件是值得的。完成此练习后，你将能够构建几乎任何使用单采样延迟元素的 DSP 滤波器——这涵盖了大量的 DSP 滤波器。书中后面的示例将不会对 RackAFX 和你的 C++ 编译器的操作进行那么详细的说明，因此请务必了解如何根据需要操作软件以完成项目。图 3.16 显示了滤波器的框图。

The design equation is as follows:

设计方程如下：

```
0.0 <= a1 <= 0.49
a0 = a1 - 1.0
(3.3)
```

![](img/b54974d0a4317ec82d7ae02126d10a6f_70_0.png)

Figure 3.16: The HF tone control block diagram.

图 3.16：高频音调控制框图。

You already know that the coefficients a0 and a1 will become float member variables in our plug-in. But what about the one-sample-delay element, z^-1? In hardware, this would be a register to store the sample for one clock period. In software, it simply becomes another float variable, but it must be able to persist over the lifetime of a processing cycle. Therefore, like the coefficients, it will become a float member variable of our plug-in object.

你已经知道系数 a0 和 a1 将成为我们插件中的 float 成员变量。但是单采样延迟元素 z^-1 呢？在硬件中，这将是一个用于存储一个时钟周期样本的寄存器。在软件中，它只是另一个 float 变量，但它必须能够在处理周期的整个生命周期内持续存在。因此，就像系数一样，它将成为我们插件对象的 float 成员变量。

You will do an example using arrays of floats in Chapter 7 when you implement digital delay lines that require long strings of z^-1 elements. For now, we need to implement the single z^-1 element in the block diagram. Right away, we need to decide if we are going to support multichannel (stereo) operation.

在第 7 章中，当你实现需要长串 z^-1 元素的数字延迟线时，你将使用 float 数组进行示例。目前，我们需要在框图中实现单个 z^-1 元素。我们需要立即决定是否支持多声道（立体声）操作。

The last rule is really important and it is easy to get into trouble if you do not follow it. Unless the algorithm specifically deals with multichannel data, you will need to implement a separate algorithm for each channel, which means having separate coefficient and data (z^-1) elements for each channel. Even if you might be able to share the coefficients, you can never share the delay elements. We will need to declare variables for the following:

最后一条规则非常重要，如果不遵循，很容易遇到麻烦。除非算法专门处理多声道数据，否则你需要为每个声道实现单独的算法，这意味着为每个声道拥有单独的系数和数据（z^-1）元素。即使你可能能够共享系数，也绝不能共享延迟元素。我们需要为以下内容声明变量：

- Left channel a0 and a1 variables
- Left channel z^-1 variable
- Right channel a0 and a1 variables
- Right channel z^-1 variable

- 左声道 a0 和 a1 变量
- 左声道 z^-1 变量
- 右声道 a0 和 a1 变量
- 右声道 z^-1 变量

Delay elements will become float member variables in your plug-in object. For single-delay elements, you can simply assign separate variables. For multiple-sample-delay elements you may also use float arrays to store the data.

延迟元素将成为你插件对象中的 float 成员变量。对于单延迟元素，你可以简单地分配单独的变量。对于多采样延迟元素，你也可以使用 float 数组来存储数据。

