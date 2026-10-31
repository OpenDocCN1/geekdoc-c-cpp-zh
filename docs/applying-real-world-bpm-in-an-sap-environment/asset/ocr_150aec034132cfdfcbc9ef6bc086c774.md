# Server Architecture

Though it seems obvious at first sight, SAP NetWeaver CE cannot simply be divided into a runtime stack running on a server and a design time running in Eclipse. The Eclipse parts are all related to design-time purposes; however, not all components on the server are relevant just for runtime. Complete design time solutions run on the server, mainly with SAP NetWeaver Visual Composer.

The applications still run on the Java EE 5 stack and utilize the standards, which means the runtimes on top of the Java EE 5 standard use the concepts of the Java server. The most important frameworks running on top of the Java EE runtime are:

+   - The Web Dynpro runtime is integrated with the web container, and every Web Dynpro application runs in the Web Dynpro servlet.
+   - The BPM runtime runs on the Java EE infrastructure. Especially for execution of a process, the cluster capabilities of the server are used to scale execution of many process instances.

# Design-Time Architecture in SAP NetWeaver Developer Studio

Composite applications are mainly developed in the Eclipse environment. Guided procedure and SAP NetWeaver Visual Composer models are developed on the server. The specific SAP NetWeaver Composition Environment frameworks have tools that are best suited for their use cases to reduce the development time of an application.

As explained before, there are several design times on the server, but the goal is to bring these toolsets to Eclipse. Lately, there have been some improvements in SAP NetWeaver Visual Composer in Eclipse. SAP NetWeaver Visual Composer runs locally in Eclipse, and it is no longer necessary to connect to a server to model a UI or portal content.

The toolset for the domain-specific models are bundled within the composite designer. This tool provides a consistent overview of a composite application, showing the dependencies and checking if the contracts between the various objects in the various domains are violated.

# SAP NetWeaver CE Programming Model

SAP NetWeaver CE provides a programming model like all platforms do. There are specific frameworks for the domains (user interface, process, business logic, etc.),