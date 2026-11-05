
```
public static T PtrToStructure<T>(IntPtr ptr);
```

T - 结构类型。

ptr - 指向非托管内存块的指针。

示例：

```
NATIVE_STRUCT result = Marshal.PtrToStructure<NATIVE_STRUCT>(ptr);
```

- 如果在读取本机结构时处理托管对象，别忘了固定你的对象 :)

```
T Read<T>(byte[] buffer)
{
    T result = default(T);
    var gch = GCHandle.Alloc(buffer, GCHandleType.Pinned);
    try
    {
        result = Marshal.PtrToStructure<T>(gch.AddrOfPinnedObject());
    }
    finally
    {
        gch.Free();
    }
    return result;
}
```

### 第155.6节：处理 Win32 错误

使用互操作方法时，你可以使用 GetLastError API 获取有关 API 调用的附加信息。

### DllImport 特性与 SetLastError 特性

SetLastError=true

表示被调用方将调用 SetLastError（Win32 API 函数）。

SetLastError=false

表示被调用方不会调用 SetLastError（Win32 API 函数），因此你将无法获取错误信息。

- 未设置 SetLastError 时，它会被设为 false（默认值）。
- 你可以使用 Marshal.GetLastWin32Error 方法获取错误代码：

示例：

```
[DllImport("kernel32.dll", SetLastError=true)]
public static extern IntPtr OpenMutex(uint access, bool handle, string lpName);
```

如果你尝试打开不存在的互斥体，GetLastError 将返回 ERROR_FILE_NOT_FOUND。

```
var lastErrorCode = Marshal.GetLastWin32Error();
```

```
if (lastErrorCode == (uint)ERROR_FILE_NOT_FOUND)
{
    //Deal with error
}
```

系统错误代码可在此处找到：

https://msdn.microsoft.com/en-us/library/windows/desktop/ms681382(vs=85).aspx

### GetLastError API

还有一个原生 GetLastError API 也可以使用：

```
[DllImport("coredll.dll", SetLastError=true)]
static extern Int32 GetLastError();
```

- 从托管代码调用 Win32 API 时，必须始终使用 Marshal.GetLastWin32Error。

原因如下：

在你的 Win32 调用（设置错误，即调用 SetLastError）与后续操作之间，CLR 可能会调用其他 Win32 调用，而这些调用也可能调用 SetLastError；这种行为可能会覆盖你的错误值。在这种情况下，如果你调用 GetLastError，你可能会获得无效的错误。

设置 SetLastError = true 可确保 CLR 在执行其他 Win32 调用之前检索错误代码。

### 第155.7节：固定对象

GC（垃圾回收器）负责清理我们的垃圾。

GC 在清理垃圾时，会从托管堆中移除未使用的对象，这些对象会导致堆碎片化。GC 完成移除后，会执行堆压缩（碎片整理），这涉及在堆上移动对象。

### 固定对象

固定对象是不允许被 GC 移动的对象。

### GC 固定句柄

你可以使用 GCHandle.Alloc 方法创建固定对象

```
GCHandle handle = GCHandle.Alloc(yourObject, GCHandleType.Pinned);
```

- 为托管对象获取固定的 GCHandle 会将特定对象标记为在释放该句柄之前不能被 GC 移动的对象

示例：

```
[DllImport("kernel32.dll", SetLastError = true)]
```

```
public int StopTime()
{
    return (int)stopWatch.ElapsedMilliseconds;
}
}
```

## 第157章：ILGenerator

### 第157.1节：创建包含 UnixTimestamp 辅助方法的 DynamicAssembly

本示例通过生成代码来展示 ILGenerator 的用法，这些代码使用了已有成员和新创建的成员，以及基本的异常处理。以下代码会生成一个 DynamicAssembly，其中包含与此 C# 代码等效的内容：

