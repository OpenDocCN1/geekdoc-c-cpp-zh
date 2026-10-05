Here I simulate that the deck of cards gets one card smaller with each draw. The card number in the ever-decreasing deck is printed.

# Distributions over Distributions

The exact formulas of all distributions and what their parameterizations mean, of course, mentioned in the standard. To the mathematically inclined, the names will probably mean more. For those, the parameterizations of the distribution functions are probably of more interest. In Table 28.4, real stands for a real number type such as float or double. An int stands for an integer type, such as int, but of course others like long long are also possible.

| Distribution | Distribution Parameters |
| --- | --- |
| Uniform Distributions | |
| uniform_int_distribution | Int a = 0, Int b = max() |
| uniform_real_distribution | Real a = 0.0, Real b = 1.0 |
| Bernoulli Family | |
| bernoulli_distribution | double p = 0.5 |
| binomial_distribution | Int t = 1, double p = 0.5 |
| geometric_distribution | double p = 0.5 |