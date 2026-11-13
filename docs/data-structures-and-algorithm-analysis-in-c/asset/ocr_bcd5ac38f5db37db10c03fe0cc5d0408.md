```
static const int A = 48271;
static const int M = 2147483647;
static const int Q = M / A;
static const int R = M % A;

/**
 * Return a pseudorandom int, and change the internal state.
 */
int Random::randomInt( )
{
   int tmpState = A * ( state % Q ) - R * ( state / Q );

   if( tmpState > 0 )
      state = tmpState;
   else
      state = tmpState + M;

   return state;
}
```

# Figure 10.55 Random-number modification that does not overflow on 32-bit machines

$x_{i+1} = (Ax_i + C) \pmod{2^B}$

where B is chosen to match the number of bits in the machine's integer, and A and C are odd. Unfortunately, these generators always produce values of x_i that alternate between even and odd—hardly a desirable property. Indeed, the lower k bits cycle with period 2^k (at best). Many other random-number generators have much smaller cycles than the one provided in Figure 10.55. These are not suitable for the case where longer sequences of random numbers are needed. The UNIX drand48 function uses a generator of this form. However, it uses a 48-bit linear congruential generator and returns only the high 32 bits, thus avoiding the cycling problem in the low-order bits. The constants are A = 25,214,903,917; B = 48; and C = 11.

C++11 provides a very general framework for the generation of random numbers. In this framework, the generation of random numbers (i.e., the type of random-number generator used) is separated from the actual distribution used (i.e., whether the numbers are uniformly distributed over integers, a range of reals, or follow other distributions, such as the normal distribution or Poisson distribution).

The generators that are provided include linear-congruential generators, with the class template linear_congruential_engine, which allows the specification of the parameters A, C, and M.

```
template <typename UnsignedType, UnsignedType A, UnsignedType C, UnsignedType M>
class linear_congruential_engine;
```