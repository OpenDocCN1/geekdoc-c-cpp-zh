# 32 ■ Cloud Computing and Digital Media

derived from M/G/1 queuing system [30]. The response time of the transmission time is formulated as

```
$$\hat{\mathbf{A}}_{i=1}\mathbf{1}_{D_i}^2 = \hat{\mathbf{A}}_{i=1}\mathbf{1}_{D_i}$$\n$\hat{\mathbf{T}}^{	ext{tra}(t)}_{\text{FCFS}} = \frac{\hat{\mathbf{A}}_{i=1}(\mathbf{B}^t\mathbf{y}^t - \mathbf{B}^t\hat{\mathbf{A}}_{i=1}\mathbf{1}_{D_i})}{i=1} + 1^t\mathbf{B}^t$
```

To ensure stable queue, $\hat{\mathbf{A}}_{i=1}\mathbf{1}_{D_i} < B^t$ is required.
Based on the above derivations, we can get the total service response time in the FCFS service case formulated as:

```
$$\hat{\mathbf{T}}^{	ext{tot}(t)}_{\text{FCFS}} = \frac{\hat{\mathbf{T}}^{	ext{sch}(t)}{\text{FCFS}} + \hat{\mathbf{T}}^{	ext{com}(t)}{\text{FCFS}} + \hat{\mathbf{T}}^{	ext{tra}(t)}{\text{FCFS}}}{1}$$\n= \frac{1/S^t}{1-1/S^t} + \frac{1/\hat{F}_i/C_t}{\hat{\mathbf{A}}_{i=1}(1-1/\hat{F}_i/C_t)}$$\n(2.2)
```

```
$$\hat{\mathbf{A}}_{i=1}\mathbf{1}_{D_i}^2 = \hat{\mathbf{A}}_{i=1}\mathbf{1}_{D_i}$$\n$\fracfrac{\mathbf{B}^t\mathbf{y}^t - \mathbf{B}^t\hat{\mathbf{A}}_{i=1}\mathbf{1}_{D_i})}{i=1} + 1^t\mathbf{B}^t$
```

Moreover, the mean service time for class-service is formulated as

```
$$\hat{\mathbf{T}}^{	ext{tot}(t)}_{\text{FCFS}} = \hat{\mathbf{T}}^{	ext{sch}(t)}{\text{FCFS}} + \hat{\mathbf{T}}^{	ext{com}(t)}{\text{FCFS}} + \hat{\mathbf{T}}^{	ext{tra}(t)}{\text{FCFS}} .$\quad(2.3)
```

The total resource cost for the multi-class service can be formulated as

```
$$\hat{\mathbf{Z}}^{	ext{tot}(t)}_{\text{FCFS}} = \frac{\hat{\mathbf{B}}}{\hat{E}}\hat{\mathbf{A}}s^t + \hat{\mathbf{B}}\hat{\mathbf{C}}C_t + \hat{\mathbf{G}}b^t - \mathbf{G}$$\quad(2.4)
```

+   1. Service response time minimization problem. Since there are different types of multimedia applications, such as video conference, cloud attendance, and 3D rendering, multimedia service providers should supply different types of multimedia services to users simultaneously. However, it is challenging to provide various multimedia services with a minimal total response time under a certain budget constraint. Therefore, we formulate the service response time minimization problem, which can be stated as follows: to minimize the total service response time in the FCFS service case by jointly optimizing the allocated scheduling resource at the master server, the computation resource at each computing