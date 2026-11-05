+   - For each named-argument Arg in N:
+     - Let Name be the identifier of the named-argument Arg.
+     - Name must identify a nonstatic read-write public field or property on T. If T has no such field or property, then a compile-time error occurs.
+   - Keep the following information for runtime instantiation of the attribute: the attribute class T, the instance constructor C on T, the positional-argument-list P, and the named-argument-list N.

> > **MAREK SAFAR** The public accessibility restriction is a little bit confusing in this case. For instance, class attributes are declared lexically outside the class but they can still use private constants declared within the same class.

# 17.3.2 Runtime Retrieval of an Attribute Instance

Compilation of an attribute yields an attribute class T, an instance constructor C on T, a positional-argument-list P, and a named-argument-list N. Given this information, an attribute instance can be retrieved at runtime using the following steps:

+   - Follow the runtime processing steps for executing an object-creation-expression of the form new T(P), using the instance constructor C as determined at compile time. These steps either result in an exception, or produce an instance O of T.
+   - For each named-argument Arg in N, in order:
+     - Let Name be the identifier of the named-argument Arg. If Name does not identify a non-static public read-write field or property on O, then an exception is thrown.
+     - Let Value be the result of evaluating the attribute-argument-expression of Arg.
+     - If Name identifies a field on O, then set this field to Value.
+     - Otherwise, Name identifies a property on O. Set this property to Value.
+     - The result is O, an instance of the attribute class T that has been initialized with the positional-argument-list P and the named-argument-list N.

# 17.4 Reserved Attributes

A small number of attributes affect the language in some way. These attributes include:

+   - System.AttributeUsageAttribute (§17.4.1), which is used to describe the ways in which an attribute class can be used.