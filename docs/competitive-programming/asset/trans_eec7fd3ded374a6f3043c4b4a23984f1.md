
```cpp
vector<point> GrahamScan(vector<point> Polygon) {
  // first, find P0 = point with lowest Y and if tie: rightmost X
  int i, P0 = 0, N = Polygon.size();
  for (i = 1; i < N; i++)
    if (Polygon[i].y < Polygon[P0].y ||
        (Polygon[i].y == Polygon[P0].y && Polygon[i].x > Polygon[P0].x))
      P0 = i;

  point temp = Polygon[0]; // swap selected vertex with Polygon[0]
  Polygon[0] = Polygon[P0];
  Polygon[P0] = temp;

  // second, sort points by angle w.r.t. P0, skipping Polygon[0]
  pivot = Polygon[0]; // use this global variable as reference
  sort(Polygon.begin() + 1, Polygon.end(), angle_cmp);

  // third, the ccw tests
  stack<point> S;
  point prev, now;
  S.push(Polygon[N - 1]); // put two starting vertices into stack S
  S.push(Polygon[0]);

  i = 1; // and start checking the rest
  while (i < N) { // note: N must be >= 3 for this method to work
    now = S.top();
    S.pop(); prev = S.top(); S.push(now); // trick to get the 2nd item from top of S
    if (ccw(prev, now, Polygon[i])) { // if these 3 points make a left turn
      S.push(Polygon[i]); // accept
      i++;
    }
    else // otherwise
      S.pop(); // pop this point until we have a left turn
  }

  vector<point> ConvexHull;
  while (!S.empty()) { // from stack back to vector
    ConvexHull.push_back(S.top());
    S.pop();
  }
  ConvexHull.pop_back(); // the last one is a duplicate of first one

  return ConvexHull; // return the result
}
```

与凸包相关的编程练习：

- 1. UVa 109 - 飞毛腿克星
- 2. UVa 218 - 消灭飞蛾
- 3. UVa 361 - 警察与强盗
- 4. UVa 681 - 凸包求解（用于入门的纯凸包问题）
- 5. UVa 811 - 加固森林（结合凸包的完全搜索）
- 6. UVa 10002 - 质心（凸多边形的重心、凸包）
- 7. UVa 10065 - 无用的瓷砖打包机（外加多边形面积）
- 8. UVa 10135 - 聚集新生
- 9. UVa 10173 - 最小外接矩形
- 10. UVa 11626 - 凸包

### 7.4 相交问题

在几何问题中，我们几乎可以取任意一对对象，判断它们是否相交；如果相交，那么交点/交面积/交体积是什么？这是竞赛中许多计算几何问题的来源。

线段相交是最常见的相交问题之一。我们可以通过若干次 ccw 测试来判断两条线段是否相交（代码如下）。

```cpp
struct line { point p1, p2; };

int intersect(line line1, line line2) {
    return
        ((ccw(line1.p1, line1.p2, line2.p1) * ccw(line1.p1, line1.p2, line2.p2)) <= 0)
        &&
        ((ccw(line2.p1, line2.p2, line1.p1) * ccw(line2.p1, line2.p2, line1.p2)) <= 0);
}
```

然而，相交也可能发生在两条线段之外的不同类型对象之间。其他对象包括：立方体、盒子、圆、多边形、三角形、矩形等。下面给出一些示例。

与相交问题相关的可解编程练习：

- 线段相交
  - 1. UVa 191 - 相交
  - 2. UVa 378 - 相交直线
  - 3. UVa 866 - 相交线段
  - 4. UVa 920 - 阳光山
  - 5. UVa 972 - 地平线
  - 6. UVa 10902 - 挑棍游戏
  - 7. UVa 11343 - 孤立线段
