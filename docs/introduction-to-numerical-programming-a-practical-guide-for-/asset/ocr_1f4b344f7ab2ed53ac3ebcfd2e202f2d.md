```
//--------------------------------------------------------------------------
{
    static double *d2y;
    static int init = 1;                         // initialization switch
    int i;

    if (init) { d2y = Vector(1,n); init = 0; }    // 1st entry allocation

    Func(t,y,dy,d2y);                            // d2y -> t

    for (i=1; i<=n; i++) {                       // propagate solution
        y[i]  += ht * dy[i];                     // y -> t+ht
        dy[i] += ht * d2y[i];                    // dy -> t+ht
    }
}
```

```
//==========================================================================
void EulerCromer(double t, double ht, double y[], double dy[], int n,
                void Func(double,double[],double[],double[]))
//--------------------------------------------------------------------------
// Propagates the solution y and the 1st derivative dy of a system of n
// 2nd order ODEs from t to t+ht using the Euler-Cromer method
//--------------------------------------------------------------------------
{
    static double *d2y;
    static int init = 1;                         // initialization switch
    int i;

    if (init) { d2y = Vector(1,n); init = 0; }    // 1st entry allocation

    Func(t,y,dy,d2y);                            // d2y -> t

    for (i=1; i<=n; i++) {                       // propagate solution
        dy[i] += ht * d2y[i];                    // dy -> t+ht
        y[i]  += ht * dy[i];                     // y -> t+ht
    }
}
```

```
//==========================================================================
void Verlet2(double ht, double m,
            double &x, double &y, double &vx, double &vy,
            double &ax, double &ay, double &Ekin, double &Epot,
            void Forces(double,double,double,double,double,
                        double&,double&,double&))
//--------------------------------------------------------------------------
// Propagates the 2D solution of Newton's equations of motion for a particle
// of mass m over a time interval ht using the velocity Verlet method
// x, y      - position components
// vx, vy    - velocity components
// ax, ay    - acceleration components (need to be initialized on 1st call)
// Ekin      - kinetic energy
// Epot      - potential energy
//--------------------------------------------------------------------------
{
    double fx, fy, ht2;

    ht2 = 0.5e0 * ht;
    vx += ht2 * ax; x += ht * vx;                // v -> t+ht/2
    vy += ht2 * ay; y += ht * vy;                // r -> t+ht
```