lows: $\alpha_t(i)=P(x_1=o_1,\ldots,x_t=o_t,y_t=q_i\mid\Lambda)$ and $\beta_t(i)=P(x_{t+1}=o_{t+1},\ldots,x_T=o_T\mid y_t=q_i,\Lambda)$. Note the forward values enable us to solve the problem through marginalizing, then we obtain

$$P(X_1^T\mid\Lambda)=\sum_{i=1}^{N}P(o_1,\ldots,o_T,y_T=q_i\mid\Lambda)=\sum_{i=1}^{N}\alpha_T(i).$$

The forward values can be computed efficiently with the principle of *dynamic programming*:

$$\alpha_1(i)=\pi_i b_i(o_1),$$
$$\alpha_{t+1}(j)=\left[\sum_{i=1}^{N}\alpha_t(i)a_{ij}\right]b_j(o_{t+1}).$$

Similarly, the backward values can be computed as

$$\beta_T(i)=1,$$
$$\beta_t(i)=\sum_{j=1}^{N}a_{ij}b_j(o_{t+1})\beta_{t+1}(j).$$

The backward values will be used in the Baum-Welch algorithm.

Given the parameters of HMM and a particular sequence of observations, another interesting task is to compute the most likely sequence of states that could have produced the observed sequence. We can find the most likely sequence by evaluating the joint probability of both the state sequence and the observations for each case. For example, in Part-of-speech (POS) tagging [18], we observe a token (word) sequence $X_1^T=o_1,\ldots,o_T$, and the goal of POS tagging is to find a stochastic optimal tag sequence $Y_1^T=y_1y_2\ldots y_T$ that maximizes $P(Y_1^T,X_1^T)$. In general, finding the most likely explanation for an observation sequence can be solved efficiently using the **Viterbi algorithm** [12] by the recurrence relations:

$$V_1(i)=b_i(o_1)\pi_i,$$
$$V_t(j)=b_j(o_t)\max_i\left(V_{t-1}(i)a_{ij}\right).$$

Here $V_t(j)$ is the probability of the most probable state sequence responsible for the first $t$ observations that has $q_j$ as its final state. The Viterbi path can be retrived by saving back pointers that remember which state $y_{t-1}=q_i$ was used in the second equation. Let $Ptr(y_t,q_i)$ be the function that returns the value of $y_{t-1}$ used to compute $V_t(i)$ as follows:

$$y_T=\arg\max_{q_i\in\Omega_Y}V_T(i),$$
$$y_{t-1}=Ptr(y_t,q_i).$$

The complexity of this algorithm is $O(T\times N^2)$, where $T$ is the length of the observed sequence and $N$ is the number of possible states.

Now we need a method of adjusting the parameters $\Lambda$ to maximize the likelihood for a given training set. The **Baum-Welch algorithm** [4] is used to find the unknown parameters of HMMs, which is a particular case of a generalized EM algorithm [9]. We start by choosing arbitrary values for the parameters, then compute the expected frequencies given the model and the observations. The expected frequencies are obtained by weighting the observed transitions by the probabilities specified in the current model. The expected frequencies obtained are then substituted for the old parameters and we iterate until there is no improvement. On each iteration we improve the probability of being observed from the model until some limiting probability is reached. This iterative procedure is guaranteed to converge on a local maximum [34].