

• 自定义成员变量后无须添加的内容

```cpp
CDiodeLadderFilter::CDiodeLadderFilter(void)
{
    // --- 初始化
    m_dK = 0;
    m_dGamma = 0.0;

    // --- 反馈增量
    m_dSG1 = 0.0; m_dSG2 = 0.0; m_dSG3 = 0.0; m_dSG4 = 0.0;

    // --- 将所有滤波器设置为低通滤波器 (LPF) 类型
    m_LPF1.setFilterType(LPF1);
    m_LPF2.setFilterType(LPF1);
    m_LPF3.setFilterType(LPF1);
    m_LPF4.setFilterType(LPF1);

    // --- 设置默认滤波器类型
    m_uFilter = LPF4;

    // --- 清空所有状态
    reset();
}
```

构造函数将初始化对象（尽管你在这里需要初始化你的 GUI 控件）

```cpp
void CDiodeLadderFilter::reset()
{
    // --- 清空所有状态
    m_LPF1.reset();
    m_LPF2.reset();
    m_LPF3.reset();
    m_LPF4.reset();
}
```

# Initialize()

- • 在滤波器上设置采样率

# update()

- • 直接更新滤波器截止频率 (fc)
- • 调用 `setQControl()` 函数设置 Q 值；对于每个合成器，其范围简单为 1 到 10
- • 调用 `update()` 函数以应用更改

# Render()

- • 修改音频渲染代码

# 使用第 2 章描述的方法设计你的 GUI。在复制到 Xcode 项目时请注意命名空间问题。

```cpp
void CDiodeLadderFilter::setQControl(double dQControl) {
    // 此映射 dQControl 从 1->10 到 K 从 0->17
    m_dK = (17.0)*(dQControl - 1.0)/(10.0 - 1.0);
}
```

## 7.25 构建与测试

在平台上构建并测试。虽然这是一个简单的合成器，但得益于虚拟振荡器和滤波器，你可以获得一些厚实的声音。使用滤波器跟踪和强度控件来感受调制对补丁的影响程度。当 Q 达到最大且启用 NLP 调制时，测试滤波器的自激荡模式。一旦对结果满意，返回并测试其余滤波器。由于它们派自同一个类，你需要执行：

- .h 文件
- 修改滤波器成员声明为新滤波器
- 在 GUI 中添加所需的任何控件；例如，如果你想使用 BSF，SEM滤波器需要；同样，Moog 和二极梯滤波器需要通带增益补偿

在下一章中，我们将返回并检查代码。我们将再次修改 NanoSynth：

- 使合成器在调制方面更具活性
- 添加复声功能
- 减少冗余编码

## 7.26 挑战

### 铜牌挑战

SEM 滤波器的 Q 控制从 0.5 调整到 25 但不会自激荡。当 Q 达到限制 25 时添加自激荡的能力。提示：查看 `update()` 函数中的 R 变量。什么值会导致自激荡？一旦开始振荡，启用 NLP 并调整控制直到其符合你的要求。

### 银牌挑战

修改基类和所有派生滤波器以实现可调的 Q 控制。你将以线性方式调制 Q，因此不需要音八度转换。对于此挑战，仅实现单一输入 `setQ()` 并确保在 `updateFilter()` 中正确计算调制后的 Q 值。

### 金牌挑战

赋予 NanoSynth 创建多个滤波器模型的能力。例如，你可以使用带有 Oberheim 波形的 Moog 梯滤波器。扩展控件允许用户选择滤波器类型，然后通过修改 `m_filterType` 变量来更新滤波器。随后，对其他滤波器进行尝试。设计一个实现所有滤波器类型的 C++ 对象。这将极大增加你合成器的活性。

```cpp
void CDiodeLadderFilter::update()
{}
```

# 铂金挑战

使用 Modified 方法推导 LPF 和 HPF 框。提示：Zavalish 方法产生相同的结果，这就是解决方案。

```cpp
// 基类调制
CFilter::update();
// 计算 alphas
double wd = 2*pi*m_dFc;
double T = 1/m_sampleRate;
double wa = (2/T)*tan(wd*T/2);
double g = wa*T/2;
```

# 钻石挑战

使用 Modified 方法推导 Moog 半梯滤波器。在代码中实现（这是可选的，不是书的一部分，如果你需要帮助的话）。

```cpp
// 大 G 值
double G4 = 0.5*g/(1.0 + g);
double G3 = 0.5*g/(1.0 + g);
double G2 = 0.5*g/(1.0 + g - 0.5*G3);
double G1 = g/(1.0 + g - g*G2);
G4 = G3*G2*G1;
```

等待，文本提到：http://www.willpirkle.com/synthbook/。接下来，回顾反馈路径并推导方程。设计之间有什么差异？你期望频率响应是双极性的（相同或否）吗？

```cpp
// 设置 betas
m_LPF1.m_dBeta = 1/(1.0 + g - g*G2);
m_LPF2.m_dBeta = 1/(1.0 + g - 0.5*g*G3);
m_LPF3.m_dBeta = 1/(1.0 + g - 0.5*g*G4);
m_LPF4.m_dBeta = 1/(1.0 + g);
// 设置 deltas
m_LPF1.m_dDelta = g;
m_LPF2.m_dDelta = 0.5*g;
m_LPF3.m_dDelta = 0.5*g;
m_LPF4.m_dDelta = 0.0;
// 设置 Gamma
m_LPF1.m_dGamma = 1.0 + G1*G2;
m_LPF2.m_dGamma = 1.0 + G2*G3;
m_LPF3.m_dGamma = 1.0 + G3*G4;
m_LPF4.m_dGamma = 1.0;
// 设置 epsilons
m_LPF1.m_dpsilon = G2;
m_LPF2.m_dpsilon = G3;
m_LPF3.m_dpsilon = G4;
m_LPF4.m_dpsilon = 0.0;
// 设置 a0
m_LPF1.m_da0 = 1.0;
m_LPF2.m_da0 = 0.5;
m_LPF3.m_da0 = 0.5;
m_LPF4.m_da0 = 0.5;
}

# 参考文献

Nagahara, Yasuo. 1977. "Voltage Controlled Filter." 美国专利. 

