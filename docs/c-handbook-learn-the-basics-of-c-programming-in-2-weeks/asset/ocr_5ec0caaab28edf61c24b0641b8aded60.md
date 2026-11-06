# Placing Your Code in the <body> </body> Area

In general, you should place a JavaScript code in the <body> section if you want it to produce content as the webpage loads. Here, you don’t have to define any function using JavaScript. Here’s an example:

```
<html>
<head>
</head>
<body>
<script type="text/javascript">
<!--
document.write("Hello World")
//-->
</script>
<p>This is web page body </p>
</body>
</html>
```

That code generates the following result:

```
Hello World
This is web page body
```