first declare an array that contains all the animals. Then, we pick a random animal using Math.random() and Math.floor().
We create a variable that stores the answer (**answerArray**). It stores the user answer. It is initialized to underscores (_) with the same length as the original animal.
The variable **remletters** is the number of remaining letters to be guessed. A while loop is created to accept user guesses as long as **remletters>0**.
Using prompt, we accept a single letter input from the user. If there is more than one letter input, we set an error message and ask the user to enter only one letter. Once the user enters a letter, we enter a loop that checks each letter of the random animal against the user letter. Each time there is a match, we subtract **remletters** by 1 and update the relevant part of **answerArray** with the matched letters. At the end of the while loop, the user has guessed the animal, and we print out a congratulatory note with the name of the animal.
At any point within the while loop, if the user doesn’t enter a letter and tries to proceed, we exit the program loop and print out the animal name.
At the end of the game, the user has the option to restart the program using the **Home** button. Here’s the code below with some examples.

```
```html
<html>
<head>
  <title>Animal Hangman</title>
  <link rel="stylesheet" href="samplestyle.css" />
</head>
<body>
<button class="btn" onclick="animalhangman()">Start Animal Hangman</button>

<script>
function animalhangman()
{
    // Create an array of animals
    var animals = [
      "tiger",
      "lion",
      "monkey",
      "kangaroo",
      "racoon",
      "flamingo",
      "elephant",
      "porcupine"
    ];
    var chosenanimal = animals[Math.floor(Math.random() * animals.length)];
    var answerArray = [];
    for (var i = 0; i < chosenanimal.length; i++)
      answerArray[i] = "_";
}
```
```