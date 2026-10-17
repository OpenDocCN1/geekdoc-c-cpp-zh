
虽然我们不能通过相位来操纵频谱的频率内容，但 `STFT` 的分辨率不足以判断声音中存在哪些频率。我们必须找到一种方法来跟踪每个频段中的瞬时频率。可以使用名为 `PV` 的已知技术来实现这一点。`PV` 分析过程有时在时域中描述为使用一组调整到从 `0` 兹到奈奎斯特频率等间隔频率的滤波器组。滤波器组输出由每个频段的幅和频率值组成。我们将采用频域方法，从 `STFT` 开始并对其调整以适应 `PV` 的输出特征。

`STFT` 后的极坐标转换也可以看作一组并行滤波器。它的输出由每个时间点或每个频段的幅度和相位值组成。将 `STFT` 转换为相位声器的第一步是生成与声音中频率成比例的值。理想情况下，这是通过对相位取导数完成的；但我们可以通过计算每个频段连续帧之间相位值的差来近似它。这种简单的操作虽然不会产生频段频率的正确值，但会输出一个与其相关的输出。

通过这些细小的变化，我们将能够以以前不可能的方式处理声音。通过跟踪相位差，我们可以拉伸或压缩声音而不改变其频率内容（或简单地说，不改变其音调）。我们可以通过重复或跳过频谱块来拉伸或压缩数据。因为我们保留了帧之间的相位差，当我们在重新合成之前对其进行累加时，我们将能够使用正确的相对相位值重构信号。

下面的代码接收矩形 `STFT` 输入并将其转换为幅度和相位差（原地转换）：

```
const double pi = twopi/2;

void deltaphi(float *spec, float *lastphs, int fftsize){
    int i, k;
    float mag, phi;

    for(k=0, i=2; i < fftsize; i+=2, k++){
        mag = (float)sqrt(spec[i]*spec[i+1]+spec[i+1]*spec[i]);
        phi = (float)atan2(spec[i+1], spec[i]);
        spec[i] = mag;
        spec[i+1] = phi - lastphs[k];
        lastphs[k] = phi;

        // 将差值带到 -pi 和 pi 范围
        while(spec[i+1] > pi) spec[i+1] -= (float)twopi;
        while(spec[i+1] < -pi) spec[i+1] += (float)twopi;
    }
}
```

反向函数输出 $-\pi$ 到 $\pi$ 范围内的相位。当计算相位差时，可能会超出此范围。在这种情况下，我们必须将它们带入期望区间（称为*主值*）。

通过这些细小的变化，我们将能够以以前不可能的方式处理声音。通过跟踪相位差，我们可以拉伸或压缩声音而不改变其频率内容（或简单地说，不改变其音调）。我们可以通过重复或跳过频谱块来拉伸或压缩数据。因为我们保留了帧之间的相位差，当我们在重新合成之前对其进行累加时，我们将能够使用正确的相对相位值重构信号。

下面的代码接收矩形 `STFT` 输入并将其转换为幅度和相位差（原地转换）：

```cpp
const double pi = twopi/2;

void deltaphi(float *spec, float *lastphs, int fftsize){
    int i, k;
    float mag, phi;

    for(k=0, i=2; i < fftsize; i+=2, k++){
        mag = (float)sqrt(spec[i]*spec[i+1]+spec[i+1]*spec[i]);
        phi = (float)atan2(spec[i+1], spec[i]);
        spec[i] = mag;
        spec[i+1] = phi - lastphs[k];
        lastphs[k] = phi;

        // 将差值带到 -pi 和 pi 范围
        while(spec[i+1] > pi) spec[i+1] -= (float)twopi;
        while(spec[i+1] < -pi) spec[i+1] += (float)twopi;
    }
}
```

反向函数输出 $-\pi$ 到 $\pi$ 范围内的相位。当计算相位差时，可能会超出此范围。在这种情况下，我们必须将它们带入期望区间（称为*主值*）。

