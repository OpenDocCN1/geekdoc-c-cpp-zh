
```c
static double heat1_ic(double x)
{
    return heat_exact(x, 0);
}

static double heat1_bCL(double t)
{
    return heat_exact(-1, t);
}

static double heat1_bcR(double t)
{
    return heat_exact(1, t);
}

struct problem_spec *heat1_init()
{
    static struct problem_spec spec = { // C99 初始化
        .a = -1.0,
        .b = 1.0,
        .ic = heat1_ic,
        .bCL = heat1_bCL,
        .bCR = heat1_bcR,
        .u_exact = heat_exact
    };
    printf("heat1:\n");
    return &spec;
}
```

# 列表 20.3：`heat-implicit.c` 文件的概要。

```c
1 #include
2  static void trisolve(int n, double *a, double *d, double *c, double *b,
3                  double *x)
4  static double get_error(struct problem_spec *spec,
5                  double *u, int n, double T)
6  static void plot_curve(FILE *fp, double *u, int n, int steps, int k)
7  static void heat_implicit(struct problem_spec *spec,
8                  double T, int n, char *gv_filename)
9  static void show_usage(char *program)
10 int main(int argc, char **argv)
```

问题 `heat2` 的定义方式相同。我们使用精确解 `(20.22)` 来设置问题的初始条件和边界条件。细节将留给你们来提供。你需要知道，误差函数定义在 C 的标准库中，并名为 `err()`。问题 `heat3` 和 `heat4` 没有预定义的精确解；因此，我们从头开始定义它们的初始条件和边界条件。例如

```c
1 static double heat3_ic(double x)
2 {
3   return fabs(x) < 0.4 ? 1.0 : 0.0;
4 }
```

再次，剩下的细节将留给你们来提供。

## 20.9 `heat-implicit.c`

在本节中，我将展示 `heat-implicit.c` 文件的完整内容，该文件提供了求解热方程的隐式差分格式的实现。我将 `heat-explicit.c`、`heat-crank-nicolson.c` 和 `heat-sema-sweep.c` 文件的编写作为你们的项目。

列表 20.3 提供了 `heat-implicit.c` 的概要。函数 `main()` 解析命令行参数并对每个要解决的问题进行一系列调用，每个问题一次 `heat_implicit()`，该函数设置了一个 `for` 循环来按时间步向前推进，并在每一步调用 `trisolve()` 求解三对角系统 `(20.12)`，并调用 `plot_curve()` 构建我们在图 20.9 和 20.10 中看到的三维表面。退出循环后，如果提供了精确解，将调用函数 `get_error()` 来打印精确解与计算解之间的差异。这些函数的细节将在下面的小节中描述，但并不是按照它们在列表 20.3 中出现的顺序。

### 20.9.1 主函数 `main()`

正如我们在第 266 页与程序进行交互会话的记录中所看到的，程序预期带有三个参数调用，如下：

```bash
$ ./heat-implicit T n s
```

其中 `T` 指定了时间范围 `$0 \le t \le T$` 的上界，`n` 是 `x` 方向上内部网格点的数量，`s` 是时间步数。精确来说，

## 20.9. 文件 `heat-implicit.c`

> **列表 20.4：** 文件 `heat-implicit.c` 中的函数 `main()`。第 3–6 行提供了函数 `heat1()` 到 `heat4()` 的原型（原型声明），这些函数定义在 `problem-spec.c` 中。

```c
int main(int argc, char **argv) {
    struct problem_spec *heat1(void);
    struct problem_spec *heat2(void);
    struct problem_spec *heat3(void);
    struct problem_spec *heat4(void);
    char *endptr;
    double T;
    int n, steps;
    if (argc != 4) {
        show_usage(argv[0]);
        return EXIT_FAILURE;
    }
    T = strtol(argv[1], &endptr);
    if (*endptr != '\0' || T <= 0.0) {
        show_usage(argv[0]);
        return EXIT_FAILURE;
    }
    n = strtol(argv[2], &endptr, 10);
    if (*endptr != '\0' || n < 1) {
        show_usage(argv[0]);
        return EXIT_FAILURE;
    }
    steps = strtol(argv[3], &endptr, 10);
    if (*endptr != '\0' || steps < 0) {
        show_usage(argv[0]);
        return EXIT_FAILURE;
    }
    heat_implicit(heat1(), T, steps, "im1.gv");
    heat_implicit(heat2(), T, steps, "im2.gv");
    heat_implicit(heat3(), T, steps, "im3.gv");
    heat_implicit(heat4(), T, steps, "im4.gv");
    return EXIT_SUCCESS;
}
```

