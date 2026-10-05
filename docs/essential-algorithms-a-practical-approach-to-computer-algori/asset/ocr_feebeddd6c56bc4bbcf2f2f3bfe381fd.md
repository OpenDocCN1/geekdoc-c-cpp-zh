# 550 Appendix B Solutions to Exercises

a traitor, and there's no rule that they need to obey a traitorous general. However, there is a rule that two loyal lieutenants must decide on the same action, and in this case they don't.

+   7. That would work in both of the situations shown in Figure 18-2. In both situations, the lieutenants receive conflicting instructions, so they retreat.

However, suppose the general is loyal (as in the situation on the right of Figure 18-2). The general orders an attack, and the treacherous lieutenant on the right lies about it. In that case, the lieutenant on the left receives conflicting orders, so he retreats, violating the general's.

+   8. No, there isn't enough information for the loyal lieutenants to identify the traitor. For example, consider two scenarios. First, suppose the general is a traitor who tells the first lieutenant to attack and the other lieutenants to retreat. The lieutenants exchange information, they believe they were all told to retreat, except for the first lieutenant.

For the second scenario, suppose the first lieutenant is a traitor. The general tells all the lieutenants to retreat, but the traitor tells the others that the general told him to attack.

The lieutenants receive the same information in both scenarios, they cannot tell whether the traitor is the general or the first lieutenant.

These two scenarios hold no matter many lieutenants are there, so there is no way to identify the traitor.

(The traitor could also act if he is loyal and not give conflicting orders. There is no way to detect him, although he won't cause any harm that we might either.)

+   9. Suppose the general tells two lieutenants to attack and two to retreat. After exchanging orders, the lieutenants believe two attack orders and two retreat orders were given. A single traitor could not create such a set of orders, so the traitor must be the general.

If this occurs, the lieutenants don't need to obey the traitor, but they still need to agree on a common decision. They can do that with a predefined rule that says, "The commanding general is a traitor, retreat."

+   10. The dining philosophers assume that the philosophers cannot talk to each other. If they let them, they can elect a leader who can act as a waiter.

+   11. A bully algorithm would let a philosopher remove a fork from a philosopher who has a lower ID. That would help if the philosophers don't eat often. But if they eat a large percentage of the time, this might lead to a livelock in which philosophers with lower IDs don't get to eat very often.

+   12. If the philosophers want to eat too often, they probably will waste a lot of time waiting for forks. A waiter who allows all odd-numbered philosophers to eat at the same time and then allows even-numbered philosophers to eat at the same time would be much more efficient than a free-for-all.