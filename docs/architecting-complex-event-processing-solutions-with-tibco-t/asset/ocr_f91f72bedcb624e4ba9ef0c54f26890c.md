# Database Interaction Using Database Concepts

The TIBCO BusinessEvents Data Modeling extension provides the ability to automatically define concepts that correspond to database tables. Rows in the database table correspond to instances of the database concept. The extension also provides a collection of related RDBMS catalog functions.

# Database Concepts and Memory Management

Database concepts operate differently than ordinary concepts. The default memory management mode for database concepts is Memory Only—concepts reside only in the inference agent. Furthermore, a database concept that is created or updated as a result of an RDBMS query is not automatically placed in working memory. It must be explicitly asserted using the Database.assertDBInstance() catalog function.

By exception, database concepts can be configured as Cache Only or Cache + Memory. However, backing store is never an option for a database concept. Even if the cluster is configured for backing store, these settings will be ignored for database concepts.

# Database Query

Database queries run against the database and return database concepts as results (Figure 12-12). These concepts are then available for subsequent processing in the agent. There are a number of RDBMS functions available for queries. If large result sets are expected, there are catalog functions for working with database cursors and walking through result sets.

![](bbox=[0.27, 0.88, 0.78, 0.95])

Figure 12-12: Database Query