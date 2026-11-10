# # Chapter 8

# ## MATLAB Illustrations on Fuzzy Systems

This chapter illustrates some applications of Fuzzy systems such as Fuzzy Washing Machine, Fuzzy Control System, and approximation of sinusoidal functions in MATLAB.

# ### 8.1 Illustration 1: Application of Fuzzy Controller Using MATLAB — Fuzzy Washing Machine

Today many household appliances have fuzzy logic built into them to make their use easier. Fuzzy logic is found in shower heads, rice cookers, vacuum cleaners, and just about everywhere. In this section we will look at a simplified model of a fuzzy washing machine.

Like a real washing machine would, the model first tests how dirty the laundry is. Once it knows how dirty the laundry is, it can easily calculate how long it should wash it. To calculate this it uses the graph shown in Figure 8.1:

First it always takes a base of 10 minutes. It does this so that people are happy with its work even if they put completely clean laundry in to wash. It then calculates to what degree it is dirty. If it is 100% dirty it adds two minutes per piece of laundry. Of course a real washing machine would just do these calculations in the end, but this model does it for each individual piece so you can keep track of what is going on easier.

On the graph in Figure 8.1, the base of ten minutes is shown. The point 0.0 is where the laundry is completely clean; non-dirty and non-greasy. The point 0.1 is where the laundry is non-greasy, but dirty. The point 1.0 is where it is greasy but not dirty and 1.1 is greasy and dirty. The washing machine adds 2 minutes per piece for 100% dirty or 100 % greasy and 4 minutes for 100% dirty and greasy.

There has been a boom for fuzzy machines in the last two decades. This is not only because they can do things, which humans had to do