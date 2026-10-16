
The HPP can be described only by exponential law, an oversimplification though. Constant failure rate, a key assumption in HPP, is too ideal to be true even in the case of mechanical systems. A bulb, under HPP, will have the same reliability after burning through 400 hours or any time fixed by the analyst. Physically this is meaningless. Similarly, the physical meaning of a failure rate in a situation shown in Figure 12.2 begs explanation. No software ever operates at a constant failure rate, although the exponential representation produces such a parameter. It must be borne in mind that Figure 12.2 has been obtained by numerical curve fitting rather than by using physically reasonable reliability parameters such as failure rates or MTBF or MTTF.

The bathtub curve, in its entirety, is true for mechanical systems. In the case of software, failures are constrained to Region 1, which records reliability growth. Hence, software failure models are called *reliability growth models*. For both cases, we now need the help of NHPP modeling for a more accurate representation of real world failure patterns.

## Nonhomogeneous Poisson Process (NHPP)

Real-life software defect arrival is more complex than simple exponential curves; an example is available in Figure 12.12. It presents a typical defect arrival pattern during system testing. Approximately 140 defects are discovered over a time span of about three months. It is not a smooth exponential cumulative distribution. The curve is irregular; defects seem to be triggered at different rates in different periods. There seem to be short test cycles within the main testing process. The curve also has several linear climbs. These details mark a clear departure from the simple exponential, making a case for building NHPP.

![](img/2f042205c6c0e14747f198ed8f9c9f40_210_0.png)

Figure 12.12 Defect arrival pattern—empirical model.

The equation to an NHPP is given as follows:

$$
P(x, m(t)) = \frac{e^{-m(t)} m(t)^x}{x!}\quad(12.13)
$$

where $m(t)$ is the mean value function that takes the place of the traditional failure rate constant $\lambda$ in the HPP model presented in Equation 12.5.

It may be noted that Equation 12.13 is exactly Equation 12.5, except for a redefinition of the rate constant $\lambda$. An NHPP is completely defined by its mean value function $m(t)$. Building an NHPP model reduces to the identification of the right function for $m(t)$ and the derivation of the parameters of the function from failure data.

There are many options available to choose a function for $m(t)$. Researchers have used different functions to suit different situations. The list includes exponential, logarithms, Gaussians, Weibulls, and logistic functions. Even mixtures of functions have been used to deal with complex events.

It is now customary to think of NHPP with two equations. The bigger Poisson equation in Equation 12.13 defines the structure, and the mean value function in Equations 12.10–12.13 defines a central component. In fitting NHPP to data, we derive the coefficients of the mean value function $m(t)$ from data. There is no need to consult the Poisson equation for this purpose. The Poisson is in the background, as an abstraction of the model.

> *Think of NHPP, think of mean value function.*

An early application of the NHPP power law is by Duane [3], who in 1964 observed,

> When he plotted cumulative MTBF estimates versus the times of failure on log-log paper, the points tended to line up following a straight line. This was true for many different sets of reliability improvement data and many other engineers have seen similar results over the last three decades. This type of plot is called a Duane Plot and the slope beta of the best line through the points is called the reliability growth slope or Duane plot slope. A straight line on a Duane plot is equivalent to the NHPP Power Law Model.

The NHPP power law has been used as a model for “reliability improvement.”

### Mean value function MVF

a = 1, b = 0.07

![](img/2f042205c6c0e14747f198ed8f9c9f40_213_0.png)

Figure 12.13 Goel–Okumoto model.

> God does not care about our mathematical difficulties.
> He integrates empirically.
>
> — Albert Einstein

There are several references to the use of the Goel–Okumoto model, often called the GO model. A few are mentioned in the following section.

### Different Applications of Goel–Okumoto (GO) Model

The law of rare events is fully realised in the structure of the GO-NHPP model, as we have seen. The GO NHPP model has been extensively researched and used as a Software Reliability Growth Model (SRGM). A few attempts are listed below. The wide varieties of applications of the GO model explore the model features and identify the limits.

- 1. Nagar and Thankachan [6] have used the GO model to “decide the amount of more testing required and for the correct estimation of the remaining errors.” They call $b$ a roundness factor, similar to a shape factor that tends to zero when irregularity increases.

- 2. Wood [7] considers nine SRGMs and has included the GO model in his study. He draws special attention to the collection of time data, the argument in SRGMs. He also proposes a two-stage NHPP “if a significant amount of new code is added during the test period.”

- 3. In a survey of software reliability models, Pai [8] considers the GO model. He makes a salient observation regarding the GO model usage, “The model requires failure counts in the testing intervals and completion time for each test period for parameter estimation.”

In our opinion, this practice gives extra credibility to the mean value function and invests it with more decision making power. An exponential model that uses sums of the defects found in test intervals and the completion time of the test interval as the argument does not depend so much on Poisson abstraction.

- 4. Liu et al. [9] propose a generalized NHPP that uses a bell curve for fault detection rate. The bell curve handles variations due to fluctuations in debugging, learning, and fault removal efficiency. The results show that the proposed model fits failure data better than some selected NHPP models, including the GO model.

- 5. Anjum et al. [10] have evaluated 16 SRGMs proposed during the past 30 years using a set of 12 comparison criteria. They find the GO model in position 6 from the top. Surprisingly, they find the generalized Goel model in the 14th position.

The generalized Goel model does not use the simple exponential law for its mean value function but adds a third parameter to generate desired shape changes. A graph of the generalized Goel model is available in Chapter 21.

- 6. Mohd and Nazir [11] have studied different reliability models and find an interesting characteristic in the GO model.

It should be noted that here the number of faults to be detected is treated as a random variable whose observed value depends on the test and other environmental factors. This is a fundamental departure from the other models which treat the number of faults to be a fixed unknown constant.

- 7. Kim et al. [12] find that the GO model can be applied to safety-critical software, although it is generally known that software reliability growth models such as the Jelinski-Moranda model and the Goel–Okumoto non-homogeneous Poisson process (NHPP) model cannot be applied to safety-critical software due to a lack of software failure data.

Their analysis confirms the fear: the estimated total number of inherent software faults varies from 27.32 to 34.83 for the GO model as the software failure numbers change from 24 to 34. Results are sensitive to the number of failure data points.

- 8. Lin and Huang [13] find the Weibull model better than the GO model in a special application but choose to refer to the GO model as a benchmark.

- 9. Gokhale and Trivedi [14] propose an enhanced NHPP, called the mean value function, as a coverage function and use the log-logistic function instead of exponential to get better results than the GO model.

### BOX 12.5 RARE BASEBALL EVENTS

Huber and Glen [15] have studied three sets of rare baseball events—pitching a no-hit game, hitting for the cycle, and turning a triple play—which offer excellent examples of events whose occurrence may be modeled as Poisson processes. From 1901 to 2004, there have been 206 no-hitters, 225 cycles, and 511 triple plays. The associated mean values per year have been calculated as follows:

- No-hitter = 1.98.
- Cycle = 2.16.
- Triple plays = 4.91.

The above mean values characterize the respective Poisson distributions. The researchers have also calculated mean interarrival times as follows:

- No-hitter = 772 games.
- Cycle = 720 games.
- Triple play = 316 games.