```cpp
int pva(float *input, float *window, float *output,
 int input_size, int fftsize, int hopsize, float sr){
  int posin, posout, i, k, mod;
  float *sigframe, *specframe, *lastph;
  float fac, scal, phi, mag, delta, pi = (float)twopi/2;
  sigframe = new float[fftsize];
  specframe = new float[fftsize];
  lastph = new float[fftsize/2];
  memset(lastph, 0, sizeof(float)*fftsize/2);
  fac = (float)(sr/hopsize*twopi);
  scal = (float)(twopi*hopsize/fftsize);
  for(posin=posout=0; posin < input_size; posin+=hopsize){
  mod = posin%rotate;
  // 旋转信号帧
  for(i=0; i < fftsize; i++)
   if(posin<i+input_size)
      sigframe[(i+mod)%fftsize] = input[posin+i]*window[i];
   else sigframe[(i+mod)%fftsize] = 0;
  // 对进行变换
  fft(sigframe, specframe, fftsize);
  // 转换为 PV 输出
  for(i=2,k=1; i < fftsize; i+=2, k++){
  // 直角坐标转极极坐标
  mag = (float)sqrt(specframe[i]*specframe[i] + specframe[i+1]*specframe[i+1]);
  phi = (float)atan2(specframe[i+1], specframe[i]);
  // 相位差
  delta = lastph[k];
  lastph[k] = phi;
  // 解包裹差异，使其处于 -pi 和 pi 之间
  while(delta > pi) delta -= (float) twopi;
  while(delta < -pi) delta += (float) twopi;
  // 构建幅度-频率对
  frame[i] = mag;
  specframe[i+1] = (delta + k*scal)*fac;
  }
  // 输出
  for(i=0; i < fftsize; i++, posout[i])
  output[posout] = specframe[i];
}
delete[] sigframe;
delete[] specframe;
delete[] lastph;

return posout;
}
```

## 9.1.2 相位声器重合成 (Phase Vocoder Resynthesis)

相位声器数据可以使用多种方法进行重合成。由于我们拥有幅度和频率数据块，可以使用某种加法合成来播放频谱帧。然而，对于具有许多分量的音频声音，转换为时域数据更有效的方法是使用类似于 `ISTFT` 中的重叠加（overlap-add）方法。我们需要做的只是反向执行变换中的步骤：

1. 通过从每个通道的中心频率（单位赫兹，k/N）中减去频率，将频率转换回每样本弧度相位差，并将结果乘以 2pi/sr，其中 sr 是合成率。
2. 累积时间以计算当前相位值。
3. 执行极坐标到直角坐标的转换。
4. 对信号帧进行逆离散傅里叶变换 (`IDFT`)。
5. 取消旋转并对生成的样本块应用窗口。
6. 连续帧重叠加。

代码如下：

```cpp
int pvs(float* input, float* window, float* output,
 int input_size, int fontsize, int hopsize, float sr){
  int posin, k, i, output_size, mod;
  float *sigframe, *specframe, *lastph;
  float fac, scal, phi, mag, delta;
  sigframe = new float[fontsize];
  specframe = new float[fontsize];
  lastph = new float[fontsize/2];
  memset(lastph, 0, sizeof(float)*fontsize/2);

  output_size = input_size*hopsize/fontsize;
  fac = (float) (hopsize*twopi/sr);
  scal = sr/fontsize;

  for(posout=posin=0; posout < output_size; posout+=hopsize);

  // 从输入中加载频谱帧
  for(i=0; i < fftsize; i++, posin++)
  specframe[i] = input[posin];

  // 从 PV 输入转换为 DFT 坐标
  for(i=2,k=1; i < fftsize; i+=2, k++){
      delta = (specframe[i+1] - k*scal)*fac;
      phi = lastph[k]+delta;
      lastph[k] = phi;
      mag = specframe[i];

      specframe[i] = (float) (mag*cos(phi));
      specframe[i+1] = (float) (mag*sin(phi));
  }

  // 逆变换
  ifft(specframe, sigframe, fftsize);
  // 取消窗口窗口并重叠加
  mod = posout%fftsize;
  for(i=0; i < fftsize; i++)
    if(posout+i < output_size)
      output[posout+i] += sigframe[(i+mod)%fftsize]*window[i];
}

delete[] sigframe;
delete[] specframe;
delete[] lastph;

return output_size;
}
```

