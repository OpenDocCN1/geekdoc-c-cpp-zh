# Replacing Strings

Now, let’s say you have a long paragraph and you want to replace a particular word with another. You use the function .replace.
In the below example, we replace “Atlanta” with “Charleston”. Please remember that this works for only 1 instance of Atlanta.

We use a html form element called textarea. Textarea is a bigger form of textbox which can take multiple lines of text from the user. And then we write the modified sentence on the screen.

```
```html
<html>
<head><title>Replacing Strings</title></head>
<body>
<form id="form1">
What was your day like?: <textarea name="sentence" cols="20" rows="5" id="sentence"></textarea><br><br>
</form>
<button onclick="strreplace()">Fix Sentence</button>
<script>
function strreplace()
{
var daysdes=document.getElementById("sentence").value;
var daysdesmod=daysdes.replace("Atlanta","Charleston");
document.write(daysdesmod);
}
</script>
</body>
</html>
```
```

Now, let’s run the program.

![](bbox=[0.105, 0.648, 0.846, 0.777])

Once we click **Fix Sentence** button, we get:

I went to Charleston this summer for a long nice summer vacation.