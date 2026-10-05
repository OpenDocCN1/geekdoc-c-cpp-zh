how easy it is to add some useful new behavior to the elementary unification procedure already built.

+   11 The extension to segments is very subtle. We thank Kenny Chen, Will Byrd, and Michael Ballantyne for helping us think about this experiment.

+   12 The procedure complement is a combinator for predicates: complement makes a new predicate that is the negation of its argument.

+   13 This is a one-sided match that could also be done with the earlier matcher, but this ability to match expressions with variables on both sides of the match is useful.

+   14 For an example of how a graph node is used, see g:cons on page 210. For a more complete description of bundle procedures see page 395.

+   15 Castling is another special case. Castling is allowed under restricted circumstances: when the king and the rook are in their initial positions, the squares between the king and rook are unoccupied, and the king is not in check and will not have to traverse or land in a square where it would be in check.

+   16 There is also a pawn move, en passant capture, that depends on the opponent's previous move.

+   17 We use zero-based indexing, unlike the traditional chess conventions, but this is not important except for input and output players.

+   18 But notice that the success continuation of the graph-matcher procedure is different from the success continuation of the expression-matcher procedure. The expression-matcher success continuation takes a dictionary and a number of elements eaten by the matcher (to make segments work), whereas the graph-matcher success continuation takes the final node and the dictionary resulting from matching the matched part of the graph.