# Placing the Code in an External File

While using JavaScript, you’ll surely find many situations where you have to use the same codes on different webpages. Typing the same code repeatedly can be boring and time-consuming. Fortunately, you can simply save your JavaScript codes in an external file. Then, you just have to link that file to the webpages that need the identical codes.

In using this method, you should use a **script** tag and the **src** attribute. Check the example below:

```
```html
<html>
<head>
<script type="text/javascript" src="filename.js" ></script>
</head>
<body>
.......
</body>
</html>
```
```

This method requires you to write your JavaScript code inside a text file and save it using “.js” as the extension (e.g. example.js).

Let’s try a simple exercise. Copy the code below into a text file and save it as “filename.js”. Then, utilize the **sayHello** function of your HTML document after adding the filename.js file.

```
```javascript
function sayHello() {
    alert("Hello World")
}
```
```