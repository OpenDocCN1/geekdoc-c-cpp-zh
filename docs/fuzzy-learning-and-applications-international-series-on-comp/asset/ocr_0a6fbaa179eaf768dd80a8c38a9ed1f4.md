# 6.3.4 Parameter Adjustment

The initial fuzzy labels assigned to a linguistic variable are not entirely capable of incorporating the human experience into the fuzzy if-then rules. Obviously, a designer, with experience, can produce a membership function which suits a particular situation. However, this is explicitly excluded here, as the experience by the designer in handcrafting the membership functions for one system does not in general carry over to the design of another system. A learning ability for membership functions in fuzzy systems can make the incorporation between the membership functions of fuzzy rules and human experience more effective.

For a given fuzzy system, it is obvious that altering the following parameters will affect the overall input-output mapping of the system.

+   1. The membership function of linguistic values,
+   2. Fuzzy reasoning methods,
+   3. The number of rules.

Assignment of a membership function to each fuzzy value is, in general, non-unique. However, there has been some research for giving a systematic approach in this direction [4, 24]. It depends, to a certain extent, on the designer in the choice of the membership functions, as well as the interpretation of the “fuzziness” of the variables concerned. Altering the membership functions has a dominant effect on the other two (fuzzy reasoning and number of rules). It can be seen that for a fixed number of rules in the rule set, changing the membership function can achieve the same input-output mapping, to a particular degree of approximation, regardless of the fuzzy reasoning method. Alternatively, for a fixed fuzzy reasoning method, we can attain to the same degree of approximation, the same input-output mapping with a different number of rules and different membership functions.

In the next section the gradient-descent or backpropagation algorithm which is also used for neural networks is employed to adapt the parameters of a fuzzy system.

# 6.4 Learning Rule

If the correct output, corresponding to a particular set of inputs to a fuzzy system, is known, then it is possible to adjust the free parameters of a fuzzy system by means of error backpropagation. The method by which this is done is the same as the way that multilayer perceptron are trained, that is:

+   1. For each known input/output relation, a cost, J, is calculated by: