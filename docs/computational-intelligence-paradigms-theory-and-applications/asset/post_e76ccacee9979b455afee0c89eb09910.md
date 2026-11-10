
The first-layer weights are initialized to the center of the input ranges with the function midpoint. The second-layer weights have 60% (6 of the 10 in Tc above) of their columns with a 1 in the first row (corresponding to class 1), and 40% of their columns will have a 1 in the second row (corresponding to class 2).

```
network = newlvq(minmax(inp),4,[.6 .4]);
network = train(network,inp,T);
```

To view the weight matrices

```
network.IW(1,1); % first layer weight matrix
```

The resulting network can be tested.

```
Y = sim(network,inp)
Yc = vec2ind(Y)
```

Output: The network has classified the inputs into two basic classes, 1 and 2.

```
Y =

1     1     1     0     0     0     0     1     1     1
0     0     0     1     1     1     1     0     0     0
Yc =
1     1     1     2     2     2     2     1     1     1
```

Weight matrix of layer 1

```
ans =
    2.6384   -0.2459
   -2.5838    0.5796
   -0.0198   -0.3065
    0.1439    0.4845
```

Thus the above code implements the learning vector quantization algorithm to classify a given set of inputs into two classes.

## 4.2.3 Counter-Propagation Network

The Counter Propagation Network was proposed and developed by Robert Hecht-Nielsen to synthesize complex classification problems instead of reducing the number of processing elements and training time. The learning process of Counter propagation is more or less similar to LVQ with a small difference such that the middle Kohonen layer plays the role of a look-up table. This look-up table finds the closest fit to a given input pattern and outputs its equivalent mapping.

The first counter-propagation network was comprised of a bi-directional mapping between the input and output layers. Essentially, while data is presented to the input layer to generate a classification pattern on the output layer, the output layer in turn would accept an additional input vector and generate an output classification on the network’s input layer. The network got its name from this counter-posing flow of information through its structure. Most developers use a uni-flow variant of this formal representation of counter-propagation. Counter propagation networks have only one feedforward path from input layer to output layer.

An example network is shown in Figure 4.3. The uni-directional counter-propagation network has three layers. If the inputs are not already normalized before they enter the network, a fourth layer is sometimes required. The main layers include an input buffer layer, a self-organizing Kohonen layer, and an output layer which uses the Delta Rule also known as the Grossberg out star layer to modify its incoming connection weights.

![](img/d9a4cc12c48f7466f309cbd3c4549c73_144_0.png)

**FIGURE 4.3:** An Example Counter-Propagation Network

Depending upon the parameters that define a problem, the input layer’s size varies. If the input layer has very few processing elements, then the network may not generalize, and if the input layer has a large number of processing elements, then the processing time is very high.

Generally for fine operation of a network, the input vector must be normalized. Normalization refers to the process of adding; that is, for every combination of input values, the total “length” of the input vector must add up to one. The normalization process can be done with a preprocessor before presenting the data to the network. In specific applications, a normalization layer is added between the input and Kohonen layers. The normalization layer requires one processing element for each input, plus one more for a balancing element. This normalization layer assures that all input sets sum up to the same total.

Normalization of the inputs is necessary to ensure that the Kohonen layer finds the correct class for the problem. Without normalization, larger input vectors bias many of the Kohonen processing elements such that weaker value input sets cannot be properly classified. Due to the competitive nature of the Kohonen layer, the bigger value input vectors overcome the smaller vectors. Counter-propagation uses a standard Kohonen layer which self-organizes the input sets into classification zones. It follows the classical Kohonen learning law. This layer acts as a closest neighbor classifier such that the processing elements in the competitive layer autonomously update their connection weights to divide up the input vector space in approximate correspondence to the frequency with which the inputs occur. There should be as many processing elements as possible in the Kohonen layer equivalent to the output classes. The Kohonen layer generally has a lot more elements than classes simply because additional processing elements provide a finer resolution between similar objects.

The output layer for counter-propagation fundamentally consists of processing elements which learn to produce an output when a specific input is applied. Because the Kohonen layer is a competitive layer, only a single winning output is produced for a given input vector. This layer renders a method of decoding the input to a purposeful output class. The delta rule is used to back-propagate the error between the desired output class and the actual output generated with the training set. The weights in the output layer alone are updated while the Kohonen layer is unaffected.

As only one output from the competitive Kohonen layer is active at a time and all other elements are zero, the only weights adjusted for the output processing elements are the ones connected to the winning element in the competitive layer. In this way the output layer learns to reproduce a definite pattern for each active processing element in the competitive layer. If numerous competitive elements belong to the same class, then the output processing element will acquire weights in response to those competitive processing elements and zero for all others.

The major limitation of this architecture is that the competitive Kohonen layer learns without any supervision. Therefore it cannot predict the type of class it is reporting to. This infers that it is possible for a processing element in the Kohonen layer to learn two or more training inputs, which belong to different classes. During this process, the output of the network will be multi-valued for any inputs. To overcome this difficulty, the processing elements in the Kohonen layer can be pre-conditioned to learn only about a specific class.

Counter propagation network is classified into two types. They are

- 1. Full counter propagation network
- 2. Forward only counter propagation network

In this section, the training algorithm and application procedure of full CPN is described.

### Training Phases of Full CPN

The full CPN is achieved in two phases.

The first phase of training is called as In star modeled training. The active units here are the units in the x-input (x = x₁, …, xᵢ, …, xₙ), z-cluster (z = z₁, …, zⱼ, …, zₚ) and y-input (y = y₁, …, yₖ, …, yₘ) layers.

Generally in CPN, the cluster unit does not assume any topology, but the winning unit is allowed to learn. This winning unit uses our standard Kohonen learning rule for its weight updation. The rule is given by

$$\begin{aligned}
v_{ij}(new) &= v_{ij}(old) + \alpha(x_i - v_{ij}(old)) \\
&= (1-\alpha)v_{ij}(old) + \alpha x_i;\quad i=1\text{ to }n \\
w_{jk}(new) &= w_{jk}(old) + \beta(y_k - w_{jk}(old)) \\
&= (1-\beta)w_{jk}(old) + \beta y_k;\quad k=1\text{ to }m
\end{aligned}$$

In the second phase, we can find only the J unit remaining active in the cluster layer. The weights from the winning cluster unit J to the output units are adjusted, so that the vector of activation of units in the y output layer, y*, is an approximation of input vector x. This phase may be called the out star modeled training. The weight updation is done by the Grossberg learning rule, which is used only for out star learning. In out star learning, no competition is assumed among the units, and the
