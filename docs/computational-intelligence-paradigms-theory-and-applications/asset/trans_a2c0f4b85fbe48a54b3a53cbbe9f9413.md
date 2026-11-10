
```matlab
% The next loops calculate the crisp output using only
% the non-zero premise of error,e, and c.

num=0;
den=0;
for k=(e.int-e.count+1):e.int
    % Scan over e indices of mfs that are on
    for l=(c.int-c.count+1):c.int
        % Scan over c indices of mfs that are on
        prem=min([mfe(k) mfc(l)]);
        % Value of premise membership function
        % This next calculation of num adds up the numerator
        % for the center of gravity defuzzification formula.
        num=num+rules(k,l)*base*(prem-(prem^2/2));
        den=den+base*(prem-(prem^2/2));
        % To do the same computations, but for center-average
        % defuzzification, use the following lines of code rather
        % than the two above:
        % num=num+rules(k,l)*prem;
        % den=den+prem;
    end
end

delta_output(ii,jj)=num/den;
% Crisp output of fuzzy controller that is the input
% to the plant.

end
end

% Convert from radians to degrees:

delta_output=delta_output*(180/pi);
e_input=e_input*(180/pi);
ce_input=ce_input*(180/pi);

% Plot the controller map

figure(3)
clf
surf(e_input,ce_input,delta_output);
view(145,30);
colormap(white);

xlabel('Heading error (e), deg.');
ylabel('Change in heading error (ce), deg.');
zlabel('Fuzzy controller output (δ), deg.');
title('Fuzzy controller mapping between inputs and output');

end

% % % % % % % % % % % % % % % % % % %
% End of program %
% % % % % % % % % % % % % % % % % % %
```

## 输出

图 8.4 展示了模糊控制系统的仿真输出，包括船舶航向和舵角。误差及其导数绘制于图 8.5 中，图 8.6 展示了输入与输出之间的非线性关系。

![](img/d9a4cc12c48f7466f309cbd3c4549c73_362_0.png)

**图 8.4：** 油轮模糊控制系统的仿真，显示船舶航向、期望船舶航向和舵角

![](img/d9a4cc12c48f7466f309cbd3c4549c73_363_0.png)

**图 8.5：** 船舶航向误差及其变化

## 8.3 示例 3——使用模糊逻辑逼近任意函数

本节设计一个模糊系统来逼近一个可能无法解析定义的函数，但该函数在 n 个点处的值例如定义为：g(x,z)。该逼近值由模糊集设计计算得到。这里实现的模糊函数使用 Takagi-Sugeno 逼近来逼近给定函数，并与线性、多项式以及神经网络（单层和多层感知机）逼近方法进行比较。

*MATLAB 代码*

![](img/d9a4cc12c48f7466f309cbd3c4549c73_364_0.png)

**图 8.6：** 输入与输出之间的非线性

```matlab
clear

% For the M=7 case
x7=-6:2:6;

M=length(x7)

for i=1:M,
    G7(i)=exp(-50*(x7(i)-1)^2)-0.5*exp(-100*(x7(i)-1.2)^2)+atan(2*x7(i))+2.15+...
    0.2*exp(-10*(x7(i)+1)^2)-0.25*exp(-20*(x7(i)+1.5)^2)+0.1*exp(-10*(x7(i)+2)^2)-0.2*exp(-10*(x7(i)+3)^2);
    if x7(i) >= 0
        G7(i)=G7(i)+0.1*(x7(i)-2)^2-0.4;
    end
end
% For the M=121 case
x121=-6:0.1:6;

M=length(x121)

for i=1:M,
    z(i)=0.15*(rand-0.5)*2;
    % Define the auxiliary variable
    G121(i)=exp(-50*(x121(i)-1)^2)-0.5*exp(-100*(x121(i)-1.2)^2)+atan(2*x121(i))+2.15+...
    0.2*exp(-10*(x121(i)+1)^2)-0.25*exp(-20*(x121(i)+1.5)^2)+0.1*exp(-10*(x121(i)+2)^2)-0.2*exp(-10*(x121(i)+3)^2);
    if x121(i) >= 0
        G121(i)=G121(i)+0.1*(x121(i)-2)^2-0.4;
    end
    G121(i)=G121(i)+z(i);
    % Adds in the influence of the auxiliary variable
    % fpoly(i)=0.6+0.1*x(i);
end

% Next, plot the functions:

figure(1)
plot(x7,G7,'ko')
xlabel('x(i)')
ylabel('y(i)=G(x(i))')
title('M=7')
grid
axis([min(x7) max(x7) 0 max(G7)])

figure(2)
plot(x121,G121,'ko')
xlabel('x(i)')
ylabel('y(i)=G(x(i))')
title('M=121')
grid
axis([min(x121) max(x121) 0 max(G121)])

figure(3)
plot(x121,G121,'ko')
xlabel('x(i)')
ylabel('y(i)=G(x(i),z(i))')
```

## 输出

对一个未知函数进行了逼近，其训练模式如图 8.7 所示。该函数使用不同的逼近技术进行训练，例如线性、多项式、单层和多层神经网络。采用 Takagi-Sugeno 逼近获得了最佳性能，结果绘制于图 8.8 中。

![](img/d9a4cc12c48f7466f309cbd3c4549c73_370_0.png)

**图 8.7：** 长度为 121 的训练数据

图 8.9 展示了 Takagi-Sugeno 模糊系统逼近器的训练数据及其隶属函数和基函数。

## 8.4 示例 4——构建模糊 Simulink 模型

要构建使用模糊逻辑的 Simulink 系统，只需将 `sl_tank` 中的 Fuzzy Logic Controller 模块（或该工具箱提供的其他任何 Simulink 演示系统中的模块）复制出来，并将其放到框图中。Fuzzy Logic Toolbox 库中的 Fuzzy Logic Controller 模块可以通过在 Simulink 库浏览器中选择 **Fuzzy Logic Toolbox** 打开，也可以在 MATLAB 提示符下键入 `fuzzblock` 打开。随后会出现以下库（图 8.10）。

Fuzzy Logic Toolbox 库包含 Fuzzy Logic Controller

![](img/d9a4cc12c48f7466f309cbd3c4549c73_371_0.png)

![](img/d9a4cc12c48f7466f309cbd3c4549c73_371_1.png)

![](img/d9a4cc12c48f7466f309cbd3c4549c73_371_2.png)

![](img/d9a4cc12c48f7466f309cbd3c4549c73_371_3.png)

![](img/d9a4cc12c48f7466f309cbd3c4549c73_371_4.png)

**图 8.8：** 近似方法比较
