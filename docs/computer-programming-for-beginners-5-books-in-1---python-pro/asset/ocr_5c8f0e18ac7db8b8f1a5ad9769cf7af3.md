# Javascript Placement

JavaScript code is inserted anywhere in an HTML document. However, you want to insert JavaScript code in an HTML file like this:
The Script within `<head> </head>` part.
The Script within `<body> </body>` part.
The Script within `<body> </body>` and `<head> </head>` part.
Include external file Script in the `<head>...</head>` part.

JavaScript in `<head>...</head>` Section
In some cases, when you want the script to run on a special event, such as an action when a button clicked, place the script in the head section like this:

```
```html
<html>
<head>
<script type="text/JavaScript">
<!--
function sayHi() {
alert("Hello World")
}
//-->
</script>
</head>
<body>
Tap here for result
<input type="button" onclick="sayHi()" value="Say Hi" />
</body>
</html>
```
```

# JavaScript in `<body>...</body>` Section

Sometimes you want a script to run immediately and to create script on the content page, insert the script within the `<body>` section. This is what the code should look like:

```
```html
<html>
<head>
</head>
<body>
<script type="text/JavaScript">
<!--
document.write("Hello World")
//-->
</script>
```
```