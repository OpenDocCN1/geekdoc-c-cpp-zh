
```cpp
c.p = r.start + c.t * r.dir; // world position of the collision
c.n = normalize(c.p - sphere_position);    // use the world position to compute the surface normal

if (c.inside)  // if collision is leaving the sphere, flip the normal
{
    c.n *= -1.0;
}
return c;
}

//------------------------------------------------------------------------
// Returns the closest collision of a ray
// object_index == -1 if no collision
// object_index == 1 if collision with sphere
// object_index == 2 if collision with box
//------------------------------------------------------------------------
Collision get_closest_collision(Ray r)
{
    Collision closest_collision, cSph, cBox;
    closest_collision.object_index = -1;

    cSph = intersect_sphere_object(r);
    cBox = intersect_box_object(r);

    if ((cSph.t > 0) && ((cSph.t < cBox.t) || (cBox.t < 0)))
    {
        closest_collision = cSph;
        closest_collision.object_index = 1;
    }
    if ((cBox.t > 0) && ((cBox.t < cSph.t) || (cSph.t < 0)))
    {
        closest_collision = cBox;
        closest_collision.object_index = 2;
    }
    return closest_collision;
}

//------------------------------------------------------------------------
// This function casts a ray into the scene and returns the final color for a pixel
//------------------------------------------------------------------------
vec3 raytrace(Ray r)
{
    Collision c = get_closest_collision(r);
    if (c.object_index == -1) return vec3(0.0);       // if no collision, return black
    if (c.object_index == 1) return sphere_color;
    if (c.object_index == 2) return box_color;
}

void main()
{
    int width = int(gl_NumWorkGroups.x);             // one workgroup = one invocation = one pixel
    int height = int(gl_NumWorkGroups.y);
    ivec2 pixel = ivec2(gl_GlobalInvocationID.xy);
```

球体对象和盒子对象（分别通过函数 intersect_sphere_object() 和 intersect_box_object()），并返回具有最短 t 的碰撞。如果没有碰撞对象，则返回特殊值 -1。

### 16.2.3 射线-球体相交

计算射线与球体的交点使用几何学推导，并有充分文献记载 [Sf86]。虽然推导相对简单，但这里只描述求解方法。交点可能有 0 个、1 个或 2 个，取决于射线是未命中球体、掠过表面，还是从一侧进入并从另一侧射出。给定射线的原点 $r_o$ 和方向 $r_d$，以及球体的位置 $s_p$ 和半径 $s_r$，那么要找到交点沿射线发生的距离 $t$，需要求解以下二次方程：

$$ (r_d \cdot r_d)t^2 + (2r_d \cdot [r_o - s_p])t + |r_o - s_p|^2 - s_r^2 = 0 \qquad [1] $$

首先，计算其判别式$^\dagger$：

$$ \Delta = (2r_d \cdot (r_o - s_p))^2 - 4|r_d|^2 (|r_o - s_p|^2 - s_r^2) $$

如果 $\Delta < 0$，我们可以停止，因为射线未命中球体（并避免尝试对负数开平方）。当 $\Delta$ 不小于零时，方程 [1] 有两个解：

$$ t = \frac{(-2r_d \cdot [r_o - s_p]) \pm \sqrt{\Delta}}{2(r_d \cdot r_d)} $$

得到的两个 $t$ 值中较小者和较大者分别记为 t_near 和 t_far。

- 当 t_near 和 t_far 都为负时，整个球体位于射线后方，没有交点。
- 当 t_near 为负且 t_far 为正时，射线从球体内部开始，第一个交点位于 t_far。
- 当两者都为正时，第一个交点位于 t_near。注意，这也处理了射线掠过球体表面的情况，此时 t_near 和 t_far 都为正且彼此相等（这发生在判别式 $\Delta$ 为零时）。

最后，一旦确定了 *t* 的值，就可以轻松计算对应点：

*碰撞点* = *r_o* + *t* * *r_d*

稍后，我们需要碰撞点处的表面法线，以下称为 *碰撞法线*，它是从球心指向交点的向量：

*碰撞法线* = normalize(*碰撞点* - *s_p*)

注意，如果射线从球体内部开始，则碰撞法线需要取反。

