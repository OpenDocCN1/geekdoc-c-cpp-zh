```
```html
<html>
<head><title>JavaScript Greetings......</title></head>
<body>
<form id="form1">
Loop Length: <input type="number" id="loop" size="20"><br>
</form>

<button onclick="printttowenty()">Print To 100</button>
<button onclick="printlooplength()">Print Loop Length</button>

<script>

function printttowenty()
{

for (i=1;i<=20;i++)
{
    document.write(i+"<br>");
}

}

function printlooplength()
{
var looplength=parseInt(document.getElementById("loop").value);

var j=1;
for (j=1;j<=looplength;j++)
{
    document.write(j+"<br>");
}
}

</script>

</body>
</html>
```
```

Now, after running the program, we get: