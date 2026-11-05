+   5. There are two basic ways to marshal an object.
+      1. *Marshal by value* the server creates a copy of the object passes the copy to the client.
+         - Marshaling by value is similar to having a copy of the server object at the client.
+         - Objects that are marshaled **by value** are created on the remote server, serialized into a stream, and transmitted to the client where an exact copy is reconstructed.
+         - Once copied to the caller's application domain (by the marshaling process), all method calls and property accesses are executed entirely within that domain.
+         - Marshal by value objects are, **very efficient** if they are small, and provide a repeated function that does not consume bandwidth.
+         - The entire object exists in the caller's domain, so there is no need to marshal accesses across domain boundaries.
+         - Using marshal-by-value objects one can **increase performance** and **reduce network traffic**, when used for small objects or objects to which one will be making many accesses.
+         - Marshal by value classes must either be marked with the **[Serilaizable]** attribute in order to use the default serialization, or must implement the ISerializable interface.
+      2. *Marshal by reference* the client creates a proxy for the object and then uses the proxy to access the object Marshaling by reference is similar to having a pointer to the object.
+         - Marshal by reference passes a reference to the remote object back to the client. This reference is an **ObjRef** class that contains all the information required to generate the proxy object that does the communication with the actual remote object.
+         - On the network, **only parameters** and **return values** are passed. A remote method invocation requires the remote object to call its method on the remote host (server).
+         - Marshal by reference classes must inherit from **System.MarshalByRefObject.**

# **24.8 Object Activation**

# **Concept**

+   1. Object activation means various ways in which a remote object can be instantiated.
+   2. Marshal by value objects have a simple activation scheme, they are created when the client first requests them.
+   3. Marshal by reference objects have following two activation schemes.