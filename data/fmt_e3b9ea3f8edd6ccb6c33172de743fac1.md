
/*
* 转换后的 Whetstone 双精度基准测试
* 版本 1.2 1998年3月22日
*
* (版权) 1998 Painter Engineering, Inc.
* 版权所有。
*
* 允许使用、复制和发布
* 此测试和程序，只要它包含了
* 此整个注释块，并受限于相应的权利引用。
*
* 由 Rich Painter 位于 Painter Engineering, Inc. 转换
* 基于从 www.nett.org 获取的 whetstone 基准
* 1998年3月16日的版本。这里使用了
* 新方法以保持与 FORTRAN 版本的外观和感受。
* 将原本基于 FORTRAN 的数组索引（
* 从元素 1 开始改为 C 语言的元素 0）
* 需要大量的修改，包括将变量索引
* 减 1。相反，在 C 中声明 `El[]` 数组时多了一个元素。
* 这使得 FORTRAN 的索引范围可以在不进行
* 字面量或变量更改的情况下运行。数组
* `El[0]` 永远不会被使用，也不会改变
* 基准测试的结果。
*
* 保留了主要的 FORTRAN 注释块，以尽量
* 减少版本之间的差异。模块 N5 和 N12。
*/

```c
for (I = 1; I <= N6; I++) {
    J = J * (K-J) * (L-K);
    K = L * K - (L+J) * K;
    L = (L-K) * (K+J);
    El[L-1] = J + K + L;
    El[K-1] = J * K * L;
}
```

```c
#ifdef PRINTOUT
IF (JJ==II) POUT (N6, J, K, E1[1],E1[2],E1[3],E1[4]);
#endif
```

```c
/*
C 模块 7: 三角函数
C
*/
```

```c
X = 0.5;
Y = 0.5;
```

```c
for (I = 1; I <= N7; I++) {
    X = T * DATAN(T*DSIN(X)*DCOS(X) / (DCOS(X+Y)+DCOS(X-Y)-1.0));
    Y = T * DATAN(T*DSIN(Y)*DCOS(Y) / (DCOS(X+Y)+DCOS(X-Y)-1.0));
}
```

```c
#ifdef PRINTOUT
IF (JJ==II) POUT (N7, J, K, X, X, Y, Y);
#endif
```

```c
/*
C 模块 8: 过程调用
C
*/
```

```c
X = 1.0;
Y = 1.0;
Z = 1.0;
```

```c
for (I = 1; I <= N8; I++) {
    P3(X,Y, &Z);
}
```

```c
#ifdef PRINTOUT
IF (JJ==II) POUT (N8, J, K, X, X, Y, Z, Z);
#endif
```

```c
/*
C 模块 9: 数组引用
C
*/
J = 1;
```

## Whetstone 689

```c
K = 2;
L = 3;
El[1] = 1.0;
El[2] = 2.0;
El[3] = 3.0;
```

```c
for (I = 1; I <= N9; I++)
    P0();
```

```c
#ifdef PRINTOUT
IF (JJ==II) POUT(N9,J,K,El[1],El[2],El[3],El[4]);
#endif
```

```c
/*
C
C 模块 10: 整数算术
C
*/
J = 2;
K = 3;
```

```c
for (I = 1; I <= N10; I++) {
    J = J + K;
    K = J + K;
    J = J - K;
    K = K - J;
}
```

```c
#ifdef PRINTOUT
IF (JJ==II) POUT(N10,J,K,X1,X2,X3,X4);
#endif
```

```c
/*
C
C 模块 11: 标准函数
C
*/
X = 0.75;
```

```c
for (I = 1; I <= N11; I++)
    X = DSQRT(DEXP(LOG(X)/T1));
```

```c
#ifdef PRINTOUT
IF (JJ==II) POUT(N11,J,K,X,X,X,X);
#endif
```

```c
/*
C
C 这是主循环的结束。
C
C
*/
```

## 690 计算系统的性能、可靠性和可用性评估

```c
if (++JJ <= II)
    goto IILOOP;
```

```c
/*
C 在此点停止基准测试计时。
C
*/
finisec = time(0);
```

```c
/*
C---------------------------------------------------------------------------------
C Whetstone KIPS 的每秒性能公式为：
C (100*LOOP+II)/TIME
C
C 其中 TIME 单位为秒。
C---------------------------------------------------------------------------------
*/
```

```c
/*
printf("\n");
if (finisec-startsec <= 0) {
    printf("持续不足——增加 LOOP 计数\n");
    return(1);
}
printf("LOOP: %ld, Iterations: %d, Duration: %ld sec.\n", LOOP, II, finisec-startsec);
KIPS = (100.0*LOOP+II)/(float)(finisec-startsec);
if (KIPS >= 1000.0) {
    printf("Double Whetstones: %.1f MIPS\n", KIPS/1000.0);
}
else
    printf("Double Whetstones: %.1f KIPS\n", KIPS);
}
if (continuous)
    goto LCONT;
return(0);
}
*/
```

```c
void PA(double E[])
{
    J = 0;
L10:
    E[1] = (E[1] + E[2] + E[3] - E[4]) * T;
    E[2] = (E[1] + E[2] - E[3] + E[4]) * T; // 注：此处原文可能存在逻辑差异，此处仅翻译结构
    E[3] = (E[1] - E[2] + E[3] + E[4]) * T;
    E[4] = (-E[1] + E[2] + E[3] + E[4]) / T;
    J += 1;
    if (J < 6)
        goto L10;
}
```

