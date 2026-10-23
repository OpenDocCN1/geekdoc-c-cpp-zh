```
// Create Sde
return std::shared_ptr<Sde<T>>(new Sde<T>(Functions, S0, B));
}

template <typename T>
std::shared_ptr<Sde<T>> CIR Sde(T alpha, T b, T sigma, T S0, T B)
{

auto drift = [=](T t, T X) { return alpha*(b-X); };
auto diffusion = [=](T t, T X) { return sigma * std::sqrt(X); };
ISde<T> Functions = std::make_tuple(drift, diffusion);

// Create Sde
return std::shared_ptr<Sde<T>>(new Sde<T>(Functions, S0, B));
}

template <typename T>
std::shared_ptr<Sde<T>> ChooseSde(const OptionData& data, T S0)
{ // Simple factory method

std::cout << "1. GBM, 2. CEV, 3. CIR: ";
int choice; std::cin >> choice;

if (1 == choice)
{
return GbmSde<T>(data, S0);
}
if (2 == choice)
{
return CevSde<T>(data, S0);
}

if (3 == choice)
{
// Feller condition => 2 a b >= sigma^2
double alpha = 0.01;
double b = 7.0;
double sigma = 0.9;
double B = 1.0; // Upper limit of interval
double X0 = 0.4;

return CIR Sde<T>(alpha, b, sigma, X0, B);
}
else
{
return GbmSde<T>(data, S0);
}
}
}
```