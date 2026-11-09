
```csharp
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
        return String.Format("InterfaceProperty:{0}",
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
        collection["Key2"] = "Value2"; // Modifies collection in place via interop
    }

    #region Method overloading
    // Overloads with same # of parameters are considered identical to JavaScript
    public void SomeMethod(Int32 x) { }

    [Windows.Foundation.Metadata.DefaultOverload] // Makes this method the default overload
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
            // Gets the existing table, or lazily creates a new one if the table is not yet initialized
            return EventRegistrationTokenTable<WinRTDelegate>
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
    // Asynchronous methods MUST return IAsyncAction[Operation]WithProgress
    // NOTE: Other languages see the DateTimeOffset as Windows.Foundation.DateTime
    public IAsyncOperationWithProgress<DateTimeOffset, Int32> DoSomethingAsync() {
        // Use the System.Runtime.InteropServices.WindowsRuntime.AsyncInfo's Run methods to
        // invoke a private method written entirely in managed code
        return AsyncInfo.Run<DateTimeOffset, Int32>(DoSomethingAsyncInternal);
    }

    // Implement the async operation via a private method using normal managed code technologies
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
        // If you don't need cancellation & progress, use System.WindowsRuntimeSystemExtensions'
        // AsAsyncAction/Operation Task extension methods (these call AsyncInfo.Run internally)
        return DoSomethingAsyncInternal(default(CancellationToken), null).AsAsyncOperation();
    }
    #endregion

    // After you ship a version, mark new members with a [Version(#)] attribute
    // so that WinMDExp.exe puts the new members in a different underlying COM
    // interface. This is required since COM interfaces are supposed to be immutable.
    [Version(2)]
    public void NewMethodAddedInV2() {
    }
```

以下 JavaScript 代码演示如何访问前面所有 WinRT 组件和功能：

```javascript
function () {
    // Make accessing the namespace more convenient in the code
    var WinRTComps = WinTellect.WinRTComponents;

    // NOTE: The JavaScript VM projects WinRT APIs via camel casing

    // Access WinRT type's static method & property
    var s = WinRTComps.WinRTClass.staticMethod(null); // NOTE: JavaScript pass "null" here!
    var struct = { aNumber: 123, aString: "Jeff", aEnum: WinRTComps.WinRTEnum.none };
    WinRTComps.WinRTClass.staticProperty = struct;
    s = WinRTComps.WinRTClass.staticProperty; // Read it back

    // If the method has out parameters, they and the return value are returned as an object's properties
    var s = WinRTComps.WinRTClass.outParameters();
    var name = s.value; // Return value
    var struct = s.x; // an 'out' parameter
    var year = s.year; // another 'out' parameter

    // Construct an instance of the WinRT component
    var winRTClass = new WinRTComps.WinRTClass(null);
    s = winRTClass.toString(); // Call ToString()

    // Demonstrate throw and catch
    try { winRTClass.throwingMethod(); }
    catch (err) { }

    // Array passing
    var a = [1, 2, 3, 4, 5];
    var sum = winRTClass.passArray(a);
}

// Array filling
var arrayOut = [7, 7, 7];    // NOTE: fillArray sees all zeros!
var length = winRTClass.fillArray(arrayOut); // On return, arrayOut = [0, 1, 2]

// Array returning
a = winRTClass.returnArray();    // a = [1, 2, 3]

// Pass a collection and have its elements modified
var localSettings = Windows.Storage.ApplicationData.current.localSettings;
localSettings.values["Key1"] = "Value1";
winRTClass.passAndModifyCollection(localSettings.values);
// On return, localSettings.values has 2 key/value pairs in it

// Call overloaded method
winRTClass.someMethod(5);       // Actually calls SomeMethod(String) passing "5"

// Consume the automatically implemented event
f = function (v) { console.log(v.target); };
winRTClass.addEventListener("autoEvent", f, false);
s = winRTClass.raiseAutoEvent(7);

// Consume the manually implemented event
winRTClass.addEventListener("manualEvent", f, false);
s = winRTClass.raiseManualEvent(8);

// Invoke asynchronous method supporting progress, cancelation, & error handling
var promise = winRTClass.doSomethingAsync();
promise.then(
    function (result) { console.log("Async op complete: " + result); },
    function (error) { console.log("Async op error: " + error); },
    function (progress) {
        console.log("Async op progress: " + progress);
        //if (progress == 30) promise.cancel();    // To test cancelation
    }
);
```

## 第26章

## 线程基础

在本章中：

-   为什么 Windows 支持线程？ 691
-   线程开销 692
-   停止这种混乱 696
-   CPU 趋势 699
-   CLR 线程与 Windows 线程 703
-   使用专用线程执行异步计算密集型操作 704
-   使用线程的理由 706
-   线程调度和优先级 708
-   前台线程与后台线程 713
-   现在做什么？

在本章中，我将介绍有关线程的基本概念，并提供一种让开发者对这些概念及其用途进行概念化的方法。我将解释 Microsoft Windows 为何引入线程概念、CPU 趋势、公共语言运行时（CLR）线程与 Windows
