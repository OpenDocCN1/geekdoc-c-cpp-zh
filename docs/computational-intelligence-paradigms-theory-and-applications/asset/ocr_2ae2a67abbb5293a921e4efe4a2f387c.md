by 2 matrix of minimum and maximum values for each of the R elements of the input vector. The second input is an array containing the sizes of each layer. The third input is a cell array containing the names of the transfer functions to be used in each layer. The final input contains the name of the training function to be used.

```
```matlab
network=newff([0 1;0 1;0 1],[6 1],
'logsig','logsig');
```
```

Before training a feedforward network, the weights and biases must be initialized. The newff command will automatically initialize the weights, but it may be required to reinitialize them. This can be done with the command init.

```
```matlab
network=init(network);
```
```

The function sim simulates a network. The function sim takes the network input, and the network object net, and returns the network outputs.

```
```matlab
y=sim(network,inp);
figure,plot(inp,out,inp,y,'o'),
title('Before Training');
axis([-5 5 -2.0 2.0]);
```
```

There are seven training parameters associated with traingd: epochs, show, goal, time, min_grad, max_fail, and lr. Here the number of epochs and the learning rate are defined as follows

```
```matlab
network.trainParam.epochs = 500;
network.trainParam.lr = 0.05;
```
```

Training the network. Simulate the network and plot the results (Figure 3.6)

```
```matlab
network=train(network,inp,out);
y=sim(network,inp);
figure,plot(inp,out,inp,y,'o'),
title('After Training');
axis([-5 5 -2.0 2.0]);
```
```

Updated weights and bias values

```
```matlab
Layer1.Weights=network.iw1
Layer1.Bias=network.b1
```
```