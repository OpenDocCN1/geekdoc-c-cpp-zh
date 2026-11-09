```
```html
<html>
<head><title>Game Score Keeper</title></head>
<link rel="stylesheet" href="samplestyle.css" />
<body>
<button class="btn" onclick="dicegame()">Start Playing</button>

<script>
var gameplayers={"Adam": 0,"Bob":7,"Carol":0,"Steve":4,"Mark":2,"Tim":0};

function dicegame()
{

for (i=0;i<10;i++)
{
gamecalc();
}
document.write("<br>");
document.write("Adam scored "+gameplayers["Adam"] + points.<br>");
document.write("Bob scored "+gameplayers["Bob"] + points.<br>");
document.write("Carol scored "+gameplayers["Carol"] + points.<br>");
document.write("Steve scored "+gameplayers["Steve"] + points.<br>");
document.write("Mark scored "+gameplayers["Mark"] + points.<br>");
document.write("Tim scored "+gameplayers["Tim"] + points.<br>");


document.write('<link rel="stylesheet" type="text/css" href="samplestyle.css" />');
document.write('<br>');

document.write('<button class="btn a" onclick="dicegame()">Check</button><br>');

}
```
```