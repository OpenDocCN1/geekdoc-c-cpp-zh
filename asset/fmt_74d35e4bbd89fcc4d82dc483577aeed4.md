
`_Floatn complex acghf(_Floatn complex z);`

`_Floatn complex casinhf(_Floatn complex z);`

`_Floatn complex acinhf(_Floatn complex z);`

`_Floatn complex catanhf(_Floatn complex z);`

`_Floatn complex atanhf(_Floatn complex z);`

`_Floatn complex cosh(_Floatn complex z);`

`_Floatn complex acosh(_Floatn complex z);`

`_Floatn complex csinh(_Floatn complex z);`

`_Floatn complex asinh(_Floatn complex z);`

`_Floatn complex tanh(_Floatn complex z);`

`_Floatn complex ctanhf(_Floatn complex z);`

### 7.3.7 指数和对数函数

`_Floatn complex expf(_Floatn complex z);`

`_Floatn complex acexpf(_Floatn complex z);`

`_Floatn complex clogf(_Floatn complex z);`

`_Floatn complex aclogf(_Floatn complex z);`

### 7.3.8 幂和绝对值函数

`_Floatn complex absf(_Floatn complex z);`

`_Floatn complex cabsf(_Floatn complex x);`

`_Floatn complex powf(_Floatn complex x, _Floatn complex y);`

`_Floatn complex cpow(_Floatn complex x, _Floatn complex y);`

`_Floatn complex sqrtf(_Floatn complex z);`

`_Floatn complex csrtf(_Floatn complex z);`

### 7.3.9 操作函数

`_Floatn complex cargf(_Floatn complex z);`

`_Floatn complex argf(_Floatn complex z);`

`_Floatn complex imagf(_Floatn complex z);`

`_Floatn complex acimagf(_Floatn complex z);`

`_Floatn complex cmplf(_Floatn complex x, _Floatn complex y);`

`_Floatn complex cnpy(_Floatn complex x, _Floatn complex y);`

`_Floatn complex conjf(_Floatn complex z);`

`_Floatn complex conjmf(_Floatn complex z);`

`_Floatn complex cprojf(_Floatn complex z);`

`_Floatn complex cprojmf(_Floatn complex z);`

`_Floatn complex crealf(_Floatn complex z);`

`_Floatn complex creall(_Floatn complex z);`

对于“未来库” `<complex.h>` (7.3) 中列出的函数，双后缀扩展为 `_fN` 和 `_fNx`。

# H.10 浮点环境

子类将浮点环境（7.6）的影响扩大到本附录中指定的类型和格式。相同的浮点状态标志用于所有类型（包括本附录中引入的）以及 ISO/IEC 60559 交换格式。通过 `fetround` 和 `fesetround` 访问的动态舍入模式适用于二进制浮点类型以及标准类型，以及进制交换格式。同样，通过 `fe_getround` 和 `fe_setround` 访问的动态舍入模式适用于所有类型（包括本附录中引入的）以及进制交换格式。表 7.1 描述了受常量舍入模式影响的标准类型，适用于二进制浮点类型。`<math.h>` 列出的每个函数族指示二进制浮点类型（例如，`acos` 族包括 `acos_f`）。表 7.2 描述了受常量舍入模式影响的进制浮点类型，`<math.h>` 每个函数族指示进制浮点类型（例如，`acos` 族包括 `acos` 和 `acosnx`）。`denormN` 和 `strN` 函数受这些常量舍入模式的影响。

# H.11 <math.h>

### H.11.1 通用

此子类指定了扩展浮点的类型、函数和宏，通常对应于 F.12 中的。所有分类宏（7.12.4）和比较宏（7.12.18）自然扩展到交换和扩展浮点类型。对于比较宏，如果参数的值不是另一个值的子集（或相等），则行为未定义。此子类还指定了 ISO/IEC 60559 非进制交换格式的编码函数。对于实现提供的每个交换或扩展浮点类型，`<math.h>` 定义关联类型和宏并声明关联函数（参见 H.8）。相反，对于实现未提供的每个类型，`<math.h>` 不定义关联类型或宏，除非另有说明。类型

```
float_t
double_t
```

在 7.12 中是 `long_double_t`，对于每个支持的类型 `_FloatN`，类型 `_FloatN_t`，对于每个支持的类型 `_DecimalN`，类型 `_DecimalN_t`，这些是浮点类型，例如：

- `long double` 是 `long_double_t` 的子集；
- `_FloatN` 是 `_FloatN` 的子集；
- `_DecimalN` 是 `_DecimalN` 的子集；
- `double_t` 是 `long_double_t` 的子集；
- 当 `M < N` 时 `_FloatM_t` 是 `_FloatN_t` 的子集；
- 当 `M < N` 时 `_DecimalM_t` 是 `_DecimalN_t` 的子集。

如果 `FLT_RADIX` 为 2 且 `FLT_EVAL_METHOD` (H.3) 非负，则对应标准或二进制浮点类型其范围和精度由 `FLT_EVAL_METHOD` 指定，用于标准或二进制浮点类型的运算和常量。如果 `DEC_EVAL_METHOD` (H.3) 非负，则对应进制浮点类型的类型其范围和精度由 `DEC_EVAL_METHOD` 指定，用于进制浮点类型的运算和常量。

示例 支持的和二进制浮点类型如表 H.6 所示：

