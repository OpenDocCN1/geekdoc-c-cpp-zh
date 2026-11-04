for demonstration (and development) purposes, we can simply copy it. The following folder structure is required:

ExtensiCalc
- ExtensiCalc.exe
+ Extensions
- Geometry.dll

To simplify debugging of our own extensions, to be loaded by the host application, we can configure the build process in Visual Studio with a post-build step on the Geometry project. Figure 21.7 illustrates a configuration that will copy the built file to the appropriate location using some relative paths. Because we're building to the bin\Debug folder underneath the Geometry folder, we need to go three levels up so that we can take a right turn into the ExtensiCalc (host application) build folder. From here, we construct the path to the Extensions subfolder alongside the ExtensiCalc executable, again under bin\Debug (assuming you're building in Debug configuration). The $(TargetPath) variable is provided by MSBuild and contains the full path to the built assembly file. Such variables can be discovered by using the Edit Post-build button.

![](bbox=[0.06, 0.55, 0.62, 0.82])

FIGURE 21.7 Configuration of a Post-build event to copy a built assembly file.

Finally, when we run the application now, we should see a Pythagoras entry appear in the operations menu, as shown in Figure 21.8.

# Managed Extensibility Framework

One of the frameworks that helps with creating extensible applications on the .NET platform is MEF. Although a thorough discussion about MEF is beyond the scope of this chapter, a short introduction is warranted, especially because .NET 4 is the first version of the framework to ship this new technology out of the box.