First, let us ignore the bias (constant term) weights B1 and B2, since they do not affect the relationship between the predictors and the response. Next, recall our exploratory data analysis (EDA), where we found that greater age and being male were both associated with higher probability of death in the Framingham Heart Study. Also, Sex is a binary predictor with 1 = Male and 2 = Female, so that an increase in the value of Sex should be associated with a decrease in probability of death. Let us see how and whether these EDA results are reflected in the neural network weights.

Now, the weight between the hidden layer node H1 and the output node O1 takes a negative value, $W_{H1O1} = -5.8477$. Thus, when the hidden layer node H1 is excited to a high value, it actually has a protective effect against death, lowering its probability, because of this negative weight.

Next, the weight from the Sex predictor to the hidden layer node takes a positive value, $W_{SexH1} = 0.6418$. This means that larger values of Sex (females) will tend to excite the hidden neuron H1 to a higher value. As we just learned, such a high value for H1 lowers the probability of death. Thus, the weights are telling us that being female protects against the probability of death, just as we saw in the EDA.

Finally, the weight from the Age predictor to the hidden layer node takes a negative value, $W_{AgeH1} = -3.0784$. This means that higher values of Age will result in a lower value for the hidden layer neuron H1. Low values from H1 to output node O1 result in a high probability of death because its weight is negative as well. Thus, the weights are telling us that an increase in age is associated with an increase in the probability of death, exactly as we saw in the EDA.

# 9.8 HOW TO USE NEURAL NETWORKS IN R

First, read in the Framingham_training data set as fram_train, and convert the binary and ordinal variables Death and Sex to factors.

```
fram_train$Death <- as.factor(fram_train$Death)
fram_train$Sex <- as.factor(fram_train$Sex)
```

Perform min-max standardization on the Age variable

```
fram_train$Age.mm <- (fram_train$Age - min(fram_train$Age)) / (max(fram_train$Age) - min(fram_train$Age))
```

Install the nnet and NeuralNetTools packages, and open both packages.

```
install.packages("nnet"); install.packages("NeuralNetTools")
library(nnet); library(NeuralNetTools)
```

Run the neural network algorithm.

```
nnet01 <- nnet(Death ~ Sex + Age.mm, data = fram_train, size = 1)
```

Note the formula structure, with the target variable Death on the left side of the tilde, and the two predictor variables Sex and Age on the right side. The