
### 5. Create a box for the interface

Now that you’ve planned what the interface will look like, you can create the rectangular boxes that will make up the GUI. Type this code below what you typed in Step 2 to create a box for the main question.

```python
WIDTH = 1280
HEIGHT = 720

main_box = Rect(0, 0, 820, 240)
```

This function takes four parameters. The first two numbers are the coordinates of the top-left corner of the box, and the last two numbers are the coordinates of the bottom-right corner of the box.

This sets the box size to 820 pixels wide and 240 pixels high.

### 6. Make the other boxes

You now need to make a box for the timer and four separate boxes for each of the answer boxes. Type the code under what you wrote in Step 5.

```python
main_box = Rect(0, 0, 820, 240)
timer_box = Rect(0, 0, 240, 240)
answer_box1 = Rect(0, 0, 495, 165)
answer_box2 = Rect(0, 0, 495, 165)
answer_box3 = Rect(0, 0, 495, 165)
answer_box4 = Rect(0, 0, 495, 165)
```

The timer box is a square 240 pixels wide and 240 pixels high.

All the answer boxes are the same size.

### 7. Move the boxes

At the moment, all the boxes will be drawn on top of each other in the top-left corner. You need to add some code to move them to their correct positions on the screen. Type this code immediately after the code from Step 6.

```python
answer_box4 = Rect(0, 0, 495, 165)

main_box.move_ip(50, 40)
timer_box.move_ip(990, 40)
answer_box1.move_ip(50, 358)
answer_box2.move_ip(735, 358)
answer_box3.move_ip(50, 538)
answer_box4.move_ip(735, 538)
```

> Arr! Time to move all these boxes into place!

move_ip() moves each rectangle to the place you want it on the screen.

The top-left corner of each box will be placed at the coordinates in the brackets.

![](img/3188b147f991a51de14dcd2bb4b4c42e_106_0.png)

### 8. Create a list of answer boxes

This game uses four boxes to show the possible answers to each question. You can keep track of these boxes by using a list. Add this code immediately after what you typed in Step 7.

```python
answer_box4.move_ip(735, 538)
answer_boxes = [answer_box1, answer_box2, answer_box3, answer_box4]
```

> This list holds all the answer boxes.

### 9. Draw the boxes

Now that you've created the boxes, it's time to add some code to draw them on the screen. Replace pass under def draw() from Step 3 with this code.

```python
def draw():
    screen.fill("dim gray")
    screen.draw.filled_rect(main_box, "sky blue")
    screen.draw.filled_rect(timer_box, "sky blue")

    for box in answer_boxes:
        screen.draw.filled_rect(box, "orange")
```

> This sets the background to a dim gray color.

> These lines draw the main box and the timer on the screen and colors them sky blue.

> This draws every box in the answer_boxes list on the screen and colors them all orange.

### 10. Try it out

Save your file and run it from the command line in the Command Prompt or Terminal window. You should be able to see your GUI, ready to be filled with quiz questions. If your program fails to run successfully, go back to your code and try to catch those bugs!

![](img/3188b147f991a51de14dcd2bb4b4c42e_107_0.png)

> I'm not sure how to run the game! Better check pages 24-25 for help.

![](img/3188b147f991a51de14dcd2bb4b4c42e_107_1.png)

### 11. Set the score

Now that the interface is ready, you need to start thinking about how the game will work. Create a variable to hold the score and set it to zero. Type this after the code you wrote in Step 8.

```python
answer_boxes = [answer_box1, answer_box2, answer_box3, answer_box4]

score = 0
```

![](img/3188b147f991a51de14dcd2bb4b4c42e_108_0.png)

### 12. Set the timer

You also need to create a timer that will hold the number of seconds the player has left to answer each question. You can give them ten seconds to answer by setting the variable to 10.

```python
score = 0
time_left = 10
```

This is the number of seconds the player has left to answer each question.

### 13. Add the first question

