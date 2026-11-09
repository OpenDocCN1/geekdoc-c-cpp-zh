
```html
<html>
<head><title>JavaScript Lesson 5 - Arrays</title></head>
<body>
<link rel="stylesheet" href="samplestyle.css" />

<button onclick="createarray()">Print Array</button>

<script>
function createarray()
{
  document.write('<link rel="stylesheet" type="text/css" href="samplestyle.css" />');
  document.write('<br>');
  var nm = ["Jim","Tim","Kim","Bim","Sam"];
  var age=[7,56,40,34,56];
  var state=["Florida","California","Georgia","Illinois","Nevada"];
  document.write(nm[0]+' lives in '+state[0]+' state and age is '+age[0]+'<br>');
  document.write(nm[1]+' lives in '+state[1]+' state and age is '+age[1]+'<br>');
  document.write(nm[2]+' lives in '+state[2]+' state and age is '+age[2]+'<br>');
  document.write(nm[3]+' lives in '+state[3]+' state and age is '+age[3]+'<br>');
  document.write(nm[4]+' lives in '+state[4]+' state and age is '+age[4]+'<br>');
  nm.push("Y");// Adding another index to the array
  age.push(20);
  state.push("California");
  document.write(nm[5]+' lives in '+state[5]+' state and age is '+age[5]+'<br>');
}
</script>
</body>
</html>
```

### Output

![](img/443990a0ec620659ce8be783c0758bc6_333_0.png)

On clicking **Print Array**, we get...

## Example 2 – Assigning An Array Through A Form

In this example, we input name, age and state through a html form. In JavaScript, we assign the form elements to variables.

3 names, ages and state locations are entered via a form and entered into 3 arrays using **document.getElementById**.

The array is printed at the end using **document.write()**.

```html
<html>
<head><title>JavaScript Lesson 5 - Arrays</title></head>
<body>
<link rel="stylesheet" href="samplestyle.css" />
Enter Name1 <input name="name" type="text" id="name0" size="20"><br>
Enter Age1 <input name="age" type="number" id="age0" size="20"><br>
Enter State1 <input name="state" type="text" id="state0" size="20"><br>

Enter Name2 <input name="name" type="text" id="name1" size="20"><br>
Enter Age2 <input name="age" type="number" id="age1" size="20"><br>
Enter State2 <input name="state" type="text" id="state1" size="20"><br>

Enter Name3 <input name="name" type="text" id="name2" size="20"><br>
Enter Age3 <input name="age" type="number" id="age2" size="20"><br>
Enter State3 <input name="state" type="text" id="state2" size="20"><br>
<button onclick="createarray()">Start Program</button>

<script>
function createarray()
{
var nm=[];
var age=[];
var state=[];

nm[0]=document.getElementById("name0").value;
age[0]=document.getElementById("age0").value;
state[0]=document.getElementById("state0").value;
nm[1]=document.getElementById("name1").value;
age[1]=document.getElementById("age1").value;
state[1]=document.getElementById("state1").value;
nm[2]=document.getElementById("name2").value;
age[2]=document.getElementById("age2").value;
state[2]=document.getElementById("state2").value;

document.write('<link rel="stylesheet" type="text/css" href="samplestyle.css" />');
document.write('<br>');
document.write(nm[0] + " is " +age[0]+ " years old and lives in " +state[0]+"<br>");
document.write(nm[1] + " is " +age[1]+ " years old and lives in " +state[1]+"<br>");
document.write(nm[2] + " is " +age[2]+ " years old and lives in " +state[2]+"<br>");
}
</script>
```

### Output

- Enter Name1: Mather
- Enter Age1: 35
- Enter State1: Illinois
- Enter Name2: Timmy
- Enter Age2: 23
- Enter State2: Georgia
- Enter Name3: Mahama
- Enter Age3: 67
- Enter State3: California
- Start Program

On Clicking **Start Program**, we get:

Mather Is 35 Years Old And Lives In Illinois

Timmy Is 23 Years Old And Lives In Georgia

Mahama Is 67 Years Old And Lives In California

## Example 3 – Guess World Capitals

In this program, we code a quiz that asks the user the capital of a random country around the world, and checks if the answer is correct.

In the program, the one button runs the **worldquiz()** function. In the function, we declare two arrays. One array contains all the countries around the world; and the other contains all the capitals.

You can get the values for these arrays below:

