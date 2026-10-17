
随机游走在计算赫斯特指数时起着核心作用。赫斯特随机游走是具有概率 $h$ 反转方向的离散随机游走。给定一个无向连通图 $G(V, E)$（V 表示顶点，E 表示边），其中 $|V| = n, |E| = m$（n 为顶点数，m 为边数），$G$ 中的随机步是从某个节点 $u$ 到随机选择的邻居节点 $v$ 的移动。随机游走是从某个初始节点开始的这些随机步的序列。

C++ 程序 `randomwalk.cpp` 实现了在二维正方形点格上的随机游走。未实现边界条件。

```cpp
// randomwalk.cpp
#include <iostream>
#include <cstdlib> // for srand(), rand()
using namespace std;

const int n = 24;

void init(char s[n][n])
{
    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++) s[i][j] = '.';
}

void display(char s[n][n])
{
    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++) cout << s[i][j];
    cout << endl;
}

int main()
{
    char s[n][n]; // two-dimensional array of char
    int x = 12, y = 12;
    init(s);
    s[x][y] = '0'; // start cell
    cout << "enter a seed: ";
    unsigned int seed;
    cin >> seed;
    srand(seed);
    int east = 0; west = 0; int north = 0; south = 0;
    for(int i=0;i<=n/2;i++)
    {
        switch(rand()%4)
        {
            case 0: x += 1; west++; break;
            case 1: y += 1; north++; break;
            case 2: x -= 1; east++; break;
            case 3: y -= 1; south++; break;
        }
        s[x][y] = '$';
    } // end loop
    display(s);
    cout << "north " << north << "\t"
    "south " << south << "\t"
    "west " << west << "\t"
    "east = " << east;
    return 0;
}
```

Java 程序 `RandomWalk.java` 在二维正方形点格上实现了随机游走。实现了循环边界条件。红点是初始位置。该 Java 程序是一个 Applet。

```java
// randomwalk.java
import javax.swing.*;
import java.awt.*;
import java.util.Random;

public class RandomWalk extends JPanel {
    Random r;
    int x0, y0, x, y;
    boolean firstName;
    int size = 370;

    public void init() {
        r = new Random();
        x0 = 150; y0 = 150; x = x0; y = y0;
        firstName = true;
    }

    public void paint(Graphics g) {
        super.paint(g);
        // draw a grid with each square 20 pixels
        for(int i=0; i<size; i+=20)
            for(int j=0; j<size; j+=20)
                g.fillRect(i,j,20,20);
        g.setColor(Color.RED);
        g.fillOval(x0-3,y0-3,6); // initial position
        // draw a blue dot that represents an ant
        g.setColor(Color.BLUE);
        g.fillOval(x-3,y-3,6);
        if(firstName) walk();
    }

    private void walk() {
        firstName = false;
        new Thread(Runnable() {
            int count = 0;
            public void run() {
                while(count++ < 400) {
                    int d = r.nextInt(4);
                    switch(d) {
                        case 0: y -= 20; if(y==-10) y = 350;
                        case 1: x += 20; if(x==370) x = 10;
                        case 2: y += 20; if(y==370) y = 10;
                        case 3: x -= 20; if(x==-10) x = 350;
                    }
                    repaint();
                }
                try { Thread.sleep(200); }
                catch (InterruptedException ie) {
                    System.err.println("interrupt " + ie.getMessage());
                }
                showResults();
            }
        }).start();
    }

    private void showResults() {
        double distance = Math.abs(x-x0)+Math.abs(y-y0)/20.0;
        JOptionPane.showMessage(null,"effective distance moved = " + distance + "blocks!", "results",JOptionPane.INFORMATION_MESSAGE);
    }

    public static void main(String[] args) {
        Applet applet = new RandomWalk();
        JFrame f = new JFrame();
        f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        f.getContentPane().add(applet);
        f.setSize(400,400);
        f.setLocation(200,200);
        applet.init();
        f.setVisible(true);
    } // end main
}
```

我们考虑在正方形点格 $\mathbb{Z}^2$ 上的随机自避游走。随机自避游走的起点为 (0,0)。该正方形点格的最近邻居数为 4。下面提供一个实现自避游走的 C++ 程序。我们将访问过的节点存储在链表中。注意，自避随机游走可能会陷入死胡同。一条导致死胡同的路径是：(0,0) - (1,0) - (1,1) - (1,2) - (0,2) - (-1,2) - (-1,1) - (0,1)。

