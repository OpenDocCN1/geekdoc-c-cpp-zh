
![](img/0faee1c17bea0aab06ee9523a28c4eaf_162_0.png)

**FIGURE 8.2:** The Taylor-Butina asymmetric clustering results are displayed for a set of conformers for JNK3-active ligands clustered with an X-ray structure (2EXC) of a bound JNK3 ligand. The cluster representatives for the largest clusters are displayed in Figure 8.2b. Figure 8.2c displays the first few cluster members of the largest cluster; note that 2EXC is the second member of the cluster and that the centroid of the cluster shown as the first depiction has a high Tversky score.

The results are displayed (as a hierarchy), rank ordered from left to right according to cluster size. Conformations of JNK3 active ligands are clustered with an X-ray structure (2EXC) of a bound JNK3 ligand. In Figure 8.2b, the cluster conformation representatives for the largest clusters are displayed. The first few cluster members of the largest cluster are displayed in Figure 8.2c, where the crystal structure, 2EXC, is the second member of the cluster. The centroid of this cluster, shown as the first depiction, has a high Tversky score with 2EXC.

Likewise in 3D, if a large chemical structure has a sub-shape that is very similar to the entire shape of a smaller molecular structure, these two shapes will have one of the two very similar asymmetric measures. These measures can then in turn be used in similarity or clustering studies, where the clustering is performed using asymmetric clustering algorithms.

Sequence alignment is an area of research in bioinformatics where symmetric measures are not always the most effective comparison tool. Aligning sequences of different lengths and character shares similar issues with the size/shape discussion of chemical structures described above. A subset of a sequence may exactly match a subsection of a larger sequence and knowledge of that 'similarity' in the case of genes or protein sequences should be reflected in the similarity scores in the analysis. Edit distance, a common measure applied in sequence comparisons, is discussed below. Edit distance is another asymmetric measure.

## 8.1 Measures

The social science example above is a form of empirical asymmetric data, but there are numerous methods that can be used to transform symmetric measures into asymmetric measures if the data warrants such comparisons. Below we discuss two common asymmetric measures used in bioinformatics and drug discovery.

### 8.1.1 Tversky

The Tversky measure is very much like the Tanimoto measure. Using the conventions in Chapter 2, the Tversky can be stated as follows:

$$s = \frac{c}{\alpha a + \beta b + c}, \tag{8.1}$$

where α and β are continuous valued parameters. In order to get a value range in [0, 1], and to relate the Tversky directly to the Tanimoto, one can constrain α and β so that α = 2 − β. In this way, when α = β = 1, the Tversky becomes the Tanimoto. The asymmetry results from swapping α and β in generating the similarity between (i, j) and (j, i). When one of the parameters is near zero, the resulting similarity is strongly asymmetric, and when both parameters are near one, the resulting similarity has very little asymmetry.

### 8.1.2 Edit Distance

Edit distance is a commonly used measure in sequence alignment [11, 94]. Given two sequences, the edit distance is the least costly transformation, namely the sum of the least number of deletions, insertions or substitutions necessary to transform one sequence into the other. For example, the edit distance to transform the string *EDIT* into *TEXT* is greater than the edit distance required to transform the string *NEXT* into *TEXT*, since the latter requires only a letter exchange and the transformation for the former requires more than one step (e.g., a letter exchange, a deletion and an insertion). There are potentially many possible transformations; the edit distance is the transformation which requires the least costly number of steps.

$$D_{ab} = \min \sum_{j=1}^{N} c_i(j) + c_s(j) + c_d(j), \tag{8.2}$$

where $D_{ab}$ is the edit distance between two sequences $a$ and $b$, $c_i(j)$ is the cost of the insertion steps in the transformation, $c_s(j)$ is the cost of the exchange steps and $c_d(j)$ is the cost of the deletion steps for a given transformation, $j$, in the set of $N$ all possible transformations.

![](img/0faee1c17bea0aab06ee9523a28c4eaf_164_0.png)

