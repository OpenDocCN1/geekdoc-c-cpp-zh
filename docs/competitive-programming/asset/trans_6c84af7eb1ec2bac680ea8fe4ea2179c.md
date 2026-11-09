

### 球体

- 1. 球体是三维空间中一种完美圆形的几何物体。

- 2. 球体上任意两点 A 和 B 之间的**大圆距离** [38] 是沿着**球体表面**上一条路径的最短距离。该路径等于经过 A、B 两点的该球体**大圆**的弧长。

球体的大圆定义为沿球体表面延伸并将球体切成两个相等半球的圆。为了求解大圆距离，我们求出该大圆的圆心角 AOB（见图 7.4），并利用它来确定弧长。

虽然相当罕见，但有些竞赛题目会使用这种距离度量。通常，球体表面上的两个点以（纬度，经度）对的形式给出。下面的库代码将帮助我们在给定球体上两个点和球体半径的情况下获得最短的大圆距离。关于此库代码的推导，请参阅 [38]。

![](img/2f3eff2c1d9ecd727dd36c1db12a8ec9_136_0.png)

![](img/2f3eff2c1d9ecd727dd36c1db12a8ec9_136_1.png)

图 7.4：大圆与大圆距离（弧 A-B）（图来自 [46]）

```cpp
double greatCircleDistance(double pLat, double pLong,
                           double qLat, double qLong, double radius) {
    pLat *= PI / 180; pLong *= PI / 180;
    qLat *= PI / 180; qLong *= PI / 180;
    return radius * acos(cos(pLat)*cos(pLong)*cos(qLat)*cos(qLong) +
                         cos(pLat)*sin(pLong)*cos(qLat)*sin(qLong) +
                         sin(pLat)*sin(qLat));
}
```

与大圆距离相关的编程练习：

- 1. UVa 535 - 环球旅行者
- 2. UVa 10075 - 航空公司（含APSP）
- 3. UVa 10316 - 航空枢纽
- 4. UVa 10897 - 旅行距离
- 5. UVa 11817 - 穿越地球

### 多边形

- 1. **多边形**是由有限条直线段组成的闭合路径或回路所围成的平面图形。这些线段称为边。两条边相交的点称为多边形的顶点或角。多边形的内部有时称为其本体。

- 2. 如果在多边形内部画出的任意线段都不会与多边形的任何边相交，则该多边形称为**凸多边形**。否则，该多边形称为**凹多边形**。

- 3. 对于具有 \(n\) 对顶点坐标且按某种顺序（顺时针或逆时针）给出的 \(n\) 边形（无论是凸还是凹），其面积 \(A\) 为：

\[
A = \frac{1}{2}\left|\begin{array}{cc}
x_1 & y_1 \\
x_2 & y_2 \\
x_3 & y_3 \\
\vdots & \vdots \\
x_n & y_n
\end{array}\right|
= \frac{1}{2}(x_1y_2 + x_2y_3 + x_3y_4 + \cdots + x_ny_1 - x_2y_1 - x_3y_2 - x_4y_3 - \cdots - x_1y_n)
\]

这可以写成下面的库代码。请注意，我们的默认设置是所有坐标均为整数，并尽可能使用整数运算。如果给定的点不是整数，则需要修改此代码的一部分：

```cpp
struct point { int x, y; } // a point has two members

int determinant(vector<point> P) { // default: integer computation
  int result = 0, x1, y1, x2, y2;
  for (int i = 0; i < P.size(); i++) {
    x1 = P[i].x; x2 = P[(i + 1) % P.size()].x;
    y1 = P[i].y; y2 = P[(i + 1) % P.size()].y;
    result += (x1 * y2 - x2 * y1);
  }
  return result;
}

// area is half of the determinant and the result may be a non-integer
double area(vector<point> P) { return fabs(determinant(P) / 2.0); }
```

- 4. 对于具有 \(n\) 对坐标且按某种顺序（顺时针或逆时针）给出的 \(n\) 边形，其周长 \(p\) 可以用勾股定理计算：

```cpp
double perimeter(vector<point> P) { // point has x & y
  double result = 0.0, x1, y1, x2, y2, dx, dy;
  for (int i = 0; i < P.size(); i++) {
    x1 = P[i].x; x2 = P[(i + 1) % P.size()].x;
    y1 = P[i].y; y2 = P[(i + 1) % P.size()].y;
    dx = x2 - x1;
    dy = y2 - y1;
    result += sqrt(dx * dx + dy * dy);
  }
  return result;
}
```

- 5. 使用一个相当稳健的^3几何谓词测试——称为 **CCW（逆时针）测试**（又称 **左转测试**），可以轻松测试多边形是否为凸（或凹）。

CCW 测试是计算几何中一个简单但重要的谓词测试。该测试接受平面上的 3 个点 \(p\)、\(q\)、\(r\)，并判断序列 \(p \rightarrow q \rightarrow r\) 是否为左转^4。例如，\(CCW(p,q,r)\)，其中 \(p=(0,0)\)、\(q=(1,0)\)、\(r=(0,1)\) 为真。此测试可以使用以下库代码实现：

