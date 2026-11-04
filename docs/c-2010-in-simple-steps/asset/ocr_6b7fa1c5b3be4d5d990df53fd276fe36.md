In Fig.C++11.3, you can see that when the dynamic method, **SomeMethod()**, is called, a value is returned according to the type of arguments passed to the **SomeMethod()** method. Also note that the result of any dynamic operation is of dynamic type.

Now, let’s examine how the dynamic types are actually resolved into the .NET types at runtime next.

# ## Runtime Lookup for Dynamic Type

When a variable is declared as dynamic the C# compiler treats all the operations performed on that variable as dynamic. Whether it is a dynamic method invocation, property access, or indexer call, the compiler knows that the result of dynamic operations will also be dynamic; therefore, the compiler transforms all the dynamic operations into a dynamic call site or DLR call site. A DLR call site is instantiated with a field of type T, which is an object of delegate type. This delegate type is used to contain the DLR caching mechanism that has been discussed in the **Describing the Dynamic Language Runtime** section of this chapter. After creating the DLR call site, the compiler invokes the delegate, which causes DLR to perform interoperability and caching. In case you do not have an **IDynamicObject**, the **CallSiteBinder** is invoked. C# has its own derived **CallSiteBinders**, which perform the correct binding. The binding results in an expression tree, which is consolidated into the DLR call site’s target delegate for DLR caching purposes. Once the expression tree becomes a part of the DLR caching mechanism, it is invoked so that the output of a user’s dynamic binding can be executed.

Now, let’s learn to create instances of **DynamicObject** and **ExpandObjects** classes in the next section.

# ## Creating the DynamicObject and ExpandObject Class Objects

If you wish to create your own dynamic objects, then you can derive the **DynamicObject** class or simply use the **ExpandObject** class. Using the **DynamicObject** class, you can specify dynamic behavior for an object. However, **DynamicObject** class cannot be directly instantiated. You first need to inherit this class. The **DynamicObject** class can be found in the **System.Dynamic** namespace. Using the **DynamicObject** class, you can specify the operations that can be performed on dynamic objects and how the operations will be performed. Some of the noteworthy methods of the **DynamicObject** class are enlisted in Table 11.1:

**Table 11.1: Noteworthy Methods of DynamicObject Class**

| Value | Description |
|---|---|
| TryBinaryOperation | Specifies how the binary operations, such as addition, subtraction, division, and multiplication can be implemented in classes that inherit the DynamicObject class. Overriding this method helps in specifying the dynamic behavior for binary operations. |
| TryConvert | Specifies how type conversion operations are implemented. Overriding this method in the classes that inherit the DynamicObject class helps in specifying the dynamic behavior for operations that deal with converting an object of one type to an object of another type. |
| TryGetIndex | Specifies how those operations, which get a value by index are implemented. Overriding this method in the classes that inherit the DynamicObject class helps in specifying the dynamic behavior for indexing operations. |
| TryGetMember | Specifies how the operations, which get member values are implemented. Overriding this method in a class that inherits the DynamicObject class helps in specifying the dynamic behavior for operations, such as retrieving a value for a property. |
| TryInvoke | Specifies how the operations, which invoke an object are implemented. Overriding this method in a class that inherits the DynamicObject class helps in specifying the dynamic behavior for operations, such as invoking a delegate. |
| TryInvokeMember | Specifies how the operations, which invoke a member are implemented. Overriding this method in a class that inherits the DynamicObject class helps in specifying the dynamic behavior for operations in which a method is invoked. |
| TrySetIndex | Specifies how those operations, which set a value by index are implemented. Overriding this method in a class that inherits the DynamicObject class helps in specifying the dynamic behavior for such operations, which use an index to access an object. |