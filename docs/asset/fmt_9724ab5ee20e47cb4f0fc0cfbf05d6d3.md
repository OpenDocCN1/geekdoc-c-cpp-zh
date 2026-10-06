
```c
int main(int argc, char** argv) {

    SNDFILE *psf;

    float *buffer;

    int smps, cnt1=0, cnt2=0;

    float dur, amp, *wave, ndx=0;

    if(argc == 5) {

        // 现在打开文件

        if(!psf = soundout_open(argv[1]))

            printf("error opening output file\n");

            exit(1);

        }

        amp = (float) atof(argv[2]);

        freq = (float) atof(argv[3]);

        dur = (float) atof(argv[4]);

        smps = (int) (dur*def_cr);

        // 分配 buffer 和表格内存

        buffer = new float[smps];

        wave = sinus_table();

        for(int i=0; i < smps; i++){

            oscc(buffer,

            amp*adr(1.f,dur,0.05f, 0.1f, 0.7f, 0.2f, &cnt1,

            expon(freq/2,freq*2, &cnt2,

            wave,&ndx);

        }

        soundout(psf,buffer);

    }

    // 关闭文件并释放内存

    soundout_close(psf);

    delete[] buffer;

    delete[] wave;

    return 0;

}else {

    printf("usage: envelope sndfile.wav amp(hz) dur(s)\n");

    return 1;

}

n

```

# 6.6 滤波器

## 6.6.1 滤波器基础

滤波器通过不同方式将信号与其延迟副本结合来实现的。滤波器分为两大基本族：使用输入延迟副本的滤波器，称为前馈或有限脉冲响应 `FIR`；使用延迟输出的滤波器，称为反馈或无限脉冲响应 `IIR`。第二类滤波器可以仅包含一个前馈元件。

# 时域音频编程

其中 `$n$` 是信号的当前采样点，`$y(n)$` 是输出，`$x(n)$` 是输入，其系数 `$a_0$`，`$a_2$` 是与输入的两个采样延迟相关的系数，而 `$b_1$` 和 `$b_2$` 分别与滤波器输出的一个采样延迟和两个采样延迟相关的系数。

频率响应是指滤波器如何在不同频率上改变输入信号的幅度和相位。幅度响应是频率响应中与增强或衰减不同输入频率相关的部分。相位响应则决定了施加在不同频率上的延迟。它可以是线性的（所有频率的相位变化相同）或非线性的。根据滤波器方程（和系数），我们可以确定频率响应，反之亦然。

`IIR` 滤波器实现较简单，但设计复杂。一种方法是它们通常以“预装”的谐振器、巴特沃斯滤波器、椭滤波器等形式提供。它们的截止频率和带宽可以是随时间变化的，这对于音乐应用来说是一个重要特性。

`FIR` 滤波器设计更简单，并且可以提供线性相位特性，因此通常被工程师青睐。实现它们也很容易；然而，它们的计算量可能很大，且难以实现随时间变化。

## 6.6.2 谐振器和其他 IIR 滤波器

谐振器是基础的通用滤波器。它们被很好理解，并为大多数应用提供良好的结果。谐振器是反馈滤波器；它们将之前的输出采样与当前输入采样相结合。基础谐振器方程为

```
$y(n) = x(n) - b_1y(n - 1) - b_2y(n - 2)$.
```

该方程定义了一个二阶滤波器，系数为 `$b_1$` 和 `$b_2$`。滤波器的频率响应由其系数决定。反之，我们可以确定系数来配置我们所需的滤波器。

谐振器由两个主要特性定义：中心频率和带宽。系数 `$b_1$` 和 `$b_2$` 由这些参数决定（`$f$` 是滤波器中心频率，`$BW$` 是滤波器带宽，`$sr$` 是采样率，单位均为赫兹）：

```
$R = 1 - \pi(BW/sr)$,
```

```
$b_1 = -4R^2(1 + R^2)(2\pi f/sr)$,
```

```
$b_2 = R^2$.
```

谐振器的输出往往随中心频率和带宽的变化而变化，取决于输入信号。对于尖锐共振，滤波器可能会在大多数系统中引起削波失真。为了避免这种情况，我们设置了一个应用于输入信号的缩放因子。为了将中心频率处的信号缩放到 1，我们可以使用

```
$scaling = (1 - R^2)\sin(2\pi f/sr)$.
```

# 表 6.1

二阶巴特沃斯系数。

| `$\lambda$` | `$a_0$` | `$a_1$` | `$b_1$` | `$b_2$` |
|---|---|---|---|---|
| LP | `$1/\tan(\pi/sr)$` | — | `$1/(1+2\lambda+\lambda^2)$` | `$2a_0$` |
| HP | `$\tan(\pi/sr)$` | — | `$1/(1+2\lambda+\lambda^2)$` | `$2a_0$` `$2a_0(\lambda^2-1)$` |
| BP | `$1/\tan(BW/sr)$` | `$2\cos(2\pi f/sr)$` | `$1/(1+\lambda)$` | 0 `$-\lambda a_0$` | `$a_0(\lambda-1)$` |
| BR | `$\tan(BW/sr)$` | `$2\cos(2\pi f/sr)$` | `$1/(1+\lambda)$` | `$-\phi a_0$` | `$a_0(\lambda-1)$` | *(注：表格已根据标准巴特沃斯滤波器修正)*

