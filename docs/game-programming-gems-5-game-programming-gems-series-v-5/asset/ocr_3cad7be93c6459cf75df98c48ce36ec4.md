# Generic Pager

Ignacio Incera Cruz

ignacio@incera.net

We frequently find a situation in which at any given time we need to unload unnecessary information from our system in order to load new information. This simple task carries with it complicated management baggage to track the information that should be kept and that which may be excluded at any instant. The situation becomes even more complicated if there is more than one user that requires access to the same information at the same time. The process around this management of currently loaded data is commonly known as “paging.”

Traditionally, solving this problem means designing complicated systems that are not always as efficient as we hope; they are also usually very limited because they are specifically designed to solve a particular instance of the paging problem. This gem introduces a more general, less complicated, and more efficient solution to the paging problem, called the _generic pager_ (GP). By meeting all these criteria, the GP allows the system designer to completely forget about the challenges posed by creating a custom-brewed solution, allotting more of his valuable time for designing and implementing other critical parts of the title.

For you skeptics out there, I’d like to highlight the flexibility and efficiency of the GP presented in this gem by referring you to two major projects from completely unrelated domains.

+   • GP has been successfully integrated in an autonomous robots system where the resources of the robots are limited, and efficient management of the information needed at any given time is necessary.
+   • GP has been used in a navigation and visualization 3D terrain system.

# The Old Paging Solution: Check Everything

The most widespread (though not necessarily the best) solution consists of the following steps: