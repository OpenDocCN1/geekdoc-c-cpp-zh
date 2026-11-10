
![](img/d9a4cc12c48f7466f309cbd3c4549c73_243_0.png)

**图6.6：** MATLAB模糊逻辑工具箱中的隶属函数。（a）三角形隶属函数（b）梯形隶属函数（c）简单高斯隶属函数（d）双边复合高斯隶属函数（e）广义钟形隶属函数（f）S形隶属函数（g）差分S形隶属函数（h）乘积S形隶属函数（i）Z曲线隶属函数（j）π曲线隶属函数（k）S曲线隶属函数

## 6.6.3 使用MATLAB代码模拟隶属函数

### 三角隶属函数

```matlab
y = trimf(x,params)
y = trimf(x,[a b c])
```

三角曲线是向量x的函数，依赖于三个标量参数a、b和c，如式(6.3)所示，更紧凑地表示为

$$f(x; a,b,c)=\max\left(\min\left(\frac{x-a}{b-a},\frac{c-x}{c-b}\right),0\right)$$

参数a和b确定了三角形的“底边”，参数c确定了“峰值”。

**代码**

```matlab
% Triangular membership function
x=0:0.1:10;
y=trimf(x,[3 6 8]);
plot(x,y)
xlabel('trimf, P=[3 6 8]');
title('Triangular Membership Function');
```

**输出**

由上述代码绘制的三角隶属函数如图6.7所示。

![](img/d9a4cc12c48f7466f309cbd3c4549c73_244_0.png)

**图6.7：** 三角隶属函数

### 梯形隶属函数

**语法**

```matlab
y = trapmf(x,[a b c d])
```

梯形曲线是向量x的函数，依赖于四个标量参数a、b、c和d，如式(6.7)所示，更紧凑地表示为

$$f(x;a,b,c,d)=\max\left(\min\left(\frac{x-a}{b-a},1,\frac{d-x}{d-c}\right),0\right)$$

参数a和d确定了梯形的“底边”，参数b和c确定了“肩部”。

**代码**

```matlab
% Trapezoidal membership function
x=0:0.1:10;
y=trapmf(x,[1 3 5 9]);
plot(x,y)
xlabel('trapmf, P=[1 3 5 9]')
title('Trapezoidal Membership Function');
```

**输出**

由上述代码绘制的梯形隶属函数如图6.8所示。

![](img/d9a4cc12c48f7466f309cbd3c4549c73_245_0.png)

**图6.8：** 梯形隶属函数

### 高斯隶属函数

**语法**

```matlab
y = gaussmf(x,[sig c])
```

对称高斯函数依赖于两个参数σ和c，如式(6.9)所示。`gaussmf` 的参数在向量 `[sig c]` 中按顺序表示参数σ和c。

**代码**

```matlab
% Gaussian membership function
x=0:0.1:10;
y=gaussmf(x,[1 6]);
plot(x,y)
xlabel('gaussmf, P=[1 6]')
title('Gaussian Membership Function');
```

**输出**

由上述代码绘制的高斯隶属函数如图6.9所示。

![](img/d9a4cc12c48f7466f309cbd3c4549c73_246_0.png)

**图6.9：** 高斯隶属函数

### 广义钟形隶属函数

**语法**

```matlab
y = gbellmf(x,params)
```

广义钟形函数依赖于三个参数a、b和c，如下所示：

$$f(x;a,b,c)=\frac{1}{1+\left|\frac{x-c}{a}\right|^{2b}}$$

其中参数b通常为正。参数c确定曲线的中心。参数向量 `params` 是 `gbellmf` 的第二个参数，其元素分别为a、b和c。

**代码**

```matlab
% Generalized Bell Shaped membership function
x=0:0.1:10;
y=gbellmf(x,[1 3 7]);
plot(x,y)
xlabel('gbellmf, P=[1 3 7]')
title('Generalized Bell Shaped Membership Function');
```

**输出**

由上述代码绘制的广义钟形隶属函数如图6.10所示。

![](img/d9a4cc12c48f7466f309cbd3c4549c73_247_0.png)

**图6.10：** 广义钟形隶属函数

### S形隶属函数

**语法**

```matlab
y = sigmf(x,[a c])
```

S形函数 `sigmf(x,[a c])` 是由下述 f(x,a,c) 给出的向量x上的映射，依赖于两个参数a和c。

