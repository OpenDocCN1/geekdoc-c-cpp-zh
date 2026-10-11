
<< 插入代码列表 11.1: 声明 **此处** >>

等……

- 创建一个包含 128 个振荡器和 128 个向量混合值的混合表面是困难且低效的；在任何时刻，对于远离混合点的样本，大多数混合值将是零或接近于零
- 在 iPad 上为每个笔记事件运行 128 个振荡器将非常繁琐，如果不是不可能的话
- 如果所有 128 个振荡器在混合点位于波形表之间时以非零比例进行混合，你将得到一大堆噪音

```cpp
AUSynth::AUSynth(AudioUnitInComponentInstance)
: AUInstrumentBase(inComponentInstance, 0, 1)
```
```cpp
{
  // --- 创建输入、输出端口、组和部分
  CreateElements();
```
```cpp
// --- 设置默认工厂预设（示例）
factoryPreset[OSC1_AMPLITUDE_DB] = 0.0;
factoryPreset[OSC2_AMPLITUDE_DB] = 0.0;
```
```cpp
<SNIP SNIP SNIP>
```
```cpp
// --- 定义参数（控件）的数量
Globals()->SetUseIndexedParameters(NUMBER_OF_SYNTH_PARAMETERS);
```
```cpp
// --- 在此处初始化控件！
// --- 这些定义在 SynthParamLimits.h 中
```
```cpp
<SNIP SNIP SNIP>
```
```cpp
// -- VS 特有
Globals()->SetParameter(VECTORJOYSTICK_X, DEFAULT_UNIPOLAR_HALF);
Globals()->SetParameter(VECTORJOYSTICK_Y, DEFAULT_UNIPOLAR_HALF);
Globals()->SetParameter(PATH_MODE, DEFAULT_PATH_MODE);
Globals()->SetParameter(ORBIT_X, DEFAULT_UNIPOLAR);
Globals()->SetParameter(ORBIT_Y, DEFAULT_UNIPOLAR);
```

- 当 `Globals()->SetParameter(ROTOR_RATE, DEFAULT_SLOW_LFO_RATE);`
`Globals()->SetParameter(ROTOR_WAVEFORM, DEFAULT_LFO_WAVEFORM);`

等……关于设备上的注释，你会听到靠近混合点的振荡器的混合，而听不到远处的音色

- - 声音平滑地相互变换，没有不连续性，除非转子速率和轨道幅度非常高，此时你可以听到波形表被跳过了

```cpp
void AuSynth::update()
{
    // --- 更新全局参数
    //
    等……
    // --- VS 特有
m_GlobalSynthParams.voiceParams.uvectorPathMode =
    Globals()->GetParameter(PATH_MODE);
m_GlobalSynthParams.voiceParams.dorbitXAmp =
    Globals()->GetParameter(ORBIT_X);
m_GlobalSynthParams.voiceParams.dorbitYAmp =
    Globals()->GetParameter(ORBIT_Y);
// --- 仅限 VST3/AU ---
// 根据 x,y 位置计算向量摇杆混合值
// (x,y 为 0到1)
calculateVectorJoystickValues(
    Globals()->GetParameter(VECTORJOYSTICK_X),
    Globals()->GetParameter(VECTORJOYSTICK_Y),
    m_GlobalSynthParams.voiceParams.dAmplitude_A,
    m_GlobalSynthParams.voiceParams.dAmplitude_B,
    m_GlobalSynthParams.voiceParams.dAmplitude_C,
    m_GlobalSynthParams.voiceParams.dAmplitude_D);
```

混合方程效果非常好且易于实现——为什么要发明轮子？`AUSynth` 将四个振荡器视为一个较小的混合表面。每个振荡器组构成一个混合表面。在任何时刻，合成器的输出是包含混合点的四个振荡器的组合。注意到任何相邻单元格都会共享两个波形表。为了简化计算并复用摇杆控件，`AUSynth` 使用正方形波形表而不是矩形。如果将摇杆控件修改为矩形，通过使用非摇杆坐标系更容易看到 `AUSynth` 如何工作，其中混合点呈正方形排列。

等…… -- LFO: `m_GlobalSynthParams.lfoParams.uWaveform = Globals()->Get(ROTOR_WAVEFORM);`
`m_GlobalSynthParams.lfofo = Globals()->Get(ROTOR_RATE);`

它不仅决定了波形表的数量，还作为计算的一部分。每边单元格的数量与总波形表数量：

图11.34：`AUSynth` 表面上的几个单元格。

图11.35：当 `C=3` 时，有 (a) 三行三列共九个单元格和 (b) 编号 0 到 15 的波形表。

`num samples = (C + 1)^2`

`AUSynth` 使用 `C=5` 波形表。我们将很快讨论这些表。为了显示 `AUSynth` 如何清晰地跨越混合表面，使用 `C=3` 或 16 的较小混合表面更简单。单元格结构和波形表如图11.35 所示。注意到每边单元格的数量也是行数。行索引值在稍后需要。在这种情况下，`C=3` 用于使图表复杂。

![](img/b42d0dca53f4a889d8162d5f7c8c05d_786_0)

# Wavetable Grid

当混合点位于单元格之外时，该单元格被激活，其顶点被视为 VS 表面的 A、B、C 和 D。随着路径/路由器的移动，活跃单元格进行切换。由于相邻单元格共享公共顶点，这只是将正确的波形表映射到语音对象的问题。`AUSynth` 对象与具有振荡器的 `VectorSynth` 对象类似，每个从采样文件读取。图11.36(a) 显示第一个单元格中的混合点正向单元格移动。注意到顶点已索引。在图11.36(b) 中，混合点触碰了 D-C 边界，其混合比例为 50% C、50% D 以及其他。

现在假设混合点跨越 D-C 边界进入下方单元格（单元格 3），如图11.37 所示。当发生时，语音对象必须为下一个单元格切换当前的波形表。然而，有两个是共享的——波表 4 和 5（D 和 C）变为下一个单元格的 A 和 B。在边界处，由于位置的原因，D 和 C 波形表被重命名为 A 和 B。注意到现在的混合比例为 50% A、50% B 以及其他，由于波形表共享共享，单元格切换没有故障或不连续。如果路径直接通过顶点，则混合值将为 100%，波形表将分布，混合继续到下一个单元格（100% 水平）。

![](img/b42d0dca53f4a88912df7c8c05d_787_0.png)

图11.36：(a) 单元格 0 中的混合点使用单元格顶点计算当前混合 (b) 混合点已移动到单元格顶点 D 和 C 的边缘。

![](img/b42d0dca53f4a88912df7c8c05d_787_1.png)

图11.37：(a) 混合点跨入下一个单元格，那里的振荡器名称被洗牌，但边缘波形表保持不变，因此当混合点进入新单元格时没有听到的点击声 (b) 混合点继续沿路径 3 移动。

![](img/b42d0dca53f4a88912df7c8c05d_787_2.png)

图 11.39 显示，路径和轨道的概念保持不变，只是被应用到了更大的表面上。

图 11.39：(a) 矢量路径和 (b) 路径加旋转器现在在更大的表面上移动，但它们被视为每个单元格内的局部向量混合。

![](img/b42d0dca53f4a889d8162d55f7c8c05d_788_0.png)

## 11.18 AniSynth 规范

图 11.40 显示了 `AniSynth` 的简化框图。它与 `VectorSynth` 相同，不同之处在于波表矩阵向振荡器 A、B、C 和 D 提供信号。

图 11.41 显示了如何将 36 个波表映射到摇杆控制上。当你移动摇杆时，混合表面变得稠密得多，波表数量是原来的八倍。

![](img/b42d0dca53f4a889d8162d55f7c8c05d_788_1.png)

