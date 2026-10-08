
而且不是一个 DCA。这个简单的补丁（patch）由其中两个这样的构建块组成。Chowing 将这些 FM 结构命名为“操作器”（operators），它们用于 DX 合成器的架构，正如本章中的 DXSynth。FM 补丁的基本音色（刺耳的、柔和的、闷的、锐的、铃音等的）是多个操作器排列的结果。Chowing 从上到下绘制信号流，因为振荡器指向下方。图 12.10 显示了 Chowing 的缩写。注意省略了关于 EG（包络器）和振荡器控制频率的细节。每个操作器始终包含一个随附 EG，载波振荡器始终设置为 MIDI 音符音高，而调制振荡器始终使用 MIDI 音符音高的比例；每个调制器可以调至不同的比例。

图 12.9：具有一个载波器和一个调制器的简单 FM 补丁框图。

图 12.10：(a) 简单的操作器补丁 (b) Chowing 版本。

图 12.11：(a) 带有细节四操作器 FM 补丁 (b) Chowing 缩写。

除了在多个调制器上堆叠多个调制器外，FM 操作器还可以进行自调制，例如图 12.11 中堆叠的四个操作器。链中的最后一个操作器（第 4 号）是自调制的。

DX7 具有 32 种不同组合的六个 FM 操作器。DX100 具有 8 种不同组合的 FM 操作器。Chowing 将这些组合称为“算法”，而 DX 合成器被标记为“数字可编程算法合成器”——事实上，合成器外壳上处处出现“FM”字样。操作器可以串联或并联，并且可以有多个载波。图 12.12 显示了另外两种算法以及涉及的含义。本章中的 DXSynth 是 DX100 的紧密复制，在相同的算法组合中使用四个操作器。这些算法在图 12.13 中所示。

![](img/b42d0dca53f4a889d8162d55f7c8c05d_814_0.png)

![](img/b42d0dca53f4a889d8162d55f7c8c05d_814_1.png)

![](img/b42d0dca53f4a889d8162d55f7c8c05d_814_2.png)

## 12.5 DXSynth 规格

由于 DXSynth 基于 DX100，其音色需要四个振荡器和四个包络生成器。没有滤波器。它有一个 DCA，但用于声位控制（panning）和音量控制；没有 EG 连接到 DCA。相反，载波的包络决定了最终的时域包络。与 DX100 一样，这里有一个 LFO，可以独立地调制每个操作器的音高颤音或输出幅度（幅度调制或 AM）。图 12.14 显示了简化的框图，而图 12.15 显示了详细连接。不要被这个合成器的简单性误导——它在极极的 CPU 开销下，可以合成比其他合成器丰富得多的声音。

图 12.12：(a) 多个调制器输出并联求和四操作器补丁 (b) 四个并行载波；输出求和形成最终输出。

![](img/b42d0dca53f4a889d8162d55f7c8c05d_815_0.png)

图 12.13：DX100 和 DXSynth 中的八种算法。

表 12.4 显示了 DXSynth 的调制矩阵，由八行组成。这些将 LFO 路由到每个操作器的输出目标（AM 或颤音）。

表 12.5 显示了 GUI 控制。这些大多是重复的操作器控制。图 12.16 和 12.17 分别显示了 RackKFX 和 VST3/AU 的 GUI 设计。VST3 包含了八种 DX 算法的奖励。

图 12.14：DXSynth 简化框图。

表 12.4：DXSynth 将 LFO 路由到每个操作器目标的调制矩阵。

![](img/b42d0dca53f4a889d8162d55f7c8c05d_815_1.png)

图 12.15：DXSynth 详细连接。注意 Op1 Out、Op2 Out、Op3 Out 和 Op4 Out 的范围从 0 到 9，默认值为 7。这是该项目特殊的输出计算。DX 系列合成器具有 0 到 9 的输出控制。在之前的合成器中，默认使用 EG1 作为输出。在 DXSynth 中，这些控制产生接近对数的音量变化。使用从 DX100 收集的实证数据，synth.h 中的 `calculateAmplitude()` 函数复制了这种行为，并计算幅度标量。DXSynth 的另一个问题涉及输出 EG。从算法图中可以看出，某些情况下多个载波。载波 EG 是控制每个载波时间包络的输出 EG。这允许你创建有趣的补丁，因为你控制着在释放（release）阶段消失较快的谐波组。

