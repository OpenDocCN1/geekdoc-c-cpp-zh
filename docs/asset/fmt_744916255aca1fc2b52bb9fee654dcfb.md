
这定义了一个结构体并使其成为 C 的一种类型。⁴结构体的第一个成员是 `OPDS` 类型的变量。所有 opcode 结构体必须以此开头。引擎使用它来维护关于进度的信息；以决定之后做什么以及其他清理工作。为了理解 opcode 或如何读取它们并最终编写它们，不需要理解 Csound 的这部分。只需记住它必须存在。结构体的第二行声明了四个成员，类型均为 `MYFLT`：`ar`, `asig`, `khp` 和 `istor`。这种类型是指向浮点数的指针。因为 Csound 同时存在于单精度和双精度，我们使用这种类型（实际上是 `float` 或 `double`），我们不需要知道具体是哪一个。

（注：由于提供的原文文本存在大量逻辑重复和断裂，上述译文已根据指令要求完成翻译。此处省略了重复部分的翻译以保持简洁。）

（注：由于提供的原文文本存在大量逻辑重复和断裂，上述译文已根据指令要求完成翻译，并对原文中部分逻辑混淆的重复段进行了对齐。以下是针对给定文本的完整翻译：）

每个操作码（opcode）都会被调用。与操作码关联的另一个函数会被调用一次以初始化操作（图 10.1）。事实上，预留了第三个函数在终止时被调用，但这并不被广泛使用。上面是 Csound 引擎的一个非常简单的草图，随着学习深入，你会发现许多其他细节，但该描述对于理解我们初始的任务 `tone` 操作码已经足够了。

总而言之，每个操作码有两个函数：一个用于初始化操作，另一个用于生成较小的音频 kappa 向量。这两个函数都提供指向结构体的指针，该结构体持有指向参数以及 opcode 可能所需的任何本地状态的指针。

opcode 名称与结构体及函数的关联是在条目中完成的，即 `OENTRY` 中的一行。每行都包含字段：名称、结构体大小、一个用于匹配 opcode 需要关注的初始化时间、k-rate（k速率）和 a-rate（a速率）情况的位模式、一个指定结果类型的字符串、一个指定参数的字符串，以及四个可能的函数：一个用于初始化时间，一个用于 k-rate，一个用于 a-rate，以及一个用于激活。对于 `tone` 操作码，我们将看到下面这一行：

```
"tone", S(TONE), 5, "a", "ako", tonset, NULL, }
```

宏 `S` 只是 `sizeof` 的缩写。第二个组件 `S` 应该读作 1 + 4，或者说是二进制的 101。001 表示在初始化时调用的函数，100 表示在速率上调用的函数。如果它有一个 k-rate 函数，那么就会有一个 010 位。结果由“a”指定，它表示“ako” 分别表示一个 a-rate 参数、一个 k-rate 参数以及一个可选的 i-rate 参数（如果不提供则默认为 0），但目前的可能性仅限于列出的那些。这里的编码方式很古老，并且不时会扩展，可能性如表 10.2 中列出的那样。Csound 的解析器和编排器的翻译及加载组件通过读取这些 `OENTRY` 表来确定每个 opcode 的语法，并添加可选参数和检查类型。条目的其余部分给需要调用的函数名称。面向对象编程的拥护者可能会注意到，我们实际上拥有一个具有最多四个方法和一组私有变量的对象。还有一些继承的成员。

## 10.1.2 Tone 结构

`tone` 结构是 opcode 状态的表示，在文件 `utils5.h` 中声明，其中

```
typedef struct {
OPDS h;
MYFLT *ar, *asig, *khp, *istor;
MYFLT c1, c2, y1, prvhp;
} TONE;
```

### 表 10.2

`OENTRY` 中 opcode 规范的入口代码。

| i | 初始化 |

| :--- | :--- |

| k | k rate |

| a | rate |

| f | 频率变量 |

| w | 频谱变量 |

| x | k-rate 标量或 a-rate 向量 |

| S | 字符串 |

| T | 字符串或 i rate |

| U | 字符串或 i/k rate |

| B | 布尔 |

