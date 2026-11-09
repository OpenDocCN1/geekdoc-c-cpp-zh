
### Output #1

Enter Name of Gym: First Fitness
Enter Gym Distance from home: 6
Enter Monthly Membership Costs: 40
Check Gym

First Fitness does not work for me

### Output #2

Enter Name of Gym: Anytime Fitness
Enter Gym Distance from home: 4
Enter Monthly Membership Costs: 50
Check Gym

Anytime Fitness is a possible gym

### Output #3

![](img/443990a0ec620659ce8be783c0758bc6_297_0.png)

![](img/443990a0ec620659ce8be783c0758bc6_297_1.png)

## FOR LOOP Example 1

A simple example of a For Loop is a program that counts to 10.

```html
<html>
<head><title>Loops.....</title></head>
<body>

<button onclick="printtoten()">Print To 10</button>

<script>

function printtoten()
{
    for (i=1;i<=10;i++)
    {
        document.write(i+"<br>");
    }
}

</script>

</body>
</html>
```

The above code is a simple example of a for loop. It has a button that runs the function printtoten(). Printtoten() has a for loop that prints numbers 1 to 10 on the screen through document.write().

`for (i=1;i<=10; i++)`

The line above means that the loop starts from 1 (i=1). It is increasing by 1 each time (i++). The loop ends when i reaches 10 (i<=10).

### Output

Once you click the button on the output, you see the numbers 1 to 10 printed on the screen.

![](img/443990a0ec620659ce8be783c0758bc6_298_0.png)

![](img/443990a0ec620659ce8be783c0758bc6_299_0.png)

## FOR LOOP Example 2

Now, let’s do a slightly different version of this. In this example, we’re going to use a form that takes in a number for the loop. That means we can make the loop as long as we want.

```html
<html>
<head><title>Loops........</title></head>
<body>

<form id="form1">
How long do you want the loop?: <input name="Loop Number" type="number" id="loop" size="20"><br>

</form>

<button onclick="printto(10)">Print To 10</button>
<button onclick="printlooplength()">Print Loop Length</button>

<script>

function printto()
{

for (i=1;i<=10;i++)
{
    document.write(i+"<br>");
}
}
function printlooplength()
{
var looplength=parseInt(document.getElementById("loop").value);

for (i=1;i<=looplength;i++)
{
    document.write(i+"<br>");
}
}
</script>

</body>
</html>
```

A html form was added to this program

The form takes in a number input and stores in a variable called **“loop”**.

There is a second button labelled **“Print Loop Length”** which runs the **“printlooplength()”** function.

In the function, we assign the form variable **“loop”** to another variable **“looplength”**. And we run the loop from 1 to **“looplength”**. The loop prints the numbers between 1 and **“looplength”**.

In the example below, we put 35 in the form; and as we can see, it prints out numbers between 1 and 35.

![](img/443990a0ec620659ce8be783c0758bc6_300_0.png)

```text
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
```

## FOR Loop Example 3 – Nested Loops

In the final example, we use FOR loops to create a star pattern. So, we create a 2<sup>nd</sup> button labelled ‘Print Star Loop’ which runs **starloop()** on clicking. In the function, again, looplength has the value of the loop we enter in the form. So, first, we create a FOR loop that goes from 1 to looplength. The variable i holds the count value of the loop and increases by 1 each time. Then, we create another FOR loop within that goes from 1 to i. The second FOR loop prints the star(“*”) i times. So, for example, if you’re going through the first loop for the 5<sup>th</sup> time, i=5. The second loop prints * from 1 to 5 (i.e. 5 times). In the example, below, we print the star loop for a looplength of 23.

### Output

