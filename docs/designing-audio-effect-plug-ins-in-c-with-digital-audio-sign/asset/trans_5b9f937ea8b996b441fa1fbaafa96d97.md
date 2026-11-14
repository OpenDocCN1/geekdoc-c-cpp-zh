

我们应该先编写一个可用于较大父插件对象的模块。图 10.11 显示了框图。

我们将提供多个用户界面（UI）组件来控制插件，它们的变量也可供父插件使用。我们将使用现有的 DDL 模块和波表振荡器插件。由于 DDL 模块具有反馈路径控制，因此有许多方法可以将这些模块组合成复杂的单元。我们将为用户提供的控件将在下一节讨论。操作计划如下：

- LFO：需要设置为单极性运行，并使用非带限表。
- 合唱延迟偏移控件将有效地移动调制延迟的操作中心。
- 颤音模式将强制反馈值为 0.0%，因为带反馈时听起来不好。

- prepareForPlay()
  - 重置 LFO 并通过设置 m_bNoteOn 标志启动它；还要设置 LFO 和 DDL 模块。
  - 设置 DDL m_nSampleRate 变量；它需要此值来正确初始化其缓冲区。
  - 将 prepareForPlay() 调用转发给子对象 LFO 和 DDL。

![](img/b54974d0a4317ec82d7ae02126d10a6f_319_0.png)

Figure 10.11: 通用调制延迟框图；它可以是任何类型的 flanger/颤音/合唱。

- processAudioFrame()
  - 在 LFO 上调用 doOscillate() 函数。
  - 使用 LFO 值为 DDL 模块计算毫秒级的延迟偏移量。
  - 将新的延迟时间写入 DDL 模块并调用其烹饪函数。
  - 在 DDL 模块上调用 processAudioFrame() 以获取当前输出样本。

- userInterfaceChange()
  - 调用 LFO 和 DDL 的更新函数。
  - 调用类型切换函数以在 flanger、颤音和合唱之间切换。

我们将继续规划一些辅助函数，以简化此过程。这不会是最精简或最高效的代码，但一旦你掌握了它，随时可以回头改进。虽然这是一个困难的项目，但你只需要两个成员变量和四个函数即可完成设计。

成员对象如下：

```cpp
CWTOscillator m_LFO;    // our LFO
CDDLModule m_DDL;       // our delay line module
```

成员变量如下：

```cpp
float m_fMinDelay_mSec; // min delay time
float m_fMaxDelay_mSec; // max delay time
```

成员函数如下：

```cpp
float updateLFO();      // change/set the type and rate
float updateDDL();      // change/set the wet/dry and feedback
float cookModType();    // set up the min/max delay times
float calculateDelayOffset(float fLFOSample); // convert the LFO to a delay value
```

## 10.3.1 项目：ModDelayModule

启动一个新项目，并确保包含您的 WTOScillator 和 DDLModule 对象（图 10.12）。

![](img/b54974d0a4317ec82d7ae02126d10a6f_320_0.png)

Figure 10.12: ModDelayModule 的项目设置。

表 10.2: GUI 组件、变量名和值。

| 滑块属性 | 值 |
|---|---|
| 控件名称 | 深度 |
| 单位 | % |
| 变量类型 | float |
| 变量名 | m_fModDepth_pct |
| 下限 | 0 |
| 上限 | 100 |
| 初始值 | 50 |

| 滑块属性 | 值 |
|---|---|
| 控件名称 | 速率 |
| 单位 | Hz |
| 变量类型 | float |
| 变量名 | m_fModFrequency_Hz |
| 下限 | 0.02 |
| 上限 | 5 |
| 初始值 | 0.18 |

| 滑块属性 | 值 |
|---|---|
| 控件名称 | 反馈 |
| 单位 | % |
| 变量类型 | float |
| 变量名 | m_fFeedback_pct |
| 下限 | -100 |
| 上限 | 100 |
| 初始值 | 0 |

| 滑块属性 | 值 |
|---|---|
| 控件名称 | 合唱偏移 |
| 单位 | 毫秒 |
| 变量类型 | float |
| 变量名 | m_fChorusOffset |
| 下限 | 0 |
| 上限 | 30 |
| 初始值 | 0 |

| 按钮属性 | 值 |
|---|---|
| 控件名称 | 调制类型 |
| 单位 | |
| 变量类型 | 枚举 |
| 变量名 | m_uModType |
| 枚举字符串 | Flanger, Vibrato, Chorus |

| 按钮属性 | 值 |
|---|---|
| 控件名称 | LFO |
| 单位 | |
| 变量类型 | 枚举 |
| 变量名 | m_uLFOType |
| 枚举字符串 | tri, sin |

使用表 10.2 在 RackAFX 中设置图形用户界面（GUI）。

## 10.3.3 ModDelayModule.h 文件

将成员对象、变量和函数声明添加到 .h 文件中：

```cpp
// Add your code here: ------------------------------------------------------ //
CWTOscillator m_LFO; // our LFO
CDDLModule m_DDL; // our delay line module

// these will depend on the type of mod
float m_fMinDelay_mSec;
float m_fMaxDelay_mSec;

// functions to update the member objects
void updateLFO();
void updateDDL();

// cooking function for mod type
void cookModType();

// convert a LFO value to a delay offset value
float calculateDelayOffset(float fLFOSample);

// END OF USER CODE ------------------------------------------------------- //
```

