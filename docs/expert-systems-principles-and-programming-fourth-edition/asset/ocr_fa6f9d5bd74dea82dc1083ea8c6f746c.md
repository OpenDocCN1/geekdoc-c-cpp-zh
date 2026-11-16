In Table 4.12, the number of nodes is the total number in the model. Askable nodes are those that ask questions of the user to obtain observable evidence. The number of rules in the table are probabilistic inference rules. As you can see, there is much uncertainty in the models, and probability is important in supporting hypotheses.

| Model Name | Model Description | Number of Nodes | Number Askable | Number of Rules |
|---|---|---|---|---|
| PCD | Porphyry Copper | 200 | 97 | 135 |
| RFU | Roll-front Uranium | 185 | 147 | 169 |
| SPB | Sandstone-hosted Lead | 35 | 21 | 32 |

# Inference Networks

Each model for PROSPECTOR is encoded as a network of connections or relations between evidence and hypotheses. Thus, an inference net is a type of semantic net. Observable facts, such as the type of rock formations obtained from field exploration, compose the evidence to support the intermediate hypotheses. Groups of intermediate hypotheses are used to support the top-level hypothesis, which is what we want to prove. If it is not important to distinguish between evidence and hypotheses, the term assertion is used for either one. A small portion of the inference net for the top-level hypothesis of the porphyry copper model is shown in Figure 4.18.

The certainty factors CHE and CHNE in Figure 4.18 are used in PROSPECTOR because experience has shown that experts find it difficult to specify posterior probabilities or likelihood ratios. Similar experiences were found in the MYCIN system for diagnosing blood disease, where physicians did not like to specify probabilities, and certainty factors were used. As in MYCIN, certainty factors are ranked on an 11-point scale from –5 to +5 where –5 means "definitely not" and +5 means "definitely yes".

PROSPECTOR is not a pure probabilistic system because it uses fuzzy logic and certainty factors for combining evidence. Certainty factors and fuzzy logic will be discussed in more detail in Chapter 5.

Figure 4.19 shows the FRE node of Figure 4.18 expanded in more detail. This particular diagram has two numbers above nodes which are the likelihood ratio, LS, and necessity measure, LN, separated by commas. For example the LS, LN values for the node labeled RCIB at the left bottom is 20.1. The acronym of each node stands for its description, such as RCIB for "the region contains intrusive breccias." Also shown at the top of each node is the single number of the prior probability, such as 0.001 for RCIB.