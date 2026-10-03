
```matlab
% 基漂移示例
% (C) 2003 by Yu Hen
% 调用 trendrm.m
% 需要信号处理工具箱
% 输入序列 gt 存储在文件.mat 中
clear all
load try; % 输入变量
[m,n] = size(gt);
cutoff = 10/m; % 这里将 3dB 截止频率设置为 10
L=input('滤波器长度-2L+1, L:');
[y,low] = trendrm(gt, L, cutoff);
figure(1), clf
subplot(3,1),plot([1:m],gt,':[1:m],y,'-'),
legend('original','baseline')
title('a) 原始序列与基线序列')
axis([0 10])
subplot(3,2),stem([1:2*L+1],b),title('FIR 冲激响应')
axis([1 2*L+1 floor(b) max(b)])
subplot(3,3),plot([1:m],y),ylabel('difference')
title('c) 差分序列')
axis([0 floor(y) ceil(max(y))])
w = [0:pi/255:pi];

Hz = freqz(b,1,w);
figure(2), clf
plot(w, 20*log10(abs(Hz))); ylabel('|H(w)|', 'db')
axis([0 1 -50 0]),title('(a) 滤波器幅度响应')
fgt = abs(fft(w));
m2 = m/2;
plot([1:m2]/m2,log10(fgt(1:m2))); ylabel('|log10X(w)|')
axis([0 2 -4]),title('(b) 原始频率响应')
flow = abs(fft(w));
plot([1:m2]/m2,log10(flow(1:m2))); ylabel('|log10B(w)|')
axis([0 1 -2 4]),title('(c) 基线频率响应')

function [y,low,b]=trendrv(x,L,wcutoff)
% 用法：移除基线，对称 FIR 滤波器
% x 是记录 N 矩阵，列需要进行低通滤波
% L 滤波器的长度（奇数）
% wcutoff: 归一化频率，正分数
% 以归一化频率表示
% y: 高通结果
% low: 基线结果
% b: 长度为 2L+1 的低通滤波器
```

# 数字信号处理背景

```matlab
T=1/fs; % 采样周期
ts=[0:T:1]; % 采样点
xs=cos(2*pi*f0*ts); % x(n)
ts=length(ts);
% 计算机重建信号
zeros=size(tx)); for i=1:nts,
xhat=xs + xi*sin(pi*fs+tx,pi*(i-1));
end
% 绘图
figure (1);clf
plot(tx,x, 'b-',ts,xs; 'bo',tx,xhat, 'r');axis([0 1 -1.5 1.5])
legend('original','samples','reconstruct')
title(['f=',f0,'] f_s=',int2str(fs), 'hz.'])
function y=sinc(x,a)
% Usage: y=sinc(x,a)
% (C) 2003 by Yu Hen Hu
y=sin(x-a)/(x)
% x: a vector
% a: a constant
% if x-a, y=1;

if margin=1,a=0; % 默认，无偏移
len=length(x); % 向量 x 的长度
yzeros(size(x));
idx=find(x=a); % sin(0)=1 需要单独计算
if ~isempty(idx)
y(idx)=1;
s=setdef([1:n],idx)
y(sidx)=sin(x(sidx)-a)/(x(sidx)-a); else
y=sin(x-a)/(x-a); end
```

# 4.0 附录 D

```matlab
用于生成图 4.5 的 MATLAB® 程序。
% 读取频谱的演示
% (C) 2003 by Yu Hen Hu

clear all
n=100;
f0 = 0.095; % 样本/分钟
%load onemat; % 变量 y(1440,2)
tx=[1:n]; % 采样周期为 1min/sample
tmp=0.2*randn(n,1);
x=sin(2*pi*f0*tx + rand(size(tx))) +tmp;
fs=1; % 每分钟 1 个采样
% 序列的频谱
% (a) n 点
n2=floor(n/2);
xs=abs(fft(x))); %
% 未绘制直流分量
figure(1),clf
subplot(4,1),plot([1:n],x(:),'g';[1:n],x(:),'b');
axis([1 min(x(:)) max(x(:))])
xlabel('min')
```

# 图像与传感器处理

