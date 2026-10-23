```
{ private:
    // PayoffStrategy* ps;   // OLD
    Function ps;

public:
    explicit Payoff(const Function& pstrat);

    // Code same as solution S3

    // ...
};
```

This means that Payoff can be instantiated by any function or callable object having the appropriate signature. We give some code examples to show how flexible this solution is:

```
using namespace std::placeholders;

double K = 20.0;
CallStrategy call(K);
Function payoffCall = std::bind(&CallStrategy::payoff, call, _1);
Payoff pay1(payoffCall);

std::cout << "Give a stock price (plain Call): ";
double S;
std::cin >> S;

//std::cout << "Call Payoff is: " << pay1.payoff(S) << '\n';
std::cout << "Call Payoff is: " << payoffCall(S) << '\n';

double K1 = 30.0;          // Strike price of bought call
double K2 = 35.0;          // Strike price of sell call

BullSpreadStrategy bull(K1, K2);    // Hull example
auto payoffBull=std::bind(&BullSpreadStrategy::payoff, bull, _1);
Payoff pay2(payoffBull);

std::cout << "Give a stock price (BullSpread): ";
std::cin >> S;

std::cout << "Bull spread Payoff: " << payoffCall(S) << '\n';

// Create a payoff on the fly, captured variables
double p = 2.0;
double C = 50.0;
double strike = 50.0;
```