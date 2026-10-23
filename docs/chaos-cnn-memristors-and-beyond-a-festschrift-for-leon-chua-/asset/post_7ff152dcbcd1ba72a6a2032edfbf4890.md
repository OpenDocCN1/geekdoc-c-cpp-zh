
![](img/039e7d3c23390584a66737067db8b75b_261_0.png)

Fig. 1. The graph of interactions \(\Gamma_{\mathcal{F}}\) and \(\Gamma_{\mathcal{X}_S\mathcal{F}}\) of \((\mathcal{F},X)\) and \((\mathcal{X}_S\mathcal{F},X_S)\) in examples 1 and 3.

dynamics \(T\) and the interaction \(F\). However, if the system has no local dynamics, i.e. \(T=\mathrm{id}\) is the identity map, then the dynamical network \(\mathcal{F}\) is simply the interaction \(F\).

Conversely, any composition \(\mathcal{F}=F\circ T\) can be considered to be an interaction. Writing \(\mathcal{F}=(F\circ T)\circ \mathrm{id}\), the dynamical network \((\mathcal{F},X)\) is simply the interaction \(\mathcal{F}=F\circ T\) with no local dynamics.

## Remark 2.

If \((\mathcal{F},X)\) is considered as a dynamical network with no local dynamics then \(\mathcal{M}_{\mathcal{F}}=\Lambda\) for any constants \(\Lambda_{ij}\) satisfying (2) for \(\mathcal{F}\). Hence, \((\mathcal{F},X)\) has a globally attracting fixed point if \(\rho(\Lambda)<1\).

Suppose \((\mathcal{F},X)\) is a dynamical network where \((\mathcal{F},X)\) is considered as a dynamical network with no local dynamics. That is, the component
$$
\mathcal{F}_j:\bigoplus_{i\in I_j}X_i\to X_j\qquad\text{for }1\le j\le n.
$$

Alternatively we write
$$
\mathcal{F}_j(\mathbf{x}|_{I_j})=\mathcal{F}_j(x_{j_1},\ldots,x_{j_m}),\qquad\text{where }I_j=\{j_1,\ldots,j_m\}.
$$

Note that if we replace the variable \(x_{j_i}\) of \(\mathcal{F}_j\) by the function \(f(y_1,\ldots,y_k)\), the result is the function
$$
\mathcal{F}_j(x_{j_1},\ldots,x_{j_{i-1}},f(y_1,\ldots,y_k),x_{j_{i+1}},\ldots,x_{j_m})
$$
having variables \(x_{j_1},\ldots,x_{j_{i-1}},y_1,\ldots,y_k,x_{j_{i+1}},\ldots,x_{j_m}\). Additionally, if \(\gamma=\ell_1,\ldots,\ell_N\), let
$$
\mathcal{F}_{j;\gamma}(x_{j_1},\ldots,x_{j_m})=\mathcal{F}_j(x_{j_1,\gamma},\ldots,x_{j_m,\gamma}).
$$
That is, the variables of the function \(\mathcal{F}_{j;\gamma}\) are indexed by the sequences \(j_i,\ell_1,\ldots,\ell_N\) for \(1\le i\le m\).

As \(\mathcal{F}\) is an interaction, the graph \(\Gamma_{\mathcal{F}}=(V,E)\) where \(e_{ij}\in E\) if \(x_i\) is a variable of \(\mathcal{F}_j\). A path \(P\) in the graph \(\Gamma_{\mathcal{F}}\) is an ordered sequence of distinct vertices \(v_1,\ldots,v_m\in V\) such that \(e_{i,i+1}\in E\) for \(1\le i\le m-1\). We call the vertices \(v_2,\ldots,v_{m-1}\) of \(P\) the interior vertices of \(P\). If the vertices \(v_1\) and \(v_m\) are the same then \(P\) is a cycle.

## Definition 5.

For \(\Gamma_{\mathcal{F}}=(V,E)\) let \(S\subset V\). The set \(S\) is a *complete structural set* of \(\Gamma_{\mathcal{F}}\) if

- (i) each cycle of \(\Gamma_{\mathcal{F}}\) contains a vertex in \(S\); and
- (ii) each vertex \(v_k\in V\) belongs to a path \(v_i,\ldots,v_j\) where \(v_i,v_j\in S\).

Let \(st_0(\Gamma_{\mathcal{F}})\) denote the set of all complete structural sets of the graph \(\Gamma_{\mathcal{F}}\). Moreover, if the complete structural set \(S=\{v_1,\ldots,v_m\}\), let \(\mathcal{I}_S=\{1,\ldots,m\}\) denote the *index set* of \(S\).

Let \((\mathcal{F},X)\) be a dynamical network with graph of interactions \(\Gamma_{\mathcal{F}}=(V,E)\) and suppose \(S\in st_0(\Gamma_{\mathcal{F}})\). For \(j\in\mathcal{I}_S\) let \(\mathcal{F}_{j,1}\) be the function
$$
\mathcal{F}_{j,1}=\mathcal{F}_j(x_{j_1},\ldots,x_{j_m})
$$
in which each variable \(x_{j_\ell}\) is replaced by \(x_{j_\ell,j}\) if \(j_\ell\notin\mathcal{I}_S\).

