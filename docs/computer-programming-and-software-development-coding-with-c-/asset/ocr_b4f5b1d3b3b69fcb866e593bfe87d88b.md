# System

![](bbox=[0.195, 0.108, 0.715, 0.415])

At the very top we have the System namespace. System itself can contain types, but then there are other namespaces whose name also starts with System, then a dot, and then, for example, Web. In that namespace there will be all kinds of types that have to do with functionality. And the nesting can be deeper, a lot deeper, in fact, as you can see within the System.Data namespace. The types in .NET are placed in namespaces, but also our custom types, we'll see later, will be placed in custom namespaces. Using namespaces, we avoid naming collisions between different types with the same name.

```
using System;

using System.Data;

DataTable dataTable = new DataTable();//available through System.Data namespace
```