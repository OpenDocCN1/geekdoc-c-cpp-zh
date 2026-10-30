
be important.¹ As mentioned earlier, when showing the results of a search, it is considered appropriate to show the important pages first, and hence estimating the importance of a page is of great value to search engine companies.

It is most natural to use an adjacency matrix T, often called the transition matrix, to represent the network of pages. The basic operation in the calculation of the page ranks will be the multiplication of this matrix using a suitable vector. We will soon describe the exact content of T, but before that we need to make our surfing model a bit more precise.

Suppose at some time t the surfer is at some page p. It is customary to assume that time is divided into steps. At each step, the surfer decides whether he/she wants to continue with that page or click a link and go to some other page. It is customary to assume that with probability 0.5 the surfer will stay on the same page at time t + 1 as he is on at time t. With probability 0.5 the surfer will click on one of the links in the page, with the link being chosen at random. Thus if d_p denotes the number of outgoing links from the page, then the probability that the surfer uses a specific link to leave the page is 0.5/d_p. The matrix is constructed so that T_ij will denote the probability that a surfer at page i in step t goes to page j in step t + 1. Clearly we have:

T_ii = 0.5 (21.1)
T_ij = 0.5/d_i if there is a link from page i to page j. (21.2)
T_ij = 0 if there is no link from page i to page j. (21.3)

Thus for the set of pages and the links between them as shown in Figure 21.1, the transition matrix will be:

T = ( 0.5 0.5 0 0 0
0 0.5 0.25 0.25 0
0.17 0 0.5 0.17 0.17
0.5 0 0 0.5 0
0.5 0 0 0 0.5 )

As an example, from page 2 we have 3 outgoing links, to pages 0, 3, and 4. Thus we have T_20 = T_23 = T_24 = 0.5/3 ≈ 0.17. And since there is no link to page 1 we have T_21 = 0, and of course T_22 = 0.5.

Suppose we are given the (row) vector x where x_i denotes the probability of the surfer being at page i at a certain step t. From page i the surfer moves to page j with probability T_ij. Thus the probability that at time t the surfer is at page i and that at time t + 1 the surfer is at page j is x_i T_ij. Thus to find the probability y_j of the surfer being at page j at time t + 1 we merely need to add the terms x_i T_ij over all choices of i. Thus we have

y_j = Σ_i x_i T_ij

In other words, if y denotes the vector with entries y_j, then we have

y = x T

![](img/c7233aedab7e4c7cad32a7615b6a4783_359_0.png)

Figure 21.1: Pages with links

In other words, to get the probabilities for the next step, we need to multiply the probability vector for the current step by the transition matrix T. Thus the probabilities at t, t + 1, t + 2, … are simply

x, xT, xT², xT³, …

We have already seen the code for multiplying a matrix by a column vector; the code for multiplying a row vector by a matrix is very similar. This is all that is needed!

So suppose now that we are at page 0. This corresponds to x being the vector (1, 0, 0, 0, 0). We can use the above method to find the probabilities of visiting different pages as the time increases. Indeed, if you compute xT¹⁰, we get

x ≈ (0.3, 0.3, 0.15, 0.225, 0.025)

You will see that the vector does not change much with subsequent multiplications. Thus from this calculation it would seem that pages 0,1 are most important, and page 4 the least.

## 21.4 Circuits

We will consider the problem of finding the currents and voltages at different points in a circuit consisting of resistors and current sources, such as the one shown in Figure 21.2. You may perhaps not be familiar with current sources, the specified current flows out of them no matter what they connect to. Circuits which contain voltage sources can also be analyzed, but the algebra is slightly more complicated. We will discuss this later.

First we view this circuit as a graph, i.e. identify the vertices and edges in it. The resistances and the current source can be considered to be the edges, the points at which these attach to each other can be considered to be the vertices. There are 6 nodes in Figure 21.2, numbered 0 to 5, shown as solid circles. There are 9 edges, one consisting of the voltage source, and 8 consisting of resistors. It is possible to have circuits in which there are devices which have more than two electrical connections to them, such as transistors. The model for such graphs will be different.

