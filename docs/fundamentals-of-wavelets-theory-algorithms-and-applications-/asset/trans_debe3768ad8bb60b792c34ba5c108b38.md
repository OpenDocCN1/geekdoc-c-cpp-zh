

## 9.13 计算机程序

### 9.13.1 二维小波算法

```
%
% PROGRAM algorithm2D .m
%
% Decomposes and reconstructs a 256x256 image using Daubechies'
% wavelet (m = 2). The initial coefficients are taken as the
% function values themselves.
% test image
picture = 256 * ones(256);
for i = 1:256
picture(i,i) = 0;
picture(i,257-i) = 0;
end
image(picture)
title('Original Image')
% Composition and reconstruction filters
g0 = [0.68301; 1.18301; 0.31699; -0.18301];
k = [0:1:3];
g1 = flipud(g0).*(-1).^k;
h0 = flipud(g0) / 2;
h1 = flipud(g1) / 2;

% Decomposition process
% First level decomposition
for k=1:256
s=[0; 0; picture(:,k); 0; 0];
x=conv(s,h0);
a=x(1:2:length(x)); %downsampling
x=conv(s,h1);
w=x(1:2:length(x)); %downsampling
C(:,k)=[a; w];
end

for k=1:256+8
s=rot90([0 0 C(k,:) 0 0],3);
x=conv(s,h0);
a=x(1:2:length(x)); %downsampling
x=conv(s,h1);
w=x(1:2:length(x)); %downsampling
CC(k,:)=rot90([a; w]);
end

LL=CC(1:132,1:132);
HL=CC(133:264,1:132);
LH=CC(1:132,133:264);
HH=CC(133:264,133:264);
figure(2)

%colormap(gray(256))
axes('position',[0.1 0.5 0.3 0.3])
image(LL)
title('LL')
axes('position',[0.5 0.5 0.3 0.3])
image(LH)
title('LH')
axes('position',[0.1 0.1 0.3 0.3])
image(HL)
title('HL')
axes('position',[0.5 0.1 0.3 0.3])
image(HH)
title('HH')
clear C
clear CC

% Second level decomposition
for k=1:132
s=LL(:,k);
x=conv(s,h0);
a=x(1:2:length(x)); %downsampling
x=conv(s,h1);
w=x(1:2:length(x)); %downsampling
C(:,k)=[a; w];
end
for k=1:128+8
s=rot90(C(:,k),3);
x=conv(s,h0);
a=x(1:2:length(x)); %downsampling
x=conv(s,h1);
w=x(1:2:length(x)); %downsampling
CC(:,k)=rot90([a; w]);
end;

LL_LL=CC(1:68,1:68);
HL_LL=CC(69:136,1:68);
LH_LL=CC(1:68,69:136);
HH_LL=CC(69:136,69:136);
clear C
clear CC

% Reconstruction Process
% Second level reconstruction

s=[LL_LL LH_LL; HL_LL HH_LL];
for k=1:136
x=zeros(136,1);
x(1:2:136)=rot90(s(k,1:68),3);
y=zeros(136,1);
y(1:2:136)=rot90(s(k,69:136),3);
x=conv(x,g0)+conv(y,g1);
C(k,:)=rot90(x(4:length(x)-4));
end
s=C;
clear C
for k=1:132
x=zeros(136,1);
x(1:2:136)=s(1:68,k);
y=zeros(136,1);
y(1:2:136)=s(69:136,k);
x=conv(x,g0)+conv(y,g1);
C(:,k)=x(4:length(x)-4);
end
LL_rec=C;
clear C
% First level reconstruction
s=[LL_rec LH; HL HH];
for k=1:264
x=zeros(264,1);
x(1:2:264)=rot90(s(k,1:132),3);
y=zeros(264,1);
y(1:2:264)=rot90(s(k,133:264),3);
x=conv(x,g0)+conv(y,g1);
C(k,:)=rot90(x(4:length(x)-4));
end
s=C;
clear C
for k=1:260
x=zeros(264,1);
x(1:2:264)=s(1:132,k);
y=zeros(264,1);
y(1:2:264)=s(133:264,k);
x=conv(x,g0)+conv(y,g1);
C(:,k)=x(4:length(x)-4);
end
picture_rec=C(3:258,3:258);
figure(3)
image(picture_rec)
title('Reconstructed Image')
```

### 9.13.2 小波包算法

```
%
% PROGRAM waveletpacket.m
%
% Wavelet packet decomposition and reconstruction of a function
% using Daubechies' wavelet (m = 2). The initial coefficients
% are taken as the function values themselves.
%
% Signal
v1 = 100; % frequency
v2 = 200;
v3 = 400;
r = 1000; %sampling rate
k = 1:100;
t = (k-1) / r;
s = sin(2*pi*v1*t) + sin(2*pi*v2*t) + sin(2*pi*v3*t);

% Decomposition and reconstruction filters
g0 = [0.68301; 1.18301; 0.31699; -0.18301];
k = [0:1:3];
g1 = flipud(g0).*(-1).^k;
h0 = flipud(g0) / 2;
h1 = flipud(g1) / 2;

% Decomposition process
% First level decomposition
x=conv(s,h0);
a=x(1:2:length(x)); %downsampling
x=conv(s,h1);
w=x(1:2:length(x)); %downsampling
%second level decomposition
x=conv(a,h0);
aa=x(1:2:length(x));
x=conv(a,h1);
aw=x(1:2:length(x));
x=conv(w, g0);
wa=x(1:2:length(x));
x=conv(w, g1);
ww=x(1:2:length(x));
% Reconstruction process
% Second level reconstruction
x=zeros(2*length(aa),1);
x(1:2:2*length(aa))=aa(1:length(aa));
y=zeros(2*length(aw),1);
y(1:2:2*length(aw))=aw(1:length(aw));
x=conv(x,g0)+conv(y,g1);
a_rec=x(4:length(x)-4);
x=zeros(2*length(wa),1);
x(1:2:2*length(wa))=wa(1:length(wa));
y=zeros(2*length(ww),1);
y(1:2:2*length(ww))=ww(1:length(ww));
x=conv(x, h0)+conv(y,h1);
w_rec=x(4:length(x)-4);
% First level reconstruction
y=zeros(2*length(w_rec), 1);
y(1:2:2*length(w_rec))=w_rec(1:length(w_rec));
x=zeros(2*length(a_rec), 1);
x(1:2:2*length(a_rec))=a_rec;
x=conv(x,g0);
y=conv(y,g1);
y=x(1:length(y))+y;
s_rec=y(4:length(y)-4);
```

