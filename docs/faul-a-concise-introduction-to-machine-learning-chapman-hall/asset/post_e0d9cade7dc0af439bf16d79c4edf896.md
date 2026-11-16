
![](img/d3c00252180686426c9e63ab889b535b_305_0.png)

![](img/d3c00252180686426c9e63ab889b535b_305_1.png)

![](img/d3c00252180686426c9e63ab889b535b_305_2.png)

Figure 9.4: Autoencoder with two hidden neurons applied to two digits.

columns and the bias, the columns can be seen as the basis functions of the model space from which the data is generated. The bias is a shift in the data space, necessary to reconstruct all training data. If the data is *mean centred*, such a shift is unnecessary and the bias is zero. The application of the transfer function ensures that the output lies again in the same range as the input.

```
E(\mathbf{w}) = \frac{1}{N} \sum_{n=1}^N ||\mathbf{x}_n - \psi(\phi(\mathbf{x}_n))||^2 + \beta \Omega_\lambda + \lambda \Omega_w,
```

where the *sparsity regularizer* \(\Omega_\lambda\) and the \(L_2\) *regularizer* \(\Omega_w\) are penalty terms to ensure sparsity and control the growth of the weights. After some trials, \(\beta\) was set to 4, while \(\lambda = 0.004\). \(\Omega_\lambda\) also depends on the *sparsity proportion* \(p\) which was chosen to be 0.15.

While it is desirable in neural networks to choose the number of hidden neurons smaller than the dimension of the input data, the assumption is that it needs to be chosen large enough so that the distinguishing features in the data are captured. However, what does large enough mean? To understand the inner workings of an algorithm it is helpful to look at smaller problems. In our first experiment, we therefore only consider the digits zero and one. Since only two classes need to be distinguished, we set the number of hidden neurons M to two. Figure 9.4 shows the results.

Firstly, in Figure 9.4a it can be seen that the activations of the training data are separated. It is a two dimensional space, since there are two hidden neurons. This space becomes close to the space spanned by the first two principal components of the training data, because there the data is most easily separated and this is the goal of the encoder. The transfer function emphasizes this separation, which can be seen in Figure 9.4b.

Secondly, the latent space is spanned by the two bases seen in Figures 9.4c and 9.4d. The numeric values at each pixel location is indicated by the colour bar. The first basis resembles a slanted one written over a zero, while the second is similar to a straight one over a zero. The bias resembles a zero. Different runs can arrive at different configurations of the bases and bias, since the neural network is initialized randomly.

Since the autoencoder strives to reconstruct the input, the basis functions it chooses resemble digits or over-laid digits to the human eye, while principal component analysis focuses on the largest eigenvalues and the principal components do not resemble digits and neither do the resulting reconstructions.

In Figure 9.5 another digit was included, but the set-up was kept the same. The reconstructions in Figure 9.5g are discernible, which cannot be said about Figure 7.3b where the reconstruction is done using principal component analysis. One might imagine a two in Figure 9.5c, a one in Figure 9.5d and a zero as the bias in Figure 9.5e. The separations in Figure 9.5b are not clear for digits zero and two, while they are still well separated in Figure 9.5a. This is mostly due to the position of the zero on the horizontal axis, since for zero the logistic sigmoid function evaluates to 0.5 making both classes equally likely. However, samples of one and two are mostly present there and they are separated along the vertical axis. The separation can be improved by shifting the activations right such that the zero point of the horizontal axis lies where the digits zero and two separate.

Alternatively, the number of hidden neurons can be increased to three. The results are shown in Figure 9.6. The reconstructions are good and the basis functions resemble elements of digits. In Figure 9.6b, the latent variables of the digit zero are packed at the (0, 0, 0) corner of the unit cube, while those of the digit one lie along the edges connecting the (0, 1, 0), (0, 1, 1), (0, 0, 1) and (1, 0, 1) corners. Hence they are separated.

To examine this further, we consider all ten digits and increase M to ten. To visualize the separation, Figures 9.7a to 9.7j display the stacked histograms (with one hundred bins) of the activations for each of the digits along the ten

