
![](img/b129720fc9ac9e14546b8756740d362a_75_0.png)

Right now, you will just have placeholder text. That means that you won't write the actual text yet; you're just trying to make sure you know where everything will go.

```html
1  <html>
2  <body>
3  <p>
4  Logo
5  <p>
6  Menu Item
7  <p>
8  Featured Dinosaur
9  <p>
10 Text about my Dinosaur right here
11 <p>
12 Footer Down Here
13 </html>

Logo and Menu up here
Text about my Dinosaur right here
Footer Down Here
```

## ADDING MORE STRUCTURE TO YOUR WEB SITE

Adding text to your web site is good, but you might want to add a little more structure to your web site, too. For example, in the wireframe example from Project 3, there was a sidebar.

![](img/b129720fc9ac9e14546b8756740d362a_76_0.png)

To add a different part of your web site, like a sidebar, you have to create new sections inside the body tags called “divs.” The first div will go to the left and take up most of the screen, and the second div will go to the right and take up only a little of the screen. To create new divs, you use the open and close div tags: `<div> </div>`. Even if you do not want these divs to be next to each other, you might want to have different divs with different colors or content.

Look through your wireframe from Project 3 and **put the text** (or placeholder text) in the correct places. For example, in the web site in this book, the text about dinosaurs is on the left of the web site. The first div that was made in this example will be the one on the left, so that’s why the dinosaur text is in the first div.

```html
<html>

<head>
<title>
Chicken
</title>
<body>
<h1>Chicken and Hen: up here</h1>
<h2>Chicken and Hen: up here</h2>
<h3>Chicken and Hen: up here</h3>
<hr>
<p>Text about my Dinosaur right here.</p>
<hr>
<p>Text about my Dinosaur right here.</p>
<ul>
<li>Eggs</li>
<li>Milk</li>
<li>Bread</li>
</ul>

</body>
</html>
```

## ADD STYLE ATTRIBUTES TO YOUR WEB SITE

Next, you will add attributes to your div sections to change the color of them, making them easier to see them. Attributes can be a lot of different things in web sites. They can be colors, size, or even the font style!

Look carefully through the code and add the following bits (see the next figure).

![](img/b129720fc9ac9e14546b8756740d362a_77_0.png)

> You have to type everything in code exactly as it is in the book. If you capitalize something that shouldn't be capitalized, or add a space where there shouldn't be a space, your web site won't work. This is because computers, even though they are powerful, aren't that smart! So they don't know that the name Sarah is the same as sarah. To a computer, those two names are different because one has a capital S and the other has a lowercase s.

The head part of your web site is where you put your style code. You might want to refer to your style guide from Project 4 for this part. The example in this book uses orange, blue, and yellow for the colors and sans serif for the font, so that's what is shown here.

- 1. Between the head tags, add an open and close style tag.

```html
<html>
<head>
  <style>
  </style>
</head>
<body>
  <header>Logo and Menu up here</header>
  <p>Text about my Dinosaurs right here.</p>
  <footer>Footer Down Here</footer>
</body>
</html>
```

- 2. Between the style tags, add a section called body. This section, instead of having the less-than and greater-than tags, will have open and close curly braces. Everything inside the body section will change what is in the body part in your code below.

```html
<html>
<head>
  <style>
    body {
    }
  </style>
</head>
<body>
  <header>Logo and Menu up here</header>
  <p>Text about my Dinosaurs right here.</p>
  <footer>Footer Down Here</footer>
</body>
</html>
```

- 3. Add the following line exactly as it is written. When you finish typing it, your font will change!

```css
body {
  font-family: "Open Sans", sans-serif;
}
```

- 4. **Add the following line** exactly as it is written. When you finish typing it, your web site should change to orange!

```html
<!doctype html>
<html>
 <head>
  <title>
   First Test Page
  </title>
  <meta charset="utf-8">
  <style>
   body {
    background-color: orange;
   }
   h1 {
    color: green;
   }
   p {
    font-family: Arial;
    font-size: 20px;
   }
  </style>
 </head>
 <body>
  <h1>
   Welcome to My Web Page
  </h1>
  <p>
   This is my first web page.
  </p>
 </body>
</html>
```

- 5. Change your style to the colors and fonts that you chose and watch your web site start to come to life.

- 6. Incredible! You are already making such good progress. Next, make sure you understand where your other sections are. Turn the header and footer into your **secondary color** from your style guide. In this book, the secondary color is blue.

```html
<!doctype html>
<html>
 <head>
  <title>
   First Test Page
  </title>
  <meta charset="utf-8">
  <style>
   body {
    background-color: orange;
   }
   header {
    background-color: blue;
   }
   h1 {
    color: green;
   }
   p {
    font-family: Arial;
    font-size: 20px;
   }
  </style>
 </head>
 <body>
  <header>
   Welcome to My Web Page
  </header>
  <p>
   This is my first web page.
  </p>
 </body>
</html>
```

- 7. Next, you are going to turn your div sections into your **tertiary color**. In this book, the tertiary color is yellow.

In this book, the two divs are meant to be side by side. But your divs don’t have to be like that; they could be one on top of the other. For example, this book names the classes for the divs “left” and “right,” but you could name yours “top” and “bottom.”

You might notice that the left div, which has a background color of #ffffff (which is white) shows up, but the right div, which has a background color of #000000 (which is black), doesn’t. That’s because there is nothing in the right div!

- 9. Add some text in the right div (or the div that you haven’t filled in), and that second div will show up; in this example, it’s the black div.

![](img/b129720fc9ac9e14546b8756740d362a_81_0.png)

- 10. Be careful! Sometimes you have your text and background colors the same, which makes it look like there is nothing there! In this book, the problem is that you can’t see the text because the text and background are black. But never fear! There is a style attribute for text color, too.

Keep adding divs, fonts, and colors until your web site looks like the wireframe that you made in Project 3.

Wow! Your web site is starting to come together. Even though it might look a little silly right now, you actually have your structure built and you have some colors down!

## ADDING PICTURES TO YOUR WEB SITE

Now that you have everything in place, you can start adding a couple of pictures to your site.

- 1. Go to http://drive.google.com and double-click **your project folder**. The one in this book is called MyDinoSite.
- 2. Click **New** and **File Upload** so that you can upload your first image to your Google Drive folder.

![](img/b129720fc9ac9e14546b8756740d362a_83_0.png)

- 6. Right-click the image and then click **Share**.

![](img/b129720fc9ac9e14546b8756740d362a_85_0.png)

- 7. Click **Advanced**.

![](img/b129720fc9ac9e14546b8756740d362a_85_1.png)

- 8. Click **Change**.

![](img/b129720fc9ac9e14546b8756740d362a_86_0.png)

- 9. Choose **On - Public on the Web** and click **Save**.

![](img/b129720fc9ac9e14546b8756740d362a_86_1.png)

- **10 Click Done.**

![](img/b129720fc9ac9e14546b8756740d362a_87_0.png)

- **11 Double-click your image, and it should open in large size on your screen.**

![](img/b129720fc9ac9e14546b8756740d362a_87_1.png)

- 12 Click the three dots on the top right and click **Open in New Window**.

![](img/b129720fc9ac9e14546b8756740d362a_88_0.png)

- 13 Click the three dots again and click **Embed Item**.

![](img/b129720fc9ac9e14546b8756740d362a_88_1.png)
