
## 22.3 Cubic spline

Cubic splines are well known for their good interpolation behaviour. The cubic spline parameterization was first used by McCulloch (1971) to estimate the nominal term structure. He later added taxes in McCulloch (1975). The cubic spline was also used by Litzenberger and Rolfo (1984). In this case the cubic spline is used to approximate the *discount factor*, not the yields.

$$d(t) = 1 + b_1 t + c_1 t^2 + d_1 t^3 + \sum_{j=1}^K F_j (t - t_j)^3 1_{\{t < t_j\}}$$

Here $1_{\{A\}}$ is the indicator function for an event $A$, and we have $K$ knots.

To estimate this we need to find the $3 + K$ parameters:

$\{b_1, c_1, d_1, F_1, \cdots, F_K\}$

If the spline *knots* are known, this is a simple linear regression. C++ Code 22.5 shows the calculation using this approximation.

```
#include <cmath>
#include <vector>
using namespace std;

double term_structure::discount_factor::cubic_spline(const double& t,
const double& b1,
const double& c1,
const double& d1,
const vector<double>& f,
const vector<double>& knots){
double d = 1.0 + b1 * t + c1 * (pow(t,2)) + d1 * (pow(t,3));
for (int i=0; i<knots.size();++i) {
if (t >= knots[i]) { d += f[i] * (pow((t-knots[i]),3)); }
else { break; }
}
return d;
};
```

C++ Code 22.5: Approximating a discount function using a cubic spline

Header File 22.3 and C++ Code 22.6 wraps this calculations into a term structure class.

```
#include "fin_recipes.h"
#include <vector>
using namespace std;

class term_structure::cubic_spline : public term_structure {
private:
double b_; double c_; double d_;
vector<double> f_; vector<double> knots_;
public:
term_structure::cubic_spline(const double& b, const double& c, const double& d,
const vector<double>& f, const vector<double>& knots);
virtual ~term_structure::cubic_spline();
virtual double d(const double& T) const;
};
```

Header file 22.3: Term structure class wrapping the cubic spline approximation

```
#include "fin_recipes.h"
term_structure::cubic_spline::cubic_spline ( const double& b, const double& c, const double& d,
const vector<double>& f, const vector<double>& knots ) {
b_ = b; c_ = c; d_ = d; f_ = f; knots_ = knots;
if (f.size()!=knots.size()){ return; } knots_.clear();
for (int i=0;i<f.size();++i) {
f_.push_back(f[i]);
knots_.push_back(knots[i]);
};
};
double term_structure::cubic_spline::d(const double& T) const {
return term_structure_discount_factor_cubic_spline(T,b_,c_,d_,f_,knots_);
};
```

C++ Code 22.6: Term structure class wrapping the cubic spline approximation

### Example

Using the parameters b = 0.1 c = 0.1, d = -0.1,

```
f = [ 0.01 ]
    [ 0.01 ]
    [ -0.01 ]
```

```
knots = [ 2 ]
    [ 7 ]
    [ 12 ]
```

Find short rates and discount factors for 1 year, and the forward rate between 1 and 2 years.

# C++ program:

```
cout << "Example term structure calculations using a cubic spline " << endl;
double b=0.1; double c=0.1; double d=-0.1;
vector<double> f; f.push_back(0.01); f.push_back(0.01); f.push_back(-0.01);
vector<double> knots; knots.push_back(2); knots.push_back(7); knots.push_back(12);
cout << " direct calculation, discount factor (t=1) "
     << term_structure::discount_factor_cubic_spline(1,b,c,d,f,knots) << endl;
cout << " Using a term structure class " << endl;
term_structure_class cs(b,c,d,f,knots);
cout << " yield (t=1) = " << cs.yield(1) << endl;
cout << " discount factor (t=1) = " << cs.d(1) << endl;
cout << " forward (t1=1, t2=2) = " << cs.f(1,2) << endl;
```

# Output from C++ program:

```
Example term structure calculations using a cubic spline
direct calculation, discount factor (t=1) 1.1
Using a term structure class
yield (t=1) = -0.0953102
discount factor (t=1) = 1.1
forward (t1=1, t2=2) = 0.318454
```

## 22.4 Cox Ingersoll Ross

The Cox et al. (1985) model is the best known example of a continuous time, general equilibrium model of the term structure. It is commonly used in academic work because it is a general equilibrium model that still is “simple enough” to let us find closed form expressions for derivative securities.

The short interest rate.

$dr(t) = \kappa(\theta - r(t))dt + \sigma\sqrt{r(t)}dW$

The discount factor for a payment at time T.

$d(t, T) = A(t, T)e^{-B(t, T)r(t)}$

where

$\gamma = \sqrt{(\kappa + \lambda)^2 + 2\sigma^2}$

