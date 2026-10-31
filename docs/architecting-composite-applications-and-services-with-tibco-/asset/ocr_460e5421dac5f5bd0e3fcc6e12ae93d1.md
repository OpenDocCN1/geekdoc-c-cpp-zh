# Summary

When you want to use a component as part of a solution, you need to understand the behavior of that component so that you can determine whether it is suitable for use in the solution. What you need to know are the aspects of the component’s behavior that are observable from outside the component. You treat the component as a black box and focus on its observable behavior.

Understanding observable behavior requires characterizing a number of things, including

+   - Context: the component’s dependencies upon external components and vice versa
+   - Usage scenarios: characterizations of the business processes in which the component is expected to participate
+   - Triggered behaviors: structures of activities that explain the relationships among the component’s triggers, responses, inputs, observable state, and outputs
+   - Observable state (information retained from one trigger to the next)
+   - Coordination: the manner in which the component’s activity can be coordinated with that of external components
+   - Constraints: limitations, particularly on the sequencing of triggers
+   - Nonfunctional Behavior: performance, availability, and so on

Some composites cannot be safely considered as black boxes. These include components whose constituent parts are operated independently or are accessible by means other than the composite’s interfaces.