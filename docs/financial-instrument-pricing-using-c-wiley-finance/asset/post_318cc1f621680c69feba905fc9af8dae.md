
where we have created a utility function:

```
std::vector<double> OptionPrice(IBvpSolver& fdm)
{ // Compute option price using a FD scheme

    return fdm.result();
}
```

This function produces the array of option prices at expiration for each discrete mesh point.

## 21.7.3 Assembling FD Schemes from Simpler Schemes

It is possible to upgrade the accuracy of the fully implicit scheme (BTCS) from first order to second order in time (Lawson and Morris, 1978). We define a derived class of IBvpSolver and we override its member function result():

```
class ExtrapolatedImplicitEulerIBVP : public IBvpSolver
{
private:
    // We must build these in constructors

    // Notice that we store the data that 'belongs' to
    // this class. It is private and will not pollute the
    // other classes.
    Vector A, B, C;  // Lower, diagonal, upper
    Vector F;        // Right-hand side of matrix

    // Vectors on mesh of size k/2, i.e. extrapolated values
    Vector vecNewE; // Computed 'real' value time level n+1 (new)
    Vector vecOldE; // Computed 'real' value at time level n (old)

    void initICExtrapolated();

public:
    ExtrapolatedImplicitEulerIBVP(IBvp& source, long NSteps, long JSteps);

    // The overridden functions in the Template Method pattern
    void calculate() override;

    Vector& result() override;
};
```

```
void ExtrapolatedImplicitEulerIBVP::initICExtrapolated()
{ // Initialise the extrapolated array at t = 0.

    // Initialise at the boundaries
    vecOldE[ 0 ] = ibvp->Bcl( ibvp->trange().low() );
    vecOldE[ vecOldE.size()-1 ] = ibvp->Bcr( ibvp->trange().high() );
```

```
// Now initialise values in interior of interval using
// the initial function 'IC' from the PDE
for(std::size_t j = 1; j < xarr.size() - 1; ++j )
{
    vecOldE[j] = ibvp->Ic( xarr[ j ] );
}
}
```

```
ExtrapolatedImplicitEulerIBVP::ExtrapolatedImplicitEulerIBVP(IBvp& source,
    long NSteps, long JSteps)
    : IBvpSolver(source, NSteps, JSteps),
      A(Vector(J + 1)), B(Vector(J + 1)), C(Vector(J + 1)),
      F(Vector(J + 1)),
      vecNewE(Vector(vecNew)), vecOldE(Vector(vecOld))
{
    initICExtrapolated();
}
```

```
void ExtrapolatedImplicitEulerIBVP::calculate()
{ // Tells how to calculate sol. at n+1

    ImplicitEulerIBVP i1(*ibvp, N, J);
    auto vecNew = i1.result();

    ImplicitEulerIBVP i2(*ibvp,2*N, J);
    auto vecNewE = i2.result();

    for (std::size_t j = 0; j < vecNew.size(); ++j)
    { // Combine in previous loop

        vecNew[j] = 2.0*vecNewE[j] - vecNew[j];
    }

}
```

```
Vector& ExtrapolatedImplicitEulerIBVP::result()
{
    ImplicitEulerIBVP i1(*ibvp, N, J);
    vecNew = i1.result();

    ImplicitEulerIBVP i2(*ibvp, 2 * N, J);
    auto vecNewE = i2.result();

    for (std::size_t j = 0; j < vecNew.size(); ++j)
    { // Combine in previous loop

        vecNew[j] = 2.0*vecNewE[j] - vecNew[j];
    }

    return vecNew;
}
```

We conclude our discussion of finite difference schemes by comparing the accuracy of fully implicit (IE), Crank–Nicolson (CN) and Richardson extrapolation (RIE) schemes for put and call option prices (exact prices are 5.84628209 and 2.133368 for S = 60, respectively) for the following data:

```
Option myOption;
myOption.sig = 0.3; myOption.K = 65.0; myOption.T = 0.25;
myOption.r = 0.08; myOption.b = 0.08; myOption.beta = 1.0;
myOption.SMax = 325.0; myOption.type = 'P';
myOption.earlyExercise = false;
```

In general, CN and RIE are the most accurate and they produce similar results. IE is less accurate, as would be expected because it is first-order accurate. We give some numeric results and we focus on NX = NT = {325, 650, 1300}. For puts, we get:

- IE: 5.841284, 5.844843, 5.845828.
- CN: 5.842044, 5.845223, 5.846018.
- RIE: 5.842043, 5.845223, 5.846017.

For calls, we get for NX = NT = {325, 650, 1300, 2600}:

- IE: 2.128331, 2.131910, 2.132904, 2.133202.
- CN: 2.129132, 2.132315, 2.133104, 2.133303.
- RIE: 2.129129, 2.132309, 2.133104, 2.133302.

