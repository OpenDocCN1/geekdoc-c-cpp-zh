
| Capability/Tool | CAF | Service Composer | Java EE |
|---|---|---|---|
| Custom coding in Java | Controlled | Limited to mapping functions | Unlimited |
| Write operations | Logic is implemented, and therefore the execution of many service calls in a chain can be implemented such that errors can be handled | If there are many write operations in a model, then it is difficult to do good enough error handling, because there is no way to trigger user interaction. Only if the error is exposed and some implementation outside of the model reacts to it | Logic is implemented, and therefore error handling is possible to every degree |

Table 14.4 Data Transformation Technology Comparison (Cont.)

SAP CAF and Service Composer are both model-driven architecture (MDA) tools for service development, but they provide different design-time and runtime capabilities, resulting in corresponding benefits. Depending on the particular use case, it might be better to use one or the other technology.

## Service consumption

In SAP CAF, WSDL artifacts can be imported to consume Web services and SAP JCo models to consume RFCs and business application programming interfaces (BAPIs). From the consumed services models, it then generates JAX-WS and RFC static proxies, resulting in improved consumption performance. Because communication-technology-specific proxies are used, it is not possible to switch the type (WS/RFC) of the consumed service once the service interface has been imported. Service Composer uses WSDL artifacts to describe imported services for both WS and RFC types. Instead of generating static proxies (as in SAP CAF), WSDL description is interpreted at runtime by SCA runtime and corresponding SDO data access services (for WS or RFC), which leads to lower performance compared to static proxies, but makes it possible to switch between WS and RFC types of consumed services. Easy service mocking can also be applied. Service Composer provides service interface reimport with delta detection capability, thus preserving the existing service flow and data transformation mapping models.

## Type reuse and collision handling

Both SAP CAF and Service Composer provide type reuse functionality, but they offer different conflict resolution approaches. In SAP CAF, conflicting type definitions cannot be imported, and the first type definition wins. In Service Composer, conflicting type definitions can be imported. Users are prompted to pick one of the conflicting type versions, and — if the newly imported version is selected — all of the occurrences of the conflicting version in the existing (previously imported) WSDL and XSD documents are replaced with the new one.

## Service simplification

Service Composer offers a wizard to create new (simplified) service from the existing service interface. The new service interface definition starts by taking the service interface of a service to be consumed and simplified and then selectively removing parts of the input and output data types. This results in a completely implemented simplified service delegate to the original service. It contains a new (simplified) service interface, import of the original service, and corresponding data transformation mappings. In SAP CAF, all steps have to be performed manually: modeling the new (simplified) service interface, importing the original service, defining mappings.

## Service execution flow

Service Composer offers a graphical modeling tool to define service execution flows using a minimal subset of BPMN, where only unconditional transitions are supported. In SAP CAF, execution flows cannot be modeled but are coded in Java using dedicated custom code sections, thus allowing more sophisticated flows — conditions, error handling, and so on.

## Data transformation mappings

SAP CAF provides a graphical tool for modeling data transformation mappings, which leads to the generation of Java code that implements the actual transformation. This allows for higher runtime performance. Only one-to-one and constant mappings are supported in SAP CAF. Service Composer offers easy graphical modeling for much more sophisticated mapping definitions. In addition to the one-to-one, one-to-many, many-to-many, and constant mapping styles there are capabilities such as mapping functions, built-in function libraries, custom functions, function nesting, iterations, collection addressing, type conversion, type casting (SAP NetWeaver CE 7.30), and evaluation at design time. Service Composer mappings are dynamically interpreted at runtime, offering poorer performance than static mappings in SAP CAF.

### Service provisioning

SAP CAF services are generated in both Web service and EJB form using JAX-WS and JAXB. In addition to JAX-WS and JAXB service implementations, Service Composer generates SDO-based EJBs that are exposed as Web services through the SCA runtime.

### Data persistency

Service Composer does not offer data persistency capabilities, because it is focused on service adaptation (such as simplification) and composition only. In SAP CAF, graphical and form-based modeling can be used to define models of the persisted data types, which are then used to generate JPA entities. There are also services on top of the JPA entities, such as data type and data instance level permissions, language-dependent attributes, bulk operations (only in SAP NetWeaver 7.3), SAP NetWeaver BW integration (SAP NetWeaver BW pulls data from SAP CAF BO nodes), and business data transport. SAP CAF also provides modeling of findBy operations, which are less powerful than Java Persistence Query Language (JPQL) but much easier to define. There is also the Service-Browser web tool for runtime testing of services developed with SAP CAF.

### Custom coding

The custom coding in Service Composer is limited to the area of custom data mapping functions, where functions can be implemented with EJBs, whereas SAP CAF provides much more controlled opportunities for custom code. In SAP CAF, you can create custom coding for declared application service operations and can override any operation in BO node and external Services. You can also add any code that is not covered by any of the models in the EJBMODULE folder.

### Write operations

The Service Composer is a model-driven tool, so all functionality has to be modeled. Unfortunately, this would even be true for the error handling, so there are definitely some limitations to the error handling in comparison to SAP NetWeaver BPM (where human activities can do error handling and error states to start compensating for successful service calls (see Error Resolution: Compensation in Section 14.1.5). These limitations make it difficult to handle many service calls in a chain in the Service Composer, so it is usually better to handle write operations in the frameworks that allow custom coding and handling of all cases (SAP CAF, Java EE).

SAP CAF provides better overall performance at runtime, whereas Service Composer provides improved usability. Below, you can find some example scenario measurements comparing Service Composer and SAP CAF in terms of runtime performance.

To illustrate this fact, Table 14.5 and Table 14.6 list performance indicators. The measurement was made on one PC, so the indicators are comparable to the each other, although there is no guarantee that every PC with the same performance will achieve the same performance.

| Technology | Test Duration | Number of Transactions | Average Response Time | Java AS CPU | Memory per Transaction |
|---|---|---|---|---|---|
| SC | ~2 hours | 126,296 | 113 ms | 60% | 14.2 MB |
| CAF | ~2 hours | 127,062 | 45 ms | 39% | 5.9 MB |

*Technical scenario definition: average payload size of composed service: 12 KB, local Java services, protocol HTTP*

Table 14.5 Performance Comparison of Service Composer and SAP CAF for Local Services

| Technology | Test Duration | Number of Transactions | Average Response Time | Java AS CPU | Memory per Transaction |
|---|---|---|---|---|---|
| SC | ~2 hours | 125,845 | 117 ms | 57% | 12.5 MB |
| CAF | ~2 hours | 126,503 | 70 ms | 35% | 5.2 MB |

*Technical scenario definition: average payload size of composed service: 12 KB, remote Java services, protocol HTTP*

Table 14.6 Performance Comparison of Service Composer and SAP CAF for Remote Services

Types are used in service consumption in SAP NetWeaver CE. All frameworks are able to consume Web services and XSD data type definitions, but there are some limitations if SAP enterprise services are consumed.