## Whetstone 691

```c
void P0(void)
{
    E[J] = E[K];
    E[K] = E[L];
    E[L] = E[J];
}
```

```c
void P3(double X, double Y, double *Z)
{
    double X1, Y1;
    X1 = X;
    Y1 = Y;
    X1 = T * (X1 + Y1);
    Y1 = T * (X1 + Y1);
    *Z = (X1 + Y1) / T;
}
```

```c
#ifndef PRINTOUT
void POUT(long N, long J, long K, double X1, double X2, double X3, double X4)
{
    printf("%d %d %d %12.4e %12.4e %12.4e %12.4e\n", N, J, K, X1, X2, X3, X4);
}
#endif
```

![](img/245014bb0cdf0eb5048_0.png)

## Linpack Bench

```c
#include <stdlib.h>
#include <stdio.h>
#include <math.h>
#include <time.h>
int main();
double cpu_time();
void daxpy(int n, double da, double dx[], int incx, double dy[], int incy);
double ddot(int n, double dx[], int incx, double dy[], int incy);
int dgefa(double a[], int lda, int n, int ipvt[]);
void dgesels(double a[], int lda, int n, int ipvt[], double b[], int ldb, int n, int info[]);
void dscal(int n, double sa, double x[], int incx);
int idamax(int n, double dx[], int incx);
double r8_epsilon();
double r8_max(double x, double y);
double r8_random(int iseed[4]);
double r8mat_gen(int lda, int n);
void timestamp();
```

```c
**************************************************
int main()
**************************************************
```

```c
/*
目的：
MAIN 是 LINPACK_BENCH 的主程序。
说明：
LINPACK_BENCH 驱动双精度基准测试程序。
修改：
2008年7月25日
参数：
N 是问题规模。
*/
```

## 694 计算系统的性能、可靠性和可用性评估

```c
#define N 1000
#define LDA (N + 1)
double *a;
double a_max;
double *b;
double b_max;
double cray = 0.056;
double eps;
int i;
int info;
int *ipvt;
int j;
int *job;
double ops;
double *resid;
double resid_max;
double residn;
double *rhs;
double t1;
double t2;
double time[6];
double total;
double *x;
```

```c
timestamp () {
  printf("\n");
  printf(" LINPACK_BENCH\n");
  printf(" C 版本\n");
  printf("\n");
  printf(" LINPACK 基准测试。\n");
  printf(" 语言: C\n");
  printf(" 数据类型: 双精度\n");
  printf(" 矩阵阶 = %d\n", N);
  ops = (double)(N * N) / 3.0 * (double)(N * N);
  /*
  为数组分配空间。
  */
  a = r8mat_gen(LDA, N);
  b = (double *)malloc(sizeof(double));
  ipvt = (int *)malloc(sizeof(int));
  resid = (double *)malloc(sizeof(double));
  rhs = (double *)malloc(sizeof(double));
  x = (double *)malloc(sizeof(double));
  a_max = 0.0;
  for (j = 0; j < N; j++) {
    a_max = r8_max(a_max, a[i + j * LDA]);
  }
  for (i = 0; i < N; i++) {
    x[i] = 1.0;
  }
  for (i = 0; i < N; i++) {
    rhs[i] = 0.0;
    for (j = 0; j < N; j++) {
      rhs[i] = rhs[i] + a[i + j * LDA] * x[j];
    }
  }
  for (i = 0; i < N; i++) {
    resid[i] = -rhs[i];
    for (j = 0; j < N; j++) {
      resid[i] = resid[i] + a[i + j * LDA] * x[j];
    }
  }
  resid_max = 0.0;
  for (i = 0; i < N; i++) {
    resid_max = r8_max(resid_max, resid[i]);
  }
  b_max = 0.0;
  for (i = 0; i < N; i++) {
    b_max = r8_max(b_max, b[i]);
  }
  eps = r8_epsilon();
  resid = resid_max / (double)N / a_max / b_max / eps;
  time[2] = total;
  if (0.0 < total) {
    time[3] = ops / (1.0E+06 + total);
  }
  else {
    time[3] = -1.0;
  }
  time[4] = 2.0 / time[3];
  time[5] = total / cray;
}
```

## 697 Linpack_Bench

```c
printf("\n");
printf("Norm. Resid MACHEP X[1] X[N]\n");
printf("\n");
printf("%14f %14f %14e %14f %14f\n", resid_max, eps, b[0], b[N-1]);
printf("\n");
printf("Factor Solve Total MFLOPS Unit Cray-Ratio\n");
printf("\n");
printf("%9f %9f %9f %9f %9f %9f\n", time[0], time[1], time[2], time[3], time[4], time[5]);
free(a);
free(b);
free(ipvt);
free(resid);
free(x);
/*
终止。
*/
printf("\n");
printf("LINPACK_BENCH\n");
printf("执行正常结束。\n");
printf("\n");
timestamp();
return 0;
#undef LDA
#undef N
```

# 698 计算系统的性能、可靠性与可用性评估

修改于：
2005年6月6日
作者：
John Burkardt

```
参数：
输出，double CPU_TIME，当前 CPU
时钟的读数，单位为秒。
*/
double value;
value = ( double ) clock ( )
/ ( double ) CLOCKS_PER_SEC;
return value;
}
```

```c
****************************************************************
void daxpy ( int n, double da, double dx[], int incx,
double dy[], int inc )
```
