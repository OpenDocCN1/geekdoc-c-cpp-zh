keywords. For example, it is not possible to assign `null` to a generic type. In this case, the keyword `default` can be used, as demonstrated in the next section. If the generic type does not require the features of the `Object` class but you need to invoke some specific methods in the generic class, you can define constraints.

This section discusses the following topics:

+   - Default values
+   - Constraints
+   - Inheritance
+   - Static members

This example begins with a generic document manager, which is used to read and write documents from and to a queue. Start by creating a new Console project named `DocumentManager` and add the class `DocumentManager<T>`. The method `AddDocument` adds a document to the queue. The read-only property `IsDocumentAvailable` returns true if the queue is not empty (code file `DocumentManager/DocumentManager.cs`):

> **NOTE** *With .NET Core, this sample needs a reference to the NuGet package* `System.Collections`.

```
using System;
using System.Collections.Generic;

namespace Wrox.ProCSharp.Generics
{
    public class DocumentManager<T>
    {
        private readonly Queue<T> documentQueue = new Queue<T>();

        public void AddDocument(T doc)
        {
            lock (this)
            {
                documentQueue.Enqueue(doc);
            }
        }

        public bool IsDocumentAvailable => documentQueue.Count > 0;
    }
}
```

Threading and the lock statement are discussed in Chapter 21, “Tasks and Parallel Programming,” and Chapter 22, “Task Synchronization.”

# Default Values

Now you add a `GetDocument` method to the `DocumentManager<T>` class. Inside this method the type `T` should be assigned to `null`. However, it is not possible to assign `null` to generic types. That’s because a generic type can also be instantiated as a value type, and `null` is allowed only with reference types. To circumvent this problem, you can use the