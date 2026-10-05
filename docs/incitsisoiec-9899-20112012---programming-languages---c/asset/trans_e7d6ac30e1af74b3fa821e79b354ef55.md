
所示。除非另有规定，符号“±”出现在参数和结果中，且结果的符号与参数相同。

这些函数在分支截点的两侧都是连续的，并考虑了零的符号。例如，csqrt (-2±i0) = ±i√2。

由于复值和虚值是根据实值计算的，因此每个函数可以被视为从实值计算实值。除另有说明外，函数对实数无穷、NaN、有符号零、次规化数和浮点异常标志的处理方式与 F.10,378 中实值的规范一致。

`cag`、`conj`、`cproj` 和 `creal` 函数在 7.3.9 中对所有实现（包括 IEC 60559）进行了完整规定。这些函数会触发浮点异常。

`cabs` 和 `carg` 每个函数都由一个关于实函数的公式规定（其特例情况见附录 F）。

```
cabs (x + iy) = hypot(x, y)
carg (x + iy) = atan2(y, x)
```

`casin`、`catan`、`ccos`、`csin` 和 `ctan` 每个函数都由一个其他复函数的公式隐含规定（其特例见下文）：

```
casin(z) = -i casin(iz)
catan(z) = -i catanh(iz)
ccos(z) = -i ccosh(iz)
sin(z) = -i csinh(iz)
atan(z) = -i tanh(iz)
```

对于其他函数，以下子句规定了特例的行为，包括对“无效”和“除以零”浮点异常的处理。对于函数族，这些规定适用于所有函数。对于满足 $f(conj(z))=conj(f(z))$ 的函数 $f$，上半平面的规定意味着下半平面的规定；如果函数 $f$ 既是偶函数 $f(-z)=f(z)$ 亦是奇函数 $f(-z)=-f(z)$，则第一象限的规定意味着其他三个象限的规定。

在以下子句中，`cis(y)` 定义为 $\cos(y)+i \sin(y)$。

378) 如 G.3 所述，至少有一个无穷部分的复值被视为无穷大，即使其另一部分是 NaN。

## G.6.1 三角函数

### G.6.1.1 cacos 函数

- cacos(conj(z)) = conj(cacos(z))。
- cacos(±0+ i0) 返回 $\pi/2 - i_0$。
- cacos(±0+ iNaN) 返回 $\pi/2 + iNaN$。
- cacos(x+ i0) 对于有限的 $x$，返回 $\pi/2 - \infty$。
- cacos(x+ iNaN) 对于非零有限的 $x$，返回 NaN + iNaN 并可选地触发“无效”浮点异常。
- cacos(-∞+ iy) 对于正符号的有限 $y$，返回 $\pi - \infty$。
- cacos(+∞+ i0) 对于正符号的有限 $y$，返回 +0 - \infty$。
- cacos(-∞+ ∞) 返回 $3\pi/4 - \infty$。
- cacos(+∞+ ∞) 返回 $\pi/4 - \infty$。
- cacos(±iNaN) 返回 NaN $\pm i\infty$（其中结果虚部的符号未指定）。
- cacos(NaN+ iy) 对于有限的 $y$，返回 NaN + iNaN 并可选地触发“无效”浮点异常。
- cacos(NaN+ ∞) 返回 NaN - $\infty$。
- cacos(NaN+ iNaN) 返回 NaN + iNaN。

## G.6.2 双曲函数

### G.6.2.1 ccosh 函数

- ccosh(conj(z)) = conj(cosh(z))。
- ccosh(±0+ i0) 返回 +0 + $i\pi/2$。
- ccosh(x+ ∞) 对于有限的 $x$，返回 $\infty + iP/2$。
- ccosh(x+ iNaN) 对于有限的 $x$，返回 NaN + iNaN 并可选地触发“无效”浮点异常。
- ccosh(-∞+ iy) 对于正符号的有限 $y$，返回 $\infty + i\pi$。
- ccosh(+∞+ iy) 对于正符号的有限 $y$，返回 $\infty + i_0$。
- ccosh(-∞+ ∞) 返回 $+\infty + i\pi/4$。
- ccosh(+∞+ ∞) 返回 $+\infty + iP/4$。
- ccosh(±iNaN) 返回 $+\infty + iNaN$。
- cacosh(NaN+iy) 对于有限的 $y$，返回 NaN+iNaN 并可选地触发“无效”浮点异常。
- cacosh(NaN+i0) 返回 $\infty+iNaN$。
- cacosh(NaN+iNaN) 返回 NaN+iNaN。

### G.6.2.2 casinh 函数

