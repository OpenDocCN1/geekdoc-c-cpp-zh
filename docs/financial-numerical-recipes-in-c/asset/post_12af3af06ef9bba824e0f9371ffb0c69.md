
P(X) = \alpha p(X e^{r(T-t)}) + (1-\alpha)p(X)

\alpha = \left( \frac{r(T-t)}{a_0 \sigma(T-t) + a_1} \right)^l, \text{ where } l = \frac{\ln(S/C_e)}{\ln(X/S_e)}

S_c = X \left( \frac{\gamma}{1+\gamma} \right)^m, \text{ where } m = \frac{\sigma^2(T-t)}{b_0 \sigma^2(T-t) + b_1} \quad \gamma = 2r/\sigma^2

The constants $a_0, a_1, b_0$ and $b_1$ are constants. Their parameter values are estimated as

$a_0 = 3.9649 \quad a_1 = 0.032325$

$b_0 = 1.040803 \quad b_1 = 0.00963$

$S$: Current value of underlying security. $X$: Exercise price of american put. $\sigma$: Volatility of underlying. $r$: risk free interest rate. $(T-t)$: Time to maturity for option.

### Formula 15.1: The functional form of the Johnson (1983) approximation to the value of an American put

### C++ program:

```
double r=0.125; double S=1.1; double X=1;
double sigma=0.5; double time = 1;
cout << "* American put price using Johnson approximation = "
<< option.price.american_put_approximated_johnson(S, X, r, sigma, time)
<< endl;
```

### Output from C++ program:

American put price using Johnson approximation = 0.11582

Barone-Adesi (2005) notes that this approximation is inaccurate outside of the parameter range considered in the paper.

```
#include <cmath>
#include "fin_recipes.h"

double option_price_american_put_approximated_johnson( const double& S,
        const double& X,
        const double& r,
        const double& sigma,
        const double& time ){

        double sigma_sqr=pow(sigma,2);
        double a0= 9.3649 ;
        double a1= 0.032325;
        double b0= 1.040803;
        double b1= 0.009834;
        double time_sqrt=sqrt(time);
        double m = (sigma_sqr*time)/(b0*sigma_sqr*time+b1);
        double Sc = X * pow( (gamma/(1+gamma)),m);
        double l = log(S/Sc)/log(X/Sc);
        double alpha = pow ( ( (r*time)/(a0*r*time+a1) ) , l );
        double P = alpha*option_price_put_black_scholes(S,X,exp(r*time),r,sigma,time)
            + (1-alpha)*option_price_put_black_scholes(S,X,r,sigma,time);
        double p=option_price_put_black_scholes(S,X,r,sigma,time); // for safety use the Black Scholes as lower bound
        return max(p,P);
};
```

### C++ Code 15.1: The Johnson (1983) approximation to an american put price

## 15.2 An approximation to the American Put due to Geske and Johnson (1984)

Geske and Johnson (1984) develop an approximation for the American put problem. The solution technique is to view the American put as a sequence of Bermudan options, with the number of exercise dates increasing. The correct value is the limit of this sequence.

Define \(P_i\) to be the price of the put option with \(i\) dates of exercise left. \(P_1\) is then the price of an european option, with the one exercise date the expiry date. \(P_2\) is the price of an option that can be exercised twice, once halfway between now and expiry, the other at expiry. Geske-Johnson shows how these options may be priced, and then develops a sequence of approximate prices that converges to the correct price. An approximation involving 3 option evaluations is

```
\(\hat{P} = P_3 + \frac{7}{2}(P_3 - P_2) - \frac{1}{2}(P_2 - P_1)\)
```

To calculate these, first define

```
\(d_1(q, \tau) = \frac{\ln\left(\frac{S}{q}\right) + (r + \frac{1}{2}\sigma^2)\tau}{\sigma\sqrt{\tau}}, d_2(q, \tau) = d_1 - \sigma\sqrt{\tau}\)
```

and

```
\(\rho_{12} = \frac{1}{\sqrt{2}}, \rho_{13} = \frac{1}{\sqrt{3}}, \rho_{23} = \sqrt{\frac{2}{3}}\)
```

In this notation, \(P_1\) is the ordinary (european) Black Scholes value:

```
\(P_1 = Xe^{-rT}N_1(-d_2(X, T)) - SN_1(d_1(X, T))\)
```

To calculate \(P_2\):

```
\(P_2 = Xe^{-r\frac{T}{2}}N_1 \left(-d_2 \left(\overline{S}_{\frac{T}{2}}, \frac{T}{2}\right)\right) - SN_1 \left(-d_1 \left(\overline{S}_{\frac{T}{2}}, \frac{T}{2}\right)\right) + Xe^{-rT}N_2 \left(d_2 \left(\overline{S}_{\frac{T}{2}}, \frac{T}{2}\right), -d_2(X, T); -\rho_{12}\right) - SN_2 \left(d_1 \left(\overline{S}_{\frac{T}{2}}, \frac{T}{2}\right), -d_1(X, T); -\rho_{12}\right)\)
```

and \(\overline{S}_{\frac{T}{2}}\) solves

```
\(S = X - p \left( S, X, \frac{T}{2}, r, \sigma \right) = \overline{S}_{\frac{T}{2}}\)
```

To calculate \(P_3\):

