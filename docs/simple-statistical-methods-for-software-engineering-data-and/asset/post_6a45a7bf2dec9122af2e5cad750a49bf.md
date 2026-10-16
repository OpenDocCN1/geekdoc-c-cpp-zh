
Working with a PDF such as gamma has further advantages. First, gaps in data are filled by the equation. Second, one can extrapolate mathematically and see beyond boundaries. Third, strategic planners can estimate risk.

There are several options available while choosing a PDF for rainfall data. Statistical techniques include the compound Poisson–exponential distribution; the log, square root, and cube root normal distributions; the gamma distribution; various normalizing transforms; the kappa distribution, the Weibull distribution, and the Box–Cox transformation.

However, the gamma distribution is frequently used to represent precipitation because it provides a flexible representation of a variety of distribution shapes while using only two parameters: shape and scale (based on Husak [4]).

## NIST Formula for Gamma Parameter Extraction

Instead of the approach we used in plotting Figure 18.4 where we had used visual judgment of histogram of data to decide on shape and the method of moment formula given in Equation 18.2, to calculate scale, we can use the more rigorous NIST [5] formulas presented in Equations 18.5 and 18.6 for parameter extraction:

Shape α = (x̄ / s)²
(18.5)

Scale β = s² / x̄
(18.6)

where x̄ is the mean and s is the standard deviation.

## Applying Gamma Distribution to Software Reliability Growth Modeling

Gamma distribution has been used in reliability studies. The gamma cumulative distribution function (CDF) is an S curve and can represent cumulative defects discovered in software. An example of CDF, although on a different metric, may be found in Figure 18.5. A CDF plotted with cumulative defects is known as the software reliability growth curve, a subject treated in detail in Chapter 19 where the Weibull distribution is used and in Chapter 21 where the Gompertz distribution is used.

Although the Weibull distribution is popularly used to fit failure data, the gamma distribution is more suited in certain cases. In a research study, Sonia Meskini [6] applies gamma distribution to construct a software reliability growth model for smart phones. Sonia observes,

In Skype Version I the Weibull distribution is the closest to the actual behavior curve of the application, followed by the gamma distribution. In Skype Version 2 it is to be noted that although the S-shaped distribution is a particular case of the gamma distribution, it fits the data slightly better. For Skype Version 3 it can be concluded that the gamma distribution is the closest to the actual behavior curve of the application failure data, followed by the Rayleigh distribution.

In her conclusion Sonia mentions,

We collected data from all over the world and divided them into different versions, and grouped them into different time periods (days, weeks, and months). Each application version failure data, when plotted in time periods, shows the same pattern: an early ‘burst of failures,’ likely due to the most evident defects, followed by a steep decrease in failure rate. We first tried several non-linear distributions to better fit the failure data, and after numerous experiments, we found that the observed behavior is better modeled by the Weibull or gamma distributions.

Sonia finally states that, in her observation,

It can be noted that the gamma distribution, along with its particular S-shaped case, model more frequently the failure data.

In essence, gamma distribution is attractive because of its simplicity, to perform as on Software reliability growth model. Gamma fits elegantly to processes that are not in our direct control but dependent on external factors like customer. With less data points we can do simulation using gamma distribution.

## BOX 18.5 MODELING EARTHQUAKE DAMAGE WITH GAMMA DISTRIBUTION

The application of the gamma distribution to failure data has been extended to model damages produced by earthquakes. Repeated overloading of structures due to earthquake shocks cumulates damage on the hit structure. The parameter “residual ductility to collapse” is used to measure this damage. The cumulated level of deterioration can be modeled by gamma distribution. The occurrence of earthquakes is a Poisson process (see Chapter 12, Law of Rare Events), but cumulative wear is a gamma process. Structure reliability is obtained by estimating the probability of cumulated damage exceeding the threshold (based on Iervolino and Chioccarelli [7]).

## Chapter 19

## Weibull Distribution: A Tool for Engineers

