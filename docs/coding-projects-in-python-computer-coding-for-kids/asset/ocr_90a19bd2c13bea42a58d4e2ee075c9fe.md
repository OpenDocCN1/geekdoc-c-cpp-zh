# # Putting it together

It's now time to build your quiz! First you'll create the questions and the numbers for checking the answers. Then you'll add the code that gives the player three attempts to answer each question.

![](bbox=[0.641, 0.066, 0.973, 0.344])

+   1. **Create a new file**  
+   Open IDLE. Under the File menu, select New File. Save the file as “animal_quiz.py”.

![](bbox=[0.407, 0.232, 0.674, 0.333])

+   2. **Create the score variable**  
+   Type in the code shown here to create a variable called `score` and set its starting value to 0.

```
```python
score = 0
```
```

You'll use this variable to keep track of the player's score.

+   3. **Introduce the game**  
+   Next, create a message to introduce the game to the player. This will be the first thing that the player sees on the screen.

```
```python
score = 0
print('Guess the Animal!')
```
```

This phrase will appear in the shell window.

+   4. **Run the code**  
+   Now try running the code. From the Run menu, choose Run Module. What happens next? You should see the welcome message in the shell window.

![](bbox=[0.407, 0.656, 0.675, 0.796])

![](bbox=[0.672, 0.592, 0.966, 0.824])

+   5. **Ask a question (user input)**  
+   The next line of code asks a question and waits for the player's response. The answer (the user input) is saved in the variable `guess1`. Run the code to make sure the question appears.

```
```python
print('Guess the Animal!')
guess1 = input('Which bear lives at the North Pole? ')
```
```

The variable `guess1` stores whatever the user types in.