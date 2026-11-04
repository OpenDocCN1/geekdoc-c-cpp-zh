![](bbox=[0.05, 0.11, 0.48, 0.42])

FIGURE 3.4 .NET Framework 4 installation.

![](bbox=[0.06, 0.5, 0.48, 0.73])

FIGURE 3.5 The version of the CLR runtime shim.

Although the file description states “Microsoft .NET Runtime Execution Engine,” this is not the CLR itself, so where does the runtime itself live?

# The .NET 4.0 CLR

Having a runtime shim is one thing; having the runtime itself is invaluable. All runtime installations live side by side in the %windir%\Microsoft.NET\Framework folder. On 64-bit systems, there’s a parallel Framework64 folder structure. Having two “bitnesses” of the CLR and accompanying libraries is required to allow applications to run either as 32-bit (Windows On Windows, or WOW) or 64-bit.