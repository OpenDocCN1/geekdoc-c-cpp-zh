
## BOX 13.1 ORIGINS OF A SOCIAL LAW

Normal distribution has cast its influence in almost every field of life and research. It has gained the status of a social law.

French-born British mathematician Abraham de Moivre (1667–1754) published *A Doctrine of Chance: A Method of Calculating the Probabilities of Events in Play* in 1718, wherein he addressed the gambling problem. The third edition appeared in 1756; it contained the approximation to the binomial distribution by the normal distribution.

> de Moivre actually had written the equation down in 1708; obtained it as a limit of coins tossing or binomial distribution. We think of a coin being tossed ‘n’ times, and note the proportion of k heads. After many k-fold trials, we obtain a graph showing the number of occasions on which we get 0 heads, 1 head, 2 heads, … n heads. The curve will peak around the probability of getting heads with the coin. As the number of tosses ‘n’ grows without a bound, a normal distribution results [1].

de Moivre’s concern was with games of chance, and his discovery showed the power of sampling to determine patterns in a population by examining only a few members. He spent the last part of his life by solving problems of chance for gamblers as the resident statistician of Slaughter’s Coffee House in London.

In 1809, German mathematician and astronomer Johann Carl Friedrich Gauss (1777–1855) showed that errors of measurement made in astronomical observations followed a symmetric distribution called *normal distribution*. Gauss was also the first to develop the utility of the normal distribution curve, which had been discovered earlier by de Moivre. This distribution is now often called *Gaussian*.

> The curve was developed by observational astronomers who used the ideas of normal distribution to verify the accuracy of measurements. They measured a distance many times and graphed the results. If most measurements clustered around the mean, then the average of the results could be considered reliable. Outliers or deviant measurements could be discounted as inaccurate [2].

The normal distribution has been studied under various names for nearly 300 years. To the historically inclined, it is Laplace’s second law, Gaussian law, or Laplace–Gaussian curve. The names law of deviation and error curve could make more sense to experimenters. Pearson, Fisher, and Galton have called it the normal curve, the name greatly favored by statisticians.

Today, in statistics books, we tend to call this the normal distribution. In the world of science, the favored name is Gaussian distribution.

the distribution. There is no separate shape parameter because the shape is fixed: it is a bell shape.

```
F(x,μ,σ) = 1/√(2πσ) e^(-(x-μ)²/(2σ²))  (13.2)
```

where μ is the mean (location parameter), and σ is the standard deviation (scale parameter).

Mean and standard deviation are part of descriptive statistics, discussed in Chapter 1. For any data set, we can estimate these two parameters. The equation is a natural sequel.

![](img/2f042205c6c0e14747f198ed8f9c9f40_221_0.png)

Figure 13.1 Standard normal curve.

The statistical properties of this distribution are as follows:

- Mean = μ
- Mode = μ
- Median = μ
- Kurtosis = 3
- Relative kurtosis = 0
- Skew = 0
- Variance = σ²
- Standard deviation = σ
- Range = −∞ to +∞

The mean code productivity in LOC per person-day and its standard deviation can be easily calculated from data and the corresponding normal distribution graph can be plotted.

In Figure 13.2, the assumed normal distribution of productivity is plotted for four different standard deviations. We have to assume normal distribution because productivity data would be seen as nonnormal had we plotted a histogram. However, we proceed with normal approximation. If dispersion decreases, it is a good sign; it indicates that the process becomes better. Figure 13.2 shows that as the standard deviation decreases, the height of the curve increases while its width decreases.

Real-world process improvement consists of reduction in variation and a simultaneous favorable shift in the mean. Figure 13.3 shows the bell curves for productivity improvement.

![](img/2f042205c6c0e14747f198ed8f9c9f40_222_0.png)

Figure 13.2 Gaussian probability density function (PDF) of productivity.

![](img/2f042205c6c0e14747f198ed8f9c9f40_223_0.png)

