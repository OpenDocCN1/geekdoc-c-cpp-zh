

```c
#pragma omp declare simd simdlen(2) \
    processor(core_i7_sse4_2)
#pragma omp declare simd simdlen(4) \
    processor(core_4th_gen_avx)
int FindPosition(double x);

#pragma omp declare simd uniform(vals) \
    processor(core_i7_sse4_2)
#pragma omp declare simd uniform(vals) \
    processor(core_4th_gen_avx)
double Interpolate(double x, const point* vals);
```

### 图 22.15：声明对多种架构的支持。

其中，使用 -x/(Qx) 指定的架构是最早的架构。例如，-xSSE4.2 -axAVX -axCORE-AVX2。

当指定多个架构时，编译器将为每个架构生成一个向量函数，在我们的示例中，即针对 SSE4.2、Intel AVX 和 Intel AVX2。图 22.15 列出了修改后的源代码。

下面来自 Intel 编译器的向量报告示例告诉我们，在使用 -xSSE4.2 和 -axCORE-AVX2 标志为两种架构编译时，它包含了一些函数（如 `main`）的自动派发代码。

```text
main.c(17): (col. 1) remark: main has been targeted for automatic
cpu dispatch
```

自动派发器是管理单个可执行文件中多个架构相关二进制的软件组件。它能够识别运行可执行文件的处理器架构，并适当地初始化内部变量（如派发表），以通过最高性能的执行路径来路由执行。

图 22.16 中的向量化报告显示，Intel 编译器为所有目标架构包含了详细信息。

## C++ 中的向量函数

在本节中，我们讨论在 C++ 中使用指令引导的向量化。C++ 类方法的向量化机制类似。然而，有几点需要特别关注。在本节中，我们通过声明一个 `Interpolator` 类来扩展 C 代码示例，如图 22.17 所示。

不幸的是，C++ 虚方法无法被向量化，因为它们以函数指针的形式实现，驻留在虚表中。无法保证虚表中的所有指针都指向相同类类型的对象，这使得虚函数无法向量化。

```text
...
remark #15489: --- begin vector function matching report ---
remark #15490: Function call: Interpolate(double, const point *)
    with simdlen=8, actual parameter types:
    (vector,uniform)  [ main.c(56,18) ]
remark #15492: A suitable vector variant was found (out of 4)
    with ymm2, simdlen=4, unmasked, formal parameter
    types: (uniform,vector)
remark #15493: --- end vector function matching report ---
...
remark #15489: --- begin vector function matching report ---
remark #15490: Function call: Interpolate(double, const point *)
    with simdlen=8, actual parameter types:
    (vector,uniform)  [ main.c(56,18) ]
remark #15492: A suitable vector variant was found (out of 4)
    with xmm, simdlen=2, unmasked, formal parameter
    types: (uniform,vector)
remark #15493: --- end vector function matching report ---
...
```

### 图 22.16：多种架构的向量化报告。

图 22.18 显示了 C++ 实现的向量报告。

请注意，关键循环已被向量化，但存在一些向量函数匹配问题，这些问题在图 22.18 中以粗体突出显示。

对 `Interpolator::Interpolate` 方法的调用有两个参数。第一个参数是指向 `Interpolator` 类实例的指针（`this`），第二个参数是输入值。由于插值对象是均匀的（uniform），而数据参数在向量化循环内是线性的（linear），编译器正在寻找 `Interpolator::Interpolate()` 方法的 (uniform,vector) 版本。然而，编译器只能找到该方法的 (vector,vector) 版本。如前所述，这会导致生成低效的机器代码。

## UNIFORM(THIS) 子句

与图 22.8 中所示的 C 代码示例类似，这种函数参数传递歧义可以通过向向量函数的声明应用 `uniform(this)` 子句来解决，如图 22.19 所示。对于多目标架构的情况，该子句必须应用于所有“declare simd”编译指示。

这些更改反映在图 22.20 列出的编译器向量化报告中，该报告显示调用了适当的函数版本。

