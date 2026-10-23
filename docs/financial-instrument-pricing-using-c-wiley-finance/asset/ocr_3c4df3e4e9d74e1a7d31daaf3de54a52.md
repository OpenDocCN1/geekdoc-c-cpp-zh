```
std::cout << "Euro call: " << euroCallPrice;

// Price an early exercise option
double earlyPutPrice = BackwardInduction<double>
    (asset, earlyPut, algo, PutPayoff,
     AmericanPutAdjuster);
std::cout << "Early put: " << earlyPutPrice;

double earlyCallPrice = BackwardInduction<double>
    (asset, earlyCall, algo, CallPayoff,
     AmericanCallAdjuster);
std::cout << "Early call: " << earlyCallPrice;
```

You can run this code and check the output. The above algorithms can run in parallel because the asset lattice is read-only shareable and each algorithm runs in its own thread. We discuss this case in detail in a later chapter. We have discovered a pattern here in the sense that several algorithms in Layer 2 can use the same data structures as in Layer 1. We shall see more examples of the same patterns of use when we discuss Monte Carlo simulation and the FDM in later chapters.

# 11.8 MERGING LATTICES

In some cases we may wish to produce a lattice, each of whose nodes are tuples consisting of the asset price and option price. To this end, one possibility is to compute the values in the asset and option lattices and then merge these two lattices to form a new lattice. This choice is useful because we may wish to print both asset and option prices in Excel or on the console, for example. To this end, we have created a function to merge two lattices having the same size. The function creates a lattice from two input lattices:

```
template <class Node, int LatticeType>
Lattice<std::tuple<Node,Node>, LatticeType> merge
    (const Lattice<Node,LatticeType>& latticeA,const Lattice<Node,
     LatticeType>& latticeB)
{ // Merge elements of two lattices to form a lattice of tuple

    Lattice<std::tuple<Node,Node>, LatticeType> result(latticeA.Depth());

    for (std::size_t n = latticeA.MinIndex(); n <= latticeA.MaxIndex();
         ++n)
    {
        for (std::size_t i = 0; i < latticeA[n].size(); ++i)
        {
            result[n][i] = std::make_tuple(latticeA[n][i],latticeB[n][i]);
        }
    }

    return result;
}
```