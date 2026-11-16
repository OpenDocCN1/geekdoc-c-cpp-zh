
![](img/d3c00252180686426c9e63ab889b535b_229_0.png)

- (a) Data samples lying approximately on the unit sphere in two groups.

![](img/d3c00252180686426c9e63ab889b535b_229_1.png)

- (b) Projection onto two principal components after a transformation to a four-dimensional space.

Figure 7.7: Principal Component Analysis on a manifold.

shifted images, which is the average of the outer products of the \(n^{th}\) column of \(\Phi(\mathbf{I} - \frac{1}{N}\mathbf{E})\) with its transpose. This can be written as

\[
\Sigma = \frac{1}{N} \sum_{n=1}^N \Phi(\mathbf{I} - \frac{1}{N}\mathbf{E})\mathbf{e}_n \mathbf{e}_n^T (\mathbf{I} - \frac{1}{N}\mathbf{E}) \Phi^T,
\]

where \(\mathbf{e}_n\) is the \(n^{th}\) standard unit basis vector, with all elements being equal to zero, apart from the \(n^{th}\) being one.

Now, \(\Phi(\mathbf{I} - \frac{1}{N}\mathbf{E})\) and its transpose are independent of \(n\) in the summation and can be taken outside the sum. Summing \(\mathbf{e}_n \mathbf{e}_n^T\) over all \(n = 1, \dots, N\) results in the identity matrix. Further, the matrix \(\mathbf{I} - \frac{1}{N}\mathbf{E}\) is *idempotent*, which means any power of it is the matrix itself, since \(\mathbf{E}^2 = N\mathbf{E}\) and

\[
(\mathbf{I} - \frac{1}{N}\mathbf{E})(\mathbf{I} - \frac{1}{N}\mathbf{E}) = \mathbf{I} - \frac{2}{N}\mathbf{E} + \frac{2}{N^2}\mathbf{E}^2 = \mathbf{I} - \frac{1}{N}\mathbf{E}.
\]

Therefore, the covariance matrix can be expressed as

\[
\Sigma = \frac{1}{N} \Phi(\mathbf{I} - \frac{1}{N}\mathbf{E}) \Phi^T.
\]

We seek the largest eigenvalues \(\lambda_k\) of \(\Sigma\) with corresponding eigenvectors \(\mathbf{w}_k, k = 1, \dots, K\). Using the above expression for \(\Sigma\), these vectors satisfy

\[
\Phi(\mathbf{I} - \frac{1}{N}\mathbf{E}) \Phi^T \mathbf{w}_k = N \lambda_k \mathbf{w}_k.
\]

Multiplying through with \((\mathbf{I} - \frac{1}{N}\mathbf{E}) \Phi^T\) from the left and using the idempotence of \(\mathbf{I} - \frac{1}{N}\mathbf{E}\), this becomes

\[
(\mathbf{I} - \frac{1}{N}\mathbf{E}) \Phi^T \Phi (\mathbf{I} - \frac{1}{N}\mathbf{E}) (\mathbf{I} - \frac{1}{N}\mathbf{E}) \Phi^T \mathbf{w}_k = N \lambda_k (\mathbf{I} - \frac{1}{N}\mathbf{E}) \Phi^T \mathbf{w}_k.
\]

![](img/d3c00252180686426c9e63ab889b535b_230_0.png)

![](img/d3c00252180686426c9e63ab889b535b_230_1.png)

![](img/d3c00252180686426c9e63ab889b535b_230_2.png)

![](img/d3c00252180686426c9e63ab889b535b_230_3.png)

Figure 7.8: Kernel Principal Component Analysis.

Hence the vector

\[
\tilde{\mathbf{w}}_k = (\mathbf{I} - \frac{1}{N}\mathbf{E})\mathbf{\Phi}^T \mathbf{w}_k \tag{7.14}
\]

is an eigenvector of the \(N \times N\), symmetric matrix \((\mathbf{I} - \frac{1}{N}\mathbf{E})\mathbf{\Phi}^T \mathbf{\Phi}(\mathbf{I} - \frac{1}{N}\mathbf{E})\) with eigenvalue \(\tilde{\lambda}_k = N \lambda_k\). Note that due to \(\mathbf{I} - \frac{1}{N}\mathbf{E}\) being idempotent, we have \((\mathbf{I} - \frac{1}{N}\mathbf{E})\mathbf{w}_k = \mathbf{w}_k\). Thus, the components of \(\tilde{\mathbf{w}}_k\) sum to zero.

The \((i,j)\) entry of \(\mathbf{\Phi}^T \mathbf{\Phi}\) is the inner product

\[
\phi(\mathbf{v}_i)^T \phi(\mathbf{v}_j) = k(\mathbf{v}_i, \mathbf{v}_j).
\]

\(\mathbf{K} = \mathbf{\Phi}^T \mathbf{\Phi}\) is known as the kernel matrix. Kernel Principal Component Analysis calculates the eigenvalues \(N \lambda_k\) and eigenvectors \(\tilde{\mathbf{w}}_k\) of \((\mathbf{I} - \frac{1}{N}\mathbf{E})\mathbf{K}(\mathbf{I} - \frac{1}{N}\mathbf{E})\).

Multiplying Equation (7.14) from the left with \(\mathbf{\Phi}/N\), gives

\[
\frac{1}{N}\mathbf{\Phi}\tilde{\mathbf{w}}_k = \frac{1}{N}\mathbf{\Phi}(\mathbf{I} - \frac{1}{N}\mathbf{E})\mathbf{\Phi}^T \mathbf{w}_k = \mathbf{\Sigma} \mathbf{w}_k = \lambda_k \mathbf{w}_k.
\]

Hence, \(\mathbf{w}_k\) is a linear combination of the images \(\phi(\mathbf{v}_1), \dots, \phi(\mathbf{v}_N)\), since

\[
\mathbf{w}_k = \frac{1}{N\lambda_k} \sum_{n=1}^N \hat{w}_{kn} \phi(\mathbf{v}_n),
\]

where $\hat{w}_{k,n}, n=1, \dots, N$, are the components of $\hat{\mathbf{w}}_k$. In practice, however, this calculation is never done, since we are only interested in expressing any data point $\mathbf{v}$ in the basis formed by the principal components, i.e. the value of the projections

\[
\mathbf{w}_k^T \phi(\mathbf{v})^T = \frac{1}{N\lambda_k} \hat{\mathbf{w}}_k^T \mathbf{\Phi}^T \phi(\mathbf{v}) = \frac{1}{N\lambda_k} \hat{\mathbf{w}}_k^T \begin{pmatrix} \phi(\mathbf{v})^T \phi(\mathbf{v}_1) \\ \vdots \\ \phi(\mathbf{v})^T \phi(\mathbf{v}_N) \end{pmatrix}
\]
\[
= \frac{1}{N\lambda_k} \hat{\mathbf{w}}_k^T \begin{pmatrix} k(\mathbf{v}, \mathbf{v}_1) \\ \vdots \\ k(\mathbf{v}, \mathbf{v}_N) \end{pmatrix}.
\]

It remains to specify the length of $\hat{\mathbf{w}}_k$. The principal components have length one. This translates into a condition on the length of $\hat{\mathbf{w}}_k$,

\[
1 = \mathbf{w}_k^T \mathbf{w}_k = \frac{1}{(N\lambda_k)^2} \hat{\mathbf{w}}_k^T \mathbf{\Phi}^T \mathbf{\Phi} \hat{\mathbf{w}}_k
\]
\[
= \frac{1}{(N\lambda_k)^2} \hat{\mathbf{w}}_k^T (\mathbf{I} - \frac{1}{N}\mathbf{E}) \mathbf{K} (\mathbf{I} - \frac{1}{N}\mathbf{E}) \hat{\mathbf{w}}_k = \frac{1}{N\lambda_k} \hat{\mathbf{w}}_k^T \hat{\mathbf{w}}_k,
\]

