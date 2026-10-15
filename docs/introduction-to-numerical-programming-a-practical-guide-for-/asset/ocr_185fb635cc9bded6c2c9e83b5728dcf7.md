# Listing 2.4 Use of the Recommended Implementation of the Factorial (C/C++ Coding)

```
// Calculates combinations using a factorial function
#include <stdio.h>

//==============================================================================
double Fact(int n)
//--------------------------------------------------------------------------------
// Returns the factorial of n
//--------------------------------------------------------------------------------
{
    double f;
    int i;

    f = 1e0;
    for (i=2; i<=n; i++) f *= i;
    return f;
}

int main()
{
    double C;
    int k, n;

    printf("n = "); scanf("%d",&n);
    printf("k = "); scanf("%d",&k);

    C = Fact(n) / (Fact(k) * Fact(n-k));

    printf("C(%d,%d) = %f\n",n,k,C);
}
```

on the stack (specialized memory region) a full set of copies of the locals and parameters associated with the particular level of recursion. To avoid infinite processes, and, thereby, the danger of overrunning the stack’s capacity, any recursive routine needs to implement a control mechanism for the depth of the self-calls and the eventual exit from the process in reversed order of the recursion levels.

The recursive implementation of the factorial as function FactRec is provided in Listings 2.5 and 2.6. It should be pointed out that, although more compact, due to the overhead brought about by the repeated self-calls and replication of the local variables on the stack, the recursive implementation is less efficient than the iterative implementation used in function Fact. Obviously, the speed difference is relevant not for single executions, but for intensive use of the functions, when the recursive approach proves to be significantly slower.

# Listing 2.5 Factorial Function Using Recursivity (Python Coding)

```
#==============================================================================
def FactRec(n):
#-------------------------------------------------------------------------------
# Returns the factorial of n using recursivity
#-------------------------------------------------------------------------------
    return (n * FactRec(n-1) if (n > 1) else 1e0)
```