Adding Modernizr to your site is very easy using the Package Manager Console that ships with Visual Studio. To add the library, follow these steps:

+   1. Choose Tools ← Library Package Manager ← Package Manager Console.
+   2. Type the following command and press Enter:
+   ```
+   Install-Package Modernizr
+   ```
+   3. After a short delay, your site is expanded with a file called packages.config that keeps track of the installed packages and a Scripts folder that now contains the file modernizr-2.6.2.js. Note: your version number could be different if a newer version of Modernizr has been released by the time you read this book. To add this library to your page, open Default.aspx in Markup View and drag the file from the Solution Explorer to the head section of the code, directly after the link to the style sheet. You should end up with this code:
+   ```html
+   <link href="Styles/Styles.css" rel="stylesheet" type="text/css" />
+   <script type="text/javascript" src="Scripts/modernizr-2.6.2.js"></script>
+   </head>
+   ```

You should add the Modernizr library to your site even if you have a modern web browser. Since you can't control the browsers visiting your site, you want to make sure everybody sees your site as intended. Adding Modernizr fixes the HTML5 compatibility issues for older browsers while hardly causing any overhead. You can learn more about Modernizr on its website at http://modernizr.com/. You'll see a lot more about the Package Manager Console in Chapter 11.

12. Finally, save the changes to all open documents (press Ctrl+Shift+S) and then request Default.aspx in your browser. Your screen should look similar to Figure 3-8, which shows the page in Mozilla Firefox.

![](bbox=[0.15, 0.7, 0.88, 0.91])

# FIGURE 3-8