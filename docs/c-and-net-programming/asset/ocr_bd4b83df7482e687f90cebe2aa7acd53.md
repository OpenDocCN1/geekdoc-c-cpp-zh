# 28.1.9 .NET Compact Framework - Supported Languages

+   - The .NET Compact Framework supports two development languages, C# .NET and Visual Basic .NET. While previous versions of Windows CE development tools favored C-based languages - namely eMbedded Visual C++ - with the .NET Compact Framework it makes little difference which of the languages to choose, because both are equally powerful and functional.
+   - As a late addition to the Visual Studio .NET development environment, J# is not supported by the .NET Compact Framework.
+   - Developer should also be aware that there is another language limitation under the .NET Compact Framework that does not exist under the .NET Framework. Under the .NET Framework mixed-language components can be used within a single project. In comparison, .NET Compact Framework projects are restricted to a single language, either C# .NET or Visual Basic .NET. The workaround to this single-language project limitation imposed by .NET Compact Framework is to create additional projects using the Class template. Alternate language code needs to be added to the template, and then simply add references to these classes in the application project.

# 28.1.10 .NET Compact Framework - Online Documentation

The documentation included with Visual Studio .NET provides information relating to the .NET Compact Framework. There are both .NET Compact Framework-specific topics, such as "Creating Custom Controls with the .NET Compact Framework", and line item identification of features supported under the .NET Compact Framework.

# 28.1.11 .NET Compact Framework IDE - Additional Features

In addition to all of the features found natively in Visual Studio .NET, there are the following device-specific features supported in .NET compact framework,

+   1. **Templates** - Predefined configurations for common project types. Templates are provided for both Pocket PC and Windows CE devices.
+   2. **Device-specific controls** - Controls specifically designed for use with the Pocket PC and Windows CE. The interface, resource consumption and functionality have been tailored for these environments.
+   3. **Device emulators** - Testing environments that simulate specific devices. Emulators run on the developer's PC, allowing for testing without the presence of a device.
+   4. **Automatic deployment of applications** - Allows easy testing for either an emulator or a device, providing developers with a seamless testing environment.