
- 3. **Highlight the code** between your style tags and press Ctrl+C if you're on Windows or ⌘-C if you're on Mac to copy the code.

```css
body {
  font-family: "Open Sans", sans-serif;
  background-color: #F88008;
}
header {
  background-color: #FFB000;
}
footer {
  background-color: #0000FF;
}
div {
  background-color: #FFFFFF;
}
.left {
  width: 75%;
  float: left;
  background-color: #FFFFFF;
}
.right {
  width: 25%;
  float: left;
  background-color: #000000;
  color: #FFFFFF;
}
```

- 4. Open your style.css file and click into the file editor. Click Ctrl+V if you're on Windows and ⌘-V if you're on Mac to paste in your style code.

```css
body {
  font-family: "Open Sans", sans-serif;
  background-color: #F88008;
}
header {
  background-color: #FFB000;
}
footer {
  background-color: #0000FF;
}
div {
  background-color: #FFFFFF;
}
.left {
  width: 75%;
  float: left;
  background-color: #FFFFFF;
}
.right {
  width: 25%;
  float: left;
  background-color: #000000;
  color: #FFFFFF;
}
```

![](img/b129720fc9ac9e14546b8756740d362a_107_0.png)

The way your code is written in your file really matters because it helps you understand what code is where. HTML and CSS Editey make this easy! Just click the Format Source Code button and your code will move so that it is easier to read!

```css
body {
    font-family: Ubuntu, Sans, sans-serif;
    background-color: #f0f0f0;
}
header {
    background-color: #ff0000;
}
footer {
    background-color: #0000ff;
}
div {
    background-color: #ffffff;
}
.left {
    width: 75%;
    float: left;
    background-color: #ffffff;
}
.right {
    width: 25%;
    float: right;
    background-color: #000000;
    color: #ffffff;
}
```

### LINK YOUR CSS FILE TO YOUR HTML FILE

Now that your style code is in its own file, you need to tell your HTML file where it can find the style code.

![](img/b129720fc9ac9e14546b8756740d362a_107_1.png)

> This is going to be a little strange. You have to get the URL exactly right for it to work properly, so do this part slowly and ask an adult for help if you need it.

- 1. Open your index.html file and write the code to link your CSS file between the two `<head>` `</head>` tags.

```html
<link rel="stylesheet" type="text/css" href="http://editey.com/preview/ID_NUMBER/style.css">
```

```html
<!DOCTYPE html>
<html>
<head>
<link rel="stylesheet" type="text/css" href="http://editey.com/preview/ID_NUMBER/style.css">
</head>
```

Everything you type should be exactly as it is in the code just above this paragraph. Don't add any spaces and don't get rid of any, and make sure everything is capitalized the same. The code is supposed to be all on one line, but as you see in the figure, depending on how wide your window is, the line of code can be split. That's okay! Just make sure that when you type it in, you never press Enter — you just type it in all at one time.

![](img/b129720fc9ac9e14546b8756740d362a_108_0.png)

- 2. You need to replace ID_NUMBER with the actual ID number of your style.css file. Open your style.css file and look at the URL from the address bar. The format is css.editey.com/file/ID_NUMBER/FILE_NUMBER.

```css
body {
    font-family: 'Open Sans', sans-serif;
}
```

- 3. Highlight the ID_NUMBER and press Ctrl+C if you're on Windows, ⌘-C if you're on Mac, to copy it.

```css
body {
    font-family: 'Open Sans', sans-serif;
    background-color: #F8F8F8;
}
h1 {
```

## PROJECT 6 MAKE YOUR WEB SITE LOOK GREAT

- 4. Open your `index.html` file and **highlight the ID_NUMBER** from Step 1.

![](img/b129720fc9ac9e14546b8756740d362a_109_0.png)

- 5. Press Ctrl+V if you’re on Windows, ⌘-V if you’re on Mac, to **paste the ID number** in the URL.

![](img/b129720fc9ac9e14546b8756740d362a_109_1.png)

- 6. Copy the entire `<link` line of code and **paste it** into the other three html files that you made in your previous project.

![](img/b129720fc9ac9e14546b8756740d362a_109_2.png)