For \(i>1\) let \(\mathcal{F}_{j,i}\) be the function
$$
\mathcal{F}_{j,i}=\mathcal{F}_{j,i-1}(x_{\gamma_1},\ldots,x_{\gamma_t})
$$
in which each \(x_{\gamma_\ell}=x_{\ell_1,\ldots,\ell_N}\) is replaced by the function \(\mathcal{F}_{\ell_1;\gamma_\ell}\) if \(\ell_1\notin\mathcal{I}_S\). If \(\ell_1\in\mathcal{I}_S\) for each \(1\le\ell\le t\), then define \(\mathcal{X}_S\mathcal{F}_j=\mathcal{F}_{j,i-1}\).

## Definition 6.

For \(S\in st_0(\Gamma_{\mathcal{F}})\) let \(\mathcal{B}_S(\Gamma_{\mathcal{F}})\) be the set of paths and cycles of \(\Gamma_{\mathcal{F}}\) that begin and end with a vertex of \(S\) having no interior vertices in \(S\). We say
$$
\mathcal{A}_S(\mathcal{F})=\{\ell_1,\ldots,\ell_N:v_{\ell_1},\ldots,v_{\ell_N}\in\mathcal{B}_S(\Gamma_{\mathcal{F}}),\ N>2\}
\tag{5}
$$
is the set of *admissible sequences* of \(\mathcal{F}\) with respect to \(S\).

Let \(\gamma=\ell_1,\ldots,\ell_N\in\mathcal{A}_S(\mathcal{F})\). For \(1<i<|\gamma|=N\) define the \(N-2\) spaces
$$
X_{i;\gamma}=X_{\ell_1}.
$$

Additionally, define the functions
$$
\mathcal{X}_S\mathcal{F}_{i;\gamma}(x_{i-1,\gamma})=x_{i-1,\gamma}.
$$

By way of notation we let
$$
X_{N-1;\gamma}=X_\gamma,\quad \mathcal{X}_S\mathcal{F}_{N-1;\gamma}=\mathcal{X}_S\mathcal{F}_\gamma,\quad\text{and}\quad x_{1,\gamma}=x_{\ell_1}.
$$

## Definition 7.

Suppose \(S\in st_0(\Gamma_{\mathcal{F}})\). Let
$$
\mathcal{X}_S\mathcal{F} =
\left(\bigoplus_{j\in\mathcal{I}_S} \mathcal{X}_S\mathcal{F}_j\right)
\oplus
\left(\bigoplus_{\substack{\underline{\gamma}\in\mathcal{A}_S(\mathcal{F})\\1<i<|\underline{\gamma}|}}
\mathcal{X}_S\mathcal{F}_{i;\underline{\gamma}}\right)
$$
and
$$
X_S =
\left(\bigoplus_{j\in\mathcal{I}_S} X_j\right)
\oplus
\left(\bigoplus_{\substack{\underline{\gamma}\in\mathcal{A}_S(\mathcal{F})\\1<i<|\underline{\gamma}|}}
X_{i;\underline{\gamma}}\right).
$$

For the function \(\mathcal{X}_S\mathcal{F}:X_S\to X_S\), the dynamical network \((\mathcal{X}_S\mathcal{F},X_S)\) is called the *dynamical network expansion* of \((\mathcal{F},X)\) with respect to \(S\).

## Example 3.

Consider the dynamical network \((\mathcal{F},X)\) where
$$
\mathcal{F}(\mathbf{x}) =
\begin{bmatrix}
\mathcal{F}_1(x_1,x_2) \\
\mathcal{F}_2(x_1,x_3) \\
\mathcal{F}_3(x_2,x_3)
\end{bmatrix}.
$$

The network has the graph of interactions \(\Gamma_{\mathcal{F}}=(V,E)\) shown in Fig. 1 (left). Moreover, the set \(S=\{v_1,v_3\}\) is a complete structural set of \(\Gamma_{\mathcal{F}}\). To see this, note that the cycles of \(\Gamma_{\mathcal{F}}\) form the set \(\{v_1,v_1;\,v_3,v_3;\,v_1,v_2,v_1;\,v_1,v_2,v_3;\,v_3,v_2,v_1;\,v_3,v_2,v_3\}\). As (i) each cycle of \(\Gamma_{\mathcal{F}}\) contains either \(v_1\) or \(v_3\), and (ii) each vertex in \(V\) belongs to the path \(v_1,v_2,v_3\), then \(S\in st_0(\Gamma_{\mathcal{F}})\). Hence, the expansion \((\mathcal{X}_S\mathcal{F},X_S)\) is well defined.

