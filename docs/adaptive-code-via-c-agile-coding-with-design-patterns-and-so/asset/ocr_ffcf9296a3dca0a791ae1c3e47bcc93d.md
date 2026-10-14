![](bbox=[0.22, 0.01, 0.8, 0.55])

FIGURE 2-23 The third layer contains processing or business logic for the application.

Again, like the data access layer, the logic layer provides interface and implementation assemblies to clients, to avoid a leaky abstraction.

Note
Although the three-layer architecture is very common for web applications, it is typically deployed in only two tiers. One node handles the database, and another node handles almost everything else: the user interface, the logic, and even part of the data access.

# Business logic

The business logic layer’s responsibilities are to:

+   - Handle commands from the user interface layer.
+   - Model the business domain to capture business processes, rules, and workflow.

The logic layer might be a command processor that receives commands from the user via the user interface layer and, by collaborating with the data access layer, solves a specific problem or executes a particular task. It could also be a fully developed domain model that aims to map a business’s processes into software. For the latter, it is common for the data access layer to include an Object/Relational Mapping component so that the logic layer can be implemented directly into classes, possibly by using domain-driven design (DDD). In a domain model, there should be no dependencies, either further down the stack or via some implementation-specific technology. For example, the domain model’s assemblies should have no dependencies on an Object/Relational