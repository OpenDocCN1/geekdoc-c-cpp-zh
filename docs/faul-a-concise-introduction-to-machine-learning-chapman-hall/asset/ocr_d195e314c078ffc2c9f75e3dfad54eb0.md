However, even if the inverse exists, the inversion might be ill-conditioned leading to large numerical errors. Numerical analysis provides many methods to solve equation (8.2) safely; see example [12].

We now have a model of the data specified by D and c. For x1, ..., xN the predicted values f = (f1, ..., fN)^T are given by

f = Dc = D(D^T D)^{-1} D^T t.

Geometrically, this is the projection of t onto the space spanned by the columns of D. If t already lies in that space, then f = t. In this case, the regressors are perfectly suited to predict the data. For the minimal value of c the error sum of squares takes the value

\sum_{n=1}^N r_n^2 = (t - D(D^T D)^{-1} D^T t)^T (t - D(D^T D)^{-1} D^T t) = t^T t - t^T D(D^T D)^{-1} D^T t = t^T (t - Dc).

It is the inner product between t and the error the model makes when predicting the data.

The regression problem can be viewed as finding an approximate solution in a finite dimensional space spanned by the basis functions, which is in some sense closest to the true solution in a possibly infinite dimensional space. A projection gives the closest solution with respect to the Euclidean norm ||.||, also known as the L2 norm.

# 8.5 Over- and Under-fitting

Figure 8.5 shows polynomial reconstructions of various degrees using data generated from the simple line y = x - 0.5 with added noise. The noise is modeled as a mixture of two probabilities, in order to generate outliers. The MATLAB code in Listing 8.1 gives details regarding how the data was generated.

The technique employed to fit the polynomials was ordinary least squares. The training data are marked by ◦. A small training set of size 10 was deliberately chosen to illustrate various effects. Also 90 test data were generated and are marked by +. One can see that some reconstructions are preferable over others.

Under-fitting occurs if there are not enough explanatory variables to explain the data. This can be seen in Figures 8.5a, and 8.5b, with the polynomial of degree 0. Note that the horizontal line is put at the mean of the training data, which is close to 0, since this is the mean of the true solution. Since the data comes from a linear degree polynomial, a polynomial of degree at least 1 is necessary to describe it. If this is not the case, the predictors fail to capture the complexity of the underlying process. The solution is to amend the dictionary of basis functions.