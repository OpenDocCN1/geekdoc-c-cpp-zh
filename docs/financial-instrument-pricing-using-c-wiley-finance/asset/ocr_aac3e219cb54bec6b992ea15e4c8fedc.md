```
ImpliedVolatilityEstimator ivp2(callMarketPrice, pricer2);

//  auto callPricer = std::bind(PutPrice, std::placeholders::_1);

// Bounds for implied volatility
value_type sigL = 0.0023; value_type sigH = 0.9;
value_type fL = 0.0;
value_type fH = 0.0;

Terminator<value_type> stopping(1.0e-12);
ReportingDefault<value_type> report;
MISDefault<int> mis;

ThreePointIntervalSolver<value_type> solver1(ivp1, sigL, sigH);
GoldenSectionIntervalSolver<value_type> solver2(ivp2, sigL, sigH);
BrentIntervalSolver<value_type> solver3(ivp2, sigL, sigH);
```

Finally, we create and run the mediators:

```
Mediator<value_type> med1(ivp1, sigL, sigH, stopping,
                             solver1, mis, report);
med1.run();

Mediator<value_type> med2(ivp2, sigL, sigH, stopping,
                             solver2, mis, report);
med2.run();

Mediator<value_type> med3(ivp2, sigL, sigH, stopping,
                             solver3, mis, report);
med3.run();
```

It is also possible to create an instantiation of the classes in Figure 19.1 by using lightweight lambda functions (we do not need to create classes as with the traditional object-oriented style):

```
ITerminationType<value_type> brentTerm
    = [](value_type a, value_type b) { return true; };

IMISType<value_type> mis4
    = [](value_type a, value_type b, value_type fa,value_type fb) {};

auto report4
    = [](value_type a, value_type b, value_type fa, value_type fb)
      {std::cout<<std::setprecision(16)<<"Brent" << (a + b)/2; };

GoldenSectionIntervalSolver<value_type> brentSolver(ivp1, sigL, sigH);

Mediator<value_type> med4
    (ivp1, sigL, sigH, stopping, brentSolver, mis4, report4);
med4.run();
```