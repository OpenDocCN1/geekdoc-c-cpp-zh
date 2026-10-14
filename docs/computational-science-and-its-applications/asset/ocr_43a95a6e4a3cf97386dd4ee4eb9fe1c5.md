where q the continuous version of the parameter of interest q_M. The discrete analogue for a two-dimensional body of the total variation regularization R_TV_c [25] is

```
R_TV(q_M) := sum_{i=1}^h l_i |Δ_i q_M |, (5.37)
```

where l_i is defined as the length of the edge corresponding to the i th adjacent pixel and

```
Δ_i = (0,0,...,0,1_{a(1,i)},0,...,0,-1_{a(2,i)},0,...,0), (5.38)
```

with a = (a_(i,j))_{i,j=1,i∈{1,2}}^h as the set containing the numbers of all adjacent pixel tuples (a_(1,i), a_(2,i)).

# 5.4.4 The Markov Chain Monte Carlo Method

In the previous sections we discussed the posterior density with several meaningful prior densities (regularizations), and hence to obtain a good estimate for q_M^* based on the measurements g_K^. That is, the algorithm seeks to find the Bayesian estimate E(q_M^* | g_K^) = ∫_{R^n} q_M π_{q_M}^* (q_M | g_K^) dq_M.

Given that the posterior density π_{q_M}^* (q_M | g_K^) does not have a closed form, there is no direct method of finding the Bayesian estimate E(q_M^* | g_K^). Therefore, one uses the Markov Chain Monte Carlo Method (MCMC) to generate a large random sample {q_M^(i)}_{i=1}^N from the posterior density π_{q_M}^* (q_M | g_K^) and then approximate the Bayesian estimate by its sample mean,

```
E(q_M^* | g_K^) = ∫_{R^n} q_M π_{q_M}^* (q_M | g_K^) dq_M ≈ (1/N) sum_{i=1}^N q_M^(i). (5.39)
```

Typical algorithms to generate such random samples from a posterior density are the Gibbs sampler or the Metropolis–Hastings algorithm [33, 19, 34].

# 5.5 Conclusion

In this chapter, we have introduced inverse problems involving PDEs for imaging applications. We described the challenges and difficulties of solving an ill-posed inverse problem. We have provided details of two very well-known examples namely EIT and DOT. A range of both deterministic and statistical regularization approaches have been exposed and summarized in this chapter. The computational approaches have been discussed without any rigorous analysis of the convergence rates. The future challenges in this area can be overcome by reformulating the inverse question either using a regularization approach such as a combination of smoothness and sparsity or statistical approaches or weakening the inverse question itself. The progress in the area of inverse problems in imaging is expected to be in the intersection of computation, statistical, and analytical