![](img/d3c00252180686426c9e63ab889b535b_307_0.png)

![](img/d3c00252180686426c9e63ab889b535b_307_1.png)

![](img/d3c00252180686426c9e63ab889b535b_307_2.png)

![](img/d3c00252180686426c9e63ab889b535b_307_3.png)

![](img/d3c00252180686426c9e63ab889b535b_307_4.png)

![](img/d3c00252180686426c9e63ab889b535b_307_5.png)

![](img/d3c00252180686426c9e63ab889b535b_307_6.png)

Figure 9.5: Autoencoder with two hidden neurons applied to three digits.

dimensions of the model space. While the set of digits as a whole seems to be centred around a mean in each of the dimensions, some digits move away from this centre. For example, in Figure 9.7a digits two, three and eight lie further to the right in this dimension, while in Figure 9.7c it is digits two and six. In Figure 9.7f the digits to the right are mostly one. Applying the logistic sigmoid maps activations to the right close to one, while those to the left are mapped close to zero. Figures 9.7k and 9.7l show the proportions of digits which get mapped close to zero and one in each of the ten dimensions corresponding to the hidden neurons. While nearly all digits are present close to zero, near one some digits are dominant. This means these neurons “fire” for particular digits.

The following table indicates for which digits an individual neuron “fires”.

![](img/d3c00252180686426c9e63ab889b535b_308_0.png)

![](img/d3c00252180686426c9e63ab889b535b_308_1.png)

![](img/d3c00252180686426c9e63ab889b535b_308_2.png)

![](img/d3c00252180686426c9e63ab889b535b_308_3.png)

![](img/d3c00252180686426c9e63ab889b535b_308_4.png)

![](img/d3c00252180686426c9e63ab889b535b_308_5.png)

![](img/d3c00252180686426c9e63ab889b535b_308_6.png)

![](img/d3c00252180686426c9e63ab889b535b_308_7.png)

Figure 9.6: Autoencoder with three hidden neurons applied to three digits.

| Neuron \ Digit | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | | | | x | x | | | | | x |
| 2 | x | | | x | | x | | | | x |
| 3 | | | x | | | x | x | | | |
| 4 | | x | | | | | | | x | |
| 5 | x | | | | | | | x | | |
| 6 | x | | | | | x | | | x | |
| 7 | x | | | | x | | x | x | | |
| 8 | | | | | x | | | | | x |
| 9 | | x | x | | | | | | | |
| 10 | | | | | | | x | | | x |

The table can also be read in the other direction telling us the input from which neurons is necessary to construct a particular digit. For example, digit four is mostly constructed from input from the eighth neuron, digit seven mostly from input from the tenth neuron, while digit nine is a mixture of the eighth and tenth neuron. We can now compare this to basis functions corresponding to each neuron given in Figure 9.8. In particular for these examples, the basis functions are shown in Figures 9.8h and 9.8k and indeed digits four, seven and nine can be seen in these. Similarly, digit one can be seen in Figures 9.8d and 9.8i. The other basis functions are not so clearly linked to a particular digit, but it has to be kept in mind that the requirement is that a digit can be reconstructed by a linear combination of the basis functions, not that a single basis function corresponds to a digit.

The bias is displayed in Figure 9.8k. It can be interpreted as the summary of what all samples have in common. Since the digits are centred in the image, the bias is this centre.

![](img/d3c00252180686426c9e63ab889b535b_310_0.png)

Figure 9.8: Basis functions and bias of an autoencoder with ten hidden neurons.

## 9.5 Relationship to Other Techniques

In this section, we examine how neural networks relate to some of the techniques we have seen before. We already touched on this in Section 5.5 with regards to classification where a neural network describes different regions as sets of points lying on different sides of a set of lines.

In Chapter 8, the assumption is that all samples are generated by an underlying process of the form

```
t = Dc + ε,
```

where ε is additive Gaussian noise with zero mean and variance σ², the D × M matrix D is the design matrix, c is the vector of coefficients, which depends on both D and t.

Recall that the prediction of the ordinary least squares solution, where D is chosen beforehand, is

```
Dc = D(DᵀD)⁻¹Dᵀt.
```
