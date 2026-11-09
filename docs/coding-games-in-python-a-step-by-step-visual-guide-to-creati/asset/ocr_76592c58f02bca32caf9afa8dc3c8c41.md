# Thinking caps on!

There may be a time limit to answer the questions, but not to build the game! Follow these steps carefully to build your own quiz show to play with your friends and family.

![](bbox=[0.536, 0.038, 0.963, 0.252])

+   1. **First steps**
+      Create a new folder called big-quiz in your python-games folder. Then open IDLE and create an empty file by going to the **File** menu and choosing **New File**. Select **Save As...** from the same menu and save the file as quiz.py in the big-quiz folder.

![](bbox=[0.502, 0.281, 0.957, 0.402])

+   2. **Set the screen size**
+      Next you need to define the size of the playing area. Add this code to the very top of your program to set the width and height of the game screen.

```
    WIDTH = 1280
    HEIGHT = 720
```

These values are in pixels.

+   3. **Create the stubs**
+      You don't need any images for this game, so you can jump straight into writing the code. First create placeholders for the functions you'll need to build the quiz.

```
    def draw():
        pass

    def game_over():
        pass

    def correct_answer():
        pass

    def on_mouse_down(pos):
        pass

    def update_time_left():
        pass
```

Remember, pass is used as a placeholder for functions that you don't want to define right away.

> > **Check page 144** to know more about placeholders.

![](bbox=[0.213, 0.866, 0.371, 0.966])