# Placing Your Code in the <head> </head> and <body> </body> Areas of the Document

You also have the option to place your JavaScript code in both the <head> and <body> areas of the HTML file. Analyze the following example:

```
<html>
<head>
<script type="text/javascript">
<!--
function sayHello() {
  alert("Hello World")
}
//-->
</script>
</head>
<body>
<script type="text/javascript">
<!--
document.write("Hello World")
//-->
</script>
<input type="button" onclick="sayHello()" value="Say Hello" />
</body>
</html>
```

If you entered the code properly, opening the HTML file will give you this:

![](bbox=[0.06, 0.52, 0.23, 0.62])