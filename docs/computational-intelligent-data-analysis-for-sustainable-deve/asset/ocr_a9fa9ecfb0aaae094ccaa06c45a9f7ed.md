A variety of methods are developed by Rogers et al. [8] to evaluate the accuracy of the predicted wind speed distribution. One method measures the accuracy in terms of ratios between true and actual parameters of the Weibull distribution: that is, true shape versus estimated shape and true scale versus estimated scale. To completely capture any possible inaccuracy in the predicted distribution, we measure a symmetric Kullback-Leibler (KL) distance. It is important to note that this measure is different from the mean-squared error or mean-absolute error, which measure the accuracy in terms of difference between each predicted value and the true observation. Methods that minimize these errors would not necessarily accurately express how close the approximation is to the true distribution. We now proceed to describe the set of statistical approaches we introduce for deployment within the MCP framework.

# ## 10.3 METHODOLOGY FOR WIND SPEED ESTIMATION

Notationally, we refer to a training point as l ∈ {1...L} and a point for which we have to make a prediction as k ∈ {1...K}. We drop the notation for time after having time-synchronized all the measurements across locations. We also drop the subscript for directional bin. From this point onward, when we refer to a model, it is the model for a particular bin j. Then, f_Z(z) refers to a probability density function of the variable (or set of variables) z. F_Z(z) refers to a cumulative distribution function for the variable z such that

$$F_Z(z=\alpha)=\int_{-\infty}^{\alpha} f_Z(z)\,dz$$

for a continuous density function.

Our methodology for MCP has four steps:

+   - **Step 1:** To start, we build a multivariate distribution with the probability density function f_{X,Y}(x,y), where x = {x_1,...,x_m} are the wind speeds at the historical sites and y is the wind speed at the site. To do this, we employ likelihood parameter estimation. The model building process is similar for all the bins, and only the data need to be changed.
+   - **Step 2:** Given the joint distribution from Step 1, we predict the probability density of y that corresponds to a given test sample x_k = {x_1,...,x_m} by estimating the conditional density f_Y(y|x_k). The conditional can be estimated by