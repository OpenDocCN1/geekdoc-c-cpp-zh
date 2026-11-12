![](bbox=[0.1, 0.08, 0.9, 0.38])

# Figure 9.3 Details of neural network, showing input to node A, combination function, and output from node A.

neurons when the combination of inputs to a particular neuron crosses a certain threshold and the neuron “fires.” This is nonlinear behavior, since the firing response is not necessarily linearly related to the increment in input stimulation.

The most common activation function is the sigmoid function:

```
y = \frac{1}{1 + e^{-x}}
```

where e is the base of natural logarithms, equal to about 2.718281828. Thus, within node A, the activation would take net_A = 1.32 as an input to the sigmoid activation function and produce an output value of

```
y = f(net_A) = \frac{1}{1 + e^{-1.32}} = 0.7892
```

Node A’s work is done (for the moment) and this output value would then be passed along the connection to the output node Z, where it would form (via another linear combination) a component of net_z.

It is left as an exercise to calculate net_z = 1.5 and f(net_z) = \frac{1}{1 + e^{-1.3}} = 0.8176.

Node Z then combines these outputs from nodes A and B, through net_z, a weighted sum, using the weights associated with the connections between these nodes. Note that the inputs x_i to node Z are not data-attribute values but the outputs from the sigmoid functions from upstream nodes: