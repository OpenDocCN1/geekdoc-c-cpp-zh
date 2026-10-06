# Box 3.5 Composite protein sequence databases

Although choice is usually a good thing, the abundance of databases can also complicate matters. Faced with a range of resources that contain similar information and do similar things, a user will want to know which is the most comprehensive or the most up-to-date - in short, which is the best to use. One to the proliferation of databases is to aggregate resources into a composite, removing much of the redundancy in order to make data storage and searching more efficient. Over the years, researchers saw the advantages of aggregating databases, which in turn gave to several composites, with different format and redundancy criteria. Today, the main composite protein sequence resources are the NCBI's non-redundant NRDB, and the EBI's UniProtKB, their data sources are listed in the Table 3.7.

# Table 3.7

Comparison of the contents of the NRDB and UniProtKB databases.

| NRDB | UniProtKB |
|---|---|n| GenBank CDS translations | Swiss-Prot |
| PDB | TrEMBL |
| Swiss-Prot | PIR-PSD |
| PIR-PSD | |
| PRF | |

The availability of different databases begs the same questions: which is best, which is the most comprehensive, which is the most-to-date, which should be used? In practice, the choice is determined largely by the task at hand, and what we care about, searching or more about the most comprehensive search. Although databases offer various advantages, such as efficiency of searching, more intelligible search, outputs (uncomplicated to the same sequence) and so on, they also have details. Much depends on how a composite is made, the level of redundancy it contains and its error rate. A database built by eliminating identical sequences within and between its sources will guarantee that copies of the same sequence aren't included (and hence interrogated or searched twice when users query the resource). This scenario is shown in Figure 3.10 for two databases (left-hand side and centre). The resulting non-identical composite (right) is smaller than the sum of the contents of its sources, because it has eliminated duplicate sequences (those denoted by the black, white and primary colours).

![](bbox=[0.153, 0.626, 0.823, 0.836])

Figure 3.10
Building a non-identical database.

(continued)