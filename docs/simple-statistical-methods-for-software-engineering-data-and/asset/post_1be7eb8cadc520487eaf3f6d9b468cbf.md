
## Figure 12.1 Exponential distribution of Radioactive decay.

![](img/2f042205c6c0e14747f198ed8f9c9f40_198_0.png)

![](img/2f042205c6c0e14747f198ed8f9c9f40_198_1.png)

| Decay constant | - | 0.172 |
| Mean life time | Mean | 5.814 |
| Half-life time | Median | 4.030 |

## Figure 12.2 Half-life analysis using exponential distribution.

It can be seen that Equation 12.1 is just a variant of the proper exponential probability density function (PDF) shown as follows:

```
f(t) = λe^{-λt}    (12.3)
```

The cumulative distribution function (CDF) is as follows:

```
F(t) = 1 - e^{-λt}    (12.4)
```

where t is time and λ is the rate constant. The mean of this distribution is 1/λ. The standard deviation is also equal to 1/λ.

In engineering, exponential distribution is primarily used in reliability applications. In the context of reliability, λ is known as the failure rate or hazard rate. In a chemical engineering example, corrosion rate is represented in exponential form. In an electrical engineering example, electrical charge stored in a capacitor decays exponentially. In a geophysics example, atmospheric pressure decreases exponentially with height.

Equation 12.3 shows that a single parameter completely specifies the PDF, a unique aspect responsible for the simplicity of the equation.

The other model statistics are as follows:

- The median is (ln 2)/λ.
- The mode is 0.
- The skewness is 2.
- The kurtosis is 9.

The metric% software defects discovered during system testing decreases exponentially with time, as shown in Figure 12.3. Initial test effort discovers more defects, and subsequent tests begin to show lesser results, a common experience in software testing. We assume that risky modules are tested first, as per a well-designed test strategy. Representing defect metrics is a classic application of the exponential model.

Defects found in a testing day are counted and summed up to obtain Figure 12.3. The x-axis of the plot could be test day or even calendar day. We can plot total defects found every week and establish the exponential nature.

In reliability analysis, the median value (ln 2)/λ is called half-life. The mean 1/λ is known as mean time to fail (MTTF). Also, f(t) = e^{-λt} is known as survival function or reliability function. If the MTTF of a bulb is 400 hours, the corresponding f(t) would define the reliability of the bulb. As time goes on, the reliability would decrease, notably after 400 hours, and the reliability of the bulb can be calculated directly from the following expression:

```
Bulb reliability = e^{-(t/400)}
```

![](img/2f042205c6c0e14747f198ed8f9c9f40_200_0.png)

## Figure 12.3 Exponential distribution of defect discovery.

where t is elapsed time in hours (see Box 12.2 for a note on a Super Bulb burning for 113 years).

## BOX 12.2 SUPER BULB

