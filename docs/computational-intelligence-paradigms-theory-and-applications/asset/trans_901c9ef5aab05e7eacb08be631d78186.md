

```matlab
else
    net.weightsnew.index = ones(1,2*net.D);
end

net.weightsnew.index = net.beta*(min(input,net.weights{new.index})) + ...
    (1-net.beta)*net.weightsnew.index;

net.labels(new.index) = input.label;
network.changed = true;
end
end % samples loop

if ~network.changed
    fprintf(1,'Network trained in %d epochs.\n',e);
    break
end
end % epochs loop
```

### 观察结果

```text
tnet =
D : 2
max_categories : 100
vigilance : 0.7500
alpha : 1.0000e-003
epochs : 10
beta : 1
weights : [ ]
labels : [ ]
epsilon : 1.0000e-003
singlePrecision : 0
```

```text
tnet =
D : 2
max_categories : 100
vigilance : 0.7500
alpha : 1.0000e-003
epochs : 1
```

**表 10.1：训练样本**

| 训练样本 | 原型数量 | 耗时（秒） |
|---:|---:|---:|
| 100 | 20 | 0.047000 |
| 200 | 27 | 0.047000 |
| 300 | 29 | 0.062000 |
| 400 | 29 | 0.047000 |
| 500 | 31 | 0.063000 |
| 600 | 33 | 0.062000 |
| 700 | 34 | 0.063000 |
| 800 | 35 | 0.062000 |
| 900 | 37 | 0.063000 |
| 1000 | 38 | 0.063000 |

```text
beta : 1
weights : 1x38 cell
labels : [2 1 2 2 1 2 2 1 2 1 1 1 2 2 1 1 1 2
          2 1 1 2 1 2 1 2 2 2 1 1 2 2]
epsilon : 1.00000e-003
singlePrecision : 0
```

命中率：96.000000

**表 10.2：测试样本**

| 测试样本 | 命中数 | 耗时（秒） |
|---:|---:|---:|
| 10 | 10 | 0.00 |
| 20 | 20 | 0.00 |
| 30 | 30 | 0.02 |
| 40 | 39 | 0.00 |
| 50 | 49 | 0.00 |
| 60 | 58 | 0.02 |
| 70 | 68 | 0.00 |
| 80 | 77 | 0.00 |
| 90 | 86 | 0.02 |
| 100 | 96 | 0.00 |

## 10.2 示例 2：模糊 C 均值聚类——对比案例研究

本程序展示了两个层次的模糊 C 均值聚类。FCM 聚类通常比 Otsu 方法效果更好，后者在荧光图像上输出的阈值偏大或偏小。

```matlab
- - - - - - - - - - - - - - - - - - - - - - - - -
% Main Program
- - - - - - - - - - - - - - - - - - - - - - - - -
clear; close all;
im=imread('cell.png');
J = filter2(fspecial('sobel'), im);
fim=mat2gray(J);
level=graythresh(fim);
bwfm=im2bw(fim,level);
[bwfim0,level0]=fcmthresh(fim,0);
[bwfim1,level1]=fcmthresh(fim,1);
subplot(2,2,1);
imshow(fim);title('Original');
subplot(2,2,2);
imshow(bwfm);title(sprintf('Otsu,level=%f', ...
             level));
subplot(2,2,3);
imshow(bwfim0);title(sprintf('FCM0,level=%f', ...
             level0));
subplot(2,2,4);
imshow(bwfim1);title(sprintf('FCM1,level=%f', ...
             level1));
- - - - - - - - - - - - - - - - - - - - - - - - -
% Subprograms
- - - - - - - - - - - - - - - - - - - - - - - - -
function [bw,level]=fcmthresh(IM,sw)
% Thresholding by fuzzy c-means clustering
% [bw,level]=fcmthresh(IM,sw) outputs the binary
%   image bw and threshold level of
%   image IM using a fuzzy c-means clustering.
% sw is 0 or 1, a switch of cut-off position.
% sw=0, cut between the small and middle class
% sw=1, cut between the middle and large class
% check the parameters
if (nargin<1)
    error('You must provide an image.');
elseif (nargin==1)
    sw=0;
elseif (sw~=0 && sw~=1)
    error('sw must be 0 or 1.');
end

data=reshape(IM,[],1);
[center,member]=fcm(data,3);
[center,cidx]=sort(center);
member=member';
member=member(:,cidx);
[maxmember,label]=max(member,[],2);
if sw==0
    level=(max(data(label==1))+min(data(label==2)))/2;
else
    level=(max(data(label==2))+min(data(label==3)))/2;
end
bw=im2bw(IM,level);
```

### 观察结果

图 10.1 展示了原始图像和聚类后的图像。将模糊 C 均值聚类与 Otsu 方法进行比较，可以看出 FCM 的性能优于 Otsu 方法。阈值根据切换截断位置取 0 或 1。如果阈值水平为 0，则在较小类与中间类之间进行截断；如果阈值水平为 1，则在中间类与较大类之间进行截断。

![](img/d9a4cc12c48f7466f309cbd3c4549c73_431_0.png)

