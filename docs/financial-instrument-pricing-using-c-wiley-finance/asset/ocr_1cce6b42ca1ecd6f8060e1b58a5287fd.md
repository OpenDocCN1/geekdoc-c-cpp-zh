At the ex-dividend date the value of the stock drops in value at time n to:

$S(1 - D)u^{j}d^{n-j}, \quad 1 \le j \le n. \tag{12.8}$

When using dividends with the binomial method we note that the nodes prior to the ex-dividend date remain unchanged while the nodes after the ex-dividend date are modified based on formula (12.8). We need to give the dividend value and the ex-dividend date when we design the C++ code.

In the case of a simple lattice ADT the ex-dividend date is a number while in the case of a generalised lattice ADT it can be a date object, for example.

From a C++ perspective we note that the current framework can handle discrete proportional dividends but we must modify the lattice to reflect formula (12.8) after the basic forward induction algorithm has been executed. A typical example is:

```
// Create basic structure for plain options
Lattice<double,2> lattice(N, 0.0); // init
double rootVal =100.0;
LatticeMechanisms::ForwardInduction<double>(lattice, algorithm, rootVal);

// Modify the basic lattice to account for known
// discrete proportional dividend
double div = 0.03;
double factor = 1.0 - div;
int n = 2; // Ex-dividend date

// Modify values to multiply by factor in [n,end]
for (std::size_t j = n; j <= lattice.MaxIndex(); ++j)
{
    for (std::size_t i = 0;i<lattice[j].size(); ++i)
    {
        lattice[j][i] *= factor;
    }
}
```

See Exercise 8 where we discuss possible performance improvements.

# 12.4.3 Perpetual American Options

In general, there is no closed-form solution for the price of dividend-paying American options. There is one exception (Haug, 2007) and this is the case of a perpetual option, that is one with an infinite expiration. For a call option the price is:

$c = \frac{K}{y_1 - 1}\left(\frac{y_1 - 1}{y_1}\frac{S}{K}\right)^{y_1} \quad \text{where} \quad y_1 = \frac{1}{2} - \frac{b}{\sigma^2} + \sqrt{\left(\frac{b}{\sigma^2} - \frac{1}{2}\right)^2 + \frac{2r}{\sigma^2}} \tag{12.9}$

while for a put option the price is:

$p = \frac{K}{1 - y_2}\left(\frac{y_2 - 1}{y_2}\frac{S}{K}\right)^{y_2} \quad \text{where} \quad y_2 = \frac{1}{2} - \frac{b}{\sigma^2} - \sqrt{\left(\frac{b}{\sigma^2} - \frac{1}{2}\right)^2 + \frac{2r}{\sigma^2}}. \tag{12.10}$