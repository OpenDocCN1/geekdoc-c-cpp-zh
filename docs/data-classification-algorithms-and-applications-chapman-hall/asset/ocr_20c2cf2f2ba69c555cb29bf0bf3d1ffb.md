# 18.4.2.2 Online Information Theoretic Metric Learning (OITML)

Another technique we want to review here is the Online Information Theoretic Metric Learning (OITML) approach [3]. This method also falls into the category of supervised metric learning. It is the online version of the ITML approach we introduced in Section 18.3.5. Suppose at time t + 1, we need to randomly pick a pair of data from the constraint set, and minimize the following objective

M_{t+1} = arg min_M R(M, M_t) + η_t ℓ(D_t, D̂_t) (18.46)

where D̂_t = (x_i - x_j)^T M (x_i - x_j) and R(M, M_t) = d_logdet(M, M_t) is the logdet divergence. [3] showed that M_{t+1} can be updated with the following rule

M_{t+1} ← M_t - [2 η_t (D_t - D̂_t) M_t (x_i - x_j)(x_i - x_j)^T M_t] / [1 + 2 η_t (D_t - D̂_t) (x_i - x_j)^T M_t (x_i - x_j)] (18.47)

where

η_t = { η0, D_t - D̂_t ≤ 0; min { η0, 1/[2(D_t - D̂_t)] ( 1 / [(x_i - x_j)^T (I + (M_t^{-1} - I)^{-1}) (x_i - x_j)] ) }, otherwise. (18.48)

POLA and OITML are only two examples of online distance metric learning.

# 18.5 Conclusions and Discussions

Till now we have introduced the state-of-the-art supervised distance metric learning algorithms of recent years. All of those supervised metric learning approaches we listed above require some pre-specified free parameters, and all of them involve some expensive computational procedures such as eigenvalue decomposition or semi-definite programming. One exception is the ITML approach, as it deploys a Bregman projection strategy that may make the solution relatively efficient. However, ITML is sensitive to the initial choice of M0, which makes it difficult to apply in the case when we do not have enough prior knowledge. In practice, according to the type of supervision information provided, we can select a proper supervised metric learning approach that can handle that supervision information. However, in many real world applications, it may be expensive and time consuming to get that supervision information. Next we survey semi-supervised approaches that can leverage both labeled and unlabeled information. For the future of distance metric learning research, we believe the following directions are promising.

+   - Large scale distance metric learning. Most of the existing distance metric learning approaches involve computationally expensive procedures. How can we make distance metric learning efficient and practical on large-scale data? Promising solutions include online learning or distributed learning. We have introduced the most recent works on online distance metric learning in Section 4.1. For parallel/distributed distance metric algorithms, as the major computational techniques involved are eigenvalue decomposition and quadratic programming, we can adopt parallel matrix computation/optimization algorithms [1,15] to make distance metric learning more scalable and efficient.

+   - Empirical evaluations. Although a lot of distance metric learning algorithms have been proposed, there is still a lack of systematic comparison and proof points on the utility of many