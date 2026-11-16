# Chapter 16

# Average, lookback and other exotic options

# Contents

| Section | Page |
| :--- | :--- |
| 16.1 Bermudan options | 166 |
| 16.2 Asian options | 169 |
| 16.3 Lookback options | 170 |
| 16.4 Monte Carlo Pricing of options whose payoff depend on the whole price path | 172 |
| 16.4.1 Generating a series of lognormally distributed variables | 172 |
| 16.5 Control variate | 175 |
| 16.6 References | 176 |

We now look at a type of options that has received a lot of attention in later years. The distinguishing factor of these options is that they depend on the whole price path of the underlying security between today and the option maturity.

# 16.1 Bermudan options

A Bermudan option is, as the name implies,¹ a mix of an European and American option. It is a standard put or call option which can only be exercised at discrete dates throughout the life of the option. The simplest way to do the pricing of this is again the binomial approximation, but now, instead of checking at every node whether it is optimal to exercise early, only check at the nodes corresponding to the potential exercise times. C++ Code 16.1 shows the calculation of the Bermudan price using binomial approximations. The times as which exercise can happen is passed as a vector argument to the routine, and in the binomial a list of which nodes exercise can happen is calculated and checked at every step.

# Example

Price a Bermudan put. The following informaton is given S = 80, K = 100 r = 0.20; time = 1; σ = 0.25, steps = 500, q = 0.0. Potential exercise times = 0.25, 0.5 and 0.75.

¹Since Bermuda is somewhere between America and Europe...