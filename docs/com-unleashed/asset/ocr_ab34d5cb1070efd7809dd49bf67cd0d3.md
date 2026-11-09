# Business Processes

This is the heart, or *hot zone*, of DNA. Herein live the core server-side products that enable developers to focus on the solution and not the implementation details. Most of the plumbing required for managing transactions, for example, is provided by MTS. If queuing services are required, MSMQ exports a simple interface to make this happen with minimal development and configuration effort. Finally, to connect the application to the Internet, an HTTP server, such as IIS, must exist. As you will see in a later section, IIS does a lot more than interpret HTTP.

The application must also be solving a problem, so the logic and rules to accomplish this are present in this tier. It is preferable that the rules be encapsulated in processing using COM+, but this is not a requirement. COM+ components allow for reusability and interoperability across platforms, just as long as the business rules can be activated and information passed back and forth between tiers, any programming technology can be used.

> **Tip**
> 
> Server-side products like MTS and MSMQ can certainly be used within a local, standalone environment. The DNA services do have a clear design goal of scalability, particularly Web traffic, but this does not imply they can be used only within a distributed environment.
> 
> It is also important to note that MSMQ doesn't always belong in the middle tier. MSMQ can be used as a form of storage, in which case it would belong in the lowest tier: Integrated Storage. The hypothetical example presented in the next section illustrates this idea.

# Integrated Storage

Not all storage must be tied to a database. Many forms of physical storage are acceptable and sometimes required. With DNA and its strong ties to the Internet, email or multimedia binary streams (like audio or video) are strong contenders for primary data sources or sinks. A file system can also be used as storage when relational data is not required. Log files, for example, are typically text files stored on the file system that are incrementally built as an application runs.

When data must be associated with other data, a relational database like SQL Server 7.0 can be used through Microsoft's Universal Data Access mechanisms. OLE DB and its superset, Active Data Objects, are perfect for DNA because of their component nature. Other methods of storage like local collections can exist, too.