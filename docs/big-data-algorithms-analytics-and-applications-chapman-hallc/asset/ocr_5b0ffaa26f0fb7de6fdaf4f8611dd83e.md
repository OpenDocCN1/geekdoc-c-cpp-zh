# Algorithm 4: Demo Script for YouTube Network Using BAF Criterion

# Data:

```
netname = 'youtube_mod';    //Name of the file and extension should be '.txt'
baseinfo = 0;    //Ground truth does not exists
cominfo = [];    //No ground truth file so empty set as input
weighted = 0;    //Whether a network is weighted or unweighted
frac_network = 10;    //Percentage of network to be used as training and
                      //validation set
maxk = 100;    //maxk is maximum value of k to be used in eigen-decomposition,
               //use maxk = 10 for k < 10 else use maxk = 100
mod_sel = 'BAF';    //Method for model selection (options are 'BAF' or 'Self')
output = KSCnet(netname,baseinfo,cominfo,weighted,frac_network,maxk,mod_sel);
```

# Result:

```
output = 1;    //When community detection operation completes
netname_numclu_mod_sel.csv;    //Number of clusters detected
netname_outputlabel.csv;    //Cluster labels assigned to the nodes
```

# 9.4 CONCLUSION

In this chapter, we gave a practical exposition of a methodology to perform community detection for Big Data networks. The technique was built on the concept of spectral clustering and referred to as KSC. The core concept was to build a model on a small representative subgraph that captured the inherent community structure of the large-scale network. The subgraph was obtained by the FURS [2] selection technique. Then, the KSC model was built on this subgraph. The model parameters were obtained by one of the two techniques: (1) BAF criterion or (2) self-tuned technique. The KSC model has a powerful out-of-sample extensions property. This property was used for community affiliation of previously unseen nodes in the Big Data network. We also explained and demonstrated the usage of the KSC-net software, which uses the KSC methodology as the underlying core concept.

# ACKNOWLEDGMENTS

EU: The research leading to these results has received funding from the European Research Council under the European Union’s Seventh Framework Programme (FP7/2007-2013)/ ERC AdG A-DATADRIVE-B (290923). This chapter reflects only the authors’ views; the Union is not liable for any use that may be made of the information contained. Research Council KUL: GOA/10/09 MaNet, CoE PFV/10/002 (OPTEC), BIL12/11T; PhD/postdoc grants. Flemish government—FWO: projects G.0377.12 (structured systems), G.088114N (tensor-based data similarity); PhD/postdoc grants. IWT: project SBO POM (100031); PhD/postdoc grants. iMinds Medical Information Technologies: SBO 2014. Belgian Federal Science Policy Office: IUAP P7/19 (DYSCO, dynamical systems, control and optimization, 2012–2017).