## 10.3.4 ModDelayModule.cpp 文件

### 构造函数

- 初始化所有变量。

```cpp
CModDelayModule::CModDelayModule()
{
	<SNIP SNIP SNIP>

	// Finish initializations here
	m_fMinDelay_mSec = 0.0;
	m_fMaxDelay_mSec = 0.0;
	m_fChorusOffset = 0.0;

	m_LFO.m_fFrequency_Hz = 0;
	m_LFO.m_uOscType = m_uLFOType; // triangle enum(tri,sin);

	m_DDL.m_bUseExternalFeedback = false;
	m_DDL.m_fDelay_ms = 0;
}
```

编写 update() 函数：

```cpp
// LFO function to set:
// - the LFO Frequency
// - the oscillator type
void CModDelayModule::updateLFO()
{
    // set raw data
    m_LFO.m_fFrequency_Hz = m_fModFrequency_Hz;
    m_LFO.m_uOscType = m_uLFOType;

    // cook it
    m_LFO.cookFrequency();
}

// DDL function to set:
// - the DDL Feedback amount (disabled for Vibrato)
void CModDelayModule::updateDDL()
{
    // test and set if needed
    //if(m_uModType != Vibrato)
    m_DDL.m_fFeedback_pct = m_fFeedback_pct;

    // cook it
    m_DDL.cookVariables();
}
```

使用表 10.3 中的信息编写 cookModType() 函数——当用户更改效果类型时会调用此方法。

| 效果 | 最小延迟 (mSec) | 最大延迟 (mSec) | 湿/干比 (%) | 反馈 (%) |
|---|---|---|---|---|
| Vibrato | 0 | 7-10 | 50/50 | -100 到 +100 |
| Chorus | 5 | 20-40 | 50/50 | -100 到 +100 |

```cpp
void CModDelayModule::cookModType()
{
    switch(m_uModType)
    {
        case Flanger:
        {
            m_fMinDelay_mSec = 0;
            m_fMaxDelay_mSec = 7;
            m_DDL.m_fWetLevel_pct = 50.0;
            m_DDL.m_fFeedback_pct = m_fFeedback_pct;
            break;
        }
        case Vibrato:
        {
            m_fMinDelay_mSec = 0;
            m_fMaxDelay_mSec = 7;
            m_DDL.m_fWetLevel_pct = 100.0;
            m_DDL.m_fFeedback_pct = 0.0; // NOTE! no FB for vibrato
        }
        case Chorus:
        {
            m_fMinDelay_mSec = 5;
            m_fMaxDelay_mSec = 30;
            m_DDL.m_fWetLevel_pct = 50.0;
            m_DDL.m_fInputAttenuation = 1.0;
            break;
        }
        default: // is Flanger
        {
            m_fMinDelay_mSec = 0;
            m_fMaxDelay_mSec = 7;
            m_DDL.m_fWetLevel_pct = 50.0;
            m_DDL.m_fFeedback_pct = m_fFeedback_pct;
            break;
        }
    }
}
```

表 10.3: 各种效果的默认延迟线设置。

| | 最小延迟 (mSec) | 最大延迟 (mSec) | 湿/干比 (%) | 反馈 (%) |
|---|---|---|---|---|
| Flanger | 0 | 7-10 | 50/50 | -100 到 +100 |
| Vibrato | 0 | 7-10 | 100/0 | 0 |
| Chorus | 7 | 20-40 | 50/50 | 通常为 0 |

编写 calculateDelayOffset() 函数。它通过获取 0 到 1.0 之间的 LFO 值，并将其映射到最小到最大延迟范围来工作。然后，该值由深度百分比值缩放，以便在 100% 时使用最大范围。对于合唱效果，我们通过在最小值上添加延迟偏移量，然后将其作为计算中的起始（参考）点，从而有效地移动操作范围和合唱中心。

```cpp
// calculateDelayOffset():
/*
 fLFOSample: a value from 0.0 to 1.0 from the LFO object

 returns: the calculated delay time in mSec for each effect

 NOTES: - the range for the flanger/vibrato is simply mapped from min to max
         starting at min: fLFOSample*(m_fMaxDelay_mSec - m_fMinDelay_mSec) +
         m_fMinDelay_mSec
     
     - the range for the Chorus includes the starting offset
        fStart = m_fMinDelay_mSec + m_fChorusOffset;
*/
if(m_uModType == Flanger || m_uModType == Vibrato)
{
  // flanger 0-1 gets mapped to 0->maxdelay
  return (m_fModDepth_pct/100.0)*(fLFOSample*(m_fMaxDelay_mSec -
  m_fMinDelay_mSec)) + m_fMinDelay_mSec;
}
else if(m_uModType == Chorus)
{
  // chorus adds starting offset to move delay range
  float fStart = m_fMinDelay_mSec + m_fChorusOffset;
  return (m_fModDepth_pct/100.0)*(fLFOSample*(m_fMaxDelay_mSec -
  m_fMinDelay_mSec)) + fStart;
}
```

## 10.3.5 PrepareForPlay()

- 转发对成员对象的 prepareForPlay() 调用。
- 以单极性模式重置并启动 LFO。