- 其他对象
  - 1. UVa 453 - 相交圆（圆与圆）
  - 2. UVa 460 - 重叠矩形（矩形与矩形）
  - 3. UVa 737 - 闪耀的立方体（立方体与立方体）
  - 4. UVa 904 - 重叠空中交通管制（三维盒与三维盒）
  - 5. UVa 10301 - 圆环与胶水（圆与圆）
  - 6. UVa 10321 - 多边形相交（凸多边形与凸多边形）
  - 7. UVa 11122 - 三角形相交（三角形与三角形）
  - 8. UVa 11345 - 矩形（矩形与矩形）
  - 9. UVa 11515 - 起重机（圆与圆，外加动态规划）
  - 10. UVa 11601 - 避免重叠（矩形与矩形）
  - 11. UVa 11639 - 守卫土地（矩形与矩形）

### 7.5 再谈分治法

若干计算几何问题可以用分治范式求解，该范式已在第 3.2 节详细阐述。下面给出其中一个示例。

### 几何问题的二分法

![](img/2f3eff2c1d9ecd727dd36c1db12a8ec9_142_0.png)

图 7.6：田径跑道（来自 UVa 11646）

假设我们有如下问题：给定一个期望的足球场，其期望长宽比 = A : B，两个弧来自同一个圆，圆心位于球场中央，田径跑道的长度（周长：2× 长 + 2× 弧）为 400m，求球场的实际长和宽？见图 7.6。

用纸笔很难求出解，但借助计算机和二分法（二分查找），我们可以轻松找到解。

假设我们对 L 的值进行二分查找，那么可由 b × L / a 得到 W。期望的弧长为 (400 − 2 × L)/2。现在我们可以用三角学通过三角形 CMX 计算半径 r 和角度 θ（见图 7.6）。有了 r 和 θ，我们就能计算实际弧长。然后将该值与期望弧长比较，以决定是需要增大还是减小长度 L。代码的重要部分如下所示。

```cpp
lo = 0.0; hi = 400.0; // the range of answer
while (fabs(lo - hi) > 1e-9) { // do bisection method on L
    L = (lo + hi) / 2.0;
    W = b * L / a; // W can be derived by L
    expected_arc = (400 - 2.0 * L) / 2.0;
    half_L = 0.5 * L; half_W = 0.5 * W;
    r = sqrt(half_L * half_L + half_W * half_W);
    angle = 2.0 * atan(half_W / half_L) * 180.0 / PI;
    this_arc = angle / 360.0 * PI * (2.0 * r);
    if (this_arc > expected_arc) hi = L;
    else                         lo = L;
}
printf("Case %d: %.12lf %.12lf\n", caseNo++, L, W);
```

与本节相关的编程练习：

- 1. UVa 10245 - 最近点对问题（正如题名所示）
- 2. UVa 10566 - 交叉梯子（二分法）
- 3. UVa 11378 - 贝伊之战（也是最近点对问题）
- 4. UVa 11646 - 田径跑道（二分法，圆心位于跑道中心）
- 5. UVa 11648 - 分割土地（二分法）

### 7.6 本章注释

本章部分材料源自新加坡国立大学计算学院 **Cheng Holun, Alan 博士** 提供的材料。

还有许多其他凸包算法，例如 **Jarvis 步进法**、**礼品包装法** 和 **上/下凸包法**，它们的时间复杂度与 **Graham 扫描法** 大致相似。本章介绍的 Graham 扫描算法通常足以应对大多数竞赛问题。

还有一种尚未讨论的计算几何技术：**平面扫描**。感兴趣的读者应查阅以下书籍 [19, 6, 4]。

如果你正在备战 ICPC，最好让团队中的一名成员深入研究这一主题。此人应掌握基本几何公式和高级计算几何技术。他必须训练自己熟悉某些几何问题中的许多退化（特殊）情况，并能够处理精度误差等。

本章大约讨论了 **96 道编程练习**。

## 附录 A

### 题目致谢

本书讨论的题目主要取自 UVa 在线评测系统 [17] 和 ACM ICPC Live Archive [11]。我们已尽力联系原作者并获取许可。

到目前为止，我们已联系以下出题人并获得许可：Sohel Hafiz、Shahriar Manzoor、Manzurur Rahman Khan、Rujia Liu、Gordon Cormack、Jim Knisely、Melvin Zhang 和 Colin Tan。

如果本书中讨论的某一题目的作者中，有我们尚未联系且不允许其题目用于本书者，我们将用来自不同出题人的另一道类似题目替换该题。
