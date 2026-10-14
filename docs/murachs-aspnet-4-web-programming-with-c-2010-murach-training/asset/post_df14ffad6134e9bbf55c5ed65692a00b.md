
![](img/c024ccf88e28c30c07dd410d4342288f_72_0.png)

## The design of the Future Value form in Source view

### How to enter a title for the form
- Enter text between the *<title>* and *</title>* tags.

### How to change the HTML and text for the form
- Change the source code itself.

### How to change the property settings for a control
- To select a control, move the insertion point into the aspx tag for the control. Then, use the Properties window to change the property settings for the control. Or, you can modify the property settings in the source code itself.

### How to add a control
- Drag the control from the Toolbox to the location where you want it to appear.

### Description
- Design view presents a visual representation of the code that you see in Source view.
- The source code includes HTML tags and aspx tags. Before the form is sent to a browser, the aspx tags are converted to HTML because browsers can only use HTML.
- The properties you set for a control appear as *attributes* in the aspx tag for the control.
- We refer to the source code as *aspx code*, because the source files have aspx extensions.

attributes directly in the source code whenever the syntax is obvious. That’s often the fastest way to make an adjustment.

In addition to changing the properties of an existing control in Source view, you can add a new control. To do that, you just drag the control from the Toolbox and drop it in the location where you want it to appear. Then, you can set the control’s properties using standard techniques.

## How to use Split view to work with the design

In addition to Design view and Source view, you can work in Split view. Figure 2-12 shows how the Future Value form appears in Split view. When you use this view, you can see the aspx code for the form and the visual representation of that code at the same time. This is particularly helpful when you need to make minor adjustments to the appearance of a form. Then, you can check that the changes you make in Source view look the way you want them to without having to switch to Design view.

Note that when you make a change in Source view, the change isn’t automatically reflected in Design view. Instead, a bar is displayed at the top of the Design view window that indicates that the two views are out of sync. In this figure, this bar was displayed when I changed the text in the first cell of the table. To synchronize the two views, you can click on this bar or anywhere in the Design view window. In contrast, if you make a change in Design view, it’s reflected immediately in Source view.

![](img/c024ccf88e28c30c07dd410d4342288f_74_0.png)

## The design of the Future Value form in Split view

### Description
- You can use Split view to display a form in Source view and Design view at the same time. This eliminates the need to switch back and forth between these two views.
- By default, the designer window is split horizontally as shown above. Then, the top half of the window displays the form in Source view, and the bottom half of the window displays the form in Design view.
- You can also split the designer window vertically. To do that, use the Tools ▸ Option command to display the Options dialog box. Then, expand the HTML Designer node, select the General group, and check the Split Views Vertically option.
- If you make a change in Design view, it's reflected immediately in Source view. If you make a change in Source view, however, a bar is displayed at the top of the Design view window that indicates that Design view is out of sync with Source view. Then, you can click this bar or anywhere in the Design view window to synchronize the views.

Figure 2-12 How to use Split view to work with the design of a form

If you’ve used Visual Studio to do any C# coding, you may already be familiar with code snippets. You can use them in the Code Editor to enter common code patterns. With Visual Studio 2010, you can also use code snippets in the HTML editor to enter ASP.NET and HTML elements. In this topic, I’ll show you how to use code snippets to enter ASP.NET elements, but you can apply the same techniques to HTML elements.

Figure 2-13 shows you how to use code snippets. To start, you can right-click where you want the element inserted in the HTML Editor and select the Insert Snippet command from the shortcut menu. Then, to insert an ASP.NET element, you double-click the ASP.NET folder to display the snippets in that folder. Finally, you double-click the name of the snippet you want to insert.

At that point, the code snippet is inserted into the HTML Editor. In this figure, for example, you can see that a label control has been inserted into the code. Also notice that the value of the Text property is highlighted. Now, you just need to replace the value of this property and add any other properties you want applied to the label.

In most cases, it’s just as easy to add ASP.NET controls using the Toolbox as it is to use code snippets. That’s particularly true if you use the menus shown in this figure. If you like the idea of using code snippets, though, you should know that each one has a shortcut that you can use to insert it instead of using the menus. For example, the shortcut for the code snippet that creates a label control is just “label”. To insert this code snippet using its shortcut, you just enter the shortcut and press the Tab key.

If you use code snippets frequently, you should be aware that it’s possible to add or remove snippets from the default list. To do that, you can choose the Code Snippets Manager command from the Tools menu. Then, you can use the resulting dialog box to remove code snippets that you don’t use or to add new code snippets. Be aware, however, that writing a new code snippet requires creating an XML file that defines the code snippet. To learn how to do that, you can consult the documentation for Visual Studio.

![](img/c024ccf88e28c30c07dd410d4342288f_76_0.png)

## The list that's displayed for code snippets

![](img/c024ccf88e28c30c07dd410d4342288f_76_1.png)

## The list that's displayed for ASP.NET code snippets

![](img/c024ccf88e28c30c07dd410d4342288f_76_2.png)

## The snippet that's inserted for the label control

### Description
- To insert a code snippet, right-click in the HTML Editor and select the Insert Snippet command from the resulting menu. Then, double-click the type of snippet you want to insert from the list that's displayed. Finally, double-click the snippet or highlight it and press the Tab or Enter key.
- Once a snippet has been inserted into your code, you can replace the highlighted property values with your own values and add any other required properties. To move from one highlighted value to the next, you can press the Tab key.
- You can use the Tools → Code Snippets Manager command to display a dialog box that you can use to edit the list of available code snippets and to add custom code snippets. This dialog box also lists shortcuts that you can use to insert a snippet.
- To insert a snippet using a shortcut, enter the shortcut and then press the Tab key.

## The aspx code for the Future Value form

Figure 2-14 presents the aspx code for the Future Value form that has been developed thus far (except for the Page and DocType directives, which you’ll learn more about in chapter 5). For now, though, please note that the code for the title that’s displayed in the web browser is between the <head> tags, along with the code for the style classes that are used by the form, and the code for the form design is between the <div> tags.

Within the <div> tags, I’ve highlighted the code for the HTML image control and the code for the six web server controls. If you study this code, you can see how the properties are set for each of these controls. For instance, you can see that I set the Width properties of the button controls to 100 pixels so they are both the same width. You can also see that I set the width of the drop-down list to 106 pixels, even though it appears to be the same width as the text boxes, which are 100 pixels wide. My point is that the sizing properties in the aspx code aren’t always consistent, so you often have to fiddle with these properties to get the design the way you want it.

Before I go on, I want to point out that when you drag an image from the Solution Explorer, an Accessibility Properties dialog box is displayed that lets you set two properties for the HTML image control. First, it lets you set the Alternate Text property (Alt), which specifies the text that’s displayed if for some reason the image can’t be displayed. Because the version of HTML that Visual Studio 2010 uses requires this property, you’ll want to be sure to enter a value for it.

Second, it lets you specify the Long Description property (LongDesc), which provides a *Uniform Resource Indicator* (URI) to a more extensive description of the image. A URI can be the address of a web page (a URL) or a name that identifies a resource or a unit of information (a URN, or *Uniform Resource Name*). The Long Description property isn’t required, and in most cases you’ll leave it blank.
