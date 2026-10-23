```
// Payoff as a lambda function
double K = opt.K;
auto Payoff = [&K] (double S)-> double {return std::max<double>
(K - S, 0.0);};

// Price a plain option
double res = LatticeMechanisms::BackwardInduction<double>(lattice,
algorithm, Payoff);
std::cout << "Plain Option price, classic #1: ";
```

We now price the corresponding American option price as follows:

```
// Create basic structure for early exercise options
Lattice<double,2> lattice2(lattice);

// The early exercise constraint
auto AmericanAdjuster = [&Payoff] (double& V, double S)->void
{ // e.g. early exercise

    V = std::max<double>(V, Payoff(S));
};

// Price an early exercise option
double res2 = LatticeMechanisms::BackwardInduction<double>
    (lattice2, algorithm, Payoff,AmericanAdjuster);
    std::cout << "Early exercise option price";
```

Notice that we use a lambda function to implement the early-exercise constraint.
You can run the code from the distribution medium and check the answers for a range of parameter values. We recommend that you experiment with the code, modify it and try to get a hands-on feeling for how the framework works.

# 11.6 ADVANTAGES OF SOFTWARE LAYERING

The three-layer design approach offers a number of advantages as far as software maintainability, understanding and extendibility are concerned. First, we have a well-known and defined process (the Layers pattern) on which to build the C++ lattice framework. It also gives developers a vocabulary that allows them to communicate with each other (and with themselves!) at a higher level than just (possibly undocumented) blocks of code. Second, it reduces the coupling between software components and modules. Third, it improves the cohesion of the components in each layer because their operations are closely related and hence do not depend on the components in other layers. Finally, it is relatively easy to add new modules to the framework. We now discuss these topics in more detail from the viewpoint of the quality characteristics of the ISO 9126 standard. The guidelines can also be applied to other problems.