
# Mastering Master Pages 729

- I add a Bits folder, and in that, I put folders for well, and all the bits.
- Style sheets
- Images
- JavaScript files
- Whatever else

- I then make a root folder for every section of the site. If I have three top-level-level menu items in my site, I have three folders. If I just have application files and don't have a regular menu structure, everything will be in the root.

## Mastering Master Pages

Now that there is some form and function to the project, the next step is to add some form and function to the site. Master pages are exactly what they sound: structural elements that contain the content of the site as "slave" components.

Master pages are more than page templates. They are fully functional content containers that are supported by Visual Studio in a number of ways. Master pages reduce the complexity of maintaining common content on web pages by replicating content automatically and containing the programming to one file from the developer's.

There is no requirement to use master pages. In fact, most of the projects I work on do not use Master Pages, because of dependencies on older security or navigational frameworks. That's okay. If you're building something new, certainly consider using master pages.

## Making a master page

Start by making a new master page. Just follow these steps:

1. Right-click the Chapter5 website and select Add New Item.
2. Click Master Page.
3. Keep the default name of MasterPage.Master and click Add.
4. Change to Design view.
5. Open the Properties panel.
6. Click the designer, outside of the Body marked area, so that the DOCUMENT is selected in the Properties panel.
7. Change the foreground color in the style property to read color:#333333.
8. Back in the designer, click the Body marked area and type My Website or something equally fascinating.
9. Highlight the text and select H1 in the HTML Source Editing Toolbar, like I did in Figure 5-4: click the box on the toolbar that says Paragraph.
10. Press Enter to add a blank line under the header.
11. From the Toolbox, draw a ContentPlaceholder control under the title.

Now you have a template for the rest of your pages. You can add navigation here, and I recommend it. To keep things simple for this introduction, however, move on.

![](img/6df7bb88e9302e98442acc219cfbd7fc_755_0.png)

Figure 5-4: Making a header.

## Adding content

You won't believe how simple adding content is. You see, the master page is something that the content page adheres to, not nothing you have to inject content into it. You just have to make pages like usual, and they will drop themselves in content placeholder. Follow these steps to add content:

1. Right-click the website and select Add New Item.
2. Click Web Form (the master page is probably still selected) and name it Home.aspx.
Wait! Don't click Add yet!
3. Check the Select Master Page check box in the lower right-hand corner.
4. Now you can click Add.

The Select a Master Page dialog box appears.

5. You can select which master page you want — as shown in Figure 5-4. We have only one, so click it under Contents of Folder.
6. Click OK.

Notice how different the template of the page is now that you have a master page. Visual Studio knows how to handle this! There are no HTML headers or footers, unlike VS when they are in the master.

```xml
<asp:Content Title="Content" MasterPage="/MasterPage.master" AutoEventWireup="true" CodeFile="Home.aspx" Inherits="Home#Server">
  <asp:Content ContentId="Content1" ContentHolderId="head" Runat="Server">
  </asp:Content>
  <asp:Content ContentId="Content2" ContentHolderId="ContentHolder1" Runat="Server">

  </asp:Content>
</asp:Content>
```

There is obviously more to learn about master pages and how to develop sites with them, but my main goal is to cover the best practice. Now that you know, move to MSDN and see how best to use master pages for your project.

## Testing Web Applications with Visual Studio

It's easy to test web applications using Visual Studio, though it isn't a well-advertised feature.

This is available only in Team System. If you have Professional, you can't do web tests. Also important.

4. Now you can click Add.

The Select a Master Page dialog box appears.

5. You can select which master page you want — as shown in Figure 5-4. We have only one, so click it under Contents of Folder.
6. Click OK.

Notice how different the template of the page is now that you have a master page. Visual Studio knows how to handle this! There are no HTML headers or footers, unlike VS when they are in the master.

(Wait, the OCR text seems to repeat/scramble here. I will follow the logical flow of the provided snippets.)

## Testing Web Applications with Visual Studio

It's easy to test web applications using Visual Studio, though it isn't a well-advertised feature.

This is available only in Team System. If you have Professional, you can't do web tests. Also important.

(Note: The source text contains significant noise/repetition in the latter half of page 755+. I will clean the coherent logical parts based on the provided text.)

- Dot Net Nuke, an open source content management system for ASP.NET, has taken things to extreme. When you build a new module for the, you add the script files.

...

