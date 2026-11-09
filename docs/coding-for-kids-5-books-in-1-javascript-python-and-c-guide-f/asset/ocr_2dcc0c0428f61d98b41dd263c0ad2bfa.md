```
```html
<html>
<head><title>Leap Year Check</title></head>
<body>
<form id="form1">
Enter Year: <input type="number" id="year" size="20"><br>

</form>
<button onclick="leapyear()">Leap Year?</button>

<script>

function leapyear()
{
var yr=parseInt(document.getElementById("year").value);
var leapyear=0;
    if ((yr%4)==0)//First loop that checks if the year is divisible by 4
    {
        lpyear=1;
        if((yr%100)==0)//Second loop that checks if the year is divisible by 4
        {
            lpyear=0;
            if(yr%400==0)//Third loop that checks if the year is divisible by 4
            {
                lpyear=1;
            }
        }
    }
if (lpyear==1)
{
    document.write(yr+" is a leap year");
}
else
{
    document.write(yr+" is not a leap year");
}
}
</script>
</html>
```
```