+   - Follow the compile-time processing steps for compiling an object-creation-expression of the form new T(P). These steps either result in a compile-time error, or determine an instance constructor C on T that can be invoked at run-time.
+   - If C does not have public accessibility, then a compile-time error occurs.
+   - For each named-argument Arg in N:
+     - Let Name be the identifier of the named-argument Arg.
+     - Name must identify a non-static read-write public field or property on T. If T has no such field or property, then a compile-time error occurs.
+   - Keep the following information for run-time instantiation of the attribute: the attribute class T, the instance constructor C on T, the positional-argument-list P and the named-argument-list N.

# 17.3.2 Run-time retrieval of an attribute instance

Compilation of an attribute yields an attribute class T, an instance constructor C on T, a positional-argument-list P, and a named-argument-list N. Given this information, an attribute instance can be retrieved at run-time using the following steps:

+   - Follow the run-time processing steps for executing an object-creation-expression of the form new T(P), using the instance constructor C as determined at compile-time. These steps either result in an exception, or produce an instance O of T.
+   - For each named-argument Arg in N, in order:
+     - Let Name be the identifier of the named-argument Arg. If Name does not identify a non-static public read-write field or property on O, then an exception is thrown.
+     - Let Value be the result of evaluating the attribute-argument-expression of Arg.
+     - If Name identifies a field on O, then set this field to Value.
+     - Otherwise, Name identifies a property on O. Set this property to Value.
+     - The result is O, an instance of the attribute class T that has been initialized with the positional-argument-list P and the named-argument-list N.

# 17.4 Reserved attributes

A small number of attributes affect the language in some way. These attributes include:

+   - System.AttributeUsageAttribute (§17.4.1), which is used to describe the ways in which an attribute class can be used.
+   - System.Diagnostics.ConditionalAttribute (§17.4.2), which is used to define conditional methods.
+   - System.ObsoleteAttribute (§17.4.3), which is used to mark a member as obsolete.

# 17.4.1 The AttributeUsage attribute

The attribute AttributeUsage is used to describe the manner in which the attribute class can be used.

A class that is decorated with the AttributeUsage attribute must derive from System.Attribute, either directly or indirectly. Otherwise, a compile-time error occurs.