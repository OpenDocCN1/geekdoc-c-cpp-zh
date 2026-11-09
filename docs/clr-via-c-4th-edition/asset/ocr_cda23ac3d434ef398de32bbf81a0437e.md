ILDasm.exe supports a /project command-line switch that shows you what the metadata would look like after the CLR projected the WinRT types into their .NET Framework equivalents.

The following code demonstrates how to implement various WinRT components in C#. The components leverage many of the features discussed throughout this chapter, and there are a lot of comments throughout the code to explain what is going on. If you need to implement a WinRT component in C#, I'd suggest using the code I show here as a model.

> > **Important**  When managed code consumes a WinRT component also written in managed code, the CLR treats the WinRT component as if it were a regular managed component. That is, the CLR will not create CCWs and RCWs, and therefore, it will not invoke the WinRT APIs via these wrappers. This improves performance greatly. However, when testing the component, APIs are not being invoked the way they would be if called from another language (like native C/C++ or JavaScript). So, aside from the performance and memory overhead not being real-life, managed code can pass null to a WinRT API requiring a String without an ArgumentNullException being thrown. And, WinRT APIs implemented in managed code can manipulate arrays that are passed in, and the caller will see the changed array contents when the API returns; normally, the WinRT type system forbids modifying arrays passed into an API. These are just some of the differences that you'll be able to observe, so beware.

```
```csharp
/***************************************************************
Module: WinRTComponents.cs
Notices: Copyright (c) 2012 by Jeffrey Richter
***************************************************************/

using System;
using System.Collections.Generic;
using System.Linq;
using System.Runtime.InteropServices.WindowsRuntime;
using System.Threading;
using System.Threading.Tasks;
using Windows.Foundation;
using Windows.Foundation.Metadata;

// The namespace MUST match the assembly name and cannot be "Windows"
namespace Wintellect.WinRTComponents {

    // [Flags] // Must not be present if enum is int; required if enum is uint
    public enum WinRTEnum : int {    // Enums must be backed by int or uint
        None,
        NotNone
    }

    // Structures can only contain core data types, String, & other structures
    // No constructors or methods are allowed
    public struct WinRTStruct {
        public Int32 ANumber;
        public String AString;
    }
```
```