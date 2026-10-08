
按照如下方式创建并添加这四个控件；首先调用基类并向其传递 FUnknown 指针，然后创建并添加参数：

The result PLUGIN_API Controller::initialize(FUnknown* context)
`RangeParameter` 构造函数从控制表以及索引值中获取值——我们在枚举中设置了这些。

```cpp
// --- 基类执行其基础操作
tresult result = EditController::initialize(context);
// 现在定义控件
if (result == kResultTrue) {
    // 初始化参数
    Parameter* param;
    // 创建一个音量参数
    param = new RangeParameter(USTRING("Volume"),
        VOLUME_DB,
        USTRING("dB"), /* 单位 */
        MIN_OUTPUT_AMPLITUDE_DB, /* LOW */
        MAX_OUTPUT_AMPLITUDE_DB, /* HIGH */
        DEFAULT_OUTPUT_AMPLITUDE_DB); /* DEF */

    // 设置 UI 的有效数字
    param->setPrecision(1);

    // 将其添加到容器
    parameters.addParameter(param);
}
```

枚举。你可以很容易看到这个构造函数是如何与表格和枚举关联的。注意最小、最大和默认值来自 `SynthLimits` h 头文件。

```cpp
#define MIN_OUTPUT_AMPLITUDE_DB
96.0
#define MAX_OUTPUT_AMPLITUDE_DB
24.0
#define DEFAULT_OUTPUT_AMPLITUDE_DB
0.0
```

创建控件后，`setPrecision()` 方法告诉 UI 小小数点后显示多少位有效数字，因此在这里将显示一位，例如 -21.6。最后，使用 `addParameter()` 方法将新对象添加到容器中。现在看 Octave 控件：

```cpp
param = new RangeParameter(STRING("Octave"),
OCTAVE,
STRING(""),
MIN_OCTAVE,
MAX_OCTAVE,
DEFAULT_OCTAVE);
/* 控制名称 */
/* 索引 */
/* 单位 */
/* LOW */
/* HIGH */
/* DEF */
// 整数，无有效数字
param->setPrecision(0); // <---这是一个整数 (int)
// 添加到容器
parameters.addParameter(param);
```

非常直观；我们将参数设置为 0，这表示整数显示——注意控件仍将传输从 0.0 到 1.0 的原始值。对数刻度参数需要更多的设置工作。在对象方法之外的 .cpp 文件顶部，你定义了缩放：

前四个参数显示了控件从 0.0 到 1.0 的范围映射，将映射到 80.0 到 18000.0，最后两个参数显示了中心锚点——你可以将这些参数理解为“当原始值为 0.5 时，控件将显示为 1800”。最后两个参数允许你创建具有扩展、压缩或更低范围的准对数控件。

```cpp
// 这些定义在 SynthParamLimits.h 中
#define MIN_UNIPOLAR 0.0
#define MAX_UNIPOLAR 1.0
#define DEFAULT_UNIPOLAR 0.0
```

对于 `LogScaleParameter`，你必须在一个单独的函数中设置默认值，并且你只能设置归一化（原始）值。要此此，请使用名为 `toNormalized()` 的辅助方法，它会为你转换值。这在这里特别重要，因为控件是对数性的，且映射不是线性的。在这种情况下，我们将控件设置了默认值 `DEFAULT_FILTER_FC`。

最后，我们可以使用 `StringListParameter` 来定义滤波器类型（Filter Type）控件。首先，你创建参数，然后加载字符串：

注意字符串索引——记住在 VST3 中，由你来协调整数值（0,1,2...）与字符串（LPF,HPF,BPF...）。

## 2.24 VST3 控制器序列化

### 第四步：在 componentState() 方法中实现序列化-ReadState()

对于 Controller，`componentState()` 方法是序列化读取方法。Processor 使用稍有不同的函数名称，我们稍后介绍。在这两个对象中，传递给函数的参数都是 `IBState` 指针。该接口允许对二进制文件进行读写。我们将存储和加载你的变量，它们的类型为上述列出的，如 `int` 和 `UINT`。`IBState` 接口提供了相对简单的方法来写入值。在这种情况下，我们将读取值。这段代码最需要记住的一点是，变量读取和写入顺序必须完全一致，否则你的变量将无法被正确读取或写入。由于我们的数据类型是 double、int 的混合体

```cpp
#define MIN_FILTER_FC 80.0
#define MAX_FILTER_FC 18000.0
#define DEFAULT_FILTER_FC 10000.0
#define FILTER_RAW_MAP 0.5
#define FILTER_COOKED_MAP 1800.0
// 这为滤波器 Fc 控制定义了对数缩放
LogScale<ParamValue> filterLogScale(MIN_UNIPOLAR), /* GUI MIN */
MAX_UNIPOLAR, /* GUI MAX */
MIN_FILTER_FC, /* LO */
MAX_FILTER_FC, /* HI */
FILTER_RAW_MAP, /* 0.5 */
FILTER_COOKED_MAP); /* 1800 */
// 设置归一化值
param->setNormalized(param->toNormalized(DEFAULT_FILTER_FC));
// 设置有效数字
param->setPrecision(1);
// 添加到容器
parameters.addParameter(param);

StringListParameter* enumParam = new StringListParameter(STRING("Filter Type"),
/* 控制名称 */
/* 索引 */
/* 单位 */
// 添加字符串
enumParam->addString(STRING("LPF"));
enumParam->addString(STRING("HPF"));
enumParam->addString(STRING("BPF"));
// 添加到容器
parameters.addParameter(enumParam);
```
