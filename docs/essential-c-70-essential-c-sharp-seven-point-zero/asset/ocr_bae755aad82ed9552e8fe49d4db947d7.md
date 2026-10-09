The following additional restrictions on the yield statement result in compiler errors if they are violated:

+   * The yield statement may appear only inside a method, a user-defined operator, or the get accessor of an indexer or property. The member must not take any ref or out parameter.

+   * The yield statement may not appear anywhere inside an anonymous method or lambda expression (see Chapter 13).

+   * The yield statement may not appear inside the catch and finally clauses of the try statement. Furthermore, a yield statement may appear in a try block only if there is no catch block.

# **SUMMARY**

In this chapter, we reviewed the key collection classes and how they fit into categories according to the interfaces that they support. Each class focuses on inserting items into and retrieving items from the collection, using mechanisms such as by key, by index, or by FIFO or LIFO, to name a few. We also explored how to iterate over the collection. In addition, the chapter explained how to define custom collections with custom iterators for enumerating through items within the collection. (Iterators involve a contextual keyword, yield, that C# uses to generate underlying CIL code that implements the iterator pattern used by the foreach loop.)

In Chapter 18, we explore reflection, a topic briefly touched on earlier, albeit with little to no explanation. Reflection allows us to examine the structure of a type within CIL code at runtime.