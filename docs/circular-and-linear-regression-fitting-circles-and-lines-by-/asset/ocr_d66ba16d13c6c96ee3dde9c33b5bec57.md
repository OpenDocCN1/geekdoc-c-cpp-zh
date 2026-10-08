because the measurements may be imprecise (our pieces of iron may be con- tinuanted by other elements).

Similar problems commonly occur in economics (where, for instance, $x$ may be the price of a certain good and $y$ the demand, see Wald [187]) and in sociology. For a fascinating collection of other examples, including the studies of A-bomb survivors, see Chapter 1 in [28].

So how do we solve the iron density problem? For example, we can assume (or rather, pretend) that the volumes $x_i$'s are measured precisely and apply the classical regression of $y$ on $x$, i.e., determine $y = bx$ and set $\rho = b$. Alternatively, we can assume that our masses $y_i$'s are error-free and do the regression of $x$ on $y$, i.e., find $x = b'y$ and then set $\rho = 1/b'$.

This may sound like a good plan, but it gives us two different estimates, $\rho_1 = b$ and $\rho_2 = 1/b'$, which should make us at least suspicious. An objection was raised against this strategy as early as in 1901 by K. Pearson, see p. 559 in [144]: "we get one straight line or plane if we treat some one variable as independent, and a quite different one if we treat another variable as the independent variable." See Fig. 1.2.

![](bbox=[0.26, 0.42, 0.71, 0.66])

It was later determined that under natural statistical assumptions (to be de- scribed shortly) both estimates, $\rho_1$ and $\rho_2$, are inconsistent and may be heavily biased, see e.g., [8, 118, 142]; the consequences of this biasedness in econ- ometrics are discussed in Chapter 10 of [128]. In fact, $\rho_1$ systematically under- estimates the true density $\rho$, and $\rho_2$ systematically overestimates it.

Thus the new type of regression problem calls for nonclassical approaches. First we need to adopt an appropriate statistical model in which both $x_i$'s and $y_i$'s are subject to errors; it is called *errors-in-variables* (EIV) model${}^1$. It as- sumes that there are some "true" values $\tilde{x}_i$ and $\tilde{y}_i$, that are linked by the (un- known) functional relation $\tilde{y}_i = g(\tilde{x}_i)$, and the experimenters observe their per- fectly measured pairs $(x_i, y_i)$, where $x_i$ and $y_i$ are obtained by adding errors to $\tilde{x}_i$ and $\tilde{y}_i$.