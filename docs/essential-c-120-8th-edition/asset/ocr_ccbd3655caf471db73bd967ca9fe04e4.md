frameworks are emerging from .NET Core as more and more operating systems are supported.

# .NET Multi-platform App UI (MAUI)

This cross-platform development tool includes application UI development support for Microsoft Windows, Android, macOS, and iOS. What makes MAUI especially powerful is that single code base can be used to produce platform-native user interfaces on each of the operating systems supported.

# .NET Standard

Historically, it has been quite difficult to write a library of C# code that can be used on multiple operating systems or even different .NET frameworks on the same operating system. The problem was that the framework APIs on each framework had different classes available (and/or methods in those classes). The .NET Standard solves this issue by defining a common set of .NET APIs that each framework must implement to be compliant with a specified version of the .NET Standard. This uniformity ensures that developers have a consistent set of APIs available to them across each .NET framework that is compliant with the .NET Standard version they target.

For more information, including the mapping of .NET framework implementations and their versions to their corresponding .NET Standard version, see http://it.lc/NETStandard.

# Base Class Library

In addition to providing a runtime environment in which CIL code can execute, the CLI defines a core set of class libraries that programs may employ, called the Base Class Library. The class libraries contained in the BCL provide foundational types and APIs, allowing programs to interact with the runtime and underlying operating system in a consistent manner. The BCL includes support for collections, simple file access, some security, fundamental data types (string, among others), streams, and the like.