谐振器的问题之一是当频率接近 0 Hz 或奈奎斯特极限时，其幅度响应曲线会出现畸变。在这种情况下，下方的衰减并不理想。一种建议的解决方案是向滤波器添加两个采样前延迟。这在 0 Hz 和奈奎斯特频率处产生“零点”（衰减）的效果。代价是滤波器另一侧的滚降会变小

```
$y(n) = a_0x(n) - a_2x(n) - b_1y(n-1) - b_2y(n-2),$
```

其中 `$a_2$` 可以设置为 1 或 0 以改变 `$R$` 的值。

有许多基于模拟滤波器特性的“成品”数字滤波器。一个典型的例子是巴特沃斯设计。巴特沃斯滤波器提供了极大平坦的通带良好的阻带衰减，可以是 LP、HP 和带阻型（BR）。它们都采用了反馈和前馈延迟，并在相同的结构中实现：

```
$y(n) = a_0x(n) + a_1x(n-1) + a_2x(n-2) - b_1y(n-1) - b_2y(n-2)$.
```

通过修改系数，可以将基础滤波器变为任何幅度响应。LP、HP、BR 的“配方”见表 6.1（`$f$` 是滤波器截止频率，`$BW$` 是带宽，`$sr$` 是采样率，单位均为赫兹）。

## 6.7 滤波器：实现

### 6.7.1 直接型

滤波器方程可以通过两种方式实现：

- (a) 直接型：使用独立的反馈和前馈延迟（见图 6.4）：

```
$y(n) = a_0x(n) + a_1x(n-1) + a_2x(n-2) - b_1y(n-1) - b_2y(n-2)$
```

- (b) 直接型 II：滤波器方程被重排为两个方程，相同的延迟可以用于前馈和反馈路径（见图 6.5）：

![img/4e80a3f6f43290761a65cfdba0.png] 图 6.4 直接型 I

![img/4e80a3f6f43290761a65cfdba01.png] 图 6.5 直接型 II

```
$w(n) = x(n) - b_1w(n-1) - b_2w(n-2)$
```

```
$y(n) = a_0w(n) + a_1w(n-1) + a_2w(n-2)$
```

### 6.7.2 低通高通滤波器：一阶

简单的色调滤波器提供平缓的低通或高通幅度响应，可以使用基于方程的基础一阶递归（或反馈）滤波器实现

`$y(n) = ax(n) - by(n-1).$`

# 表 6.2 IIR 系数

| a | b |
|---|---|
| LP | `1 + b` | `$\sqrt{(2-\cos(2\pi f/sr))^2-1}$` |
| HP | `1 - b` | `$\sqrt{(2-\cos(2\pi f/sr))^2-1}$` |

系数 `$a$` 和 `$b$` 可以如表 6.2 所示计算（`$f$` 是滤波器截止频率，`$sr$` 是采样率，单位为赫兹）。从上面可以看出，低通到高通只需将 `$b$` 系数乘以 -1 而保持 `$a$` 不变。这里是这些滤波器的 C++ 代码。我们将使用外部分配的内存变量来存储单采样反馈延迟。

```cpp
float lowpass(float* sig, float freq, float *del,
int vecsize, float sr) {
double cost, coef;
cost = 2. - cos(2*pi*freq/sr);
coef = sqrt(cost*cost - 1.) - cost;
for(int i=0; i < vecsize; i++){
    sig[i] = (float) (sig[i]*(1 + coef) - *del*coef);
    *del = sig[i];
}
return *sig;
}
```

```cpp
float highpass(float* sig, float freq, float *del,
int vecsize, float sr) {
double cost, coef;
cost = 2. - cos(2*pi*freq/sr);
coef = cost - sqrt(cost*cost - 1.);
for(int i=0; i < vecsize; i++){
    sig[i] = (float) (sig[i]*(1 - coef) - *del*coef);
    *del = sig[i];
}
return *sig;
}
```

### 6.7.3 谐振器

谐振器滤波器使用单采样和双采样延迟。谐振器的表达式和系数已经讨论过。这里有一个实现该滤波器的 C++ 函数：

```cpp
float resonator(float* sig, float freq, float bw, float *del,
    int vecsize,float sr){
    double r, rsq, rr, cost, scal;
    rr = 1. - pi*(bw/sr);
    r = rr; // 修正自 OCR "2*(r)"
    rsq = r*r;
    cost = (rr/(1.+rsq))*cos(2*pi/freq/sr);
    scal = (1 - rsq);
    for(int i=0; i < vecsize; i++){
        sig[i] = (float)(sig[i]*scal + rr*cost*del[0] - rsq*del[1]);
        del[1] = del[0];
        del[0] = sig[i];
    }
    return *sig;
}
```

