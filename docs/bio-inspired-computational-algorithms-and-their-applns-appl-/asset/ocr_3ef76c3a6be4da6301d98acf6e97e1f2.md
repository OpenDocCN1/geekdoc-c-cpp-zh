of the form:

$$Z_t = \delta + \phi_1 Z_{t-1} + \phi_2 Z_{t-2} + \ldots + \phi_p Z_{t-p} + a_t \qquad (1)$$

Where $Z_t$ is the observable variable in question, δ and $φ_i$ are the parameters to be determined and the variable $a_t$ represents a random variable of noise called *residual*. The expression (1) means that to predict what will happen at the time $t$ are required the $p$ values previous to $t$, these values are called *delays* or *lags*.

In the classic theory of linear models is set the restriction that $a_t$ represents a white noise, but in this work it was not included this boundary, which will allow to find AR expressions for the residuals with which it will be possible to increase the accuracy of the models.

The interest in this type of models is originated in the fact that they represent the most important information about the behavior of the series eliminating the noise that may appear. It should also be added that, for these models, it is important that in the expression (1) only appears a number of terms set in advance. This will allow finding models for a TS, controlling the accuracy of the approximation of the same series according to the number of terms utilized.

**Problem 1:** If {$Z_t$} is the original TS and {$F_t$} is the forecasting obtained of the form

$$F_t = \delta + \phi_1 Z_{t-1} + \phi_2 Z_{t-2} + \ldots + \phi_p Z_{t-p} \qquad (2)$$

with $t > p$.

It is necessary to find the values for δ and $φ_i$ that minimize the function:

$$\sqrt{\sum_{i=p}^{N}(Z_i-F_i)^2} \qquad (3)$$

This function will be called *Root of the Sum of Squares* (RSS). It is necessary to add that for rapidity in calculation it is preferable to use the square of this function obtaining the same results.

In this initial setting out the construction of the model is presented as if a linear interpolation problem was solved, and given that the values for δ and $φ_i$ will not be arbitrary but will be looked at certain intervals are necessary methods to solve the Problem 1 working in addition with bounded variables.

The RSS function can have multiple local optima, and to solve this problem it was developed an original version of SAGA algorithms, which allows to solve real nonlinear optimization problems and with bounded variables. The selection of a self Adaptive version was carried out by the fact that it is wanted to automate as much as possible the process of building these models.

# ### 3. Self adaptive genetic algorithms

The SAGA algorithms were developed by Thomas Back (Back, 1992a, 1992b) and have the characteristic that they alone look for the best parameters for their operation. In them, the parameters that will be self Adaptive are encoded in the representation of the individual, for which they are altered by the actions of the genetic operators. With this, the best