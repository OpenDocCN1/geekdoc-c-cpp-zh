```
```cpp
std::vector<double> y0{ 1.0, 1.0 };

// System (24.48)
VectorValuedFunction func(2);
RealValuedFunction f1 = [](double x, std::vector<double> y)
    { return -2*y[0] + y[1] + 2*std::sin(x); };
RealValuedFunction f2 = [](double x, std::vector<double> y)
    { return -2 * y[1] + 1*y[0] + 2 * (std::cos(x) - std::sin(x)); };

func[0] = f1; func[1] = f2;

auto valSystem = PredictorCorrector(func, x, y0, T, N, TOL);
std::cout << "Solution PC system: " << valSystem[0] << ", "
          << valSystem[1] << ", " << '\n';
auto valRK4 = RK4(func, x, y0, T, N, TOL);
std::cout << "Solution RK system: " << valRK4[0] << ", "
          << valRK4[1] << ", " << '\n';

auto valEuler = Euler(func, x, y0, T, N, TOL);
std::cout << "Solution Euler system: " << valEuler[0] << ", "
          << valEuler[1] << ", " << '\n';

auto y1 = 2 * std::exp(-T) + std::sin(T);
auto y2 = 2 * std::exp(-T) + std::cos(T);
std::cout << "Exact solution PC system: " << y1 << ", "
          << y2 << ", " << '\n';
```
```

# 24.7.3  Stiff Systems

We conclude this chapter with the numerical approximation of the stiff system (24.51):

```
```cpp
// 2X2 system
std::size_t n = 2;
std::vector<double> y0{ 2.0, 0.0 };

double T = 1.0; double x = 0.0;
std::size_t N = 1200; double TOL = 1.0e-4;

double lambda1 = -1.0; double lambda2 = -1000;
double a = (lambda1 + lambda2) / 2; double b = (lambda1 - lambda2) / 2;
VectorValuedFunction func(2);

// Component functions of fun
RealValuedFunction f1 = [](double x, std::vector<double> y)
    { return a*y[0] + b*y[1]; };
RealValuedFunction f2 = [](double x, std::vector<double> y)
    { return b*y[0] + a*y[1]; };
func[0] = f1; func[1] = f2;
```
```