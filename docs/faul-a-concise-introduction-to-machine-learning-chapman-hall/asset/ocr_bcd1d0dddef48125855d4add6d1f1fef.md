![](bbox=[0.33, 0.1, 0.62, 0.33])

Note that the final equality in (2.22) does not involve \(\mu\), since \(\mu\) is a latent variable, but does involve \(N\) and \(m\), which specify \(\mathcal{D}\). Graphically, the information from the parameters \(\alpha\) and \(\beta\) and the data \(\mathcal{D}\) are combined in the node \(\mu\) to inform node \(x\).

The graph for the categorical case is very similar, except now we have a parameter vector \(\alpha\), \(\mu\) is vector valued and \(\mathbf{x}_1, \dots, \mathbf{x}_N\) and \(\mathbf{x}\) are 1-of-\(K\) representations:

![](bbox=[0.33, 0.49, 0.62, 0.7])

The other main difference is that the underlying prior and posterior distributions are no longer beta distributions, but Dirichlet distributions.

Following the Bayesian paradigm, \(\alpha, \beta\), and \(\alpha\) would not be parameters to be chosen, but would also be treated as random variables with their own prior distributions, called *hyper-priors* as discussed in [16]. This will grow the graphs. Complex inter-dependencies between various random variables and parameters can be visualized graphically. For a good introductory text consult [24].