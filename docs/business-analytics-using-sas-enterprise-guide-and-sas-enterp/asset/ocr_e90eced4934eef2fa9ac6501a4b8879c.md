exp (β₀ + β₁X₁ + β₂X₂ + … + βₙXₙ)). This formula is also written in a simpler form as follows: *p* = 1/(1 + exp (−(β₀ + β₁X₁ + β₂X₂ + … + βₙXₙ))).

+   6. The process starts with a given value for response at each value of age. Values for *p* are bounded by 0 and 1. Using a link function, you derive a model using maximum likelihood. The result is log (*p* / (1 − *p*)) = 1.233 + 6.39 × prospect’s age and *p* = 1/(1 + e^(−(1.233+6.39×prospect’s age))).

The formula enables you to estimate the response rate, given the value for prospect’s age.

This example is a simple one; logistic regression models typically have numerous predictive variables.

# Neural Networks

Neural network processing differs greatly from regression in that the process does not follow any statistical distribution. Instead, a neural network is modeled after the function of the human brain. The process is one of pattern recognition and error minimization. You can think of it as ingesting information and learning from each experience.

Neural networks are made up of nodes that are arranged in layers. This construction varies, depending on the type and complexity of the neural network. Figure 3.9 illustrates a simple neural network with one hidden layer. Before the process begins, the data is split into *training* and *testing* data sets. (A third group is sometimes held out for final validation.) Then weights or “inputs” are assigned to each of the nodes in the first layer. During each iteration, the inputs are processed through the system and compared with the actual value. The error is measured and fed back through the system to adjust the weights. In most cases, the weights improve in their ability to predict the actual values. The process ends when a predetermined minimum error level is reached.