It's time to create the first quiz question. All the questions will be multiple choice, which means there are several possible answers, but only one of them is correct. You can use a list to store the information about each question. Type this code next.

This is the name of the list. Here it means question 1.

This is the question, the first item in the list.

```python
q1 = ["What is the capital of France?",
      "London", "Paris", "Berlin", "Tokyo", 2]
```

These are all the possible answers to the question.

This number indicates the position of the correct answer. Here it's 2, which means Paris is the correct answer.

### 14. More questions

Let's add some more questions by typing the code shown in black below the lines from Step 13. Remember, you can create your own set of questions if you like. You could base them on your favorite sports team, or show off what you know about your favorite series of books.

```python
q2 = ["What is 5+7?",
      "12", "10", "14", "8", 1]

q3 = ["What is the seventh month of the year?",
      "April", "May", "June", "July", 4]

q4 = ["Which planet is closest to the Sun?",
      "Saturn", "Neptune", "Mercury", "Venus", 3]

q5 = ["Where are the pyramids?",
      "India", "Egypt", "Morocco", "Canada", 2]
```

![](img/3188b147f991a51de14dcd2bb4b4c42e_108_1.png)

### 15. Create a list for the questions

Next you need to add some code to keep the questions in order. You can do this using a list, just like you did for the answer boxes in Step 8. Add this line under the code from Step 14.

```python
q5 = ["Where are the pyramids?",
      "India", "Egypt", "Morocco", "Canada", 2]
```

```python
questions = [q1, q2, q3, q4, q5]
```

This lists all the questions.

### 16. Add a function

In a real-life quiz, the quizmaster begins by picking up the first question from the top of a list. In Python, you can do the same thing by using the pop() function. This function removes the first item from the list, which makes the second item move to the top of the list. So in your code, pop() will remove q1, and q2 will take its place. Type this code next.

```python
questions = [q1, q2, q3, q4, q5]
question = questions.pop(0)
```

This gets the first question from the questions list and stores it in a variable called question.

> **EXPERT TIPS**
>
> ### Pop the stack
>
> When you place items in a list, Python stacks them on top of each other. The first item in the list appears at the top of the stack. Using the pop() function removes an item from the top of the stack.

### 17. Display the boxes

Now you need to update the draw() function to display the questions and the timer on the screen. Use a for loop to draw the possible answers inside the answer boxes. Add this code to the draw() function under what you typed in Step 9.

```python
screen.draw.filled_rect(main_box, "sky blue")
screen.draw.filled_rect(timer_box, "sky blue")

for box in answer_boxes:
    screen.draw.filled_rect(box, "orange")

screen.draw.textbox(str(time_left), timer_box, color=("black"))
screen.draw.textbox(question[0], main_box, color=("black"))

index = 1
for box in answer_boxes:
    screen.draw.textbox(question[index], box, color=("black"))
    index = index + 1
```

This line displays the number of seconds remaining in the timer box.

This displays the question in the main box.

These lines draw each possible answer in an answer box.

### 18. Run the code again

Save your code and run it from the command line again. You should see the first question and its four possible answers. At the moment, you can’t click on any of the options, and the timer is also fixed at ten. You’ll add the code to do these things soon.

![](img/3188b147f991a51de14dcd2bb4b4c42e_110_0.png)

The first question is displayed on screen.

### 19. Set up the final screen

It’s time to think about how the game should end. Write some code that displays the final screen when the game ends. Replace `pass` under `def game_over()` from Step 3 with this code.

```python
def game_over():
    global question, time_left
    message = "Game over. You got %s questions correct" % str(score)
    question = [message, "", "", "", 5]
    time_left = 0
```

This creates a message that will show the player’s final score.

Since there’s no correct answer here, it’s set to 5, which isn’t on the list.

The final message is displayed instead of another question. This will set all possible answers to a dash because you don’t want the player to be able to answer.

This sets the time to zero when the game ends.
