The NMSE for a clustered data set is given as follows:

\[
NMSE = \frac{\sum_{h=1}^H \sum_{i=1}^{m_h} \sum_{j=1}^{n_h} \sum_{j=m_h+1}^N \left(y_{j}^{(h)}\right)^2}{\sum_{h=1}^H \sum_{i=1}^{m_h} \sum_{j=1}^{n_h} \sum_{j=1}^N \left(y_{j}^{(h)}\right)^2} = \frac{\sum_{h=1}^H m_h \sum_{j=m_h+1}^N \lambda_{j}^{(h)}}{\sum_{h=1}^H m_h \sum_{j=1}^N \lambda_{j}^{(h)}} \quad (3.9)
\]

*Index space compression*: The index volume is computed as successive dimensions in the transposed space are removed.

*TNMSE*: The target NMSE (TNMSE) is recomputed as successive dimensions are omitted.

*Recall*: As dimensions are omitted, an experiment is run to determine the recall with a sufficiently large number of sample queries [3].

+   6. The *within-cluster index-construction step* operates separately on each cluster $\mathbf{Y}^{(b)}$. Following data reduction, each cluster is much more amenable to efficient indexing than the entire table. The OP-tree proposed in Reference 2 and utilized in Reference 3 is very efficient for k-NN search in medium- and even high-dimensionality spaces.

# ### 3.5 NEAREST NEIGHBORS QUERIES IN HIGH-DIMENSIONAL SPACE

Queries on high-dimensional data can be classified as follows [70]: (1) *point queries* to determine if an object with a specified feature vector is available in the database, (2) *range queries* to determine if objects within a certain distance are available in the database, (3) *k-NN queries*, and (4) *spatial join* an all closest pairs of points.

Similarity between two objects $U$ and $V$, $\mathbf{u} = [u_1, \dots, u_n]^T$ and $\mathbf{v} = [v_1, \dots, v_n]^T$, can be measured by their *Euclidean distance*:

\[
D(\mathbf{u},\mathbf{v}) = (\mathbf{u}-\mathbf{v})^T (\mathbf{u}-\mathbf{v})^{1/2} = \left[ \|\mathbf{u}\|^2 + \|\mathbf{v}\|^2 - 2\mathbf{u}^T\mathbf{v} \right]^{1/2} = \left[ \sum_{i=1}^n (u_i-v_i)^2 \right]^{1/2} \quad (3.10)
\]

Given precomputed vector norms, we need to compute only the inner product of the two vectors.

Similarity search based on *k*-NN queries, which determine the *k* images that are closest to a target image, is expensive when the number of dimensions per image ($N$) is in the hundreds and the number of images ($M$) is in the millions. The *k*-NNs can be determined by a sequential scan of an $M \times N$ matrix $\mathbf{X}$. Retrieved points are inserted into a heap, as long as they are no further than the *k* nearest points extracted so far. Determining *k*-NN queries in high dimensions is not a trivial task, due to *"the curse of dimensionality"* [71].

As dimensionality increases, all points begin to appear almost equidistant from one another. They are effectively arranged in a d-dimensional sphere around the query, no matter where the query (point) is located. The radius of the sphere increases,