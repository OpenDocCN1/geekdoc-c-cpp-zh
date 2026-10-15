and Microsoft Office 2010 to extend these office productivity tools with application-like features. Many organizations use Microsoft Office for tasks that border on custom applications. This is especially true for Microsoft Excel. VSTO provides project templates based on these Microsoft Office products that enable, for example, a spreadsheet to retrieve its contents from an SQL Server database instead of the local file system. These tools provide the capability not only to manipulate data retrieval and saving, but also to customize the user interface, including direct access to the task pane and custom toolbar options within Microsoft Office products; they are covered in more detail in Chapter 25.

Visual Studio 2010 Premium and Ultimate focus on extending a developer’s reach beyond just writing code. These tools are used to examine code for flaws, manage the deployment environment, and define relationships between applications. The high-end versions are focused on tools that support repeatable software processes and best practices. They are geared toward examining source code for hidden flaws that might not cause the code to fail, but might hide a hidden security flaw or make it difficult to maintain or deploy the application. More important, the suite includes tools for creating unit test tools that attempt to cause the code to fail, whether through bad input data or heavy load.

Complete coverage of all of Visual Studio Ultimate’s features warrants a book of its own, especially when you take into account all of the collaborative features introduced by Team Foundation Server and its tight integration with both Team Build and SharePoint Server. Team Foundation Server goes beyond just being a replacement for Visual Source Safe. It is the basis for true process-driven development, and it even includes documentation to help train your organization on two process models supported by Microsoft.

# VISUAL BASIC KEYWORDS AND SYNTAX

Those with previous experience with Visual Basic are already familiar with many of the language keywords and syntax. However, not all readers will fall into this category so this introductory section is for those new to Visual Basic. A glossary of keywords is provided after which this section will use many of these keywords in context.

Although they’re not the focus of the chapter, with so many keywords, a glossary follows. Table 1-2 briefly summarizes most of the keywords discussed in the preceding section, and provides a short description of their meaning in Visual Basic. Keep in mind there are two commonly used terms that aren’t Visual Basic keywords that you will read repeatedly including in the glossary:

+   > **Method** — A generic name for a named set of commands. In Visual Basic, both `subs` and `functions` are types of methods.

+   > **Instance** — When a class is created, the resulting object is an instance of the class’s definition.

TABLE 1-2: Commonly Used Keywords in Visual Basic

| KEYWORD | DESCRIPTION |
|---|---|
| Namespace | A collection of classes that provide related capabilities. For example, the `System.Drawing` namespace contains classes associated with graphics. |
| Class | A definition of an object. Includes properties (variables) and methods, which can be `Subs` or `Functions`. |
| Sub | A method that contains a set of commands, allows data to be transferred as parameters, and provides scope around local variables and commands, but does not return a value |
| Function | A method that contains a set of commands, returns a value, allows data to be transferred as parameters, and provides scope around local variables and commands |
| Return | Ends the currently executing `Sub` or `Function`. Combined with a return value for functions. |
| Dim | Declares and defines a new variable |
| New | Creates an instance of an object |