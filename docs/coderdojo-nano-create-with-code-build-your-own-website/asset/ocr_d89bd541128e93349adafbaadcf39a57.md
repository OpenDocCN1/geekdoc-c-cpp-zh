# # &lt;JAVASCRIPT&gt;

![](bbox=[0.65, 0.06, 0.99, 0.24])

When you're developing your website, sooner or later you'll encounter **JavaScript**. **JavaScript** is a programming language that lets you add all kinds of special effects and features to your pages. Things like games, charts, and animations. We don't have enough space in this book to show you all the things that **JavaScript** can do, but here is an example to give you an idea of the sort of things you can do. We'll use a simple function that swaps one image for another.

The JavaScript behind the image swapper is embedded inside a page. It's called embedded because the actual JavaScript is in the body of the page inside the **script** element. (You can also put the JavaScript into a separate file if you like. See scholastic.com/coder-dojo/javascript for more information about this and about JavaScript in general.)

```
    <!DOCTYPE HTML>
    <html>
    <head>
    <link type="text/css" rel="stylesheet" href="css/full-style.css"/>
    </head>
    <body>
    <p>
    <img id="display-image" onclick="swapImage()" src="images/01.png" width="180"
    height="180"/>
    </p>
    <p>Click the image to change it!</p>
    <script>
    function swapImage() {
    var imageDisplayed = document.getElementById('display-image');
    if (imageDisplayed.src.match("images/01.png")) {
    imageDisplayed.src = "images/02.png";
    }
    else {
    imageDisplayed.src = "images/01.png";
    }
    }
    </script>
    </body>
    </html>
```

If we look at the code above we can see that the **img** element has an attribute named **onclick** with a value of **swapImage()**.