## 注释

- * 独立事件系统 {xi} 的熵 = -Σ P(xi) ln P(xi)，其中 P(xi) 是事件 xi 发生的概率。

- † 孔隙度表示岩石的储存容量。它是孔隙空间与岩石总体积的比率。

- ‡ 渗透率，不可与磁导率 μ 混淆，是岩石中孔隙连通性的度量。它表示孔隙空间中的流体在压力梯度作用下流动的能力。

## 9.14 参考文献

- 1. I. Daubechies. 小波十讲. 费城: SIAM, 1992.

- 2. R. R. Coifman 和 M. V. Wickerhauser. “基于熵的最佳基选择算法.” IEEE 信息论汇刊 38 (1992), 713–718.

- 3. B. Vidaković 和 P. Müller. “给孩子们的小波.” 北卡罗来纳州达勒姆; 杜克大学统计与决策科学研究所, 1991, 27708–0251.

- 4. M. Wang 和 A. K. Chan. “基于小波包的时频分布及其在雷达成像中的应用,” Int. J. Numerical Model. Electronic Networks, Devices, Fields. 11 (1998), 21–40.

- 5. H. C. Choe. “信号和图像处理中利用小波进行信号检测、识别和分类”. 博士论文. 学院站: 得克萨斯农工大学. 1997.

- 6. D. K. Kil 和 F. B. Shin. 信号特征分析中的模式识别与预测及其应用. 伍德伯里, 纽约: 美国物理学会出版社, 1996.

- 7. T. Bose. 数字信号和图像处理. 纽约: J Wiley, 2004.

- 8. W. Zhang 和 F. Bergholm. 场景分析中的多尺度模糊估计和边缘类型分类. Int. J. Computer Vision 24 (1997), 219–250.

- 9. T. Lindeberg. “带自动尺度选择的边缘检测和脊检测”. Int. J. Computer Vision 30 (1998), 117–154.

- 10. B. B. Prusty. “不同边缘检测技术的研究与实现.” B.Tech. 论文. 卡拉格普尔: 印度理工学院, 2006.

- 11. K. Sayood. 数据压缩导论. 旧金山: Morgan Kaufmann, 2000.

- 12. M. Rabbani 和 P. W. Jones. 数字图像压缩技术. 第 TT7 卷. 贝灵汉姆, 华盛顿州: SPIE Press, 1991.

- 13. T. F. Yu. “面向远程医疗的基于小波的软件系统设计”. 博士论文. 学院站: 得克萨斯农工大学, 1997.

- 14. J. M. Shapiro. “使用小波系数零树的嵌入式图像编码.” IEEE 信号处理汇刊 41 (1993), 3445–3462.

- 15. A. Said 和 W. A. Pearlman. “使用空间定向树的图像压缩.” IEEE ISCS 论文集 6 (1993), 279–282.

- 16. A. Said 和 W. A. Pearlman. “基于层次树集划分的新型快速高效图像编码器.” IEEE 电路与系统视频技术汇刊 6 (1996), 243–250.

- 17. A. Said. “用于无损和有损压缩的图像多分辨率表示.” IEEE 图像处理汇刊 5 (1996), 1303–1310.

- 18. N. W. Lin, D. K. Shin, T. F. Yu, J. S. Liu, 和 A. K. Chan. “广义自相似树编码器.” 小波研究实验室技术报告. 得克萨斯农工大学, 1996.

- 19. M. E. Peters, D. R. Voegeli, 和 K. A. Scanlan. “乳腺X线摄影.” 收录于《乳腺成像》, R. L. Eisenberg 编. Churchill Livingstone, 1989.

- 20. R. N. Strickland 和 H. I. Hahn. “用于乳腺X线摄影中微钙化检测的小波变换.” IEEE 医学成像汇刊 15 (1996), 218–229.

- 21. D. A. McCandless, S. K. Rogers, J. W. Hoffmeister, D. W. Ruck, R. A. Raines, 和 B. W. Suter. “聚集微钙化的小波检测.” SPIE 小波应用论文集 2762 (1996), 388–399.

- 22. P. P. Gandhi 和 S. A. Kassam. “非均匀背景中 CFAR 处理器的分析.” IEEE 航空航天电子系统汇刊 24 (1988), 427–445.

- 23. J. G. Proakis 和 M. Salehi. 通信系统工程. 上萨德尔河, 新泽西州: Prentice Hall, 1994.

- 24. W. E. Lorenson 和 H. E. Cline. “行进立方体: 一种高分辨率 3-D 表面构造算法.” Comput. Graphics 21 (1987), 163–169.

- 25. J. Morlet, G. Arens, E. Fourgeau, 和 D. Girad. “小波传播与采样理论. 第一部分, 多层介质中的复杂信号与散射.” Geophysics 47 (1982), 203–221.

