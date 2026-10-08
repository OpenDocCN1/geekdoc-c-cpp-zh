| PARAMETER | DESCRIPTION |
| --- | --- |
| registeredorganization | The registry key value from HKLM\Software\Windows NT\CurrentVersion\RegisteredOrganization |
| rootnamespace | The root namespace of the current project. This parameter is used to replace the namespace in an item being added to a project. |
| safeitemname | The name provided by the user in the Add New Item dialog box, with all unsafe characters removed and replaced by underscores. |
| safeprojectname | The name provided by the user in the New Project dialog box, with all unsafe characters removed and replaced by underscores. |
| time | The current time in the format DD/MM/YYYY 00:00:00. |
| userdomain | The current user domain name. |
| username | The current user name. |
| webnamespace | The name of the current web site. This parameter is used in the web template to guarantee unique class names. The web site is at the root directory of the web server, this template resolves to the root directory of the web Server. |
| year | The current year in the format YYYY. |

# # Custom Template Parameters

The <TemplateContent> element has an optional child element <CustomParameters> that can be used independently if the template is a project or item template. <CustomParameters> is a container that hold one or more <CustomParameter> elements, each of which holds two attributes: Name and Value. A <CustomParameter> describes a placeholder substitution, where Name is the placeholder to be replaced with Value.

Let's assume you have the following <TemplateContent> section in the manifest file:

```
<TemplateContent>
  <!-- ... -->
  <CustomParameters>
    <CustomParameter Name="$ClassName$ Value="EventClass" />
    <CustomParameter Name="$idPropertyType$ Value="long" />
    <CustomParameter Name="$idProperty$ Value="SeqNo" />
    <CustomParameter Name="$displayNameProperty$ Value="ShortName" />
  </CustomParameters>
</TemplateContent>
```