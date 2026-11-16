# Algorithm 2.7 Planning_Agent

```
Procedure Planning;
A11 = true;
repeat
    Knowledge_Base = Knowledge_Base U set of new perceptions;
    using Deduction_Rules and Knowledge_Base,
    add all possible deductions to Knowledge_Base;
    if there is a current plan
        perform next action in that plan;
    else
        develop a new plan if possible and execute first action in the plan;
    if the current square contains the gold
        stop;
    else if the current square contains the wumpus or a pit
        die;
until stop is executed or agent is dead or there is no plan;
```

# 2.3.2.3 More Complex Wumpus World

We presented a very simple version of the wumpus world. Both the environment and the tasks required of the agent could be made more complex. For example, the agent could be required to turn and face a direction before moving in that direction, or the agent could be required to pick up the gold and return back to square [1,1] in order to succeed. The environment could include several squares containing gold or containing a wumpus, or the wumpus could be allowed to move.

# 2.4 Discussion and Further Reading

In the procedural approach to system design, the steps that accomplish the desired task are hard-coded in the program. We would be using this approach if we directly coded the decision tree in Figure 2.2. In the declarative approach, the knowledge is separated from the reasoning. This is the approach taken when we used forward chaining and backward chaining to reason with rules, and when we developed wumpus algorithms that reasoned with knowledge bases. Boden [1977] provides an early discussion of the two approaches, while Newell [1981] discusses the problem of representation and knowledge. The two approaches are contrasted further in [Brooks, 1991], [Nilsson, 1991], and [Shaparau et al., 2008].

XCON [McDermott, 1982] was a system that operated in a fashion similar to our grocery bagger. The system configured Digital Equipment Corporation's VAX computers. Since then propositional logic has been used to actually design computer hardware. For example, Norwick et al. [1993] discuss the design of a high-performance cache controller.

Yob [1975] developed the wumpus world. The version of the wumpus world shown here is based on one that appeared in [Russell and Norvig, 1995].