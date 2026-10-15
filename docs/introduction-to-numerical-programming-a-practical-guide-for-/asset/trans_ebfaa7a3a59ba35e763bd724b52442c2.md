
}
    for (j=2; j<=ny-1; j++) {
        i = 1;
        uij = betXmin[j]*u[i+1][j] + gamXmin[j]; Save                 // 左边界
        for (i=2; i<=nx-1; i++) {
            uij = (kx*(u[i-1][j] + u[i+1][j]) +
                   ky*(u[i][j-1] + u[i][j+1]) - f[i][j]) / kxy; Save
        }
        i = nx;
        uij = betXmax[j]*u[i-1][j] + gamXmax[j]; Save                 // 右边界
    }
    j = ny;
    for (i=1; i<=nx; i++) {
        uij = betYmax[i]*u[i][ny-1] + gamYmax[i]; Save                 // 上边界
    }
    if (err <= eps) break;                                         // 收敛测试
}

FreeMatrix(f,1,1);
FreeVector(betXmin,1); FreeVector(betXmax,1);
FreeVector(gamXmin,1); FreeVector(gamXmax,1);
FreeVector(betYmin,1); FreeVector(betYmax,1);
FreeVector(gamYmin,1); FreeVector(gamYmax,1);

if (it > itmax) {
    printf("PoissonXY: max. number of iterations exceeded !\n"); return 1;
}
return 0;
}
//==============================================================================
int Poisson2D(double **u, double x[], double y[],
              int imin[], int imax[], int nx, int ny, double eps,
              double Func(double,double))
//--------------------------------------------------------------------------------
// 在具有 (nx x ny) 个节点 (x[],y[]) 的规则网格上，采用直角坐标求解二维泊松方程，
// 沿 x 方向的限制索引由 imin[j] 和 imax[j] (j=1,ny) 指定，
// 使用 Gauss-Seidel 方法。
// 解 u[] [] 以相对精度 eps 收敛。
// 返回一个错误索引：0 - 正常执行。
// 调用：Func(x,y) - 泊松方程的右端项（RHS）
//--------------------------------------------------------------------------------
{
    const int itmax = 10000;                                    // 最大迭代次数
    double **f;
    double eij, err, hx, hy, kx, ky, kxy, uij;
    int i, it, j;

    f = Matrix(1,nx,1,ny);

    hx = (x[nx]-x[1])/(nx-1); kx = 1e0/(hx*hx);                  // 网格间距
    hy = (y[ny]-y[1])/(ny-1); ky = 1e0/(hy*hy);
    kxy = 2e0*(kx + ky);

    for (j=2; j<=ny-1; j++)                                      // 内部点的偏微分方程右端项
        for (i=imin[j]+1; i<=imax[j]-1; i++) f[i][j] = Func(x[i],y[j]);

    for (it=1; it<=itmax; it++) {                               // Gauss-Seidel 迭代循环
        err = 0e0;

for (j=2; j<=ny-1; j++) {
    for (i=imin[j]+1; i<=imax[j]-1; i++) {        // 内部网格点
        uij = (kx*(u[i-1][j] + u[i+1][j]) - f[i][j]) / kxy;
        if (i >= imin[j-1] && i <= imax[j-1]) uij += ky*u[i][j-1] / kxy;
        if (i >= imin[j+1] && i <= imax[j+1]) uij += ky*u[i][j+1] / kxy;

        eij = uij ? 1e0 - u[i][j]/uij : uij - u[i][j]; // 误差估计
        if (fabs(eij) > err) err = fabs(eij);        // 最大分量误差
        u[i][j] = uij;
    }
}
    if (err <= eps) break;                        // 收敛测试
}

FreeMatrix(f,1,1);

if (it > itmax) {
    printf("Poisson2D: max. number of iterations exceeded !\n"); return 1;
}
return 0;
}

//================================================================================
void PropagFTCS(double u0[], double u[], int nx, double D, double hx,
                double ht)
//--------------------------------------------------------------------------------
// 对扩散方程的解 u0[] 进行传播
//     du/dt = D d2u/dx2，D - 扩散系数（常数）
// 在时间区间 ht 上，使用显式 FTCS 差分格式，
// 在具有 nx 个节点且间距为 hx 的空间网格上求解。结果返回在 u[] 中。
//--------------------------------------------------------------------------------
{
    double lam, lam1;
    int i;

    lam = D * ht/(hx*hx);
    lam1 = 1e0 - 2e0*lam;

    u[1] = u0[1]; u[nx] = u0[nx];
    for (i=2; i<=(nx-1); i++)
        u[i] = lam*u0[i-1] + lam1*u0[i] + lam*u0[i+1];
}

//================================================================================
void PropagBTCS(double u0[], double u[], int nx, double D, double hx,
                double ht)
//--------------------------------------------------------------------------------
// 对扩散方程的解 u0[] 进行传播
//     du/dt = D d2u/dx2，D - 扩散系数（常数）
// 在时间区间 ht 上，使用隐式 BTCS 差分格式，
// 在具有 nx 个节点且间距为 hx 的空间网格上求解。结果返回在 u[] 中。
//--------------------------------------------------------------------------------
{
    static double *a, *b, *c;
    double lam, lam1;
    static int init = 1;                            // 初始化开关
    int i;

    if (init)
{ a = Vector(1,nx); b = Vector(1,nx); c = Vector(1,nx); init = 0; }

lam = D * ht/(hx*hx);
lam1 = 1e0 + 2e0*lam;

b[1] = 1e0; c[1] = 0e0;            // 构建离散化系统的系数
u[1] = u0[1];
for (i=2; i<=nx-1; i++) {
    a[i] = -lam; b[i] = lam1; c[i] = -lam;
    u[i] = u0[i];
}
a[nx] = 0e0; b[nx] = 1e0;
u[nx] = u0[nx];

TriDiagSys(a,b,c,u,nx);            // 求解三对角离散化系统
}

