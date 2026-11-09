
ILDasm.exe 支持 /project 命令行开关，该开关可显示在 CLR 将 WinRT 类型投影为其 .NET Framework 等效类型后元数据会是什么样子。

以下代码演示如何在 C# 中实现各种 WinRT 组件。这些组件利用了本章中讨论的许多功能，并且代码中有大量注释解释正在发生的事情。如果你需要在 C# 中实现 WinRT 组件，我建议将此处展示的代码用作模型。

> **重要**  当托管代码使用同样用托管代码编写的 WinRT 组件时，CLR 会将该 WinRT 组件视为常规托管组件。也就是说，CLR 不会创建 CCW 和 RCW，因此不会通过这些包装器调用 WinRT API。这大大提高了性能。然而，在测试该组件时，API 的调用方式不会像从另一种语言（如原生 C/C++ 或 JavaScript）调用时那样。因此，除了性能和内存开销并非真实情况之外，托管代码可以将 null 传递给要求 String 的 WinRT API，而不会引发 ArgumentNullException。并且，用托管代码实现的 WinRT API 可以操作传入的数组，当 API 返回时，调用方会看到更改后的数组内容；通常，WinRT 类型系统禁止修改传入 API 的数组。这些只是你能够观察到的一些差异，所以请小心。

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
        public WinRTEnum AEnum;    // Really just a 32-bit integer
    }

    // Delegates must have WinRT-compatible types in the signature (no BeginInvoke/EndInvoke)
    public delegate String WinRTDelegate(Int32 x);

    // Interfaces can have methods, properties, & events but cannot be generic.
    public interface IWinRTInterface {
        // Nullable<T> marshals as IReference<T>
        Int32? InterfaceProperty { get; set; }
    }

    // Members without a [Version(#)] attribute default to the class's
    // version (1) and are part of the same underlying COM interface
    // produced by WinMDExp.exe.
    [Version(1)]
    // Class must be derived from Object, sealed, not generic,
    // implement only WinRT interfaces, & public members must be WinRT types
    public sealed class WinRTClass : IWinRTInterface {
        // Public fields are not allowed

        #region Class can expose static methods, properties, and events
        public static String StaticMethod(String s) { return "Returning " + s; }
        public static WinRTStruct StaticProperty { get; set; }

        // In JavaScript 'out' parameters are returned as objects with each
        // parameter becoming a property along with the return value
        public static String OutParameters(out WinRTStruct x, out Int32 year) {
            x = new WinRTStruct { AEnum = WinRTEnum.None, ANumber = 333, AString = "Jeff" };
            year = DateTimeOffset.Now.Year;
            return "Grant";
        }
        #endregion

        // Constructor can take arguments but not out/ref arguments
        public WinRTClass(Int32? number) { InterfaceProperty = number; }

        public Int32? InterfaceProperty { get; set; }

        // Only ToString is allowed to be overridden
        public override String ToString() {
            return String.Format("InterfaceProperty={0}",
                InterfaceProperty.HasValue ? InterfaceProperty.Value.ToString() : "(not set)");
        }

        public void ThrowingMethod() {
            throw new InvalidOperationException("My exception message");

            // To throw a specific HRESULT, use COMException instead
            //const Int32 COR_E_INVALIDOPERATION = unchecked((Int32)0x80131509);
            //throw new COMException("Invalid Operation", COR_E_INVALIDOPERATION);
        }

        #region Arrays are passed, returned OR filled; never a combination
        public Int32 PassArray([ReadOnlyArray] /* [In] implied */ Int32[] data) {
            // NOTE: Modified array contents MAY not be marshaled out; do not modify the array
            return data.Sum();
        }

        public Int32 FillArray([WriteOnlyArray] /* [Out] implied */ Int32[] data) {
            // NOTE: Original array contents MAY not be marshaled in;
            // write to the array before reading from it
            for (Int32 n = 0; n < data.Length; n++) data[n] = n;
            return data.Length;
        }

        public Int32[] ReturnArray() {
            // Array is marshaled out upon return
            return new Int32[] { 1, 2, 3 };
        }
        #endregion

        // Collections are passed by reference
        public void PassAndModifyCollection(Dictionary<String, Object> collection) {
            collection["Key2"] = "Value2";  // Modifies collection in place via interop
        }

        #region Method overloading
        // Overloads with same # of parameters are considered identical to JavaScript
        public void SomeMethod(Int32 x) { }

        [Windows.Foundation.Metadata.DefaultOverload]  // Makes this method the default overload
        public void SomeMethod(String s) { }
        #endregion

        #region Automatically implemented event
        public event WinRTDelegate AutoEvent;

        public String RaiseAutoEvent(Int32 number) {
            WinRTDelegate d = AutoEvent;
            return (d == null) ? "No callbacks registered" : d(number);
        }
        #endregion

        #region Manually implemented event
        // Private field that keeps track of the event's registered delegates
        private EventRegistrationTokenTable<WinRTDelegate> m_manualEvent = null;

        // Manual implementation of the event's add and remove methods
        public event WinRTDelegate ManualEvent {
            add {
                // Gets the existing table, or creates a new one if the table is not yet initialized
                EventRegistrationTokenTable<WinRTDelegate>
                    .GetOrCreateEventRegistrationTokenTable(ref m_manualEvent)
                    .AddEventHandler(value);
            }
            remove {
                EventRegistrationTokenTable<WinRTDelegate>
                    .GetOrCreateEventRegistrationTokenTable(ref m_manualEvent)
                    .RemoveEventHandler(value);
            }
        }

        public String RaiseManualEvent(Int32 number) {
            WinRTDelegate d = EventRegistrationTokenTable<WinRTDelegate>
                .GetOrCreateEventRegistrationTokenTable(ref m_manualEvent).InvocationList;
            return (d == null) ? "No callbacks registered" : d(number);
        }
        #endregion

        #region Asynchronous methods
        // Async methods MUST return IAsync[Action|Operation](WithProgress)
        // NOTE: Other languages see the DateTimeOffset as Windows.Foundation.DateTime
        public IAsyncOperationWithProgress<DateTimeOffset, Int32> DoSomethingAsync() {
            // Use the System.Runtime.InteropServices.WindowsRuntime.AsyncInfo's Run methods to
            // invoke a private method written entirely in managed code
            return AsyncInfo.Run<DateTimeOffset, Int32>(DoSomethingAsyncInternal);
        }

        // Implement the async operation via a private method using normal .NET technologies
        private async Task<DateTimeOffset> DoSomethingAsyncInternal(
            CancellationToken ct, IProgress<Int32> progress) {

            for (Int32 x = 0; x < 10; x++) {
                // This code supports cancellation and progress reporting
                ct.ThrowIfCancellationRequested();
                if (progress != null) progress.Report(x * 10);
                await Task.Delay(1000); // Simulate doing something asynchronously
            }
            return DateTimeOffset.Now; // Ultimate return value
        }

        public IAsyncOperation<DateTimeOffset> DoSomethingAsync2() {
            // If you don't need cancellation & progress, use
            // System.WindowsRuntimeSystemExtensions' AsAsync[Action|Operation]Task
            // extension methods (these call AsyncInfo.Run internally)
            return DoSomethingAsyncInternal(default(CancellationToken), null).AsAsyncOperation();
        }
        #endregion

        // After you ship a version, mark new members with a [Version(#)] attribute
        // so that WinMDExp.exe puts the new members in a different underlying COM
        // interface. This is required since COM interfaces are supposed to be immutable.
        [Version(2)]
        public void NewMethodAddedInV2() {
        }
    }
}
```