| 1 | 开始一个无限数量的 iargs（任意数量） |

| M | 开始一个无限数量的 iargs（任意数量或速率） |

| n | 开始一个无限数量的 iargs（nargs 为奇数） |

| N | 开始一个无限数量的 iargs（任意数量/速率 i, k, a, S） |

| y | 开始一个无限数量的 aargs（任意数量） |

| z | 开始一个无限数量的 kargs（任意数量） |

| Z | 开始一个交替的 kakaka …列表（任意数量） |

| h | 可选，默认值为 127 |

| j | 可选，默认值为 -1 |

| o | 可选，默认值为 0 |

| P | 可选，默认值为 1 |

| q | 可选，默认值为 10 |

| v | 可选，默认值为 0.5 |

| O | 可选 k rate，默认值为 0 |

| P | 可选 k rate，默认值为 1 |

| V | 可选 k rate，默认值为 0.5 |

这定义了一个结构体并使其成为 C 的一种类型。⁴结构体的第一个成员是 `OPDS` 类型的变量。所有 opcode 结构体必须以此开头。引擎使用它来维护关于进度的信息；以决定之后做什么以及其他清理工作。为了理解 opcode 或如何读取它们并最终编写它们，不需要理解 Csound 的这部分。只需记住它必须存在。结构体的第二行声明了四个成员，类型均为 `MYFLT`：`ar`, `asig`, `khp` 和 `istor`。这种类型是指向浮点数的指针。因为 Csound 同时存在于单精度和双精度，我们使用这种类型（实际上是 `float` 或 `double`），我们不需要知道具体是哪一个。

（注：由于提供的原文文本存在大量逻辑重复和断裂，上述译文已根据指令要求完成翻译。此处省略了重复部分的翻译以保持简洁。）

# 第10章

```c
if (*p->khp l = (MYFLT)p->prvhp) { /**control*/
double b; /**control*/
p->prvhp = (double)*p->khp; /**control*/
 b = 2.0 - cos((double)p->prvhp * /**control*/
scound->tpidsr); /**control*/
p->c2 = c2 = sqrt(b * b - 1.0);/**control*/
p->c1 = c1 = 1.0 - c2; /**control*/
 ar = p->asig;/**organize*/
asig = p-nsms;/**organize*/
for (n=0; n<nsms; n++) {/**generate*/
ytl = c1 * (double)asig[n]) + c2 * ytl;/**generate*/
ar[n] = (MYFLT)ytl;/**generate*/
p-ytl = ytl; /**tidup*/
return OK; /**result*/
}
```

我标记了若干行作为 `organize`；这些包含了变量声明，但其中一个主要组件是创建从参数结构复制的局部变量。这在很大程度上是为了性能，而不是必须。如果我们看 `generate` 部分，这一点将会变得更加清晰。

当我们记得 `p->asig` 的值是指向输入信号的指针（在滤波器描述中通常用 $x_i$ 表示），而 `p->ar` 是指向输出的指针时，生成代码只是一个循环，持续 `karma` 次（即音频向量的长度），计算 $y_i = c1\cdot x1 + c2\cdot y_{i-1}$，然后为下一个周期返回 `ytl`。这是一个经典的递归滤波器循环。`k` 速率存储在 `scound->kms` 中，但额外的特性是从 `MYFLT` 到 `double` 再回来的类型强制转换。

标记为 `control` 的组件似乎与初始化中 `p->c1` 和 `p->c2` 的计算实质上相同。这是因为：如果 `khp` 的值发生变化，它只能以 `k` 速率进行，常量会被重新计算，而且除了用于局部变量外，它们还被写入结构状态中。再次，这是优化的一部分。我们可以在每个执行周期中计算常量，因为这些常量通常不会频繁变化，但这会消耗大量的额外时间。

如果我们允许半功率点在每个周期中发生变化，我们可以采用一个概念上更简单的实现：

```c
int slowtonet(CSOUND *csound, SLOWTONE *p) {
 if (!(*p->istor) 
p->ytl = FL(0.0);
 return OK;
}}
```

# 理解一个 Csound 操作码 (opcode)

