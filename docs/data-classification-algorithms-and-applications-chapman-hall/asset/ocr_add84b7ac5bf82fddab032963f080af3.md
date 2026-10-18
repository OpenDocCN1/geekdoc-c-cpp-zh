![](bbox=[0.24, 0.08, 0.74, 0.32])

FIGURE 7.9: The margins of multiclass SVM.

ing problem,
min_{w1,...,wk} sum_{m=1}^k w_m^T w_m
s.t. w_{y_i}^T x_i - w_m^T x_i >= 1,
∀ m = 1,...,k, m ≠ y_i, ∀ i = 1,...,l.

For the nonseparable scenario, the formulation with a loss term ξ is
min_{w1,...,wk, ξ} 1/2 sum_{m=1}^k w_m^T w_m + C sum_{i=1}^l ξ_i
subject to w_{y_i}^T x_i - w_m^T x_i >= (1 - δ_{y_i,m}) - ξ_i,
∀ i = 1...l, ∀ m = 1...k,

where δ_{y_i,m} is defined to be 1 when y_i equals m, and 0 otherwise. We could validate that when y_i equals m, the corresponding inequality becomes ξ_i ≥ 0. This formulation is referred to as the Crammer and Singer’s SVM (CSSVM) [10, 11]. Similarly, we can derive its dual problem and the kernelized form. Compared to the binary reduction strategies, the work in [17] shows that CSSVM usually gives similar classification accuracy, but needs more training time. Other similar, but slightly different strategies, are provided in [22, 36].

# 7.8 Conclusion

SVM is now considered a mature machine learning method. It has been widely applied in different applications. Furthermore, SVM has been well-studied, both from theoretical and practical perspectives. In this chapter we focus on the kernelized SVMs, which construct nonlinear separating surfaces. However, on sparse data with many features and instances, a linear SVM may achieve similar accuracy with a kernelized SVM, but is significantly faster. Readers may refer to [13] and [37] for details.

The topic of kernelized SVM is broader than one can hope to cover in a single chapter. For example, we have not discussed topics such as kernelized support vector regression (SVR) and kernel approximations to improve the training speed. Our aim was to introduce the basic concepts