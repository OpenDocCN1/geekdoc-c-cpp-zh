![](bbox=[0.35, 0.12, 0.7, 0.48])

# Figure 5-21: Black Box Perspective

Key indicators that the composite is not a black box include

+   - Different organizations are responsible for operating (starting and stopping) different parts of the composite.
+   - Decisions to start and stop the composite are separate from decisions to start and stop its component parts.
+   - A component part can be accessed directly via its own interfaces, interfaces that are not declared to be part of the composite’s interfaces. This is particularly important when the constituent component is stateful.

An example of a component that should not be treated as a black box is a service (interface) wrapping the functionality of a stateful back-end system that other solution components access directly. In this situation, state changes made via the service interface may be visible through the back-end system’s interface, and vice versa. Characterizing the observable behavior of the service will not explain the state changes that are visible through the service interface but did not originate as the result of a service interaction.

Any of these conditions make it important for the user of the composite to be aware of the composite’s architectural structure—aware of those components that are independently accessible or managed. Under such circumstances, you can’t treat the composite, including its component parts, as a single entity—a black box. Instead, each of the components becomes a black box in its own right. The context and usage scenarios for the “composite” then indicate how these supporting components collaborate with the composite.