Zavalin's version of the SVF is not the solution. Simer (2011, 2013) details a completely different derivation and implementation of the SVF using analog circuit analysis with equivalent capacitor currents and nodal analysis. Simer also has optimized solutions for calculating the filter coefficients. See the Bibliography for more details.

# 4.12 Series and Parallel VA Filters

It is easy to derive the filter equations for the series and parallel VA filters shown in Figure 4.21, and they both end up as y = Gx + S type filters. Once again we only simple algebra and zero calculus to create the necessary filter equations. In the case of series filters, an intermediate node u is inserted between them and used to calculate the output.

Figure 4.21: Series (top) and parallel (bottom) connections of VA filters.

Figure 4.22: Three delay-less feedback networks; (a) the feed-forward path contains a simple multiplier (b) the feed-forward path is processed through some function f(u) and (c) the feed-forward path contains a multiplier and a function block; the block marked "Any Network" can contain anything that includes at least one (or more) delay-path.

![](bbox=[0.435, 0.273, 0.952, 0.513])

# 4.13 Resolving Delay-loss Loops: Modified Härmä Method

Next, let's look at some generic examples involving delay-loops to see how more

![](bbox=[0.435, 0.553, 0.952, 0.672])

complex structures can be realized using the Modified Härmä method. With it, you can easily find the filter structure that resolves the delay-loop. For a single loop filter, the process can be applied swiftly. Recursive filters will use one of the three forms shown in Figure 4.22. The box marked "Any Network" can be anything from a short, to a simple multiplier, to a complex network that includes at least one delay-path filter; if there is a processing function in the feed-forward path, it is shown as a generic function of the input f(u). In this notice generic examples, the variables labeled G and S are likewise generic—represent any coefficient multiplier.

Härmä describes the technique for the block diagram in Figure 4.22 (a) and with K = 1 so that the feed-forward path is a short circuit. We modify the technique (Pirkle, 2014) to accommodate the situations where there is something meaningful in the feed-forward path, either a constant gain or function of the loop input f(u). You can find the full derivation at http://www.willpirinkle/synthbook/. This modified method can be applied to any filter in the box and is named the Modified Härmä method. Both methods produce the same results and structures. We often found the Modified Härmä method produces results with quicker and faster execution than Zavalinin's basic idea is to split the algorithm/block diagram into two parts—one that depends only