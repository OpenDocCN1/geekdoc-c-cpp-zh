the value of A is used as an operand of B, unless:

+   * B is an invocation of the kill_dependency macro,
* A is the left operand of a && or || operator,
* A is the left operand of a ? : operator, or
* A is the left operand of a , operator;

or A writes a scalar object or bit-field M, B reads from M the value written by A, and A is sequenced before B, or for some evaluation X, A carries a dependency to X and X carries a dependency to B.
An evaluation A is dependency-ordered before^{16)} an evaluation B if:

+   * A performs a release operation on an atomic object M, and in another, B performs a consume operation on M and reads a value written by any side effect in the release sequence headed by A, or
* for some evaluation X, A is dependency-ordered before X and X carries a dependency to B.

An evaluation A inter-happens before an evaluation B if A synchronizes with B, A is dependency-ordered before B, or for some evaluation X:
* A synchronizes with X and X is sequenced before
* A is sequenced before X and X inter-happens before B,
* A inter-thread happens before X and X inter-happens before B.

NOTE 7 The “inter-thread happens before” relation describes arbitrary concatenations of “sequenced before”, “synchronizes with”, and “dependency-ordered before” relationships, with two exceptions. The first exception is that a concatenation is not permitted to end with “dependency-ordered before” followed by “sequenced before”. The reason for this limitation is that a consume operation participating in a concatenation carries a dependency. The reason that this limitation applies only to one of such a concatenation is that subsequent release operation will provide the ordering for a prior consume operation. The second exception is that a concatenation is not permitted to consist entirely of “sequenced before”. The reasons for this limitation are (1) to permit “inter-thread happens before” to be transitively closed and (2) the “happens before” relation, defined below, provides for relationships consisting entirely of “sequenced before”.

An evaluation A happens before an evaluation B if A is sequenced before B or A inter-thread happens before B.

16) The “dependency-ordered before” relation is anomalous to the “synchronizes with” relation, but uses release/consume in place of release/acquire.