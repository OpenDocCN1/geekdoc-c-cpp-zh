```
```cpp
// We start at 1st time point
double current = k;

StopWatch<> sw;
sw.Start();

while (current <= T)
{
    // Update at new time level n+1

    // Compute inhomogeneous term
    for (std::size_t j = 1; j < r.size()-1; ++j)
    {
        r[j] = (lambda*(1.0-theta)*vecOld[j+1]
              + (1.0 - 2.0*lambda*(1.0-theta))*vecOld[j]
              + (lambda*(1.0-theta)*vecOld[j-1]);
    }

    // DoubleSweep<double> mySolver(a, b, c, r, BCL, BCR);
    L U T r i d i a g o n a l S o l v e r < d o u b l e > mySolver(a, b, c, r);
    vecNew = mySolver.solve();
    vecOld = vecNew;

    current += k;
}
sw.Stop();
std::cout << "Elapsed time: "
```
```

We use two arrays to store values at time levels *n* and *n + 1*. We note that this scheme becomes even easier to solve in the case of the explicit Euler method (13.26) (also known as the FTCS scheme) in which case we can compute the solution at time level *n + 1* without the need to solve a tridiagonal system. This feature comes at a cost, because FTCS is only *conditionally stable* and a small time step is needed if we wish to avoid oscillations.

Having created the code, we test it to determine if it is a good approximation (in some sense) to the exact solution or to the exact finite difference solution of the initial boundary value problem (13.16).

# 13.4  THE ADE METHOD FOR THE IMPATIENT

The explicit finite difference method for the heat equation *must satisfy* the constraint **k ≤ h²/2** where *k* is the mesh size in time (some authors use Δt to denote the mesh size), in other words we must take very small time steps if we wish to get decent results. The method is first-order accurate in time, which makes it unsuitable for real applications. However, an advantage of the method is that we do not need to use a tridiagonal solver to compute a solution at each time level. A question we could ask is whether we can discover explicit finite difference schemes that are explicit, unconditionally stable and (ideally) second-order accurate. Such a family of schemes would result in code that is easy to write and understand. Furthermore, we expect these methods to be very efficient. To this end, we introduce the ADE method (Barakat and