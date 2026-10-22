
![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_224_0.png)

# Figure 6.4 Neural network representation of a fuzzy system with 2 inputs, 3 membership functions for each input, 9 rules and 1 output

linguistic information. That is, one would like to be able to use the same intuitive understanding, which was used to create the fuzzy system, to interpret its behaviour at all times in the future. In general, this ideal cannot be guaranteed in a learning fuzzy system.

A neuro-fuzzy model is built using a multilayer neural network and it has a total of five layers [14]. A neuro-fuzzy model with two inputs and a single output is considered here for convenience and it is shown in Figure (6.4). Accordingly, there are two nodes in layer 1 and one node in layer 5. Nodes in layer 1 are input nodes that directly transmit input signals to the next layer. Layer 5 is the output layer. Nodes in layer 2 and 4 are “term nodes” and they act as membership functions to express the fuzzy values of linguistic variables. Each node of layer 3 is a “rule node” and represents a single fuzzy rule [6]. In total, there are K1 × K2 nodes in layer 3. K1 and K2 are the number of individual membership functions for each input.

## 6.3.4 Parameter Adjustment

The initial fuzzy labels assigned to a linguistic variable are not entirely capable of incorporating the human experience into the fuzzy if-then rules. Obviously, a designer, with experience, can produce a membership function which suits a particular situation. However, this is explicitly excluded here, as the experience by the designer in handcrafting the membership functions for one system does not in general carry over to the design of another system. A learning ability for membership functions in fuzzy systems can make the incorporation between the membership functions of fuzzy rules and human experience more effective.

For a given fuzzy system, it is obvious that altering the following parameters will affect the overall input-output mapping of the system.

- 1. The membership function of linguistic values,
- 2. Fuzzy reasoning methods,
- 3. The number of rules.

Assignment of a membership function to each fuzzy value is, in general, non-unique. However, there has been some research for giving a systematic approach in this direction [4, 24]. It depends, to a certain extent, on the designer in the choice of the membership functions, as well as the interpretation of the “fuzziness” of the variables concerned. Altering the membership functions has a dominant effect on the other two (fuzzy reasoning and number of rules). It can be seen that for a fixed number of rules in the rule set, changing the membership function can achieve the same input-output mapping, to a particular degree of approximation, regardless of the fuzzy reasoning method. Alternatively, for a fixed fuzzy reasoning method, we can attain to the same degree of approximation, the same input-output mapping with a different number of rules and different membership functions.

In the next section the gradient-descent or backpropagation algorithm which is also used for neural networks is employed to adapt the parameters of a fuzzy system.

## 6.4 Learning Rule

If the correct output, corresponding to a particular set of inputs to a fuzzy system, is known, then it is possible to adjust the free parameters of a fuzzy system by means of error backpropagation. The method by which this is done is the same as the way that multilayer perceptron are trained, that is:

- 1. For each known input/output relation, a cost, J, is calculated by:

J = 1/2 ε² (6.5)

where ε = y_d − y, y_d is desired (i.e., known) output, and y is the output of the fuzzy system.

2. The partial derivatives, ∂J/∂c_j,k, ∂J/∂σ_j,k, and ∂J/∂B_i for each of the free parameters, are calculated using the chain-rule; they are:

∂J/∂B_i = − ε f^i / Σ_{t=1}^n f^t (6.6)

∂J/∂c_j,k = − 2ε(x_j − c_j,k)[ Σ_{i=1}^n d_i,j,k f^i(B^i − y)] / [(σ_j,k)^2 Σ_{i=1}^n f^i] (6.7)

∂J/∂σ_j,k = − 2ε(x_j − c_j,k)^2[ Σ_{i=1}^n d_i,j,k f^i(B^i − y)] / [(σ_j,k)^3 Σ_{i=1}^n f^i] (6.8)

where d_i,j,k is 1 if the i-th rule is dependent on the k-th membership function of the j-th input or 0 if it is not dependent.

3. The free parameters B^i, c_j,k, and σ_j,k are then adjusted by:

B_i' = B_i − η ∂J/∂B_i (6.9)

c_j,k' = c_j,k − η ∂J/∂c_j,k (6.10)

σ_j,k' = σ_j,k − η ∂J/∂σ_j,k (6.11)

where B_i', c_j,k', and σ_j,k' are the new values of the free parameters and η is the “learning rate” which determines the size of the adjustments made.

### 6.4.1 Example 3: Learning Fuzzy Systems

Consider the example 1 presented in section 6.3. Following the training algorithm explained in the previous section, the result of function approximation for the given non-linear input-output data after 150 epochs of training is depicted in Figure (6.6). The learning rate, η, was 0.01. The final membership functions after training is depicted in Figure(6.7).

Allowing the membership functions to change can violate the interpretation in that the meaning initially assigned to the linguistic values can be lost. This

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_228_0.png)

# Figure 6.6 Function approximation with a learning fuzzy system after N=150 epochs training.

danger is evident, if the initial membership functions given in Figure (6.2) are contrasted with the membership functions after training. In Figure (6.7) membership function Ã¹ has moved to the right and Ã³ is completely contained within Ã².

## 6.5 Interpretation Preservation

If allowed to adapt freely, the membership functions of a learning fuzzy system may lose the meaning which was initially assigned to them. They may change their relative positions such that, for example, “low” may become greater than “high”, or the range of their activations may become excessively wide or narrow [7, 11, 12, 28].

Although the adapted membership functions may have attained a new significance, after the original meaning has been lost, it may be very difficult or

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_229_0.png)

# Figure 6.7 Membership functions Ãⁱ: i = 1, 2, 3, 4, 5 after N = 150 epochs training without constraints.

otherwise undesirable to interpret this. In some cases a learning fuzzy system may have changed to such a degree that a conventional linguistic interpretation is no longer possible. In such a case, the learning fuzzy system may be viewed as a “black box” function approximator similar in function to a neural network. All these possibilities make a conventional learning fuzzy system unsuitable for many industrial applications in which maintainability and reliability are of importance, despite their likely performance superiority.

### 6.5.1 Constraint Learning

In [16], a constrained training algorithm, which maintains the interpretation of learning fuzzy system during training, is proposed. It is a paradigm which will enable the learning fuzzy controller to adapt and optimise itself while still remaining conceptually comprehensible to a human expert. This may be achieved at the cost of a slight degradation of the performance of the learning fuzzy system, in the sense that the error function may attain a higher value than if the membership functions are allowed to adapt freely. In most cases, this trade-off is acceptable, as it is often more important to be able to interpret the behaviour of the learning fuzzy system than to achieve a lower minimum in the cost function.

The membership function assigned to a fuzzy value should not exceed certain

maximum and minimum limits of fuzziness after adaptation. If the similarity between the initial membership function and the membership function during training is measured, when the similarity measure exceeds its limit, the linguistic meaning assigned to the membership function is said to be lost.

### 6.5.2 Constraint Learning Rule

Consider the updating rules given in Equations (6.6-6.8). They can be modified for constraint learning by updating the parameters after each iteration using the following update rule.

B'_i = B_i - η ∂J/∂B_i × ℛ_{B_i} (6.12)
c'_{j,k} = c_{j,k} - η ∂J/∂c_{j,k} × ℛ_{c_{j,k}} (6.13)
σ'_{j,k} = σ_{j,k} - η ∂J/∂σ_{j,k} × ℛ_{σ_{j,k}} (6.14)

The restriction functions, ℛ_σ, ℛ_c and ℛ_B, are introduced to limit the freedom of updating the parameters and they are governed by the following equations.

ℛ_σ = 1/(1 + e^{-(σ-σ̲)/ν_σ}) - 1/(1 + e^{-(σ-σ̄)/ν_σ}) (6.15)
ℛ_c = 1/(1 + e^{-(c- c̲)/ν_c}) - 1/(1 + e^{-(c- c̄)/ν_c}) (6.16)
ℛ_B = 1/(1 + e^{-(B- B̲)/ν_B}) - 1/(1 + e^{-(B- B̄)/ν_B}) (6.17)

where ν_σ, ν_c and ν_B are respectively dispersion parameters of σ, c and B. These are introduced so that a “gentle roll off” is achieved. As the parameters approach their predefined maximum and minimum limits, smaller and smaller updates are performed. By controlling the parameter ν, this can be controlled.

Hence, regardless of whether or not a minimum solution for the cost function, J, is achieved or not, the restriction bounds do not permit the free parameters to move beyond the defined limits. It preserves the interpretation at the possible expense of yielding a less optimal solution.

## 6.5.3 Example 4: Interpretation Preservation of Learning Fuzzy Systems
