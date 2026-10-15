```
//================================================================================
void LinFit(double x[], double y[], double sigmy[], int n, int iopt,
            double &a, double &b, double &sigma, double &sigmb, double &chi2)
//--------------------------------------------------------------------------------
// Determines the coefficients a and b of a linear model P(x;a,b) = a * x + b
// and the associated uncertainties, sigma and sigmb, for a set of observed
// data points by "Chi-square" regression
// x[]       - x-coordinates of observed data, i = 1,..,n
// y[]       - y-coordinates of observed data
// sigmy[]   - standard deviations of observed data
// n         - number of observed data points
// iopt      - iopt == 0 - initializes sigmy[i] = 1 (equal weights)
//             iopt != 0 - uses the received values of sigmy[i]
// a, b      - parameters of the linear model (output)
// sigma     - uncertainties associated with the model parameters (output)
// sigmb     - value of Chi-square merit function for the output parameters
//--------------------------------------------------------------------------------
{
    double f, s, sx, sy, sxx, sxy;
    int i;

    if (iopt == 0)
        for (i=1; i<=n; i++) sigmy[i] = 1e0;          // iopt = 0: equall weights

    s = sx = sy = sxx = sxy = 0e0;                    // prepare sums
    for (i=1; i<=n; i++) {
        f = 1e0/(sigmy[i]*sigmy[i]);
        s += f;
        sx += x[i] * f; sxx += x[i] * x[i] * f;
        sy += y[i] * f; sxy += x[i] * y[i] * f;
    }

    f = 1e0/(s*sxx - sx*sx);
    a = (s *sxy - sx*sy ) * f; sigma = sqrt(s*f);     // model parameters
    b = (sy*sxx - sx*sxy) * f; sigmb = sqrt(sxx*f);   // and uncertainties

    chi2 = 0e0;                                       // value of Chi-square function
    for (i=1; i<=n; i++) {
        f = (y[i] - a*x[i] - b)/sigmy[i];
        chi2 += f*f;
    }
}

//================================================================================
void MultiFit(double x[], double y[], double sigmy[], int n, int iopt,
              double a[], double sigma[], int npar, double &chi2,
              void Func(double, double [], int))
//--------------------------------------------------------------------------------
// Determines the coefficients a[i], i=1,..,npar of a multilinear model
// F(x;a) = a[1] * func[1](x) + ... + a[npar] * func[npar](x)
// and the associated uncertainties, sigma[i], for a set of observed data
// points by "Chi-square" regression
// x[]       - x-coordinates of observed data, i = 1,..,n
// y[]       - y-coordinates of observed data
// sigmy[]   - standard deviations of observed data
// n         - number of observed data points
// iopt      - iopt == 0 - initializes sigmy[i] = 1 (equal weights)
//             iopt != 0 - uses the received values of sigmy[i]
```