![](img/b42d0dca53f4a889d8162d55f7c8c05d_16_0.png)

| 源 | 目标/强度 | 变换/范围 | 启用 |
| :--- | :--- | :--- | :--- |
| SOURCE_LFO | DEST_C1_OUTPUT_AMP | TRANSFORM_BIPOL_TO_BIPOL | FALSE |
| | dLFO1scModIntensity | m_DefaultRange | |
| SOURCE_LFO | DEST_C1_FO | TRANSFORM_NONE | FALSE |
| | dLFO1scModIntensity | | |
| SOURCE_LFO | DEST_C2_OUTPUT_AMP | TRANSFORM_BIPOL_TO_BIPOL | FALSE |
| | dLFO1scModIntensity | m_DefaultRange | |
| SOURCE_LFO | DEST_C2_FO | TRANSFORM_NONE | FALSE |
| | dLFO1scModIntensity | dOscFoRange | |
| SOURCE_LFO | DEST_C3_OUTPUT_AMP | TRANSFORM_BIPOL_TO_BIPOL | FALSE |
| | dLFO1scModIntensity | m_DefaultRange | |
| SOURCE_LFO | DEST_C3_FO | TRANSFORM_NONE | FALSE |
| | dLFO1scModIntensity | dOscFoRange | |
| SOURCE_LFO | DEST_C4_OUTPUT_AMP | TRANSFORM_BIPOL_TO_BIPOL | FALSE |
| | dLFO1scModIntensity | m_DefaultRange | |
| SOURCE_LFO | DEST_C4_FO | TRANSFORM_NONE | FALSE |
| | dLFO1scModIntensity | dOscFoRange | |

图 12.16：RackKFX 中可能的 DXSynth GUI；注意 LCD 中嵌入了多个控制。

图 12.17：VST3 和 AU 项目的 DXSynth GUI。

对于 DX 算法，只有当载波操作器的 EG 过期时触发音符。此外，延续（legato）模式和重置仅应用于输出 EG，而不是调制器，尽管你也可以尝试这一点。我们将使用之前 DXSynth 项目中使用的标准 EG，但如果你想要真实的，请考虑实现图 12.18 所示的 EG；只有这个 EG 有五个段和不同的编程模式，其攻击曲线与其他任何状态都不同。具体操作请参见挑战章节。

图 12.18：Yamaha DX 包络生成器有一个额外的段并使用 LEVEL 和 RATE 值进行。

## 12.6 振荡器中的 FM 和 PM

两个振荡器对象 `WTOillator` 和 `CBLimillator` 已经为 FM 和 PM 操作进行了设计和编码。首先，如第 5 章所示，允许正负频率。接下来，两者都允许瞬时频率。我们之前跳过了这一点，现在来看看。

# FM

![](img/b42d0dca53f4a889d8162d55f7c8c05d_817_0.png)

我们最终正在设计一个 PM 合成器，但今天仍然可以尝试 FM。频率调制在此计算之前作为音符频率的偏移进行计算——我们实际上在每个采样间隔内改变瞬时频率。

这段代码位于 `update()` 函数中：

你使用 `setModLn()` 函数设置线性频率偏移。要使用它，你需要将调制器的输出乘以频率偏差值，这将调制器缩放到某些正负频率偏移。

```
// --- Op2*EG2 值的输出
```

| 操作器 1 | Attack | Decay | Sustain | Release | 输出 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 12.34 | 12.34 | 12.34 | 12.34 | 12.34 | |

| 操作器 2 | Attack | Decay | Sustain | Release | 输出 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 12.34 | 12.34 | 12.34 | 12.34 | 12.34 | |

| 操作器 3 | Attack | Decay | Sustain | Release | 输出 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 12.34 | 12.34 | 12.34 | 12.34 | 12.34 | |

| 操作器 4 | Attack | Decay | Sustain | Release | 反馈 | Op21 | Op22 | Op23 | Op24 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 12.34 | 12.34 | 12.34 | 12.34 | | | | | | |

