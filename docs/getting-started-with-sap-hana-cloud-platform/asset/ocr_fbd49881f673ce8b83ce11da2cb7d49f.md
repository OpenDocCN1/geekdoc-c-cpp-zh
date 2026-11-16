so tight that most enterprise applications can't even be launched if the database is unavailable. Recognizing this critical requirement, SAP designed SAP HCP from the ground up to include first-class support for persistence in relational databases. This support is provided in the form of a core service called the Persistence Service.

# 6.2.1 Conceptual Overview

In the Java world, the Persistence Service is an abstraction layer built into the Application Runtime Container that provides access to virtualized databases hosted in the cloud. As such, it plays more of a behind-the-scenes role, taking care of low-level technical details such as database backup and recovery, load balancing and scaling, connection management, and so forth.

> Note
> For SAP HANA XS applications, there's no real need for a separate persistence service, because SAP HANA XS applications naturally have a direct connection to the backend SAP HANA database.

The architectural diagram contained in Figure 6.2 illustrates how the Persistence Service fits into the Application Runtime Container. Here, you can see how database access is abstracted using the industry-standard JPA and JDBC APIs. From a development perspective, this is huge; it allows Java developers who are already comfortable working with these APIs to jump in and begin consuming the Persistence Service right away.

![](bbox=[0.13, 0.62, 0.75, 0.86])

Figure 6.2 Understanding the Positioning of the Persistence Service