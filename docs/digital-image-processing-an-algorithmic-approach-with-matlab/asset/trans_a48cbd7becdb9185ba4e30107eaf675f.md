

![](img/fc093ca9cc8a631842aa559a749dca54_260_0.png)

图 13.5 互相关法目标检测。(a) 目标以虚线矩形突出显示的灰度图像，并也在插图中复现，(b) 相关后的灰度图像，(c) 后处理后的图像。

场景。在此情况下，选定特定的树冠图像作为目标，并使用卷积方法在整个图像中定位它。然后对得到的图像进行阈值处理以提取最大相关点，最终得出树木计数。

该技术同样应用于图 13.2(a) 的示例图像，结果如图 13.5 所示。如图 13.5 所示，由于卷积漂移，精确位置略微偏离目标图像中心。

## 13.6 基于颜色的跟踪

基于颜色跟踪对象是从一帧图像跟踪到下一帧图像最快、最简单的方法之一。该技术的速度使其非常适合近实时应用，但由于其简单性，存在许多可能导致跟踪失败的问题。

在此背景下，可以使用基于颜色的分类方法（如第 12 章所述）。首先，使用交互式或自动化方法定义主要目标对象的颜色。所有其他颜色（包括背景和其他不需要的伪影）被识别为一个或多个具有相同代表伪彩色的类。分类结果是一个二值图像，目标对象以一种颜色显示（此处示例中为红色），而其他所有内容则以不同颜色显示。

图 13.6 显示了使用图形 ROI 函数进行类别选择的过程。图 13.7 显示了此类跟踪的结果。在此示例中，首先识别红色气球，并通过某种感兴趣区域（ROI）选择方法选定其颜色。同样，其他主要颜色也以相同方式识别，并分配相同的代表

![](img/fc093ca9cc8a631842aa559a749dca54_261_0.png)

![](img/fc093ca9cc8a631842aa559a749dca54_261_1.png)

![](img/fc093ca9cc8a631842aa559a749dca54_261_2.png)

![](img/fc093ca9cc8a631842aa559a749dca54_261_3.png)

图 13.6。（参见第 204 页后的彩色插页。）为基于颜色的跟踪声明各个类别。(a) 目标 1 以红色突出显示，(b) 目标 2 以蓝色突出显示，(c) 背景被突出显示，(d) 暗区域被突出显示。

类颜色，因此所有非目标伪影和背景都将由相同颜色表示，并显示为与实际目标类不同的完整类。

使用颜色处理获得的结果更快，并可以在相机级别嵌入机器视觉系统。目标颜色可以在采集级别过滤，此时可以阻止所有其他颜色，使只有选定的颜色到达传感器。这使得机器视觉系统的跟踪非常容易，因为大多数产生错误的元素已经被移除。

## 13.7 算法说明

前几节介绍的四种跟踪算法可以表示为流程图，用于在任何环境中进行编码。图 13.8–13.11 表示这些算法。

## 13.8 MATLAB 代码

本节介绍了用于生成图 13.2、13.3、13.5、13.6 和 13.7 中图像的 MATLAB 代码。我们从图 13.2 的背景减法方法开始：首先需要文件 track1.m 来生成必要的图像文件。但是，测试图像也存储在二进制文件中，即 x1.mat、x2.mat、x3.mat 和 x4.mat，分别对应单个红色对象、单个蓝色对象、两个对象和三个对象。

![](img/fc093ca9cc8a631842aa559a749dca54_263_0.png)

图 13.8 背景减法方法的算法逻辑。

![](img/fc093ca9cc8a631842aa559a749dca54_263_1.png)

图 13.9 时间帧减法方法的算法逻辑。

![](img/fc093ca9cc8a631842aa559a749dca54_264_0.png)

图 13.10 相关方法的算法逻辑。

```
% First Run track1.m to get the mat files
% This file uses background subtraction only
clear all
close all
load x1
bk = imread('p00.jpg') ;
XG = [] ;
XB = [] ;
ro = 480 ; co = 640 ;
for i = 1 : length(X1)/ro
  x = X1((i-1)*ro+i*ro,:,:) ;
  x = bk - x ;
  xg = rgb2gray(x) ;
  xg(ro-1:ro-2, 1:co) = 255 ;
  xb = im2bw(xg,0.1) ;
  XG = [ XG ; xg ] ;
  XB = [ XB ; xb ] ;
end
```

![](img/fc093ca9cc8a631842aa559a749dca54_265_0.png)

