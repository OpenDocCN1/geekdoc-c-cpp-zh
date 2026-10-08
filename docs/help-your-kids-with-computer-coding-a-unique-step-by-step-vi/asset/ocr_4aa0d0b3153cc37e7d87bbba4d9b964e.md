# Draw a flowchart

Coders often plan programs on paper, to help them write better code with fewer errors. One way to plan is to draw a flowchart—a diagram of the steps and decisions that the program needs to follow.

+   - This flowchart shows the plan for the Turtle controller function. It takes a letter ("do") and number ("val") and turns them into a turtle command. For example, "F" and "100" will be turned into the command forward(100). If the function doesn't recognize the letter, it reports an error to the user.

Each command has two variables: "do" (a string) tells the turtle what to do, and "val" (an integer, or whole number) tells the turtle how much or how far to do it

The function has to decide if the "do" value is a letter recognizes

If "do" isn't, the function runs through other letters it recognizes

# EXPERT TIPS

# Squares and diamonds

Flowcharts are made up of squares and diamonds. The squares contains actions that the program performs. The diamonds are points where it makes a decision.

![](bbox=[0.635, 0.315, 0.925, 0.425])

![](bbox=[0.395, 0.435, 0.735, 0.805])

# EXPERT TIPS

# Letter commands

The Turtle controller will use these letters to stand for different turtle commands:

+   - N = New drawing (reset)
U/D = Pen up/down
F = Forward
B = Backwards
R = Right turn
L = Left turn

> "do" isn't "R":
isis it "U"?

If "do" = F, the turtle moves forward

If "do" = R, the turtle turns right

Because "do" is "U", the command "penup() stops the turtle from drawing

If "do" isn't a letter the function recognizes, it reports an error

Once the command is finished you return to the main program

After any command is executed successfully, the program goes to the end of the function

report unknown command

return from function