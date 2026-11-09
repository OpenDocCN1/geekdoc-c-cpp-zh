# IF LOOP EXAMPLE 1

IF loops are also called conditionals. A conditional is a piece of code that checks if a certain condition has been fulfilled. For example, an insurance company might want to give you a lower rate if the combined ages of your two kids is higher than 15. So, you check for those condition. Let’s look at it using an IF loop below.

```
```html
<html>
<head><title>Insurance Test</title></head>
<body>
Enter Age of 1st Kid:<input name="a1" type="number" id="age1" size="20"><br>
Enter Age of 2nd Kid:<input name="a2" type="number" id="age2" size="20"><br><br>

<button onclick="checkinsuranceprice()">Check Price</button>

<script>
function checkinsuranceprice()
{
var incost=0;
var a1 = parseInt(document.getElementById("age1").value);
var a2 = parseInt(document.getElementById("age2").value);

//Check condition
if ((a1+a2)>15)
{
incost=incost+300;
}
else
{
incost=incost+600;
}
document.write("Your annual car insurance is $"+incost);
}
</script>

</body>
</html>
```
```

In the above a html form allows the user to enter two ages with ids: “age1” and “age2”. The JavaScript variables a1 and a2 store the values of the variables. The IF statement checks if the sum of the two is greater than 15. If it’s greater than 15, insurance cost is $300; otherwise it’s $600. Finally, we print out the value of the insurance. Here’s the output below.

# Output #1: