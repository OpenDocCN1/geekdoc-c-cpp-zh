
# Building Online Code Snippet Providers

With code snippets, you can create an online repository where you can select snippets categorized by your interest, and then download them to your machine. While snippets can be converted into the .snippet file format, you can import them with Code Snippets Manager or create your own custom template.

When you have a code snippet, you can upload it to a site with its .snippet file format. The structure of a snippet file contains a few elements (such as the <Keywords> and <HelpUrl> child elements of <Header>) is intended to be used by online snippet providers to help with the categorization and organization of snippets.

You can even add new information to your code snippets, although the current code snippet scheme does not allow creating your own elements or attributes. Despite this schema constraint, you can add your own elements and attributes, as shown in the following example:

```
<Snippet>
<Code Language="C#" MyAttr="myfile">
<![CDATA[Console.WriteLine();]]>
</Code>
<XmlElement Element="#####">\XmlElement>
</Snippet>
```

Here, MyElement and MyAttr are invalid elements by schema definition, but in reality, the Code Snippets Manager does not validate the .snippet file against the schema. While the Code Snippets Manager finds the elements it looks for, it remains happy, and simply does not take care of other elements and attributes.

> Although you can do this trick, it is not recommended. You cannot be sure that a future release of Visual Studio will not change this undocumented behavior. If you want to provide some kind of extension, you can use the kind attribute of the element or the <Function> element nested inside <Object>.

# SNIPPET EDITORS

Editing .snippet files in Visual Studio is easy when you attach the appropriate XSD schema file to it, because IntelliSense helps by listing elements, attributes, and values in the current context. However, the user experience through editing the XML file (even with IntelliSense) is not always pleasant. The less complex code of your XML file is the  element encapsulating the body of the code. The more complex code template you create, the larger the <Declaration> part is. As you use the declarations longer than one or two pages on the screen, you can easily lose the focus. You must manage up and understand what the code template is about.

The community recognized that the built-in Visual Studio editing support can be improved with other tools that provide code template editing similar to editing the original code. Tag 3-5 shows a few snippet editors created and supported by the community.

# TABLE 3-5: Code Snippet Editors and Tools

| NAME | URL |
|---|---|
| Snippy | http://www.codeplex.com/snippy |
| Export as Code Snippet Add-In | http://exportcodesnippet.codeplex.com |
| Snipp Dogg | http://snippddogg.codeplex.com/ |
| Snippet Builder | http://snippetbuilder.codeplex.com/ |
| Snippet Designer | http://snippetdesigner.codeplex.com/ |
| Snippet Editor | http://www.codeplex.com/SnippetEditor |

Let's take a quick look at three of these, each using a separate approach to help code snippet development.

# Export as Code Snippet Add-In

This add-in was created by Alessandro Del Sole, and it works only with Visual Studio 2008. However, the full source code of the add-in can be downloaded, so you can update it to work with Visual Studio 2010 as well.

This is a good add-in because it is simple and helps you create snippets directly from your code. Often, you get the idea of making a snippet from a part of code right when you are typing the text and recognize that it is recognizable. With this add-in, you simply right-click on the selected code (this would be the base of the code template), and your snippet is about to be created. Figure 3-22 shows this step.

![](img/b5597c749e848b27b0d305153ae16106_101_0.png)

FIGURE 3-22: Selecting the code template

Next, you can add metadata attributes to the code template by filling in the form shown in Figure 3-23.

When you click the Export button, you can save the snippet into a file and use it like other snippet files.

# Snippet Designer

This utility provides an even better experience than Export as Code Snippet. Although, as of writing, the utility is available only for Visual Studio 2008, the full source code is available, and it requires only small changes and recompilation to work with Visual Studio 2010.

You can start developing your snippets in two ways. The first is to use the File command and select Code Snippet File from the General category. The second is to select a piece of code while you are in the text editor, and use the “Export as Snippet” command from the context menu.

Independently of that, you can edit your .snippet file in a custom editor, as shown in Figure 3-24.

![](img/b5597c749e848b27b0d305153ae16106_102_0.png)

FIGURE 3-23: Add metadata to the code template

![](img/b5597c749e848b27b0d305153ae16106_102_1.png)

FIGURE 3-24: Plain code template

The code template you can edit here not provide any placeholders, but you can add easily with the context menu. Also, snippet metadata can be edited in the Properties window, as shown in Figure 3-25.

![](img/b5597c749e848b27b0d305153ae16106_103_0.png)

**FIGURE 3-25:** Code editing with Snippet Designer supports Basic, Visual C#, and XML snippets.

# Snippet Editor

The previous two utilities are integrated with Visual Studio to help in code snippet editing. Snippet Editor is an external tool running out of Visual Studio. The great benefit of this tool is that it simultaneously supports Visual Studio 2005, 2008, and 2010. It allows you to focus on editing a single snippet, it also allows you browsing the snippet library. Figure 3-26 shows this application in action.

![](img/b5597c749e848b27b0d305153ae16106_103_1.png)

**FIGURE 3-26:** Snippet Editor in Action

The drop-down box at the top of the pane allows you to select one of the Visual Studio versions installed on your machine. In the left pane of the screen, you can manage the library of your snippets. The tree view displays the languages as top-level folders, and under them, you can see the directory of snippets similar to what you can do with Code Snippets Manager. When double-click on a snippet, you can see its properties — including the code template — and you can immediately edit them.

The editor highlights the placeholders and allows the setting of their properties. In addition to being able to save the snippets, you can also export .vsl files and use them with the Visual Studio Community Content Installer to deploy the snippet.

If you intend to use this tool often, use the External Tools command to set up Snippet Editor so that it can be launched from the IDE.

# SUMMARY

Visual Studio snippets play important role in personal productivity. The concept behind them is simple and powerful. Snippets are source code pieces that range from one character to pages of text, and can be easily inserted into the code. The code to be inserted is defined with a template mechanism that allows placeholders and changing when the template is about to be applied.

Visual Studio 2010 supports code snippets for the HTML, JavaScript, Visual Basic, Visual C#, SQL, and XML languages. There are minor differences in features available, depending on the host language.

The IDE ships with a few hundred code snippets altogether, and you can easily add your own snippets to the directory. By creating an XML file with the .snippet extension following the predefined schema, and importing this with Code Snippets Manager, you can put your snippets in a few minutes.

In addition to Visual Studio, you can use community tools to create and manage snippets. Some of these tools are integrated with the IDE; some are external applications. Generally, they provide a better user experience than pure XML snippet file editing.

In Chapter 4, you will learn about the concept of Visual Studio templates. In addition to familiarizing you with using the built-in project and item templates, the chapter will teach you how to create your own templates and integrate them with Visual Studio.