The Centennial Light is the world’s longest-lasting light bulb. It is at 4550 East Avenue, Livermore, California, and maintained by the Livermore-Pleasanton Fire Department. The fire department says that the bulb is at least 113 years old and has been turned off only a handful of times. It is a 4-watt, hand-blown, carbon filament, common light bulb manufactured by the Shelby Electric Company in Shelby, Ohio, in the late 1890s. The Livermore-Pleasanton Fire Department plans to house and maintain the bulb for the rest of its life. (http://en.wikipedia.org/wiki/Livermore-Pleasanton_Fire_Department)

In software applications, there is a reversal of thinking: the CDF F(t) = 1 − e^{−λt} is known as the reliability function.

As time progresses, more defects are removed, and the product becomes more reliable, contrasting with the bulb. It is rather easy to calculate the fraction found

until a given date by dividing the defects found until now by the total number of estimated defects, as shown in Figure 12.4. The cumulative defects found represent software reliability.

There is a caveat.

> The rule says failure interval follows exponential distribution while defect events follow Poisson distribution. The essential truth is both follow the exponential law; one in continuous form, the other in discrete form.

In an ideal situation, we should use failure interval or time to fail in Equation 12.3 and plot a graph (that would resemble the same pattern in Figure 12.4). In real-life projects, the exact time of defect discovery is not always available. People accumulate information and submit reports on a weekly basis, occasionally on a daily basis, never on an hourly basis, unless of course if the bug tracking tool has a provision to capture defect events precisely in real time. Hence, we move away philosophically from reporting defect counts to reporting a metric called defects per week. Some people use defect density (defects per KLOC or defects per FP) instead of defect count. Either way, we have a density metric, which would still fit into a model represented in Figure 12.4.

![](img/2f042205c6c0e14747f198ed8f9c9f40_201_0.png)

Figure 12.4 Exponential distribution cumulative distribution function (CDF) of cumulative defects found.

## BOX 12.3 SIMÉON DENIS POISSON (1781–1840)

Siméon Denis Poisson was a French mathematician. His teachers Laplace and Lagrange quickly saw his mathematical talents. They became friends for life with their extremely able young student, and they gave him strong support in a variety of ways.

His paper on the theory of equations written in his third year was of such quality that Poisson could graduate without taking the final examination. He was employed as a tutor and appointed deputy professor 2 years later in 1802. In 1806, he become a full professor.

One of Poisson’s contributions was the development of equations to analyze random events, later dubbed the Poisson distribution. It describes the probability that a random event will occur in a time or space interval under the conditions that the probability of the event occurring is very small but the number of trials is very large; hence, the event actually occurs a few times.

The fame of this distribution is often attributed to the following story. Many soldiers in the Prussian Army died due to kicks from horses. To determine whether this was due to a random occurrence or the wrath of god, the Czar commissioned a Russian mathematician to determine the statistical significance of the events. It was found that the data fitted remarkably well to a Poisson distribution. There was an order in the data, and deaths were now statistically predictable.

Poisson never tried experimental designs. He said,

> Life is good for only two things, discovering mathematics and teaching mathematics.

## Poisson Distribution

The exponential law for discrete events can be expressed as follows:

```
P(x,λ) = e^{-λ} λ^x / x! (12.5)
```

where x takes discrete integer values 0, 1, 2, …, and λ is the mean value of x.

The Poisson distribution can be solved in Excel using the statistical function POISSON.DIST. For given values of x and λ, the function returns Poisson probability. While entering data by making cumulative = 0, we get probability distribution function, and by making cumulative = 1, we get cumulative probability.

Plots of Poisson probabilities of Equation 12.5 for λ = 1, 2, 3, and 4 are plotted in Figure 12.5.

As λ increases, the distribution shifts to the right and tends to turn symmetrical.

The corresponding cumulative probabilities are plotted in Figure 12.6. As λ increases, the curve attains an S shape.

The Poisson distribution was created by Siméon-Denis Poisson. In 1837, Poisson’s Sorbonne lectures on probability and decision theory were published. They

![](img/2f042205c6c0e14747f198ed8f9c9f40_203_0.png)

Figure 12.5 Poisson probability density function (PDF).

![](img/2f042205c6c0e14747f198ed8f9c9f40_203_1.png)

Figure 12.6 Poisson cumulative distribution function (CDF).

contained the Poisson distribution, which predicts the pattern in which random events of very low probability occur in the course of a very large number of trials. Poisson distribution is called the *law of rare events*.

A biographical note on the inventor of this distribution, Poisson, may be seen in Box 12.3. Poisson seems to have touched upon a universal law. Poisson distribution and its extensions are actively pursued by researchers in many domains, including software engineering.

## A Historic Poisson Analysis: Deaths of Prussian Cavalrymen

In the historic data analysis done by von Bortkiewicz in 1898, deaths of Prussian cavalrymen due to horse kicks were fitted to a Poisson distribution. We can look at the data made available in *Statistics: The Poisson Distribution* [2], where the mean value of death per corps is given as *p* = 0.5434. Substituting this value in Equation 12.5 and treating *x* as the number of deaths, we can construct a Poisson distribution as follows:

```
$$P(x,0.5434)=\frac{e^{-0.5434}\,0.5434^{x}}{x!}\tag{12.6}$$
```

where *x* is number of deaths in a single corps.

Figure 12.7 shows a plot of this Poisson distribution.

![](img/2f042205c6c0e14747f198ed8f9c9f40_204_0.png)

Figure 12.7 Poisson distribution of Prussian cavalrymen deaths.
