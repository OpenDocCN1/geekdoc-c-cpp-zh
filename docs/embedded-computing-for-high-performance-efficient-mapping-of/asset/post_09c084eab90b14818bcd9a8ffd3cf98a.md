
## 7.3 WORKLOAD DISTRIBUTION

As discussed in the previous section, it is important to understand both the nature of the application and the features of the underlying platform to derive an efficient mapping between them. This is particularly critical, as platforms are becoming more heterogeneous, allowing various types of hardware accelerators to assist in speeding up computations running on the host processor. Hence, we need to understand in what conditions should we offload computations to these devices and what factors affect overall performance. This is the subject of this section.

When computations are offloaded to an accelerator, there is a cost overhead that is absent when the entire computation is carried out by the host processor, namely:

- 1. Data transfer to and from the host to the accelerator’s storage or address space.
- 2. Synchronization to initiate and terminate the computation by the accelerator.

Given the current system-level organization of most computing systems, data needs to be physically copied between storage devices often via a bus. This has been traditionally the major source of overhead when dealing with accelerators. Furthermore, the host needs to actively engage in polling to observe the termination of the computations on the accelerators, thus synchronization also incurs an overhead, which is typically proportional to the number of tasks to be offloaded to the accelerators.

Hence, in cases where the host and the accelerators execute in sequence (i.e., the host blocks until the accelerator terminates execution), it is only profitable to offload kernels to accelerators if they exhibit a very high operational intensity (the ratio of computation to data used—see previous section). Furthermore, for offloading to be profitable, the accelerator methods to execute the computation considerably faster than the host to offset the aforementioned overheads.

To measure the benefits of offloading, we need to first select one or more metrics of performance, such as execution time and energy consumption. Typically, developers compare the execution time of a kernel running on the host for each relevant problem of size $n$, i.e., $T_{host}(n)$, against the time it takes to perform the same computation using an accelerator, say $T_{comp}(n)$.

Note that the execution time (or another metric such as energy) can depend non-linearly on the problem size. For linear algebra operations, such as matrix-matrix multiplications, simple algorithms can be described as having a computational complexity that increases with the cube of the input matrix dimension size $n$ (the *number of columns or rows for squared matrices*), i.e., the computation time on the host can be modeled as $T_{host}^{comp}(n) = \alpha_0 n^3 + \beta_0$ for a square matrix with dimension size $n$. For other computations, the complexity might be quadratic as in $T_{host}^{comp}(n) = \alpha_0 n^2 + \beta_0$.

When the same computation is executed on an accelerator, while the complexity may not change, the values of the coefficients $\alpha_0$ and $\beta_0$ may be different due to other sources of overhead, namely, data transfer cost.

To assess the benefits and hence to aid in deciding whether to offload computations, programmers can build execution models for the host and for the accelerator, capturing both execution time and any additional overheads for a given problem size. As an example, consider the following two execution models:

- 1. **Blocking coprocessor execution model.** In this execution model, the host processor is responsible for transferring data to and from the accelerator storage space (or simply copying it to a selected region of its own address space) and by initiating and observing the completion of a task's execution by the accelerator. While the host processor can carry on other unrelated computations as the accelerator is computing, it is often the responsibility of the host to check when the accelerator has terminated its execution. The following analytical expression (Eq. 7.1) captures the execution time of this model:

\( T_{comp}^{acc}(n) = T_{comm}^{HostAcc}(n) + T_{acc}^{exec}(n) + T_{comm}^{AccHost}(n) \) (7.1)

Clearly, for an accelerator operating under this execution model to be effective, the data transfer time needs to be either reduced to a minimum or hidden as is the case of the nonblocking model as explained next.

- 2. **Nonblocking coprocessor execution model.** In this execution model, and after triggering the execution of the first task on the accelerator, the host can initiate a second task (if it is independent from the previous one) by transferring the data for the second task to the accelerator while the accelerator is carrying out the computation corresponding to the first task.

The analytical expression in (Eq. 7.2) captures the execution time of this model for a “steady state” operation mode, where the communication for the first and the last task is ignored, and where the max function is used to capture the fact that if the computation takes longer than the communication, the accelerator will delay the communication or if the data transfer from the host to the accelerator takes longer than the computation of the previous task, the accelerator will stall.

\( T_{comp}^{acc}(n) = \max(T_{comm}^{HostAcc}(n) + T_{acc}^{exec}(n), T_{acc}^{exec}(n)) \) (7.2)

This model is only possible if there are no dependences between the two computations and there is enough memory space to save the data for the computation scheduled to be executed next. This execution model reaches its maximum benefit when the communication between the host and the accelerator can be entirely masked by the computation, and excluding the initial and final computations, the execution time is simply dictated by the maximum duration of the communication or the accelerator execution.

Given the execution models described earlier, and under the assumption developers can accurately model the various sources of overhead, it is possible to determine when it is profitable to use an accelerator to execute a set of computational tasks based on the problem (workload) size $n$. For simplicity, we assume the overall computation is composed of a series of tasks with the same data sizes.

Using the execution models earlier, we can depict in a chart when it becomes profitable to offload the computation's execution to an accelerator with the two execution models. Fig. 7.2 illustrates when it is profitable to offload the computation to an accelerator in both execution models described earlier.

![](img/55beb9162c0073b3a3d7b44f1d5873e8_240_0.png)

![](img/55beb9162c0073b3a3d7b44f1d5873e8_240_1.png)

![](img/55beb9162c0073b3a3d7b44f1d5873e8_240_2.png)

![](img/55beb9162c0073b3a3d7b44f1d5873e8_240_3.png)

FIG. 7.2 Illustration of computation time with and without accelerator using blocking and nonblocking execution models. This depiction assumes a quadratic computational effort with respect to the input problem size and the linear cost for data transfer to and from the accelerator (shown on the right-hand side of the figure).

In this illustrative example, we have assumed a quadratic cost model with respect to the input problem (or data) size for the computation effort of the host processor and the accelerator for any of the tasks involved. In contrast, the communication costs for the transfer of data to and from the accelerator follow a linear cost model.

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

![](img/55beb9162c0073b3a3d7b44f1d5873e8_241_0.png)

### FIG. 7.3 Communication cost model between the host and the accelerator.
