# Clustering Multimedia Data

Spectral clustering is used to textual feature. To combine the two, the authors use

```
$S_{combine}(i, j) = \begin{cases} S_{textual}(i, j) \le 1 & \text{if } S_{link}(i, j) = 0 \ 1 & \text{if } S_{link}(i, j) > 0 \end{cases} \quad (14.39)$
```

Then, the images within clusters are further arranged by their visual features. The organization is more user-friendly for browsing, and the clusters are more reliable than those produced using only the visual content of the images.

Bekerman and Jeon [2] proposes applying combinatorial Markov random field (Comraf) to multimodal clustering. A combinatorial Markov random field is an MRF in which at least one node is a combinatorial random variable, which can be partitions, partial orderings, etc., of a finite set. Thus, the result of an MRF can be directly converted to clustering. Given a Comraf model over $m$ combinatorial variables $X^c = \{X_0^c, ..., X_{m-1}^c\}$, where $X_0^c$ corresponds to the target modality, the task is to find the most probable instantiation of $X^c = \arg\max P(X^c)$. Since $X_0^c$ is the only target modality, for $i > 0$, $X_i^c$ is known and will correspond to a clustering of all singleton clusters. The structure of the Comraf is an asterisk with target weighted information to be the pairwise function between two modalities, i.e.,

```
$(\hat{X}_0, X_j)_{MPE} = \arg\max \sum_{j=1}^{m-1} f_j(\hat{X}_0, X_j) = \arg\max \sum_{j=1}^{m-1} w_j I(\hat{X}_0, X_j) \quad (14.40)$
```

where $I(\hat{X}_0, X_j)$ evaluates the mutual information between two clusters and $w_j$ is the weight. In practice, the observed modalities are words, rectangular blocks, color, and texture. Through experiments, this framework is shown to obtain 2.5–3 times higher accuracy compared with a unimodal k-means algorithm.

# 14.5 Summary and Future Directions

This chapter concisely reviews, using some concrete examples, different categories of classical multimedia applications which directly or indirectly influence clustering techniques. For each example, we discussed the application-specific technical challenges for developing effective and efficient clustering algorithms, for example, multimodality and high-dimensionality. One of prominent emerging multimedia applications invokes the interaction between multimedia data with the fact developed networks. For example, the users or groups who favor the multimedia documents have immersed research efforts. On one hand, this additional dimensionality of social relations might provide useful information and insights from users affinities and behavior. On the other hand, these relationships are often dynamic and incomplete, making the problem more complicated and challenging.

# Bibliography

+   [1] Kobus Barnard, Pinar Duygulu, and David Forsyth. Clustering art. in CVPR, pages 434–441, 2001.