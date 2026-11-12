
- 5. In style.css, add a new style definition for any new classes that you create, like the content class.

![](img/b129720fc9ac9e14546b8756740d362a_116_0.png)

- 6. One trick to making sure your web site is always covering the entire screen and your footer is always at the bottom is to set the vertical height to your header, footer, and the main area (in this example, the content div). For this example, the height of the content style definition is 80%, the height of the header is 15%, and the height of the footer is 5%. This will make the header, footer, and content always fit on the screen, no matter what size the screen is.

## PROJECT 6 MAKE YOUR WEB SITE LOOK GREAT

```css
body {
    font-family: 'Open Sans', sans-serif;
    background-color: #ffffff;
    color: #ffffff;
}
header {
    background-color: #ff0000;
    height: 15%;
}
footer {
    background-color: #ff0000;
    color: #000000;
    text-align: center;
    height: 5%;
}
.left {
    width: 75%;
    float: left;
    background-color: #0000ff;
}
.right {
    width: 22%;
    float: left;
    background-color: #0000ff;
    color: #ffffff;
    margin-left: 10px;
}
.content {
    height: 60%;
}
```

- 7. After you have fixed the vertical sizing, try resizing your window to see the footer moving.

![](img/b129720fc9ac9e14546b8756740d362a_117_0.png)

![](img/b129720fc9ac9e14546b8756740d362a_119_0.png)

**Highlight all the code and press Ctrl+C if you're on Windows and ⌘+C if you're on Mac to copy it.**

### The CSS

```css
.button {
  border: 1px solid #d6d6d6;
  background: #ffffff;
  background: -webkit-gradient(linear, left top, left bottom, from(#f7f7f7), to(#e6e6e6));
  background: -webkit-linear-gradient(top, #f7f7f7, #e6e6e6);
  background: -moz-linear-gradient(top, #f7f7f7, #e6e6e6);
  background: -ms-linear-gradient(top, #f7f7f7, #e6e6e6);
  background: -o-linear-gradient(top, #f7f7f7, #e6e6e6);
  padding: 6px 13px;
  -webkit-border-radius: 4px;
  -moz-border-radius: 4px;
  border-radius: 4px;
  -webkit-box-shadow: rgba(0,0,0,0.1) 0 1px 0;
  -moz-box-shadow: rgba(0,0,0,0.1) 0 1px 0;
  box-shadow: rgba(0,0,0,0.1) 0 1px 0;
  color: white;
  font-size: 13px;
  font-family: 'Helvetica', Arial, sans-serif;
  text-decoration: none;
  vertical-align: middle;
}

.button:hover {
  border-top-color: #d3d3d3;
  background: #f2f2f2;
  color: #333;
}

.button:active {
  border-top-color: #d3d3d3;
  background: #f2f2f2;
}
```

Go to your style.css file and press Ctrl+V or ⌘+V to paste the code.

![](img/b129720fc9ac9e14546b8756740d362a_120_0.png)

- 5. Go to index.html and add class="button" to each of your a tags.

![](img/b129720fc9ac9e14546b8756740d362a_121_0.png)

- 6. Go to your other HTML files and add class="button" to the a tags.

```html
10 <a class="button" href="http://driv...">Book Home</a>
```

### CHANGE YOUR BACKGROUND

The background of your content area is just white. This section walks you through changing it to an image instead.

- 1. Go to your style.css file and add background-image: url("IMAGE_URL"); to your content style definition.

```css
29 .content {
30   height: 80%;
31   background-image: url("IMAGE_URL");}
```

- 2. If you want to use a dinosaur picture, you can go to http://www.thewecan.zone/website-building and click Dino.png. Otherwise, just find your own background image by searching on google.com. Remember to always ask permission from a parent first!

- 3. Copy the URL of the image you found from the address bar. Highlight the URL and press Ctrl+C if you're on Windows and ⌘+C if you're on Mac. If you decided to find your own image, you can right-click the image and press Copy Image Address instead of copying the URL from the address bar.

![](img/b129720fc9ac9e14546b8756740d362a_122_0.png)

- 4. Paste the URL where it says IMAGE_URL from Step 1.

![](img/b129720fc9ac9e14546b8756740d362a_122_1.png)

