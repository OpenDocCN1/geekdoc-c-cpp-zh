# Version Numbers

In the previous section, you saw that several version numbers can be applied to an assembly. All of these version numbers have the same format: each consists of four period-separated parts, as shown in Table 2-5.

**TABLE 2-5** Format of Version Numbers

| Major Number | Minor Number | Build Number | Revision Number |
| --- | --- | --- | --- |
| Example: | 2 | 5 | 719 | 2 |

Table 2-5 shows an example of a version number: 2.5719.2. The first two numbers make up the public perception of the version. The public will build this example as 2.5 of the assembly. The third number, 719, indicates the build of the assembly. If your company builds its assembly every day, you increment the build number each day. The last, 2, indicates the revision of the build. If some reason your company has to build an assembly twice in one day, maybe to resolve a bug that is halting work, the revision number should be incremented. Microsoft uses this version-numbering scheme, and it's recommended that you use this scheme as well.

You'll notice that an assembly has three version numbers associated with it. This is very unfortunate and leads to a lot of confusion. Let me explain each version's version number and how it is expected to be used:

+   * AssemblyFileVersion This version number is stored in the Win32 version resource. This number is for information purposes only; the CLR doesnt examine this version in any way. Typically, you set the major and minor parts to represent the version you want the public to see. Then you increment the build and revision parts each time a build is performed. Ideally, Microsoft's tool (such as CSC.exe or AL.exe) would automatically update the build and revision numbers for you (based on date and time when the build was performed), but unfortunately, they don't. This version number can be seen when using Windows Explorer and is typically used to identify a specific version of an assembly when troubleshooting a customer's system.

+   * AssemblyInformationalVersion This version number is also stored in the Win32 version resource, and this number is for information purposes only; the CLR doesnt examine or care about it in any. This version number exists to identify the version of the product that includes this assembly. For example, version 2.0 of a product might contain several assemblies; one of these assemblies is marked as version 1.0 because it's a new assembly that didn't ship in version 1.0 of the same product. Typically, you set the major and minor parts of this version number to represent the public version of your product. Then you increment the build and revision parts each time you package a complete product with all its assemblies.