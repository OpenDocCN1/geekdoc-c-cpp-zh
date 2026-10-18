rules to cover the training data D. The set of selected rules, including a default class, is then used as the classifier. The selection of rules is based on a total order defined on the rules in S. Given two rules, r_i and r_j, we say r_i > r_j or r_i precedes r_j or r_i has a higher precedence than r_j if

+   1. the confidence of r_i is greater than that of r_j, or
+   2. their confidences are the same, but the support of r_i is greater than that of r_j, or
+   3. both the confidences and supports of r_i and r_j are the same, but r_i is generated earlier than r_j.

A CBA classifier C is of the form:

C = < r1, r2, ..., rk, default - class > (5.10)

where r_i ∈ S, r_i > r_j if j > i. When classifying a test case, the first rule that satisfies the case will be used to classify it. If there is not a single rule that can be applied to the test case, it takes the default class, i.e., default - class, in Equation 5.10. A simplified version of the algorithm for building such a classifier is given in the following algorithm. The classifier is the RuleList.

# Algorithm CBA (T)

+   1. S = sort(S); // sorting is done according to the precedence >
+   2. RuleList = ∅ ; // the rule list classifier is initialized as empty set
+   3. For each rule r ∈ S in sequence do
+   4. If (D ≠ ∅) AND r classifies at least one example in D correctly Then
+   5. delete from D all training examples covered by r;
+   6. add r at the end of RuleList
+   7. EndIf
+   8. EndFor
+   9. add the majority class as the default class at the end of RuleList

In Algorithm CBA, we first sort all the rules in S according to their precedence defined above. Then we through the rules one by one, from the highest precedence to the lowest precedence, during the for-loop. Particularly, for each rule, we will perform sequential covering from step 3 to 8. Finally, we construct our RuleList by appending the majority class so that we can classify any test instance.

# Combine Multiple Rules: Like the first method Use the Strongest Rule, this method does not take any additional step to build a classifier. Instead, at the classification time, for each test instance, the system first searches a subset of rules that cover the instance.

+   1. If all the rules in the subset have the same class, then the class is assigned to the test instance.
+   2. If the rules have different classes, then the system divides the rules into a number of groups according to their classes, i.e., all rules of from the same class are in the same group. The system then compares the aggregated effects of the rule groups and finds the strongest group. Finally, the class label of the strongest group is assigned to the test instance.

To measure the strength of each rule group, there again can be many possible ways. For example, the CMAR system uses a weighted χ² measure [31].

# Class Association Rules as Features: In this method, rules are used as features to augment the original data or simply form a new data set, which is subsequently fed to a traditional classification algorithm, e.g., Support Vector Machines (SVM), Decision Trees (DT), Naïve Bayesian (NB), K-Nearest Neighbour (KNN), etc.

To make use of CARs as features, only the conditional part of each rule is needed. For each training and test instance, we will construct a feature vector where each dimension corresponds to a specific rule. Specifically, if a training or test instance in the original data satisfies the conditional