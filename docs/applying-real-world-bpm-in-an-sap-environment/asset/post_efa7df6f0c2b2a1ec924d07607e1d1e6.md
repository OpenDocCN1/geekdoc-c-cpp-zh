
between steps (e.g., details read via a service call that is then passed to a UI) or as a convenient generic persistence layer.

## Recommendation: Name your primary data as such.

Use meaningful names, comments, or your own conventions to achieve this. Primary data, in particular status variables, must be understood by anybody who attempts to use, manipulate, or refactor the process. Overlooking or misinterpreting primary data results in difficult-to-catch application errors and misuse of the process.

## Recommendation: Minimize the amount of secondary data in your process.

If you reuse services or UIs, you have to work with the given set of interfaces that you have to populate or interpret, meaning your choice of data you have to provide or accept is limited. You should, however, be able to use reduced (thinned out) data structures within your process that only store the attributes you actually need. In SAP NetWeaver Composition Environment [7.20], you can use CE service adaptation to thin out vast interfaces to the data you really require. See the performance and data volume sections to fully appreciate the meaning of this recommendation. See the concept/notation of business entities as well.

If you determine the interfaces of services and UIs yourself, for example, because you design them as part of your project, you should do everything you can to adhere to this guideline. In particular:

## Recommendation: Design new interfaces with small signatures.

Let these interfaces expose less than 25 parameters and favor copy-by-reference to copy-by-value. Whereas the first part of the recommendation is self-explanatory (smaller interfaces = fewer dependencies, less complexity, and less data overhead), the second part merits an example because it is valid both for services and for UIs. Passing references (e.g., to business objects) typically works well if the receiving application can interpret the references and can access the referenced object's data effectively. Passing references typically means you transport only the ID/key of a business entity between different participants in the flow. For example, if you pass the reference to a service contract, the contract number, for example, to a UI, and the UI application can use this key to read the required details of the contract, such as the issue date, the contract value, and so on without a performance penalty. As a consequence, the UI's interface contains only the contract number instead of the 75 attributes that a fully fledged contract business object might have.

Copying data (as opposed to referencing it) has several other unwanted implications, such as:

munication, and fail-over mechanisms are in place to ensure efficient use of the full cluster resource.

The engine executes process instances in a transactional and fail-safe manner. This means the state of a process is stored in the database (DB) at save points whenever the process logic, technical constraints, or general monitoring requirements demand it. Because the engine executes an arbitrary number of different process models, all with different data context definitions, it cannot use dedicated (transparent) DB tables to store this data. Instead, at every save point, the data context of a process is serialized to XML and stored as one “blob.” When the data needs to be read back, it is fetched from the DB and parsed to re-instantiate the data objects in the memory. This engine-persistent storage is required to enable fail-over of process instances in case of a Java engine — or a hardware failure. If this occurs, the engine will simply reload its previous state and continue process execution from the previous save point.

Whenever a context switch occurs for a process instance, the entire instance must be serialized on the node where it is currently executed and later de-serialized on the node where execution is to continue. A context switch like this can occur when an incoming request is issued on a node in the cluster where the process instance is not currently running. Requests of this kind are service requests, a BPMN event (via correlation), or a human interaction leading to a status change of a task.

For auditing reasons, note that there are at least two save points for every activity in your process: one after creation when the input data is available and another one after completion, when the output data is available. Human tasks can have significantly more save points than automated activities, typically one after each status change (e.g., task created, task started, task claimed, task failed, task completed, etc.). Also note that all major changes to a process instance and its activities (including changed process data) are written to the business log, where they are the basis for providing information about the history and the current state of the process (in graphical or textual form).

In memory, data objects are represented using a standard compliant Service Data Objects (SDO) implementation.

The size and complexity of the data context of a process therefore directly impact engine performance in three ways:

- The data context of every process instance currently in execution must be kept in the main memory. Very large data contexts (>1MB) can significantly impact the number of process instances that can be simultaneously executed.
- When a save point is reached, the process instance must be serialized and written to the database. Serialization consumes application server CPU time, and the serialized data stream consumes DB server CPU time and DB space.
- When a process instance is reloaded from the database, its data is de-serialized, and the Java runtime objects are reconstructed.

Please consider that each attribute in the global data context is serialized and stored in the business log whenever it is changed. Each activity in the process has at least two save points, where the full input and output data, respectively, are serialized and stored.

## Sizing

Note that a dedicated sizing procedure document for SAP NetWeaver BPM starting with release 7.20 is available on SAP Service Marketplace.

## Structure

The artifacts of a composite application can be structured in many different ways according to the SAP component model. This is an explanation of how to structure a composite application.

During development of a composite application, one of the most important questions is how the application will be structured in projects, in particular, how many software components (SCs) and development components (DCs) will be used. Also, considering build-time procedures and the possibility of clustering content will help resolve structuring issues.

### Software Component Granularity

An SC is usually created if the parts of the composite applications should be executed on different servers because an SC is defining the deployment granularity or if the parts of a composite application can be deployed independently, for example, if some of the functionality is optional.

Every software component archive (SCA) defines a distribution archive. The argument for SC granularity is therefore deployment. We definitely do not recommend creating different SCs only to bundle the business-relevant parts together (or separate them). If the parts of a composite application should be executed on one server, and there is absolutely no intention of deploying them on different servers, the content should be put into the same SC.

If the application design is done in such a way that different parts can be distributed independently, we recommend putting the parts of the application in different SCs, because the smallest distribution granularity in software logistics is the software component. The SC is also the entity that is versioned, so the SC is the entity that is meant to structure the deployment.

There are other reasons to define SCs, such as project organization and semantic reasons.

### Development Component Granularity

The different domains provide separate DC types. It is therefore a good choice (and sometimes the only option) to put the content for different domains in separate DCs. Therefore, all process content is located in a process composer DC, all Web Dynpro content is part of a Web Dynpro DC, and so on.

A DC is the atom of reuse, that is, the smallest undividable functional piece. The composite application developer therefore has to plan for reuse and proper segregation of reusable pieces into a minimal number of DCs. For generic functions, individual DCs should be created to facilitate their reusability and to collect all required elements of the function in this DC.

As a result, parts that are meant for reuse should be put into separate DCs including sufficient definition time for planning the API and separate API implementation. You can add the API to a public part of your DC in these ways:

- Choose the DC structure according to its function and not according to the organizational structure of the responsible developers.
- Choose the DCs in such a way that the involved developers work in the same team and at the same location. Only if these conditions are met can you use the inactive state of objects, which is mandatory for distributed responsibilities.

These two guidelines seem contradictory, but you should use both guidelines together, so that together they define the minimal structure of DCs.

After a change, you must rebuild the entire DC. You should therefore choose the size carefully so that it does not contain too many objects. This is a very broad statement, so some more details are required.

### Build Time

This section provides more details regarding the general recommendations about how to structure content and what these recommendations look like in the light
