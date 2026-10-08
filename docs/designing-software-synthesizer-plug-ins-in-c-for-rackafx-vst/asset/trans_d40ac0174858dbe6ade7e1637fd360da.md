
将一个源处理到一个目标所需的必要信息。

操作如下：

- 清除所有目标

```cpp
if(!m_ppMatrixCore) return false;

for(int i=0; i<m_nSize; i++) {
    modMatrixRow* pRow = m_ppMatrixCore[i];

    // 寻找匹配的源/目标对
    if(pRow->uSourceIndex == uSourceIndex && pRow->uDestinationIndex == uDestinationIndex) {
        if (pRow->bEnable == bEnable) {
            return true; // 找到了
        }
    }
}
return false;
```

- 遍历矩阵行并：
  - 获取矩阵行指针
  - 检查行是否已启用
  - 确保这是要处理的正确目标（层）
  - 从数组获取源值
  - 如果有变换，则应用变换
  - 检查目标；如果是通用“ALL”类型之一，则处理到所有这些类型中（注意它也会也将值写入 ALL 槽位），否则仅执行单次源->目标操作

请注意，对于所有将目标缩放源累积到目标的行，处理函数是相同的：

ModulationMatrix.cpp 文件包含了非常简单的构造函数和析构函数。注意，构造函数分配了矩阵核心，而析构函数什么都没做——因为核心是共享的，它将由全局所有者负责删除该核心。

## 8.3 使用和对调制矩阵编程：

在我们所有的合成器中，调制矩阵都是一个共享对象；每个设备只有一个矩阵。在 NanoSynth 中，插件插件对象通过创建并填充其行来使用调制矩阵程序，然后将调制矩阵对象的指针传递给设计的每个系统组件。当我们引入以下内容时，将会发生细微变化：

```cpp
inline bool checkDestinationLayer(UINT uLayer, modMatrixRow* pRow)
{
    bool bLayer0 = false;
    if(pRow->uDestinationIndex >= DEST_LF01_FO &&
        pRow->uDestinationIndex <= DEST_ALL_EG_SUSTAIN_OVERRIDE)
        bLayer0 = true;

    if(uLayer == 0)
        return bLayer0;

    if(uLayer == 1)
        return !bLayer0;

    return false;
}

destination += source*intensity*range
inline void doModulationMatrix(UINT uModLayer)
{
    if(!m_ppMatrixCore) return;

    // 清除目标寄存器
    clearDestinations();

    for (int i=0; i<m_nSize; i++)
    {
        // 获取行
        modMatrixRow* pRow = m_pModMatrix[i];

        // --- 这不应该发生
        if(!p) continue;

        // --- 如果禁用，跳过该行
```cpp
if(! pRow->bEnable) continue;
```

```cpp
// --- 检查调制层
if(!checkDestinationLayer(uModLayer, pRow)) continue;
```

```cpp
// 获取源值
double dSource = m_dSources[pRow->uSourceIndex];
```

```cpp
switch(pRow->uSourceTransform) {
    case TRANSFORM_UNIPOLAR_TO_BIPOLAR:
        dSource = unipolarToBipolar(dSource);
        break;

case TRANSFORM_BIPOLAR_TO_UNIPOLAR:
        dSource = bipolarToUnipolar(dSource);
        break;

    <SNIP SNIP>
    default:
        break;
}
```

```cpp
// destination += source*intensity*range
//
```

```cpp
double dModValue = dSource*(pRow->pModIntensity)
    *(pRow->pModRange);
```

```cpp
// 检查 DEST_ALL 类型
switch(pRow->uDestinationIndex);
```

图图 8.9 显示了 NanoSynth 的简化连接图，以及一个显示调制矩阵和每个组件拥有该矩阵指针的示意图。

矩阵分两步编程：首先，必须告诉每个对象源数组或目标的调制值。然后，动态分配矩阵行并添加到矩阵，然后设置

```cpp
case DEST_ALL_OSC_FO:
    m_dDestinations[DEST_OS1_FO] += dModValue;
    m_dDestinations[DEST_OS2_FO] += dModValue;
    m_dDestinations[DEST_OS3_FO] += dModValue;
    m_dDestinations[DEST_OS4_FO] += dModValue;
    m_dDestinations[DEST_ALL_OSC_FO] += dModValue;
    break;
