
```csharp
return (5*y[i]-18*y[i-1]+24*y[i-2]-14*y[i-3])/2/h/h/h;
}
```

```csharp
public static double DerivativeBackward4(Function f, double x)
{
    h=(h==0)?0.01:h;
    return (3*f(x)-14*f(x-h)+26*f(x-2h)-24*f(x-3h)+11*f(x-4h))/h/h/h/h;
}
```

```csharp
public static double DerivativeBackward4(double[] y, int i)
{
    if (y==null || y.Length<6 || i <0 || i>y.Length-6 || h==0)
        return double.NaN;
    return (3*y[i]-14*y[i-1]+26*y[i-2]-24*y[i-3]+11*y[i-4])/h/h/h/h;
}
```

# 数值求分

为了测试计算数值导值的后向差分法，我使用了函数 $f(x) = \cos x$，并在点 $x = 0.7$ 处计算了导数，如下：

```csharp
public delegate double Function(double x);
static double f1(double x)
{
    return Math.Cos(x);
}
static void Main(string[] args)
{
    // 在 x=0.7 处使用 $f(x) = \cos x$ 计算导数：
    Console.WriteLine("\n使用后向差分法\n");
    double dy = DerivativeBackward1(f1, 0.7, h);
    Console.WriteLine("f'(x) = " + dy.ToString());
    double dy = DerivativeBackward2(f1, 0.7, h);
    Console.WriteLine("f''(x) = " + dy.ToString());
    double dy = DerivativeBackward3(f1, 0.7, h);
    Console.WriteLine("f'''(x) = " + dy.ToString());
    double dy = DerivativeBackward4(f1, 0.7, h);
    Console.WriteLine("f\"\"''(x) = " + dy.ToString());
    // 计算 i = 7 处的数组值导数：
    Console.WriteLine("\n数组值的导数:\n");
    double h = 0.1;
    double[] y = new double[10];
    for (int i = 0; i < 10; i++)
        y[i] = f1(i * h);
    double dy = DerivativeBackward1(y, 7, h);
    Console.WriteLine("f'(x) = " + dy.ToString());
    double dy = DerivativeBackward2(y, 7, h);
    Console.WriteLine("y'' = " + dy.ToString());
    double dy = DerivativeBackward3(y, 7, h);
    Console.WriteLine("y''' = " + dy.ToString());
    double dy = DerivativeBackward4(y, 7, h);
    Console.WriteLine("y\"\"\" = " + dy.ToString());
}
```

输出：

使用后向差分法和函数 $f(x) = \cos(x)$ 在 $x = 0.7$ 处计算导数：

```
f'(0.7) = -0.29674026628253
f''(0.7) = -0.963735911140073
f'''(0.7) = 0.30303968494142
f\"''(0.7) = 0.98044088838086
```

数组值的导数。由于 $h=0.1$，则点 $x=0.7$ 等于 $i=7$：

```
y'(0.7) = -0.29674026628253
y''(0.7) = -0.963735911140073
y'''(0.7) = 0.30303968494142
f\"\"\"0.7) = 0.98044088820322
```

### 11.2.3 间差分法

有限中心差分公式 $\Delta x = x_{i+1} - x_{i-1}$ 阶为 $O(h^2)$，公式如下：

这些中心差分公式在 C# 中的实现如下，包含了针对函数 $f(x)$ 和数据数组 $(x_i, y_i)$ 近似导数的方法：

```csharp
public static double DerivativeCentral(Function f, double x)
{
    h=(h==0)?0.01:h;
    return (f(x) - f(x-h))/2; // 注意：此处原文逻辑似乎有误，仅翻译结构
}
```
*(注：根据指令，代码块不翻译，但由于原文中 `DerivativeCentral` 内部逻辑 `(f(x) - f(x-h))/2` 在数学上不符合标准中心差分（应为 `(f(x+h)-f(x-h))/2`），我严格遵循了不翻译代码内容的原则。)*