相比 `STFT`，`PV` 分析有几个优势。第一个优势是时间尺度和频率尺度的独立性。另一个是表示形式的灵活性，可以用于许多应用。对幅度和频率的处理在音乐上是有意义的。此外，之前讨论的所有 `STFT` 技术也适用于 `PV` 格式，这使得相位声器成为 `STFT` 更通用的工具。因此，对于某些应用，如果 `STFT` 就足够了，基于 `DFT` 的算法在频率分辨率方面存在限制。分析能够解析每个频带的一个正弦分量。如果一个频带内有两个或多个分量，相位声器将无法输出正确的幅度和频率。因为 `DFT` 将频谱分为等大的频带，这暗示相位声器更适合频谱分析。

### 频谱演变 (Spectral Morphing)

典型的 `PV` 数据变换是频谱插值或演变。之前讨论的频谱交叉是在两个频谱之间进行频率的插值。以下代码通过频率之间的线性插值来实现此操作。参数 `morph` 和 `morphfr` 定义了插值量，范围应在 0–1 之间。

```cpp
void pvmorph(float *input1, float *input2, float *output,
 float morph, float morphfr, int fftsize, float sr) {
  int i;
  float ampl1, ampl2, fr2;
  double div;
  for(i=0; i<fftsize; i+=2) {
    ampl = input1[i];
    ampl2 = input2[i];
    output[i] = ampl + (ampl2-ampl)*morph;
    if(i) {
      // 插值频率
      fr1 = input1[i+1];
      fr2 = input2[i];
      div = fr1 ? fr2/fr1 : HUGE_VAL;
      div = div > 0 ? div : -div;
      output[i+1] = (float)(fr1*pow(div,morphfr));
    } else {
      // 这是奎奎斯特频带
      ampl = input1[i+1];
      ampl2 = input2[i+1];
      output[i+1] = ampl + (ampl2-ampl)*morph;
    }
  }
}
```

这是一个使用上述函数进行频谱演变的示例完整代码：

```cpp
#include <stdio.h>
#include "spec.h"
#include "fourier.h"

/*
pv morphing 主程序
use: pvmorph infile infile2 dur(s)

infile: input1 (起始声音)文件名
infile: input2 (目标声音)文件名
outfile: 输出文件名
dur: 输入时长（秒）

所有提供的文件均为单声道
*/

int main(int argc, char **argv){
  SNDFILE *fin, *fin2, *fout;
  SF_INFO input_info, input_info2;
  float *win, *in, *in2, *out, *spec, *spec2;
  int outsize, specsize, fftsize=1024,hopsize=256;
  int dataario=fftsize/hopsize;
  int frames, extraframes;
  int read=0, written = 0, i,j, dur;
  float *buff,sr;

  if(argc < 3) {
    printf("%s: 参数不足（得到 %d, 需要 3)\n", argv[0], argc-1);
    usage();
    exit(-1);
  }
  if(!(fin = sf_open(argv[1], SFM_READ, &input_info))){
    printf("无法打开 %s \n", argv[1]);
    exit(-1);
  }

  if(!(fin2 = sf_open(argv[2], SFM_READ, &input_info2))){
    printf("无法打开 %s \n", argv[2]);
    exit(-1);
  }

  if(!formats_equal(input_info, input_info2)) {
    sf_close(fin2);
    sf_close(fin);
    printf("%s 和 %s 格式不相同或文件不是单声道\n",
           argv[1], argv[2]);

    exit(-1);
  }

  dur = input_info.frames > input_info2.frames ?
    input_info2.frames : input_info.frames;
  sr = input_info.sampler;
  buff = new float[100];
  win = new float[fftsize];
  in = new float[dur];
  in2 = new float[dur];
  /* 完全数据帧数 */
  frames = (dur*dataario)/fftsize;
  /* 额外帧 [未完全填充] */
  extraframes = 1 -
    (frames*fftsize - dur*dataario)/fftsize;
  /* 频谱数据大小 */
  specsize = (frames + extraframes)*fftsize;
  spec = new float[specsize];
  spec2 = new float[specsize];
  outsize = specsize/dataario;
  out = new float[outsize];

  if(!(sf_open(argv[3], SFM_WRITE, &input_info))){
    printf("无法打开 %s \n\n", argv[3]);
    exit(-1);
  }
```
