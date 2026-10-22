![](bbox=[0.11, 0.11, 0.86, 0.48])

# Figure 4.4 Performance of the k-Nearest-Neighbour on the test and validation sets using as reference data base the training set.

of k. Due to noise in the data, the best performance was obtained for k = 1. The training of the networks was stopped using the test set (early stopping).

We remark that the FBF48 network got a better performance with respect to NR. Moreover, the average recognition time per pattern of the NR was .733 sec, while for the FBF48 network it was .004 sec. In addition, it can be observed that the generalization performances of the FBF10 network and the SFBF network were similar, while the SFBF network resulted to be faster in learning, in accordance with the lower complexity of the learning rules.

Finally, a significant improvement was obtained by the ESFBF with 20 rules (2 for each class). The training and test curves for this network are reported in Figure 4.5. It must be noted that the performance of this network was very close to the performance of the FBF network with 48 units, thus showing that the ESFBF networks, besides being much faster in training (i.e., it is comparable with a FBF with 10 rules), can reach generalization performances which are comparable to the ones obtained by more complex models.

In Figure 4.6, we have reported an histogram representing how many times a winning rule performs a correct classification after training. This histogram