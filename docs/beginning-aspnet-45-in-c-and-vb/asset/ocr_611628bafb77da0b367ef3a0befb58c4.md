ameS has been renamed to _TestPage to reflect the new name of the page. If everything looks OK, you can delete TestPage.aspx because it's not used in the Planet Wrox website.

![](bbox=[0.1, 0.2, 0.8, 0.57])

FIGURE 6-11

# How It Works

When you export the template, Visual Studio creates a zip file with the necessary files—an ASPX file and a Code Behind file in this exercise. This zip file is then stored in the ItemTemplates subfolder of the Visual Studio 2012 folder under your Documents folder. Some of the files in the zip file contain the placeholders $relurInamespace$ and $safeitemname$. When you add a new file to the site that is based on your template using the Add New Item dialog box, VS replaces $relurInamespace$ with the name of the folder (nothing, in the case of a file added to the root of the site) and $safeitemname$ with the actual name of the page. In this exercise, you typed TestPage.aspx as the new name for the page, so you ended up with a class in the Code Behind called _TestPage, which in turn inherits from the global BasePage. The underscore (_) is hard-coded between the two placeholders and is really only needed when adding a Web Form based on this template to a subfolder. However, it's a valid start of a class identifier so you can safely leave it in for pages at the root of your website. If you add a file to a subfolder, such as the Demos folder, the class name is prefixed with the name of the folder so you end up with a class called Demos_TestPage. In addition to $relurInamespace$ and $safeitemname$, you can use a few other placeholders. Search the MSDN site at http://msdn.microsoft.com for the term $safeitemname$ to find the other template parameters.

If you need to make a change to the exported template, either redo the entire export process, or manually edit the files in the zip file.