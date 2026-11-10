+   - **Design phase:**
+     - Define the number of nodes in each of the three layers (input, hidden, output)
+     - Define the transfer functions
+     - Initialize the training routine that is to be used.
+     - Optional parts of the design: Error function (Mean Square Error is the default), plot the progress of training, etc.

+   - **Training phase:**
+     - Once the network has been designed, the network is designed by optimizing the error function
+     - This process determines the “best” set of weights and biases for the users data set.

+   - **Testing phase**
+     - Test the network to see if it has found a good balance between memorization (accuracy) and generalization

The BPN network can be implemented in MATLAB using the Neural Network Toolbox as follows.

```
clc;
clear all;
close all;
```

The first step in training a feedforward network is to create the network object. The function newff creates a feedforward network. It requires four inputs and returns the network object. The first input is an R by 2 matrix of minimum and maximum values for each of the R elements of the input vector. The second input is an array containing the sizes of each layer. The third input is a cell array containing the names of the transfer functions to be used in each layer. The final input contains the name of the training function to be used.

```
% Creating a network
net=newff([-1 2; 0,
5], [3,1],'tansig','purelin','traingd');
```

Before training a feedforward network, the weights and biases must be initialized. The newff command will automatically initialize the weights, but it may be required to reinitialize them. This can be done with the command init.