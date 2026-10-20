example. That is, consider taking the square
of the number on the top of the stack. The
undo operation would be to take the square
root of the result of the squaring operation.
However, was the original number the
positive or negative root of the square?
Without retaining additional state
information, the inversion method breaks
down.

The alternative to implementing undo as an
inverse operation is to preserve the state of
the system before the command is first
executed and then implement the undo as a
reversion to this prior state. Returning to our
example of squaring a number, the forward
operation would both compute the square, but
also save the top number on the stack. The
undo operation would then be implemented
by dropping the result from the stack and
pushing the saved state from before the
forward operation was performed. This
procedure is enabled by the command pattern
since all commands are implemented as
instantiations of concrete command classes
that are permitted to carry state. An