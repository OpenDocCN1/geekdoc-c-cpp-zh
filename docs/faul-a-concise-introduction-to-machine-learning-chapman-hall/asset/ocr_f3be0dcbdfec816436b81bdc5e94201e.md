![](bbox=[0.26, 0.1, 0.49, 0.25])

![](bbox=[0.51, 0.1, 0.74, 0.25])

![](bbox=[0.25, 0.28, 0.39, 0.4])

![](bbox=[0.42, 0.28, 0.56, 0.4])

![](bbox=[0.59, 0.28, 0.74, 0.4])

![](bbox=[0.26, 0.43, 0.49, 0.61])

![](bbox=[0.51, 0.43, 0.74, 0.61])

Figure 9.5: Autoencoder with two hidden neurons applied to three digits.

dimensions of the model space. While the set of digits as a whole seems to be centred around a mean in each of the dimensions, some digits move away from this centre. For example, in Figure 9.7a digits two, three and eight lie further to the right in this dimension, while in Figure 9.7c it is digits two and six. In Figure 9.7f the digits to the right are mostly one. Applying the logistic sigmoid maps activations to the right close to one, while those to the left are mapped close to zero. Figures 9.7k and 9.7l show the proportions of digits which get mapped close to zero and one in each of the ten dimensions corresponding to the hidden neurons. While nearly all digits are present close to zero, near one some digits are dominant. This means these neurons “fire” for particular digits.

The following table indicates for which digits an individual neuron “fires”.