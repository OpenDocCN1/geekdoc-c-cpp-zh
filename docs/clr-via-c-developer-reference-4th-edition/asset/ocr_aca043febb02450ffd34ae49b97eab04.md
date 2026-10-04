ILDasm supports a /project command-line switch that shows what the metadata would look after the CLR projected into their .NET Framework equivalents.

The following code demonstrates how to implement various WinRT components in C#. The components leverage many of the features discussed throughout this chapter, and there are a lot of comments throughout to explain what is going on. If you need to implement a WinRT component in C#, I'd suggest using the code I show as a model.

> > When managed code consumes a WinRT component also written in managed code, the CLR treats the WinRT component as if were a regular managed component. That is, the CLR will not create CCWs and RCW, and therefore it will not invoke the WinRT APIs via these. This improves performance greatly. However, when testing the component, APIs are not being invoked the way they would be called from another language (like native C++ or JavaScript). So, aside the performance and memory overhead not being real-life, managed code can pass null to a WinRT API requiring an ArgumentNullException being thrown. WinRT APIs implemented in managed code can manipulate arrays that are passed in, and the caller will see the array contents when the API returns; normally, the WinRT type system forbids passing arrays into an API. These are just some of the differences you'll be able to observe, so beware.

```
****************************************************************************************************
Module: WinRTComponents.cs
Notices: Copyright (c) 2012 by Jeffrey Richter
****************************************************************************************************

using System;
using System.Collections.Generic;
using System.Linq;
using System.Runtime.InteropServices.WindowsRuntime;
using System.Threading;
using System.Threading.Tasks;
using Windows.Foundation;
using Windows.Foundation.Metadata;

// The namespace MUST match the assembly name and cannot be "Windows"
namespace Intellect.WinRTComponents {
// [Flags] // Must not be present if enum is int; required if enum is uint
    public enum WinRTEnum : int { // Enums must be backed by int or uint
        None,
        NotNone
}

// Structures can only contain core data types, String, & other structures
// No constructors or methods are allowed
    public struct WinRTStruct {
        public int32 ANumber;
        public String AString;
```