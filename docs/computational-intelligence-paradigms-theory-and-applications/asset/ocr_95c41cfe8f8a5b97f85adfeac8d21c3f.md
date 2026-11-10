the role of a look-up table. This look-up table finds the closest fit to a given input pattern and outputting its equivalent mapping.

The first counter-propagation network comprised of a bi-directional mapping between the input and output layers. Essentially, while data is presented to the input layer to generate a classification pattern on the output layer, the output layer in turn would accept an additional input vector and generate an output classification on the network’s input layer. The network got its name from this counter-posing flow of information through its structure. Most developers use a uni-flow variant of this formal representation of counter-propagation. Counter propagation networks have only one feedforward path from input layer to output layer.

An example network is shown in Figure 4.3. The uni-directional counter-propagation network has three layers. If the inputs are not already normalized before they enter the network, a fourth layer is sometimes required. The main layers include an input buffer layer, a self-organizing Kohonen layer, and an output layer which uses the Delta Rule also known as the Grossberg out star layer to modify its incoming connection weights.

![](bbox=[0.055, 0.5, 0.884, 0.875])

**FIGURE 4.3:** An Example Counter-Propagation Network