| 类型 | ISO/IEC 6059 格式 |
| :--- | :--- |
| `_Float16` | binary16 |
| `_Float32` | binary32 |
| `double`, `_Float64`, `_Float32x` | binary64 |
| `long_double`, `_Float64x` | 80-bit binary64-extended |
| `_Float128` | binary128 |

表 H.6 — 示例支持类型

表 H.7 给出了给定值 m `FLT_EVAL_METHOD` 下带有 `_t` 后缀的类型：

| _t 类型 | | 0 | 2 | 32 |
| :--- | :--- | :--- | :--- | :--- |
| `_Float16_t` | float | double | long double | `_Float32` |
| `_float_t` | float | double | long double | float |
| `_Float32_t` | `_Float32` | double | long double | `_Float32` |
| `_double_t` | double | double | long double | double |
| `_Float64_t` | `_Float64` | `_Float64` | long double | `_Float64` |
| `long.double.t` | long double | long double | long double | long double |
| `_Float128_t` | `_Float128` | `_Float128` | `_Float128` | `_Float128` |

表 H.7 — `_t` 类型（垂直）与 m（水平）的的关系

© ISO/IEC 2024 — 版权所有

576

# ISO/IEC 9899:2024(en)

| _t type | 64 | 128 | 32 | 65 |
| :--- | :--- | :--- | :--- | :--- |
| `_Float16_t` | `_Float64` | `_Float128` | `_Float32x` | `_Float64x` |
| `float_t` | `_Float64` | `_Float128` | `_Float32x` | `_Float64x` |
| `_Float32_t` | `_Float64` | `_Float128` | `_Float32x` | `_Float64x` |
| `double_t` | double | `_Float128` | double | `_Float64x` |
| `_Float64_t` | `_Float64` | `_Float128` | `_Float64` | `_Float64x` |
| `Long_double_t` | long double | `_Float128` | long double | long double |
| `_Float128_t` | `_Float128` | `_Float128` | `_Float128` | `_Float128` |

## H.11.2 宏

此子类在 7.12 中添加了如下宏。

这些宏

```
HUGE_VAL_FN
HUGE_VAL_DN
HUGE_VAL_FN
HUGE_VAL_DNX
```

分别展开为表示类型 *FloatN*、*DecimalN*、*FloatNx* 和 *DecimalNx* 的表达式，表示正无穷大。

这些宏

```
FP_FAST_FMAFN
FP_FAST_FMADN
FP_FAST_FMANX
FP_FAST_FMADNX
```

是 *FloatN*、*DecimalN*、*FloatNx* 和 *DecimalNx* 类型的 `FP_FAST_FMA` 对应物。后续列表中的宏是 `FP_FAST_FADD`、`FP_FAST_FADDL`、`FP_FAST_DADDL` 的互换且扩展浮点类型对应物，这些宏

对于 `M < N`，这些宏

```
FP_FAST_FADDFN
FP_FAST_FSUBFN
FP_FAST_FMULFN
FP_FAST_FHDIVFN
FP_FAST_FMAFN
FP_FAST_FSQRTFN
FP_FAST_DADDDN
FP_FAST_DHSUBDN
FP_FAST_DMDULDN
FP_FAST_DDIVDN
FP_FAST_DFMAWDN
FP_FAST_DSQRTDN
```

刻画了相应的函数，其参数为 N 的互换浮点类型，且返回类型为 M 的互换浮点类型。

对于 `M ≤ N`，这些宏

```
FP_FAST_FADDNX
FP_FAST_FSUBNX
FP_FAST_FMULFX
FP_FAST_FHDIVFX
FP_FAST_FMAFX
FP_FAST_FSQRTNX
```

```
FP_FAST_DYADDVX
FP_FAST_DMSUBVX
FP_FAST_DMMULDVX
FP_FAST_DMIDVX
FP_FAST_DFMFADVX
FP_FAST_DSQRTDX
```

刻画了相应的函数，其参数为扩展宽度 N 的扩展浮点类型，且返回类型为宽度 M 的互换浮点类型。

对于 `M < N`，这些宏

```
FP_FAST_FXADDVX
FP_FAST_FXMSUBVX
FP_FAST_FXMULDVX
FP_FAST_FXDIVVX
FP_FAST_FXMAVFX
FP_FAST_FXSQRTVX
FP_FAST_DXADDVX
FP_FAST_DXMSUBVX
FP_FAST_DXMULDVX
FP_FAST_DXDIVVX
FP_FAST_DXMFADVX
FP_FAST_DXSQRDTX
```

刻画了相应的函数，其参数为扩展宽度 N 的互换浮点类型，且返回类型为扩展宽度 M 的扩展浮点类型。

对于 `M < N`，这些宏

```
FP_FAST_FXADDVX
FP_FAST_FXMSUBVX
FP_FAST_FXMULDVX
FP_FAST_FXDIVVX
FP_FAST_FXMFADVX
FP_FAST_FXSQRTVX
FP_FAST_DYADDVX
FP_FAST_DYMSUBVX
FP_FAST_DYMULDVX
FP_FAST_DYDIVVX
FP_FAST_DYMFADVX
FP_FAST_DYSQRDTX
```

刻画了相应的函数，其参数为扩展宽度 N 的扩展浮点类型，且返回类型为扩展宽度 M 的扩展浮点类型。

## H.11.3 函数

此子句向 7.12 中的子句中添加了以下函数。

### 7.12.5 三角函数