To construct this expansion, we first consider the components of \(\mathcal{F}\) indexed by \(\mathcal{I}_S=\{1,3\}\). For \(\mathcal{F}_1=\mathcal{F}_1(x_1,x_2)\), note that the variable \(x_2\) is indexed by an element not in \(\mathcal{I}_S\). Hence, \(\mathcal{F}_{\langle1,1\rangle}=\mathcal{F}_1(x_1,x_{21})\). Replacing \(x_{21}\) by the function \(\mathcal{F}_{2;21}=\mathcal{F}_2(x_{121},x_{321})\) yields \(\mathcal{F}_{\langle1,2\rangle}=\mathcal{F}_1(x_1,\mathcal{F}_2(x_{121},x_{321}))\). Since each variable of \(\mathcal{F}_{\langle1,2\rangle}\) is indexed by a sequence beginning with an element of \(\mathcal{I}_S\), \(\mathcal{X}_S\mathcal{F}_1=\mathcal{F}_1(x_1,\mathcal{F}_2(x_{121},x_{321}))\). Similarly, the function \(\mathcal{X}_S\mathcal{F}_3\) can be shown to be \(\mathcal{X}_S\mathcal{F}_3=\mathcal{F}_3(\mathcal{F}_2(x_{123},x_{323}),x_3)\).

Note that the set \(\mathcal{B}_S(\Gamma_{\mathcal{F}})=\{v_i,v_i;\,v_i,v_2,v_i;\,v_i,v_2,v_j: i,j\in\mathcal{I}_S\}\) implying \(\mathcal{A}_S(\mathcal{F})=\{121,123,321,323\}\). Then for any \(\underline{\gamma}\in\mathcal{A}_S(\mathcal{F})\) there is a single function \(\mathcal{X}_S\mathcal{F}_{2;\underline{\gamma}}\) corresponding to \(\underline{\gamma}\), given by
$$
\mathcal{X}_S\mathcal{F}_{\underline{\gamma}}(x_i)=x_i \quad\text{for}\quad \underline{\gamma}=i,2,j.
$$

By Definition 7, the expansion \(\mathcal{X}_S\mathcal{F}\) is given by
$$
\mathcal{X}_S\mathcal{F}(\mathbf{x})
=
\begin{bmatrix}
\mathcal{X}_S\mathcal{F}_1(x_1,x_{121},x_{321}) \\
\mathcal{X}_S\mathcal{F}_3(x_{123},x_{323},x_3) \\
\mathcal{X}_S\mathcal{F}_{121}(x_1) \\
\mathcal{X}_S\mathcal{F}_{123}(x_1) \\
\mathcal{X}_S\mathcal{F}_{321}(x_3) \\
\mathcal{X}_S\mathcal{F}_{323}(x_3)
\end{bmatrix}
=
\begin{bmatrix}
\mathcal{F}_1(x_1,\mathcal{F}_2(x_{121},x_{321})) \\
\mathcal{F}_3(\mathcal{F}_2(x_{123},x_{323}),x_3) \\
x_1 \\
x_1 \\
x_3 \\
x_3
\end{bmatrix}
\tag{6}
$$
where \(X_S=(X_1\oplus X_3)\oplus(X_{121}\oplus X_{321}\oplus X_{123}\oplus X_{323})\). The graph of interactions \(\Gamma_{\mathcal{X}_S\mathcal{F}}\) is shown in Fig. 1 (right).

A natural question to ask is whether the expansion \((\mathcal{X}_S\mathcal{F},X_S)\) and the initial (real) dynamical network \((\mathcal{F},X)\) have similar dynamics.

## Theorem 2.

Suppose \((\mathcal{X}_S\mathcal{F},X_S)\) is a dynamical network expansion of \((\mathcal{F},X)\). If \((\mathcal{X}_S\mathcal{F},X_S)\) has a globally attracting fixed point, then \((\mathcal{F},X)\) also has a globally attracting fixed point.

In particular, suppose \(\mathbf{y}_S\in X_S\) is a globally attracting fixed point of \((\mathcal{X}_S\mathcal{F},X_S)\). Then the globally attracting fixed point \(\mathbf{y}\in X\) of \((\mathcal{F},X)\) has the property \(y_j=(\mathbf{y}_S)_j\) for \(j\in\mathcal{I}_S\), from which the other coordinates of \(\mathbf{y}\) can be easily deduced.

The following is an immediate corollary to Theorem 2 and Remark 2.

## Corollary 1.

Let \((\mathcal{X}_S\mathcal{F},X_S)\) be a dynamical network expansion of \((\mathcal{F},X)\). Suppose the constants \(\tilde{\Lambda}_{ij}\) satisfy (2) for \(\mathcal{X}_S\mathcal{F}\). If \(\rho(\tilde{\Lambda})<1\), then \((\mathcal{F},X)\) has a globally attracting fixed point.

The question then is whether there is any advantage in considering a dynamical network expansion over the original unexpanded network. As it turns out, dynamical network expansions always allow for better estimates (or at least no worse) of a dynamical network's global stability.

## Theorem 3. (Improved Stability Estimates for Dynamical Networks)

Let \((\mathcal{X}_S\mathcal{F},X_S)\) be an
