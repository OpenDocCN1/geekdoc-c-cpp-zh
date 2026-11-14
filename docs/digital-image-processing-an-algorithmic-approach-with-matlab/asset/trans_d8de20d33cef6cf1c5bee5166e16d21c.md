

![](img/fc093ca9cc8a631842aa559a749dca54_294_0.png)

### 图 15.6 模糊聚类算法。

## 15.3 算法说明

前一节介绍的两个示例可以分别根据图 15.6 和 15.7 所示的逻辑进行编程。

## 15.4 MATLAB 代码

本节介绍了用于生成图 15.4 和 15.5 中图像的 MATLAB 代码。

```matlab
% Unsupervised Classification with Fuzzy C-Mean
% Only input from user is the number of classes (N)
close all
clear all
N = 5 ; % Number of classes
x=imread('onion.png');
figure ; imshow(x)
y = rgb2gray(x);
figure ; imshow(y)
z = double(y) ;
[r,c] = size(y) ;
Z = im2col(z,[1 1])' ;
[center,U,obj_fcn] = fcm(Z,N) ;
c1 = sort(center,max(center)) ;
bn = (c1(2:N) - c1(1:N-1) ) / 2 + c1(1:N-1) ;
colors = [ 255 0 0 ; 0 255 0 ; 0 0 255 ; 255 255 0 ; 255 0 255 ; 0 255 255 ; 255 255 255 ; 0 0 0 ] ;
Y = x ;
for j = 1 : 3
Y(:,:,j) = colors(N,j) ;
end
for i = 1 : length(bn)
z = col2im(U(i,:),[1 1],[r c]) ;
[A,B] = find(z>=bn(i)) ;
for k = 1 : length(A)
    for j = 1 : 3
        Y(A(k),B(k),j) = colors(i,j) ;
    end
end
end
figure ; imshow(Y)

% Filtering
close all
clear all
x=imread('onion.png') ;
figure ; imshow(x)
y = rgb2gray(x);
figure ; imshow(y)

z = imnoise(y,'gaussian',0.1) ; % actual noisy version
yn = imnoise(y,'gaussian') ; % low noise version
figure ; imshow(z)

y = double(y) ;
yn = double(yn) ;
z = double(z) ;
[r,c] = size(y) ;
Y = im2col(y,[1 1])' ;
YN = im2col(yn,[1 1])' ;
Z = im2col(z,[1 1])' ;

delayed_Y = [0 ; Y(1:length(Y)-1)] ;
trn_data = [delayed_Y YN Z] ;
% Generating the initial PIS
mf_n = 3;
ss = 0.3;
in_fismat=genfis1(trn_data, mf_n);
% Using ANFIS to finetune the initial PIS
out_fismat = anfis(trn_data, in_fismat, [nan nan ss]) ;
% Testing the tuned model with training data
estimated_n2 = evalfis(trn_data(:, 1:2), out_fismat) ;
estimated_X = Z - estimated_n2;
yf = col2im(estimated_n2,[1 1],[r c]) ;
figure ; imshow(yf*0.004)
```

![](img/fc093ca9cc8a631842aa559a749dca54_295_0.png)

### 图 15.7 模糊去噪逻辑。

![](img/fc093ca9cc8a631842aa559a749dca54_298_0.png)

## 15.5 总结

- 软计算代表了解决与建模、估计和模式识别相关的工程问题的非传统方法。
- 一般来说，软计算的领域涵盖模糊逻辑、神经网络、遗传和进化算法、群体智能、混沌理论及类似技术。
- 软计算可应用于图像处理中的特定任务。
- 本章介绍了模糊逻辑及其在图像分类和去噪中的应用。
- 对于分类，使用了模糊 C 均值聚类算法。
- 对于去噪，使用了带有参考图像的模糊推理系统来近似输入图像像素。
- 使用了 MATLAB 的模糊逻辑工具箱来实现算法。
- 同样，神经网络也可用于这两个应用。
- 也可以使用其他软计算方法。但是，哪种方法更好将取决于问题的性质。
- 通常，更好的方法是混合技术，以利用每种方法的最佳特性。

## 15.6 练习

- 1. 使用神经网络作为主要决策者而非邻域规则，重复第 15.2.3 节讨论的去噪应用。对主网络使用 NEWPNN 函数。可参考图 15.7 以进一步澄清。
- 2. 使用以下一组核，并制定一组 if-then-else 规则来决定前景像素是否为 1。
- 3. 使用 MATLAB 中的 RBFNN 函数实现问题 #2。

## 参考文献

Abeyratne, U. R., Petropulu, A. P., and Reid, J. M. “基于高阶频谱的超声图像去卷积” IEEE Transactions on Ultrasonics, Ferroelectrics, and Frequency Control 42, no. 6 (1995): 1064-1075.

Ahn, H., and Yagle, A. E. “基于离散 Radon 变换将问题分解为耦合的一维问题的二维盲去卷积。” Proceedings of the International Conference on Image Processing (1995): 37-40.

