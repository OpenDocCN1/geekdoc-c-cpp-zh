![](bbox=[0.355, 0.119, 0.655, 0.285])

Fig. 3. Solution of the differential equation system.

![](bbox=[0.355, 0.356, 0.655, 0.522])

Fig. 4. Phase plane.

Since the classical model ignores spatial correlations it does not take into account important effects that spatial inhomogeneity may cause on the dynamics of the system. Moreover in such a model we do not have any information about the spatial distribution of the populations.

# 2.3 Description of the cellular automata simulation

The following five parameters need to be chosen to set up a simulation: 1. number of fish; 2. number of sharks; 3. fish reproductive age; 4. sharks reproductive age; 5. sharks starvation period. The initial number of sharks and fish as their respective ages are randomly distributed in a rectangular grid whose opposite sides are identified in pairs. The cells states in the grid are updated according to the local dynamical rules of each cell. For instance, in a 40x40 cell grid, 300 fish and 10 sharks are placed at random positions. All fish and sharks have a reproductive age, i.e., 3 and 10 iterations respectively and sharks starvation period is 3.

# 2.3.1 Behavior of fish in Wa-Tor

Each fish chooses a free place in its neighborhood, moves and ages there (if all places are occupied, then it remains where it is and ages). When it achieves the reproductive age, it leaves behind a single offspring. They move according to a randomly assigned integer that indicates a direction. More specifically, depending on whether the value of the integer is equal