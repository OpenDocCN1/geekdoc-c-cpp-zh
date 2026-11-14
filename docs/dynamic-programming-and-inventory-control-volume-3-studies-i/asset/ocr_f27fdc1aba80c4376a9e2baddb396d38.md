This implies, using the limit of the right hand side

$$z_1(i) - z_2(i) \ge \sum_j m_j^{v_{i_1}}(z_1(j) - z_2(j)).$$

If $i_0$ is the index of minimum of $z_1(i) - z_2(i)$, we have necessarily

$$z_1(i_0) - z_2(i_0) = \sum_j m_j^{v_{i_1}}(z_1(j) - z_2(j)).$$

This implies also

$$m_j^{v_{i_1}}(z_1(i_0) - z_2(i_0)) = m_j^{v_{i_1}}(z_1(j) - z_2(j)), \forall j.$$

Now from the property (6.1.3) we get easily $m_j^{v_{i_1}} > \delta, \forall j$ hence

$$z_1(i_0) - z_2(i_0) = z_1(j) - z_2(j)), \forall j,$$

which proves the uniqueness of $z$ up to an additive constant.

# 6.1.4. EXTENSION.

In fact, the assumption (6.1.1) is much too strong. It is sufficient to assume that

(6.1.9)

$$U \text{ compact}$$ 
$$\varpi^{v_0}(i,j) \text{ is continuous in } v, \forall i, j.$$ 
$$\varpi^{v_0}(i,j) > 0, \forall i, j \text{ and some } v_0$$

We want to prove the following improvement to Theorem 6.1

# **Theorem 6.2.** Under the assumptions (6.1.9) and (6.1.6) there exists one and only one pair $\lambda, z$ which is the solution of (6.1.7).

Proof. To the transition matrix $\varpi^{v_0}(i,j)$ corresponds a unique invariant measure $m_i^{v_0}$. These numbers are strictly positive. We can thus consider the inverse

$$q_i^{v_0} = \frac{1}{m_i^{v_0}}.$$

We omit the index $v_0$ in the following, to simplify the notation. We shall write $\varpi(i,j), m_i, q_i$, and $\Phi$ will denote the operator $\Phi^{v_0}$.

Consider the system

(6.1.10)

$$q_{ij} - \sum_{k \neq j} \varpi(i,k)q_{kj} = 1, \forall j$$ 
$$q_{jj} = q_j$$

We have

# **Lemma 6.1.** The system (6.1.10) has a unique positive solution.

PROOF. The system can be rewritten as follows

$$q_{ij} - \sum_k \varpi(i,k)q_{kj} = \theta_{ij},$$

with

$$\theta_{ij} = 1 - \varpi(i,j)q_j,$$

and we have

$$\sum_i m_i \theta_{ij} = 1 - \sum_i m_i \varpi(i,j)q_j = 1 - m_j q_j = 0.$$