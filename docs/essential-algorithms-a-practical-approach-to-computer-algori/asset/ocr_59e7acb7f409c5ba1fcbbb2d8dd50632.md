You can use branch and bound and heuristics on the optimization version of this problem but not on the nonoptimization version.

# Bin Packing

In the *bin-packing* problem, you have a set of items of different weights and a series of bins that have the same capacity. (In a generalized version, the bins could have different capacities.) The goal is to pack the items into the bins so that you use as few bins as possible.

You could model this as a decision tree in which each branch corresponds to putting an item in a particular bin. If you have N items and K bins, the tree would have N levels with K branches at each node, so the tree would have $K^N$ leaf nodes.

This is an optimization problem. You can use branch and bound and heuristics to try to find good solutions.

A related problem is to find a way to pack the items into bins so that you use only⌈weight of all items+bin capacity⟩⌈ where ⌈ means to round up. For example, if the total weight of the items is 115, and the bins have a capacity of 20, you can find a way to pack the items into six bins? You can use heuristics to try to find a good solution, but if you don't find a solution, that doesn't mean no one exists.

# Cutting Stock

The cutting stock problem is basically a two-dimensional version of the bin-packing problem. In this problem, you need to cut out a collection of shapes (usually rectangles) from a set of boards, pieces of cloth, or other stock. The goal is to use as few pieces of stock as possible.

Modeling this problem as a decision tree is much harder than it is for the bin-packing problem, because how you position shapes on a piece of stock changes the number of pieces you can fit on that piece. That means assigning a shape to a piece of stock is not enough. You must also assign a position to the shape within the stock. If you have K pieces of stock, there are more than K places where you can position a shape, a node may have more than K branches.

If you make some simplifying assumptions, you can use a decision tree for this problem. For example, if the pieces of stock are 36 inches by 72 inches, and you allow a shape to be positioned at only an (X, Y) position where X and Y are integer numbers of inches, there are $36 \times 72 = 2,592$ positions where you can place a shape on a particular piece of stock. That means each node in the tree would have $K \times 2,592$ branches.

Fortunately, many of those branches are easy to trim from the tree. For example, some branches place a shape so close to an edge of the stock that it won't fit.