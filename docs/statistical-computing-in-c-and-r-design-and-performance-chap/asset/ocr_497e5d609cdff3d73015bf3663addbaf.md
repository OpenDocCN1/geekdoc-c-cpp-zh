# GOLDEN SECTION

```
Vector smooth(double* lam, double* GCV, double a = -5, double b = 5,
    int nGridPts = 100 const;
```

When the Optim class has completed its work the GCV and lam arguments will point to memory that contains the value for approximating smoothing parameter and the corresponding value of the objective function. Additional arguments that provide the lower and upper search interval (for powers of 10) and the number of grid points to use in the search have been suitable default values that will be effective in most instances. Thus, the user can simply call the smooth method and receive a “best” in the returned Vector object. There is a bit of subtlety here merits a comment. The compiler can distinguish between the second version of smooth with its default arguments and the first is due to the use of double* (as opposed to double) for the type of the lam argument and the newer version. The pointer type for lam is the correct choice in the second instance because lam is really an output after input.

The definition of our new smooth method

```
Vector Linss(double* lam, double* GCV, double a, double b,
    int nGridPts) const {
    Function<const Linss> F(this, &gcv);
    Optim<const Linss> Opt;
    //grid search
    double gcvMin = Opt.gridSearch(F, a, b, nGridPts);

    //golden section in the neighborhood of the minimizer
    double halfRange = (b - a)/((double)nGridPts);
    double low = gcvMin - halfRange;
    double up = gcvMin + halfRange;
    gcvMin = Opt.golden(F, low, up);
    *lam = pow(10, gcvMin);
    // compute the fit at the GCV optimal lambda
    Vector fit = smooth*(lam, GCV);
    return fit;
}
```

The method begins by creating a function for the object's gcv function using this pointer and template parameter at T = const Linss. A class Opt object, also with T = const Linss, is created and used with the gcv function to apply the gridSize method. If the default arguments are used, a 100 point search is carried out over the range λ [10⁻⁵,0]. This provides two points around the (possibly local) minimizer that are then passed to the Opt class golden method. Finally the returned value from golden is used by the smooth method to obtain the fit of the data at the minimizer that is returned to the calling program.

Some discussion may be helpful and subsequently on how the const modifier is used in creating the function objects in the smooth method. Smooth should not allow the members of a linss object which it has designated as a const method. This has the effect of making the object's this pointer to a const linss object. The template parameter must therefore be set as const Linss. However, there is a bit more going on here. The optimization is applied to the linss class gcv function which will be called by this pointer an opt object. Seeing as const functions can be called by const objects, it is necessary that gcv also becomes a const class methods. Failure to do will lead to a compilation error.

Upon compilation, the Linss class smooth method was applied to the data created in Section 7.2.5 that is shown in Figure 8.2. This produces a minimizing value of λ_opt = .155978 and GCV(λ_opt) = 3.700569. In Section 7.2.5 the value λ = .1 was used