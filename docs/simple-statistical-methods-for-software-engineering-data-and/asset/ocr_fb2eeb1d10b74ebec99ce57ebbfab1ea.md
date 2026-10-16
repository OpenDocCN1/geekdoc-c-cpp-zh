what the Project Manager expected. When we investigated the reason, it turned out that the software was not completely developed.

We learned that the Gompertz model can only be used in the test–analyze–fix cycle and not when full-fledged software development is in progress. We also learned that the model should not be used for prediction at the early stages of the test–analyze–fix cycle. The product under test has to reach a certain maturity before we start using the data for predicting.

As a Gompertzian rule of thumb, until inflection is visible, the model should not be used for prediction. It takes time and sufficient data to reach the inflection point. The model is to be kept dormant until such a time.

# Gompertz Curve versus GO NHPP Model

The two-parameter GO model is discussed in Chapter 12. This original model has been criticized because it is concave and lacks the flexibility of the S curve. A third parameter c was added by Goel to this model to make it reflect real-life testing. The model is known as the generalized GO model, (NHPP: non homogeneous poisson process) as shown in Figure 21.8.

This model can be compared with the Gompertz curve for ready reference, also shown in Figure 21.8. The two curves shown are representative samples from the generalized GO family and the Gompertz family.

Both are S curves; the similarity is interesting coming from two different domains, one from computer science and the other from actuarial studies. Both the models, generalized GO and Gompertz curve, are capable controlled inflection. However, the Gompertz curve is a wee bit more practical and flexible.

![](bbox=[0.12, 0.62, 0.88, 0.88])

Figure 21.8 Gompertz curve versus GO NHPP model.