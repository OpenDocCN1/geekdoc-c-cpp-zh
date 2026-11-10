+   - *Write Barriers.* Intercept writes of references into a *Scanned* object \(o_1\), when the reference is to an *Unreached* object \(o_2\). In this case, classify \(o_2\) as reachable and place it in the *Unscanned* set. Alternatively, place the written object \(o_2\) back in the *Unscanned* set so we can rescan it.
+   - *Read Barriers.* Intercept the reads of references in *Unreached* or *Unscanned* objects. Whenever the mutator reads a reference to an object \(o\) from an object in either the *Unreached* or *Unscanned* state, classify \(o\) as reachable and place it in the *Unscanned* set.
+   - *Transfer Barriers.* Intercept the loss of the original reference in an *Unreached* or *Unscanned* object. Whenever the mutator overwrites a reference in an *Unreached* or *Unscanned* object, save the reference being overwritten, classify it as reachable, and place the reference itself in the *Unscanned* set.

None of the options above finds the smallest set of reachable objects. If the tracing process determines an object to be reachable, it stays reachable even though all references to it are overwritten before tracing completes. That is, the set of reachable objects found is between \((R \cup New) - Lost\) and \((R \cup New)\).

Write barriers are the most efficient of the options outlined above. Read barriers are more expensive because typically there are many more reads than there are writes. Transfer barriers are not competitive; because many objects “die young,” this approach would retain many unreachable objects.

# Implementing Write Barriers

We can implement write barriers in two ways. The first approach is to remember, during a mutation phase, all new references written into the *Scanned* objects. We can place all these references in a list; the size of the list is proportional to the number of write operations to *Scanned* objects, unless duplicates are removed from the list. Note that references on the list may later be overwritten themselves and potentially could be ignored.

The second, more efficient approach is to remember the locations where the writes occur. We may remember them as a list of locations written, possibly with duplicates eliminated. Note it is not important that we pinpoint the exact locations written, as long as all the locations that have been written are rescanned. Thus, there are several techniques that allow us to remember less detail about exactly where the rewritten locations are.

+   - Instead of remembering the exact address or the object and field that is written, we can remember just the objects that hold the written fields.
+   - We can divide the address space into fixed-size blocks, known as *cards*, and use a bit array to remember the cards that have been written into.