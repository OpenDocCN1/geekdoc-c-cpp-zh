

processAudioFrame() 仅用于左声道。几乎所有内容都为四相输出复制了一份。当然，你可以深入代码并精简它以提高效率，但你可以在这里清楚地看到两个输出的操作。将加粗的内容添加到你从 processAudioFrame() 复制的代码中：

```
void CWTOscillator::doOscillate(float* pYn, float* pYqn)
{
    // IMPORTANT: for future modules, bail out if no note-on event!
    if(!m_bNoteOn)
    {
        *pYn = 0.0;
        *pYqn = 0.0;
        return;
    }
    // our output value for this cycle
    float fOutSample = 0;
    float fQuadPhaseOutSample = 0;

    // get INT part
    int nReadIndex = (int)m_fReadIndex;
    int nQuadPhaseReadIndex = (int)m_fQuadPhaseReadIndex;

    // get FRAC part - NOTE no Quad Phase frac is needed because it will be the same!
    float fFrac = m_fReadIndex - nReadIndex;

    // setup second index for interpolation: wrap the buffer if needed
    int nReadIndexNext = nReadIndex + 1 > 1023 ? 0 : nReadIndex + 1;
    int nQuadPhaseReadIndexNext = nQuadPhaseReadIndex + 1 > 1023 ? 0 : nQuadPhaseReadIndex + 1;

    // interpolate the output
    switch(m_uOscType)
    {
        case sine:
            fOutSample = dLinTerp(0, 1, m_SinArray[nReadIndex],
                                  m_SinArray[nReadIndexNext], fFrac);
            fQuadPhaseOutSample = dLinTerp(0, 1,
                                           m_SinArray[nQuadPhaseReadIndex],
                                           m_SinArray[nQuadPhaseReadIndexNext], fFrac);
            break;

        case saw:
            if(m_uTableMode == normal) // normal
            {
                fOutSample = dLinTerp(0, 1, m_SawtoothArray[nReadIndex],
                                      m_SawtoothArray[nReadIndexNext], fFrac);
                fQuadPhaseOutSample = dLinTerp(0, 1,
                                               m_SawtoothArray[nQuadPhaseReadIndex],
                                               m_SawtoothArray[nQuadPhaseReadIndexNext], fFrac);
            }
            else // bandlimited
            {
                fOutSample = dLinTerp(0, 1,
                                      m_SawtoothArray_BL5[nReadIndex],
                                      m_SawtoothArray_BL5[nReadIndexNext], fFrac);
                fQuadPhaseOutSample = dLinTerp(0, 1,
                                               m_SawtoothArray_BL5[nQuadPhaseReadIndex],
                                               m_SawtoothArray_BL5[nQuadPhaseReadIndexNext],
                                               fFrac);
            }
            break;

        case tri:
            // ETC.. FOLLOW THE SAME LOGIC AS THE OTHER TABLES //

        case SQUARE:
            // ETC... FOLLOW THE SAME LOGIC AS THE OTHER TABLES //
            // always need a default
        default:
            fOutSample = dLinTerp(0, 1, m_SinArray[nReadIndex],
                                  m_SinArray[nReadIndexNext], fFrac);
            fQuadPhaseOutSample = dLinTerp(0, 1,
                                           m_SinArray[nQuadPhaseReadIndex],
                                           m_SinArray[nQuadPhaseReadIndexNext], fFrac);
            break;
    }

    // add the increment for next time
    m_fReadIndex += m_f_inc;
    m_fQuadPhaseReadIndex += m_f_inc;

    // check for wrap
    if(m_fReadIndex > 1024)
        m_fReadIndex -= 1024;

    if(m_fQuadPhaseReadIndex > 1024)
        m_fQuadPhaseReadIndex -= 1024;

    // invert?
    if(m_bInvert)
    {
        fOutSample *= -1.0;
        fQuadPhaseOutSample *= -1.0;
    }

    // write out
    *pYn = fOutSample;
    *pYqn = fQuadPhaseOutSample;
}
```

## processAudioFrame()

- 使用 doOscillate() 函数。

```
bool __stdcall CWTOscillator::processAudioFrame(float* pInputBuffer, float* pOutputBuffer, UINT uNumInputChannels, UINT uNumOutputChannels)
{
    // Do LEFT (MONO) Channel
    // if not running, write 0s and bail
    if(!m_bNoteOn)
    {
        pOutputBuffer[0] = 0.0;
        if(uNumOutputChannels == 2)
            pOutputBuffer[1] = 0.0;
        return true;
    }

    // some intermediate variables for return
    float fY = 0;
    float fYq = 0;

    // call the oscillator function, return values into fY and fYq
    doOscillate(&fY, &fYq);

    // write fY to the Left
    pOutputBuffer[0] = fY;

    // write fYq to the Right
    if(uNumOutputChannels == 2)
    {
        pOutputBuffer[1] = fYq;
    }
    return true;
}
```

