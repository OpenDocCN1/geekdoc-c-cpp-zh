# HOUR 20

# Programming with Attributes

# What You'll Learn in This Hour:

+   - Understanding Attributes  
- Working with the Common Attributes  
- Using Custom Attributes  
- Accessing Attributes at Runtime

In Hour 1, "The .NET Framework and C#," you learned that C# supports component-oriented programming by enabling you to create assemblies that are self-contained, self-documenting, redistributable units of code. Metadata specifies how the types, properties, events, methods, and other code elements relate to one another. Attributes enable you to add additional metadata to an assembly, providing a way of associating declarative information with your code. Attributes are compiled and stored in the resulting CLI and can be accessed at runtime.

The .NET Framework provides and uses attributes for many different purposes. You saw one example of attributes in Hour 5, "Creating Enumerated Types and Structures," when you learned about flags enumerations. Attributes also describe security, describe how to serialize data, limit optimizations by the JIT compiler, and control the visibility of properties and methods during application development, among many other things. To add your own custom metadata, you use custom attributes that you create.

In this hour, you learn more about attributes—how to use them, create your own custom attributes, and access them at runtime.