- 5. Add two more lines of code to your content style definition. `background-size: cover;` will make sure that the image fills the entire content area, and `background-position: center;` will make sure that the image is centered on your page.

![](img/b129720fc9ac9e14546b8756740d362a_122_2.png)

### ADD YOUR CONTENT

Here comes the fun part! Add all your content about your topic into all your pages! If you had left and right divs, as in this example, add text about your dinosaurs on the left, and media on the right!

### ADD CONTENT AND WIDGETS TO YOUR HOME PAGE

First, you can add some information about your favorite fact in your topic. In this example, it is about a triceratops. You can also add fun widgets, like YouTube videos, into your sidebar!

- 1. **Delete the placeholder text that says “Text about my topic right here” and write about your topic instead.**

```html
<div class="left">My favorite dinosaur is the Triceratops!
<br><br>
Go to http://www.kids-dinosaurs.com/dinosaurs-triceratops.html I found
some information about the triceratops.
<br><br>
They lived about 68 to 65 million years ago - in the cretaceous
period. This was at the same time as some really big meat eating
dinosaurs such as Tyrannosaurus rex, Albertosaurus and Spinosaurus.
<br><br>
<img class="logo" src="http://www.kids-dinosaurs.com/images/kids-dinosaurs-triceratops-facts.jpg.png/pagespeed.ic.c8bMQHqgXAw.webp" />
<br><br>
To defend itself against meat eaters (predators) it had two long
brow horns. These could grow to be at least 1 metre (3 feet) long.
Triceratops would have been able to cause a lot of damage to an
attacker!
<br><br>
It also had a third shorter horn at the end of its nose. This gives
it its dinosaur name, which means ‘three-horned face’.
</div>
```

![](img/b129720fc9ac9e14546b8756740d362a_123_0.png)

If you copy anything from a book or web site, or you got ideas from a book or web site, you should cite your source! That means you are giving credit to that web site or book so that people know that the person who made that web site or book are the ones who came up with that information.

![](img/b129720fc9ac9e14546b8756740d362a_123_1.png)

Go to http://www.w3schools.com/tags/ for a guide reference on all the different tags you can use. Notice that in the previous image, there is a new img tag. Try using that one to add more pictures!

- 2. Go to YouTube.com with an adult’s permission and find a video on your topic.

- 3. Click Share and then Embed. Copy the HTML code with the iframe tag in it by pressing Ctrl+C if you’re on Windows and ⌘+C if you’re on Mac.

![](img/b129720fc9ac9e14546b8756740d362a_124_0.png)

- 4. Go back to your index.html and delete the text “My right div.” Then paste the iframe tag in the right div by pressing Ctrl+V if you’re on Windows and ⌘+V if you’re on Mac.

```html
<div class="right">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/rk0RipISIU4" frameborder="0" allowfullscreen></iframe>
</div>
```

- 5. Change width="###" to max-width="100%" and change height="###" to height="auto".

```html
<div class="right">
  <iframe max-width="100%" height="auto" src="https://www.youtube.com/embed/rk0RipISIU4" frameborder="0" allowfullscreen></iframe>
</div>
```

### CHANGE YOUR FOOTER TEXT

Don't forget to make changes to the text in your footer! Make your footer say something fun, but remember – don’t put any information about you. Not even your name.

```html
<footer>
    This is my website about dinosaurs.
    <br>
    I learned how to build it from a book!
</footer>
```

### ADD CONTENT TO YOUR OTHER PAGES

You now have the skills to be able to add content to all your other pages! Try making more pages, and even try playing around with the style!

For more information about web site building, you can always check out the wecan.zone/website-building for updated content, videos, and more.

### SHARE WITH YOUR FRIENDS

The final thing to do is share your web site! You know how to see your own web site, but the URL is really long and complicated.

- 1. Highlight the URL in the address bar and press Ctrl+C if you're on Windows and ⌘+C if you're on Mac to copy it.

![](img/b129720fc9ac9e14546b8756740d362a_125_0.png)

- 2. Go to goo.gl. This is a web site that takes a long URL and gives it a shorter version that is easier to remember!

![](img/b129720fc9ac9e14546b8756740d362a_125_1.png)
