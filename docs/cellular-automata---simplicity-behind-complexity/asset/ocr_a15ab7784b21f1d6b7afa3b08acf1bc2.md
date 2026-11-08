(Hurst, 1951) is the most classic estimation method of Hurst exponent. Edgar E. Peters used R/S analysis to find the fractal feature of financial time series, and built the Fractal Market Hypothesis (FMH). R/S analysis is also provided in E-AFM.

We have a time series, which length is $T$. First, we should divided the time series into $N$ adjacent $\nu$-length sub-periods, and $N\nu=T$. Each sub-period is recorded as $I_n$, $n=1,\ldots,N$. Each element in $I_n$ is recorded as $r_{n,t}$, $t=1,2,\ldots,\nu$. $M_n$ is the arithmetic mean value of $I_n$. We can calculate the accumulated deviation $X_{t,n}$ from the mean using following equation:

$$X_{t,n}=\sum_{i=1}^{t}X_i-M_n$$  \hfill (9)

Let:

$$R_n=\left(\max(X_{t,n})-\min(X_{t,n})\right)$$  \hfill (10)

$R_n$ is called range of $I_n$. Let $S$ is the standard deviation of the $I_n$. Then the Rescaled Range is defined as:

$$E(R_n/S_n)=(aN)^H\quad\text{as }N\to\infty.$$  \hfill (11)

or:

$$\log(E(R_n/S_n))=H\log(N)+\log(a)$$  \hfill (12)

The slope $H$ is the Hurst exponent. It can be estimated by least square method or other methods.

One of E-AFM's tasks is to find how does the microstructure of the capital market cause complexity of macrodynamics. For example, the structure of neighbourhood graph can influence the spread of non-public information in the capital market. We use the degree distribution to measure the complexity of the networks, and use the clustering coefficient to measure the dependency level within the investors. The clustering coefficient $\gamma_v$ of a vertex $v$ in a graph can be defined as:

$$\gamma_v=\frac{|E(\Gamma_v)|}{\binom{k_v}{2}}$$  \hfill (13)

Where $\Gamma_v$ is the neighbourhood of vertex $v$, and $|E(\Gamma_v)|$ is the number of edges in the neighbourhood. $\binom{k_v}{2}$ is the maximum number of possible edges in the neighbourhood.

There are still many other methods could be used to measure the time-space complexity of the artificial financial market. Due to space limitations, we don't discuss them individually.

# 6. Dynamic analysis of an Artificial Financial Market

In the last part of this chapter, we'd like to show the readers an example artificial financial market which is based on E-AFM, and analysis the results of simulation. The assumptions of this artificial financial market are not complete enough to proclaim a new capital market