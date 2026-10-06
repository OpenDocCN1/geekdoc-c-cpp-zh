
头文件将包含 `BREAKPOINT` 函数的定义以及 `BREAKPOINT` 相关函数 `get_breakpoints` 和 `maxpoint` 的原型。由于 `get_breakpoints` 的参数之一使用了 `FILE` 类型，请在 `breakpoints.h` 顶部添加 `#include <stdio.h>`。同样，我们从 `breakdur.c`（见第一章）将两个 `BREAKPOINT` 相关函数的代码拷贝到 `breakpoints.c`。

注意 `breakpoints.c` 使用了几个标准库函数（`malloc`, `realloc` 和 `free`），因此 `breakpoints.c` 还需要 `#include <stdlib.h>`。最后，将 `breakpoints.c` 添加到 Makefile。该文件成为 `sfpan` 的新依赖项：

```
sfpan: sfpan.c breakpoints.c /lib/libports.a

$(CC) -o sfpan breakpoints.c $(INCLUDES) $(LIBS)
```

我们现在准备好设计程序。这确定了每个阶段可能需要的内容。某些材料已经就绪，另一些必须从头实现。

在阶段 1（定义变量），某些元素是明确的。我们正在读取一个作为 `fp` 打开的文件，因此我们需要一个 `FILE*` 变量，还需要其他存储断点文件大小的变量，以及指向断点本身的指针（见第一章中的 `breakdur.c`）：

```
FILE* fp = NULL;

long size;

BREAKPOINT* points = NULL;
```

我们预计随着其他阶段的发展完成此阶段。我们还需要更新用法信息以反映新功能：

```
if(argc < ARG_NARGS)

printf("insufficient arguments.\n");
```

```
"usage:\nt"

"\sfgain infile outfile posfile.brk\n"

"\tposfile.brk is breakpoint file\n"

"with values in range -1.0 <= pos <= 1.0\n"

"where -1.0 = full Left, 0 = Centre, +1.0 = full Right\n"

);

return 1;
```

在阶段 2（从用户处获取并验证参数），有两个任务。第一个是简单的打开新的断点文件。我们已经在第 1 章（1.1.7 节）中实现了此代码。它包含了对文件的一些重要的基础错误检查：

```c
/* breakpoint file and verify it */
fp = fopen(argv[ARG_BRKFILE],"r");
if(fp == NULL) {
    printf("Error: unable to open\nbreakpoint file %s\n",argv[ARG_BRKFILE]);
    error++;
    goto exit;
}
points = get_breakpoints(fp, &size);
if(points==NULL) {
    printf("No breakpoints read.\n",);
    error++;
    goto exit;
}
if(size < 2) {
    printf("Error: at least two breakpoints required\n",);
    free(points);
    fclose(fp);
    return 1;
}
/* we require breakpoints to start from 0 */
if(points[0].time != 0.0) {
    printf("Error in breakpoint data: \nfirst time must be 0.0\n",);
    error++;
    goto exit;
}
```

我们还需要检查文件中的断点是否都在允许的范围内。在 `breakdur` 中使用的 `get_maxpoint` 函数完成了一部分工作，我们也可以创建一个匹配的 `get_minpoint` 函数来完成另一部分，但使用这两个函数将对数据进行两次扫描。对于断点文件来说这是微不足道的，但如果它是从音频文件中提取的（正如我们在本章稍晚将要做的那样），并且包含成千上万个点，这种开销是值得避免的。相反，我们可以将上面 2.3.4 节演示的代码修改成一个通用函数，该函数接收所需的范围并扫描断点数组，如果发现超出范围的值则返回 0，如果都在范围内则返回 1：

```c
int inrange(const BREAKPOINT* points,
    double minval,
    double maxval,
    unsigned long npoints)
{
    unsigned long range_OK = 1;
    for(i=0; i < npoints; i++){
        if(points[i].value < minval || points[i].value > maxval){
            range_OK = 0;
            break;
        }
    }
    return range_OK;
}
```

在 `breakpoints.h` 中添加此新函数的声明，并将整个函数体拷贝到 `breakpoints.c` 中。然后你可以在上面的验证测试之后调用此函数：

```c
if(!inrange(points,-1,1,0,size())) {
    printf("Error in breakpoint file: \tvalues out of range -1 to +1 \n");
    error++;
    goto exit;
}
```

注意，这里使用了运算符 `!`（逻辑非或“取反”），因此测试询问的是“如果断点数据**不在**范围内，则报告错误”。

