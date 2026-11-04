
*This page intentionally left blank*

## Exploring the System Namespace

This chapter explores the **System** namespace. **System** is a top-level namespace of the .NET Framework class library. It directly contains those classes, structures, interfaces, delegates, and enumerations that are most commonly used by a C# program or that are deemed otherwise integral to the .NET Framework. Thus, **System** defines the core of the library.

**System** also contains many nested namespaces that support specific subsystems, such as **System.Net**. Several of these subsystems are described later in this book. This chapter is concerned only with the members of **System**, itself.

## The Members of System

In addition to a large number of exception classes, **System** contains the following classes:

|  |  |  |
|---|---|---|
| ActivationContext | Activator | AppDomain |
| AppDomainManager | AppDomainSetup | ApplicationId |
| ApplicationIdentity | Array | AssemblyLoadEventArgs |
| Attribute | AttributeUsageAttribute | BitConverter |
| Buffer | CharEnumerator | CLSCompliantAttribute |
| Console | ConsoleCancelEventArgs | ContextBoundObject |
| ContextStaticAttribute | Convert | DBNull |
| Delegate | Enum | Environment |
| EventArgs | Exception | FileStyleUriParser |
| FlagsAttribute | FtpStyleUriParser | GC |
| GenericUriParser | GopherStyleUriParser | HttpStyleUriParser |
| LdapStyleUriParser | LoaderOptimizationAttribute | LocalDataStoreSlot |
| MarshalByRefObject | Math | MTAThreadAttribute |
| MulticastDelegate | NetPipeStyleUriParser | NetTcpStyleUriParser |
| NewsStyleUriParser | NonSerializedAttribute | Nullable |
| Object | ObsoleteAttribute | OperatingSystem |
| ParamArrayAttribute | Random | ResolveEventArgs |
| SerializableAttribute | STATThreadAttribute | String |
| StringComparer | ThreadStaticAttribute | TimeZone |
| TimeZoneInfo | TimeZoneInfo.AdjustmentRule | Type |
| UnhandledExceptionEventArgs | Uri | UriBuilder |
| UriParser | UriTemplate | UriTemplateEquivalenceComparer |
| UriTemplateTable | UriTypeConverter | ValueType |
| Version | WeakReference |  |

**System** defines the following structures:

|  |  |  |
|---|---|---|
| ArgIterator | ArraySegment<T> | Boolean |
| Byte | Char | ConsoleKeyInfo |
| DateTime | DateTimeOffset | Decimal |
| Double | Guid | Int16 |
| Int32 | Int64 | IntPtr |
| ModuleHandle | Nullable<T> | RuntimeArgumentHandle |
| RuntimeFieldHandle | RuntimeMethodHandle | RuntimeTypeHandle |
| SByte | Single | TimeSpan |
| TimeZoneInfo.TransitionTime | TypedReference | UInt16 |
| UInt32 | UInt64 | UIntPtr |
| Void |  |  |

**System** defines the following interfaces:

|  |  |  |
|---|---|---|
| _AppDomain | IAppDomainSetup | IAsyncResult |
| ICloneable | IComparable | IComparable<T> |
| IConvertible | ICustomFormatter | IDisposable |
| IEquatable<T> | IFormatProvider | IFormattable |
| IServiceProvider |  |  |

System defines the following delegates:

| Action | Action<T> | Action<T1, T2> |
|---|---|---|
| Action<T1, T2, T3> | Action<T1, T2, T3, T4> | AppDomainInitializer |
| AssemblyLoadEventHandler | AsyncCallback | Comparison<T> |
| ConsoleCancelEventHandler | Converter<T, V> | CrossAppDomainDelegate |
| EventHandler | EventHandler<T> | Func<TResult> |
| Func<T, TResult> | Func<T1, T2, TResult> | Func<T1, T2, T3, TResult> |
| Func<T1, T2, T3, T4, TResult> | Predicate<T> | ResolveEventHandler |
| UnhandledExceptionEventHandler |  |  |

System defines these enumerations:

| ActivationContext.contextForm | AppDomainManagerInitializationOptions | AttributeTargets |
|---|---|---|
| Base64FormattingOptions | ConsoleColor | ConsoleKey |
| ConsoleModifiers | ConsoleSpecialKey | DateTimeKind |
| DayOfWeek | Environment.SpecialFolder | EnvironmentVariableTarget |
| GCCollectionMode | GenericUriParserOptions | LoaderOptimization |
| MidpointRounding | PlatformID | StringComparison |
| StringSplitOptions | TypeCode | UriComponents |
| UriFormat | UriHostNameType | UriIdnScope |
| UriKind | UriPartial |  |

As the preceding tables show, **System** is quite large. It is not possible to examine all of its constituents in detail in a single chapter. Furthermore, several of **System**'s members, such as **Nullable<T>**, **Type**, **Exception**, and **Attribute**, are discussed in Part I or elsewhere in Part II. Finally, because **System.String**, which defines the C# **string** type, is such a large and important topic, it is covered in Chapter 22 along with formatting. For these reasons, this chapter explores only those members that are most commonly used by C# programmers and that are not fully covered elsewhere.