**图 10.1：** 使用 Otsu 方法和 FCM 方法进行聚类的图

## 10.3 示例 3——K 均值聚类

本示例展示了使用 MATLAB 实现 K 均值算法，对给定图像进行聚类并形成重新聚类后的图像。

```matlab
% MATLAB Code
fprintf('\n Execution Starts...');

clear;
close all;
% Size Of The Image
wd=256;

X=im2double(imread('ALLPICDATA.bmp'));
X=imresize(X,[wd wd]);
X=im2uint8(X);
X=double(X);

mean1 = mean(mean(X(:,:,1)));
mean2 = mean(mean(X(:,:,2)));
mean3 = mean(mean(X(:,:,3)));

mean_mat = [mean1 mean2 mean3];
[dum,dom]=max(mean_mat);

switch dom
    case 1
        plane1=2;
        plane2=3;
    case 2
        plane1=1;
        plane2=3;
    case 3
        plane1=1;
        plane2=2;
end

PP=X(:,:,dom);

no_of_cluster = 5;
ipimage=PP;
e=0.03;
thrd=e*mean(mean(ipimage));

% Initial Centroids
miniv = min(min(ipimage));
maxiv = max(max(ipimage));
range = maxiv - miniv;
stepv = range/no_of_cluster;
incrval = stepv;
for i = 1:no_of_cluster
    K(i).centroid = incrval;
    incrval = incrval + stepv;
end

imax=size(ipimage,1);
jmax=size(ipimage,2);

% Initialization Starts...here...
for i=1:imax
    for j=1:jmax
        opimage(i,j).pixel=ipimage(i,j);
    end
end

loop=1;
for ii=1:no_of_cluster
    dist(ii)=K(ii).centroid;
end
while dist>thrd
    temp=K;
    % Initial Clustering...
    for i=1:imax
        for j=1:jmax
            for k=1:no_of_cluster
                diff(k)=abs(ipimage(i,j)-K(k).centroid);
            end
            [y,ind]=min(diff);
            opimage(i,j).index=ind;
        end
    end

    % New Centroids...
    summ=zeros(no_of_cluster,1);
    count=zeros(no_of_cluster,1);

    sum1 = zeros(no_of_cluster,1);
    sum2 = zeros(no_of_cluster,1);

    for i=1:imax
        for j=1:jmax
            for k=1:no_of_cluster
                if(opimage(i,j).index==k)
                    summ(k)=summ(k)+opimage(i,j).pixel;
                    sum1(k)=sum1(k)+X(i,j,plane1);
                    sum2(k)=sum2(k)+X(i,j,plane2);
                    count(k)=count(k)+1;
                end
            end
        end
    end

    % Update Centroids...
    for k=1:no_of_cluster
        K(k).centroid=summ(k)/count(k);
    end
    fprintf('\nNew Loop...');
    loop=loop+1
    clear dist;
    % New distance...
    for ii=1:no_of_cluster
        dist(ii)=abs(temp(ii).centroid-K(ii).centroid);
    end
end
% End Of while Loop

for k=1:no_of_cluster
    OtherPlane1(k).centroid=sum1(k)/count(k);
    OtherPlane2(k).centroid=sum2(k)/count(k);
end
% Resultant Image
reimage=zeros(wd,wd,3);
for i=1:imax
    for j=1:jmax
        reimage(i,j,dom) = K(opimage(i,j).index).centroid;
        reimage(i,j,plane1) = OtherPlane1(opimage(i,j).index).centroid;
        reimage(i,j,plane2) = OtherPlane2(opimage(i,j).index).centroid;
    end
end

% End Of K-Means Algorithm...

% Results...
for k=1:no_of_cluster
    rimage=zeros(imax,jmax,3);
    for i=1:imax
        for j=1:jmax
            if opimage(i,j).index==k
                rimage(i,j,dom) = K(k).centroid; % opimage(i,j).pixel;
                rimage(i,j,plane1) = OtherPlane1(k).centroid;
                rimage(i,j,plane2) = OtherPlane2(k).centroid;
            end
        end
    end
    strbuf = sprintf('Cluster No %d ',k);
    figure,imshow(uint8(rimage));
    title(strbuf);
end

figure;
```

![](img/d9a4cc12c48f7466f309cbd3c4549c73_435_0.png)

**图 10.2：** 输入图像

```matlab
imshow(uint8(reimage));title('Re Clustered Image');
fprintf('\n Done...');
```

### 观察结果

图 10.2 至图 10.8 展示了原始图像和聚类后的图像。

![](img/d9a4cc12c48f7466f309cbd3c4549c73_435_1.png)

**图 10.3：** 聚类图像 1

![](img/d9a4cc12c48f7466f309cbd3c4549c73_436_0.png)

**图 10.4：** 聚类图像 2

![](img/d9a4cc12c48f7466f309cbd3c4549c73_436_1.png)

**图 10.5：** 聚类图像 3

![](img/d9a4cc12c48f7466f309cbd3c4549c73_437_0.png)

**图 10.6：** 聚类图像 4

![](img/d9a4cc12c48f7466f309cbd3c4549c73_437_1.png)

**图 10.7：** 聚类图像 5

