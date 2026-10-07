
```cpp
if(f < bestf) { bestf=f; bestf=population+i*g_len; }

}

iterations++;

print(bestf);

cout << endl;

cout << "Fitness of " << bestf << " after "

cout << " iterations" << endl;

delete[] population; delete[] elim;

}

int main(void) {

    srand(time(NULL)); // 随机数生成器种子

    double data[] = { 0,0,1.0,0.0,0.5,1.0,0.25,0.5,0.75,0.5,

0.25,1,-0.75,1,-1 };

    gep(data,7,30.001);

    cout << endl;

    return 0;

}
```

我们在下文列出了一些典型结果，它们的适应度均为 0。

- `((1-x)*(x(((x-x)+x)+x))=4x(1-x)`
- `(x+(((((((x-x)-x)+x)*x)*x)+x))=x(1-x) (2x+3)`
- `((x-(x))((x-1)-x))=4x(1-x)`
- `((1-x)*1)((1+1)+1)*x)=4x(1-x)`
- `((1-1)-(((x-x)+x)*x)+x)=x(1-x) (2x+3)`
- `(1*((x-(((x-x)+x)+x))+x))+x+x) (2x+3)`
- `(1-x)*(((((x-x)+x)+x)+1)*x)+x)=x(1-x) (2x+3)`
- `(1-(1-(((x-x)+x)+x))-1))+x=4x(1-x)`

我们发现，大部分情况下，`4x(1-x)` 或 `x(1-x)(2x+3)` 是适应度最高的映射。当然，如果使用种群，我们可以在较少的迭代次数找到所需的函数。映射 `g:→ℝ`，`g(x)=x(1-x)(2x+3)` 满足上述所有条件，但 `g` 在区间 `(1/2, (√-5)/2)` 上具有大于 1 的取值。我们发现，几乎所有的初始值 `$x_0 \in [0,1]$` 在映射的迭代下都会逃离该区间。所有留在 `[0,1]` 中的点的测度为 0，并形成一个康尔集。我们还可以修改符号数组以包含代表余弦的 `c`、代表正弦的 `s` 以及代表 `π x` 的 `y`。在这种情况下，我们发现几乎每次找到的 `sin(π x)` 都是适应度最高的映射。

## 第 15 章 基因表达编程

### 15.2.2 布尔表达式

基因表达编程的另一个应用是寻找布尔表达式。在布尔表达式中，我们有与（AND）、或（OR）、异或（XOR）和非（NOT）运算。与门是一个与门后接非门。与门是通用的，可以从它构建其他门。例如，考虑以下真值表

| a | b | O |
|---|---|---|
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

其中 `a` 和 `b` 是输入，`O` 是输出。假设 `·`（在 C++ 中为按位运算符 `&`）是与运算，`+`（在 C++ 中为按位运算符 `|`）是或运算，`$\overline{a}$`（在 C++ 中为按位运算符 `~`）是非运算。使用基因表达编程，我们可以找到表达式：

```
&a|1|b|aabb10bb
|b|abab
```

第一个布尔表达式是 `$a \cdot (1+b)$`。第二个布尔表达式是 `$b \cdot \overline{a}$`。在第一种情况下，树结构如下所示

![](img/e89136779f66a50f0bd7e926e5daf1d2_508_0.png)

对于适应度函数，我们将给定真值表中每个项目的输出与基因的输出进行比较。例如，考虑基因表达编程编写的表达式 `$E(a,b)=\overline{a} \cdot b0$`。该表达式可以用标准记法写作：

`$E(a,b) = a \cdot (b+0)$`。

因此我们找到：

`$E(0,0) = 1, E(0,1) = 1, E(1,0) = 1, E(1,1) = 0$`。

因此适应度为 2，因为有两个目的值不同。当然，我们需要达到的适应度是 0。

## 15.2 示例

// `gepbool.cpp`

```cpp
#include <cstdlib>
#include <ctime>
#include <cmath>
#include <iostream>
#include <string>
using namespace std;

const int nsymbols = 7;
// 4 个终端符号（无参数）a, b, 0 和 1
const int terminals = 4;
// 终端符号
const char symbols[nsymbols] = {'0','1','a','b','|','-','&'};
const int n = 2; // +, - 需要两个参数
int h = 10;
int evalr(char *e, int a, int b) {
    switch(*e++) {
        case '0': return 0; case '1': return 1;
        case 'a': return a; case 'b': return b;
        case '|': return evalr(e,a,b) | evalr(e,a,b);
        case '~': return evalr(e,a,b);
        case '&': return evalr(e,a,b) & evalr(e,a,b);
        default: return 0;
    }
}
```

```cpp
int evalr(char *e, int a, int b) { char *c = e; return evalr(e,a,b); }
void printr(char *e) {
    switch(*e++) {
        case '0': cout << '0'; break;
        case '1': cout << '1'; break;
        case 'a': cout << 'a'; break;
        case 'b': cout << 'b'; break;
        case '|': cout << '|'; break;
        case '~': cout << '~'; break;
        case '-': cout << '-'; break;
        case '&': cout << '&'; break;
    }
}
```

```cpp
void print(char *e) { char *c = e; printr(c); }
double fitness(char* c, int* data, int N) {
    int d, sum = 0;
    for(int j=0;j<N;j++)
        d=evalr(c,data[j],data[j+1]);
    sum += d;
    return sum;
}
```

