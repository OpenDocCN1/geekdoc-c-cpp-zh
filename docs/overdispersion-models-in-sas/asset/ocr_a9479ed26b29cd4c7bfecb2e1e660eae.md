# 6.7 Hurdle Models

In this section we discuss Hurdle models, which are widely used to model extra zeros in the data. We include this discussion because of two important connections between the Random-clumped count models (RCM) and the Hurdle models. First, the Hurdle models can be thought of as clumping a random number of responses into a pre-selected category, namely zero, whereas in RCM the responses to be clumped are selected randomly. Second, the probability functions of the Hurdle and RCM models can be written as finite mixtures. We will also include a discussion of the relationships between zero-inflated distributions and Hurdle models after the illustrative example given below.

Consider the data in Table 6.4, which corresponds to daily milk consumption (number of glasses) of n=1,900 subjects. The original data were taken from the 1980 WAVE II of the National Survey of Personal Health Practices and Concerns were used by Mullahy (1986) to illustrate the testing of some modified count models. The data contained several explanatory variables such as age in years, years of completed schooling, family income, gender, etc. For simplicity and for illustrative purposes, we will restrict ourselves to models without covariates. We refer to Cameron and Trivedi (1998, Chapter 4) for a discussion on the Zero-inflated, and several other count regression models.

Note that 40% of the subjects in the survey indicated that they did not consume any milk. Certainly, there seems to be an excess of zeros, and it is very likely that these data might exhibit overdispersion. The other aspect of this data is that the model reporting consumption of milk from two different sources, namely those who do not drink milk at all, and those who drank milk but not during the time the survey was conducted. The data from the two sources are expected to follow different probability laws. Since the source of each individual zero-response is unknown, the observation may be modeled as a mixture of the two candidate distributions. The class models known as Hurdle models are created to explain such data.

Table 6.4: Daily Milk Consumption of n=1,900 Subjects

| Milk Consumption (in glasses) | Frequency Distribution |
|---|---|
| 0 | 767 |
| 1 | 557 |
| 2 | 333 |
| 3 | 142 |
| 4 | 62 |
| 5 | 23 |
| 6 | 16 |

A Hurdle model is interpreted as a two-part model. As pointed out by Mullahy (1986, p. 345), “the idea under the hurdle formulations is that a binomial probability model governs the binary outcome of whether a count variable has a zero or a positive realization.” He indicated that if the realization is positive, “the ‘hurdle’ is crossed, and the conditional distribution of the positives is governed by a truncated-at-zero count model.” Towards defining a Hurdle model for a random variable Y on the set of non-negative integers, consider independent random variables Y and Y+, each taking values 0,1,2,..., and let