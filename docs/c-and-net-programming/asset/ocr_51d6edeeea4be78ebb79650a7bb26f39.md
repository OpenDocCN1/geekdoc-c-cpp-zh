# 10. Workflow-enabled apps using Windows Workflow Foundation (WWF) - WWF is a programming model that provides way to model process, activities and workflows.

All types of .NET applications use one or more .NET compliant languages for their design and development. The .NET Framework includes various technologies, such as ASP.NET, VB.NET, VC++.NET and ADO.NET. The ASP.NET is used to build Web applications and services, VB.NET and VC++.NET to create Windows applications, and ADO.NET for flexible access to databases.

# Q.9 Define Marshaling.

Ans. : A .NET code is referred to as “managed” because it is controlled (managed) by the CLR. Other code that is not controlled by the CLR is called unmanaged.

+   - In context with C# programming, marshaling is the process of creating a bridge between managed code and unmanaged code; it is the local one that carries messages from the managed to the unmanaged environment and reverse. It is one of the core services offered by the CLR (Common Language Runtime). Because much of the types in unmanaged environment do not have counterparts in managed environment, one needs to create conversion routines that convert the managed types into unmanaged and vice versa; and that is the marshaling process.
+   - In ASP .NET context marshaling is a process of transforming or serializing data from one application domain and exporting it to another application domain.
+   - There are two types of marshalling,
+     - Marshal by value : A copy of an object is created by the server and is passed and used by the client.
+     - Marshal by reference : The client creates a proxy to access the object.

# Long Answered Questions

+   - Q.1 Explain .NET architecture. (Refer section 1.1)
+   - Q.2 What are features of .NET features ? (Refer section 1.1)
+   - Q.3 What is JIT and its various types in .NET environment ? (Refer section 1.1)
+   - Q.4 Write a note on C# programming language. (Refer section 1.12)
+   - Q.5 What are OOP features ? (Refer section 1.3)