# 678 Styling Your Controls

![](bbox=[0.239, 0.125, 0.435, 0.483])

Figure 3-7: Styles in the Properties panel.

# # Binding styles with CSS

Because we in a Web application, using Cascading Style Sheets (CSS) seems like a good approach to handle our styles. Nearly every control in ASP.NET has a property — CSSClass — that takes advantage of the styles loaded as part of the project.

To started, you need a few CSS classes, which are not the same as .NET classes. A CSS is a collection of styles that can be connected to a collection of markup, so as to match the properties that can be matched between. To bind styles with CSS, follow these steps:

+   1. Right-click the project and select Add New.

+   2. Select Style Sheet from the dialog box.

I named Chapter3.css.

+   3. When the style sheet comes up, right-click the CSS Outline and select Add Style Rule.

+   4. In the element dialog box, select Class Name and type GridViews in the text box.

+   5. Click the right arrow button as shown in Figure 3-8.

+   6. Press OK, and notice the new entry in the style sheet.