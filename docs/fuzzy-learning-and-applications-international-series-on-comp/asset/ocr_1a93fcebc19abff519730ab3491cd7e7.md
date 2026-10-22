equation (11.52) may be written in the form:

```
y0 = D(x0)^T P. (11.63)
```

Hence parameters P may be estimated by means of the least squares method. To eliminate the matrix inverse we use the recurrent method. For k-th step, e.g., (k-th element from the learning set) we get [18]:

```
P̂(k) = P̂(k - 1) + G(k - 1)D[x0(k)] { y0(k) - D[x0(k)]^T P̂(k - 1) }, (11.64)
```

```
G(k) = G(k - 1) - G(k - 1)D[x0(k)] × { D[x0(k)]^T G(k - 1)D[x0(k)] + 1 }^-1 D[x0(k)]^T G(k - 1). (11.65)
```

To initialize the computations we take:

```
{ P̂(0) = 0, G(0) = βI, } (11.66)
```

where I is an identity matrix, β is a large positive constant (e.g., 10^6).

Finally in each iteration parameters p^(k) are estimated on the basis of equations (11.64) and (11.65), whereas the other parameters are by means of a gradient method (11.54), (11.55), (11.56), (11.59).

Another problem is the estimation of the number m of if-then rules and initial values of membership functions for the premise part. This task is solved by means of preliminary clustering of the input part of training data using fuzzy c-means method [1], [23]. This method assigns each input vector x0(k) ; k = 1,2,...,N to clusters represented by prototypes vi; i = 1,...,K measured by grade of membership uik ∈ [0,1]. The K × n dimensional partition matrix fulfills the following assumptions:

```
{ ∀k Σ_{i=1}^K uik = 1, ∀i Σ_{k=1}^N uik ∈ (0,N). } (11.67)
```

The c-means method minimizes the scalar index for parameter r > 1:

```
Jr = Σ_{k=1}^N Σ_{i=1}^K (uik)^r ||x0(k) - vi||^2. (11.68)
```

Defining D_{ik}^2 = ||x0(k) - vi||^2, where ||·|| is a vector norm (the most frequent Euclidean norm), we get an iterative method of commutative modification of