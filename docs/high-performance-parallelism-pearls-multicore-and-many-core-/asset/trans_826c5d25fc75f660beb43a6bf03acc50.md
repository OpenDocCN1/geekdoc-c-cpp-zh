

# 双精度三叉树模型加速
归一化到单线程非向量化的 x5472(2007) 代码

![](img/16cb41208935c5f22dd1044f03f2e31b_473_0.png)

## 图 22.2

线程化代码与线程化+向量化代码之间的加速对比。

## 指令引导的向量化

对于希望利用支持SIMD的指令来提高性能的程序员，有多种方法可用。编译器内建函数（intrinsic operations）是一种选择，但它们与特定架构相关，而且往往难以使用。更简单的方法是使用编译器指令或pragma来注释C、C++或Fortran代码，并让编译器生成SIMD指令。

OpenMP 4.0 标准中提供的 SIMD 指令使程序员能够引导编译器决定何时使用以及使用哪些 SIMD 指令。在本节中，我们将通过示例演示 OpenMP 4.0 扩展的基本用法，并解释 SIMD 使能函数的使用。

## 循环向量化

图22.3展示了用C语言在Interpolate()函数中实现的线性样条插值方法。

大多数现代编译器都能应用自动向量化算法，判断循环是否可以被向量化，并在适当的时候执行向量化。

下面的向量化报告显示，图22.3中的关键循环未被向量化，因为编译器无法确定对Interpolate()函数的调用是否安全。编译器开关

```c
static const int steps = 512;
static const int ARRAY_SIZE = 4096;

int main(int argc, const char* argv[]) {
    point vals[steps+1];
    double src[ARRAY_SIZE];
    double dst[ARRAY_SIZE];

    /* Set interpolation array */
    double delta = 1.0 / steps;
    double delta_inv = 1./delta;

    vals[0].c0 = 0.;
    vals[0].c1 = erfc(0.);

    double prev_val = vals[0].c1;
    // Fill interpolation array
    for(int ind=1; ind <= steps; ++ind) {
        double x = ind * delta;
        double val = erfc(x);
        double c0 = (val - prev_val)*delta_inv;
        double c1 = val - c0*x;
        vals[ind].c0 = c0;
        vals[ind].c1 = c1;
        prev_val = val;
    }

    /* Initialize input array */
    ...
```

## **图 22.3**

线性样条的未优化 C 源代码。

```
/*Critical loop requires vectorization */
for(int i=0; i<ARRAY_SIZE;++i) {
    dst[i] = Interpolate(src[i],vals);
}

/* Print results */
/* . . . full code on lotsof cores.com . . . */
return 0;
}
```

```
//Implementation of Interpolate() and FindPosition()
double Interpolate(double x, point* vals){
    int ind = FindPosition(x);
    const point* pnt = &vals[ind];
    double res = pnt->c0*x+pnt->c1;
    return res;
}
```

```
/* . . . full code on lotsof cores.com . . . */int FindPosition(double x) {
    return (int)(x*steps);
}
```

## 图 22.3（续）

要获取这些报告，在 Linux 上使用 –qopt-report=5 –qopt-report-phase=vec，在 Windows 上使用 /Qopt-report=5 /Qopt-report-phase=vec。

```
remark #15382: vectorization support: call to function Interpolate(double, const point *) cannot be vectorized
[ main.c(56,18) ]
remark #15344: loop was not vectorized: vector dependence prevents vectorization
```

虽然报告中以粗体突出显示的消息对于不熟悉编译器的开发者来说有些晦涩，但它确实告诉我们，编译器无法解析与 Interpolate() 函数相关的所有依赖关系。在这种特定情况下，编译器的自动向量化算法需要依赖代码内联来解析循环次数以及潜在的数据、指针和循环依赖。由于 Interpolate() 函数不是内联函数，编译器采取了保守策略，决定不对循环进行向量化。

如图 22.4 所示，可以通过使用 OpenMP 4.0 C/C++ 的 #pragma omp simd 指令来强制进行向量化，该指令告诉编译器忽略内建的向量化启发式规则并对循环进行向量化。

