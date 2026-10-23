```
U = u::matrix<double>(xmesh.size(), ymesh.size());
V = u::matrix<double>(xmesh.size(), ymesh.size());

MatNew = u::matrix<double>(xmesh.size(), ymesh.size());

initIC();
}

~TwoFactorAsianADESolver()
{
}

////////////////////////////////////////////////////////////
void initIC()
{ // Utility function to initialise payoff function and BCs at t = 0

tprev = tnow = tmesh[0];

// Now initialise values in interior of interval using
// the initial function 'IC' from the PDE
for (std::size_t i = 0; i < xmesh.size(); ++i)
{
    for (std::size_t j = 0; j < ymesh.size(); ++j)
    {
        MatNew(i,j) = U(i, j) = V(i, j) = AnchorPde::IC(xmesh[i], ymesh[j]);
    }
}
}

void calculateBC()
{ // Calculate the discrete BC on the FOUR edges of the boundary

// Lower and Upper BC
std::size_t lower = 0;
std::size_t upper = ymesh.size()-1;
for (std::size_t i = 0; i < xmesh.size(); ++i)
{
    MatNew(i, lower) = U(i, lower) = V(i, lower)
        = AnchorPde::BCLower(xmesh[i], tnow);// N/A
        // anymore
    MatNew(i, upper) = U(i, upper) = V(i, upper)
        = AnchorPde::BCUpper(xmesh[i], tnow);
}

// Left and Right BC
std::size_t left = 0;
std::size_t right = xmesh.size() -1;
for (std::size_t j = 0; j < ymesh.size(); ++j)
{
```