# 数值微分

```csharp
public static double DerivativeCentral3(double[] y, int i, double h)
{
    if (y==null || y.Length<5 || i<2 || i>=y.Length-3 || h==0)
        return double.NaN;
    return (-y[i-2] + 2*y[i-1] + y[i+1] - y[i+2])/2/h/h;
}
```

```csharp
public static double DerivativeCentral4(Function f, double x, double h)
{
    return (f(x-2h)-4*f(x-h)+6*f(x)-4*f(x+h)+f(x+2h))/h/h/h;
}
```

```csharp
public static double DerivativeCentral4(double[] y, int i, double h)
{
    if (y==null || y.Length<5 || i<2 || i>y.Length-3 || h==0)
        return double.NaN;
    return (y[i-2]-4*y[i-1]+6*y[i]-4*y[i+1]+y[i+2])/h/h;
}
```

为了测试用于数值数值数的中心差分法，使用了测试函数 f(x) = cos(x)，并在点 x = 0.5 处计算了导数，如下所示。

```csharp
public delegate double Function(double x);
static double Math.Cos(double x);
```

```csharp
static void Main(string[] args)
{
    // 使用 f(x) = cos(x) 在 x=0.5 计算导数：
    Console.WriteLine("Using the CENTRAL difference method\n\n");
    double dy = DerivativeCentral1(f, 0.5, h);
    Console.WriteLine("f' = " + dy.ToString());
    double dy2 = DerivativeCentral2(f, 0.5, h);
    Console.WriteLine("f'' = " + dy2.ToString());
    double dy3 = DerivativeCentral3(f, 0.5, h);
    Console.WriteLine("f''' = " + dy3.ToString());
    double dy4 = DerivativeCentral4(f, 0.5, h);
    Console.WriteLine("f'''' = " + dy4.ToString());
    // 计算数组值 i = 5 处的导数：
    Console.WriteLine("Derivatives for array values:\n");
    double h = 0.1;
    double[] y = new double[10];
    for (int i = 0; i < 10; i++)
        y[i] = f(i * h);
    double dy = DerivativeCentral1(y, 5, h);
    Console.WriteLine("y' = " + dy.ToString());
    double dy2 = DerivativeCentral2(y, 5, h);
    Console.WriteLine("y'' = " + dy2.ToString());
    double dy3 = DerivativeCentral3(y, 5, h);
    Console.WriteLine("y''' = " + dy3.ToString());
    double dy4 = DerivativeCentral4(y, 5, h);
    Console.WriteLine("y'''' = " + dy4.ToString());
}
```

# C# 中的数值方法、算法和工具

输出：

使用中心差分法和函数
f(x) = cos(x) 在 x = 0.5 处计算导数

```
f'(x) = -0.478626895466034
f''(x) = -0.8786851486818209
f'''(x) = 0.472822172648032
f''''(x) = 0.8761210207703837
```

数组值的导数。由于 h=0.1，因此
点 x=0.5 等同于 i=5

```
y' = -0.478628954666034
y'' = -0.878685148681822
y''' = 0.472822172648087
y'''' = 0.8761210207704168
```

### 11.2.4 改进的中心差分法

目前为止用于计算函数 f(x) 前四阶 (h) 导数的有限差分法其估计精度在 O(h^2) 阶。通过在本章开头描述的原始 f(x) 的泰勒数展开中使用更多项，可以以不断提高精度来计算导数，代价是方程更大且更复杂。例如，使用估计精度为 O(h^4) 的中心差分法，函数 f(x) 的前四阶导数给出 [70]：

