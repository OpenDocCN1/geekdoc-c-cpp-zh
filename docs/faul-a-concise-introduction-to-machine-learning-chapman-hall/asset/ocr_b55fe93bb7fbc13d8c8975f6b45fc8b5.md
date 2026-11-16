To find the extremum, we set this to zero and solve for \(\alpha_1\):

```
\exp(2\alpha_1) = \frac{N_C}{N - N_C}
\alpha_1 = \frac{1}{2} \log \frac{N_C}{N - N_C}.
```

Thus \(\alpha_1\) is half the logarithm of the ratio of the number of correctly classified samples over the number of misclassified samples. If \(N_C = N/2\), then \(\alpha_1 = 0\), meaning so that we have no confidence in the classification, since it is equal to random guessing. Note that \(N_C\) cannot be less than \(N/2\), since the weak classifiers need to be better than random guessing, i.e. they need to classify at least more than \(N/2\) samples correctly. The larger the \(N_C\), the higher the confidence.

In the \(m^{th}\) iteration we generate \(\mathcal{C}_m\) as \(\mathcal{C}_{m-1} + \alpha_m k_m\). The total error is

```
E(\mathcal{C}_m) = \sum_{i=1}^N \exp(-c_i \mathcal{C}_{m-1}(\mathbf{v}_i) - c_i \alpha_m k_m(\mathbf{v}_i))
= \sum_{i=1}^N \exp(-c_i \mathcal{C}_{m-1}(\mathbf{v}_i)) \exp(-c_i \alpha_m k_m(\mathbf{v}_i))
= \exp(-\alpha_m) \sum_{c_i = k_m(\mathbf{v}_i)} w_{i,m} + \exp(\alpha_m) \sum_{c_i \neq k_m(\mathbf{v}_i)} w_{i,m}, \quad (5.7)
```

where we defined the weights \(w_{i,m} = \exp(-c_i \mathcal{C}_{m-1}(\mathbf{v}_i))\). Hence the weight \(w_{i,m}\) is the exponential error the current classifier makes when classifying sample \(\mathbf{v}_i\). The total error can be rewritten as

```
E(\mathcal{C}_m) = \exp(-\alpha_m) \sum_{i=1}^N w_{i,m} + (\exp(\alpha_m) - \exp(-\alpha_m)) \sum_{c_i \neq k_m(\mathbf{v}_i)} w_{i,m}.
```

Only the last sum depends on the weak classifier \(k_m\). To make \(E(\mathcal{C}_m)\) small, the weak classifier should the sum of weights over the misclassified elements is smallest should be chosen. That is the classifier which classifies most samples with large weights correctly.

Having chosen \(k_m\), we differentiate the last line of 5.7 with respect to \(\alpha_m\) and set to zero, solving for \(\alpha_m\). This results in

```
\alpha_m = \frac{1}{2} \log \frac{\sum_{c_i = k_m(\mathbf{x}_i)} w_{i,m}}{\sum_{c_i \neq k_m(\mathbf{x}_i)} w_{i,m}}.
```

The more samples with large weights \(k_m\) classify correctly the larger \(\alpha_m\) and the confidence in \(k_m\). On the other hand, \(k_m\) classifying a sample with small weight incorrectly has little effect, since a small weight indicates that \(\mathcal{C}_{m-1}\) classifies this sample correctly.