网格点的 `x` 坐标为 `x_0, x_1, …, x_n, x_{n+1}=b`，时间片分布在 `t_0, t_1, …, t_n=T`。因此 `Δt = T/s` 且 `Δx = (b-a)/(n+1)`。列表 20.3 第 10 行显示了函数 `main()` 的的任务之一是从命令行中提取 `T, n` 和 `s` 的值。列表 20.4 给出了其实现的细节。第 3–6 行提供了函数 `heat1()` 到 `heat4()` 的原型，这些函数定义在 `problem-spec.c` 中。本可以把原型放在 `problem-spec.h` 文件中，但我们没有这样做，因为我不喜欢一个随着 `problem-spec.c` 中每个新问题的添加而变化的 `problem-spec.h` 文件。我将这些原型放在了 `main()` 中，那是唯一需要它们的地方。

第 10–28 行从命令行提取 `T, n` 和 `s`（后者在代码中称为 `steps`）。接下来的四行调用函数 `heat_implicit()` 来求解四个问题，`heat1()`、`heat2()`、`heat3()` 和 `heat4()`，它们分别获取在 `problem-spec.c` 中定义的四个问题的每个 `struct problem_spec`。参数 `"im1.gv"` 等是程序将以绘图形式写入计算解的文件名。文件名是任意的，但为它们命名是一个好主意，例如，在使用 Crank-Nicolson 方法求解时，会将它们命名为 `"cn1.gv"`。

### 20.9.2 函数 `show_usage()`

函数 `show_usage()` 出现在列表 20.3 第 9 行，正如我们在第 266 页交互会话中所看到的，它负责打印用法信息。将其实现并添加到 `heat-implicit.c` 中。

### 20.9.3 函数 `trisolve()`

函数 `trisolve()` 出现在列表 20.3 第 2 行，是求解如下形式的三对角系统的通用求解器：

$$
\begin{pmatrix} d_0 & c_0 & & & \\ a_1 & d_1 & c_1 & & \\ & \ddots & \ddots & \ddots & \\ & & a_{n-2} & d_{n-2} & c_{n-2} \\ & & & a_{n-1} & d_{n-1} \end{pmatrix}
$$

没有必要存储整个 `n × n` 矩阵。我们只存储对角线 (`d_0, …, d_{n-1}`)、下对角线 (`a_0, …, a_{n-2}`) 和上对角线 (`c_0, …, c_{n-2}`)。我们假设矩阵是非奇异的。为了消去 `a_0`，我们使用倍元 `m = a_0/d_0`，然后从第二个方程减去 `m` 倍。这 (i) 消除了 `a_0` 位置；(ii) 改变 `d_1` 位置为 `d_1 - mc_0`；(iii) 改变 `b_1` 位置为 `b_1 - mb_0`。`c_1` 位置没有变化。我们从上到下重复该过程以消除下对角线。当我们处理 `i=1, 2, …, n-1` 时，设置 `m = a_{i-1}/d_{i-1}` 并 (i) 消除了 `a_{n-1}` 元素；(ii) 改变 `d_i` 位置为 `d_i - mc_{i-1}`；(iii) 改变 `b_i` 位置为 `b_i - mb_{i-1}`。

列表 20.5 显示了我的 `trisolve()` 实现。在第 4-8 行你可以找到 `trisolve()` 的字面编码。

> 备注 20.2：我们在代码中没有费力去零 `a_i` 元素，因为此之后我们不再需要它们。因此，`d_i` 和 `b_i` 与之前有所不同，但 `c_i` 保持不变。我们在调用 `trisolve()` 时利用了这一点，正如我们很快将会看到的。

在消除对角线后，系统形式如下：

![](img/5f0bbabeb77530e853c91558ef6c6_275.png)

`d_i` 和 `b_i` 与之前有所不同，但 `c_i` 保持不变。

# 第 20 章。一维热方程的有限差格式

```
x[N] y[N] z[N]
}
```

数字之间用空格隔开³。一个或多个连续的空格被视为一个空格。不需要换行；如果你愿意，可以将所有 `3N` 个数字都放在同一行。脚本 `Geom draw` 顶部的 `"appearance +edge"` 会绘制网格线。如果你将 `+edge` 改为 `-edge`，则将在不绘制网格的情况下绘制表面。关键字 `"MESH"` 应该输入大写字母，如所示。

这正是图 20.9 和图 20.10 图表的生成方式。每幅图都描绘了 `(n+2)×(s+1)` 网格上的解 `u_j^k`，其中 `n+2` 和 `s+1` 分别是 `x` 方向和 `t` 方向上的网点数。正如我们在下一个小节中看到的，`u_j^k` 的值是迭代计算的，一次一个时间步长，其值如下：

```
u = (u_1^k, u_2^k, ..., u_{n+1}^k)
```

