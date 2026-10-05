# Chapter 18 ■ Distributed Algorithms 463

In what order do the philosophers eat? In other words, who eats first, second, third, and so on? (Hint: It may be helpful to draw a series of pictures to show what happens.)

+   4. In the two generals problem, what happens if some of the initial messages get through, and general B sends some acknowledgments, but he is unlucky, and none of the acknowledgments makes it back to general A?

+   5. In the two generals problem, let PAB the probability that a messenger is caught going from general A to general B. PBA be the probability that a messenger is caught going from general B to general A. The original algorithm assumes PAB = PBA, but suppose that it's not true. How can the generals figure out the two probabilities?

+   6. Consider the three-person general and lieutenant problem shown in Figure 18-2. You could try to solve the problem by making a rule that any lieutenant who has conflicting orders should follow the order given by the general. Why won't that work?

+   7. Consider the three-person general and lieutenant problem shown in Figure 18-2. You could try to solve the problem by making a rule that any lieutenant who has conflicting orders should retreat. Why won't that work?

+   8. In the four-person general and lieutenant problem shown in Figure 18-3, can the loyal lieutenants figure out who the traitor is? If they cannot, how many lieutenants would be needed to figure it out?

+   9. In the four-person general and lieutenant problem shown in Figure 18-3, find a scenario that allows the lieutenants to identify the traitor. In this scenario, what action should the lieutenants take? (Of course, if the traitor is smart, he will never let this happen.)

+   10. What modification would you need to make to the dining philosophers problem to let the leader algorithm help with it? How would it help?

+   11. With a bully-style algorithm help with the dining philosophers problem?

+   12. Define a ravenous philosophers problem. It is similar to the dining philosophers problem, this time the philosophers are always hungry. After a philosopher finishes eating, he puts down his forks. If one picks them up right away, he grabs them and eats again. What problems would this cause? What sort of algorithm might fix the problem?

+   13. In the clock synchronization algorithm, suppose the time needed to send a message from A to B differs from the time needed to send a message