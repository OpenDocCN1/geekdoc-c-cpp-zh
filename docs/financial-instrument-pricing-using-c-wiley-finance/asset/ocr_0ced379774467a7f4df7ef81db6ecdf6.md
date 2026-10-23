The body is:

```
CNIBVP::CNIBVP(): IBvpSolver(), A(Vector(J + 1)), B(Vector(J + 1)),
                 C(Vector(J + 1)), F(Vector(J + 1)){}

CNIBVP::CNIBVP(IBvp& source, long NSteps, long JSteps)
        : IBvpSolver(source, NSteps, JSteps),
          A(Vector(J + 1)), B(Vector(J + 1)), C(Vector(J + 1)),
          F(Vector(J + 1)){}

void CNIBVP::calculate()
{
  // Tells how to calculate sol. at n+1

  // In general we need to solve a tridiagonal system

  double t1, t2, t3, Low, Mid, Upp;

  for (std::size_t i = 0; i < F.size(); i++)
  {
    t1 = (0.5*k*ibvp->Diffusion(xarr[i], tnow);
    t2 = 0.25*k * h* ibvp->Convection(xarr[i], tnow);
    t3 = 0.5*k*h2*ibvp->Reaction(xarr[i], tnow);

    // Coefficients of the U terms
    A[i] = t1 - t2;
    B[i] = -h2 - 2.0*t1 + t3;
    C[i] = t1 + t2;

    // Coefficients of the U terms
    double t1A = 0.5*k*ibvp->Diffusion(xarr[i], tnow);
    double t2A =
          0.25 * k * h* ibvp->Convection(xarr[i], tprev);
    double t3A = 0.5*k*h2*ibvp->Reaction(xarr[i],tprev);

    Low = -t1A + t2A;
    Mid = -h2 + 2.0*t1A - t3A;
    Upp = -t1A - t2A;

    F[i] = Low*vecOld[i-1] + Mid*vecOld[i] + Upp*vecOld[i+1]
           +0.5*k*h2*ibvp -> Rhs(xarr[i], tnow)
           +0.5*k*h2*ibvp -> Rhs(xarr[i], tprev);
  }

  double BCL = ibvp->Bcl(tnow);
  double BCR = ibvp->Bcr(tnow);
  DoubleSweep<double> mySolver(A, B, C, F, BCL, BCR);

  // The matrix must be diagonally dominant; we call the
  // assert macro and the program stops
  // assert (mySolver.diagonallyDominant() == true);

  vecNew = mySolver.solve();
}
```