The genesis of the Weibull distribution goes back to the Rayleigh distribution. The Rayleigh distribution was invented in 1905 (see Box 19.1). The Weibull distribution was invented much later by Waloddi Weibull in Sweden in 1939 (see a brief biographical note in Box 19.2). Since the discovery of the Weibull distribution, it has cast great influence in engineering, especially in reliability analysis. The scope of its application has widened to several areas of physics and management (see Box 19.3 for a few instances).

## BOX 19.1 RAYLEIGH FLIGHT

It so happens that the Rayleigh distribution, invented in 1905, is a special case of the Weibull distribution invented in 1939. The Weibull distribution type II with location constant 0 and shape factor 2 is the Rayleigh curve. Both are skewed to the right.

The discovery follows research on the historic “random walk” problem posed by Pearson.

Pearson posed his problem in Nature (July 27, 1905).

A man starts from a point 0 and walks l yards in a straight line; he then turns through any angle whatever and walks another l yards in a second

straight line. He repeats this process n times. I require the probability that after n of these stretches he is at a distance between r and r + δr from his starting point.

Rayleigh pointed out that, for large values of n, the answer given by Rayleigh was

```
2/(n l²) e^(-r²/(n l²)) r δr
```

(19.1)

This actually has the shape of a normal distribution, centered at the origin. In this equation Rayleigh assumed that the drunkard walks in one dimension. The model suggests that the drunkard will return to the origin after a random walk. If we allow two additional dimensions and solve the problem, a new phenomenon called Rayleigh Flight occurs. The distribution now is Rayleigh. The drunkard will not return to the origin.

Rayleigh missed Smoluchowski’s 1906 paper on the motion of colloidal particles, in which he introduces the random flight idea.

A one-dimensional walk is Gaussian. A multidimensional walk is Rayleigh. Brownian motion in one dimension is Gaussian. The vector sum of Brownian movements in several dimensions is Rayleigh. Simple processes follow Gaussian. A combination of several simple processes is Rayleigh.

Software development is due to the combined work of several people and several processes. Even if the individual processes are Gaussian, the combined result can be the skewed Rayleigh. This being the essential case, can we expect team results to be normally distributed? Relentless pursuit of normality in software engineering data is futile.

IBM’s Peter Norden (see Box 19.4) favored the Weibull equation over the logistic curve to model software development project cost. Lawrence Putnam promoted the Weibull curve with shape factor = 2 as a Rayleigh distribution. Putnam used this in his estimation model SLIM to estimate cost and defect. He went further to call this distribution the software equation.

> The Weibull distribution is by far the world’s most popular statistical model for life data. It is also used in many other

applications, such as weather forecasting and fitting data of all kinds. Among all statistical techniques it may be employed for engineering analysis with smaller sample sizes than any other method.

Robert B. Abernethy

## Weibull Curves

We will start with Weibull plots with three standard values for the shape parameter: 1, 2, and 3. These three plots are shown in Figure 19.1. We have chosen a scale factor of 20 and have kept it the same for the three plots. The shapes of these three curves resemble the shapes of the exponential distribution, the Rayleigh distribution, and the normal distribution, respectively. The three figures represent a family of curves known as the Weibull family.

The curves shown are possible models for service time in a software maintenance project with a median value of 20 days and hypothetically equating the scale parameter to the median value.

The Weibull equation, which has been used in creating the curves, is given as follows:

```
W(x) = α/β (x/β)^{α-1} e^{-(x/β)^α}    α, β > 0    (19.2)
```

where α is the shape parameter and β is the scale parameter.

The value of shape factor is not limited to the three integers shown in Figure 19.1. It can be any positive number and can be used to generate an infinite number of the Weibull curves.

## Parameter Extraction

## Rules of Thumb

The shape factor can be judged by looking at data histograms. To start the iteration of curve fitting, it is good to begin with the nearest of the three shapes 1, 2, and 3 and then converge using the least square error method. Scale is substantially influenced by median, as shown in the following rule of thumb:

```
Scale = C₁ median
```

```
C₁ = 0.09 shape factor + 0.636
```
