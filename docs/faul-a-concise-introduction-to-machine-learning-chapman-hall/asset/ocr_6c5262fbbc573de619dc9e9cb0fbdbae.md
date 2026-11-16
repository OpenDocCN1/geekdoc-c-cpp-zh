```
function [idx,K,MU,SIGMA] = InferDP(V,alpha,m,lambda,Psi,nu,iter)
% Input:
%   V:        data,
%   alpha:    prior concentration parameter,
%   m:        prior location vector,
%   lambda:   prior mean fraction,
%   Psi:      prior inverse scale matrix,
%   nu:       prior degrees of freedom,
%   iter:     number of iterations
% Output:
%   idx:      index vector of cluster assignments,
%   K:        number of clusters
%   K:        array of the means sampled from the posterior normal
%   MU:       inverse Wishart distributions for each cluster,
%   SIGMA:    array of the covariance matrices sampled from the posterior
%             normal inverse Wishart distributions for each cluster.
%
N = size(V,1);    % Number of samples.
K = 0;            % Number of clusters.
idx = zeros(N,1); % Vector cluster assignments.
nk = [];          % Vector of cluster sizes.
%
% For each cluster:
M = [];           % Posterior location vector.
LAMBDA = [];      % Posterior mean fraction.
Psi = [];         % Cholesky factorization of posterior inverse
                  % scale matrix.
NU = [];          % Posterior degrees of freedom.
SIGMA = [];       % Covariance matrix draw.
MU = [];          % Mean draw.
%
% Use Cholesky factorization of Psi to ensure positive definiteness.
Psi = chol(Psi);
%
% Consider samples in a random order.
order = randperm(N);
% Initialize cluster assignments.
for n = 1:N
    v = V(order(n),:);
    % Calculate cluster assignment probabilities.
    p = zeros(1,K+1);
    for k = 1:K
        p(k) = nk(k)/(n-1+alpha)*mvnpdf(v',MU(:,k),SIGMA(:,:,k));
    end
    p(K+1) = alpha/(n-1+alpha)*mvnpdf(v',m,Psi);
    p = p/sum(p);
    % Sample new indicator variable.
    l = randsample(K+1,true,p);
    idx(order(n)) = l;
end
```