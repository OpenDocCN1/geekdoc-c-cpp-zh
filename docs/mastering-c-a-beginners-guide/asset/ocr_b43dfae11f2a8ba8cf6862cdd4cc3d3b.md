For instance, Generic is the nested namespace in the collections namespace as System.Collections.Generic and has the following syntax:

```
namespace name_of_namespace_1
{
    // Member declarations & definitions
    namespace name_of_namespace_2
    {
        // Member declarations & definitions
    .
    .
    }
}
```

Program:

```
// C# program to illustrate use of
// nested namespace
using System;
// You can also use
// using Main_name.Nest_name;
// to avoid the use of fully
// qualified name
// main namespace
namespace Main_name
{
    // nested namespace
    namespace Nest_name
    {
        // class within nested namespace
```