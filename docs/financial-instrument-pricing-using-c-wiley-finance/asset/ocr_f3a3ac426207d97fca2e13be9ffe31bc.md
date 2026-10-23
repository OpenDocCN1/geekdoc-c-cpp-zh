```
std::cout << "Type 2: " << cType2 << std::endl;
std::cout << "Type 3: " << cType3 << std::endl;
std::cout << "Type 4: " << cType4 << std::endl;
}

return 0;
}
```

We tested these algorithms using the Genz/West code:

```
double M(double a, double b, double rho)
{
    return bivarcumnorm(a, b, rho);
}
```

The output is:

```
Call correlation: 4.707330012666851
Put correlation: 3.909280147364093
Call min K: 0.0180004745810719
Call max K: 20.94494846250169
Call worst cash-or-nothing best: 2.793935852582142
Two-asset cash-or-nothing types:
Type 1: 2.498749451519521
Type 2: 2.156694921716584
Type 3: 0.2128123872130617
Type 4: 4.644037484557975
```

We now price these options using the extrapolated version of the finite difference scheme:

```
double M(double a, double b, double rho)
{
    using value_type = double;

    std::size_t NX = 50;    std::size_t NY = 50;
    value_type AL = -8.0; value_type BL = -8.0;
    auto xarr = CreateMesh(NX, AL, a);
    auto yarr = CreateMesh(NY, BL, b);

    BVNFunction<value_type> bvn(rho);
    GoursatFdmExtrapolation<value_type> fdm(AL, BL, bvn, NX, NY);

    return fdm(a, b);
}
```

The output in this case is:

```
Call correlation: 4.707325487726628
Put correlation: 3.909281409246201
```