图 13.11 基于颜色的分类方法的算法逻辑。

```
figure ; imshow(X1)
figure ; imshow(XG)
figure ; imshow(XB)
```

对于图 13.3 的时间帧减法策略，使用了以下代码：

```
% First Run track1.m to get the mat files
% This file uses inter-frame difference
clear all
close all
load x1
bk = imread('p00.jpg') ;
XG = [] ;
YB = [] ;
Z1G = [] ;
Z1B = [] ;
ro = 480 ; co = 640 ;
for i = 1 : length(X1)/ro
x = X1((i-1)*ro+1:i*ro,:, :) ;
X = bk - x ;
xg = rgb2gray(x) ;
xg(ro:1:ro-2, 1:co) = 255 ;
xb = im2bw(xg, 0.1) ;
XG = [ XG ; xg ] ;
XB = [ XB ; xb ] ;
if i > 1
y = X1((i-2)*ro+1:(i-1)*ro,:, :) ;
y = y - bk ;
yg = rgb2gray(y) ;
zig = yg - xg ;
zig = yg - zig ;
z1b = im2bw(zig, 0.01) ;
Z1G = [ Z1G ; zig ] ;
Z1B = [ Z1B ; z1B ] ;
end
end
```

```
figure ; imshow(X1)
figure ; imshow(Z1G*100)
figure ; imshow(Z1B)
```

```
% Post-processing
ZZB = medfilt2(Z1B,[3 3]) ;
y = bwmorph(ZZB,'dilate',5) ;
ZZB = medfilt2(y,[15 15]) ;
y = bwmorph(ZZB,'erode',7) ;
figure ; imshow(y)
```

相关方法使用傅里叶变换方法实现，所需代码如下：

```
% First Run track1.m to get the mat files
% This file uses correlation of target in grayscale
clear all
close all
load x3
X1 = X3 ;
bk = imread('p00.jpg') ;
XG = [] ;
Z1G = [] ;
Z1B = [] ;
ro = 480 ; co = 640 ;
p = 3 ; % image # (select 4 for single object (xi.mat) or 3 for two object (x3.mat) case
xm = X1((p-1)*ro+1:p*ro,:,:) ;
xm = bk - xm ;
xmg = rgb2gray(xm) ;
figure ; imshow(xmg) ;
rect = getrect(gca) ;
xmm = xm(rect(2):rect(2)+rect(3)-1,rect(1):rect(1)+rect(4)-1) ;
XMM = fft2(double(xmm),1024,1024) ;
figure ; imshow(xmm*10)
for i = 1 : length(X1)/ro
    x = X1((i-1)*ro+1:i*ro,:,:) ;
    x = bk - x ;
    xg = rgb2gray(x) ;
    y = xg ;
    y(ro:1:ro-2, 1:co) = 255 ;
    XG = [ XG ; y ] ;
    XMM = fft2(double(xg),1024,1024) ;
    Y = XMG .* XMM ;
    y = ifft2(Y) ;
    y = y(1:ro,1:co) ;
    x = y*0.0000004 ;
    z=im2bw(x) ;
    z = bwmorph(z,'erode',19) ;
    Z1G = [ Z1G ; x ] ;
    Z1B = [ Z1B ; z ] ;
end
figure ; imshow(Z1G)
figure ; imshow(Z1B)
```

最后，基于颜色的分类代码：

```
% First Run track1.m to get the mat files
% This file uses color classification method
clear all
close all

load x3
X1 = X3 ;
bk = imread('p00.jpg') ;
X = [ ] ;
XC = [ ] ;
ZIG = [ ] ;
ZIB = [ ] ;
S = 10 ;
```

```
ro = 480 ; co = 640 ;
p = 2 ; % image #
X = X1((p-1)*ro+1:p*ro,:,:) ;
x = x - bk ;
x = x * S ;
figure ; imshow(x) ;

[r,c,s] = size(x) ;
```

```
% Initialize storage for each sample region.
classes = { 'target1','target2','background' , 'dark' } ;
nclasses = length(classes) ;
sample_regions = false([r c nclasses]) ;
```

```
% Select each sample region.
f = figure ;
for count = 1:nClasses
    set(f, 'name', 'Select sample region for ' classes{count}) ;
    sample_regions(:,:,count) = roipoly(x) ;
end
close(f) ;
```

```
for i = 1 : length(X1)/ro
    x = X1((i-1)*ro+1:i*ro,:,:) ;
    % Convert the RGB image into an L*a*b* image
    x = x - bk ;
```

