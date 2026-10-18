![](bbox=[0.125, 0.115, 0.865, 0.395])

**FIGURE 15.1:** (a) An illustration of the common i.i.d. supervised learning setting. Here each instance is represented by a subgraph consisting of a label node (blue) and several local feature nodes (purple). (b) The same problem, cast in the relational setting, with links connecting instances in the training and testing sets, respectively. The instances are no longer independent. (c) A relational learning problem in which each node has a varying number of local features and relationships, implying that the nodes are neither independent nor identically distributed. (d) The same problem, with relationships (links) between the training and test set.

![](bbox=[0.231, 0.614, 0.844, 0.764])

**FIGURE 15.2:** Example BN for collective classification. Label nodes (green) determine features (purple), which are represented by a single vector-varied variable. An edge variable (yellow) is defined for all potential edges in the data graph. In (a), labels are determined by link structure, representing contagion. In (b), links are functions of labels, representing homophily. Both structures are acyclic.