Amari, S., Cichocki, A., and Yang, H. H. “一种用于盲信号分离的新学习算法。” In D. Touretzky, M. Mozer, and M. Hasselmo (Eds.) 神经信息处理系统进展 8. Cambridge, MA: MIT Press, 1996, pp. 757-763.

Arlt, B. and Brause, R. “图像的主要独立成分。” Internal Report 1/98, J. W. Goethe-Universität Frankfurt, Germany, 1998, http://www.informatik.uni-frankfurt.de/fbreports/OL_98.ps.gz.

Ballard, D. H. “将霍夫变换推广以检测任意形状。” 模式识别, 13 (1981): 111-122.

Ballard, D. H., and Brown, C. 计算机视觉. Englewood Cliffs, NJ: Prentice Hall, 1982.

Banham, M. R., and Katsaggelos, A. K. “数字图像恢复。” IEEE Signal Processing Magazine (March 1997): 24-41.

Banham, M. R., and Katsaggelos, A. K. “基于空间自适应小波的多尺度图像恢复。” IEEE Transactions on Image Processing 5, no. 4 (1996): 619-634.

Barlow, H. B. “无监督学习。” 神经计算, (1989): 295-311.

Bartlett, M. S. and Lades, H. M. “Sejnowski: 用于人脸识别的独立成分表示。” Proceedings of the SPIE Symposium on Electronic Imaging (in press) 1998.

Bennett, J., and Khotanzad, A. “多光谱随机场图像模型的最大似然估计方法。” IEEE Transactions on Pattern Analysis and Machine Intelligence, 21, no. 6 (1999): 337-543.

Bernd J. 科学应用图像处理实用手册. CRC Press, New York, 1997.

Burns, J. B., Weiss, R. S., and Riseman, E. M. “点集和线段特征的视图变化。” IEEE Transactions on Pattern Analysis and Machine Intelligence, 15, no. 1 (1993): 51-68.

Comon, P. “独立成分分析——一个新概念？” 信号处理, 36 (1994): 287–314.

Cristianini, N., Shawe-Taylor, J., and Kandola, J. “用于聚类的谱核方法,” in T. G. Dietterich, S. Becker, and Z. Ghahramani (Eds.) 神经信息处理系统进展 14. Cambridge MA: MIT Press, 2002.

Davies, E. R. 机器视觉——理论、算法与实践. New York: Academic Press, 1990.

Demoment, G. “图像重建与恢复：常见估计结构和问题概述。” IEEE Transactions on Acoustics, Speech, and Signal Processing, 37, no. 12 (1989): 2024–2036.

Dhawan, A. P., Rangarayan, R. M., and Gordon, R. “有限视角计算机断层扫描中的维纳去卷积图像恢复。” Applied Optics, 24, no. 23 (1985): 4013–4020.

Drury, Stephen A. “地质学中的图像解释,” Chap. 5 in 数字图像处理, 3rd ed. New York: Routledge, 2001.

Duda, R. O. and Hart, P. E. “使用霍夫变换检测图片中的线条和曲线。” Communications of the ACM, 15 (1972): 11–15.

Duda, R. O., Hart, P. E., and Stork, D. G. 模式分类, 2nd ed. New York: Wiley, 2001.

Fyfe, C., and Lai, P. L. “使用核规范相关分析的 ICA.” In International Workshop on Independent Component Analysis and Blind Signal Separation (ICA2000), Helsinki, June 2000.

Galatsanos, N. P., Katsaggelos, A. K., Chin, R. T., and Hillery, A. D. “多通道图像的最小二乘恢复。” IEEE Transactions on Signal Processing 39, no. 10 (1993): 2222–2236.

Gonzalez, R. C., and Woods, R. E. 数字图像处理. New York: Addison-Wesley Publishing Company, 1992.

Gonzales, R. C., Woods, R. E., and Eddins, S. L. 使用 MATLAB® 进行数字图像处理. Upper Saddle River, NJ: Pearson Education Inc., 2004.

Harikumar, G., and Bresler, Y. “来自多个 FIR 模糊的精确图像去卷积。” IEEE Transactions on Image Processing 8, no. 6 (1999): 846–862.

Harikumar, G., and Bresler, Y. “被多个滤波器模糊的图像的完美盲恢复：理论与高效算法。” IEEE Transactions on Image Processing 8, no. 2 (1999): 202–219.

Horn, R. A., and Johnson, C. R. 矩阵分析. Cambridge, UK: Cambridge University Press, 1985.

Horn, R. A., and Johnson, C. R. 矩阵分析专题. Cambridge, UK: Cambridge University Press, 1991.

Huang, T. S., Schreiber, W. F., and Tretiak, O. J. “图像处理。” Proceedings of the IEEE 59, no. 11 (1972): 1586–1609.

Javidi, B., Caulfield, H. J., and Horner, J. L. “通过非线性信号处理进行图像去卷积。” Applied Optics 28, no. 15 (1989): 3106–3111.

Jensen, J. R. “入门数字图像处理：遥感视角,” Chap. 8 in 主题信息提取：图像分类. Upper Saddle River, NJ: Prentice Hall, 1996.