```
public static class UnixTimeHelper
{
    private readonly static DateTime EpochTime = new DateTime(1970, 1, 1);

    public static int UnixTimestamp(DateTime input)
    {
        int totalSeconds;
        try
        {
            totalSeconds = checked((int)input.Subtract(UnixTimeHelper.EpochTime).TotalSeconds);
        }
        catch (OverflowException overflowException)
        {
            throw new InvalidOperationException("It's too late for an Int32 timestamp.", overflowException);
        }
        return totalSeconds;
    }
}

//Get the required methods
var dateTimeCtor = typeof (DateTime)
    .GetConstructor(new[] {typeof (int), typeof (int), typeof (int)});
var dateTimeSubtract = typeof (DateTime)
    .GetMethod(nameof(DateTime.Subtract), new[] {typeof (DateTime)});
var timeSpanSecondsGetter = typeof (TimeSpan)
    .GetProperty(nameof(TimeSpan.TotalSeconds)).GetGetMethod();
var invalidOperationCtor = typeof (InvalidOperationException)
    .GetConstructor(new[] {typeof (string), typeof (Exception)});

if (dateTimeCtor == null || dateTimeSubtract == null ||
    timeSpanSecondsGetter == null || invalidOperationCtor == null)
{
    throw new Exception("Could not find a required Method, can not create Assembly.");
}

//Setup the required members
var an = new AssemblyName("UnixTimeAsm");
var dynAsm = AppDomain.CurrentDomain.DefineDynamicAssembly(an, AssemblyBuilderAccess.RunAndSave);
var dynMod = dynAsm.DefineDynamicModule(an.Name, an.Name + ".dll");

var dynType = dynMod.DefineType("UnixTimeHelper",
    TypeAttributes.Abstract | TypeAttributes.Sealed | TypeAttributes.Public);

var epochTimeField = dynType.DefineField("EpochStartTime", typeof (DateTime),
    FieldAttributes.Private | FieldAttributes.Static | FieldAttributes.InitOnly);

var cctor =
    dynType.DefineConstructor(
```
```csharp
MethodAttributes.Private | MethodAttributes.HideBySig | MethodAttributes.SpecialName |
MethodAttributes.RTSpecialName | MethodAttributes.Static, CallingConventions.Standard,
Type.EmptyTypes);

var cctorGen = cctor.GetILGenerator();
cctorGen.Emit(OpCodes.Ldc_I4, 1970); //Load the DateTime constructor arguments onto the stack
cctorGen.Emit(OpCodes.Ldc_I4_1);
cctorGen.Emit(OpCodes.Ldc_I4_1);
cctorGen.Emit(OpCodes.Newobj, dateTimeCtor); //Call the constructor
cctorGen.Emit(OpCodes.Stsfld, epochTimeField); //Store the object in the static field
cctorGen.Emit(OpCodes.Ret);

var unixTimestampMethod = dynType.DefineMethod("UnixTimestamp",
    MethodAttributes.Public | MethodAttributes.HideBySig | MethodAttributes.Static,
    CallingConventions.Standard, typeof (int), new[] { typeof (DateTime) });

unixTimestampMethod.DefineParameter(1, ParameterAttributes.None, "input");

var methodGen = unixTimestampMethod.GetILGenerator();
methodGen.DeclareLocal(typeof (TimeSpan));
methodGen.DeclareLocal(typeof (int));
methodGen.DeclareLocal(typeof (OverflowException));

methodGen.BeginExceptionBlock(); //Begin the try block
methodGen.Emit(OpCodes.Ldarga_S, (byte) 0); //To call a method on a struct we need to load the
//address of it
methodGen.Emit(OpCodes.Ldsfld, epochTimeField);
    //Load the object of the static field we created as argument for the following call
methodGen.Emit(OpCodes.Call, dateTimeSubtract); //Call the subtract method on the input DateTime
methodGen.Emit(OpCodes.Stloc_0); //Store the resulting TimeSpan in a local
methodGen.Emit(OpCodes.Ldloca_S, (byte) 0); //Load the locals address to call a method on it
methodGen.Emit(OpCodes.Call, timeSpanSecondsGetter); //Call the TotalSeconds Get method on the
TimeSpan
methodGen.Emit(OpCodes.Conv_Ovf_I4); //Convert the result to Int32; throws an exception on overflow
methodGen.Emit(OpCodes.Stloc_1); //store the result for returning later
//The leave instruction to jump behind the catch block will be automatically emitted
methodGen.BeginCatchBlock(typeof (OverflowException)); //Begin the catch block
//When we are here, an OverflowException was thrown, that is now on the stack
methodGen.Emit(OpCodes.Stloc_2); //Store the exception in a local.
methodGen.Emit(OpCodes.Ldstr, "It's too late for an Int32 timestamp.");
    //Load our error message onto the stack
methodGen.Emit(OpCodes.Ldloc_2); //Load the exception again
methodGen.Emit(OpCodes.Newobj, InvalidOperationCtor);
    //Create an InvalidOperationException with our message and inner Exception
methodGen.Emit(OpCodes.Throw); //Throw the created exception
methodGen.EndExceptionBlock(); //End the catch block
//When we are here, everything is fine
methodGen.Emit(OpCodes.Ldloc_1); //Load the result value
methodGen.Emit(OpCodes.Ret); //Return it

dynType.CreateType();

dynAsm.Save(an.Name + ".dll");
```
```

### 第157.2节：创建方法重写

本示例展示如何在生成的类中重写 ToString 方法

```
```csharp
// create an Assembly and new type
var name = new AssemblyName("MethodOverriding");
var dynAsm = AppDomain.CurrentDomain.DefineDynamicAssembly(name, AssemblyBuilderAccess.RunAndSave);
```

