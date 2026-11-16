# Table 3.2 Action Rules for the Blocks World

| Rule | Formula |
| :--- | :--- |
| 1 | ∀x pickup(x) ⇒ (gripping(nothing) ∧ clear(x) ⇒ gripping(x)) |
| 2 | ∀x putdown(x) ⇒ (gripping(x) ⇒ clear(x) ∧ ontable(x) ∧ gripping(nothing)) |
| 3 | ∀x ∀y stack(x, y) ⇒ (gripping(x) ∧ clear(y) ⇒ gripping(nothing) ∧ on(x, y)) |
| 4 | ∀x ∀y unstack(x, y) ⇒ (on(x, y) ∧ clear(x) ∧ gripping(nothing) ⇒ gripping (x) ∧ clear(y)) |

![](bbox=[0.1, 0.22, 0.9, 0.56])

Figure 3.2 A portion of the state space tree when searching for a plan in the blocks world.

Next we need action rules for changing the state of the world. They are expressed in Table 3.2 using first-order logic.

These action rules mean that if we take the given action (make it true) stated as the premise of the rule, then the conclusion of the rule becomes true. For example, in rule 1 if we take the action to pickup(a), then if the robot is not gripping anything and a is clear, the robot will end up gripping a.

Now that we can describe the state of the world and the actions for changing, we can discuss developing a plan. One simple way to obtain a plan is to perform a breadth-first search of possible moves. When we arrive at the state that is our goal, the plan is the sequence of moves that led to that state. Figure 3.2 shows a portion of the search. The problem with this method is that it becomes computationally unfeasible for large problem instances. In Section 3.2.2.2 we discuss a way to address this problem.

The blocks world suffers from the frame problem, which concerns expressing using logic those aspects of the world that remain unchanged by an action