![](img/b129720fc9ac9e14546b8756740d362a_110_0.png)

To open each HTML file, go to http://drive.google.com, open your project folder, right-click the file you want to open, and choose HTML Editey.

![](img/b129720fc9ac9e14546b8756740d362a_110_1.png)

You should delete the style tags in all the HTML files. You need only the link tag now.

### TEST YOUR CHANGES

Wow! You just made a lot of changes that could potentially hurt your web site. Before moving on, you should test to make sure everything still works.

- 1. Go to http://drive.google.com and open your project folder.

- 2. Right-click **index.html**, go to **Open With**, and click **HTML Viewer**.

![](img/b129720fc9ac9e14546b8756740d362a_110_2.png)

- 3. If your style isn’t showing up, click the **Refresh** button.

![](img/b129720fc9ac9e14546b8756740d362a_110_3.png)

After all that work, your web site should look the same as it did at the end of the Project 5. Now you are ready to make changes to make it look better, and it will be much easier to make those changes!

![](img/b129720fc9ac9e14546b8756740d362a_111_0.png)

> *When you test your web site, make sure to click all the buttons on your web site to make sure they all still work. Just because something looks right doesn't mean it is acting right!*

### STYLING YOUR WEB SITE

Now that you have a style.css file, you can update the style of your web site quickly! Before you add more content, you should fix the style.

### DECIDE WHERE TO PUT THE BACKGROUND COLORS

You can decide where to put the different colors yourself, but one way to help you decide is to look up other web sites with similar colors.

> *You should always ask an adult's permission before looking anything up on the Internet.*

If you're following the example in this book using orange and blue, you might change your header and footer to be orange, your left and right class to be blue, and your body to be white. The background color attribute (the name of the color for your background) is background-color.

```css
body {
    font-family: 'Open Sans', sans-serif;
    background-color: #ffffff;
}

header {
    background-color: #ff8800;
}

footer {
    background-color: #ff8800;
}

div {
    background-color: #ffffff;
}

.left {
    width: 75%;
    float: left;
    background-color: #0000ff;
}

.right {
    width: 25%;
    float: left;
    background-color: #0000ff;
    color: #ffffff;
}
```

### CHANGE THE FONT COLOR

Now that you have your background colors how you want them, change the text so that it's easy to read.

- 1. You might have to play around with the different colors. For the example of using orange and blue, the text in the body looks best as white. The font color attribute (the name of the color for your text) is color.

```css
body {
    font-family: 'Open Sans', sans-serif;
    background-color: #ffffff;
    color: #ffffff;
}
```

- 2. For an orange background, or other colors like orange, the white text doesn't look as good. If the white text doesn't look good on one of your colors, change the text to be a different color. For example, on an orange background, you would change the color of the text in your footer to be black (`color: #000000`).

![](img/b129720fc9ac9e14546b8756740d362a_113_0.png)

### FORMAT YOUR PAGE

You can do a few simple things to make your web site look even better! Follow these steps to format your page.

- 1. Center the text of the footer. To move the text to the left, right, or center, you use the `text-align` attribute. This is a good idea for any web site.

```css
footer {
    background-color: #ff8000;
    color: #000000;
    text-align: center;
}
```

![](img/b129720fc9ac9e14546b8756740d362a_113_1.png)

## 数字图像处理与分析

### 图像分割（1）

### 阈值化分割

阈值化分割作为最经典的图像分割方法，其基本思想是确定一个阈值，然后根据该阈值将图像中的每个像素划分为目标或背景。阈值化分割方法计算简单、效率高，在图像分割领域占有重要地位。

### 阈值化分割的基本原理

阈值化分割的基本原理是依据一定的准则，将图像的灰度值划分为不同的集合。对于一幅灰度图像 f(x, y)，若选择一个阈值 T，则分割后的图像 g(x, y) 可表示为：

```text
g(x, y) = 1,  f(x, y) > T
           = 0,  f(x, y) ≤ T
```

其中，f(x, y) 为输入图像，g(x, y) 为输出二值图像，T 为阈值。阈值 T 的选择是阈值化分割的关键，通常可以表示为：

```text
T = T[x, y, p(x, y), f(x, y)]
```