$$f(x;a,c)=\frac{1}{1+e^{-a(x-c)}}$$

根据参数a的符号，S形隶属函数本质上是向右或向左开放的，因此适合表示“很大”或“很小”等概念。可以通过取两个不同S形隶属函数的乘积（psigmf）或差（dsigmf）来构造各种传统隶属函数。

**代码**

```matlab
% Sigmoidal Shaped membership function
x=0:0.1:10;
y=sigmf(x,[3 6]);
plot(x,y)
xlabel('sigmf, P=[3 6]')
title('Sigmoidal Shaped Membership Function');
```

**输出**

由上述代码绘制的S形隶属函数如图6.11所示。

![](img/d9a4cc12c48f7466f309cbd3c4549c73_248_0.png)

**图6.11：** S形隶属函数

### Z曲线隶属函数

**语法**

```matlab
y = zmf(x, [a b])
```

基于样条的函数之所以被称为Z形，是因为它的形状像字母Z。参数a和b确定了曲线倾斜部分的端点，如式(6.6)所示。

**代码**

```matlab
% Z Curve membership function
x=0:0.1:10;
y=zmf(x,[3 6]);
plot(x,y)
xlabel('zmf, P=[3 6]')
title('Z Curve Membership Function');
```

**输出**

由上述代码绘制的Z曲线隶属函数如图6.12所示。

![](img/d9a4cc12c48f7466f309cbd3c4549c73_250_0.png)

**图6.13：** π曲线隶属函数

曲线的倾斜部分的端点。

```matlab
% S Curve membership function
x=0:0.1:10;
y=smf(x,[1 8]);
plot(x,y)
xlabel('smf, P=[1 8]')
title('S Curve Membership Function');
```

**输出**

由上述代码绘制的S曲线隶属函数如图6.14所示。

![](img/d9a4cc12c48f7466f309cbd3c4549c73_250_1.png)

**图6.14：** S曲线隶属函数

## 6.6.4 使用MATLAB在隶属函数之间转换参数

要在隶属函数之间转换参数，MATLAB模糊逻辑工具箱中提供了一个函数 “mf2mf”。该函数的一般语法为

```matlab
outParams = mf2mf (inParams, inType, outType)
```

其中

- `inParams` - 待转换的隶属函数的参数
- `inType` - 待转换的隶属函数类型的字符串名称
- `outType` - 新的隶属函数类型的字符串名称

以下代码将多项式Z曲线隶属函数转换为三角隶属函数。

```matlab
x=0:0.1:5;
mfp1 = [1 2 3];
mfp2 = mf2mf(mfp1,'zmf','trimf');
plot(x,zmf(x,mfp1),x,trimf(x,mfp2))
```

得到的曲线如图6.15所示。

![](img/d9a4cc12c48f7466f309cbd3c4549c73_251_0.png)

**图6.15：** “mf2mf”函数的示意图

## 6.7 单点

严格来说，模糊集合D是一组有序对的集合

$$A=\{(x,\mu(x))\} \tag{6.11}$$

其中x属于论域，μ(x)是x在A中的隶属度。单独的一个有序对(x,μ(x))称为模糊单点；因此，整个集合可以看作是所有组成单点的并集。通常可以方便地将集合A视为一个向量

$$a = (\mu(x_1), \mu(x_2), \mu(x_3), \ldots, \mu(x_n)) \tag{6.12}$$

因此，这里理解为每个位置i（1,2,3,...,n）对应于包含n个点的论域中的一个点。

## 6.8 语言变量

就像代数变量以数值为值一样，语言变量以单词或句子为值。它可以取值的集合称为其术语集。术语集中的每个值都是定义在基变量上的模糊变量。基变量为术语集中的所有模糊变量定义了论域。简而言之，层次结构如下：语言变量 → 模糊变量 → 基变量。

### 示例4（术语集）

设x是一个标签为“年龄”的语言变量。该语言变量的项（即模糊集合）可以是术语集中的“老”、“年轻”、“非常年轻”。

$$T = \{Old, Very Old, Not So Old, More or Less Young, Quite Young, Very Young\}$$

每一项都是一个定义在基变量上的模糊变量，基变量可能是0到100岁的尺度。

## 6.9 模糊集合的运算

模糊集合运算是经典集合运算的推广。可能存在不止一种推广方式。最广泛使用的运算称为标准模糊集合运算。设U是一个域，A、B是U上的模糊集合。模糊集合有三种基本运算：

