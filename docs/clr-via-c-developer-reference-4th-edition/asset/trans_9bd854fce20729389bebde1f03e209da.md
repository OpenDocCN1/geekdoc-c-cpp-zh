
ILDasm 支持 `/project` 命令行开关，它可以显示将 CLR 投影到其 .NET Framework 等效项后的元数据数据格式。

以下代码演示了如何在 C# 中实现各种 WinRT 组件。这些组件利用了本章讨论的许多特性，并在期间有大量的注释来解释其运行机制。如果你需要在 C# 中实现 WinRT 组件，我建议使用我展示的代码作为模型。

> 当托管代码消耗同样用托管代码编写的 WinRT 组件时，CLR 将该 WinRT 组件视为一个普通的托管组件。也就是说，CLR 不会创建 CCW 和 RCW，因此它不会通过这些对象调用 WinRT API。这极地提升了性能。然而，在测试组件时，API 的调用方式与从其他语言（如原生 C++ 或 JavaScript）调用时不同。因此，除了性能和内存开销并非真实存在外，托管代码可以向 `null` 传递给本要求抛出 `ArgumentNullException` 的 WinRT API。托管代码中实现的 WinRT API 可以操作传入的数组，调用者会在 API 返回时看到数组的内容；而通常情况下，WinRT 类型系统禁止将数组传入 API。这些只是你能够观察到的一些区别，请务必注意。

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

// 命名空间必须匹配程序集名称且不能为 "Windows"
namespace Intellect.WinRTComponents {
    // [Flags] // 如果 enum 是 int，则不能存在；如果 enum 是 uint，则需要存在
    public enum WinRTEnum : int { // 枚举必须由 int 或 uint 支持
        None,
        NotNone
    }

    // 结构体只能包含核心数据类型、String 以及其他结构体
    // 不允许构造函数或方法
    public struct WinRTStruct {
        public int32 ANumber;
        public String AString;
        public WinRTEnum AEnum; // 本质上就是一个 32 位整数
    }
```

```
// 委托的签名必须具有 WinRT 兼容的类型（没有 BeginInvoke/EndInvoke）
public delegate String WinRTDelegate(Int32 x);
```

```
// 接口可以有方法、属性和事件，但不能是泛型的。
public interface IWinRT{
    // Nullable<T> 封化为 IReference<T>
    Int32 InterfaceProperty { get; set; }
}
```

```
// 没有 [Version()] 属性的成员默认使用类的版本
// 版本 (1)，并且是由 WinMDExp.exe 生成的同一个底层 COM 接口的一部分。
[Version(1)]
// 类必须派自 object、密封的 (sealed)、不能是泛型，
// 仅实现 WinRT 接口，且公共成员必须是 WinRT 的
public sealed class WinRTClass : IWinRTInterface{
    // 不允许公共字段

    #Region 类暴露的静态方法、属性和事件
    public static String Method(String s) { return "Returning " + s; }
    public static WinRTStruct StaticProperty { get; set; }

    // 在 JavaScript 中，“out" 参数被返回为对象，
    // 每个参数都变成一个属性，同返回值
    public static String OutParameters(out WinRTStruct x, out Int32 year) {
        x = new WinRTStruct { AEnum = WinRTEnum.None, ANumber = 333, AString = "Jeff" };
        year = DateTimeOffset.Now.Year;
        return "Grant";
    }
    #endregion

    // 构造函数可以接受参数，但不能接受 out/ref 参数
    public WinRTClass(Int32 number) : InterfaceProperty { get; set; }

    // 只允许覆盖 ToString()
    public override String ToString() {
        return String.Format("InterfaceProperty={0}",
        InterfaceProperty.HasValue ? InterfaceProperty.Value.ToString() : "not set");
    }

    public void ThrowsMethod() {
        throw new InvalidOperationException("My exception message");
    }

