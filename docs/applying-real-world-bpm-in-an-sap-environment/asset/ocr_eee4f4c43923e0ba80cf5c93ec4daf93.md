+   - Developing replicated solutions adds additional effort to a project. You need mapping of a local data structure to the information providers’ structure, conflict management, replication scheduling, and so on.
+   - Replication data (mapping, scheduling) must be maintained. Conflict resolution might even cause manual resolutions. This all leads to slightly increased TCO.

# Reference Architectures

How can the framework above be used in a specific project situation to help find an appropriate architecture?

The described framework delivers powerful but numerous alternatives, and it is not trivial to find an appropriate architecture for a given input. The input of a planned project can be separated in several groups:

+   - Functional requirements
+   - Nonfunctional requirements, also called quality attribute requirements (security, scalability, etc.) following Software Engineering Institute methodology
+   - Design constraints, also called external forces and boundary conditions, which are given by laws, corporate rules, or technical limitations

Besides the approach to use this input, explore the pattern catalog, and compose an architecture blueprint based on the architecture variants and options, we want to analyze typical project situations and create an architecture blueprint for these typical situations upfront. We call such a preassessed architecture blueprint the reference architecture. This would be a very mature starting point for further enhancements.

A weak but self-explanatory analogy can be found in car purchasing: You can either select your favorite model, start a car configurator, and define your major requirements such as engine, color, interior color, multimedia equipment, security features, and much more, or the manufacturer can offer you preselected compositions (such as the models business, family, or sports), which all are optimized combinations of basic features for typical usage situations.

To outline the idea, we introduce a more detailed assessment of the example referenced in Section 16.5.2.