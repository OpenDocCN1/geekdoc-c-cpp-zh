
### 6.5b: Bayes' rule and Gibbs sampling determining the mixture model for a fixed number of clusters - iterations.

```matlab
for i = 1:iter
    % Consider the data in a random order.
    for n = randperm(N)
        v = [n,:];
        l = idx(n);
        % Remove this sample from the data set and update the cluster
        % it was assigned to.
        priorlambda = LAMBDA(1,:);
        % Rank one update on the Cholesky factorization to preserve
        % positive definiteness.
        update = sqrt(LAMBDA(1,:)/priorlambda) * (v' - M(:,l));
        PSI(:,:,l) = cholupdate(PSI(:,:,l),update,'-');
        M(:,l) = (LAMBDA(1,:)*M(:,l,:) - v(:))/priorlambda;
        NU(1) = NU(1)-1;
        LAMBDA(1,:) = priorlambda;
        SIGMA(:,:,l) = iwishrnd(PSI(:,:,l)'* PSI(:,:,l),NU(1));
        MU(:,1) = mvnrnd(M(:,l),SIGMA(:,:,l)/LAMBDA(1));
        nk(l) = nk(l)-1;
        % Calculate cluster assignment probabilities.
        p = zeros(1,K);
        for k = 1:K
            p(k) = (nk(k) + alpha/K)/(N-1+alpha) ...
                mvnpdf(v',MU(:,k),SIGMA(:,:,k));
        end
        p = p/sum(p);
        % Sample new indicator variable.
        l = randsample(K,1,true,p);
        idx(n) = l;
        % Update the cluster the sample is now assigned to.
        postlambda = LAMBDA(1,l);
        % Rank one update on the Cholesky factorization to preserve
        % positive definiteness.
        update = sqrt(LAMBDA(1,l)/postlambda) * (v' - M(:,l));
        PSI(:,:,l) = cholupdate(PSI(:,:,l),update,'+');
        M(:,l) = (LAMBDA(1,l)*M(:,l,:) + v(:))/postlambda;
        NU(1) = NU(1)+1;
        LAMBDA(1,l) = postlambda;
        SIGMA(:,:,l) = iwishrnd(PSI(:,:,l)'* PSI(:,:,l),NU(1));
        nk(l) = nk(l) + 1;
    end
end
```

![](img/d3c00252180686426c9e63ab889b535b_197_0.png)

![](img/d3c00252180686426c9e63ab889b535b_197_1.png)

![](img/d3c00252180686426c9e63ab889b535b_197_2.png)

**(a)** Initial random cluster assignment.

**(b)** Cluster assignment after 5 iterations.

**(c)** Cluster assignment after 100 iterations.

**Figure 6.9:** Bayes' rule and Gibbs sampling determining the mixture model for a fixed number of clusters.

given \(\mathcal{D} \setminus \{\mathbf{v}_n\}\), the current assignments and the prior. With these results,

\[
p(z_{n,k}=1 \mid \mathbf{v}_n, \mathcal{D}\setminus\{\mathbf{v}_n\}, \alpha, \mathbf{m}, \lambda, \mathbf{\Psi}, \nu) \approx
\frac{n_k + \alpha/K}{N-1+\alpha}
\frac{1}{\sqrt{2\pi \Sigma_k}}
\exp\left(-\frac{1}{2}(\mathbf{v}_n - \mu_k)^T \Sigma_k^{-1} (\mathbf{v}_n - \mu_k)\right)
\]

Since these are approximations, we have to divide by the sum of probabilities to ensure they add to one. We use these probabilities to draw a new indicator variable \(z_n\) for \(\mathbf{v}_n\).

Having assigned sample \(\mathbf{v}_n\) to a new cluster \(m\), all parameters for this cluster need to be updated following (6.11). A new mean \(\mu_m\) and covariance matrix \(\Sigma_m\) are drawn from this posterior distribution. \(N_m\) is increased by one. This completes the cluster re-assignment for \(\mathbf{v}_n\).

An iteration is complete, if all samples have been considered in a random order. The process is repeated for a fixed number of iterations. Sometimes this form of Gibbs sampling is called collapsed Gibbs sampling, since the cluster assignments of the other samples are not explicitly used, when sampling \(z_n\) for \(\mathbf{v}_n\). They are indirectly encoded in the parameters of the posterior, normal inverse Wishart distribution for each cluster. This reduces the parameters influencing the sampling to a multiple of \(K\).

Listing 6.5 is a function implementing this clustering algorithm. Some implementations do not draw from the posterior, normal, inverse Wishart distributions, but instead set \(\mu_k = m_k\) and \(\Sigma_k = \Psi_k\).

Figure 6.9 shows the results, when the method is applied to the same data as in Figures 6.3a and 6.3b. The algorithm was initialized with \(\alpha = K\), \(\lambda = 1\), \(\nu = 2\). The parameter \(m\) was set to the sample mean of all data, while \(\Psi\) was set to the average squared distance of all samples to the mean divided by the number of dimensions times the identity matrix.

Figure 6.9a shows the initial random cluster assignments. The clusters start to separate after five iterations in 6.9b. 320 samples are given the wrong (up-to re-labeling) assignment. With more iterations this number reduces. After a hundred iterations 53 samples belong to the wrong cluster. A perfect result

**(a)** Original data.

**(b)** Final cluster assignment.

