
```
public static T PtrToStructure<T>(IntPtr ptr);
```

T - structure type.

ptr - A pointer to an unmanaged block of memory.

Example:

```
NATIVE_STRUCT result = Marshal.PtrToStructure<NATIVE_STRUCT>(ptr);
```

- If you are dealing with managed objects while reading native structures, don't forget to pin your object :)

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

### Section 155.6: Dealing with Win32 Errors

When using interop methods, you can use GetLastError API to get additional information on your API calls.

### DllImport Attribute SetLastError Attribute

SetLastError=true

Indicates that the callee will call SetLastError (Win32 API function).

SetLastError=false

Indicates that the callee will not call SetLastError (Win32 API function), therefore you will not get an error information.

- When SetLastError isn't set, it is set to false (Default value).
- You can obtain the error code using Marshal.GetLastWin32Error Method:

Example:

```
[DllImport("kernel32.dll", SetLastError=true)]
public static extern IntPtr OpenMutex(uint access, bool handle, string lpName);
```

If you are trying to open mutex which does not exist, GetLastError will return ERROR_FILE_NOT_FOUND.

```
var lastErrorCode = Marshal.GetLastWin32Error();
```

```
if (lastErrorCode == (uint)ERROR_FILE_NOT_FOUND)
{
    //Deal with error
}
```

System Error Codes can be found here:

https://msdn.microsoft.com/en-us/library/windows/desktop/ms681382(vs=85).aspx

### GetLastError API

There is a native GetLastError API which you can use as well :

```
[DllImport("coredll.dll", SetLastError=true)]
static extern Int32 GetLastError();
```

- When calling Win32 API from managed code, you must always use the Marshal.GetLastWin32Error.

Here's why:

Between your Win32 call which sets the error (calls SetLastError), the CLR can call other Win32 calls which could call SetLastError as well, this behavior can override your error value. In this scenario, if you call GetLastError you can obtain an invalid error.

Setting SetLastError = true, makes sure that the CLR retrieves the error code before it executes other Win32 calls.

### Section 155.7: Pinned Object

GC (Garbage Collector) is responsible for cleaning our garbage.

While GC cleans our garbage, it removes the unused objects from the managed heap which cause heap fragmentation. When GC is done with the removal, it performs a heap compression (defragmentation) which involves moving objects on the heap.

### Pinned Object

Pinned object is an object that is not allowed to move by GC.

### Gc Pinned Handle

You can create a pin object using GCHandle.Alloc method

```
GCHandle handle = GCHandle.Alloc(yourObject, GCHandleType.Pinned);
```

- Obtaining a pinned GCHandle to managed object marks a specific object as one that cannot be moved by GC, until freeing the handle

Example:

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

## Chapter 157: ILGenerator

### Section 157.1: Creates a DynamicAssembly that contains a UnixTimestamp helper method

This example shows the usage of the ILGenerator by generating code that makes use of already existing and new created members as well as basic Exception handling. The following code emits a DynamicAssembly that contains an equivalent to this C# code:

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

### Section 157.2: Create method override

This example shows how to override ToString method in generated class

```
```csharp
// create an Assembly and new type
var name = new AssemblyName("MethodOverriding");
var dynAsm = AppDomain.CurrentDomain.DefineDynamicAssembly(name, AssemblyBuilderAccess.RunAndSave);
```
