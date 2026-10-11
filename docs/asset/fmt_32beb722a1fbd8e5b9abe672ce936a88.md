
```
$L' = T(t_x, t_y) * L$
```

```
$$\begin{bmatrix} x'_1 & x'_2 \\ y'_1 & y'_2 \\ 1 & 1 \end{bmatrix} = \begin{bmatrix} 1 & 0 & t_x \\ 0 & 1 & t_y \\ 0 & 0 & 1 \end{bmatrix} * \begin{bmatrix} x_1 & x_2 \\ y_1 & y_2 \\ 1 & 1 \end{bmatrix}$$
```

其中 `$L'$` 是点 `$(x'_1, y'_1)$` 和 `$(x'_2, y'_2)$` 之间平移后的线段矩阵。

### 数据

### 平移矩阵

```
$$\begin{bmatrix} 1 & 0 & t_x \\ 0 & 1 & t_y \\ 0 & 0 & 1 \end{bmatrix}$$
```

### 坐标矩阵：旧线 `oldline`

```
$$\begin{bmatrix} x_1 & x_2 \\ y_1 & y_2 \\ 1 & 1 \end{bmatrix}$$
```

### 伪代码

```
main:
输入平移矩阵
输入坐标矩阵
funcmultiply
输出新线矩阵。
停止
```

`functransansmat`:

```
输入平移值并建立平移矩阵
end
```

# 522 多维数组

`funcinput`:

输入线段坐标并建立坐标矩阵

end

`funccmult`:

平移矩阵与线坐标矩阵相乘

end

`funcoutput`:

输出线坐标

end

# 程序

```c
****************************************************************/
/* x-y 平面内线段的平移 */
/* main: x-y 平面内线段的平移 */
****************************************************************/
/* 输入变量: */
/* transmat[3][3] - 平移矩阵 */
/* oldline[3][2] - 线的坐标点 */
/* 计算变量: */
/* newline[3][2] - 平移后的线坐标点 */
/* */
/* 输出变量: */
/* oldline[3][2] - 线的旧坐标点 */
/* newline[3][2] - 线的的新坐标点 */

/* 调用的函数: */
/* funccmult - 坐标矩阵与 */
/* 变换矩阵的乘法 */
****************************************************************/
#include <stdio.h>
#define IMAX 3
#define JMAX 2
#define KMAX 3

void functransmat(float [][JMAX]);
void funcinputline(float [][JMAX]);
void funcmultiply(float [][IMAX], float [][JMAX], float [][JMAX]);
void funcoutput(float [][JMAX]);

int main()
{
    float transmat[IMAX][IMAX] = {0.0};
    float oldline[IMAX][JMAX], newline[IMAX][JMAX];

    functransmat(transmat);
    funcinputline(oldline);
    funcmultiply(transmat, oldline, newline);

    printf("\n旧坐标点的输出: x1 y1,\n");
    printf(" x2 y2\n\n");
    funcoutput(oldline);
    printf("\n新坐标点的输出: x1 y1,\n");
    printf(" x2 y2\n\n");
    funcoutput(newline);
    return 0;
}
```

```c
****************************************************/
/* functransmat: 建立平移矩阵 */
****************************************************/
/* 局部变量: */
/* tx - x 坐标的平移值 */
/* ty - y 坐标的平移值 */
/* 输出变量: */
/* transmat[][IMAX] - 平移矩阵 */
/* */
****************************************************/
void functransmat(float transmat[][IMAX])
{
    float tx, ty;
    printf("输入平移值 tx 和 ty:\n");
    scanf("%f %f", &tx, &ty);

    transmat[0][0] = 1.0;
    transmat[0][2] = tx;
    transmat[1][1] = 1.0;
    transmat[1][2] = ty;
    transmat[2][2] = 1.0;

    return;
}

void funcinputline(float oldline[][JMAX])
{
    int i, j;
    printf("\n输入坐标点 x1 y1, x2 y2:\n");
    for(j = 0; j < JMAX; j++) {
        for(i = 0; i < IMAX-1; i++) {
            scanf("%f", &oldline[i][j]);
        }
        oldline[IMAX-1][j] = 1.0;
    }
    return;
}

************************************************************************************
/* funcmultiply - 此函数用于乘法 */

```

# 8.7. 示例程序

```c
/*
 * 坐标矩阵与
 * 变换矩阵
 *
 * *********************************************************************************/

 * 输入参数:
 * transmat[IMAX] - 变换矩阵
 * oldline[IMAX] - 旧线的坐标
 * 计算变量:
 * newline[IMAX] - 新线的平移后坐标
 * 输出变量:
 * newline[JMAX] - 线的的新坐标
 * *********************************************************************************/
void funcmultiply(float transmat[][IMAX], float oldline[][JMAX], float newline[][JMAX])
{
    int i, j, k;
    for(i = 0; i < IMAX; i++) {
        for(j = 0; j < JMAX; j++) {
            newline[i][j] = 0.0;
            for(k = 0; k < KMAX; k++) {
                newline[i][j] += transmat[i][k] * oldline[k][j];
            }
        }
    }
    return;
}
********************************************************************************/
/* funcoutput: 输出线坐标 */
 *********************************************************************************/
/* 局部变量:
 * i, j
 */

输入与输出
输入平移值 tx 和 ty:
2.0 3.0

输入坐标点 x1 y1, x2 y2:
1.5 2.5
2.5 4.5

旧坐标点的输出:
1.5 2.5
2.5 4.5

新坐标点的输出: x1 y1, x2 y2
3.5 5.5
4.5 7.5

注意，此程序被工程师和科学家使用。该程序用于计算 `$(x'_1, y'_1)$` 和 `$(x'_2, y'_2)$` 之间平移后的线段。`funcmultiply` 函数用于坐标矩阵与变换矩阵的乘法。

```c

