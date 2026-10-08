

# 调制层

在查看调制矩阵对象之前，我们需要先考虑调制层。对于 NanoSynth 来说，非常简单：LFO 和 EG 调制振荡器、滤波器和 DCA。这里只有一层调制。但如果我们为 NanoSynth 添加了另一个名为 LFO2 的 LFO，并如图 8.7 所示用来调制 LFO1 的频率会怎样？那么我们就有了两层，并且需要使用两次调制矩阵。需要记住的一点是，目标（destinations）定义了层数。

调制矩阵的设计最多仅使用两层；不过你可以轻松地修改它以使用你需要的任意层数。我们将从在 NanoSynth 中实现层 1 调制开始。在章节后面的部分，我们将添加一些发生在层 0 的高级 MIDI 调制。

![](img/b42d0dca53f4a889d8162d55f7c8c05d_468_0.png)

图 8.7：(a) 层 1 的目标点是引擎组件。(b) 层 0 的目标点是层 1 的源（Sources）。

图 8.8 显示了一个概念性的 CMod 类图，而表 8.2 列出了成员变量和函数。该对象相当简单；成员变量包括源（sources）和目标（destinations）的数组、指向矩阵的指针以及一个指示矩阵行数的变量。成员函数的命名非常直观；最重要的函数有：

- addMatrixRow()——在检查该行已存在后，向矩阵添加新创建的行。
- doMod()——执行遍历行并将源累积到目标的操作。

大部分功能实现在 `ModulationMatrix.h` 文件中，因此请查看该文件。第一部分是成员声明。注意，矩阵是静态声明的，其大小为每个源都调制每个目标时的最坏情况最大。没有 `removeMatrixRow()` 函数——你做不到。在设计合成器时，你只需要填充路由所需的行即可。未使用的行不会被处理。

```cpp
class CModulationMatrix{
public:
    CModulationMatrix(void);
    ~CModulationMatrix(void);
protected:
    // --- 调制行矩阵，具有最坏情况的大小（每个源
    // 调制每个目标
    // 这是一个双指针，因为它是动态分配的 (*)
    // 并指向指针数组(**)
    modMatrixRow** m_ppMatrixCore;
```

**图 8.8：** CModulationMatrix 的概念类图，显示了其成员属性；在此示例中，矩阵大小为八。

**表 8.2：** CModulationMatrix 变量和函数。

| CModulationMatrix | 矩阵核心 |
|--- |--- |
| m_ppMatrixCore | pRow0 -> |
| m_nSize = 8 | pRow1 -> |
| m_dSources[] | pRow2 -> |
| LFO1 Out | ... |
| LFO2 Out | ... |
| 等... | ... |
| m_dDestinations[] | pRow7 -> |
| OSC1 Fo | 0x00000000 |
| OSC2 Fo | 0x00000000 |
| 等... | |

# CModulationMatrix 成员变量

| 类型 | 变量名 | 描述 |
|---|---|---|
| modMatrixRow** | m_ppMatrixCore | 指向矩阵行指针数组的指针——核心 |
| int | m_nSize | 核心中空行的数量 |
| double [] | m_dSources | 源寄存器数组 |
| double [] | m_dDestinations | 目标寄存器数组 |

# CModulationMatrix 成员函数

| 函数名 | 描述 |
|---|---|
| getMatrixCore | 返回矩阵核心的指针 |
| setMatrixCore | 设置矩阵核心指针 |
| getMatrixSize | 返回空行的数量 |
| clearMatrix | 清空核心矩阵，不删除指针 |
| clearSources | 清空源数组 |
| clearDestinations | 清空目标数组 |
| addMatrixRow | 添加新行，在添加前检查行是否存在 |
| matrixRowExists | 检查行是否存在 |
| createMatrixCore | 创建新矩阵；删除现有核心 |
| deleteMatrix | 删除行然后删除矩阵数组 |
| enableDestinationRow | 启用或禁用现有行以实现灵活路由 |
| checkDestinationLayer | 检查目标是否在层 N 组中 |
| doModulationMatrix | 执行矩阵操作 |

