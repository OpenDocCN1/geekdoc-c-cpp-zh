
3. Odds ratio: Odds ratio measures the odds of a sequence occurring in input-sequences labeled with some class c_i, normalized by the odds that it occurs in input-sequences labeled with some class other than c_i. If X is a sequence feature, P(X|c_i) denotes the probability that the sequence X occurs in class c_i, and P(X|\bar{c_i}) denotes the probability that the sequence X occurs in any class other than c_i, then the odds ratio of X can be computed by \frac{P(X|c_i)\cdot(1-P(X|\bar{c_i}))}{P(X|\bar{c_i})\cdot(1-P(X|c_i))}.

If the value of odds ratio is near 1, then the sequence X is a poor feature, as it is equally likely to occur in input-sequences of class c_i and also in input-sequences of classes other than c_i. An odds ratio greater (less) than 1 indicates that X is more (less) likely to occur in input sequences of class c_i than in input sequences of other classes; in that case X is a good feature. The odds ratio must be nonnegative if it is defined. It is undefined if the denominator is equal to 0.

Note that sometimes, we take the absolute value of the logarithm of odds ratio instead of odds-ratio. Then, for a poor feature, log-odds-ratio is a small number near 0, but for a good feature, it is a large positive number. To obtain a small subset of sequential features, we can simply rank the sequential features based on the log-odds-ratio, and consider a desired number of features according to the ranking.

Besides the above, there are other measures, such as Kullback-Leibler (K-L) divergence, Euclidean distance, feature-class entropy, etc., that can also be used for feature ranking.

## 14.4.2 Pattern Mining Framework for Mining Sequential Features

In the previous subsection, we considered a two-step scenario where a set of sequential features are mined first, and then, using filtering methods, a small set of features are selected. One of the drawbacks of this method is that it is inefficient, because a very large number of features are typically generated in the first step. Another drawback is that such methods consider each of the features independently, whereas many of the sequential features that are mined in the first step are actually highly correlated. If many of the selected features are highly correlated the performance of the classifier sometimes degrades. An alternative to the above two-step method is to unify the mining and feature selection in a single step. Lesh et al. [28] proposed such a method, named FEATUREMINE, which we describe below.

FEATUREMINE adapts a frequent sequence mining algorithm, called SPADE [55]; it takes a labeled dataset as input and mines features that are suited for sequence classification. For selecting good features it uses the following three heuristics that are domain-and-classifier independent:
- Features should be frequent (high support);
- Features should be distinctive of at least one class (high confidence);
- Feature sets should not contain redundant features.

The first of the above heuristics ensures that the chosen feature is not rare, otherwise, it will only be rarely useful for classifying unseen sequence instances. The second heuristic simply prefers features that are more accurate. The third heuristic reduces the size of the feature-set by ignoring a sequence that can be subsumed by one of its subsequence. If M(f, D) is the set of input-sequences in D that contain the feature f, a feature f1 subsumes a feature f2 with respect to predicting class c, if and only if M(f2, Dc) ⊆ M(f1, Dc) and M(f1, D¬c) ⊆ M(f2, D¬c).

FEATUREMINE accepts a labeled dataset D, along with parameters for minimum support (s), maximum length (l), maximum width (w), and returns feature set F such that for every feature fi and for any class cj, if length(fi) ≤ l and width(fi) ≤ w, and support(fi) ≥ s, and conf(fi → cj) is significantly greater than |Dc_j| / |D|, then either F contains fi, or F contains a feature that subsumes fi with respect to class cj in dataset D. FEATUREMINE prunes frequent patterns as it enumerates them using the SPADE algorithm by using several pruning rules:
- if the confidence of the pattern is 1.0, FEATUREMINE does not extend the pattern any further;
- if an item B appears in every event where item A occurs in every sequence in D, then any feature containing a set with both A and B will be subsumed by A only.

Authors show experimental results for naive Bayes, and

## 14.4.3 A Wrapper-Based Method for Mining Sequential Features

Kudenko and Hirsh [25] proposed a method called FGEN, for mining sequential patterns from string sequences. FGEN is conceptually similar to a wrapper method for feature selection. However, it is different than a wrapper feature selection method because the latter uses a holdout set for evaluating a feature subset, but FGEN uses the hold-out set for evaluating a single feature at any given iteration. Each of the features that FGEN generates is a macro-feature, i.e., they represent information containing more than a single subsequence. A feature F is a Boolean feature that is written as s1^n1 ∧ s2^n2 ∧ … ∧ sk^nk, where each of the si’s is a sequence (or substring), and each of the ni’s is an integer. For a given sequence S, the feature F is true if each of the si occurs at least ni times in the sequence S. For example, if F = AC^2 ∧ CB^3, then F(ACBBACBCB) = true, but F(ACBAC) = false. If a feature F is evaluated to true for a given sequence s, it is said that F subsumes s.

The FGEN algorithm consists of two main parts:
- feature building; and
- generalization.

Features are built incrementally, starting with a feature that corresponds to just a single example (seed) of the target class. Initially, the set of potential seeds consists of all the input sequences of the target class. At every iteration, the seed sequence is chosen from the potential seed-list, to be the one whose feature subsumes the greatest number of sequences remaining in the seed-list. Once a feature is chosen all the input sequences that are subsumed by the feature are removed from the seed-list. Thus, every iteration of feature generation builds a feature and removes a list of input sequences from the potential seed-list; the process continues until the potential seed-list is empty.

The seed feature generated from a seed sequence denotes the minimum frequency restrictions on all subsequences (up to some maximum length) of the seed sequences. For example, if the seed sequence is ABB, then the corresponding seed feature is defined as follows: F = A^1 ∧ B^2 ∧ AB^1 ∧ BB^1 ∧ ABB^1, where we consider all subsequences up to length 3. At every iteration, once a seed feature is generated, it is evaluated for accuracy against a holdout set and the feature is generalized to subsume at least one extra sequence in the seed-list. The generalization continues as long as the accuracy on the hold-out set increases, in a hill climbing fashion.

At the end of the feature building step, a dedicated generalization step is used to generalize each of the features (say, F) by decrementing a frequency restriction in F. Again, the holdout set is used to perform the generalization as long as the accuracy improves. Authors show that the number of features that FGEN finally keeps is small (typically around 50), and the performance of C4.5 (decision tree classifier) and Ripper is better with FGEN feature than a comprehensive list of features using all n-grams upto a given length.

## 14.5 Distance-Based Methods

Distance based classification methods compute a distance score between a pair of sequences, and then use those distances for classifying an unseen sequence. Typically, a distance based classification method is used in applications where a non-standard distance metric is required for achieving good classification performance. On many occasions, such metrics encode domain knowledge within the definition of the distance. For instance, while classifying protein sequences, a standard distance metric that considers each amino acid as an independent entity may not work well. This is due to the fact that a protein sequence may be composed of various functional domains, and two protein
