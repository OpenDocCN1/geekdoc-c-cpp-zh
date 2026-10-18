# Algorithm CAR-Apriori(T)

+   1. C₁ ← init-pass(T); // the first pass over T
+   2. F₁ ← {f | f ∈ C₁, f.rulesupCount / f.condsupCount ≥ minsup}; // n is the no. of transactions in T;
+   3. CAR₁ ← {f | f ∈ F₁, f.rulesupCount / n ≥ minconf}; // n is the no. of transactions in T;
+   4. For (k = 2; Fₖ₋₁ ≠ ∅; k++) do
+   5.   Cₖ ← CARcandidate-gen(Fₖ₋₁);
+   6.   For each transaction t ∈ T do
+   7.     For each candidate c ∈ Cₖ do
+   8.       If c.condset is contained in t then // c is a subset of t
+   9.         c.condsupCount ++;
+   10.        if t.class = c.class then
+   11.          c.rulesupCount ++;
+   12.      EndFor
+   13.  EndFor
+   14.  Fₖ ← {c ∈ Cₖ | c.rulesupCount / n ≥ minsup}
+   15.  CARₖ ← {f | f ∈ Fₖ, f.rulesupCount / f.condsupCount ≥ minconf};
+   16. EndFor
+   17. Output CAR ← ∪ₖ CARₖ.

One important observation regarding ruleitem generation is that if a ruleitem/rule has a confidence of 100%, then extending the ruleitem with more conditions, i.e., adding items to its condset, will also result in rules with 100% confidence although their supports may drop with additional items. In some applications, we may consider these subsequent rules with more conditions redundant because these additional conditions do not provide any more information for classification. As such, we should not extend such ruleitems in candidate generation for the next level (from k − 1 to k), which can reduce the number of generated rules significantly. Of course, if desired, redundancy handling procedure can be added in the CAR-Apriori algorithm easily to stop the unnecessary expanding process.

Finally, the CARcandidate-gen() function is very similar to the candidate-gen() function in the Apriori algorithm, and it is thus not included here. The main difference lies in that in CARcandidate-gen(), ruleitems with the same class label are combined together by joining their condsets.

We now give an example to illustrate the usefulness of CARs. Table 5.2 shows a sample loan application dataset from a bank, which has four attributes, namely Age, Has_job, Own_house, and Credit_rating. The first attribute Age has three possible values, i.e., young, middle, and old. The second attribute Has_Job indicates whether an applicant has a job, with binary values: true (has a job) and false (does not have a job). The third attribute Own_house shows whether an applicant owns a house (similarly, it has two values denoted by true and false). The fourth attribute, Credit_rating, has three possible values: fair, good, and excellent. The last column is the class/target attribute, which shows whether each loan application was approved (denoted by Yes) or not (denoted by No) by the bank.

Assuming the user-specified minimal support minsup = 2/15 = 13.3% and the minimal confidence minconf = 70%, we can mine the above dataset to find the following rules that satisfy the two constraints:
Own_house = false, Has_job = true → Class = Yes [sup=3/15, conf=3/3]
Own_house = true → Class = Yes [sup=6/15, conf=6/6]
Own_house = false, Has_job = true → Class = Yes [sup=3/15, conf=3/3]