波表以 0 索引，并如图 11.40 所示通过连续行推进。`AniSynth` 在渲染和 `loadSamples()` 函数上确实与 `VectorSynth` 有不同。GUI 和调制矩阵是相同的，因此你可以修改 `VectorSynth`，也可以将其作为 `AniSynth` 的基础。为了演示另一种滤波器，你在该项目中使用了二极管阶梯滤波器。

## 振荡器：

- 四个 `CSampleOscillators`，每个播放 36 个不同波表之一；每个波表都从 `.wav` 文件提取。

## 滤波器：

- 两个 `CDiodeLadderFilters`（一个用于左声道，一个用于右声道）。

## LFO

- 两个 `CLFOs`，一个通用的，一个用于旋转器。

`AniSynth` 并不像 `VectorSynth` 那样预先定义任何 `CSampleOscillators`。相反，它根据 `CSample` 振荡器数组运行。它会跟踪当前激活的单元格。当不同的单元格激活时，`CAniSynthVoice` 会切换四个振荡器指针。这如图 11.42 所示。此版本的 `AniSynth` 使用单采样（single-samples）而非多采样（multi-samples）。

## 波表

对波表有一些重要的限制。`CAniSynthVoice` 在激活单元格改变时会切换表指针。振荡器的索引值在切换期间不会更改。因此，波表必须遵循以下规则（注意：你可以使用单采样或多采样）。

- 所有表的长度必须以采样数为单位。
- 所有表都应该包含一个波形的周期，并且每个表包含的周期数相同。
- 如果每个表的周期数多于一个，你将需要修改调谐方程。
- 合成质量与波表的质量直接相关。
- 表行的排列（即 AniMoog 的音色）也是一个重要的考虑因素。

图 11.40：`AniSynth` 简化框图。

图 11.41：在 (a) RackAFX 和 (b) VST3 及 AU 中将 36 个波表映射到摇杆控制。

对于 `AniSynth`，我们使用一个包含 4,300 个单周期波表的库作为选择所需的 36 个波表的基础。该库被称为 Adventure Kid Wave Forms (AKWF)，它是免费的：

![](img/b42d0dca53f4a889d8162d55f7c8c05d_789_0.png)

![](img/b42d0dca53f4a889d8162d55f7c8c05d_789_1.png)

www.adventurekid.se/akrt/waveforms/adventure-kid-waveforms/，或者我的网站。该集合包含了 4,300 个单周期波形，提取自合成器、计算机以及大提琴、单簧等声学器。还有 FM、原始（锯波、正弦波、方波）以及人声波。这些波表是单声的，长度均为 600 采样。

波表在 `Table(function)` 中加载。`CAniSynthObject` 存储了从 `.wav` 文件动态创建的 `CSampleOscillator` 对象的数组。这些 `CSOscillator` 对象实际上是波表。指针以采样的相同顺序填充数组。你可以从图 11.43 查看指针在单元格中的排列模式。

## 图 11.42：`AniSynth` 在激活单元格改变时切换振荡器表；注意表 5 和表 4 分别从 OscC 和 OscD 移动到 OscB 和 OscA 单元格；新表被添加而旧表被丢弃。

![](img/b42d0dca53f4a889d8162d55f7c8c05d_790_0.png)

一些 AKWF 波形听起来很悦耳，另一些则不然。该库巨大且免费。强烈鼓励你为该项目寻找自己的高质量单周期波形。首选立体波形，因为它们听起来更好。你还应该尝试使用声音相似的采样行。使用 AKWF 采样这很容易，它们根据来源或声音被分成若干文件组。

# initOscWithFilePath()

# initOscWithFolderPath()

```cpp
void CAniSynth::prepareForPlay()
{
```

这两个函数通过文件或文件夹从主数组中初始化一个从零开始索引的振荡器。它会在数组中找到该振荡器并调用其初始化函数。

```cpp
// --- 始终先基类
VectorSynth::prepareForPlay();
```
```cpp
// --- 找到中心单元格
```

