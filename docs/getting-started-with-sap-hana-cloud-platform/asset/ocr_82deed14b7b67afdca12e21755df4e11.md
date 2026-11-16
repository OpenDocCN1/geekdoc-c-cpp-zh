limited to, home page tiles, navigation entries, UI generation metadata, or other embeddable UI fragments. SAP's midterm goal is that all of the imports are handled by the low-level infrastructure integration between SAP HCP and the corresponding extended SAP Cloud solution.

A typical extension application will have a combination of one or more of the described UI artifacts. If there are none, then you should seriously consider using SAP HANA Cloud Integration (SAP HCI), instead of implementing the data transformation logic yourself.

# 11.2.2 Extension Application Backend Layer

Similar to the frontend layer, there are a number of artifacts that belong to the backend layer and contribute to the overall solution (Figure 11.5).

![](bbox=[0.15, 0.39, 0.85, 0.68])

Figure 11.5 Extension Backend Artifacts and Where They Are Handled during Installation

The main part of the business logic is typically implemented in Java or accessed via remote API services in the extended SAP Cloud solution. Depending on the complexity of the application, you're free to choose any of the Java runtimes available. We strongly recommend that you not use Java 6, but select from Java 7 or Java 8. Java 6 is still supported on SAP HCP, but it's mostly there to cover backwards compatibility scenarios, because Java 6 itself is long out of mainstream maintenance in the developer community. While implementing your application,