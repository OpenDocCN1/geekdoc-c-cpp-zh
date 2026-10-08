```
$w^T = (w_1 \quad w_2 \quad w_3 \quad \dots \quad w_N) \quad (6.8)$
```

```
$R = \begin{pmatrix} \tilde{r}_1 \ \tilde{r}_2 \ \tilde{r}_3 \ \cdot \ \vdots \ \tilde{r}_N \end{pmatrix} \quad (6.9)$
```

Although $w^T$ and $R$ are vectors, they can also be thought of as $(n \times 1)$ or $(1 \times n)$ matrices. The *portfolio variance* in matrix form can thus be written as:

```
$$\sigma_p^2 = \sum_{i=1}^N \sum_{j=1}^N w_i w_j \sigma_{ij} = w^T \Sigma w \quad (6.10)$
```

Where $\Sigma$ is the *variance-covariance matrix* for the individual assets $i$ and $j$ given by:$4$

```
$$\Sigma = \begin{pmatrix} \sigma_1^2 & cov_{12} & cov_{13} & \cdot & cov_{1n} \ cov_{21} & \sigma_2^2 & cov_{23} & \cdot & \cdot \ cov_{31} & cov_{32} & \sigma_3^2 & \cdot & \cdot \ \cdot & \vdots & \vdots & \vdots & \cdot \ cov_{n1} & \cdot & \cdot & \cdot & \sigma_N^2 \end{pmatrix} \quad (6.11)$
```

Source 6.2 shows the PRet() and PVar() member functions and method implementations.

```
SOURCE 6.2: THE PRet() AND PVar() MEMBER FUNCTION AND METHOD IMPLEMENTATIONS

// Optimise.h
#pragma once;

#include "Matrix.h"
#include "Stats.h"
```