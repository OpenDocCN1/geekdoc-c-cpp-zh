

```cpp
public:
    u::matrix<double> MatNew;                 // averaged solution, level n+1
private:
    // Mesh-related data
    double hx, hy, delta_k, hx1, hy1, hx2, hy2;

    // Mesh-point values of coefficients
    double A,B,C,D,E,F,G;
    double t2,tx1,ty1;

    // Other variables
    double tprev, tnow, T;
    std::size_t NX, NY, NT;

public:
    std::vector<double> xmesh;
    std::vector<double> ymesh;
    std::vector<double> tmesh;

public:

    TwoFactorAsianADESolver(const TwoFactorPdeDomain<double>& domain,
                            const std::vector<double>& xarr,
                            const std::vector<double>& yarr,
                            const std::vector<double>& tarr)
        : xmesh(xarr), ymesh(yarr), tmesh(tarr)
    {
        cout << "Two-factor ADE Asian classic version\n";
        pdeDomain = domain;

        hx=pdeDomain.rx.spread() / static_cast<double>(xmesh.size() - 1);
        hy=pdeDomain.ry.spread() / static_cast<double>(ymesh.size() - 1);
        delta_k = pdeDomain.rt.spread()
                / static_cast<double>(tmesh.size() - 1);

        T = pdeDomain.rt.high();

        // Extra, handy variables
        hx1 = 1.0/hx;
        hx2 = 1.0/(hx*hx);
        hy1 = 1.0/hy;
        hy2 = 1.0/(hy*hy);

        // Some optimising variables
        t2 = delta_k * hx2;
        tx1 = delta_k * hx1;
        ty1 = delta_k * hy1;

        // Initialise U, Uold, V, Vold, MatNew data structures
        // NumericMatrix(I rows, I columns, I rowStart, I columnStart);
        // Constructor with size & start index
    }
```

U = u::matrix<double>(xmesh.size(), ymesh.size());
V = u::matrix<double>(xmesh.size(), ymesh.size());

MatNew = u::matrix<double>(xmesh.size(), ymesh.size());

initIC();
}

~TwoFactorAsianADESolver()
{
}

////////////////////////////////////////////////////////////
void initIC()
{ // Utility function to initialise payoff function and BCs at t = 0

tprev = tnow = tmesh[0];

// Now initialise values in interior of interval using
// the initial function 'IC' from the PDE
for (std::size_t i = 0; i < xmesh.size(); ++i)
{
    for (std::size_t j = 0; j < ymesh.size(); ++j)
    {
        MatNew(i,j) = U(i, j) = V(i, j) = AnchorPde::IC(xmesh[i], ymesh[j]);
    }
}
}