![](img/c7233aedab7e4c7cad32a7615b6a4783_360_0.png)

### Figure 21.2: Circuit to be analyzed

It could be said that the graph of a circuit is commonly represented by its adjacency matrix, the so called conductance matrix which we will denote by G. The entries of the matrix are filled in a special way, so as to help in analysing the circuit. Specifically we will have

- 1. G_ij = -1/R_ij : if R_ij is the value of the resistance connecting vertices i and j, where i ≠ j. Note that if no resistor is shown between vertices i, j then we consider the resistance between them to be ∞, in which case G_ij = 0. You may know that a resistance of value R is the same as a conductance of value 1/R. Thus G_ij can be considered to be the negative of the conductance connected between nodes i, j.
- 2. G_ii = Σ_j 1/R_ij : The value of G_ii is thus set to be the sum of the conductances connected to vertex i.

Note that the current source values does not figure in setting the values of the conductance matrix.

You can see that the conductance matrix can roughly be considered to be an adjacency matrix for the circuit: the entries are 0 when there is no connection, and the entries are large (though negative) when there is a high conductance between two vertices. But the real motivation in setting the entries in this manner is that it helps in circuit analysis.

with the matrix and vectors shown in full becomes

Note that in our example, S₀ = 1 because unit current must flow out of vertex 0 into the current source. Similarly, S₁ = −1 because unit current must flow in to vertex 1 from the current source. There are no current sources associated with the other vertices, and hence the corresponding Sᵢ are 0. Let us first write down the equation for our circuit, after that we will explain why the equation is correct.

A matrix equation really consists of as many ordinary equations as there are rows. So for example, considering the first row of the product we will get:

V₀(1/5 + 1/3) + V₁(−1/5) + V₅(−1/3) = −1

This equation really turns out to be saying that the total current entering vertex 0, through voltage sources and resistors, must equal 0, since charge cannot be created nor destroyed. This can be seen if we rewrite the equation a bit.

(V₀ − V₁) · 1/5 + (V₀ − V₅) · 1/3 + 1 = 0

In this you can see the first term (V₀ − V₁) · 1/5 as the current entering vertex 0 through the 5 Ohm resistance, (V₀ − V₅) · 1/3 as the current entering through the 3 Ohm resistance, and 1 as the current entering through the current source. Indeed you will see the iᵗʰ row of the matrix equation to simply be asserting that the total current leaving and entering vertex i must be 0. Thus the matrix equation is valid.

Thus, analysis of this circuit is merely solving this set of equations! And we know how to do it from Section 14.2.1! There is one slight twist. You may know that voltages in a circuit are relative, i.e. we can arbitrarily designate one of the voltages to be 0. For example, we can substitute V₀ into the matrix. We will now get n equations but only n − 1 unknowns! However, this is not a problem: one of the equations is superfluous, it does not contain new information, and can indeed be obtained by adding the remaining equations! Thus, we can remove one of the equations too. Typically we remove the equation for the same node for which we set the voltage value to 0. This is equivalent to removing row 0 from the matrix and from both vectors, and also column 0 of the matrix. Thus we will get a system of equations in n − 1 variables which we can solve as per Section 14.2.1.

We can compute the currents in the different resistors by multiplying by the voltage drop across the resistance. Thus the current through the 4 Ohm resistance in the direction vertex 1 to vertex 2 is (V₂ − V₁) · 1/4, which can be calculated given values of V₁, V₂.

We finally consider how to deal with voltage sources. Suppose we have a voltage source connecting vertices i, j. Then we will need to have an additional variable Iᵢⱼ to represent the current through that voltage source. But we will also have an equation, viz. Vᵢ − Vⱼ must equal the specified voltage source value. Thus again we will have as many equations as there are unknowns, and we can solve the system.
