30 seconds if you like. You can make a commit every time you get a unit test to pass.

And that brings us to the point of this whole historical discussion.

If you stand back and look at the trajectory of the evolution of source code control systems, you can see that they have been driven, perhaps unconsciously, by a single underlying imperative.

# Short Cycles

Consider again how we began. How long was the cycle when source code was controlled by physically possessing a deck of cards?

You checked the source code out by taking those cards out of the cabinet. You held on to those cards until you were done with your project. Then you committed your changes by putting the changed deck of cards back in the cabinet. The cycle time was the whole project.

Then, when we used thumbtacks on the bulletin board, the same rule applied. You kept your thumbtacks in the modules you were changing until you were done with the project you were working on.

Even in the late 1970s and into the 1980s when we were using SCCS and RCS, we continued to use this pessimistic locking strategy, keeping others from touching the modules we were changing until we were done.

But CVS changed things—at least for some of us. Optimistic locking meant that one programmer could not lock others out of a module. We still committed only when we were done with a project, but others could be working concurrently on the same modules. Consequently, the average time between commits on a project shrank drastically. The cost of concurrency, of course, was merges.

And how we hated doing merges. Merges are awful. Especially without unit tests! They are tedious, time-consuming, and dangerous.

Our distaste for merges drove us to a new strategy.