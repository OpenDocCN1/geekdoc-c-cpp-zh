
providers. The more sophisticated investors may be less susceptible to risk preference bias.

One way to determine the relative investor sophistication is to look at the historical relation between net equity mutual fund flows for different types of mutual funds and risk aversion over time. The seasoned investor with constant risk preferences would rationally rebalance to equity mutual funds during a bear market. A biased investor may be less attracted to equity funds as valuations fall, increasing the portfolio share of safe assets when valuations of risky assets are most attractive. One may use three different methods to classify investors based on net equity mutual fund flows:

- 1) Sort by whether funds are actively or passively managed. Passive mutual funds are assumed to be those classified as "index" funds by Morningstar, Inc., while all other mutual funds are considered actively managed funds. There is evidence that investors in passive funds are more sophisticated than investors in active funds that are most often sold through the broker channel.
- 2) Classify mutual funds into four different fund groups: broker-sold, institutional, investor, or retirement.
- 3) One may further decompose the broker-sold category by the form of compensation paid to the financial advisor. Differences in the method of compensation provided through share class structure may influence whether the advisor gains from debiasing a client who is tempted to shift the portfolio to safety during an equity market decline.

## 5.5 A Unified Approach for Time Varying Risk Aversion

Although traditional finance theory assumes that risk aversion is not time-varying, there is a growing body of empirical research that suggests that risk preferences change with market conditions. Using a unique dataset with daily responses to a risk tolerance questionnaire from participants in a defined contribution plan, one may find significant evidence that risk aversion is time-varying. It is also noted that investor expectations tend to be a better predictor of time-varying risk aversion than historical performance. Thus, it seems that risk aversion is driven more by the unknown future than the known past.

While investor expectations influence risk aversion over time, other investor attributes (such as age, equity allocation, and salary, etc.) appear to play an even greater role in shaping risk aversion. Time-varying risk aversion has important implications for the demand for risky assets since investors tend to avoid risky assets when valuations are most attractive and when traditional portfolio theory would predict greater demand for equities to rebalance a portfolio. This effect is especially noteworthy given the increasing use of the “traditional” RTQs by investment advisors when recommending an optimal client portfolio allocation. This is important because the primary reason that individual investors under-perform institutional investors is their tendency to sell equity mutual funds during a bear market.

More sophisticated investors, such as those who use index (versus active) mutual funds and buy institutional share classes, exhibit lower time-varying risk aversion. It is also noted that a consistent negative relation between time-varying risk aversion and net equity mutual fund flows when sorted by fees. Trail compensation, which provides the same incentive whether the client buys new funds to match their changing risk preferences, is associated with a lower variable risk preference bias. Financial advisor compensation schemes that provide greater compensation for acceding to variable risk preference biases are associated with a failure to debias. This finding is consistent with research on perverse incentives from traditional commission.

## 5.6 Assets Allocation Worked Examples

### 5.6.1 Worked Example 1: Assets Allocation Using R

### The Black-Litterman (B-L) Asset Allocation Model

### Overview

Combining information from two sources to create an estimate of expected returns:

Source 1: What does the current market tell us about the expected excess returns? Implied excess equilibrium returns?

Source 2: What views does the investment manager have about particular stocks, sectors, asset classes, or country?

The B-L model combines these different sources to produce estimates of excess returns.

### Combining predicted and implied returns

```
E(r - r_f) = [(τΣ)^-1 + P^T Ω^-1 P]^-1 [(τΣ)^-1 Π + P^T Ω^-1 Q]
```

### Basic Notation

- τ = A scalar (assume τ = 1).
- Σ = Variance–Covariance matrix for all assets under consideration
- Ω = Uncertainty surrounding your views.
- Π = Implied excess returns
- Q = Views on expected excess returns for some or all assets
- P = Link matrix identifying which assets you have views about

### Understanding the Formula Splitting into two sections for better understanding

Consider the second section first:

(τΣ)^-1    Π    +    P^T Ω^-1    Q
↓          ↓          ↓          ↓
Measures   Implied   Confidence  Our
of confidence excess returns    views

We are combining implied excess returns with our own views on excess returns:

A weighted average

What are the weights?

E(r - r_f) = [(τΣ)^-1 + P^T Ω^-1 P]^-1 [(τΣ)^-1 Π + P^T Ω^-1 Q]