```cpp
class Interpolator {
public:
    /* . . . full code on lotsof cores.com . . . */
    #pragma omp declare simd simdlen(2) \
        processor(core_i7_sse4_2)
    #pragma omp declare simd simdlen(4) \
        processor(core_4th_gen_avx)
    int FindPosition(double x) const {
        return (int)(x*delta_inv);
    }

    #pragma omp declare simd processor(core_i7_sse4_2)
    #pragma omp declare simd processor(core_4th_gen_avx)
    double Interpolate(double x) const {
        int ind = FindPosition(x);
        const point& pnt = val_ptr[ind];
        double res = pnt.c0*x+pnt.c1;
        return res;
    }
private:
    double delta;
    double delta_inv;
}
/* . . . full code on lotsof cores.com . . . */
int main(int argc, char* argv[])
{
    Interpolator interpolator(512);
    /* . . . full code on lotsof cores.com . . . */
    #pragma omp simd
    for(int i=0; i<ARRAY_SIZE; ++i) {
        dst_ptr[i] = interpolator.Interpolate(src_ptr[i]);
    }
    /* . . . full code on lotsof cores.com . . . */
    return 0;
}
```

### 图 22.17：启用了 SIMD 方法的 C++ 类声明。

```text
...
LOOP BEGIN at main.cpp(111,14)
    remark #15388: vectorization support: reference src_ptr
                         has aligned access  [ main.cpp(106,35) ]
    remark #15388: vectorization support: reference dst_ptr
                         has aligned access  [ main.cpp(106,9) ]
    remark #15399: vectorization support: unroll factor set to 4
    remark #15301: OpenMP SIMD LOOP WAS VECTORIZED
    remark #15442: entire loop may be executed in remainder
    remark #15448: unmasked aligned unit stride loads: 1
    remark #15449: unmasked aligned unit stride stores: 1
    remark #15475: --- begin vector loop cost summary ---
    remark #15476: scalar loop cost: 112
    remark #15477: vector loop cost: 29.000
    remark #15478: estimated potential speedup: 7.720
    remark #15479: lightweight vector operations: 8
    remark #15480: medium-overhead vector operations: 1
    remark #15484: vector function calls: 1
    remark #15488: --- end vector loop cost summary ---
    remark #15489: --- begin vector function matching report ---
    remark #15490: Function call: Interpolator::Interpolate(const
                         Interpolator *, double) const with simdlen=8,
                         actual parameter types: (uniform,vector)
                         [ main.cpp(106,35) ]
    remark #15492: A suitable vector variant was found (out of 4)
                         with ymm2, simdlen=4, unmasked, formal parameter
                         types: (vector,vector)
    remark #15493: --- end vector function matching report ---
                         LOOP END
. . .
```

### 图 22.18：C++ 代码向量化报告。

```cpp
class Interpolator {
    /* . . . full code on lotsof cores.com . . . */
#pragma omp declare simd \
    processor(core_i7_sse4_2)
#pragma omp declare simd uniform(this) \
    processor(core_i7_sse4_2)
#pragma omp declare simd \
    processor(core_4th_gen_avx)
#pragma omp declare simd uniform(this) \
    processor(core_4th_gen_avx)

double Interpolate(double x) const {
    int ind = FindPosition(x);
    const point& pnt = val_ptr[ind];
    double res = pnt.c0*x+pnt.c1;
    return res;
}
    /* . . . full code on lotsof cores.com . . . */
}
```

### 图 22.19：为均匀调用扩展方法声明。

```text
...
remark #15489: --- begin vector function matching report ---
remark #15490: Function call: Interpolator::Interpolate(const Interpolator *, double) const with simdlen=2,
    actual parameter types: (uniform,vector)
    [ main.cpp(106,35) ]
remark #15492: A suitable vector variant was found (out of 8)
    with ymm2, simdlen=4, unmasked, formal parameter types: (uniform,vector)
remark #15493: --- end vector function matching report ---
...
```

### 图 22.20：为均匀调用扩展方法声明。