```html
<html>
<head><title>Loops........</title></head>
<body>
<form id="form1">
Loop Number: <input name="Loop Number" type="number" id="loop" size="20"><br>
</form>
<button class="btn printoten" onclick="printtoten()">Print To 10</button>
<button class="btn printoten" onclick="printlooplength()">Print Loop Length</button>
<button class="btn printoten" onclick="starloop()">Print Star Loop</button>
<script>

function printtoten()
{
for (i=1;i<=10;i++)
{
    document.write(i+"<br>");
}
}
function printlooplength()
{
var looplength=parseInt(document.getElementById("loop").value);

for (i=1;i<=looplength;i++)
{
    document.write(i+"<br>");
}
}
function starloop()
{
var looplength=parseInt(document.getElementById("loop").value);

for (i=1;i<=looplength;i++)
{
    for (j=1;j<=i;j++)
    {
        document.write("*");
    }
    document.write("<br>");
}
}
</script>
</body>
</html>
```

![](img/443990a0ec620659ce8be783c0758bc6_303_0.png)

```text
*
**
***
****
*****
******
*******
********
*********
**********
***********
************
*************
**************
***************
****************
*****************
******************
*******************
********************
*********************
**********************
***********************
```

## WHILE LOOP EXAMPLE 1

A while loop runs while a certain condition is met. If the condition is no longer met, it breaks out of the loop. In the below example, the program executes a while loop that takes in a user input via the prompt function. The while loop keeps running and printing the user text. The loop stops when the user inputs the word ‘STOP’. Once the word is input, that’s the end of the while loops and the program stops.

```html
<html>
<head><title>While Loop Test</title></head>
<body>

<button onclick="testwhileloop()">Test</button>

<script>
function testwhileloop()
{
var inputtext = ""
while (inputtext != "STOP")
{
    inputtext = prompt("Enter what you want to do now (Enter in ALL CAPS)");
    document.write("Next Activity = "+inputtext+"<br>");
}
}
</script>

</body>
</html>
```

Here’s the output below that shows how this works.

### Output

![](img/443990a0ec620659ce8be783c0758bc6_306_0.png)

![](img/443990a0ec620659ce8be783c0758bc6_306_1.png)

![](img/443990a0ec620659ce8be783c0758bc6_306_2.png)

## Practice Problems

and adds to the candidate vote total. There is a final prompt that asks if there are any more votes and it accepts the values of ‘Y/N’. If ‘N’, then it stops the program and prints out the winner. If ‘Y’, then it asks for the vote again and repeats the process.

- 7. Write a program that takes a user input and outputs the following star pattern below. For example, if the user inputs the number ‘6’ it outputs:

```text
******
*****
****
***
**
*
```

- 8. Write a program that takes in a user input and prints out the sum of numbers from 1 to that number. For example, if the user inputs 3; the sum is 1+2+3=6.

## Game Time - Loops

Now, it’s time to design a few games based on what we’ve learned so far. There’s no better way of learning concepts than applying them; and even better to apply them to something fun. Before getting started, let’s talk about one concept; which is adding html elements using JavaScript.

### Adding html Elements using JavaScript

What if we want to add a button or textbox in the middle of the JavaScript program? Yes, you can do that within JavaScript using the document.write() function. For example, you can create a button using:

```javascript
document.write('<button onClick="afunction()">Restart</button>');
```

In the above line, we create a button with text ‘Restart’ on it. On clicking the button, afunction() is run. This is very useful in games where we have the option to keep running the program instead of stopping. Now, let’s look at a similar program below.

```html
<html>
<head><title>Sample Form</title></head>
<body>
<link rel='stylesheet' type='text/css' href='samplestyle.css' />
<form id='form1'>
Enter First Number:<input name='number1' type='number' id='num1' size='20'><br>
Enter Second Number:<input name='number2' type='number' id='num2' size='20'><br>
Enter Third Number: <input name='number3' type='number' id='num3' size='20'><br><br>
</form>

<button class = "btn submit" onclick="multiplynum()">Submit</button>

<script>
function multiplynum()
{
var n1 = document.getElementById('num1').value;
var n2 = document.getElementById('num2').value;
var n3 = document.getElementById('num3').value;
document.write('<link rel="stylesheet" type="text/css" href="samplestyle.css" />');
document.write('<br>');
document.write('<button onClick="redirect()">Home</button>');
}

function redirect()
{
window.location.replace("form_JavaScript.html");
}
</script>

</body>
</html>
```