```cpp
// --- 当前大小取决于添加的行数
int m_nSize;
```

public:

```cpp
// sources：每个源 (LFO, EG, ETC) 写入输出值的地方
double m_dSources[MAX_SOURCES];
```

```cpp
// destinations：从这里读取新计算的调制值
double m_dDestinations[MAX_DESTINATIONS];
```

# getModMatrixCore() 和 setMatrixCore()

`getModMatrixCore()` 和 `setMatrixCore()` 只是获取和设置指针；在设置期间，如果矩阵已存在则将其删除。矩阵核心在构造过程中动态分配。`getMatrixSize()` 只是遍历行并计算大小。

```cpp
// --- 获取矩阵核心
modMatrixRow** getModMatrixCore(){return m_ppMatrixCore;}

// --- 设置矩阵核心
void setModMatrixCore(modMatrixRow** pModMatrix)
{
    if(m_ppMatrixCore)
    {
        for(int i=0; i<m_nSize; i++)
        {
            // 删除指针
            modMatrixRow* pRow = m_ppMatrixCore[i];
            delete pRow;
            m_nSize--;
        }
    }
    m_nSize = 0;
    delete [] m_ppMatrixCore;
}

m_ppMatrixCore = pModMatrix;
m_nSize = getMatrixSize();
```

clearSources() 和 clearDestinations()

随后是源数组、目标数组以及矩阵核心的简单清空方法。每次调制矩阵运行时都会调用 `clearDestinations()`，因为它会将值累积到目标数组中。

```cpp
// 在初始化时调用一次
inline void clearSources()
{
    memset(m_dSources,0,sizeof(m_dSources));
}
```

```cpp
// 每次遍历矩阵时调用
inline void clearDestinations()
{
    memset(m_dDestinations,0,sizeof(m_dDestinations));
}
```

# addMatrixRow() 和其他

`addMatrixRow()` 函数添加行，但使用 `matrixRowExists()` 函数确保其不存在。行永远不会重复。`deleteMatrix()` 函数销毁所有指针和数组。`enableDestinationRow()` 函数使用 `modRow` 结构体中的布尔标志来启用或禁用矩阵行。

```cpp
inline void addMatrixRow(modMatrixRow* pRow)
{
    if(!m_ppMatrixCore)
        createMatrixCore();

    // 如果不存在则添加
    if(!matrixRowExists(pRow->uSourceIndex, pRow->uDestinationIndex))
    {
        m_ppMatrixCore[m_nSize] = pRow;
        m_nSize++;
    }
    else
        delete pRow;
}

inline bool matrixRowExists(UINT uSourceIndex, UINT uDestinationIndex)
{
    if(!m_ppMatrixCore) return false;

    for(int i=0; i<m_nSize; i++)
    {
        modMatrixRow* pRow = m_ppMatrixCore[i];

        // 寻找匹配的索引源/目标对
        if(pRow->uSourceIndex == uSourceIndex &&
            pRow->uDestinationIndex == uDestinationIndex)
        {
            return true;
        }
    }
    return false;
}
```

```cpp
inline void deleteMatrix(){
    if(!m_ppMatrixCore) return;

    for(int i=0; i<m_nSize; i++)
    {
        // 删除指针
        modMatrixRow* pRow = m_ppMatrixCore[i];
        delete pRow;
        m_nSize--;
    }
    m_nSize = 0;
    delete [] m_ppMatrixCore;
    m_ppMatrixCore = NULL;
}
```

# checkDestinationLayer()

`checkDestinationLayer()` 函数检查目标索引以判断其是层 0 还是层 1 目标。如果你愿意，可以在这里定义更多层。现在你应该明白为什么目标枚举将层 0 目标放在前面——你只需要检查目标是否在组第一个和最后一个枚举的边界内。

最后，对象的方法在 `deModificationMatrix()` 函数中。参数是目标层。参考 `modMatrix` 结构体；每一行指向这些结构之一，且每一行都包含了所有的

