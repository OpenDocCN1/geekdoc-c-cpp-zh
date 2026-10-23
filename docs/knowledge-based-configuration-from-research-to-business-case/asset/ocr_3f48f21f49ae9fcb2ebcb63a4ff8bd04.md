**Table 8.1 Example of determining relevant questions on the basis of collaborative filtering (Konstan et al., 1997).**

| User | CPU | MB | OS | Screen | HD | Internet | Applications |
|------|-----|----|----|--------|----|----------|--------------|
| 1 | 1 | 4 | 2 | 5 | 3 | 6 | 7 |
| 2 | 3 | 1 | 2 | 4 | 5 | 7 | 6 |
| 3 | 1 | 3 | 2 | 5 | 4 | 7 | 6 |
| 4 | 1 | 3 | 2 | 4 | 5 | 6 | 7 |
| 5 | 2 | 1 | 3 | 5 | 4 | 6 | 7 |
| Current | 1 | ? | 2 | ? | ? | ? | ? |

**Table 8.2 Example of determining relevant constraints on the basis of collaborative filtering (Konstan et al., 1997).**

| User | c₁ | c₂ | c₃ | c₄ | c₅ | c₆ |
|------|----|----|----|----|----|----|
| 1 | 4 | 2 | 3 | 5 | 1 | 6 |
| 2 | 3 | 2 | 5 | 6 | 1 | 4 |
| 3 | 1 | 3 | 2 | 4 | 6 | 5 |
| 4 | 3 | 2 | 4 | 5 | 1 | 6 |
| Current | ? | 2 | ? | ? | 1 | ? |

and c₂. The constraint that should be recommended next to the current user is c₁ since this one has been inspected next by the majority of the nearest neighbors of the current user (user 2 and user 4).

The ICONE¹² knowledge acquisition prototype is an example of a graphical knowledge acquisition user interface that includes recommendation technologies for proactively supporting knowledge engineers and domain experts in their development and maintenance activities. The ICONE user interface is depicted in Figure 8.1. On the left-hand side, the user can exploit typical functionalities such as product data (component) management, definition and maintenance of constraints, and the definition of the configuration process (dialog management). In addition to these basic functionalities, the ICONE environment includes intelligent recommendation functionalities that proactively support the user in inspecting the knowledge base (e.g., the functionality take a look at ... on the right-hand side of Figure 8.1). From the definition of products (components) and constraints, the ICONE knowledge acquisition user interface can directly generate the corresponding configurator applications for different platforms (iOS, Android, and HTML). Note that the exploitation of recommender algorithms and machine learning approaches in knowledge acquisition and maintenance scenarios is a young and evolving discipline;