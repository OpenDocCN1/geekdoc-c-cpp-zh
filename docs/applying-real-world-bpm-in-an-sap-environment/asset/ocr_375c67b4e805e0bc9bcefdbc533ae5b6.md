# Quadrant 1: custom developed SAP Business Suite applications using BRFplus

Quadrant 1 characterizes standard use cases where BRFplus is used to solve business rules requirements for custom developed applications, which extend the business suite functionality. Custom developed applications can externalize business logic using BRFplus and improve the flexibility greatly. Because the execution environment and the application data reside on the ABAP stack, BRFplus is the natural technology fit in such cases, providing deep integration and best performance.

# Quadrant 2: custom developed SAP Business Suite applications using SAP NetWeaver BRM

Quadrant 2 characterizes use cases where custom developed applications in the suite (ABAP stack) use SAP NetWeaver BRM for managing business rules. In such cases applications may need Rete rules capabilities that are not available in BRFplus. Or applications may interact with non-SAP systems in a heterogeneous landscape, and the data needed for the business rule processing is mostly spread across this landscape. When applications in the ABAP stack use SAP NetWeaver BRM, it is possible to make the usage transparent by natively connecting to SAP NetWeaver BRM by using a BRFplus BRMS connector expression that is optimized for SAP NetWeaver BRM.

# Quadrant 3: composite applications using SAP NetWeaver BRM

Quadrant 3 characterizes use cases where composites developed with SAP NetWeaver Composition Environment (CE) use SAP NetWeaver BRM natively. SAP NetWeaver BRM is closely integrated with SAP NetWeaver Business Process Management, so modeled business processes use SAP NetWeaver BRM to solve decisioning problems.

# Quadrant 4: composite applications using BRFplus

Quadrant 4 characterizes use cases where composite applications developed using SAP NetWeaver CE and modeled business processes in SAP NetWeaver BPM use existing business rules in the core suite applications designed using BRFplus. In these use cases, composites leverage existing rules in BRFplus by calling them as Web services.

# Circle 1: mixed-usage scenarios with BRFplus and SAP NetWeaver BRM

In addition to BRFplus-only and SAP NetWeaver BRM-only usage scenarios in the four quadrants, there is an increasing need for mixed usage scenarios in which BRFplus and SAP NetWeaver BRM are used together in heterogeneous environments involving both SAP and non-SAP systems. Several use cases require business rules to be modeled in a single place and executed in both BRFplus and SAP NetWeaver BRM within the same scenario.