
## Functions of Neural Network Toolbox

| Function | Description |
|---|---|
| Analysis Functions | Analyze network properties |
| Distance Functions | Compute distance between two vectors |
| Graphical Interface Functions | Open GUIs for building neural networks |
| Layer Initialization Functions | Initialize layer weights |
| Learning Functions | Learning algorithms used to adapt networks |
| Line Search Functions | Line-search algorithms |
| Net Input Functions | Sum excitations of layer |
| Network Initialization Function | Initialize network weights |
| New Networks Functions | Create network architectures |
| Network Use Functions | High-level functions to manipulate networks |
| Performance Functions | Measure network performance |
| Plotting Functions | Plot and analyze networks and network performance |
| Processing Functions | Preprocess and postprocess |
| Simulink Support Function | Generate Simulink block for network simulation |
| Topology Functions | Arrange neurons of layer according to specific topology |
| Training Functions | Train networks |
| Transfer Functions | Transform output of network layer |
| Utility Functions | Internal utility functions |
| Vector Functions | Internal functions for network computations |
| Weight and Bias Initialization Functions | Initialize weights and biases |
| Weight Functions | Convolution, dot product, scalar product, and distance weight functions |

### Analysis Functions

| Function | Description |
|---|---|
| `errsurf` | Error surface of single-input neuron |
| `confusion` | Classification confusion matrix |
| `minlinlr` | Maximum learning rate for linear neuron |
| `roc` | Receiver operating characteristic |

### Distance Functions

| Function | Description |
|---|---|
| `boxdist` | Distance between two position vectors |
| `dist` | Euclidean distance weight function |
| `linkdist` | Link distance function |
| `mandist` | Manhattan distance weight function |

### Graphical Interface Functions

| Function | Description |
|---|---|
| `nctool` | Neural network classification tool |
| `nftool` | Open Neural Network Fitting Tool |
| `nntool` | Open Network/Data Manager |
| `nntraintool` | Neural network training tool |
| `nprtool` | Neural network pattern recognition tool |
| `view` | View a neural network |

### Layer Initialization Functions

| Function | Description |
|---|---|
| `initnw` | Nguyen-Widrow layer initialization function |
| `initwb` | By-weight-and-bias layer initialization function |

### Learning Functions

| Function | Description |
|---|---|
| `learncon` | Conscience bias learning function |
| `learngd` | Gradient descent weight/bias learning function |
| `learngdm` | Gradient descent with momentum weight/bias learning function |
| `learnh` | Hebb weight learning function |
| `learnhd` | Hebb with decay weight learning rule |
| `learnis` | Instar weight learning function |
| `learnk` | Kohonen weight learning function |
| `learnlv1` | LVQ1 weight learning function |
| `learnlv2` | LVQ2 weight learning function |
| `learnos` | Outstar weight learning function |
| `learnp` | Perceptron weight and bias learning function |
| `learnpn` | Normalized perceptron weight and bias learning function |
| `learnsom` | Self-organizing map weight learning function |
| `learnsomb` | Batch self-organizing map weight learning function |
| `learnwh` | Widrow-Hoff weight and bias learning rule |

### Line Search Functions

| Function | Description |
|---|---|
| `srchbac` | 1-D minimization using backtracking search |
| `srchbre` | 1-D interval location using Brent’s method |
| `srchcha` | 1-D minimization using Charalambous’ method |
| `srchgol` | 1-D minimization using golden section search |
| `srchhyb` | 1-D minimization using hybrid bisection/cubic search |

### Performance Functions

| Function | Description |
|---|---|
| `mae` | Mean absolute error performance function |
| `mse` | Mean squared error performance function |
| `msereg` | Mean squared error with regularization performance function |
| `mseregec` | Mean squared error with regularization and economization performance function |
| `sse` | Sum squared error performance function |

### Plotting Functions