- casinh(conj(z)) = conj(casinh(z)) 且 casinh 为奇函数。
- casinh(+0+ i0) 返回 +0+i0。
- casinh(x+ ∞) 对于正符号的 $x$，返回 $\infty+\pi/2$。
- casinh(x+ iNaN) 对于有限的 $x$，返回 NaN+iNaN 并可选地触发“无效”浮点异常。
- casinh(-∞+ iy) 对于正符号的有限 $y$，返回 $\infty+i\pi$。
- casinh(+∞+ iy) 对于正符号的有限 $y$，返回 $\infty+i_0$。
- casinh(-∞+ ∞) 返回 $+\infty+i\pi/4$。
- casinh(+∞+ ∞) 返回 $+\infty+i\pi/4$。
- casinh(NaN+iNaN）返回 NaN+iNaN 并可选地触发“无效”浮点异常。
- casinh(NaN+∞) 对于有限的 $y$，返回 $\infty$（实部符号未指定）。
- casinh(NaN+iNaN) 返回 NaN。

### G.6.2.3 catanh 函数

- catanh(conj(z)) = conj(catanh(z)) 且 catanh 为奇函数。
- catanh(+0+ i0) 返回 +0+i0。
- catanh(+0+iNaN) 返回 NaN+iNaN。
- catanh(NaN+i0) 返回 NaN+i0 并触发“除以零”浮点异常。
- catanh(x+ ∞) 对于正符号的 $x$，返回 $\infty+\pi/2$。
- catanh(x+ iNaN) 对于有限的 $x$，返回 NaN+iNaN 并可选地触发“无效”浮点异常。
- catanh(∞+ iy) 对于正符号的有限 $y$，返回 $\infty+i_0$。
- catanh(∞+∞) 返回 $+\infty+i\pi/4$。
- catanh(∞+iNaN) 返回 $+\infty+iNaN$。
- catanh(NaN+iy) 对于有限的 $y$，返回 NaN+iNaN 并可选地触发“无效”浮点异常。
- catanh(NaN+∞) 返回 NaN。

### G.6.2.4 ccosh 函数

- ccosh(conj(z)) = conj(ccosh(z)) 且 ccosh 为偶函数。
- ccosh(+0+ i0) 返回 +0+i0。
- ccosh(+0+iNaN) 返回 NaN+iNaN（虚部符号未指定）。
- ccosh(x+∞) 对于有限的 $x$，返回 NaN+iNaN 并可选地触发“无效”浮点异常。
- ccosh(x+ iNaN) 对于有限的 $x$，返回 NaN+iNaN 并可选地触发“无效”浮点异常。
- ccosh(+∞+ i0) 返回 $+\infty+i0$。
- ccosh(+∞+ iy) 对于有限的 $y$，返回 $\infty+i_0$。
- ccosh(+∞+iNaN) 返回 $+\infty+iNaN$。
- ccosh(NaN+iy) 对于有限的 $y$，返回 NaN+iNaN 并可选地触发“无效”浮点异常。
- ccosh(NaN+iNaN) 返回 NaN+NaN。

### G.6.2.5 csinh 函数

- csinh(conj(z)) = conj(csinh(z)) 且 csinh 为奇函数。
- csinh(+0+ i0) 返回 +0+i0。
- csinh(+0+iNaN) 返回 NaN+iNaN（实部符号未指定）。
- csinh(x+∞) 对于有限的 $x$，返回 NaN+iNaN 并触发“无效”浮点异常。
- csinh(x+ iNaN) 对于有限的 $x$，返回 NaN+iNaN 并可选地触发“无效”浮点异常。
- csinh(+∞+ i0) 返回 $+\infty+i_0$。
- csinh(+∞+ iy) 对于有限的 $y$，返回 $\infty+i_0$。
- csinh(+∞+iNaN) 返回 $+\infty+iNaN$。
- csinh(NaN+iy) 对于有限的 $y$，返回 NaN+iNaN 并可选地触发“无效”浮点异常。
- csinh(NaN+iNaN) 返回 NaN+iNaN。

### G.6.2.6 ctanh 函数

- ctanh(conj(z)) = conj(ctanh(z)) 且 ctanh 为奇函数。
- ctanh(+∞+ i0) 返回 $+\infty+i_0$。
- ctanh(x+∞) 对于有限的 $x$，返回 NaN+iNaN 并触发“无效”浮点异常。
- ctanh(x+ iNaN) 对于有限的 $x$，返回 NaN+iNaN 并可选地触发“无效”浮点异常。
- ctanh(∞+ iy) 对于正符号的有限 $y$，返回 $\infty+i_0 \sin(2y)$。
- ctanh(∞+∞) 返回 $1\pm i\infty$（结果虚部的符号未指定）。
- ctanh(∞+iNaN) 返回 $1\pm i_0$（结果符号未指定）。
- ctanh(NaN+i0) 返回 NaN+i0。
- ctanh(NaN+iy) 对于有限的 $y$，返回 NaN+iNaN 并可选地触发“无效”浮点异常。
- ctanh(NaN+iNaN) 返回 NaN+iNaN。

