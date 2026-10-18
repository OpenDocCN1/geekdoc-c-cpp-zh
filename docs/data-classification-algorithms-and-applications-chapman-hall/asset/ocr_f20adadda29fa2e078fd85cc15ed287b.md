# 11.2.2 Information Gain

Another related measure that is commonly used for text feature selection is that of information gain or entropy. Let P_i be the global probability of class i, and p_i(w) be the probability of class i, given that the document contains the word w. Let F(w) be the fraction of the documents containing the word w. The information gain measure I(w) for a given word w is defined as follows:

I(w) = -∑_{i=1}^k P_i · log(P_i) + F(w) · ∑_{i=1}^k p_i(w) · log(p_i(w)) + +(1 - F(w)) · ∑_{i=1}^k (1 - p_i(w)) · log(1 - p_i(w)).

The greater the value of the information gain I(w), the greater the discriminatory power of the word w. For a document corpus containing n documents and d words, the complexity of the information gain computation is O(n · d · k).

# 11.2.3 Mutual Information

This mutual information measure is derived from information theory [37], and provides a formal way to model the mutual information between the features and the classes. The pointwise mutual information M_i(w) between the word w and the class i is defined on the basis of the level of co-occurrence between the class i and word w. We note that the expected co-occurrence of class i and word w on the basis of mutual independence is given by P_i · F(w). The true co-occurrence is of course given by F(w) · p_i(w). In practice, the value of F(w) · p_i(w) may be much larger or smaller than P_i · F(w), depending upon the level of correlation between the class i and word w. The mutual information is defined in terms of the ratio between these two values. Specifically, we have:

M_i(w) = log( (F(w) · p_i(w)) / (F(w) · P_i) ) = log( p_i(w) / P_i ). (11.5)

Clearly, the word w is positively correlated to the class i, when M_i(w) > 0, and the word w is negatively correlated to class i, when M_i(w) < 0. We note that M_i(w) is specific to a particular class i. We need to compute the overall mutual information as a function of the mutual information of the word w with the different classes. These are defined with the use of the average and maximum values of M_i(w) over the different classes.

M_avg(w) = ∑_{i=1}^k P_i · M_i(w)
M_max(w) = max_i {M_i(w)}.

Either of these measures may be used in order to determine the relevance of the word w. The second measure is particularly useful, when it is more important to determine high levels of positive correlation of the word w with any of the classes.

# 11.2.4 χ²-Statistic

The χ² statistic is a different way to compute the lack of independence between the word w and a particular class i. Let n be the total number of documents in the collection, p_i(w) be the conditional probability of class i for documents that contain w, P_i be the global fraction of documents containing the class i, and F(w) be the global fraction of documents that contain the word w. The χ²-statistic of the word between word w and class i is defined as follows:

χ_i²(w) = [n · F(w)² · (p_i(w) - P_i)²] / [F(w) · (1 - F(w)) · P_i · (1 - P_i)] (11.6)