

$$\frac{\Delta\omega_{mod}}{\omega_c} = \sin(\omega_r t)\omega_{out} = (\omega_c + \omega_{mod})t$$ (12.19)

```cpp
// --- 执行完整的频率调制
m_dFo = m_d0scFo*m_dDFoRatio*pitchShiftMultiplier(m_dDFoMod + 
m_dPitchBendMod + 
m_nOctave*12.0 + 
m_nSemititones + 
m_nCents/100.0);
```

```cpp
// --- 应用线性 FM（未在书中项目未使用）
m_dFo += m_dFoModLin;
```

```cpp
// --- 计算增量，等..
```

```cpp
dOut2 = 
dEG2*m_Op2.doOscillate();
// --- 计算频率偏移 DF = 
(fm)
dFreqDev =
IMAX*m_Opl.m_d0scFo;
```

图 1.29：模计数器也是相位增量计数器；当它在 0.0 和 1.0 之间摆动时，振荡器的瞬时相位从 0 移动到 $2\pi$ 弧度。

![](img/b42d0dca53f4a889d8162d55f7c8c05d_819_0.png)

```cpp
// --- 设置 FM 
调制
m_Opl1.setFoModLin(dFreqDev*dOut2);

// --- 更新新振荡器
fo
m_Opl.update();
```

PM

相位调制在两个振荡器对象之间的实现方式略有不同。QCBLimitOscillator 使用模计数器并对其进行增加，不仅是为了一来而是为了形成输出波形。在波形的一个周期内，模值从 0.0 变为 1.0，因此当前的模输出代表 0 到 2π 弧度的相位值。这在图 12.19 中所示。

因此，我们可以通过偏移模计数器的当前值来获取振荡器的瞬时相位。

在 DXSynth 中，相位模的索引（也是相位偏移）是以 2π 弧度的倍数给出的。对 DX100 的实验表明最大相位偏移为 8.0π 弧度。在 DXSynth 中，根据 Chowings 0 到 4 的 iMAX 范围，相位偏移被给出 0.0 到 4.0 之间的值。当应用于双极正弦波振荡器时，它会产生从 -8.0π 到 +8.0π 的相位偏移。因此，+1.0 的相位偏移意味着相当于一个完整波形或 +2π 弧度的位移。

所以，如果我们给当前模值加上 1.0，相位就会向前位移 2π 弧度。如果我们减去 1.0，我们就在向后位移 2π 弧度。COscillator 对象有一个相位调制变量和一个用于它的 `set()` 函数。因此，相位调制被实现为模计数器的偏移。由于偏移可能大于 1，我们必须多次取模（wrap）增量值，直到它落在 [0..1] 的模区间内。这段代码是 QCBLimitOscillator 的 `dooscillator()` 方法。

虚拟内联双精度 dooscillator(double* pAuxOutput = NULL`

```cpp
{
    if(!m_bNoteOn)
        return 0.0;

    double dOut = 0.0;

    // 总是优先
    bool bWrap = checkWrapModulo();

    // 为相位调制添加
    double dCalcModulo = m_dModulo + m_dPhaseMod;
    checkWrapIndex(dCalcModulo);
```

`checkWrapIndex()` 位于 `synthfunctions.h` 中，它简单地反复封装该值，直到它位于范围内。

在波形表振荡器中，我们几乎处于相同的情况——模计数器跟踪一个周期循环的时间，但我们使用索引值来遍历表格。由于增量值是：

```cpp
switch(m_uWaveform)
{
    case SINE:
        etc...
```

1.0 的相位偏移（代表 2π 弧度）意味着我们需要通过一个完整周期的长度来改变当前索引值，即波形表本身的长度。因此，在它的 `doWetable()` 函数内部，我们通过乘以表长度来更改用于查找的索引值。所以你可以看到两种 PM 计算几乎完全相同，且非常容易实现。

## 12.7 Yamaha DX100 vs. DXSynth

DXSynth 的基本架构与 DX100 非常吻合。在设计 DXSynth 时，使用一台真实的 DX100 进行比较和调优。DX 输出幅度建模便于测试，以便可以快速评估补色（patches）。图 12.20–23 显示了在某些设置下 DX100 与 DXSynth 的时域输出。

```cpp
inline void checkWrapIndex(double& dIndex)
    while(dIndex < 0.0)
        dIndex += 1.0;
```

```cpp
while(dIndex >= 1.0)
    dIndex -= 1.0;
```

```cpp
inc = L / f;
```

(12.20)

```cpp
double CWTOscillator::waveTable(double& dReadIndex, double dWT_inc)
    double dOut = 0;
```

```cpp
// 应用相位调制，任意
double dReadIndex = dReadIndex + m_dPhaseMod*WT_LENGTH;

// 检查读取索引上的多次取模
checkWrapIndex(dModReadIndex);

// 获取整数部分
int nReadIndex = abs((int)dReadIndex);
```

等...12.24–12.25 显示了某些补色下 DX100 与 DXSynth 的频谱。我们还注意到 DX 输出的微小变化会导致频谱分量发生巨大变化。例如，在图 12.24 中，将 DXSynth Op3 输出从 75.0 更改到 75.2 会导致非常不同的频谱。这导致了你在频谱中看到的差异。

图 12.20：(a) 真实的 DX100 和 (b) 基本双算子补色的 DXSynth 输出：算法：DX1, Op1 输出: 99, Op2 输出: 99, Op3 输出: 0, Op4 输出: 0, Note：F2。

图 12.21：(a) 真实的 DX100 和 (b) 基本三算子补色的 DXSynth 输出：算法：DX1, Op1 输出: 99, Op2 输出: 99, Op3 输出： 75, Note：F2。

图 12.22：(a) 真实的 DX100 和 (b) 基本四算子补色的 DXSynth 输出：算法：DX1, Op1 输出: 99, Op2 输出: 99, Op3 输出: 75, Op4 输出：0, Note：F2。

图 12.23：(a) 真实的 DX100 和 (b) 基本四算子补色的 DXSynth 输出：算法：DX1, Op1 输出: 99, Op2 输出: 99, Op3 输出： 75, Op4 输出：50, Note：F2。

![](img/b42d0dca53f4a889d8162d55f7c8c05d_)

图 12.24：(a) 真实的 DX100 和 (b) 基本双算子补色的 DXSynth 输出：算法：DX1, Op1 输出: 99, Op2 输出: 99, Op3 输出： 0, Op4 输出：0, Note：F2。

![](img/b42d0dca53f4a889d8162d55f7c8c05d_)

图 12.25：(a) 真实的 DX100 和 (b) 基本三算子补色的 DXSynth 输出：算法：DX1, Op1 输出: 99, Op2 输出: 99, Op3 输出： 75, Note：F2。