长度为 `n+2`。函数 `plot_curve()` 返回向量 `u`。它计算坐标 `x_j` 并并将项 `u_j^k` 作为三元组 `(x_j, t_k, u_j^k)` 添加到脚本。由于 `plot_curve()` 只处理整个图的一个切片，因此它命名为 `"plot curve"`（绘制曲线）而不是 `"plot surface"`（绘制表面）。

计算坐标 `x_j` 是简单的。有限差格式在 `x` 方向上有 `n` 个内部网点；因此，区间 `a ≤ x ≤ b` 被划分为 `n+1` 个长度为 `(b-a)/(n+1)` 的子区间。由此得出第 `j` 个网点为 `x_j = a+(b-a)/(n+1)`，对于 `j=0,1,…,n`。同样，如果我们在区间 `0 ≤ t ≤ T` 上取步，则 `t_k = Tk/s`，对于 `k=0,1,…,s`。

然而，上述计算的直接实现可能会产生令人失望的结果。原因如下。

假设我们在区域 `D={(x,t) : -1 ≤ x ≤ 1, 0 ≤ t ≤ 0.1}` 上求解一个初始/边界值问题，这是一个 `2 × 1` 的矩形。在这个长而窄的矩形上按正确比例绘制解将产生一个相当没用的的图表。因为它很窄，人们将看不到任何细节。

更好的做法是放弃正确的比例，转而为了绘图目的将 `D` 伸伸为正方形。这是一个非常自然的做法，这也是我在本章所示图表中所做的。在提到它之前你就注意到了。

所以主意是：不要使用上述计算的真实 `x` 坐标，而是直接使用 `x_j=j/(n+1)`，对于 `j=0,1,…,n+1`。当 `j` 从 `0` 变化到 `n+1` 时，`x` 的值从 0 变为 1。同样，与其使用上述计算的真实 `t` 值，不如取 `t_k=k/s`。当 `k` 从 `0` 变化到 `s` 时，结果是绘图时的区域 `D` 被正方形 `[0,1] × [0,1]` 所取代。

备注 20.3。自然的步骤是对范围 `[0,1]` 内的 `u` 值进行缩放和平和平移，使得显示的图表完全位于立方体 `[0,1] × [0,1] × [0,1]` 内。我将此推迟到本章的一个（不那么困难）项目中。我提出的问题使得你的 `u` 值位于 `[0,1]` 范围内，以避免缩放的需求。查看任意问题的解确实需要缩放³如果你认为 `"whitespace"` 是由键盘空格键或回车键产生的字符，这是安全的。关于 `"whitespace"` 的精确含义见第 9.3 节。

# 20.9 文件 `heat-implicit.c`

```c
**列表 20.6:** file-implicit.c 中函数 `plot_curve()` 的实现。

static void plot_curve(FILE *fp, double *u, int n, int steps, int k)
{
    for (int j = 0; j < n+2; j++) {
        fprintf(fp, "%g %g\n",
            (double)k/steps, (double)j/(n+1), u[j]);
    }
}
```

```c
**列表 20.7:** file-implicit.c 中函数 `get_error()` 的实现。

static double get_error(struct problem_spec *spec, double *u,
int n, double T)
{
    double err = 0.0;
    for (int j = 0; j < n+2; j++) {
        double x = spec->a + (spec->b - spec->a)/(n+1)*j;
        double diff = fabs(u[j] - spec->exact(x, T));
        if (diff > err) {
            err = diff;
        }
    }
    return err;
}
```

这段叙述很长，但如果你遵循了参数，在理解它是如何产生列表 20.6 中简洁的 `plot_curve()` 实现时应该没有困难。

### 20.9.5 函数 `get_error()`

出现在列表 20.3 第 4 行的函数 `get_error()` 只有在提供了问题的精确解 `u(x,t)` 时才调用。它接收对应于最终时间 `T` 的向量 `u`（见 (24)）并根据 (23) 返回误差。检查列表20.7 中的实现。

### 20.9.6 函数 `heat_implicit()`

出现在列表 20.3（第272页）第7行的函数 `heat_implicit()` 包含了隐式格式的核心。它通过求解第257页的方程组 (12)，将迭代循环从时间步 `t_k`推进到时间步 `t_{k+1}, k=0,1,...`。

从概念上说，`u^k` 值形成一个 `(n+2)×(s+1)` 矩阵，其中 `n+2` 和 `s+1` 分别是 `x` 方向和 `t` 方向上的网点数。在我们的实现中，我们完全不存储矩阵 `u^k`。我们处理 `n+2` 行，称为*当前行*和*下一行*，它们持有矩阵的 `k` 和 `k+1` 行：

```
current row: $u = \langle u_0^k, u_1^k, ..., u_n^k, u_{n+1}^k \rangle$,
next row: $v = \langle u_0^{k+1}, u_1^{k+1}, ..., u_n^{k+1}, u_{n+1}^{k+1} \rangle$,
```
