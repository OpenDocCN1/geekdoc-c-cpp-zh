# Modularization

When you modularize a design, you are defining a decomposition of your design into units that are more readily maintained, managed, and tuned. The modularization of your design can be as important as the functionality itself in determining the success of your solution.

# Modularization Units

There are three levels of modularization in a TIBCO BusinessEvents® solution (Figure 17-1). At the highest level is the cluster. Each cluster contains one or more processing units, and each processing unit contains one or more agents.

Each solution requires at least one cluster, and some may involve more than one. For example, a solution using both inference agents and process agents must have at least two clusters, since inference agents and process agents cannot be deployed in the same cluster. For performance reasons, a solution in which dashboard agents are being used for visualization should have a separate cluster for the agents involved in managing the visualization (including inference, cache, and dashboard agents). These should be in a cluster separate from the cluster executing the functional part of the solution.

Modularization is largely about the packaging of functionality. It reflects your decisions about where different blocks of functionality

![](bbox=[0.38, 0.82, 0.62, 0.95])

Figure 17-1: TIBCO BusinessEvents® Modularization Units