
# MATLAB 多维函数处理与优化

MATLAB 具有多种处理多维函数的能力。回想第 13 章，我们对一维搜索的视觉化就像过山车。对于二维情况，图像变成了山峰和山谷。在接下来的示例中，MATLAB 的图形化能力提供了一种可视化此类函数的方便方法。

## 示例 15.6 二维函数的可视化

**问题描述**。使用 MATLAB 的图形化能力显示以下函数，并估计在范围 $-2 \le x_1 \le 0$ 和 $0 \le x_2 \le 3$ 内的最小值：
$$f(x_1, x_2) = 2 + x_1 - x_2 + 2x_1^2 + 2x_1 x_2 + x_2^2$$

**解答**。以下脚本生成该函数的等线图和网格图：

```matlab
x = linspace(-2, 0, 20);
y = linspace(0, 3, 40);

[X, Y] = meshgrid(x, y);

Z = 2 - X + 2*Y + 2*X.^2 + 2*X.*Y + Y.^2;

subplot(1, 2, 1);
contour(X, Y, Z);
clabel(cs);
xlabel('x1');
ylabel('x2');
title('a) 等线图');
grid on;

subplot(1, 2, 2);
surface(X, Y, Z);
xlabel('x1');
ylabel('x2');
zlabel('f(x1,x2)');
title('b) 网格图');
```

如图 15.8 所示，两幅图都表明该函数有一个最小值 $f(x_1, x_2) = 1$，位于 $x_1 = -1$ 和 $x_2 = 1$。

标准 MATLAB 提供了 `fminsearch` 函数，可用于确定多维函数的最小值。它基于 Nelder-Mead 方法，这是一种仅使用函数值不需要导数的直接搜索方法，并且可以处理非光滑函数。其简单语法为：

```matlab
[xmin, fval] = fminsearch(function, x)
```

其中 `xmin` 和 `fval` 分别是最小值的位置和值，`function` 是被搜索的函数名，`x` 是初始猜测值（即搜索起始点）。

## 示例 15.5 使用 MATLAB 进行一维优化

**问题描述**。使用 MATLAB 的 `fminbnd` 函数找到示例 15.5 所示函数的最大值，在 $x = 0$ 和 $x = 4$ 的区间内。

**解答**。由于我们感兴趣的是最大化，因此我们输入函数的负值。我们通过以下命令调用 `fminbnd`：

```matlab
>> fminbnd('fx', 0, 4)
```

结果为：

```
f = -1.7757
x = 1.4275
```

注意，可以包含额外的参数。一个有用的补充是设置选项，例如误差容差或最大迭代次数。这是通过 `optimset` 函数实现的，之前在示例 7.6 中用过，其通用格式为：

```matlab
optimset('param', value, 'param', value, ...)
```

其中 `param` 是指定选项类型的参数，`value` 是分配给它的值。例如，如果你想将容差设置为 $1 \times 10^{-2}$：

```matlab
optimset('TolX', 1e-2)
```

因此，以 $1 \times 10^{-2}$ 的容差求解当前问题可以生成：

```matlab
>> fminbnd('fx', 0, 4, optimset('TolX', 1e-2))
```

结果为：

```
f = -1.7757
ans = 1.4270
```

## 15.3 使用软件包进行优化

可以通过如下方式调用 `help` 找到完整的参数集：

```matlab
>> help optimset
```

## 示例 15.7 使用 MATLAB 进行多维优化

**问题描述**。使用 MATLAB 的 `fminsearch` 函数找到以下函数的最大值：

$$f(x) = 2 \sin x - \frac{x^2}{2}$$

在 $x = 0$ 和 $x = 4$ 的区间内。回想在第 13 章中，我们使用了多种方法求解了 $x = 1.4276$ 且 $f(x) = 1.7757$ 的问题。

**解答**。首先，我们必须创建一个 M-文件来存储该函数。

```matlab
function f = fmfx(x)
    f = -(2*sin(x) - x^2/2);
end
```

由于我们感兴趣的是最大化，因此我们输入函数的负值。我们通过以下命令调用 `fminbnd`（注：一维有界优化应使用 `fminbnd`）：

```matlab
>> fminbnd('fmfx', 0, 4)
```

结果为：

```
f = -1.7757
x = 1.4275
```

注意，可以包含额外的参数。一个有用的补充是设置选项，例如误差容差或最大迭代次数。这是通过 `optimset` 函数实现的，之前在示例 7.6 中用过，其通用格式为：

```matlab
optimset('param', value, 'param', value, ...)
```

其中 `param` 是指定选项类型的参数，`value` 是分配给它的值。例如，如果你想将容差设置为 $1 \times 10^{-2}$：

```matlab
optimset('TolX', 1e-2)
```

因此，以 $1 \times 10^{-2}$ 的容差求解当前问题可以生成：

```matlab
>> fminbnd('fmfx', 0, 4, optimset('TolX', 1e-2))
```

结果为：

```
f = -1.7757
ans = 1.4270
```
