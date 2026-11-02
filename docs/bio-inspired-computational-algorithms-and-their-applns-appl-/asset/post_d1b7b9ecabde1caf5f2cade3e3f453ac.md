
Once that was chosen the series to work with, it will be estimated how many terms are necessary for the linear approximation of the series based on the autocorrelation function. In this work were calculated 30 values for the autocorrelation function and for selecting how many terms are required two cases were utilized. If the function is decreasing a value of 4 is taken, on the contrary a value equal to the value in which the first maximum of this function is observed it will be chosen (see Figure 3). With this procedure if the series presents stationarity and the period is smaller than 30 the models that are built here can represent appropriately such stationarity.

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_233_0.png)

Fig. 3. Possible autocorrelation function graphs.

With this information are built the limits for the coefficients intervals of the chosen series, for that are taken all the φi in [−1, 1] except the independent term δ which limits are calculated between zero and the average value of the series. The reason why these limits are established is obtained from the equations presented in (6). With all the previous information it is complete the proposal of the p number of terms required and that are the limits of its coefficients. From this information is solved the problem 1 applying the SAGA in the first two stages depicted in section 3.2 based on the following:

### Result 1.

If {y_t} is a difference series for {x_t} with a model

$y_t = h_0 + h_1 y_{t-1} + h_2 y_{t-2} + ... + h_k y_{t-k}$

then, for the difference series with terms $y_t = x_t - x_{t-1}$ must be

$x_t = h_0 + (1 + h_1) x_{t-1} + (h_2 - h_1) x_{t-2} + ... + (h_k - h_{k-1}) y_{t-k} - h_k y_{t-k-1}$  (7)

is a model for the series {x_t}.

- From this result two important consequences are obtained:
  - The model for the series |x_t| has one term more than the series |y_t|
  - If y_t has a coefficient value between −1.0 and 1.0, the coefficient of x_t may not be in this range.

Applying the result 1 as many times as necessary, it can be obtained a model for the original series, and to this model it is applied the stage three of section 3.2 to obtain a linear model for the TS. Note that if it is had a model AR for some series of differences, the model built for the original series has more terms than the series of differences, so if K terms are needed for the original series, then must be found models for the series of differences of less terms that K.

### 4.2.2 Second algorithm

The second algorithm only utilizes of the BJ methodology the estimation of how many terms are necessary in the linear approximation of the series of differences, which could be stationary, thus, from this is determined the numbers of terms that will be used in the original series.

From now on, are applied the stages presented in section 3.2, taking the limits of all the coefficients in [-1,1], but always working with the original series. There is not a result that justifies the use of these limits, and only it has been found a reference (Cortez et al., 2004) where it is used. On the other hand, is a fact that a high percentage of cases in the NN3 presented better results with this algorithm than with the first. As an example of this the second algorithm outperformed the first in 46 of the 111 examples of NN3-Complete.

## 5. NN3 results

The international competition NN3 Artificial Neural Network & Computational Intelligence Forecasting Competition 2007 aims at assessing the latest methodologies for the forecasting of TS. This competition is open to use methods based on Neural Networks, Fuzzy Logic, Genetic Algorithms and others in the area of artificial intelligence. The problems in question are presented in two groups called NN3-Complete (with 111 examples), and the purpose of the competition is to obtain the best models for each example of the two sets using the same methodology. The notation of this section is similar to that used in NN3.

To evaluate the performance of a model in some example s, it is estimated the forecasting F and it is measured the performance with the average of the indicator Symmetric Mean Absolute Percent Error SMAPE in all the values of the series. The SMAPE measures the absolute symmetric error in percentage between the real values of the original series Z and the forecasting F for all observations t of the test set of size n for each series s with SMAPE equal to:

$$\frac{1}{n} \sum_{t=1}^{n} \frac{|z_t - f_t|}{(z_t + f_t)/2} * 100 \tag{8}$$

