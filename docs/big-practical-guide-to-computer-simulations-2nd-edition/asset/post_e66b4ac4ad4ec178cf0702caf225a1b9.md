
where the sum ∑i here and in the following runs from 0 to n − 1. Since we will be interested in the spread of the cloud, i.e., in the variance of the data, it is sufficient to consider the center of the cloud shifted to the origin. Therefore, we normalize the data points by the mean:

$$\bar{x}^{(i)} = \tilde{x}^{(i)} - \overline{\tilde{x}}.\tag{8.84}$$

An example of such a sample for d = 3 dimensions, shifted to the origin, is shown in Fig. 8.41.

![](img/0dfb82b7d27bdfebb8b65cb33de3626a_356_0.png)

Fig. 8.41 A sample of random three-dimensional vectors (x1, x2, x3)T (“+” symbols). The “x” symbols show the same sample projected on the x1, x2 plane. The two arrows indicate the most important principal components, i.e., the two eigenvectors of the covariance matrix corresponding to the two largest eigenvalues. The length of the vectors is the square roots of the corresponding eigenvalues.

The basic idea is to find directions u (with length |u| = 1) in the cloud which characterize the data sample most, i.e., along which the variance of the data is largest. These are the principal components. For the sample data, the two most important directions are indicated in Fig. 8.41 by arrows.

Now we will see step by step that obtaining the principal components can be actually performed via calculating eigenvectors and eigenvalues of the (empirical) covariance matrix of the sample of data points. For this purpose we project each normalized data point on the direction x, i.e., calculate the scalar products q^(i) ≡ x · x^(i). Thus, for the sample variance in direction x we obtain using Eq. (8.55):

Var_x{(x^(i))} = 1/n Σ_i (q^(i) - q̄)^2 , q̄=0 = 1/n Σ_i (q^(i))^2 = 1/n Σ_i (x · x^(i))^2 ,

where the average q̄ = 1/n Σ_i q^(i) vanishes because the data points have been normalized by their mean. Using the transpose ...^T a scalar product can be written as a · b = a^T b. When additionally using the symmetry of the scalar product a · b = b · a we can rewrite the above expression as

Var_x{(x^(i))} = 1/n Σ_i x^T x^(i) (x^(i))^T x . (8.85)

The expression 1/n Σ_i x^(i) (x^(i))^T denotes a d × d matrix which is called the (sample) covariance matrix C, which has the entries

C_kl ≡ 1/n Σ_i x_k^(i) x_l^(i) = 1/n Σ_i (x_k^(i) - x̄_k)(x_l^(i) - x̄_l) = 1/n Σ_i x_k^(i) x_l^(i) - x̄_k x̄_l . (8.86)

The covariance matrix is real, symmetric and positive semi-definite.17 i.e., it exhibits only non-negative eigenvalues λ_z (z = 1, …, d) and corresponding normalized eigenvectors e_z, i.e.,

C e_z = λ_z e_z  (λ_z ≥ 0) . (8.87)

Without loss of generality, we can assume that the eigenvalues are ordered in descending order λ1 > λ2 > … > λd and that the eigenvectors form an orthonormal (e_z · e_z' = δ_z,z') basis of the d-dimensional vector space.18 This means, any vector can be represented as linear combination of the eigenvectors. Thus, we can write x = Σ_z r_z e_z, where here and in the following sums Σ_z run from 1 to d, and r_z ≡ x · e_z. This we can insert into Eq. (8.85), resulting in

17 Any matrix of the form A A^T is semi-definite. 18 In case of degeneracy, i.e., if some eigenvalues appear multiple times, one can turn the set of eigenvectors into an orthonormal basis.

