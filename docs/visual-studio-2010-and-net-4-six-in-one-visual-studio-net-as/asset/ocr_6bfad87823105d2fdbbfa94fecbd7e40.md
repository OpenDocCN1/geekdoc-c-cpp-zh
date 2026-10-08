+   * It recognizes a .zip file in a template folder is not a simple .zip archive, but rather a template definition file.

+   * It uses the manifest to display information about templates in the New Project or Add New Item dialogs.

+   * It retrieves the list of items to be created for the new project or project item.

The following discussions describe the structure of the manifest file in detail and show a few samples to help you perform common tasks related to templates.

# The General Structure of the Manifest File

The .vtemplate file contains three fundamental, and two optional, elements representing its general structure:

```
<VTemplate Type="_type" Version="2.0.0"
xmlns="http://schemas.microsoft.com/developer/vtemplate/2005">
<TemplateData>
  <TemplateContent>
  </TemplateContent>
  <WizardExtension>
  </WizardExtension>
  <WizardData>

  </WizardData>
</VTemplate>
```

The VTemplate element has a Type attribute used to identify the template as a project or item. It can have the values Project or Item. As a special template type, it can also have the value of ProjectGroup that has been explained a bit later.

The Version attribute specifies the version number for the template. Since Visual Studio 2005, the value has been 2.0.0.

Following are the two other fundamental elements:

+   * <TemplateData> — This template categorization information and display characters for the New Project and Add New Item dialogs.

+   * <TemplateContent> — This specifies the files included in the template.

Visual Studio allows using wizards that can add functionality to the templates. The <WizardExtension> and <WizardData> elements are responsible for specifying the assembly implementing the wizard and for passing information used by the wizard. These elements are optional.

Let’s look into the manifest file of the Command Processor item template you created earlier. Listing 4-5 shows the file.