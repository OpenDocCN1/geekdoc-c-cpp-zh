# Identifying the Functions

# Example 9.1 Designing a Counter (cont)

The first diagram, in Figure 9.28, presents an aggregation of the objects in the system. That aggregation includes both the environment and the counter being designed.

![](bbox=[0.15, 0.17, 0.9, 0.4])

Figure 9.28 A Model of the Environment and the Counter as an Aggregation of Objects

The model of the measurement system is expressed as a collection of:

+   - The user
+   - The factory
+   - The future remote computer
+   - The counter.

**aggregation, composition**

The factory is an aggregation of test lines and numbers of navigation radios that must be tested. Note that we are using the looser term aggregation rather than composition here.

# Functional Decomposition

The Design Specification provided a high-level block diagram of the system. For this problem, such a diagram provides a good starting place for the initial hierarchical decomposition of the system. Figure 9.29 elaborates on the counter component and gives one possible decomposition for that system.

The interface to the outside world is segregated into two functional blocks. The first is associated with the presentation of information to the user. The second is charged with bringing in information from the user and other tasks necessary to support the measurement. Both functional blocks are further decomposed into local operations versus remote operations.

presentation of information, bringing in information

Such a choice is made in the first case because the display is considered an output function and control an input function. In the second case, two different sets of functionality and different grammars for expressing the user's commands are anticipated. Front panel operations tend to be rather straight forward; remote operations can be a bit more involved. Certainly, these are not the only choices.