example, we have assumed a quadratic cost model with respect to the input problem (or data) size for the computation effort of the host processor and the accelerator for any of the tasks involved. In contrast, the communication costs for the transfer of data to and from the accelerator follow a linear cost model.

This figure depicts two breakeven points beyond which, and despite the communication overhead of the data transfer, it becomes profitable to use the accelerator for offloading computation. Clearly, the relative position of these breakpoints depends on the relative values of the fixed overhead costs, \(\delta\), and the \(\alpha\) and \(\beta\) coefficients for the various model components outlined in Eqs. (7.1) and (7.2).

The performance speedup for either of these two execution models is thus given by the expression in Eq. (7.3), which can asymptotically reach the raw performance benefit of an accelerator when the overhead of communication and synchronization reaches zero.

```
SpeedUp = \frac{T_{comp}^{host}}{T_{acc}^{comp}} = \frac{T_{acc}^{host}}{T_{acc}^{exec}}
```

Note that while it may be profitable to offload the computation to an accelerator, the problem size might become too large to fit the accelerator's internal storage. In this scenario, developers need to restructure computations by resorting to different partitioning strategies so that the data for each task considered for offloading can fit in the accelerator's storage.

The communication cost between the host and the accelerator is modeled using a simple affine function as illustrated in FIG. 7.3, where n corresponds to the problem size (Eq. 7.4), which is proportional to the amount of data transferred. Note that other application parameters can be considered when modeling communication cost. For instance, for image processing, the amount of data transferred might depend not only on the image size, but also on the color depth used and filter size.

```
T_{comm}^{host2accel} = \beta n + \delta
```

Commonly, developers resort to analytical modeling based on empirical data to model the performance of specific tasks on their accelerators. Often, this approach uses regression models to fit the observed data to an assumed analytical model

![](bbox=[0.21, 0.7, 0.85, 0.88])

# FIG. 7.3 Communication cost model between the host and the accelerator.