void calculateBC()
{ // Calculate the discrete BC on the FOUR edges of the boundary

// Lower and Upper BC
std::size_t lower = 0;
std::size_t upper = ymesh.size()-1;
for (std::size_t i = 0; i < xmesh.size(); ++i)
{
    MatNew(i, lower) = U(i, lower) = V(i, lower)
        = AnchorPde::BCLower(xmesh[i], tnow);// N/A
        // anymore
    MatNew(i, upper) = U(i, upper) = V(i, upper)
        = AnchorPde::BCUpper(xmesh[i], tnow);
}

// Left and Right BC
std::size_t left = 0;
std::size_t right = xmesh.size() -1;
for (std::size_t j = 0; j < ymesh.size(); ++j)
{
```

sgn = MySign(E);
F = AnchorPde::d(mx, my, tnow) * delta_k;
G = AnchorPde::F(mx, my, tnow) * delta_k;

// Larkin + 1st order upwind
V(i, j) = (V(i, j)*(1.0 - A) + V(i - 1, j)*(A - D)
          + V(i+1, j)*(A + D) + sgn*E*V(i, j + sgn) + G)
          / (1.0 + A - F + sgn*E);
}
}

for (std::size_t i = 0; i < MatNew.size1(); ++i)
{
    for (std::size_t j = 0; j < MatNew.size2(); ++j)
    {
        MatNew(i,j) = 0.5 * (U(i,j) + V(i,j));
        U(i, j) = MatNew(i, j);
        V(i, j) = MatNew(i, j);
    }
}

void result()
{ // The result of the calculation

    cout << "result";

    for (std::size_t n = 1; n < tmesh.size(); ++n)
    {
        if ((n/100)*100 == n)
        {
            cout << n << ", ";
        }

        tnow = tmesh[n];

        calculateBC();    // Calculate the BC at n+1
        calculate ();     // Calculate the solution at n+1

        tprev = tnow;
    }
}

// Domain
TwoFactorPdeDomain<double> pdeDomain;
CreateAnchorPdeDomain(pdeDomain, xMax, yMax, T, payoff);

An example of use is:

```
// Meshes. Create the mesh
long NX = 100; long NY = 100; long NT = 100;
cout << "Give NX \n"; cin >> NX;
cout << "Give NY \n"; cin >> NY;
cout << "Give NT \n"; cin >> NT;

std::vector<double> xmesh = pdeDomain.rx.mesh(NX);
std::vector<double> ymesh = pdeDomain.ry.mesh(NY);
std::vector<double> tmesh = pdeDomain.rt.mesh(NT);

cout << "Now creating solver\n";

TwoFactorAsianADESolver solver(pdeDomain, xmesh, ymesh, tmesh);
solver.result();
```

Then we can access the option values in solver.MatNew by displaying them in Excel, for example.

## 23.5.1 The Saul’yev Method and Factory Method Pattern

我们现在讨论如何应用第 23.4 节中提到的选择 A3 来实现 Saul’yev (1964) 中发展的原始 ADE 方法。在这种情况下，我们创建一个实现该方法的类，该类由域和对式 (23.7) 建模的 PDE 组成。这种设计比基于选择 A1 和 A2 的设计更易于维护，因为现在类具有紧密的内部内聚性，并且与其他类松散耦合。此外，每个类都有单一的主要职责。

我们现在讨论的类几乎与第 23.5 节中的类相同，只是它额外包含了一个嵌入的 PDE 实例（换句话说，我们使用组合）：

```
class SaulyevTwoFactorAsianADESolverVersion2
{
private:
    TwoFactorPdeDomain<double> pdeDomain;          // Domain, BC, IC
    std::shared_ptr<TwoFactorAsianPde<double>> pde; // The new extra
                                                    // member
    // ETC. as in section 23.5
};
```

该类的组件通过其构造函数进行初始化：

```
SaulyevTwoFactorAsianADESolverVersion2
(const std::shared_ptr<TwoFactorAsianPde<double>>& asianPde,
    const TwoFactorPdeDomain<double>& domain,
    const std::vector<double>& xarr,
    const std::vector<double>& yarr,
    const std::vector<double>& tarr)
{
    // body
}
```

由于我们有不同的方式来创建 PDE，我们将每种选择封装在一个工厂方法中，其唯一职责是根据来自给定源的输入创建 PDE 实例。为此，我们考虑了多个工厂，其中之一是（我们注释掉并移除了第 23.4 节中已引入的代码）：

```
std::shared_ptr<TwoFactorAsianPde<double>> CreateAsianPde(double K,
 double T)
{ // Factory method to create an Asian pde for input to FDM

    // Steps
    // 1. Get input data
    // 2. Create the components of the PDE
    // 3. Return the instance of AsianPde

    double r = 0.049;

    // Values where price is calculated S/I == 1
    double S = 100; double I = 100;

    double lambda = 0.5;

    // Define payoff as a lambda function
    double xMax = 1.0;            // x far field
    double yMax = 1.0;            // y FF

    double xHotSpot = 0.5; double yHotSpot = 0.5;
    double scale1 = S*(1.0 - xHotSpot) / xHotSpot;
    double scale2 = I*(1.0 - yHotSpot) / yHotSpot;

    TwoFactorAsianPde<double> pde;

    // Build components of pde
    auto SIGMOID2 = [] (double t)
    { // t = S/A

        //

    };

    auto a11 = [=] (double x, double y, double t)
    {
        //

    };

    auto b1 = [=] (double x, double y, double t)
    {
        //
    };

    auto b2 = [=] (double x, double y, double t)
```

```
{
    //
};

auto d = [=] (double x, double y, double t)
{
    //
};

auto F= [=] (double x, double y, double t)
{
    //
};

pde.a11 = a11;

// a22 = c = 0

pde.b1 = b1;
pde.b2 = b2;
pde.d = d;
pde.F = F;

return std::shared_ptr<TwoFactorAsianPde<double>>
    (new TwoFactorAsianPde<double>(pde));
}
```

这种设计可以应用于通过有限差分方法近似 PDE 的各种问题。它是结构模式和创建模式的结合，分别是 *Adapter* 和 *Factory Method*（见 GOF, 1995 中讨论）。设计步骤总结如下：

- 1. 创建一个由通用函数包装器组成的抽象 PDE 类。
- 2. 创建一个 FD 类，其中嵌入指向 PDE 类实例的指针以及嵌入的域对象。
- 3. 创建一个工厂方法来实例化步骤 1 中的 PDE 类，并在步骤 2 中的 FD 类的构造函数中提供新创建的对象。

简而言之，我们使用 *组合*（HAS-A 关系）而不是表征子类型多态和类层次结构的更普遍的 IS-A 关系。例如，可以基于此设计在 C++ 中实现 Barakat 和 Clark 变体的 ADE。这将是一个有用的练习。

## 23.6 USEFUL UTILITIES

我们已使用域变换将 $(S, A)$ 空间映射到 $(x, y)$ 空间，如第 23.3 节所述。然后我们通过用有限差分格式在 $(x, y)$ 空间中近似 PDE 来计算期权价格。由此得到的数据结构是在到期时间 $t = T$ 时 $(x, y)$ 空间中的离散值的矩阵。一个具体场景是计算热点 $(0.5, 0.5)$ 处的

