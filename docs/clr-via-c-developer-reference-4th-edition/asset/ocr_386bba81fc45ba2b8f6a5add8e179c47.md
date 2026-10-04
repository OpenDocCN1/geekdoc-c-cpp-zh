DirectX or XAML

XAML

HTML & CSS

C/C++

CRT

C#/VB

FCL

JS

WinJS

(no runtime: rebuild for x86, x64, ARM)

CLR

"Chakra"

![](bbox=[0.125, 0.199, 0.678, 0.335])

**25-1** The kinds of features exposed by Windows's WinRT components and the various languages that Microsoft supports to access them.

WinRT components are internally implemented as Component Object Model (COM) components, which is a technology that Microsoft introduced in 1999. At the time, COM was considered a complicated model with a lot of arcane rules and a tedious programming model. However, there are lot of good ideas in COM, and over the years, Microsoft has tweaked it in to greatly simplify it. For WinRT, Microsoft made a significant tweak: instead of using type libraries to describe a COM component's API, they now use metadata. That's right, WinRT components describe their API using the .NET metadata format (ECMA-335) as standardized by the ECMA-mittee. This is the same metadata format I've been describing throughout this whole book.

Metadata is much richer than type libraries and the CLR already has a complete understanding of metadata. In addition, the CLR has supported interoperating with COM components Runtime Callable Wrappers (RCWs) and COM Callable Wrappers (CCWs) since its inception. For the most part, this allows (like C#) running on the CLR to seamlessly operate with WinRT types and components.

In C#, when you have a reference to a WinRT object, you really have a reference to an RCW that internally refers to the WinRT object. Similarly, if you pass a CLR object to a WinRT API, you are really passing a reference to a CCW to the WinRT API and the CCW holds a reference to your CLR object.

WinRT components have their metadata embedded in files with .winmd extension. The WinRT components that ship with Windows have their metadata in the various Windows.*winmd files, which can be found in the %WindowsDir%\System32\Metadata directory. When building an app, you would reference the winmd file that the Windows SDK installs here.

%ProgramFiles(x86)%\Windows Kits\8.0\CommonConfiguration\Neutral\Windows.winmd