The investor weights his/her views relative to the implied excess returns.

- How confident?

Ω will be large ⇒ Ω^-1 will be small

### Understanding the formula:

E(r - r_f) = [(τΣ)^-1 + P^T Ω^-1 P]^-1 [(τΣ)^-1 Π + P^T Ω^-1 Q]

The first part of this formula:
[(τΣ)^-1 + P^T Ω^-1 P]^-1

- τ implies excess returns and our views add up to 1.
- Namely, the formula is just a weighted average!

### Consider a worked example:

Consider 1 stock: AMZN (Amazon.com)

- The implied excess returns are 0.74% per month and the variance is 2.018%
  We predict excess returns of 2% per month. The uncertainty surrounding this view is reflected by a variance of 0.50%
  ⇒ Π = 0.74%
  S = 2.015%
  Q = 2%
  Ω = 0.50%
- Assume τ = 1, P = 1

Substituting into the B-L formula:

E(r - r_f) = [(τΣ)^{-1} + P^T Ω^{-1} P]^{-1} [(τΣ)^{-1} Π + P^T Ω^{-1} Q]
= [0.02015^{-1} + 0.005^{-1}]^{-1} × [0.02015^{-1} × 0.0074 + 0.005^{-1} × 0.02]
= [49.63 + 200]^{-1} × [49.63 × 0.0074 + 200 × 0.02]
= [249.64]^{-1} × [0.3673 + 4]
= 4.3673/249.63
= 0.017495
= 1.749% per month

Does this estimate make sense?

Since we are confident about our views, now, try a more complicated example:

### Incorporating Investor Views:

1) Analysts tell you that AEP has found a way to store electricity. Based on this breakthrough, they expect AEP to outperform XOM by 1% per month.

| Stock^a) | Historical excess returns | CAPM excess returns | Implied excess returns |
|---|---|---|---|
| INTC^a) | 0.0035 | 0.0135 | 0.0092 |
| AEP | 0.0026 | 0.0064 | 0.0032 |
| AMZN | 0.0326 | 0.0111 | 0.0074 |
| MRK | 0.0002 | 0.0057 | 0.0059 |
| XOM | 0.0111 | 0.0052 | 0.0064 |

a) Intel, American Electric Power Company, Inc., Amazon, Merck, Exxon Mobil

2) Given the current economic conditions, we think that INTC will outperform AMZN by 1.75% per month.

- Relative views are common in reality.
- Absolute views, such as AEP having returns of 2% per month, are much less common.

### Views versus Implied Excess Returns:

View (1): AEP outperforms XOM by 1% per month

- The difference in implied excess returns is -0.32% per month.
- One would expect that incorporating these views would lead to an increase in one's holdings of AEP and a decrease in XOM:0.0092.

View (2): INTC will outperform AMZN by 1.75% per month.

- The difference in implied excess returns is 0.18% per month.
- We would expect that incorporating our view would increase our holdings of INTC and reduce our holdings of AMZN.

The views expressed above are relative views of assets.

### Incorporating Our Views:

To link our views to implied excess returns, we need a link matrix, P.

Matrix P is constructed in the following way:

Each row represents a view, each column represents a company

|  | INTC | AEP | AMZN | MRK | XOM |
|---|---|---|---|---|---|
| View 1 | 0 | 1 | 0 | 0 | -1 |
| View 2 | 1 | 0 | -1 | 0 | 0 |
| View 3 | 0.5 | 0 | 0.5 | -0.5 | -0.5 |

### The View Vector and Uncertainty

What do Q and Ω look like?

Q + ε = [ |Q₁| ; |Qₖ| ] + [ |ε₁| ; |εₖ| ] → Q + ε = [ 0.01 ; 0.0175 ] + [ ε₁ ; ε₂ ]
View 1 ↓
View 2 ↑

where
[ε₁]   ([0] [ω₁₁ … ω₁ₖ])
[ : ] ~ N ([ : ] ; [ : ] … ; [ : ])
[εₖ]   ([0] [ωₖ₁ … ωₖₖ])
Ω

### Calculating Ω

There is no best way to calculate Ω. It will depend on how confident you are of your predictions.

Black and Litterman recommend
Base ⇒ Ω = τ P Σ Pᵀ , where P = Link matrix and Σ = variance—covariance matrix
