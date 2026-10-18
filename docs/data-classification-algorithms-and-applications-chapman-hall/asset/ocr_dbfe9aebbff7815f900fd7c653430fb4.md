as follows: for each edge $(i,j) \in \mathcal{E}$, define a weight matrix $\mathbf{W} \in \mathbb{R}^{n\times n}$, where each element $w_{i,j}$ is defined using the radial basis function in (15.1); define a diagonal matrix $\mathbf{D} \in \mathbb{R}^{n\times n}$ as

$d_{i,i} \triangleq \sum_{j=1}^{n} w_{i,j}$;

one then computes the regularizer as $\mathbf{Q} \triangleq \mathbf{D} - \mathbf{W}$.

One could alternately define the regularizer as a *normalized* Laplacian, $\mathbf{Q} \triangleq \mathbf{I} - \mathbf{D}^{-\frac{1}{2}} \mathbf{W} \mathbf{D}^{-\frac{1}{2}}$, per [47]. [15] extended this method for heterogeneous networks—that is, graphs with multiple types of nodes and edges. Another variant, due to [43], sets $\mathbf{Q} \triangleq (\mathbf{I} - \mathbf{A})^{\top} (\mathbf{I} - \mathbf{A})$, where $\mathbf{A} \in \mathbb{R}^{n\times n}$ is a row-normalized matrix capturing the local pairwise similarities. All of these formulations impose a *smoothness* constraint on the predictions, that “similar” nodes—where similarity can be defined by the Gaussian in (15.1) or some other kernel—should be assigned the same label.

There is an interesting connection between graph-based regularization and label propagation. Under the various parameterizations of $\mathbf{Q}$, one can show that (15.4) provides a closed-form solution to the label propagation algorithm in Section 15.3.1 [48]. This means that one can compute certain formulations of label propagation without directly computing the iterative algorithm. Heavily optimized linear algebra solvers can be used to compute (15.4) quickly. Another appealing aspect of these methods is their strong theoretical guarantees [8].

# 15.5 Probabilistic Graphical Models

Graphical models are powerful tools for joint, probabilistic inference, making them ideal for collective classification. They are characterized by a graphical representation of a probability distribution $P$, in which random variables are nodes in a graph $\mathcal{G}$. Graphical models can be broadly categorized by whether the underlying graph is directed (e.g., Bayesian networks or collections of local classifiers) or undirected (e.g., Markov random fields). In this section, we discuss both kinds.

Collective classification in graphical models involves finding the assignment $\mathbf{y}^{u}$ that maximized the conditional likelihood of $\mathbf{Y}^{u}$, given evidence $(\mathbf{X}=\mathbf{x}, \mathbf{Y}^{\ell}=\mathbf{y}^{\ell})$; i.e., $\arg\max_{\mathbf{y}} P(\mathbf{Y}^{u}=\mathbf{y}^{u} \mid \mathbf{X}=\mathbf{x}, \mathbf{Y}^{\ell}=\mathbf{y}^{\ell})$, (15.5)

where $\mathbf{y} = (\mathbf{y}^{\ell}, \mathbf{y}^{u})$. This type of inference—known alternately as *maximum a posteriori* (MAP) or *most likely explanation* (MPE)—is known to be NP-hard in general graphical models, though there are certain exceptions in which it can be computed efficiently, and many approximation algorithms that perform well in most settings. We will review selected inference algorithms where applicable.

# 15.5.1 Directed Models

The fundamental directed graphical model is a *Bayesian network* (also called *Bayes net*, or BN).