distribution. RDN inference is therefore only approximate, but can be very fast. Learning RDNs is also fast, because it reduces to independently learning a set of CPDs.

# 15.5.2 Undirected Models

While directed graphical models are useful for their representation of causality, sometimes we do not need (or want) to explicitly define causality; sometimes we only know the interactions between random variables. This is where undirected graphical models are useful. Moreover, undirected models are strictly more general than directed models; any directed model can be represented by an undirected model, but there are distributions induced by undirected models that cannot be reproduced in directed models. Specifically, graph structures involving cycles are representable in undirected models, but not in directed models.

Most undirected graphical models fall under the umbrella of Markov random fields (MRFs), sometimes called Markov networks [40].

Definition 15.5.2 (Markov random field) A Markov random field (MRF) is defined by a set of random variables Z ≡ {Z1, …, Zn}, a graph G ≡ (V, E), and a set of clique potentials {φc : dom(c) → ℝ}c∈C, where C is a set of predefined cliques and dom(c) is the domain of clique c. (To simplify notation, assume that potential φc only operates on the set of variables contained in clique c.) The potentials are often defined as a log-linear combination of features fc and weights wc, such that φc(z) ≡ exp(wc · fc(z)). An MRF defines a probability distribution P that factorizes as

P(Z = z) = 1/Φ ∏_{c∈C} φc(z) = 1/Φ exp( ∑_{c∈C} wc · fc(z) ),

where Φ ≡ ∑_{z'} ∏_{c∈C} φc(z') is a normalizing constant. This model is said to be Markovian because any variable Zi is independent of any non-adjacent variables, conditioned its neighborhood Z_{N(i)} (sometimes referred to as its Markov blanket).

For collective classification, one can define a conditional MRF (sometimes called a CRF), whose conditional distribution is

P(Y^u = y^u | X = x, Y^ℓ = y^ℓ) = 1/Φ ∏_{c∈C} φc(x,y) = 1/Φ exp( ∑_{c∈C} wc · fc(x,y) ).

For relational tasks, such as collective classification, one typically defines the cliques via templating. Similar to a PRM (see Section 15.5.1), a clique template is just a subgraph pattern—although in this case it is a fully-connected, undirected subgraph. The types of templates used directly affects model complexity, in that smaller templates correspond to a simpler model, which usually generalizes better to unseen data. Thus, MRFs are commonly defined using low-order templates, such as singletons, pairs, and sometimes triangles. Examples of templated MRFs include relational MRFs [40], Markov logic networks [36], and hinge-loss Markov random fields [2].

To make this concrete, we consider the class of pairwise MRFs. A pairwise MRF has features and weights for all singleton and pairwise cliques in the graph; thus, its distribution factorizes as

P(Z = z) = 1/Φ ( ∏_{i∈V} φi(z) ) ( ∏_{(i,j)∈E} φi,j(z) ) = 1/Φ exp[ ( ∑_{i∈V} wi · fi(z) ) + ( ∑_{(i,j)∈E} wi,j · fij(z) ) ].