`NOT` 运算符在应用于值零时返回 `true`，否则返回 `false`，这就是为什么当 `inrange` 发现超出范围的值时返回 0 的原因。如果我们有一个接受的断点文件，只需要在主处理循环中将其应用到音频文件中。在这个阶段，我们需要能够准确地描述我们正在尝试。

![](img/4e80a3f6f432392037615a065cf9d4ba_256_0.png)

图 2.4
断点数据的线性插值。

## 2.3.7 基础断点处理——使用线性插值

当前的任务是，给定一组在任意（非递减）时间上的时间/值断点，找到相邻点之间某个时间的值。图 2.4 阐述了这种情况，假设断点文件包含以下数据：

0.0 0.0
2.0 1.0
4.5 0.0

我们想要知道时间 = 2.25 时的值。在遵循此步骤时，考虑的不是单个断点，而是一对相邻点，我们将其称为“跨度”（span）。在上面的图中段两个跨度，第一个长 2 秒，第二个长 2.5 秒。我们想知道时间 = 2.25 处的值，如水平轴下方的向上箭头所示。

由于目标时间不能为负数，第一个点的时间必须为零，且后续时间不能减小，因此沿着数组移动直到找到一个右侧时间大于或等于目标时间的断点是简易的事——在这种情况下，是第二个跨度。我们需要知道请求的时间在这个跨度上延伸了多远，表示为整个跨度的简单分值——即从左侧到目标时间的距离（在图 2.4 中标记为 $a$）与整个跨度宽度（在图 2.4 中标记为 $b$）之间的比例：

```
a = time - time_{left} = 0.25
```

```
b = time_{right} - time_{left} = 2.5
```

```
fraction = \frac{a}{b} = 0.1.
```

由于断点文件定义了一条连接跨度内两个值的单线，我们可以将其应用于跨度值以找到所需的值：

```
c = value_{right} - value_{left} = -1.0,
```

```
target\_distance = c \times fraction = -0.1,
```

```
target\_value = value_{left} + target\_distance = 1.0 - 0.9
```

## 2.3.8 完成并测试新的 sspan

为了给 sspan 添加新的泛声函数，仅剩最后一个任务：获取提供给函数的时间值。为了追求最终质量，我们希望每个样本执行一次。因此，我们需要计算每个样本的增量。样本之间的距离是恒定的，它等于采样率的倒数：

```
double timeincr = 1.0 / inprops.rate;
```

因此，我们都在处理循环外部初始化一个变量为零：
`double sampletime = 0.0;`

并且每个样本对其增加 `timeincr`。变量必须在 main 的开头（阶段 1）声明，但也许它们最好在处理循环开始后立即初始化（当然，`timeincr` 无法在打开音频文件之前初始化），以便阅读代码的人清楚这些初始化与该循环紧密相关。最后，我们在循环之前的原始 `simplepan` 调用必须移动到循环内部，并增加 `sampletime` 值。这导致了处理循环的最终代码：

# C语言中的音频编程

```c
/* 初始化读取包络的时间位置 */
timecr = 1.0 / inpropsrate;
sampleletime = 0.0;
```

```c
while ((framesread = psf_sndReadFloatFrames(ifd,inframe,nframes)) > 0) {
    int i, out_i;
    double stereos;
    for(i=0, out_i = 0; i < framesread; i++){
        sttereopos = val_atbrktime(points, size,sampletime);
        simplepan(stereos);
        outframe[out_i++] = (float)(inframe[i]*pos.left);
        outframe[out_i++] = (float)(inframe[i]*pos.right);
        sampletime += timecr;
    }
    if(psf_sndWriteFloatFrames(ofd,outframe,framesread)
       != framesread) {
        printf("Error writing to outfile\n");
        error++;
        break;
    }
```

现在是时候构建并测试整个程序了。记住要仔细阅读第一条信息；在此阶段，大多数错误都是简单的拼写错误。

测试涉及选择一个合适的输入文件，并创建一个断点文件，其中包含一个与文件时长匹配的声场轨迹（或者更短——取决于这里的最终值行为）。先不要尝试做任何“创新性”的操作。一个简单的三点断点就足够检查这些方向的性能了：

- 0.0 -1.0
- 2.0 1.0
- 4.0 -1.0

这会让声音从完全左侧稳定移动到完全右侧，然后缓慢返回，速度足够让人清晰地听到这种运动。记住，作为一名音频/音乐程序员，你评估的不仅是程序在不崩溃的情况下运行得有多好，还有结果的音质。请使用易于评估的测试源。对于评估声场函数，需要电平相当恒定的声音。你可以使用正弦波（特别适用于使用 Audacity 进行图形化测试），但通常认为脉冲声在立体声场中更容易定位，因此一个简单的鼓点循环也同样有效。你需要在没有

