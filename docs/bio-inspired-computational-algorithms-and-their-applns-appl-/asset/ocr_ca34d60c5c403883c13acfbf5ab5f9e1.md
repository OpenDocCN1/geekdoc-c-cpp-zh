Third, the difference between the desired and the actual output is computed, producing the network error. This error term is then passed backwards through the network to adjust the connection weights.

Each network input unit takes a single numeric value, x_i, which is usually scaled or normalized to a value between 0.0 and 1.0. This value becomes the input unit activation. Next, we need to propagate the data forward, through the neural network. For each unit in the hidden layer, we compute the sum of the products of the input unit activations and the weights connecting those input layer units to the hidden layer. This sum is the inner product (also called the dot or scalar product) of the input vector and the weights in the hidden unit. Once this sum is computed, we add a threshold value and then pass this sum through a nonlinear activation function, f, producing the unit activation y_j. The formula for computing the activation of any unit in a hidden or output layer in the network is

$y_j = f\left(\text{sum}_j = \sum_i x_i w_{ij} + \theta\right)$ (34)

where i ranges over all the units leading into the j-th unit, and the activation function is

$f(\text{sum}_j) = \frac{1}{1 + e^{-\text{sum}_j}}$ (35)

As mentioned earlier, we use the S-shape sigmoid or logistic function for f. The formula for calculating the changes of the weights is

$\Delta w_{ij} = \eta \delta_j y_i$ (36)

where w_ij is the weight connecting unit i to unit j, η is the learn rate parameter, δ_j is the error signal for that unit, and y_i is the output or activation value of unit i. For units in the output layer, the error signal is the difference between the target output t_j and the actual output y_j multiplied by the derivative of the logistic activation function.

$\delta_j = (t_j - y_j) f'(\text{sum}_j) = (t_j - y_j) y_j (1 - y_j)$ (37)