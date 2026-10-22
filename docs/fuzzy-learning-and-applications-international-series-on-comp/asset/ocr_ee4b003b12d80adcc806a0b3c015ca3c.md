Figure 1.6 The architecture of the neuro-fuzzy system. The system has two-inputs, one output, and two rules. It is based on the WS.

+   - The second is the fuzzification layer. Here, the activation degrees α_ir of the antecedents are calculated. It is possible to distinguish the activation function f = e^{-net_ir^2} = α_ir where net_ir = x_i γ_ir - d_ir. Of course, d_ir = c_ir γ_ir. The weights that can be learned are γ_ir and d_ir. The total number of neurons is at maximum R × I.
+   - After, there is the inference layer. It is necessary to calculate the degree of truth of the R rules. It has R neurons and weights fixed to one.
+   - Lastly, there is the linear output layer in which the WS defuzzification is calculated. The weights that can be learned are z_or. The neurons are O. Also in the neuro-fuzzy system the SVD is used to find the best output singletons.

![](bbox=[0.12, 0.1, 0.88, 0.75])