### 16.2.4 轴对齐射线-盒子相交

计算射线与盒子的交点同样有充分文献记载，并使用几何学推导，最常见的方法由 Kay 和 Kajiya [KK86] 推导。这里再次只描述求解方法，并针对 GPU 向量运算进行了调整 [H98]。与球体一样，射线与盒子会有 0 个、1 个或 2 个交点。

程序 16.2 假设盒子与世界坐标轴对齐（稍后处理其他朝向）。我们使用对角相对的两个点来定义盒子；即 (*x_min*, *y_min*, *z_min*) 和 (*x_max*, *y_max*, *z_max*)。在程序 16.2 中，这两个点分别是位于 (-2, -2, 0) 和 (-0.5, 1, 2) 的 *box_mins* 和 *box_maxs*。然后使用这两个点来确定组成盒子的六个 X/Y/Z 平面。例如，两个“X”平面由平行于 YZ 平面的两个盒子侧面的 X 值指定。使用 GLSL vec3 运算可以高效地求出射线与这六个平面相交的距离 *t*（推导见 [S11]）：

*t_mins* = (*box_mins* - *r_o*)/*r_d*
*t_maxs* = (*box_maxs* - *r_o*)/*r_d*

得到的 *t_mins* 和 *t_maxs* 向量包含到由 X、Y、Z 对齐的盒子侧面所定义平面的最小和最大距离。然后可以按如下方式高效地求出其中每一对的最小值和最大值：

*tminDist* = min(*t_mins*, *t_maxs*)
*tmaxDist* = max(*t_mins*, *t_maxs*)

（在 GLSL 中，两个 vec3 的“min”是一个 vec3，其中包含每对 X、Y、Z 元素中的较小者。）

向量 tminDist 则包含（从 r_o 到 x_min 的距离、从 r_o 到 y_min 的距离、从 r_o 到 z_min 的距离）。

向量 tmaxDist 则包含（从 r_o 到 x_max 的距离、从 r_o 到 y_max 的距离、从 r_o 到 z_max 的距离）。

有些平面碰撞点实际上位于盒子外部。从射线原点到实际位于盒子表面上的最近碰撞点的距离，是 tminDist 各值中的 *最大* 值；而从射线原点到位于盒子表面上的最远碰撞点的距离，是 tmaxDist 各值中的 *最小* 值：

t_near = max(tminDist_x, tminDist_y, tminDist_z)
t_far = min(tmaxDist_x, tmaxDist_y, tmaxDist_z)

于是有三种情况：

- 射线完全不与盒子相交，即 t_near > t_far 或 t_far ≤ 0 的情况。
- 当射线从盒子内部开始并射出盒子时，有一个碰撞点，即 t_near < 0 且 t_far > 0 的情况。
- 否则，有两个碰撞点，分别位于距离 t_near 和 t_far 处。

然后，计算最近碰撞点的世界坐标的方式与球体相同。计算该点处的法线时，根据碰撞发生在哪个表面，法线为 (±1,0,0)、(0,±1,0) 或 (0,0,±1)。

### 16.2.5 无光照的简单光线投射输出

图 16.3 显示了程序 16.2 的输出。场景右侧有一个红色球体，左侧有一个绿色盒子。盒子是轴对齐的，并且比球体稍微更靠近相机。注意，尚未应用光照，因此表面看起来是平的，球体看起来就像一个圆盘。

![](img/1695de1bc7486362f86c143285f3fb40_426_0.png)

图 16.3
程序 16.2 的输出，显示无光照的简单光线投射

### 16.2.6 添加 ADS 光照

第 7 章介绍了 ADS（“环境-漫反射-镜面反射”）光照。这里，我们通过添加代码在光线投射计算着色器中实现它，这些代码指定全局环境光、位置光源的位置和 ADS 特性、场景中对象的 ADS 材质特性，以及一个以与第 7 章相同的方式计算 ADS 光照的函数。

程序 16.3 展示了对光线投射计算着色器的添加和更改。着色器顶部添加了一些声明，还添加了一个新函数 ads_phong_lighting()。对 raytrace() 函数的更改以红色显示，其中光照结果乘以对象的颜色。在这个简单示例中，