构建并测试代码。图 9.16 清晰地显示了四相输出：左声道中的 sin()，右声道中的 cos()。

## 9.9 双极/单极功能

### 9.9.1 WTOscillator GUI

使用表 9.5 中的属性，通过下一组单选按钮将双极/单极开关添加到 UI 中。像处理之前的按钮一样编辑它，并为其赋予枚举值。我将变量命名为“m_uPolarity”，并使用“bipolar”和“unipolar”作为我的字符串/枚举。默认值将为双极。

![](img/b54974d0a4317ec82d7ae02126d10a6f_311_0.png)

图 9.16：左信号和右信号的正交相位输出。注意：你必须将示波器设置为自由运行模式，才能看到声道之间的相位差异。

表 9.5：极性控制的按钮属性。

| 滑块属性 | 值 |
|---|---|
| 控件名称 | 振荡器类型 |
| 单位 | |
| 变量类型 | enum |
| 变量名 | m_uPolarity |
| 枚举字符串 | bipolar, unipolar |

### 9.9.2 WTOscillator.cpp 文件

按照以下方式，将双极/单极功能添加到 doOscillate() 的最后部分，先除以 2 然后偏移 0.5：

```
void CWTOscillator::doOscillate(float* pYn, float* pYqn)
{
    <SNIP SNIP SNIP>
    /* write out
    *pYn = fOutSample;
    *pYqn = fQuadPhaseOutSample;
    // create unipolar; div 2 then shift up 0.5
    if(m_uPolarity == unipolar)
    {
        *pYn /= 2.0;
        *pYn += 0.5;

        *pYqn /= 2.0;
        *pYqn += 0.5;
    }
}
```

![](img/b54974d0a4317ec82d7ae02126d10a6f_312_0.png)

### 图 9.17：单极运行，正弦波。

构建并测试代码；图 9.17 显示了单极正弦波的输出。

以下是一些可以尝试的项目：

- 高分辨率表；钢琴指板的每个八度都有自己的表格，包含该八度最高音允许的尽可能多的谐波。
- 一个带有其中一个振荡器去调控制的双振荡器合成器模块。
- 一个仅播放音乐音高的振荡器。

在下一章中，我们将使用新的波表振荡器来制作调制延迟效果。

## 参考文献

- Dattorro, J. 2003. 效果设计，第 3 部分，振荡器：正弦和伪噪声。音频工程学会杂志，50(3): 114–146.
- Gordon, J. W., and Smith, J. O. 1985. 针对 VLSI 应用的正弦生成算法。国际计算机音乐会议论文集，第 165–168 页.
- Moore, R. 1990. 计算机音乐要素，第 3 章。恩格尔伍德克利夫斯，新泽西州：Prentice-Hall.
- Roads, C. 1996. 计算机音乐教程，第 2 章。剑桥，马萨诸塞州：麻省理工学院出版社.

从听觉和工程角度来看，最有趣的音频效果类型或许是调制延迟效果。它们包括合唱和弗兰杰/颤音；此外，调制延迟也出现在某些混响算法中。这些时变滤波器实际上非常精巧且实现起来很有趣，我们不遗余力地创建了有用的子模块。这些子模块包括数字延迟效果或 DDL（数字延迟线）模块和波表振荡器。如果你能设计、构建和实现调制延迟效果，那么你就在音频效果编程方面走向熟练的道路上了。这些效果的参数和系数会在每个采样周期中发生变化。

图 10.1a 显示了标准延迟线或 DDL。输出通过 fb 系数反馈。延迟保持不变，直到用户将其更改为另一个固定值。在图 10.1b 的调制延迟线（MDL）中，延迟量会随时间不断变化。系统仅使用总可用延迟量的一部分。

![](img/b54974d0a4317ec82d7ae02126d10a6f_313_0.png)

图 10.1：（a）静态延迟和（b）调制延迟效果。

调制深度与正在读取的延迟线部分的大小相关。调制速率是读取索引在调制延迟部分来回移动的速度。使用低频振荡器（LFO）来调制延迟量，LFO 可以是几乎任何类型的波形，甚至是噪声。最常见的波形是三角波和正弦波。要制作调制延迟效果，你首先需要创建一个延迟线，然后对其进行修改，以便在每个采样间隔不断更改和更新读取位置。