```

<SNIP SNIP>

```cpp
// 对于所有“单个”源/目标，这是调制
default:

m_dDestinations[pRow->uDestinationIndex]
    += dModValue;
```

```cpp
CModulationMatrix::CModulationMatrix(void)
```

```cpp
// --- 矩阵的动态分配
m_ppMatrixCore = new modMatrixRow*[MAX_SOURCES*MAX_DESTINATIONS];
    memset(m_ppMatrixCore, 0,
        sizeof(modMatrixRow));
```

```cpp
m_nSize = 0;
clearMatrix(); // 填充

clearSources();
clearDestinations();
```

```cpp
CModulationMatrix::~ModulationMatrix(void)
```

![](img/b420dca53f4a889d16d55f7c05d_478_0.png)

- 幅度（幅度调制 AM）

目标（我们写入输出的地方）：

- 输出 1（对于 LFO 来说是普通输出；对于振荡器来说是左输出）

- 输出 2（对于 LFO 来说是相位输出；对于振荡器来说是右输出）

## "ModulationMatrix.h"

```cpp
#define OSC_FO_MOD_RANGE 2      // 2 半音
#define OSC_HARD_SYNC_RATIO 4  // 4
#define OSC_PITCHEND_MOD_RANGE 12 // 12 Hz-等待，12 半音
#define OSC_FC_MIN 20                // 20 Hz
#define OSC_FC_MAX 20480             // 2048 kHz
#define OSC_ULSEWIDTH_MIN 2         // 2%
#define OSC_ULSEWIDTH_MAX 98        // 98%
```

```cpp
class CModulationMatrix {
public:
    CModulationMatrix(void);
    virtual ~CModulationMatrix(void);

    // 共享矩阵核心
    modMatrixRow** m_ppMatrixCore;
    int m_nSize;

    void clearMatrix();
    void clearSources();
    void clearDestinations();
};
```

```cpp
class COscillator {
public:
    COscillator(void);
    virtual ~COscillator();

    // 调制矩阵
    CModulationMatrix* m_pModMatrix;

    // 我们读取的源
    UINT m_uSourceFo;
    UINT m_uSourceWidth;
    UINT m_uSourceAmp;

    // 我们写入的目标
    UINT m_uDestOutput1;
    UINT m_uDestOutput2;

    // 振荡器运行标志
    bool m_bNoteOn;

    virtual void updateOscillator();
};
```

你在构造函数中初始化变量。调制矩阵指针为 NULL，在我们的对象中总是可选的。如果此指针不为空，我们知道使用了该矩阵。

## COscillator 派生类

```cpp
inline void updateOscillator()
{
    // --- 噪声源忽略 LFO 模式
    if(m_uWaveform == rsh || m_uWaveform == qrsh)
        m_uLFMode = free;
    
    // --- 调制矩阵
    // --- 从矩阵获取
    if (m_pModulationMatrix) {
        // --- 这些置零
        m_dFMod = m_pModulationMatrix->m_Destinations[m_uSourceFo];
        m_dPWMod = m_pModulationMatrix->m_Destinations[m_uSourceWidth];
        // --- 幅度调制 0->1
        // --- 振荡器输出反转
        m_dAmpMod = m_pModulationMatrix->m_Destinations[m_uSourceAmp];
        m_dAmpMod = 1.0 - m_dAmpMod;
    }
}
```

```cpp
// --- 完成完整的频率调制
m_dFo = m_d0scFo*m_dFoRatio*pitchShiftMultiplier(m_dFoMod +
    m_dPitchMod +
    m_noctave*12.0 +
    m_nSemitones +
    m_nC/100.0);
```

等等...

功能。对于 LFO，目标输出是普通和四相，而振荡器则以左右对的形式写入输出。

```cpp
COscillator::COscillator(void)
{
    // --- 初始化变量
    m_dSampleRate = 44100;

    <SNIP SNIP SNIP>

    // --- 用于硬同步
    m_pBuddyOscillator = NULL;
    m_bMasterOsc = false;

    // --- 默认调制矩阵初始化
    m_pModulationMatrix = NULL;

    // --- 除非使用调制矩阵，否则都是断开的
    m_uSourceFo = DEST_NONE;
}
```