```cpp
int turn(point p, point q, point r) {
    int result = (r.x - q.x) * (q.y - p.y) - (r.y - q.y) * (p.x - q.x);
    if (result < 0) return -1; // P->Q->R is a right turn
    if (result > 0) return 1;  // P->Q->R is a left turn
    return 0; // P->Q->R is a straight line, i.e. P, Q, R are collinear
}

// Note: sometimes, we change the '> 0' to '>= 0' to accept collinear points
bool ccw(point p, point q, point r) { return (turn(p, q, r) > 0); }
```

借助上述库代码，我们现在可以通过验证多边形中所有连续三个点是否在按逆时针顺序访问时都进行左转来检查多边形是否为凸。如果我们能找到至少一个不满足该条件的三元组，那么多边形就是凹的。

与多边形相关的编程练习：

- 1. UVa 478 - 图形中的点：矩形、圆形和三角形（点在多边形内）
- 2. UVa 634 - 多边形（点在多边形内）
- 3. UVa 10078 - 艺术画廊（测试多边形是否为凸）
- 4. UVa 10112 - Myacm 三角形（像 UVa 478 那样用面积测试检查点是否在三角形内）
- 5. UVa 11447 - 水库日志（多边形面积）
- 6. UVa 11473 - 校园道路（多边形周长）

当然，还有许多其他几何形状、物体和公式尚未涉及，例如 3D 物体等。到目前为止，我们所介绍的是编程竞赛中出现频率较高的那些。

其他与基础几何相关的编程练习（未在上面列出）：

- 1. UVa 10088 - 我岛上的树（Georg A. Pick 定理：\(A = i + \frac{b}{2} - 1\)，参见 [43]）
- 2. UVa 10297 - Beavergnaw（圆锥、圆柱、体积）
- 3. UVa 10387 - 台球（展开表面、三角学）
- 4. UVa 11322 - 圆柱体（圆、矩形、圆柱体）
- 5. UVa 11507 - Bender B. Rodriguez 问题（模拟）

## 7.3 格雷厄姆扫描

点集 \(P\) 的**凸包**是包含 \(P\) 中每个点（要么在 \(CH(P)\) 的边界上，要么在其内部）的最小凸多边形 \(CH(P)\)（见图 7.5.D）。\(CH(P)\) 中的每个顶点都是原集合 \(P\) 中的一个顶点。因此，寻找凸包的算法必须决定选择 \(P\) 中的哪些顶点作为凸包的一部分。

![](img/2f3eff2c1d9ecd727dd36c1db12a8ec9_139_0.png)

图 7.5：点集 \(P\) 的凸包 \(CH(P)\)

可用的凸包算法有好几种。在本节中，我们选择 \(O(n \log n)\) 的罗纳德·格雷厄姆扫描算法。该算法首先根据所有 \(n\) 个点相对于一个称为基准点的角度对 \(P\) 中的点进行排序（图 7.5.A）。在我们的例子中，我们选择 \(P\) 中最低且最右的点作为基准点（参见图 7.5.B 中的点 0 以及其余点的逆时针顺序）。

然后，该算法维护一个候选点栈 \(S\)。\(P\) 中的每个点都会被压入 \(S\) 一次，而最终不会成为 \(CH(P)\) 一部分的点会从 \(S\) 中弹出。观察图 7.5.C。栈先前包含（栈底）11-0-1-2（栈顶），但当我们尝试插入 3 时，1-2-3 构成右转，因此我们弹出 2。现在 0-1-3 是左转，因此我们将 3 压入栈，此时栈包含（栈底）11-0-1-3（栈顶）。

当格雷厄姆扫描结束时，留在 \(S\) 中的就是 \(CH(P)\) 的点（见图 7.5.D），栈包含（栈底）11-0-1-4-7-10-11（栈顶）。格雷厄姆扫描消除了所有右转！检查 \(CH(P)\) 中顶点的序列总是构成左转——这是一个凸多边形。

下面是格雷厄姆扫描的实现，省略了之前已经展示过的部分（如 ccw 函数）：

```cpp
point pivot; // global variable
vector<point> polygon, CH;

int area2(point a, point b, point c) {
    return a.x * b.y - a.y * b.x + b.x * c.y - b.y * c.x + c.x * a.y - c.y * a.x;
}

int dist2(point a, point b) { // function to compute distance between 2 points
    int dx = a.x - b.x, dy = a.y - b.y; return dx * dx + dy * dy;
}

bool angle_cmp(point a, point b) { // important angle-sorting function
    if (area2(pivot, a, b) == 0) // collinear
        return dist2(pivot, a) < dist2(pivot, b); // which one closer

    int d1x = a.x - pivot.x, d1y = a.y - pivot.y;
    int d2x = b.x - pivot.x, d2y = b.y - pivot.y;
    return (atan2((double)d1y, (double)d1x) - atan2((double)d2y, (double)d2x)) < 0;
}
```