```matlab
ylabel('a) x(n)')
% (b) 采样 2:1
xc0=1:2:n); nc=length(xc0); tc=1:2:n;
xsc=abs(xc0); plot(tc,xc0, 'g,'); nsc=floor(nc/2)
subplot(1,3,tc,xc0, 'b.')
axis([1 max(tc) min(x(:))])
xlabel('min')
ylabel('c') Y(1)
t0=0:nsc-1/(nc*fs2);
% 频率 0 到 2pi，采样频率
tc=1:nsc); plot 的前半部分由于 mag(DFT) 的对称性
length=length(tc);
subplot(4,1),stem(tc,xc(1:nsc), 'filled')
xlabel('frequency (samples/min.)')
axis([0 0.25 0 max(xsc)])
ylabel('d') Y(m)
t2=0:n2-1/n2*fs/2;
subplot(4,2),stem(t2(1:nsc),xs(1:nsc), 'filled'),hold on
t2(nsc+1:n2),xs(nsc+1:n2)),hold off,xlabel('hz')
axis([0 0.5 0 max(xs)])
xlabel('frequency (samples/min.)')
ylabel('b') |X(k)|
```

# 参考文献

- 1. Mitra, S.K., Digital Signal Processing: A Computer-Based Approach, McGraw Hill, New York, 2001.
- 2. Oppenheim, A.V. and Schafer, R.W., Digital Signal Processing, Prentice-Hall, Englewood Cliffs, NJ, 1975.
- 3. Mitra, S.K. and Kaiser, J.F, Handbook for Digital Signal Processing, John Wiley & Sons, New York, 1993.

# 5 图像处理背景

- 5.1 引言 ................................................................59
- 5.2 动机 .................................................................60
- 5.3 图像创建 ..............................................................61
  - 图像频谱 • 图像维度 • 图像传感器
  - 模拟数字图像
- 5.4 图像域：空间、频率 .................................................67
- 5.5 点运算 ................................................................69
  - 阈值化 • 转换 • 对比度拉伸与直方图均衡化 • 反转
  - 电平处理 • 位面切片 • 图像减法 • 图像平均
- 5.6 区域运算 ................................................................72
  - 低通滤波器 • 高通滤波器 • 中值滤波器 • 边缘检测 • 形态算子
- 5.7 噪声去除 ........................................................76
- 5.8 特征提取 .......................................................77
  - 边缘 • 霍变换：形状检测 • 分割：表面 • 示例
- 5.9 配准、校准与融合问题 .............................................81
  - 配准 • 几何变换 • 校准 • 融合问题

Lynne L. Grewe

加州州立大学

Ben Shahshahani

- 5.10 压缩与传输：分布式传感网络的输入 ................................................85
- 5.11 图像重采样 .................................................................86
- 5.12 用于输出的图像处理 ................................................86
- 5.13 传感器网络应用中的更多成像 ...................87
- 参考文献 ............................................................89

## 5.1 引言

来自可见光、光电相机或其他传感器的图像是分布式传感器网络中的关键和主要数据源。理解并有效处理这些图像至关重要的。分布式传感器网络中图像的常见使用可能是因为我们人类对图像的严重依赖。俗语说：“一画胜千言”。传感器网络中图像的显著性可能也由于存在许多类型的图像，不仅限于可见光谱，还包括红外、光谱和声呐图像。本章将让读者理解从创建到处理的图像，并介绍图像和图像处理在传感器网络中的应用。

图像处理简单定义为对图像的处理。处理图像的过程首先取决于它在传感器网络中如何使用以及网络的目标。例如，图像可以作为网络中的信息数据源，也可以用于校准或监控网络进度。图像处理可以在许多阶段进行。这些阶段通常被称为预处理、特征或信息处理以及后处理。另一个重要的图像处理是压缩和传输。在分布式传感器网络中，这尤其重要，因为图像尺寸往往会造成巨大的存储和传输负担。

我们首先通过几个图像在传感器网络中使用的示例来提供动机。

## 5.2 动机

在开始讨论图像处理之前，让我们看几个图像起着重要作用的传感器网络示例。

在 Ros [09] 中，讨论了一种同时使用视觉和红外（IR）图像的人员检测系统。在该系统中，使用背景减法技术在每幅图像中单独检测可能的人员。

在 Foresti [02] 中，描述了一个使用外部环境图像的分布式传感器网络。这些图像是传感器所监测的外部环境中目标的唯一信息源。两种图像的使用允许系统在白天黑夜条件下追踪产生量的物体，如人类和其他动物。请参见图 5.2 的系统某些图像。

Bhatia [00] 描述了一种车载传感器网络，它使用各种类型的图像执行户外环境中的地雷探测任务。在这里，图像在提供探测地雷的信息方面起着关键作用。特别是红外穿地雷达（GPR）和金属检测图像。

在 Verma [01] 中，多个摄像头和激光测距仪分布在工作环境中供机器人系统使用，以帮助完成目标任务如物体检测、避障和导航。图 5.3 显示了该系统的示例环境。

另一个使用多种传感器的机器人系统，这种是光电相机和激光测距仪，用于 [Luo 09] 系统。该目标是人员追踪，利用图像和激光测距数据检测人员，然后对结果进行融合。

