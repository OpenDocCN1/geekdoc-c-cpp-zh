
# NanoSynth 处理代码

`NanoSynth` 的处理代码将渲染音频。这是一个非常重要的函数，我们需要理解它，因为我们在后续章节中将保留它，然后在第 6 章，我们将找到一种既简化又能大幅扩展合成器功能的方法。如果你没有跟随处理代码，这将非常困难。无论什么种平台，`NanoSynth` 将遵循相同的模式。第一部分通过检查其音符标志位来检查振荡器是否正在运行。在文中，我们渲染了调制器输入。在这种情况下，它是一个 `LFO` 对象：

```cpp
void CWTOscillator::updateOscillator()
{
// -- 先处理基类
COscillator::updateOscillator();
// -- 计算增量
m_dWT_inc = WT_LENGTH*m_dInc;
// -- 选择表格
selectTable();
}
```

接下来是处理该 `LFO` 输出，它在 `[-1,+1]` 范围内摆动，通过调用 `eFoModExp` 函数来调制音高振荡器的频率。注意 `LFO` 值（在振荡器中定义并以半音为单位给出）如何创建一个在 `[-OSC_FO_MOD_RANGE]` 之间波动的值。理解其工作原理以后将非常重要。应用修改后，我们调用 `update` 函数来应用振荡器中的更改。

最后，实现了音频引擎。两个振荡器按 50/50 的比例混合。

我们需要修改 `MIDI` 音符开启和关闭（`note` and `note off`）的处理。在第 3 章中，我们简单地记录了 `MIDI` 消息。现在我们要使用它们了。

```cpp
void WT0oscillator::createWaveTables()
```

## 音符说明 (Note On)

对于音符开启事件，我们需要：

```cpp
// 创建表格
//
// 正弦波: 只需要一个表格
for(int i = 0; i < WT_LENGTH; i++)
{
    // 采样正弦波，WT_LENGTH 点
    // sin(wNT) = sin(2*pi*i/WT_LENGTH)
    mDSineTable[i] = sin((double)i/WT_LENGTH)*(2*pi));
}
```

- 设置

```cpp
// 锯波、三角波: 需要 10 个表格
double dSeedFreq = 27.5; // 音符 A0，钢琴底部
for(int j = 0; j < NUM_TABLES; j++)

{
    double* pSawTable = new double[WT_LENGTH];
    memset(pSawTable, 0, WT_LENGTH*sizeof(double));

    double* pTTable = new double[WT_LENGTH];
    memset(pTTable, 0, WT_LENGTH*sizeof(double));
}
```

```cpp
int nHarms = (int)(m_nSamplesRate/2.0/dSeedFreq) - 1.0;
int nHalfHarms = (int)((float)nHarms/2.0);

double dMaxSaw = 0;
double dMaxTri = 0;
```

```cpp
for(int i = 0; i < WT_LENGTH; i++)
{
    // 锯波 += (-1)^g+1(1/g)sin(wNT)
    for(int g = 1; g <= nHarms; g++)
    {
        // Lanczos Sigma 因子
        double x = g*pi/nHarms;
        double sigma = sin(x)/x;

        // 仅应用于基频以上的泛音
        if(g - 1)
            sigma = 1.0;

        double n = double(g);

        pSawTable[i] += pow((float)-1.0,(float(g+1))*(1.0/n) * sigma*sin(2.0*pi*i/WT_LENGTH);
    }
}
```

```cpp
// 三角波: += (-1)^g(1/(2g+1^2)sin(w(2n+1)T))
// 注意：这里的限制是 nHalfHarms，因为
// 求和的构建方式（看 (2n+1））
// 分量
for(int g = 0; g <= nHalfHarms; g++)

else 
{
    double n = double(g);
    pTTable[i] += pow((float)-1.0,(float)n) * (1.0/pow((float)(2*n + 1),(float)2.0))*sin(2.0*pi*(2.0*n + 1)*i/WT_LENGTH;
}
```

```cpp
// 存储最大值
if(i == 0) {
    dMaxSaw = pSawTable[i];
    dMaxTri = pTTable[i];
}
```

使用 `MIDI` 码计算新的频率查找表，该表在 `synth.h` 中声明 - 更新振荡器变量

```cpp
if(pSawTable[i] > dMaxSaw)
    dMaxSaw = pSawTable[i];
if(pTTable[i] > dMaxTri)
    dMaxTri = pTTable[i];
```

```cpp
// 归一化
for(int i = 0; i < WT_LENGTH; i++) {
    // 归一化
    pSawTable[i] = dMaxSaw;
    pTTable[i] = dMaxTri;
}

// 存储
m_pSawTables[j] = pSawTable;
m_pTriangleTables[j] = pTriangleTable;
```

对于音符关闭（`note off`）事件，我们只需要停止所有振荡器。

```cpp
// --- 进入下一个八度
dSeedFreq *= 2.0;
```

## 音符关闭 (Note Off)

对于音符关闭事件，我们需要停止所有振荡器。

由于你没有跟随处理代码，这将非常困难。无论什么平台，`NanoSynth` 将遵循相同的模式。第一部分通过检查其音符标志位来检查振荡器是否正在运行。在文中，我们渲染了调制器输入。在这种情况下，它是一个 `LFO` 对象：

```cpp
void CWTOscillator::updateOscillator()
{
// -- 先处理基类
COscillator::updateOscillator();
// -- 计算增量
m_dWT_inc = WT_LENGTH*m_dInc;
// -- 选择表格
selectTable();
}
```

接下来是该 `LFO` 输出，它在 `[-1,+1]` 范围内摆动，通过调用 `eFoModExp` 函数来调制音高振荡器的频率。注意 `LFO` 值（在振荡器中定义并以半音为单位给出）如何创建一个在 `[-OSC_FO_MOD_RANGE]` 之间波动的值。理解其工作原理以后将非常重要。应用修改后，我们调用 `update` 函数来应用振荡器中的更改。

最后，音频引擎的实现。两个振荡器按 50/50 的比例混合。

我们需要修改 `MIDI` 音符开启和关闭的处理。在第 3 章中，我们简单地记录了 `MIDI` 消息。现在我们要使用它们了。

```cpp
void WT0oscillator::createWaveTables()
```
