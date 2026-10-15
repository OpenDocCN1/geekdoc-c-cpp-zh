The Development Fabric window enables you to view the trace logs of the various running Web and worker roles, as well as view the current settings for these running services.

# Storage Services

The Storage services provide the means of saving data for your cloud applications. Why not just let you use existing data storage mechanisms? The main problem with allowing you to just write as needed is that your code is running within multiple virtual machines. If you were allowed to use file I/O and write to the hard drive, Azure would have to ensure that this data was written consistently across all of the virtual machines running your application. In addition, it would have to duplicate this data in any new virtual machines that might start after the data was written. As you can imagine, these would be very difficult problems to solve.

Instead, Windows Azure provides four storage mechanisms for saving data:

+   - Blob storage
+   - Table storage
+   - Queues
+   - SQL Azure

These are actually provided by separate instances within the cloud, and not dependant on your applications. All of your data is stored multiple times throughout the cloud — for redundancy and reliability — as well as backed up and maintained.

# Blob Storage

The simplest form of storage available within Azure is blob storage. As the name implies, blob (Binary Large Object) storage simply gives you a set of space to store binary information. Blobs are created within containers, and can be quite large (they have a maximum individual size of 50GB). Each container may hold multiple blobs, but there is no real hierarchy such as you have on your disk drive.

Blobs are excellent storage when you have video or audio data, or when you want to create your own storage mechanism (maybe you want to keep a 50GB XML file in the cloud for some reason). You access these blobs using a REST interface, and with a URL like one of the following:

```
http://{your account}.blob.core.windows.net/{container}/{blob}
http://127.0.0.1:10000/devstoreaccount1/{container}/{blob}
```

The first URL scheme is used when accessing the live servers, while the second is used when accessing storage in the development environment.

WCF Data Services (see Chapter 12) makes working with these URLs (and blob storage) fairly transparent to the developer.

# Table Storage

The next form of storage available with Azure is table storage. While the name implies database access, it is actually much simpler than that. Table storage enables you to create one or more tables for your application. Each table consists of one or more entities; and each entity has one or more properties, each with a name, a value, and a type. All of that sounds like a normal database, but the difference is in the details. The primary differences between a storage table and a database table are as follows:

+   - A storage table is not stored within a relational database.
+   - You cannot use SQL to query a storage table, nor do you use ADO.NET to access it. Instead, you use WCF Data Services to access them.
+   - Each entity within a table might have different sets of properties. That is, the individual “rows” of data within a table do not have to match a specific schema.
+   - When you edit an entity, the entire entity is considered altered. That is, changing a single property of the entity means that the entire entity is considered changed.