# 9.4.2 Hybrid Learning Algorithm

The hybrid learning algorithm of ANFIS proposed by Jang, Sun, and Mizutani is a combination of Steepest Descent and Least Squares Estimate Learning. Let the total set of parameters be S and let S1 denote the premise parameters and S2 denote the consequent parameters. The premise parameters are known as nonlinear parameters and the consequent parameters are known as linear parameters. The ANFIS uses a two pass learning algorithm: forward pass and backward pass. In forward pass the premise parameters are not modified and the consequent parameters are computed using the Least Squares Estimate Learning algorithm. In backward pass, the consequent parameters are not modified and the premise parameters are computed using the gradient descent algorithm. Based on these two learning algorithms, ANFIS adapts the parameters in the adaptive network. From the architecture, it is clear that the overall output of the ANFIS can be represented as a linear combination of the consequent parameters as

$$f = \frac{w_1}{w_1+w_2}f_1 + \frac{w_2}{w_1+w_2}f_2 = \bar{w}_1f_1 + \bar{w}_2f_2$$

In forward pass the signals move in forward direction till layer 4 and the consequent parameters are computed while in the backward pass, the error rates are propagated backward and the premise parameters are updated by the gradient descent method.

# Forward Pass: Least Squares Estimate Method

The least squares estimate method estimates the unknown values of the parameters, $\alpha_0, \alpha_1$ from the regression function, $f(\vec{x}; \vec{\alpha})$ by finding numerical values for the parameters that minimize the sum of the squared deviations between the observed responses and the functional portion of the model. The mathematical expression to obtain the parameter estimates is

$$Q = \sum_{i=1}^{n} [y_i - f(\vec{x}; \vec{\alpha})]^2$$

Here $\alpha_0, \alpha_1, \ldots$ are the variables to be optimized and $x_1, x_2, \ldots$ are the predictor variable values which are considered as coefficients. For linear models, the least squares minimization is usually done analytically using calculus. For nonlinear models, on the other hand, the minimization must almost always be done using iterative numerical algorithms.

The steps to compute the consequent parameters by maintaining the premise parameters fixed during the forward pass are: