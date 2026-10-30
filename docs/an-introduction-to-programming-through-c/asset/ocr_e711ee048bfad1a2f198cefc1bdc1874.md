be important.¹ As mentioned earlier, when showing the results of a search, it is considered appropriate to show the important pages first, and hence estimating the importance of a page is of great value to search engine companies.

It is most natural to use an adjacency matrix T, often called the transition matrix, to represent the network of pages. The basic operation in the calculation of the page ranks will be the multiplication of this matrix using a suitable vector. We will soon describe the exact content of T, but before that we need to make our surfing model a bit more precise.

Suppose at some time t the surfer is at some page p. It is customary to assume that time is divided into steps. At each step, the surfer decides whether he/she wants to continue with that page or click a link and go to some other page. It is customary to assume that with probability 0.5 the surfer will stay on the same page at time t + 1 as he is on at time t. With probability 0.5 the surfer will click on one of the links in the page, with the link being chosen at random. Thus if d_p denotes the number of outgoing links from the page, then the probability that the surfer uses a specific link to leave the page is 0.5/d_p. The matrix is constructed so that T_ij will denote the probability that a surfer at page i in step t goes to page j in step t + 1. Clearly we have:

T_ii = 0.5 (21.1)
T_ij = 0.5/d_i if there is a link from page i to page j. (21.2)
T_ij = 0 if there are is no link from page i to page j. (21.3)

Thus for the set of pages and the links between them as shown in Figure 21.1, the transition matrix will be:

T = ( 0.5 0.5 0 0 0
0 0.5 0.25 0.25 0
0.17 0 0.5 0.17 0.17
0.5 0 0 0.5 0
0.5 0 0 0 0.5 )

As an example, from page 2 we have 3 outgoing links, to pages 0, 3, and 4. Thus we have T_20 = T_23 = T_24 = 0.5/3 ≈ 1.7. And since there is no link to page 1 we have T_21 = 0, and of course T_22 = 0.5.

Suppose we are given the (row) vector x where x_i denotes the probability of the surfer being at page i at a certain step t. From page i the surfer moves to page j with probability T_ij. Thus the probability that at time t the surfer is at page i and that at time t + 1 the surfer is at page j is x_i T_ij. Thus to find the probability y_j of the surfer being at page j at time t + 1 we merely need to add the terms x_i T_ij over all choices of i. Thus we have

y_j = Σ_i x_i T_ij

In other words, if y denotes the vector with entries y_j, then we have

y = x T