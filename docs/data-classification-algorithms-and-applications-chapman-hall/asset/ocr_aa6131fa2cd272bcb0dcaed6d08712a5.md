Finally, we count the frequency of {Chicken, Clothes, Milk} in database and it is stored in F3 given that its support is greater than the minimal support.

F3: {{Chicken, Clothes, Milk}:3}.

Note that since we only have one itemset in F3, the algorithm stops since we need at least two itemsets to generate a candidate itemset for C4. Apriori algorithm is just a representative of a large number of association rule mining algorithms that have been developed over the last 20 years. For more algorithms, please see [19].

# STEP2: Association Rule Generation

As we mentioned earlier, the Apriori algorithm can generate all frequent itemsets as well as all confident association rules. Interestingly, generating association rules is fairly straightforward compared with frequent itemset generation. In fact, we generate all association rules from frequent itemsets. For each frequent itemset f, we use all its non-empty subsets to generate association rules. In particular, for each such subset β, β ⊆ f, we output a Rule 5.5 if the confidence condition in Equation 5.6 is satisfied.

(f − β) → β, (5.5)

confidence = f.count / (f − β).count ≥ minconf (5.6)

Note the f.count and (f − β).count are the supports count of itemset f and itemset (f − β), respectively. According to Equation 5.3, our rule support is f.count / n, where n is the total number of transactions in the transaction set T. Clearly, if f is frequent, then any of its non-empty subsets is also frequent according to the downward closure property. In addition, all the support counts needed for confidence computation in Equation 5.6, i.e., f.count and (f − β).count, are available as we have recorded the supports for all the frequent itemsets during the mining process, e.g., using the Apriori algorithm. As such, there is no additional database scan needed for association rule generation.

# 5.3.2 Mining Class Association Rules

The association rules mined using Apriori algorithm are generic and flexible. An item can appear as part of the conditions or as part of the consequent in a rule. However, in some real-world applications, users are more interested in those rules with some fixed target items (or class labels) on the right-hand side. Obviously, such kinds of rules are very useful for our rule-based classification models.

For example, banks typically maintain a customer database that contains demographic and financial information of individual customers (such as gender, age, ethnicity, address, employment status, salary, home ownership, current loan information, etc) as well as the target features such as whether or not they repaid the loans or defaulted. Using association rule mining technique, we can investigate what kinds of customers are likely to repay (good credit risks) or to default (bad credit risks) — both of them are target feature values, so that banks can reduce the rate of loan defaults if they can predict those customers who are likely to default in advance based on their personal demographic and financial information. In other words, we are interested in a special set of rules whose consequents are only those target features — these rules are called class association rules (CARs) where we require only target feature values to occur as consequents of rules, although the conditions can be any items or their combinations from financial and demographic information.

Let T be a transaction data set consisting of n transactions. Each transaction in T has been labeled with a class y (y ∈ Y; Y is the set of all class labels or target features/items). Let I be the set of all items in T, and I ∩ Y = ∅. Note here we treat the label set Y differently from the standard