应用 simd 指令并重新编译后，向量化报告包含如图 22.5 所示的消息。

编译器现在报告循环已被向量化，但无法找到合适的 Interpolate() 函数向量版本。因此，编译器使用了串行版本。为了提供帮助，编译器建议程序员添加一条 “declare simd” 指令，将 Interpolate() 标识为支持向量的函数。

```
//Critical loop
#pragma omp simd
for(int i=0; i<ARRAY_SIZE;++i) {
    dst[i] = Interpolate(src[i],vals);
}
```

## 图 22.4

应用 #pragma omp simd 以强制向量化。

```
LOOP BEGIN at main.c(55,9)
...
remark #15525: call to function 'Interpolate' is serialized
    [ main.c(56,18) ]
remark #15301: OpenMP SIMD LOOP WAS VECTORIZED
...
remark #15489: --- begin vector function matching report ---
remark #15490: Function call: Interpolate(double, const point *)
    with simdlen=2, actual parameter types:
    (vector,uniform)[ main.c(56,18) ]
remark #15545: SIMD annotation was not seen, consider adding
    'declare simd' directives at function declaration
remark #15493: --- end vector function matching report ---
LOOP END
```

## 图 22.5

对关键循环应用 #pragma omp simd 后的报告。

## SIMD 使能函数

在向量循环中调用 SIMD 使能函数意味着该函数的多个连续实例并行执行。用 OpenMP 的术语来说，这些向量函数对 simdlen() 数据块进行操作，就好像它们被编译为向量循环体的一部分一样。

能够创建可链接的独立向量函数（而不是作为内联函数编译）意味着，程序员现在可以创建独立的向量库，这些库可以作为二进制文件分发，而不是包含完整源代码的头文件。这对商业软件开发的优势显而易见，利用模块化编程技术的能力也同样如此。

OpenMP 4.0 中 SIMD 使能函数的语法为 omp declare simd [clauses]，在 C/C++ 中前面加上 #pragma，在 Fortran 中前面加上 !$omp。该 pragma 接受若干子句，这些将在后续章节中讨论。每个子句都提供额外的信息和细节，使编译器能够针对合适的处理器架构生成高效、有针对性的向量代码。

默认情况下，SIMD 操作的宽度由函数返回类型决定。此外，编译器默认还会生成针对 SSE2 CPU 架构的代码，该架构使用 128 位向量寄存器。

以下向量化报告是使用默认值生成的。它显示编译器找不到函数 `FindPosition` 的合适向量版本。

```
remark #15397: Suitable vector variant of function 'FindPosition' was not found [ interpolate.c(16,15) ]
```

不兼容的原因在于 Interpolate() 的返回类型是 double，这意味着 SIMD 元素计数（也称为 simdlen）默认设置为 2（因为编译器当前默认是 SSE）。FindPosition() 的返回类型是 int，这意味着它的 simdlen 为 4（同样是由于编译器默认 SSE）。因此，依赖默认值会导致两个向量函数之间的调用约定不兼容（例如 simdlen 为 2 对 4），因此编译器告诉我们，它找不到函数 FindPosition() 的“合适变体”。

OpenMP 4 标准提供了 simdlen() 子句，可在函数调用期间修改默认的 SIMD 元素数量。如图 22.6 所示，我们使用 simdlen() 子句来修改 FindPosition() 函数的 SIMD 元素数量。

重新编译后，我们发现向量化警告（图 22.7）已从向量化报告中消失。我们还看到，报告确认关键循环已被向量化。

```
#pragma omp declare simd
double Interpolate(double x, point* vals);
/* . . . full code on lotsof cores.com . . . */
#pragma omp declare simd simdlen(2)
int FindPosition(double x);
/* . . . full code on lotsof cores.com . . . */
```

## 图 22.6

在函数声明中将 Interpolate() 和 FindPosition() 标识为 SIMD 使能函数。

