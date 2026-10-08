# LISTING 4-13 (continued)

```
<SupportedFrameworkRuntime minversion="4.0" maxversion="4.0" />
</Identifier>
<References />
<Content>
<ProjectTemplate>Template</ProjectTemplate>
<Assembly assemblyName="SimpleCommentWizard", Version=1.0.0.0, Culture=Neutral, 
  ublicKeyToken=641eb734f7120d3"*SimpleCommentWizard.dll"</Assembly>
</Content>
</VSX>
```

Code file [source.extension.vsmanifest] available for download at Wrox.

As you can see, a few options have been changed within <Identifier>, but the most important change is in <Content>:

+   The <ProjectTemplate> element indicates that the installer will look in the Template folder and copy it into the local application data of Visual Studio.
The <Assembly> element specifies that SimpleCommentWizard.dll is an assembly, and it should also be copied to the Extensions folder.

![](bbox=[0.513, 0.336, 0.879, 0.568])

FIGURE 4-25: Visual Studio Installer

After you have followed these steps, the installation is ready to build. Use the Build Rebuild command to create the .vsix file representing your project and open the output folder under your VS project folder, by default, and you can see the BasicConsoleInstaller.vsix file there. Opening this file will start the Visual Studio Extension Installer tool, as shown in Figure 4-25.

Click the Install button, and in few seconds, the utility will do what you expect, as shown in Figure 4-26.

![](bbox=[0.513, 0.606, 0.879, 0.836])

FIGURE 4-26: The template is installed