[https://drive.google.com/file/d/1VBnrlk290oVmh3Vn8Jv2EgFBL1w8vSd/view?usp=sharing](https://drive.google.com/file/d/1VBnrlk290oVmh3Vn8Jv2EgFBL1w8vSd/view?usp=sharing)

We then choose a random number between 0 and x, x being the length of the array. This random number picks a random country from the array. We do this using **Math.random()** and **Math.floor()**.

We take in a user guess for the capital using **prompt**. We compare the user guess to the actual capital. Then, we send the user a message telling them they’re correct or wrong (with the correct capital if they’re wrong).

Then, the user has the chance to restart the program with the **Home** button that runs the **redirect()** function. The redirect function runs ‘**GuessWorldCapitals.html**’ which is the name of the file. The code and the outputs are shown below.

```html
<html>
<head><title>Guess World Capitals</title>
<link rel="stylesheet" href="styles.css" />
</head>
<body>
<button class="btn a" onclick="worldquiz()">Start Quiz</button>
<script>
function worldquiz()
{
var countries = ["Afghanistan","Albania","Algeria","Andorra","Angola","Antigua and Barbuda","Argentina","Armenia",
var capitals = ["Kabul","Tirana (Tirane)","Algiers","Andorra la Vella","Luanda","Saint John's","Buenos Aires","Yer
var randomcountrynumber = Math.floor(Math.random() * countries.length);
var chosencountry = countries[randomcountrynumber];
var chosencapital = capitals[randomcountrynumber];
var guess = prompt("What is the capital of "+chosencountry+" ?");
if (guess.toUpperCase()==chosencapital.toUpperCase())
{
    document.write("<p>Congratulations. You are correct.</p>");
}
else
{
    document.write("<p>Wrong. The capital is "+chosencapital+"</p>");
}
document.write('<link rel="stylesheet" type="text/css" href="styles.css" />');
document.write('<br>');
document.write('<button onclick="redirect()">Home</button>');
}
function redirect()
{
window.location.replace("GuessWorldCapitals.html");
}
</script>
</body>
</html>
```

### Output #1

![](img/443990a0ec620659ce8be783c0758bc6_338_0.png)

Click Start Quiz

![](img/443990a0ec620659ce8be783c0758bc6_339_0.png)

![](img/443990a0ec620659ce8be783c0758bc6_339_1.png)

### Output #2

![](img/443990a0ec620659ce8be783c0758bc6_339_2.png)

Wrong. The Capital Is Addis Ababa

[Home]

## Example 4 – Random Jokes

This program prints a random joke picked from a list of jokes. The one button runs the **writejoke()** function. In the function, we declare an array that contains all the jokes. You can get the values for all below:

[https://drive.google.com/file/d/1xDN9dt2Gvj-mdPmi5ATCnP1tv0ZtZ5/view?usp=sharing](https://drive.google.com/file/d/1xDN9dt2Gvj-mdPmi5ATCnP1tv0ZtZ5/view?usp=sharing)

We then choose a random number between 0 and x, x is the length of the array. This random number picks a random joke. We do this using **Math.random()** and **Math.floor()**.

We then print out the joke using the **document.write()** function.

Then, the user has the chance to restart the program with the **Home** button that runs the **redirect()** function.

```html
<html>
<head><title>Random Duck Joke</title>
<link rel="stylesheet" href="samplestyle.css" />
</head>
<body>
<button class="btn a" onclick="writejoke()">Get A Duck Joke</button>
<script>
var duckjokes = [
"Why did the duck cross the road? It was the chicken's day off",
"Why did the duck detective get promoted? He quacked the case",
"Why did the tiger cross the road? To eat the duck and then her",
"What did the duck do when he saw the clown? He started quacking up",
"Why is the duck always standing straight? To hide his butt-quack",
"Which is the heaviest bird? The crane",
"Why did the duck go to prison? He became a quackpot.",
"Why did the bee do his own haircuts? He did buzzcuts",
"Why did the duck lose the race? Because he was a lame duck",
"What happened after the duck got injured? He went to a ducktor!",
"Where did the duck eat breakfast? Quacker barrel",
"Why did the hen keep its nest warm? Because it was eggstremely cold outside",
"Why did the duck not like the soup? Because it had no quackers!",
"Why were the two ducks always together? They were stuck together with duck-tape",
"Why do swans avoid the stock market? Because they're afraid of the black-swan",
"How do ducks know if it's about to rain? Because they checked the feather-forecast",
"What did the duck do on July 4th? It burst quackers",
]
function writejoke()
{
var chosenjoke = duckjokes[Math.floor(Math.random() * duckjokes.length)];

document.write(chosenjoke);
document.write('<link rel="stylesheet" type="text/css" href="samplestyle.css" />');
document.write('<br>');
document.write('<button onclick="redirect()">Home</button>');
}
function redirect()
{
window.location.replace("RandomJoke.html");
}
</script>
</body>
</html>
```
