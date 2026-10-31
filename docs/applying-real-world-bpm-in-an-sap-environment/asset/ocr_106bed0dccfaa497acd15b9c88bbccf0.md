contract implementation layer can be implemented in different ways. First, the composite application design has to be clear if a complete decoupling has to be achieved. In that case SAP provides the following solutions:

+   - **SAP NetWeaver BPM**  
+     The service contract implementation layer implements an interface by using BPM modeling capabilities to allow execution of service calls asynchronously (see Asynchronous Write in Section 14.1.5). If an error happens during invocation of the Enterprise Service, a full error handling including user steps can be implemented.
+   
+   - **SAP NetWeaver Process Integration (PI)**  
+     The implementation of the service contract implementation layer is not done via SAP NetWeaver CE; it is done via the process integration hub of SAP. The benefit is the same as the case of SAP NetWeaver CE; the only difference is that the capabilities of SAP NetWeaver Process Integration can be used (e.g., routing, ccBPM, etc.).
+   
+   - **Java Message Service (JMS)**  
+     The service contract implementation layer contains a very small implementation of the service contract, and only an event via JMS is raised that is processed on the Java server itself, so the message queue is used to decouple the functionality. The benefit is that only Java EE technologies are used.

The above options decouple the execution of the enterprise service call from the basic composite application. If the asynchronous behavior is not a requirement, then the other technologies of SAP NetWeaver CE (SAP CAF, service composition, EJB) that transform the delivered data of the enterprise services to the composite can be used. This solution has the drawback that a complete decoupling of the UI parts of the composite application is not achieved; it goes in the direction of tight coupling with all of the disadvantages.

# **Structure of the Service Contract Layer in a Composite Application**

The service contract and the service contract implementation layer have to be structured in a way that real decoupling is achieved. Figure 14.9 shows the structure of a decoupled composite application.