> **NOTE** Creating NuGet packages is discussed in Chapter 17, “Visual Studio 2015.”

With portable libraries, Microsoft maintains a huge list of which API is supported by what platform. When you’re creating a portable library, you see the dialog to configure what target platforms you need to support. Figure 31.7 shows a selection for .NET Framework 4.6, Windows Universal 10.0, Xamarin.Android, and Xamarin.iOS. With the selection, you’re limited to the APIs that are available with all selected target platforms. With the current selection, you can read the note in the dialog that .NET Framework 4.5, Windows 8, and Xamarin.iOS (Classic) are automatically targeted as well because these platforms do not have any APIs that are not already in the combined intersect of the selection.

![](bbox=[0.22, 0.34, 0.78, 0.79])

# Figure 31.7

The big disadvantage of the portable library is that you can’t have any code that is available only with specific platforms. You can use only what’s available everywhere, with all the selected target platforms. As a way around this, you can use portable libraries to define code for contracts and implement the contracts with platform-specific libraries where needed. To use the code from the platform-specific libraries with