# 第2章

干扰反射的空间里配备一套良好的音频设备。耳机通常很有用，但只能作为辅助——评估声场过程时，你需要通过间距合理的立体声扬声器听。

不要忘记测试程序的基本功能。检查它是否能正确打开单声道文件并拒绝其他文件，以及它是否能生成立体声输出而不崩溃或打印不当的错误信息。相反，也要测试在传递不存在的文件名时，是否传递了正确的信息。

预先定义（只要可以的话）你期望听到的内容是非常重要的。如果你有一个程序（可能是 DAW）可以通过自动化动态对声音进行声场处理，请用它创建一个声音，来与 *sfan* 的输出进行比较。有时，在没有先例的情况下评估一个新效果非常困难，将其联系起来会有帮助。如果你说立体声平衡器的叙述需求是让声音在立体声场中平滑移动，保持与听者之间的距离感，从而保持恒定的音量。

## 2.3.9 更好的方案——恒功率函数

如果你遵循了上述所有步骤，并听了 *sfan* 的输出，你可能会产生以下一个或多个印象：

- 声音倾向于向左侧或右侧扬声器聚集。
- 当输入处于声场中央时，声音似乎在后退（远离听者）。
- 当声音处于声场中央时，电平似乎略有下降。

其原因是声音的振幅和感知的强度（或响度）并不是等同的。耳朵对强度的敏感度高于振幅（这就是为什么分贝刻度对音频工程师如此重要），而强度（与信号功率相关）是通过读取振幅的*平方*而非振幅本身来衡量的。如果想想找到一对声音的总强度，我们需要将每个信号的平方根平方以得到功率，然后通过这些值变回振幅：

```
$P = \sqrt{amp_1^2 + amp_2^2}.
```

当使用 *simplepan* 将声音置于中央时，将此公式应用于每个扬声器的音平，我们发现结果相加并不等于于 1：

```
$P = \sqrt{0.5^2 + 0.5^2} = 0.707$.
```

这相当于音平下降了 3 dB。从直觉上，我们可以理解这一点：两个同样响亮的歌手声音并不是一个人的两倍（这很好；一个平均规模的合唱团会超过疼痛阈值）。因此，我们需要的不是简单的线性函数，而是一个在应用上述公式时，在所需范围内结果为 1 的函数。

![](img/4e80a3f6f432392037615a065cf9d4ba_261_0.png)

图 2.5
恒功率平衡。

这样的函数将确保声音位于立体声场内的任何位置时都能保持*恒功率*。数学家可以设计任何符合此要求的函数。恒功率平衡器最广泛使用的函数是那些“听觉数学”的基石：正弦函数和余弦函数。恒功率平衡的公式为：

$A_{left} = \frac{\sqrt{2}}{2}\cos(\theta)$

$A_{right} = \frac{\sqrt{2}}{2}\sin(\theta)$

其中 $\theta$ 是弧度。

# 列表 2.3.3：恒功率函数

```c
double constpower(double position) {
    double pos;
    /* 每个通道 */
    const double root2 = 0.70710678118;
    /* 角度 */
    double angle = position;
    pos.left = root2 * cos(angle);
    pos.right = root2 * sin(angle);
    return pos;
}
```

## 2.3.10 关于 sfpan 的目标

我们在这一章做了很多工作。我们编写了一个恒功率程序，包含使用断点文件进行动态声场处理。在此过程中，我们学习了线性插值的原理。程序已经过测试，运行良好。

值本身不能为负数。可以添加所有这些检查，并对函数格式进行修改，使其返回一个错误值。所需的断点值可以通过由调用函数提供的指针返回，该指针也必须为 NULL。

然而，所有这些过程都是耗时的，而时间是音频程序员最宝贵的资源。在实现函数时，我们将信任它会被正确使用——当断点数据被加载时，会对其的合理性进行验证。同样，出于效率的考虑，每个样本都返回一个返回值是非常理想的，而且所有的验证检查都会增加函数的开销。在接下来的章节中，我们将遇到可选的实现策略以及进一步的 C 语言用法，这些将有助于提高代码的效率和健壮性。

## 2.3.11 练习

### 练习 2.3.1

函数 `val_at_brktime` 在 14–15 行有以下代码：

```
if(i == npoints) {
    return points[i-1].value;
}
```