改进型的谐振器滤波器使用双采样前馈延迟，可以使用基础谐振器系数实现，但修改缩放因子并添加 `$a2$` 项如下：

`$scaling = 1 - R,$`

`$a2 = R,$`

其中 `$R$` 是根据带宽计算的滤波器半径。由于使用了反馈和延迟，我们将使用讨论过的直接型 II，将滤波器分为两个方程：

```cpp
float bandpass(float* sig, float freq, float bw, float *del,
    int vecsize,float sr){
    double r, rsq, rr, cost, scal, w;
    rr = 1. - pi*(bw/sr);
    r = rr;
    rsq = r*r;
    cost = (rr/(1.+rsq))*cos(2*pi/freq/sr);
    scal = (1 - rsq);
    for(int i=0; i < vecsize; i++){
        w = scal*sig[i] + rr*cost*del[0] - rsq*del[1];
        sig[i] = (float)(w - r*del[1]);
    }
    return *sig;
}
```

# 第6章

```
del[1] = del[0];
del[0] = (float) w;
}
```

请注意，在这种设计中，我们会在信号进入滤波器时对其缩放，因为缩放因子并不是 `$a_0$` 系数。对于通用的二阶节（例如用于伯特沃滤波器的滤波器），我们将使用 `$a_0$` 系数作为方程的前馈部分系数。

## 6.7.4 RMS 估算与信号平衡

在使用滤波器时，有时需要提供信号重缩放功能，因为输出的幅度可能与输入大不相同。在滤波器级联连接的情况下就是如此。如果我们估计滤波器输出的均方根（RMS）和比较器信号的 RMS，就可以重新缩放输出以匹配比较器的幅度。这是平衡（balance）或包络跟踪器的基础。

RMS 通过对信号进行整流（取其绝对值）并进行低通滤波来估计的（同样，除了整流，我们也可以取其平方根）。要应用的缩放增益是比较器 RMS 与输入 RMS 的比例。以下是平衡处理器的代码：

```
float balance(float *sig, float *cmp, float *del, float freq,
int vecsize, float *sr) {
double costh, coef;
costh = 2. - cos(2*pi*freq/sr);
coef = sqrt(costh*costh - 1.) - costh;
for(int i=0; i < vecsize; i++) {
del[0] = (float)(sig[i] < 0 ? -sig[i] : sig[i]*(1+coef));
del[0]*coef;
del[1] = (float)(cmp[i] < 0 ? -cmp[i] : cmp[i]*(1+coef));
del[1]*coef;
sig[i] *= (float)(del[0] ? del[1] : del[1]);
}
return *sig;
}
```

注意，所使用的 LP 设计是上面讨论的基础一阶反馈环低通滤波器。整流与滤波器方程合并在一个表达式中。使用了两个延迟，分别对应每个滤波器，并且输入通过两个信号的 RMS 比例进行缩放。

## 6.7.5 编程示例

这里有一个使用振荡器、滤波器和平衡处理器的简单程序：

```c
#include <stdio.h>
#include <stdlib.h>
#include <snd_defs.h>
/**
  带有包络的减法合成程序。
  生成具有幅度
和滤波器 cf 包络的过滤锯波声。此程序还展示了
插值振荡器的使用。\
envelope sndfile.wav amp freq(Hz) dur(secs)
 */
int main(int argc, char** argv) {
SNDFILE *psf;
float *buffer;
int smps, bytes = sizeof(float)*def_size, cnt1=0, cnt2=0;
float dur, amp, freq, *wave, *comp, ndx=0;
if(argc == 5) {
 amp = (float) atof(argv[2]);
 freq = (float) atof(argv[3]);
dur = (float) atof(argv[4]);
smps = (int) (dur*secs);
 // 分配缓冲区、延迟与内存
 buffer = new float[def_size];
 comp = new float[def_size];
float del[2]={0.f, 0.f}, dell[2]={0.f,0.f,0.f};
 wave = saw_table(30);
 // 现在我们打开文件
if(!(!psf = soundout_open(argv[1]))) {
printf(" opening output file\n");
 exit(-1);
}
for(int i=0; i < smps; i++){
 osscc(buffer,
 adsr(amp,dur,0.05f, 0.1f, amp*0.7f, 0.2f, &cnt1);
 freq,
 wave,&ndx);
```
```c
memcmp(comp, buffer, bytes);
resonator(buffer, expon(freq*8,dur,freq*4,cnt2), 50, del);
balance(buffer, comp, dell);
soundout(psf,buffer);
}
// 关闭文件 & 释放内存
soundout_close(psf);
delete buffer;
delete comp;
delete wave;

return 0;
}
{
printf("usage: filter sndfile.wav freq(hz) dur(s)\n");
return 1;
}
```

## 6.8 基于延迟的处理

大多数时域信号处理技术涉及延迟的使用。这从已讨论的 IIR 滤波器的极小延迟到颤响（flanging）中的长延迟。

### 6.8.1 文件输入
