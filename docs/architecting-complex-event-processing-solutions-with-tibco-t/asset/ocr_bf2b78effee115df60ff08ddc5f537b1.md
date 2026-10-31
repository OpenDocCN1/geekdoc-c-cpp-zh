# Database Update and Delete

While an inference agent can make changes to a database concept, those changes are not automatically saved in the database. An explicit call to the RDBMS catalog function Database.update() is required (Figure 12-13).

Conversely, changes in the database itself are not automatically reflected in the database concept, nor is there any automatic mechanism for knowing that the database has changed (see section on using TIBCO ActiveMatrix® Adapter for Database). In order to get updated database information into database concepts, another query is required.

A database deletion can be performed with a call to the RDBMS function Database.delete(). Deletions in the database itself are not automatically reflected in the database concept. Recognizing a database deletion requires removing the database concept from memory and then repeating the query.

# Database Interaction Using TIBCO ActiveMatrix® Adapter for Database

The TIBCO ActiveMatrix® Adapter for Database can also be used for database interactions (Figure 12-14). The adapter communicates with the target database using the JDBC or ODBC protocols.

There are three interaction patterns possible with the adapter:

+   1. Inference Agent Publication
+   2. Inference Agent Request-Reply
+   3. Inference Agent Subscription

![](bbox=[0.28, 0.78, 0.82, 0.94])

Figure 12-13: Database Update