//==============================================================================
void PropagCN(double u0[], double u[], int nx, double D, double hx, double ht)
//--------------------------------------------------------------------------------
// 对扩散方程的解 u0[] 进行传播
//    du/dt = D d2u/dx2，D - 扩散系数（常数）
// 在时间区间 ht 上，使用 Crank-Nicolson 差分格式，
// 在具有 nx 个节点且间距为 hx 的空间网格上求解。结果返回在 u[] 中。
//--------------------------------------------------------------------------------
{
    static double *a, *b, *c;
    double lam, lam1, lam2;
    static int init = 1;                    // 初始化开关
    int i;

    if (init)
        { a = Vector(1,nx); b = Vector(1,nx); c = Vector(1,nx); init = 0; }

    lam = 0.5e0 + D * ht/(hx*hx);
    lam1 = 1e0 + 2e0*lam; lam2 = 1e0 - 2e0*lam;

    b[1] = 1e0; c[1] = 0e0;            // 构建离散化系统的系数
u[1] = u0[1];
    for (i=2; i<=(nx-1); i++) {
        a[i] = -lam; b[i] = lam1; c[i] = -lam;
        u[i] = lam*u0[i-1] + lam2*u0[i] + lam*u0[i+1];
    }
    a[nx] = 0e0; b[nx] = 1e0;
    u[nx] = u0[nx];

    TriDiagSys(a,b,c,u,nx);            // 求解三对角离散化系统
}

//==============================================================================
void PropagDiff(double u0[], double u[], double D[], int nx, double hx,
                double ht, int iopBC1, int iopBC2, double Jdiff1, double Jdiff2)
//--------------------------------------------------------------------------------
// 对扩散方程的解 u0[] 进行传播
//    du/dt = D d2u/dx2，D - 扩散系数（随空间变化）
// 在时间区间 ht 上，使用 Crank-Nicolson 差分格式，
// 在具有 nx 个节点且间距为 hx 的空间网格上求解。结果返回在 u[] 中。
// iopBC1, iopBC2 - 左/右边界条件：0 - Dirichlet，1 - Neumann
// Jdiff1, Jdiff2 - Neumann 条件下的左/右边界通量
//---------------------------------------------------------------------
{
    static double *a, *b, *c;
    double f, lam, lam1, lam2, uint, uint0;
    static int init = 1;                         // 初始化开关
    int i;

    if (init)
        { a = Vector(1,nx); b = Vector(1,nx); c = Vector(1,nx); init = 0; }

    f = 0.5e0 * ht/(hx*hx);

    b[1] = 1e0; c[1] = -iopBC1;    // 构建离散化系统的系数
    u[1] = iopBC1 ? hx*Jdiff1/D[1] : u0[1];
    for (i=2; i<=(nx-1); i++) {
        lam = D[i] * f;
        lam1 = 0.5e0 * (D[i] + D[i-1]) * f;
        lam2 = 0.5e0 * (D[i] + D[i+1]) * f;
        a[i] = -lam1;
        b[i] = 1e0 + 2e0*lam;
        c[i] = -lam2;
        u[i] = lam1*u0[i-1] + (1e0 - 2e0*lam)*u0[i] + lam2*u0[i+1];
    }
    a[nx] = -iopBC2; b[nx] = 1e0;
    u[nx] = iopBC2 ? -hx*Jdiff2/D[nx] : u0[nx];

    TriDiagSys(a,b,c,u,nx);                     // 求解三对角离散化系统

    for (i=1; i<=nx; i++) if (u[i] < 0e0) u[i] = 0e0;    // 保持解 >= 0

    uint0 = 0.5e0*(u0[1] + u0[nx]);                 // 旧解的积分
    for (i=2; i<=nx-1; i++) uint0 += u0[i];         // 梯形法则
    uint0 *= hx;
    if (iopBC1 == 1) uint0 += Jdiff1*ht;            // 左通量的贡献
    if (iopBC2 == 1) uint0 -= Jdiff2*ht;            // 右通量的贡献

    uint = 0.5e0*(u[1] + u[nx]);                    // 新解的积分
    for (i=2; i<=nx-1; i++) uint += u[i];           // 梯形法则
    uint *= hx;

    f = uint0/uint;                                 // 归一化因子
    if (f < 0e0) f = 0e0;
    for (i=1; i<=nx; i++) u[i] *= f;                // 归一化解
}

//=====================================================================
void PropagQTD(dcmplx Psi[], double V[], int nx, double hx, double ht)
//---------------------------------------------------------------------
// 对一维薛定谔方程的解 PSI = Psi + i Chi 进行传播
//   i d/dt PSI(x,t) = [-(1/2) d2/dx2 - V(x)] PSI(x,t),
// 在时间区间 ht 上，使用 Crank-Nicolson 格式，
// 在具有 nx 个节点且间距为 hx 的网格上求解三对角离散化系统，
// 使用 LU 分解。使用复数运算。
//---------------------------------------------------------------------
{
    static dcmplx *a, *b, *c;                   // 离散化系统的对角线
    dcmplx Psii, Psii;
    double lam, W;

