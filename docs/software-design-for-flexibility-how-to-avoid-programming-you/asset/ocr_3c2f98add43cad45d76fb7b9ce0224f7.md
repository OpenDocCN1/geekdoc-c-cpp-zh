eliminate the specific idea of king and non-king pieces, instead using a symbolic type. This introduces two new operations:

(piece-type piece)
gets the type of piece.

(piece-new-type piece type)
gets a new piece identical to piece except that it has the given type.

We redefine should-be-crowned? and crown-piece to use the piece type, so they behave the same as before, but they are no longer part of the core domain model.

Although the procedure possible-directions is specific to checkers, we will use it here, but only when defining the rules of checkers. It is not part of the new domain model.

The step data structure is specific to checkers, because it specifies whether a step is a jump. We will replace it with a more general structure called a change:

(make-change board piece flags)
creates a new change object. The argument is a list of symbols that we can use to indicate changes of state such as capture of a piece. The selectors get-board, get-piece, and get-flags can be used to get the corresponding parts of a change.

Like the piece type, the change flags provide a way to add game-specific features to the domain model without baking them in.

We will replace the path idea with a more abstract notion called a partial move. A partial move consists of an initial board and piece, together with zero or more changes. Our code uses the identifier pmove for a partial move.

(initial-pmove board piece)
creates a pmove with no changes and no flags.

(is-pmove-empty? pmove)
tests whether pmove pmove is empty: in other words, if it has no changes.

(is-pmove-finished? pmove)