probably greatly exceeds the cost of flexible design, both in the cost of disasters and in the lost opportunity costs due to the time of redesign and rebuilding. And if a significant fraction of the time spent reprogramming a system for a new requirement is replaced by having that system adapt itself to the new situation, that can be an even bigger win.

# The problem with correctness

> To the optimist, the glass is half full. To the pessimist, the glass is half empty. To the engineer, the glass is twice as big as it needs to be.
author unknown

There may be an even bigger cost to building systems in a way that gives them a range of applicability greater than the set of situations that we have considered at design time. Because we intend to be willing to apply our systems in contexts for which they were not designed, we cannot be sure that they work correctly!

In computer science we are taught that the “correctness” of software is paramount, and that correctness is to be achieved by establishing formal specification of components and systems of components and by providing proofs that the specifications of a combination of components are met by the specifications of the components and the pattern by which they are combined.¹19 We assert that this discipline makes systems more brittle. In fact, to make truly robust systems we must discard such a tight discipline.

The problem with requiring proofs is that it is usually harder to prove general properties of general mechanisms than it is to prove special properties of special mechanisms used in constrained circumstances. This encourages us to make our parts and combinations as special as possible so we can simplify our proofs. But the combination of tightly specialized parts is brittle—there is no room for variation.¹20

We are not arguing against proofs. They are wonderful when available. Indeed, they are essential for critical system components,