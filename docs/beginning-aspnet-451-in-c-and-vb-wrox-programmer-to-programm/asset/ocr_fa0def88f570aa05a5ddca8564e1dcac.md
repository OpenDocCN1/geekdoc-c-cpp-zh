# Extending Themes

In addition to CSS files and skins (discussed toward the end of this chapter), a theme can also contain images. The most common use of theme images is referring to them from your CSS. To put to good this it's important to understand how CSS refers to images.

By design, an image referred to by a CSS selector will be searched relative to the location of the CSS file, unless you give it a path that starts with a forward slash (/) to indicate the root of the site. For example, the App_Themes folder depicted in Figure 6-17.

To refer to the MenuBackground.jpg file in the Images folder of the Monochrome theme, you can add the following CSS to Monochrome.css:

```
nav {
  background-image: url(Images/MenuBackground.jpg);
}
```

If you wanted to refer to an image in the Images folder of the root of the site, you would use this CSS:
background-image: url(/Images/MenuBackground.jpg);

Note the forward slash in front of the image path to indicate the root of the site. This latter syntax is useful if you want to share images between different themes. Simply put them in a folder outside a specific theme, like an Images folder at the root, and then use root-based syntax to refer to them. The next chapter digs lot deeper into the forms a URL can take to refer to a resource like an image.

![](bbox=[0.666, 0.066, 0.873, 0.335])

# TRY IT OUT Adding Images to Your Theme

In this Try It Out you add the images and CSS files to the theme to complete them. You overwrite the file Monochrome.css in the Monochrome theme, so if you made any customizations you would like to keep, create a backup of it first.

+   1. Open File Explorer and navigate to the files extracted from the zip file for this chapter (at C:\BegASNET\Resources). Open the Chapter 06 folder and then the Monochrome folder. Select the Images folder and copy the Monochrome.css file.
2. Drag (or copy and paste) the selected folder and files from File Explorer into the Monochrome theme folder in VS. Click Yes when you're ready to overwrite Monochrome.css.
3. Repeat steps 1 and 2, but then drag (copy and paste) only the Images folder from the File Explorer's DarkGrey folder into the DarkGrey theme folder in VS. Your Solution now looks like Figure 6-17.
4. Open up the master page from the MasterPages folder, and remove the text Header Goes Here from the <header> element. Make sure you don't accidentally remove the <a> element, which should not be empty.