The ADE method is also second-order accurate. For example, the Barakat–Clark–Towler–Yang and Larkin–Roberts–Weiss methods give the following results, respectively:

- ADE_1: 5.841828, 5.845019, 5.84582, 5.84602.
- ADE_2: 5.841764, 5.844956, 5.845756, 5.845902.

We see that the Larkin method is less accurate than the Barakat–Clark method. We do not include a discussion of the performance of these schemes.

## 21.8 EXAMPLES AND TEST CASES

We give some initial examples. In this case we are interested in comparing the accuracy of the different schemes. For each scheme we display an array of option prices at expiration. In order to visualise the results we use the functionality of the Excel driver that we introduced in Chapter 14. We have already shown fragments of the following code in Chapter 14 and for this reason we give the code for a full program without further comment:

```
std::vector<double> OptionPrice(IBvpSolver& fdm)
{ // Compute option price using a FD scheme

    return fdm.result();
}
```

```
auto vADELarkin= OptionPrice(fdmADELarkin);
auto vADEBCUpwind = OptionPrice(fdmADEBCUpwind);

// Names of each vector
std::list<std::string> labels
    { "EE", "CN", "IE", "RIE","ADEBC",
      "Larkin", "ADE upwind"};

// The list of Y values
std::list<std::vector<double> > curves
    { vEE, vCN, vIE, vEIE, vADEBC,
      vADELarkin, vADEBCUpwind };

ExcelDriver xl; xl.MakeVisible(true);
xl.CreateChart(fdmEE.XValues(), labels, curves,
    "Comparing Schemes", "S", "price");

return 0;
}
```

We give a snapshot from the generated Excel sheet so that the values produced by the different schemes can be compared as shown in Table 21.1.

# TABLE 21.1 Comparison of methods

| S | EE | CN | IE | RIE | ADEBC | Larkin | ADE upwind |
|---|---|---|---|---|---|---|---|
| 0 | 65 | 65 | 65 | 65 | 65 | 65 | 65 |
| 1 | 62.71292 | 62.71292 | 62.71295 | 62.71292 | 62.71256 | 62.71295 | 62.70956 |
| 2 | 61.71291 | 61.71291 | 61.71293 | 61.71291 | 61.71293 | 61.71293 | 61.71279 |
| 3 | 60.71291 | 60.71291 | 60.71294 | 60.71291 | 60.71294 | 60.71294 | 60.71293 |
| 4 | 59.71291 | 59.71291 | 59.71294 | 59.71291 | 59.71294 | 59.71294 | 59.71294 |
| 5 | 58.71291 | 58.71291 | 58.71294 | 58.71291 | 58.71294 | 58.71294 | 58.71294 |
| 6 | 57.71291 | 57.71291 | 57.71294 | 57.71291 | 57.71294 | 57.71294 | 57.71294 |
| 7 | 56.71291 | 56.71291 | 56.71294 | 56.71291 | 56.71294 | 56.71294 | 56.71294 |
| 8 | 55.71291 | 55.71291 | 55.71294 | 55.71291 | 55.71294 | 55.71294 | 55.71294 |
| 9 | 54.71291 | 54.71291 | 54.71294 | 54.71291 | 54.71294 | 54.71294 | 54.71294 |
| 10 | 53.71291 | 53.71291 | 53.71294 | 53.71291 | 53.71294 | 53.71294 | 53.71294 |
| 11 | 52.71291 | 52.71291 | 52.71294 | 52.71291 | 52.71294 | 52.71294 | 52.71294 |
| 12 | 51.71291 | 51.71291 | 51.71294 | 51.71291 | 51.71294 | 51.71294 | 51.71294 |
| 13 | 50.71291 | 50.71291 | 50.71294 | 50.71291 | 50.71294 | 50.71294 | 50.71294 |
| 14 | 49.71291 | 49.71291 | 49.71294 | 49.71291 | 49.71294 | 49.71294 | 49.71294 |
| 15 | 48.71291 | 48.71291 | 48.71294 | 48.71291 | 48.71294 | 48.71294 | 48.71294 |
| 16 | 47.71291 | 47.71291 | 47.71294 | 47.71291 | 47.71294 | 47.71294 | 47.71294 |
| 17 | 46.71291 | 46.71291 | 46.71294 | 46.71291 | 46.71294 | 46.71294 | 46.71294 |
| 18 | 45.71291 | 45.71291 | 45.71294 | 45.71291 | 45.71294 | 45.71294 | 45.71294 |
| 19 | 44.71291 | 44.71291 | 44.71294 | 44.71291 | 44.71294 | 44.71294 | 44.71294 |
| 20 | 43.71291 | 43.71291 | 43.71294 | 43.71291 | 43.71294 | 43.71294 | 43.71294 |
| 21 | 42.71291 | 42.71291 | 42.71294 | 42.71291 | 42.71294 | 42.71294 | 42.71294 |

