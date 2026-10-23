```
double K;
cout << "K: "; cin >> K;

double lambda = 0.5;

// Define payoff as a lambda function

double xMax = 1.0;        // x far field
double yMax = 1.0;        // y FF

double xHotSpot = 0.5; double yHotSpot = 0.5;
double scale1 = S*(1.0 - xHotSpot) / xHotSpot;
double scale2 = I*(1.0 - yHotSpot) / yHotSpot;

TwoFactorAsianPde<double> pde;

// Build components of pde
auto SIGMOID2 = [] (double t)
{ // t = S/A

    // Example of Table 2
    const double a = 0.6;  // (vol for low S/I)
    const double b = 0.15; // (vol for high S/I)
    const double c = 10.0;
    const double d = -0.3; // (when S=I vol is in the middle)
    const double ecd = std::exp(c*d);

    // Sigmoid2 function
    double val = exp(-c*(log(t) - d));

    double val2 = a + (b - a) / (1.0 + val);
    return val2;
};

auto a11 = [=] (double x, double y, double t)
{
    // return 0;
    double tx = 1.0 - x; double ty = 1.0 - y;

    double S = scale1*x / tx;
    double I = scale2*y / ty;

    // Straight computation, i.e. function call
    double s1 =SIGMOID2(S / I);

    return 0.5*s1*s1*x*x*tx*tx;
};

auto b1 = [=] (double x, double y, double t)
{
    double tx = 1.0 - x; double ty = 1.0 - y;
```