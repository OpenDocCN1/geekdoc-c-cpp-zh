In the current case the mediator/SUD class is composed of its template parameters (using shared pointers). The mediator class has the form:

```
template <typename Sde, typename Pricer, typename Fdm, typename Rng>
class SUD : private Sde, private Pricer, private Fdm, private Rng
{ // System under discussion

private:
    // Four main components
    std::shared_ptr<Sde> sde;
    std::shared_ptr<Fdm> fdm;
    std::shared_ptr<Rng> rng;
    std::shared_ptr<Pricer> pricer;

private:
    // Other MC-related data

    int NSim;
    std::vector<double> res;      // Generated path per simulation

public:
    SUD() {}
    SUD(const std::shared_ptr<Sde>& s,
    const std::shared_ptr<Pricer>& p,
    const std::shared_ptr<Fdm>& f,
    const std::shared_ptr<Rng>& r,
    int numberSimulations, int NT)
        : sde(s), pricer(p), fdm(f), rng(r)
    {
        NSim = numberSimulations;
        res = std::vector<double>(NT + 1);
    }

    void start()
    { // Main event loop for path generation

        double VOld, VNew;

        for (int i = 1; i <= NSim; ++i)
        { // Calculate a path at each iteration

            if ((i / 100000) * 100000 == i)
            { // Give status after a given numbers of iterations

                std::cout << i << ",";
            }

            VOld = sde->InitialCondition(); res[0] = VOld;

            for (std::size_t n = 1; n < res.size(); n++)
```