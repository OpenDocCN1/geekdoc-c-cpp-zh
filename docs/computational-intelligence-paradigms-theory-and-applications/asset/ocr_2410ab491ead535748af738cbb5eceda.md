Again, the value of an element in the solution array does not exclude any values for other array elements, but the total number of steps in the optimal solution is not known at the start of the search.

Finally, diagonal moves can be allowed by letting each array element be a number between 1 and 8.

# *The Location/Allocation Problem Type*

In contrast to the other problem types described above, a solution vector for the Location/Allocation problem and the Conformation of a Molecule is a fixed length array of floating-point numbers, not integers. In the Location/Allocation problem, a company has many customers spread across a map and the object is to find the optimal location of a fixed number of distribution centers. If the user wants to place two distribution centers, the solution vector contains the following four floating-point numbers (X1,Y1,X2,Y2), where (X1,Y1) is the map coordinates of the first distribution center and (X2,Y2) is the map coordinates of the second. All customers would be serviced by the closest distribution center, and the quality of the solution could be either an unweighted sum of the distances to each customer, or a weighted sum of this distance so that a customer with many deliveries per month should be closer to the distribution center than one with few deliveries.

To determine the optimal conformation of a molecule, the molecule's geometry is uniquely determined by the values of the dihedral angle for all “rotatable bonds”. Therefore, if a molecule contains 4 rotatable bonds, a possible solution is described by an array of four floating-point numbers which set the values of these four dihedral angles. The quality of this solution is inversely proportional to the internal energy of this geometry, and the object is to find the values of the dihedral angles that yield the lowest internal energy.

Both of these problems have solutions that are fixed-length arrays of floating-point numbers, and the value of an array element in one position does not exclude any possible values at other positions in the array.

# **Extending the Coding Scheme**

Up to this point, the coding scheme has only been used to store a putative solution to the problem. There is no reason why this coding can't contain additional information.

Evolutionary Programming can use different *mutation operators* for a particular coding scheme. If two such operators are available in a particular algorithm, there is a probability that one or the other will be used. The value of this probability used to generate a putative solution can