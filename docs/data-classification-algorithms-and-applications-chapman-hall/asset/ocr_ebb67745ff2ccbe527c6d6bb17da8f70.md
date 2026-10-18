**TABLE 4.2: Summary of Notation for Data and Partitions**

| Symbol | Definition |
|---|---|
| **X** | set of all training data = {X₁, …, Xₙ} |
| **A** | set of attributes = {A₁, …, A_d} |
| **Y** | domain of class values = {y₁, …, y_m} |
| *Xᵢ* | a subset of X |
| *S* | a splitting rule |
| **Xₛ** | a partitioning of **X** into {X₁, …, Xₖ} |

A partitioning rule *S* subdivides data set **X** into a set of subsets collectively known as **Xₛ**; that is, **Xₛ** = {X₁, X₂, …, Xₖ} where ⋃ᵢXᵢ = **X**. A decision tree is a rooted tree in which each set of children of each parent node corresponds to a partitioning (**Xₛ**) of the parent’s data set, with the full data set associated with the root. The number of items in *Xᵢ* that belong to class *yⱼ* is |Xᵢⱼ|. The probability that a randomly selected member of *Xᵢ* is of class *yⱼ* is pᵢⱼ = |Xᵢⱼ| / |Xᵢ|.

The remainder of the chapter is organized as follows. Section 4.2 describes the operation of classical top-down decision tree induction. We break the task down into several subtasks, examining and comparing specific splitting and pruning algorithms that have been proposed. Section 4.3 features case studies of two influential decision tree algorithms, C4.5 [66] and CART [8]. Here we delve into the details of start-to-finish decision tree induction and prediction. In Section 4.4, we describe how data summarization and parallelism can be used to achieve scalability with very large datasets. Then, in Section 4.5, we introduce techniques and algorithms that enable incremental tree induction, especially in the case of streaming data. We conclude with a review of the advantages and disadvantages of decision trees compared to other classification methods.

# 4.2  Top-Down Decision Tree Induction

The process of learning the structure of a decision tree, to construct the classifier, is called decision tree induction [63]. We first describe the classical approach, top-down selection of partitioning rules on a static dataset. We introduce a high-level generic algorithm to convey the basic idea, and then look deeper at various steps and subfunctions within the algorithm.

The decision tree concept and algorithm can be tracked back to two independent sources: AID (Morgan and Sonquist, 1963) [56] and CLS in *Experiments in Induction* (Hunt, Marin, and Stone, 1966) [34]. The algorithm can be written almost entirely as a single recursive function, as shown in Algorithm 4.1. Given a set of data items, which are each described by their attribute values, the function builds and returns a subtree. The key subfunctions are shown in small capital letters. First, the function checks if it should stop further refinement of this branch of the decision tree (line 3, subfunction STOP). If so, it returns a leaf node, labeled with the class that occurs most frequently in the current data subset X′. Otherwise, it proceeds to try all feasible splitting options and selects the best one (line 6, FINDBESTSPLITTINGRULE). A splitting rule partitions the dataset into subsets. What constitutes the “best” rule is perhaps the most distinctive aspect of one tree induction algorithm versus another. The algorithm creates a tree node for the chosen rule (line 8).

If a splitting rule draws all the classification information out of its attribute, then the attribute is exhausted and is ineligible to be used for splitting in any subtree (lines 9–11). For example, if a discrete attribute with *k* different values is used to create *k* subsets, then the attribute is “exhausted.”