## The Math Class

**Math** defines several standard mathematical operations, such as square root, sine, cosine, and logarithms. The **Math** class is **static**, which means all of the methods defined by **Math** are **static** and no object of type **Math** can be constructed. It also means **Math** is implicitly sealed and cannot be inherited. The methods defined by **Math** are shown in Table 21-1. All angles are in radians.

**Math** also defines these two fields:

```
public const double E
public const double PI
```

E is the value of the natural logarithm base, commonly referred to as e. PI is the value of pi.

| Method | Meaning |
|---|---|
| public static double Abs(double v) | Returns the absolute value of v. |
| public static float Abs(float v) | Returns the absolute value of v. |
| public static decimal Abs(decimal v) | Returns the absolute value of v. |
| public static int Abs(int v) | Returns the absolute value of v. |
| public static short Abs(short v) | Returns the absolute value of v. |
| public static long Abs(long v) | Returns the absolute value of v. |
| public static sbyte Abs(sbyte v) | Returns the absolute value of v. |
| public static double Acos(double v) | Returns the arc cosine of v. The value of v must be between −1 and 1. |
| public static double Asin(double v) | Returns the arc sine of v. The value of v must be between −1 and 1. |
| public static double Atan(double v) | Returns the arc tangent of v. |
| public static double Atan2(double y, double x) | Returns the arc tangent of y/x. |
| public static long BigMul(int x, int y) | Returns the result of x * y as a long value, thus avoiding overflow. |
| public static double Ceiling(double v) | Returns the smallest integer (represented as a floating-point value) not less than v. For example, given 1.02, Ceiling() returns 2.0. Given −1.02, Ceiling() returns −1. |
| public static double Ceiling(decimal v) | Returns the smallest integer (represented as a decimal value) not less than v. For example, given 1.02, Ceiling() returns 2.0. Given −1.02, Ceiling() returns −1. |
| public static double Cos(double v) | Returns the cosine of v. |
| public static double Cosh(double v) | Returns the hyperbolic cosine of v. |
| public static int DivRem(int x, int y, out int rem) | Returns the result of x / y. The remainder is returned in rem. |
| public static long DivRem(long x, long y, out long rem) | Returns the result of x / y. The remainder is returned in rem. |
| public static double Exp(double v) | Returns the natural logarithm base e raised to the v power. |
| public static decimal Floor(decimal v) | Returns the largest integer (represented as a decimal value) not greater than v. For example, given 1.02, Floor() returns 1.0. Given −1.02, Floor() returns −2. |
| public static double Floor(double v) | Returns the largest integer (represented as a floating-point value) not greater than v. For example, given 1.02, Floor() returns 1.0. Given -1.02, Floor() returns -2. |
| public static double IEEEremainder(double dividend, double divisor) | Returns the remainder of dividend / divisor. |
| public static double Log(double v) | Returns the natural logarithm for v. |
| public static double Log(double v, double base) | Returns the logarithm for v using base base. |
| public static double Log10(double v) | Returns the base 10 logarithm for v. |
| public static double Max(double v1, double v2) | Returns the greater of v1 and v2. |
| public static float Max(float v1, float v2) | Returns the greater of v1 and v2. |
| public static decimal Max(decimal v1, decimal v2) | Returns the greater of v1 and v2. |
| public static int Max(int v1, int v2) | Returns the greater of v1 and v2. |
| public static short Max(short v1, short v2) | Returns the greater of v1 and v2. |
| public static long Max(long v1, long v2) | Returns the greater of v1 and v2. |
| public static uint Max(uint v1, uint v2) | Returns the greater of v1 and v2. |
| public static ushort Max(ushort v1, ushort v2) | Returns the greater of v1 and v2. |
| public static ulong Max(ulong v1, ulong v2) | Returns the greater of v1 and v2. |
| public static byte Max(byte v1, byte v2) | Returns the greater of v1 and v2. |
| public static sbyte Max(sbyte v1, sbyte v2) | Returns the greater of v1 and v2. |
| public static double Min(double v1, double v2) | Returns the lesser of v1 and v2. |
| public static float Min(float v1, float v2) | Returns the lesser of v1 and v2. |
| public static decimal Min(decimal v1, decimal v2) | Returns the lesser of v1 and v2. |
| public static int Min(int v1, int v2) | Returns the lesser of v1 and v2. |
| public static short Min(short v1, short v2) | Returns the lesser of v1 and v2. |
| public static long Min(long v1, long v2) | Returns the lesser of v1 and v2. |
| public static uint Min(uint v1, uint v2) | Returns the lesser of v1 and v2. |
| public static ushort Min(ushort v1, ushort v2) | Returns the lesser of v1 and v2. |