# setActiveCell()

```cpp
if(m_nCells != 0)
	setActiveCell((m_nCells - 1)/2.0);
```

此函数实现了根据单元格索引对四个振荡器指针的查找逻辑。

# doVoice()

`doVoice()` 函数的实现与 `VectorSynthVoice()` 中的实现几乎相同，因此我们只讨论新部分。根本区别在于，在运行摇杆程序并找到当前的摇杆混合位置后，你需要找到该点所在的单元格。这是通过 `synthfunctions.h` 中的函数 `translateRotorPointToGridCell()` 完成的。它仅仅是一个从坐标到单元格的数学映射。如果单元格自上一个采样周期以来发生了变化，则调用 `setActiveCell()` 函数来切换振荡器指针。单元格被视为局部混合表面，函数的其余部分与 `VectorSynthVoice` 相同。

`loadSamples()` 函数在每个平台上几乎完全相同，并且类似于 `VectorSynth`。该函数使用单独的 `.wav` 文件初始化每个振荡器；文件名被保留，且由于该函数体量过大，在此处无法完整重复。请下载示例代码以获取完整列表。此处显示的是 RackAFX 版本；平台之间唯一的区别是根据 DLL 位置生成路径。

# 11.20 AniSynth 文件

`AniSynth` 使用以下文件，你将按照通常的方式将它们添加到编译器的项目单元。

对于 VST3 和 AU，你还需要添加 `SynthParamLimits.h`，它位于 `AniSynth` 示例代码中——记住，每个合成器的该文件都略有不同，因为它包含了 GUI 控制索引枚举。

`AniSynth` 与 `VectorSynth` 相同，仅使用 `CAniSynthVoice` 代替了 `CVectorSynthVoice`，且 `loadSamples()` 函数有所不同。调制矩阵和 GUI 控制是相同的。你可以选择复制并修改你的 `VectorSynth` 项目，或者从头开始。

对于 `plugin.h` 文件：

- 在文件顶部包含 `"AniSynthVoice.h"`
- 使用下方的代码列表——注意唯一的区别是存储在数组中的语音对象指针的类型

# 11.21 AniSynth,

RackAFX, VST3 和 AU。使用 `VectorSynth` 作为起点创建 `AniSynth` 项目——GUI 控制是相同的。用新的 `loadSamples()` 函数替换原始函数，并更改所有引用，以：

```cpp
bool AniSynth::createOscillatorArray(int nCellsPerSide) {
    // --- 如果已存在则删除
    if(m_ppOscArray) {
        // --- 尺寸
        int nArraySize = pow(m_nCellsPerSide + 1.0, 2.0);
        for(int i=0; i<nArraySize; i++)
            delete m_ppOscArray[i];
    }
    // --- 尺寸（使用参数）
    int nArraySize = pow(nCellsPerSide + 1.0, 2.0);
# --- 创建新的指针数组
    m_ppOscArray = new CSampleOscillator[nArraySize];
    // --- 验证
    if(!m_ppOscArray)return false;
    // --- 载入新的振荡器指针
    for (int i=0; i<nArraySize; i++)
        m_ppOscArray[i] = new CSampleOscillator();
    // --- 存储备后用
    m_nCellsPerSide = nCellsPerSide;
    m_nCells = pow(m_nCellsPerSide, 2.0);
    return true;
}
```

将插件对象中的 `CVectorSynthVoice` 更改为 `CAniSynthVoice`。不要删除或修改 `CSynthVoice`，因为 `CAniSynthVoice` 派自它。此合成器的外观和行为与 `VectorSynth` 完全相同，只是混合表面有 36 个声源而不是4 个。路径、旋转器和编程完全相同。如果你决定使用自己的 wavetable 文件，请确保遵守规则。

```cpp
inline bool initOscWithFilePath(int noscIndex, char* pPath, bool bSingleCycleSample, bool bPitchlessSample) {
    if(!m_ppOscArray) return false;
```
