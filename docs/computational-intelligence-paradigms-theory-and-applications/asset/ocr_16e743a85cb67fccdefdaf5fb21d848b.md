![](bbox=[0.397, 0.096, 0.638, 0.381])

**FIGURE 9.10:** Architecture Design for Evolutionary Design of Neuro-Fuzzy Systems

**TABLE 9.1:** Performance of NF systems and ANN

| System | Epochs | RMSE |
|---|---:|---:|
| ANFIS | 75 | 0.0017 |
| NEFPROX | 216 | 0.0332 |
| EFuNN | 1 | 0.0140 |
| DmEFuNN | 1 | 0.0042 |
| SONFIN | — | 0.0180 |

process of FALCON, GARIC, ANFIS, NEFCON, SONFIN, FINEST and FUN are only concerned with parameter level adaptation within fixed structures and hence it is suitable only for small problems. The learning process and the determination of the rule base in large scale problems is complicated. In such a case the systems expects the user to provide the architecture details, type of fuzzy operators, etc. An important feature of EFuNN and DmEFuNN is the one pass (epoch) training, which is highly capable for online learning. As the problem becomes more complicated manual definition of NF architecture/parameters becomes complicated.

More specifically, for processes that require an optimal NF system, the evolutionary design approach seems to be the best solution. Table 9.1 provides a comparative performance of some Neuro-Fuzzy systems, where training was performed on 500 data sets and NF models were tested with another 500 data sets.