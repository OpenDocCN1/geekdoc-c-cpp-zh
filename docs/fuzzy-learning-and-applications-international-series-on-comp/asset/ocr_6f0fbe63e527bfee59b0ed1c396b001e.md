assumed that M(1) = M(2) = 0.3n, because we know that if there are fewer 1s in each row or column it is not necessary to make great modifications in the HCs for the first two surrounding conditions. Vice versa, if the number of 1s in each row or column is greater than 0.3n, there is a great violation of the invalidity condition and robust tuning of the relative HCs is needed. The same considerations hold for M(3) = 1.5n.

# TSP: Szu's Solution by Hopfield Network

The Hopfield and Tank's paper [2] has stirred a great deal of interest in solving the TSP. Many researchers have investigated both modifications to the Hopfield and Tank's network energy function, and other architectures to solve the problem. David Van den Bout and T.K.Miller [24] did work with a Hopfield network that had a simpler energy function but relied on a simulated annealing schedule to ensure good itineraries. Durbin and Willshaw [25] came up with an elastic net method. This method was further refined by D.J.Burr [26] by adding an annealing schedule to the elastic net method, which generates good solutions more quickly. H. Szu [5] suggested a modification to the Hopfield and Tank's original net. In the following, this modification will be clearly explained.

Szu's modification to the Hopfield and Tank's network is to change the C term in the energy function so that there is a separate excitation on a per row and per column basis. Thus all the neurons in a row or column will get excited whenever no neurons are firing in the respective row/column. In the Hopfield and Tank's solution the excitation is on entire network basis. By exciting just the row or column, only the appropriate neurons can possibly turn on.

The Szu's energy function is characterized by the following five terms:

E = A/2 Σ_{x,i,j≠i} O_{xi}O_{xj} + B/2 Σ_{i,x,y≠x} O_{xi}O_{yi} + C/2 Σ_x (Σ_i O_{xi} -1)^2 + C/2 Σ_i (Σ_x O_{xi} -1)^2 + D/2 Σ_{x,y≠x,i} d_{xy} O_{xi}(O_{y,i+1} + O_{y,i-1}) (8.15)

where, as seen before, each coefficient (A,B,C,D) (HCs) refers to the surrounding conditions in the order in which they are described, and the term d_{xy} represents the distance between the generic adjacent cities x and y.

# Membership Functions Choice

The TSP solution by Szu features four surrounding conditions. The meaning of the values of the variable c (c can be equal to 1,2,3 or 4) was previously described. Table 8.2 shows the values of the parameters m(c), t(c), M(c) and Cause(c) for each HC related to the