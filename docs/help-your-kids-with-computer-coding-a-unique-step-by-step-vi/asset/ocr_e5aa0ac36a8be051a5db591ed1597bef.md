# Using JavaScript

JavaScript is great for creating mini programs that run inside HTML, bringing websites to life and allowing users to interact with them. Although it works like Python, JavaScript code is more concise and trickier to learn.

# Getting input

As with Python, you can use JavaScript to ask the user for information. JavaScript can do this with a pop-up box. The following program prompts the user to enter their name and responds with a greeting.

This line creates a pop-up box and stores the text the user into it

+   This script stores the user's name in a variable. Type the code into the IDLE code window and remember to save it with `index.html`.

The text in quotes appears in the box

```
<script>
var name = prompt("Please enter your name");
var greeting = "Hello " + name + "!";
document.write(greeting);
</script>
```

JavaScript lines always end with a semicolon

The `<script>` tag shows where the JavaScript ends

This line displays the greeting

+   Double-click the HTML file to launch a browser window. Enter your name in the box and click "OK" to see the greeting.

# EXPERT TIPS

# Type carefully

When working with JavaScript, be careful to check that you've typed out the code correctly. If there's an error, the browser will simply ignore the block of JavaScript and create a blank window, without any error saying what went wrong. If that happens, check the code again carefully.

A prompt box always has "OK" and "Cancel" buttons

| JavaScript |
| Please enter your name |
| Charlie |

The greeting appears in the browser window

![](bbox=[0.068, 0.803, 0.46, 0.932])

![](bbox=[0.633, 0.77, 0.932, 0.896])