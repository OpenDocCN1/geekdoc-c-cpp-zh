conversion, type casting (SAP NetWeaver CE 7.30), and evaluation at design time. Service Composer mappings are dynamically interpreted at runtime, offering poorer performance than static mappings in SAP CAF.

+   - **Service provisioning**
+   
+     SAP CAF services are generated in both Web service and EJB form using JAX-WS and JAXB. In addition to JAX-WS and JAXB service implementations, Service Composer generates SDO-based EJBs that are exposed as Web services through the SCA runtime.

+   - **Data persistency**
+   
+     Service Composer does not offer data persistency capabilities, because it is focused on service adaptation (such as simplification) and composition only. In SAP CAF, graphical and form-based modeling can be used to define models of the persisted data types, which are then used to generate JPA entities. There are also services on top of the JPA entities, such as data type and data instance level permissions, language-dependent attributes, bulk operations (only in SAP NetWeaver 7.3), SAP NetWeaver BW integration (SAP NetWeaver BW pulls data from SAP CAF BO nodes), and business data transport. SAP CAF also provides modeling of findBy operations, which are less powerful than Java Persistence Query Language (JPQL) but much easier to define. There is also the Service-Browser web tool for runtime testing of services developed with SAP CAF.

+   - **Custom coding**
+   
+     The custom coding in Service Composer is limited to the area of custom data mapping functions, where functions can be implemented with EJBs, whereas SAP CAF provides much more controlled opportunities for custom code. In SAP CAF, you can create custom coding for declared application service operations and can override any operation in BO node and external Services. You can also add any code that is not covered by any of the models in the EJBMODULE folder.

+   - **Write operations**
+   
+     The Service Composer is a model-driven tool, so all functionality has to be modeled. Unfortunately, this would even be true for the error handling, so there are definitely some limitations to the error handling in comparison to SAP NetWeaver BPM (where human activities can do error handling and error states to start compensating for successful service calls (see Error Resolution: Compensation in Section 14.1.5). These limitations make it difficult to handle many service calls in a chain in the Service Composer, so it is usually better