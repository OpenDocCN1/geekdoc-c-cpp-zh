```
#include <cmath>
using namespace std;

#include "newmat.h"
using namespace NEWMAT;

double mv_calculate_mean(const Matrix& e, const Matrix& w){
    Matrix tmp = e.t()*w;
    return tmp(1,1);
};

double mv_calculate_variance(const Matrix& V, const Matrix& w){
    Matrix tmp = w.t()*V*w;
    return tmp(1,1);
};

double mv_calculate_std_dev(const Matrix& V, const Matrix& w){
    double var = mv_calculate_variance(V,w);
    return sqrt(var);
};
```

# C++ Code 6.2: Mean variance calculations using Newmat

# C++ program:

```
cout << "Simple example of mean variance calculations " << endl;
Matrix e(2,1);
e(1,1)=0.05; e(2,1)=0;
Matrix V(2,2);
V(1,1)=1.0; V(2,1)=0.0;
V(1,2)=0.0; V(2,2)=1.0;
Matrix w(2,1);
w(1,1)=0.5;
w(2,1)=0.5;
cout << " mean " << mv_calculate_mean(e,w) << endl;
cout << " variance " << mv_calculate_variance(V,w) << endl;
cout << " stdev " << mv_calculate_std_dev(V,w) << endl;
```

# Output from C++ program:

```
Simple example of mean variance calculations
mean 0.075
variance 0.5
stdev 0.707107
```