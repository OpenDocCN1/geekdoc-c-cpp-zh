![](bbox=[0.25, 0.08, 0.8, 0.58])

# FIGURE 7.7 General blind deconvolution algorithm.

an iterative algorithm with a preselected structure (state-space or transfer function) with random or flat initialization. Using this assumed structure, a new image estimate is then obtained. A tuning parameter is then adjusted based on the error between this estimate and the actual image. Because nothing is known about the true image as well, some statistical assumptions are needed to decide on the correction. Usually, some form of covariance matrix is used to adjust the underlying model, and then the iterative procedure is continued until a suitable convergence is reached. The general algorithm is shown in Figure 7.7.

As discussed toward the end of Section 7.3, the H2 norm-based solution has certain statistical limitations, and H∞ can be a better approach.