since $\hat{\mathbf{w}}_k = (\mathbf{I} - \frac{1}{N}\mathbf{E})\mathbf{w}_k$ is an eigenvector with eigenvalue $N\lambda_k$. Thus, $\hat{\mathbf{w}}_k$ has to have length $\sqrt{N\lambda_k}$.

The kernel function does not need to be defined via a mapping $\phi$ and an inner product in a higher dimensional space. Section 5.2 gives several examples of kernel functions. Figure 7.8 shows the results of kernel Principal Component Analysis applied to the data in Figure 7.7a for various choices of kernels. Visually the results are quite different, but what they have in common is that the two data sets are grouped towards the left or right. This means that they can be separated along one principal component.

![](img/d3c00252180686426c9e63ab889b535b_232_0.png)

Taylor & Francis

Taylor & Francis Group

http://taylorandfrancis.com

## Regression

Regression developed from interpolation and is introduced as building a model of the process generating the data where the building blocks are chosen. The first choice of building blocks are polynomials. Ordinary Least Squares are introduced as the simplest method arising from assumed normally distributed noise. The concepts of over- and under-fitting are explained using the degree of polynomials as a descriptor for the complexity of the model space. Bias and variance are two contributors to the expected error of the model. Cross-validation is a method to decide the goodness of the model. If the building blocks are too similar to each other, multicollinearity becomes a problem. Principal component regression ensures small correlation between building blocks, while Partial Least Squares emphasizes strong correlation with the data at the same time. Regularization controls model complexity. The chapter concludes with taking a probabilistic viewpoint in form of Bayesian regression leading to Gaussian processes.

In regression, we try to find the relationship between variables. Regression is related to curve fitting, interpolation, and data prediction. As an example, we consider colour vision. Spectral colours, as seen in Figure 8.1, are evoked by a single wavelength. Colours change continuously as the wavelength changes. A physical colour is a combination of pure spectral colours. Hence there are infinitely many possibilities.

![](img/d3c00252180686426c9e63ab889b535b_233_0.png)

Figure 8.1: Spectral colours.

Around 1854, James Clerk Maxwell [8] showed that all colours can be mixed by different combinations of the three primary colours, red, green and blue. He did so by using a colour-mixing top which can be seen in Figure 8.2 consisting of three coloured paper discs overlapping by different amounts. A smaller central disc contained a wedge of a colour sample. The brightness could be adjusted by the width of the wedge. When the top spun, the outer colours would mix and one could adjust how much each colour contributed until it matched the colour in the centre.

![](img/d3c00252180686426c9e63ab889b535b_234_0.png)

Figure 8.2: Maxwell's colour-mixing top.

Photo courtesy of Professor John Mollon, Cambridge University.

There is a biological explanation for this. The human eye has only three types of measuring devices to perceive colours – the cones. Figure 8.3 shows to which wavelengths different type of cones are sensitive. The blue peak is well separated from the red and green peaks. It is believed that the separation between red and green is evolutionarily fairly new and that the curves will move further apart with time. Colour blindness is in most cases due to one type of cone missing or malfunctioning. With three measurements, the human eye can distinguish ten million colours. This is an example of regression, and shows how powerful our brain is. From only three measurements our brain is able to infer millions of colours.

These are not just spectral colours, but also non-spectral ones. Magenta is an extraordinary colour. It is a mixture of the primary colours red and blue which lie far apart in the colour spectrum. It occurs in nature when the green component of white light is absorbed, since it is the complementary colour to green. In fact, magenta did not exist as a dye until 1859/60, when it was invented by François-Emmanuel Verguin (Lyon), Chambers Nicolson and George Maule (London). It is an aniline dye, and was named after the battle of Magenta. It caused a fashion craze with those who could afford it, showing off in magenta clothes some of which can be seen in the Victoria and Albert Museum in London, England.

Different animals and insects have different numbers of cone types. Refer to Table 8.1 for an overview.