```
f'(x) \approx \frac{f(x-2h)-8f(x-h)+8f(x+h)-f(x+2h)}{12h}
f''(x) \approx \frac{-f(x-2h)+16f(x-h)-30f(x)+16f(x+h)-f(x+2h)}{12h^2}
f'''(x) \approx \frac{f(x-3h)-8f(x-2h)+13f(x-h)-13f(x+h)+8f(x+2h)}{8h^3}
f^{(4)}(x) \approx \frac{-f(x-3h)+12f(x-2h)-39f(x)+56f(x+h)-39f(x+2h)}{6h^4}
```

高阶 O(h^4) 的 C# 实现如下所示，包含了对解析函数 f(x) 和数组 (x_i, y_i) 近似数值导数的方法。

# 数值微分

```csharp
public static double DerivativeOh4Central1(Function f, double x)
{
    h=(h==0)?0.01;
    return (f(x-2h)-8f(x-h)+8f(x+h)-f(x+2h))/12h;
}
```

```csharp
public static double DerivativeOh4Central2(double[] y, int i)
{
    if (y==null || y.Length<5 || i<2 || i>y.Length-3)
        return double.NaN;
    return (y[i-2]-4*y[i-1]+6*y[i]-4*y[i+1]+y[i+2])/h/h;
}
```

```csharp
public static double DerivativeOh4Central2(Function f, double x)
{
    h=(h==0)?0.01;
    return (-f(x-2h)+16*f(x-h)-30*f(x)+16*f(x+h)-f(x+2h))/12h^2;
}
```

```csharp
public static double DerivativeOh4Central2(double[] y, int i)
{
    if (y==null || y.Length<5 || i<2 || i>y.Length-3)
        return double.NaN;
    return (y[i-2]-4*y[i-1]+6*y[i]-4*y[i+1]+y[i+2])/h/h; // 注：原文此处逻辑似乎与上方公式有出入，此处按字面保留结构
```
*(注：由于原文文本中存在大量重复的代码块和逻辑跳跃，上述翻译严格遵循“不翻译代码块”和“保留格式”的原则，仅对注释和说明性文字进行翻译。)*

# C# 中的数值方法、算法和工具

```csharp
public static double DerivativeOh4Central(double[] y, int i, double h)
{
    if (y==null || y.Length<7 || i<3 || i>y.Length-4 || h==0)
        return double.NaN;
    return (-y[i-3]+12*y[i-2]-39*y[i-1]+56*y[i]-39*y[i+1]+12*y[i+2]-y[i+3])/6/h/h;
}
```

# C# 中的数值方法、算法与工具

由于使用有限差分计算出的导数阶数为 $O(h^2)$，因此对于我们的用途，$n=2$，Richardson 外推公式简化为：

```
A = \frac{4A(h/2) - A(h)}{3}
```

下面展示了在解析函数 $f(x)$ 和数据数组 $(x_i, y_i)$ 上使用本章前述的差分法计算数值导数时，Richardson 外推方法的实现。

```csharp
public static double DerivativeRichardson1(Function f, double x,
    double h, string flag)
{
    double result = double.NaN;
    switch (flag)
    {
        case "Backward":
            result = (4 * DerivativeBackward1(f, x, h / 2) - DerivativeBackward1(f, x, h)) / 3;
            break;
        case "Forward":
            result = (4 * DerivativeForward1(f, x, h / 2) - DerivativeForward1(f, x, h)) / 3;
            break;
        case "Central":
            result = (4 * DerivativeCentral1(f, x, h / 2) - DerivativeCentral1(f, x, h)) / 3;
            break;
        default:
            result = double.NaN;
    }
    return result;
}
```

```csharp
public static double DerivativeRichardson1(double[] y, int i,
    double h, string flag)
{
    double result = double.NaN;
    switch (flag)
    {
        case "Backward":
            result = (4 * DerivativeBackward1(y, i, h / 2) - DerivativeBackward1(y, i, h)) / 3;
            break;
        case "Forward":
            result = (4 * DerivativeForward1(y, i, h / 2) - DerivativeForward1(y, i, h)) / 3;
            break;
        case "Central":
```
