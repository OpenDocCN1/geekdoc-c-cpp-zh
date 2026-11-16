# Polymorphic Solution

+   - What is the effect on each solution of a request to handle a new type of vehicle to stop?

+   - In both solutions, we would provide the new vehicle with all of the operations provided by the other vehicles.

+   - However, in the traditional solution, we must also modify all operations on vehicles since they all contain logic similar to the previous solution.

+   - In every situation, a new else or case must be added.

+   - In a large system, this kind of activity is extremely error-prone. Chances are that we will fail to make one or more of the necessary changes.

+   - In the object-oriented system, the changes required are localized. We simply implement the necessary operations on vehicles without changing anything else.