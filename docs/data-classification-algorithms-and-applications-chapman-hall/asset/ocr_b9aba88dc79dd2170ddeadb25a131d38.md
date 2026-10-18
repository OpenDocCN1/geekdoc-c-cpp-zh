# Algorithm SubspaceDecisionPath(Test Example: t, Data Set: D, MaxDimensionality: l, MaxBranchFactor: b_max, Minimum Interest Ratio: ir_min)

```
begin
  PATH = {D};
  while not(termination) do
  begin
    Pick the last data set L indicated in PATH;
    E = {E1 ... Eq} = ComputeClassificationSubspaces(L, t, l, b_max, ir_min);
    for each Ei ConstructDensityProfile(Ei, L, t);
    { "Zooming in" refers to further subspace exploration }
    if (zoom-in (user-specified)) then
    begin
      User specifies choice of branch Ei;
      User specifies accuracy density threshold λ for zoom-in;
      { p(L', Ci) is accuracy significance of class Ci in L' with respect to L }
      (L', p(L', C1) ... p(L', Ck)) = IsolateData(L, t, λ);
      Add L' to the end of PATH;
    end;
    else begin (retreat)
      User specifies data set L' on PATH to backtrack to;
      Delete all data set pointers occuring after L' on PATH; (backtrack)
    end;
    { Calculate cumulative dominance of each class Ci along PATH in order to provide the user a measure of its significance }
    for each class Ci do
      Output CD(PATH, Ci) = 1 − ∏_{L∈PATH, L≠D} (1 − p(L, Ci)) to user;
  end;
end
```

# FIGURE 6.5: The subspace decision path method.

diagnostic characteristics, a maximum branch factor b_max, and a minimum interest density ir_min. In addition, the maximum dimensionality l of any subspace utilized in data exploration is utilized as user input. The value of l = 2 is especially interesting because it allows for the use of visual profile of the accuracy density. Even though it is natural to use 2-dimensional projections because of their visual interpretability, the data exploration process along a given path reveals a higher dimensional combination of dimensions, which is most suitable for the test instance. The branch factor b_max is the maximum number of possibilities presented to the user, whereas the value of ir_min is the corresponding minimum interest density of the test instance in any subspace presented to the user. The value of ir_min is chosen to be 1, which is the break-even value for interest density computation. This break-even value is one at which the interest density neither under-estimates nor over-estimates the accuracy of the test instance with respect to a class. The variable PATH consists of the pointers to the sequence of successively reduced training data sets, which are obtained in the process of interactive decision tree construction. The list PATH is initialized to a single element, which is the pointer to the original data set D. At each point in the decision path construction process, the subspaces E1 ... Eq are determined, which have the greatest interest density (of the dominant class) in the locality of the test instance t. This process is accomplished by the procedure ComputeClassificationSubspaces. Once these subspaces have been determined, the density profile is constructed for each of them by