| CHILD ELEMENT | DESCRIPTION |
|---|---|
| OpenInHelpBrowser | This optional attribute specifies whether the item should be opened in the Help viewer when a project is created from the template. Only HTML files and text files are local to the project can be opened in the Help browser. External URLs cannot be opened with this attribute. The default value is false. |
| OpenOrder | This optional attribute specifies a numeric value that represents the order in which items will be opened in their respective views (editors, web browser, or Helper). All values are multiples of ten. Items with lower OpenOrder values are opened first. |

The <TemplateContent> section of the Basic Command Console manifest is as follows:

```
<TemplateContent>
<Project TargetFileName="ConsoleBase.csproj" File="ConsoleBase.csproj"
ReplaceParameters="true">
<ProjectItem ReplaceParameters="true" TargetFileName="CommandProcessor.cs">
CommandProcessor.cs
</ProjectItem>
<ProjectItem ReplaceParameters="true"
TargetFileName="CommandProcessorItem.cs">
</ProjectItem>
<ProjectItem ReplaceParameters="true" TargetFileName="Program.cs">
Program.cs
</ProjectItem>
<Folder Name="Properties" TargetFolderName="Properties">
<ProjectItem ReplaceParameters="true" TargetFileName="AssemblyInfo.cs">
AssemblyInfo.cs
</ProjectItem>
</Folder>
</Project>
</TemplateContent>
```

You can see that all files — including the project file — preserve their original names in the .zip archive, and are ready for parameter replacement. As read in Table 4-5, the TargetFileName attribute can also be used to rename files with parameters. For example, in this template, you could replace the Program.cs filename with the project name by changing the related <ProjectItem> element to the following:

```
<ProjectItem ReplaceParameters="true" TargetFileName="$safaproject.cs"
Program.cs
</ProjectItem>
```

Attributes with the OpenIn prefix also be very useful. With them, you can automatically open the files you intend (or recommend to your template's users) to edit, and you can also display help