$A(t, T) = \left[ \frac{2\gamma e^{\frac{1}{2}(\kappa + \lambda + \gamma)(T-t)}}{(\gamma + \kappa + \lambda)(e^{\gamma(T-t)} - 1) + 2\gamma} \right]^{\frac{2\kappa\theta}{\sigma^2}}$

and

$B(t, T) = \frac{2\gamma e^{\gamma(T-t)} - 1}{(\gamma + \kappa + \lambda)(e^{\gamma(T-t)} - 1) + 2\gamma}$

Five parameters: $r$, the short term interest rate, $\kappa$, the mean reversion parameter, $\lambda$, the “market” risk parameter, $\theta$ the long-run mean of the process and $\sigma$, the variance rate of the process.

```
#include <cmath>
using namespace std;
double term_structure::discount_factor_cir(const double& t,
                                           const double& r,
                                           const double& kappa,
                                           const double& lambda,
                                           const double& theta,
                                           const double& sigma){
    double sigma_sqr=pow(sigma,2);
    double gamma = sqrt(pow((kappa+lambda),2)+2.0*sigma_sqr);
    double denum = (gamma+kappa+lambda)*(exp(gamma*t)-1)+2*gamma;
    double p=2*kappa*theta/sigma_sqr;
    double numer1 = 2*gamma*exp(0.5*(kappa+lambda+gamma)*t);
    double A = pow((numer1/denum),p);
    double B = (2*(exp(gamma*t)-1))/denum;
    double disc_factor=A*exp(-B*r);
    return disc_factor;
};
```

C++ Code 22.7: Calculation of the discount factor using the Cox et al. (1985) model

```
#include "fin_recipes.h"
class term_structure_class_cir : public term_structure {
private:
double r_; // interest rate
double kappa_; // mean reversion parameter
double lambda_; // risk aversion
double theta_; // long run mean
double sigma_; // volatility
public:
term_structure_class_cir(const double& r, const double& k, const double& l,
const double& th, const double& sigma);
virtual double d(const double& T) const;
};
```

Header file 22.4: Class definition, Cox et al. (1985) model, header file

```
#include "fin_recipes.h"
//term_structure_class_cir::term_structure_class_cir(){};
term_structure_class_cir::term_structure_class_cir(const double& r, const double& k, const double& l,
const double& th, const double& sigma) {
r_ = r; kappa_=k; lambda_=l; theta_=th; sigma_=sigma;
};
double term_structure_class_cir::d(const double& T) const{
return term_structure::discount_factor_cir(T,r,kappa_,lambda_,theta_,sigma_);
};
```

C++ Code 22.8: Class definition, Cox et al. (1985) model

### Example

Parameters: r = 0.05, κ = 0.01, σ = 0.1, θ = 0.08 and λ = 0.0. Use the CIR term structure model. Find short rate and discount factor for t = 1, and forward rate between years 1 and 2.

```
C++ program:
cout << "Example calculations using the Cox Ingersoll Ross term structure model " << endl;
double r = 0.05; double kappa=0.01; double sigma=0.1; double theta=0.08; double lambda=0.0;
cout << " direct calculation, discount factor (t=1): " << endl;
cout << " using a class " << endl;
cout << term_structure::discount_factor_cir(1, r, kappa, lambda, theta, sigma) << endl;
cout << " using a class " << endl;
term_structure_class cir(r,kappa,lambda,theta,sigma);
cout << " yield (t=1) = " << cir.yield(1) << endl;
cout << " discount factor (t=1) = " << cir.d(1) << endl;
cout << " forward (t1=1, t2=2) = " << cir.f(1,2) << endl;
```

Output from C++ program:
Example calculations using the Cox Ingersoll Ross term structure model
direct calculation, discount factor (t=1): 0.951166
using a class
yield (t=1) = 0.0500668
discount factor (t=1) = 0.951166
forward (t1=1, t2=2) = 0.04989756

## 22.5 Vasicek

```
#include <cmath>
using namespace std;
double term_structure::discount_factor_vasicek(const double& time,
                                             const double& r,
                                             const double& a,
                                             const double& b,
                                             const double& sigma){
    double A,B;
    double sigma_sqr = sigma*sigma;
    double aa = a*a;
    if (aa==0.0){
        B = time;
        A = exp(sigma_sqr*pow(time,3))/6.0;
    }
    else {
        B = (1.0 - exp(-a*time))/a;
        A = exp( ((B-time)*(aa*b-0.5*sigma_sqr))/aa - ((sigma_sqr*B*B)/(4*a)));
    }
    double dfact = A*exp(-B*r);
    return dfact;
}
```

C++ Code 22.9: Calculating a discount factor using the Vasicek functional form

```
#include "fin_recipes.h"
class term_structure_class_vasicek : public term_structure_class {
private:
    double r_; double a_; double b_; double sigma_;
public:
    term_structure_class_vasicek(const double& r, const double& a, const double& b, const double& sigma);
    virtual double discount_factor(const double& T) const;
};
```

Header file 22.5: Class definition, Vasicek (1977) model
