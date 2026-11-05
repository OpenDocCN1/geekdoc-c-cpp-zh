
Figure 15-7 shows most of the `Site.master` file. You will notice it contains formatting HTML tags. A master page can include static text, HTML elements, and server controls. If you look at the `Site.master` file in Figure 15-7, you will find `html`, `head`, `body`, `form`, and `div` elements on the page. There are a few subtle differences between a master page and other pages, like the `Default.aspx` page. First, it has a special `@ Master` directive instead of the `@ Page` directive.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1033_0.png)

**FIGURE 15-7** Site.master Master page

Master pages actually consist of two pieces: the master page itself and one or more content pages. Individual content pages contain the content you want to display in the context of the master page template. When users request the content pages, the master page is merged with the content page to produce output that combines the layout of the master page with the new material from the content page. The content pages associated with the master page for the DynamicPage example are `About.aspx` and `Default.aspx`.

The other major difference between a master page and content pages like `Default.aspx` and `About.aspx` is that the master page has one or more `ContentPlaceHolders` defined with an ID. These placeholders define areas where replaceable content will appear. With areas collapsed, the `HeadContent`, `FeaturedContent`, and `MainContent` `ContentPlaceHolders` are shown on Lines 14, 75, and 77 in Figure 15-7. Figures 15-8 and 15-9 show the replaceable content for the About.aspx and Default.aspx pages. Figure 15-8 shows both the Source and Design windows for the About.aspx page.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1034_0.png)

**FIGURE 15-8** MainContent in the About.aspx page

Lines 4 through 32 provide the content for the MainContent ContentPlaceHolder shown in Figure 15-8 for the About page. The static text "Your app description page." and "Use this area to provide additional information." are the content used to fill the white area (MainContent) on the page. As you review Figure 15-9, notice the content for MainContent is defined on lines 21 through 41 for the Default.aspx page.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1035_0.png)

**FIGURE 15-9** MainContent in the Default.aspx page

Here, in Figure 15-9, in addition to the static text "We suggest the following:", three dynamic links were included in the MainContent ContentPlaceHolder area. For the content pages shown in Figures 15-8 and 15-9, the line begins with `<asp:Content>`; this is what ties the element back to the Site.master page.

> **NOTE** As you review the DynamicPage Web application, you will discover additional content pages under the Account node. Login.aspx and Register.aspx are both associated with the Site.master master page. No changes were made to the DynamicPage Web application.

As you closely review Figures 15-7 through 15-9, you will notice that there is a node named Content folder shown in the Solution Explorer window. It is expanded to reveal a file named Site.css. This is a style sheet. The file is automatically added to the project when a Visual Studio Web site is created.

## Cascading Style Sheet (CSS)

Visual Studio provides support for incorporating **Cascading Style Sheets (CSS)** into ASP.NET Web applications. CSS, like master pages, enable you to provide more consistency across pages on your Web site. They let you separate the actual content from how it is going to look. Before CSS, all of the presentational attributes, like sizes and colors of fonts and alignment of text were all included within the HTML markup. You often repeated the properties and had to work at providing consistent presentation of elements.

CSS uses style sheets to describe how elements will look in terms of their layout, fonts, and colors. Style sheets enhance your ability to improve the appearance of pages. Most developers feel that style sheets represent a major breakthrough for Web page designers because of the added ability to improve the appearance of pages. There is a whole new language for style sheets used to define how an HTML document will look.

The syntax for the language used by CSS is very high level—close to English. CSS uses a number of keywords to describe different style properties. It is beyond the scope of this chapter to describe all of the different properties; however, as you review Figure 15-10 you will find the style sheet very readable and easy to modify.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1036_0.png)

**FIGURE 15-10** Site.css

From the **Solution Explorer** window, the Site.css file is opened. Shown on the left in Figure 15-10 is one of the special tools in Visual Studio that shows an outline of the **Style Sheet Elements** and **Classes**. When you select one of the items in the **CSS Outline** window, the item is selected in the center window.

> **NOTE:** If you close the **CSS Outline** window, it can be reopened from the **VIEW** menu by selecting **Synchronize Document Outline**.

By definition a **style sheet** includes a list of rules. Each rule consists of a selector and one or more declaration blocks. The declaration block is enclosed in curly braces. Inside the block you will find a property, colon, and a value. Like C#, each property assignment ends with a semicolon. Example 15-2 shows the style rule for body that was included when the **DynamicPage** Web site was created.

**Example 15-2**

```css
body
{
    background-color: #fff;
    border-top: solid 10px #000;
    color: #333;
    font-size: .85em;
    font-family: "Segoe UI", Verdana, Helvetica, Sans-Serif;
    margin: 0;
    padding: 0;
}
```

You can go directly into the Site.css file and type new values or add additional property lines. Another option, a better option, is to use the **Modify Style** configuration wizard. As you look back at Figure 15-10, you will notice that the **Properties** window has a single entry, Style. It does not matter which of the elements or classes you select, there is always just that one property. You can select an element using the **Outline** window or from the actual .css file in the center window. Both ways will reveal the property for the item you select. When you click the ellipsis for the **Style** value, the **Modify Style** dialog box shown in Figure 15-11 is revealed.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1038_0.png)

**FIGURE 15-11** Modify Style

Each of the Category items shown in Figure 15-11, the Modify Style dialog box, reveals a number of options you can set for the element. Selections you make are added as new style rules. You are encouraged to explore by making changes and then reviewing the .css file and the output you get from your changes when you launch the site. No changes were made to the DynamicPage Web site example.

As you review Figures 15-7, 15-8, and 15-9, notice that all three files have a CodeFile page directive attribute, indicating that there is an associated code-behind file. If you expand any of the .aspx files, like Default.aspx, in the Solution Explorer window, you will find the code-behind files. They all have .cs appended onto the end of their filenames.

## CODE-BEHIND FILE

You can open the .aspx.cs file from the Solution Explorer window. At first glance, the .aspx.cs code-behind file looks very similar to a Windows application. However, there are a number of differences, as shown in Figure 15-12.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1039_0.png)

**FIGURE 15-12** Code-behind file

As you examine Figure 15-12, notice that there is no Main() method. Instead there is a Page_Load() event handler. It is added automatically when the project is created. The code generated by the Web Forms Designer is no longer included. A significant difference exists between an ASP.NET Web Forms and Windows application in that the autogenerated code is not created for ASP.NET applications until you run the application. Notice the heading for the class declaration in Figure 15-12 includes the partial keyword. You saw that with Windows applications. The autogenerated code was placed in another partial class. Recall with Windows applications, the Windows-generated code included object instantiations for the visual controls that were placed on the form and event-handler hookups. These were placed in the .Designer.cs file. Unlike Windows applications, one of the differences you'll observe when you explore the Solution Explorer window for ASP.NET applications is that there is no .Designer.cs file listed. Note the many namespaces imported automatically when the ASP.NET Web Forms Site template is selected.

As you saw from the previous example, when you create a Web site using the ASP.NET Web Forms Site template in Visual Studio, a number of files including a master page, style sheet, and content pages for Default, About, and Login are automatically