```cpp
// rwalk1.cpp
#include <algorithm>
#include <cstdlib>
#include <ctime>
#include <iostream>
#include <list>
#include <utility>
using namespace std;

int main(void)
{
    int i;
    // ... (rest of code)
}
```

## 2. 时间分析

```cpp
// rwalk2.cpp
#include <algorithm>
#include <cstdlib>
#include <ctime>
#include <iostream>
#include <list>
#include <utility>
using namespace std;

int main(void)
{
    int i;
    // ... (rest of code)
}
```

我们考虑在正方形点格 $\mathbb{Z}^2$ 上的随机自避游走。随机自避游走的起点为 (0,0)。该正方形点格的最近邻居数为 4。下面提供一个实现自避游走的 C++ 程序。我们将访问过的节点存储在链表中。注意，自避随机游走可能会陷入死胡同。一条导致死胡同的路径是：(0,0) - (1,0) - (1,1) - (1,2) - (0,2) - (-1,2) - (-1,1) - (0,1)。

# 第2章 时间序列分析

时间 $t$ 刻的累积位置 $X(t)$ 满足：

$$(X(t) - X(0)) = 0, \quad \langle X(t) - X(0)|^{2/2}\rangle \propto |t|^{1/2}$$

因此距离原点的标准差随 $t^{1/2}$ 增长，

Mandelbrot 和 Wallis [164] 以及 Mandelbrot 和 Van Ness [165] 引入了*分形布朗运动*作为增长速率为 $t^H$ 过程的泛化：

$$\langle X_H(t) - X_H(0)|^{2/2}\rangle \propto |t|^H$$

其中 $0 < H < 1$ 是 Hurst 指数。分形布朗运动的连续增量 $\xi_H$ 称为分形高斯噪声

$$\xi_H(t) = X_H(t + \delta) - X_H(t)$$

其中 $\delta$ 可以与其自身进行缩放。自相关函数衡量数据集在某些滞后时间 $\tau$ 下与其自身的协方差，其正式定义为：

$$C(\tau) := \frac{\langle(\xi_H(t) - \xi_H(t-\tau))(\xi_H(t) - \xi_H(t-\tau))\rangle}{\langle(\xi_H(t) - \xi_H(0))^{2}\rangle\langle(\xi_H(t-\tau) - \xi_H(0))^{2}\rangle}^{^{1/2}}$$

对于分形高斯噪声过程，该定义得出

$$C(\tau) = \frac{1}{2}(\tau + 1)^{2H-2}|\tau|^{2H} + |\tau - 1|^{2H}$$

当 $H=1/2$ 时（除 $\tau=0$ 外），自相关性为零；而当 $H \neq 1/2$ 且 $\tau$ 很大时，我们：

$$\lim C(\tau) \propto \tau^{2H-2}$$

因此自相关性衰减缓慢，产生的分形布朗运动表现出长记忆效应。当 $H > 1/2$ 时相关性为正（持久性），当 $H < 1/2$ 时为负（反持久性）。与标准布朗运动一样，所有的分形布朗运动都是自仿射的

$$X_H(at) := a^H X_H(t)$$

这意味着当时间轴按因子 $a$ 缩放而位移 $X_H$ 按 $a^H$ 缩放时，序列在统计上是相同的。因此，分形布朗运动缺乏任何特征尺度，在生成或采样分形布朗运动序列时，可以使用任意长度的单位而不丧失一般性。自仿射信号由分形维度 $D$（容积）描述，对于布朗运动，它与 Hurst 指数的关系为 $D = 2 - H$。分形维度 $D$ 可以粗略解释为信号填充的维度数。令 $F_H$ 为 $X_H$ 的傅里叶变换。分形布朗运动的功率谱（定义为频率 $\pm f$ 的幅平方贡献）

$$S(f) = |F_H(f)|^2 + |F_H(-f)|^2$$

也表现出缩放行为。对于低频，它可以被近似为*幂律*

$$S(f) \sim 1/f^{2H+1}$$

## 2.7 HIGUCHI 算法

Higuchi [114] 提出了一种计算一维时间序列分形维度的方法。考虑在等间隔间隔采集的长度为 $N$ 的时间序列

$u_1, u_2, u_3, \dots, u_N$。