# TABLE 21.1 (Continued)

| S | EE | CN | IE | RIE | ADEBC | Larkin | ADE upwind |
|---|---|---|---|---|---|---|---|
| //... |  |  |  |  |  |  |  |
| 50 | 13.90229 | 13.90232 | 13.90291 | 13.90232 | 13.90242 | 13.9024 | 13.90944 |
| 51 | 12.97235 | 12.97238 | 12.97298 | 12.97238 | 12.97248 | 12.97246 | 12.9811 |
| 52 | 12.06168 | 12.06171 | 12.06228 | 12.06171 | 12.0618 | 12.06178 | 12.07216 |
| 53 | 11.17351 | 11.17353 | 11.17404 | 11.17353 | 11.17362 | 11.17359 | 11.18582 |
| 54 | 10.31111 | 10.31113 | 10.31155 | 10.31113 | 10.31119 | 10.31117 | 10.3253 |
| 55 | 9.47769 | 9.477705 | 9.478009 | 9.477705 | 9.477753 | 9.477725 | 9.493789 |
| 56 | 8.676324 | 8.676332 | 8.676496 | 8.676332 | 8.676356 | 8.676326 | 8.694279 |
| 57 | 7.90982 | 7.90982 | 7.909825 | 7.90982 | 7.909815 | 7.909785 | 7.929533 |
| 58 | 7.180647 | 7.180638 | 7.180475 | 7.180638 | 7.180603 | 7.180574 | 7.20197 |
| 59 | 6.490865 | 6.490849 | 6.490517 | 6.490849 | 6.490782 | 6.490754 | 6.513605 |
| 60 | 5.842068 | 5.842044 | 5.84155 | 5.842043 | 5.841946 | 5.84192 | 5.865992 |
| 61 | 5.235345 | 5.235313 | 5.234673 | 5.235313 | 5.235187 | 5.235163 | 5.260194 |
| 62 | 4.671269 | 4.671231 | 4.670464 | 4.67123 | 4.671079 | 4.671058 | 4.696763 |
| 63 | 4.149897 | 4.149854 | 4.148989 | 4.149853 | 4.149681 | 4.149664 | 4.175751 |
| 64 | 3.670797 | 3.670751 | 3.669818 | 3.67075 | 3.670562 | 3.67055 | 3.696726 |
| 65 | 3.233083 | 3.233035 | 3.232065 | 3.233035 | 3.232837 | 3.232829 | 3.258812 |
| 66 | 2.835464 | 2.835416 | 2.83444 | 2.835415 | 2.835213 | 2.83521 | 2.860739 |
| 67 | 2.476302 | 2.476255 | 2.475302 | 2.476254 | 2.476053 | 2.476055 | 2.500892 |
| 68 | 2.153675 | 2.153631 | 2.152728 | 2.15363 | 2.153436 | 2.153443 | 2.17738 |
| 69 | 1.865444 | 1.865403 | 1.864572 | 1.865402 | 1.86522 | 1.865231 | 1.888096 |
| 70 | 1.609313 | 1.609276 | 1.608533 | 1.609275 | 1.609109 | 1.609124 | 1.630778 |
| 71 | 1.382891 | 1.382859 | 1.382218 | 1.382858 | 1.382711 | 1.382729 | 1.40307 |
| 72 | 1.183749 | 1.183722 | 1.18319 | 1.183722 | 1.183596 | 1.183617 | 1.202574 |
| 73 | 1.009467 | 1.009446 | 1.009025 | 1.009445 | 1.009342 | 1.009365 | 1.026901 |
| 74 | 0.857675 | 0.85766 | 0.857349 | 0.85766 | 0.85758 | 0.857604 | 0.87371 |
| 75 | 0.726091 | 0.726081 | 0.725876 | 0.726081 | 0.726024 | 0.72605 | 0.740741 |
| 76 | 0.612542 | 0.612537 | 0.61243 | 0.612537 | 0.612502 | 0.612528 | 0.625841 |
| 77 | 0.514989 | 0.514987 | 0.514969 | 0.514987 | 0.514973 | 0.514999 | 0.526988 |

In general, the ADE methods are approximately 40% faster than Crank–Nicolson or the fully implicit method. Richardson extrapolation is the slowest as we would expect, but its performance can be improved by code parallelisation.

## 21.9 SUMMARY AND CONCLUSIONS

In this chapter we have introduced a software framework (Figure 21.2) that allows us to approximate the solution of linear convection–diffusion–reaction PDEs in non-conservative form by finite difference methods. We then discussed the applicability to one-factor plain option pricing problems. The designs and documented experience can be applied to other kinds of applications.

We continue with more examples and extensions in Chapter 22.
