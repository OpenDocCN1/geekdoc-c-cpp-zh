The basic algorithm for the detection of such rules works as follows: Given a collection of attribute-value pairs, in the first step the algorithm identifies the complete set of frequent patterns from the training dataset, given the user-specified minimum support threshold and/or discriminative measurements like the minimum confidence threshold. Then, in the second step a set of rules are selected based on several covering paradigms and discrimination heuristics. Finally, the rules for classification extracted in the first step can be used to classify novel database entries or for training other classifiers. In many studies, associative classification has been found to be more accurate than some traditional classification algorithms, such as decision tree, which only considers one attribute at a time, because it explores highly confident associations among multiple attributes.

In the case of uncertain data, specialized associative classification solutions are required. The work called HARMONY proposed in [35] has been extended for uncertain data classification in [16], which is called uHARMONY. It efficiently identifies discriminative patterns directly from uncertain data and uses the resulting classification features/rules to help train either SVM or rule-based classifiers for the classification procedure.

# Input: A set of labeled objects whose uncertain attributes are associated with pmf models.

# Algorithm: uHARMONY follows the basic framework of algorithm HARMONY [35]. The first step is to search for frequent patterns. Traditionally an itemset y is said to be supported by a tuple xi if y ⊆ xi. For a given certain database D consisting of n tuples x1,x2,⋯,xn. The label of xi is denoted by ci. {xi|xi ⊆ D ∧ y ⊆ xi} is called the support of itemset y with respect to D, denoted by supy. The support value of itemset y under class c is defined as |{xi|ci = c ∧ xi ⊆ D ∧ y ⊆ xi}|, denoted by supy^c. y is said to be frequent if supy ≥ supmin, where supmin is a user specified minimum support threshold. The confidence of y under class c can be defined as confy^c = supy^c / supy.

However, for a given uncertain database, there exists a probability of y ⊆ xi when y contains at least one item of uncertain attribute, and the support of y is no longer a single value but a probability distribution function instead. uHARMONY defines pattern frequentness by means of the expected support and uses the expected confidence to represent the discrimination of found patterns.

# 1. Expected Confidence. For a given itemset y on the training dataset, its expected support E(supy) is defined as E(supy) = Σ_{i=1}^n P(y ⊆ xi). Its expected support on class c is defined as E(supy^c) = Σ_{i=1}^n (P(y ⊆ xi) ∧ ci = c). Its expected confidence can be defined as Definition 1.

# Definition 1. Given a set of objects and the set of possible worlds W with respect to it, the expected confidence of an itemset y on class c is

```
E(conf_y^c) = Σ_{w_i ∈ W} conf_{y,w_i}^c × P(w_i) = Σ_{w_i ∈ W} [sup_{y,w_i}^c / sup_{y,w_i}] × P(w_i)   (16.2)
```

where P(wi) stands for the probability of world wi; conf_{y,wi}^c is the confidence of y on class c in world wi, while sup_{y,wi} (sup_{y,wi}^c) is the support of x (on class c) in world wi.