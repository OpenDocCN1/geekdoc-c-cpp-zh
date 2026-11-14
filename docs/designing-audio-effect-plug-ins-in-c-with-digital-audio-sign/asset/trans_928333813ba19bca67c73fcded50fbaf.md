

初始条件：
y(n - 1) = sin(ωnT)
y(n - 2) = sin(ω(n - 1)T)
(9.4)

我们的问题是，我们知道新频率 ω，并且由于采样率也是已知的，因此我们也知道 ωT，但我们不知道自己处于第 n 个采样间隔。不过，我们可以按以下方式找出来：

- 对 y(n - 1) 延迟元素取反正弦。
- 将其除以 ωT 来找到 n 的值。
- arcsine() 返回 -π/2 到 +π/2 之间的值，即正弦波的上升沿，与原始初始条件相同。
- 如果处于上升沿，则按 sin((n - 1)ωT) 计算新的 y(n - 2) 值。
- 如果处于下降沿，则按 sin((n + 1)ωT) 计算新的 y(n - 2) 值。

在 cookFrequency() 函数中按以下方式更改很简单，所以请在代码中进行更改。请注意，原始初始条件代码被注释掉了，以便日后参考。同时请注意用于判断是上升还是下降的逻辑。我们需要这个逻辑，因为 arcsine() 函数只返回半个正弦波的角度。仔细想想，这很合理。如果你给它一个 0.707 的值，它无法判断角度是 45 度还是 135 度，两者的正弦值都是 0.707。

```
void CDirectOscillator::cookFrequency()
{
    // Oscillation Rate = theta = wT = w/fs
    float f_wT = (2.0f*pi*mFrequency_Hz)/(float)m_nSampleRate;

    // coefficients according to design equations
    m_f_b1 = -2.0f*cos(f_wT);
    m_f_b2 = 1.0f;

    // set initial conditions so that first sample out is 0.0
    // m_f_y_z1 = sin(-1.0f*f_wT); // sin(wnt) = sin(w-1)T
    m_f_y_z2 = sin(-2.0f*f_wT); // sin(wnt) = sin(w-2)T

    // re calculate the new initial conditions
    // arcsine of y(n-1) gives us wnT
    double wnT1 = asin(m_f_y_z1);
    // find n by dividing wnT by wT
    float n = wnT1/f_wT;

    // re calculate the new initial conditions
    // asin returns values from -pi/2 to +pi/2 where the sinusoid
    // moves from -1 to +1 - the leading (rising) edge of the
    // sinewave. If we are on that leading edge (increasing)
    // then we use the value 1T behind.
    //
    // If we are on the falling edge, we use the value 1T ahead
    // because it mimics the value that would be 1T behind
    if(m_f_y_z1 > m_f_y_z2)
        n-=1;
    else
        n+=1;

    // calculate the new (old) sample
    m_f_y_z2 = sin(n*f_wT);
}
```

构建并加载 DLL。然后，点击“开始”和“停止”按钮来控制振荡器。使用频率滑块更改数值。如果滑块变化过大，由于频率相差太远，会在波形中产生明显的偏移，因此在某些不连续处仍会听到咔哒声。

既然你已经了解如何在 RackAFX 中编写直接计算振荡器，接下来是几个供你尝试的示例振荡器设计。请记住，必须设置标志 m_bOutputOnlyPlugIn，才能使振荡器在 RackAFX 中正常工作。你还必须提供启动/停止机制。附带示例代码以供参考。

## 9.3 戈登-史密斯振荡器

戈登-史密斯振荡器使用一对按圆形配置排列的延迟元件，以产生正弦和余弦振荡。两个输出几乎完全处于正交相位（相差 90 度），仅相差半个采样周期。其正弦振荡足够纯净，可用于音频测试设备。而且，由于每个输出只使用一个延迟元件，更改频率时无需更新初始状态；单个 y(n - 1) 样本以与直接形式振荡器相同的方式与新频率共享。只需更新系数 e。当振荡频率变化时，会观察到微小的幅度变化，但它足够小，不会在输出中造成咔哒声或爆裂声。当缓慢调整频率时，它听起来与直接形式振荡器一样平滑。

两个输出标记为 y(n) 和 yq(n)，其中“q”代表正交。因此，有两个差分方程。必须先求解 yq(n) 的差分方程，因为 y(n) 依赖于它。戈登-史密斯振荡器框图如图 9.8 所示。

差分方程如下：

```
yq(n) = yq(n - 1) - εy(n - 1)
y(n) = εyq + y(n - 1)
```

指定：
- f_o，所需振荡频率

设计方程如下：

```
θ = 2πf_o / fs
ε = 2sin(θ/2)
```

初始条件：
y(n - 1) = sin(-1.0)
yq(n - 1) = cos(-1.0)

![](img/b54974d0a4317ec82d7ae02126d10a6f_287_0.png)

图 9.8：戈登-史密斯振荡器。

戈登-史密斯振荡器的 C++ 代码如下（已声明两个内存元素 m_f_yn_z 和 m_f_yq_z，以及系数 m_fGorSmithEpsilon）。在 cookFrequency() 中：

```
// calculate HS Epsilon
```

```
float f_Wt = (2.0*pi*m_Frequency_Hz)/(float)m_nSampleRate;
m_fGorSmithEpsilon = 2.0*sin(f_Wt/2.0);
```

在 processAudioFrame() 中：

```
// form yq(n) first
float f_yqn = m_f_yq_z - m_fGorSmithEpsilon*m_f_yn_z;
// y(n)
float f_yn = m_fGorSmithEpsilon*f_yqn + m_f_yn_z;
// shuffle delays
m_f_yq_z = f_yqn;
m_f_yn_z = f_yn;
// write out
pOutputBuffer[0] = f_yn;
etc...
```

## 9.4 波形表振荡器

波形表振荡器，顾名思义，是一种基于表格的系统，用于创建周期信号。循环缓冲区预加载了一个波形的一个周期（减去一个样本）。该波形可以是数学波形（sin、cos、脉冲、方波、锯齿波、三角波等），也可以是任意波形或录制的信号。基本思路是读取表格并从中输出样本。考虑一个包含 1024 个样本的表格，由一个正弦波的一个周期（减去一个样本）组成（图 9.9）。

假设你从 i = 0 开始，在每个采样周期内读取一个值并移动到下一个。在缓冲区末尾，你会环绕并重新开始。如果你每个采样周期读取一个值，那么生成的波形频率是多少？

答案是，当索引增量在表格中正好为 1.0 时，f_table = fs/L。在 44,100 Hz 采样率下，1024 点波形表的表频率为 43.06 Hz。如果你确实需要精确的 43.06 Hz 正弦波，那么这种方法将产生近乎完美的结果。唯一的因素是加载到表格中的正弦波的精度。如果表格中存储的是锯齿波，它的基频也将是 43.06 Hz。

很可能，你想要生成任意频率，也许侧重于音乐音高频率。除了音符 A 之外，这些频率将是带有小数部分的浮点数。要生成任意频率，请使用公式 9.7 计算 inc 值：

![](img/b54974d0a4317ec82d7ae02126d10a6f_289_0.png)

图 9.9：一个正弦波的一个周期减去一个样本。表格用值 $i$ 索引，起始值为 0；表格中的最后一项位于 $i = 1023$，它是波形重新开始前的那个样本。

```
inc = L \frac{f_{desired}}{f_s} (9.7)
```

$L$ 是表格长度，$f_{desired}$ 是目标频率。你得到的增量值将用于跳过表格，在每个采样间隔内向前移动 $inc$。如果 $inc$ 小于 1.0，则所需频率低于表频率；如果大于 1.0，则必须高于表频率。如果 $inc$ 是 2.0，则生成的频率是表频率的两倍。很可能，$inc$ 值将是非整数，因此将由整数部分和小数部分组成。例如，如果 $inc = 24.9836$，则整数部分为 24，小数部分为 0.9836。在这里，整数部分称为 $int$，小数部分称为 $frac$。

与你在第 8 章中构建的延迟模块一样，处理增量值小数部分有几种选择。你可以：
- 截断该值，忽略 $frac$。
- 在 $int$ 和 $int + 1$ 之间按 $frac$ 距离对表格进行线性插值。
- 使用多项式插值或其他插值方法代替线性插值。

如果截断 $inc$ 值，那么你会有多个问题——你合成的音符不会准确调音。此外，由于从表格转录时的不准确，它会失真。线性插值和多项式插值都能克服这些问题，尽管输出中仍然存在失真。行业标准是在波形表上使用四阶拉格朗日插值，使用目标插值点的相邻四个点（左侧两个和右侧两个）。

在编写波形表振荡器之前，你需要注意一件事：波形表的危险在于，存储在其中的数据周期可能充满了混叠分量。换句话说，你可以创建一个数据表，如果它是被采样的模拟信号，则永远无法通过输入低通滤波器（LPF）。我们将正是这样做，并创建一些信号，这些信号 do

