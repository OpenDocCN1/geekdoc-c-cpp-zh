
wants to play by the old rules. That is, tell the CLR that your **catch (Exception)** blocks should not catch an instance of the new **RuntimeWrappedException** class. And instead, the CLR should unwrap the non-CLS-compliant object and call your code only if you have a **catch** block that doesn't specify any type at all. You tell the CLR that you want the old behavior by applying an instance of the **RuntimeCompatibilityAttribute** to your assembly like this:

```csharp
using System.Runtime.CompilerServices;
[assembly:RuntimeCompatibility(WrapNonExceptionThrows = false)]
```

![](img/3c46ff5b170881db4209d365b1f7a808_491_0.png)

> **Note** This attribute has an assembly-wide impact. There is no way to mix wrapped and unwrapped exception styles in the same assembly. Be careful when adding new code (that expects the CLR to wrap exceptions) to an assembly containing old code (in which the CLR didn't wrap exceptions).

## The System.Exception Class

The CLR allows an instance of any type to be thrown for an exception—from an **Int32** to a **String** and beyond. However, Microsoft decided against forcing all programming languages to throw and catch exceptions of any type, so they defined the **System.Exception** type and decreed that all CLS-compliant programming languages must be able to throw and catch exceptions whose type is derived from this type. Exception types that are derived from **System.Exception** are said to be CLS-compliant. C# and many other language compilers allow your code to throw only CLS-compliant exceptions.

The **System.Exception** type is a very simple type that contains the properties described in Table 20-1. Usually, you will not write any code to query or access these properties in any way. Instead, when your application terminates due to an unhandled exception, you will look at these properties in the debugger or in a report that gets generated and written out to the Windows Application event log or crash dump.

**TABLE 20-1 Public Properties of the System.Exception Type**

| Property | Access | Type | Description |
|---|---|---|---|
| **Message** | Read-only | **String** | Contains helpful text indicating why the exception was thrown. The message is typically written to a log when a thrown exception is unhandled. Since end users do not see this message, the message should be as technical as possible so that developers viewing the log can use the information in the message to fix the code when producing a new version. |

The string returned from the StackTrace property doesn't include any of the methods in the call stack that are above the point where the catch block accepted the exception object. If you want the complete stack trace from the start of the thread up to the exception handler, you can use the System.Diagnostics.StackTrace type. This type defines some properties and methods that allow a developer to programmatically manipulate a stack trace and the frames that make up the stack trace.

You can construct a StackTrace object by using several different constructors. Some constructors build the frames from the start of the thread to the point where the StackTrace object is constructed. Other constructors initialize the frames of the StackTrace object by using an Exception-derived object passed as an argument.

If the CLR can find debug symbols (located in the .pdb files) for your assemblies, the string returned by System.Exception's StackTrace property or System.Diagnostics.StackTrace's ToString method will include source code file paths and line numbers. This information is incredibly useful for debugging.

Whenever you obtain a stack trace, you might find that some methods in the actual call stack don't appear in the stack trace string. There are two reasons for this. First, the stack is really a record of where the thread should return to, not where the thread has come from. Second, the just-in-time (JIT) compiler can inline methods to avoid the overhead of calling and returning from a separate method. Many compilers (including the C# compiler) offer a /debug command-line switch. When this switch is used, these compilers embed information into the resulting assembly to tell the JIT compiler not to inline any of the assembly's methods, making stack traces more complete and meaningful to the developer debugging the code.

![](img/3c46ff5b170881db4209d365b1f7a808_494_0.png)

> **Note** The JIT compiler examines the **System.Diagnostics.DebuggableAttribute** custom attribute applied to the assembly. The C# compiler applies this attribute automatically. If this attribute has the **DisableOptimizations** flag specified, the JIT compiler won't inline the assembly's methods. Using the C# compiler's **/debug** switch sets this flag. By applying the **System.Runtime.CompilerServices.MethodImplAttribute** custom attribute to a method, you can forbid the JIT compiler from inlining the method for both debug and release builds. The following method definition shows how to forbid the method from being inlined:

```csharp
using System;
using System.Runtime.CompilerServices;

internal sealed class SomeType {

    [MethodImpl(MethodImplOptions.NoInlining)]
    public void SomeMethod() {
        ...
    }
}
```

## FCL-Defined Exception Classes

The Framework Class Library (FCL) defines many exception types (all ultimately derived from **System.Exception**). The following hierarchy shows the exception types defined in the MSCorLib.dll assembly; other assemblies define even more exception types. (The application used to obtain this hierarchy is shown in Chapter 23, "Assembly Loading and Reflection.")

- System.Exception
  - System.AggregateException
  - System.ApplicationException
    - System.Reflection.InvalidFilterCriteriaException
    - System.Reflection.TargetException
    - System.Reflection.TargetInvocationException
    - System.Reflection.TargetParameterCountException
    - System.Threading.WaitHandleCannotBeOpenedException
    - System.InvalidTimeZoneException
    - System.IO.IsolatedStorage.IsolatedStorageException
    - System.Runtime.CompilerServices.RuntimeWrappedException
  - System.SystemException
    - System.AccessViolationException
    - System.AppDomainUnloadedException
    - System.ArgumentException
      - System.ArgumentNullException
      - System.ArgumentOutOfRangeException
      - System.DuplicateWaitObjectException
      - System.Globalization.CultureNotFoundException
      - System.Text.DecoderFallbackException
      - System.Text.EncoderFallbackException
    - System.ArithmeticException
      - System.DivideByZeroException
      - System.NotFiniteNumberException
      - System.OverflowException
    - System.ArrayTypeMismatchException
    - System.BadImageFormatException
    - System.CannotUnloadAppDomainException
    - System.Collections.Generic.KeyNotFoundException
    - System.ContextMarshalException
    - System.DataMisalignedException
    - System.ExecutionEngineException
    - System.FormatException
      - System.Reflection.CustomAttributeFormatException
    - System.IndexOutOfRangeException
    - System.InsufficientExecutionStackException
    - System.InvalidCastException
    - System.InvalidOperationException
      - System.ObjectDisposedException
    - System.InvalidProgramException
    - System.IO.IOException
      - System.IO.DirectoryNotFoundException
      - System.IO.DriveNotFoundException
      - System.IO.EndOfStreamException
      - System.IO.FileLoadException
      - System.IO.FileNotFoundException
      - System.IO.PathTooLongException
    - System.MemberAccessException
      - System.FieldAccessException
      - System.MethodAccessException
      - System.MissingMemberException
        - System.MissingFieldException
        - System.MissingMethodException
    - System.MulticastNotSupportedException
    - System.NotImplementedException
    - System.NotSupportedException
      - System.PlatformNotSupportedException
    - System.NullReferenceException
    - System.OperationCanceledException
      - System.Threading.Tasks.TaskCanceledException
    - System.OutOfMemoryException
      - System.InsufficientMemoryException
    - System.RankException
    - System.Reflection.AmbiguousMatchException
    - System.Reflection.ReflectionTypeLoadException
    - System.Resources.MissingManifestResourceException
    - System.Resources.MissingSatelliteAssemblyException
    - System.Runtime.InteropServices.ExternalException
      - System.Runtime.InteropServices.COMException
      - System.Runtime.InteropServices.SEHException
      - System.Runtime.InteropServices.InvalidComObjectException
      - System.Runtime.InteropServices.InvalidOleVariantTypeException
      - System.Runtime.InteropServices.MarshalDirectiveException
      - System.Runtime.InteropServices.SafeArrayRankMismatchException
      - System.Runtime.InteropServices.SafeArrayTypeMismatchException
    - System.Runtime.Remoting.RemotingException
      - System.Runtime.Remoting.RemotingTimeoutException
      - System.Runtime.Remoting.ServerException
    - System.Runtime.Serialization.SerializationException
    - System.Security.Cryptography.CryptographicException
      - System.Security.Cryptography.CryptographicUnexpectedOperationException
    - System.Security.HostProtectionException
    - System.Security.Policy.PolicyException
    - System.Security.Principal.IdentityNotMappedException
    - System.Security.SecurityException
    - System.Security.VerificationException
    - System.Security.XmlSyntaxException
    - System.StackOverflowException
    - System.Threading.AbandonedMutexException
    - System.Threading.SemaphoreFullException
    - System.Threading.SynchronizationLockException
    - System.Threading.ThreadAbortException
    - System.Threading.ThreadInterruptedException
    - System.Threading.ThreadStartException
    - System.Threading.ThreadStateException
    - System.TimeoutException
    - System.TypeInitializationException
    - System.TypeLoadException
      - System.DllNotFoundException
      - System.EntryPointNotFoundException
    - System.TypeUnloadedException
    - System.UnauthorizedAccessException
      - System.Security.AccessControl.PrivilegeNotHeldException
    - System.Threading.LockRecursionException
    - System.Threading.Tasks.TaskSchedulerException
    - System.TimeZoneNotFoundException
