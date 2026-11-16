# Figure 12.2 Decision Tree with Multiple Branches

![](bbox=[0.046, 0.076, 0.856, 0.335])

# Decision Trees That Learn

Occasionally it is useful to add new knowledge to a decision tree as it is learned, as in the commonly used example of the animal identification decision tree. Once the decision tree has reached an answer, it asks whether the answer is correct, and if so, then nothing more is done. If the answer is incorrect, however, the decision tree is modified to accommodate the correct answer. The answer node is replaced with a decision node that contains a question that will differentiate between the old answer that was at the node and the answer that was not correctly guessed. Figure 12.3 shows a decision tree that will classify an animal by characteristics. This decision tree is somewhat naive (it knows only three animals) and is in need of learning.

# Figure 12.3 Animal Identification Decision Tree

![](bbox=[0.056, 0.7, 0.856, 0.945])