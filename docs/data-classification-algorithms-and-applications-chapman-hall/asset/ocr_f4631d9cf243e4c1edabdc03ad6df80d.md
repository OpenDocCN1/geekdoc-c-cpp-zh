structure prediction. Each of these subfields is quite mature and one can find various surveys for each of them.

Even though semi-supervised learning techniques are widely used, our theoretical understanding and analysis of various semi-supervised learning methods are yet far from complete. On the one hand, we need asymptotic results of various methods saying that in the limit the estimator under consideration converges to the true underlying classifier, which will ensure that the procedure does the “right” thing given enough labeled and unlabeled examples. On the other hand, we need to have finite sample bounds that will specifically tell us how fast the estimator converges to the true underlying classifier as a function of number of labeled and unlabeled examples. This type of results are completely missing. For example, various graph-based algorithms are quite popular and widely used but yet we hardly have any theoretical finite sample result! Another area of concern is that there are so many different semi-supervised learning algorithms that can be very different from each other under the same assumption or very similar algorithms with only a minor difference. In both the cases, performance of the algorithms can be totally different. This suggests that analysis of individual semi-supervised learning algorithms that perform well in practice, are also very important. This kind of analysis will not only help us understand the behavior of the existing semi-supervised learning algorithms but also help us design better semi-supervised algorithms in the future. In the coming years, researchers from the semi-supervised learning community need to put significant effort towards resolving these issues.

# Bibliography

[1] S. Abney. Bootstrapping. In Fortieth Annual Meeting of the Association for Computational Linguistics, pages 360–367, 2002.

[2] A. Azran. The rendezvous algorithm: Multi-class semi-supervised learning with Markov random walks. In Twenty-fourth International Conference on Machine Learning (ICML), pages 47–56 2007.

[3] M.-F. Balcan, A. Blum and K. Yang. Co-training and expansion: Towards bridging theory and practice In Nineteenth Annual Conference on Neural Information Processing Systems (NIPS), 2005.

[4] M.-F. Balcan and A. Blum. An augmented PAC model for learning from labeled and unlabeled data. In O. Chapelle, B. Schölkopf and A. Zien, editors. Semi-Supervised Learning, MIT Press, Cambridge, MA, 2006.

[5] S. Baluja. Probabilistic modeling for face orientation discrimination: Learning from labeled and unlabeled data In Twelfth Annual Conference on Neural Information Processing Systems (NIPS), pages 854–860, 1998.

[6] M. Belkin, I. Matveeva and P. Niyogi. Regularization and semi-supervised learning on large graphs. In Seventeenth Annual Conference on Learning Theory(COLT), pages 624–638, 2004.

[7] M. Belkin and P. Niyogi. Semi-supervised learning on Reimannian manifold. Machine Learning, 56:209–239, 2004.

[8] M. Belkin, P. Niyogi and V. Sindhwani. Manifold regularization: A geometric framework for learning from labeled and unlabeled examples. Journal of Machine Learning Research, 7: 2399–2434. 2006.