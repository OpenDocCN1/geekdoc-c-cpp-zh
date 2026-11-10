
- where `x_Ai` — *i*th training pattern from class A
- `n` — Dimension of the input vectors
- `σ` — Smoothing parameter (corresponds to standard deviations of Gaussian distribution)

The function `f_A(x)` acts as an estimator as long as the parent density is smooth and continuous. `f_A(x)` approaches the parent density function as the number of data points used for the estimation increases. The function `f_A(x)` is a sum of Gaussian distributions. The disadvantage of using this parent density function along with Bayes decision rule is that the entire training set must be stored and the computation needed to classify an unknown vector is proportional to the size of the training set.

### Architecture

The architecture of the probabilistic neural net is shown in Figure 4.5. The architecture is made up of four types of units.

- Input units
- Pattern units — Class A and Class B.
- Summation units
- Output units

The weights between the summation unit and the output unit are,

$$V_A = 1$$
$$V_B = -\frac{P_B C_B m_A}{P_A C_A m_B}$$

### Training Algorithm

The training algorithm for the probabilistic neural net is given as,

```
For each training input pattern, x(p), p = 1, ..., P
    Create pattern unit Zp:
    Weight vector for unit Zp:    wp = x(p)
    (unit Zp is either a ZA unit or ZB unit)
    Connect the pattern unit to summation unit
    If x(p) belongs to class A,
        Then connect pattern unit Zp to summation unit SA
    Else
        connect pattern unit Zp to summation unit SB
    End If
End For
```

![](img/d9a4cc12c48f7466f309cbd3c4549c73_154_0.png)

**FIGURE 4.5:** Architecture of Probabilistic Neural Net

### Application Algorithm

The pseudocode of the application algorithm for classifying is given as,

```
Initialize weights from training algorithm.
For input pattern to be classified
    Pattern units:
        Calculate net input,
            z_{ij} = x.w_j = x^T W_j
        Calculate the output,
            Z = exp{(z_{ij}-1)/σ²}
    Summation units:
        The weights used by the summation unit for class B is,
            V_B = -P_B C_B m_A / P_A C_A m_B
    Output unit:
        Sums the signals from f_A and f_B
        Input vector is classified as class A if the
        total input to decision unit is positive
End For
```

### 4.2.5 Implementation of the Probabilistic Neural Net Using MATLAB

The probabilistic neural net can be implemented in MATLAB using the following function

```
net = newpnn(P, T, spread)
```

where,

- `P` — matrix of Q input vectors
- `T` — matrix of Q target class vectors
- `spread` — Spread of radial basis functions, default = 0.1

The function returns a new probabilistic neural network. If spread is near zero, the network will act as a nearest neighbor classifier. As spread becomes larger, the designed network will take into account several nearby design vectors.

### Example

Enter the input and the target vectors

```
clear all;
close all;
```

The input vectors P and target classes Tc below define a classification problem to be solved by an LVQ network.

```
inp = [1 2 3 4 5 6 7 8 9;9 8 7 6 5 4 3 2 1];
target_class = [1 1 1 2 2 2 3 3 3];
```

The target classes are converted to target vectors T. Then, an LVQ network is created (with input ranges obtained from P, four hidden neurons, and class percentages of 0.6 and 0.4) and is trained.

```
T = ind2vec(target_class);
```

The network is created and simulated, using the input to make sure that it does produce the correct classifications. The function vec2ind is used to convert the output Y into a row Yc to make the classifications clear.

```
network = newpnn(inp,T);
```

```
Y = sim(network,inp)
```

```
Yc = vec2ind(Y)
```

**Output**

```
Y =

   (1,1)   1
   (1,2)   1
   (1,3)   1
   (2,4)   1
   (2,5)   1
   (2,6)   1
   (3,7)   1
   (3,8)   1
   (3,9)   1
Yc =
   1  1  1  2  2  2  3  3  3
```

Thus the probabilistic neural net can be used for classification of patterns from each of the two classes that has been presented. This type of probabilistic neural net can be used to classify electrocardiogram's output as normal or abnormal.

## 4.3 Data Association Networks

The classification networks discussed in the previous sections are related to data association networks. In data association, classification is also done. For instance, a recognition unit can classify each of its scanned inputs into several groups. Yet, some data with errors are also available. The data association networks recognize these error occurrences as merely defective data and that this defective data can span all classifications.

### 4.3.1 Hopfield Network

The first data association network was proposed by John Hopfield in 1982 at the National Academy of Sciences and it was named as the Hopfield network. The network is conceived based on energy functions. Here in the Hopfield network, the processing elements update or change their state only if the overall “energy” of the state space is minimized. Basic applications for these kinds of networks have included associative and optimization problems, like the shortest path algorithm. Figure 4.6 shows the basic model of a Hopfield network. Earlier the original network used processing elements in binary formats which later on changed to bipolar format. Therefore the restriction in binary processing elements was during the quantization, that is the output is quantized to a zero or one.

![](img/d9a4cc12c48f7466f309cbd3c4549c73_157_0.png)

The basic model of Hopfield network includes three layers; an input buffer layer, a middle Hopfield layer, and an output layer. All the layers have equal number of processing elements. The inputs of the Hopfield layer are connected to the outputs of the corresponding processing elements in the input buffer layer through variable connection weights. The outputs of the Hopfield layer are connected back to the inputs of every other processing element except itself. While training, the network applies the data from the input layer through the learned connection weights to the Hopfield layer. The Hopfield layer takes some time to saturate, and the current state of that layer is passed on to the output layer. This state matches a pattern that is predefined and programmed into the network.

During learning the network requires the training pattern to be presented to the input and the output layer at the same time. The recursive and oscillating nature of the Hopfield layer allows the network to adjust all connection weights. The learning rule is the Hopfield Law, which states that “if the desired output and the input are both active or both inactive, increment the connection weight by the learning rate, otherwise decrement the weight by the learning rate”. Evidently, any non-binary implementation of the network must have a threshold mechanism in the transfer function, or matching input-output pairs could be too rare to train the network properly.

The network can be used as a content addressable memory. While applied as a content addressable memory, there are a few limitations like

- The amount of patterns that can be stored and precisely recalled is severely bounded. If too many patterns are stored, the network may converge to a wrong pattern or may not converge at all. Therefore the storage capacity should be limited to approximately fifteen percent of the number of processing elements in the Hopfield layer.
- The Hopfield layer may become unstable if there are common patterns. A pattern is considered unstable if it is applied at time zero and the network converges to some other pattern from the training set. This disadvantage is overcome by altering the pattern sets to be orthogonal with each other.

### Architecture

The architecture of the discrete Hopfield net is shown in Figure 4.7. It consists of “n” number of x input neurons and “y” output neurons. It should be noted that apart from receiving a signal from input, the y1 neuron receives a signal from its other output neurons also. This is the same for all the other output neurons. Thus, there exists a feedback output being returned to each output neuron. That is why the Hopfield network is called a feedback network.

### Training Algorithm

Discrete Hopfield net is described for both binary as well as bipolar vector patterns. The weight matrix to store the set of binary input patterns s(p), p = 1, ..., P, where

$$s(p) = (s_1(p), ..., s_i(p), ..., s_n(p))$$
