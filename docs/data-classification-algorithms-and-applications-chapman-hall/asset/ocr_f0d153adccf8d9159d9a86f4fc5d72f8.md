Among all the candidate conjuncts of all the attributes, we choose the conjunct with the highest probabilistic information gain, which is defined as Definition 1, as the best conjunct of R, and then add it to R.

# Definition 1. Let R′ be a rule by adding a conjunct to R. The probabilistic information gain between R and R′ over the interval or split point related to this conjunct is

```
ProbInfo(R,R′) = PC⁺(R′) · [ log₂ PC⁺(R′)/(PC⁺(R′)+PC⁻(R′)) − log₂ PC⁺(R)/(PC⁺(R)+PC⁻(R)) ]. (16.1)
```

From Definition 1, we can see that the probabilistic information gain is proportional to PC⁺(R′) and PC⁺(R′)/(PC⁺(R′)+PC⁻(R′)), so it prefers rules that have high accuracies.

# 2. Rule Pruning Phase.

After extracting a rule from grow_Dataset, we have to conduct pruning on it because it may perform well on grow_Dataset, but it may not perform well in the test phase. So we should prune some conjuncts of it based on its performance on the validation set prune_Dataset. For a given rule R in the pruning phase, uRule starts with its most recently added conjuncts when considering pruning. For each conjunct of R’s condition, we consider a new rule R′ by removing it from R. Then we use R′ and R to classify the prune_Dataset, and get the set of positive instances and the set of negative instances of them. If the proportion of positive instances of R′ is larger than that of R, it means that the accuracy can be improved by removing this conjunct, so we remove this conjunct from R and repeat the same pruning steps on other conjuncts of R, otherwise we keep it and stop the pruning.

# 3. Classification Phase.

Once the rules are learnt from the training dataset, we can use them to classify unlabeled instances. In traditional rule-based classifications such as RIPPER [12], they often use the first rule that covers the instance to predict the label. However, an uncertain data object may be covered by several rules, and so we have to consider the weight of an object covered by different rules (conceptually, the weight here is the probability that an instance is covered by a rule; for details, please read [25]), and then assign the class label of the rule with the highest weight to the instance.

# Discussions:

The algorithm uRule follows the basic framework of the traditional rule-based classification algorithm RIPPER [12]. It extracts rules from one class at a time by the Learn_One_Rule procedure. In the Learn_One_Rule procedure, it splits the training dataset into grow_Dataset, and prune_Dataset, generates rules from grow_Dataset and prunes rules based on prune_Dataset. To choose the best conjunct when generating rules, uRule proposes the concept of probability cardinality, and uses a measure called probabilistic information gain, which is based on probability cardinality, to choose the best conjunct for a rule. In the test phase, since a test object may be covered by one or several rules, uRule has considered the weight of coverage for final classification. Their experimental results show that this method can achieve relative stable accuracy even though the extent of uncertainty reaches 20%. So it is very robust in cases which contain large ranges of uncertainty.

# 16.3.3 Associative Classification

# Overview:

Associative classification is based on frequent pattern mining. The basic idea is to search for strong associations between frequent patterns (conjunctions of a set of attribute-value pairs) and class labels [17]. A strong association is generally expressed as a rule in the form p1 ∧ p2 ∧ ⋯ ∧ ps ⇒ ck, called association rule, where the rule consequent ck ∈ C is a class label. Typical associative classification algorithms are, for example, CBA [21], CMAR [22], and HARMONY [35]. Strong associations are usually detected by identifying patterns covering a set of attribute-value pairs and a class label associated with this set of attribute-value pairs that frequently appear in a given database.