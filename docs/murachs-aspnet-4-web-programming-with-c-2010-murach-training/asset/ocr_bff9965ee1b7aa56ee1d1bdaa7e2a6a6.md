# The starting code for a WCF service library

![](bbox=[0.155, 0.108, 0.826, 0.533])

# Description

+   - By default, a new WCF service library includes two files named IService1.cs and Service1.cs. The IService1.cs file contains an interface named IService1, along with a class named CompositeType that defines a composite data type. The Service1.cs file contains a class named Service1 that implements the IService1 interface.
+   - To define the operations of a service, you code an interface that has the ServiceContract attribute. Then, you can code one or more methods that have the OperationContract attribute.
+   - To define the data that’s used by a service, you code a class that has the DataContract attribute. Then, you code one or more properties that have the DataMember attribute.
+   - To implement the operations of a service, you code a class that implements the interface for the service.
+   - To add a WCF service to the library, select the Project➜Add New Item command. Then, select the WCF Service item from the resulting dialog box, enter a name for the service, and click Add.

Figure 23-4　How to develop the code for a WCF service library