Marcano [02] 描述另一种以图像作为唯一数据源的监控应用类型。在这里，使用了静态和移动摄像头来收集数据，如图 5.4 所示。

这些只是使用图像的许多传感器网络中的几个。在剩余章节中，当我们重新回顾这些和其他网络时，了解图像以及如何有效处理图像以实现网络系统的目标。

# 图像处理背景

![](img/11e8580124e6543d23c6c1d715727b6a_85_0.png)
![](img/11e8580124e6543d23c6c1d715727b6a_85_1.png)
![](img/11e8580124e6543d23c6c1d715727b6a_85_2.png)
![](img/11e8580124e6543d23c6c1d715727b6a_85_3.png)

**图 5.1** 使用视觉和红外进行人员检测的系统：(a) 视觉图像；(b) 视觉图像的背景减法掩码；(c) 红外图像；(d) 红外图像的背景减法掩码。（来自 Ros, J. and Mekhnakha, K., Multi-sensor human tracking with the Bayesian occupancy filter, *International Conference on Digital Signal Processing*, Santorini, Greece, 2009.）

## 5.3 图像创建

在传感器网络中有效使用图像需要理解图像是如何生成的。网络中使用了多种“类型”的图像。它们的区别在于使用的传感器不同，这些传感器记录了从根本上不同的信息。传感器可以根据其工作的能量光谱（光）、产生的数据维度，以及是主动式还是被动式进行分类。

![](img/11e8580124e6543d23c6c1d715727b6a_86_0.png)

**图 5.2** 描述了一个户外监控系统：(a) 原始图像，(b) 原始红外图像，(c) 经过斑块检测处理后的图像 (a)，以及 (d) 经过斑块检测处理后的图像 (b)。（来自 Foresti, G. and Snidaro, L., A distributed sensor network for video surveillance of video of outdoor environments, *International Conference on Image Processing*, pp. 525–528, New York, 2002.）

![](img/11e8580124e6543d23c6c1d715727b6a_86_1.png)

**图 5.3** 一个分布式传感器环境，其中机器人系统导航并尝试将箱子从一个位置推到另一个位置。同时使用了摄像头和激光测距仪。（来自 Verma, A. et al. Computational intelligence in robotics and automation. *Proceedings 2001 IEEE International Symposium on Computational Intelligence in Robotics and Automation*, pp. 212–217, Alberta, Canada, 2001.）

![](img/11e8580124e6543d23c6c1d715727b6a_86_2.png)

### 5.3.1 图像光谱

我们用“光电”相机捕捉的图像测量的是可见光光谱信息。图 5.5a 显示了光光谱以及人类可见光谱所在的位置。图 5.5 中的其他图像说明了采样该光光谱不同部分的传感器创建的图像。

最常用的图像来自测量可见光光谱的传感器。这一频段的名称来源于它是人类视觉的范围。我们常见的

![](img/11e8580124e6543d23c6c1d715727b6a_87_0.png)

(a) (b)

**图 5.4** 开发的系统... 此图显示了一个行人通过大门：(a) 静态摄像机的图像和 (b) 移动摄像机的图像。（来自 Marcenaro, L. et al., A multi-resolution outdoor dual camera system for robust video-event metadata extraction, FUSION 2002: Proceedings of the Fifth International Conference on Information Fusion, pp. 1184–1189, Annapolis, MD, 2002.）

| 伽马射线 | X射线 | 紫外线 | 光 | 红外 | 微波 | 射波 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |

(a) (b) (c) (d) (e) (f) (g) (h)

![](img/11e8580124e6543d23c6c1d715727b6a_87_1.png)

**图 5.5** 通过伪彩色图像像素值创建的一些图像：(a) 光谱，(b) 仙女座星系的可见图像，(c) (b) 的红外版本，(d) X射线图像，(e) 紫外图像，(f) 可见光图像，(g) 近红外图像，以及 (h) 射电图像。（图像由 NASA 提供，Multavelength milky way: Across the spectrum, http://adc.gsfc.nasa.gov/mmw_across.html Version 2, September 2001.）

对我们所看到的图像的理解，解释了为什么它可能是传感器网络中最常用的传感器。这些传感器通常被称为光电传感器或光学传感器。

网络系统中使用的另一种传感器是红外传感器。这种传感器具有对光谱中热（红外）区域敏感的元件。前视红外 (FLIR) 传感器对光谱中的热区域敏感。近外红外是光谱中与可见光最接近的部分。这种传感器通常用于夜视设备。

网络系统中使用的另一种传感器是紫外线传感器。这种传感器具有对光谱中紫外线区域敏感的元件。紫外线传感器常用于大气监测。
