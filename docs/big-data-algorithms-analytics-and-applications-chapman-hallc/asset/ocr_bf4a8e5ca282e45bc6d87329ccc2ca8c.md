![](bbox=[0.14, 0.11, 0.81, 0.38])

FIGURE 9.4 Selection of optimal k by self-tuned criterion for synthetic network.

network. The adjusted Rand index (ARI) [25] value is 0.999, which means that the community membership provided by the KSC methodology is as good as the original ground truth. If we put mod_sel = 'Self' in the demo script of Algorithm 3, then we perform the self-tuned model selection. It uses the concept of entropy and balance clusters to identify the optimal number of clusters k in the network. Figure 9.4 showcases the block diagonal affinity matrix S generated from the eigen-projections of the validation set using the self-tuned model selection procedure. From Figure 9.4, we can observe that there are seven blocks in the affinity matrix S. In order to calculate the number of these blocks, the self-tuned procedure uses the concept of entropy and balance together as an F-measure. Figure 9.4 shows that the F-measure is maximum for threshold t = 0.2, for which it takes the value 2.709. The number of clusters k identified corresponding to this threshold value is 7, which is equivalent to the number of ground truth communities.

# Algorithm 3: Demo Script for Synthetic Network Using BAF Criterion

```
Data:
netname = 'network'; //Name of the file and extension should be '.txt'
baseinfo = 1; //Ground truth exists
cominfo = 'community'; //Name of ground truth file and extension should be '.txt'
weighted = 0; //Whether a network is weighted or unweighted
frac_network = 15; //Percentage of network to be used as training and
maxk = 10; //maxk is maximum value of k to be used in eigen-decomposition, use
//maxk = 10 for k <= 10 else use maxk = 100
mod_sel = 'BAF'; //Method for model selection (options are 'BAF' or 'Self')
output = KS Cnet(netname,baseinfo,cominfo,weighted,frac_network,maxk,mod_sel);
```

```
Result
output = 1; //When community detection operation completes
netname_numclu_mod_sel.csv; //Number of clusters detected
netname_outputlabel.csv; //Cluster labels assigned to the nodes
netname_ARI.csv; //Valid only when ground truth is known, provides information
//about ARI and number of communities covered
```