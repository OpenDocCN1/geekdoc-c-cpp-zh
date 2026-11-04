we use the cast operator to convert the int value in sumOfDice to type DiceNames and compare it to each of the constants in DiceNames. Lines 35–36 determine whether the player won on the first roll with Seven (7) or YoLeven (11). Lines 39–41 determine whether the player lost on the first roll with SnakeEyes (2), Trey (3) or BoxCars (12). After the first roll, if the game is not over, the default case (lines 44–48) saves sumOfDice in myPoint (line 46) and displays the point (line 47).

# Additional Rolls of the Dice

If we're still trying to "make our point" (i.e., the game is continuing from a prior roll), the loop in lines 52–69 executes. Line 54 rolls the dice again. If sumOfDice matches myPoint in line 57, line 59 sets gameStatus to Status.Won, and the loop terminates because the game is complete. In line 64, we use the cast operator (int) to obtain the underlying value of DiceNames.Seven so that we can compare it to sumOfDice. If sumOfDice is equal to Seven (7), line 66 sets gameStatus to Status.Lost, and the loop terminates because the game is over. When the game completes, lines 72–79 display a message indicating whether the player won or lost, and the app terminates.

# Control Statements in the Craps Example

Note the use of the various program-control mechanisms we've discussed. The Craps class uses two methods—Main and RollDice (called twice from Main)—and the switch, while, if...else and nested if control statements. Also, notice that we use multiple case labels in the switch statement to execute the same statements for sums of Seven and YoLeven (lines 35–36) and for sums of SnakeEyes, Trey and BoxCars (lines 39–41).

# Code Snippets for Auto-Implemented Properties

Visual Studio has a feature called code snippets that allows you to insert predefined code templates into your source code. One such snippet enables you to easily create a switch statement with cases for all possible values for an enum type. Type switch in the C# code then press Tab twice. If you specify a variable of an enum type in the switch statement's expression and press Enter, a case for each enum constant will be generated automatically.

To get a list of all available code snippets, type Ctrl + k, Ctrl + x. This displays the Insert Snippet window in the code editor. You can navigate through the Visual C# snippet folders with the mouse to see the snippets. This feature also can be accessed by right clicking in the source code editor and selecting the Insert Snippet... menu item.

# 7.10 Scope of Declarations

You've seen declarations of C# entities, such as classes, methods, properties, variables and parameters. Declarations introduce names that can be used to refer to such C# entities. The scope of a declaration is the portion of the app that can refer to the declared entity by its unqualified name. Such an entity is said to be "in scope" for that portion of the app. This section introduces several important scope issues. The basic scope rules are as follows:

+   1. The scope of a parameter declaration is the body of the method in which the declaration appears.
+   2. The scope of a local-variable declaration is from the point at which the declaration appears to the end of the block containing the declaration.