2 and so on till 256 nodes at distance 8, and the remaining 1000 − 256 − 128 − ⋯ − 1 = 489 nodes at level 9. So the height of this tree would be 9.

So it is nice to know that on the average we are likely to be much closer to the best height rather than the worst. Or alternatively, on the average our find and insert functions will run fast.

# 22.2.6 Balancing the search tree

You might be bothered that the above program will work fast “on the average”, but might take very long if you are unlucky. What if the numbers in the set got inserted in ascending order, or some such bad order?

In that case there are advanced algorithms that try to balance the tree as it gets built. This is done by modifying an already built tree, and say changing the root. With such rebalancing, it is indeed possible to ensure that the height of the tree remains small. Further, rebalancing algorithms have been developed that also run very fast. But this is outside the scope of this book.

# 22.2.7 Search trees and maps

The (index,value) pairs constituting a map from the C++ Standard Library are stored using binary search trees. The ordering rule is that all pairs in the left subtree must have index smaller than that at the root, which in turn must be smaller than the indices of the elements in the right subtree. Further, the tree is kept balanced as discussed above. Thus making an access such as value[index] happens fairly fast, i.e. in time proportional to log₂ n, where n is the number of pairs stored in the map.

# 22.3 Exercises

+   1. Extend the formula drawing program so that it allows the operators '∗', '+' and '−'. This is not entirely trivial: make sure your program works correctly for input ((x+3)*(x−2)). You will see that you may need to add parenthesization to the output. For simplicity, you could parenthesize every expression when in doubt.
+   2. Add an operator '^' to denote exponentiation in the formula drawing program. In other words, Node('^',Node("x"), Node("y")) which will print as x^y.
+   3. Allow the implicit multiplication operator, i.e. it should be possible to draw x^(n)/(v).
+   4. Suppose the user gives the position of the top left corner of the bounding box of the formula. Show how you could do this. Also if the user asks that the formula be centered at some given point.
+   5. Write a constructor function which takes as input a single reference argument, infile& which is a reference to an istream, and constructs an expression based on what it reads there. The associated file should contain valid expressions but written in a prefix form. Note that in the prefix form, the operator comes first, and every operator is