```
```cpp
for (i=1; i<=n; i++) y[i] = yt[i];        // update y with the O(h5) solution
}

//=============================================================================
void Euler1(double t, double ht, double &y, double &dy,
            double Func(double,double,double))
//-----------------------------------------------------------------------------
// Propagates the solution y and 1st derivative dy of a 2nd order ODE from t
// to t+ht using Euler’s method
//-----------------------------------------------------------------------------
{
    double d2y;

    d2y = Func(t,y,dy);                                      // d2y -> t
    y  += ht * dy;                                           // y -> t+ht
    dy += ht * d2y;                                          // dy -> t+ht
}

//=============================================================================
void EulerCromer1(double t, double ht, double &y, double &dy,
                  double Func(double,double,double))
//-----------------------------------------------------------------------------
// Propagates the solution y and the 1st derivative dy of a 2nd order ODE
// from t to t+ht using the Euler-Cromer method
//-----------------------------------------------------------------------------
{
    double d2y;

    d2y = Func(t,y,dy);                                      // d2y -> t
    dy += ht * d2y;                                          // dy -> t+ht
    y  += ht * dy;                                           // y -> t+ht
}

//=============================================================================
void Verlet1(double t, double ht, double &y, double &dy, double &d2y,
             double Func(double,double,double))
//-----------------------------------------------------------------------------
// Propagates the solution y and the 1st derivative dy of a 2nd order ODE
// from t to t+ht using the Verlet method; returns 2nd derivative in d2y;
// d2y needs to be initialized on first call and saved between calls
//-----------------------------------------------------------------------------
{
    double ht2;

    ht2 = 0.5e0 * ht;
    dy += ht2 * d2y;                                         // dy -> t+ht/2
    y  += ht * dy;                                            // y -> t+ht

    d2y = Func(t,y,dy);                                       // d2y -> t+ht

    dy += ht2 * d2y;                                         // dy -> t+ht
}

//=============================================================================
void Euler2(double t, double ht, double y[], double dy[], int n,
            void Func(double,double[],double[],double[]))
//-----------------------------------------------------------------------------
// Propagates the solution y and the 1st derivative dy of a system of n
// 2nd order ODEs from t to t+ht using the Euler method
```
```