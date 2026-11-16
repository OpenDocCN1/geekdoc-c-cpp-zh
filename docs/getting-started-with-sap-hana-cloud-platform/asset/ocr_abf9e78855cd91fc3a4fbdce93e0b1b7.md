+   > Compatibility with legacy or third-party applications/frameworks
+   
+   Because SAP HCP is fully Java EE compliant, there may be cases in which you want to deploy preexisting applications or frameworks based on JDBC. Here, there’s no need to reinvent the wheel with JPA.

+   > Access to database-specific features
+   
+   In cases in which performance is critical, it might make sense to use JDBC as a mechanism for implementing database pushdown techniques. For example, you might utilize the SQLScript language of the SAP HANA database to create stored procedures that bundle together related database operations in close proximity to the data. You can then access these stored procedures using the JDBC API at runtime to minimize the amount of data exchanged over the network and take advantage of the raw calculation power of the SAP HANA database engines.

Of course, there’s no reason why you can’t mix and match techniques as needed. For example, you can use the JPA for defining your entity model and handling basic CRUD operations and then pick and choose the places in which you might want to utilize the JDBC API to improve performance.

# 6.2.5 Database Management Concepts

As you’ve seen throughout the course of this section, the Persistence Service takes care of most of the low-level database management tasks required for on-premise database instances. However, although you needn’t worry about performing backups or (re)allocating disk space, there are certain administrative tasks that you need to perform from time to time. Therefore, in this section you’ll learn how to perform some common administrative tasks for database schemas hosted in the cloud.

# Accessing Database Schemas Remotely

For security reasons, database instances in the cloud are protected by a network firewall. This firewall is designed to prevent unauthorized access to sensitive data from the outside world. Although all this is of no concern to cloud-based applications running inside the firewall, it does present a bit of a challenge in situations in which you have legitimate need to access database instances remotely. Fortunately, SAP HCP makes it possible to establish secure database tunnels so that you