**FIGURE 8.3:** A Tversky similarity comparison between an X-ray structure (2EXC) of a compound with known activity to JNK3 (a kinase implicated in neuronal apoptosis) and a conformer of a ligand found to have activity to JNK3 in a screening assay [78, 4, 139]. The overlay in 3D of the two structures shows a subsume match in Tversky space for these two JNK3 active ligands.

## 8.2 Algorithms

### 8.2.1 Strongly Connected Components Agglomerative Hierarchical Algorithm

Strongly connected components (SCC) is a directed graph algorithm that finds components in a graph if they admit to being cycles. More formally, a strongly connected component in the graph is a vertex set, where there is a directed path from vertex u to vertex v for all u and v in the vertex set. If the graph is weighted, the SCC algorithm can be used recursively to first find the smallest strongly connected components with the sum of the least weighted edges, and successively merging components with the sum of the least weights until there is just one strongly connected component representing all of the vertices in the graph. This process builds an agglomerative hierarchy from single data items through components of ever increasing size. Much like complete link and single link can be considered in terms of graph models (finding maximal cliques, and finding minimum spanning tree subgraphs respectively). The SCC agglomerative hierarchical algorithm is a directed graph approach that lies somewhere in between furthest neighbor behavior of complete link clustering and the chaining behavior of single link approach. Its closest analogue to undirected graphs is bi-connected components (there are at least two paths between u and v in the vertex set in an undirected graph). (Note, there are other forms of connectivity: tri-connected, k-connected, that have also been used in clustering [67, 119].)

An efficient algorithm for the use of SCC to create an agglomerative hierarchy is due to Tarjan [131]. To see how the method works, however, we show it here in the form of a simple agglomerative hierarchical algorithm, where the merge criterion is based on merging strongly connected components with the least edge weights.

**Algorithm 8.1 SCC AgglomerativeHierarchy(Data)**
```
1: N ← Size(Data)
2: G ← Groups(Data) //One data element per group in G
3: repeat
4:   G ← MergeWeightedSCC(G) //Merge closest group based on SCC edge weights
5:   Output: Merged Group Pair and Merge Criterion Value //Value is the weight of the last edge added to create the SCC
6: until |G| == 1
```

### 8.2.2 Modified Taylor-Butina Algorithm

The simplest asymmetric version of Taylor-Butina can be represented by the simple exclusion region algorithm, where the input matrix is a sparse asymmetric matrix. Here, the largest nearest neighbor table, whether in the row or column space, that is left in the matrix at each iteration is considered the next cluster. Setting up the asymmetric sparse matrix data structure is a bit more complex than the simple nearest neighbor table of the symmetric form of the algorithm, and the manipulation of that matrix to remove all of those members in the exclusion region also requires searching in both the row and column space of the matrix. The algorithm is therefore roughly twice as slow as the symmetric version, providing twice as much space is used to store both the row and column space. Smaller memory usage can be arranged, but only at the expense of the search time.

**Algorithm 8.2 AsymmetricExclusionRegion(AsymSparseMatrix)**
```
1: repeat
2:   C ← FindLargestSetNN(AsymSparseMatrix) //Assign largest row (or column) in matrix to cluster
3:   SparseMatrix ← SparseMatrix \ C //Remove row (or column) and its elements from the matrix
4:   Append(C,G) //Append cluster C to set of clusters G
5: until SparseMatrix == NULL
6: Output : G
```

In a bit of irony, the above asymmetric clustering algorithm with the use of SAM (sequence alignment and modeling system with the use of hidden Markov models), akin to edit distance in generation of asymmetric associations, was utilized for bank customer retention segmentation clustering [110]. Clearly, the asymmetry inherent in genetic sequence data relationships could utilize the same technique.

## 8.3 Glossary

- **asymmetric matrix:** a square matrix where the (i,j) element does not necessarily equal (j,i)
- **homology model:** a prediction of a 3D protein structure for a novel protein sequence that shares sequence homology with a known protein structure
- **similarity searching:** an m×n matrix of similarities where m ≪ n
- **skew symmetric:** the average difference between the (i,j)th element and the (j,i)th element in an asymmetric matrix
