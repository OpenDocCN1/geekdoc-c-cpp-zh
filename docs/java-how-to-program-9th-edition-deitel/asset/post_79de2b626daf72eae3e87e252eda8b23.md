
## Good Programming Practice 6.2

Using enumeration constants (like Status.WON, Status.LOST and Status.CONTINUE) rather than literal values (such as 0, 1 and 2) makes programs easier to read and maintain.

## Logic of the main Method

Line 26 in main calls rollDice, which picks two random values from 1 to 6, displays the values of the first die, the second die and their sum, and returns the sum. Method main next enters the switch statement (lines 29–45), which uses the sumOfDice value from line 26 to determine whether the game has been won or lost, or should continue with another roll. The values that result in a win or loss on the first roll are declared as public static final int constants in lines 14–18. The identifier names use casino parlance for these sums. These constants, like enum constants, are declared by convention with all capital letters, to make them stand out in the program. Lines 31–34 determine whether the player won on the first roll with SEVEN (7) or YO_LEVEN (11). Lines 35–39 determine whether the player lost on the first roll with SNAKE_EYES (2), TREY (3), or BOX_CARS (12). After the first roll, if the game is not over, the default case (lines 40–44) sets gameStatus to Status.CONTINUE, saves sumOfDice in myPoint and displays the point.

If we’re still trying to “make our point” (i.e., the game is continuing from a prior roll), lines 48–58 execute. Line 50 rolls the dice again. If sumOfDice matches myPoint (line 53), line 54 sets gameStatus to Status.WON, then the loop terminates because the game is complete. If sumOfDice is SEVEN (line 56), line 57 sets gameStatus to Status.LOST, and the loop terminates because the game is complete. When the game completes, lines 61–64 display a message indicating whether the player won or lost, and the program terminates.

The program uses the various program-control mechanisms we’ve discussed. The Craps class uses two methods—main and rollDice (called twice from main)—and the switch, while, if...else and nested if control statements. Note also the use of multiple case labels in the switch statement to execute the same statements for sums of SEVEN and YO_LEVEN (lines 31–32) and for sums of SNAKE_EYES, TREY and BOX_CARS (lines 35–37).

## Why Some Constants Are Not Defined as enum Constants

You might be wondering why we declared the sums of the dice as public final static int constants rather than as enum constants. The reason is that the program must compare the int variable sumOfDice (line 26) to these constants to determine the outcome of each roll. Suppose we declared enum Sum containing constants (e.g., Sum.SNAKE_EYES) representing the five sums used in the game, then used these constants in the switch statement (lines 29–45). Doing so would prevent us from using sumOfDice as the switch statement’s controlling expression, because Java does not allow an int to be compared to an enumeration constant. To achieve the same functionality as the current program, we would have to use a variable currentSum of type Sum as the switch’s controlling expression. Unfortunately, Java does not provide an easy way to convert an int value to a particular enum constant. This could be done with a separate switch statement. Clearly this would be cumbersome and not improve the program’s readability (thus defeating the purpose of using an enum).

## 6.11 Scope of Declarations

You’ve seen declarations of various Java entities, such as classes, methods, variables and parameters. Declarations introduce names that can be used to refer to such Java entities. The scope of a declaration is the portion of the program that can refer to the declared entity by its name. Such an entity is said to be “in scope” for that portion of the program. This section introduces several important scope issues.

The basic scope rules are as follows:

- 1. The scope of a parameter declaration is the body of the method in which the declaration appears.
- 2. The scope of a local-variable declaration is from the point at which the declaration appears to the end of that block.
- 3. The scope of a local-variable declaration that appears in the initialization section of a for statement’s header is the body of the for statement and the other expressions in the header.
- 4. A method or field’s scope is the entire body of the class. This enables non-static methods of a class to use the fields and other methods of the class.

Any block may contain variable declarations. If a local variable or parameter in a method has the same name as a field of the class, the field is “hidden” until the block terminates execution—this is called shadowing. In Chapter 8, we discuss how to access shadowed fields.

## Error-Prevention Tip 6.3

Use different names for fields and local variables to help prevent subtle logic errors that occur when a method is called and a local variable of the method shadows a field in the class.

Figure 6.9 demonstrates scoping issues with fields and local variables. Line 7 declares and initializes the field x to 1. This field is shadowed (hidden) in any block (or method) that declares a local variable named x. Method main (lines 11–23) declares a local variable x (line 13) and initializes it to 5. This local variable’s value is output to show that the field x (whose value is 1) is shadowed in main. The program declares two other methods—useLocalVariable (lines 26–35) and useField (lines 38–45)—that each take no arguments and return no results. Method main calls each method twice (lines 17–20). Method useLocalVariable declares local variable x (line 28). When useLocalVariable is first called (line 17), it creates local variable x and initializes it to 25 (line 28), outputs the value of x (lines 30–31), increments x (line 32) and outputs the value of x again (lines 33–34). When useLocalVariable is called a second time (line 19), it recreates local variable x and reinitializes it to 25, so the output of each useLocalVariable call is identical.

Fig. 6.9 | Scope class demonstrates field and local variable scopes. (Part 1 of 2.)

```
// Fig. 6.9: Scope.java
// Scope class demonstrates field and local variable scopes.

public class Scope
{
    // field that is accessible to all methods of this class
    private static int x = 1;

// method main creates and initializes local variable x
// and calls methods useLocalVariable and useField
public static void main( String[] args )
{
    int x = 5; // method's local variable x shadows field x

    System.out.printf( "local x in main is %d\n", x );

    useLocalVariable(); // useLocalVariable has local x
    useField(); // useField uses class Scope's field x
    useLocalVariable(); // useLocalVariable reinitializes local x
    useField(); // class Scope's field x retains its value

    System.out.printf( "\nlocal x in main is %d\n", x );
} // end main

// create and initialize local variable x during each call
public static void useLocalVariable()
{
    int x = 25; // initialized each time useLocalVariable is called

    System.out.printf(
        "\nlocal x on entering method useLocalVariable is %d\n", x );
    ++x; // modifies this method's local variable x
    System.out.printf(
        "local x before exiting method useLocalVariable is %d\n", x );
} // end method useLocalVariable

// modify class Scope's field x during each call
public static void useField()
{
    System.out.printf(
        "\nfield x on entering method useField is %d\n", x );
    x *= 10; // modifies class Scope's field x
    System.out.printf(
        "field x before exiting method useField is %d\n", x );
} // end method useField
} // end class Scope
```

```
local x in main is 5

local x on entering method useLocalVariable is 25
local x before exiting method useLocalVariable is 26

field x on entering method useField is 1
field x before exiting method useField is 10

local x on entering method useLocalVariable is 25
local x before exiting method useLocalVariable is 26

field x on entering method useField is 10
field x before exiting method useField is 100

local x in main is 5
```

Fig. 6.9 | Scope class demonstrates field and local variable scopes. (Part 2 of 2.)
