

## 输入扩散

| Slider Property | Value |
|---|---|
| Control Name | 带宽 |
| Units | |
| Variable Type | float |
| Variable Name | m_fInputLPF_g |
| Low Limit | 0 |
| High Limit | 1 |
| Initial Value | 0.45 |

| Slider Property | Value |
|---|---|
| Control Name | APF1 延迟 |
| Units | mSec |
| Variable Type | float |
| Variable Name | m_fAPF_1_Delay_mSec |
| Low Limit | 0 |
| High Limit | 100 |
| Initial Value | 13.28 |

| Slider Property | Value |
|---|---|
| Control Name | APF1 增益 |
| Units | |
| Variable Type | float |
| Variable Name | m_fAPF_1_g |
| Low Limit | -1 |
| High Limit | 1 |
| Initial Value | 0.7 |

| Slider Property | Value |
|---|---|
| Control Name | APF2 延迟 |
| Units | mSec |
| Variable Type | float |
| Variable Name | m_fAPF_2_Delay_mSec |
| Low Limit | 0 |
| High Limit | 100 |
| Initial Value | 28.13 |

## 并行梳状滤波器组 1

| Slider Property | Value |
|---|---|
| Control Name | PComb1 延迟 |
| Units | mSec |
| Variable Type | float |
| Variable Name | m_fPComb_1_Delay_mSec |
| Low Limit | 0 |
| High Limit | 100 |
| Initial Value | 31.71 |

| Slider Property | Value |
|---|---|
| Control Name | PComb2 延迟 |
| Units | mSec |
| Variable Type | float |
| Variable Name | m_fPComb_2_Delay_mSec |
| Low Limit | 0 |
| High Limit | 100 |
| Initial Value | 37.11 |

| Slider Property | Value |
|---|---|
| Control Name | PComb3 延迟 |
| Units | mSec |
| Variable Type | float |
| Variable Name | m_fPComb_3_Delay_mSec |
| Low Limit | 0 |
| High Limit | 100 |
| Initial Value | 40.23 |

| Slider Property | Value |
|---|---|
| Control Name | PComb4 延迟 |
| Units | mSec |
| Variable Type | float |
| Variable Name | m_fPComb_4_Delay_mSec |
| Low Limit | 0 |
| High Limit | 100 |
| Initial Value | 44.14 |

## 并行梳状滤波器组 2

| Slider Property | Value |
|---|---|
| Control Name | PComb5 延迟 |
| Units | mSec |
| Variable Type | float |
| Variable Name | m_fPComb_5_Delay_mSec |
| Low Limit | 0 |
| High Limit | 100 |
| Initial Value | 30.47 |

| Slider Property | Value |
|---|---|
| Control Name | PComb6 延迟 |
| Units | mSec |
| Variable Type | float |
| Variable Name | m_fPComb_6_Delay_mSec |
| Low Limit | 0 |
| High Limit | 100 |
| Initial Value | 33.98 |

| Slider Property | Value |
|---|---|
| Control Name | PComb7 延迟 |
| Units | mSec |
| Variable Type | float |
| Variable Name | m_fPComb_7_Delay_mSec |
| Low Limit | 0 |
| High Limit | 100 |
| Initial Value | 41.41 |

| Slider Property | Value |
|---|---|
| Control Name | PComb8 延迟 |
| Units | mSec |
| Variable Type | float |
| Variable Name | m_fPComb_8_Delay_mSec |
| Low Limit | 0 |
| High Limit | 100 |
| Initial Value | 42.58 |

## 输入扩散与阻尼

| Slider Property | Value |
|---|---|
| Control Name | 阻尼 |
| Units | |
| Variable Type | float |
| Variable Name | m_fLPF2_g2 |
| Low Limit | 0 |
| High Limit | 1 |
| Initial Value | 0.5 |

| Slider Property | Value |
|---|---|
| Control Name | APF3 延迟 |
| Units | mSec |
| Variable Type | float |
| Variable Name | m_fAPF_3_Delay_mSec |
| Low Limit | 0 |
| High Limit | 100 |
| Initial Value | 9.38 |

| Slider Property | Value |
|---|---|
| Control Name | APF3 增益 |
| Units | |
| Variable Type | float |
| Variable Name | m_fAPF_3_g |
| Low Limit | -1 |
| High Limit | 1 |
| Initial Value | -0.6 |

| Slider Property | Value |
|---|---|
| Control Name | APF4 延迟 |
| Units | mSec |
| Variable Type | float |
| Variable Name | m_fAPF_4_Delay_mSec |
| Low Limit | 0 |
| High Limit | 100 |
| Initial Value | 11 |

| Slider Property | Value |
|---|---|
| Control Name | APF4 增益 |
| Units | |
| Variable Type | float |
| Variable Name | m_fAPF_4_g |
| Low Limit | -1 |
| High Limit | 1 |
| Initial Value | 0.6 |

## 混响输出

| Slider Property | Value |
|---|---|
| Control Name | 混响时间 |
| Units | mSec |
| Variable Type | float |
| Variable Name | m_fRT60 |
| Low Limit | 0 |
| High Limit | 5000 |
| Initial Value | 1000 |

| Slider Property | Value |
|---|---|
| Control Name | 湿/干 |
| Units | % |
| Variable Type | float |
| Variable Name | m_fWet_pct |
| Low Limit | 0 |
| High Limit | 100 |
| Initial Value | 50 |

