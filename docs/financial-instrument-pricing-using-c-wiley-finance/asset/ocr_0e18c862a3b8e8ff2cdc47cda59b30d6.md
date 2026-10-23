The computational form of the schemes (13.29), (13.30) is:

U_j^{n+1} (1 + λ) = U_j^{n} (1 - λ) + λ (U_{j+1}^{n} + U_{j-1}^{n+1}),   (λ = k / h²)

and

V_{j}^{n+1} (1 + λ) = V_{j}^{n} (1 - λ) + λ (V_{j+1}^{n+1} + V_{j-1}^{n}).

The terms on the right-hand side of these equations are known.

# 13.4.1 C++ Implementation of ADE (Barakat and Clark) for the Heat Equation

We have discussed the Crank–Nicolson method in Section 13.3. It is unconditionally stable and second-order accurate. However, we need to solve a tridiagonal matrix system at each time level, which can have an impact on run-time performance. The ADE method is unconditionally stable, explicit and second-order accurate (the Barakat and Clark version; see Barakat and Clark, 1966). The C++ implementation of the discrete scheme (13.29)–(13.31) is:

```
long J = 20;

std::cout << "Number of space subdivisions: ";
std::cin >> J;

std::cout << "Number of time subdivisions: ";
long N = 100; std::cin >> N;

std::cout << "Expiration: ";
double T = 1.0; std::cin >> T;

// Space interval [A,B]
double A = 0.0;      // LHS
double B = 1.0;      // RHS
double h = (B-A) / static_cast<double>(J);
double k = T / static_cast<double>(N);

// Boundary conditions
double BCL = 0.0;
double BCR = 0.0;

double lambda = k / (h*h);

// Create mesh in space
auto xarr = CreateMesh(J, A, B);

Vector<double> U(xarr.size());      // L-R sweep
Vector<double> V(xarr.size());      // R-L sweep
```