    // 如果要抛出特定的 HRESULT，请改用 COMException
    const Int32 COR_E_INVALIDOPERATION = unchecked((Int32)0x800131509);
    // throw new COMException("Invalid Operation", COR_E_INVALIDOPERATION);

    //region 数组可以是传递、返回或填充；绝不能同时进行
    public Int32 PassArray([ReadOnlyArray] / [Implied as / Int32[]] data {
        // 注意：修改后的数组内容可能 不被封化输出；不要修改数组
        return data.Sum();
    }

    public Int32 FillArray(WriteOnlyArray [] /* [Out] implied */ Int32[] data) {
        // 注意：原始数组内容可能 不被封化输入；
        // 在读取数组之前向数组写入
        for (Int32 n = 0; n < data.Length; n++) data[n] = n;
        return data.Length;
    }

    public Int32[] ReturnArray() {
        // 数组在返回时被封化输出
        return new Int32[] { 1, 2, 3 };
    }
    #endregion

    // 集合通过引用传递
    public void PassCollection(IDictionary<String, Object> collection) {
        collection["Key"] = "Value";
    }

    // 参数相同的重载是等等的
    public void SomeMethod(Int32 x) { }
    public void SomeMethod(String s) { }

    // 自动实现
    public event WinRTDelegate AutoEvent;

    public String RaiseAutoEvent(Int32 number) {
        WinRTDelegate d = AutoEvent;
        return (d == null) ? "No callbacks registered" : d(number);
    }

    // 手动实现
    // 用于跟踪事件的私有字段
    private EventRegistrationTable<WinRTDelegate> m_manualEvent = null;

    // 事件 add 和 remove 方法的手动实现
    public event WinRTDelegate ManualEvent {
        add {
            // 获取条目，如果表未初始化则创建一个新的
            GetOrCreateEventTokenTable<WinRTDelegate>(ref m_manualEvent).AddEventHandler(value);
        }
        remove {
            GetOrCreateEventTokenTable<WinRTDelegate>(ref m_manualEvent).RemoveEventHandler(value);
        }
    }

    public String RaiseManualEvent(Int32 number) {
        WinRTDelegate d = m_manualEvent.InvocationList;
        return (d == null) ? "No callbacks registered" : d(number);
    }

    #region 异步方法
    // 异步方法必须运行 IAsyncOperation(WithProgress)
    // 注意：其他语言使用 DateTimeOffset 作为 Windows.Foundation
    public IAsyncOperationWithProgress<DateTimeOffset, Int32> DoSomethingAsync() {
        // 使用 System.Runtime.Interop.Windows.Runtime.AsyncInfo 的方法来
        // 调用完全用托管代码编写的方法
        return AsyncInfo.Runtime<DateTimeOffset, Int32>DoSomethingAsyncInternal;
    }

    // 使用普通 .NET 技术的方法实现异步操作
    private async Task<DateTimeOffset> DoSomethingAsyncInternal(CancellationToken token, IProgress<Int32> progress) {
        for (Int32 x = 0; x < 10; x++) {
            // 此代码支持取消和进度报告
            token.ThrowIfCancellationRequested();
            if (progress != null) progress.Report(x * 10);
            await Task.Delay(1000); // 模拟异步操作
        }
        return DateTimeOffset.Now; // 最终返回值
    }

    public IAsyncOperation<DateTimeOffset> DoSomethingAsync2() {
        // 如果不需要取消和进度，请使用
        // System.Windows.RuntimeSystemExtensions 的 AsAsync Task
        // 扩展方法（此调用内部运行 AsyncInfo.Run）
        return DoSomethingAsyncInternal(default(CancellationToken), null).AsAsyncOperation();
    }
    #endregion
}
    // 在发布版本后，为新成员标记 [Version(#)] 属性
    // 这样 WinMDE.exp 将将新成员放在不同的底层 COM
    // 接口中。这是必要的，因为 COM 接口应该是不可变的。
    [Version(2)]
    public void NewMethodAddedInV2() { }
}
}
