(in contrast to the direct requirement matrix) is the sum of an infinite series starting with the identity matrix I:

I = I + A + A² + A³ + … = ∑_{n=0}^{∞} Aⁿ

Leontief realized that this is simply the matrix inversion

L = (I − A)⁻¹

Each element of the matrix Leontief inverse matrix L thus reports the total quantity input required to produce one unit of output. The inputs can be weighted by their environmental load, using the satellite indicators, in order to find the environmentally weighted total input required for each unit product produced.

Structural Path Analysis (SPA) can be used to selectively perform this series expansion on individual elements and trace out supply chains. SPA is commonly used to search the top-ranked (largest flow) supply chain or chains, starting or ending at sectors of interest. The idea of SPA is not difficult but implementation is an art. SPA algorithms must essentially search a 15,000 * 15,000 = 225,000,000-branch tree whose leaf node values asymptotically approach zero with depth. In the worst case, a single input could visit every single sector in the world before being finally consumed. In practice, evaluating each supply chain to 10 to 15 steps captures 99% of the chain’s value. Still, intelligent heuristics for pruning and sorting are mandatory. The Leontief inverse and SPA are used complementarily. Footprints calculated using the Leontief inverse report the total footprint of products and sectors and SPA algorithms search for the individual supply chains involved.

# 2.6 APPLICATIONS OF THE EORA MRIO

The Eora MRIO provides a time series of MRIO tables with matching environmental and social satellite accounts for the entire world economy at a high level of sector and country detail. Some 187 countries are represented at resolutions of 25 to 500 sectors, depending on raw data availability, tracing over 5 billion supply chains. The time series covers 1990 to 2010. The Eora MRIO presents a completely harmonized and balanced world MRIO table, incorporating millions of raw data points from major sources