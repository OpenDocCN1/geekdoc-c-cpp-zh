```
// Function call operator; Template Method pattern
double operator () ()
{
    return rng();
}
```

Some implementations are:

```
#include <random>
#include <cstdlib> // rand()
#include <memory>
#include <vector>
#include <algorithm>
#include <iostream>
#include <ctime>
#include <boost/random.hpp>
```

```
class InfamousRng : public Rng
{
public:
    InfamousRng()
    {
        srand(std::time(0));
    }

    double rng() override
    {
        return rand();
    }
};
```

```
class MTRng : public Rng
{ // Mersenne Twister
private:
    std::mt19937 eng;
    std::uniform_real_distribution<double> d;

public:
    MTRng() : eng(std::mt19937(std::time(0))),
              d(std::uniform_real_distribution<double>(0.0, RAND_MAX))
    {}

    double rng() override
    {
        return d(eng);
    }
};
```