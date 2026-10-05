| Distribution | Distribution Parameters |
| --- | --- |
| Sample Family | |
| discrete_distribution | initializer_list<double> wl |
| piecewise_constant_distribution | initializer_list<R> bl, Op1 fw |
| piecewise_linear_distribution | initializer_list<R> bl, Op1 fw |

**Table 28.4** Parameters of the distribution functions.

This is the list of distributions specified in the standard. It is up to the library manufacturer to contribute more. g++ 6.2, for example, adds the following:

+   * arcsine_distribution
* beta_distribution
* exponential_distribution
* hoyt_distribution
* hypergeometric_distribution
* k_distribution
* logistic_distribution
* nakagami_distribution
* normal_mv_distribution
* pareto_distribution
* rice_distribution