```
template <typename D>
    void ADE_CRTP<D>::calculate()
{ // Tells how to calculate sol. at n+1, Explicit ADE schemes

    static_cast<D*>(this) -> calculate();
}
```

The most interesting function is calculate() because it forwards the request to its template parameter. We discuss the derived class that implements the Barakat and Clark scheme for the diffusion term and the (derived class) Towler–Yang scheme for the convection term:

```
class ADE_BC_CRTP: public ADE_CRTP<ADE_BC_CRTP>
{
private:

    // Intermediate values
    Vector U;
    Vector V;
    Vector UOld;
    Vector VOld;

public:
    ADE_BC_CRTP(IBvp& source, long NSteps, long JSteps);

    // Hook function for Template Method pattern
    void calculate();
};

#include "ADESolver_BC_CRTP.cpp"
```

The corresponding code is based on the algorithms in Chapter 20:

```
ADE_BC_CRTP::ADE_BC_CRTP(IBvp& source, long NSteps, long JSteps)
    : ADE_CRTP<ADE_BC_CRTP>(source, NSteps, JSteps),
      U(Vector(vecNew)), V(Vector(vecNew)), UOld(Vector(vecOld)),
      VOld(Vector(vecOld)) { }
```

```
// Sequential version
void ADE_BC_CRTP::calculate()
{ // Tells how to calculate sol. at n+1, Explicit ADE_BC_CRTP schemes

    U[0] = ibvp->Bcl(tnow);
    U[U.size()-1] = ibvp->Bcr(tnow);

    // Necessary?
    V[0] = ibvp->Bcl(tnow);
    V[V.size()-1] = ibvp->Bcr(tnow);
```