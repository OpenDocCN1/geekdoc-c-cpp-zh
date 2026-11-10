
## Learning in Back Propagation

There are two types of learning.

- i. Sequential learning or per-pattern method
- ii. Batch learning or per-epoch method

In sequential learning a given input pattern is propagated forward, the error is determined and back propagated, and the weights are updated.

In Batch learning the weights are updated only after the entire set of training network has been presented to the network. Thus the weight update is only performed after every epoch.

If p = patterns in one epoch, then

$$\Delta w = \frac{1}{p}\sum_{p=1}^{P}\Delta w_p$$

In some cases, it is advantageous to accumulate the weight correction terms for several patterns and make a single weight adjustment (equal to the average of the weight correction terms) for each weight rather than updating the weights after each pattern is presented. This procedure has a “smoothing effect”. In some cases the smoothing may increase the chances of convergence to the local minimum.

### Time taken to train a net

The need for applying back propagation network is to accomplish a balance between memorization and generalization; it is not necessarily appropriate to proceed training until the error reaches minimum value. The two disjoint sets of data used during training are:

- Set of training patterns
- Set of training-testing patterns.

Training patterns have a great influence on weight adjustments. As the error in a neural network increases the network starts to store and memorise the training patterns.

### Number of Training Pairs

The number of training pairs likewise plays a crucial part on training of the nets. A simple rule of thumb is utilized to ascertain the number of training pairs.

Consider a net trained to classify the fraction (1-e/2) of the trained patterns correctly. This means it will also classify (1-e) of the testing pattern correctly by using the following condition. If there are enough training patterns the net will be able to generalize as desired. Enough training pattern is given by w/p = e, where p = number of training patterns and w = number of weights to be trained.

The value of e lies between 0 to 1/8. The necessary condition is given by

$$p > |w|/(1-a)$$

where a = expected accuracy for the test set.

Sufficient condition is given as

$$p > |w|/(1-a)\log(n/(1-a))$$

where n = number of nodes.

### Number of Hidden Units

In general, the choice of hidden units depends on many factors such as:

- numbers of input and output units
- number of training patterns
- noise in the target vectors
- complexity of the function or classification to be learned
- architecture
- type of hidden unit activation function
- training algorithm
- regularization

In a number of situations, there is no specific way to determine the best number of hidden units without training several networks and estimating the generalization error of each. If there are a few hidden units, then the training error and generalization error are very high due to underfitting and there occurs high statistical bias. If there are too many hidden units, then the training error is too low but still has high generalization error due to overfitting and high variance.

### Momentum Factor

The weight updation in a BPN is proceeded in a direction which is a combination of present gradient and the former gradient. This kind of an approach is advantageous while a few training data differ from a majority of the data. A low value of learning rate is applied to avoid great disturbance in the direction of learning whenever identical and unusual pair of training patterns is presented. The speed of convergence increases as if the momentum factor is added to the weight updation rule. The weights from one or more former training patterns must be saved in order to use momentum. For the BPN with momentum, the new weights for training step t+2 is based on t and t+1. It is found that momentum allows the net to perform for weight adjustments as long as the correction proceeds in the same general direction for several patterns. Hence applying momentum, the net does not go forward in the direction of the gradient, just travels in the direction of the combination of the present gradient and the former gradient for which the weight updation is made. The main purpose of the momentum is to speed up the convergence of error propagation algorithm. This method makes the current weight adjustment with the fraction of the recent weight adjustment.

The weight updating formula for BPN with momentum is:

$$w_{jk}(t+1)=w_{jk}(t)+\alpha\delta_k z_j+\mu[w_{jk}(t)-w_{jk}(t-1)]$$

$$v_{ij}(t+1)=v_{ij}(t)+\alpha\delta_j x_i+\mu[v_{ij}(t)-v_{ij}(t-1)]$$

μ is called the momentum factor. It ranges from 0<μ<1.

### Application Algorithm

The application procedure for BPN is shown below:

```
Initialize weights from (training algorithm).
    For each input vector
        For i=1,..,n ;
            set activation of input unit, xᵢ;
        End For
        For j=1,..,p ;
            zᵢₙⱼ = v₀ⱼ + Σᵢ₌₁ⁿ xᵢvᵢⱼ
        End For
        For k=1,..,m ;
            yᵢₙₖ = w₀ₖ + Σⱼ₌₁ᵖ zⱼwⱼₖ
        End For
    End For
End
```

## 3.3.4 Implementation of BPN Using MATLAB

MATLAB has a suite of inbuilt functions designed to build neural networks, the Neural Networks Toolbox. Basically a programmer has to go through three phases to implement neural networks: Design, Training, and Testing.

- **Design phase:**
  - Define the number of nodes in each of the three layers (input, hidden, output)
  - Define the transfer functions
  - Initialize the training routine that is to be used.
  - Optional parts of the design: Error function (Mean Square Error is the default), plot the progress of training, etc.
- **Training phase:**
  - Once the network has been designed, the network is designed by optimizing the error function
  - This process determines the “best” set of weights and biases for the user's data set.
- **Testing phase**
  - Test the network to see if it has found a good balance between memorization (accuracy) and generalization

The BPN network can be implemented in MATLAB using the Neural Network Toolbox as follows.

```
clc;
clear all;
close all;
```

The first step in training a feedforward network is to create the network object. The function newff creates a feedforward network. It requires four inputs and returns the network object. The first input is an R by 2 matrix of minimum and maximum values for each of the R elements of the input vector. The second input is an array containing the sizes of each layer. The third input is a cell array containing the names of the transfer functions to be used in each layer. The final input contains the name of the training function to be used.

```
% Creating a network
net=newff([-1 2; 0 5], [3,1], {'tansig','purelin'}, 'traingd');
```

Before training a feedforward network, the weights and biases must be initialized. The newff command will automatically initialize the weights, but it may be required to reinitialize them. This can be done with the command init.

```
% Initialising weights
net = init(net);
```

The function `sim` simulates a network. The function `sim` takes the network input `p`, and the network object `net`, and returns the network outputs `a`.

```
% Simulating the network
p = [1 2 3 4 5; 6 7 8 9 0];
a = sim(net,p)
```

There are seven training parameters associated with `traingd`: epochs, show, goal, time, min_grad, max_fail, and lr. The learning rate lr is multiplied times the negative of the gradient to determine the changes to the weights and biases. The larger the learning rate, the bigger the step. If the learning rate is made too large, the algorithm becomes unstable. If the learning rate is set too small, the algorithm takes a long time to converge. The training status is displayed for every show iteration of the algorithm. (If show is set to NaN, then the training status never displays.) The other parameters determine when the training stops. The training stops if the number of iterations exceeds epochs, if the performance function drops below goal, if the magnitude of the gradient is less than min_grad, or if the training time is longer than time seconds.

```
% Parameter setting
net.trainParam.show = 50;
net.trainParam.lr = 0.05;
net.trainParam.epochs = 300;
net.trainParam.goal = 1e-5;
```

Now the network is ready for the training phase

```
% Training the network
t = [1 -1 1 -1 1];
[net,tr]=train(net,p,t);
```

The output obtained is shown in Figure 3.8. The observations are shown below

```
TRAINING, Epoch 0/300, MSE 1.27137/1e-005, Gradient 2.30384/1e-010
TRAINING, Epoch 50/300, MSE 0.730344/1e-005, Gradient 0.17989/1e-010
TRAINING, Epoch 100/300, MSE 0.684018/1e-005, Gradient 0.0927535/1e-010
```