使用上面的控件列表构建 UI；我在项目中使用的变量名已在表中列出。你可以使用自己的变量名，但需要确保它们正确实现。图 11.46 显示了我的 GUI；我按照算法框图将控件组合在一起。

## 11.17.3 Reverb.h

在 .h 文件中，声明成员对象以及一个一次性更改所有模块的烹饪函数（它并不精简，但一次性全部烹饪很简单）。算法中的每个块都有一个现成对象。

![](img/b54974d0a4317ec82d7ae02126d10a6f_385_0.png)

图 11.46：完成的混响原型 GUI。

```
// Add your code here: ------------------------------------ //
//
// Pre-Delay Block
CDelay m_PreDelay;

// input Diffusion
COnePoleLPF m_InputLPF;
CDelayAPF m_InputAPF_1;
CDelayAPF m_InputAPF_2;

// parallel Comb Bank 1
CCombFilter m_Parallel1CF_1;
CCombFilter m_Parallel1CF_2;
CLPFBCombFilter m_Parallel1CF_3;
CLPFBCombFilter m_Parallel1CF_4;

// parallel Comb Bank 2
CCombFilter m_Parallel2CF_5;
CCombFilter m_Parallel2CF_6;
CLPFBCombFilter m_Parallel2CF_7;
CLPFBCombFilter m_Parallel2CF_8;

// damping
COnePoleLPF m_DampingLPF1;
COnePoleLPF m_DampingLPF2;

// output diffusion
CDelayAPF m_OutputAPF_3;
CDelayAPF m_OutputAPF_4;

// function to cook all member object's variables at once
void cookVariables();

// END OF USER CODE ------------------------------------ //
```

## 11.17.4 Reverb.cpp

编写唯一的额外函数 cookVariables()：

```
// function to cook all variables at once
void CReverb::cookVariables()
{
    // Pre-Delay
    m_PreDelay.setDelay_mSec(m_fPreDelay_mSec);
    m_PreDelay.setOutputAttenuation_dB(m_fPreDelayAtten_dB);

    // input diffusion
    m_InputAPF_1.setDelay_mSec(m_fAPF_1_Delay_mSec);
    m_InputAPF_1.setAPF_g(m_fAPF_1_g);
    m_InputAPF_2.setDelay_mSec(m_fAPF_2_Delay_mSec);
    m_InputAPF_2.setAPF_g(m_fAPF_2_g);

    // Output diffusion
    m_OutputAPF_3.setDelay_mSec(m_fAPF_3_Delay_mSec);
    m_OutputAPF_3.setAPF_g(m_fAPF_3_g);

    m_OutputAPF_4.setDelay_mSec(m_fAPF_4_Delay_mSec);
    m_OutputAPF_4.setAPF_g(m_fAPF_4_g);

    // comb filters
    // set delays first...
    m_Parallel1CF_1.setDelay_mSec(m_fPComb_1_Delay_mSec);
    m_Parallel1CF_2.setDelay_mSec(m_fPComb_2_Delay_mSec);
    m_Parallel1CF_3.setDelay_mSec(m_fPComb_3_Delay_mSec);
    m_Parallel1CF_4.setDelay_mSec(m_fPComb_4_Delay_mSec);
    m_Parallel2CF_5.setDelay_mSec(m_fPComb_5_Delay_mSec);
    m_Parallel2CF_6.setDelay_mSec(m_fPComb_6_Delay_mSec);
    m_Parallel2CF_7.setDelay_mSec(m_fPComb_7_Delay_mSec);
    m_Parallel2CF_8.setDelay_mSec(m_fPComb_8_Delay_mSec);

    // ...then calculate comb g's from RT60:
    m_Parallel1CF_1.setComb_g_with_RT60(m_fRT60);
    m_Parallel1CF_2.setComb_g_with_RT60(m_fRT60);
    m_Parallel1CF_3.setComb_g_with_RT60(m_fRT60);
    m_Parallel1CF_4.setComb_g_with_RT60(m_fRT60);
    m_Parallel2CF_5.setComb_g_with_RT60(m_fRT60);
    m_Parallel2CF_6.setComb_g_with_RT60(m_fRT60);
    m_Parallel2CF_7.setComb_g_with_RT60(m_fRT60);
    m_Parallel2CF_8.setComb_g_with_RT60(m_fRT60);

    // LPFs
    m_DampingLPF1.setLPF_g(m_fLPF2_g2);
    m_DampingLPF2.setLPF_g(m_fLPF2_g2);
    m_InputLPF.setLPF_g(m_fInputLPF_g);

    // LPF-comb filters
    m_Parallel1CF_3.setLPF_g(m_fLPF2_g2);
    m_Parallel1CF_4.setLPF_g(m_fLPF2_g2);
    m_Parallel2CF_7.setLPF_g(m_fLPF2_g2);
    m_Parallel2CF_8.setLPF_g(m_fLPF2_g2);
}
```

## 构造函数

这里无需操作，因为子对象构造函数会处理这些细节。

## prepareForPlay()

- 使用最大延迟时间初始化所有对象；除预延迟外，所有延迟时间的最大值均为 100 mSec。
- 将预延迟初始化为其最大值 2 秒。
- 重置所有延迟。
- 为延迟设置采样率。
- 一次性烹饪所有变量。
- 初始化延迟以刷新缓冲区。