| Function | Description |
|---|---|
| `hintonw` | Hinton graph of weight matrix |
| `hintonwb` | Hinton graph of weight matrix and bias vector |
| `plotbr` | Plot network performance for Bayesian regularization training |
| `plotconfusion` | Plot classification confusion matrix |
| `plotep` | Plot weight and bias position on error surface |
| `plotes` | Plot error surface of single-input neuron |
| `plotfit` | Plot function fit |
| `plotpc` | Plot classification line on perceptron vector plot |
| `plotperf` | Plot network performance |
| `plotpv` | Plot perceptron input target vectors |
| `plotregression` | Plot linear regression |
| `plotroc` | Plot receiver operating characteristic |
| `plotsom` | Plot self-organizing map |
| `plotsomhits` | Plot self-organizing map sample hits |
| `plotsomnc` | Plot self-organizing map neighbor connections |
| `plotsomnd` | Plot self-organizing map neighbor distances |
| `plotsompos` | Plot self-organizing map weight positions |
| `plotsomtop` | Plot self-organizing map topology |
| `plottrainstate` | Plot training state values |
| `plotv` | Plot vectors as lines from origin |
| `plotvec` | Plot vectors with different colors |
| `postreg` | Postprocess trained network response with linear regression |

### Processing Functions

| Function | Description |
|---|---|
| `fixunknowns` | Process data by marking rows with unknown values |
| `mapminmax` | Process matrices by mapping row minimum and maximum values to [-1 1] |
| `mapstd` | Process matrices by mapping each row's means to 0 and deviations to 1 |
| `processpca` | Process columns of matrix with principal component analysis |
| `removeconstantrows` | Process matrices by removing rows with constant values |
| `removerows` | Process matrices by removing rows with specified indices |

### Simulink Support Function

| Function | Description |
|---|---|
| `gensim` | Generate Simulink block for neural network simulation |

### Topology Functions

| Function | Description |
|---|---|
| `gridtop` | Gridtop layer topology function |
| `hextop` | Hexagonal layer topology function |
| `randtop` | Random layer topology function |

### Training Functions

| Function | Description |
|---|---|
| `trainb` | Batch training with weight and bias learning rules |
| `trainbfg` | BFGS quasi-Newton backpropagation |
| `trainbfgc` | BFGS quasi-Newton backpropagation for use with NN model reference adaptive controller |
| `trainbr` | Bayesian regularization |
| `trainbuwb` | Batch unsupervised weight/bias training |
| `trainc` | Cyclical order incremental update |
| `traincgb` | Powell-Beale conjugate gradient backpropagation |
| `traincgf` | Fletcher-Powell conjugate gradient backpropagation |
| `traincgp` | Polak-Ribière conjugate gradient backpropagation |
| `traingd` | Gradient descent backpropagation |
| `traingda` | Gradient descent with adaptive learning rule backpropagation |
| `traingdm` | Gradient descent with momentum backpropagation |
| `traingdx` | Gradient descent with momentum and adaptive learning rule backpropagation |
| `trainlm` | Levenberg-Marquardt backpropagation |
| `trainoss` | One step secant backpropagation |
| `trainr` | Random order incremental training with learning functions |
| `trainrp` | Resilient backpropagation (Rprop) |
| `trains` | Sequential order incremental training with learning functions |
| `trainscg` | Scaled conjugate gradient backpropagation |

### Transfer Functions

| Function | Symbol | Description |
|---|---|---|
| `compet` | [图标] | Competitive transfer function |
| `hardlim` | [图标] | Hard limit transfer function |
| `hardlims` | [图标] | Symmetric hard limit transfer function |
| `logsig` | [图标] | Log-sigmoid transfer function |
| `netinv` | [图标] | Inverse transfer function |
| `poslin` | [图标] | Positive linear transfer function |
| `purelin` | [图标] | Linear transfer function |
| `radbas` | [图标] | Radial basis transfer function |
| `satlin` | [图标] | Saturating linear transfer function |
| `satlins` | [图标] | Symmetric saturating linear transfer function |
| `softmax` | [图标] | Softmax transfer function |
| `tansig` | [图标] | Hyperbolic tangent sigmoid transfer function |
| `tribas` | [图标] | Triangular basis transfer function |