**Figure 6.10:** Incorrect cluster assignment.

is generally not possible; since for some samples the posterior probabilities \(p(z_{n,k} = 1 | \mathbf{v}_n, \mathcal{D} \setminus \{ \mathbf{v}_n \}, \alpha, \mathbf{m}, \lambda, \mathbf{\Psi}, \nu)\) might be very similar for two clusters, with there being no clear maximal probability. In these cases, it is more useful to return the vector of posterior probabilities instead of a cluster assignment. Even though the number of clusters is specified, this does not mean that this number of clusters is used. It is an upper bound. Figure 6.10 shows that the algorithm combined two clusters into one. Since all the generation of data as well as the inference of clusters is governed by probabilities, there is always the chance of the algorithm getting it wrong.

## 6.6 The Chinese Restaurant Process

In all the above, the number of clusters was fixed at the start of the algorithm. This is, however, undesirable, since in general it is not known beforehand, how many clusters there are. Ideally, the number of clusters should be determined by the data.

It is helpful to revisit the assumptions we made about how the data is generated. Previously, a new data sample was generated by choosing one of the \(K\) processes and then generating the sample according to the probability distribution for that process. We now take the view that there is a chance that the sample is generated by a completely new process, which is different from the processes which generated the previous samples.

It is more convenient to take a sequential view of the generation of samples. For the first sample, a process and its distribution are generated. The second sample can either be generated from the same distribution as the first sample or from a new distribution. We need to define a probability for these two cases. Let \(\alpha\) be an additional parameter governing this probability. It is known as dispersion, concentration, scaling parameter or strength. The probability that the second sample is generated by the first process is \(1/(1 + \alpha)\), while the probability that it is generated by a new process is \(\alpha/(1 + \alpha)\). If \(\alpha = 1\), these two probabilities are the same and are both one half. If \(\alpha\) is greater than 1, then a new process is favoured, while for \(\alpha < 1\) the already existing process is more likely to be used to generate the second sample.

![](img/d3c00252180686426c9e63ab889b535b_199_0.png)

![](img/d3c00252180686426c9e63ab889b535b_199_1.png)

![](img/d3c00252180686426c9e63ab889b535b_199_2.png)

![](img/d3c00252180686426c9e63ab889b535b_199_3.png)

**(a)** \(\alpha = 0.5\)

**(b)** \(\alpha = 1\)

**(c)** \(\alpha = 2\)

**(d)** \(\alpha = 2\)

**Figure 6.11:** Data generated for various values of \(\alpha\).

When generating the \(n^{\text{th}}\) sample, it is generated by

\[
\begin{cases}
\text{process } k \text{ with probability } \frac{n_k}{n - 1 + \alpha} \\
\text{a new process with probability } \frac{\alpha}{n - 1 + \alpha}
\end{cases}
\]

where \(n_k\) denotes the number of samples generated by process \(k\) so far. When summing the samples generated by each process over all processes, the result is \(n - 1\). Therefore these probabilities sum to 1.

Note that as more and more samples are generated by a particular process \(k\), it gets more likely that this process will generate further samples, since \(n_k/(n - 1 + \alpha)\) increases relatively to the other probabilities. This is again the *rich-get-richer* phenomenon.

Listing 6.6 generates data in this fashion. The results for various values of \(\alpha\) are shown in Figure 6.11. The distributions for each cluster were drawn

```matlab
function [V,idx,MU,SIGMA] = CRP( N, alpha, mu0, lambda, Psi, nu)
% Input:
% N: number of data points to be generated,
% alpha: concentration parameter,
% mu0: mean location,
% lambda: mean fraction,
% Psi: inverse scale matrix,
% nu: degrees of freedom.
% Output:
% V: data vector,
% idx: input vector which process generated the sample,
% MU: array of the means of all processes,
% SIGMA: array of the covariance matrices of all processes.
% Generate distribution of first process.
SIGMA(:,:,1) = rwishrnd(Psi,nu);
MU = mvnrnd(mu0,lambda * SIGMA);
V = mvnrnd(MU,SIGMA);
% The vector n_k tracks the number of samples generated by the k-th
% process, where k is the vector index.
n_k = 1;
for i = 2:N
% Calculate probabilities which process generates the next sample.
p = n_k/(i-1+alpha);
% Append the probability that a new process is generated.
p = cat(1,p,alpha/(i-1+alpha));
% Sample which process generates the next data point is taken or
% whether a new process is created.
compidx = randsample(length(p),1,true,p/sum(p));
if compidx < length(p)
% Generate new sample from existing process indicated by
% compidx.
V = cat(1,V,mvnrnd(MU(compidx,:),SIGMA(:,:,compidx)));
idx = cat(1,idx,compidx);
% Update vector n_k of the number of samples generated by each
% process.
n_k(compidx) = n_k(compidx)+1;
else
% New process is generated.
sigma = iwishrnd(Psi,nu);
mu = mvnrnd(mu0,lambda * sigma);
V = cat(1,V,mvnrnd(mu,sigma));
idx = cat(1,idx,compidx);
% Append mean and covariance matrix of new process to arrays
% of means and covariances.
MU = cat(1,MU,mu);
SIGMA = cat(3,SIGMA,sigma);
% Update vector n_k of the number of samples generated by each
% process.
n_k = cat(1,n_k,1);
end
end
```

Listing 6.6: Generating data from a distribution of distributions where the number of clusters is variable.