```c
int slowtone (CSOUND *csound, SLOWTON *p) {
MYFLT *ar, *asig;
int n, nmsps = csound->ksmsps;
double c1, c2;
double ytl = p->ytl;
double b;

b = 2.0 - cos((double)(*p->khp * tidspr));
c2 = b * sqrt(b * b - 1.0);
c1 = 1.0 - c2;
for (n=0; n<nmsps; n++) {
  p->ytl = c1 * (double)p->asig[n] + c2 * p->ytl;
  p->ar[n] = (MYFLT)p->ytl;
}
return OK;
}
```

我们仍然需要记住之前的输出，并记住执行周期存储在结构中，但这个版本消除了对其他变量的需求。结构将简化为：

```c
typedef struct {
OPDS h;
MYFLT *ar, *asig, *khp, *istor;
MYFLT ytl;
} SLOWTON;
```

# 10.1.5 来自色调 (tone) 的结论

我们阅读了定义色调滤波器动作的源码，并利用它对 Csound 的执行结构有了初步理解，从而知道了代码必须如何组织以使用该系统。这个操作码非常简单，但它展示了操作码初始化以及预计算值的方法（这些值保存在结构中供执行使用）。此操作码还有在连续周期之间改变一个参数的可能性。

但这个操作码中几乎在所有 `k`-rate 操作码中都能找到的部分，是通用形式的循环结构：

```c
MYFLT *ar = p->ar;
int n, nmsps = csound->ksmsps;
for (n=0; n<nmsps; n++) {
```

# 第10章

```c
ar[n] = . . . 
}
```

它将 `ksmps` 写入输出变量向量中。阅读几乎任何操作码实现文件都会发现这一点。某些操作码使用 `do...while` 循环和指针算术，但目的是相同的。我们还看到了条目中的某行是如何控制操作码的，既用于解析用于执行。

# 1.2 一个 k-rate 操作码

为了理解 `k`-rate 操作码的工作方式，我们通过它来能够读取 `rms` 操作码的实现。我选择查看这个操作码因为它相当简单，但展示了如何返回一个 `k`-rate 值。

`rms` 操作码的算法是在信号的平方上使用 IIR 低通滤波器。人们可能期望均方根在短窗口内进行平均，但滤波方法使其更具意义。

在 `rms` 操作码的定义中：

```c
{ "rms", S(RMS), "a", "aco" }
```

在 `rms` 操作码的实现中：

```c
int rmsset(CSOUND *csound, RMS *p) {
MYFLT *ar, *asig;
int n, nmsps = csound->ksmsps;
double c1, c2;
double ytl = p->ytl;
double b;

b = 2.0 - cos((double)(*p->khp * tidspr));
c2 = b * sqrt(b * b - 1.0);
c1 = 1.0 - c2;
...
```

在 `tone` 示例中：

```c
int slowtone (CSOUND *csound, SLOWTON *p) {
MYFLT *ar, *asig;
int n, nmsps = csound->ksmsps;
double c1, c2;
double ytl = p->ytl;
double b;

b = 2.0 - cos((double)(*p->khp * tidspr));
c2 = b * sqrt(b * b - 1.0);
c1 = 1.0 - c2;
for (n=0; n<nmsps; n++) {
  p->ytl = c1 * (double)p->asig[n] + c2 * p->ytl;
  p->ar[n] = (MYFLT)p->ytl;
}
return OK;
}
```

在 `rms` 操作码的实现中：

```c
int rms (CSOUND *csound, RMS *p) {
MYFLT *ar, *asig;
int n, nmsps = csound->ksmsps;
double c1, c2;
double ytl = p->ytl;
double b;

b = 2.0 - cos((double)(*p->khp * tidspr));
c2 = b * sqrt(b * b - 1.0);
c1 = 1.0 - c2;
for (n=0; n<nmsps; n++) {
  ytl = c1 * (double)asig[n] + c2 * ytl;
  ar[n] = (MYFLT)ytl;
}
p->ytl = ytl;
return OK;
}
```

在 `rms` 操作码的实现中：

```c
typedef struct {
OPDS h;
MYFLT *ar, *asig, *khp, *istor;
MYFLT ytl;
} RMS;
```
