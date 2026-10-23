```
// Display in Excel
ExcelDriver xl; xl.MakeVisible(true);
xl.CreateChart(S, C, "Call Delta as a function of S");
}

void DisplayCallGamma()
{ // Cox and Rubinstein 1985 Figure 5-16

double K = 50.0;
double T = 0.4;
double r = 0.0106;
double b = r;
double sig = 0.3;

// Use lambda function for convenience
auto callGamma = [&] (double S)
{

double tmp = sig * std::sqrt(T);
double d1 = (log(S / K) + (b + (sig*sig)*0.5) * T) / tmp;

return n(d1) * std::exp((b - r)*T) / (S * tmp);
};

std::size_t N = 100;
std::vector <double> S(N);
std::vector <double> C(S.size());

// Generate array of underlyings
double startS = 5.0;
std::iota(std::begin(S), std::end(S), startS);

for (std::size_t i = 0; i < S.size(); ++i)
{
C[i] = callGamma(S[i]);

// Display in Excel
ExcelDriver xl; xl.MakeVisible(true);
xl.CreateChart(S, C, "Call Gamma as a function of S");
}
```

The output is shown in Figures 15.4 and 15.5, respectively.

# 15.4 OPTION SENSITIVITIES AND SURFACES

We now discuss displaying sensitivities in Excel as a function of two independent variables. There are several parameters that are used as input to the Black–Scholes formula and we select two of them as independent variables. They vary in a range while keeping the other parameters constant. For example, we may wish to compute option delta as a function of asset price and days to maturity. We have a formula to compute delta but in this case we model it as a stored