and finally it is averaged over all examples in the same set of data. Other measures of forecasting accuracy of a model can be found in (Hyndman & Koehler, 2006).

This indicator can evaluate the performance of applying different methodologies on the same set of data and the methodology that produces the lowest value is considered the best. In the set NN3-Complete the best result was of 14.84% and applying the algorithms developed in this work was of 16.31%. In the NN3-Reduced the results were 13.07% and 15.00% respectively. However, it is possible to build linear models with the methodology presented in this work to improve these results because:

- Although the competition was intended to determine the best model for each example in this work was found an AR model with 4 terms for each example. It is expected that if it is divided the series in a training set and in other set of test it can be found models with higher forecasting capacity that improve the results obtained.
- ARMA models were not used that include the behavior of the residuals or the advancement of forecasting that substantially improve the results.

To build the NN3 competition models were conducted several activities. First it was worked the NN3-Reduced problems where, with the two algorithms developed, were realized 50 runs of every algorithm in each example looking for linear models with 4 terms. Table 1 presents the results of linear expressions and calculation of RSS.

After reviewing the behavior of the 50 solutions of these examples it was concluded that five runs were enough to obtain satisfactory results. For this reason only five runs were realized for the examples of the NN3-Complete using each algorithm and it was chosen the best of these. The results of the NN3-Complete examples are not presented.

| Problem | Linear Model | RSS |
|---|---|---|
| 101 | $F_t = 1269.3358 + 0.3467Z_{t-1} + 0.6978Z_{t-12} - 0.2921Z_{t-13}$ | 1713.55 |
| 102 | $F_t = 1.9887 + 0.9218Z_{t-1} + 0.9574Z_{t-12} + 0.8972Z_{t-14}$ | 5440.262 |
| 103 | $F_t = 1.9989 + 0.9218Z_{t-1} + 0.8124Z_{t-12} - 0.3734Z_{t-13}$ | 80019.738 |
| 104 | $F_t = 9.113 + 0.7252Z_{t-1} + 0.8316Z_{t-12} - 0.5592Z_{t-13}$ | 7321.538 |
| 105 | $F_t = 1.998 + 0.9099Z_{t-1} + 0.3104Z_{t-11} + 0.2225Z_{t-13}$ | 1513.964 |
| 106 | $F_t = 2821.954 + 0.2673Z_{t-2} - 0.1699Z_{t-7} + 0.3422Z_{t-12}$ | 4464.87 |
| 107 | $F_t = 1.9978 + 0.7937Z_{t-1} + 0.3152Z_{t-12} - 0.1125Z_{t-13}$ | 1387.011 |
| 108 | $F_t = 2000.5819 + 0.2885Z_{t-2} - 0.1456Z_{t-4} + 0.2379Z_{t-5}$ | 10417.433 |
| 109 | $F_t = 1.9988 + 0.9951Z_{t-1}$ | 2297.306 |
| 110 | $F_t = 1863.0699 + 0.2520Z_{t-1} - 0.1058Z_{t-5} + 0.2359Z_{t-11}$ | 18593.279 |
| 111 | $F_t = 474.1106 + 0.2420Z_{t-11} - 0.3319Z_{t-12} + 0.2688Z_{t-13}$ | 7248.281 |

Table 1. Linear models for the NN3-REDUCED.

### 5.1 NN3 graphs

In this section are showed some of the graphs of the series obtained with the best result of some heuristic algorithms here presented. The values correspondent to the last 18 points on the graph are the result of the forecasting obtained on having evaluated the expressions of the linear models that appear in Table 1.

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_235_0.png)

Fig. 4. Example 101.

## 6. ARMA models for time series

In this section the methodology already developed is applied to obtain AR components of the error series obtained by subtracting from the original series the values that are assigned by the AR model. With this is obtained a new model by adding these two components, thus it is obtained the equivalent in our methodology of the traditional ARMA models.
