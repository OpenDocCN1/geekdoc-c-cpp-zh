# Activities have two types of behavior

+   - **Runtime** - Specifies the actions upon execution.
+   - **Design time** - Controls the appearance of the activity and its interaction while being displayed within the designer.

# 25.2.2.4 Services

+   - The workflow runtime engine uses many services when a workflow instance runs. WWF provides default implementations of the runtime services that meet the needs of many types of applications, such as a persistence service, which stores the execution details of a workflow instance in a SQL database. These service components are pluggable, which allows applications to provide these services in ways that are unique to their execution environment. Other types of services used by the runtime engine include scheduling services, transaction services, and tracking services.
+   - Custom services can be created to extend the WWF platform by deriving from the base service classes. An example of this would be a persistence service that uses an XML file instead of a database for storage.

# 25.2.2.5 Compensation Overview

Compensation is the act of undoing any actions that were performed by a successfully completed compensable activity because of an exception that occurred elsewhere in a workflow.

# 25.2.2.6 Local Communication and Correlation

+   - **Host processes** can communicate with workflows by exchanging data through custom local communication services. These local communication services implement user-defined interfaces that define methods and events that will be passed between the workflow and the host process.
+   - Host processes can also interact with a specific activity in a specific workflow instance by using a unique ID that is passed between the host process and the workflow as an event argument. This is known as **correlation**.

# 25.2.2.7 Persistency

+   - WWF simplifies the process of creating stateful, long-running, persistent workflow applications. The workflow runtime engine manages workflow execution and enables workflows to remain active for long periods of time and survive application restarts. This durability is a key principle of WWF. It means that workflows can be unloaded