Var_{\underline{r}}{(x^{(i)})} = \underline{r}^T C \underline{r} = \left(\sum_z r_z e_z\right)^T C \left(\sum_{z'} r_{z'} e_{z'}\right)
\stackrel{(8.87)}{=} \left(\sum_z r_z e_z\right)^T \left(\sum_{z'} r_{z'} \lambda_z e_{z'}\right)
= \sum_z r_z^2 \lambda_z . \tag{8.88}

where for the last equality, we have used the orthonormality of the basis of eigenvectors. As mentioned in the beginning, we are interested in the direction which maximizes the variance of the projection of the data sample onto the \underline{r} direction, hence the maximum of (8.88). Due to the normalization of \underline{r} we have 1 = \underline{r}^2 = (\sum_z r_z e_z)^2 = \sum_z r_z^2. Since the eigenvalues are sorted in descending order, we obtain the maximum for Var_{\underline{r}}{(x^{(i)})} simply by setting r_1 = 1 and r_z = 0 for z = 2, ..., d, thus \underline{r} = e_1. The direction of the maximum spread of the data, i.e., the first principal component, is simply the direction of the eigenvector corresponding to the largest eigenvalue of the (sample) covariance matrix, and the variance in that direction is the largest eigenvalue itself.

Thus, it is straightforward to see that the direction of the second largest spread of the data (orthogonal to the direction of the largest spread), i.e., the second principal component, is the eigenvector corresponding to eigenvalue \lambda_2 and so on. Finally, the total spread (variance) of the data is simply the sum \lambda = \sum_z \lambda_z of all eigenvalues and the amount \lambda_z / \lambda denotes the relative amount of the spread corresponding to the zth eigenvector, i.e., corresponding to the zth most important principal component. Thus, using the eigenvalues one can somehow estimate how many really important independent degrees of freedom the data exhibits. For example, if in a sample of d = 10 dimensional data points, the first three eigenvalues sum up to 99% of the total variance \lambda of the sample, then in fact the data can be represented by three more or less independent variables. The dependencies inherent in the variables are described by the eigenvectors, which are often, unfortunately, hard to interpret.

The C function `principal_components()` calculates the principal components of a data sample. Here we again use some data types and functions from the GNU scientific library,

|  |
|---|
| GET SOURCE CODE |
| DIR: randomness |
| FILE(S): princ.comp.c |

in particular for the calculation of the eigenvalues and eigenvectors, which keeps the code compact. Thus, we use the GSL data types gsl_vector and gsl_matrix, see page 239 in Sec. 7.3.

The function receives a matrix data which contains the data points, {z^(i)}, each column of the matrix contains one data point. To return the eigenvalues, a vector eval is used. The corresponding eigenvectors are returned in the matrix evec, again one vector per column.

```c
void principal_components(gsl_vector *eval, gsl_matrix *evec,
    gsl_matrix *data)
{
    int t,d1, d2;                     /* loop counters */
    int dim;      /* number of components of data point vectors */
    int num_points;   /* number of data points */
    gsl_matrix *cov;  /* covariance matrix */
    gsl_vector *avg;  /* averages */
    gsl_eigen_symmv_workspace *w;  /* memory for eigenvalues etc */
}
```

Locally, we need a vector avg to hold the averages of the different components of the data points, and a matrix cov which stores the covariance matrix. These are allocated next, using the dimension d which is read off from the number of rows of data and stored in variable dim. The number n of data points is stored in variable num_points:

```c
num_points = data->size2;          /* initialize */
dim = data->size1;
avg = gsl_vector_alloc(dim);
cov = gsl_matrix_alloc(dim, dim);
```

Next, the averages are calculated. Here, the following two GSL functions are used: gsl_vector_set(), which sets an entry in the vector (taking the vector, the index of the entry and the value as arguments) and gsl_vector_get(), which returns the value of an entry (taking the vector and the index of the entry as arguments). The GSL function gsl_vector_scale() (line 21) multiplies every entry of a given vector with some number.

```c
for(di=0; di<dim; di++)             /* calculate averages */
{
    gsl_vector_set(avg, di, 0);
    for(t=0; t<num_points; t++)
        gsl_vector_set(avg, di, gsl_vector_get(avg, di)
            + gsl_matrix_get(data, di, t);
}
```

```c
gsl_vector_scale(avg, 1.0/ num_points);
```

Using these averages, the covariance matrix can be calculated according to Eq. (8.86). Similar to the corresponding vector functions, the GSL matrix access functions gsl_matrix_get() and gsl_matrix_set() are used, where in both cases a row (2nd argument) and a column index (3rd argument) have to be supplied.

```c
for(d1=0; d1<dim; d1++)          /* calculate covariance matrix */
  for(d2=d1; d2<dim; d2++)
  {
    gsl_matrix_set(cov, d1, d2,
                   -gsl_vector_get(avg, d1)*gsl_vector_get(avg, d2));
    for(t=0; t<num_points; t++)
      gsl_matrix_set(cov, d1, d2, gsl_matrix_get(cov, d1, d2)+
                     gsl_matrix_get(data, d1, t)
                     *gsl_matrix_get(data, d2, t)/num_points);
    gsl_matrix_set(cov, d2, d1, gsl_matrix_get(cov, d1, d2));
  }
```

The actual calculation of the eigenvalues and eigenvectors is now very simple using the GSL build-in functions. First, one has to provide some “work space” w (line 33) and then the actual calculation is performed and the results are stored in the eigenvalue vector eval and in the matrix evec of eigenvectors:

```c
w = gsl_eigen_symmv_alloc(dim); /* calculate eigenvectors/values */
gsl_eigen_symmv(cov, eval, evec, w);
```

Finally, the eigenvalues and the corresponding eigenvectors are sorted in descending eigenvalue order. For brevity, a simple neighbor exchange algorithm is used here. Since the dimension d is typically small, there is no benefit in using a more complicated algorithm which pays off only asymptotically. Finally, all locally used memory is freed.

```c
for(t=0; t<dim; t++) /* order eigenvalues (and corresp. vectors) */
  for(d1=0; d1<dim-1; d1++)
    if(gsl_vector_get(eval, d1) < gsl_vector_get(eval, d1+1))
    {
      gsl_matrix_swap_columns(evec, d1, d1+1);
      gsl_vector_swap_elements(eval, d1, d1+1);
    }

gsl_eigen_symmv_free(w);
```
