libraries to describe a COM component's API, they now use metadata. That's right, WinRT components describe their API using the same .NET metadata format (ECMA-335) as was standardized by the ECMA committee. This is the same metadata format I've been discussing throughout this whole book.

Metadata is much richer than type libraries and the CLR already has a complete understanding of metadata. In addition, the CLR has supported interoperating with COM components via Runtime Callable Wrappers (RCWs) and COM Callable Wrappers (CCWs) since its inception. For the most part, this allows languages (like C#) running on top of the CLR to seamlessly interoperate with WinRT types and components.

In C#, when you have a reference to a WinRT object, you really have a reference to an RCW that internally refers to the WinRT object. Similarly, if you pass a CLR object to a WinRT API, you are really passing a reference to a CCW to the WinRT API and the CCW holds a reference to your CLR object.

WinRT components have their metadata embedded in files with a .winmd file extension. The WinRT components that ship with Windows have their metadata in the various Windows.*.winmd files, which can be found in the %WinDir%\System32\WinMetadata directory. When building an app, you would reference the one Windows.winmd file that the Windows SDK installs here:

```
```
%ProgramFiles(x86)%\Windows Kits\8.0\References\CommonConfiguration\Neutral\Windows.winmd
```
```

A major design goal of the Windows Runtime type system is to enable developers to be successful in writing apps using the technologies, tools, practices, and conventions that are already familiar and well-known to them. In order to achieve this, some WinRT features are projected to the respective development technologies. For .NET Framework developers, there are two kinds of projections:

+   - **CLR projections**   CLR projections are mappings performed implicitly by the CLR, usually related to reinterpreting metadata. The next section focuses on the WinRT Component Type System Rules and how the CLR projects these rules to the .NET Framework developer.
+   - **Framework projections**   Framework projections are mappings performed explicitly in your code by leveraging new APIs introduced into the Framework Class Library. Framework projections are required when the impedance mismatch between the WinRT type system and the CLR's type system is too great for the CLR to do it implicitly. Framework projections are discussed later in this chapter.

# # CLR Projections and WinRT Component Type System Rules

WinRT components conform to a type system similar to how the CLR enforces a type system. When the CLR sees a WinRT type, it usually allows that type to be used via the CLR's normal COM interop technologies. But, in some cases, the CLR hides the WinRT type (by dynamically setting it to private) and then the CLR exposes the type via a different type. Internally, the CLR is looking for certain types (via metadata) and then mapping these types to types in the Framework Class Library. For the complete list of WinRT types that the CLR implicitly projects to Framework Class Library types, see