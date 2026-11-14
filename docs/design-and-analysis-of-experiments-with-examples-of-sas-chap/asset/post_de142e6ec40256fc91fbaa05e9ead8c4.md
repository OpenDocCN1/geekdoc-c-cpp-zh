
- (a) Why do you think it might be appropriate to use a crossover design for this study? What is the alternative?
- (b) Modify the SAS code in Section 9.4.1 to create Williams' crossover design for four treatments to use for this experiment.
- (c) Decide how many subjects to include in your study and create a randomized list assigning each subject to one of the four sequence groups.
- (d) Write the model you would use to analyze this data.
- (e) Make a data input form and show how you would code the indicators for the subject, period, treatment and carryover effects.

- 4. Consider the data from the repeated measures design shown in Table 9.10.
  - (a) Use proc glm to compute the sphericity test and determine if the Huynh-Feldt condition holds.
  - (b) Use proc glm to make the Greenhouse-Geisser and Huynh-Feldt adjusted F-tests of the subplot effects.
  - (c) Do you find more terms significant using the adjusted F-tests than were found using the growth curve analysis shown in the text? If so, explain why.

- 5. Consider the results of the repeated measurements experiment from Usage note: Stat-40 (1997) from the University of Texas at Austin. In this experiment the purpose was to determine how diet and exercise affect the pulse of subjects. Eighteen subjects were randomly assigned to one of three exercises (1=aerobic stair climbing, 2=racquetball, 3=weight training) and one of two diets (1=include meat, 2=vegetarian). After a training period where all subjects followed their assigned exercise and diet routine, their pulse was measured three successive times (once after a warm-up, again after jogging and finally after running). The results are shown in the table on the next page.
  - (a) Make a plot of the average trend in pulse over the three repeat measures for each of the six combinations of diet and exercise.
  - (b) Do a normal split-plot analysis of the data treating diet and exercise as whole-plot factors and the repeated measurements as a subplot factor.
  - (c) Use the sphericity test to determine if the normal analysis is justified.
  - (d) Make the Huynh-Feldt and Greenhouse-Geisser adjusted F-tests for the subplot effects. Are the results different than the unadjusted tests?
  - (e) Do a conservative growth-curve analysis of the linear contrast in pulse measurements over time. Do the results of this analysis confirm what you found in (b) and (d)? If not, why?

| Exercise | Diet | Pulse 1 | Pulse 2 | Pulse 3 |
|---|---|---|---|---|
| 1 | 1 | 112 | 166 | 215 |
| 1 | 1 | 111 | 166 | 225 |
| 1 | 1 | 89 | 132 | 189 |
| 1 | 2 | 95 | 134 | 186 |
| 1 | 2 | 66 | 109 | 150 |
| 1 | 2 | 69 | 119 | 177 |
| 2 | 1 | 125 | 177 | 241 |
| 2 | 1 | 85 | 117 | 186 |
| 2 | 1 | 97 | 137 | 185 |
| 2 | 2 | 93 | 151 | 217 |
| 2 | 2 | 77 | 122 | 178 |
| 2 | 2 | 78 | 119 | 173 |
| 3 | 1 | 81 | 134 | 205 |
| 3 | 1 | 88 | 133 | 180 |
| 3 | 1 | 88 | 157 | 224 |
| 3 | 2 | 58 | 99 | 131 |
| 3 | 2 | 85 | 132 | 186 |
| 3 | 2 | 78 | 110 | 164 |

## Response Surface Designs

### 10.1 Introduction

In a response surface experiment, the independent variables or factors can be varied over a continuous range. The goal is to determine the factor settings that produce a maximum or minimum response or to map the relationship between the response and the factor settings over this contiguous factor space. As a practical matter, if we want to know a lot about the relationship between the factors and the response, it will require many experiments. For that reason, response surface designs are rarely conducted with more than six factors.

Response surface experiments are normally used at the last stage of experimentation. The important factors have already been determined in earlier experiments, and at this stage of experimentation the purpose is to describe in detail the relationship between the factors and the response. It is usually known or assumed that a simple linear model, even with interactions, is not good enough to represent that relationship. In order to locate maxima or minima in the response as a function of the factor settings, at least three levels of each factor should be utilized.

Response surface methods generally refer to a complete package of statistical design and analysis tools that are used for the following three steps.

