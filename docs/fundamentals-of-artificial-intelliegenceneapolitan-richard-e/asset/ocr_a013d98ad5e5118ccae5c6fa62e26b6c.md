# Table 11.5 Performance of the ID3 Algorithm in a Chess Domain

| Training Set Size | Fraction of Entire Universe | Errors in 10,000 trials |
|---|---|---|
| 200 | .0001 | 199 |
| 1000 | .0007 | 33 |
| 5000 | .0036 | 8 |
| 25,000 | .0179 | 6 |
| 125,000 | .0893 | 2 |

The global call to function Addnode is as follows:

```
root_of_tree = Addnode(datafile, set_of_predictors);
```

where datafile contains all the records and set_of_predictors contains all the predictors.

Although the ID3 Algorithm produces a parsimonious decision tree, the question remains as the whether the resultant tree performs well at classifying new instances. Quinlan [1983] evaluated the performance of ID3 on the problem of learning to classify boards in a chess-related game. The game involved white versus black, where white played with a king and a rook, and black played with a king and a knight. The goal was to learn to recognize boards that would lead to a loss for black within three moves. The predictors consisted of 23 properties of the board such as “there is an inability to move the king safely.” There were 1,400,000 possible boards, of which 474,000 led to a loss for black within three moves. Results of the evaluation appear Table 11.5.

# 11.3.3 Overfitting

As discussed in Section 11.2.3, overfitting can occur when we learn a model from data. In the case of learning a decision tree, we can address overfitting by pruning the tree after learning it. Quinlan [1987] introduced several methods for pruning decision trees including Reduced Error Pruning, which we discuss next.

When we prune a node from a decision tree, we replace the node by the most common-occurring value of the target at that node. For example, suppose we are pruning the node on the branch labeled sunny that is a child of Outlook in the tree in Figure 11.4. Suppose further that we are pruning using the data file in Table 11.4. Of the 6 records that have Outlook equal to sunny, 5 have Activity equal to tennis. Therefore if we pruned the node labeled Temp that touches the edge labeled sunny, we would replace node Temp by a node labeled tennis.

In Reduced Error Pruning, the data set is partitioned into a training set and a test set. We learn a decision tree from the training set using an algorithm such as ID3, and then prune the tree using the test set. This is done by first determining the predictive accuracy of the tree for the test set. Next we