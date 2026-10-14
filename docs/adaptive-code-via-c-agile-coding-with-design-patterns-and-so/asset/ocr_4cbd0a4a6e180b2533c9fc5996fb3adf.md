Mapping library. Instead, a separate mapping assembly should be created that is implementation specific and instructs the ORM how to map to the domain model. This allows the domain model’s core classes to be reused without depending on the ORM, and the ORM could be replaced without affecting the domain model or its clients. Figure 2-24 shows a possible implementation of a logic layer that uses a domain model.

![](bbox=[0.22, 0.13, 0.78, 0.68])

FIGURE 2-24 How the assemblies of a domain model collaborate to form a logic layer.

The addition of a logic layer is necessary when there is complex logic in the application, such as business rules that aim to reflect the real-world workflows of people’s jobs. Even if the logic is not particularly complex but changes often, this is a good argument for introducing a separate layer for encapsulating this behavior. It simplifies the user interface and data access layers, allowing them to concentrate fully on their only purpose.

# Cross-cutting concerns

Sometimes a component’s responsibilities are not easily limited to a single layer. Functions such as auditing, security, and caching can permeate through the entire application, because they are applicable at every layer. Tracing the code’s actions at each method call and return, for example, is a useful debugging tool when the application has been deployed and if the Visual Studio debugger cannot be attached to step through the code. You can manually produce an output of the values of parameters as they are passed around, and the return values of various methods, as shown in Listing 2-23.

# LISTING 2-23 Manually applying cross-cutting concerns quickly swamps the real intent of the code.

Click here to view code image