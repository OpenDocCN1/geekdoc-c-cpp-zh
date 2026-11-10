schematic of this still simplistic artificial neuron.

![](bbox=[0.133, 0.167, 0.904, 0.301])

# **FIGURE 2.3:** A Model of a “Processing Element”

In Figure 2.3, inputs enter into the processing element from the upper left. The initial step is to multiply each of the inputs with their corresponding weighting factor (w(n)). Then these altered inputs are fed into the summing function, which usually just sums these products. Eventually, several kinds of operations can be selected. These operations could produce a number of different values, which are then propagated forward; values such as the average, the largest, the smallest, the ORed values, the ANDed values, etc. Moreover, most commercial development products allow software engineers to create their own summing functions through routines coded in a higher-level language. Occasionally the summing function is further elaborated by the addition of an activation function which enables the summing function to operate in a time sensitive manner.

Either way, the output of the summing function is then sent into a transfer function. This function then turns this number into a real output via some algorithm. It is this algorithm that takes the input and turns it into a zero or a one, a minus one or a one, or some other number. The transfer functions that are commonly supported are sigmoid, sine, hyperbolic tangent, etc. This transfer function also can scale the output or control its value via thresholds. The result of the transfer function is usually the direct output of the processing element. An example of how a transfer function works is shown in Figure 2.4.

This sigmoid transfer function takes the value from the summation function, called sum in the Figure 2.4, and turns it into a value between zero and one.

Finally, the processing element is ready to output the result of its transfer function. This output is then input into other processing elements, or to an outside connection, as determined by the structure of