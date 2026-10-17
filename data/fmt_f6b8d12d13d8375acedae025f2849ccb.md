
这种创建与初始化分离的方法在交互式实时应用（包括音频插件）中通常是必要的，因为在对象创建时可能无法采样率。这使得重新初始化对象变得可能——例如，重启包络器或设置新的采样率。然而，这种双功能方法对于自包含的程序并不是理想的，因为它更容易出错，特别是对于那些仍处于编程学习早期阶段的人来说。例如，错误地只声明了指向 `OSCIL` 的指针并传递给函数，或者如果指针为 `NULL`，`osc_init` 将因访问违规而崩溃。为了防止这种情况，并封装一种能够同时创建和初始化对象的设计，这是可能的（见列表 2.5.5）。将此添加到 `wave` 中。函数不再返回 `void`，而是返回 `NULL`（在内存失败时）或一个完全创建并初始化的对象。

这种方法的主要方面是使用 `malloc` 为 `OSCIL` 创建外部存储，该存储在函数返回后仍然存在。该函数的文档应该告诉用户在不再需要时释放（`free`）该对象。

为特定对象定义替代的创建或初始化函数是完全合理的。C++ 语言的唯一要求是函数名称必须是唯一的。

当我们探索 C++ 时，我们将发现一种名为“函数重载”的有价值的新功能，它允许在参数和/或返回类型不同的情况下定义多个同名函数。然而，目前，我们可以使用这种紧凑的“全合一”方法来处理。

## 列表 2.5.5：组合的 OSCIL 创建与初始化函数

```c
OSCIL* new_osc(unsigned long rate)
{
OSCIL* p_osc;
p_osc = (OSCIL*) malloc(sizeof(OSCIL));
if(p_osc == NULL)
    return NULL;
p_osc->twiovipr = TWOPI / (double) rate;
p_osc->curfreq = 0.0;
p_osc->curpurase = 0.0;
p_osc->incr = 0.0;
return p_osc;
}
```

*使用方法如下：*

```c
OSCIL *osc = new_osc(44100);
```

我们现在可以定义采样生成函数（列表 2.5.6），它是基于 2.5.2 中的示例建模的。它必须为每个所需的样本进行调用。它包含了对频率变化值以及负频率的必要支持。检查它在第一次调用时的行为非常重要。该函数在生成初始样本（仅取决于相位）后执行的第一件事是更改频率，这在必要时更新 `incr` 的值——这是一种“读取并更新”的方法。注意，当 `crfreq` 改变时，`incr` 会被重新计算，这样在频率不变的情况下，冗余处理被降到最低。同样注意，对输入指针没有进行错误检查——这是出于效率考虑，因为该函数会被频繁地调用。

### 列表 2.5.6：OSCIL 类型的采样生成函数

```c
double sinetick(OSCIL* p_osc, double freq)
{
  double val;
  val = sin(p_osc->curphase) * freq;
  if(p_osc->crfreq != freq)
    p_osc->crfreq = freq;
    p_osc->incr = p_osc->twopiovsr * freq;
  }
  p_osc->curphase += p_osc->incr;
  if(p_osc->curphase >= TWOPI)
    p_osc->curphase -= TWOPI;
  if(p_osc->curphase < 0.0)
    p_osc->curphase += TWOPI;
  return val;
}
```

*使用方法如下：*

```c
for(i=0; i < nframes;i++)
  frame[i] = sinetick(osc,freq); /* 随意修改 freq */
```

通过这种方式，我们几乎完全地创建了我们在 2.5.1 节开头寻找的函数，区别在于需要传递一个 `OSCIL` 变量的指针，用于在调用之间保留振荡器的内部状态。这在 C 中是一种非常地道的方法。我们将大量使用它。

# 第 2 章

## 2.5.4 创建一个简单的测试程序

在转向更复杂的功能之前，在一个初始的“概念验证”程序中实现目前开发的代码是合理的，该程序简单地根据要求的频率、振幅和频率产生单声道声波（正弦波）。你以前确实做过这件事，在第 1 章中；这里的区别在于代码的设计以及 `portfs` 库的使用。你有两种选择：将 `main.c` 复制到新文件并从那里开发新程序，或者复制并适配之前介绍的程序。由于这是一个合成程序，没有输入文件。调用 `sigen("signal generation")` 程序，并像往常调用源文件 `sigen.c`，程序需要与 `portfs` 链接，当然我们使用了新的源文件 `wave.c`，这是一个变得复杂的程序——DVD 上的 `sigen.c` 版本是最终版本，而不是初步阶段。最重要的是从原理遵循编写此程序的细节。

第一个任务是完成实现振荡器代码的源文件。头文件 `wave.h` 应该包含 `OSCIL` 的定义，以及 `M_PI` 和 `TWOPI` 的定义，以及列表 2.5.4 和 2.5.5 中定义的 `new_osc` 和 `sinetick` 函数原型。对于合成，我们需要一个至少包含持续时间、振幅和频率作为输入的命令行；但采样率参数将非常有用：

```bash
sinetest outline srate freq
```

这导致了一个枚举：

```c
enum (ARG_PRONAME, ARG_OUTFILE, ARG_DUR, ARG_SRATE,
      ARG_AMP, ARG_FREQ, ARG_NARGS);
```

你必须以通常的方式为这些参数每一个定义 `srate`、`dur` 和 `freq` 变量，并编写代码从命令行获取它们。

与之前的程序最明显的区别是，这是一个合成程序，没有输入文件。这不仅需要适配模板代码，还需要适配处理循环本身。在没有输入文件的情况下，我们必须直接设置它们：

```c
srate = atof(ARG_SRATE);
outprops.srate = srate;
outprops.ch = 1;
outprops.sametype = PSF_SAMP_16; /* 或无论需要的 */
outprops.chformat = STDWAVE
```

在一个完全开发的程序中，所有设置可能从命令行获取。从 `srate` 和 `dur` 可以推导出所需的采样数（四舍五入到最近的采样）；然后可以使用它找到 `NFRAMES` 块的数量。

```c
unsigned nbufs, outframes, remainder;
dur = atof(argv[ARG_DUR]);
outframes = (unsigned long) (dur * outprops.srate + 0.5);
nbufs = outframes / nframes;
remainder = outframes - nbufs * nframes;
if(remainder > 0)
nbuffs++;
```

注意这使用了整数除法，`nbufs` 可能为零。对 `nbufs` 的最后的条件递增确保了处理循环至少运行一次。之前的代码将拒绝零索引。

### 列表 2.5.7：合成的处理循环

```c
for(i=0; i < nbufs; i++){
if(i == nbufs-1)
remainder = remainder;
for(j=0; j < nframes; j++)
outframe[j] = (float) (amp * sinetick(p_osc, freq));
if(psf_sndWriteFloats(ofd,
outframe, nframes)!=nframes){
printf("Error writing to outfile\n");
error++;
break;
}
}
```

这完成了基础单声道正弦波振荡器的要求。构建程序，并以各种频率生成一些正弦波。不要认为程序运行完成这一事实就足以保证程序正常工作。PEAK 信息是一个初步确认——
