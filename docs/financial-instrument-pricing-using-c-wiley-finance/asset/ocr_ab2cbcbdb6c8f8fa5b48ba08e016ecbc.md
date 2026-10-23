```
SUD<GBM, EuropeanPricer, EulerFdm<GBM>, MTRng>
    s2(sde, pricerPut, fdm, rng2, NSim, NT);
SUD<GBM, EuropeanPricer, EulerFdm<GBM>, MTRng64>
    s3(sde, pricerCall, fdm, rng3, NSim, NT);
SUD<GBM, EuropeanPricer, EulerFdm<GBM>, FibonacciRng>
    s4(sde, pricerCall, fdm, rng4, NSim, NT);
```

```
auto fn1 = [&]()
{ s.start(); std::cout << "\n Polar Marsaglia: " << s.Price(); };
auto fn2 = [&]()
{ s2.start(); std::cout << "\n MT: " << s2.Price(); };
auto fn3 = [&]()
{s3.start(); std::cout << "\n MT64:" << s3.Price(); };
auto fn4 = [&]()
{ s4.start(); std::cout << "\n Fibonacci: " << s4.Price(); };
```

The tests are (we discuss them in later sections):

```
int main()
{
    SequentialMonteCarlo();
    MonteCarloPPLParallel_Invoke();
    MonteCarloCPP11_Futures();
    MonteCarloCPP11_Threads();
    MonteCarloCPP11_OpenMP();

    return 0;
}
```

The output and run-time performance of each test is:

# Sequential

```
Polar Marsaglia: 5.85298
MT: 5.84891
MT 64: 2.12642
Fibonacci: 2.13177
```

```
Elapsed time sequential in seconds: 585.127
```

# PPL tasks

```
Fibonacci: 2.13151
MT 64: 2.13177
MT: 5.84637
Polar Marsaglia: 5.84895
```

```
Elapsed time PPL tasks in seconds: 299.583
```