# Exercise 4 Solution

To change the property of a control on a page, you can click the control in Design or Markup View and then use the Properties Grid (which you can bring up by pressing F4) to change the value of the property. Alternatively, you can change the property directly in Markup View.

# CHAPTER 2

# Exercise 1 Solution

A number of files fall in the Web Files category, including .aspx files (Web Forms that end up as pages in the web browser), .html files (that contain static HTML for your site), .css files (that contain cascading style sheet information), and .config files (that contain configuration information for the website). Refer to the table with the different file types in Chapter 2 for a complete list of files.

# Exercise 2 Solution

When you want to make a piece of text both bold and italicized, you need to select the text and then click the Bold button on the Formatting toolbar. Next you need to click the Italic button. The final HTML code in the page should look like this:

```
<strong><em>Welcome to Planet Wrox</em></strong>
```

You may also come across <b> and <i> elements, which have the same effect. However, these are now considered outdated and you're encouraged to use <strong> and <em> instead.

# Exercise 3 Solution

The first way is using the Solution Explorer. Right-click your site, choose Add Existing Item, and then browse for the item(s) you want to add.

Secondly, you can drag and drop files from File Explorer or Windows Explorer or from your desktop directly into a VS website. As a third alternative, you could put the files directly in the site’s folder using Windows Explorer. For example, files you add to the folder C:\BegASPNET\Site become part of your website automatically. If you don’t see the new files appear in VS directly, click the Refresh icon on the Solution Explorer toolbar.

# Exercise 4 Solution

In VS, you have three different views on your code: Design View, Markup View (also referred to as Source View or Code View), and Split View. The first gives you an impression of how your web page is going to look in the browser, and the second view shows you the raw markup. Split View enables you to see both views at the same time. VS also has different views for other files. For example, programming code for an ASPX page is generally referred to as the Code Behind view or simply the Code Behind. The new HTML editor (which you cannot use for Web Forms) only has a Markup View.