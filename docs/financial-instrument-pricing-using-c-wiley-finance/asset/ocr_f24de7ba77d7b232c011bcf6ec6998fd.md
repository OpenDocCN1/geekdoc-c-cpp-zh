In Layer 3 we configure and initialise the parameters and functions for an application, for example:

+   - The option parameters.
+   - The kind of payoff.
+   - Whether to use the binomial method or trinomial method.
+   - Accommodating extra features such as early exercise and barriers, for example.

From a software viewpoint it is possible to configure an application in many ways. An important requirement is to determine how maintainable the code in Layer 3 should be. In Duffy (2006A) we used class hierarchies to add flexibility into the configuration process. A more flexible solution is to use the Builder pattern (see GOF, 1995) that configures the application’s object network. In this section, however, we avoid creating class hierarchies and instead we use function objects, lambda functions and function wrappers to configure applications. This approach leads to readable and understandable code in our opinion. We now give an initial example to price European and American options.

# 11.5 INITIAL '101' EXAMPLES OF OPTION PRICING

We take a complete example of pricing European and American options using the Cox-Rubinstein-Ross (CRR) method (see Clewlow and Strickland, 1998). We compute the up and down jump size and probability parameters and furthermore we encapsulate these parameters in a class called CRRLatticeAlgorithms. This class is a function object because it has two operators that are compatible with the function wrappers needed by the algorithms in Layer 2 of the framework:

```
class CRRLatticeAlgorithms
{ // The function object that implements forward and backward
// induction algorithms based on CRR

private:
    double u;
    double d;
    double p;
    double discounting;

public:
    CRRLatticeAlgorithms(const OptionData& option, double dt)
    {

        double s = option.sig;
        double r = option.r;

        double R1 = (r - 0.5 * s * s) * dt;
        double R2 = s * std::sqrt(dt);
```