#include <stdio.h>

#include <math.h>

#define IMAX 3

#define JMAX 2

#define KMAX 3

void funcrocate(float [] [IMAX]);

int main() {

    float angle, theta, rotation[IMAX][IMAX] = {0.0};

    float oldline[IMAX][JMAX],newline[IMAX][JMAX];

    funcinline(oldline); /* same as before */

    oldline[2][0] = 0;

    oldline[2][1] = 0;

    funcrocate(rotation);

    funcmultiply(rotation, oldline, newline); /* same as before */

    printf("Output of old coordinates points x1 y1,\n");

    printf("x2 y2:\n\n");

    funcoutput(oldline); /* same as before */

    printf("Output of new coordinates points x1 y1,\n");

    printf("x2 y2:\n\n");

    funcoutput(newline); /* same as before */

    return 0;

}

```

# 8.7 示例程序

```c

void funcrotate(float rotatem1[ ][IMAX])

{

    const float PI = 3.141593;

    float angle, theta;

    printf("Input the angle of rotation (degrees):\n");

    scanf("%f",&angle);

    theta = (PI /180.0) * angle;

    rotatem1[0][0] = cos(theta);

    rotatem1[0][1] = -sin(theta);

    rotatem1[1][0] = sin(theta);

    rotatem1[1][1] = cos(theta);

    rotatem1[2][2] = 1.0;

    return;

}

```

输入与输出

Input the coordinate points x1 y1, x2 y2:
1.50 2.50
2.50 4.50

Input the angle of rotation (degrees):
10.0

Output of old coordinates points x1 y1,x2 y2:
POINT 1: ( 1.50 2.50 )
POINT 2: ( 2.50 4.50 )

Output of new coordinates points x1 y1,x2
POINT 1: ( 1.04 2.72 )
POINT 2: ( 1.68 4.87 )

注意，乘法矩阵 `funcmultiply` 使用自直线变换程序，仅将变换矩阵的参数替换为旋转矩阵。

直线的缩放

问题：将坐标点 `L(x1, y1)` 和 `L(x2, y2)` 之间的直线在 x 方向上按因子 `$s_1$`，在 y 方向上按因子 `$s_2$` 进行缩放。

![](img/8356e6c3bfe3b10354682c60b1e74b1d_551_0.png)

方法：建立缩放矩阵。

$$S(s_x, s_y) = \begin{bmatrix} s_x & 0 & 0 \\ 0 & s_y & 0 \\ 0 & 0 & 1 \end{bmatrix}$$

其中 `$s_x$` 是 `$x$` 坐标的缩放因子，`$s_y$` 是 `$y$` 坐标的缩放因子。

输入直线的坐标。建立坐标矩阵。

$$L = \begin{bmatrix} x_1 & x_2 \\ y_1 & y_2 \\ 1 & 1 \end{bmatrix}$$

缩放矩阵与坐标矩阵相乘。

$L' = S(s_x, s_y) * L$

$$\begin{bmatrix} x'_1 & x'_2 \\ y'_1 & y'_2 \\ 1 & 1 \end{bmatrix} = \begin{bmatrix} s_x & 0 & 0 \\ 0 & s_y & 0 \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x_1 & x_2 \\ y_1 & y_2 \\ 1 & 1 \end{bmatrix}$$

### 数据

缩放矩阵：

$S = \begin{bmatrix} s_x & 0 & 0 \\ 0 & s_y & 0 \\ 0 & 0 & 1 \end{bmatrix}$

坐标矩阵：

$L = \begin{bmatrix} x_1 & x_2 \\ y_1 & y_2 \\ 1 & 1 \end{bmatrix}$

### 伪代码

```
main

输入缩放矩阵

输入坐标矩阵

缩放矩阵与坐标矩阵相乘

输出变换后的矩阵

停止
```

# 多维数组

### 程序

```c

****************************************************

/*

* x-y 平内线段的缩放                     */

************************************/

/* 输入变量:                                            */

* sx - x坐标比例                             */

* sy - y坐标比例                               */

* oldline[3][2] - 直线坐标                  */

/* 计算变量:                                          */

* newline[3][2] - 变换后的直线坐标             */

/* 输出变量:                                            */

* oldline[3][2] - 直线坐标               */

* newline[3][2] - 变换后的直线坐标              */

****************************************************/

#include <stdio.h>

#define IMAX 3

#define JMAX 2

#define KMAX 3

void funcscalemat(float scalemat[][IMAX]);

void funcinputline(float [][JMAX]);

void funcmultiply(float [] [IMAX], float [] [JMAX], float [][JMAX]);

void funcoutput(float [][JMAX]);

int main()

{

    int i, j, k;

    float sx, sy, scalemat[IMAX][IMAX] = {0.0};

    oldline[IMAX][JMAX],newline[IMAX][JMAX];

    funcscalemat(scalemat);

    funcinputline(oldline); /* same as before */

    funcmultiply(scalemat, oldline, newline); /* same as before */

    printf("\noutput of old coordinates points x1 y1,\n");

    printf("x2 y2\n");

    funcoutput(oldline); /* same as before */

    printf("\noutput of new coordinates points x1 y1,\n");

    printf("x2 y2\n");

    funcoutput(newline); /* same as before */

    return 0;

}

```

```c

**************************************************

/* funcscalemat: 建立缩放矩阵 */

/*                               */

/* 局部变量:                                */

* sx - x坐标的缩放因子      */

* sy - y坐标的缩放因子        */

/*                               */
```
