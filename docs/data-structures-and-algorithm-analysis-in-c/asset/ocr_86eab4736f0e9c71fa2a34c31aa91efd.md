![](bbox=[0.05, 0.08, 0.75, 0.3])

Figure 10.69 Two searches that arrive at identical position

tree is actually constructed by the algorithm. The game tree is just an abstract concept.) The value of the game tree is 44.

Figure 10.71 shows the evaluation of the same game tree with several (but not all possible) unevaluated nodes. Almost half of the terminal nodes have not been checked. We show that evaluating them would not change the value at the root.

First, consider node D. Figure 10.72 shows the information that has been gathered when it is time to evaluate D. At this point, we are still in findHumanMove and are contemplating a call to findCompMove on D. However, we already know that findHumanMove will return at most 40, since it is a min node. On the other hand, its max node parent has already found a sequence that guarantees 44. Nothing that D does can possibly increase this value. Therefore, D does not need to be evaluated. This pruning of the tree is known as \(\alpha\) pruning. An identical situation occurs at node B. To implement \(\alpha\) pruning, findCompMove passes its tentative maximum (\(\alpha\)) to findHumanMove. If the tentative minimum of findHumanMove falls below this value, then findHumanMove returns immediately.

A similar thing happens at nodes A and C. This time, we are in the middle of a findCompMove and are about to make a call to findHumanMove to evaluate C. Figure 10.73 shows the situation that is encountered at node C. However, the findHumanMove, at the min

![](bbox=[0.05, 0.7, 0.95, 0.85])

Figure 10.70 A hypothetical game tree