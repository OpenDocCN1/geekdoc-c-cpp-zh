# Hacking the Project Types 553

7. Right-click csConsoleApplication.vtemplate and select Edit from the menu to open the file in Notepad.

8. In the file, change each instance of ConsoleApplication to ConsoleApplication.

9. Add the bonded line to the file, in order to reference the new file.

```
<?xml version="1.0" encoding="utf-8"?>
<VTemplate Version="3.0" Type="Project" xmlns="http://schemas.microsoft.com/developer/VisualStudio/2005">
<TemplateData>
<Package Name="F40ACEC1-301F-11D3-B4F9-00C479EFFBC" ID="2320" />
<Description Package="F40ACEC1-301F-11D3-B4F9-00C479EFFBC" ID="2321" />
<Icon Package="F40ACEC1-301F-11D3-B4F9-00C479EFFBC" ID="4548" />
<TemplateType="Microsoft.CSharp.ConsoleApplication/"></TemplateType>
<RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
<SortOrder>70</SortOrder>
<NumberOfCategoriesToRollUp>1</NumberOfCategoriesToRollUp>
<NumberParentCategoriesToRollUp>
<CreateFolder="true"/>
<DefaultName="ConsoleApplication"/></DefaultName>
<ProvideDefaultName="true"/></ProvideDefaultName>
</TemplateData>
<TemplateContent>
<Project File="csConsoleApplication.csproj">
<ItemGroup>
<ProjectItem TargetFileName="Properties\AssemblyInfo.cs" ReplaceParameters="true" OpenEditor="true" />
<ProjectItem ReplaceParameters="true" OpenEditor="true">Program.cs</ProjectItem>
<ProjectItem ReplaceParameters="true" OpenEditor="true">Class1.cs</ProjectItem>
</ItemGroup>
</Project>
</TemplateContent>
</VTemplate>
```

10. Save and close ConsoleApplication.vtemplate.

11. Rename consoleapplication.csproj to consoleclass application.csproj.

12. Copy the directory back to the original folder.

13. Close Visual Studio Command Prompt as Administrator.

14. Open the Visual Studio All Programs in the Start Bar, by Visual Studio 2012:Visual Studio tools.

15. Run devenv /setup.

Now, when you open Visual Studio and create New Project, there should be a new project type, called Console And Class. Create a new project based on this type, and it will make you a Console .cs file and a .cs file.

![](bbox=[0.886, 0.693, 0.959, 0.853])