# # <ADD A STYLESHEET>

We're now going to change how the page looks. To do this we're going to create a **stylesheet**. A stylesheet tells you how the web page should look. Should the background be white or blue or green? Should the text be large or small? Should the links change color when you roll the mouse over them?

The stylesheet is the place where you keep all this information. The stylesheet is kept separate from the .html file so that you can change the web page's color scheme without having to change the HTML code of the page itself.

+   1. The stylesheet we'll be creating will be in a new file called **my-first-stylesheet.css**. Notice that the file extension of the stylesheet is **.css**, not **.html**. (Stylesheets in this book will be orange, so that you can tell the difference at a glance.) To keep things neat, we'll save our stylesheet in its own folder. We'll name this folder **css** and create it inside the **nanonauts** folder.
+   2. Type in the code from the orange box and save it as **my-first-stylesheet.css** in the **css** folder.
+   3. To link the stylesheet to the web page, you need to add an extra line into your HTML – it's highlighted in the code below.

![](bbox=[0.5, 0.24, 0.96, 0.49])

```
```css
body {
font-family: sans-serif;
}
```
```

+   4. What this line does is link the web page to the stylesheet called **my-first-stylesheet.css**

This stylesheet is kept in the **css** folder. (That's what the line of code **css/my-first-stylesheet.css** refers to!) In other words, the stylesheet you've just created.

```
```html
<!DOCTYPE html>
<html>
<head>
<title>About Us</title>
<link type="text/css" rel="stylesheet"
href="css/my-first-stylesheet.css"/>
</head>
<body>
<h1>About Us</h1>
<p>We are the Nanonauts.</p>
<p>Our names are Holly, Dervla, Daniel, and Sam.</p>
</body>
</html>
```
```

To see the difference the stylesheet makes to the web page, you must reload the page. To reload the page, click on the Reload symbol in the toolbar.

![](bbox=[0.837, 0.84, 0.949, 0.946])