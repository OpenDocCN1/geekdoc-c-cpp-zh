# Building Service-Oriented Applications 727

![](bbox=[0.231, 0.137, 0.846, 0.335])

**Figure 1-4:** Separating the layers.

Because the services use a common format — usually XML over HTTP — you can relatively easily install parts of the application on their own machines to isolate them by functionality. Because the functionality of the deleted part is called via a service, you can scale the application horizontally.

+   **Reusability:** Every organization has a list of its participants — clients, users, voters, cooks, or mailing list subscribers, for example. Regardless of the type of participant, all the people on the list have first and last names and identifying characteristics.

It seems like nearly every application written today has a table of People. Savvy programmers use slick tricks to keep these tables in sync or to share information, for example, but only one way exists to share the People table — by using a data silo, as shown in Figure 1-5.

A data silo works this way:

+   1. A database on some server contains all participants' demographic information.

+   2. The data silo is surrounded by a service layer containing all allowed operations.

+   3. The service layer is consumed by all other applications in the system, as shown in Figure 1-5.

This set of steps shows you the concept of reuse. It isn't about bits of code (no matter what you might hear) — it's about *data*. Services help to provide access to the data silo.