```
\(P_3 = Xe^{-r\frac{T}{3}}N_1 \left(-d_2 \left(\overline{S}_{\frac{T}{3}}, \frac{T}{3}\right)\right) - SN_1 \left(-d_1 \left(\overline{S}_{\frac{T}{3}}, \frac{T}{3}\right)\right) + Xe^{-r\frac{2T}{3}}N_2 \left(d_2 \left(\overline{S}_{\frac{T}{3}}, \frac{T}{3}\right), -d_2 \left(\overline{S}_{\frac{2T}{3}}, \frac{2T}{3}\right); -\rho_{12}\right) - SN_2 \left(d_1 \left(\overline{S}_{\frac{T}{3}}, \frac{T}{3}\right), -d_1 \left(\overline{S}_{\frac{2T}{3}}, \frac{2T}{3}\right); -\rho_{12}\right) + Xe^{-rT}N_3 \left(d_1 \left(\overline{S}_{\frac{T}{3}}, \frac{T}{3}\right), d_1 \left(\overline{S}_{\frac{2T}{3}}, \frac{2T}{3}\right), -d_1(X, T); \rho_{12}, -\rho_{13}, -\rho_{23}\right) - SN_3 \left(d_2 \left(\overline{S}_{\frac{T}{3}}, \frac{T}{3}\right), d_2 \left(\overline{S}_{\frac{2T}{3}}, \frac{2T}{3}\right), -d_2(X, T); \rho_{12}, -\rho_{13}, -\rho_{23}\right)\)
```

where the critical stock prices solves

$$S = X - P_2 \left( S, X, \frac{2T}{3}, r, \sigma \right) = \overline{S}_{T/3}$$

$$S = X - p \left( S, X, \frac{T}{3}, r, \sigma \right) = \overline{S}_{2T/3}$$

The main issue in implementation of this formula (besides keeping the notation straight) is the evaluation of $P_3$, since it involves the evaluation of a trivariate normal cumulative distribution. The evaluation of $N_3()$ is described later, since it involves calls to external routines for numerical integration.

To solve for

$$S = X - p \left( S, X, \frac{T}{2}, r, \sigma \right) = \overline{S}_{\frac{T}{2}}$$

involves Newton steps. Define

$$g(S) = S - X + p \left( S, X, \frac{T}{2}, r, \sigma \right)$$

Iterate on S

$$S = S - \frac{g}{g'}$$

until g is equal to zero with some given tolerance.

```
#include <cmath>
#include "normdist.h"
#include "fin_recipes.h"
#include <iostream>

const double ACCURACY=1e-6;

inline double d1(const double& S, const double& X, const double& r, const double& sigma, const double& tau){
    return (log(S/X) + (r+0.5*pow(sigma,2))*tau)/(sigma*sqrt(tau));
};

inline double d2(const double& S, const double& X, const double& r, const double& sigma, const double& tau){
    return d1(S,X,r,sigma,tau)-sigma*sqrt(tau);
};

inline double calcP2(const double& S, const double& X, const double& r, const double& sigma, const double& time,
                     double& t2, const double& S2_bar, const double& rho12){
    double P2 = X*exp(-r*t2)*N(-d2(S,S2_bar,r,sigma,t2));
    P2 -= S*N(-d1(S2_bar,X,r,sigma,t2));
    P2 += X*exp(-r*t2)*N(d2(S,S2_bar,r,sigma,t2),-d2(S,X,r,sigma,time),-rho12);
    P2 -= S*N(d1(S2_bar,X,r,sigma,t2),-d1(S,X,r,sigma,time),-rho12);
    return P2;
};

double option_price_american_put_approximated_geske_johnson( const double& S, const double& X, const double& r,
                                                             const double& sigma, const double& time ){
    double P1 = option_price_put_black_scholes( S,X,r,sigma,time);
    double rho12=1.0/sqrt(2.0); double rho13=1.0/sqrt(3.0); double rho23=sqrt(2.0/3.0);
    double t2 = time/2.0; double t23 = time*2.0/3.0; double t3 = time/3.0;
    double S1=S; double S2_bar=S;
    double g=1; double gprime=1;
    while (fabs(g)>ACCURACY){
        g=(S1-X)-option_price_put_black_scholes(S1,X,r,sigma,t2);
        gprime=1.0-option_price_delta_put_black_scholes(S1,X,r,sigma,t2);
        S2_bar=S1;
        S1=S1-g/gprime;
    };
    double P2 = calcP2(S,X,r,sigma,time,t2,S2_bar,rho12);
    P2=max(P1,P2); // for safety, use one less step as lower bound
    double S23_bar=S2_bar;
    g=1;
    while (fabs(g)>ACCURACY){
        g=S1-X-option_price_put_black_scholes(S1,X,r,sigma,t23);
        gprime=1.0-option_price_delta_put_black_scholes(S1,X,r,sigma,t23);
        S23_bar=S1;
        S1=S1-g/gprime;
    };
    double S3_bar=S23_bar;
    g=1;
    while (fabs(g)>ACCURACY){
        g=S1-X-option_price_put_black_scholes(S1,X,r,sigma,t3);
        gprime=1.0-option_price_delta_put_black_scholes(S1,X,r,sigma,t3);
        S3_bar=S1;
        S1=S1-g/gprime;
    };
    double P3 = X * exp(-r*t3) * N(-d1(S3_bar,X,r,sigma,t3));
    P3 += -S*N(-d1(S3_bar,X,r,sigma,t3));
    P3 += S*N(-d1(S3_bar,X,r,sigma,t3));
    P3 += S*N(d1(S3_bar,X,r,sigma,t3),-d1(S23_bar,X,r,sigma,t23),-rho12);
    P3 += -S*N(-d1(S23_bar,X,r,sigma,t23),-d1(S,X,r,sigma,time),-rho12);
    P3 += -S*N(d2(S,S3_bar,r,sigma,t3),d2(S,S23_bar,r,sigma,t23),-d1(S,X,r,sigma,time),rho12,-rho13,-rho23);
    P3 = max(P2,P3); // for safety, use one less step as lower bound
    return P3+4.5*(P3-P2)-0.5*(P2-P1);
};
```

### C++ Code 15.2: Geske Johnson approximation of American put
