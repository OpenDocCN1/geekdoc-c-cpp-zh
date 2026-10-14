# THE BASICS OF INCLUDING JAVASCRIPT

Although you can add more advanced features with JavaScript, its support among mobile devices is spotty at best, and you should test it thoroughly before deploying the site to patrons.

JavaScript is a scripting language that works on any computer. It is included in the HTML of a page and allows browsers to perform a variety of functions. The code appears in the following format:

```
<script type="text/javascript">
document.write('Your message here!'); </script>
```

In the context of a full page, the script would be expressed in the following way:

```
<html>
<head>
</head>
<body>
<script type="text/javascript">
document.write('Your message here!');
</script>
<noscript>
```

Your browser either does not support JavaScript, or you have JavaScript turned off.

```
</noscript>
</body>
</html>
```

This script would tell the browser to write “Your message here!” on the page in the position determined by the script’s location in the HTML. You can specify the font and other attributes of the text, just as you can for any other element on an HTML page. JavaScript can get very complex, though, and some large scripts constitute large parts of the content of some web pages.

In the event that the visitor’s browser doesn’t support JavaScript, the site visitor would receive the message “Your browser either does not support JavaScript, or you have JavaScript turned off.”

Some scripts are contained in the header of the HTML document and are called at the point in the body where their output is desired by a second code. These scripts can perform functions such as displaying dynamic information, providing messages based on user actions, or date and time. They can also be used to process some types of information and to perform simple functions. JavaScript can be custom coded, but even