Higuchi 算法基于使用 $k$ 个样本段作为测量单位对曲线长度 $L(k)$ 进行测量。令 $m$ 和 $k$ 为正整数，且 $m=1,2,\dots,k$。从时间序列可知 $k$ 个新时间序列：

$u_k^m = u_m, u_{m+k}, u_{m+2k}, \dots, u_{m+(N-m)/k}$

其中 $[\cdot]$ 是符号，$[x]$ 是不超过 $x$ 的最大整数，$m$ 表示初始时间，$k$ 表示间隔。因此，对于等于 $k$ 的间隔，我们得到 $k$ 组新的时间序列。例如，在 $N=100$ 且 $k=3$ 的情况下

$u_{k=3}^1 = u_1, u_4, u_7, \dots, u_{100}$

$u_{k=3}^2 = u_2, u_5, u_8, \dots, u_{98}$

$u_{k=3}^3 = u_3, u_6, u_9, \dots, u_{90}$

定义时间序列 $\{u_k^m\}$ 的长度为：

$L_m(k) := \frac{1}{k} \frac{N-1}{\lfloor(N-m)/k\rfloor} \sum_{j=1}^{\lfloor(N-m)/k\rfloor} |u_{m+jk}-u_{m+(j-1)k}|$

项 $(N-1)/(\lfloor(N-m)/k\rfloor)$ 是时间序列长度的归一化因子。因此，$L_m(k)$ 对于 $m=1,2,\dots,k$ 的计算是 $k$ 个值的算术平均值。如果该值与 $k^{-D}$ 成比，即 $L(k) \propto k^{-D}$，则时间序列具有分形维度 $D$。如果将 $L(k)$ $(k > 1)$ 在 $k=1,\dots,k_{max}$ 的双对数坐标系下绘制，数据应落在斜率为 $-D$ 的直线上。

## 2.8 复杂度

文献中提出了许多不同的*复杂度*定义。其中：

- 算法复杂度 (Kolmogorov-Chaitin)
- Lempel-Ziv 复杂度
- Bennett 的逻辑深度
- Grassberger 的有效复杂度
- 基于多样性的热力学深度
- 统计复杂度量（见 Steeb 及其参考文献）

接下来我们考虑 Lempel-Ziv 复杂度（Lempel 和 Ziv [148]）。字符串（零和一字符串）的复杂度定义（Chaitin [34]）为生成该字符串的最短程序的比特数。一个通用算法确定可以使用哪种程序。Lempel 和 Ziv [148] 从所有可能的程序选择了两种操作：复制和插入。首先给出一些定义。非空集合称为*字母表*，集合中的元素称为*符号*或*字母*。字母表 $A$ 的*单词*（或*字符串*）是来自 $A$ 的符号的任意有限序列，不带标点。例如，如果 $A := \{0, 1\}$，那么以下属于 $A$：

$11, 0001, 10101,$

空单词是符号序列，记为 $\lambda$。单词 $S$ 的*长度*（写作 $|S|$）是 $S$ 中符号的数量，包括重复。因此，单词 $11, 0001, 10101, \lambda$ 的长度分别为 $2, 4, 5, 1$。来自 $A$ 的所有单词集记为 $A^*$。

那么 $A^* = \{\lambda, 0, 1, 00, 01, 11, 001, \dots\}$。

量 $S(i, j)$ 表示子串

$S(i, j) = s_i s_{i+1} \cdots s_j$。

字符串 $S$ 的*词表* $v(S)$ 是 $A^*$ 的一个子集，由 $S$ 的所有子串或单词 $S(i, j)$ 组成。

**定义。** 如果 $S = s_1 s_2 \cdots s_m$ 和 $R = r_1 r_2 \cdots r_n$ 是 $A$ 单词，且每个 $s_i$ 和 $r_j$ 都在 $A$ 中，那么 $S$ 和 $R$ 的*拼接*是单词 $s_1 s_2 \cdots s_m r_1 r_2 \cdots r_n$。

记为 $SR$。

显然有

(i) $S(RQ) = \langle SR\rangle Q$

(ii) $S\lambda = \lambda S$

(iii) $|SR| = |S| + |R|$

(iv) $SR \neq RS$ 已重构

现在让我们描述如何评估 Lempel-Ziv 复杂度（Lempel 和 Ziv [148], Steeb [239]）。给定一个有限长度的字符串 $S = s_1s_2\cdots s_n$。
