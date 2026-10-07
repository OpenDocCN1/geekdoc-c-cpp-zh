
```cpp
void Vector::printVec() const {
  for(int i = 0; i < nRows; i++)
    cout << pA[i] << " " << endl;
}

Vector operator*(double b, const Vector& v){
  Vector B = v;
  return B*b;
}
```

# APPENDIX E

## The ranGen class

The “complete” version of the class ranGen that was used in Chapter 8 and elsewhere is given in this appendix. We begin the header file below.

Listing E.1 ranGen.h

```cpp
//ranGen.h
#ifndef RANGEN_H
#define RANGEN_H
enum unType {FM2, WH};
enum normType {BM, C};

class ranGen {
    unType T;
    normType NT;
    unsigned long seed1, seed2, seed3;

    double gCauchy(double x) const;
    double gInvCauchy(double u) const;
    double fNorm(double x) const;
public:
    ranGen(unType t = WH, normType nt = BM) : T(t), NT(nt) {}
    ~ranGen();
    void ranUnif(int n, double* pu);
    void ranNorm(int n, double* pNorm, double mu = 0,
        double sig = 1);
    void setSeed(unsigned long si);
};
#endif
```

There are two types of uniform number generators: the Fishman-Moore II (FM2) generator and the Wichmann-Hill (WH) generator. These are packaged together in the method ranUnif. Both the Cauchy-accept (C) and the Box-Muller (BM) methods are provided as options for generating random numbers in the method ranNorm. Selection of the different algorithms is accomplished by specification of the symbolic constants FM2, WH and C are defined using an enum statement. The default choices of WH and BM for the uniform and normal generator types are set in the class constructor. The ranNorm allows specification of the mean and standard deviation of the distribution with default values that produce normal.

The other class members are three unsigned long seeds for the generators. These values are set by the user with the public setSeed method that takes only one unsigned long argument. It then an integer form of the FM2 generator to set the two additional seeds for the WH generator.

The method definitions are given in the next listing.

Listing E.2 ranGen.cpp

```cpp
//ranGen.cpp
#include "ranGen.h"
#include <iostream>
#include <cmath>

//anonymous namespace
namespace i {
    double pi = 2.**acos(0);
    double sqrtpi = sqrt(2.*pi);
    unsigned long a1 = 171, m1 = 30269, a2 = 172, m2 = 30307,
    a3 = 170, m3 = 30323, m4 = 2147483647, a5 = 630600616;
}

void ranUnif(int n, double* pu) {
    if (T == WH) {
        double temp = 0;
        for (int i=0; i<n; i++) {
            seed1=(a1*seed1)%m1;
            seed2=(a2*seed2)%m2;
            seed3=(a3*seed3)%m3;
            temp = ((double)seed1)/((double)m1) + ((double)seed2)/((double)m2)
                + ((double)seed3)/((double)m3);
            if(temp > 2.)
                if(temp > 1.) temp -= 1.
            pu[i] = temp;
        }
    } else {
        for (int i=0; i<n; i++) {
            seed1=(a4*seed1)%m4;
            pu[i]=((double)seed1)/((double)m4);
        }
    }
}

void ranNorm(int n, double* pNorm, double* mu) {
    double sig = 0;
    int nFill = 0, iAccept = 0, nReject = 0;
    if (NT != BM) {
        double spare = 0, mult = 0, Rsq = 0;
        while(nFill<n) {
            if(iAccept) { //if we have one left, use it now
                pNorm[nFill] = spare;
                iAccept = 0;//next time we need to generate another pair
                nFill += 1;
            } else while(iAccept == 0){
                //generate two uniforms on [-1, 1]
                ranUnif(2,pu);
                pu[0] = 2*pu[0] - 1;
                pu[1] = 2*pu[1] - 1;
                Rsq = pu[0]*pu[0] + pu[1]*pu[1];
                if(Rsq <= 1 && Rsq != 0){ //accept the result
                    mult = sqrt(-2.*log(Rsq)/Rsq);
                    pNorm[nFill] = mu + sig*pu[0]*mult;
                    spare = mu + sig*pu[1]*mult;//save this one for next time
                    nFill += 1;
                }
            }
        }
    }
}
```

# THE RANGEN CLASS

```cpp
// ... inside ranNorm logic ...
iAccept = 1;//now we have one left over
}
else nReject += 2;
}
}
else{
    double y;
    double c = sqrt(2*pi/exp(1.));

    while (nFill < n){
        iAccept = 0;
        while (iAccept == 0){
            ranUnif(2, pu);
            y = gCauchy(pu[1]);
            if(c*gCauchy(pu[0]) < norm(y))){//the result
                pNorm[nFill] = mu + sig*y;
                nFill++; //augment the number of samples
                iAccept = 1;//the interior loop
            }
            else nReject += 1;
        }
    }
}
```

```cpp
void ranGen::setSeed(unsigned long s1){
    if (T == WH){
        seed1 = s1;
        seed2=(a4*seed1)%m4;
        seed3=(a4*seed2)%m4;
    } else
        seed1 = s1;
}
```

```cpp
double ranGen::gCauchy(double x) const {
    return 1./((1.+ x*x)*pi);
}
```

```cpp
double ranGen::fNorm(double x) const {
    return exp(-.5*x*x)/sqrt(pi);
}
```

There are several global constants that are needed in various functions in the class. These could simply have been defined at the outset of any function allowing them to have global scope. However, name clashes can occur when the class is used in other programs. This is particularly true for the constant pi. To avoid this constants can be wrapped in an anonymous namespace which is what has done here. Then, the constants exist only inside this particular file (i.e., ranGen.cpp) and can only be accessed by the functions in that file.

# References

- C. Aggarwal, editor, Data Streams, volume 31 of Advances in Database Systems, 2007.
- G. Andrews, Number Theory, Dover, 1971.
- S. Arora and B. Barak, Computational Complexity: A Modern Approach, Second Edition, 2009.
- M. Austen, Technical report on C++ standard, ISO/IEC TR 1968, 2005.
- P. Becker, The C++ Standard Libraries: A Tutorial, Addison-Wesley, 2006.
- G. Bleisle, Convergence theorems for simulated annealing, Journal of Applied Probability, 29:885-895, 1996.
- A. Ben-Israel and T. Greville, Generalized Inverses Theory and Applications, Second Edition, New York, NY, 2003.
- Y. Benjamini and Y. Hochberg, Controlling the false discovery rate: multiple testing, Journal of the Royal Society, Series B, 57:289-300, 1995.
- Y. Benjamini and D. Yutieli, The control of the false discovery rate under dependency, Annals of Statistics, 29:1165-1188, 2001.
- A. Björ, Numerical Methods for Least Squares, SIAM, 1996.
- G. Box, M. Muller, A note on the generation of random normal deviations, Annals of Mathematical Statistics, 29:610-611, 1958.
- A. Broder and M. Mitten, Network applications of blood flow: a study of Internet Mathematics, 1485-505, 2009.
- T. Budd, Class Data Structures in C++, Addison-Wesley, New York, NY, 1994.
- R. Byrd, P. Lu, J. Nodel, and C. Zhu, A limited memory algorithm for bound constrained optimization, SIAM Journal of Scientific Computing, 16:1190-1288, 1995.
- C. Carter and M. Wegman, Universal classes of hash functions, Journal of Computer and Science Sciences, 8:143-159, 1979.
- J. Chambers, Programming with Data: A Guide to the S Language, Springer, New York, NY, 1998.
- T. Chan and J. Lewis, Computing standard deviations: accuracy, Communications of the Association, 22:520-539, 1971.
- T. Chan, G. Golub, and R. LeVeque, Algorithms for computing the sample variance: analysis and recommendations, American Statistics, 37:242-247, 1983.
- R. Chandra, L. Dagum, D. Koh, J. Maydan, and R. McDonald, Parallel Programming in OpenMP, Morgan Kaufmann, San Francisco, CA, 2001.
- R. Cheng and G. Feast, Some simple gamma variance, Applied Statistics, 28:290-295, 1979.
- P.ing, Practical number generators for parallel computers, NHSE Review, 1, 1996.
- S. Conte and C. de Boer, Elementary Nonnumerical Analysis, Second Edition, McGraw Hill, New York, NY, 1972.
