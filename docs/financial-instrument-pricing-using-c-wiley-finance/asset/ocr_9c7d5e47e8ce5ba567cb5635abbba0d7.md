```
double K;
double T;
double r;
double sig;

// Extra data
double D;      // dividend

int type;      // 1 == call, -1 == put

explicit constexpr OptionData(double strike, double expiration,
                              double interestRate,
                              double volatility, double dividend,
                              int PC)
    : K(strike), T(expiration), r(interestRate),
      sig(volatility), D(dividend), type(PC)
{}

template <typename ArgPack> OptionData(const ArgPack& args)
{
    K = args[OptionParams::strike];
    T = args[OptionParams::expiration];
    r = args[OptionParams::interestRate];
    sig = args[OptionParams::volatility];
    D = args[OptionParams::dividend];
    type = args[OptionParams::optionType];

    std::cout << "K " << K << ", T " << T << ", r " << r << std::endl;
    std::cout << "vol " << sig << ", div " << D << ",type "
              << type << std::endl;
}

};
```

We can initialise the elements of the struct OptionData by calling its constructor (the position of args is important), by uniform initialisation or by using named variables as supported in the Boost Parameter library. In this last case the relative order of the input arguments is immaterial, as the following example shows:

```
//OptionData opt2 { 100.0, 1.0, 0.06, 0.2, 0.03, 1 };

// Init via named Boost variables
OptionData myOption((OptionParams::strike = 65.0,
                    OptionParams::expiration = 1.0,
                    OptionParams::volatility = 0.001,
                    OptionParams::dividend = 0.0,
                    OptionParams::optionType = -1,
                    OptionParams::interestRate = 0.1));
```