# Clustering Multimedia Data 343

as noise and outliers better than using the absolute distances as $L_1$ or $L_2$. Based on this rank-distance, the authors used a clustering algorithm to group faces into a small number of clusters for face annotation. However, as observed by the authors, the faces of the same person usually form several "subclusters" due to the variations in illumination, pose, and expression. To improve the clustering, authors further introduced a cluster-level rank-order distance in conjunction with a cluster-level normalized distance to merge these clusters. Their algorithm shows superior performance on four face databases over classical clustering methods such as affinity propagation, spectral clustering, and shared neighbors in terms of effectiveness (based on four evaluation measures—precision, recall, compression ratio, normalized mutual information) and efficiency (time taken for clustering).

# 14.2.3 Photo Album Recognition

Collection-level analysis of consumer photos has not drawn too much attention in the past. [7] and [8], the authors explored the relationship between collection-level annotation and image-level annotation with help GPS and time information about the photos. Without using metadata, the authors of [18] proposed to describe images and videos with a set of 21 visual concepts. Then, in order to account for typical and nontypical photos within each album, they (partially) matched the photos from two albums when computing the Earth Mover's Distance (EMD) between them. The EMD is a robust distance metric which computes the minimum weighted distance among two image sets to weight-normalization constraints. It allows all pairwise distances between data points (album) and can alleviate the influence of outlier images. Assume there are $n_1$ and $n_2$ albums in $x_1$ and $x_2$, the EMD between them is a linear combination of ground distance $d(f_p^1, f_q^2)$ weighted by flow $f(f_p^1, f_q^2)$ between any two images:

```
$D(x_1, x_2) = \frac{\sum_{p=1}^{n_1}\sum_{q=1}^{n_2} f_{pq}^1 d(f_p^1, f_q^2)}{\sum_{p=1}^{n_1} \sum_{q=1}^{n_2} f_{pq}^1}$ \quad (14.1)
```

where an optimal flow $f(f_p^1, f_q^2)$ is defined by the following linear program:

```
min \sum_{p=1}^{n_1}\sum_{q=1}^{n_2} d(f_p^1, f_q^2)f_{pq}^1 \ns.t. \quad 1 \leq p \leq n_1, 1 \leq q \leq n_2, f(f_p^1, f_q^2) \geq 0, \ns. \sum_{q=1}^{n_2} f_{pq}^1 \leq w_p^1 \ns. \sum_{p=1}^{n_1} f_{pq}^1 \leq \min{\sum_{p=1}^{n_1} w_p^1, \sum_{q=1}^{n_2} w_q^2}$$ (14.2)
```

where $w_p^1$ and $w_q^2$ are the weights of images $f_p$ in albums $x_1$ and $x_2$, respectively. They are set $w_p^1=1/n_1, w_q^2=1/n_2$, and $d(f_p^1, f_q^2)$ takes the value of the Euclidean distance over score concepts. The interpretation of EMD is that a matching between images of two albums can be mapped to a unique flow described in Equation (14.2), and hence, even sets of $\{w_p^1\}$ and $\{w_q^2\}$ imply that all the images within the same album are "exactly matched". The last set of constraints in Equation (14.2) deals with the imbalance of photos in two albums. The final similarity metric at the album is $S(x_1,x_2)=\exp(-D(x_1,x_2)/r)$, where $r$ is the mean of all pairwise distances between all

© 2014 by Taylor & Francis Group