# CHAPTER 6 CREATING CONSISTENT LOOKING WEBSITES

```
<title>Welcome to Planet Wrox</title>
<script src="Scripts/modernizr-2.7.1.js"></script>
<link href="App.Themes/Monochrome/Monochrome.css"
type="css" rel="stylesheet" />
</head>
<body>
```

Note that a link to the style sheet from the Monochrome folder is injected in the <head> of the page. ASP.NET run does this for every CSS file it includes in the currently active folder (in alphabetical order), so be sure to keep your theme folder to avoid unnecessary files from being included and downloaded by the browser. Also notice how the <link> is added just right after the <head-tag>. This ensures that the file is included after all other files you have added (through the master page, for example). This is in contrast to how the StyleSheet attribute. This type of theme allows its settings to be overridden, it's imported from the top of the file, giving room for other CSS files it follows to change the look and feel of the page.

+   7. Return to Visual Studio and open the master page in Design View. Notice how all the design is gone and now follows the layout of the page. Unfortunately, VS does not display the theme you've using the theme attribute. However, you can overcome this by setting the StyleSheetTheme attribute. To do this, open the Web.config file, locate the <pages> element you created earlier, and add the following attribute:

<pages theme="Monochrome" StyleSheetTheme="Monochrome" />

+   8. Save the changes to Web.config, reopen the master page, and switch to Design View. You'll see that VS now applies the correct information to your pages.

+   9. To add another theme to the site, create a new folder under App_Themes and call it DarkGrey. Now, open the folder where you extracted the downloaded code that comes with this book. If you followed the instructions in this book, your folder is located at C:\ASPNET\Resources. If you don't have these files, they are available at www.wrox.com/go/aspnet-451. Open the chapter 06 and the theme folder, and drag the DarkGrey folder from File Explorer into the DarkGrey theme folder in VS. If dragging doesn't work for you, then use Ctrl+C in File Explorer to copy the file, and then use Ctrl+V in VS to paste the file in your project. Your Solution Explorer should now reveal Figure 6-15.

You add images that the CSS file refers to in a later entry.

+   10. Open the Web.config file once more and change others of Monochrome to DarkGrey in the <pages> element. Save the changes again and press Ctrl+F5. Instead of the blue Monochrome, you'll see the site with the DarkGrey theme applied as is visible in Figure 6-16. If you don't see the place holder, the main content, and the sidebar next to each other, make sure your browser is wide enough to display all content.

![](bbox=[0.655, 0.515, 0.865, 0.77])

FIGURE 6-15