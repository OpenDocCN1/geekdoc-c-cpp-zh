In the final assessment step, you will employ the Model Comparison node to compare all three models, using both gains tables and a cumulative-lift graph.

# Neural Network

As described in Chapter 3, neural networks are models that capture many of the nonlinear relationships in data. So, although neural network models sometimes do a better job of fitting the model than the decision tree or regression models, they might not perform as well on the validation data or maintain their ability to predict as accurately over time. Another disadvantage of neural network models is that they are more difficult for marketers to interpret than the decision tree models.

Under the Model tab, drag the Neural Network icon (fifth from the right) onto the diagram and connect it to the Transform Variables node. Figure 9.14 shows the diagram and the Neural Network Property window. In the Train section, next to Model Selection Criterion, change Value to Misclassification. Right-click the model node, and click Run ▶ Yes. When the window appears, click Results.

Figure 9.14: Neural Network Property Window

![](bbox=[0.12, 0.63, 0.9, 0.82])

As shown in Output 9.11, the cumulative lift is much higher for the neural network train data than for the validation data.