```cpp
// N 点，P 种群大小，要求的 eps
// 此函数的逻辑在 OCR 中是片段化的，但遵循源码结构
void gep(char*data, int N, int P, double eps) {
    int i,j,replace,replace2,rp;
    int t = h-i;
    int g_len = h+t;
    int pop_len = P*g_len;
    int iterations = 0;
    char *population = new char[pop_len];
    char *elim = new char[P];
    int toelim = P/2;
    double bestf,f;
    double sum = 0.0; // 适应度值和
    double pmutate = 0.1; // 变异概率
    double pinsert = 0.4; // 插入概率
    double precomb = 0.7; // 重组概率
    double r,last;
    char *best = (char*)NULL; // 最优基因
    char *iter; // 迭代变量
// 初始化种群
for(i=0;i<pop_len;i++)
    if(i%g_len < h) population[i] = symbols[rand()%nsymbols];
    else population[i] = symbols[rand()%terminals];
// 初始化计算
bestf = fitness(population,data,N);
best = population;
for(i=0,sum=0.0,iter=population;i<P;iter+=g_len)
{
    f = fitness(iter,data,N);
    sum += f;
    if(f<bestf) { bestf = f; best = population+i*g_len; }
}
while(best >= eps)
{ // 繁殖，轮盘选择
    for(i=0;i<P;i++) elim[i] = 0;
    for(i=0;i<toelim;i++)
    {
      r = sum+(double(rand()/RAND_MAX);
      double lastf = 0.0;
      for(j=0;j<P;j++)
      {
        f = fitness(population+j*g_len,data,N);
        if((lastf<r) && (r<lastf)) { elim[j] = 1; j = P; }
        lastf += f;
      }
    }
    for(i=0;i<pop_len;i++)
    {
      if(population+i==best) i+=g_len; // 永远不修改/替换基因
      else for(j=0;j<g_len;j++)
      {
        // 选择失败导致的变异或淘汰
        if((double(rand()/RAND_MAX) < pmutate) || elim[i/g_len])
        if(i % g_len < h) population[i] = symbols[rand()%nsymbols];
        else population[i] = symbols[rand()%terminals];
      }
    }
    // 插入
    if(double(rand()/RAND_MAX) < pinsert)
    {
      // 在该代头部寻找插入位置
      // 由于我们移动到了下一代，基因减去 g_len
      replace = i-g_len;
      rp = rand()*Y;
      // 插入源的随机位置
      replace2 = rand()%pop_len;
      // 从基因中插入的随机长度
      int rlen = rand()*(h-rp);
      // 创建新基因
      char *c = new char[g_len];
      // 拷贝移动后的头部部分
      strcpy(c+rp,population+replace+rp);
      // 拷贝尾部
      strcpy(c+th,population+h);
      // 拷贝片段
      strcpy(c+rp,replace2);
      // 如果新代更优则使用它
      if(fitness(c,data,N) < fitness(population+replace,data,N))
      strcpy(population+replace,c);
      delete[] c;
    }
    // 重组
    if(double(rand()/RAND_MAX) < precomb)
    {
      // 在基因中寻找单点重组位置
      replace = i-g_len;
      rlen = rand()%g_len;
      // 重组的随机基因
      replace2 = (rand()*P)*g_len;
      // 创建新基因
      char *c[5];
      c[0] = population+replace; c[1] = population+replace2;
      c[2] = new char[g_len]; c[3] = new char[g_len]; c[4] = new char[g_len];
      strncpy(c[2],c[0],rlen);
      strncpy(c[2]+rlen,c[1],g_len-rlen);
      strncpy(c[3],c[1],rlen);
      strncpy(c[3]+rlen,c[0],g_len-rlen);
      // 选取最优的基因
      for(j=0;j<4;j++)
      for(k=j+1;k<4;k++)
      if(fitness(c[k],data,N) < fitness(c[j],data,N))
      {
        strncpy(c[4],c[j],g_len); strncpy(c[k],c[4],g_len); // 注意：OCR 逻辑似乎很乱
      }
    }
  }
}
```
```

## 15.3 数值-符号操作

我们考虑涉及多项式和指数函数的有限表达式的演化积分。假设我们希望用初等函数确定积分

`$\int g(x)dx$`

答案应该是符号形式的。然而，我们需要一个适应度函数，为任何近似该积分的符号表达式提供一个实值适应度。我们知道

`$\frac{d}{dx}g(x)dx - g(x) = 0$`。

评估近似误差等同于再次转化为积分问题。我们为

`{-1, -0.9, -0.8, -0.7, \dots, 0.9, 1}`

选择一组具有代表性的点，

我们可以估算 `[-1, 1]` 上的近似误差：

`$\sum_{j=0}^{20} |(\frac{d}{dx}f(x) - g(x))|_{x=-1+0.1j}|$`

因此，积分的一个可能的适应度函数给出：

`$fitness(f)=\sum_{j=0}^{20} |f'(x=-1+0.1j)-g(x=-1+0.1j)|$`

即我们结合了符号和数值计算。我们寻找一个符号表达式，其导数在给定点集上最接近被积函数。适应度越接近零的个体越适应。

另一种可能性是使用 `$\frac{d}{dx}f(x)-g(x)$` 简化后表达式的长度，其中长度为 0 是最适应的值（即我们找到了积分）。我们在下面的程序中使用第一种适应度度量。

```cpp
// geopint.cpp
#include <cstdlib>
#include <ctime>
#include <cmath>
#include <iostream>
#include <string>
```

## 第 15 章 基因表达编程
