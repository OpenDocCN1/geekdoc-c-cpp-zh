The ▷ operator, unlike addition for the real and natural numbers, is not commutative or associative. Observe that

(1, 1) ▷ (0, 1) = (1, 2)

but

(0, 1) ▷ (1, 1) = (1, 0)

and so a ▷ b ≠ b ▷ a; the first and second arguments cannot be interchanged. Also observe that

((1, 0) ▷ (1, 1)) ▷ (0, 1) = (2, 1)

but

(1, 0) ▷ ((1, 1) ▷ (0, 1)) = (2, 0)

and so (a ▷ b) ▷ c ≠ a ▷ (b ▷ c); changing the order in which ▷ is applied changes the outcome of the calculation.

The trajectories of a discrete-event system are functions from ℝ × ℕ to the set X (an input trajectory), Y (an output trajectory), and Q (a state trajectory). The operator ℓ gives the real length of a trajectory, specifically

ℓ(ζ < (t₁, c₁), (t₂, c₂) >) = φ((t₂, c₂)) − φ((t₁, c₁)) = t₂ − t₁    (4.5)

Recall that the trajectories of a discrete-event system change only a finite number of times in any interval of finite length. The input and output trajectories satisfy one additional property—they are equal to the nonzero Φ at all except a finite number of points in any finite interval. Trajectories that satisfy this second property are called *event trajectories*, and legitimate discrete-event systems provided an event trajectory at their input produce an event trajectory at their output.¹

Figure 4.1 illustrates an event trajectory. Real time flows from left to right. At each real instant of time there can be a finite number of discrete transitions. Discrete time at each point of real time flows from bottom to top. The value of each event is written at its location in the time plane.

The rules introduced in Section 3.1.1 for concatenating trajectories are unchanged, but the convenience of “translate and concatenate,” the • operator, is lost because without addition trajectories are not easily translated. The · operator is still applicable, and it will play the same role in defining the state transition function of a discrete-event system that it played for discrete-time systems.

¹ A system that, given an event trajectory at its input, does not produce an event trajectory at its output is called illegitimate or, more recently, Zeno. The term illegitimate is due to Zeigler (see, e.g., Ref. 152); Zeno is a modern term, inspired by Zeno’s paradox of Achilles and the Tortoise, for the same concept (see, e.g., Ref. 160).