Figure 13.3 Gaussian model for productivity improvement.

The best performance is where the mean is 49 and the standard deviation 2. This gets closer to the oft spoken about rule of thumb of 50 LOC per person-day. The curves are still hypothetical, at best approximate. The bell curves in Figure 13.3 portray a story of improvement captured from a Gaussian lens.

## First-Order Approximation of Variation

> If that enabled us to predict the succeeding situation with the same approximation, that is all we require, and we should say that the phenomenon had been predicted, that it is governed by the laws.
> 
> Henri Poincare

Building a Gaussian is rather easy, from just two parameters, mean and standard deviation. These two can be obtained by expert judgment as well if data were not accessible. If we can guess optimistic and pessimistic values, we can “estimate” the Gaussian mean and standard deviation. The difference between the maximum and the minimum values is the estimated range. The rule of thumb we use to find standard deviation is given as follows:

```
Standard deviation = Range / 6  (13.3)
```

![](img/2f042205c6c0e14747f198ed8f9c9f40_224_0.png)

Figure 13.4 Gaussian distribution of effort variance.

The mean is recalled from the central tendency of the process. The ability of the Gaussian distribution to connect easily with approximate data makes it a “social law.”

> The Gaussian distribution allows us to see the two sides of truth: tendency and dispersion and facilitates fair judgment.

For example, from remembered mean value of effort variance = 5% and range = 30%, we can construct the Gaussian distribution shown in Figure 13.4. The central tendency, pictorially seen, reveals the problem. If planning and estimation practices were perfect, the central tendency would be zero. Nonzero tendency is a remark on project management.

## BOX 13.2 IS THE BELL CURVE FAIR?

The power of the bell curve is linked to the central limit theorem (CLT): sample means tend to be normally distributed as sample size N tends to be large. French mathematician Pierre-Simon Laplace rescued the CLT from the nearly forgotten work of Abraham de Moivre and published it in his monumental work Théorie Analytique des Probabilités. In 1901, Russian mathematician Aleksandr Lyapunov defined it in general terms and proved precisely how it worked mathematically [3].

Sir Francis Galton described the CLT as follows [4]:

> I know of scarcely anything so apt to impress the imagination as the wonderful form of cosmic order expressed by the “Law of Frequency of Error.” Whenever a large sample of chaotic elements are taken in hand and marshaled in the order of their magnitude, an unsuspected and most beautiful form of regularity proves to have been latent all along.

The actual term central limit theorem was first used by George Pólya in 1920 in the title of a paper. Pólya referred to the theorem as central because of its importance in probability theory [5].

According to Le Cam, the French school of probability interprets the word central in the sense that “it describes the behaviour of the centre of the distribution as opposed to its tails” [6].

Between 1870 and 1913, Markov, Chebyshev, and Lyapunov contributed to CLT. During 1920 to 1937, Lindeberg, Feller, and Lévy perfected the CLT [7].

CLT sets the context for a bell curve paradigm. The science of measurements presents another truth. Whatever we measure, we make repetitions to make measurements credible, and we measure the bell curve of the measured parameter. The limit or peak of the bell curve is the truth. The tails denote errors. Criticism of the bell curve as a grading curve (by some educationalists) is ill founded. The bell curve represents data and cannot be made responsible for hypothesis.

To sum it up, the bell curve represents truth better than isolated data.

## Estimation Error

Variance metrics is a double-edged sword. On the one side, it measures how well a plan is executed; on the other side, it measures how well a project is estimated. If applied to estimation, this metric can be renamed as the percentage of estimation error.

When processes mature, estimation errors tend to be the curve shown in Figure 13.5. Estimation errors are measurement errors; they resemble the astronomical measurement errors used by Gauss when he discovered a path breaking application of normal distribution. This is true in the case of size estimation, schedule estimation, and effort estimation and even defect count estimation; errors in all these are Gaussian.