- 1. Design and collection of data to fit an equation to approximate the relationship between the factors and response.
- 2. Regression analysis to fit a model to describe the data.
- 3. Examination of the fitted relationship through graphical and numerical techniques.

Response surface methods have found considerable use in industry especially in chemical processes where the reaction yield or cost of production can be optimized as a function of the settings of controllable process factors. Since their origin these designs have also found successful applications in food science, engineering, biology, psychology, textiles, education and many other areas.

### 10.2 Fundamentals of Response Surface Methodology

#### 10.2.1 Empirical Quadratic Model

In response surface methods, the relationship between the response (y) and the factor settings (x's) is assumed to be a nonlinear equation given by y = f(x) + ε. For two factors or independent variables we could write this equation

```
y = f(x_1, x_2) + \epsilon \tag{10.1}
```

where \( f \) is a nonlinear function and \( \epsilon \) is the random effect of experimental error. When \( f \) is unknown it can be approximated near the point \( (x_{10}, x_{20}) \) using the two-term Taylor series approximation, i.e.,

```
\( f(x_1, x_2) \approx f(x_{10}, x_{20}) + (x_1 - x_{10}) \frac{\partial f(x_1, x_2)}{\partial x_1} \bigg|_{x_1=x_{10}, x_2=x_{20}} + (x_2 - x_{20}) \frac{\partial f(x_1, x_2)}{\partial x_2} \bigg|_{x_1=x_{10}, x_2=x_{20}} + \frac{(x_1 - x_{10})^2}{2} \frac{\partial^2 f(x_1, x_2)}{\partial x_1^2} \bigg|_{x_1=x_{10}, x_2=x_{20}} + \frac{(x_2 - x_{20})^2}{2} \frac{\partial^2 f(x_1, x_2)}{\partial x_2^2} \bigg|_{x_1=x_{10}, x_2=x_{20}} + \frac{(x_1 - x_{10})(x_2 - x_{20})}{2} \frac{\partial^2 f(x_1, x_2)}{\partial x_1 \partial x_2} \bigg|_{x_1=x_{10}, x_2=x_{20}}, \tag{10.2} \)
```

which leads to a general quadratic equation of the form

```
y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \beta_{11} x_1^2 + \beta_{22} x_2^2 + \beta_{12} x_1 x_2 + \epsilon \tag{10.3}
```

where \( \beta_1 = \frac{\partial f(x_1, x_2)}{\partial x_1} |_{x_1=x_{10}, x_2=x_{20}} \), etc. If the region of interest is of moderate size, this general quadratic equation will provide a good approximation to \( f \) and can be used for interpolation within this region. The general quadratic equation is quite flexible and with appropriate coefficients it can describe a wide variety of surfaces such as hilltops, valleys, rising or falling ridges, or saddle points as shown with contour plots in Figure 10.1.

With \( k \) factors or independent variables the general quadratic equation can be written in the form

```
y = \beta_0 + \sum_{i=1}^k \beta_i x_i + \sum_{i=1}^k \beta_{ii} x_i^2 + \sum \sum_{i<j} \beta_{ij} x_i x_j + \epsilon, \tag{10.4}
```

and unless the function \( f \) is known, this equation forms the basis of response surface methods. Response surface designs were created to provide data to approximate this equation, and mathematical tools were created to explore the fitted surface represented by this equation.

Figure 10.1 Surfaces That Can Be Described by General Quadratic Equation

![](img/878b651cdbe9da3d6d22e64d64b8a54f_397_0.png)

#### 10.2.2 Design Considerations

The first requirement of a response surface design is that it should provide data that will allow estimation of the coefficients in model (10.4). This model has 1+2k+k(k-1)/2 coefficients, thus any response surface design must have at least three levels for each factor (to allow estimation of quadratic terms) and at least 1+2k+k(k-1)/2 total runs. 3k factorial designs have three levels for every factor. However, Box and Wilson (1951) showed that they were less satisfactory as a response surface design than an alternative design they called the central composite design. The central composite will be the first standard response surface design we will discuss in the next section.

Normally the factors or independent variables (x) in the general quadratic Equation (10.4) are coded and scaled as shown in Sections 3.7.2 and 3.7.3 so that the experimental region is a hyper-cube or hyper-sphere with radius R in the coded space. This general quadratic model can be written in matrix terms as

```
y = xb + x'Bx + ε (10.5)
```

where x' = (1, x1, x2, ..., xk), b' = (β0, β1, ..., βk) and the symmetric matrix
