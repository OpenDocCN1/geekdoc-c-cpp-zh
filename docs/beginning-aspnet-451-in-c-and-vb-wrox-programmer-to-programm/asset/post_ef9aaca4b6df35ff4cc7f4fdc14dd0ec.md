
# Introduction to User Controls | 275

![](img/9e033e3b9560597824f8b22941d6d8bb_312_0.png)

FIGURE 8-1

This marks the file as a user control, the ASP.NET runtime knows how to deal with it. Other than that, the directive is similar to a standard ASPX page that doesn't use a master page.

With the user control open in the VS Window, you can use all the tools you have used in the previous chapters to create pages. You can use the Toolbox to drag controls into Markup and Design View, the CSS windows to change the look and feel of the user control, and the Properties Grid to change the properties of controls in your user controls. You can also write code that reacts to the events that the control raises.

To try out yourself, the next exercise shows how to create your first user control. In a later exercise, you will see how to use the control in ASPX pages in your site.

# TRY IT OUT Creating a User Control

In this exercise, you create a basic user control that displays a single vertical banner using an Image control. Later, exercises will see how to use this control in your pages and how to add another (horizontal)

For this exercise, you need two images that represent banners — one in portrait mode with dimensions of roughly 120 x 240 pixels, and one in landscape mode with a size of around 486 x 60 pixels. The Resources folder for this chapter's code download comes with this book has two images, but you could also create your own. Don't worry about the exact size of the images; as long as they are close to these dimensions, you should be fine.

- 1. Open the Planet W site in VS.
- 2. If you haven't already created, create a new folder called Controls in the root of the site. Although user controls can be placed anywhere in the site hierarchy, placing them in a separate folder makes them easier to find and manage.

- 3. Create another folder named Images at the root of the site.

- 4. Using File Explorer (Windows Explorer on Windows 7), open the Resources folder for this chapter (C:\BegASPNET\Resources\Chapter 08 if you followed the instructions in the introduction of this book). If you haven't done already, you can download the necessary resources from www.wrox.com. Drag (or copy and paste) the files Banner120x240.gif and Banner48x60.gif from File Explorer into the Images folder you created in Step 3. If you are using your images, drag them into the Images folder and give them the same names.

- 5. Right-click the Controls folder and click Add New Item. In the dialog box that follows, choose your programming language, click Web Control, and make sure that Place Code in Separate is checked, name the file Banner and then click Add to add it to the control to. Note how VS handles the extension of .ascx for all file types you add through the Add New Item dialog box so you don't need to type the extension yourself. Your Solution Explorer should now look like Figure 8-2.

![](img/9e033e3b9560597824f8b22941d6d8bb_313_0.png)

FIGURE 8-2

- 6. Switch your control to Design View and drag a Panel from the Standard category of the Toolbox onto the design. Use the ID of the Panel to VerticalPanel. The Properties Grid shows

- 7. From the Toolbox, drag an Image control into the Properties Grid. Select the Image and then click its ellipsis button, shown in Figure 8-3.

![](img/9e033e3b9560597824f8b22941d6d8bb_313_1.png)

Browse to the Images folder, select the Banner120x240.gif image, and click OK to add it to your control. Your Design now looks like Figure 8-4.

FIGURE 8-3

![](img/9e033e3b9560597824f8b22941d6d8bb_313_2.png)

FIGURE 8-4

- 8. Using the same Properties Grid, locate the AlternateText property and type This is a sample banner. Most browsers display the alternate text (rendered as a client-side alt attribute) when the image cannot be displayed. Some older browsers show the alternate text as the tooltip for when you hover your mouse over it.

- 9. Wrap the Image in a standard <a> element and set its href attribute to http://pzp.wrox.com. If you want to, you can use a code snippet to insert a link for the you. To do this, type the letter and then press Tab. Vs inserts a link and enables you to type in the href value directly. When you press Tab again, the content of the link is selected, you can delete by pressing Del (the Image will be the contents of the link). Finally, close the </a tag and move it after the image.

- 10. Set the target of the anchor <a> to blank to force the browser to open the page in a new window when the image is clicked. When you're, the code for the user control should look like the following code, for the Language attribute that you may have to VB and the AutoEventWire is False in VB.NET.

```xml
<@ Language="C#" AutoEventWire="true" CodeFile="Banner.ascx.cs"
<asp:Panel ID="Vertical" runat="server">
  <a href="http://pzp.wrox.com" target="blank">
  <asp:Image ID="Image" runat="server" AlternateText="This is a sample banner"
  ImageUrl="/Images/Banner120x240.gif" />
  </a>
</asp:Panel>
```

- 11. Save the changes by pressing Ctrl+S and close the user control by pressing Ctrl+F4.

# How It Works

The design experience of user controls in the Visual Studio IDE is identical to that of pages. You can use and drop; the Toolbox; the Markup, Split, and Design Views; and so on. This makes it easy to work with user controls because you can use all the familiar tools you use for development.

The control you just created displays a single image wrapped in an anchor element. In the next section, you will see how to add the control to the master page so it will be displayed in the Sidebar element of every page in the site. Later sections in this chapter show you how to add the other image that you can use to display a horizontal banner in individual pages.

# Adding User Controls to a Content Page or Master Page

To use a user control in a master page or in another user control, you need to perform two steps. First, you must register the control by adding an @ Register directive to the page or control where you want the user control to appear. The second step involves adding the tags for the user control to the page and optionally setting some attributes on it.

A typical @ Register for a user control looks like this:

```xml
<@ Src="ControlName.ascx" TagName="ControlName" TagPrefix="ucl" %>
```

The directive contains three important attributes, described in the following table:

| ATTRIBUTE | DESCRIPTION |
|---|---|
| Src | Points to the user control you want to use. To make it easier to move pages at a later stage, you can also use the tilde (-) syntax to point to the control from the application root |
| TagName | The name for the tag that is used in the control declaration. You're free to make this up, but usually it is the same as the name of the control. |
| TagPrefix | Holds the prefix of the TagName that is used in the control declaration. ASP.NET uses the prefix to refer to its controls, you need to provide a prefix for your controls. By default, this prefix is uc followed by a sequential number, but you can also change it to your liking. |

Consider the user control you created in the preceding exercise, your Register directive could look like this:

```xml
<@Register Src="/Controls/Banner.ascx" TagName="Banner" TagPrefix="uc" />
```

When the control is registered, you can add it to the page using the TagPrefix:TagName construct, similar to the way you add server controls to a page. Given the Register directive for the banner control, you will need the following markup to add to your page:

```xml
<uc:Banner ID="Banner1" runat="server" />
```

This is the minimum code needed for a user control in a page. Note that the control is defined by a combination of the TagPrefix and the TagName. The two attributes — ID and runat — are standard attributes that most controls in an ASP.NET page have.

Fortunately, in most cases, you don't have to type all this yourself. When you drag a user control from the Solution Explorer into the page Design View, VS adds the required code for you automatically. This exercise demonstrates how it works.

# TRY IT Adding the User Control to Your Page

In this exercise, you add the control Banner.ascx to the master page, so it displays a banner on each page in the site in the sidebar area.

- 1. Open up Frontend.master from the MasterPages folder and switch it into Design View.
- 2. Locate the drop-down list that enables you to select a theme, position your cursor right after the drop-down list, and press Enter three times to create some room.
- 3. From the Solution Explorer, drag the Banner.ascx file from the Controls folder into the empty spot you just created. Design View is updated and now looks like Figure 8-5.
